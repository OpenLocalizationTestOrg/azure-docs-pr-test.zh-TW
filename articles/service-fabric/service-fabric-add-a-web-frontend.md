---
title: "使用 ASP.NET Core Azure Service Fabric 應用程式的 web 前端 aaaCreate |Microsoft 文件"
description: "使用 ASP.NET Core 專案和服務間的通訊透過服務遠端公開 Service Fabric 應用程式 toohello web。"
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
ms.openlocfilehash: 0c4454d6cac4c2e343bd6e93e56d3d2f0ebfc4ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-web-service-front-end-for-your-application-using-aspnet-core"></a><span data-ttu-id="09bf0-103">使用 ASP.NET Core 建置應用程式的 Web 服務前端</span><span class="sxs-lookup"><span data-stu-id="09bf0-103">Build a web service front end for your application using ASP.NET Core</span></span>
<span data-ttu-id="09bf0-104">根據預設，Azure Service Fabric 服務不提供公用介面 toohello web。</span><span class="sxs-lookup"><span data-stu-id="09bf0-104">By default, Azure Service Fabric services do not provide a public interface toohello web.</span></span> <span data-ttu-id="09bf0-105">tooexpose 功能 tooHTTP 用戶端應用程式，您有 web 專案 tooact 做為進入點，然後從那裡 tooyour 通訊的 toocreate 個別的服務。</span><span class="sxs-lookup"><span data-stu-id="09bf0-105">tooexpose your application's functionality tooHTTP clients, you have toocreate a web project tooact as an entry point and then communicate from there tooyour individual services.</span></span>

<span data-ttu-id="09bf0-106">在本教學課程中，我們挑選我們離開的地方在 hello [Visual Studio 中建立第一個應用程式](service-fabric-create-your-first-application-in-visual-studio.md)教學課程和加入 ASP.NET Core web 服務前方 hello 可設定狀態的計數器服務。</span><span class="sxs-lookup"><span data-stu-id="09bf0-106">In this tutorial, we pick up where we left off in hello [Creating your first application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md) tutorial and add an ASP.NET Core web service in front of hello stateful counter service.</span></span> <span data-ttu-id="09bf0-107">如果您尚未這麼做，請返回並先逐步進行該教學課程。</span><span class="sxs-lookup"><span data-stu-id="09bf0-107">If you have not already done so, you should go back and step through that tutorial first.</span></span>

## <a name="set-up-your-environment-for-aspnet-core"></a><span data-ttu-id="09bf0-108">設定環境使其適用於 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="09bf0-108">Set up your environment for ASP.NET Core</span></span>

<span data-ttu-id="09bf0-109">您需要 Visual Studio 2017 toofollow 本教學課程。</span><span class="sxs-lookup"><span data-stu-id="09bf0-109">You need Visual Studio 2017 toofollow along with this tutorial.</span></span> <span data-ttu-id="09bf0-110">任何版本都可以。</span><span class="sxs-lookup"><span data-stu-id="09bf0-110">Any edition will do.</span></span> 

 - [<span data-ttu-id="09bf0-111">安裝 Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="09bf0-111">Install Visual Studio 2017</span></span>](https://www.visualstudio.com/)

<span data-ttu-id="09bf0-112">toodevelop ASP.NET Core Service Fabric 應用程式，您應該有下列安裝的工作負載的 hello:</span><span class="sxs-lookup"><span data-stu-id="09bf0-112">toodevelop ASP.NET Core Service Fabric applications, you should have hello following workloads installed:</span></span>
 - <span data-ttu-id="09bf0-113">**Azure 開發** (在 [Web 和 Cloud] 之下)</span><span class="sxs-lookup"><span data-stu-id="09bf0-113">**Azure development** (under *Web & Cloud*)</span></span>
 - <span data-ttu-id="09bf0-114">**ASP.NET 與 Web 開發** (在 [Web 和 Cloud] 之下)</span><span class="sxs-lookup"><span data-stu-id="09bf0-114">**ASP.NET and web development** (under *Web & Cloud*)</span></span>
 - <span data-ttu-id="09bf0-115">**.NET Core 跨平台開發** (在 [其他工具集] 之下)</span><span class="sxs-lookup"><span data-stu-id="09bf0-115">**.NET Core cross-platform development** (under *Other Toolsets*)</span></span>

>[!Note] 
><span data-ttu-id="09bf0-116">hello.NET Core tools for Visual Studio 2015 不會再正在更新，但是如果您仍在使用 Visual Studio 2015，您必須 toohave [.NET Core VS 2015 Tooling Preview 2](https://www.microsoft.com/net/download/core)安裝。</span><span class="sxs-lookup"><span data-stu-id="09bf0-116">hello .NET Core tools for Visual Studio 2015 are no longer being updated, however if you are still using Visual Studio 2015, you need toohave [.NET Core VS 2015 Tooling Preview 2](https://www.microsoft.com/net/download/core) installed.</span></span>

## <a name="add-an-aspnet-core-service-tooyour-application"></a><span data-ttu-id="09bf0-117">加入 ASP.NET Core service tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="09bf0-117">Add an ASP.NET Core service tooyour application</span></span>
<span data-ttu-id="09bf0-118">ASP.NET Core 是輕量型、 跨平台的 web 開發架構，您可以使用 toocreate 新式 web UI 和 web 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="09bf0-118">ASP.NET Core is a lightweight, cross-platform web development framework that you can use toocreate modern web UI and web APIs.</span></span> 

<span data-ttu-id="09bf0-119">讓我們加入 ASP.NET Web API 專案 tooour 現有的應用程式。</span><span class="sxs-lookup"><span data-stu-id="09bf0-119">Let's add an ASP.NET Web API project tooour existing application.</span></span>

1. <span data-ttu-id="09bf0-120">在 方案總管 中，以滑鼠右鍵按一下**服務**內 hello 應用程式專案，然後選擇 **新增 > 新增 Service Fabric 服務**。</span><span class="sxs-lookup"><span data-stu-id="09bf0-120">In Solution Explorer, right-click **Services** within hello application project and choose **Add > New Service Fabric Service**.</span></span>
   
    ![加入新的服務 tooan 現有應用程式][vs-add-new-service]
2. <span data-ttu-id="09bf0-122">在 hello**建立服務**頁面上，選擇**ASP.NET Core**並為它命名。</span><span class="sxs-lookup"><span data-stu-id="09bf0-122">On hello **Create a Service** page, choose **ASP.NET Core** and give it a name.</span></span>
   
    ![在 [hello 新增服務] 對話方塊中選擇 ASP.NET web 服務][vs-new-service-dialog]

3. <span data-ttu-id="09bf0-124">hello 下一個頁面會提供一組 ASP.NET Core 專案範本。</span><span class="sxs-lookup"><span data-stu-id="09bf0-124">hello next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="09bf0-125">請注意，這些是 hello 相同，您會看到 是否您只需要編寫小量的額外的程式碼 tooregister 建立 Service Fabric 應用程式之外的 ASP.NET Core 專案選擇 hello 與 hello Service Fabric 執行階段服務。</span><span class="sxs-lookup"><span data-stu-id="09bf0-125">Note that these are hello same choices that you would see if you created an ASP.NET Core project outside of a Service Fabric application, with a small amount of additional code tooregister hello service with hello Service Fabric runtime.</span></span> <span data-ttu-id="09bf0-126">在本教學課程中，選擇 [Web API]。</span><span class="sxs-lookup"><span data-stu-id="09bf0-126">For this tutorial, choose **Web API**.</span></span> <span data-ttu-id="09bf0-127">但是，您可以套用 hello 相同概念 toobuilding 完整 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="09bf0-127">However, you can apply hello same concepts toobuilding a full web application.</span></span>
   
    ![選擇 ASP.NET 專案類型][vs-new-aspnet-project-dialog]
   
    <span data-ttu-id="09bf0-129">建立 Web API 專案後，您的應用程式中應有兩個服務。</span><span class="sxs-lookup"><span data-stu-id="09bf0-129">Once your Web API project is created, you should have two services in your application.</span></span> <span data-ttu-id="09bf0-130">當您繼續 toobuild 您的應用程式，您可以加入更多服務完全 hello 中相同的方式。</span><span class="sxs-lookup"><span data-stu-id="09bf0-130">As you continue toobuild your application, you can add more services in exactly hello same way.</span></span> <span data-ttu-id="09bf0-131">每個服務都可以獨立設定版本和升級。</span><span class="sxs-lookup"><span data-stu-id="09bf0-131">Each can be independently versioned and upgraded.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="09bf0-132">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="09bf0-132">Run hello application</span></span>
<span data-ttu-id="09bf0-133">tooget 完成的內容，讓我們了解部署 hello 新應用程式，並採取提供查看 hello hello ASP.NET Core Web API 範本的預設行為。</span><span class="sxs-lookup"><span data-stu-id="09bf0-133">tooget a sense of what we've done, let's deploy hello new application and take a look at hello default behavior that hello ASP.NET Core Web API template provides.</span></span>

1. <span data-ttu-id="09bf0-134">在 Visual Studio toodebug hello 應用程式，請按 F5。</span><span class="sxs-lookup"><span data-stu-id="09bf0-134">Press F5 in Visual Studio toodebug hello app.</span></span>
2. <span data-ttu-id="09bf0-135">部署完成時，Visual Studio 會啟動瀏覽器 toohello 根的 hello ASP.NET Web API 服務。</span><span class="sxs-lookup"><span data-stu-id="09bf0-135">When deployment is complete, Visual Studio launches a browser toohello root of hello ASP.NET Web API service.</span></span> <span data-ttu-id="09bf0-136">hello ASP.NET Core Web API 範本不會提供預設行為 hello 根目錄，因此您應該會看到 404 錯誤 hello 瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="09bf0-136">hello ASP.NET Core Web API template doesn't provide default behavior for hello root, so you should see a 404 error in hello browser.</span></span>
3. <span data-ttu-id="09bf0-137">新增`/api/values`toohello hello 瀏覽器中的位置。</span><span class="sxs-lookup"><span data-stu-id="09bf0-137">Add `/api/values` toohello location in hello browser.</span></span> <span data-ttu-id="09bf0-138">這樣會叫用 hello`Get`上 hello ValuesController hello Web API 範本中的方法。</span><span class="sxs-lookup"><span data-stu-id="09bf0-138">This invokes hello `Get` method on hello ValuesController in hello Web API template.</span></span> <span data-ttu-id="09bf0-139">它會傳回所提供的 hello 範本--JSON 陣列，其中包含兩個字串 hello 預設回應：</span><span class="sxs-lookup"><span data-stu-id="09bf0-139">It returns hello default response that is provided by hello template--a JSON array that contains two strings:</span></span>
   
    ![從 ASP.NET Core Web API 範本傳回的預設值][browser-aspnet-template-values]
   
    <span data-ttu-id="09bf0-141">根據 hello hello 教學課程結束，此頁面會顯示我們可設定狀態的服務，而不是 hello hello 最近計數器值的預設字串。</span><span class="sxs-lookup"><span data-stu-id="09bf0-141">By hello end of hello tutorial, this page will show hello most recent counter value from our stateful service instead of hello default strings.</span></span>

## <a name="connect-hello-services"></a><span data-ttu-id="09bf0-142">Hello 服務連接</span><span class="sxs-lookup"><span data-stu-id="09bf0-142">Connect hello services</span></span>
<span data-ttu-id="09bf0-143">對於您與可靠服務通訊的方式，Service Fabric 會提供完整的彈性。</span><span class="sxs-lookup"><span data-stu-id="09bf0-143">Service Fabric provides complete flexibility in how you communicate with reliable services.</span></span> <span data-ttu-id="09bf0-144">在單一應用程式中，您可能擁有可透過 TCP 存取的服務、可透過 HTTP REST API 存取的其他服務，並且還有其他可透過 Web 通訊端存取的服務。</span><span class="sxs-lookup"><span data-stu-id="09bf0-144">Within a single application, you might have services that are accessible via TCP, other services that are accessible via an HTTP REST API, and still other services that are accessible via web sockets.</span></span> <span data-ttu-id="09bf0-145">如需有關可用的 hello 選項以及 hello 權衡取捨的背景，請參閱[與服務通訊](service-fabric-connect-and-communicate-with-services.md)。</span><span class="sxs-lookup"><span data-stu-id="09bf0-145">For background on hello options available and hello tradeoffs involved, see [Communicating with services](service-fabric-connect-and-communicate-with-services.md).</span></span> <span data-ttu-id="09bf0-146">在此教學課程中，我們使用[Service Fabric 服務遠端處理](service-fabric-reliable-services-communication-remoting.md)hello SDK 中提供。</span><span class="sxs-lookup"><span data-stu-id="09bf0-146">In this tutorial, we use [Service Fabric Service Remoting](service-fabric-reliable-services-communication-remoting.md), provided in hello SDK.</span></span>

<span data-ttu-id="09bf0-147">Hello （模擬遠端程序呼叫或 Rpc） 服務遠端處理方法，在中，您會定義介面 tooact 為 hello hello 服務公開的合約。</span><span class="sxs-lookup"><span data-stu-id="09bf0-147">In hello Service Remoting approach (modeled on remote procedure calls or RPCs), you define an interface tooact as hello public contract for hello service.</span></span> <span data-ttu-id="09bf0-148">然後，您可以使用該介面 toogenerate proxy 類別與 hello 服務互動。</span><span class="sxs-lookup"><span data-stu-id="09bf0-148">Then, you use that interface toogenerate a proxy class for interacting with hello service.</span></span>

### <a name="create-hello-remoting-interface"></a><span data-ttu-id="09bf0-149">建立 hello 遠端介面</span><span class="sxs-lookup"><span data-stu-id="09bf0-149">Create hello remoting interface</span></span>
<span data-ttu-id="09bf0-150">讓我們開始建立 hello 介面 tooact 做為 hello hello 可設定狀態的服務和其他服務，在此案例的 hello ASP.NET Core web 專案之間的合約。</span><span class="sxs-lookup"><span data-stu-id="09bf0-150">Let's start by creating hello interface tooact as hello contract between hello stateful service and other services, in this case hello ASP.NET Core web project.</span></span> <span data-ttu-id="09bf0-151">此介面必須使用 toomake RPC 呼叫，因此我們將建立它自己的類別庫專案中的所有服務所共用。</span><span class="sxs-lookup"><span data-stu-id="09bf0-151">This interface must be shared by all services that use it toomake RPC calls, so we'll create it in its own Class Library project.</span></span>

1. <span data-ttu-id="09bf0-152">在 [方案總管] 中，以滑鼠右鍵按一下您的方案並選擇 [加入] **將** > 。</span><span class="sxs-lookup"><span data-stu-id="09bf0-152">In Solution Explorer, right-click your solution and choose **Add** > **New Project**.</span></span>

2. <span data-ttu-id="09bf0-153">選擇 hello **Visual C#** hello 左瀏覽窗格中，然後選取 hello 中的項目**類別庫**範本。</span><span class="sxs-lookup"><span data-stu-id="09bf0-153">Choose hello **Visual C#** entry in hello left navigation pane and then select hello **Class Library** template.</span></span> <span data-ttu-id="09bf0-154">請確定該 hello.NET Framework 版本設定太**4.5.2**。</span><span class="sxs-lookup"><span data-stu-id="09bf0-154">Ensure that hello .NET Framework version is set too**4.5.2**.</span></span>
   
    ![為具狀態服務建立介面專案][vs-add-class-library-project]

3. <span data-ttu-id="09bf0-156">安裝 hello **Microsoft.ServiceFabric.Services.Remoting** NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="09bf0-156">Install hello **Microsoft.ServiceFabric.Services.Remoting** NuGet package.</span></span> <span data-ttu-id="09bf0-157">搜尋**Microsoft.ServiceFabric.Services.Remoting**在 hello NuGet 封裝管理員，並將它安裝在 hello 方案中使用服務遠端處理的所有專案包括：</span><span class="sxs-lookup"><span data-stu-id="09bf0-157">Search for  **Microsoft.ServiceFabric.Services.Remoting** in hello NuGet package manager and install it for all projects in hello solution that use Service Remoting, including:</span></span>
   - <span data-ttu-id="09bf0-158">hello 包含 hello 服務介面的類別庫專案</span><span class="sxs-lookup"><span data-stu-id="09bf0-158">hello Class Library project that contains hello service interface</span></span>
   - <span data-ttu-id="09bf0-159">hello 可設定狀態服務專案</span><span class="sxs-lookup"><span data-stu-id="09bf0-159">hello Stateful Service project</span></span>
   - <span data-ttu-id="09bf0-160">hello ASP.NET Core web 服務專案</span><span class="sxs-lookup"><span data-stu-id="09bf0-160">hello ASP.NET Core web service project</span></span>
   
    ![正在將 hello 服務 NuGet 封裝][vs-services-nuget-package]

4. <span data-ttu-id="09bf0-162">Hello 類別庫中建立的介面具有單一方法， `GetCountAsync`，並擴充 hello 介面從`Microsoft.ServiceFabric.Services.Remoting.IService`。</span><span class="sxs-lookup"><span data-stu-id="09bf0-162">In hello class library, create an interface with a single method, `GetCountAsync`, and extend hello interface from `Microsoft.ServiceFabric.Services.Remoting.IService`.</span></span> <span data-ttu-id="09bf0-163">hello 遠端介面必須衍生自這個介面 tooindicate 它已服務遠端處理介面。</span><span class="sxs-lookup"><span data-stu-id="09bf0-163">hello remoting interface must derive from this interface tooindicate that it is a Service Remoting interface.</span></span>
   
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

### <a name="implement-hello-interface-in-your-stateful-service"></a><span data-ttu-id="09bf0-164">在您可設定狀態的服務中實作 hello 介面</span><span class="sxs-lookup"><span data-stu-id="09bf0-164">Implement hello interface in your stateful service</span></span>
<span data-ttu-id="09bf0-165">既然我們已經定義 hello 介面，現在需要 tooimplement 在 hello 具狀態服務。</span><span class="sxs-lookup"><span data-stu-id="09bf0-165">Now that we have defined hello interface, we need tooimplement it in hello stateful service.</span></span>

1. <span data-ttu-id="09bf0-166">在您可設定狀態的服務中，加入包含 hello 介面的參考 toohello 類別庫專案。</span><span class="sxs-lookup"><span data-stu-id="09bf0-166">In your stateful service, add a reference toohello class library project that contains hello interface.</span></span>
   
    ![在 hello 具狀態服務中加入參考 toohello 類別庫專案][vs-add-class-library-reference]
2. <span data-ttu-id="09bf0-168">找出 hello 類別繼承自`StatefulService`，例如`MyStatefulService`，並將它延伸 tooimplement hello`ICounter`介面。</span><span class="sxs-lookup"><span data-stu-id="09bf0-168">Locate hello class that inherits from `StatefulService`, such as `MyStatefulService`, and extend it tooimplement hello `ICounter` interface.</span></span>
   
    ```c#
    using MyStatefulService.Interface;
   
    ...
   
    public class MyStatefulService : StatefulService, ICounter
    {        
         ...
    }
    ```
3. <span data-ttu-id="09bf0-169">現在，實作 hello hello 中定義的單一方法`ICounter`介面， `GetCountAsync`。</span><span class="sxs-lookup"><span data-stu-id="09bf0-169">Now implement hello single method that is defined in hello `ICounter` interface, `GetCountAsync`.</span></span>
   
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

### <a name="expose-hello-stateful-service-using-a-service-remoting-listener"></a><span data-ttu-id="09bf0-170">公開 hello 可設定狀態的服務，使用服務遠端接聽程式</span><span class="sxs-lookup"><span data-stu-id="09bf0-170">Expose hello stateful service using a service remoting listener</span></span>
<span data-ttu-id="09bf0-171">以 hello`ICounter`介面實作，hello 最後一個步驟是 tooopen hello 服務遠端處理通訊通道。</span><span class="sxs-lookup"><span data-stu-id="09bf0-171">With hello `ICounter` interface implemented, hello final step is tooopen hello Service Remoting communication channel.</span></span> <span data-ttu-id="09bf0-172">對於具狀態服務，Service Fabric 會提供稱為 `CreateServiceReplicaListeners`的可覆寫方法。</span><span class="sxs-lookup"><span data-stu-id="09bf0-172">For stateful services, Service Fabric provides an overridable method called `CreateServiceReplicaListeners`.</span></span> <span data-ttu-id="09bf0-173">使用此方法，您可以指定一或多個通訊接聽程式，根據您想 tooenable，為您的服務通訊的 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="09bf0-173">With this method, you can specify one or more communication listeners, based on hello type of communication that you want tooenable for your service.</span></span>

> [!NOTE]
> <span data-ttu-id="09bf0-174">hello 等的方法，以開啟通訊通道 toostateless 服務稱為`CreateServiceInstanceListeners`。</span><span class="sxs-lookup"><span data-stu-id="09bf0-174">hello equivalent method for opening a communication channel toostateless services is called `CreateServiceInstanceListeners`.</span></span>

<span data-ttu-id="09bf0-175">在此情況下，我們將取代現有的 hello`CreateServiceReplicaListeners`方法，並提供的執行個體`ServiceRemotingListener`，這會建立 RPC 端點是可從用戶端透過呼叫`ServiceProxy`。</span><span class="sxs-lookup"><span data-stu-id="09bf0-175">In this case, we replace hello existing `CreateServiceReplicaListeners` method and provide an instance of `ServiceRemotingListener`, which creates an RPC endpoint that is callable from clients through `ServiceProxy`.</span></span>  

<span data-ttu-id="09bf0-176">hello `CreateServiceRemotingListener` hello 上的擴充方法`IService`介面可讓您 tooeasily 建立`ServiceRemotingListener`使用所有預設設定。</span><span class="sxs-lookup"><span data-stu-id="09bf0-176">hello `CreateServiceRemotingListener` extension method on hello `IService` interface allows you tooeasily create a `ServiceRemotingListener` with all default settings.</span></span> <span data-ttu-id="09bf0-177">toouse 這個擴充方法，請確定您有 hello`Microsoft.ServiceFabric.Services.Remoting.Runtime`匯入的命名空間。</span><span class="sxs-lookup"><span data-stu-id="09bf0-177">toouse this extension method, ensure you have hello `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace imported.</span></span> 

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


### <a name="use-hello-serviceproxy-class-toointeract-with-hello-service"></a><span data-ttu-id="09bf0-178">使用 hello ServiceProxy 類別 toointeract 與 hello 服務</span><span class="sxs-lookup"><span data-stu-id="09bf0-178">Use hello ServiceProxy class toointeract with hello service</span></span>
<span data-ttu-id="09bf0-179">我們可設定狀態的服務是透過 RPC 現在準備好 tooreceive 流量從其他服務。</span><span class="sxs-lookup"><span data-stu-id="09bf0-179">Our stateful service is now ready tooreceive traffic from other services over RPC.</span></span> <span data-ttu-id="09bf0-180">因此，仍然從 hello ASP.NET web 服務加入 hello 與它的程式碼 toocommunicate。</span><span class="sxs-lookup"><span data-stu-id="09bf0-180">So all that remains is adding hello code toocommunicate with it from hello ASP.NET web service.</span></span>

1. <span data-ttu-id="09bf0-181">在 ASP.NET 專案中，新增參考 toohello 類別庫包含 hello`ICounter`介面。</span><span class="sxs-lookup"><span data-stu-id="09bf0-181">In your ASP.NET project, add a reference toohello class library that contains hello `ICounter` interface.</span></span>

2. <span data-ttu-id="09bf0-182">您稍早加入 hello **Microsoft.ServiceFabric.Services.Remoting** NuGet 封裝 toohello ASP.NET 專案。</span><span class="sxs-lookup"><span data-stu-id="09bf0-182">Earlier you added hello **Microsoft.ServiceFabric.Services.Remoting** NuGet package toohello ASP.NET project.</span></span> <span data-ttu-id="09bf0-183">此封裝提供 hello`ServiceProxy`類別您使用 toomake RPC 呼叫 toohello 可設定狀態的服務。</span><span class="sxs-lookup"><span data-stu-id="09bf0-183">This package provides hello `ServiceProxy` class which you use toomake RPC calls toohello stateful service.</span></span> <span data-ttu-id="09bf0-184">請確認此 NuGet 封裝安裝在 hello ASP.NET Core web 服務專案。</span><span class="sxs-lookup"><span data-stu-id="09bf0-184">Ensure this NuGet package is installed in hello ASP.NET Core web service project.</span></span>

4. <span data-ttu-id="09bf0-185">在 hello**控制器**資料夾中，開啟 hello`ValuesController`類別。</span><span class="sxs-lookup"><span data-stu-id="09bf0-185">In hello **Controllers** folder, open hello `ValuesController` class.</span></span> <span data-ttu-id="09bf0-186">請注意該 hello`Get`方法目前只會傳回"value1"和"value2"-符合我們稍早在 hello 瀏覽器中看到的硬式編碼的字串陣列。</span><span class="sxs-lookup"><span data-stu-id="09bf0-186">Note that hello `Get` method currently just returns a hard-coded string array of "value1" and "value2"--which matches what we saw earlier in hello browser.</span></span> <span data-ttu-id="09bf0-187">取代這項實作以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="09bf0-187">Replace this implementation with hello following code:</span></span>
   
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
   
    <span data-ttu-id="09bf0-188">hello 第一行程式碼是 hello 金鑰一。</span><span class="sxs-lookup"><span data-stu-id="09bf0-188">hello first line of code is hello key one.</span></span> <span data-ttu-id="09bf0-189">toocreate hello ICounter proxy toohello 具狀態服務，您需要 tooprovide 兩項資訊： hello 服務的分割區識別碼和 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="09bf0-189">toocreate hello ICounter proxy toohello stateful service, you need tooprovide two pieces of information: a partition ID and hello name of hello service.</span></span>
   
    <span data-ttu-id="09bf0-190">您可以使用資料分割的 tooscale 可設定狀態服務分割成不同的值區，其狀態根據定義，例如客戶編號或郵遞區號的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="09bf0-190">You can use partitioning tooscale stateful services by breaking up their state into different buckets, based on a key that you define, such as a customer ID or postal code.</span></span> <span data-ttu-id="09bf0-191">一般應用程式中，在 hello 可設定狀態的服務只有一個資料分割，所以 hello 金鑰並不重要。</span><span class="sxs-lookup"><span data-stu-id="09bf0-191">In our trivial application, hello stateful service only has one partition, so hello key doesn't matter.</span></span> <span data-ttu-id="09bf0-192">您提供任何索引鍵時，會造成 toohello 相同的資料分割。</span><span class="sxs-lookup"><span data-stu-id="09bf0-192">Any key that you provide will lead toohello same partition.</span></span> <span data-ttu-id="09bf0-193">toolearn 進一步了解資料分割的服務，請參閱[如何 toopartition Service Fabric 可靠服務](service-fabric-concepts-partitioning.md)。</span><span class="sxs-lookup"><span data-stu-id="09bf0-193">toolearn more about partitioning services, see [How toopartition Service Fabric Reliable Services](service-fabric-concepts-partitioning.md).</span></span>
   
    <span data-ttu-id="09bf0-194">hello 服務名稱是 hello 表單網狀架構的 URI: /&lt;application_name&gt;/&lt;service_name&gt;。</span><span class="sxs-lookup"><span data-stu-id="09bf0-194">hello service name is a URI of hello form fabric:/&lt;application_name&gt;/&lt;service_name&gt;.</span></span>
   
    <span data-ttu-id="09bf0-195">使用這兩個資訊片段，Service Fabric 可唯一識別要求應該要傳送的 hello 機器。</span><span class="sxs-lookup"><span data-stu-id="09bf0-195">With these two pieces of information, Service Fabric can uniquely identify hello machine that requests should be sent to.</span></span> <span data-ttu-id="09bf0-196">hello`ServiceProxy`類別也順暢地處理 hello 案例，其中裝載 hello 可設定狀態的服務資料分割的 hello 機器失敗，而另一部電腦必須升級的 tootake 其所在位置。</span><span class="sxs-lookup"><span data-stu-id="09bf0-196">hello `ServiceProxy` class also seamlessly handles hello case where hello machine that hosts hello stateful service partition fails and another machine must be promoted tootake its place.</span></span> <span data-ttu-id="09bf0-197">這個抽象層可讓撰寫 hello 與其他服務簡單得多的用戶端程式碼 toodeal。</span><span class="sxs-lookup"><span data-stu-id="09bf0-197">This abstraction makes writing hello client code toodeal with other services significantly simpler.</span></span>
   
    <span data-ttu-id="09bf0-198">一旦 hello proxy，我們只叫用 hello`GetCountAsync`方法並傳回其結果。</span><span class="sxs-lookup"><span data-stu-id="09bf0-198">Once we have hello proxy, we simply invoke hello `GetCountAsync` method and return its result.</span></span>

5. <span data-ttu-id="09bf0-199">按 F5 再次 toorun hello 修改應用程式。</span><span class="sxs-lookup"><span data-stu-id="09bf0-199">Press F5 again toorun hello modified application.</span></span> <span data-ttu-id="09bf0-200">為之前，Visual Studio 會自動啟動 hello web 專案的 hello 瀏覽器 toohello 根目錄。</span><span class="sxs-lookup"><span data-stu-id="09bf0-200">As before, Visual Studio automatically launches hello browser toohello root of hello web project.</span></span> <span data-ttu-id="09bf0-201">加入 hello 「 api/值 」 的路徑，以及您應該會看到 hello 傳回目前計數器值。</span><span class="sxs-lookup"><span data-stu-id="09bf0-201">Add hello "api/values" path, and you should see hello current counter value returned.</span></span>
   
    ![hello 瀏覽器中顯示 hello 可設定狀態的計數器值][browser-aspnet-counter-value]
   
    <span data-ttu-id="09bf0-203">重新整理 hello 瀏覽器定期 toosee hello 計數器值更新。</span><span class="sxs-lookup"><span data-stu-id="09bf0-203">Refresh hello browser periodically toosee hello counter value update.</span></span>

## <a name="kestrel-and-weblistener"></a><span data-ttu-id="09bf0-204">Kestrel 和 WebListener</span><span class="sxs-lookup"><span data-stu-id="09bf0-204">Kestrel and WebListener</span></span>

<span data-ttu-id="09bf0-205">hello 預設 ASP.NET Core web 伺服器，又稱為 Kestrel，是[目前不支援處理直接網際網路流量](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel)。</span><span class="sxs-lookup"><span data-stu-id="09bf0-205">hello default ASP.NET Core web server, known as Kestrel, is [not currently supported for handling direct internet traffic](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel).</span></span> <span data-ttu-id="09bf0-206">如此一來，hello 適用於 Service Fabric ASP.NET Core 無狀態的服務範本會使用[WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener)預設。</span><span class="sxs-lookup"><span data-stu-id="09bf0-206">As a result, hello ASP.NET Core stateless service template for Service Fabric uses [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) by default.</span></span> 

<span data-ttu-id="09bf0-207">Service Fabric 服務中的深入了解 Kestrel 和 WebListener toolearn，請參閱太[Service Fabric 可靠的服務中的 ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md)。</span><span class="sxs-lookup"><span data-stu-id="09bf0-207">toolearn more about Kestrel and WebListener in Service Fabric services, please refer too[ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md).</span></span>

## <a name="connecting-tooa-reliable-actor-service"></a><span data-ttu-id="09bf0-208">連接 tooa Reliable Actor 服務</span><span class="sxs-lookup"><span data-stu-id="09bf0-208">Connecting tooa Reliable Actor service</span></span>
<span data-ttu-id="09bf0-209">本教學課程著重於新增會與具狀態服務通訊的 Web 前端。</span><span class="sxs-lookup"><span data-stu-id="09bf0-209">This tutorial focused on adding a web front end that communicated with a stateful service.</span></span> <span data-ttu-id="09bf0-210">不過，您可以依照類似的模型 tootalk tooactors。</span><span class="sxs-lookup"><span data-stu-id="09bf0-210">However, you can follow a very similar model tootalk tooactors.</span></span> <span data-ttu-id="09bf0-211">當您建立 Reliable Actor 專案時，Visual Studio 會自動替您產生介面專案。</span><span class="sxs-lookup"><span data-stu-id="09bf0-211">When you create a Reliable Actor project, Visual Studio automatically generates an interface project for you.</span></span> <span data-ttu-id="09bf0-212">您可以使用該介面 toogenerate 執行者 proxy hello web 專案 toocommunicate 中，與 hello 動作項目。</span><span class="sxs-lookup"><span data-stu-id="09bf0-212">You can use that interface toogenerate an actor proxy in hello web project toocommunicate with hello actor.</span></span> <span data-ttu-id="09bf0-213">會自動提供 hello 通訊通道。</span><span class="sxs-lookup"><span data-stu-id="09bf0-213">hello communication channel is provided automatically.</span></span> <span data-ttu-id="09bf0-214">因此您不需要 toodo 任何項目，是對等 tooestablishing`ServiceRemotingListener`像 hello 可設定狀態服務在本教學課程。</span><span class="sxs-lookup"><span data-stu-id="09bf0-214">So you do not need toodo anything that is equivalent tooestablishing a `ServiceRemotingListener` like you did for hello stateful service in this tutorial.</span></span>

## <a name="how-web-services-work-on-your-local-cluster"></a><span data-ttu-id="09bf0-215">Web 服務在本機叢集上的運作方式</span><span class="sxs-lookup"><span data-stu-id="09bf0-215">How web services work on your local cluster</span></span>
<span data-ttu-id="09bf0-216">一般情況下，您可以部署完全 hello 相同 Service Fabric 應用程式 tooa 多電腦叢集您部署您的本機叢集上，並深信高它如預期運作。</span><span class="sxs-lookup"><span data-stu-id="09bf0-216">In general, you can deploy exactly hello same Service Fabric application tooa multi-machine cluster that you deployed on your local cluster and be highly confident that it works as you expect.</span></span> <span data-ttu-id="09bf0-217">這是因為您的本機叢集只是五個節點的組態是摺疊 tooa 單一電腦。</span><span class="sxs-lookup"><span data-stu-id="09bf0-217">This is because your local cluster is simply a five-node configuration that is collapsed tooa single machine.</span></span>

<span data-ttu-id="09bf0-218">Tooweb 服務時，不過，還有一個索引鍵的細微差別。</span><span class="sxs-lookup"><span data-stu-id="09bf0-218">When it comes tooweb services, however, there is one key nuance.</span></span> <span data-ttu-id="09bf0-219">當叢集位於負載平衡器後方，如同在 Azure 中時，您必須確保您的 web 服務每台機器上部署 hello 負載平衡器後只循 robins 流量分散到 hello 電腦。</span><span class="sxs-lookup"><span data-stu-id="09bf0-219">When your cluster sits behind a load balancer, as it does in Azure, you must ensure that your web services are deployed on every machine since hello load balancer simply round-robins traffic across hello machines.</span></span> <span data-ttu-id="09bf0-220">您可以透過設定 hello `InstanceCount` hello 服務 toohello 特殊值"-1"。</span><span class="sxs-lookup"><span data-stu-id="09bf0-220">You can do this by setting hello `InstanceCount` for hello service toohello special value of "-1".</span></span>

<span data-ttu-id="09bf0-221">相反地，當您在本機執行 web 服務，您需要 tooensure hello 服務該只有一個執行個體正在執行。</span><span class="sxs-lookup"><span data-stu-id="09bf0-221">By contrast, when you run a web service locally, you need tooensure that only one instance of hello service is running.</span></span> <span data-ttu-id="09bf0-222">否則，您遇到衝突都在接聽 hello 相同的多個處理序從路徑與連接埠。</span><span class="sxs-lookup"><span data-stu-id="09bf0-222">Otherwise, you run into conflicts from multiple processes that are listening on hello same path and port.</span></span> <span data-ttu-id="09bf0-223">如此一來，hello web 服務執行個體計數應該設定太"1"的本機部署。</span><span class="sxs-lookup"><span data-stu-id="09bf0-223">As a result, hello web service instance count should be set too"1" for local deployments.</span></span>

<span data-ttu-id="09bf0-224">如何 tooconfigure 不同的值不同的環境，請參閱的 toolearn[管理多個環境的應用程式參數](service-fabric-manage-multiple-environment-app-configuration.md)。</span><span class="sxs-lookup"><span data-stu-id="09bf0-224">toolearn how tooconfigure different values for different environment, see [Managing application parameters for multiple environments](service-fabric-manage-multiple-environment-app-configuration.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="09bf0-225">後續步驟</span><span class="sxs-lookup"><span data-stu-id="09bf0-225">Next steps</span></span>
<span data-ttu-id="09bf0-226">現在，您已使用 ASP.NET Core 為應用程式設定 Web 前端，請參閱 [Service Fabric Reliable Services 中的 ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) 以深入了解 ASP.NET Core 如何與 Service Fabric 合作。</span><span class="sxs-lookup"><span data-stu-id="09bf0-226">Now that you have a web front end set up for your application with ASP.NET Core, learn more about [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) for an in-depth understanding of how ASP.NET Core works with Service Fabric.</span></span>

<span data-ttu-id="09bf0-227">下一步[深入了解與服務通訊](service-fabric-connect-and-communicate-with-services.md)一般的完整 tooget 圖片的服務如何通訊適用於 Service Fabric。</span><span class="sxs-lookup"><span data-stu-id="09bf0-227">Next, [learn more about communicating with services](service-fabric-connect-and-communicate-with-services.md) in general tooget a complete picture of how service communication works in Service Fabric.</span></span>

<span data-ttu-id="09bf0-228">一旦您已經了解的服務通訊的運作方式，[在 Azure 中建立叢集，並部署您的應用程式 toohello 雲端](service-fabric-cluster-creation-via-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="09bf0-228">Once you have a good understanding of how service communication works, [create a cluster in Azure and deploy your application toohello cloud](service-fabric-cluster-creation-via-portal.md).</span></span>

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
