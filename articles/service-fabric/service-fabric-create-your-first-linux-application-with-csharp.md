---
title: "aaaCreate 第一個 Azure microservices 上的應用程式使用 C# 的 Linux |Microsoft 文件"
description: "使用 C# 建立和部署 Service Fabric 應用程式"
services: service-fabric
documentationcenter: csharp
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 5a96d21d-fa4a-4dc2-abe8-a830a3482fb1
ms.service: service-fabric
ms.devlang: csharp
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/21/2017
ms.author: subramar
ms.openlocfilehash: 68d685e130be338ebcdb2f1af24b66d1e14f580a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-azure-service-fabric-application"></a><span data-ttu-id="e26a3-103">建立第一個 Azure Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="e26a3-103">Create your first Azure Service Fabric application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e26a3-104">C# - Windows</span><span class="sxs-lookup"><span data-stu-id="e26a3-104">C# - Windows</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
> * [<span data-ttu-id="e26a3-105">Java - Linux</span><span class="sxs-lookup"><span data-stu-id="e26a3-105">Java - Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
> * [<span data-ttu-id="e26a3-106">C# - Linux</span><span class="sxs-lookup"><span data-stu-id="e26a3-106">C# - Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

<span data-ttu-id="e26a3-107">Service Fabric 提供了在 Linux 上建置服務的 .NET Core 和 Java SDK。</span><span class="sxs-lookup"><span data-stu-id="e26a3-107">Service Fabric provides SDKs for building services on Linux in both .NET Core and Java.</span></span> <span data-ttu-id="e26a3-108">在本教學課程中，我們看看 toocreate 適用於 Linux 和組建服務，使用 C# (.NET Core) 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e26a3-108">In this tutorial, we look at how toocreate an application for Linux and build a service using C# (.NET Core).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e26a3-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="e26a3-109">Prerequisites</span></span>
<span data-ttu-id="e26a3-110">開始之前，請確定您已 [設定 Linux 開發環境](service-fabric-get-started-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="e26a3-110">Before you get started, make sure that you have [set up your Linux development environment](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="e26a3-111">如果您使用 Mac OS X，您可以 [使用 Vagrant 在虛擬機器中設定 Linux 一整體環境](service-fabric-get-started-mac.md)。</span><span class="sxs-lookup"><span data-stu-id="e26a3-111">If you are using Mac OS X, you can [set up a Linux one-box environment in a virtual machine using Vagrant](service-fabric-get-started-mac.md).</span></span>

<span data-ttu-id="e26a3-112">您也想 tooinstall hello[服務網狀架構 CLI](service-fabric-cli.md)</span><span class="sxs-lookup"><span data-stu-id="e26a3-112">You will also want tooinstall hello [Service Fabric CLI](service-fabric-cli.md)</span></span>

### <a name="install-and-set-up-hello-generators-for-csharp"></a><span data-ttu-id="e26a3-113">安裝和設定 CSharp hello 產生器</span><span class="sxs-lookup"><span data-stu-id="e26a3-113">Install and set up hello generators for CSharp</span></span>
<span data-ttu-id="e26a3-114">Service Fabric 提供的 Scaffolding 工具可協助您從終端機使用 Yeoman 範本產生器建立 Service Fabric CSharp 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e26a3-114">Service Fabric provides scaffolding tools which will help you create a Service Fabric CSharp application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="e26a3-115">請遵循下列 tooensure 您尚未使用您的電腦上的 CSharp hello Service Fabric yeoman 範本產生器的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="e26a3-115">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator for CSharp working on your machine.</span></span>
1. <span data-ttu-id="e26a3-116">在電腦上安裝 nodejs 和 NPM</span><span class="sxs-lookup"><span data-stu-id="e26a3-116">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="e26a3-117">在電腦上從 NPM 安裝 [Yeoman](http://yeoman.io/) 範本產生器</span><span class="sxs-lookup"><span data-stu-id="e26a3-117">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="e26a3-118">從 NPM 安裝 hello 服務網狀架構 Yeo Java 應用程式產生器</span><span class="sxs-lookup"><span data-stu-id="e26a3-118">Install hello Service Fabric Yeo Java application generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfcsharp
  ```

## <a name="create-hello-application"></a><span data-ttu-id="e26a3-119">建立 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="e26a3-119">Create hello application</span></span>
<span data-ttu-id="e26a3-120">Service Fabric 應用程式可以包含一或多個服務，每個都有特定角色中傳送嗨應用程式的功能。</span><span class="sxs-lookup"><span data-stu-id="e26a3-120">A Service Fabric application can contain one or more services, each with a specific role in delivering hello application's functionality.</span></span> <span data-ttu-id="e26a3-121">hello Service Fabric [Yeoman](http://yeoman.io/) CSharp，您安裝最後一個步驟中，產生器可讓您輕鬆 toocreate 第一個服務和 tooadd 多更新的版本。</span><span class="sxs-lookup"><span data-stu-id="e26a3-121">hello Service Fabric [Yeoman](http://yeoman.io/) generator for CSharp, which you installed in last step, makes it easy toocreate your first service and tooadd more later.</span></span> <span data-ttu-id="e26a3-122">讓我們 Yeoman toocreate 應用程式使用單一的服務。</span><span class="sxs-lookup"><span data-stu-id="e26a3-122">Let's use Yeoman toocreate an application with a single service.</span></span>

1. <span data-ttu-id="e26a3-123">在終端機中，輸入下列命令 toostart 建置 hello scaffolding hello:`yo azuresfcsharp`</span><span class="sxs-lookup"><span data-stu-id="e26a3-123">In a terminal, type hello following command toostart building hello scaffolding: `yo azuresfcsharp`</span></span>
2. <span data-ttu-id="e26a3-124">為您的應用程式命名。</span><span class="sxs-lookup"><span data-stu-id="e26a3-124">Name your application.</span></span>
3. <span data-ttu-id="e26a3-125">選擇您的第一個服務的 hello 類型並將它命名。</span><span class="sxs-lookup"><span data-stu-id="e26a3-125">Choose hello type of your first service and name it.</span></span> <span data-ttu-id="e26a3-126">基於 hello 本教學課程中，我們選擇可靠的動作項目服務。</span><span class="sxs-lookup"><span data-stu-id="e26a3-126">For hello purposes of this tutorial, we choose a Reliable Actor Service.</span></span>

   ![適用於 C# 的 Service Fabric Yeoman 產生器][sf-yeoman]

> [!NOTE]
> <span data-ttu-id="e26a3-128">如需 hello 選項的詳細資訊，請參閱[Service Fabric 程式設計模型概觀](service-fabric-choose-framework.md)。</span><span class="sxs-lookup"><span data-stu-id="e26a3-128">For more information about hello options, see [Service Fabric programming model overview](service-fabric-choose-framework.md).</span></span>
>
>

## <a name="build-hello-application"></a><span data-ttu-id="e26a3-129">建置 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="e26a3-129">Build hello application</span></span>
<span data-ttu-id="e26a3-130">hello 服務網狀架構 Yeoman 範本包含建置指令碼，您可以使用從終端機 hello toobuild hello 應用程式 （之後瀏覽 toohello 應用程式資料夾）。</span><span class="sxs-lookup"><span data-stu-id="e26a3-130">hello Service Fabric Yeoman templates include a build script that you can use toobuild hello app from hello terminal (after navigating toohello application folder).</span></span>

  ```sh
 cd myapp
 ./build.sh
  ```

## <a name="deploy-hello-application"></a><span data-ttu-id="e26a3-131">部署 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="e26a3-131">Deploy hello application</span></span>

<span data-ttu-id="e26a3-132">建置 hello 應用程式之後，您可以將它部署 toohello 本機叢集。</span><span class="sxs-lookup"><span data-stu-id="e26a3-132">Once hello application is built, you can deploy it toohello local cluster.</span></span>

1. <span data-ttu-id="e26a3-133">Toohello 本機 Service Fabric 叢集連線。</span><span class="sxs-lookup"><span data-stu-id="e26a3-133">Connect toohello local Service Fabric cluster.</span></span>

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. <span data-ttu-id="e26a3-134">提供在 hello 範本 toocopy hello 應用程式封裝 toohello 叢集映像存放區、 註冊 hello 應用程式類型，以及建立 hello 應用程式的執行個體，請執行 hello 安裝指令碼。</span><span class="sxs-lookup"><span data-stu-id="e26a3-134">Run hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

    ```bash
    ./install.sh
    ```

<span data-ttu-id="e26a3-135">部署的 hello 建置應用程式是相同 hello 做為任何其他的 Service Fabric 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e26a3-135">Deploying hello built application is hello same as any other Service Fabric application.</span></span> <span data-ttu-id="e26a3-136">請參閱 hello 說明文件[管理 Service Fabric 應用程式以 hello 服務網狀架構 CLI](service-fabric-application-lifecycle-sfctl.md)如需詳細指示。</span><span class="sxs-lookup"><span data-stu-id="e26a3-136">See hello documentation on [managing a Service Fabric application with hello Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) for detailed instructions.</span></span>

<span data-ttu-id="e26a3-137">參數 toothese 命令可以在 hello 應用程式封裝內的 hello 產生資訊清單中找到。</span><span class="sxs-lookup"><span data-stu-id="e26a3-137">Parameters toothese commands can be found in hello generated manifests inside hello application package.</span></span>

<span data-ttu-id="e26a3-138">一旦部署的 hello 應用程式，開啟瀏覽器並瀏覽至[Service Fabric 總管](service-fabric-visualizing-your-cluster.md)在[http://localhost:19080/總管](http://localhost:19080/Explorer)。</span><span class="sxs-lookup"><span data-stu-id="e26a3-138">Once hello application has been deployed, open a browser and navigate to [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) at [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="e26a3-139">然後，展開 hello**應用程式**節點，請注意，現在您的應用程式類型的項目，另一個用於 hello 該類型的第一個執行個體。</span><span class="sxs-lookup"><span data-stu-id="e26a3-139">Then, expand hello **Applications** node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>

## <a name="start-hello-test-client-and-perform-a-failover"></a><span data-ttu-id="e26a3-140">啟動 hello 測試用戶端，然後執行容錯移轉</span><span class="sxs-lookup"><span data-stu-id="e26a3-140">Start hello test client and perform a failover</span></span>
<span data-ttu-id="e26a3-141">動作項目專案沒有任何屬於自己的項目。</span><span class="sxs-lookup"><span data-stu-id="e26a3-141">Actor projects do not do anything on their own.</span></span> <span data-ttu-id="e26a3-142">它們需要另一個服務或用戶端 toosend 這些訊息。</span><span class="sxs-lookup"><span data-stu-id="e26a3-142">They require another service or client toosend them messages.</span></span> <span data-ttu-id="e26a3-143">hello 動作項目範本包含簡單的測試指令碼，您可以搭配 toointeract hello 動作項目服務。</span><span class="sxs-lookup"><span data-stu-id="e26a3-143">hello actor template includes a simple test script that you can use toointeract with hello actor service.</span></span>

1. <span data-ttu-id="e26a3-144">執行使用 hello 監看式公用程式 toosee hello 輸出 hello 行動服務的 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="e26a3-144">Run hello script using hello watch utility toosee hello output of hello actor service.</span></span>

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```
2. <span data-ttu-id="e26a3-145">在 Service Fabric 總管 中，找出裝載 hello hello 行動服務的主要複本的節點。</span><span class="sxs-lookup"><span data-stu-id="e26a3-145">In Service Fabric Explorer, locate node hosting hello primary replica for hello actor service.</span></span> <span data-ttu-id="e26a3-146">在 hello 以下螢幕擷取畫面，它可以是節點 3。</span><span class="sxs-lookup"><span data-stu-id="e26a3-146">In hello screenshot below, it is node 3.</span></span>

    ![Service Fabric 總管中尋找 hello 主要複本][sfx-primary]
3. <span data-ttu-id="e26a3-148">按一下您在 hello 先前步驟中，找到並選取 hello 節點**停用 （重新啟動）**從 hello 動作 功能表。</span><span class="sxs-lookup"><span data-stu-id="e26a3-148">Click hello node you found in hello previous step, then select **Deactivate (restart)** from hello Actions menu.</span></span> <span data-ttu-id="e26a3-149">這個動作會在您強制容錯移轉 tooa 次要複本執行另一個節點上的本機叢集，重新啟動一個節點。</span><span class="sxs-lookup"><span data-stu-id="e26a3-149">This action restarts one node in your local cluster forcing a failover tooa secondary replica running on another node.</span></span> <span data-ttu-id="e26a3-150">當您執行此動作，請注意 toohello 輸出 hello 測試用戶端與 hello 計數器繼續 tooincrement 儘管 hello 容錯移轉附註。</span><span class="sxs-lookup"><span data-stu-id="e26a3-150">As you perform this action, pay attention toohello output from hello test client and note that hello counter continues tooincrement despite hello failover.</span></span>

## <a name="adding-more-services-tooan-existing-application"></a><span data-ttu-id="e26a3-151">新增更多服務 tooan 現有應用程式</span><span class="sxs-lookup"><span data-stu-id="e26a3-151">Adding more services tooan existing application</span></span>

<span data-ttu-id="e26a3-152">tooadd 另一個 tooan 建立服務應用程式已經使用`yo`，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="e26a3-152">tooadd another service tooan application already created using `yo`, perform hello following steps:</span></span>
1. <span data-ttu-id="e26a3-153">變更 hello 現有應用程式的根目錄 toohello。</span><span class="sxs-lookup"><span data-stu-id="e26a3-153">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="e26a3-154">例如， `cd ~/YeomanSamples/MyApplication`，如果`MyApplication`是 hello Yeoman 所建立的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e26a3-154">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="e26a3-155">執行 `yo azuresfcsharp:AddService`</span><span class="sxs-lookup"><span data-stu-id="e26a3-155">Run `yo azuresfcsharp:AddService`</span></span>

## <a name="migrating-from-projectjson-toocsproj"></a><span data-ttu-id="e26a3-156">從 project.json too.csproj 移轉</span><span class="sxs-lookup"><span data-stu-id="e26a3-156">Migrating from project.json too.csproj</span></span>
1. <span data-ttu-id="e26a3-157">執行 'dotnet 移轉' 在專案根目錄中，會將移轉所有 hello project.json toocsproj 格式。</span><span class="sxs-lookup"><span data-stu-id="e26a3-157">Running 'dotnet migrate' in project root directory will migrate all hello project.json toocsproj format.</span></span>
2. <span data-ttu-id="e26a3-158">更新 hello 專案據以參考專案檔中的 toocsproj 檔案。</span><span class="sxs-lookup"><span data-stu-id="e26a3-158">Update hello project references accordingly toocsproj files in project files.</span></span>
3. <span data-ttu-id="e26a3-159">更新 hello 中的專案檔案名稱 toocsproj 檔 build.sh。</span><span class="sxs-lookup"><span data-stu-id="e26a3-159">Update hello project file names toocsproj files in build.sh.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e26a3-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e26a3-160">Next steps</span></span>

* [<span data-ttu-id="e26a3-161">深入了解 Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="e26a3-161">Learn more about Reliable Actors</span></span>](service-fabric-reliable-actors-introduction.md)
* [<span data-ttu-id="e26a3-162">互動使用 hello 服務網狀架構 CLI Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="e26a3-162">Interacting with Service Fabric clusters using hello Service Fabric CLI</span></span>](service-fabric-cli.md)
* <span data-ttu-id="e26a3-163">了解 [Service Fabric 支援選項](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="e26a3-163">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>
* [<span data-ttu-id="e26a3-164">開始使用 Service Fabric CLI</span><span class="sxs-lookup"><span data-stu-id="e26a3-164">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-csharp/yeoman-csharp.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-csharp/sfx-primary.png
