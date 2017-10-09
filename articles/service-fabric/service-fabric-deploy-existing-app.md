---
title: "現有的可執行檔 tooAzure Service Fabric aaaDeploy |Microsoft 文件"
description: "逐步解說如何 toopackage 客體可執行檔，讓它可以是現有的應用程式部署 tooa Service Fabric 叢集"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: d799c1c6-75eb-4b8a-9f94-bf4f3dadf4c3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 07/02/2017
ms.author: mfussell;mikhegn
ms.openlocfilehash: 5599802bdb6bda2407a138d77e12148ccb64f437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-guest-executable-tooservice-fabric"></a><span data-ttu-id="00da0-103">部署客體可執行檔 tooService 網狀架構</span><span class="sxs-lookup"><span data-stu-id="00da0-103">Deploy a guest executable tooService Fabric</span></span>
<span data-ttu-id="00da0-104">您可以在 Azure Service Fabric 中將任何類型的程式碼 (例如 Node.js、Java 或 C++) 當作服務來執行。</span><span class="sxs-lookup"><span data-stu-id="00da0-104">You can run any type of code, such as Node.js, Java, or C++ in Azure Service Fabric as a service.</span></span> <span data-ttu-id="00da0-105">Service Fabric 是指 toothese 類型的服務，做為客體可執行檔。</span><span class="sxs-lookup"><span data-stu-id="00da0-105">Service Fabric refers toothese types of services as guest executables.</span></span>

<span data-ttu-id="00da0-106">Service Fabric 將來賓可執行檔視為無狀態服務。</span><span class="sxs-lookup"><span data-stu-id="00da0-106">Guest executables are treated by Service Fabric like stateless services.</span></span> <span data-ttu-id="00da0-107">因此會根據可用性和其他度量將它們放在叢集的節點上。</span><span class="sxs-lookup"><span data-stu-id="00da0-107">As a result, they are placed on nodes in a cluster, based on availability and other metrics.</span></span> <span data-ttu-id="00da0-108">本文說明如何 toopackage 和客體可執行檔 tooa Service Fabric 叢集，部署使用 Visual Studio 或命令列公用程式。</span><span class="sxs-lookup"><span data-stu-id="00da0-108">This article describes how toopackage and deploy a guest executable tooa Service Fabric cluster, by using Visual Studio or a command-line utility.</span></span>

<span data-ttu-id="00da0-109">在本文中，我們會涵蓋 hello 步驟 toopackage 客體可執行檔，並將其部署 tooService 網狀架構。</span><span class="sxs-lookup"><span data-stu-id="00da0-109">In this article, we cover hello steps toopackage a guest executable and deploy it tooService Fabric.</span></span>  

## <a name="benefits-of-running-a-guest-executable-in-service-fabric"></a><span data-ttu-id="00da0-110">在 Service Fabric 中執行來賓可執行檔的優點</span><span class="sxs-lookup"><span data-stu-id="00da0-110">Benefits of running a guest executable in Service Fabric</span></span>
<span data-ttu-id="00da0-111">有數個優點 toorunning 客體可執行檔中的 Service Fabric 叢集：</span><span class="sxs-lookup"><span data-stu-id="00da0-111">There are several advantages toorunning a guest executable in a Service Fabric cluster:</span></span>

* <span data-ttu-id="00da0-112">高可用性。</span><span class="sxs-lookup"><span data-stu-id="00da0-112">High availability.</span></span> <span data-ttu-id="00da0-113">在 Service Fabric 中執行的應用程式都會具有高可用性。</span><span class="sxs-lookup"><span data-stu-id="00da0-113">Applications that run in Service Fabric are made highly available.</span></span> <span data-ttu-id="00da0-114">Service Fabric 會確保應用程式執行個體正在執行。</span><span class="sxs-lookup"><span data-stu-id="00da0-114">Service Fabric ensures that instances of an application are running.</span></span>
* <span data-ttu-id="00da0-115">健康狀況監視。</span><span class="sxs-lookup"><span data-stu-id="00da0-115">Health monitoring.</span></span> <span data-ttu-id="00da0-116">Service Fabric 健全狀況監控會偵測應用程式是否正在執行，如果發生失敗情況，則會提供診斷資訊。</span><span class="sxs-lookup"><span data-stu-id="00da0-116">Service Fabric health monitoring detects if an application is running, and provides diagnostic information if there is a failure.</span></span>   
* <span data-ttu-id="00da0-117">應用程式生命週期管理。</span><span class="sxs-lookup"><span data-stu-id="00da0-117">Application lifecycle management.</span></span> <span data-ttu-id="00da0-118">除了提供沒有停機的升級，Service Fabric 會提供自動回復 toohello 先前的版本，如果沒有在升級期間所報告的錯誤健全狀況事件。</span><span class="sxs-lookup"><span data-stu-id="00da0-118">Besides providing upgrades with no downtime, Service Fabric provides automatic rollback toohello previous version if there is a bad health event reported during an upgrade.</span></span>    
* <span data-ttu-id="00da0-119">密度。</span><span class="sxs-lookup"><span data-stu-id="00da0-119">Density.</span></span> <span data-ttu-id="00da0-120">您可以在叢集中，這麼做可免除在自己的硬體上的每個應用程式 toorun hello 需要執行多個應用程式。</span><span class="sxs-lookup"><span data-stu-id="00da0-120">You can run multiple applications in a cluster, which eliminates hello need for each application toorun on its own hardware.</span></span>
* <span data-ttu-id="00da0-121">探索： 使用 REST 可以呼叫 hello Service Fabric 命名服務 toofind 其他服務 hello 叢集中。</span><span class="sxs-lookup"><span data-stu-id="00da0-121">Discoverability: Using REST you can call hello Service Fabric Naming service toofind other services in hello cluster.</span></span> 

## <a name="samples"></a><span data-ttu-id="00da0-122">範例</span><span class="sxs-lookup"><span data-stu-id="00da0-122">Samples</span></span>
* [<span data-ttu-id="00da0-123">封裝和部署來賓可執行檔的範例</span><span class="sxs-lookup"><span data-stu-id="00da0-123">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="00da0-124">兩個客體可執行檔 （C# 和 nodejs） 通訊透過 hello 命名服務使用 REST 範例</span><span class="sxs-lookup"><span data-stu-id="00da0-124">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="overview-of-application-and-service-manifest-files"></a><span data-ttu-id="00da0-125">應用程式和服務資訊清單檔案的概觀</span><span class="sxs-lookup"><span data-stu-id="00da0-125">Overview of application and service manifest files</span></span>
<span data-ttu-id="00da0-126">部署客體可執行檔的一部分，它是有用的 toounderstand hello Service Fabric 封裝和部署模型中所述[應用程式模型](service-fabric-application-model.md)。</span><span class="sxs-lookup"><span data-stu-id="00da0-126">As part of deploying a guest executable, it is useful toounderstand hello Service Fabric packaging and deployment model as described in [application model](service-fabric-application-model.md).</span></span> <span data-ttu-id="00da0-127">hello Service Fabric 封裝模型依賴兩個 XML 檔案： hello 應用程式和服務資訊清單。</span><span class="sxs-lookup"><span data-stu-id="00da0-127">hello Service Fabric packaging model relies on two XML files: hello application and service manifests.</span></span> <span data-ttu-id="00da0-128">hello 結構描述定義的 hello ApplicationManifest.xml 和 ServiceManifest.xml 檔案會隨 hello 到 Service Fabric SDK *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="00da0-128">hello schema definition for hello ApplicationManifest.xml and ServiceManifest.xml files is installed with hello Service Fabric SDK into *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

* <span data-ttu-id="00da0-129">**應用程式資訊清單**hello 應用程式資訊清單是使用的 toodescribe hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="00da0-129">**Application manifest** hello application manifest is used toodescribe hello application.</span></span> <span data-ttu-id="00da0-130">它會列出 hello 服務組成和使用方式的一或多個服務應部署，例如 hello 執行個體數目的 toodefine 其他參數。</span><span class="sxs-lookup"><span data-stu-id="00da0-130">It lists hello services that compose it, and other parameters that are used toodefine how one or more services should be deployed, such as hello number of instances.</span></span>

  <span data-ttu-id="00da0-131">在 Service Fabric 中，應用程式是部署和升級的單位。</span><span class="sxs-lookup"><span data-stu-id="00da0-131">In Service Fabric, an application is a unit of deployment and upgrade.</span></span> <span data-ttu-id="00da0-132">應用程式可以當作單一單位來升級，而得以掌控可能的失敗和可能需要的回復。</span><span class="sxs-lookup"><span data-stu-id="00da0-132">An application can be upgraded as a single unit where potential failures and potential rollbacks are managed.</span></span> <span data-ttu-id="00da0-133">Service Fabric 可以確保 hello 升級程序將會是成功，或如果 hello 升級失敗，並不會讓 hello 應用程式處於不明或不穩定的狀態。</span><span class="sxs-lookup"><span data-stu-id="00da0-133">Service Fabric guarantees that hello upgrade process is either successful, or, if hello upgrade fails, does not leave hello application in an unknown or unstable state.</span></span>
* <span data-ttu-id="00da0-134">**服務資訊清單**hello 服務資訊清單會描述服務的 hello 元件。</span><span class="sxs-lookup"><span data-stu-id="00da0-134">**Service manifest** hello service manifest describes hello components of a service.</span></span> <span data-ttu-id="00da0-135">它包含資料，例如 hello 名稱和服務類型，其程式碼和組態。</span><span class="sxs-lookup"><span data-stu-id="00da0-135">It includes data, such as hello name and type of service, and its code and configuration.</span></span> <span data-ttu-id="00da0-136">hello 服務資訊清單也包含一些額外的參數可能是一旦部署之後使用 tooconfigure hello 服務。</span><span class="sxs-lookup"><span data-stu-id="00da0-136">hello service manifest also includes some additional parameters that can be used tooconfigure hello service once it is deployed.</span></span>

## <a name="application-package-file-structure"></a><span data-ttu-id="00da0-137">應用程式套件檔案結構</span><span class="sxs-lookup"><span data-stu-id="00da0-137">Application package file structure</span></span>
<span data-ttu-id="00da0-138">toodeploy 應用程式 tooService 網狀架構，hello 應用程式應依照預先定義的目錄結構。</span><span class="sxs-lookup"><span data-stu-id="00da0-138">toodeploy an application tooService Fabric, hello application should follow a predefined directory structure.</span></span> <span data-ttu-id="00da0-139">hello 以下是該結構的範例。</span><span class="sxs-lookup"><span data-stu-id="00da0-139">hello following is an example of that structure.</span></span>

```
|-- ApplicationPackageRoot
    |-- GuestService1Pkg
        |-- Code
            |-- existingapp.exe
        |-- Config
            |-- Settings.xml
        |-- Data
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```

<span data-ttu-id="00da0-140">hello ApplicationPackageRoot 包含定義 hello 應用程式的 hello ApplicationManifest.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="00da0-140">hello ApplicationPackageRoot contains hello ApplicationManifest.xml file that defines hello application.</span></span> <span data-ttu-id="00da0-141">Hello 應用程式中包含每一個服務子目錄是使用的 toocontain 所有 hello hello 服務所需的成品。</span><span class="sxs-lookup"><span data-stu-id="00da0-141">A subdirectory for each service included in hello application is used toocontain all hello artifacts that hello service requires.</span></span> <span data-ttu-id="00da0-142">這些子目錄的 hello ServiceManifest.xml 和，一般而言，下列的 hello:</span><span class="sxs-lookup"><span data-stu-id="00da0-142">These subdirectories are hello ServiceManifest.xml and, typically, hello following:</span></span>

* <span data-ttu-id="00da0-143">*Code*。</span><span class="sxs-lookup"><span data-stu-id="00da0-143">*Code*.</span></span> <span data-ttu-id="00da0-144">此目錄包含 hello 服務程式碼。</span><span class="sxs-lookup"><span data-stu-id="00da0-144">This directory contains hello service code.</span></span>
* <span data-ttu-id="00da0-145">*Config*。此目錄包含 Settings.xml 檔案 （和其他檔案，如有必要） hello 服務可以存取在執行階段 tooretrieve 特定的組態設定。</span><span class="sxs-lookup"><span data-stu-id="00da0-145">*Config*. This directory contains a Settings.xml file (and other files if necessary) that hello service can access at runtime tooretrieve specific configuration settings.</span></span>
* <span data-ttu-id="00da0-146">*Data*。</span><span class="sxs-lookup"><span data-stu-id="00da0-146">*Data*.</span></span> <span data-ttu-id="00da0-147">這是其他目錄 toostore 其他本機資料可能需要 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="00da0-147">This is an additional directory toostore additional local data that hello service may need.</span></span> <span data-ttu-id="00da0-148">資料應該是使用的 toostore 只是暫時的資料。</span><span class="sxs-lookup"><span data-stu-id="00da0-148">Data should be used toostore only ephemeral data.</span></span> <span data-ttu-id="00da0-149">Service Fabric 會複製或 replicate 變更 toohello 資料目錄，如果 hello 服務需要 toobe 重新配置 （例如，在容錯移轉期間）。</span><span class="sxs-lookup"><span data-stu-id="00da0-149">Service Fabric does not copy or replicate changes toohello data directory if hello service needs toobe relocated (for example, during failover).</span></span>

> [!NOTE]
> <span data-ttu-id="00da0-150">您不需要 toocreate hello`config`和`data`目錄，如果您不需要它們。</span><span class="sxs-lookup"><span data-stu-id="00da0-150">You don't have toocreate hello `config` and `data` directories if you don't need them.</span></span>
>
>

## <a name="package-an-existing-executable"></a><span data-ttu-id="00da0-151">封裝現有的執行檔</span><span class="sxs-lookup"><span data-stu-id="00da0-151">Package an existing executable</span></span>
<span data-ttu-id="00da0-152">當封裝客體可執行檔，您可以選擇任一 toouse Visual Studio 專案範本或太[手動建立 hello 應用程式封裝](#manually)。</span><span class="sxs-lookup"><span data-stu-id="00da0-152">When packaging a guest executable, you can choose either toouse a Visual Studio project template or too[create hello application package manually](#manually).</span></span> <span data-ttu-id="00da0-153">使用 Visual Studio，hello 應用程式封裝的結構，並為您建立資訊清單檔案的 hello 新的專案範本。</span><span class="sxs-lookup"><span data-stu-id="00da0-153">Using Visual Studio, hello application package structure and manifest files are created by hello new project template for you.</span></span>

> [!TIP]
> <span data-ttu-id="00da0-154">最簡單方式 toopackage hello 現有的 Windows 服務可執行檔是 toouse Visual Studio 在 Linux toouse Yeoman</span><span class="sxs-lookup"><span data-stu-id="00da0-154">hello easiest way toopackage an existing Windows executable into a service is toouse Visual Studio and on Linux toouse Yeoman</span></span>
>

## <a name="use-visual-studio-toopackage-and-deploy-an-existing-executable"></a><span data-ttu-id="00da0-155">使用 Visual Studio toopackage 及部署現有的可執行檔</span><span class="sxs-lookup"><span data-stu-id="00da0-155">Use Visual Studio toopackage and deploy an existing executable</span></span>
<span data-ttu-id="00da0-156">Visual Studio 提供 Service Fabric 服務範本 toohelp 部署客體可執行檔 tooa Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="00da0-156">Visual Studio provides a Service Fabric service template toohelp you deploy a guest executable tooa Service Fabric cluster.</span></span>

1. <span data-ttu-id="00da0-157">選擇 [檔案]  >  [新增專案]，然後建立 Service Fabric 應用程式。</span><span class="sxs-lookup"><span data-stu-id="00da0-157">Choose **File** > **New Project**, and create a Service Fabric application.</span></span>
2. <span data-ttu-id="00da0-158">選擇**客體可執行檔**作為 hello 服務範本。</span><span class="sxs-lookup"><span data-stu-id="00da0-158">Choose **Guest Executable** as hello service template.</span></span>
3. <span data-ttu-id="00da0-159">按一下**瀏覽**tooselect hello 資料夾與您的可執行檔中的 hello 參數 toocreate hello 服務的 hello 其餘部分填滿。</span><span class="sxs-lookup"><span data-stu-id="00da0-159">Click **Browse** tooselect hello folder with your executable and fill in hello rest of hello parameters toocreate hello service.</span></span>
   * <span data-ttu-id="00da0-160">「Code Package Behavior」。</span><span class="sxs-lookup"><span data-stu-id="00da0-160">*Code Package Behavior*.</span></span> <span data-ttu-id="00da0-161">可以是集合 toocopy 您資料夾 toohello Visual Studio 專案中，所有 hello 內容會很有用，如果 hello 可執行檔不會變更。</span><span class="sxs-lookup"><span data-stu-id="00da0-161">Can be set toocopy all hello content of your folder toohello Visual Studio Project, which is useful if hello executable does not change.</span></span> <span data-ttu-id="00da0-162">如果您預期 hello 可執行檔 toochange，且想 hello 能力 toopick 新組建上的以動態方式，您可以改為選擇 toolink toohello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="00da0-162">If you expect hello executable toochange and want hello ability toopick up new builds dynamically, you can choose toolink toohello folder instead.</span></span> <span data-ttu-id="00da0-163">在 Visual Studio 中建立 hello 應用程式專案時，您可以使用連結的資料夾。</span><span class="sxs-lookup"><span data-stu-id="00da0-163">You can use linked folders when creating hello application project in Visual Studio.</span></span> <span data-ttu-id="00da0-164">這會連結 toohello 來源位置，從在 hello 專案中，讓您 tooupdate hello 客體可執行檔在其來源的目的地。</span><span class="sxs-lookup"><span data-stu-id="00da0-164">This links toohello source location from within hello project, making it possible for you tooupdate hello guest executable in its source destination.</span></span> <span data-ttu-id="00da0-165">這些更新會成為 hello 上建置的應用程式套件的一部分。</span><span class="sxs-lookup"><span data-stu-id="00da0-165">Those updates become part of hello application package on build.</span></span>
   * <span data-ttu-id="00da0-166">*程式*指定應執行 toostart hello 服務的 hello 可執行檔。</span><span class="sxs-lookup"><span data-stu-id="00da0-166">*Program* specifies hello executable that should be run toostart hello service.</span></span>
   * <span data-ttu-id="00da0-167">*引數*指定 hello 傳遞引數應該 toohello 可執行檔。</span><span class="sxs-lookup"><span data-stu-id="00da0-167">*Arguments* specifies hello arguments that should be passed toohello executable.</span></span> <span data-ttu-id="00da0-168">這可以是具有引數的參數清單。</span><span class="sxs-lookup"><span data-stu-id="00da0-168">It can be a list of parameters with arguments.</span></span>
   * <span data-ttu-id="00da0-169">*WorkingFolder*指定 hello 即將啟動 toobe hello 程序的工作目錄。</span><span class="sxs-lookup"><span data-stu-id="00da0-169">*WorkingFolder* specifies hello working directory for hello process that is going toobe started.</span></span> <span data-ttu-id="00da0-170">您可以指定三個值：</span><span class="sxs-lookup"><span data-stu-id="00da0-170">You can specify three values:</span></span>
     * <span data-ttu-id="00da0-171">`CodeBase`指定該 hello 工作目錄即將 toobe hello 應用程式封裝中設定 toohello 程式碼目錄 (`Code` hello 前面檔案結構中顯示的目錄)。</span><span class="sxs-lookup"><span data-stu-id="00da0-171">`CodeBase` specifies that hello working directory is going toobe set toohello code directory in hello application package (`Code` directory shown in hello preceding file structure).</span></span>
     * <span data-ttu-id="00da0-172">`CodePackage`指定該 hello 工作目錄即將 toobe 設定 toohello 根 hello 應用程式封裝 (`GuestService1Pkg` hello 前面檔案結構所示)。</span><span class="sxs-lookup"><span data-stu-id="00da0-172">`CodePackage` specifies that hello working directory is going toobe set toohello root of hello application package    (`GuestService1Pkg` shown in hello preceding file structure).</span></span>
     * <span data-ttu-id="00da0-173">`Work`指定 hello 檔案會放置於稱為工作的子目錄。</span><span class="sxs-lookup"><span data-stu-id="00da0-173">`Work` specifies that hello files are placed in a subdirectory called work.</span></span>
4. <span data-ttu-id="00da0-174">指定服務的名稱，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="00da0-174">Give your service a name, and click **OK**.</span></span>
5. <span data-ttu-id="00da0-175">如果您的服務端點需要通訊，您現在可以新增 hello 通訊協定、 連接埠和型別 toohello ServiceManifest.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="00da0-175">If your service needs an endpoint for communication, you can now add hello protocol, port, and type toohello ServiceManifest.xml file.</span></span> <span data-ttu-id="00da0-176">例如： `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`。</span><span class="sxs-lookup"><span data-stu-id="00da0-176">For example: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.</span></span>
6. <span data-ttu-id="00da0-177">您現在可以使用 hello 封裝，並對本機叢集發行動作的偵錯 Visual Studio 中的 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="00da0-177">You can now use hello package and publish action against your local cluster by debugging hello solution in Visual Studio.</span></span> <span data-ttu-id="00da0-178">準備就緒時，您可以發行 hello 應用程式 tooa 遠端叢集，或檢查 hello 方案 toosource 控制項中。</span><span class="sxs-lookup"><span data-stu-id="00da0-178">When ready, you can publish hello application tooa remote cluster or check in hello solution toosource control.</span></span>
7. <span data-ttu-id="00da0-179">如何移 toohello 結尾此發行項 toosee tooview Service Fabric 總管中執行您客體可執行服務。</span><span class="sxs-lookup"><span data-stu-id="00da0-179">Go toohello end of this article toosee how tooview your guest executable service running in Service Fabric Explorer.</span></span>

## <a name="use-yoeman-toopackage-and-deploy-an-existing-executable-on-linux"></a><span data-ttu-id="00da0-180">使用 Yoeman toopackage 及部署 Linux 上的現有可執行檔</span><span class="sxs-lookup"><span data-stu-id="00da0-180">Use Yoeman toopackage and deploy an existing executable on Linux</span></span>

<span data-ttu-id="00da0-181">用於建立及部署可在 Linux 上執行客體 hello 程序是 hello 與部署 csharp 或 java 應用程式相同。</span><span class="sxs-lookup"><span data-stu-id="00da0-181">hello procedure for creating and deploying a guest executable on Linux is hello same as deploying a csharp or java application.</span></span>

1. <span data-ttu-id="00da0-182">在終端機中，輸入 `yo azuresfguest`。</span><span class="sxs-lookup"><span data-stu-id="00da0-182">In a terminal, type `yo azuresfguest`.</span></span>
2. <span data-ttu-id="00da0-183">為您的應用程式命名。</span><span class="sxs-lookup"><span data-stu-id="00da0-183">Name your application.</span></span>
3. <span data-ttu-id="00da0-184">命名您的服務，並提供包括 hello 可執行檔的路徑和 hello 參數必須以叫用的 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="00da0-184">Name your service, and provide hello details including path of hello executable and hello parameters it must be invoked with.</span></span>

<span data-ttu-id="00da0-185">Yeoman 與 hello 適當的應用程式建立應用程式套件和資訊清單檔案，以及安裝和解除安裝指令碼。</span><span class="sxs-lookup"><span data-stu-id="00da0-185">Yeoman creates an application package with hello appropriate application and manifest files along with install and uninstall scripts.</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-an-existing-executable"></a><span data-ttu-id="00da0-186">手動封裝和部署現有執行檔</span><span class="sxs-lookup"><span data-stu-id="00da0-186">Manually package and deploy an existing executable</span></span>
<span data-ttu-id="00da0-187">hello 程序手動封裝客體可執行檔為基礎 hello 下列一般步驟：</span><span class="sxs-lookup"><span data-stu-id="00da0-187">hello process of manually packaging a guest executable is based on hello following general steps:</span></span>

1. <span data-ttu-id="00da0-188">建立 hello 封裝目錄結構。</span><span class="sxs-lookup"><span data-stu-id="00da0-188">Create hello package directory structure.</span></span>
2. <span data-ttu-id="00da0-189">新增 hello 應用程式的程式碼和組態檔。</span><span class="sxs-lookup"><span data-stu-id="00da0-189">Add hello application's code and configuration files.</span></span>
3. <span data-ttu-id="00da0-190">編輯 hello 服務資訊清單檔。</span><span class="sxs-lookup"><span data-stu-id="00da0-190">Edit hello service manifest file.</span></span>
4. <span data-ttu-id="00da0-191">編輯 hello 應用程式資訊清單檔案。</span><span class="sxs-lookup"><span data-stu-id="00da0-191">Edit hello application manifest file.</span></span>

<!--
>[AZURE.NOTE] We do provide a packaging tool that allows you toocreate hello ApplicationPackage automatically. hello tool is currently in preview. You can download it from [here](http://aka.ms/servicefabricpacktool).
-->

### <a name="create-hello-package-directory-structure"></a><span data-ttu-id="00da0-192">建立 hello 封裝目錄結構</span><span class="sxs-lookup"><span data-stu-id="00da0-192">Create hello package directory structure</span></span>
<span data-ttu-id="00da0-193">您可以在 hello 前面一節中所述建立 hello 目錄結構，啟動 「 應用程式套件檔案結構。 」</span><span class="sxs-lookup"><span data-stu-id="00da0-193">You can start by creating hello directory structure, as described in hello preceding section, "Application package file structure."</span></span>

### <a name="add-hello-applications-code-and-configuration-files"></a><span data-ttu-id="00da0-194">新增 hello 應用程式的程式碼和組態檔</span><span class="sxs-lookup"><span data-stu-id="00da0-194">Add hello application's code and configuration files</span></span>
<span data-ttu-id="00da0-195">建立 hello 目錄結構之後，您可以加入 hello 程式碼和組態目錄下的 hello 應用程式的程式碼和組態檔案。</span><span class="sxs-lookup"><span data-stu-id="00da0-195">After you have created hello directory structure, you can add hello application's code and configuration files under hello code and config directories.</span></span> <span data-ttu-id="00da0-196">您也可以建立其他目錄或 hello 程式碼或設定目錄下的子目錄。</span><span class="sxs-lookup"><span data-stu-id="00da0-196">You can also create additional directories or subdirectories under hello code or config directories.</span></span>

<span data-ttu-id="00da0-197">Service Fabric 沒有`xcopy`的 hello hello 應用程式根目錄，因此沒有任何的預先定義的結構 toouse 以外建立兩個最上層目錄、 程式碼和設定的內容。</span><span class="sxs-lookup"><span data-stu-id="00da0-197">Service Fabric does an `xcopy` of hello content of hello application root directory, so there is no predefined structure toouse other than creating two top directories, code and settings.</span></span> <span data-ttu-id="00da0-198">(您可以選擇不同的名稱。</span><span class="sxs-lookup"><span data-stu-id="00da0-198">(You can pick different names if you want.</span></span> <span data-ttu-id="00da0-199">更多詳細資料位於 hello 下一節。）</span><span class="sxs-lookup"><span data-stu-id="00da0-199">More details are in hello next section.)</span></span>

> [!NOTE]
> <span data-ttu-id="00da0-200">請確定您包含所有 hello 檔案和 hello 應用程式所需的相依性。</span><span class="sxs-lookup"><span data-stu-id="00da0-200">Make sure that you include all hello files and dependencies that hello application needs.</span></span> <span data-ttu-id="00da0-201">Service Fabric hello 應用程式服務的部署進行 toobe hello 叢集中複製 hello hello 應用程式套件的所有節點上的內容。</span><span class="sxs-lookup"><span data-stu-id="00da0-201">Service Fabric copies hello content of hello application package on all nodes in hello cluster where hello application's services are going toobe deployed.</span></span> <span data-ttu-id="00da0-202">hello 套件應該包含所有 hello 應用程式需要 toorun hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="00da0-202">hello package should contain all hello code that hello application needs toorun.</span></span> <span data-ttu-id="00da0-203">請勿假設已安裝的 hello 相依性。</span><span class="sxs-lookup"><span data-stu-id="00da0-203">Do not assume that hello dependencies are already installed.</span></span>
>
>

### <a name="edit-hello-service-manifest-file"></a><span data-ttu-id="00da0-204">編輯 hello 服務資訊清單檔</span><span class="sxs-lookup"><span data-stu-id="00da0-204">Edit hello service manifest file</span></span>
<span data-ttu-id="00da0-205">hello 下一個步驟是 tooedit hello 服務資訊清單檔案 tooinclude hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="00da0-205">hello next step is tooedit hello service manifest file tooinclude hello following information:</span></span>

* <span data-ttu-id="00da0-206">hello hello 服務型別名稱。</span><span class="sxs-lookup"><span data-stu-id="00da0-206">hello name of hello service type.</span></span> <span data-ttu-id="00da0-207">這是 Service Fabric 使用 tooidentify 服務識別碼。</span><span class="sxs-lookup"><span data-stu-id="00da0-207">This is an ID that Service Fabric uses tooidentify a service.</span></span>
* <span data-ttu-id="00da0-208">hello 命令 toouse toolaunch hello 應用程式 (ExeHost)。</span><span class="sxs-lookup"><span data-stu-id="00da0-208">hello command toouse toolaunch hello application (ExeHost).</span></span>
* <span data-ttu-id="00da0-209">需要執行 toobe tooset hello 應用程式 (SetupEntrypoint) 的任何指令碼。</span><span class="sxs-lookup"><span data-stu-id="00da0-209">Any script that needs toobe run tooset up hello application (SetupEntrypoint).</span></span>

<span data-ttu-id="00da0-210">hello 的範例如下的`ServiceManifest.xml`檔案：</span><span class="sxs-lookup"><span data-stu-id="00da0-210">hello following is an example of a `ServiceManifest.xml` file:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="NodeApp" Version="1.0.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceTypes>
      <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true"/>
   </ServiceTypes>
   <CodePackage Name="code" Version="1.0.0.0">
      <SetupEntryPoint>
         <ExeHost>
             <Program>scripts\launchConfig.cmd</Program>
         </ExeHost>
      </SetupEntryPoint>
      <EntryPoint>
         <ExeHost>
            <Program>node.exe</Program>
            <Arguments>bin/www</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
         </ExeHost>
      </EntryPoint>
   </CodePackage>
   <Resources>
      <Endpoints>
         <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
   </Resources>
</ServiceManifest>
```

<span data-ttu-id="00da0-211">下列各節的 hello 介紹 hello 您需要 tooupdate 的 hello 檔案的不同部分。</span><span class="sxs-lookup"><span data-stu-id="00da0-211">hello following sections go over hello different parts of hello file that you need tooupdate.</span></span>

#### <a name="update-servicetypes"></a><span data-ttu-id="00da0-212">更新 ServiceTypes</span><span class="sxs-lookup"><span data-stu-id="00da0-212">Update ServiceTypes</span></span>
```xml
<ServiceTypes>
  <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true" />
</ServiceTypes>
```

* <span data-ttu-id="00da0-213">您可以挑選任何您要用於 `ServiceTypeName` 的名稱。</span><span class="sxs-lookup"><span data-stu-id="00da0-213">You can pick any name that you want for `ServiceTypeName`.</span></span> <span data-ttu-id="00da0-214">hello 值是否會在 hello`ApplicationManifest.xml`檔案 tooidentify hello 服務。</span><span class="sxs-lookup"><span data-stu-id="00da0-214">hello value is used in hello `ApplicationManifest.xml` file tooidentify hello service.</span></span>
* <span data-ttu-id="00da0-215">指定 `UseImplicitHost="true"`。</span><span class="sxs-lookup"><span data-stu-id="00da0-215">Specify `UseImplicitHost="true"`.</span></span> <span data-ttu-id="00da0-216">這個屬性會告知 Service Fabric hello 服務為基礎的獨立應用程式，因此所有的 Service Fabric 需要 toodo 是 toolaunch 它做為處理序並監視其健康情況。</span><span class="sxs-lookup"><span data-stu-id="00da0-216">This attribute tells Service Fabric that hello service is based on a self-contained app, so all Service Fabric needs toodo is toolaunch it as a process and monitor its health.</span></span>

#### <a name="update-codepackage"></a><span data-ttu-id="00da0-217">更新 CodePackage</span><span class="sxs-lookup"><span data-stu-id="00da0-217">Update CodePackage</span></span>
<span data-ttu-id="00da0-218">hello CodePackage 元素會指定 hello 服務的程式碼 hello 位置 （和版本）。</span><span class="sxs-lookup"><span data-stu-id="00da0-218">hello CodePackage element specifies hello location (and version) of hello service's code.</span></span>

```xml
<CodePackage Name="Code" Version="1.0.0.0">
```

<span data-ttu-id="00da0-219">hello`Name`項目是使用的 toospecify hello hello 包含 hello 服務的程式碼的應用程式封裝中的 hello 目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="00da0-219">hello `Name` element is used toospecify hello name of hello directory in hello application package that contains hello service's code.</span></span> <span data-ttu-id="00da0-220">`CodePackage`也有 hello`version`屬性。</span><span class="sxs-lookup"><span data-stu-id="00da0-220">`CodePackage` also has hello `version` attribute.</span></span> <span data-ttu-id="00da0-221">這可以是使用的 toospecify hello 版本 hello 程式碼，而且可以也可能會利用 Service Fabric 中的 hello 應用程式生命週期管理基礎結構使用 tooupgrade hello 服務的程式碼。</span><span class="sxs-lookup"><span data-stu-id="00da0-221">This can be used toospecify hello version of hello code, and can also potentially be used tooupgrade hello service's code by using hello application lifecycle management infrastructure in Service Fabric.</span></span>

#### <a name="optional-update-setupentrypoint"></a><span data-ttu-id="00da0-222">選擇性︰更新 SetupEntrypoint</span><span class="sxs-lookup"><span data-stu-id="00da0-222">Optional: Update SetupEntrypoint</span></span>
```xml
<SetupEntryPoint>
   <ExeHost>
       <Program>scripts\launchConfig.cmd</Program>
   </ExeHost>
</SetupEntryPoint>
```
<span data-ttu-id="00da0-223">hello SetupEntryPoint 項目是使用的 toospecify hello 服務的程式碼啟動前應該執行的任何可執行檔或批次檔案。</span><span class="sxs-lookup"><span data-stu-id="00da0-223">hello SetupEntryPoint element is used toospecify any executable or batch file that should be executed before hello service's code is launched.</span></span> <span data-ttu-id="00da0-224">是選擇性步驟中，因此不需要 toobe 包含如果有任何需要的初始化。</span><span class="sxs-lookup"><span data-stu-id="00da0-224">It is an optional step, so it does not need toobe included if there is no initialization required.</span></span> <span data-ttu-id="00da0-225">hello SetupEntryPoint 執行每次 hello 服務重新啟動。</span><span class="sxs-lookup"><span data-stu-id="00da0-225">hello SetupEntryPoint is executed every time hello service is restarted.</span></span>

<span data-ttu-id="00da0-226">沒有一個 SetupEntryPoint，因此安裝程式指令碼需要 toobe 分組在單一批次檔中，如果 hello 應用程式的安裝程式需要多個指令碼。</span><span class="sxs-lookup"><span data-stu-id="00da0-226">There is only one SetupEntryPoint, so setup scripts need toobe grouped in a single batch file if hello application's setup requires multiple scripts.</span></span> <span data-ttu-id="00da0-227">hello SetupEntryPoint 能夠執行任何類型的檔案： 可執行檔、 批次檔，以及 PowerShell 指令程式。</span><span class="sxs-lookup"><span data-stu-id="00da0-227">hello SetupEntryPoint can execute any type of file: executable files, batch files, and PowerShell cmdlets.</span></span> <span data-ttu-id="00da0-228">如需詳細資訊，請參閱[設定 SetupEntryPoint](service-fabric-application-runas-security.md)。</span><span class="sxs-lookup"><span data-stu-id="00da0-228">For more details, see [Configure SetupEntryPoint](service-fabric-application-runas-security.md).</span></span>

<span data-ttu-id="00da0-229">在上述範例中的 hello，hello SetupEntryPoint 執行批次檔呼叫`LaunchConfig.cmd`也就是位於的 hello `scripts` hello （假設 hello WorkingFolder 元素設定 tooCodeBase） 的程式碼目錄的子目錄。</span><span class="sxs-lookup"><span data-stu-id="00da0-229">In hello preceding example, hello SetupEntryPoint runs a batch file called `LaunchConfig.cmd` that is located in hello `scripts` subdirectory of hello code directory (assuming hello WorkingFolder element is set tooCodeBase).</span></span>

#### <a name="update-entrypoint"></a><span data-ttu-id="00da0-230">更新 EntryPoint</span><span class="sxs-lookup"><span data-stu-id="00da0-230">Update EntryPoint</span></span>
```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
  </ExeHost>
</EntryPoint>
```

<span data-ttu-id="00da0-231">hello `EntryPoint` hello 服務資訊清單檔中的項目，則使用的 toospecify 如何 toolaunch hello 服務。</span><span class="sxs-lookup"><span data-stu-id="00da0-231">hello `EntryPoint` element in hello service manifest file is used toospecify how toolaunch hello service.</span></span> <span data-ttu-id="00da0-232">hello`ExeHost`項目會指定可執行檔的 hello （和引數），應該使用 toolaunch hello 服務。</span><span class="sxs-lookup"><span data-stu-id="00da0-232">hello `ExeHost` element specifies hello executable (and arguments) that should be used toolaunch hello service.</span></span>

* <span data-ttu-id="00da0-233">`Program`指定 hello 應該啟動 hello 服務的 hello 可執行檔名稱。</span><span class="sxs-lookup"><span data-stu-id="00da0-233">`Program` specifies hello name of hello executable that should start hello service.</span></span>
* <span data-ttu-id="00da0-234">`Arguments`指定應該傳遞 toohello 可執行檔的 hello 引數。</span><span class="sxs-lookup"><span data-stu-id="00da0-234">`Arguments` specifies hello arguments that should be passed toohello executable.</span></span> <span data-ttu-id="00da0-235">這可以是具有引數的參數清單。</span><span class="sxs-lookup"><span data-stu-id="00da0-235">It can be a list of parameters with arguments.</span></span>
* <span data-ttu-id="00da0-236">`WorkingFolder`指定即將啟動 toobe hello 處理序的 hello 工作目錄。</span><span class="sxs-lookup"><span data-stu-id="00da0-236">`WorkingFolder` specifies hello working directory for hello process that is going toobe started.</span></span> <span data-ttu-id="00da0-237">您可以指定三個值：</span><span class="sxs-lookup"><span data-stu-id="00da0-237">You can specify three values:</span></span>
  * <span data-ttu-id="00da0-238">`CodeBase`指定該 hello 工作目錄即將 toobe hello 應用程式封裝中設定 toohello 程式碼目錄 (`Code`目錄 hello 前面檔案結構中)。</span><span class="sxs-lookup"><span data-stu-id="00da0-238">`CodeBase` specifies that hello working directory is going toobe set toohello code directory in hello application package (`Code` directory in hello preceding file structure).</span></span>
  * <span data-ttu-id="00da0-239">`CodePackage`指定該 hello 工作目錄即將 toobe 設定 toohello 根 hello 應用程式封裝 (`GuestService1Pkg` hello 前面檔案結構中)。</span><span class="sxs-lookup"><span data-stu-id="00da0-239">`CodePackage` specifies that hello working directory is going toobe set toohello root of hello application package    (`GuestService1Pkg` in hello preceding file structure).</span></span>
    * <span data-ttu-id="00da0-240">`Work`指定 hello 檔案會放置於稱為工作的子目錄。</span><span class="sxs-lookup"><span data-stu-id="00da0-240">`Work` specifies that hello files are placed in a subdirectory called work.</span></span>

<span data-ttu-id="00da0-241">hello WorkingFolder 是有用的 tooset hello 正確的工作目錄，以便可以使用相對路徑，由任一 hello 應用程式或初始化指令碼。</span><span class="sxs-lookup"><span data-stu-id="00da0-241">hello WorkingFolder is useful tooset hello correct working directory so that relative paths can be used by either hello application or initialization scripts.</span></span>

#### <a name="update-endpoints-and-register-with-naming-service-for-communication"></a><span data-ttu-id="00da0-242">更新端點，並向命名服務註冊以進行通訊</span><span class="sxs-lookup"><span data-stu-id="00da0-242">Update Endpoints and register with Naming Service for communication</span></span>
```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
</Endpoints>

```
<span data-ttu-id="00da0-243">在上述範例中的 hello，hello`Endpoint`項目會指定 hello hello 應用程式可以接聽的端點。</span><span class="sxs-lookup"><span data-stu-id="00da0-243">In hello preceding example, hello `Endpoint` element specifies hello endpoints that hello application can listen on.</span></span> <span data-ttu-id="00da0-244">在此範例中，hello Node.js 應用程式會接聽連接埠 3000 的 http。</span><span class="sxs-lookup"><span data-stu-id="00da0-244">In this example, hello Node.js application listens on http on port 3000.</span></span>

<span data-ttu-id="00da0-245">此外您可以要求 Service Fabric toopublish 這個端點 toohello 命名服務讓其他服務可以探索 hello 端點位址 toothis 服務。</span><span class="sxs-lookup"><span data-stu-id="00da0-245">Furthermore you can ask Service Fabric toopublish this endpoint toohello Naming Service so other services can discover hello endpoint address toothis service.</span></span> <span data-ttu-id="00da0-246">這可讓您 toobe 無法 toocommunicate 客體可執行檔的服務之間。</span><span class="sxs-lookup"><span data-stu-id="00da0-246">This enables you toobe able toocommunicate between services that are guest executables.</span></span>
<span data-ttu-id="00da0-247">hello 已發行的端點位址是 hello 表單的`UriScheme://IPAddressOrFQDN:Port/PathSuffix`。</span><span class="sxs-lookup"><span data-stu-id="00da0-247">hello published endpoint address is of hello form `UriScheme://IPAddressOrFQDN:Port/PathSuffix`.</span></span> <span data-ttu-id="00da0-248">`UriScheme` 和 `PathSuffix` 是選擇性的屬性。</span><span class="sxs-lookup"><span data-stu-id="00da0-248">`UriScheme` and `PathSuffix` are optional attributes.</span></span> <span data-ttu-id="00da0-249">`IPAddressOrFQDN`是 hello IP 位址或完整的網域名稱的 hello 節點取得置於這個可執行檔，而且它會針對您計算。</span><span class="sxs-lookup"><span data-stu-id="00da0-249">`IPAddressOrFQDN` is hello IP address or fully qualified domain name of hello node this executable gets placed on, and it is calculated for you.</span></span>

<span data-ttu-id="00da0-250">在 hello 下列範例中，一次 hello 服務部署，請在 Service Fabric 總管您會看到類似端點太`http://10.1.4.92:3000/myapp/`發行 hello 服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="00da0-250">In hello following example, once hello service is deployed, in Service Fabric Explorer you see an endpoint similar too`http://10.1.4.92:3000/myapp/` published for hello service instance.</span></span> <span data-ttu-id="00da0-251">或者，如果這是本機電腦，則您會看到 `http://localhost:3000/myapp/`。</span><span class="sxs-lookup"><span data-stu-id="00da0-251">Or if this is a local machine, you see `http://localhost:3000/myapp/`.</span></span>

```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000"  UriScheme="http" PathSuffix="myapp/" Type="Input" />
</Endpoints>
```
<span data-ttu-id="00da0-252">您可以使用這些位址與[反向 proxy](service-fabric-reverseproxy.md) toocommunicate 服務之間。</span><span class="sxs-lookup"><span data-stu-id="00da0-252">You can use these addresses with [reverse proxy](service-fabric-reverseproxy.md) toocommunicate between services.</span></span>

### <a name="edit-hello-application-manifest-file"></a><span data-ttu-id="00da0-253">編輯 hello 應用程式資訊清單檔</span><span class="sxs-lookup"><span data-stu-id="00da0-253">Edit hello application manifest file</span></span>
<span data-ttu-id="00da0-254">一旦設定 hello`Servicemanifest.xml`檔案中，您需要某些變更 toohello toomake`ApplicationManifest.xml`檔案 hello 的 tooensure 正確使用的服務類型和名稱。</span><span class="sxs-lookup"><span data-stu-id="00da0-254">Once you have configured hello `Servicemanifest.xml` file, you need toomake some changes toohello `ApplicationManifest.xml` file tooensure that hello correct service type and name are used.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="NodeAppType" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
   </ServiceManifestImport>
</ApplicationManifest>
```

#### <a name="servicemanifestimport"></a><span data-ttu-id="00da0-255">ServiceManifestImport</span><span class="sxs-lookup"><span data-stu-id="00da0-255">ServiceManifestImport</span></span>
<span data-ttu-id="00da0-256">在 hello`ServiceManifestImport`項目，您可以指定您想 tooinclude hello 應用程式中的一或多個服務。</span><span class="sxs-lookup"><span data-stu-id="00da0-256">In hello `ServiceManifestImport` element, you can specify one or more services that you want tooinclude in hello app.</span></span> <span data-ttu-id="00da0-257">服務使用參考`ServiceManifestName`，以指定 hello hello 目錄名稱，其中 hello`ServiceManifest.xml`檔所在。</span><span class="sxs-lookup"><span data-stu-id="00da0-257">Services are referenced with `ServiceManifestName`, which specifies hello name of hello directory where hello `ServiceManifest.xml` file is located.</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
</ServiceManifestImport>
```

## <a name="set-up-logging"></a><span data-ttu-id="00da0-258">設定記錄</span><span class="sxs-lookup"><span data-stu-id="00da0-258">Set up logging</span></span>
<span data-ttu-id="00da0-259">針對客體可執行檔，如果就會很有用的 toobe 無法 toosee 主控台記錄檔 toofind 出 hello 應用程式和組態指令碼會顯示任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="00da0-259">For guest executables, it is useful toobe able toosee console logs toofind out if hello application and configuration scripts show any errors.</span></span>
<span data-ttu-id="00da0-260">主控台重新導向可以設定在 hello`ServiceManifest.xml`檔案使用 hello`ConsoleRedirection`項目。</span><span class="sxs-lookup"><span data-stu-id="00da0-260">Console redirection can be configured in hello `ServiceManifest.xml` file using hello `ConsoleRedirection` element.</span></span>

> [!WARNING]
> <span data-ttu-id="00da0-261">絕對不要使用的應用程式，因為這可能會影響 hello 應用程式容錯移轉，在生產環境中部署的 hello 主控台重新導向原則。</span><span class="sxs-lookup"><span data-stu-id="00da0-261">Never use hello console redirection policy in an application that is deployed in production because this can affect hello application failover.</span></span> <span data-ttu-id="00da0-262">僅將此原則用於本機開發及偵錯。</span><span class="sxs-lookup"><span data-stu-id="00da0-262">*Only* use this for local development and debugging purposes.</span></span>  
>
>

```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="5" FileMaxSizeInKb="2048"/>
  </ExeHost>
</EntryPoint>
```

<span data-ttu-id="00da0-263">`ConsoleRedirection`可以使用的 tooredirect 主控台輸出 （stdout 與 stderr） tooa 工作目錄。</span><span class="sxs-lookup"><span data-stu-id="00da0-263">`ConsoleRedirection` can be used tooredirect console output (both stdout and stderr) tooa working directory.</span></span> <span data-ttu-id="00da0-264">這會提供 hello 能力 tooverify hello 安裝程式或 hello hello Service Fabric 叢集中的應用程式執行期間沒有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="00da0-264">This provides hello ability tooverify that there are no errors during hello setup or execution of hello application in hello Service Fabric cluster.</span></span>

<span data-ttu-id="00da0-265">`FileRetentionCount`決定多少檔案會儲存在 hello 工作目錄。</span><span class="sxs-lookup"><span data-stu-id="00da0-265">`FileRetentionCount` determines how many files are saved in hello working directory.</span></span> <span data-ttu-id="00da0-266">值為 5，比方說，表示 hello hello 先前五個執行的記錄檔會儲存在 hello 工作目錄。</span><span class="sxs-lookup"><span data-stu-id="00da0-266">A value of 5, for example, means that hello log files for hello previous five executions are stored in hello working directory.</span></span>

<span data-ttu-id="00da0-267">`FileMaxSizeInKb`指定 hello hello 記錄檔的大小上限。</span><span class="sxs-lookup"><span data-stu-id="00da0-267">`FileMaxSizeInKb` specifies hello maximum size of hello log files.</span></span>

<span data-ttu-id="00da0-268">記錄檔會儲存在其中一個 hello 服務的工作目錄。</span><span class="sxs-lookup"><span data-stu-id="00da0-268">Log files are saved in one of hello service's working directories.</span></span> <span data-ttu-id="00da0-269">toodetermine hello 檔案位於何處，使用 Service Fabric 總管 toodetermine 哪一種節點 hello 服務正在執行，且正在使用的工作目錄。</span><span class="sxs-lookup"><span data-stu-id="00da0-269">toodetermine where hello files are located, use Service Fabric Explorer toodetermine which node hello service is running on, and which working directory is being used.</span></span> <span data-ttu-id="00da0-270">本文稍後會說明此程序。</span><span class="sxs-lookup"><span data-stu-id="00da0-270">This process is covered later in this article.</span></span>

## <a name="deployment"></a><span data-ttu-id="00da0-271">部署</span><span class="sxs-lookup"><span data-stu-id="00da0-271">Deployment</span></span>
<span data-ttu-id="00da0-272">最後一個步驟中 hello 太[部署您的應用程式](service-fabric-deploy-remove-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="00da0-272">hello last step is too[deploy your application](service-fabric-deploy-remove-applications.md).</span></span> <span data-ttu-id="00da0-273">hello 下列 PowerShell 指令碼顯示如何 toodeploy 您的應用程式 toohello 本機開發叢集，並啟動新的 Service Fabric 服務。</span><span class="sxs-lookup"><span data-stu-id="00da0-273">hello following PowerShell script shows how toodeploy your application toohello local development cluster, and start a new Service Fabric service.</span></span>

```PowerShell

Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath 'C:\Dev\MultipleApplications' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'nodeapp'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'nodeapp'

New-ServiceFabricApplication -ApplicationName 'fabric:/nodeapp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0

New-ServiceFabricService -ApplicationName 'fabric:/nodeapp' -ServiceName 'fabric:/nodeapp/nodeappservice' -ServiceTypeName 'NodeApp' -Stateless -PartitionSchemeSingleton -InstanceCount 1

```

>[!TIP]
> <span data-ttu-id="00da0-274">[壓縮 hello 封裝](service-fabric-package-apps.md#compress-a-package)複製 toohello 映像存放區，如果 hello 套件很大，或具有許多檔案之前。</span><span class="sxs-lookup"><span data-stu-id="00da0-274">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store if hello package is large or has many files.</span></span> <span data-ttu-id="00da0-275">請在[這裡](service-fabric-deploy-remove-applications.md#upload-the-application-package)閱讀更多資訊。</span><span class="sxs-lookup"><span data-stu-id="00da0-275">Read more [here](service-fabric-deploy-remove-applications.md#upload-the-application-package).</span></span>
>

<span data-ttu-id="00da0-276">Service Fabric 服務可以各種「組態」部署。</span><span class="sxs-lookup"><span data-stu-id="00da0-276">A Service Fabric service can be deployed in various "configurations."</span></span> <span data-ttu-id="00da0-277">例如，它可以部署為單一或多個執行個體，或它可以部署的方式會有一個 hello hello Service Fabric 叢集的每個節點上的服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="00da0-277">For example, it can be deployed as single or multiple instances, or it can be deployed in such a way that there is one instance of hello service on each node of hello Service Fabric cluster.</span></span>

<span data-ttu-id="00da0-278">hello `InstanceCount` hello 參數`New-ServiceFabricService`指令程式是使用的 toospecify 多少個 hello 服務執行個體應該啟動 hello Service Fabric 叢集中。</span><span class="sxs-lookup"><span data-stu-id="00da0-278">hello `InstanceCount` parameter of hello `New-ServiceFabricService` cmdlet is used toospecify how many instances of hello service should be launched in hello Service Fabric cluster.</span></span> <span data-ttu-id="00da0-279">您可以設定 hello`InstanceCount`值，視您要部署的應用程式的 hello 類型而定。</span><span class="sxs-lookup"><span data-stu-id="00da0-279">You can set hello `InstanceCount` value, depending on hello type of application that you are deploying.</span></span> <span data-ttu-id="00da0-280">hello 兩個最常見情況包括：</span><span class="sxs-lookup"><span data-stu-id="00da0-280">hello two most common scenarios are:</span></span>

* <span data-ttu-id="00da0-281">`InstanceCount = "1"`。</span><span class="sxs-lookup"><span data-stu-id="00da0-281">`InstanceCount = "1"`.</span></span> <span data-ttu-id="00da0-282">在此情況下，只有一個 hello 服務執行個體被部署在 hello 叢集中。</span><span class="sxs-lookup"><span data-stu-id="00da0-282">In this case, only one instance of hello service is deployed in hello cluster.</span></span> <span data-ttu-id="00da0-283">Service Fabric 排程器會決定哪一種節點 hello 服務即將 toobe 上部署。</span><span class="sxs-lookup"><span data-stu-id="00da0-283">Service Fabric's scheduler determines which node hello service is going toobe deployed on.</span></span>
* <span data-ttu-id="00da0-284">`InstanceCount ="-1"`。</span><span class="sxs-lookup"><span data-stu-id="00da0-284">`InstanceCount ="-1"`.</span></span> <span data-ttu-id="00da0-285">在此情況下，一個 hello 服務執行個體部署的 hello Service Fabric 叢集中的每個節點。</span><span class="sxs-lookup"><span data-stu-id="00da0-285">In this case, one instance of hello service is deployed on every node in hello Service Fabric cluster.</span></span> <span data-ttu-id="00da0-286">hello 結果 hello 叢集中有一個 （且只有一個） 的每個節點的 hello 服務的執行個體。</span><span class="sxs-lookup"><span data-stu-id="00da0-286">hello result is having one (and only one) instance of hello service for each node in hello cluster.</span></span>

<span data-ttu-id="00da0-287">這是前端應用程式 （例如，REST 端點），如有用的組態，因為用戶端應用程式需要太 「 連接 」 tooany hello 叢集 toouse hello 端點中的 hello 節點。</span><span class="sxs-lookup"><span data-stu-id="00da0-287">This is a useful configuration for front-end applications (for example, a REST endpoint), because client applications need too"connect" tooany of hello nodes in hello cluster toouse hello endpoint.</span></span> <span data-ttu-id="00da0-288">這項設定也可用時，例如 hello Service Fabric 叢集的所有節點連線的 tooa 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="00da0-288">This configuration can also be used when, for example, all nodes of hello Service Fabric cluster are connected tooa load balancer.</span></span> <span data-ttu-id="00da0-289">用戶端流量然後分散 hello 服務 hello 叢集中所有節點上執行。</span><span class="sxs-lookup"><span data-stu-id="00da0-289">Client traffic can then be distributed across hello service that is running on all nodes in hello cluster.</span></span>

## <a name="check-your-running-application"></a><span data-ttu-id="00da0-290">來查執行中的應用程式</span><span class="sxs-lookup"><span data-stu-id="00da0-290">Check your running application</span></span>
<span data-ttu-id="00da0-291">在 Service Fabric 總管，識別 hello hello 服務執行所在的節點。</span><span class="sxs-lookup"><span data-stu-id="00da0-291">In Service Fabric Explorer, identify hello node where hello service is running.</span></span> <span data-ttu-id="00da0-292">在此範例中，它是在 Node1 上執行：</span><span class="sxs-lookup"><span data-stu-id="00da0-292">In this example, it runs on Node1:</span></span>

![服務執行所在的節點](./media/service-fabric-deploy-existing-app/nodeappinsfx.png)

<span data-ttu-id="00da0-294">如果您瀏覽 toohello 節點，並瀏覽 toohello 應用程式，您會看到 hello 不可或缺的節點資訊，包括其磁碟上的位置。</span><span class="sxs-lookup"><span data-stu-id="00da0-294">If you navigate toohello node and browse toohello application, you see hello essential node information, including its location on disk.</span></span>

![在磁碟上的位置](./media/service-fabric-deploy-existing-app/locationondisk2.png)

<span data-ttu-id="00da0-296">如果使用伺服器總管瀏覽 toohello 目錄，您可以找到 hello 工作目錄和 hello 服務記錄檔資料夾中 hello 下列螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="00da0-296">If you browse toohello directory by using Server Explorer, you can find hello working directory and hello service's log folder, as shown in hello following screenshot:</span></span> 

![記錄檔的位置](./media/service-fabric-deploy-existing-app/loglocation.png)

## <a name="next-steps"></a><span data-ttu-id="00da0-298">後續步驟</span><span class="sxs-lookup"><span data-stu-id="00da0-298">Next steps</span></span>
<span data-ttu-id="00da0-299">在本文中，您已經學會如何 toopackage 客體可執行檔並將其部署 tooService 網狀架構。</span><span class="sxs-lookup"><span data-stu-id="00da0-299">In this article, you have learned how toopackage a guest executable and deploy it tooService Fabric.</span></span> <span data-ttu-id="00da0-300">請參閱下列文章中的相關的資訊和工作的 hello。</span><span class="sxs-lookup"><span data-stu-id="00da0-300">See hello following articles for related information and tasks.</span></span>

* <span data-ttu-id="00da0-301">[範例封裝和部署客體可執行檔](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)，包括連結 toohello 發行前版本的 hello 封裝工具</span><span class="sxs-lookup"><span data-stu-id="00da0-301">[Sample for packaging and deploying a guest executable](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), including a link toohello prerelease of hello packaging tool</span></span>
* [<span data-ttu-id="00da0-302">兩個客體可執行檔 （C# 和 nodejs） 通訊透過 hello 命名服務使用 REST 範例</span><span class="sxs-lookup"><span data-stu-id="00da0-302">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
* [<span data-ttu-id="00da0-303">部署多個來賓可執行檔</span><span class="sxs-lookup"><span data-stu-id="00da0-303">Deploy multiple guest executables</span></span>](service-fabric-deploy-multiple-apps.md)
* [<span data-ttu-id="00da0-304">使用 Visual Studio 建立第一個 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="00da0-304">Create your first Service Fabric application using Visual Studio</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
