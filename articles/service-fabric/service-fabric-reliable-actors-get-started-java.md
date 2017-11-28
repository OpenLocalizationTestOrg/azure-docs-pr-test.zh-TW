---
title: "aaaCreate 您第一次行動為基礎 Azure 微服務在 Java 中的 |Microsoft 文件"
description: "本教學課程將引導您完成建立、 偵錯和部署簡單動作項目為基礎的服務使用服務網狀架構 Reliable Actors hello 步驟。"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d31dc8ab-9760-4619-a641-facb8324c759
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/04/2017
ms.author: vturecek
ms.openlocfilehash: 24718a8d7034360c53597f139169580f1a6ce732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-reliable-actors"></a><span data-ttu-id="5cdec-103">開始使用 Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="5cdec-103">Getting started with Reliable Actors</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5cdec-104">Windows 上的 C# </span><span class="sxs-lookup"><span data-stu-id="5cdec-104">C# on Windows</span></span>](service-fabric-reliable-actors-get-started.md)
> * [<span data-ttu-id="5cdec-105">在 Linux 上使用 Java</span><span class="sxs-lookup"><span data-stu-id="5cdec-105">Java on Linux</span></span>](service-fabric-reliable-actors-get-started-java.md)
> 
> 

<span data-ttu-id="5cdec-106">本文章說明 Azure Service Fabric Reliable Actors hello 基本概念，並將告訴您如何建立和部署簡單的 Reliable Actor 應用程式在 Java 中。</span><span class="sxs-lookup"><span data-stu-id="5cdec-106">This article explains hello basics of Azure Service Fabric Reliable Actors and walks you through creating and deploying a simple Reliable Actor application in Java.</span></span>

## <a name="installation-and-setup"></a><span data-ttu-id="5cdec-107">安裝與設定</span><span class="sxs-lookup"><span data-stu-id="5cdec-107">Installation and setup</span></span>
<span data-ttu-id="5cdec-108">開始之前，請確定您擁有 hello Service Fabric 開發環境設定您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="5cdec-108">Before you start, make sure you have hello Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="5cdec-109">如果您需要 tooset 總太移[Mac 上開始使用](service-fabric-get-started-mac.md)或[開始使用 Linux](service-fabric-get-started-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="5cdec-109">If you need tooset it up, go too[getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="5cdec-110">基本概念</span><span class="sxs-lookup"><span data-stu-id="5cdec-110">Basic concepts</span></span>
<span data-ttu-id="5cdec-111">tooget 入門 Reliable Actors，您只需要 toounderstand 某些基本概念：</span><span class="sxs-lookup"><span data-stu-id="5cdec-111">tooget started with Reliable Actors, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="5cdec-112">**動作項目服務**。</span><span class="sxs-lookup"><span data-stu-id="5cdec-112">**Actor service**.</span></span> <span data-ttu-id="5cdec-113">Reliable Actors 被封裝在可靠的服務，可以部署在 hello 服務網狀架構基礎結構。</span><span class="sxs-lookup"><span data-stu-id="5cdec-113">Reliable Actors are packaged in Reliable Services that can be deployed in hello Service Fabric infrastructure.</span></span> <span data-ttu-id="5cdec-114">動作項目執行個體會在指定的服務執行個體中啟動。</span><span class="sxs-lookup"><span data-stu-id="5cdec-114">Actor instances are activated in a named service instance.</span></span>
* <span data-ttu-id="5cdec-115">**動作項目註冊**。</span><span class="sxs-lookup"><span data-stu-id="5cdec-115">**Actor registration**.</span></span> <span data-ttu-id="5cdec-116">為使用可靠的服務，Reliable Actor 服務需要 toobe 向 hello Service Fabric 執行階段。</span><span class="sxs-lookup"><span data-stu-id="5cdec-116">As with Reliable Services, a Reliable Actor service needs toobe registered with hello Service Fabric runtime.</span></span> <span data-ttu-id="5cdec-117">此外，hello 動作項目類型必須 toobe 向 hello 動作項目執行階段。</span><span class="sxs-lookup"><span data-stu-id="5cdec-117">In addition, hello actor type needs toobe registered with hello Actor runtime.</span></span>
* <span data-ttu-id="5cdec-118">**動作項目介面**。</span><span class="sxs-lookup"><span data-stu-id="5cdec-118">**Actor interface**.</span></span> <span data-ttu-id="5cdec-119">hello 執行者介面是使用的 toodefine 執行者的強型別的公用介面。</span><span class="sxs-lookup"><span data-stu-id="5cdec-119">hello actor interface is used toodefine a strongly typed public interface of an actor.</span></span> <span data-ttu-id="5cdec-120">在 hello Reliable Actor 模型術語，hello 執行者介面會定義的 hello hello 執行者的訊息類型可以了解並處理。</span><span class="sxs-lookup"><span data-stu-id="5cdec-120">In hello Reliable Actor model terminology, hello actor interface defines hello types of messages that hello actor can understand and process.</span></span> <span data-ttu-id="5cdec-121">hello 執行者介面由其他的動作，用戶端應用程式太 「 傳送 」 （非同步） 訊息 toohello 動作項目。</span><span class="sxs-lookup"><span data-stu-id="5cdec-121">hello actor interface is used by other actors and client applications too"send" (asynchronously) messages toohello actor.</span></span> <span data-ttu-id="5cdec-122">Reliable Actors 可實作多個介面。</span><span class="sxs-lookup"><span data-stu-id="5cdec-122">Reliable Actors can implement multiple interfaces.</span></span>
* <span data-ttu-id="5cdec-123">**ActorProxy 類別**。</span><span class="sxs-lookup"><span data-stu-id="5cdec-123">**ActorProxy class**.</span></span> <span data-ttu-id="5cdec-124">hello ActorProxy 類別由用戶端應用程式 tooinvoke hello hello 執行者介面透過公開的方法。</span><span class="sxs-lookup"><span data-stu-id="5cdec-124">hello ActorProxy class is used by client applications tooinvoke hello methods exposed through hello actor interface.</span></span> <span data-ttu-id="5cdec-125">hello ActorProxy 類別提供兩個重要功能：</span><span class="sxs-lookup"><span data-stu-id="5cdec-125">hello ActorProxy class provides two important functionalities:</span></span>
  
  * <span data-ttu-id="5cdec-126">名稱解析： 它是無法 toolocate hello hello 叢集 （尋找 hello hello 叢集節點的裝載位置） 中的動作項目。</span><span class="sxs-lookup"><span data-stu-id="5cdec-126">Name resolution: It is able toolocate hello actor in hello cluster (find hello node of hello cluster where it is hosted).</span></span>
  * <span data-ttu-id="5cdec-127">錯誤處理： 它可以重試方法引動過程，和重新解析 hello 動作項目位置之後、 需要 hello 執行者 toobe 失敗，例如重新定位 tooanother hello 叢集中的節點。</span><span class="sxs-lookup"><span data-stu-id="5cdec-127">Failure handling: It can retry method invocations and re-resolve hello actor location after, for example, a failure that requires hello actor toobe relocated tooanother node in hello cluster.</span></span>

<span data-ttu-id="5cdec-128">下列規則的相關 tooactor 介面 hello 是值得一提的是：</span><span class="sxs-lookup"><span data-stu-id="5cdec-128">hello following rules that pertain tooactor interfaces are worth mentioning:</span></span>

* <span data-ttu-id="5cdec-129">動作項目介面方法無法多載。</span><span class="sxs-lookup"><span data-stu-id="5cdec-129">Actor interface methods cannot be overloaded.</span></span>
* <span data-ttu-id="5cdec-130">動作項目介面方法不能有 out、ref 或選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="5cdec-130">Actor interface methods must not have out, ref, or optional parameters.</span></span>
* <span data-ttu-id="5cdec-131">不支援泛型介面。</span><span class="sxs-lookup"><span data-stu-id="5cdec-131">Generic interfaces are not supported.</span></span>

## <a name="create-an-actor-service"></a><span data-ttu-id="5cdec-132">建立動作項目服務</span><span class="sxs-lookup"><span data-stu-id="5cdec-132">Create an actor service</span></span>
<span data-ttu-id="5cdec-133">以建立新 Service Fabric 應用程式的方式開始。</span><span class="sxs-lookup"><span data-stu-id="5cdec-133">Start by creating a new Service Fabric application.</span></span> <span data-ttu-id="5cdec-134">hello Service Fabric SDK for Linux 包含 Yeoman Service Fabric 應用程式與無狀態服務的產生器 tooprovide hello scaffolding。</span><span class="sxs-lookup"><span data-stu-id="5cdec-134">hello Service Fabric SDK for Linux includes a Yeoman generator tooprovide hello scaffolding for a Service Fabric application with a stateless service.</span></span> <span data-ttu-id="5cdec-135">開始執行 hello Yeoman 下列命令：</span><span class="sxs-lookup"><span data-stu-id="5cdec-135">Start by running hello following Yeoman command:</span></span>

```bash
$ yo azuresfjava
```

<span data-ttu-id="5cdec-136">請遵循 hello 指示 toocreate **Reliable Actor Service**。</span><span class="sxs-lookup"><span data-stu-id="5cdec-136">Follow hello instructions toocreate a **Reliable Actor Service**.</span></span> <span data-ttu-id="5cdec-137">本教學課程中，命名 hello 應用程式"HelloWorldActorApplication 」 和 hello 執行者 」 HelloWorldActor。 」</span><span class="sxs-lookup"><span data-stu-id="5cdec-137">For this tutorial, name hello application "HelloWorldActorApplication" and hello actor "HelloWorldActor."</span></span> <span data-ttu-id="5cdec-138">將建立下列 scaffolding hello:</span><span class="sxs-lookup"><span data-stu-id="5cdec-138">hello following scaffolding will be created:</span></span>

```bash
HelloWorldActorApplication/
├── build.gradle
├── HelloWorldActor
│   ├── build.gradle
│   ├── settings.gradle
│   └── src
│       └── reliableactor
│           ├── HelloWorldActorHost.java
│           └── HelloWorldActorImpl.java
├── HelloWorldActorApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldActorPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   ├── _readme.txt
│       │   └── Settings.xml
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── HelloWorldActorInterface
│   ├── build.gradle
│   └── src
│       └── reliableactor
│           └── HelloWorldActor.java
├── HelloWorldActorTestClient
│   ├── build.gradle
│   ├── settings.gradle
│   ├── src
│   │   └── reliableactor
│   │       └── test
│   │           └── HelloWorldActorTestClient.java
│   └── testclient.sh
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="reliable-actors-basic-building-blocks"></a><span data-ttu-id="5cdec-139">Reliable Actors 項目基本建置組塊</span><span class="sxs-lookup"><span data-stu-id="5cdec-139">Reliable Actors basic building blocks</span></span>
<span data-ttu-id="5cdec-140">hello 稍早所述的基本概念會轉譯為 hello 基本建置組塊 Reliable Actor 服務。</span><span class="sxs-lookup"><span data-stu-id="5cdec-140">hello basic concepts described earlier translate into hello basic building blocks of a Reliable Actor service.</span></span>

### <a name="actor-interface"></a><span data-ttu-id="5cdec-141">動作項目介面</span><span class="sxs-lookup"><span data-stu-id="5cdec-141">Actor interface</span></span>
<span data-ttu-id="5cdec-142">這包含 hello 執行者的 hello 介面定義。</span><span class="sxs-lookup"><span data-stu-id="5cdec-142">This contains hello interface definition for hello actor.</span></span> <span data-ttu-id="5cdec-143">這個介面會定義 hello 動作項目實作和呼叫 hello 動作項目，因此它通常會建立它的位置中分隔與 hello 動作項目實作，並且可由多個其他共用的意義上 toodefine hello 用戶端共用的 hello 執行者合約服務或用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="5cdec-143">This interface defines hello actor contract that is shared by hello actor implementation and hello clients calling hello actor, so it typically makes sense toodefine it in a place that is separate from hello actor implementation and can be shared by multiple other services or client applications.</span></span>

<span data-ttu-id="5cdec-144">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`：</span><span class="sxs-lookup"><span data-stu-id="5cdec-144">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:</span></span>

```java
public interface HelloWorldActor extends Actor {
    @Readonly   
    CompletableFuture<Integer> getCountAsync();

    CompletableFuture<?> setCountAsync(int count);
}
```

### <a name="actor-service"></a><span data-ttu-id="5cdec-145">動作項目服務</span><span class="sxs-lookup"><span data-stu-id="5cdec-145">Actor service</span></span>
<span data-ttu-id="5cdec-146">這包含您的動作項目實作和動作項目註冊碼。</span><span class="sxs-lookup"><span data-stu-id="5cdec-146">This contains your actor implementation and actor registration code.</span></span> <span data-ttu-id="5cdec-147">hello 動作項目類別實作 hello 動作項目介面。</span><span class="sxs-lookup"><span data-stu-id="5cdec-147">hello actor class implements hello actor interface.</span></span> <span data-ttu-id="5cdec-148">這是您的動作項目工作之處。</span><span class="sxs-lookup"><span data-stu-id="5cdec-148">This is where your actor does its work.</span></span>

<span data-ttu-id="5cdec-149">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`：</span><span class="sxs-lookup"><span data-stu-id="5cdec-149">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:</span></span>

```java
@ActorServiceAttribute(name = "HelloWorldActor.HelloWorldActorService")
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class HelloWorldActorImpl extends ReliableActor implements HelloWorldActor {
    Logger logger = Logger.getLogger(this.getClass().getName());

    protected CompletableFuture<?> onActivateAsync() {
        logger.log(Level.INFO, "onActivateAsync");

        return this.stateManager().tryAddStateAsync("count", 0);
    }

    @Override
    public CompletableFuture<Integer> getCountAsync() {
        logger.log(Level.INFO, "Getting current count value");
        return this.stateManager().getStateAsync("count");
    }

    @Override
    public CompletableFuture<?> setCountAsync(int count) {
        logger.log(Level.INFO, "Setting current count value {0}", count);
        return this.stateManager().addOrUpdateStateAsync("count", count, (key, value) -> count > value ? count : value);
    }
}
```

### <a name="actor-registration"></a><span data-ttu-id="5cdec-150">動作項目註冊</span><span class="sxs-lookup"><span data-stu-id="5cdec-150">Actor registration</span></span>
<span data-ttu-id="5cdec-151">hello actor 服務必須向 hello Service Fabric 執行階段中的服務類型。</span><span class="sxs-lookup"><span data-stu-id="5cdec-151">hello actor service must be registered with a service type in hello Service Fabric runtime.</span></span> <span data-ttu-id="5cdec-152">在順序 hello Actor 服務 toorun 您的動作項目執行個體，動作項目類型也必須向 hello 動作項目服務。</span><span class="sxs-lookup"><span data-stu-id="5cdec-152">In order for hello Actor Service toorun your actor instances, your actor type must also be registered with hello Actor Service.</span></span> <span data-ttu-id="5cdec-153">hello`ActorRuntime`註冊方法為執行者執行這項工作。</span><span class="sxs-lookup"><span data-stu-id="5cdec-153">hello `ActorRuntime` registration method performs this work for actors.</span></span>

<span data-ttu-id="5cdec-154">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`：</span><span class="sxs-lookup"><span data-stu-id="5cdec-154">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:</span></span>

```java
public class HelloWorldActorHost {

    public static void main(String[] args) throws Exception {

        try {
            ActorRuntime.registerActorAsync(HelloWorldActorImpl.class, (context, actorType) -> new ActorServiceImpl(context, actorType, ()-> new HelloWorldActorImpl()), Duration.ofSeconds(10));

            Thread.sleep(Long.MAX_VALUE);

        } catch (Exception e) {
            e.printStackTrace();
            throw e;
        }
    }
}
```

### <a name="test-client"></a><span data-ttu-id="5cdec-155">Test client</span><span class="sxs-lookup"><span data-stu-id="5cdec-155">Test client</span></span>
<span data-ttu-id="5cdec-156">這是簡單的測試用戶端應用程式，您可以分開執行 hello Service Fabric 應用程式 tootest 動作項目服務。</span><span class="sxs-lookup"><span data-stu-id="5cdec-156">This is a simple test client application you can run separately from hello Service Fabric application tootest your actor service.</span></span> <span data-ttu-id="5cdec-157">這是範例的位置 hello ActorProxy 可以使用的 tooactivate 和動作項目執行個體進行通訊。</span><span class="sxs-lookup"><span data-stu-id="5cdec-157">This is an example of where hello ActorProxy can be used tooactivate and communicate with actor instances.</span></span> <span data-ttu-id="5cdec-158">它不會與您的服務一同部署。</span><span class="sxs-lookup"><span data-stu-id="5cdec-158">It does not get deployed with your service.</span></span>

### <a name="hello-application"></a><span data-ttu-id="5cdec-159">hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="5cdec-159">hello application</span></span>
<span data-ttu-id="5cdec-160">最後，hello 應用程式套件 hello 動作項目服務和任何其他您可能會在未來一起部署的 hello 新增的服務。</span><span class="sxs-lookup"><span data-stu-id="5cdec-160">Finally, hello application packages hello actor service and any other services you might add in hello future together for deployment.</span></span> <span data-ttu-id="5cdec-161">它包含 hello *ApplicationManifest.xml*和 hello actor 服務封裝的預留位置。</span><span class="sxs-lookup"><span data-stu-id="5cdec-161">It contains hello *ApplicationManifest.xml* and place holders for hello actor service package.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="5cdec-162">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="5cdec-162">Run hello application</span></span>

<span data-ttu-id="5cdec-163">hello Yeoman scaffolding 包含 gradle 指令碼 toobuild hello 應用程式和 bash 指令碼 toodeploy 和移除應用程式。</span><span class="sxs-lookup"><span data-stu-id="5cdec-163">hello Yeoman scaffolding includes a gradle script toobuild hello application and bash scripts toodeploy and remove the application.</span></span> <span data-ttu-id="5cdec-164">toodeploy hello 應用程式，第一個使用 gradle 的組建 hello 應用程式：</span><span class="sxs-lookup"><span data-stu-id="5cdec-164">toodeploy hello application, first build hello application with gradle:</span></span>

```bash
$ gradle
```

<span data-ttu-id="5cdec-165">這會產生可以使用 Service Fabric Azure CLI 工具來部署的 Service Fabric 應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="5cdec-165">This will produce a Service Fabric application package that can be deployed using Service Fabric CLI tools.</span></span>

### <a name="deploy-service-fabric-cli"></a><span data-ttu-id="5cdec-166">部署 Service Fabric CLI</span><span class="sxs-lookup"><span data-stu-id="5cdec-166">Deploy Service Fabric CLI</span></span>

<span data-ttu-id="5cdec-167">hello 為 install.sh 指令碼包含 hello 所需服務網狀架構 CLI (sfctl) 命令 toodeploy hello 應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="5cdec-167">hello install.sh script contains hello necessary Service Fabric CLI (sfctl) commands toodeploy hello application package.</span></span>
<span data-ttu-id="5cdec-168">執行 hello 為 install.sh 指令碼 toodeploy hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5cdec-168">Run hello install.sh script toodeploy hello application.</span></span>

```bash
$ ./install.sh
```

## <a name="next-steps"></a><span data-ttu-id="5cdec-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5cdec-169">Next steps</span></span>

* [<span data-ttu-id="5cdec-170">開始使用 Service Fabric CLI</span><span class="sxs-lookup"><span data-stu-id="5cdec-170">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
