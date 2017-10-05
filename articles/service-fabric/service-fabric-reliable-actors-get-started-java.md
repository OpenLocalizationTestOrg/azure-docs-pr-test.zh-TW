---
title: "使用 Java 建立您的第一個動作項目型 Azure 微服務 | Microsoft Docs"
description: "本教學課程將引導您使用 Service Fabric Reliable Actors，建立、偵錯及部署簡易動作項目型服務的步驟。"
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
ms.openlocfilehash: 288f1ed1016f50031065e66444d2562427194dc7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="getting-started-with-reliable-actors"></a><span data-ttu-id="f4586-103">開始使用 Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="f4586-103">Getting started with Reliable Actors</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f4586-104">Windows 上的 C# </span><span class="sxs-lookup"><span data-stu-id="f4586-104">C# on Windows</span></span>](service-fabric-reliable-actors-get-started.md)
> * [<span data-ttu-id="f4586-105">在 Linux 上使用 Java</span><span class="sxs-lookup"><span data-stu-id="f4586-105">Java on Linux</span></span>](service-fabric-reliable-actors-get-started-java.md)
> 
> 

<span data-ttu-id="f4586-106">本文說明 Azure Service Fabric Reliable Actors 的基本概念，並將逐步引導您在 Java 中建立及部署簡單的 Reliable Actors 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f4586-106">This article explains the basics of Azure Service Fabric Reliable Actors and walks you through creating and deploying a simple Reliable Actor application in Java.</span></span>

## <a name="installation-and-setup"></a><span data-ttu-id="f4586-107">安裝與設定</span><span class="sxs-lookup"><span data-stu-id="f4586-107">Installation and setup</span></span>
<span data-ttu-id="f4586-108">開始之前，確定機器上已設定 Service Fabric 開發環境。</span><span class="sxs-lookup"><span data-stu-id="f4586-108">Before you start, make sure you have the Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="f4586-109">如果您需要加以設定，請移至[在 Mac 上開始使用](service-fabric-get-started-mac.md)或[在 Linux 上開始使用](service-fabric-get-started-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="f4586-109">If you need to set it up, go to [getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="f4586-110">基本概念</span><span class="sxs-lookup"><span data-stu-id="f4586-110">Basic concepts</span></span>
<span data-ttu-id="f4586-111">若要開始使用 Reliable Actors，您只需要了解幾個基本概念：</span><span class="sxs-lookup"><span data-stu-id="f4586-111">To get started with Reliable Actors, you only need to understand a few basic concepts:</span></span>

* <span data-ttu-id="f4586-112">**動作項目服務**。</span><span class="sxs-lookup"><span data-stu-id="f4586-112">**Actor service**.</span></span> <span data-ttu-id="f4586-113">Reliable Actors 封裝在可在 Service Fabric 基礎結構內部署的 Reliable Services 中。</span><span class="sxs-lookup"><span data-stu-id="f4586-113">Reliable Actors are packaged in Reliable Services that can be deployed in the Service Fabric infrastructure.</span></span> <span data-ttu-id="f4586-114">動作項目執行個體會在指定的服務執行個體中啟動。</span><span class="sxs-lookup"><span data-stu-id="f4586-114">Actor instances are activated in a named service instance.</span></span>
* <span data-ttu-id="f4586-115">**動作項目註冊**。</span><span class="sxs-lookup"><span data-stu-id="f4586-115">**Actor registration**.</span></span> <span data-ttu-id="f4586-116">和 Reliable Services 一樣，Reliable Actor 服務必須向 Service Fabric 執行階段註冊。</span><span class="sxs-lookup"><span data-stu-id="f4586-116">As with Reliable Services, a Reliable Actor service needs to be registered with the Service Fabric runtime.</span></span> <span data-ttu-id="f4586-117">此外，動作項目類型必須向 Actor 執行階段註冊。</span><span class="sxs-lookup"><span data-stu-id="f4586-117">In addition, the actor type needs to be registered with the Actor runtime.</span></span>
* <span data-ttu-id="f4586-118">**動作項目介面**。</span><span class="sxs-lookup"><span data-stu-id="f4586-118">**Actor interface**.</span></span> <span data-ttu-id="f4586-119">動作項目介面用於定義動作項目的強型別公用介面。</span><span class="sxs-lookup"><span data-stu-id="f4586-119">The actor interface is used to define a strongly typed public interface of an actor.</span></span> <span data-ttu-id="f4586-120">在 Reliable Actor 模型術語中，動作項目介面定義動作項目可以了解並處理的訊息類型。</span><span class="sxs-lookup"><span data-stu-id="f4586-120">In the Reliable Actor model terminology, the actor interface defines the types of messages that the actor can understand and process.</span></span> <span data-ttu-id="f4586-121">其他的動作項目或用戶端應用程式會使用動作項目介面將訊息「傳送」(非同步) 給動作項目。</span><span class="sxs-lookup"><span data-stu-id="f4586-121">The actor interface is used by other actors and client applications to "send" (asynchronously) messages to the actor.</span></span> <span data-ttu-id="f4586-122">Reliable Actors 可實作多個介面。</span><span class="sxs-lookup"><span data-stu-id="f4586-122">Reliable Actors can implement multiple interfaces.</span></span>
* <span data-ttu-id="f4586-123">**ActorProxy 類別**。</span><span class="sxs-lookup"><span data-stu-id="f4586-123">**ActorProxy class**.</span></span> <span data-ttu-id="f4586-124">用戶端應用程式會使用 ActorProxy 類別來叫用透過動作項目介面公開的方法。</span><span class="sxs-lookup"><span data-stu-id="f4586-124">The ActorProxy class is used by client applications to invoke the methods exposed through the actor interface.</span></span> <span data-ttu-id="f4586-125">ActorProxy 類別提供兩個重要的功能：</span><span class="sxs-lookup"><span data-stu-id="f4586-125">The ActorProxy class provides two important functionalities:</span></span>
  
  * <span data-ttu-id="f4586-126">名稱解析︰它能夠在叢集中找到動作項目 (尋找裝載動作項目的叢集節點)。</span><span class="sxs-lookup"><span data-stu-id="f4586-126">Name resolution: It is able to locate the actor in the cluster (find the node of the cluster where it is hosted).</span></span>
  * <span data-ttu-id="f4586-127">處理失敗：它可以重試方法叫用並重新解析動作項目位置，例如在需要動作項目重新定位至叢集中另一個節點失敗後進行。</span><span class="sxs-lookup"><span data-stu-id="f4586-127">Failure handling: It can retry method invocations and re-resolve the actor location after, for example, a failure that requires the actor to be relocated to another node in the cluster.</span></span>

<span data-ttu-id="f4586-128">值得一提的是下列與動作項目介面相關的規則︰</span><span class="sxs-lookup"><span data-stu-id="f4586-128">The following rules that pertain to actor interfaces are worth mentioning:</span></span>

* <span data-ttu-id="f4586-129">動作項目介面方法無法多載。</span><span class="sxs-lookup"><span data-stu-id="f4586-129">Actor interface methods cannot be overloaded.</span></span>
* <span data-ttu-id="f4586-130">動作項目介面方法不能有 out、ref 或選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="f4586-130">Actor interface methods must not have out, ref, or optional parameters.</span></span>
* <span data-ttu-id="f4586-131">不支援泛型介面。</span><span class="sxs-lookup"><span data-stu-id="f4586-131">Generic interfaces are not supported.</span></span>

## <a name="create-an-actor-service"></a><span data-ttu-id="f4586-132">建立動作項目服務</span><span class="sxs-lookup"><span data-stu-id="f4586-132">Create an actor service</span></span>
<span data-ttu-id="f4586-133">以建立新 Service Fabric 應用程式的方式開始。</span><span class="sxs-lookup"><span data-stu-id="f4586-133">Start by creating a new Service Fabric application.</span></span> <span data-ttu-id="f4586-134">適用於 Linux 的 Service Fabric SDK 包含 Yeoman 產生器，可提供具無狀態服務之 Service Fabric 應用程式的樣板。</span><span class="sxs-lookup"><span data-stu-id="f4586-134">The Service Fabric SDK for Linux includes a Yeoman generator to provide the scaffolding for a Service Fabric application with a stateless service.</span></span> <span data-ttu-id="f4586-135">執行下列 Yeoman 命令開始作業：</span><span class="sxs-lookup"><span data-stu-id="f4586-135">Start by running the following Yeoman command:</span></span>

```bash
$ yo azuresfjava
```

<span data-ttu-id="f4586-136">遵循指示建立 **Reliable Actors 服務**。</span><span class="sxs-lookup"><span data-stu-id="f4586-136">Follow the instructions to create a **Reliable Actor Service**.</span></span> <span data-ttu-id="f4586-137">本教學課程中，將應用程式命名為 HelloWorldActorApplication，將動作項目命名為 HelloWorldActor。</span><span class="sxs-lookup"><span data-stu-id="f4586-137">For this tutorial, name the application "HelloWorldActorApplication" and the actor "HelloWorldActor."</span></span> <span data-ttu-id="f4586-138">將會建立下列樣板：</span><span class="sxs-lookup"><span data-stu-id="f4586-138">The following scaffolding will be created:</span></span>

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

## <a name="reliable-actors-basic-building-blocks"></a><span data-ttu-id="f4586-139">Reliable Actors 項目基本建置組塊</span><span class="sxs-lookup"><span data-stu-id="f4586-139">Reliable Actors basic building blocks</span></span>
<span data-ttu-id="f4586-140">稍早所述的基本概念轉化為 Reliable Actors 服務的基本建置組塊。</span><span class="sxs-lookup"><span data-stu-id="f4586-140">The basic concepts described earlier translate into the basic building blocks of a Reliable Actor service.</span></span>

### <a name="actor-interface"></a><span data-ttu-id="f4586-141">動作項目介面</span><span class="sxs-lookup"><span data-stu-id="f4586-141">Actor interface</span></span>
<span data-ttu-id="f4586-142">包含動作項目的介面定義。</span><span class="sxs-lookup"><span data-stu-id="f4586-142">This contains the interface definition for the actor.</span></span> <span data-ttu-id="f4586-143">這個介面定義由動作項目實作與呼叫動作項目的用戶端所共用的動作項目合約，因此通常適合在不同於動作項目實作的地方定義該合約，並可由多個其他服務或用戶端應用程式共用。</span><span class="sxs-lookup"><span data-stu-id="f4586-143">This interface defines the actor contract that is shared by the actor implementation and the clients calling the actor, so it typically makes sense to define it in a place that is separate from the actor implementation and can be shared by multiple other services or client applications.</span></span>

<span data-ttu-id="f4586-144">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`：</span><span class="sxs-lookup"><span data-stu-id="f4586-144">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:</span></span>

```java
public interface HelloWorldActor extends Actor {
    @Readonly   
    CompletableFuture<Integer> getCountAsync();

    CompletableFuture<?> setCountAsync(int count);
}
```

### <a name="actor-service"></a><span data-ttu-id="f4586-145">動作項目服務</span><span class="sxs-lookup"><span data-stu-id="f4586-145">Actor service</span></span>
<span data-ttu-id="f4586-146">這包含您的動作項目實作和動作項目註冊碼。</span><span class="sxs-lookup"><span data-stu-id="f4586-146">This contains your actor implementation and actor registration code.</span></span> <span data-ttu-id="f4586-147">動作項目類別會實作動作項目介面。</span><span class="sxs-lookup"><span data-stu-id="f4586-147">The actor class implements the actor interface.</span></span> <span data-ttu-id="f4586-148">這是您的動作項目工作之處。</span><span class="sxs-lookup"><span data-stu-id="f4586-148">This is where your actor does its work.</span></span>

<span data-ttu-id="f4586-149">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`：</span><span class="sxs-lookup"><span data-stu-id="f4586-149">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:</span></span>

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

### <a name="actor-registration"></a><span data-ttu-id="f4586-150">動作項目註冊</span><span class="sxs-lookup"><span data-stu-id="f4586-150">Actor registration</span></span>
<span data-ttu-id="f4586-151">必須在 Service Fabric 執行階段中以某個服務類型註冊動作項目服務。</span><span class="sxs-lookup"><span data-stu-id="f4586-151">The actor service must be registered with a service type in the Service Fabric runtime.</span></span> <span data-ttu-id="f4586-152">為了讓動作項目服務執行您的動作項目執行個體，也必須向動作項目服務註冊動作項目類型。</span><span class="sxs-lookup"><span data-stu-id="f4586-152">In order for the Actor Service to run your actor instances, your actor type must also be registered with the Actor Service.</span></span> <span data-ttu-id="f4586-153">`ActorRuntime` 註冊方法會替動作項目執行這項工作。</span><span class="sxs-lookup"><span data-stu-id="f4586-153">The `ActorRuntime` registration method performs this work for actors.</span></span>

<span data-ttu-id="f4586-154">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`：</span><span class="sxs-lookup"><span data-stu-id="f4586-154">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:</span></span>

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

### <a name="test-client"></a><span data-ttu-id="f4586-155">Test client</span><span class="sxs-lookup"><span data-stu-id="f4586-155">Test client</span></span>
<span data-ttu-id="f4586-156">這是簡單的測試用戶端應用程式，可以和 Service Fabric 應用程式分開執行，以測試您的動作項目服務。</span><span class="sxs-lookup"><span data-stu-id="f4586-156">This is a simple test client application you can run separately from the Service Fabric application to test your actor service.</span></span> <span data-ttu-id="f4586-157">這是 ActorProxy 可用來啟動和與動作項目執行個體通訊的位置範例。</span><span class="sxs-lookup"><span data-stu-id="f4586-157">This is an example of where the ActorProxy can be used to activate and communicate with actor instances.</span></span> <span data-ttu-id="f4586-158">它不會與您的服務一同部署。</span><span class="sxs-lookup"><span data-stu-id="f4586-158">It does not get deployed with your service.</span></span>

### <a name="the-application"></a><span data-ttu-id="f4586-159">應用程式</span><span class="sxs-lookup"><span data-stu-id="f4586-159">The application</span></span>
<span data-ttu-id="f4586-160">最後，應用程式會將動作項目服務以及您未來可能會加入的其他任何服務封裝在一起以便部署。</span><span class="sxs-lookup"><span data-stu-id="f4586-160">Finally, the application packages the actor service and any other services you might add in the future together for deployment.</span></span> <span data-ttu-id="f4586-161">它包含了 ApplicationManifest.xml 以及動作項目服務套件的預留位置。</span><span class="sxs-lookup"><span data-stu-id="f4586-161">It contains the *ApplicationManifest.xml* and place holders for the actor service package.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="f4586-162">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="f4586-162">Run the application</span></span>

<span data-ttu-id="f4586-163">Yeoman 樣板包含可建置應用程式的 gradle 指令碼，以及可部署和移除應用程式的 bash 指令碼。</span><span class="sxs-lookup"><span data-stu-id="f4586-163">The Yeoman scaffolding includes a gradle script to build the application and bash scripts to deploy and remove the application.</span></span> <span data-ttu-id="f4586-164">若要部署應用程式，請先使用 gradle 來建置應用程式︰</span><span class="sxs-lookup"><span data-stu-id="f4586-164">To deploy the application, first build the application with gradle:</span></span>

```bash
$ gradle
```

<span data-ttu-id="f4586-165">這會產生可以使用 Service Fabric Azure CLI 工具來部署的 Service Fabric 應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="f4586-165">This will produce a Service Fabric application package that can be deployed using Service Fabric CLI tools.</span></span>

### <a name="deploy-service-fabric-cli"></a><span data-ttu-id="f4586-166">部署 Service Fabric CLI</span><span class="sxs-lookup"><span data-stu-id="f4586-166">Deploy Service Fabric CLI</span></span>

<span data-ttu-id="f4586-167">Install.sh 指令碼包含部署應用程式封裝所需的 Service Fabric CLI (sfctl) 命令。</span><span class="sxs-lookup"><span data-stu-id="f4586-167">The install.sh script contains the necessary Service Fabric CLI (sfctl) commands to deploy the application package.</span></span>
<span data-ttu-id="f4586-168">請執行 install.sh 指令碼來部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="f4586-168">Run the install.sh script to deploy the application.</span></span>

```bash
$ ./install.sh
```

## <a name="next-steps"></a><span data-ttu-id="f4586-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f4586-169">Next steps</span></span>

* [<span data-ttu-id="f4586-170">開始使用 Service Fabric CLI</span><span class="sxs-lookup"><span data-stu-id="f4586-170">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
