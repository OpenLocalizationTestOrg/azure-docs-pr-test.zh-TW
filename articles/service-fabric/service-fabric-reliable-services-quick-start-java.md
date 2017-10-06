---
title: "aaaCreate 您第一次可靠 Azure 微服務在 Java 中的 |Microsoft 文件"
description: "簡介 toocreating 無狀態與可設定狀態服務的 Microsoft Azure Service Fabric 應用程式。"
services: service-fabric
documentationcenter: java
author: vturecek
manager: timlt
editor: 
ms.assetid: 7831886f-7ec4-4aef-95c5-b2469a5b7b5d
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 577d96591797bbfe6be5c1094426b5f1435cca0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-reliable-services"></a><span data-ttu-id="59fe5-103">開始使用 Reliable Service</span><span class="sxs-lookup"><span data-stu-id="59fe5-103">Get started with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="59fe5-104">Windows 上的 C# </span><span class="sxs-lookup"><span data-stu-id="59fe5-104">C# on Windows</span></span>](service-fabric-reliable-services-quick-start.md)
> * [<span data-ttu-id="59fe5-105">在 Linux 上使用 Java</span><span class="sxs-lookup"><span data-stu-id="59fe5-105">Java on Linux</span></span>](service-fabric-reliable-services-quick-start-java.md)
>
>

<span data-ttu-id="59fe5-106">本文章說明 hello Azure Service Fabric 可靠服務基本概念，並將告訴您如何建立及部署在 Java 中撰寫的簡單可靠的服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="59fe5-106">This article explains hello basics of Azure Service Fabric Reliable Services and walks you through creating and deploying a simple Reliable Service application written in Java.</span></span> <span data-ttu-id="59fe5-107">Microsoft Virtual Academy 影片也將示範如何 toocreate 無狀態 Reliable service:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span><span class="sxs-lookup"><span data-stu-id="59fe5-107">This Microsoft Virtual Academy video also shows you how toocreate a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span></span>  
<img src="./media/service-fabric-reliable-services-quick-start-java/ReliableServicesJavaVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="installation-and-setup"></a><span data-ttu-id="59fe5-108">安裝與設定</span><span class="sxs-lookup"><span data-stu-id="59fe5-108">Installation and setup</span></span>
<span data-ttu-id="59fe5-109">開始之前，請確定您擁有 hello Service Fabric 開發環境設定您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="59fe5-109">Before you start, make sure you have hello Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="59fe5-110">如果您需要 tooset 總太移[Mac 上開始使用](service-fabric-get-started-mac.md)或[開始使用 Linux](service-fabric-get-started-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="59fe5-110">If you need tooset it up, go too[getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="59fe5-111">基本概念</span><span class="sxs-lookup"><span data-stu-id="59fe5-111">Basic concepts</span></span>
<span data-ttu-id="59fe5-112">tooget 開始使用可靠的服務，您只需要 toounderstand 某些基本概念：</span><span class="sxs-lookup"><span data-stu-id="59fe5-112">tooget started with Reliable Services, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="59fe5-113">**服務類型**：這是您的服務實作。</span><span class="sxs-lookup"><span data-stu-id="59fe5-113">**Service type**: This is your service implementation.</span></span> <span data-ttu-id="59fe5-114">它由您撰寫可擴充 hello 類別所定義`StatelessService`和任何其他程式碼或使用另有規定，以及名稱和版本號碼的相依性。</span><span class="sxs-lookup"><span data-stu-id="59fe5-114">It is defined by hello class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span></span>
* <span data-ttu-id="59fe5-115">**名為服務執行個體**: toorun 您的服務，您建立您的服務類型的具名執行個體更像建立的類別類型的物件執行個體。</span><span class="sxs-lookup"><span data-stu-id="59fe5-115">**Named service instance**: toorun your service, you create named instances of your service type, much like you create object instances of a class type.</span></span> <span data-ttu-id="59fe5-116">服務執行個體實際上就是您所撰寫服務類型的物件具現化。</span><span class="sxs-lookup"><span data-stu-id="59fe5-116">Service instances are in fact object instantiations of your service class that you write.</span></span>
* <span data-ttu-id="59fe5-117">**服務主機**: hello 名為您建立需要 toorun 主機內部的服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="59fe5-117">**Service host**: hello named service instances you create need toorun inside a host.</span></span> <span data-ttu-id="59fe5-118">只要您的服務執行個體可以在上面執行的處理序 hello 服務主機。</span><span class="sxs-lookup"><span data-stu-id="59fe5-118">hello service host is just a process where instances of your service can run.</span></span>
* <span data-ttu-id="59fe5-119">**服務註冊**：註冊可將所有項目結合在一起。</span><span class="sxs-lookup"><span data-stu-id="59fe5-119">**Service registration**: Registration brings everything together.</span></span> <span data-ttu-id="59fe5-120">hello 服務類型必須註冊以 hello Service Fabric 服務中的執行階段裝載 tooallow Service Fabric toocreate 的執行個體，toorun。</span><span class="sxs-lookup"><span data-stu-id="59fe5-120">hello service type must be registered with hello Service Fabric runtime in a service host tooallow Service Fabric toocreate instances of it toorun.</span></span>  

## <a name="create-a-stateless-service"></a><span data-ttu-id="59fe5-121">建立無狀態服務</span><span class="sxs-lookup"><span data-stu-id="59fe5-121">Create a stateless service</span></span>
<span data-ttu-id="59fe5-122">從建立 Service Fabric 應用程式開始著手。</span><span class="sxs-lookup"><span data-stu-id="59fe5-122">Start by creating a Service Fabric application.</span></span> <span data-ttu-id="59fe5-123">hello Service Fabric SDK for Linux 包含 Yeoman Service Fabric 應用程式與無狀態服務的產生器 tooprovide hello scaffolding。</span><span class="sxs-lookup"><span data-stu-id="59fe5-123">hello Service Fabric SDK for Linux includes a Yeoman generator tooprovide hello scaffolding for a Service Fabric application with a stateless service.</span></span> <span data-ttu-id="59fe5-124">開始執行 hello Yeoman 下列命令：</span><span class="sxs-lookup"><span data-stu-id="59fe5-124">Start by running hello following Yeoman command:</span></span>

```bash
$ yo azuresfjava
```

<span data-ttu-id="59fe5-125">請遵循 hello 指示 toocreate**可靠的無狀態服務**。</span><span class="sxs-lookup"><span data-stu-id="59fe5-125">Follow hello instructions toocreate a **Reliable Stateless Service**.</span></span> <span data-ttu-id="59fe5-126">此教學課程中，名稱 hello 應用程式"HelloWorldApplication 」 和 hello 服務"HelloWorld"。</span><span class="sxs-lookup"><span data-stu-id="59fe5-126">For this tutorial, name hello application "HelloWorldApplication" and hello service "HelloWorld".</span></span> <span data-ttu-id="59fe5-127">hello 結果包含目錄 hello`HelloWorldApplication`和`HelloWorld`。</span><span class="sxs-lookup"><span data-stu-id="59fe5-127">hello result includes directories for hello `HelloWorldApplication` and `HelloWorld`.</span></span>

```bash
HelloWorldApplication/
├── build.gradle
├── HelloWorld
│   ├── build.gradle
│   └── src
│       └── statelessservice
│           ├── HelloWorldServiceHost.java
│           └── HelloWorldService.java
├── HelloWorldApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   └── _readme.txt
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="implement-hello-service"></a><span data-ttu-id="59fe5-128">實作 hello 服務</span><span class="sxs-lookup"><span data-stu-id="59fe5-128">Implement hello service</span></span>
<span data-ttu-id="59fe5-129">開啟 **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**。</span><span class="sxs-lookup"><span data-stu-id="59fe5-129">Open **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**.</span></span> <span data-ttu-id="59fe5-130">這個類別定義 hello 服務型別，而且可以執行任何程式碼。</span><span class="sxs-lookup"><span data-stu-id="59fe5-130">This class defines hello service type, and can run any code.</span></span> <span data-ttu-id="59fe5-131">hello 服務 API 提供兩個進入點的程式碼：</span><span class="sxs-lookup"><span data-stu-id="59fe5-131">hello service API provides two entry points for your code:</span></span>

* <span data-ttu-id="59fe5-132">開放式的進入點方法 (稱為 `runAsync()`)，您可以在這裡開始執行任何工作負載，包括長時間執行的計算工作負載。</span><span class="sxs-lookup"><span data-stu-id="59fe5-132">An open-ended entry point method, called `runAsync()`, where you can begin executing any workloads, including long-running compute workloads.</span></span>

```java
@Override
protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {
    ...
}
```

* <span data-ttu-id="59fe5-133">通訊進入點，您可以在這裡插入選擇的通訊堆疊。</span><span class="sxs-lookup"><span data-stu-id="59fe5-133">A communication entry point where you can plug in your communication stack of choice.</span></span> <span data-ttu-id="59fe5-134">這就是您可以開始接收來自使用者和其他服務要求的地方。</span><span class="sxs-lookup"><span data-stu-id="59fe5-134">This is where you can start receiving requests from users and other services.</span></span>

```java
@Override
protected List<ServiceInstanceListener> createServiceInstanceListeners() {
    ...
}
```

<span data-ttu-id="59fe5-135">在本教學課程中，我們將重點放在 hello`runAsync()`進入點方法。</span><span class="sxs-lookup"><span data-stu-id="59fe5-135">In this tutorial, we focus on hello `runAsync()` entry point method.</span></span> <span data-ttu-id="59fe5-136">這就是您可以立即開始執行程式碼的地方。</span><span class="sxs-lookup"><span data-stu-id="59fe5-136">This is where you can immediately start running your code.</span></span>

### <a name="runasync"></a><span data-ttu-id="59fe5-137">RunAsync</span><span class="sxs-lookup"><span data-stu-id="59fe5-137">RunAsync</span></span>
<span data-ttu-id="59fe5-138">服務的執行個體時放置並準備好 tooexecute hello 平台會呼叫這個方法。</span><span class="sxs-lookup"><span data-stu-id="59fe5-138">hello platform calls this method when an instance of a service is placed and ready tooexecute.</span></span> <span data-ttu-id="59fe5-139">無狀態的服務，這只是表示開啟 hello 服務執行個體時。</span><span class="sxs-lookup"><span data-stu-id="59fe5-139">For a stateless service, that simply means when hello service instance is opened.</span></span> <span data-ttu-id="59fe5-140">取消語彙基元提供 toocoordinate 您服務執行個體需要 toobe 關閉時。</span><span class="sxs-lookup"><span data-stu-id="59fe5-140">A cancellation token is provided toocoordinate when your service instance needs toobe closed.</span></span> <span data-ttu-id="59fe5-141">在 Service Fabric 服務執行個體的此開啟/關閉週期可以發生多次存留 hello hello 服務的整個。</span><span class="sxs-lookup"><span data-stu-id="59fe5-141">In Service Fabric, this open/close cycle of a service instance can occur many times over hello lifetime of hello service as a whole.</span></span> <span data-ttu-id="59fe5-142">發生這種情形的原因有很多，包括：</span><span class="sxs-lookup"><span data-stu-id="59fe5-142">This can happen for various reasons, including:</span></span>

* <span data-ttu-id="59fe5-143">hello 系統移動資源平衡服務執行的個體。</span><span class="sxs-lookup"><span data-stu-id="59fe5-143">hello system moves your service instances for resource balancing.</span></span>
* <span data-ttu-id="59fe5-144">在您的程式碼中發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="59fe5-144">Faults occur in your code.</span></span>
* <span data-ttu-id="59fe5-145">hello 應用程式或系統也會升級。</span><span class="sxs-lookup"><span data-stu-id="59fe5-145">hello application or system is upgraded.</span></span>
* <span data-ttu-id="59fe5-146">hello 基礎硬體發生中斷。</span><span class="sxs-lookup"><span data-stu-id="59fe5-146">hello underlying hardware experiences an outage.</span></span>

<span data-ttu-id="59fe5-147">此協調流程由 Service Fabric tookeep 管理您的服務高可用性且正確平衡。</span><span class="sxs-lookup"><span data-stu-id="59fe5-147">This orchestration is managed by Service Fabric tookeep your service highly available and properly balanced.</span></span>

<span data-ttu-id="59fe5-148">`runAsync()` 不應該同步封鎖。</span><span class="sxs-lookup"><span data-stu-id="59fe5-148">`runAsync()` should not block synchronously.</span></span> <span data-ttu-id="59fe5-149">RunAsync 的實作應該傳回 CompletableFuture tooallow hello 執行階段 toocontinue。</span><span class="sxs-lookup"><span data-stu-id="59fe5-149">Your implementation of runAsync should return a CompletableFuture tooallow hello runtime toocontinue.</span></span> <span data-ttu-id="59fe5-150">如果您的工作負載需要 tooimplement 長時間執行的工作應該在 hello CompletableFuture。</span><span class="sxs-lookup"><span data-stu-id="59fe5-150">If your workload needs tooimplement a long running task that should be done inside hello CompletableFuture.</span></span>

#### <a name="cancellation"></a><span data-ttu-id="59fe5-151">取消</span><span class="sxs-lookup"><span data-stu-id="59fe5-151">Cancellation</span></span>
<span data-ttu-id="59fe5-152">取消您的工作負載是由提供取消語彙基元的 hello 協調合作式工作。</span><span class="sxs-lookup"><span data-stu-id="59fe5-152">Cancellation of your workload is a cooperative effort orchestrated by hello provided cancellation token.</span></span> <span data-ttu-id="59fe5-153">hello 系統會等到工作 tooend （由成功完成、 取消作業或錯誤） 之間移動之前。</span><span class="sxs-lookup"><span data-stu-id="59fe5-153">hello system waits for your task tooend (by successful completion, cancellation, or fault) before it moves on.</span></span> <span data-ttu-id="59fe5-154">它是重要的 toohonor hello 取消語彙基元，完成任何工作，並結束`runAsync()`hello 系統要求取消盡快。</span><span class="sxs-lookup"><span data-stu-id="59fe5-154">It is important toohonor hello cancellation token, finish any work, and exit `runAsync()` as quickly as possible when hello system requests cancellation.</span></span> <span data-ttu-id="59fe5-155">hello 下列範例會示範如何 toohandle 取消事件：</span><span class="sxs-lookup"><span data-stu-id="59fe5-155">hello following example demonstrates how toohandle a cancellation event:</span></span>

```java
    @Override
    protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {

        // TODO: Replace hello following sample code with your own logic
        // or remove this runAsync override if it's not needed in your service.

        CompletableFuture.runAsync(() -> {
          long iterations = 0;
          while(true)
          {
            cancellationToken.throwIfCancellationRequested();
            logger.log(Level.INFO, "Working-{0}", ++iterations);

            try
            {
              Thread.sleep(1000);
            }
            catch (IOException ex) {}
          }
        });
    }
```

### <a name="service-registration"></a><span data-ttu-id="59fe5-156">服務註冊</span><span class="sxs-lookup"><span data-stu-id="59fe5-156">Service registration</span></span>
<span data-ttu-id="59fe5-157">服務類型必須向 hello Service Fabric 執行階段。</span><span class="sxs-lookup"><span data-stu-id="59fe5-157">Service types must be registered with hello Service Fabric runtime.</span></span> <span data-ttu-id="59fe5-158">hello 服務類型定義於 hello`ServiceManifest.xml`和您的服務類別可實作`StatelessService`。</span><span class="sxs-lookup"><span data-stu-id="59fe5-158">hello service type is defined in hello `ServiceManifest.xml` and your service class that implements `StatelessService`.</span></span> <span data-ttu-id="59fe5-159">服務登錄是在 hello 程序的主要進入點執行。</span><span class="sxs-lookup"><span data-stu-id="59fe5-159">Service registration is performed in hello process main entry point.</span></span> <span data-ttu-id="59fe5-160">在此範例中，hello 程序的主要進入點是`HelloWorldServiceHost.java`:</span><span class="sxs-lookup"><span data-stu-id="59fe5-160">In this example, hello process main entry point is `HelloWorldServiceHost.java`:</span></span>

```java
public static void main(String[] args) throws Exception {
    try {
        ServiceRuntime.registerStatelessServiceAsync("HelloWorldType", (context) -> new HelloWorldService(), Duration.ofSeconds(10));
        logger.log(Level.INFO, "Registered stateless service type HelloWorldType.");
        Thread.sleep(Long.MAX_VALUE);
    }
    catch (Exception ex) {
        logger.log(Level.SEVERE, "Exception in registration:", ex);
        throw ex;
    }
}
```

## <a name="run-hello-application"></a><span data-ttu-id="59fe5-161">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="59fe5-161">Run hello application</span></span>

<span data-ttu-id="59fe5-162">hello Yeoman scaffolding 包含 gradle 指令碼 toobuild hello 應用程式和 bash 指令碼 toodeploy 和移除應用程式。</span><span class="sxs-lookup"><span data-stu-id="59fe5-162">hello Yeoman scaffolding includes a gradle script toobuild hello application and bash scripts toodeploy and remove the application.</span></span> <span data-ttu-id="59fe5-163">toorun hello 應用程式，第一個使用 gradle 的組建 hello 應用程式：</span><span class="sxs-lookup"><span data-stu-id="59fe5-163">toorun hello application, first build hello application with gradle:</span></span>

```bash
$ gradle
```

<span data-ttu-id="59fe5-164">這會產生可使用 Service Fabric CLI 來部署的 Service Fabric 應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="59fe5-164">This produces a Service Fabric application package that can be deployed using Service Fabric CLI.</span></span>

### <a name="deploy-with-service-fabric-cli"></a><span data-ttu-id="59fe5-165">使用 Service Fabric CLI 部署</span><span class="sxs-lookup"><span data-stu-id="59fe5-165">Deploy with Service Fabric CLI</span></span>

<span data-ttu-id="59fe5-166">hello 為 install.sh 指令碼包含 hello 所需服務網狀架構 CLI 命令 toodeploy hello 應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="59fe5-166">hello install.sh script contains hello necessary Service Fabric CLI commands toodeploy hello application package.</span></span> <span data-ttu-id="59fe5-167">執行為 install.sh 的指令碼 toodeploy hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="59fe5-167">Run the install.sh script toodeploy hello application.</span></span>

```bash
$ ./install.sh
```

## <a name="next-steps"></a><span data-ttu-id="59fe5-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="59fe5-168">Next steps</span></span>

* [<span data-ttu-id="59fe5-169">開始使用 Service Fabric CLI</span><span class="sxs-lookup"><span data-stu-id="59fe5-169">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
