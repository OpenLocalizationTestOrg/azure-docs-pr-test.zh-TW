---
title: "aaaCreate Linux 上的 Azure Service Fabric 可靠執行者 Java 應用程式 |Microsoft 文件"
description: "深入了解如何 toocreate 和部署 Java Service Fabric 可靠執行者應用程式在五分鐘。"
services: service-fabric
documentationcenter: java
author: rwike77
manager: timlt
editor: 
ms.assetid: 02b51f11-5d78-4c54-bb68-8e128677783e
ms.service: service-fabric
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: ryanwi
ms.openlocfilehash: 11496b767811c89969c65d1682d843448eb6a922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-service-fabric-reliable-actors-application-on-linux"></a><span data-ttu-id="da74e-103">在 Linux 上建立第一個 Java Service Fabric Reliable Actors 應用程式</span><span class="sxs-lookup"><span data-stu-id="da74e-103">Create your first Java Service Fabric Reliable Actors application on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="da74e-104">C# - Windows</span><span class="sxs-lookup"><span data-stu-id="da74e-104">C# - Windows</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
> * [<span data-ttu-id="da74e-105">Java - Linux</span><span class="sxs-lookup"><span data-stu-id="da74e-105">Java - Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
> * [<span data-ttu-id="da74e-106">C# - Linux</span><span class="sxs-lookup"><span data-stu-id="da74e-106">C# - Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

<span data-ttu-id="da74e-107">本快速入門可協助您在短短幾分鐘內在 Linux 開發環境中建立第一個 Azure Service Fabric Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="da74e-107">This quick-start helps you create your first Azure Service Fabric Java application in a Linux development environment in just a few minutes.</span></span>  <span data-ttu-id="da74e-108">當您完成時，您必須在 hello 本機開發叢集上執行簡單 Java 單一服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="da74e-108">When you are finished, you'll have a simple Java single-service application running on hello local development cluster.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="da74e-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="da74e-109">Prerequisites</span></span>
<span data-ttu-id="da74e-110">開始之前，安裝 hello Service Fabric SDK、 hello 服務網狀架構 CLI，並設定開發叢集，在您[Linux 開發環境](service-fabric-get-started-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="da74e-110">Before you get started, install hello Service Fabric SDK, hello Service Fabric CLI, and setup a development cluster in your [Linux development environment](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="da74e-111">如果您使用 Mac OS X，您可以[使用 Vagrant 在虛擬機器中設定 Linux 開發環境](service-fabric-get-started-mac.md)。</span><span class="sxs-lookup"><span data-stu-id="da74e-111">If you are using Mac OS X, you can [set up a Linux development environment in a virtual machine using Vagrant](service-fabric-get-started-mac.md).</span></span>

<span data-ttu-id="da74e-112">您也想 tooinstall hello[服務網狀架構 CLI](service-fabric-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="da74e-112">You will also want tooinstall hello [Service Fabric CLI](service-fabric-cli.md).</span></span>

### <a name="install-and-set-up-hello-generators-for-java"></a><span data-ttu-id="da74e-113">安裝及設定 java hello 產生器</span><span class="sxs-lookup"><span data-stu-id="da74e-113">Install and set up hello generators for Java</span></span>
<span data-ttu-id="da74e-114">Service Fabric 提供的 Scaffolding 工具可協助您從終端機使用 Yeoman 範本產生器建立 Service Fabric Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="da74e-114">Service Fabric provides scaffolding tools which will help you create a Service Fabric Java application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="da74e-115">請遵循下列 tooensure 您尚未在電腦上使用 for Java 的 hello Service Fabric yeoman 範本產生器的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="da74e-115">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator for Java working on your machine.</span></span>
1. <span data-ttu-id="da74e-116">在電腦上安裝 nodejs 和 NPM</span><span class="sxs-lookup"><span data-stu-id="da74e-116">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="da74e-117">在電腦上從 NPM 安裝 [Yeoman](http://yeoman.io/) 範本產生器</span><span class="sxs-lookup"><span data-stu-id="da74e-117">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="da74e-118">從 NPM 安裝 hello 服務網狀架構 Yeo Java 應用程式產生器</span><span class="sxs-lookup"><span data-stu-id="da74e-118">Install hello Service Fabric Yeo Java application generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfjava
  ```

## <a name="create-hello-application"></a><span data-ttu-id="da74e-119">建立 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="da74e-119">Create hello application</span></span>
<span data-ttu-id="da74e-120">Service Fabric 應用程式包含一個或多個服務，每個都有特定角色中傳送嗨應用程式的功能。</span><span class="sxs-lookup"><span data-stu-id="da74e-120">A Service Fabric application contains one or more services, each with a specific role in delivering hello application's functionality.</span></span> <span data-ttu-id="da74e-121">hello 產生器安裝在 hello 最後一個區段中，可讓您輕鬆 toocreate 第一個服務和 tooadd 多更新的版本。</span><span class="sxs-lookup"><span data-stu-id="da74e-121">hello generator you installed in hello last section, makes it easy toocreate your first service and tooadd more later.</span></span>  <span data-ttu-id="da74e-122">您也可以使用適用於 Eclipse 的外掛程式，建立、建置及部署 Service Fabric Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="da74e-122">You can also create, build, and deploy Service Fabric Java applications using a plugin for Eclipse.</span></span> <span data-ttu-id="da74e-123">請參閱[使用 Eclipse 建立和部署第一個 Java 應用程式](service-fabric-get-started-eclipse.md)。</span><span class="sxs-lookup"><span data-stu-id="da74e-123">See [Create and deploy your first Java application using Eclipse](service-fabric-get-started-eclipse.md).</span></span> <span data-ttu-id="da74e-124">這個快速入門中，使用 Yeoman toocreate 應用程式的單一服務，用來儲存和取得計數器值。</span><span class="sxs-lookup"><span data-stu-id="da74e-124">For this quick start, use Yeoman toocreate an application with a single service that stores and gets a counter value.</span></span>

1. <span data-ttu-id="da74e-125">在終端機中，輸入 ``yo azuresfjava``。</span><span class="sxs-lookup"><span data-stu-id="da74e-125">In a terminal, type ``yo azuresfjava``.</span></span>
2. <span data-ttu-id="da74e-126">為您的應用程式命名。</span><span class="sxs-lookup"><span data-stu-id="da74e-126">Name your application.</span></span>
3. <span data-ttu-id="da74e-127">選擇您的第一個服務的 hello 類型並將它命名。</span><span class="sxs-lookup"><span data-stu-id="da74e-127">Choose hello type of your first service and name it.</span></span> <span data-ttu-id="da74e-128">在本教學課程中，選擇 Reliable Actor 服務。</span><span class="sxs-lookup"><span data-stu-id="da74e-128">For this tutorial, choose a Reliable Actor Service.</span></span> <span data-ttu-id="da74e-129">如需有關 hello 其他類型的服務，請參閱[Service Fabric 程式設計模型概觀](service-fabric-choose-framework.md)。</span><span class="sxs-lookup"><span data-stu-id="da74e-129">For more information about hello other types of services, see [Service Fabric programming model overview](service-fabric-choose-framework.md).</span></span>
   <span data-ttu-id="da74e-130">![適用於 Java 的 Service Fabric Yeoman 產生器][sf-yeoman]</span><span class="sxs-lookup"><span data-stu-id="da74e-130">![Service Fabric Yeoman generator for Java][sf-yeoman]</span></span>

## <a name="build-hello-application"></a><span data-ttu-id="da74e-131">建置 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="da74e-131">Build hello application</span></span>
<span data-ttu-id="da74e-132">hello 服務網狀架構 Yeoman 範本包括的組建指令碼[Gradle](https://gradle.org/)，而您可以使用從終端機 hello toobuild hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="da74e-132">hello Service Fabric Yeoman templates include a build script for [Gradle](https://gradle.org/), which you can use toobuild hello application from hello terminal.</span></span>
<span data-ttu-id="da74e-133">從 Maven 擷取的 Service Fabric Java 相依性。</span><span class="sxs-lookup"><span data-stu-id="da74e-133">Service Fabric Java dependencies get fetched from Maven.</span></span> <span data-ttu-id="da74e-134">toobuild 及 hello 服務網狀架構 Java 應用程式上的工作，您必須確認您有 JDK 且 Gradle 安裝 tooensure。</span><span class="sxs-lookup"><span data-stu-id="da74e-134">toobuild and work on hello Service Fabric Java applications, you need tooensure that you have JDK and Gradle installed.</span></span> <span data-ttu-id="da74e-135">如果尚未安裝，您可以執行 hello 下列 tooinstall JDK(openjdk-8-jdk) 和 Gradle-</span><span class="sxs-lookup"><span data-stu-id="da74e-135">If not yet installed, you can run hello following tooinstall JDK(openjdk-8-jdk) and Gradle -</span></span>

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

<span data-ttu-id="da74e-136">toobuild 和套件 hello 應用程式，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="da74e-136">toobuild and package hello application, run hello following:</span></span>

  ```bash
  cd myapp
  gradle
  ```

## <a name="deploy-hello-application"></a><span data-ttu-id="da74e-137">部署 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="da74e-137">Deploy hello application</span></span>
<span data-ttu-id="da74e-138">建置 hello 應用程式之後，您可以將它部署 toohello 本機叢集。</span><span class="sxs-lookup"><span data-stu-id="da74e-138">Once hello application is built, you can deploy it toohello local cluster.</span></span>

1. <span data-ttu-id="da74e-139">Toohello 本機 Service Fabric 叢集連線。</span><span class="sxs-lookup"><span data-stu-id="da74e-139">Connect toohello local Service Fabric cluster.</span></span>

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. <span data-ttu-id="da74e-140">提供在 hello 範本 toocopy hello 應用程式封裝 toohello 叢集映像存放區、 註冊 hello 應用程式類型，以及建立 hello 應用程式的執行個體，請執行 hello 安裝指令碼。</span><span class="sxs-lookup"><span data-stu-id="da74e-140">Run hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

    ```bash
    ./install.sh
    ```

<span data-ttu-id="da74e-141">部署的 hello 建置應用程式是相同 hello 做為任何其他的 Service Fabric 應用程式。</span><span class="sxs-lookup"><span data-stu-id="da74e-141">Deploying hello built application is hello same as any other Service Fabric application.</span></span> <span data-ttu-id="da74e-142">請參閱 hello 說明文件[管理 Service Fabric 應用程式以 hello 服務網狀架構 CLI](service-fabric-application-lifecycle-sfctl.md)如需詳細指示。</span><span class="sxs-lookup"><span data-stu-id="da74e-142">See hello documentation on [managing a Service Fabric application with hello Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) for detailed instructions.</span></span>

<span data-ttu-id="da74e-143">參數 toothese 命令可以在 hello 應用程式封裝內的 hello 產生資訊清單中找到。</span><span class="sxs-lookup"><span data-stu-id="da74e-143">Parameters toothese commands can be found in hello generated manifests inside hello application package.</span></span>

<span data-ttu-id="da74e-144">一旦部署的 hello 應用程式，開啟瀏覽器並瀏覽至[Service Fabric 總管](service-fabric-visualizing-your-cluster.md)在[http://localhost:19080/總管](http://localhost:19080/Explorer)。</span><span class="sxs-lookup"><span data-stu-id="da74e-144">Once hello application has been deployed, open a browser and navigate to [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) at [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span>
<span data-ttu-id="da74e-145">然後，展開 hello**應用程式**節點，請注意，現在您的應用程式類型的項目，另一個用於 hello 該類型的第一個執行個體。</span><span class="sxs-lookup"><span data-stu-id="da74e-145">Then, expand hello **Applications** node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>

## <a name="start-hello-test-client-and-perform-a-failover"></a><span data-ttu-id="da74e-146">啟動 hello 測試用戶端，然後執行容錯移轉</span><span class="sxs-lookup"><span data-stu-id="da74e-146">Start hello test client and perform a failover</span></span>
<span data-ttu-id="da74e-147">動作項目不會進行任何各自獨立的但需要其他服務或用戶端 toosend 這些訊息。</span><span class="sxs-lookup"><span data-stu-id="da74e-147">Actors do not do anything on their own, they require another service or client toosend them messages.</span></span> <span data-ttu-id="da74e-148">hello 動作項目範本包含簡單的測試指令碼，您可以搭配 toointeract hello 動作項目服務。</span><span class="sxs-lookup"><span data-stu-id="da74e-148">hello actor template includes a simple test script that you can use toointeract with hello actor service.</span></span>

1. <span data-ttu-id="da74e-149">執行使用 hello 監看式公用程式 toosee hello 輸出 hello 行動服務的 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="da74e-149">Run hello script using hello watch utility toosee hello output of hello actor service.</span></span>  <span data-ttu-id="da74e-150">hello 測試指令碼會呼叫 hello `setCountAsync()` hello 執行者 tooincrement 計數器，方法會呼叫 hello `getCountAsync()` hello 執行者 tooget hello 新計數器的值，並顯示該值 toohello 主控台上的方法。</span><span class="sxs-lookup"><span data-stu-id="da74e-150">hello test script calls hello `setCountAsync()` method on hello actor tooincrement a counter, calls hello `getCountAsync()` method on hello actor tooget hello new counter value, and displays that value toohello console.</span></span>

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```

2. <span data-ttu-id="da74e-151">在 Service Fabric 總管中，找出 hello 節點裝載 hello 主要複本 hello 動作項目服務。</span><span class="sxs-lookup"><span data-stu-id="da74e-151">In Service Fabric Explorer, locate hello node hosting hello primary replica for hello actor service.</span></span> <span data-ttu-id="da74e-152">在 hello 以下螢幕擷取畫面，它可以是節點 3。</span><span class="sxs-lookup"><span data-stu-id="da74e-152">In hello screenshot below, it is node 3.</span></span> <span data-ttu-id="da74e-153">hello 主要服務複本控點會讀取和寫入作業。</span><span class="sxs-lookup"><span data-stu-id="da74e-153">hello primary service replica handles read and write operations.</span></span>  <span data-ttu-id="da74e-154">Toohello 次要複本，0 和 1 hello 下列螢幕擷取畫面中的節點上執行時，會再複寫服務狀態的變更。</span><span class="sxs-lookup"><span data-stu-id="da74e-154">Changes in service state are then replicated out toohello secondary replicas, running on nodes 0 and 1 in hello screen shot below.</span></span>

    ![Service Fabric 總管中尋找 hello 主要複本][sfx-primary]

3. <span data-ttu-id="da74e-156">在**節點**，按一下您在 hello 先前步驟中，找到並選取 hello 節點**停用 （重新啟動）**從 hello 動作 功能表。</span><span class="sxs-lookup"><span data-stu-id="da74e-156">In **Nodes**, click hello node you found in hello previous step, then select **Deactivate (restart)** from hello Actions menu.</span></span> <span data-ttu-id="da74e-157">這個動作會重新啟動執行 hello 主要服務複本的 hello 節點，並強制 hello 另一個節點上執行的次要複本的容錯移轉 tooone。</span><span class="sxs-lookup"><span data-stu-id="da74e-157">This action restarts hello node running hello primary service replica and forces a failover tooone of hello secondary replicas running on another node.</span></span>  <span data-ttu-id="da74e-158">該次要複本會提升的 tooprimary、 另一個次要複本上建立另一個節點，而 hello 主要複本就會開始 tootake 讀取/寫入作業。</span><span class="sxs-lookup"><span data-stu-id="da74e-158">That secondary replica is promoted tooprimary, another secondary replica is created on a different node, and hello primary replica begins tootake read/write operations.</span></span> <span data-ttu-id="da74e-159">Hello 節點重新啟動時，觀賞 hello 輸出 hello 測試用戶端與 hello 計數器繼續 tooincrement 儘管 hello 容錯移轉附註。</span><span class="sxs-lookup"><span data-stu-id="da74e-159">As hello node restarts, watch hello output from hello test client and note that hello counter continues tooincrement despite hello failover.</span></span>

## <a name="remove-hello-application"></a><span data-ttu-id="da74e-160">移除 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="da74e-160">Remove hello application</span></span>
<span data-ttu-id="da74e-161">使用提供 hello 範本 toodelete hello 應用程式執行個體中的 hello 解除安裝指令碼、 取消登錄 hello 應用程式封裝，並移除 hello 應用程式套件 hello 叢集映像存放區。</span><span class="sxs-lookup"><span data-stu-id="da74e-161">Use hello uninstall script provided in hello template toodelete hello application instance, unregister hello application package, and remove hello application package from hello cluster's image store.</span></span>

```bash
./uninstall.sh
```

<span data-ttu-id="da74e-162">Service Fabric 總管 中看到的 hello 應用程式和應用程式類型不會再出現在 hello**應用程式**節點。</span><span class="sxs-lookup"><span data-stu-id="da74e-162">In Service Fabric explorer you see that hello application and application type no longer appear in hello **Applications** node.</span></span>

## <a name="service-fabric-java-libraries-on-maven"></a><span data-ttu-id="da74e-163">Maven 上的 Service Fabric Java 程式庫</span><span class="sxs-lookup"><span data-stu-id="da74e-163">Service Fabric Java libraries on Maven</span></span>
<span data-ttu-id="da74e-164">Service Fabric Java 程式庫已裝載於 Maven 中。</span><span class="sxs-lookup"><span data-stu-id="da74e-164">Service Fabric Java libraries have been hosted in Maven.</span></span> <span data-ttu-id="da74e-165">您可以在 hello 新增 hello 相依性``pom.xml``或``build.gradle``從您專案 toouse 服務網狀架構 Java 程式庫**mavenCentral**。</span><span class="sxs-lookup"><span data-stu-id="da74e-165">You can add hello dependencies in hello ``pom.xml`` or ``build.gradle`` of your projects toouse Service Fabric Java libraries from **mavenCentral**.</span></span>

### <a name="actors"></a><span data-ttu-id="da74e-166">動作項目</span><span class="sxs-lookup"><span data-stu-id="da74e-166">Actors</span></span>

<span data-ttu-id="da74e-167">您應用程式的 Service Fabric Reliable Actor 支援。</span><span class="sxs-lookup"><span data-stu-id="da74e-167">Service Fabric Reliable Actor support for your application.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-actors-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-actors-preview:0.10.0'
  }
  ```

### <a name="services"></a><span data-ttu-id="da74e-168">服務</span><span class="sxs-lookup"><span data-stu-id="da74e-168">Services</span></span>

<span data-ttu-id="da74e-169">您應用程式的 Service Fabric 無狀態服務支援。</span><span class="sxs-lookup"><span data-stu-id="da74e-169">Service Fabric Stateless Service support for your application.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-services-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-services-preview:0.10.0'
  }
  ```

### <a name="others"></a><span data-ttu-id="da74e-170">其他</span><span class="sxs-lookup"><span data-stu-id="da74e-170">Others</span></span>
#### <a name="transport"></a><span data-ttu-id="da74e-171">傳輸</span><span class="sxs-lookup"><span data-stu-id="da74e-171">Transport</span></span>

<span data-ttu-id="da74e-172">Service Fabric Java 應用程式的傳輸層支援。</span><span class="sxs-lookup"><span data-stu-id="da74e-172">Transport layer support for Service Fabric Java application.</span></span> <span data-ttu-id="da74e-173">您不需要 tooexplicitly 將此相依性 tooyour Reliable Actor 或服務應用程式，除非您在 hello 傳輸層級進行程式設計。</span><span class="sxs-lookup"><span data-stu-id="da74e-173">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications, unless you program at hello transport layer.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-transport-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-transport-preview:0.10.0'
  }
  ```

#### <a name="fabric-support"></a><span data-ttu-id="da74e-174">網狀架構支援</span><span class="sxs-lookup"><span data-stu-id="da74e-174">Fabric support</span></span>

<span data-ttu-id="da74e-175">系統層級支援適用於 Service Fabric，交談 toonative Service Fabric 執行階段。</span><span class="sxs-lookup"><span data-stu-id="da74e-175">System level support for Service Fabric, which talks toonative Service Fabric runtime.</span></span> <span data-ttu-id="da74e-176">您不需要 tooexplicitly 加入此相依性 tooyour Reliable Actor 或服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="da74e-176">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications.</span></span> <span data-ttu-id="da74e-177">從 Maven 自動擷取這取得，當您包含 hello 上述其他相依性。</span><span class="sxs-lookup"><span data-stu-id="da74e-177">This gets fetched automatically from Maven, when you include hello other dependencies above.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-preview:0.10.0'
  }
  ```

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a><span data-ttu-id="da74e-178">移轉舊服務網狀架構 Java 應用程式 toobe 搭配 Maven 使用</span><span class="sxs-lookup"><span data-stu-id="da74e-178">Migrating old Service Fabric Java applications toobe used with Maven</span></span>
<span data-ttu-id="da74e-179">我們最近已從 Service Fabric Java SDK tooMaven 儲存機制移服務網狀架構 Java 文件庫。</span><span class="sxs-lookup"><span data-stu-id="da74e-179">We have recently moved Service Fabric Java libraries from Service Fabric Java SDK tooMaven repository.</span></span> <span data-ttu-id="da74e-180">雖然 hello 新應用程式，您可以產生使用 Yeoman 或 Eclipse 中，將會產生 （這會是可以與 Maven toowork） 最新版本更新的專案，您可以更新您現有的 Service Fabric 無狀態或執行者 Java 應用程式，而且已使用 hello 服務網狀架構 Java SDK 更早版本，從 Maven toouse hello 服務網狀架構 Java 相依性。</span><span class="sxs-lookup"><span data-stu-id="da74e-180">While hello new applications you generate using Yeoman or Eclipse, will generate latest updated projects (which will be able toowork with Maven), you can update your existing Service Fabric stateless or actor Java applications, which were using hello Service Fabric Java SDK earlier, toouse hello Service Fabric Java dependencies from Maven.</span></span> <span data-ttu-id="da74e-181">請遵循所述的 hello 步驟[這裡](service-fabric-migrate-old-javaapp-to-use-maven.md)tooensure Maven 適用於較舊的應用程式。</span><span class="sxs-lookup"><span data-stu-id="da74e-181">Please follow hello steps mentioned [here](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure your older application works with Maven.</span></span>

## <a name="next-steps"></a><span data-ttu-id="da74e-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="da74e-182">Next steps</span></span>

* [<span data-ttu-id="da74e-183">使用 Eclipse 在 Linux 上建立第一個 Service Fabric Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="da74e-183">Create your first Service Fabric Java application on Linux using Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="da74e-184">深入了解 Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="da74e-184">Learn more about Reliable Actors</span></span>](service-fabric-reliable-actors-introduction.md)
* [<span data-ttu-id="da74e-185">互動使用 hello 服務網狀架構 CLI Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="da74e-185">Interact with Service Fabric clusters using hello Service Fabric CLI</span></span>](service-fabric-cli.md)
* <span data-ttu-id="da74e-186">了解 [Service Fabric 支援選項](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="da74e-186">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>
* [<span data-ttu-id="da74e-187">開始使用 Service Fabric CLI</span><span class="sxs-lookup"><span data-stu-id="da74e-187">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-yeoman.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-java/sfx-primary.png
[sf-eclipse-templates]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-eclipse-templates.png
