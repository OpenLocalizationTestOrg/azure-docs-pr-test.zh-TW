---
title: "在 C# 中建立第一個 Service Fabric 應用程式 | Microsoft Docs"
description: "概述使用無狀態與具狀態服務來建立 Microsoft Azure Service Fabric 應用程式。"
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
ms.openlocfilehash: 813021d6239ae3cf79bb84b78f77e39c9e0783f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-reliable-services"></a><span data-ttu-id="e6e5a-103">開始使用 Reliable Service</span><span class="sxs-lookup"><span data-stu-id="e6e5a-103">Get started with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e6e5a-104">Windows 上的 C# </span><span class="sxs-lookup"><span data-stu-id="e6e5a-104">C# on Windows</span></span>](service-fabric-reliable-services-quick-start.md)
> * [<span data-ttu-id="e6e5a-105">Linux 上的 Java</span><span class="sxs-lookup"><span data-stu-id="e6e5a-105">Java on Linux</span></span>](service-fabric-reliable-services-quick-start-java.md)
> 
> 

<span data-ttu-id="e6e5a-106">Azure Service Fabric 應用程式包含一個或多個執行您的程式碼的服務。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-106">An Azure Service Fabric application contains one or more services that run your code.</span></span> <span data-ttu-id="e6e5a-107">本指南說明如何透過 [Reliable Services](service-fabric-reliable-services-introduction.md)同時建立無狀態與具狀態的 Service Fabric 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-107">This guide shows you how to create both stateless and stateful Service Fabric applications with [Reliable Services](service-fabric-reliable-services-introduction.md).</span></span>  <span data-ttu-id="e6e5a-108">此 Microsoft Virtual Academy 影片也示範如何建立無狀態的 Reliable Service：<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965"></span><span class="sxs-lookup"><span data-stu-id="e6e5a-108">This Microsoft Virtual Academy video also shows you how to create a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965"></span></span>  
<img src="./media/service-fabric-reliable-services-quick-start/ReliableServicesVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="basic-concepts"></a><span data-ttu-id="e6e5a-109">基本概念</span><span class="sxs-lookup"><span data-stu-id="e6e5a-109">Basic concepts</span></span>
<span data-ttu-id="e6e5a-110">若要開始使用 Reliable Services，您只需要了解幾個基本概念：</span><span class="sxs-lookup"><span data-stu-id="e6e5a-110">To get started with Reliable Services, you only need to understand a few basic concepts:</span></span>

* <span data-ttu-id="e6e5a-111">**服務類型**：這是您的服務實作。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-111">**Service type**: This is your service implementation.</span></span> <span data-ttu-id="e6e5a-112">它是由您撰寫的類別定義，它會擴充 `StatelessService` 與其中使用的任何其他程式碼或相依性，以及名稱與版本號碼。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-112">It is defined by the class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span></span>
* <span data-ttu-id="e6e5a-113">**具名服務執行個體**：若要執行您的服務，可以建立您服務類型的具名執行個體，很像您建立類別類型的物件執行個體一樣。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-113">**Named service instance**: To run your service, you create named instances of your service type, much like you create object instances of a class type.</span></span> <span data-ttu-id="e6e5a-114">服務執行個體的名稱格式是使用「fabric:/」配置的 URI，例如「fabric:/MyApp/MyService」。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-114">A service instance has a name in the form of a URI using the "fabric:/" scheme, such as "fabric:/MyApp/MyService".</span></span>
* <span data-ttu-id="e6e5a-115">**服務主機**：您建立的具名服務執行個體需要在主機處理序內部執行。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-115">**Service host**: The named service instances you create need to run inside a host process.</span></span> <span data-ttu-id="e6e5a-116">服務主機只是您服務的執行個體可執行所在的程序。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-116">The service host is just a process where instances of your service can run.</span></span>
* <span data-ttu-id="e6e5a-117">**服務註冊**：註冊可將所有項目結合在一起。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-117">**Service registration**: Registration brings everything together.</span></span> <span data-ttu-id="e6e5a-118">服務類型必須在服務主機的 Service Fabric 執行階段中註冊，以允許 Service Fabric 建立其執行個體來執行。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-118">The service type must be registered with the Service Fabric runtime in a service host to allow Service Fabric to create instances of it to run.</span></span>  

## <a name="create-a-stateless-service"></a><span data-ttu-id="e6e5a-119">建立無狀態服務</span><span class="sxs-lookup"><span data-stu-id="e6e5a-119">Create a stateless service</span></span>
<span data-ttu-id="e6e5a-120">無狀態服務是目前在雲端應用程式中做為基準的服務類型。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-120">A stateless service is a type of service that is currently the norm in cloud applications.</span></span> <span data-ttu-id="e6e5a-121">服務會視為無狀態，因為服務本身不包含需要可靠地儲存或設為高度可用的資料。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-121">It is considered stateless because the service itself does not contain data that needs to be stored reliably or made highly available.</span></span> <span data-ttu-id="e6e5a-122">如果無狀態服務的執行個體關閉，其所有內部狀態都會遺失。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-122">If an instance of a stateless service shuts down, all of its internal state is lost.</span></span> <span data-ttu-id="e6e5a-123">在此類型的服務中，狀態必須保存到外部存放區，例如 Azure 資料表或 SQL 資料庫中，才能成為高度可用且可靠。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-123">In this type of service, state must be persisted to an external store, such as Azure Tables or a SQL database, for it to be made highly available and reliable.</span></span>

<span data-ttu-id="e6e5a-124">以管理員身分啟動 Visual Studio 2015 或 Visual Studio 2017，並建立新的 Service Fabric 應用程式專案，命名為 HelloWorld：</span><span class="sxs-lookup"><span data-stu-id="e6e5a-124">Launch Visual Studio 2015 or Visual Studio 2017 as an administrator, and create a new Service Fabric application project named *HelloWorld*:</span></span>

![使用新增專案對話方塊來建立新的 Service Fabric 應用程式](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject.png)

<span data-ttu-id="e6e5a-126">然後建立名為 *HelloWorldStateless*的無狀態服務專案：</span><span class="sxs-lookup"><span data-stu-id="e6e5a-126">Then create a stateless service project named *HelloWorldStateless*:</span></span>

![在第二個對話方塊中，建立無狀態服務專案](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject2.png)

<span data-ttu-id="e6e5a-128">您的方案現在包含兩個專案：</span><span class="sxs-lookup"><span data-stu-id="e6e5a-128">Your solution now contains two projects:</span></span>

* <span data-ttu-id="e6e5a-129">*HelloWorld*。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-129">*HelloWorld*.</span></span> <span data-ttu-id="e6e5a-130">這是包含您*服務*的*應用程式*專案。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-130">This is the *application* project that contains your *services*.</span></span> <span data-ttu-id="e6e5a-131">它也包含描述應用程式的應用程式資訊清單，以及一些幫助您部署應用程式的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-131">It also contains the application manifest that describes the application, as well as a number of PowerShell scripts that help you to deploy your application.</span></span>
* <span data-ttu-id="e6e5a-132">*HelloWorldStateless*。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-132">*HelloWorldStateless*.</span></span> <span data-ttu-id="e6e5a-133">這是服務專案。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-133">This is the service project.</span></span> <span data-ttu-id="e6e5a-134">它包含無狀態服務實作。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-134">It contains the stateless service implementation.</span></span>

## <a name="implement-the-service"></a><span data-ttu-id="e6e5a-135">實作服務</span><span class="sxs-lookup"><span data-stu-id="e6e5a-135">Implement the service</span></span>
<span data-ttu-id="e6e5a-136">在服務專案中開啟 **HelloWorldStateless.cs** 檔案。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-136">Open the **HelloWorldStateless.cs** file in the service project.</span></span> <span data-ttu-id="e6e5a-137">在 Service Fabric 中，服務可以執行任何商務邏輯。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-137">In Service Fabric, a service can run any business logic.</span></span> <span data-ttu-id="e6e5a-138">服務 API 為您的程式碼提供兩個進入點：</span><span class="sxs-lookup"><span data-stu-id="e6e5a-138">The service API provides two entry points for your code:</span></span>

* <span data-ttu-id="e6e5a-139">開放式的進入點方法，稱為 *RunAsync*，您可以在這裡開始執行任何工作負載，包括長時間執行的計算工作負載。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-139">An open-ended entry point method, called *RunAsync*, where you can begin executing any workloads, including long-running compute workloads.</span></span>

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    ...
}
```

* <span data-ttu-id="e6e5a-140">通訊進入點，您可以在這裡插入選擇的通訊堆疊，例如 ASP.NET Core。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-140">A communication entry point where you can plug in your communication stack of choice, such as ASP.NET Core.</span></span> <span data-ttu-id="e6e5a-141">這就是您可以開始接收來自使用者和其他服務要求的地方。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-141">This is where you can start receiving requests from users and other services.</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}
```

<span data-ttu-id="e6e5a-142">在本教學課程中，我們將著重在 `RunAsync()` 進入點方法。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-142">In this tutorial, we will focus on the `RunAsync()` entry point method.</span></span> <span data-ttu-id="e6e5a-143">這就是您可以立即開始執行程式碼的地方。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-143">This is where you can immediately start running your code.</span></span>
<span data-ttu-id="e6e5a-144">專案範本包括 `RunAsync()` 的實作範例，它會遞增一個循環計數。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-144">The project template includes a sample implementation of `RunAsync()` that increments a rolling count.</span></span>

> [!NOTE]
> <span data-ttu-id="e6e5a-145">如需有關如何使用通訊堆疊的詳細資訊，請參閱 [Service Fabric Web API 服務與 OWIN 自我裝載](service-fabric-reliable-services-communication-webapi.md)</span><span class="sxs-lookup"><span data-stu-id="e6e5a-145">For details about how to work with a communication stack, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md)</span></span>
> 
> 

### <a name="runasync"></a><span data-ttu-id="e6e5a-146">RunAsync</span><span class="sxs-lookup"><span data-stu-id="e6e5a-146">RunAsync</span></span>
```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace the following sample code with your own logic
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

<span data-ttu-id="e6e5a-147">當服務的執行個體已放置並且可以執行時，平台會呼叫這個方法。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-147">The platform calls this method when an instance of a service is placed and ready to execute.</span></span> <span data-ttu-id="e6e5a-148">針對無狀態服務，這僅表示開啟服務執行個體的時間。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-148">For a stateless service, that simply means when the service instance is opened.</span></span> <span data-ttu-id="e6e5a-149">會提供取消語彙基元以協調服務執行個體何時需要關閉。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-149">A cancellation token is provided to coordinate when your service instance needs to be closed.</span></span> <span data-ttu-id="e6e5a-150">在 Service Fabric 中，服務執行個體的開啟/關閉循環可能會在整個服務存留期中發生許多次。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-150">In Service Fabric, this open/close cycle of a service instance can occur many times over the lifetime of the service as a whole.</span></span> <span data-ttu-id="e6e5a-151">發生這種情形的原因有很多，包括：</span><span class="sxs-lookup"><span data-stu-id="e6e5a-151">This can happen for various reasons, including:</span></span>

* <span data-ttu-id="e6e5a-152">系統可能為了資源平衡移動您的服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-152">The system moves your service instances for resource balancing.</span></span>
* <span data-ttu-id="e6e5a-153">在您的程式碼中發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-153">Faults occur in your code.</span></span>
* <span data-ttu-id="e6e5a-154">應用程式或系統已升級。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-154">The application or system is upgraded.</span></span>
* <span data-ttu-id="e6e5a-155">基礎硬體發生中斷。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-155">The underlying hardware experiences an outage.</span></span>

<span data-ttu-id="e6e5a-156">此協調流程是由系統管理，可讓您的服務維持高度可用且正確平衡。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-156">This orchestration is managed by the system to keep your service highly available and properly balanced.</span></span>

<span data-ttu-id="e6e5a-157">`RunAsync()` 不應該同步封鎖。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-157">`RunAsync()` should not block synchronously.</span></span> <span data-ttu-id="e6e5a-158">RunAsync 的實作應該傳回工作或等待任何長時間執行或封鎖作業，以允許執行階段繼續執行。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-158">Your implementation of RunAsync should return a Task or await on any long-running or blocking operations to allow the runtime to continue.</span></span> <span data-ttu-id="e6e5a-159">請注意，在上一個範例的 `while(true)` 迴圈中，會使用 Task-returning `await Task.Delay()`。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-159">Note in the `while(true)` loop in the previous example, a Task-returning `await Task.Delay()` is used.</span></span> <span data-ttu-id="e6e5a-160">如果您的工作負載必須同步封鎖，您應該使用 `Task.Run()` 在您的 `RunAsync` 實作中排定一個新的工作。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-160">If your workload must block synchronously, you should schedule a new Task with `Task.Run()` in your `RunAsync` implementation.</span></span>

<span data-ttu-id="e6e5a-161">取消您的工作負載是由所提供的取消語彙基元協調的協同努力。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-161">Cancellation of your workload is a cooperative effort orchestrated by the provided cancellation token.</span></span> <span data-ttu-id="e6e5a-162">系統會先等待您工作結束 (成功完成、取消或錯誤) 再繼續。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-162">The system will wait for your task to end (by successful completion, cancellation, or fault) before it moves on.</span></span> <span data-ttu-id="e6e5a-163">系統要求取消時，務必接受取消權杖、完成任何工作，並儘快結束 `RunAsync()`。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-163">It is important to honor the cancellation token, finish any work, and exit `RunAsync()` as quickly as possible when the system requests cancellation.</span></span>

<span data-ttu-id="e6e5a-164">在這個無狀態服務範例中，計數會儲存在本機變數。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-164">In this stateless service example, the count is stored in a local variable.</span></span> <span data-ttu-id="e6e5a-165">但是，因為這是無狀態服務，所儲存的值只針對其服務執行個體的目前生命週期而存在。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-165">But because this is a stateless service, the value that's stored exists only for the current lifecycle of its service instance.</span></span> <span data-ttu-id="e6e5a-166">當服務移動或重新啟動時，值將會遺失。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-166">When the service moves or restarts, the value is lost.</span></span>

## <a name="create-a-stateful-service"></a><span data-ttu-id="e6e5a-167">建立具狀態服務</span><span class="sxs-lookup"><span data-stu-id="e6e5a-167">Create a stateful service</span></span>
<span data-ttu-id="e6e5a-168">Service Fabric 導入了一種可設定狀態的新服務。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-168">Service Fabric introduces a new kind of service that is stateful.</span></span> <span data-ttu-id="e6e5a-169">具狀態服務能夠可靠地在服務本身維持狀態，和使用它的程式碼共置。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-169">A stateful service can maintain state reliably within the service itself, co-located with the code that's using it.</span></span> <span data-ttu-id="e6e5a-170">狀態是由 Service Fabric 設為高度可用，而不需要將狀態保存到外部存放區。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-170">State is made highly available by Service Fabric without the need to persist state to an external store.</span></span>

<span data-ttu-id="e6e5a-171">若要將計數器值從無狀態轉換成高度可用且持續，即使服務移動或重新啟動亦然，您需要具狀態服務。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-171">To convert a counter value from stateless to highly available and persistent, even when the service moves or restarts, you need a stateful service.</span></span>

<span data-ttu-id="e6e5a-172">在同一個 *HelloWorld* 應用程式中，於應用程式專案中的服務參考上按一下滑鼠右鍵並選取 [新增] -> [新增 Service Fabric 服務]，以加入新的服務。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-172">In the same *HelloWorld* application, you can add a new service by right-clicking on the Services references in the application project and selecting **Add ->  New Service Fabric Service**.</span></span>

![將服務加入 Service Fabric 應用程式](media/service-fabric-reliable-services-quick-start/hello-stateful-NewService.png)

<span data-ttu-id="e6e5a-174">選取 [具狀態服務]  並將它命名為 *HelloWorldStateful*。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-174">Select **Stateful Service** and name it *HelloWorldStateful*.</span></span> <span data-ttu-id="e6e5a-175">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-175">Click **OK**.</span></span>

![使用新增專案對話方塊來建立新的 Service Fabric 具狀態服務](media/service-fabric-reliable-services-quick-start/hello-stateful-NewProject.png)

<span data-ttu-id="e6e5a-177">您的應用程式現在應該有兩個服務：無狀態服務 *HelloWorldStateless*和具狀態服務 *HelloWorldStateful*。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-177">Your application should now have two services: the stateless service *HelloWorldStateless* and the stateful service *HelloWorldStateful*.</span></span>

<span data-ttu-id="e6e5a-178">具狀態服務與無狀態服務具有相同的進入點。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-178">A stateful service has the same entry points as a stateless service.</span></span> <span data-ttu-id="e6e5a-179">主要差異在於可以可靠地儲存狀態之狀態供應器  的可用性。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-179">The main difference is the availability of a *state provider* that can store state reliably.</span></span> <span data-ttu-id="e6e5a-180">Service Fabric 隨附稱為 [可靠的集合](service-fabric-reliable-services-reliable-collections.md)的狀態供應器實作，它可讓您透過可靠狀態管理員建立複寫的資料結構。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-180">Service Fabric comes with a state provider implementation called [Reliable Collections](service-fabric-reliable-services-reliable-collections.md), which lets you create replicated data structures through the Reliable State Manager.</span></span> <span data-ttu-id="e6e5a-181">具狀態可靠服務預設會使用此狀態供應器。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-181">A stateful Reliable Service uses this state provider by default.</span></span>

<span data-ttu-id="e6e5a-182">在 HelloWorldStateful  中開啟 *HelloWorldStateful.cs*，其中包含下列 RunAsync 方法：</span><span class="sxs-lookup"><span data-stu-id="e6e5a-182">Open **HelloWorldStateful.cs** in *HelloWorldStateful*, which contains the following RunAsync method:</span></span>

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace the following sample code with your own logic
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

            // If an exception is thrown before calling CommitAsync, the transaction aborts, all changes are
            // discarded, and nothing is saved to the secondary replicas.
            await tx.CommitAsync();
        }

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
```

### <a name="runasync"></a><span data-ttu-id="e6e5a-183">RunAsync</span><span class="sxs-lookup"><span data-stu-id="e6e5a-183">RunAsync</span></span>
<span data-ttu-id="e6e5a-184">`RunAsync()` 在具狀態和無狀態服務中的運作方式類似。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-184">`RunAsync()` operates similarly in stateful and stateless services.</span></span> <span data-ttu-id="e6e5a-185">只不過在具狀態服務中，平台會代替您執行額外的工作，然後才執行 `RunAsync()`。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-185">However, in a stateful service, the platform performs additional work on your behalf before it executes `RunAsync()`.</span></span> <span data-ttu-id="e6e5a-186">這項工作包含確保可靠狀態管理員和可靠的集合可以使用。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-186">This work can include ensuring that the Reliable State Manager and Reliable Collections are ready to use.</span></span>

### <a name="reliable-collections-and-the-reliable-state-manager"></a><span data-ttu-id="e6e5a-187">可靠的集合與可靠狀態管理員</span><span class="sxs-lookup"><span data-stu-id="e6e5a-187">Reliable Collections and the Reliable State Manager</span></span>
```csharp
var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
```

<span data-ttu-id="e6e5a-188">[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) 是一個字典實作，您可以在服務中可靠地儲存狀態。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-188">[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) is a dictionary implementation that you can use to reliably store state in the service.</span></span> <span data-ttu-id="e6e5a-189">有了 Service Fabric 和可靠的集合，您可以直接在服務中儲存資料，而不需要外部的持續性存放區。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-189">With Service Fabric and Reliable Collections, you can store data directly in your service without the need for an external persistent store.</span></span> <span data-ttu-id="e6e5a-190">可靠的集合可讓您的資料具備高可用性。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-190">Reliable Collections make your data highly available.</span></span> <span data-ttu-id="e6e5a-191">Service Fabric 會藉由為您建立與管理服務的多個複本  來完成此作業。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-191">Service Fabric accomplishes this by creating and managing multiple *replicas* of your service for you.</span></span> <span data-ttu-id="e6e5a-192">它也提供 API 讓管理這些複本和其狀態轉換的複雜性抽象化。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-192">It also provides an API that abstracts away the complexities of managing those replicas and their state transitions.</span></span>

<span data-ttu-id="e6e5a-193">可靠的集合可以儲存任何 .NET 類型 (包括您的自訂類型)，不過有幾個需要注意的事項：</span><span class="sxs-lookup"><span data-stu-id="e6e5a-193">Reliable Collections can store any .NET type, including your custom types, with a couple of caveats:</span></span>

* <span data-ttu-id="e6e5a-194">Service Fabric 藉由在節點之間複寫  狀態來使您的狀態高度可用，而可靠的集合會將您的資料儲存到每個複本上的本機磁碟。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-194">Service Fabric makes your state highly available by *replicating* state across nodes, and Reliable Collections store your data to local disk on each replica.</span></span> <span data-ttu-id="e6e5a-195">這表示所有儲存在可靠的集合中的項目必須可序列化 。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-195">This means that everything that is stored in Reliable Collections must be *serializable*.</span></span> <span data-ttu-id="e6e5a-196">根據預設，可靠的集合使用 [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) 進行序列化，因此在您使用預設序列化程式時，請務必確定您的類型受到[資料合約序列化程式支援](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-196">By default, Reliable Collections use [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) for serialization, so it's important to make sure that your types are [supported by the Data Contract Serializer](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) when you use the default serializer.</span></span>
* <span data-ttu-id="e6e5a-197">當您在可靠的集合上認可交易時，物件會複寫以獲得高可用性。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-197">Objects are replicated for high availability when you commit transactions on Reliable Collections.</span></span> <span data-ttu-id="e6e5a-198">儲存在可靠集合中的物件會保留在服務中的本機記憶體。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-198">Objects stored in Reliable Collections are kept in local memory in your service.</span></span> <span data-ttu-id="e6e5a-199">這表示您有物件的本機參考。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-199">This means that you have a local reference to the object.</span></span>
  
   <span data-ttu-id="e6e5a-200">很重要的一點是，您不要改變那些物件的本機執行個體而不在交易中的可靠集合上執行更新作業。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-200">It is important that you do not mutate local instances of those objects without performing an update operation on the reliable collection in a transaction.</span></span> <span data-ttu-id="e6e5a-201">這是因為不會自動複寫對本機物件執行個體所做的變更。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-201">This is because changes to local instances of objects will not be replicated automatically.</span></span> <span data-ttu-id="e6e5a-202">您必須將物件重新插入到字典中，或在字典上使用其中一個更新  方法。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-202">You must re-insert the object back into the dictionary or use one of the *update* methods on the dictionary.</span></span>

<span data-ttu-id="e6e5a-203">可靠狀態管理員會為您管理可靠的集合。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-203">The Reliable State Manager manages Reliable Collections for you.</span></span> <span data-ttu-id="e6e5a-204">在您的服務中隨時隨地，您只需要以名稱向可靠狀態管理員要求可靠的集合。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-204">You can simply ask the Reliable State Manager for a reliable collection by name at any time and at any place in your service.</span></span> <span data-ttu-id="e6e5a-205">可靠狀態管理員會確保您取回參考。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-205">The Reliable State Manager ensures that you get a reference back.</span></span> <span data-ttu-id="e6e5a-206">不建議您將可靠集合執行個體的參考儲存在類別成員變數或屬性中。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-206">We don't recommended that you save references to reliable collection instances in class member variables or properties.</span></span> <span data-ttu-id="e6e5a-207">請特別小心以確保在服務生命週期中隨時將參考設定為執行個體。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-207">Special care must be taken to ensure that the reference is set to an instance at all times in the service lifecycle.</span></span> <span data-ttu-id="e6e5a-208">可靠狀態管理員會為您處理這項工作，並且針對重複造訪最佳化。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-208">The Reliable State Manager handles this work for you, and it's optimized for repeat visits.</span></span>

### <a name="transactional-and-asynchronous-operations"></a><span data-ttu-id="e6e5a-209">交易式和非同步作業</span><span class="sxs-lookup"><span data-stu-id="e6e5a-209">Transactional and asynchronous operations</span></span>
```C#
using (ITransaction tx = this.StateManager.CreateTransaction())
{
    var result = await myDictionary.TryGetValueAsync(tx, "Counter-1");

    await myDictionary.AddOrUpdateAsync(tx, "Counter-1", 0, (k, v) => ++v);

    await tx.CommitAsync();
}
```

<span data-ttu-id="e6e5a-210">可靠的集合與其 `System.Collections.Generic` 和 `System.Collections.Concurrent` 對應項目具有許多相同的作業 (LINQ 除外)。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-210">Reliable Collections have many of the same operations that their `System.Collections.Generic` and `System.Collections.Concurrent` counterparts do, except LINQ.</span></span> <span data-ttu-id="e6e5a-211">可靠的集合上的作業是非同步的。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-211">Operations on Reliable Collections are asynchronous.</span></span> <span data-ttu-id="e6e5a-212">這是因為具備可靠集合的寫入作業執行 I/O 作業以將資料複寫並保存至磁碟。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-212">This is because write operations with Reliable Collections perform I/O operations to replicate and persist data to disk.</span></span>

<span data-ttu-id="e6e5a-213">可靠的集合作業為「交易式」 作業，因此您可以在多個可靠的集合和作業之間維持狀態的一致。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-213">Reliable Collection operations are *transactional*, so that you can keep state consistent across multiple Reliable Collections and operations.</span></span> <span data-ttu-id="e6e5a-214">比方說，您可能會從可靠佇列取出一個工作項目、對它執行作業，然後將結果儲存在可靠字典中，全都在單一交易中完成。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-214">For example, you may dequeue a work item from a Reliable Queue, perform an operation on it, and save the result in a Reliable Dictionary, all within a single transaction.</span></span> <span data-ttu-id="e6e5a-215">這會被視為不可部分完成的作業，而且它可保證整個作業都會成功，或整個作業都會回復。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-215">This is treated as an atomic operation, and it guarantees that either the entire operation will succeed or the entire operation will roll back.</span></span> <span data-ttu-id="e6e5a-216">如果您從佇列取消項目之後，但在您儲存結果之前發生錯誤，那麼會回復整個交易，且項目會保持在佇列中進行處理。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-216">If an error occurs after you dequeue the item but before you save the result, the entire transaction is rolled back and the item remains in the queue for processing.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="e6e5a-217">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="e6e5a-217">Run the application</span></span>
<span data-ttu-id="e6e5a-218">現在我們回到 HelloWorld  應用程式。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-218">We now return to the *HelloWorld* application.</span></span> <span data-ttu-id="e6e5a-219">您現在可以建置並部署您的服務。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-219">You can now build and deploy your services.</span></span> <span data-ttu-id="e6e5a-220">當您按下 **F5**，您的應用程式會建置並部署至本機叢集。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-220">When you press **F5**, your application will be built and deployed to your local cluster.</span></span>

<span data-ttu-id="e6e5a-221">服務開始執行之後，您可以在 [診斷事件]  視窗中檢視產生的 Windows 事件追蹤 (ETW) 事件。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-221">After the services start running, you can view the generated Event Tracing for Windows (ETW) events in a **Diagnostic Events** window.</span></span> <span data-ttu-id="e6e5a-222">請注意，應用程式中會同時顯示無狀態服務和具狀態服務的事件。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-222">Note that the events displayed are from both the stateless service and the stateful service in the application.</span></span> <span data-ttu-id="e6e5a-223">您可以按一下 [暫停]  按鈕來暫停串流。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-223">You can pause the stream by clicking the **Pause** button.</span></span> <span data-ttu-id="e6e5a-224">然後，您可以藉由展開訊息來檢查訊息的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-224">You can then examine the details of a message by expanding that message.</span></span>

> [!NOTE]
> <span data-ttu-id="e6e5a-225">在您執行應用程式之前，請確定您有執行中的本機開發叢集。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-225">Before you run the application, make sure that you have a local development cluster running.</span></span> <span data-ttu-id="e6e5a-226">查看 [入門指南](service-fabric-get-started.md) 以取得設定您的本機環境的資訊。</span><span class="sxs-lookup"><span data-stu-id="e6e5a-226">Check out the [getting started guide](service-fabric-get-started.md) for information on setting up your local environment.</span></span>
> 
> 

![在 Visual Studio 中檢視診斷事件](media/service-fabric-reliable-services-quick-start/hello-stateful-Output.png)

## <a name="next-steps"></a><span data-ttu-id="e6e5a-228">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e6e5a-228">Next steps</span></span>
[<span data-ttu-id="e6e5a-229">在 Visual Studio 中偵錯 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="e6e5a-229">Debug your Service Fabric application in Visual Studio</span></span>](service-fabric-debugging-your-application.md)

[<span data-ttu-id="e6e5a-230">開始使用：Service Fabric Web API 服務與 OWIN 自我裝載 | Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="e6e5a-230">Get started: Service Fabric Web API services with OWIN self-hosting</span></span>](service-fabric-reliable-services-communication-webapi.md)

[<span data-ttu-id="e6e5a-231">深入了解可靠的集合</span><span class="sxs-lookup"><span data-stu-id="e6e5a-231">Learn more about Reliable Collections</span></span>](service-fabric-reliable-services-reliable-collections.md)

[<span data-ttu-id="e6e5a-232">部署應用程式</span><span class="sxs-lookup"><span data-stu-id="e6e5a-232">Deploy an application</span></span>](service-fabric-deploy-remove-applications.md)

[<span data-ttu-id="e6e5a-233">應用程式升級</span><span class="sxs-lookup"><span data-stu-id="e6e5a-233">Application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="e6e5a-234">Reliable Services 的開發人員參考資料</span><span class="sxs-lookup"><span data-stu-id="e6e5a-234">Developer reference for Reliable Services</span></span>](https://msdn.microsoft.com/library/azure/dn706529.aspx)

