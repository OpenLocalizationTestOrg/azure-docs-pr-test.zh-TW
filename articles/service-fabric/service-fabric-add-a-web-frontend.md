---
title: "使用 ASP.NET Core 建立 Azure Service Fabric 應用程式的 Web 前端 | Microsoft Docs"
description: "使用 ASP.NET Core 專案，以及透過服務遠端進行的服務間通訊，對 Web 公開 Service Fabric 應用程式。"
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
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: b19aaa652f2c15573ded632ca1348e1a6752f080
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="build-a-web-service-front-end-for-your-application-using-aspnet-core"></a><span data-ttu-id="c67c2-103">使用 ASP.NET Core 建置應用程式的 Web 服務前端</span><span class="sxs-lookup"><span data-stu-id="c67c2-103">Build a web service front end for your application using ASP.NET Core</span></span>
<span data-ttu-id="c67c2-104">根據預設，Azure Service Fabric 服務不提供 Web 的公用介面。</span><span class="sxs-lookup"><span data-stu-id="c67c2-104">By default, Azure Service Fabric services do not provide a public interface to the web.</span></span> <span data-ttu-id="c67c2-105">若要對 HTTP 用戶端公開應用程式的功能，您必須建立 Web 專案來作為進入點，然後從該處與個別服務通訊。</span><span class="sxs-lookup"><span data-stu-id="c67c2-105">To expose your application's functionality to HTTP clients, you have to create a web project to act as an entry point and then communicate from there to your individual services.</span></span>

<span data-ttu-id="c67c2-106">在本教學課程中，我們從[在 Visual Studio 中建立第一個應用程式](service-fabric-create-your-first-application-in-visual-studio.md)教學課程中斷處來開始講起，並在具狀態計數器服務前面新增 ASP.NET Core 的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="c67c2-106">In this tutorial, we pick up where we left off in the [Creating your first application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md) tutorial and add an ASP.NET Core web service in front of the stateful counter service.</span></span> <span data-ttu-id="c67c2-107">如果您尚未這麼做，請返回並先逐步進行該教學課程。</span><span class="sxs-lookup"><span data-stu-id="c67c2-107">If you have not already done so, you should go back and step through that tutorial first.</span></span>

## <a name="set-up-your-environment-for-aspnet-core"></a><span data-ttu-id="c67c2-108">設定環境使其適用於 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="c67c2-108">Set up your environment for ASP.NET Core</span></span>

<span data-ttu-id="c67c2-109">您需要 Visual Studio 2017 才能完成本教學課程。</span><span class="sxs-lookup"><span data-stu-id="c67c2-109">You need Visual Studio 2017 to follow along with this tutorial.</span></span> <span data-ttu-id="c67c2-110">任何版本都可以。</span><span class="sxs-lookup"><span data-stu-id="c67c2-110">Any edition will do.</span></span> 

 - [<span data-ttu-id="c67c2-111">安裝 Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="c67c2-111">Install Visual Studio 2017</span></span>](https://www.visualstudio.com/)

<span data-ttu-id="c67c2-112">若要開發 ASP.NET Core Service Fabric 應用程式，您應該安裝下列工作負載：</span><span class="sxs-lookup"><span data-stu-id="c67c2-112">To develop ASP.NET Core Service Fabric applications, you should have the following workloads installed:</span></span>
 - <span data-ttu-id="c67c2-113">**Azure 開發** (在 [Web 和 Cloud] 之下)</span><span class="sxs-lookup"><span data-stu-id="c67c2-113">**Azure development** (under *Web & Cloud*)</span></span>
 - <span data-ttu-id="c67c2-114">**ASP.NET 與 Web 開發** (在 [Web 和 Cloud] 之下)</span><span class="sxs-lookup"><span data-stu-id="c67c2-114">**ASP.NET and web development** (under *Web & Cloud*)</span></span>
 - <span data-ttu-id="c67c2-115">**.NET Core 跨平台開發** (在 [其他工具集] 之下)</span><span class="sxs-lookup"><span data-stu-id="c67c2-115">**.NET Core cross-platform development** (under *Other Toolsets*)</span></span>

>[!Note] 
><span data-ttu-id="c67c2-116">適用於 Visual Studio 2015 的 .NET Core 工具不會再更新，但是如果您仍在使用 Visual Studio 2015，則必須安裝 [.NET Core VS 2015 工具預覽 2](https://www.microsoft.com/net/download/core)。</span><span class="sxs-lookup"><span data-stu-id="c67c2-116">The .NET Core tools for Visual Studio 2015 are no longer being updated, however if you are still using Visual Studio 2015, you need to have [.NET Core VS 2015 Tooling Preview 2](https://www.microsoft.com/net/download/core) installed.</span></span>

## <a name="add-an-aspnet-core-service-to-your-application"></a><span data-ttu-id="c67c2-117">將 ASP.NET Core 服務新增至您的應用程式</span><span class="sxs-lookup"><span data-stu-id="c67c2-117">Add an ASP.NET Core service to your application</span></span>
<span data-ttu-id="c67c2-118">ASP.NET Core 是輕量型、跨平台的 Web 開發架構，可供您用來建立新式 Web UI 和 Web API。</span><span class="sxs-lookup"><span data-stu-id="c67c2-118">ASP.NET Core is a lightweight, cross-platform web development framework that you can use to create modern web UI and web APIs.</span></span> 

<span data-ttu-id="c67c2-119">讓我們將 ASP.NET Web API 專案新增至現有的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c67c2-119">Let's add an ASP.NET Web API project to our existing application.</span></span>

1. <span data-ttu-id="c67c2-120">在 [方案總管] 中，以滑鼠右鍵按一下應用程式專案中的 [服務]，然後選擇 [新增] > [新增 Service Fabric Explorer]。</span><span class="sxs-lookup"><span data-stu-id="c67c2-120">In Solution Explorer, right-click **Services** within the application project and choose **Add > New Service Fabric Service**.</span></span>
   
    ![將新服務加入至現有的應用程式][vs-add-new-service]
2. <span data-ttu-id="c67c2-122">在 [建立服務] 頁面上，選擇 [ASP.NET Core] 並予以命名。</span><span class="sxs-lookup"><span data-stu-id="c67c2-122">On the **Create a Service** page, choose **ASP.NET Core** and give it a name.</span></span>
   
    ![在新服務對話方塊中選擇 ASP.NET Web 服務][vs-new-service-dialog]

3. <span data-ttu-id="c67c2-124">下一頁會提供一組 ASP.NET Core 專案範本。</span><span class="sxs-lookup"><span data-stu-id="c67c2-124">The next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="c67c2-125">請注意，如果利用少量的額外程式碼來註冊 Service Fabric 執行階段的服務，建立了 Service Fabric 應用程式之外的 ASP.NET Core 專案，則這些全都是您會看到的相同選擇。</span><span class="sxs-lookup"><span data-stu-id="c67c2-125">Note that these are the same choices that you would see if you created an ASP.NET Core project outside of a Service Fabric application, with a small amount of additional code to register the service with the Service Fabric runtime.</span></span> <span data-ttu-id="c67c2-126">在本教學課程中，選擇 [Web API]。</span><span class="sxs-lookup"><span data-stu-id="c67c2-126">For this tutorial, choose **Web API**.</span></span> <span data-ttu-id="c67c2-127">但您可以將相同的概念套用於建置完整的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c67c2-127">However, you can apply the same concepts to building a full web application.</span></span>
   
    ![選擇 ASP.NET 專案類型][vs-new-aspnet-project-dialog]
   
    <span data-ttu-id="c67c2-129">建立 Web API 專案後，您的應用程式中應有兩個服務。</span><span class="sxs-lookup"><span data-stu-id="c67c2-129">Once your Web API project is created, you should have two services in your application.</span></span> <span data-ttu-id="c67c2-130">隨著您繼續建置應用程式，您可以用完全相同的方式新增更多服務。</span><span class="sxs-lookup"><span data-stu-id="c67c2-130">As you continue to build your application, you can add more services in exactly the same way.</span></span> <span data-ttu-id="c67c2-131">每個服務都可以獨立設定版本和升級。</span><span class="sxs-lookup"><span data-stu-id="c67c2-131">Each can be independently versioned and upgraded.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="c67c2-132">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="c67c2-132">Run the application</span></span>
<span data-ttu-id="c67c2-133">若要了解我們所做的事情，就讓我們部署新的應用程式並看看 ASP.NET Core Web API 範本所提供的預設行為。</span><span class="sxs-lookup"><span data-stu-id="c67c2-133">To get a sense of what we've done, let's deploy the new application and take a look at the default behavior that the ASP.NET Core Web API template provides.</span></span>

1. <span data-ttu-id="c67c2-134">在 Visual Studio 按 F5 以進行應用程式偵錯。</span><span class="sxs-lookup"><span data-stu-id="c67c2-134">Press F5 in Visual Studio to debug the app.</span></span>
2. <span data-ttu-id="c67c2-135">部署完成時，Visual Studio 會啟動瀏覽器並瀏覽至 ASP.NET Web API 服務的根目錄。</span><span class="sxs-lookup"><span data-stu-id="c67c2-135">When deployment is complete, Visual Studio launches a browser to the root of the ASP.NET Web API service.</span></span> <span data-ttu-id="c67c2-136">ASP.NET Core 的 Web API 範本不提供根目錄的預設行為，因此您會在瀏覽器中看到 404 錯誤。</span><span class="sxs-lookup"><span data-stu-id="c67c2-136">The ASP.NET Core Web API template doesn't provide default behavior for the root, so you should see a 404 error in the browser.</span></span>
3. <span data-ttu-id="c67c2-137">將 `/api/values` 新增至瀏覽器中的位置。</span><span class="sxs-lookup"><span data-stu-id="c67c2-137">Add `/api/values` to the location in the browser.</span></span> <span data-ttu-id="c67c2-138">這會叫用 Web API 範本中 ValuesController 上的 `Get` 方法。</span><span class="sxs-lookup"><span data-stu-id="c67c2-138">This invokes the `Get` method on the ValuesController in the Web API template.</span></span> <span data-ttu-id="c67c2-139">它會傳回範本所提供的預設回應，也就是包含兩個字串的 JSON 陣列：</span><span class="sxs-lookup"><span data-stu-id="c67c2-139">It returns the default response that is provided by the template--a JSON array that contains two strings:</span></span>
   
    ![從 ASP.NET Core Web API 範本傳回的預設值][browser-aspnet-template-values]
   
    <span data-ttu-id="c67c2-141">在本教學課程結束前，此頁面會顯示我們的具狀態服務中的最新計數器值，而不是這些預設值。</span><span class="sxs-lookup"><span data-stu-id="c67c2-141">By the end of the tutorial, this page will show the most recent counter value from our stateful service instead of the default strings.</span></span>

## <a name="connect-the-services"></a><span data-ttu-id="c67c2-142">連接服務</span><span class="sxs-lookup"><span data-stu-id="c67c2-142">Connect the services</span></span>
<span data-ttu-id="c67c2-143">對於您與可靠服務通訊的方式，Service Fabric 會提供完整的彈性。</span><span class="sxs-lookup"><span data-stu-id="c67c2-143">Service Fabric provides complete flexibility in how you communicate with reliable services.</span></span> <span data-ttu-id="c67c2-144">在單一應用程式中，您可能擁有可透過 TCP 存取的服務、可透過 HTTP REST API 存取的其他服務，並且還有其他可透過 Web 通訊端存取的服務。</span><span class="sxs-lookup"><span data-stu-id="c67c2-144">Within a single application, you might have services that are accessible via TCP, other services that are accessible via an HTTP REST API, and still other services that are accessible via web sockets.</span></span> <span data-ttu-id="c67c2-145">如需可用選項和相關權衡取捨的背景，請參閱 [與服務進行通訊](service-fabric-connect-and-communicate-with-services.md)。</span><span class="sxs-lookup"><span data-stu-id="c67c2-145">For background on the options available and the tradeoffs involved, see [Communicating with services](service-fabric-connect-and-communicate-with-services.md).</span></span> <span data-ttu-id="c67c2-146">在此教學課程中，我們使用 SDK 中提供的 [Service Fabric 服務遠端](service-fabric-reliable-services-communication-remoting.md)。</span><span class="sxs-lookup"><span data-stu-id="c67c2-146">In this tutorial, we use [Service Fabric Service Remoting](service-fabric-reliable-services-communication-remoting.md), provided in the SDK.</span></span>

<span data-ttu-id="c67c2-147">在服務遠端的做法中 (模仿遠端程序呼叫 (RPC))，您會定義一個介面以作為服務的公用合約。</span><span class="sxs-lookup"><span data-stu-id="c67c2-147">In the Service Remoting approach (modeled on remote procedure calls or RPCs), you define an interface to act as the public contract for the service.</span></span> <span data-ttu-id="c67c2-148">然後使用該介面來產生 Proxy 類別，以便與服務進行互動。</span><span class="sxs-lookup"><span data-stu-id="c67c2-148">Then, you use that interface to generate a proxy class for interacting with the service.</span></span>

### <a name="create-the-remoting-interface"></a><span data-ttu-id="c67c2-149">建立遠端介面</span><span class="sxs-lookup"><span data-stu-id="c67c2-149">Create the remoting interface</span></span>
<span data-ttu-id="c67c2-150">一開始先建立介面作為具狀態服務與其他服務之間的合約，在這個案例中是 ASP.NET Core 的 Web 專案。</span><span class="sxs-lookup"><span data-stu-id="c67c2-150">Let's start by creating the interface to act as the contract between the stateful service and other services, in this case the ASP.NET Core web project.</span></span> <span data-ttu-id="c67c2-151">這個介面必須由使用它進行 RPC 呼叫的所有服務共用，因此我們會在它自己的類別庫專案中建立它。</span><span class="sxs-lookup"><span data-stu-id="c67c2-151">This interface must be shared by all services that use it to make RPC calls, so we'll create it in its own Class Library project.</span></span>

1. <span data-ttu-id="c67c2-152">在 [方案總管] 中，以滑鼠右鍵按一下您的方案並選擇 [加入] **將** > 。</span><span class="sxs-lookup"><span data-stu-id="c67c2-152">In Solution Explorer, right-click your solution and choose **Add** > **New Project**.</span></span>

2. <span data-ttu-id="c67c2-153">在左側導覽窗格中選擇 [Visual C#] 項目，然後選取 [類別庫] 範本。</span><span class="sxs-lookup"><span data-stu-id="c67c2-153">Choose the **Visual C#** entry in the left navigation pane and then select the **Class Library** template.</span></span> <span data-ttu-id="c67c2-154">確定 .NET Framework 版本已設定為 **4.5.2**。</span><span class="sxs-lookup"><span data-stu-id="c67c2-154">Ensure that the .NET Framework version is set to **4.5.2**.</span></span>
   
    ![為具狀態服務建立介面專案][vs-add-class-library-project]

3. <span data-ttu-id="c67c2-156">安裝 **Microsoft.ServiceFabric.Services.Remoting** NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="c67c2-156">Install the **Microsoft.ServiceFabric.Services.Remoting** NuGet package.</span></span> <span data-ttu-id="c67c2-157">在 NuGet 套件管理員中搜尋**Microsoft.ServiceFabric.Services.Remoting**，並將它安裝在使用服務遠端的所有解決方案中的專案，包括：</span><span class="sxs-lookup"><span data-stu-id="c67c2-157">Search for  **Microsoft.ServiceFabric.Services.Remoting** in the NuGet package manager and install it for all projects in the solution that use Service Remoting, including:</span></span>
   - <span data-ttu-id="c67c2-158">包含服務介面的類別庫專案</span><span class="sxs-lookup"><span data-stu-id="c67c2-158">The Class Library project that contains the service interface</span></span>
   - <span data-ttu-id="c67c2-159">具狀態的服務專案</span><span class="sxs-lookup"><span data-stu-id="c67c2-159">The Stateful Service project</span></span>
   - <span data-ttu-id="c67c2-160">ASP.NET Core 的 Web 服務專案</span><span class="sxs-lookup"><span data-stu-id="c67c2-160">The ASP.NET Core web service project</span></span>
   
    ![新增服務 NuGet 封裝][vs-services-nuget-package]

4. <span data-ttu-id="c67c2-162">在類別庫中，透過單一方法 `GetCountAsync` 建立介面，並從 `Microsoft.ServiceFabric.Services.Remoting.IService` 擴充介面。</span><span class="sxs-lookup"><span data-stu-id="c67c2-162">In the class library, create an interface with a single method, `GetCountAsync`, and extend the interface from `Microsoft.ServiceFabric.Services.Remoting.IService`.</span></span> <span data-ttu-id="c67c2-163">遠端介面必須衍生自這個介面，以指出它是服務遠端的介面。</span><span class="sxs-lookup"><span data-stu-id="c67c2-163">The remoting interface must derive from this interface to indicate that it is a Service Remoting interface.</span></span>
   
    ```c#
    using Microsoft.ServiceFabric.Services.Remoting;
    using System.Threading.Tasks;
        
    ...

    namespace MyStatefulService.Interface
    {
        public interface ICounter: IService
        {
            Task<long> GetCountAsync();
        }
    }
    ```

### <a name="implement-the-interface-in-your-stateful-service"></a><span data-ttu-id="c67c2-164">在具狀態服務中實作介面</span><span class="sxs-lookup"><span data-stu-id="c67c2-164">Implement the interface in your stateful service</span></span>
<span data-ttu-id="c67c2-165">既然我們已定義介面，我們必須在具狀態服務中實作該介面。</span><span class="sxs-lookup"><span data-stu-id="c67c2-165">Now that we have defined the interface, we need to implement it in the stateful service.</span></span>

1. <span data-ttu-id="c67c2-166">在具狀態服務中，新增含有此介面之類別庫專案的參考。</span><span class="sxs-lookup"><span data-stu-id="c67c2-166">In your stateful service, add a reference to the class library project that contains the interface.</span></span>
   
    ![新增具狀態服務中的類別庫專案的參考][vs-add-class-library-reference]
2. <span data-ttu-id="c67c2-168">找出繼承自 `StatefulService` 的類別 (例如 `MyStatefulService`)，然後加以擴充以實作 `ICounter` 介面。</span><span class="sxs-lookup"><span data-stu-id="c67c2-168">Locate the class that inherits from `StatefulService`, such as `MyStatefulService`, and extend it to implement the `ICounter` interface.</span></span>
   
    ```c#
    using MyStatefulService.Interface;
   
    ...
   
    public class MyStatefulService : StatefulService, ICounter
    {        
         ...
    }
    ```
3. <span data-ttu-id="c67c2-169">現在實作 `ICounter` 介面中所定義的單一方法，即 `GetCountAsync`。</span><span class="sxs-lookup"><span data-stu-id="c67c2-169">Now implement the single method that is defined in the `ICounter` interface, `GetCountAsync`.</span></span>
   
    ```c#
    public async Task<long> GetCountAsync()
    {
        var myDictionary = 
            await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
   
        using (var tx = this.StateManager.CreateTransaction())
        {          
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");
            return result.HasValue ? result.Value : 0;
        }
    }
    ```

### <a name="expose-the-stateful-service-using-a-service-remoting-listener"></a><span data-ttu-id="c67c2-170">使用服務遠端處理接聽程式公開具狀態服務</span><span class="sxs-lookup"><span data-stu-id="c67c2-170">Expose the stateful service using a service remoting listener</span></span>
<span data-ttu-id="c67c2-171">實作 `ICounter` 介面後，最後一個步驟是開啟服務遠端的通訊通道。</span><span class="sxs-lookup"><span data-stu-id="c67c2-171">With the `ICounter` interface implemented, the final step is to open the Service Remoting communication channel.</span></span> <span data-ttu-id="c67c2-172">對於具狀態服務，Service Fabric 會提供稱為 `CreateServiceReplicaListeners`的可覆寫方法。</span><span class="sxs-lookup"><span data-stu-id="c67c2-172">For stateful services, Service Fabric provides an overridable method called `CreateServiceReplicaListeners`.</span></span> <span data-ttu-id="c67c2-173">透過此方法，您可以根據想要為服務啟用的通訊類型，指定一或多個通訊接聽程式。</span><span class="sxs-lookup"><span data-stu-id="c67c2-173">With this method, you can specify one or more communication listeners, based on the type of communication that you want to enable for your service.</span></span>

> [!NOTE]
> <span data-ttu-id="c67c2-174">用於開啟無狀態服務之通訊通道的對等方法稱為 `CreateServiceInstanceListeners`。</span><span class="sxs-lookup"><span data-stu-id="c67c2-174">The equivalent method for opening a communication channel to stateless services is called `CreateServiceInstanceListeners`.</span></span>

<span data-ttu-id="c67c2-175">在此案例中，我們取代現有的 `CreateServiceReplicaListeners` 方法，並提供 `ServiceRemotingListener` 的執行個體，此執行個體會透過 `ServiceProxy` 建立可從用戶端呼叫的 RPC 端點。</span><span class="sxs-lookup"><span data-stu-id="c67c2-175">In this case, we replace the existing `CreateServiceReplicaListeners` method and provide an instance of `ServiceRemotingListener`, which creates an RPC endpoint that is callable from clients through `ServiceProxy`.</span></span>  

<span data-ttu-id="c67c2-176">`IService` 介面上的 `CreateServiceRemotingListener` 擴充方法可讓您輕鬆地使用所有預設設定建立 `ServiceRemotingListener`。</span><span class="sxs-lookup"><span data-stu-id="c67c2-176">The `CreateServiceRemotingListener` extension method on the `IService` interface allows you to easily create a `ServiceRemotingListener` with all default settings.</span></span> <span data-ttu-id="c67c2-177">若要使用這個擴充方法，請確定您已匯入 `Microsoft.ServiceFabric.Services.Remoting.Runtime` 命名空間。</span><span class="sxs-lookup"><span data-stu-id="c67c2-177">To use this extension method, ensure you have the `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace imported.</span></span> 

```c#
using Microsoft.ServiceFabric.Services.Remoting.Runtime;

...

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new List<ServiceReplicaListener>()
    {
        new ServiceReplicaListener(
            (context) =>
                this.CreateServiceRemotingListener(context))
    };
}
```


### <a name="use-the-serviceproxy-class-to-interact-with-the-service"></a><span data-ttu-id="c67c2-178">使用 ServiceProxy 類別來與服務互動</span><span class="sxs-lookup"><span data-stu-id="c67c2-178">Use the ServiceProxy class to interact with the service</span></span>
<span data-ttu-id="c67c2-179">現在，具狀態服務已經準備好接收透過 RPC 來自其他服務的流量。</span><span class="sxs-lookup"><span data-stu-id="c67c2-179">Our stateful service is now ready to receive traffic from other services over RPC.</span></span> <span data-ttu-id="c67c2-180">因此，剩下的工作便是從 ASP.NET Web 服務加入程式碼來與其通訊。</span><span class="sxs-lookup"><span data-stu-id="c67c2-180">So all that remains is adding the code to communicate with it from the ASP.NET web service.</span></span>

1. <span data-ttu-id="c67c2-181">在 ASP.NET 專案中，新增對含有 `ICounter` 介面之類別庫的參考。</span><span class="sxs-lookup"><span data-stu-id="c67c2-181">In your ASP.NET project, add a reference to the class library that contains the `ICounter` interface.</span></span>

2. <span data-ttu-id="c67c2-182">稍早您將 **Microsoft.ServiceFabric.Services.Remoting** NuGet 套件新增到 ASP.NET 專案。</span><span class="sxs-lookup"><span data-stu-id="c67c2-182">Earlier you added the **Microsoft.ServiceFabric.Services.Remoting** NuGet package to the ASP.NET project.</span></span> <span data-ttu-id="c67c2-183">這個套件提供 `ServiceProxy` 類別，可用來對具狀態服務進行 RPC 呼叫。</span><span class="sxs-lookup"><span data-stu-id="c67c2-183">This package provides the `ServiceProxy` class which you use to make RPC calls to the stateful service.</span></span> <span data-ttu-id="c67c2-184">請確定此 NuGet 套件已安裝在 ASP.NET Core 的 Web 服務專案中。</span><span class="sxs-lookup"><span data-stu-id="c67c2-184">Ensure this NuGet package is installed in the ASP.NET Core web service project.</span></span>

4. <span data-ttu-id="c67c2-185">在 **Controllers** 資料夾中，開啟 `ValuesController` 類別。</span><span class="sxs-lookup"><span data-stu-id="c67c2-185">In the **Controllers** folder, open the `ValuesController` class.</span></span> <span data-ttu-id="c67c2-186">請注意， `Get` 方法目前只會傳回 "value1" 和 "value2" 的硬式編碼字串陣列，這符合我們稍早在瀏覽器中所見的內容。</span><span class="sxs-lookup"><span data-stu-id="c67c2-186">Note that the `Get` method currently just returns a hard-coded string array of "value1" and "value2"--which matches what we saw earlier in the browser.</span></span> <span data-ttu-id="c67c2-187">使用下列程式碼來取代此實作：</span><span class="sxs-lookup"><span data-stu-id="c67c2-187">Replace this implementation with the following code:</span></span>
   
    ```c#
    using MyStatefulService.Interface;
    using Microsoft.ServiceFabric.Services.Client;
    using Microsoft.ServiceFabric.Services.Remoting.Client;
   
    ...

    [HttpGet]
    public async Task<IEnumerable<string>> Get()
    {
        ICounter counter =
            ServiceProxy.Create<ICounter>(new Uri("fabric:/MyApplication/MyStatefulService"), new ServicePartitionKey(0));
   
        long count = await counter.GetCountAsync();
   
        return new string[] { count.ToString() };
    }
    ```
   
    <span data-ttu-id="c67c2-188">第一行程式碼是關鍵程式碼。</span><span class="sxs-lookup"><span data-stu-id="c67c2-188">The first line of code is the key one.</span></span> <span data-ttu-id="c67c2-189">若要建立具狀態服務的 ICounter Proxy，您必須提供兩項資訊：資料分割識別碼和服務名稱。</span><span class="sxs-lookup"><span data-stu-id="c67c2-189">To create the ICounter proxy to the stateful service, you need to provide two pieces of information: a partition ID and the name of the service.</span></span>
   
    <span data-ttu-id="c67c2-190">您可以使用資料分割，根據您定義的索引鍵 (例如客戶識別碼或郵遞區號) 將具狀態服務的狀態劃分為不同的值區，藉此調整具狀態服務。</span><span class="sxs-lookup"><span data-stu-id="c67c2-190">You can use partitioning to scale stateful services by breaking up their state into different buckets, based on a key that you define, such as a customer ID or postal code.</span></span> <span data-ttu-id="c67c2-191">在我們的簡單應用程式中，具狀態服務只有一個資料分割，所以索引鍵並不重要。</span><span class="sxs-lookup"><span data-stu-id="c67c2-191">In our trivial application, the stateful service only has one partition, so the key doesn't matter.</span></span> <span data-ttu-id="c67c2-192">您所提供的任何索引鍵將會造成相同的資料分割。</span><span class="sxs-lookup"><span data-stu-id="c67c2-192">Any key that you provide will lead to the same partition.</span></span> <span data-ttu-id="c67c2-193">如深入了解分割服務，請參閱 [如何分割 Service Fabric 可靠的服務](service-fabric-concepts-partitioning.md)。</span><span class="sxs-lookup"><span data-stu-id="c67c2-193">To learn more about partitioning services, see [How to partition Service Fabric Reliable Services](service-fabric-concepts-partitioning.md).</span></span>
   
    <span data-ttu-id="c67c2-194">服務名稱是 fabric:/&lt;application_name&gt;/&lt;service_name&gt; 形式的 URI。</span><span class="sxs-lookup"><span data-stu-id="c67c2-194">The service name is a URI of the form fabric:/&lt;application_name&gt;/&lt;service_name&gt;.</span></span>
   
    <span data-ttu-id="c67c2-195">利用這兩項資訊，Service Fabric 即可唯一識別要求應傳送至的電腦。</span><span class="sxs-lookup"><span data-stu-id="c67c2-195">With these two pieces of information, Service Fabric can uniquely identify the machine that requests should be sent to.</span></span> <span data-ttu-id="c67c2-196">`ServiceProxy` 類別也會順暢地處理裝載具狀態服務分割區的電腦發生失敗的情況，而另一部電腦則必須進行升級才能取而代之。</span><span class="sxs-lookup"><span data-stu-id="c67c2-196">The `ServiceProxy` class also seamlessly handles the case where the machine that hosts the stateful service partition fails and another machine must be promoted to take its place.</span></span> <span data-ttu-id="c67c2-197">此概念讓撰寫用戶端程式碼來處理其他服務變得簡單許多。</span><span class="sxs-lookup"><span data-stu-id="c67c2-197">This abstraction makes writing the client code to deal with other services significantly simpler.</span></span>
   
    <span data-ttu-id="c67c2-198">一旦擁有 Proxy，我們只需叫用 `GetCountAsync` 方法並傳回其結果。</span><span class="sxs-lookup"><span data-stu-id="c67c2-198">Once we have the proxy, we simply invoke the `GetCountAsync` method and return its result.</span></span>

5. <span data-ttu-id="c67c2-199">再次按 F5 以執行修改過的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c67c2-199">Press F5 again to run the modified application.</span></span> <span data-ttu-id="c67c2-200">像之前一樣，Visual Studio 會自動啟動瀏覽器並瀏覽至 Web 專案的根目錄。</span><span class="sxs-lookup"><span data-stu-id="c67c2-200">As before, Visual Studio automatically launches the browser to the root of the web project.</span></span> <span data-ttu-id="c67c2-201">新增 "api/values" 路徑，您應該會看到傳回的目前計數器值。</span><span class="sxs-lookup"><span data-stu-id="c67c2-201">Add the "api/values" path, and you should see the current counter value returned.</span></span>
   
    ![在瀏覽器中顯示的具狀態計數器值][browser-aspnet-counter-value]
   
    <span data-ttu-id="c67c2-203">定期重新整理瀏覽器，以查看計數器值更新。</span><span class="sxs-lookup"><span data-stu-id="c67c2-203">Refresh the browser periodically to see the counter value update.</span></span>

## <a name="kestrel-and-weblistener"></a><span data-ttu-id="c67c2-204">Kestrel 和 WebListener</span><span class="sxs-lookup"><span data-stu-id="c67c2-204">Kestrel and WebListener</span></span>

<span data-ttu-id="c67c2-205">預設的 ASP.NET Core 網頁伺服器，稱為 Kestrel，[目前不支援處理直接的網際網路流量](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel)。</span><span class="sxs-lookup"><span data-stu-id="c67c2-205">The default ASP.NET Core web server, known as Kestrel, is [not currently supported for handling direct internet traffic](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel).</span></span> <span data-ttu-id="c67c2-206">因此，Service Fabric 的 ASP.NET Core 無狀態服務範本會使用[ WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener)。</span><span class="sxs-lookup"><span data-stu-id="c67c2-206">As a result, the ASP.NET Core stateless service template for Service Fabric uses [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) by default.</span></span> 

<span data-ttu-id="c67c2-207">若要深入了解 Service Fabric 中的 Kestrel 和 WebListener，請參閱 [Service Fabric Reliable Services 中的 ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md)。</span><span class="sxs-lookup"><span data-stu-id="c67c2-207">To learn more about Kestrel and WebListener in Service Fabric services, please refer to [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md).</span></span>

## <a name="connecting-to-a-reliable-actor-service"></a><span data-ttu-id="c67c2-208">連線至 Reliable Actor 服務</span><span class="sxs-lookup"><span data-stu-id="c67c2-208">Connecting to a Reliable Actor service</span></span>
<span data-ttu-id="c67c2-209">本教學課程著重於新增會與具狀態服務通訊的 Web 前端。</span><span class="sxs-lookup"><span data-stu-id="c67c2-209">This tutorial focused on adding a web front end that communicated with a stateful service.</span></span> <span data-ttu-id="c67c2-210">但是您可以依照非常類似的模型來與動作項目交談。</span><span class="sxs-lookup"><span data-stu-id="c67c2-210">However, you can follow a very similar model to talk to actors.</span></span> <span data-ttu-id="c67c2-211">當您建立 Reliable Actor 專案時，Visual Studio 會自動替您產生介面專案。</span><span class="sxs-lookup"><span data-stu-id="c67c2-211">When you create a Reliable Actor project, Visual Studio automatically generates an interface project for you.</span></span> <span data-ttu-id="c67c2-212">您可以使用該介面在 Web 專案中產生動作項目 Proxy 來與動作項目進行通訊。</span><span class="sxs-lookup"><span data-stu-id="c67c2-212">You can use that interface to generate an actor proxy in the web project to communicate with the actor.</span></span> <span data-ttu-id="c67c2-213">系統會自動提供通訊通道。</span><span class="sxs-lookup"><span data-stu-id="c67c2-213">The communication channel is provided automatically.</span></span> <span data-ttu-id="c67c2-214">因此您不需要如同在本教學課程中處理具狀態服務一樣，建立 `ServiceRemotingListener` 。</span><span class="sxs-lookup"><span data-stu-id="c67c2-214">So you do not need to do anything that is equivalent to establishing a `ServiceRemotingListener` like you did for the stateful service in this tutorial.</span></span>

## <a name="how-web-services-work-on-your-local-cluster"></a><span data-ttu-id="c67c2-215">Web 服務在本機叢集上的運作方式</span><span class="sxs-lookup"><span data-stu-id="c67c2-215">How web services work on your local cluster</span></span>
<span data-ttu-id="c67c2-216">一般而言，您可以將完全相同的 Service Fabric 應用程式部署到您在本機叢集上部署之多部電腦的叢集，而且有把握它會如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="c67c2-216">In general, you can deploy exactly the same Service Fabric application to a multi-machine cluster that you deployed on your local cluster and be highly confident that it works as you expect.</span></span> <span data-ttu-id="c67c2-217">這是因為本機叢集只是摺疊成單一機器的五個節點的組態。</span><span class="sxs-lookup"><span data-stu-id="c67c2-217">This is because your local cluster is simply a five-node configuration that is collapsed to a single machine.</span></span>

<span data-ttu-id="c67c2-218">不過，提到 Web 服務，有一個重要細微差別。</span><span class="sxs-lookup"><span data-stu-id="c67c2-218">When it comes to web services, however, there is one key nuance.</span></span> <span data-ttu-id="c67c2-219">當您的叢集位於負載平衡器後方時，如同在 Azure 中一樣，您必須確定 Web 服務已部署在每一部機器上，因為負載平衡器只會將流量循環配置於各電腦。</span><span class="sxs-lookup"><span data-stu-id="c67c2-219">When your cluster sits behind a load balancer, as it does in Azure, you must ensure that your web services are deployed on every machine since the load balancer simply round-robins traffic across the machines.</span></span> <span data-ttu-id="c67c2-220">您可以將服務的 `InstanceCount` 設定為特殊值 "-1" 來達到此目的。</span><span class="sxs-lookup"><span data-stu-id="c67c2-220">You can do this by setting the `InstanceCount` for the service to the special value of "-1".</span></span>

<span data-ttu-id="c67c2-221">相反地，當您在本機執行 Web 服務時，您必須確定服務只有一個執行個體正在執行。</span><span class="sxs-lookup"><span data-stu-id="c67c2-221">By contrast, when you run a web service locally, you need to ensure that only one instance of the service is running.</span></span> <span data-ttu-id="c67c2-222">否則，您會與正在相同路徑和連接埠上進行接聽的多個處理序發生衝突。</span><span class="sxs-lookup"><span data-stu-id="c67c2-222">Otherwise, you run into conflicts from multiple processes that are listening on the same path and port.</span></span> <span data-ttu-id="c67c2-223">因此，本機部署的 Web 服務執行個體計數應該設為 "1"。</span><span class="sxs-lookup"><span data-stu-id="c67c2-223">As a result, the web service instance count should be set to "1" for local deployments.</span></span>

<span data-ttu-id="c67c2-224">若要了解如何針對不同環境設定不同的值，請參閱 [管理多個環境的應用程式參數](service-fabric-manage-multiple-environment-app-configuration.md)。</span><span class="sxs-lookup"><span data-stu-id="c67c2-224">To learn how to configure different values for different environment, see [Managing application parameters for multiple environments](service-fabric-manage-multiple-environment-app-configuration.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c67c2-225">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c67c2-225">Next steps</span></span>
<span data-ttu-id="c67c2-226">現在，您已使用 ASP.NET Core 為應用程式設定 Web 前端，請參閱 [Service Fabric Reliable Services 中的 ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) 以深入了解 ASP.NET Core 如何與 Service Fabric 合作。</span><span class="sxs-lookup"><span data-stu-id="c67c2-226">Now that you have a web front end set up for your application with ASP.NET Core, learn more about [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) for an in-depth understanding of how ASP.NET Core works with Service Fabric.</span></span>

<span data-ttu-id="c67c2-227">接下來，從整體角度[深入了解與服務進行通訊](service-fabric-connect-and-communicate-with-services.md)，以完整了解 Service Fabric 中的服務通訊如何運作。</span><span class="sxs-lookup"><span data-stu-id="c67c2-227">Next, [learn more about communicating with services](service-fabric-connect-and-communicate-with-services.md) in general to get a complete picture of how service communication works in Service Fabric.</span></span>

<span data-ttu-id="c67c2-228">充分了解服務通訊的運作方式之後，您就可以[在 Azure 中建立叢集並將應用程式部署至雲端](service-fabric-cluster-creation-via-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="c67c2-228">Once you have a good understanding of how service communication works, [create a cluster in Azure and deploy your application to the cloud](service-fabric-cluster-creation-via-portal.md).</span></span>

<!-- Image References -->

[vs-add-new-service]: ./media/service-fabric-add-a-web-frontend/vs-add-new-service.png
[vs-new-service-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-service-dialog.png
[vs-new-aspnet-project-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-aspnet-project-dialog.png
[browser-aspnet-template-values]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-template-values.png
[vs-add-class-library-project]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-project.png
[vs-add-class-library-reference]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-reference.png
[vs-services-nuget-package]: ./media/service-fabric-add-a-web-frontend/vs-services-nuget-package.png
[browser-aspnet-counter-value]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-counter-value.png
[vs-create-platform]: ./media/service-fabric-add-a-web-frontend/vs-create-platform.png


<!-- external links -->
[dotnetcore-install]: https://www.microsoft.com/net/core#windows
