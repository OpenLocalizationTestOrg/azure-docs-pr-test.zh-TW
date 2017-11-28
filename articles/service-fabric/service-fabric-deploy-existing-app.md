---
title: "將現有的可執行檔部署至 Azure Service Fabric | Microsoft Docs"
description: "逐步解說如何將現有應用程式封裝為來賓可執行檔，使其可以部署至 Service Fabric 叢集"
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
ms.openlocfilehash: a1db3dda674ffe43587333d88f3816549af3019c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-guest-executable-to-service-fabric"></a><span data-ttu-id="e0f72-103">將來賓可執行檔部署至 Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e0f72-103">Deploy a guest executable to Service Fabric</span></span>
<span data-ttu-id="e0f72-104">您可以在 Azure Service Fabric 中將任何類型的程式碼 (例如 Node.js、Java 或 C++) 當作服務來執行。</span><span class="sxs-lookup"><span data-stu-id="e0f72-104">You can run any type of code, such as Node.js, Java, or C++ in Azure Service Fabric as a service.</span></span> <span data-ttu-id="e0f72-105">Service Fabric 將這些類型的服務稱為客體可執行檔。</span><span class="sxs-lookup"><span data-stu-id="e0f72-105">Service Fabric refers to these types of services as guest executables.</span></span>

<span data-ttu-id="e0f72-106">Service Fabric 將來賓可執行檔視為無狀態服務。</span><span class="sxs-lookup"><span data-stu-id="e0f72-106">Guest executables are treated by Service Fabric like stateless services.</span></span> <span data-ttu-id="e0f72-107">因此會根據可用性和其他度量將它們放在叢集的節點上。</span><span class="sxs-lookup"><span data-stu-id="e0f72-107">As a result, they are placed on nodes in a cluster, based on availability and other metrics.</span></span> <span data-ttu-id="e0f72-108">本文說明如何使用 Visual Studio 或命令列公用程式，封裝來賓執行檔並部署至 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="e0f72-108">This article describes how to package and deploy a guest executable to a Service Fabric cluster, by using Visual Studio or a command-line utility.</span></span>

<span data-ttu-id="e0f72-109">本文中涵蓋將來賓可執行檔封裝並部署至 Service Fabric 的步驟。</span><span class="sxs-lookup"><span data-stu-id="e0f72-109">In this article, we cover the steps to package a guest executable and deploy it to Service Fabric.</span></span>  

## <a name="benefits-of-running-a-guest-executable-in-service-fabric"></a><span data-ttu-id="e0f72-110">在 Service Fabric 中執行來賓可執行檔的優點</span><span class="sxs-lookup"><span data-stu-id="e0f72-110">Benefits of running a guest executable in Service Fabric</span></span>
<span data-ttu-id="e0f72-111">在 Service Fabric 叢集中執行來賓執行檔有幾個優點：</span><span class="sxs-lookup"><span data-stu-id="e0f72-111">There are several advantages to running a guest executable in a Service Fabric cluster:</span></span>

* <span data-ttu-id="e0f72-112">高可用性。</span><span class="sxs-lookup"><span data-stu-id="e0f72-112">High availability.</span></span> <span data-ttu-id="e0f72-113">在 Service Fabric 中執行的應用程式都會具有高可用性。</span><span class="sxs-lookup"><span data-stu-id="e0f72-113">Applications that run in Service Fabric are made highly available.</span></span> <span data-ttu-id="e0f72-114">Service Fabric 會確保應用程式執行個體正在執行。</span><span class="sxs-lookup"><span data-stu-id="e0f72-114">Service Fabric ensures that instances of an application are running.</span></span>
* <span data-ttu-id="e0f72-115">健康狀況監視。</span><span class="sxs-lookup"><span data-stu-id="e0f72-115">Health monitoring.</span></span> <span data-ttu-id="e0f72-116">Service Fabric 健全狀況監控會偵測應用程式是否正在執行，如果發生失敗情況，則會提供診斷資訊。</span><span class="sxs-lookup"><span data-stu-id="e0f72-116">Service Fabric health monitoring detects if an application is running, and provides diagnostic information if there is a failure.</span></span>   
* <span data-ttu-id="e0f72-117">應用程式生命週期管理。</span><span class="sxs-lookup"><span data-stu-id="e0f72-117">Application lifecycle management.</span></span> <span data-ttu-id="e0f72-118">除了提供無需停機的升級，如果升級期間回報健全狀況不良事件，Service Fabric 也支援回復到舊版。</span><span class="sxs-lookup"><span data-stu-id="e0f72-118">Besides providing upgrades with no downtime, Service Fabric provides automatic rollback to the previous version if there is a bad health event reported during an upgrade.</span></span>    
* <span data-ttu-id="e0f72-119">密度。</span><span class="sxs-lookup"><span data-stu-id="e0f72-119">Density.</span></span> <span data-ttu-id="e0f72-120">您可以在叢集中執行多個應用程式，每個應用程式不必在自己的硬體上執行。</span><span class="sxs-lookup"><span data-stu-id="e0f72-120">You can run multiple applications in a cluster, which eliminates the need for each application to run on its own hardware.</span></span>
* <span data-ttu-id="e0f72-121">可探索性：藉由使用 REST，您可以呼叫 Service Fabric 命名服務來尋找叢集中的其他服務。</span><span class="sxs-lookup"><span data-stu-id="e0f72-121">Discoverability: Using REST you can call the Service Fabric Naming service to find other services in the cluster.</span></span> 

## <a name="samples"></a><span data-ttu-id="e0f72-122">範例</span><span class="sxs-lookup"><span data-stu-id="e0f72-122">Samples</span></span>
* [<span data-ttu-id="e0f72-123">封裝和部署來賓可執行檔的範例</span><span class="sxs-lookup"><span data-stu-id="e0f72-123">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="e0f72-124">兩個客體可執行檔 (C# 和 nodejs) 使用 REST 透過命名服務進行通訊的範例</span><span class="sxs-lookup"><span data-stu-id="e0f72-124">Sample of two guest executables (C# and nodejs) communicating via the Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="overview-of-application-and-service-manifest-files"></a><span data-ttu-id="e0f72-125">應用程式和服務資訊清單檔案的概觀</span><span class="sxs-lookup"><span data-stu-id="e0f72-125">Overview of application and service manifest files</span></span>
<span data-ttu-id="e0f72-126">在部署來賓執行檔的過程中，最好先了解 Service Fabric 封裝和部署模型，如[應用程式模型](service-fabric-application-model.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="e0f72-126">As part of deploying a guest executable, it is useful to understand the Service Fabric packaging and deployment model as described in [application model](service-fabric-application-model.md).</span></span> <span data-ttu-id="e0f72-127">Service Fabric 封裝模型依賴兩個 XML 檔案：應用程式和服務資訊清單。</span><span class="sxs-lookup"><span data-stu-id="e0f72-127">The Service Fabric packaging model relies on two XML files: the application and service manifests.</span></span> <span data-ttu-id="e0f72-128">ApplicationManifest.xml 和 ServiceManifest.xml 檔案的結構描述定義是和 Service Fabric SDK 一起安裝在 C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd。</span><span class="sxs-lookup"><span data-stu-id="e0f72-128">The schema definition for the ApplicationManifest.xml and ServiceManifest.xml files is installed with the Service Fabric SDK into *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

* <span data-ttu-id="e0f72-129">**應用程式資訊清單**：應用程式資訊清單用來描述應用程式。</span><span class="sxs-lookup"><span data-stu-id="e0f72-129">**Application manifest** The application manifest is used to describe the application.</span></span> <span data-ttu-id="e0f72-130">其中列出組成該應用程式的服務，以及用來定義應如何部署一或多個服務的其他參數，例如執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="e0f72-130">It lists the services that compose it, and other parameters that are used to define how one or more services should be deployed, such as the number of instances.</span></span>

  <span data-ttu-id="e0f72-131">在 Service Fabric 中，應用程式是部署和升級的單位。</span><span class="sxs-lookup"><span data-stu-id="e0f72-131">In Service Fabric, an application is a unit of deployment and upgrade.</span></span> <span data-ttu-id="e0f72-132">應用程式可以當作單一單位來升級，而得以掌控可能的失敗和可能需要的回復。</span><span class="sxs-lookup"><span data-stu-id="e0f72-132">An application can be upgraded as a single unit where potential failures and potential rollbacks are managed.</span></span> <span data-ttu-id="e0f72-133">Service Fabric 可保證升級程序一定成功，萬一升級失敗，也不會讓應用程式處於不明或不穩定的狀態。</span><span class="sxs-lookup"><span data-stu-id="e0f72-133">Service Fabric guarantees that the upgrade process is either successful, or, if the upgrade fails, does not leave the application in an unknown or unstable state.</span></span>
* <span data-ttu-id="e0f72-134">**服務資訊清單**：服務資訊清單描述服務的元件。</span><span class="sxs-lookup"><span data-stu-id="e0f72-134">**Service manifest** The service manifest describes the components of a service.</span></span> <span data-ttu-id="e0f72-135">它包含資料，例如服務的名稱和類型、其程式碼、組態。</span><span class="sxs-lookup"><span data-stu-id="e0f72-135">It includes data, such as the name and type of service, and its code and configuration.</span></span> <span data-ttu-id="e0f72-136">服務資訊清單還包含一些在服務部署後可用來設定服務的額外參數。</span><span class="sxs-lookup"><span data-stu-id="e0f72-136">The service manifest also includes some additional parameters that can be used to configure the service once it is deployed.</span></span>

## <a name="application-package-file-structure"></a><span data-ttu-id="e0f72-137">應用程式套件檔案結構</span><span class="sxs-lookup"><span data-stu-id="e0f72-137">Application package file structure</span></span>
<span data-ttu-id="e0f72-138">為了將應用程式部署至 Service Fabric，應用程式應遵循預先定義的目錄結構。</span><span class="sxs-lookup"><span data-stu-id="e0f72-138">To deploy an application to Service Fabric, the application should follow a predefined directory structure.</span></span> <span data-ttu-id="e0f72-139">以下是該結構的範例。</span><span class="sxs-lookup"><span data-stu-id="e0f72-139">The following is an example of that structure.</span></span>

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

<span data-ttu-id="e0f72-140">ApplicationPackageRoot 包含可定義應用程式的 ApplicationManifest.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="e0f72-140">The ApplicationPackageRoot contains the ApplicationManifest.xml file that defines the application.</span></span> <span data-ttu-id="e0f72-141">對於應用程式包含的每個服務，都有一個子目錄用來包含服務所需的所有構件。</span><span class="sxs-lookup"><span data-stu-id="e0f72-141">A subdirectory for each service included in the application is used to contain all the artifacts that the service requires.</span></span> <span data-ttu-id="e0f72-142">這些子目錄是 ServiceManifest.xml，通常如下︰</span><span class="sxs-lookup"><span data-stu-id="e0f72-142">These subdirectories are the ServiceManifest.xml and, typically, the following:</span></span>

* <span data-ttu-id="e0f72-143">*Code*。</span><span class="sxs-lookup"><span data-stu-id="e0f72-143">*Code*.</span></span> <span data-ttu-id="e0f72-144">此目錄包含服務程式碼。</span><span class="sxs-lookup"><span data-stu-id="e0f72-144">This directory contains the service code.</span></span>
* <span data-ttu-id="e0f72-145">*Config*。</span><span class="sxs-lookup"><span data-stu-id="e0f72-145">*Config*.</span></span> <span data-ttu-id="e0f72-146">此目錄包含服務可在執行階段存取的 settings.xml 檔案 (和其他必要檔案)，以擷取特定組態設定。</span><span class="sxs-lookup"><span data-stu-id="e0f72-146">This directory contains a Settings.xml file (and other files if necessary) that the service can access at runtime to retrieve specific configuration settings.</span></span>
* <span data-ttu-id="e0f72-147">*Data*。</span><span class="sxs-lookup"><span data-stu-id="e0f72-147">*Data*.</span></span> <span data-ttu-id="e0f72-148">這是額外的目錄，用來儲存服務可能需要的其他本機資料。</span><span class="sxs-lookup"><span data-stu-id="e0f72-148">This is an additional directory to store additional local data that the service may need.</span></span> <span data-ttu-id="e0f72-149">資料應該只用來儲存短期資料。</span><span class="sxs-lookup"><span data-stu-id="e0f72-149">Data should be used to store only ephemeral data.</span></span> <span data-ttu-id="e0f72-150">如果必須重新定位服務 (例如在容錯移轉期間)，Service Fabric 不會將變更複製/複寫到資料目錄。</span><span class="sxs-lookup"><span data-stu-id="e0f72-150">Service Fabric does not copy or replicate changes to the data directory if the service needs to be relocated (for example, during failover).</span></span>

> [!NOTE]
> <span data-ttu-id="e0f72-151">如果不需要 `config` 和 `data` 目錄，則不必建立。</span><span class="sxs-lookup"><span data-stu-id="e0f72-151">You don't have to create the `config` and `data` directories if you don't need them.</span></span>
>
>

## <a name="package-an-existing-executable"></a><span data-ttu-id="e0f72-152">封裝現有的執行檔</span><span class="sxs-lookup"><span data-stu-id="e0f72-152">Package an existing executable</span></span>
<span data-ttu-id="e0f72-153">在封裝來賓執行檔時，您可以選擇使用 Visual Studio 專案範本，或是[手動建立應用程式套件](#manually)。</span><span class="sxs-lookup"><span data-stu-id="e0f72-153">When packaging a guest executable, you can choose either to use a Visual Studio project template or to [create the application package manually](#manually).</span></span> <span data-ttu-id="e0f72-154">使用 Visual Studio 時，就可讓 [新增專案範本] 為您建立應用程式套件的結構和資訊清單檔案。</span><span class="sxs-lookup"><span data-stu-id="e0f72-154">Using Visual Studio, the application package structure and manifest files are created by the new project template for you.</span></span>

> [!TIP]
> <span data-ttu-id="e0f72-155">將現有 Windows 可執行檔封裝成服務的最簡單方式，就是使用 Visual Studio，而在 Linux 上則是使用 Yeoman</span><span class="sxs-lookup"><span data-stu-id="e0f72-155">The easiest way to package an existing Windows executable into a service is to use Visual Studio and on Linux to use Yeoman</span></span>
>

## <a name="use-visual-studio-to-package-and-deploy-an-existing-executable"></a><span data-ttu-id="e0f72-156">使用 Visual Studio 來封裝及部署現有的可執行檔</span><span class="sxs-lookup"><span data-stu-id="e0f72-156">Use Visual Studio to package and deploy an existing executable</span></span>
<span data-ttu-id="e0f72-157">Visual Studio 會提供 Service Fabric 服務範本，協助您將來賓可執行檔部署至 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="e0f72-157">Visual Studio provides a Service Fabric service template to help you deploy a guest executable to a Service Fabric cluster.</span></span>

1. <span data-ttu-id="e0f72-158">選擇 [檔案]  >  [新增專案]，然後建立 Service Fabric 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e0f72-158">Choose **File** > **New Project**, and create a Service Fabric application.</span></span>
2. <span data-ttu-id="e0f72-159">選擇 [來賓執行檔] 做為服務範本。</span><span class="sxs-lookup"><span data-stu-id="e0f72-159">Choose **Guest Executable** as the service template.</span></span>
3. <span data-ttu-id="e0f72-160">按一下 [瀏覽] 以選取內含執行檔的資料夾，並填入其餘參數以建立服務。</span><span class="sxs-lookup"><span data-stu-id="e0f72-160">Click **Browse** to select the folder with your executable and fill in the rest of the parameters to create the service.</span></span>
   * <span data-ttu-id="e0f72-161">「Code Package Behavior」。</span><span class="sxs-lookup"><span data-stu-id="e0f72-161">*Code Package Behavior*.</span></span> <span data-ttu-id="e0f72-162">可設定為將資料夾的所有內容複製到 Visual Studio 專案，這在執行檔沒有變更時很有用。</span><span class="sxs-lookup"><span data-stu-id="e0f72-162">Can be set to copy all the content of your folder to the Visual Studio Project, which is useful if the executable does not change.</span></span> <span data-ttu-id="e0f72-163">如果您預期會變更可執行檔，並想要以動態方式取得新組建，則可以選擇改為連結到資料夾。</span><span class="sxs-lookup"><span data-stu-id="e0f72-163">If you expect the executable to change and want the ability to pick up new builds dynamically, you can choose to link to the folder instead.</span></span> <span data-ttu-id="e0f72-164">在 Visual Studio 中建立應用程式專案時，您可以使用連結的資料夾。</span><span class="sxs-lookup"><span data-stu-id="e0f72-164">You can use linked folders when creating the application project in Visual Studio.</span></span> <span data-ttu-id="e0f72-165">這會從專案內連結到來源位置，讓您可以在來源目的地更新來賓執行檔。</span><span class="sxs-lookup"><span data-stu-id="e0f72-165">This links to the source location from within the project, making it possible for you to update the guest executable in its source destination.</span></span> <span data-ttu-id="e0f72-166">在組建時使這些更新會成為應用程式套件的一部分。</span><span class="sxs-lookup"><span data-stu-id="e0f72-166">Those updates become part of the application package on build.</span></span>
   * <span data-ttu-id="e0f72-167">「Program」指定應執行以便啟動服務的執行檔。</span><span class="sxs-lookup"><span data-stu-id="e0f72-167">*Program* specifies the executable that should be run to start the service.</span></span>
   * <span data-ttu-id="e0f72-168">「Arguments」指定應傳遞至執行檔的引數。</span><span class="sxs-lookup"><span data-stu-id="e0f72-168">*Arguments* specifies the arguments that should be passed to the executable.</span></span> <span data-ttu-id="e0f72-169">這可以是具有引數的參數清單。</span><span class="sxs-lookup"><span data-stu-id="e0f72-169">It can be a list of parameters with arguments.</span></span>
   * <span data-ttu-id="e0f72-170">「WorkingFolder」指定即將啟動之程序的工作目錄。</span><span class="sxs-lookup"><span data-stu-id="e0f72-170">*WorkingFolder* specifies the working directory for the process that is going to be started.</span></span> <span data-ttu-id="e0f72-171">您可以指定三個值：</span><span class="sxs-lookup"><span data-stu-id="e0f72-171">You can specify three values:</span></span>
     * <span data-ttu-id="e0f72-172">`CodeBase` 指定工作目錄即將設為應用程式套件中的 code 目錄 (先前檔案結構中所示的 `Code` 目錄)。</span><span class="sxs-lookup"><span data-stu-id="e0f72-172">`CodeBase` specifies that the working directory is going to be set to the code directory in the application package (`Code` directory shown in the preceding file structure).</span></span>
     * <span data-ttu-id="e0f72-173">`CodePackage` 指定工作目錄即將設為應用程式套件中的根目錄 (先前檔案結構中所示的 `GuestService1Pkg`)。</span><span class="sxs-lookup"><span data-stu-id="e0f72-173">`CodePackage` specifies that the working directory is going to be set to the root of the application package    (`GuestService1Pkg` shown in the preceding file structure).</span></span>
     * <span data-ttu-id="e0f72-174">`Work` 指定檔案放在名為 work 的子目錄中。</span><span class="sxs-lookup"><span data-stu-id="e0f72-174">`Work` specifies that the files are placed in a subdirectory called work.</span></span>
4. <span data-ttu-id="e0f72-175">指定服務的名稱，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="e0f72-175">Give your service a name, and click **OK**.</span></span>
5. <span data-ttu-id="e0f72-176">如果服務需要用來進行通訊的端點，您現在可以將 protocol、port 和 type 新增至 ServiceManifest.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="e0f72-176">If your service needs an endpoint for communication, you can now add the protocol, port, and type to the ServiceManifest.xml file.</span></span> <span data-ttu-id="e0f72-177">例如：`<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`。</span><span class="sxs-lookup"><span data-stu-id="e0f72-177">For example: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.</span></span>
6. <span data-ttu-id="e0f72-178">您現在可以藉由在 Visual Studio 中偵錯方案，對本機叢集執行封裝和發佈動作。</span><span class="sxs-lookup"><span data-stu-id="e0f72-178">You can now use the package and publish action against your local cluster by debugging the solution in Visual Studio.</span></span> <span data-ttu-id="e0f72-179">準備好時，即可將應用程式發佈至遠端叢集，或將方案簽入到原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="e0f72-179">When ready, you can publish the application to a remote cluster or check in the solution to source control.</span></span>
7. <span data-ttu-id="e0f72-180">請移至本文結尾，以了解如何檢視 Service Fabric Explorer 中執行的來賓執行檔服務。</span><span class="sxs-lookup"><span data-stu-id="e0f72-180">Go to the end of this article to see how to view your guest executable service running in Service Fabric Explorer.</span></span>

## <a name="use-yoeman-to-package-and-deploy-an-existing-executable-on-linux"></a><span data-ttu-id="e0f72-181">使用 Yoeman 在 Linux 上封裝及部署現有的可執行檔</span><span class="sxs-lookup"><span data-stu-id="e0f72-181">Use Yoeman to package and deploy an existing executable on Linux</span></span>

<span data-ttu-id="e0f72-182">在 Linux 上建立及部署來賓可執行檔的程序與部署 csharp 或 java 應用程式的程序相同。</span><span class="sxs-lookup"><span data-stu-id="e0f72-182">The procedure for creating and deploying a guest executable on Linux is the same as deploying a csharp or java application.</span></span>

1. <span data-ttu-id="e0f72-183">在終端機中，輸入 `yo azuresfguest`。</span><span class="sxs-lookup"><span data-stu-id="e0f72-183">In a terminal, type `yo azuresfguest`.</span></span>
2. <span data-ttu-id="e0f72-184">為您的應用程式命名。</span><span class="sxs-lookup"><span data-stu-id="e0f72-184">Name your application.</span></span>
3. <span data-ttu-id="e0f72-185">為您的服務命名並提供詳細資料，包括可執行檔的路徑，以及叫用它時所必須使用的參數。</span><span class="sxs-lookup"><span data-stu-id="e0f72-185">Name your service, and provide the details including path of the executable and the parameters it must be invoked with.</span></span>

<span data-ttu-id="e0f72-186">Yeoman 會建立應用程式套件，其中包含適當的應用程式和資訊清單檔案，以及安裝和解除安裝指令碼。</span><span class="sxs-lookup"><span data-stu-id="e0f72-186">Yeoman creates an application package with the appropriate application and manifest files along with install and uninstall scripts.</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-an-existing-executable"></a><span data-ttu-id="e0f72-187">手動封裝和部署現有執行檔</span><span class="sxs-lookup"><span data-stu-id="e0f72-187">Manually package and deploy an existing executable</span></span>
<span data-ttu-id="e0f72-188">手動封裝來賓執行檔的程序是基於下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e0f72-188">The process of manually packaging a guest executable is based on the following general steps:</span></span>

1. <span data-ttu-id="e0f72-189">建立套件目錄結構。</span><span class="sxs-lookup"><span data-stu-id="e0f72-189">Create the package directory structure.</span></span>
2. <span data-ttu-id="e0f72-190">新增應用程式的程式碼和組態檔。</span><span class="sxs-lookup"><span data-stu-id="e0f72-190">Add the application's code and configuration files.</span></span>
3. <span data-ttu-id="e0f72-191">編輯服務資訊清單檔。</span><span class="sxs-lookup"><span data-stu-id="e0f72-191">Edit the service manifest file.</span></span>
4. <span data-ttu-id="e0f72-192">編輯應用程式資訊清單檔。</span><span class="sxs-lookup"><span data-stu-id="e0f72-192">Edit the application manifest file.</span></span>

<!--
>[AZURE.NOTE] We do provide a packaging tool that allows you to create the ApplicationPackage automatically. The tool is currently in preview. You can download it from [here](http://aka.ms/servicefabricpacktool).
-->

### <a name="create-the-package-directory-structure"></a><span data-ttu-id="e0f72-193">建立套件目錄結構</span><span class="sxs-lookup"><span data-stu-id="e0f72-193">Create the package directory structure</span></span>
<span data-ttu-id="e0f72-194">您可以如先前＜應用程式套件檔案結構＞一節所述開始建立目錄結構。</span><span class="sxs-lookup"><span data-stu-id="e0f72-194">You can start by creating the directory structure, as described in the preceding section, "Application package file structure."</span></span>

### <a name="add-the-applications-code-and-configuration-files"></a><span data-ttu-id="e0f72-195">新增應用程式的程式碼和組態檔</span><span class="sxs-lookup"><span data-stu-id="e0f72-195">Add the application's code and configuration files</span></span>
<span data-ttu-id="e0f72-196">建立目錄結構之後，您可以在 code 和 config 目錄之下新增應用程式的程式碼和組態檔。</span><span class="sxs-lookup"><span data-stu-id="e0f72-196">After you have created the directory structure, you can add the application's code and configuration files under the code and config directories.</span></span> <span data-ttu-id="e0f72-197">您也可以在 code 和 config 目錄之下建立其他目錄或子目錄。</span><span class="sxs-lookup"><span data-stu-id="e0f72-197">You can also create additional directories or subdirectories under the code or config directories.</span></span>

<span data-ttu-id="e0f72-198">Service Fabric 會進行應用程式根目錄內容的 `xcopy`，所以除了建立兩個最上層目錄 code 和 settings 以外，沒有預先定義的結構可使用 </span><span class="sxs-lookup"><span data-stu-id="e0f72-198">Service Fabric does an `xcopy` of the content of the application root directory, so there is no predefined structure to use other than creating two top directories, code and settings.</span></span> <span data-ttu-id="e0f72-199">(您可以選擇不同的名稱。</span><span class="sxs-lookup"><span data-stu-id="e0f72-199">(You can pick different names if you want.</span></span> <span data-ttu-id="e0f72-200">下一節中有更多詳細資訊)。</span><span class="sxs-lookup"><span data-stu-id="e0f72-200">More details are in the next section.)</span></span>

> [!NOTE]
> <span data-ttu-id="e0f72-201">請確定您包含應用程式需要的所有檔案和相依項目。</span><span class="sxs-lookup"><span data-stu-id="e0f72-201">Make sure that you include all the files and dependencies that the application needs.</span></span> <span data-ttu-id="e0f72-202">Service Fabric 會將應用程式套件的內容，複製到即將部署應用程式服務的叢集中的所有節點上。</span><span class="sxs-lookup"><span data-stu-id="e0f72-202">Service Fabric copies the content of the application package on all nodes in the cluster where the application's services are going to be deployed.</span></span> <span data-ttu-id="e0f72-203">該套件應包含應用程式需要執行的所有程式碼。</span><span class="sxs-lookup"><span data-stu-id="e0f72-203">The package should contain all the code that the application needs to run.</span></span> <span data-ttu-id="e0f72-204">請勿假設已經安裝相依項目。</span><span class="sxs-lookup"><span data-stu-id="e0f72-204">Do not assume that the dependencies are already installed.</span></span>
>
>

### <a name="edit-the-service-manifest-file"></a><span data-ttu-id="e0f72-205">編輯服務資訊清單檔</span><span class="sxs-lookup"><span data-stu-id="e0f72-205">Edit the service manifest file</span></span>
<span data-ttu-id="e0f72-206">下一步就是編輯服務資訊清單檔以包含下列資訊：</span><span class="sxs-lookup"><span data-stu-id="e0f72-206">The next step is to edit the service manifest file to include the following information:</span></span>

* <span data-ttu-id="e0f72-207">服務類型的名稱。</span><span class="sxs-lookup"><span data-stu-id="e0f72-207">The name of the service type.</span></span> <span data-ttu-id="e0f72-208">這是 Service Fabric 用來識別服務的識別碼。</span><span class="sxs-lookup"><span data-stu-id="e0f72-208">This is an ID that Service Fabric uses to identify a service.</span></span>
* <span data-ttu-id="e0f72-209">用來啟動應用程式 (ExeHost) 的命令。</span><span class="sxs-lookup"><span data-stu-id="e0f72-209">The command to use to launch the application (ExeHost).</span></span>
* <span data-ttu-id="e0f72-210">必須執行才能安裝應用程式 (SetupEntrypoint) 的任何指令碼。</span><span class="sxs-lookup"><span data-stu-id="e0f72-210">Any script that needs to be run to set up the application (SetupEntrypoint).</span></span>

<span data-ttu-id="e0f72-211">以下是 `ServiceManifest.xml` 檔案的範例：</span><span class="sxs-lookup"><span data-stu-id="e0f72-211">The following is an example of a `ServiceManifest.xml` file:</span></span>

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

<span data-ttu-id="e0f72-212">接下來幾節說明您需要更新的不同檔案部分。</span><span class="sxs-lookup"><span data-stu-id="e0f72-212">The following sections go over the different parts of the file that you need to update.</span></span>

#### <a name="update-servicetypes"></a><span data-ttu-id="e0f72-213">更新 ServiceTypes</span><span class="sxs-lookup"><span data-stu-id="e0f72-213">Update ServiceTypes</span></span>
```xml
<ServiceTypes>
  <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true" />
</ServiceTypes>
```

* <span data-ttu-id="e0f72-214">您可以挑選任何您要用於 `ServiceTypeName` 的名稱。</span><span class="sxs-lookup"><span data-stu-id="e0f72-214">You can pick any name that you want for `ServiceTypeName`.</span></span> <span data-ttu-id="e0f72-215">此值在 `ApplicationManifest.xml` 檔案中用來識別服務。</span><span class="sxs-lookup"><span data-stu-id="e0f72-215">The value is used in the `ApplicationManifest.xml` file to identify the service.</span></span>
* <span data-ttu-id="e0f72-216">指定 `UseImplicitHost="true"`。</span><span class="sxs-lookup"><span data-stu-id="e0f72-216">Specify `UseImplicitHost="true"`.</span></span> <span data-ttu-id="e0f72-217">此屬性會告知 Service Fabric，此服務是以獨立式 (Self-Contained) 應用程式為基礎，所以 Service Fabric 只要將它當作程序啟動並監視其健康狀況即可。</span><span class="sxs-lookup"><span data-stu-id="e0f72-217">This attribute tells Service Fabric that the service is based on a self-contained app, so all Service Fabric needs to do is to launch it as a process and monitor its health.</span></span>

#### <a name="update-codepackage"></a><span data-ttu-id="e0f72-218">更新 CodePackage</span><span class="sxs-lookup"><span data-stu-id="e0f72-218">Update CodePackage</span></span>
<span data-ttu-id="e0f72-219">CodePackage 元素指定服務程式碼的位置 (和版本)。</span><span class="sxs-lookup"><span data-stu-id="e0f72-219">The CodePackage element specifies the location (and version) of the service's code.</span></span>

```xml
<CodePackage Name="Code" Version="1.0.0.0">
```

<span data-ttu-id="e0f72-220">`Name` 元素用來在包含服務程式碼的應用程式套件中指定目錄的名稱。</span><span class="sxs-lookup"><span data-stu-id="e0f72-220">The `Name` element is used to specify the name of the directory in the application package that contains the service's code.</span></span> <span data-ttu-id="e0f72-221">`CodePackage` 也有 `version` 屬性。</span><span class="sxs-lookup"><span data-stu-id="e0f72-221">`CodePackage` also has the `version` attribute.</span></span> <span data-ttu-id="e0f72-222">這可用來指定程式碼的版本，而在 Service Fabric 中利用應用程式生命週期管理基礎結構，也可能用來升級服務的程式碼。</span><span class="sxs-lookup"><span data-stu-id="e0f72-222">This can be used to specify the version of the code, and can also potentially be used to upgrade the service's code by using the application lifecycle management infrastructure in Service Fabric.</span></span>

#### <a name="optional-update-setupentrypoint"></a><span data-ttu-id="e0f72-223">選擇性︰更新 SetupEntrypoint</span><span class="sxs-lookup"><span data-stu-id="e0f72-223">Optional: Update SetupEntrypoint</span></span>
```xml
<SetupEntryPoint>
   <ExeHost>
       <Program>scripts\launchConfig.cmd</Program>
   </ExeHost>
</SetupEntryPoint>
```
<span data-ttu-id="e0f72-224">SetupEntryPoint 元素用來指定任何應在服務的程式碼啟動前執行的可執行檔或批次檔。</span><span class="sxs-lookup"><span data-stu-id="e0f72-224">The SetupEntryPoint element is used to specify any executable or batch file that should be executed before the service's code is launched.</span></span> <span data-ttu-id="e0f72-225">這是選擇性步驟，因此如果不需要初始化，則不需納入此元素。</span><span class="sxs-lookup"><span data-stu-id="e0f72-225">It is an optional step, so it does not need to be included if there is no initialization required.</span></span> <span data-ttu-id="e0f72-226">每次重新啟動服務時，就會執行 SetupEntrypoint。</span><span class="sxs-lookup"><span data-stu-id="e0f72-226">The SetupEntryPoint is executed every time the service is restarted.</span></span>

<span data-ttu-id="e0f72-227">只有一個 SetupEntryPoint，所以如果應用程式的 setup 需要多個指令碼，則必須將 setup 指令碼組合在單一批次檔中。</span><span class="sxs-lookup"><span data-stu-id="e0f72-227">There is only one SetupEntryPoint, so setup scripts need to be grouped in a single batch file if the application's setup requires multiple scripts.</span></span> <span data-ttu-id="e0f72-228">SetupEntryPoint 可以執行任何類型的檔案：執行檔、批次檔、PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="e0f72-228">The SetupEntryPoint can execute any type of file: executable files, batch files, and PowerShell cmdlets.</span></span> <span data-ttu-id="e0f72-229">如需詳細資訊，請參閱[設定 SetupEntryPoint](service-fabric-application-runas-security.md)。</span><span class="sxs-lookup"><span data-stu-id="e0f72-229">For more details, see [Configure SetupEntryPoint](service-fabric-application-runas-security.md).</span></span>

<span data-ttu-id="e0f72-230">在上述範例中，SetupEntryPoint 會執行位於 code 目錄的 `scripts` 子目錄中的批次檔 `LaunchConfig.cmd` (假設 WorkingFolder 元素已設為 CodeBase)。</span><span class="sxs-lookup"><span data-stu-id="e0f72-230">In the preceding example, the SetupEntryPoint runs a batch file called `LaunchConfig.cmd` that is located in the `scripts` subdirectory of the code directory (assuming the WorkingFolder element is set to CodeBase).</span></span>

#### <a name="update-entrypoint"></a><span data-ttu-id="e0f72-231">更新 EntryPoint</span><span class="sxs-lookup"><span data-stu-id="e0f72-231">Update EntryPoint</span></span>
```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
  </ExeHost>
</EntryPoint>
```

<span data-ttu-id="e0f72-232">服務資訊清單檔中的 `EntryPoint` 元素用來指定如何啟動服務。</span><span class="sxs-lookup"><span data-stu-id="e0f72-232">The `EntryPoint` element in the service manifest file is used to specify how to launch the service.</span></span> <span data-ttu-id="e0f72-233">`ExeHost` 元素指定應用來啟動服務的可執行檔 (和引數)。</span><span class="sxs-lookup"><span data-stu-id="e0f72-233">The `ExeHost` element specifies the executable (and arguments) that should be used to launch the service.</span></span>

* <span data-ttu-id="e0f72-234">`Program` 指定應啟動服務的執行檔名稱。</span><span class="sxs-lookup"><span data-stu-id="e0f72-234">`Program` specifies the name of the executable that should start the service.</span></span>
* <span data-ttu-id="e0f72-235">`Arguments` 指定應傳遞至可執行檔的引數。</span><span class="sxs-lookup"><span data-stu-id="e0f72-235">`Arguments` specifies the arguments that should be passed to the executable.</span></span> <span data-ttu-id="e0f72-236">這可以是具有引數的參數清單。</span><span class="sxs-lookup"><span data-stu-id="e0f72-236">It can be a list of parameters with arguments.</span></span>
* <span data-ttu-id="e0f72-237">`WorkingFolder` 指定即將啟動之程序的工作目錄。</span><span class="sxs-lookup"><span data-stu-id="e0f72-237">`WorkingFolder` specifies the working directory for the process that is going to be started.</span></span> <span data-ttu-id="e0f72-238">您可以指定三個值：</span><span class="sxs-lookup"><span data-stu-id="e0f72-238">You can specify three values:</span></span>
  * <span data-ttu-id="e0f72-239">`CodeBase` 指定工作目錄即將設為應用程式套件中的 code 目錄 (先前檔案結構中的 `Code` 目錄)。</span><span class="sxs-lookup"><span data-stu-id="e0f72-239">`CodeBase` specifies that the working directory is going to be set to the code directory in the application package (`Code` directory in the preceding file structure).</span></span>
  * <span data-ttu-id="e0f72-240">`CodePackage` 指定工作目錄即將設為應用程式套件中的根目錄 (先前檔案結構中的 `GuestService1Pkg`)。</span><span class="sxs-lookup"><span data-stu-id="e0f72-240">`CodePackage` specifies that the working directory is going to be set to the root of the application package    (`GuestService1Pkg` in the preceding file structure).</span></span>
    * <span data-ttu-id="e0f72-241">`Work` 指定檔案放在名為 work 的子目錄中。</span><span class="sxs-lookup"><span data-stu-id="e0f72-241">`Work` specifies that the files are placed in a subdirectory called work.</span></span>

<span data-ttu-id="e0f72-242">WorkingFolder 適合用來設定正確的工作目錄，以便應用程式或初始化指令碼可使用相對路徑。</span><span class="sxs-lookup"><span data-stu-id="e0f72-242">The WorkingFolder is useful to set the correct working directory so that relative paths can be used by either the application or initialization scripts.</span></span>

#### <a name="update-endpoints-and-register-with-naming-service-for-communication"></a><span data-ttu-id="e0f72-243">更新端點，並向命名服務註冊以進行通訊</span><span class="sxs-lookup"><span data-stu-id="e0f72-243">Update Endpoints and register with Naming Service for communication</span></span>
```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
</Endpoints>

```
<span data-ttu-id="e0f72-244">在前述範例中，`Endpoint` 元素指定應用程式可以接聽的端點。</span><span class="sxs-lookup"><span data-stu-id="e0f72-244">In the preceding example, the `Endpoint` element specifies the endpoints that the application can listen on.</span></span> <span data-ttu-id="e0f72-245">在此範例中，Node.js 應用程式會接聽 http 連接埠 3000。</span><span class="sxs-lookup"><span data-stu-id="e0f72-245">In this example, the Node.js application listens on http on port 3000.</span></span>

<span data-ttu-id="e0f72-246">此外，您可以要求 Service Fabric 將此端點發佈至命名服務，讓其他服務可以探索這項服務的端點位址。</span><span class="sxs-lookup"><span data-stu-id="e0f72-246">Furthermore you can ask Service Fabric to publish this endpoint to the Naming Service so other services can discover the endpoint address to this service.</span></span> <span data-ttu-id="e0f72-247">這可讓您在服務 (來賓可執行檔) 之間通訊。</span><span class="sxs-lookup"><span data-stu-id="e0f72-247">This enables you to be able to communicate between services that are guest executables.</span></span>
<span data-ttu-id="e0f72-248">發佈的端點位址格式為 `UriScheme://IPAddressOrFQDN:Port/PathSuffix`。</span><span class="sxs-lookup"><span data-stu-id="e0f72-248">The published endpoint address is of the form `UriScheme://IPAddressOrFQDN:Port/PathSuffix`.</span></span> <span data-ttu-id="e0f72-249">`UriScheme` 和 `PathSuffix` 是選擇性的屬性。</span><span class="sxs-lookup"><span data-stu-id="e0f72-249">`UriScheme` and `PathSuffix` are optional attributes.</span></span> <span data-ttu-id="e0f72-250">`IPAddressOrFQDN` 是此執行檔所在節點的 IP 位址或完整網域名稱，系統會自動為您計算。</span><span class="sxs-lookup"><span data-stu-id="e0f72-250">`IPAddressOrFQDN` is the IP address or fully qualified domain name of the node this executable gets placed on, and it is calculated for you.</span></span>

<span data-ttu-id="e0f72-251">在下列範例中，部署服務後，您在 Service Fabric Explorer 中會看到服務執行個體已發佈的端點，類似於 `http://10.1.4.92:3000/myapp/`。</span><span class="sxs-lookup"><span data-stu-id="e0f72-251">In the following example, once the service is deployed, in Service Fabric Explorer you see an endpoint similar to `http://10.1.4.92:3000/myapp/` published for the service instance.</span></span> <span data-ttu-id="e0f72-252">或者，如果這是本機電腦，則您會看到 `http://localhost:3000/myapp/`。</span><span class="sxs-lookup"><span data-stu-id="e0f72-252">Or if this is a local machine, you see `http://localhost:3000/myapp/`.</span></span>

```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000"  UriScheme="http" PathSuffix="myapp/" Type="Input" />
</Endpoints>
```
<span data-ttu-id="e0f72-253">您可以使用這些位址搭配[反向 Proxy](service-fabric-reverseproxy.md)，就能在服務之間進行通訊。</span><span class="sxs-lookup"><span data-stu-id="e0f72-253">You can use these addresses with [reverse proxy](service-fabric-reverseproxy.md) to communicate between services.</span></span>

### <a name="edit-the-application-manifest-file"></a><span data-ttu-id="e0f72-254">編輯應用程式資訊清單檔</span><span class="sxs-lookup"><span data-stu-id="e0f72-254">Edit the application manifest file</span></span>
<span data-ttu-id="e0f72-255">設定 `Servicemanifest.xml` 檔案之後，您需要對 `ApplicationManifest.xml` 檔進行一些變更，以確保使用正確的服務類型和名稱。</span><span class="sxs-lookup"><span data-stu-id="e0f72-255">Once you have configured the `Servicemanifest.xml` file, you need to make some changes to the `ApplicationManifest.xml` file to ensure that the correct service type and name are used.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="NodeAppType" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
   </ServiceManifestImport>
</ApplicationManifest>
```

#### <a name="servicemanifestimport"></a><span data-ttu-id="e0f72-256">ServiceManifestImport</span><span class="sxs-lookup"><span data-stu-id="e0f72-256">ServiceManifestImport</span></span>
<span data-ttu-id="e0f72-257">在 `ServiceManifestImport` 元素中，您可以指定要包含在應用程式中的一個或多項服務。</span><span class="sxs-lookup"><span data-stu-id="e0f72-257">In the `ServiceManifestImport` element, you can specify one or more services that you want to include in the app.</span></span> <span data-ttu-id="e0f72-258">`ServiceManifestName` 指定 `ServiceManifest.xml` 檔案所在的目錄名稱，用來參考服務。</span><span class="sxs-lookup"><span data-stu-id="e0f72-258">Services are referenced with `ServiceManifestName`, which specifies the name of the directory where the `ServiceManifest.xml` file is located.</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
</ServiceManifestImport>
```

## <a name="set-up-logging"></a><span data-ttu-id="e0f72-259">設定記錄</span><span class="sxs-lookup"><span data-stu-id="e0f72-259">Set up logging</span></span>
<span data-ttu-id="e0f72-260">對於來賓可執行檔，最好能夠查看主控台記錄檔，以查明應用程式和設定指令碼是否顯示任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="e0f72-260">For guest executables, it is useful to be able to see console logs to find out if the application and configuration scripts show any errors.</span></span>
<span data-ttu-id="e0f72-261">在 `ServiceManifest.xml` 檔案中，可使用 `ConsoleRedirection` 元素設定主控台重新導向。</span><span class="sxs-lookup"><span data-stu-id="e0f72-261">Console redirection can be configured in the `ServiceManifest.xml` file using the `ConsoleRedirection` element.</span></span>

> [!WARNING]
> <span data-ttu-id="e0f72-262">切勿在實際部署的應用程式中使用主控台重新導向原則，因為這可能會影響應用程式容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="e0f72-262">Never use the console redirection policy in an application that is deployed in production because this can affect the application failover.</span></span> <span data-ttu-id="e0f72-263">僅將此原則用於本機開發及偵錯。</span><span class="sxs-lookup"><span data-stu-id="e0f72-263">*Only* use this for local development and debugging purposes.</span></span>  
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

<span data-ttu-id="e0f72-264">`ConsoleRedirection` 可用來將主控台輸出 (stdout 和 stderr) 重新導向到工作目錄。</span><span class="sxs-lookup"><span data-stu-id="e0f72-264">`ConsoleRedirection` can be used to redirect console output (both stdout and stderr) to a working directory.</span></span> <span data-ttu-id="e0f72-265">這提供了在 Service Fabric 叢集中設定或執行應用程式期間確認沒有發生任何錯誤的功能。</span><span class="sxs-lookup"><span data-stu-id="e0f72-265">This provides the ability to verify that there are no errors during the setup or execution of the application in the Service Fabric cluster.</span></span>

<span data-ttu-id="e0f72-266">`FileRetentionCount` 決定工作目錄中儲存多少個檔案。</span><span class="sxs-lookup"><span data-stu-id="e0f72-266">`FileRetentionCount` determines how many files are saved in the working directory.</span></span> <span data-ttu-id="e0f72-267">例如，值為 5 表示工作目錄中會儲存先前 5 次執行的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="e0f72-267">A value of 5, for example, means that the log files for the previous five executions are stored in the working directory.</span></span>

<span data-ttu-id="e0f72-268">`FileMaxSizeInKb` 指定記錄檔的大小上限。</span><span class="sxs-lookup"><span data-stu-id="e0f72-268">`FileMaxSizeInKb` specifies the maximum size of the log files.</span></span>

<span data-ttu-id="e0f72-269">記錄檔會儲存在服務的其中一個工作目錄中。</span><span class="sxs-lookup"><span data-stu-id="e0f72-269">Log files are saved in one of the service's working directories.</span></span> <span data-ttu-id="e0f72-270">若要判斷檔案的位置，使用 Service Fabric Explorer 來判斷服務執行所在的節點以及目前使用的工作目錄。</span><span class="sxs-lookup"><span data-stu-id="e0f72-270">To determine where the files are located, use Service Fabric Explorer to determine which node the service is running on, and which working directory is being used.</span></span> <span data-ttu-id="e0f72-271">本文稍後會說明此程序。</span><span class="sxs-lookup"><span data-stu-id="e0f72-271">This process is covered later in this article.</span></span>

## <a name="deployment"></a><span data-ttu-id="e0f72-272">部署</span><span class="sxs-lookup"><span data-stu-id="e0f72-272">Deployment</span></span>
<span data-ttu-id="e0f72-273">最後一個步驟是[部署應用程式](service-fabric-deploy-remove-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="e0f72-273">The last step is to [deploy your application](service-fabric-deploy-remove-applications.md).</span></span> <span data-ttu-id="e0f72-274">下列 PowerShell 指令碼示範如何將應用程式部署至本機開發叢集，並啟動新的 Service Fabric 服務。</span><span class="sxs-lookup"><span data-stu-id="e0f72-274">The following PowerShell script shows how to deploy your application to the local development cluster, and start a new Service Fabric service.</span></span>

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
> <span data-ttu-id="e0f72-275">如果封裝很大或有許多檔案，請在將它複製到映像存放區之前[壓縮封裝](service-fabric-package-apps.md#compress-a-package)。</span><span class="sxs-lookup"><span data-stu-id="e0f72-275">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store if the package is large or has many files.</span></span> <span data-ttu-id="e0f72-276">請在[這裡](service-fabric-deploy-remove-applications.md#upload-the-application-package)閱讀更多資訊。</span><span class="sxs-lookup"><span data-stu-id="e0f72-276">Read more [here](service-fabric-deploy-remove-applications.md#upload-the-application-package).</span></span>
>

<span data-ttu-id="e0f72-277">Service Fabric 服務可以各種「組態」部署。</span><span class="sxs-lookup"><span data-stu-id="e0f72-277">A Service Fabric service can be deployed in various "configurations."</span></span> <span data-ttu-id="e0f72-278">例如，它可部署為單一或多個執行個體，也可以 Service Fabric 叢集的每個節點上有一個服務執行個體的方式部署。</span><span class="sxs-lookup"><span data-stu-id="e0f72-278">For example, it can be deployed as single or multiple instances, or it can be deployed in such a way that there is one instance of the service on each node of the Service Fabric cluster.</span></span>

<span data-ttu-id="e0f72-279">`New-ServiceFabricService` Cmdlet 的 `InstanceCount` 參數用來指定應在 Service Fabric 叢集中啟動多少個服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="e0f72-279">The `InstanceCount` parameter of the `New-ServiceFabricService` cmdlet is used to specify how many instances of the service should be launched in the Service Fabric cluster.</span></span> <span data-ttu-id="e0f72-280">您可以根據要部署的應用程式類型來設定 `InstanceCount` 值。</span><span class="sxs-lookup"><span data-stu-id="e0f72-280">You can set the `InstanceCount` value, depending on the type of application that you are deploying.</span></span> <span data-ttu-id="e0f72-281">兩個最常見的案例包括：</span><span class="sxs-lookup"><span data-stu-id="e0f72-281">The two most common scenarios are:</span></span>

* <span data-ttu-id="e0f72-282">`InstanceCount = "1"`。</span><span class="sxs-lookup"><span data-stu-id="e0f72-282">`InstanceCount = "1"`.</span></span> <span data-ttu-id="e0f72-283">在此案例中，叢集中只部署一個服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="e0f72-283">In this case, only one instance of the service is deployed in the cluster.</span></span> <span data-ttu-id="e0f72-284">Service Fabric 的排程器會決定即將部署服務的節點。</span><span class="sxs-lookup"><span data-stu-id="e0f72-284">Service Fabric's scheduler determines which node the service is going to be deployed on.</span></span>
* <span data-ttu-id="e0f72-285">`InstanceCount ="-1"`。</span><span class="sxs-lookup"><span data-stu-id="e0f72-285">`InstanceCount ="-1"`.</span></span> <span data-ttu-id="e0f72-286">在此案例中，Service Fabric 叢集中的每個節點上都部署一個服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="e0f72-286">In this case, one instance of the service is deployed on every node in the Service Fabric cluster.</span></span> <span data-ttu-id="e0f72-287">結果，叢集中的每個節點都有一個 (且僅只一個) 服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="e0f72-287">The result is having one (and only one) instance of the service for each node in the cluster.</span></span>

<span data-ttu-id="e0f72-288">這是前端應用程式 (例如 REST 端點) 很有用的組態，因為用戶端應用程式只需要「連線」到叢集中的任何節點，即可使用端點。</span><span class="sxs-lookup"><span data-stu-id="e0f72-288">This is a useful configuration for front-end applications (for example, a REST endpoint), because client applications need to "connect" to any of the nodes in the cluster to use the endpoint.</span></span> <span data-ttu-id="e0f72-289">當 Service Fabric 叢集的所有節點都連線到負載平衡器時，也可使用此組態。</span><span class="sxs-lookup"><span data-stu-id="e0f72-289">This configuration can also be used when, for example, all nodes of the Service Fabric cluster are connected to a load balancer.</span></span> <span data-ttu-id="e0f72-290">如此便可將用戶端流量分散於在叢集中所有節點上執行的服務。</span><span class="sxs-lookup"><span data-stu-id="e0f72-290">Client traffic can then be distributed across the service that is running on all nodes in the cluster.</span></span>

## <a name="check-your-running-application"></a><span data-ttu-id="e0f72-291">來查執行中的應用程式</span><span class="sxs-lookup"><span data-stu-id="e0f72-291">Check your running application</span></span>
<span data-ttu-id="e0f72-292">在 Service Fabric Explorer 中，找出執行服務的節點。</span><span class="sxs-lookup"><span data-stu-id="e0f72-292">In Service Fabric Explorer, identify the node where the service is running.</span></span> <span data-ttu-id="e0f72-293">在此範例中，它是在 Node1 上執行：</span><span class="sxs-lookup"><span data-stu-id="e0f72-293">In this example, it runs on Node1:</span></span>

![服務執行所在的節點](./media/service-fabric-deploy-existing-app/nodeappinsfx.png)

<span data-ttu-id="e0f72-295">如果您巡覽至節點並瀏覽至應用程式，您會看到基本節點資訊，包括它在磁碟上的位置。</span><span class="sxs-lookup"><span data-stu-id="e0f72-295">If you navigate to the node and browse to the application, you see the essential node information, including its location on disk.</span></span>

![在磁碟上的位置](./media/service-fabric-deploy-existing-app/locationondisk2.png)

<span data-ttu-id="e0f72-297">如果您使用「伺服器總管」來瀏覽至目錄，您可以找到工作目錄和服務的記錄檔資料夾，如以下螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="e0f72-297">If you browse to the directory by using Server Explorer, you can find the working directory and the service's log folder, as shown in the following screenshot:</span></span> 

![記錄檔的位置](./media/service-fabric-deploy-existing-app/loglocation.png)

## <a name="next-steps"></a><span data-ttu-id="e0f72-299">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e0f72-299">Next steps</span></span>
<span data-ttu-id="e0f72-300">在本文中，您已經學會如何封裝來賓可執行檔並部署至 Service Fabric。</span><span class="sxs-lookup"><span data-stu-id="e0f72-300">In this article, you have learned how to package a guest executable and deploy it to Service Fabric.</span></span> <span data-ttu-id="e0f72-301">請參閱下列文章以了解相關資訊和工作。</span><span class="sxs-lookup"><span data-stu-id="e0f72-301">See the following articles for related information and tasks.</span></span>

* <span data-ttu-id="e0f72-302">[封裝和部署來賓可執行檔的範例](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)，包括封裝工具預先發行版本的連結</span><span class="sxs-lookup"><span data-stu-id="e0f72-302">[Sample for packaging and deploying a guest executable](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), including a link to the prerelease of the packaging tool</span></span>
* [<span data-ttu-id="e0f72-303">兩個客體可執行檔 (C# 和 nodejs) 使用 REST 透過命名服務進行通訊的範例</span><span class="sxs-lookup"><span data-stu-id="e0f72-303">Sample of two guest executables (C# and nodejs) communicating via the Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
* [<span data-ttu-id="e0f72-304">部署多個來賓可執行檔</span><span class="sxs-lookup"><span data-stu-id="e0f72-304">Deploy multiple guest executables</span></span>](service-fabric-deploy-multiple-apps.md)
* [<span data-ttu-id="e0f72-305">使用 Visual Studio 建立第一個 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="e0f72-305">Create your first Service Fabric application using Visual Studio</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
