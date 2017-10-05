---
title: "Azure Service Fabric 應用程式模型 | Microsoft Docs"
description: "如何在 Service Fabric 中建立模型和描述應用程式與服務。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: mani-ramaswamy
ms.assetid: 17a99380-5ed8-4ed9-b884-e9b827431b02
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: ryanwi
ms.openlocfilehash: e30482427b88eb3e58d39075c7f0734664b79aa2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="model-an-application-in-service-fabric"></a><span data-ttu-id="89bcd-103">在 Service Fabric 中模型化應用程式</span><span class="sxs-lookup"><span data-stu-id="89bcd-103">Model an application in Service Fabric</span></span>
<span data-ttu-id="89bcd-104">本文提供 Azure Service Fabric 應用程式模型的概觀，以及如何透過資訊清單檔案定義應用程式和服務。</span><span class="sxs-lookup"><span data-stu-id="89bcd-104">This article provides an overview of the Azure Service Fabric application model and how to define an application and service via manifest files.</span></span>

## <a name="understand-the-application-model"></a><span data-ttu-id="89bcd-105">了解應用程式模型</span><span class="sxs-lookup"><span data-stu-id="89bcd-105">Understand the application model</span></span>
<span data-ttu-id="89bcd-106">應用程式是組成服務的集合，這些服務會執行特定函數。</span><span class="sxs-lookup"><span data-stu-id="89bcd-106">An application is a collection of constituent services that perform a certain function or functions.</span></span> <span data-ttu-id="89bcd-107">服務會執行完整且獨立的函式，並且可獨立於其他服務啟動和執行。</span><span class="sxs-lookup"><span data-stu-id="89bcd-107">A service performs a complete and standalone function and can start and run independently of other services.</span></span>  <span data-ttu-id="89bcd-108">服務是由程式碼、組態和資料所組成。</span><span class="sxs-lookup"><span data-stu-id="89bcd-108">A service is composed of code, configuration, and data.</span></span> <span data-ttu-id="89bcd-109">針對每個服務，程式碼由可執行檔二進位檔組成、組態由可在執行階段載入的服務設定組成，而資料由讓服務使用的任意靜態資料組成。</span><span class="sxs-lookup"><span data-stu-id="89bcd-109">For each service, code consists of the executable binaries, configuration consists of service settings that can be loaded at run time, and data consists of arbitrary static data to be consumed by the service.</span></span> <span data-ttu-id="89bcd-110">此階層應用程式模型中的每個元件都可以獨立建立版本和升級。</span><span class="sxs-lookup"><span data-stu-id="89bcd-110">Each component in this hierarchical application model can be versioned and upgraded independently.</span></span>

![Service Fabric 應用程式模型][appmodel-diagram]

<span data-ttu-id="89bcd-112">應用程式類型是應用程式的分類，由服務類型的組合所組成。</span><span class="sxs-lookup"><span data-stu-id="89bcd-112">An application type is a categorization of an application and consists of a bundle of service types.</span></span> <span data-ttu-id="89bcd-113">服務類型是一項服務分類。</span><span class="sxs-lookup"><span data-stu-id="89bcd-113">A service type is a categorization of a service.</span></span> <span data-ttu-id="89bcd-114">分類可以有不同的設定和組態，但是核心功能保持不變。</span><span class="sxs-lookup"><span data-stu-id="89bcd-114">The categorization can have different settings and configurations, but the core functionality remains the same.</span></span> <span data-ttu-id="89bcd-115">服務的執行個體是相同服務類型的不同服務組態變形。</span><span class="sxs-lookup"><span data-stu-id="89bcd-115">The instances of a service are the different service configuration variations of the same service type.</span></span>  

<span data-ttu-id="89bcd-116">應用程式和服務的類別 (或「類型」) 是透過 XML 檔案 (應用程式資訊清單和服務資訊清單) 來說明。</span><span class="sxs-lookup"><span data-stu-id="89bcd-116">Classes (or "types") of applications and services are described through XML files (application manifests and service manifests).</span></span>  <span data-ttu-id="89bcd-117">資訊清單是應用程式可以從叢集的映像存放區具現化的範本。</span><span class="sxs-lookup"><span data-stu-id="89bcd-117">The manifests are the templates against which applications can be instantiated from the cluster's image store.</span></span> <span data-ttu-id="89bcd-118">ServiceManifest.xml 和 ApplicationManifest.xml 檔案的結構描述定義是和 Service Fabric SDK 及工具一起安裝在 C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd。</span><span class="sxs-lookup"><span data-stu-id="89bcd-118">The schema definition for the ServiceManifest.xml and ApplicationManifest.xml file is installed with the Service Fabric SDK and tools to *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

<span data-ttu-id="89bcd-119">不同應用程式執行個體的程式碼會以個別程序的形式執行，即使是由相同的 Service Fabric 節點所裝載。</span><span class="sxs-lookup"><span data-stu-id="89bcd-119">The code for different application instances run as separate processes even when hosted by the same Service Fabric node.</span></span> <span data-ttu-id="89bcd-120">此外，每個應用程式執行個體的生命週期可以獨立進行管理 (例如，升級)。</span><span class="sxs-lookup"><span data-stu-id="89bcd-120">Furthermore, the lifecycle of each application instance can be managed (for example, upgraded) independently.</span></span> <span data-ttu-id="89bcd-121">下圖顯示應用程式類型如何由服務類型組成，依序分別為程式碼、組態和資料套件的組成。</span><span class="sxs-lookup"><span data-stu-id="89bcd-121">The following diagram shows how application types are composed of service types, which in turn are composed of code, configuration, and data packages.</span></span> <span data-ttu-id="89bcd-122">為了簡化此圖，只會顯示 `ServiceType4` 的程式碼/組態/資料套件，但每個服務類型都包含這其中部分或所有的套件類型。</span><span class="sxs-lookup"><span data-stu-id="89bcd-122">To simplify the diagram, only the code/config/data packages for `ServiceType4` are shown, though each service type would include some or all those package types.</span></span>

![Service Fabric 應用程式類型和服務類型][cluster-imagestore-apptypes]

<span data-ttu-id="89bcd-124">兩個用來說明應用程式和服務的不同資訊清單檔案：服務資訊清單和應用程式資訊清單。</span><span class="sxs-lookup"><span data-stu-id="89bcd-124">Two different manifest files are used to describe applications and services: the service manifest and application manifest.</span></span> <span data-ttu-id="89bcd-125">下列各節會詳細討論資訊清單。</span><span class="sxs-lookup"><span data-stu-id="89bcd-125">Manifests are covered in detail in the following sections.</span></span>

<span data-ttu-id="89bcd-126">叢集中可以有一或多個使用中的服務類型執行個體。</span><span class="sxs-lookup"><span data-stu-id="89bcd-126">There can be one or more instances of a service type active in the cluster.</span></span> <span data-ttu-id="89bcd-127">例如，可設定狀態的服務執行個體或複本，藉由複寫叢集中不同節點上複本之間的狀態達到高可靠性。</span><span class="sxs-lookup"><span data-stu-id="89bcd-127">For example, stateful service instances, or replicas, achieve high reliability by replicating state between replicas located on different nodes in the cluster.</span></span> <span data-ttu-id="89bcd-128">即使叢集中有一個節點失敗，複寫基本上會提供備援讓服務可供使用。</span><span class="sxs-lookup"><span data-stu-id="89bcd-128">Replication essentially provides redundancy for the service to be available even if one node in a cluster fails.</span></span> <span data-ttu-id="89bcd-129">[分割服務](service-fabric-concepts-partitioning.md) 進一步在叢集中的節點之間分割其狀態 (並且存取該狀態的模式)。</span><span class="sxs-lookup"><span data-stu-id="89bcd-129">A [partitioned service](service-fabric-concepts-partitioning.md) further divides its state (and access patterns to that state) across nodes in the cluster.</span></span>

<span data-ttu-id="89bcd-130">下圖顯示應用程式和服務執行個體、分割和複本之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="89bcd-130">The following diagram shows the relationship between applications and service instances, partitions, and replicas.</span></span>

![服務內的分割和複本][cluster-application-instances]

> [!TIP]
> <span data-ttu-id="89bcd-132">您可以使用 Service Fabric Explorer 工具，在叢集中檢視應用程式的配置，該工具可以在 http://&lt;yourclusteraddress&gt;:19080/Explorer 上取得。</span><span class="sxs-lookup"><span data-stu-id="89bcd-132">You can view the layout of applications in a cluster using the Service Fabric Explorer tool available at http://&lt;yourclusteraddress&gt;:19080/Explorer.</span></span> <span data-ttu-id="89bcd-133">如需詳細資訊，請參閱[使用 Service Fabric Explorer 視覺化叢集](service-fabric-visualizing-your-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="89bcd-133">For more information, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
> 
> 

## <a name="describe-a-service"></a><span data-ttu-id="89bcd-134">描述服務</span><span class="sxs-lookup"><span data-stu-id="89bcd-134">Describe a service</span></span>
<span data-ttu-id="89bcd-135">服務資訊清單以宣告方式定義服務類型和版本。</span><span class="sxs-lookup"><span data-stu-id="89bcd-135">The service manifest declaratively defines the service type and version.</span></span> <span data-ttu-id="89bcd-136">它會指定如服務類型的服務中繼資料、健康狀態屬性、負載平衡度量、服務二進位檔和組態檔。</span><span class="sxs-lookup"><span data-stu-id="89bcd-136">It specifies service metadata such as service type, health properties, load-balancing metrics, service binaries, and configuration files.</span></span>  <span data-ttu-id="89bcd-137">換句話說，它會描述組成服務封裝的程式碼、組態和資料封裝，以支援一或多個服務類型。</span><span class="sxs-lookup"><span data-stu-id="89bcd-137">Put another way, it describes the code, configuration, and data packages that compose a service package to support one or more service types.</span></span> <span data-ttu-id="89bcd-138">以下是簡單的範例服務資訊清單：</span><span class="sxs-lookup"><span data-stu-id="89bcd-138">Here is a simple example service manifest:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="MyCode" Version="CodeVersion1">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
    <EnvironmentVariables>
      <EnvironmentVariable Name="MyEnvVariable" Value=""/>
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentVariables>
  </CodePackage>
  <ConfigPackage Name="MyConfig" Version="ConfigVersion1" />
  <DataPackage Name="MyData" Version="DataVersion1" />
</ServiceManifest>
```

<span data-ttu-id="89bcd-139">**版本** 屬性為非結構化字串，不是由系統剖析。</span><span class="sxs-lookup"><span data-stu-id="89bcd-139">**Version** attributes are unstructured strings and not parsed by the system.</span></span> <span data-ttu-id="89bcd-140">版本屬性用於設定每個元件的版本以進行升級。</span><span class="sxs-lookup"><span data-stu-id="89bcd-140">Version attributes are used to version each component for upgrades.</span></span>

<span data-ttu-id="89bcd-141">**ServiceTypes** 會宣告此資訊清單中 **CodePackages** 支援哪些服務類型。</span><span class="sxs-lookup"><span data-stu-id="89bcd-141">**ServiceTypes** declares what service types are supported by **CodePackages** in this manifest.</span></span> <span data-ttu-id="89bcd-142">當針對其中一種服務類型來具現化服務時，會藉由執行其進入點來啟動此資訊清單中宣告的所有程式碼封裝。</span><span class="sxs-lookup"><span data-stu-id="89bcd-142">When a service is instantiated against one of these service types, all code packages declared in this manifest are activated by running their entry points.</span></span> <span data-ttu-id="89bcd-143">產生的處理程序預期在執行階段註冊支援的服務類型。</span><span class="sxs-lookup"><span data-stu-id="89bcd-143">The resulting processes are expected to register the supported service types at run time.</span></span> <span data-ttu-id="89bcd-144">服務類型是在資訊清單層級而非程式碼套件層級宣告。</span><span class="sxs-lookup"><span data-stu-id="89bcd-144">Service types are declared at the manifest level and not the code package level.</span></span> <span data-ttu-id="89bcd-145">因此如果有多個程式碼封裝，每當系統尋找任何一個宣告的服務類型時，它們都會啟動。</span><span class="sxs-lookup"><span data-stu-id="89bcd-145">So when there are multiple code packages, they are all activated whenever the system looks for any one of the declared service types.</span></span>

<span data-ttu-id="89bcd-146">**SetupEntryPoint** 是以與 Service Fabric 相同的認證執行的特殊權限進入點 (通常 *LocalSystem* 帳戶)，優先於任何其他進入點。</span><span class="sxs-lookup"><span data-stu-id="89bcd-146">**SetupEntryPoint** is a privileged entry point that runs with the same credentials as Service Fabric (typically the *LocalSystem* account) before any other entry point.</span></span> <span data-ttu-id="89bcd-147">**EntryPoint** 指定的可執行檔通常是長時間執行的服務主機。</span><span class="sxs-lookup"><span data-stu-id="89bcd-147">The executable specified by **EntryPoint** is typically the long-running service host.</span></span> <span data-ttu-id="89bcd-148">有個別設定的進入點，就不需要使用較高權限來長時間執行服務主機。</span><span class="sxs-lookup"><span data-stu-id="89bcd-148">The presence of a separate setup entry point avoids having to run the service host with high privileges for extended periods of time.</span></span> <span data-ttu-id="89bcd-149">**EntryPoint** 指定的可執行檔是在 **SetupEntryPoint** 成功結束之後執行。</span><span class="sxs-lookup"><span data-stu-id="89bcd-149">The executable specified by **EntryPoint** is run after **SetupEntryPoint** exits successfully.</span></span> <span data-ttu-id="89bcd-150">如果程序曾經終止或當機，則產生的程序會受到監視並重新啟動 (以 **SetupEntryPoint**再次開始)。</span><span class="sxs-lookup"><span data-stu-id="89bcd-150">If the process ever terminates or crashes, the resulting process is monitored and restarted (beginning again with **SetupEntryPoint**).</span></span>  

<span data-ttu-id="89bcd-151">使用 **SetupEntryPoint** 的一般案例，是當您在服務啟動之前執行可執行檔，或使用提高的權限來執行作業時。</span><span class="sxs-lookup"><span data-stu-id="89bcd-151">Typical scenarios for using **SetupEntryPoint** are when you run an executable before the service starts or you perform an operation with elevated privileges.</span></span> <span data-ttu-id="89bcd-152">例如：</span><span class="sxs-lookup"><span data-stu-id="89bcd-152">For example:</span></span>

* <span data-ttu-id="89bcd-153">設定及初始化服務可執行檔需要的環境變數。</span><span class="sxs-lookup"><span data-stu-id="89bcd-153">Setting up and initializing environment variables that the service executable needs.</span></span> <span data-ttu-id="89bcd-154">這不限於透過 Service Fabric 程式設計模型撰寫的執行檔。</span><span class="sxs-lookup"><span data-stu-id="89bcd-154">This is not limited to only executables written via the Service Fabric programming models.</span></span> <span data-ttu-id="89bcd-155">例如，npm.exe 部署 node.js 應用程式，需要設定某些環境變數。</span><span class="sxs-lookup"><span data-stu-id="89bcd-155">For example, npm.exe needs some environment variables configured for deploying a node.js application.</span></span>
* <span data-ttu-id="89bcd-156">透過安裝安全性憑證設定存取控制。</span><span class="sxs-lookup"><span data-stu-id="89bcd-156">Setting up access control by installing security certificates.</span></span>

<span data-ttu-id="89bcd-157">如需有關如何設定 **SetupEntryPoint** 的更多詳細資料，請參閱[設定服務安裝程式進入點的原則](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="89bcd-157">For more details on how to configure the **SetupEntryPoint** see [Configure the policy for a service setup entry point](service-fabric-application-runas-security.md)</span></span>

<span data-ttu-id="89bcd-158">**EnvironmentVariables** 提供針對此程式碼封裝設定的環境變數清單。</span><span class="sxs-lookup"><span data-stu-id="89bcd-158">**EnvironmentVariables** provides a list of environment variables that are set for this code package.</span></span> <span data-ttu-id="89bcd-159">您可以在 `ApplicationManifest.xml` 中覆寫環境變數，以針對不同的服務執行個體提供不同的值。</span><span class="sxs-lookup"><span data-stu-id="89bcd-159">Environmentment variables can be overridden in the `ApplicationManifest.xml` to provide different values for different service instances.</span></span> 

<span data-ttu-id="89bcd-160">**DataPackage** 宣告 **Name** 屬性所命名的資料夾，包含由程序在執行階段使用的任意靜態資料。</span><span class="sxs-lookup"><span data-stu-id="89bcd-160">**DataPackage** declares a folder, named by the **Name** attribute, that contains arbitrary static data to be consumed by the process at run time.</span></span>

<span data-ttu-id="89bcd-161">**ConfigPackage** 宣告 **Name** 屬性所命名的資料夾，其中包含 *Settings.xml* 檔案。</span><span class="sxs-lookup"><span data-stu-id="89bcd-161">**ConfigPackage** declares a folder, named by the **Name** attribute, that contains a *Settings.xml* file.</span></span> <span data-ttu-id="89bcd-162">設定檔案包含程序在執行階段讀回的使用者定義、成對的索引鍵/值設定等區段。</span><span class="sxs-lookup"><span data-stu-id="89bcd-162">The settings file contains sections of user-defined, key-value pair settings that the process reads back at run time.</span></span> <span data-ttu-id="89bcd-163">在升級期間，如果只有 **ConfigPackage** **版本**已變更，則不會重新啟動執行中程序。</span><span class="sxs-lookup"><span data-stu-id="89bcd-163">During an upgrade, if only the **ConfigPackage** **version** has changed, then the running process is not restarted.</span></span> <span data-ttu-id="89bcd-164">相反地，回呼會通知程序組態設定已變更，因此它們可以動態方式重新載入。</span><span class="sxs-lookup"><span data-stu-id="89bcd-164">Instead, a callback notifies the process that configuration settings have changed so they can be reloaded dynamically.</span></span> <span data-ttu-id="89bcd-165">以下是 *Settings.xml* 檔案的範例：</span><span class="sxs-lookup"><span data-stu-id="89bcd-165">Here is an example *Settings.xml* file:</span></span>

```xml
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MyConfigurationSection">
    <Parameter Name="MySettingA" Value="Example1" />
    <Parameter Name="MySettingB" Value="Example2" />
  </Section>
</Settings>
```

> [!NOTE]
> <span data-ttu-id="89bcd-166">服務資訊清單可以包含多個程式碼、組態和資料封裝。</span><span class="sxs-lookup"><span data-stu-id="89bcd-166">A service manifest can contain multiple code, configuration, and data packages.</span></span> <span data-ttu-id="89bcd-167">每個皆可獨立建立版本。</span><span class="sxs-lookup"><span data-stu-id="89bcd-167">Each of those can be versioned independently.</span></span>
> 
> 

<!--
For more information about other features supported by service manifests, refer to the following articles:

*TODO: LoadMetrics, PlacementConstraints, ServicePlacementPolicies
*TODO: Resources
*TODO: Health properties
*TODO: Trace filters
*TODO: Configuration overrides
-->

## <a name="describe-an-application"></a><span data-ttu-id="89bcd-168">描述應用程式</span><span class="sxs-lookup"><span data-stu-id="89bcd-168">Describe an application</span></span>
<span data-ttu-id="89bcd-169">應用程式資訊清單以宣告方式描述應用程式類型和版本。</span><span class="sxs-lookup"><span data-stu-id="89bcd-169">The application manifest declaratively describes the application type and version.</span></span> <span data-ttu-id="89bcd-170">它指定服務組成中繼資料，例如穩定的名稱、分割配置、執行個體計數/複寫因數、安全性/隔離原則、安置限制、組態覆寫和組成服務類型。</span><span class="sxs-lookup"><span data-stu-id="89bcd-170">It specifies service composition metadata such as stable names, partitioning scheme, instance count/replication factor, security/isolation policy, placement constraints, configuration overrides, and constituent service types.</span></span> <span data-ttu-id="89bcd-171">也說明要放置應用程式的負載平衡網域。</span><span class="sxs-lookup"><span data-stu-id="89bcd-171">The load-balancing domains into which the application is placed are also described.</span></span>

<span data-ttu-id="89bcd-172">因此，應用程式資訊清單描述應用程式層級的元素，並參考用來組成應用程式類型的一個或多個服務資訊清單。</span><span class="sxs-lookup"><span data-stu-id="89bcd-172">Thus, an application manifest describes elements at the application level and references one or more service manifests to compose an application type.</span></span> <span data-ttu-id="89bcd-173">以下是簡單的範例應用程式資訊清單：</span><span class="sxs-lookup"><span data-stu-id="89bcd-173">Here is a simple example application manifest:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ApplicationManifest
      ApplicationTypeName="MyApplicationType"
      ApplicationTypeVersion="AppManifestVersion1"
      xmlns="http://schemas.microsoft.com/2011/01/fabric"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example application manifest</Description>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="MyServiceManifest" ServiceManifestVersion="SvcManifestVersion1"/>
    <ConfigOverrides/>
    <EnvironmentOverrides CodePackageRef="MyCode"/>
  </ServiceManifestImport>
  <DefaultServices>
     <Service Name="MyService">
         <StatelessService ServiceTypeName="MyServiceType" InstanceCount="1">
             <SingletonPartition/>
         </StatelessService>
     </Service>
  </DefaultServices>
</ApplicationManifest>
```

<span data-ttu-id="89bcd-174">如同服務資訊清單， **版本** 屬性為非結構化字串，不是由系統剖析。</span><span class="sxs-lookup"><span data-stu-id="89bcd-174">Like service manifests, **Version** attributes are unstructured strings and are not parsed by the system.</span></span> <span data-ttu-id="89bcd-175">版本屬性也用於設定每個元件的版本以進行升級。</span><span class="sxs-lookup"><span data-stu-id="89bcd-175">Version attributes are also used to version each component for upgrades.</span></span>

<span data-ttu-id="89bcd-176">**ServiceManifestImport** 包含組成此應用程式類型之服務資訊清單的參考。</span><span class="sxs-lookup"><span data-stu-id="89bcd-176">**ServiceManifestImport** contains references to service manifests that compose this application type.</span></span> <span data-ttu-id="89bcd-177">匯入的服務資訊清單會決定此應用程式類型中哪些服務類型有效。</span><span class="sxs-lookup"><span data-stu-id="89bcd-177">Imported service manifests determine what service types are valid within this application type.</span></span> <span data-ttu-id="89bcd-178">在 ServiceManifestImport 內，您可覆寫 Settings.xml 中的組態值和 ServiceManifest.xml 檔案中的環境變數。</span><span class="sxs-lookup"><span data-stu-id="89bcd-178">Within the ServiceManifestImport, you override configuration values in Settings.xml and environment variables in ServiceManifest.xml files.</span></span> 


<span data-ttu-id="89bcd-179">**DefaultServices** 宣告服務執行個體，該執行個體會在每次應用程式針對此應用程式類型具現化時建立。</span><span class="sxs-lookup"><span data-stu-id="89bcd-179">**DefaultServices** declares service instances that are automatically created whenever an application is instantiated against this application type.</span></span> <span data-ttu-id="89bcd-180">預設服務只是為了方便起見，在建立之後，其行為在每個方面就像正常的服務。</span><span class="sxs-lookup"><span data-stu-id="89bcd-180">Default services are just a convenience and behave like normal services in every respect after they have been created.</span></span> <span data-ttu-id="89bcd-181">它們會與應用程式執行個體中的其他任何服務一起升級，也可以一起移除。</span><span class="sxs-lookup"><span data-stu-id="89bcd-181">They are upgraded along with any other services in the application instance and can be removed as well.</span></span>

> [!NOTE]
> <span data-ttu-id="89bcd-182">應用程式資訊清單可以包含多個服務資訊清單匯入和預設服務。</span><span class="sxs-lookup"><span data-stu-id="89bcd-182">An application manifest can contain multiple service manifest imports and default services.</span></span> <span data-ttu-id="89bcd-183">每個服務資訊清單匯入都可以獨立建立版本。</span><span class="sxs-lookup"><span data-stu-id="89bcd-183">Each service manifest import can be versioned independently.</span></span>
> 
> 

<span data-ttu-id="89bcd-184">若要了解如何針對個別環境維護不同的應用程式和服務參數，請參閱 [管理多個環境的應用程式參數](service-fabric-manage-multiple-environment-app-configuration.md)</span><span class="sxs-lookup"><span data-stu-id="89bcd-184">To learn how to maintain different application and service parameters for individual environments, see [Managing application parameters for multiple environments](service-fabric-manage-multiple-environment-app-configuration.md).</span></span>

<!--
For more information about other features supported by application manifests, refer to the following articles:

*TODO: Application parameters
*TODO: Security, Principals, RunAs, SecurityAccessPolicy
*TODO: Service Templates
-->



## <a name="next-steps"></a><span data-ttu-id="89bcd-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="89bcd-185">Next steps</span></span>
<span data-ttu-id="89bcd-186">[封裝應用程式](service-fabric-package-apps.md)並讓它準備好進行部署。</span><span class="sxs-lookup"><span data-stu-id="89bcd-186">[Package an application](service-fabric-package-apps.md) and make it ready to deploy.</span></span>

<span data-ttu-id="89bcd-187">[部署與移除應用程式][10]說明如何使用 PowerShell 來管理應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="89bcd-187">[Deploy and remove applications][10] describes how to use PowerShell to manage application instances.</span></span>

<span data-ttu-id="89bcd-188">[管理多個環境的應用程式參數][11]說明如何為不同的應用程式執行個體設定參數和環境變數。</span><span class="sxs-lookup"><span data-stu-id="89bcd-188">[Managing application parameters for multiple environments][11] describes how to configure parameters and environment variables for different application instances.</span></span>

<span data-ttu-id="89bcd-189">[設定應用程式的安全性原則][12]說明如何依據安全性原則執行服務來限制存取。</span><span class="sxs-lookup"><span data-stu-id="89bcd-189">[Configure security policies for your application][12] describes how to run services under security policies to restrict access.</span></span>

<span data-ttu-id="89bcd-190">[應用程式主控模型][13]說明已部署之服務的複本 (或執行個體) 與服務主機處理序之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="89bcd-190">[Application hosting models][13] describe relationship between replicas (or instances) of a deployed service and service-host process.</span></span>

<!--Image references-->
[appmodel-diagram]: ./media/service-fabric-application-model/application-model.png
[cluster-imagestore-apptypes]: ./media/service-fabric-application-model/cluster-imagestore-apptypes.png
[cluster-application-instances]: media/service-fabric-application-model/cluster-application-instances.png

<!--Link references--In actual articles, you only need a single period before the slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
[13]: service-fabric-hosting-model.md
