---
title: "aaaCreate C# 中的第一個 Service Fabric 應用程式 |Microsoft 文件"
description: "簡介 toocreating 無狀態與可設定狀態服務的 Microsoft Azure Service Fabric 應用程式。"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d9b44d75-e905-468e-b867-2190ce97379a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/06/2017
ms.author: vturecek
ms.openlocfilehash: e95e67cc84be1b83c936b250cae9112ddc77b963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-reliable-services"></a><span data-ttu-id="b267b-103">開始使用 Reliable Service</span><span class="sxs-lookup"><span data-stu-id="b267b-103">Get started with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b267b-104">Windows 上的 C# </span><span class="sxs-lookup"><span data-stu-id="b267b-104">C# on Windows</span></span>](service-fabric-reliable-services-quick-start.md)
> * [<span data-ttu-id="b267b-105">Linux 上的 Java</span><span class="sxs-lookup"><span data-stu-id="b267b-105">Java on Linux</span></span>](service-fabric-reliable-services-quick-start-java.md)
> 
> 

<span data-ttu-id="b267b-106">Azure Service Fabric 應用程式包含一個或多個執行您的程式碼的服務。</span><span class="sxs-lookup"><span data-stu-id="b267b-106">An Azure Service Fabric application contains one or more services that run your code.</span></span> <span data-ttu-id="b267b-107">本指南也說明如何 toocreate 無狀態與可設定狀態的 Service Fabric 應用程式與[可靠服務](service-fabric-reliable-services-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="b267b-107">This guide shows you how toocreate both stateless and stateful Service Fabric applications with [Reliable Services](service-fabric-reliable-services-introduction.md).</span></span>  <span data-ttu-id="b267b-108">Microsoft Virtual Academy 影片也將示範如何 toocreate 無狀態 Reliable service:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965"></span><span class="sxs-lookup"><span data-stu-id="b267b-108">This Microsoft Virtual Academy video also shows you how toocreate a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965"></span></span>  
<img src="./media/service-fabric-reliable-services-quick-start/ReliableServicesVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="basic-concepts"></a><span data-ttu-id="b267b-109">基本概念</span><span class="sxs-lookup"><span data-stu-id="b267b-109">Basic concepts</span></span>
<span data-ttu-id="b267b-110">tooget 開始使用可靠的服務，您只需要 toounderstand 某些基本概念：</span><span class="sxs-lookup"><span data-stu-id="b267b-110">tooget started with Reliable Services, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="b267b-111">**服務類型**：這是您的服務實作。</span><span class="sxs-lookup"><span data-stu-id="b267b-111">**Service type**: This is your service implementation.</span></span> <span data-ttu-id="b267b-112">它由您撰寫可擴充 hello 類別所定義`StatelessService`和任何其他程式碼或使用另有規定，以及名稱和版本號碼的相依性。</span><span class="sxs-lookup"><span data-stu-id="b267b-112">It is defined by hello class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span></span>
* <span data-ttu-id="b267b-113">**名為服務執行個體**: toorun 您的服務，您建立您的服務類型的具名執行個體更像建立的類別類型的物件執行個體。</span><span class="sxs-lookup"><span data-stu-id="b267b-113">**Named service instance**: toorun your service, you create named instances of your service type, much like you create object instances of a class type.</span></span> <span data-ttu-id="b267b-114">服務執行個體已使用 hello URI 的 hello 表單中的名稱 「 網狀架構: /"配置，例如"fabric: / MyApp/MyService"。</span><span class="sxs-lookup"><span data-stu-id="b267b-114">A service instance has a name in hello form of a URI using hello "fabric:/" scheme, such as "fabric:/MyApp/MyService".</span></span>
* <span data-ttu-id="b267b-115">**服務主機**: hello 名為您建立需要 toorun 主機處理序內的服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="b267b-115">**Service host**: hello named service instances you create need toorun inside a host process.</span></span> <span data-ttu-id="b267b-116">只要您的服務執行個體可以在上面執行的處理序 hello 服務主機。</span><span class="sxs-lookup"><span data-stu-id="b267b-116">hello service host is just a process where instances of your service can run.</span></span>
* <span data-ttu-id="b267b-117">**服務註冊**：註冊可將所有項目結合在一起。</span><span class="sxs-lookup"><span data-stu-id="b267b-117">**Service registration**: Registration brings everything together.</span></span> <span data-ttu-id="b267b-118">hello 服務類型必須註冊以 hello Service Fabric 服務中的執行階段裝載 tooallow Service Fabric toocreate 的執行個體，toorun。</span><span class="sxs-lookup"><span data-stu-id="b267b-118">hello service type must be registered with hello Service Fabric runtime in a service host tooallow Service Fabric toocreate instances of it toorun.</span></span>  

## <a name="create-a-stateless-service"></a><span data-ttu-id="b267b-119">建立無狀態服務</span><span class="sxs-lookup"><span data-stu-id="b267b-119">Create a stateless service</span></span>
<span data-ttu-id="b267b-120">無狀態服務是一種服務正在為雲端應用程式中的 hello 範數。</span><span class="sxs-lookup"><span data-stu-id="b267b-120">A stateless service is a type of service that is currently hello norm in cloud applications.</span></span> <span data-ttu-id="b267b-121">因為 hello 服務本身不包含需要 toobe 可靠地儲存，或成為高可用性的資料，則會視為無狀態。</span><span class="sxs-lookup"><span data-stu-id="b267b-121">It is considered stateless because hello service itself does not contain data that needs toobe stored reliably or made highly available.</span></span> <span data-ttu-id="b267b-122">如果無狀態服務的執行個體關閉，其所有內部狀態都會遺失。</span><span class="sxs-lookup"><span data-stu-id="b267b-122">If an instance of a stateless service shuts down, all of its internal state is lost.</span></span> <span data-ttu-id="b267b-123">在這種服務，狀態必須是永續性的 tooan 外部存放區，例如 Azure 資料表或 SQL 資料庫中，為其 toobe 會進行高度可用且可靠。</span><span class="sxs-lookup"><span data-stu-id="b267b-123">In this type of service, state must be persisted tooan external store, such as Azure Tables or a SQL database, for it toobe made highly available and reliable.</span></span>

<span data-ttu-id="b267b-124">以管理員身分啟動 Visual Studio 2015 或 Visual Studio 2017，並建立新的 Service Fabric 應用程式專案，命名為 HelloWorld：</span><span class="sxs-lookup"><span data-stu-id="b267b-124">Launch Visual Studio 2015 or Visual Studio 2017 as an administrator, and create a new Service Fabric application project named *HelloWorld*:</span></span>

![使用 hello 新增專案 對話方塊的方塊 toocreate 新的 Service Fabric 應用程式](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject.png)

<span data-ttu-id="b267b-126">然後建立名為 *HelloWorldStateless*的無狀態服務專案：</span><span class="sxs-lookup"><span data-stu-id="b267b-126">Then create a stateless service project named *HelloWorldStateless*:</span></span>

![在 hello 第二個對話方塊中，建立無狀態服務專案](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject2.png)

<span data-ttu-id="b267b-128">您的方案現在包含兩個專案：</span><span class="sxs-lookup"><span data-stu-id="b267b-128">Your solution now contains two projects:</span></span>

* <span data-ttu-id="b267b-129">*HelloWorld*。</span><span class="sxs-lookup"><span data-stu-id="b267b-129">*HelloWorld*.</span></span> <span data-ttu-id="b267b-130">這是 hello*應用程式*專案，其中包含您*服務*。</span><span class="sxs-lookup"><span data-stu-id="b267b-130">This is hello *application* project that contains your *services*.</span></span> <span data-ttu-id="b267b-131">它也包含說明 hello 應用程式，以及一些可協助您 toodeploy PowerShell 指令碼應用程式的 hello 應用程式資訊清單。</span><span class="sxs-lookup"><span data-stu-id="b267b-131">It also contains hello application manifest that describes hello application, as well as a number of PowerShell scripts that help you toodeploy your application.</span></span>
* <span data-ttu-id="b267b-132">*HelloWorldStateless*。</span><span class="sxs-lookup"><span data-stu-id="b267b-132">*HelloWorldStateless*.</span></span> <span data-ttu-id="b267b-133">這是 hello 服務專案。</span><span class="sxs-lookup"><span data-stu-id="b267b-133">This is hello service project.</span></span> <span data-ttu-id="b267b-134">它包含 hello 無狀態服務實作。</span><span class="sxs-lookup"><span data-stu-id="b267b-134">It contains hello stateless service implementation.</span></span>

## <a name="implement-hello-service"></a><span data-ttu-id="b267b-135">實作 hello 服務</span><span class="sxs-lookup"><span data-stu-id="b267b-135">Implement hello service</span></span>
<span data-ttu-id="b267b-136">開啟 hello **HelloWorldStateless.cs** hello 服務專案中的檔案。</span><span class="sxs-lookup"><span data-stu-id="b267b-136">Open hello **HelloWorldStateless.cs** file in hello service project.</span></span> <span data-ttu-id="b267b-137">在 Service Fabric 中，服務可以執行任何商務邏輯。</span><span class="sxs-lookup"><span data-stu-id="b267b-137">In Service Fabric, a service can run any business logic.</span></span> <span data-ttu-id="b267b-138">hello 服務 API 提供兩個進入點的程式碼：</span><span class="sxs-lookup"><span data-stu-id="b267b-138">hello service API provides two entry points for your code:</span></span>

* <span data-ttu-id="b267b-139">開放式的進入點方法，稱為 *RunAsync*，您可以在這裡開始執行任何工作負載，包括長時間執行的計算工作負載。</span><span class="sxs-lookup"><span data-stu-id="b267b-139">An open-ended entry point method, called *RunAsync*, where you can begin executing any workloads, including long-running compute workloads.</span></span>

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    ...
}
```

* <span data-ttu-id="b267b-140">通訊進入點，您可以在這裡插入選擇的通訊堆疊，例如 ASP.NET Core。</span><span class="sxs-lookup"><span data-stu-id="b267b-140">A communication entry point where you can plug in your communication stack of choice, such as ASP.NET Core.</span></span> <span data-ttu-id="b267b-141">這就是您可以開始接收來自使用者和其他服務要求的地方。</span><span class="sxs-lookup"><span data-stu-id="b267b-141">This is where you can start receiving requests from users and other services.</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}
```

<span data-ttu-id="b267b-142">在本教學課程中，我們將著重在 hello`RunAsync()`進入點方法。</span><span class="sxs-lookup"><span data-stu-id="b267b-142">In this tutorial, we will focus on hello `RunAsync()` entry point method.</span></span> <span data-ttu-id="b267b-143">這就是您可以立即開始執行程式碼的地方。</span><span class="sxs-lookup"><span data-stu-id="b267b-143">This is where you can immediately start running your code.</span></span>
<span data-ttu-id="b267b-144">hello 專案範本包含的範例實作`RunAsync()`增量循環計數。</span><span class="sxs-lookup"><span data-stu-id="b267b-144">hello project template includes a sample implementation of `RunAsync()` that increments a rolling count.</span></span>

> [!NOTE]
> <span data-ttu-id="b267b-145">如需如何 toowork 通訊堆疊的詳細資訊，請參閱[與 OWIN 自我主控的服務網狀架構 Web API 服務](service-fabric-reliable-services-communication-webapi.md)</span><span class="sxs-lookup"><span data-stu-id="b267b-145">For details about how toowork with a communication stack, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md)</span></span>
> 
> 

### <a name="runasync"></a><span data-ttu-id="b267b-146">RunAsync</span><span class="sxs-lookup"><span data-stu-id="b267b-146">RunAsync</span></span>
```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace hello following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    long iterations = 0;

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        ServiceEventSource.Current.ServiceMessage(this, "Working-{0}", ++iterations);

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
}
```

<span data-ttu-id="b267b-147">服務的執行個體時放置並準備好 tooexecute hello 平台會呼叫這個方法。</span><span class="sxs-lookup"><span data-stu-id="b267b-147">hello platform calls this method when an instance of a service is placed and ready tooexecute.</span></span> <span data-ttu-id="b267b-148">無狀態的服務，這只是表示開啟 hello 服務執行個體時。</span><span class="sxs-lookup"><span data-stu-id="b267b-148">For a stateless service, that simply means when hello service instance is opened.</span></span> <span data-ttu-id="b267b-149">取消語彙基元提供 toocoordinate 您服務執行個體需要 toobe 關閉時。</span><span class="sxs-lookup"><span data-stu-id="b267b-149">A cancellation token is provided toocoordinate when your service instance needs toobe closed.</span></span> <span data-ttu-id="b267b-150">在 Service Fabric 服務執行個體的此開啟/關閉週期可以發生多次存留 hello hello 服務的整個。</span><span class="sxs-lookup"><span data-stu-id="b267b-150">In Service Fabric, this open/close cycle of a service instance can occur many times over hello lifetime of hello service as a whole.</span></span> <span data-ttu-id="b267b-151">發生這種情形的原因有很多，包括：</span><span class="sxs-lookup"><span data-stu-id="b267b-151">This can happen for various reasons, including:</span></span>

* <span data-ttu-id="b267b-152">hello 系統移動資源平衡服務執行的個體。</span><span class="sxs-lookup"><span data-stu-id="b267b-152">hello system moves your service instances for resource balancing.</span></span>
* <span data-ttu-id="b267b-153">在您的程式碼中發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="b267b-153">Faults occur in your code.</span></span>
* <span data-ttu-id="b267b-154">hello 應用程式或系統也會升級。</span><span class="sxs-lookup"><span data-stu-id="b267b-154">hello application or system is upgraded.</span></span>
* <span data-ttu-id="b267b-155">hello 基礎硬體發生中斷。</span><span class="sxs-lookup"><span data-stu-id="b267b-155">hello underlying hardware experiences an outage.</span></span>

<span data-ttu-id="b267b-156">此協調流程由 hello 系統 tookeep 管理您的服務高可用性且正確平衡。</span><span class="sxs-lookup"><span data-stu-id="b267b-156">This orchestration is managed by hello system tookeep your service highly available and properly balanced.</span></span>

<span data-ttu-id="b267b-157">`RunAsync()` 不應該同步封鎖。</span><span class="sxs-lookup"><span data-stu-id="b267b-157">`RunAsync()` should not block synchronously.</span></span> <span data-ttu-id="b267b-158">RunAsync 的實作應該傳回的工作，或等待任何長時間執行或封鎖作業 tooallow hello 執行階段 toocontinue 上。</span><span class="sxs-lookup"><span data-stu-id="b267b-158">Your implementation of RunAsync should return a Task or await on any long-running or blocking operations tooallow hello runtime toocontinue.</span></span> <span data-ttu-id="b267b-159">請注意，在 hello `while(true)` hello 前一個範例中，傳回工作的迴圈`await Task.Delay()`用。</span><span class="sxs-lookup"><span data-stu-id="b267b-159">Note in hello `while(true)` loop in hello previous example, a Task-returning `await Task.Delay()` is used.</span></span> <span data-ttu-id="b267b-160">如果您的工作負載必須同步封鎖，您應該使用 `Task.Run()` 在您的 `RunAsync` 實作中排定一個新的工作。</span><span class="sxs-lookup"><span data-stu-id="b267b-160">If your workload must block synchronously, you should schedule a new Task with `Task.Run()` in your `RunAsync` implementation.</span></span>

<span data-ttu-id="b267b-161">取消您的工作負載是由提供取消語彙基元的 hello 協調合作式工作。</span><span class="sxs-lookup"><span data-stu-id="b267b-161">Cancellation of your workload is a cooperative effort orchestrated by hello provided cancellation token.</span></span> <span data-ttu-id="b267b-162">hello 系統將會等到工作 tooend （由成功完成、 取消作業或錯誤） 之間移動之前。</span><span class="sxs-lookup"><span data-stu-id="b267b-162">hello system will wait for your task tooend (by successful completion, cancellation, or fault) before it moves on.</span></span> <span data-ttu-id="b267b-163">它是重要的 toohonor hello 取消語彙基元，完成任何工作，並結束`RunAsync()`hello 系統要求取消盡快。</span><span class="sxs-lookup"><span data-stu-id="b267b-163">It is important toohonor hello cancellation token, finish any work, and exit `RunAsync()` as quickly as possible when hello system requests cancellation.</span></span>

<span data-ttu-id="b267b-164">無狀態服務在本例中，hello 計數會儲存在本機變數。</span><span class="sxs-lookup"><span data-stu-id="b267b-164">In this stateless service example, hello count is stored in a local variable.</span></span> <span data-ttu-id="b267b-165">但 hello 儲存的值，這是無狀態服務，因為存在只會針對目前 hello 其服務執行個體生命週期。</span><span class="sxs-lookup"><span data-stu-id="b267b-165">But because this is a stateless service, hello value that's stored exists only for hello current lifecycle of its service instance.</span></span> <span data-ttu-id="b267b-166">當 hello 服務移動或重新啟動時，將會遺失 hello 值。</span><span class="sxs-lookup"><span data-stu-id="b267b-166">When hello service moves or restarts, hello value is lost.</span></span>

## <a name="create-a-stateful-service"></a><span data-ttu-id="b267b-167">建立具狀態服務</span><span class="sxs-lookup"><span data-stu-id="b267b-167">Create a stateful service</span></span>
<span data-ttu-id="b267b-168">Service Fabric 導入了一種可設定狀態的新服務。</span><span class="sxs-lookup"><span data-stu-id="b267b-168">Service Fabric introduces a new kind of service that is stateful.</span></span> <span data-ttu-id="b267b-169">可設定狀態的服務可以維護可靠地 hello 服務本身，共 hello 正在使用它的程式碼中的狀態。</span><span class="sxs-lookup"><span data-stu-id="b267b-169">A stateful service can maintain state reliably within hello service itself, co-located with hello code that's using it.</span></span> <span data-ttu-id="b267b-170">狀態進行高可用性服務網狀架構不含 hello 需要 toopersist 狀態 tooan 外部存放區。</span><span class="sxs-lookup"><span data-stu-id="b267b-170">State is made highly available by Service Fabric without hello need toopersist state tooan external store.</span></span>

<span data-ttu-id="b267b-171">tooconvert 無狀態 toohighly 可用且持續性的計數器值，即使 hello 服務移動或重新啟動時，您需要具狀態的服務。</span><span class="sxs-lookup"><span data-stu-id="b267b-171">tooconvert a counter value from stateless toohighly available and persistent, even when hello service moves or restarts, you need a stateful service.</span></span>

<span data-ttu-id="b267b-172">在 hello 相同*HelloWorld*應用程式，可以加入新的服務，以滑鼠右鍵按一下在 hello 應用程式專案，並選取 hello uddi 服務參照**新增-> 新增 Service Fabric 服務**。</span><span class="sxs-lookup"><span data-stu-id="b267b-172">In hello same *HelloWorld* application, you can add a new service by right-clicking on hello Services references in hello application project and selecting **Add ->  New Service Fabric Service**.</span></span>

![新增服務 tooyour Service Fabric 應用程式](media/service-fabric-reliable-services-quick-start/hello-stateful-NewService.png)

<span data-ttu-id="b267b-174">選取 [具狀態服務]  並將它命名為 *HelloWorldStateful*。</span><span class="sxs-lookup"><span data-stu-id="b267b-174">Select **Stateful Service** and name it *HelloWorldStateful*.</span></span> <span data-ttu-id="b267b-175">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="b267b-175">Click **OK**.</span></span>

![使用 hello 新增專案 對話方塊的方塊 toocreate 新的 Service Fabric 具狀態服務](media/service-fabric-reliable-services-quick-start/hello-stateful-NewProject.png)

<span data-ttu-id="b267b-177">您的應用程式現在應該會有兩個服務： hello 無狀態服務*HelloWorldStateless*和 hello 可設定狀態服務*HelloWorldStateful*。</span><span class="sxs-lookup"><span data-stu-id="b267b-177">Your application should now have two services: hello stateless service *HelloWorldStateless* and hello stateful service *HelloWorldStateful*.</span></span>

<span data-ttu-id="b267b-178">可設定狀態的服務具有 hello 為無狀態服務的同一個進入點。</span><span class="sxs-lookup"><span data-stu-id="b267b-178">A stateful service has hello same entry points as a stateless service.</span></span> <span data-ttu-id="b267b-179">hello 主要差異在於 hello 可用性*狀態提供者*可以可靠地儲存狀態。</span><span class="sxs-lookup"><span data-stu-id="b267b-179">hello main difference is hello availability of a *state provider* that can store state reliably.</span></span> <span data-ttu-id="b267b-180">Service Fabric 隨附呼叫狀態提供者實作[可靠集合](service-fabric-reliable-services-reliable-collections.md)，可讓您建立可靠的狀態管理員的 hello 透過複寫的資料結構。</span><span class="sxs-lookup"><span data-stu-id="b267b-180">Service Fabric comes with a state provider implementation called [Reliable Collections](service-fabric-reliable-services-reliable-collections.md), which lets you create replicated data structures through hello Reliable State Manager.</span></span> <span data-ttu-id="b267b-181">具狀態可靠服務預設會使用此狀態供應器。</span><span class="sxs-lookup"><span data-stu-id="b267b-181">A stateful Reliable Service uses this state provider by default.</span></span>

<span data-ttu-id="b267b-182">開啟**HelloWorldStateful.cs**中*HelloWorldStateful*，其中包含下列 RunAsync 方法 hello:</span><span class="sxs-lookup"><span data-stu-id="b267b-182">Open **HelloWorldStateful.cs** in *HelloWorldStateful*, which contains hello following RunAsync method:</span></span>

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace hello following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        using (var tx = this.StateManager.CreateTransaction())
        {
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");

            ServiceEventSource.Current.ServiceMessage(this, "Current Counter Value: {0}",
                result.HasValue ? result.Value.ToString() : "Value does not exist.");

            await myDictionary.AddOrUpdateAsync(tx, "Counter", 0, (key, value) => ++value);

            // If an exception is thrown before calling CommitAsync, hello transaction aborts, all changes are
            // discarded, and nothing is saved toohello secondary replicas.
            await tx.CommitAsync();
        }

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
```

### <a name="runasync"></a><span data-ttu-id="b267b-183">RunAsync</span><span class="sxs-lookup"><span data-stu-id="b267b-183">RunAsync</span></span>
<span data-ttu-id="b267b-184">`RunAsync()` 在具狀態和無狀態服務中的運作方式類似。</span><span class="sxs-lookup"><span data-stu-id="b267b-184">`RunAsync()` operates similarly in stateful and stateless services.</span></span> <span data-ttu-id="b267b-185">不過，在可設定狀態的服務中，hello 平台執行額外工作代替您執行前先`RunAsync()`。</span><span class="sxs-lookup"><span data-stu-id="b267b-185">However, in a stateful service, hello platform performs additional work on your behalf before it executes `RunAsync()`.</span></span> <span data-ttu-id="b267b-186">這項工作可確保該 hello 可靠狀態管理員和可靠的集合是準備 toouse。</span><span class="sxs-lookup"><span data-stu-id="b267b-186">This work can include ensuring that hello Reliable State Manager and Reliable Collections are ready toouse.</span></span>

### <a name="reliable-collections-and-hello-reliable-state-manager"></a><span data-ttu-id="b267b-187">可靠的集合和 hello 可靠狀態管理員</span><span class="sxs-lookup"><span data-stu-id="b267b-187">Reliable Collections and hello Reliable State Manager</span></span>
```csharp
var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
```

<span data-ttu-id="b267b-188">[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx)是字典實作，您可以使用 tooreliably hello 服務中的存放區狀態。</span><span class="sxs-lookup"><span data-stu-id="b267b-188">[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) is a dictionary implementation that you can use tooreliably store state in hello service.</span></span> <span data-ttu-id="b267b-189">Service Fabric 和可靠的集合，您可以直接在您的服務而 hello 需要在外部的持續性存放區中儲存資料。</span><span class="sxs-lookup"><span data-stu-id="b267b-189">With Service Fabric and Reliable Collections, you can store data directly in your service without hello need for an external persistent store.</span></span> <span data-ttu-id="b267b-190">可靠的集合可讓您的資料具備高可用性。</span><span class="sxs-lookup"><span data-stu-id="b267b-190">Reliable Collections make your data highly available.</span></span> <span data-ttu-id="b267b-191">Service Fabric 會藉由為您建立與管理服務的多個複本  來完成此作業。</span><span class="sxs-lookup"><span data-stu-id="b267b-191">Service Fabric accomplishes this by creating and managing multiple *replicas* of your service for you.</span></span> <span data-ttu-id="b267b-192">它也提供 API，以區隔離開 hello 變得複雜，管理這些複本和其狀態轉換。</span><span class="sxs-lookup"><span data-stu-id="b267b-192">It also provides an API that abstracts away hello complexities of managing those replicas and their state transitions.</span></span>

<span data-ttu-id="b267b-193">可靠的集合可以儲存任何 .NET 類型 (包括您的自訂類型)，不過有幾個需要注意的事項：</span><span class="sxs-lookup"><span data-stu-id="b267b-193">Reliable Collections can store any .NET type, including your custom types, with a couple of caveats:</span></span>

* <span data-ttu-id="b267b-194">Service Fabric 讓高可用性，您的狀態*複寫*跨節點和可靠的集合狀態儲存資料 toolocal 磁碟上每個複本。</span><span class="sxs-lookup"><span data-stu-id="b267b-194">Service Fabric makes your state highly available by *replicating* state across nodes, and Reliable Collections store your data toolocal disk on each replica.</span></span> <span data-ttu-id="b267b-195">這表示所有儲存在可靠的集合中的項目必須可序列化 。</span><span class="sxs-lookup"><span data-stu-id="b267b-195">This means that everything that is stored in Reliable Collections must be *serializable*.</span></span> <span data-ttu-id="b267b-196">根據預設，使用可靠集合[DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx)進行序列化，因此，確定您的型別是重要 toomake [hello 資料合約序列化程式所支援](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx)當您使用 hello 預設序列化程式。</span><span class="sxs-lookup"><span data-stu-id="b267b-196">By default, Reliable Collections use [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) for serialization, so it's important toomake sure that your types are [supported by hello Data Contract Serializer](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) when you use hello default serializer.</span></span>
* <span data-ttu-id="b267b-197">當您在可靠的集合上認可交易時，物件會複寫以獲得高可用性。</span><span class="sxs-lookup"><span data-stu-id="b267b-197">Objects are replicated for high availability when you commit transactions on Reliable Collections.</span></span> <span data-ttu-id="b267b-198">儲存在可靠集合中的物件會保留在服務中的本機記憶體。</span><span class="sxs-lookup"><span data-stu-id="b267b-198">Objects stored in Reliable Collections are kept in local memory in your service.</span></span> <span data-ttu-id="b267b-199">這表示您有本機參考 toohello 物件。</span><span class="sxs-lookup"><span data-stu-id="b267b-199">This means that you have a local reference toohello object.</span></span>
  
   <span data-ttu-id="b267b-200">請務必您不要變更這些物件的本機執行個體不在交易中執行 hello 可靠集合上的更新作業。</span><span class="sxs-lookup"><span data-stu-id="b267b-200">It is important that you do not mutate local instances of those objects without performing an update operation on hello reliable collection in a transaction.</span></span> <span data-ttu-id="b267b-201">這是因為不會自動複寫的物件變更 toolocal 執行個體。</span><span class="sxs-lookup"><span data-stu-id="b267b-201">This is because changes toolocal instances of objects will not be replicated automatically.</span></span> <span data-ttu-id="b267b-202">您必須重新 hello 物件插入回 hello 字典，或使用其中一種 hello*更新*hello 字典上的方法。</span><span class="sxs-lookup"><span data-stu-id="b267b-202">You must re-insert hello object back into hello dictionary or use one of hello *update* methods on hello dictionary.</span></span>

<span data-ttu-id="b267b-203">hello 可靠狀態管理員會為您管理可靠的集合。</span><span class="sxs-lookup"><span data-stu-id="b267b-203">hello Reliable State Manager manages Reliable Collections for you.</span></span> <span data-ttu-id="b267b-204">您可以只要求 hello 可靠狀態管理員可靠的集合名稱在任何時候，而且在任何地方在您的服務。</span><span class="sxs-lookup"><span data-stu-id="b267b-204">You can simply ask hello Reliable State Manager for a reliable collection by name at any time and at any place in your service.</span></span> <span data-ttu-id="b267b-205">hello 可靠狀態管理員可確保重新取得的參考。</span><span class="sxs-lookup"><span data-stu-id="b267b-205">hello Reliable State Manager ensures that you get a reference back.</span></span> <span data-ttu-id="b267b-206">我們不建議您儲存參考 tooreliable 集合執行個體中的類別成員變數或屬性。</span><span class="sxs-lookup"><span data-stu-id="b267b-206">We don't recommended that you save references tooreliable collection instances in class member variables or properties.</span></span> <span data-ttu-id="b267b-207">特別注意，必須進行設定 hello 參考的 tooensure tooan 執行個體隨時 hello 服務生命週期中。</span><span class="sxs-lookup"><span data-stu-id="b267b-207">Special care must be taken tooensure that hello reference is set tooan instance at all times in hello service lifecycle.</span></span> <span data-ttu-id="b267b-208">hello 可靠狀態管理員處理這項工作，並針對重複的瀏覽進行最佳化。</span><span class="sxs-lookup"><span data-stu-id="b267b-208">hello Reliable State Manager handles this work for you, and it's optimized for repeat visits.</span></span>

### <a name="transactional-and-asynchronous-operations"></a><span data-ttu-id="b267b-209">交易式和非同步作業</span><span class="sxs-lookup"><span data-stu-id="b267b-209">Transactional and asynchronous operations</span></span>
```C#
using (ITransaction tx = this.StateManager.CreateTransaction())
{
    var result = await myDictionary.TryGetValueAsync(tx, "Counter-1");

    await myDictionary.AddOrUpdateAsync(tx, "Counter-1", 0, (k, v) => ++v);

    await tx.CommitAsync();
}
```

<span data-ttu-id="b267b-210">可靠的集合都具有許多 hello 相同的作業，其`System.Collections.Generic`和`System.Collections.Concurrent`對應項目，除非 LINQ。</span><span class="sxs-lookup"><span data-stu-id="b267b-210">Reliable Collections have many of hello same operations that their `System.Collections.Generic` and `System.Collections.Concurrent` counterparts do, except LINQ.</span></span> <span data-ttu-id="b267b-211">可靠的集合上的作業是非同步的。</span><span class="sxs-lookup"><span data-stu-id="b267b-211">Operations on Reliable Collections are asynchronous.</span></span> <span data-ttu-id="b267b-212">這是因為與可靠的集合寫入作業執行 I/O 作業 tooreplicate 和保存資料 toodisk。</span><span class="sxs-lookup"><span data-stu-id="b267b-212">This is because write operations with Reliable Collections perform I/O operations tooreplicate and persist data toodisk.</span></span>

<span data-ttu-id="b267b-213">可靠的集合作業為「交易式」 作業，因此您可以在多個可靠的集合和作業之間維持狀態的一致。</span><span class="sxs-lookup"><span data-stu-id="b267b-213">Reliable Collection operations are *transactional*, so that you can keep state consistent across multiple Reliable Collections and operations.</span></span> <span data-ttu-id="b267b-214">比方說，您可能會清除佇列工作項目從可靠的佇列、 上，執行作業和可靠的字典，全部都在單一交易中儲存 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="b267b-214">For example, you may dequeue a work item from a Reliable Queue, perform an operation on it, and save hello result in a Reliable Dictionary, all within a single transaction.</span></span> <span data-ttu-id="b267b-215">這會被視為不可部分完成的作業，而且它不保證是 hello 整個作業會成功，或 hello 整個作業會回復。</span><span class="sxs-lookup"><span data-stu-id="b267b-215">This is treated as an atomic operation, and it guarantees that either hello entire operation will succeed or hello entire operation will roll back.</span></span> <span data-ttu-id="b267b-216">如果您清除佇列 hello 項目之後，就會發生錯誤，但儲存 hello 結果前，回復 hello 整個交易，並 hello 項目保持開啟 hello 佇列中進行處理。</span><span class="sxs-lookup"><span data-stu-id="b267b-216">If an error occurs after you dequeue hello item but before you save hello result, hello entire transaction is rolled back and hello item remains in hello queue for processing.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="b267b-217">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="b267b-217">Run hello application</span></span>
<span data-ttu-id="b267b-218">我們現在傳回 toohello *HelloWorld*應用程式。</span><span class="sxs-lookup"><span data-stu-id="b267b-218">We now return toohello *HelloWorld* application.</span></span> <span data-ttu-id="b267b-219">您現在可以建置並部署您的服務。</span><span class="sxs-lookup"><span data-stu-id="b267b-219">You can now build and deploy your services.</span></span> <span data-ttu-id="b267b-220">當您按**F5**，您的應用程式將會建置及部署 tooyour 本機叢集。</span><span class="sxs-lookup"><span data-stu-id="b267b-220">When you press **F5**, your application will be built and deployed tooyour local cluster.</span></span>

<span data-ttu-id="b267b-221">Hello 服務開始執行之後，您可以檢視中的 hello 產生事件的 Windows 追蹤 (ETW) 事件**診斷事件**視窗。</span><span class="sxs-lookup"><span data-stu-id="b267b-221">After hello services start running, you can view hello generated Event Tracing for Windows (ETW) events in a **Diagnostic Events** window.</span></span> <span data-ttu-id="b267b-222">請注意，顯示 hello 事件從 hello 無狀態服務和 hello hello 應用程式中可設定狀態的服務。</span><span class="sxs-lookup"><span data-stu-id="b267b-222">Note that hello events displayed are from both hello stateless service and hello stateful service in hello application.</span></span> <span data-ttu-id="b267b-223">您可以暫停 hello 資料流，依序按一下 hello**暫停** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b267b-223">You can pause hello stream by clicking hello **Pause** button.</span></span> <span data-ttu-id="b267b-224">接著，您可以檢查 hello 訊息詳細資料的方法是展開該訊息。</span><span class="sxs-lookup"><span data-stu-id="b267b-224">You can then examine hello details of a message by expanding that message.</span></span>

> [!NOTE]
> <span data-ttu-id="b267b-225">執行 hello 應用程式之前，請確定您已執行的本機開發叢集。</span><span class="sxs-lookup"><span data-stu-id="b267b-225">Before you run hello application, make sure that you have a local development cluster running.</span></span> <span data-ttu-id="b267b-226">簽出 hello[入門指南](service-fabric-get-started.md)如需有關設定本機環境資訊。</span><span class="sxs-lookup"><span data-stu-id="b267b-226">Check out hello [getting started guide](service-fabric-get-started.md) for information on setting up your local environment.</span></span>
> 
> 

![在 Visual Studio 中檢視診斷事件](media/service-fabric-reliable-services-quick-start/hello-stateful-Output.png)

## <a name="next-steps"></a><span data-ttu-id="b267b-228">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b267b-228">Next steps</span></span>
[<span data-ttu-id="b267b-229">在 Visual Studio 中偵錯 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="b267b-229">Debug your Service Fabric application in Visual Studio</span></span>](service-fabric-debugging-your-application.md)

[<span data-ttu-id="b267b-230">開始使用：Service Fabric Web API 服務與 OWIN 自我裝載 | Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="b267b-230">Get started: Service Fabric Web API services with OWIN self-hosting</span></span>](service-fabric-reliable-services-communication-webapi.md)

[<span data-ttu-id="b267b-231">深入了解可靠的集合</span><span class="sxs-lookup"><span data-stu-id="b267b-231">Learn more about Reliable Collections</span></span>](service-fabric-reliable-services-reliable-collections.md)

[<span data-ttu-id="b267b-232">部署應用程式</span><span class="sxs-lookup"><span data-stu-id="b267b-232">Deploy an application</span></span>](service-fabric-deploy-remove-applications.md)

[<span data-ttu-id="b267b-233">應用程式升級</span><span class="sxs-lookup"><span data-stu-id="b267b-233">Application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="b267b-234">Reliable Services 的開發人員參考資料</span><span class="sxs-lookup"><span data-stu-id="b267b-234">Developer reference for Reliable Services</span></span>](https://msdn.microsoft.com/library/azure/dn706529.aspx)

