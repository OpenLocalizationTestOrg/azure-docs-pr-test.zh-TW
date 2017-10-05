---
title: "使用 C# 建立您的第一個動作項目型 Azure 微服務 | Microsoft Docs"
description: "本教學課程將引導您使用 Service Fabric Reliable Actors，建立、偵錯及部署簡易動作項目型服務的步驟。"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d4aebe72-1551-4062-b1eb-54d83297f139
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 3f447e049ccd33c77f422e8aa703ad6646f9ffa2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-reliable-actors"></a><span data-ttu-id="e7c40-103">開始使用 Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="e7c40-103">Getting started with Reliable Actors</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e7c40-104">Windows 上的 C# </span><span class="sxs-lookup"><span data-stu-id="e7c40-104">C# on Windows</span></span>](service-fabric-reliable-actors-get-started.md)
> * [<span data-ttu-id="e7c40-105">在 Linux 上使用 Java</span><span class="sxs-lookup"><span data-stu-id="e7c40-105">Java on Linux</span></span>](service-fabric-reliable-actors-get-started-java.md)
> 
> 

<span data-ttu-id="e7c40-106">本文說明 Azure Service Fabric Reliable Actors 的基本概念，並將逐步引導您在 Visual Studio 中建立、偵錯及部署簡單的 Reliable Actor 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e7c40-106">This article explains the basics of Azure Service Fabric Reliable Actors and walks you through creating, debugging, and deploying a simple Reliable Actor application in Visual Studio.</span></span>

## <a name="installation-and-setup"></a><span data-ttu-id="e7c40-107">安裝與設定</span><span class="sxs-lookup"><span data-stu-id="e7c40-107">Installation and setup</span></span>
<span data-ttu-id="e7c40-108">開始之前，確定機器上已設定 Service Fabric 開發環境。</span><span class="sxs-lookup"><span data-stu-id="e7c40-108">Before you start, ensure that you have the Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="e7c40-109">如果需要加以設定，請參閱 [如何設定開發環境](service-fabric-get-started.md)的詳細指示。</span><span class="sxs-lookup"><span data-stu-id="e7c40-109">If you need to set it up, see detailed instructions on [how to set up the development environment](service-fabric-get-started.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="e7c40-110">基本概念</span><span class="sxs-lookup"><span data-stu-id="e7c40-110">Basic concepts</span></span>
<span data-ttu-id="e7c40-111">若要開始使用 Reliable Actors，您只需要了解幾個基本概念：</span><span class="sxs-lookup"><span data-stu-id="e7c40-111">To get started with Reliable Actors, you only need to understand a few basic concepts:</span></span>

* <span data-ttu-id="e7c40-112">**動作項目服務**。</span><span class="sxs-lookup"><span data-stu-id="e7c40-112">**Actor service**.</span></span> <span data-ttu-id="e7c40-113">Reliable Actors 封裝在可在 Service Fabric 基礎結構內部署的 Reliable Services 中。</span><span class="sxs-lookup"><span data-stu-id="e7c40-113">Reliable Actors are packaged in Reliable Services that can be deployed in the Service Fabric infrastructure.</span></span> <span data-ttu-id="e7c40-114">動作項目執行個體會在指定的服務執行個體中啟動。</span><span class="sxs-lookup"><span data-stu-id="e7c40-114">Actor instances are activated in a named service instance.</span></span>
* <span data-ttu-id="e7c40-115">**動作項目註冊**。</span><span class="sxs-lookup"><span data-stu-id="e7c40-115">**Actor registration**.</span></span> <span data-ttu-id="e7c40-116">和 Reliable Services 一樣，Reliable Actor 服務必須向 Service Fabric 執行階段註冊。</span><span class="sxs-lookup"><span data-stu-id="e7c40-116">As with Reliable Services, a Reliable Actor service needs to be registered with the Service Fabric runtime.</span></span> <span data-ttu-id="e7c40-117">此外，動作項目類型必須向 Actor 執行階段註冊。</span><span class="sxs-lookup"><span data-stu-id="e7c40-117">In addition, the actor type needs to be registered with the Actor runtime.</span></span>
* <span data-ttu-id="e7c40-118">**動作項目介面**。</span><span class="sxs-lookup"><span data-stu-id="e7c40-118">**Actor interface**.</span></span> <span data-ttu-id="e7c40-119">動作項目介面用於定義動作項目的強型別公用介面。</span><span class="sxs-lookup"><span data-stu-id="e7c40-119">The actor interface is used to define a strongly typed public interface of an actor.</span></span> <span data-ttu-id="e7c40-120">在 Reliable Actor 模型術語中，動作項目介面定義動作項目可以了解並處理的訊息類型。</span><span class="sxs-lookup"><span data-stu-id="e7c40-120">In the Reliable Actor model terminology, the actor interface defines the types of messages that the actor can understand and process.</span></span> <span data-ttu-id="e7c40-121">其他的動作項目或用戶端應用程式會使用動作項目介面將訊息「傳送」(非同步) 給動作項目。</span><span class="sxs-lookup"><span data-stu-id="e7c40-121">The actor interface is used by other actors and client applications to "send" (asynchronously) messages to the actor.</span></span> <span data-ttu-id="e7c40-122">Reliable Actors 可實作多個介面。</span><span class="sxs-lookup"><span data-stu-id="e7c40-122">Reliable Actors can implement multiple interfaces.</span></span>
* <span data-ttu-id="e7c40-123">**ActorProxy 類別**。</span><span class="sxs-lookup"><span data-stu-id="e7c40-123">**ActorProxy class**.</span></span> <span data-ttu-id="e7c40-124">用戶端應用程式會使用 ActorProxy 類別來叫用透過動作項目介面公開的方法。</span><span class="sxs-lookup"><span data-stu-id="e7c40-124">The ActorProxy class is used by client applications to invoke the methods exposed through the actor interface.</span></span> <span data-ttu-id="e7c40-125">ActorProxy 類別提供兩個重要的功能：</span><span class="sxs-lookup"><span data-stu-id="e7c40-125">The ActorProxy class provides two important functionalities:</span></span>
  
  * <span data-ttu-id="e7c40-126">名稱解析︰它能夠在叢集中找到動作項目 (尋找裝載動作項目的叢集節點)。</span><span class="sxs-lookup"><span data-stu-id="e7c40-126">Name resolution: It is able to locate the actor in the cluster (find the node of the cluster where it is hosted).</span></span>
  * <span data-ttu-id="e7c40-127">處理失敗：它可以重試方法叫用並重新解析動作項目位置，例如在需要動作項目重新定位至叢集中另一個節點失敗後進行。</span><span class="sxs-lookup"><span data-stu-id="e7c40-127">Failure handling: It can retry method invocations and re-resolve the actor location after, for example, a failure that requires the actor to be relocated to another node in the cluster.</span></span>

<span data-ttu-id="e7c40-128">值得一提的是下列與動作項目介面相關的規則︰</span><span class="sxs-lookup"><span data-stu-id="e7c40-128">The following rules that pertain to actor interfaces are worth mentioning:</span></span>

* <span data-ttu-id="e7c40-129">動作項目介面方法無法多載。</span><span class="sxs-lookup"><span data-stu-id="e7c40-129">Actor interface methods cannot be overloaded.</span></span>
* <span data-ttu-id="e7c40-130">動作項目介面方法不能有 out、ref 或選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="e7c40-130">Actor interface methods must not have out, ref, or optional parameters.</span></span>
* <span data-ttu-id="e7c40-131">不支援泛型介面。</span><span class="sxs-lookup"><span data-stu-id="e7c40-131">Generic interfaces are not supported.</span></span>

## <a name="create-a-new-project-in-visual-studio"></a><span data-ttu-id="e7c40-132">在 Visual Studio 中建立新專案</span><span class="sxs-lookup"><span data-stu-id="e7c40-132">Create a new project in Visual Studio</span></span>
<span data-ttu-id="e7c40-133">以管理員身分啟動 Visual Studio 2015 或 Visual Studio 2017，並建立新的 Service Fabric 應用程式專案：</span><span class="sxs-lookup"><span data-stu-id="e7c40-133">Launch Visual Studio 2015 or Visual Studio 2017 as an administrator, and create a new Service Fabric application project:</span></span>

![適用於 Visual Studio 的 Service Fabric 工具 - 新專案][1]

<span data-ttu-id="e7c40-135">在下一個對話方塊中，您可選擇您要建立的專案類型。</span><span class="sxs-lookup"><span data-stu-id="e7c40-135">In the next dialog box, you can choose the type of project that you want to create.</span></span>

![Service Fabric 專案範本][5]

<span data-ttu-id="e7c40-137">讓我們為 HelloWorld 專案使用 Service Fabric Reliable Actors 服務。</span><span class="sxs-lookup"><span data-stu-id="e7c40-137">For the HelloWorld project, let's use the Service Fabric Reliable Actors service.</span></span>

<span data-ttu-id="e7c40-138">建立方案之後，您應該會看到下列結構：</span><span class="sxs-lookup"><span data-stu-id="e7c40-138">After you have created the solution, you should see the following structure:</span></span>

![Service Fabric 專案結構][2]

## <a name="reliable-actors-basic-building-blocks"></a><span data-ttu-id="e7c40-140">Reliable Actors 項目基本建置組塊</span><span class="sxs-lookup"><span data-stu-id="e7c40-140">Reliable Actors basic building blocks</span></span>
<span data-ttu-id="e7c40-141">典型的 Reliable Actors 方案是由 3 個專案組成：</span><span class="sxs-lookup"><span data-stu-id="e7c40-141">A typical Reliable Actors solution is composed of three projects:</span></span>

* <span data-ttu-id="e7c40-142">**應用程式專案 (MyActorApplication)**。</span><span class="sxs-lookup"><span data-stu-id="e7c40-142">**The application project (MyActorApplication)**.</span></span> <span data-ttu-id="e7c40-143">此專案會將所有的服務封裝在一起部署。</span><span class="sxs-lookup"><span data-stu-id="e7c40-143">This is the project that packages all of the services together for deployment.</span></span> <span data-ttu-id="e7c40-144">其包含了用於管理應用程式的 ApplicationManifest.xml  與 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="e7c40-144">It contains the *ApplicationManifest.xml* and PowerShell scripts for managing the application.</span></span>
* <span data-ttu-id="e7c40-145">**介面專案 (MyActor.Interfaces)**。</span><span class="sxs-lookup"><span data-stu-id="e7c40-145">**The interface project (MyActor.Interfaces)**.</span></span> <span data-ttu-id="e7c40-146">此專案包含動作項目的介面定義。</span><span class="sxs-lookup"><span data-stu-id="e7c40-146">This is the project that contains the interface definition for the actor.</span></span> <span data-ttu-id="e7c40-147">在 MyActor.Interfaces 專案中，您可以定義將由方案中的動作項目使用者介面。</span><span class="sxs-lookup"><span data-stu-id="e7c40-147">In the MyActor.Interfaces project, you can define the interfaces that will be used by the actors in the solution.</span></span> <span data-ttu-id="e7c40-148">可以在任何專案中使用任何名稱定義動作項目介面，不過該介面會定義由動作項目實作與呼叫動作項目的用戶端所共用的動作項目合約，因此通常適合在不同於動作項目實作的組件中定義該合約，並可由多個其他專案共用。</span><span class="sxs-lookup"><span data-stu-id="e7c40-148">Your actor interfaces can be defined in any project with any name, however the interface defines the actor contract that is shared by the actor implementation and the clients calling the actor, so it typically makes sense to define it in an assembly that is separate from the actor implementation and can be shared by multiple other projects.</span></span>

```csharp
public interface IMyActor : IActor
{
    Task<string> HelloWorld();
}
```

* <span data-ttu-id="e7c40-149">**動作項目服務專案 (MyActor)**。</span><span class="sxs-lookup"><span data-stu-id="e7c40-149">**The actor service project (MyActor)**.</span></span> <span data-ttu-id="e7c40-150">此專案用於定義即將裝載動作項目的 Service Fabric 服務。</span><span class="sxs-lookup"><span data-stu-id="e7c40-150">This is the project used to define the Service Fabric service that is going to host the actor.</span></span> <span data-ttu-id="e7c40-151">它包含動作項目的實作。</span><span class="sxs-lookup"><span data-stu-id="e7c40-151">It contains the implementation of the actor.</span></span> <span data-ttu-id="e7c40-152">動作項目實作是衍生自基底類型 `Actor` 的類別，可實作 MyActor.Interfaces 專案中所定義的介面。</span><span class="sxs-lookup"><span data-stu-id="e7c40-152">An actor implementation is a class that derives from the base type `Actor` and implements the interface(s) that are defined in the MyActor.Interfaces project.</span></span> <span data-ttu-id="e7c40-153">動作項目類別也必須實作建構函式來接受 `ActorService` 執行個體和 `ActorId`，並將它們傳遞至基底 `Actor` 類別。</span><span class="sxs-lookup"><span data-stu-id="e7c40-153">An actor class must also implement a constructor that accepts an `ActorService` instance and an `ActorId` and passes them to the base `Actor` class.</span></span> <span data-ttu-id="e7c40-154">這可允許平台相依性的建構函式相依性插入。</span><span class="sxs-lookup"><span data-stu-id="e7c40-154">This allows for constructor dependency injection of platform dependencies.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<string> HelloWorld()
    {
        return Task.FromResult("Hello world!");
    }
}
```

<span data-ttu-id="e7c40-155">必須在 Service Fabric 執行階段中以某個服務類型註冊動作項目服務。</span><span class="sxs-lookup"><span data-stu-id="e7c40-155">The actor service must be registered with a service type in the Service Fabric runtime.</span></span> <span data-ttu-id="e7c40-156">為了讓動作項目服務執行您的動作項目執行個體，也必須向動作項目服務註冊動作項目類型。</span><span class="sxs-lookup"><span data-stu-id="e7c40-156">In order for the Actor Service to run your actor instances, your actor type must also be registered with the Actor Service.</span></span> <span data-ttu-id="e7c40-157">`ActorRuntime` 註冊方法會替動作項目執行這項工作。</span><span class="sxs-lookup"><span data-stu-id="e7c40-157">The `ActorRuntime` registration method performs this work for actors.</span></span>

```csharp
internal static class Program
{
    private static void Main()
    {
        try
        {
            ActorRuntime.RegisterActorAsync<MyActor>(
                (context, actorType) => new ActorService(context, actorType, () => new MyActor())).GetAwaiter().GetResult();

            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ActorEventSource.Current.ActorHostInitializationFailed(e.ToString());
            throw;
        }
    }
}

```

<span data-ttu-id="e7c40-158">如果您從在 Visual Studio 中建立新專案開始，且您只有一個動作項目定義，則該註冊預設會包含在 Visual Studio 產生的程式碼中。</span><span class="sxs-lookup"><span data-stu-id="e7c40-158">If you start from a new project in Visual Studio and you have only one actor definition, the registration is included by default in the code that Visual Studio generates.</span></span> <span data-ttu-id="e7c40-159">如果您在服務中定義其他的動作，您必須使用下列項目新增動作項目註冊：</span><span class="sxs-lookup"><span data-stu-id="e7c40-159">If you define other actors in the service, you need to add the actor registration by using:</span></span>

```csharp
 ActorRuntime.RegisterActorAsync<MyOtherActor>();

```

> [!TIP]
> <span data-ttu-id="e7c40-160">Service Fabric Actors 執行階段會發出某些 [事件和與動作項目方法相關的效能計數器](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters)。</span><span class="sxs-lookup"><span data-stu-id="e7c40-160">The Service Fabric Actors runtime emits some [events and performance counters related to actor methods](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters).</span></span> <span data-ttu-id="e7c40-161">這些項目對於診斷與效能監視很有幫助。</span><span class="sxs-lookup"><span data-stu-id="e7c40-161">They are useful in diagnostics and performance monitoring.</span></span>
> 
> 

## <a name="debugging"></a><span data-ttu-id="e7c40-162">Debugging</span><span class="sxs-lookup"><span data-stu-id="e7c40-162">Debugging</span></span>
<span data-ttu-id="e7c40-163">Visual Studio 專用的 Service Fabric 工具支援在本機機器上偵錯。</span><span class="sxs-lookup"><span data-stu-id="e7c40-163">The Service Fabric tools for Visual Studio support debugging on your local machine.</span></span> <span data-ttu-id="e7c40-164">您可以點擊 F5 鍵開始偵錯工作階段。</span><span class="sxs-lookup"><span data-stu-id="e7c40-164">You can start a debugging session by hitting the F5 key.</span></span> <span data-ttu-id="e7c40-165">Visual Studio 會建置封裝 (如有必要)。</span><span class="sxs-lookup"><span data-stu-id="e7c40-165">Visual Studio builds (if necessary) packages.</span></span> <span data-ttu-id="e7c40-166">它也會在本機 Service Fabric 叢集上部署應用程式並附加偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="e7c40-166">It also deploys the application on the local Service Fabric cluster and attaches the debugger.</span></span>

<span data-ttu-id="e7c40-167">在部署的過程中，您可在 [輸出]  視窗中查看進度。</span><span class="sxs-lookup"><span data-stu-id="e7c40-167">During the deployment process, you can see the progress in the **Output** window.</span></span>

![Service Fabric 偵錯輸出視窗][3]

## <a name="next-steps"></a><span data-ttu-id="e7c40-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e7c40-169">Next steps</span></span>
<span data-ttu-id="e7c40-170">深入了解 [Reliable Actor 如何使用 Service Fabric 平台](service-fabric-reliable-actors-platform.md)。</span><span class="sxs-lookup"><span data-stu-id="e7c40-170">Learn more about [how Reliable Actors use the Service Fabric platform](service-fabric-reliable-actors-platform.md).</span></span>

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject.PNG
[2]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-projectstructure.PNG
[3]: ./media/service-fabric-reliable-actors-get-started/debugging-output.PNG
[4]: ./media/service-fabric-reliable-actors-get-started/vs-context-menu.png
[5]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject1.PNG
