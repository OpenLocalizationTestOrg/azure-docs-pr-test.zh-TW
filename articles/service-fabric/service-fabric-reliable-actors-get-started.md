---
title: "aaaCreate 您第一次行動為基礎 Azure 微服務在 C# |Microsoft 文件"
description: "本教學課程將引導您完成建立、 偵錯和部署簡單動作項目為基礎的服務使用服務網狀架構 Reliable Actors hello 步驟。"
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
ms.openlocfilehash: ab4f75bef0adb6e70f0ead587475b3fb51e6e6a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-reliable-actors"></a><span data-ttu-id="ae814-103">開始使用 Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="ae814-103">Getting started with Reliable Actors</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ae814-104">Windows 上的 C# </span><span class="sxs-lookup"><span data-stu-id="ae814-104">C# on Windows</span></span>](service-fabric-reliable-actors-get-started.md)
> * [<span data-ttu-id="ae814-105">在 Linux 上使用 Java</span><span class="sxs-lookup"><span data-stu-id="ae814-105">Java on Linux</span></span>](service-fabric-reliable-actors-get-started-java.md)
> 
> 

<span data-ttu-id="ae814-106">本文章說明 Azure Service Fabric Reliable Actors hello 基本概念，並將引導您建立、 偵錯和部署 Visual Studio 中的簡單 Reliable Actor 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ae814-106">This article explains hello basics of Azure Service Fabric Reliable Actors and walks you through creating, debugging, and deploying a simple Reliable Actor application in Visual Studio.</span></span>

## <a name="installation-and-setup"></a><span data-ttu-id="ae814-107">安裝與設定</span><span class="sxs-lookup"><span data-stu-id="ae814-107">Installation and setup</span></span>
<span data-ttu-id="ae814-108">在開始之前，請確定您已擁有 hello Service Fabric 開發環境設定您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="ae814-108">Before you start, ensure that you have hello Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="ae814-109">如果您需要 tooset 它，請參閱詳細的指示[如何 hello 開發環境 tooset](service-fabric-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="ae814-109">If you need tooset it up, see detailed instructions on [how tooset up hello development environment](service-fabric-get-started.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="ae814-110">基本概念</span><span class="sxs-lookup"><span data-stu-id="ae814-110">Basic concepts</span></span>
<span data-ttu-id="ae814-111">tooget 入門 Reliable Actors，您只需要 toounderstand 某些基本概念：</span><span class="sxs-lookup"><span data-stu-id="ae814-111">tooget started with Reliable Actors, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="ae814-112">**動作項目服務**。</span><span class="sxs-lookup"><span data-stu-id="ae814-112">**Actor service**.</span></span> <span data-ttu-id="ae814-113">Reliable Actors 被封裝在可靠的服務，可以部署在 hello 服務網狀架構基礎結構。</span><span class="sxs-lookup"><span data-stu-id="ae814-113">Reliable Actors are packaged in Reliable Services that can be deployed in hello Service Fabric infrastructure.</span></span> <span data-ttu-id="ae814-114">動作項目執行個體會在指定的服務執行個體中啟動。</span><span class="sxs-lookup"><span data-stu-id="ae814-114">Actor instances are activated in a named service instance.</span></span>
* <span data-ttu-id="ae814-115">**動作項目註冊**。</span><span class="sxs-lookup"><span data-stu-id="ae814-115">**Actor registration**.</span></span> <span data-ttu-id="ae814-116">為使用可靠的服務，Reliable Actor 服務需要 toobe 向 hello Service Fabric 執行階段。</span><span class="sxs-lookup"><span data-stu-id="ae814-116">As with Reliable Services, a Reliable Actor service needs toobe registered with hello Service Fabric runtime.</span></span> <span data-ttu-id="ae814-117">此外，hello 動作項目類型必須 toobe 向 hello 動作項目執行階段。</span><span class="sxs-lookup"><span data-stu-id="ae814-117">In addition, hello actor type needs toobe registered with hello Actor runtime.</span></span>
* <span data-ttu-id="ae814-118">**動作項目介面**。</span><span class="sxs-lookup"><span data-stu-id="ae814-118">**Actor interface**.</span></span> <span data-ttu-id="ae814-119">hello 執行者介面是使用的 toodefine 執行者的強型別的公用介面。</span><span class="sxs-lookup"><span data-stu-id="ae814-119">hello actor interface is used toodefine a strongly typed public interface of an actor.</span></span> <span data-ttu-id="ae814-120">在 hello Reliable Actor 模型術語，hello 執行者介面會定義的 hello hello 執行者的訊息類型可以了解並處理。</span><span class="sxs-lookup"><span data-stu-id="ae814-120">In hello Reliable Actor model terminology, hello actor interface defines hello types of messages that hello actor can understand and process.</span></span> <span data-ttu-id="ae814-121">hello 執行者介面由其他的動作，用戶端應用程式太 「 傳送 」 （非同步） 訊息 toohello 動作項目。</span><span class="sxs-lookup"><span data-stu-id="ae814-121">hello actor interface is used by other actors and client applications too"send" (asynchronously) messages toohello actor.</span></span> <span data-ttu-id="ae814-122">Reliable Actors 可實作多個介面。</span><span class="sxs-lookup"><span data-stu-id="ae814-122">Reliable Actors can implement multiple interfaces.</span></span>
* <span data-ttu-id="ae814-123">**ActorProxy 類別**。</span><span class="sxs-lookup"><span data-stu-id="ae814-123">**ActorProxy class**.</span></span> <span data-ttu-id="ae814-124">hello ActorProxy 類別由用戶端應用程式 tooinvoke hello hello 執行者介面透過公開的方法。</span><span class="sxs-lookup"><span data-stu-id="ae814-124">hello ActorProxy class is used by client applications tooinvoke hello methods exposed through hello actor interface.</span></span> <span data-ttu-id="ae814-125">hello ActorProxy 類別提供兩個重要功能：</span><span class="sxs-lookup"><span data-stu-id="ae814-125">hello ActorProxy class provides two important functionalities:</span></span>
  
  * <span data-ttu-id="ae814-126">名稱解析： 它是無法 toolocate hello hello 叢集 （尋找 hello hello 叢集節點的裝載位置） 中的動作項目。</span><span class="sxs-lookup"><span data-stu-id="ae814-126">Name resolution: It is able toolocate hello actor in hello cluster (find hello node of hello cluster where it is hosted).</span></span>
  * <span data-ttu-id="ae814-127">錯誤處理： 它可以重試方法引動過程，和重新解析 hello 動作項目位置之後、 需要 hello 執行者 toobe 失敗，例如重新定位 tooanother hello 叢集中的節點。</span><span class="sxs-lookup"><span data-stu-id="ae814-127">Failure handling: It can retry method invocations and re-resolve hello actor location after, for example, a failure that requires hello actor toobe relocated tooanother node in hello cluster.</span></span>

<span data-ttu-id="ae814-128">下列規則的相關 tooactor 介面 hello 是值得一提的是：</span><span class="sxs-lookup"><span data-stu-id="ae814-128">hello following rules that pertain tooactor interfaces are worth mentioning:</span></span>

* <span data-ttu-id="ae814-129">動作項目介面方法無法多載。</span><span class="sxs-lookup"><span data-stu-id="ae814-129">Actor interface methods cannot be overloaded.</span></span>
* <span data-ttu-id="ae814-130">動作項目介面方法不能有 out、ref 或選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="ae814-130">Actor interface methods must not have out, ref, or optional parameters.</span></span>
* <span data-ttu-id="ae814-131">不支援泛型介面。</span><span class="sxs-lookup"><span data-stu-id="ae814-131">Generic interfaces are not supported.</span></span>

## <a name="create-a-new-project-in-visual-studio"></a><span data-ttu-id="ae814-132">在 Visual Studio 中建立新專案</span><span class="sxs-lookup"><span data-stu-id="ae814-132">Create a new project in Visual Studio</span></span>
<span data-ttu-id="ae814-133">以管理員身分啟動 Visual Studio 2015 或 Visual Studio 2017，並建立新的 Service Fabric 應用程式專案：</span><span class="sxs-lookup"><span data-stu-id="ae814-133">Launch Visual Studio 2015 or Visual Studio 2017 as an administrator, and create a new Service Fabric application project:</span></span>

![適用於 Visual Studio 的 Service Fabric 工具 - 新專案][1]

<span data-ttu-id="ae814-135">在 hello 下一步 對話方塊中，您可以選擇 hello 類型的專案，您會想 toocreate。</span><span class="sxs-lookup"><span data-stu-id="ae814-135">In hello next dialog box, you can choose hello type of project that you want toocreate.</span></span>

![Service Fabric 專案範本][5]

<span data-ttu-id="ae814-137">Hello HelloWorld 專案，讓我們使用 hello 服務網狀架構 Reliable Actors 服務。</span><span class="sxs-lookup"><span data-stu-id="ae814-137">For hello HelloWorld project, let's use hello Service Fabric Reliable Actors service.</span></span>

<span data-ttu-id="ae814-138">建立 hello 方案之後，您應該會看到下列結構的 hello:</span><span class="sxs-lookup"><span data-stu-id="ae814-138">After you have created hello solution, you should see hello following structure:</span></span>

![Service Fabric 專案結構][2]

## <a name="reliable-actors-basic-building-blocks"></a><span data-ttu-id="ae814-140">Reliable Actors 項目基本建置組塊</span><span class="sxs-lookup"><span data-stu-id="ae814-140">Reliable Actors basic building blocks</span></span>
<span data-ttu-id="ae814-141">典型的 Reliable Actors 方案是由 3 個專案組成：</span><span class="sxs-lookup"><span data-stu-id="ae814-141">A typical Reliable Actors solution is composed of three projects:</span></span>

* <span data-ttu-id="ae814-142">**hello 應用程式專案 (MyActorApplication)**。</span><span class="sxs-lookup"><span data-stu-id="ae814-142">**hello application project (MyActorApplication)**.</span></span> <span data-ttu-id="ae814-143">這是封裝所有 hello 服務一起部署的 hello 專案。</span><span class="sxs-lookup"><span data-stu-id="ae814-143">This is hello project that packages all of hello services together for deployment.</span></span> <span data-ttu-id="ae814-144">它包含 hello *ApplicationManifest.xml*和 PowerShell 指令碼，以管理 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ae814-144">It contains hello *ApplicationManifest.xml* and PowerShell scripts for managing hello application.</span></span>
* <span data-ttu-id="ae814-145">**hello 介面專案 (MyActor.Interfaces)**。</span><span class="sxs-lookup"><span data-stu-id="ae814-145">**hello interface project (MyActor.Interfaces)**.</span></span> <span data-ttu-id="ae814-146">這是包含 hello 執行者的 hello 介面定義的 hello 專案。</span><span class="sxs-lookup"><span data-stu-id="ae814-146">This is hello project that contains hello interface definition for hello actor.</span></span> <span data-ttu-id="ae814-147">在 hello MyActor.Interfaces 專案中，您可以定義將由 hello 執行者 hello 方案中的 hello 介面。</span><span class="sxs-lookup"><span data-stu-id="ae814-147">In hello MyActor.Interfaces project, you can define hello interfaces that will be used by hello actors in hello solution.</span></span> <span data-ttu-id="ae814-148">動作項目介面可以定義任何專案中使用任何名稱，不過 hello 介面定義 hello 動作項目實作和呼叫 hello 動作項目，因此它通常會建立有意義 toodefine hello 用戶端共用的 hello 執行者合約中的組件分隔與 hello 動作項目實作，並且可由多個其他專案共用。</span><span class="sxs-lookup"><span data-stu-id="ae814-148">Your actor interfaces can be defined in any project with any name, however hello interface defines hello actor contract that is shared by hello actor implementation and hello clients calling hello actor, so it typically makes sense toodefine it in an assembly that is separate from hello actor implementation and can be shared by multiple other projects.</span></span>

```csharp
public interface IMyActor : IActor
{
    Task<string> HelloWorld();
}
```

* <span data-ttu-id="ae814-149">**hello 行動服務專案 (MyActor)**。</span><span class="sxs-lookup"><span data-stu-id="ae814-149">**hello actor service project (MyActor)**.</span></span> <span data-ttu-id="ae814-150">這是 hello 專案使用 toodefine hello Service Fabric 服務進行 toohost hello 動作項目。</span><span class="sxs-lookup"><span data-stu-id="ae814-150">This is hello project used toodefine hello Service Fabric service that is going toohost hello actor.</span></span> <span data-ttu-id="ae814-151">它包含 hello 執行者 hello 實作。</span><span class="sxs-lookup"><span data-stu-id="ae814-151">It contains hello implementation of hello actor.</span></span> <span data-ttu-id="ae814-152">動作項目實作是類別，衍生自基底型別 hello`Actor`和實作 hello hello MyActor.Interfaces 專案中所定義的介面。</span><span class="sxs-lookup"><span data-stu-id="ae814-152">An actor implementation is a class that derives from hello base type `Actor` and implements hello interface(s) that are defined in hello MyActor.Interfaces project.</span></span> <span data-ttu-id="ae814-153">動作項目類別也必須實作的建構函式可接受`ActorService`執行個體和`ActorId`並將其傳遞 toohello 基底`Actor`類別。</span><span class="sxs-lookup"><span data-stu-id="ae814-153">An actor class must also implement a constructor that accepts an `ActorService` instance and an `ActorId` and passes them toohello base `Actor` class.</span></span> <span data-ttu-id="ae814-154">這可允許平台相依性的建構函式相依性插入。</span><span class="sxs-lookup"><span data-stu-id="ae814-154">This allows for constructor dependency injection of platform dependencies.</span></span>

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

<span data-ttu-id="ae814-155">hello actor 服務必須向 hello Service Fabric 執行階段中的服務類型。</span><span class="sxs-lookup"><span data-stu-id="ae814-155">hello actor service must be registered with a service type in hello Service Fabric runtime.</span></span> <span data-ttu-id="ae814-156">在順序 hello Actor 服務 toorun 您的動作項目執行個體，動作項目類型也必須向 hello 動作項目服務。</span><span class="sxs-lookup"><span data-stu-id="ae814-156">In order for hello Actor Service toorun your actor instances, your actor type must also be registered with hello Actor Service.</span></span> <span data-ttu-id="ae814-157">hello`ActorRuntime`註冊方法為執行者執行這項工作。</span><span class="sxs-lookup"><span data-stu-id="ae814-157">hello `ActorRuntime` registration method performs this work for actors.</span></span>

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

<span data-ttu-id="ae814-158">如果您從新的專案，Visual Studio 中啟動，您只能有一個動作項目定義 hello 註冊預設隨附在 Visual Studio 會產生的 hello 程式碼中。</span><span class="sxs-lookup"><span data-stu-id="ae814-158">If you start from a new project in Visual Studio and you have only one actor definition, hello registration is included by default in hello code that Visual Studio generates.</span></span> <span data-ttu-id="ae814-159">如果您在 hello 服務中定義其他的動作，您會需要使用 tooadd hello 執行者註冊：</span><span class="sxs-lookup"><span data-stu-id="ae814-159">If you define other actors in hello service, you need tooadd hello actor registration by using:</span></span>

```csharp
 ActorRuntime.RegisterActorAsync<MyOtherActor>();

```

> [!TIP]
> <span data-ttu-id="ae814-160">hello Service Fabric 動作項目執行階段發出某些[事件和效能計數器相關 tooactor 方法](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters)。</span><span class="sxs-lookup"><span data-stu-id="ae814-160">hello Service Fabric Actors runtime emits some [events and performance counters related tooactor methods](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters).</span></span> <span data-ttu-id="ae814-161">這些項目對於診斷與效能監視很有幫助。</span><span class="sxs-lookup"><span data-stu-id="ae814-161">They are useful in diagnostics and performance monitoring.</span></span>
> 
> 

## <a name="debugging"></a><span data-ttu-id="ae814-162">Debugging</span><span class="sxs-lookup"><span data-stu-id="ae814-162">Debugging</span></span>
<span data-ttu-id="ae814-163">Visual Studio 的 hello Service Fabric 工具支援偵錯在本機電腦上。</span><span class="sxs-lookup"><span data-stu-id="ae814-163">hello Service Fabric tools for Visual Studio support debugging on your local machine.</span></span> <span data-ttu-id="ae814-164">您可以叫用 hello F5 鍵啟動偵錯工作階段。</span><span class="sxs-lookup"><span data-stu-id="ae814-164">You can start a debugging session by hitting hello F5 key.</span></span> <span data-ttu-id="ae814-165">Visual Studio 會建置封裝 (如有必要)。</span><span class="sxs-lookup"><span data-stu-id="ae814-165">Visual Studio builds (if necessary) packages.</span></span> <span data-ttu-id="ae814-166">它也將 hello hello 本機 Service Fabric 叢集上的應用程式部署，並附加 hello 偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="ae814-166">It also deploys hello application on hello local Service Fabric cluster and attaches hello debugger.</span></span>

<span data-ttu-id="ae814-167">在 hello 部署過程中，您可以看到 hello hello 正在**輸出**視窗。</span><span class="sxs-lookup"><span data-stu-id="ae814-167">During hello deployment process, you can see hello progress in hello **Output** window.</span></span>

![Service Fabric 偵錯輸出視窗][3]

## <a name="next-steps"></a><span data-ttu-id="ae814-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ae814-169">Next steps</span></span>
<span data-ttu-id="ae814-170">深入了解[Reliable Actors 使用 hello Service Fabric 平台的方式](service-fabric-reliable-actors-platform.md)。</span><span class="sxs-lookup"><span data-stu-id="ae814-170">Learn more about [how Reliable Actors use hello Service Fabric platform](service-fabric-reliable-actors-platform.md).</span></span>

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject.PNG
[2]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-projectstructure.PNG
[3]: ./media/service-fabric-reliable-actors-get-started/debugging-output.PNG
[4]: ./media/service-fabric-reliable-actors-get-started/vs-context-menu.png
[5]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject1.PNG
