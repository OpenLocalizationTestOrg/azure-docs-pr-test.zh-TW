---
title: "使用 Java 建立您第一個可靠的 Azure 微服務 | Microsoft Docs"
description: "概述使用無狀態與具狀態服務來建立 Microsoft Azure Service Fabric 應用程式。"
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
ms.openlocfilehash: 1ebabe4844732412e04bab8c277f7ebbc4a5737c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-reliable-services"></a><span data-ttu-id="03f62-103">開始使用 Reliable Service</span><span class="sxs-lookup"><span data-stu-id="03f62-103">Get started with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="03f62-104">Windows 上的 C# </span><span class="sxs-lookup"><span data-stu-id="03f62-104">C# on Windows</span></span>](service-fabric-reliable-services-quick-start.md)
> * [<span data-ttu-id="03f62-105">在 Linux 上使用 Java</span><span class="sxs-lookup"><span data-stu-id="03f62-105">Java on Linux</span></span>](service-fabric-reliable-services-quick-start-java.md)
>
>

<span data-ttu-id="03f62-106">本文說明 Azure Service Fabric Reliable Services 的基本概念，並將逐步引導您建立及部署以 Java 撰寫的簡單 Reliable Services 應用程式。</span><span class="sxs-lookup"><span data-stu-id="03f62-106">This article explains the basics of Azure Service Fabric Reliable Services and walks you through creating and deploying a simple Reliable Service application written in Java.</span></span> <span data-ttu-id="03f62-107">此 Microsoft Virtual Academy 影片也示範如何建立無狀態的 Reliable Service：<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span><span class="sxs-lookup"><span data-stu-id="03f62-107">This Microsoft Virtual Academy video also shows you how to create a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span></span>  
<img src="./media/service-fabric-reliable-services-quick-start-java/ReliableServicesJavaVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="installation-and-setup"></a><span data-ttu-id="03f62-108">安裝與設定</span><span class="sxs-lookup"><span data-stu-id="03f62-108">Installation and setup</span></span>
<span data-ttu-id="03f62-109">開始之前，確定機器上已設定 Service Fabric 開發環境。</span><span class="sxs-lookup"><span data-stu-id="03f62-109">Before you start, make sure you have the Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="03f62-110">如果您需要加以設定，請移至[在 Mac 上開始使用](service-fabric-get-started-mac.md)或[在 Linux 上開始使用](service-fabric-get-started-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="03f62-110">If you need to set it up, go to [getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="03f62-111">基本概念</span><span class="sxs-lookup"><span data-stu-id="03f62-111">Basic concepts</span></span>
<span data-ttu-id="03f62-112">若要開始使用 Reliable Services，您只需要了解幾個基本概念：</span><span class="sxs-lookup"><span data-stu-id="03f62-112">To get started with Reliable Services, you only need to understand a few basic concepts:</span></span>

* <span data-ttu-id="03f62-113">**服務類型**：這是您的服務實作。</span><span class="sxs-lookup"><span data-stu-id="03f62-113">**Service type**: This is your service implementation.</span></span> <span data-ttu-id="03f62-114">它是由您撰寫的類別定義，它會擴充 `StatelessService` 與其中使用的任何其他程式碼或相依性，以及名稱與版本號碼。</span><span class="sxs-lookup"><span data-stu-id="03f62-114">It is defined by the class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span></span>
* <span data-ttu-id="03f62-115">**具名服務執行個體**：若要執行您的服務，可以建立您服務類型的具名執行個體，很像您建立類別類型的物件執行個體一樣。</span><span class="sxs-lookup"><span data-stu-id="03f62-115">**Named service instance**: To run your service, you create named instances of your service type, much like you create object instances of a class type.</span></span> <span data-ttu-id="03f62-116">服務執行個體實際上就是您所撰寫服務類型的物件具現化。</span><span class="sxs-lookup"><span data-stu-id="03f62-116">Service instances are in fact object instantiations of your service class that you write.</span></span>
* <span data-ttu-id="03f62-117">**服務主機**：您建立的具名服務執行個體需要在主機內部執行。</span><span class="sxs-lookup"><span data-stu-id="03f62-117">**Service host**: The named service instances you create need to run inside a host.</span></span> <span data-ttu-id="03f62-118">服務主機只是您服務的執行個體可執行所在的程序。</span><span class="sxs-lookup"><span data-stu-id="03f62-118">The service host is just a process where instances of your service can run.</span></span>
* <span data-ttu-id="03f62-119">**服務註冊**：註冊可將所有項目結合在一起。</span><span class="sxs-lookup"><span data-stu-id="03f62-119">**Service registration**: Registration brings everything together.</span></span> <span data-ttu-id="03f62-120">服務類型必須在服務主機的 Service Fabric 執行階段中註冊，以允許 Service Fabric 建立其執行個體來執行。</span><span class="sxs-lookup"><span data-stu-id="03f62-120">The service type must be registered with the Service Fabric runtime in a service host to allow Service Fabric to create instances of it to run.</span></span>  

## <a name="create-a-stateless-service"></a><span data-ttu-id="03f62-121">建立無狀態服務</span><span class="sxs-lookup"><span data-stu-id="03f62-121">Create a stateless service</span></span>
<span data-ttu-id="03f62-122">從建立 Service Fabric 應用程式開始著手。</span><span class="sxs-lookup"><span data-stu-id="03f62-122">Start by creating a Service Fabric application.</span></span> <span data-ttu-id="03f62-123">適用於 Linux 的 Service Fabric SDK 包含 Yeoman 產生器，可提供具無狀態服務之 Service Fabric 應用程式的樣板。</span><span class="sxs-lookup"><span data-stu-id="03f62-123">The Service Fabric SDK for Linux includes a Yeoman generator to provide the scaffolding for a Service Fabric application with a stateless service.</span></span> <span data-ttu-id="03f62-124">執行下列 Yeoman 命令開始作業：</span><span class="sxs-lookup"><span data-stu-id="03f62-124">Start by running the following Yeoman command:</span></span>

```bash
$ yo azuresfjava
```

<span data-ttu-id="03f62-125">遵循指示建立**可靠的無狀態服務**。</span><span class="sxs-lookup"><span data-stu-id="03f62-125">Follow the instructions to create a **Reliable Stateless Service**.</span></span> <span data-ttu-id="03f62-126">本教學課程中，將應用程式命名為 HelloWorldApplication，將服務命名為 HelloWorld。</span><span class="sxs-lookup"><span data-stu-id="03f62-126">For this tutorial, name the application "HelloWorldApplication" and the service "HelloWorld".</span></span> <span data-ttu-id="03f62-127">結果會包含 `HelloWorldApplication` 和 `HelloWorld` 的目錄。</span><span class="sxs-lookup"><span data-stu-id="03f62-127">The result includes directories for the `HelloWorldApplication` and `HelloWorld`.</span></span>

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

## <a name="implement-the-service"></a><span data-ttu-id="03f62-128">實作服務</span><span class="sxs-lookup"><span data-stu-id="03f62-128">Implement the service</span></span>
<span data-ttu-id="03f62-129">開啟 **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**。</span><span class="sxs-lookup"><span data-stu-id="03f62-129">Open **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**.</span></span> <span data-ttu-id="03f62-130">這個類別會定義服務類型，而且可以執行任何程式碼。</span><span class="sxs-lookup"><span data-stu-id="03f62-130">This class defines the service type, and can run any code.</span></span> <span data-ttu-id="03f62-131">服務 API 為您的程式碼提供兩個進入點：</span><span class="sxs-lookup"><span data-stu-id="03f62-131">The service API provides two entry points for your code:</span></span>

* <span data-ttu-id="03f62-132">開放式的進入點方法 (稱為 `runAsync()`)，您可以在這裡開始執行任何工作負載，包括長時間執行的計算工作負載。</span><span class="sxs-lookup"><span data-stu-id="03f62-132">An open-ended entry point method, called `runAsync()`, where you can begin executing any workloads, including long-running compute workloads.</span></span>

```java
@Override
protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {
    ...
}
```

* <span data-ttu-id="03f62-133">通訊進入點，您可以在這裡插入選擇的通訊堆疊。</span><span class="sxs-lookup"><span data-stu-id="03f62-133">A communication entry point where you can plug in your communication stack of choice.</span></span> <span data-ttu-id="03f62-134">這就是您可以開始接收來自使用者和其他服務要求的地方。</span><span class="sxs-lookup"><span data-stu-id="03f62-134">This is where you can start receiving requests from users and other services.</span></span>

```java
@Override
protected List<ServiceInstanceListener> createServiceInstanceListeners() {
    ...
}
```

<span data-ttu-id="03f62-135">在本教學課程中，我們會著重在 `runAsync()` 進入點方法。</span><span class="sxs-lookup"><span data-stu-id="03f62-135">In this tutorial, we focus on the `runAsync()` entry point method.</span></span> <span data-ttu-id="03f62-136">這就是您可以立即開始執行程式碼的地方。</span><span class="sxs-lookup"><span data-stu-id="03f62-136">This is where you can immediately start running your code.</span></span>

### <a name="runasync"></a><span data-ttu-id="03f62-137">RunAsync</span><span class="sxs-lookup"><span data-stu-id="03f62-137">RunAsync</span></span>
<span data-ttu-id="03f62-138">當服務的執行個體已放置並且可以執行時，平台會呼叫這個方法。</span><span class="sxs-lookup"><span data-stu-id="03f62-138">The platform calls this method when an instance of a service is placed and ready to execute.</span></span> <span data-ttu-id="03f62-139">針對無狀態服務，這僅表示開啟服務執行個體的時間。</span><span class="sxs-lookup"><span data-stu-id="03f62-139">For a stateless service, that simply means when the service instance is opened.</span></span> <span data-ttu-id="03f62-140">會提供取消語彙基元以協調服務執行個體何時需要關閉。</span><span class="sxs-lookup"><span data-stu-id="03f62-140">A cancellation token is provided to coordinate when your service instance needs to be closed.</span></span> <span data-ttu-id="03f62-141">在 Service Fabric 中，服務執行個體的開啟/關閉循環可能會在整個服務存留期中發生許多次。</span><span class="sxs-lookup"><span data-stu-id="03f62-141">In Service Fabric, this open/close cycle of a service instance can occur many times over the lifetime of the service as a whole.</span></span> <span data-ttu-id="03f62-142">發生這種情形的原因有很多，包括：</span><span class="sxs-lookup"><span data-stu-id="03f62-142">This can happen for various reasons, including:</span></span>

* <span data-ttu-id="03f62-143">系統可能為了資源平衡移動您的服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="03f62-143">The system moves your service instances for resource balancing.</span></span>
* <span data-ttu-id="03f62-144">在您的程式碼中發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="03f62-144">Faults occur in your code.</span></span>
* <span data-ttu-id="03f62-145">應用程式或系統已升級。</span><span class="sxs-lookup"><span data-stu-id="03f62-145">The application or system is upgraded.</span></span>
* <span data-ttu-id="03f62-146">基礎硬體發生中斷。</span><span class="sxs-lookup"><span data-stu-id="03f62-146">The underlying hardware experiences an outage.</span></span>

<span data-ttu-id="03f62-147">此協調流程是由 Service Fabric 管理，可讓您的服務維持高度可用且正確平衡。</span><span class="sxs-lookup"><span data-stu-id="03f62-147">This orchestration is managed by Service Fabric to keep your service highly available and properly balanced.</span></span>

<span data-ttu-id="03f62-148">`runAsync()` 不應該同步封鎖。</span><span class="sxs-lookup"><span data-stu-id="03f62-148">`runAsync()` should not block synchronously.</span></span> <span data-ttu-id="03f62-149">您的 runAsync 實作應該傳回 CompletableFuture，以允許執行階段繼續執行。</span><span class="sxs-lookup"><span data-stu-id="03f62-149">Your implementation of runAsync should return a CompletableFuture to allow the runtime to continue.</span></span> <span data-ttu-id="03f62-150">如果您的工作負載需要實作長時間執行的工作，則該工作應該在 CompletableFuture 內完成。</span><span class="sxs-lookup"><span data-stu-id="03f62-150">If your workload needs to implement a long running task that should be done inside the CompletableFuture.</span></span>

#### <a name="cancellation"></a><span data-ttu-id="03f62-151">取消</span><span class="sxs-lookup"><span data-stu-id="03f62-151">Cancellation</span></span>
<span data-ttu-id="03f62-152">取消您的工作負載是由所提供的取消語彙基元協調的協同努力。</span><span class="sxs-lookup"><span data-stu-id="03f62-152">Cancellation of your workload is a cooperative effort orchestrated by the provided cancellation token.</span></span> <span data-ttu-id="03f62-153">系統會先等待您的工作結束 (依據成功完成、取消或錯誤)，然後才繼續執行。</span><span class="sxs-lookup"><span data-stu-id="03f62-153">The system waits for your task to end (by successful completion, cancellation, or fault) before it moves on.</span></span> <span data-ttu-id="03f62-154">系統要求取消時，務必接受取消權杖、完成任何工作，並儘快結束 `runAsync()`。</span><span class="sxs-lookup"><span data-stu-id="03f62-154">It is important to honor the cancellation token, finish any work, and exit `runAsync()` as quickly as possible when the system requests cancellation.</span></span> <span data-ttu-id="03f62-155">下列範例示範如何處理取消事件：</span><span class="sxs-lookup"><span data-stu-id="03f62-155">The following example demonstrates how to handle a cancellation event:</span></span>

```java
    @Override
    protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {

        // TODO: Replace the following sample code with your own logic
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

### <a name="service-registration"></a><span data-ttu-id="03f62-156">服務註冊</span><span class="sxs-lookup"><span data-stu-id="03f62-156">Service registration</span></span>
<span data-ttu-id="03f62-157">會取消必須在 Service Fabric 執行階段註冊。</span><span class="sxs-lookup"><span data-stu-id="03f62-157">Service types must be registered with the Service Fabric runtime.</span></span> <span data-ttu-id="03f62-158">服務類型是在 `ServiceManifest.xml` 中以及實作 `StatelessService` 的服務類別中定義。</span><span class="sxs-lookup"><span data-stu-id="03f62-158">The service type is defined in the `ServiceManifest.xml` and your service class that implements `StatelessService`.</span></span> <span data-ttu-id="03f62-159">服務註冊是在程序主要進入點中執行。</span><span class="sxs-lookup"><span data-stu-id="03f62-159">Service registration is performed in the process main entry point.</span></span> <span data-ttu-id="03f62-160">在此範例中，程序的主要進入點是 `HelloWorldServiceHost.java`：</span><span class="sxs-lookup"><span data-stu-id="03f62-160">In this example, the process main entry point is `HelloWorldServiceHost.java`:</span></span>

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

## <a name="run-the-application"></a><span data-ttu-id="03f62-161">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="03f62-161">Run the application</span></span>

<span data-ttu-id="03f62-162">Yeoman 樣板包含可建置應用程式的 gradle 指令碼，以及可部署和移除應用程式的 bash 指令碼。</span><span class="sxs-lookup"><span data-stu-id="03f62-162">The Yeoman scaffolding includes a gradle script to build the application and bash scripts to deploy and remove the application.</span></span> <span data-ttu-id="03f62-163">若要執行應用程式，先建置含 gradle的應用程式︰</span><span class="sxs-lookup"><span data-stu-id="03f62-163">To run the application, first build the application with gradle:</span></span>

```bash
$ gradle
```

<span data-ttu-id="03f62-164">這會產生可使用 Service Fabric CLI 來部署的 Service Fabric 應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="03f62-164">This produces a Service Fabric application package that can be deployed using Service Fabric CLI.</span></span>

### <a name="deploy-with-service-fabric-cli"></a><span data-ttu-id="03f62-165">使用 Service Fabric CLI 部署</span><span class="sxs-lookup"><span data-stu-id="03f62-165">Deploy with Service Fabric CLI</span></span>

<span data-ttu-id="03f62-166">Install.sh 指令碼包含部署應用程式套件所需的 Service Fabric CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="03f62-166">The install.sh script contains the necessary Service Fabric CLI commands to deploy the application package.</span></span> <span data-ttu-id="03f62-167">請執行 install.sh 指令碼來部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="03f62-167">Run the install.sh script to deploy the application.</span></span>

```bash
$ ./install.sh
```

## <a name="next-steps"></a><span data-ttu-id="03f62-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="03f62-168">Next steps</span></span>

* [<span data-ttu-id="03f62-169">開始使用 Service Fabric CLI</span><span class="sxs-lookup"><span data-stu-id="03f62-169">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
