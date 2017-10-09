---
title: "aaaAzure Service Fabric 應用程式模型 |Microsoft 文件"
description: "如何 toomodel 並描述應用程式和服務網狀架構中的服務。"
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
ms.openlocfilehash: 54c4d026e7d556be5f697d4a6f2ee886687e1c35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="model-an-application-in-service-fabric"></a><span data-ttu-id="a30e3-103">在 Service Fabric 中模型化應用程式</span><span class="sxs-lookup"><span data-stu-id="a30e3-103">Model an application in Service Fabric</span></span>
<span data-ttu-id="a30e3-104">本文章提供 hello Azure Service Fabric 應用程式模型，以及如何 toodefine 應用程式和服務透過資訊清單檔案的總覽。</span><span class="sxs-lookup"><span data-stu-id="a30e3-104">This article provides an overview of hello Azure Service Fabric application model and how toodefine an application and service via manifest files.</span></span>

## <a name="understand-hello-application-model"></a><span data-ttu-id="a30e3-105">了解 hello 應用程式模型</span><span class="sxs-lookup"><span data-stu-id="a30e3-105">Understand hello application model</span></span>
<span data-ttu-id="a30e3-106">應用程式是組成服務的集合，這些服務會執行特定函數。</span><span class="sxs-lookup"><span data-stu-id="a30e3-106">An application is a collection of constituent services that perform a certain function or functions.</span></span> <span data-ttu-id="a30e3-107">服務會執行完整且獨立的函式，並且可獨立於其他服務啟動和執行。</span><span class="sxs-lookup"><span data-stu-id="a30e3-107">A service performs a complete and standalone function and can start and run independently of other services.</span></span>  <span data-ttu-id="a30e3-108">服務是由程式碼、組態和資料所組成。</span><span class="sxs-lookup"><span data-stu-id="a30e3-108">A service is composed of code, configuration, and data.</span></span> <span data-ttu-id="a30e3-109">每一個服務程式碼 hello 可執行檔的二進位檔、 組態所組成，可在執行階段載入的服務設定和組成資料包含任意的靜態資料 toobe hello 服務所使用。</span><span class="sxs-lookup"><span data-stu-id="a30e3-109">For each service, code consists of hello executable binaries, configuration consists of service settings that can be loaded at run time, and data consists of arbitrary static data toobe consumed by hello service.</span></span> <span data-ttu-id="a30e3-110">此階層應用程式模型中的每個元件都可以獨立建立版本和升級。</span><span class="sxs-lookup"><span data-stu-id="a30e3-110">Each component in this hierarchical application model can be versioned and upgraded independently.</span></span>

![hello Service Fabric 應用程式模型][appmodel-diagram]

<span data-ttu-id="a30e3-112">應用程式類型是應用程式的分類，由服務類型的組合所組成。</span><span class="sxs-lookup"><span data-stu-id="a30e3-112">An application type is a categorization of an application and consists of a bundle of service types.</span></span> <span data-ttu-id="a30e3-113">服務類型是一項服務分類。</span><span class="sxs-lookup"><span data-stu-id="a30e3-113">A service type is a categorization of a service.</span></span> <span data-ttu-id="a30e3-114">hello 分類可以有不同的設定與組態，但 hello 核心功能仍維持 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="a30e3-114">hello categorization can have different settings and configurations, but hello core functionality remains hello same.</span></span> <span data-ttu-id="a30e3-115">hello 服務執行個體是 hello 不同服務組態變化的 hello 相同服務類型。</span><span class="sxs-lookup"><span data-stu-id="a30e3-115">hello instances of a service are hello different service configuration variations of hello same service type.</span></span>  

<span data-ttu-id="a30e3-116">應用程式和服務的類別 (或「類型」) 是透過 XML 檔案 (應用程式資訊清單和服務資訊清單) 來說明。</span><span class="sxs-lookup"><span data-stu-id="a30e3-116">Classes (or "types") of applications and services are described through XML files (application manifests and service manifests).</span></span>  <span data-ttu-id="a30e3-117">hello 資訊清單是針對應用程式可以具現化 hello 叢集映像存放區中的 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="a30e3-117">hello manifests are hello templates against which applications can be instantiated from hello cluster's image store.</span></span> <span data-ttu-id="a30e3-118">hello hello ServiceManifest.xml 和 ApplicationManifest.xml 檔案的結構描述定義會隨 hello Service Fabric SDK 和工具太*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="a30e3-118">hello schema definition for hello ServiceManifest.xml and ApplicationManifest.xml file is installed with hello Service Fabric SDK and tools too*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

<span data-ttu-id="a30e3-119">hello 不同的應用程式執行個體的程式碼執行不同的處理序所裝載時，即使 hello 相同的 Service Fabric 節點。</span><span class="sxs-lookup"><span data-stu-id="a30e3-119">hello code for different application instances run as separate processes even when hosted by hello same Service Fabric node.</span></span> <span data-ttu-id="a30e3-120">此外，可以 hello 的每個應用程式執行個體的生命週期管理 （例如升級） 獨立。</span><span class="sxs-lookup"><span data-stu-id="a30e3-120">Furthermore, hello lifecycle of each application instance can be managed (for example, upgraded) independently.</span></span> <span data-ttu-id="a30e3-121">hello 下列圖表顯示應用程式類型的服務型別，則會包含程式碼、 組態和資料封裝的組成方式。</span><span class="sxs-lookup"><span data-stu-id="a30e3-121">hello following diagram shows how application types are composed of service types, which in turn are composed of code, configuration, and data packages.</span></span> <span data-ttu-id="a30e3-122">toosimplify hello 圖表中，只有 hello 程式碼/config/資料封裝的`ServiceType4`都會顯示，但每個服務類型會包含部分或所有項目套件類型。</span><span class="sxs-lookup"><span data-stu-id="a30e3-122">toosimplify hello diagram, only hello code/config/data packages for `ServiceType4` are shown, though each service type would include some or all those package types.</span></span>

![Service Fabric 應用程式類型和服務類型][cluster-imagestore-apptypes]

<span data-ttu-id="a30e3-124">兩個不同的資訊清單檔案是使用的 toodescribe 應用程式和服務： hello 服務資訊清單和應用程式資訊清單。</span><span class="sxs-lookup"><span data-stu-id="a30e3-124">Two different manifest files are used toodescribe applications and services: hello service manifest and application manifest.</span></span> <span data-ttu-id="a30e3-125">資訊清單會在 hello 下列各節中詳細說明。</span><span class="sxs-lookup"><span data-stu-id="a30e3-125">Manifests are covered in detail in hello following sections.</span></span>

<span data-ttu-id="a30e3-126">可以有一或多個執行個體服務型別的 hello 叢集中使用中。</span><span class="sxs-lookup"><span data-stu-id="a30e3-126">There can be one or more instances of a service type active in hello cluster.</span></span> <span data-ttu-id="a30e3-127">比方說，可設定狀態的服務執行個體或複本，獲得高可靠性位於 hello 叢集中不同節點上的複本之間複寫狀態。</span><span class="sxs-lookup"><span data-stu-id="a30e3-127">For example, stateful service instances, or replicas, achieve high reliability by replicating state between replicas located on different nodes in hello cluster.</span></span> <span data-ttu-id="a30e3-128">複寫實質上提供 hello 服務 toobe 可用的複本，即使在叢集中的一個節點失敗。</span><span class="sxs-lookup"><span data-stu-id="a30e3-128">Replication essentially provides redundancy for hello service toobe available even if one node in a cluster fails.</span></span> <span data-ttu-id="a30e3-129">A[分割服務](service-fabric-concepts-partitioning.md)進一步除以 hello 叢集的節點中其狀態 （和存取模式 toothat 狀態）。</span><span class="sxs-lookup"><span data-stu-id="a30e3-129">A [partitioned service](service-fabric-concepts-partitioning.md) further divides its state (and access patterns toothat state) across nodes in hello cluster.</span></span>

<span data-ttu-id="a30e3-130">hello 下列圖表顯示 hello 應用程式和服務執行個體、 資料分割和複本之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="a30e3-130">hello following diagram shows hello relationship between applications and service instances, partitions, and replicas.</span></span>

![服務內的分割和複本][cluster-application-instances]

> [!TIP]
> <span data-ttu-id="a30e3-132">您可以檢視 hello 版面配置的應用程式中使用 http:// 在 hello Service Fabric 總管工具可用的叢集&lt;yourclusteraddress&gt;: 19080/總管。</span><span class="sxs-lookup"><span data-stu-id="a30e3-132">You can view hello layout of applications in a cluster using hello Service Fabric Explorer tool available at http://&lt;yourclusteraddress&gt;:19080/Explorer.</span></span> <span data-ttu-id="a30e3-133">如需詳細資訊，請參閱[使用 Service Fabric Explorer 視覺化叢集](service-fabric-visualizing-your-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="a30e3-133">For more information, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
> 
> 

## <a name="describe-a-service"></a><span data-ttu-id="a30e3-134">描述服務</span><span class="sxs-lookup"><span data-stu-id="a30e3-134">Describe a service</span></span>
<span data-ttu-id="a30e3-135">hello 服務資訊清單以宣告方式定義 hello 服務類型和版本。</span><span class="sxs-lookup"><span data-stu-id="a30e3-135">hello service manifest declaratively defines hello service type and version.</span></span> <span data-ttu-id="a30e3-136">它會指定如服務類型的服務中繼資料、健康狀態屬性、負載平衡度量、服務二進位檔和組態檔。</span><span class="sxs-lookup"><span data-stu-id="a30e3-136">It specifies service metadata such as service type, health properties, load-balancing metrics, service binaries, and configuration files.</span></span>  <span data-ttu-id="a30e3-137">將另一種方式，描述構成服務封裝 toosupport hello 程式碼、 組態和資料封裝一或多個服務類型。</span><span class="sxs-lookup"><span data-stu-id="a30e3-137">Put another way, it describes hello code, configuration, and data packages that compose a service package toosupport one or more service types.</span></span> <span data-ttu-id="a30e3-138">以下是簡單的範例服務資訊清單：</span><span class="sxs-lookup"><span data-stu-id="a30e3-138">Here is a simple example service manifest:</span></span>

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

<span data-ttu-id="a30e3-139">**版本**屬性為非結構化的字串，且無法剖析 hello 系統。</span><span class="sxs-lookup"><span data-stu-id="a30e3-139">**Version** attributes are unstructured strings and not parsed by hello system.</span></span> <span data-ttu-id="a30e3-140">版本屬性是使用的 tooversion 升級每個元件。</span><span class="sxs-lookup"><span data-stu-id="a30e3-140">Version attributes are used tooversion each component for upgrades.</span></span>

<span data-ttu-id="a30e3-141">**ServiceTypes** 會宣告此資訊清單中 **CodePackages** 支援哪些服務類型。</span><span class="sxs-lookup"><span data-stu-id="a30e3-141">**ServiceTypes** declares what service types are supported by **CodePackages** in this manifest.</span></span> <span data-ttu-id="a30e3-142">當針對其中一種服務類型來具現化服務時，會藉由執行其進入點來啟動此資訊清單中宣告的所有程式碼封裝。</span><span class="sxs-lookup"><span data-stu-id="a30e3-142">When a service is instantiated against one of these service types, all code packages declared in this manifest are activated by running their entry points.</span></span> <span data-ttu-id="a30e3-143">hello 產生處理序在執行階段有預期的 tooregister hello 支援服務型別。</span><span class="sxs-lookup"><span data-stu-id="a30e3-143">hello resulting processes are expected tooregister hello supported service types at run time.</span></span> <span data-ttu-id="a30e3-144">服務類型會宣告 hello 資訊清單的層級和非 hello 程式碼封裝層級。</span><span class="sxs-lookup"><span data-stu-id="a30e3-144">Service types are declared at hello manifest level and not hello code package level.</span></span> <span data-ttu-id="a30e3-145">因此當有多個程式碼封裝，其所有啟動的每當 hello 系統會尋找任何一種 hello 宣告的服務型別。</span><span class="sxs-lookup"><span data-stu-id="a30e3-145">So when there are multiple code packages, they are all activated whenever hello system looks for any one of hello declared service types.</span></span>

<span data-ttu-id="a30e3-146">**SetupEntryPoint**是以 hello 相同認證為 Service Fabric 執行特殊權限的進入點 (通常 hello *LocalSystem*帳戶) 之前的任何其他的進入點。</span><span class="sxs-lookup"><span data-stu-id="a30e3-146">**SetupEntryPoint** is a privileged entry point that runs with hello same credentials as Service Fabric (typically hello *LocalSystem* account) before any other entry point.</span></span> <span data-ttu-id="a30e3-147">hello 可執行檔所指定**EntryPoint**通常是 hello 長時間執行的服務主機。</span><span class="sxs-lookup"><span data-stu-id="a30e3-147">hello executable specified by **EntryPoint** is typically hello long-running service host.</span></span> <span data-ttu-id="a30e3-148">hello 存在的個別安裝進入點可避免使用較高權限 toorun hello 服務主機很長的時間。</span><span class="sxs-lookup"><span data-stu-id="a30e3-148">hello presence of a separate setup entry point avoids having toorun hello service host with high privileges for extended periods of time.</span></span> <span data-ttu-id="a30e3-149">hello 可執行檔所指定**EntryPoint**執行**SetupEntryPoint**成功結束。</span><span class="sxs-lookup"><span data-stu-id="a30e3-149">hello executable specified by **EntryPoint** is run after **SetupEntryPoint** exits successfully.</span></span> <span data-ttu-id="a30e3-150">如果曾 hello 程序會結束，或當機，監視及重新啟動 hello 產生處理序 (開頭為再次**SetupEntryPoint**)。</span><span class="sxs-lookup"><span data-stu-id="a30e3-150">If hello process ever terminates or crashes, hello resulting process is monitored and restarted (beginning again with **SetupEntryPoint**).</span></span>  

<span data-ttu-id="a30e3-151">使用的典型案例**SetupEntryPoint**是當您執行可執行檔 hello 服務啟動前或執行的作業，以提高權限。</span><span class="sxs-lookup"><span data-stu-id="a30e3-151">Typical scenarios for using **SetupEntryPoint** are when you run an executable before hello service starts or you perform an operation with elevated privileges.</span></span> <span data-ttu-id="a30e3-152">例如：</span><span class="sxs-lookup"><span data-stu-id="a30e3-152">For example:</span></span>

* <span data-ttu-id="a30e3-153">設定及初始化 hello 服務可執行檔需要的環境變數。</span><span class="sxs-lookup"><span data-stu-id="a30e3-153">Setting up and initializing environment variables that hello service executable needs.</span></span> <span data-ttu-id="a30e3-154">這不是透過 hello Service Fabric 程式設計模型撰寫有限的 tooonly 可執行檔。</span><span class="sxs-lookup"><span data-stu-id="a30e3-154">This is not limited tooonly executables written via hello Service Fabric programming models.</span></span> <span data-ttu-id="a30e3-155">例如，npm.exe 部署 node.js 應用程式，需要設定某些環境變數。</span><span class="sxs-lookup"><span data-stu-id="a30e3-155">For example, npm.exe needs some environment variables configured for deploying a node.js application.</span></span>
* <span data-ttu-id="a30e3-156">透過安裝安全性憑證設定存取控制。</span><span class="sxs-lookup"><span data-stu-id="a30e3-156">Setting up access control by installing security certificates.</span></span>

<span data-ttu-id="a30e3-157">如需有關如何 tooconfigure hello **SetupEntryPoint**看到[設定服務安裝程式的進入點的 hello 原則](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="a30e3-157">For more details on how tooconfigure hello **SetupEntryPoint** see [Configure hello policy for a service setup entry point](service-fabric-application-runas-security.md)</span></span>

<span data-ttu-id="a30e3-158">**EnvironmentVariables** 提供針對此程式碼封裝設定的環境變數清單。</span><span class="sxs-lookup"><span data-stu-id="a30e3-158">**EnvironmentVariables** provides a list of environment variables that are set for this code package.</span></span> <span data-ttu-id="a30e3-159">Environmentment 變數會覆寫在 hello `ApplicationManifest.xml` tooprovide 不同服務執行個體的值不同。</span><span class="sxs-lookup"><span data-stu-id="a30e3-159">Environmentment variables can be overridden in hello `ApplicationManifest.xml` tooprovide different values for different service instances.</span></span> 

<span data-ttu-id="a30e3-160">**DataPackage**宣告資料夾，名為 hello**名稱**屬性包含任意的靜態資料 toobe hello 程序所耗用在執行階段。</span><span class="sxs-lookup"><span data-stu-id="a30e3-160">**DataPackage** declares a folder, named by hello **Name** attribute, that contains arbitrary static data toobe consumed by hello process at run time.</span></span>

<span data-ttu-id="a30e3-161">**Settings.xml**宣告資料夾，名為 hello**名稱**屬性包含*Settings.xml*檔案。</span><span class="sxs-lookup"><span data-stu-id="a30e3-161">**ConfigPackage** declares a folder, named by hello **Name** attribute, that contains a *Settings.xml* file.</span></span> <span data-ttu-id="a30e3-162">hello 設定檔包含 hello 處理序讀取回執行階段的使用者定義的索引鍵-值組設定的區段。</span><span class="sxs-lookup"><span data-stu-id="a30e3-162">hello settings file contains sections of user-defined, key-value pair settings that hello process reads back at run time.</span></span> <span data-ttu-id="a30e3-163">在升級期間，如果僅 hello **Settings.xml** **版本**已變更，則不會重新啟動 hello 執行程序。</span><span class="sxs-lookup"><span data-stu-id="a30e3-163">During an upgrade, if only hello **ConfigPackage** **version** has changed, then hello running process is not restarted.</span></span> <span data-ttu-id="a30e3-164">相反地，回呼會通知組態設定已變更，因此它們可以重新載入以動態方式的 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="a30e3-164">Instead, a callback notifies hello process that configuration settings have changed so they can be reloaded dynamically.</span></span> <span data-ttu-id="a30e3-165">以下是 *Settings.xml* 檔案的範例：</span><span class="sxs-lookup"><span data-stu-id="a30e3-165">Here is an example *Settings.xml* file:</span></span>

```xml
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MyConfigurationSection">
    <Parameter Name="MySettingA" Value="Example1" />
    <Parameter Name="MySettingB" Value="Example2" />
  </Section>
</Settings>
```

> [!NOTE]
> <span data-ttu-id="a30e3-166">服務資訊清單可以包含多個程式碼、組態和資料封裝。</span><span class="sxs-lookup"><span data-stu-id="a30e3-166">A service manifest can contain multiple code, configuration, and data packages.</span></span> <span data-ttu-id="a30e3-167">每個皆可獨立建立版本。</span><span class="sxs-lookup"><span data-stu-id="a30e3-167">Each of those can be versioned independently.</span></span>
> 
> 

<!--
For more information about other features supported by service manifests, refer toohello following articles:

*TODO: LoadMetrics, PlacementConstraints, ServicePlacementPolicies
*TODO: Resources
*TODO: Health properties
*TODO: Trace filters
*TODO: Configuration overrides
-->

## <a name="describe-an-application"></a><span data-ttu-id="a30e3-168">描述應用程式</span><span class="sxs-lookup"><span data-stu-id="a30e3-168">Describe an application</span></span>
<span data-ttu-id="a30e3-169">hello 應用程式資訊清單以宣告方式描述 hello 應用程式類型和版本。</span><span class="sxs-lookup"><span data-stu-id="a30e3-169">hello application manifest declaratively describes hello application type and version.</span></span> <span data-ttu-id="a30e3-170">它指定服務組成中繼資料，例如穩定的名稱、分割配置、執行個體計數/複寫因數、安全性/隔離原則、安置限制、組態覆寫和組成服務類型。</span><span class="sxs-lookup"><span data-stu-id="a30e3-170">It specifies service composition metadata such as stable names, partitioning scheme, instance count/replication factor, security/isolation policy, placement constraints, configuration overrides, and constituent service types.</span></span> <span data-ttu-id="a30e3-171">hello 應用程式所放置的 hello 負載平衡的網域也將描述。</span><span class="sxs-lookup"><span data-stu-id="a30e3-171">hello load-balancing domains into which hello application is placed are also described.</span></span>

<span data-ttu-id="a30e3-172">因此，應用程式資訊清單描述 hello 應用程式層級的項目，並參照一個或多個服務資訊清單 toocompose 應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="a30e3-172">Thus, an application manifest describes elements at hello application level and references one or more service manifests toocompose an application type.</span></span> <span data-ttu-id="a30e3-173">以下是簡單的範例應用程式資訊清單：</span><span class="sxs-lookup"><span data-stu-id="a30e3-173">Here is a simple example application manifest:</span></span>

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

<span data-ttu-id="a30e3-174">喜歡服務資訊清單、**版本**屬性為非結構化的字串，且不會剖析 hello 系統。</span><span class="sxs-lookup"><span data-stu-id="a30e3-174">Like service manifests, **Version** attributes are unstructured strings and are not parsed by hello system.</span></span> <span data-ttu-id="a30e3-175">版本屬性也會使用的 tooversion 升級每個元件。</span><span class="sxs-lookup"><span data-stu-id="a30e3-175">Version attributes are also used tooversion each component for upgrades.</span></span>

<span data-ttu-id="a30e3-176">**ServiceManifestImport**包含參考 tooservice 資訊清單構成此應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="a30e3-176">**ServiceManifestImport** contains references tooservice manifests that compose this application type.</span></span> <span data-ttu-id="a30e3-177">匯入的服務資訊清單會決定此應用程式類型中哪些服務類型有效。</span><span class="sxs-lookup"><span data-stu-id="a30e3-177">Imported service manifests determine what service types are valid within this application type.</span></span> <span data-ttu-id="a30e3-178">Hello ServiceManifestImport，在您覆寫 ServiceManifest.xml 檔案中的 Settings.xml 和環境變數中的組態值。</span><span class="sxs-lookup"><span data-stu-id="a30e3-178">Within hello ServiceManifestImport, you override configuration values in Settings.xml and environment variables in ServiceManifest.xml files.</span></span> 


<span data-ttu-id="a30e3-179">**DefaultServices** 宣告服務執行個體，該執行個體會在每次應用程式針對此應用程式類型具現化時建立。</span><span class="sxs-lookup"><span data-stu-id="a30e3-179">**DefaultServices** declares service instances that are automatically created whenever an application is instantiated against this application type.</span></span> <span data-ttu-id="a30e3-180">預設服務只是為了方便起見，在建立之後，其行為在每個方面就像正常的服務。</span><span class="sxs-lookup"><span data-stu-id="a30e3-180">Default services are just a convenience and behave like normal services in every respect after they have been created.</span></span> <span data-ttu-id="a30e3-181">它們會連同任何其他服務升級 hello 應用程式執行個體中，會一併移除。</span><span class="sxs-lookup"><span data-stu-id="a30e3-181">They are upgraded along with any other services in hello application instance and can be removed as well.</span></span>

> [!NOTE]
> <span data-ttu-id="a30e3-182">應用程式資訊清單可以包含多個服務資訊清單匯入和預設服務。</span><span class="sxs-lookup"><span data-stu-id="a30e3-182">An application manifest can contain multiple service manifest imports and default services.</span></span> <span data-ttu-id="a30e3-183">每個服務資訊清單匯入都可以獨立建立版本。</span><span class="sxs-lookup"><span data-stu-id="a30e3-183">Each service manifest import can be versioned independently.</span></span>
> 
> 

<span data-ttu-id="a30e3-184">如何 toomaintain 不同的應用程式和服務參數，針對個別的環境，請參閱的 toolearn[管理多個環境的應用程式參數](service-fabric-manage-multiple-environment-app-configuration.md)。</span><span class="sxs-lookup"><span data-stu-id="a30e3-184">toolearn how toomaintain different application and service parameters for individual environments, see [Managing application parameters for multiple environments](service-fabric-manage-multiple-environment-app-configuration.md).</span></span>

<!--
For more information about other features supported by application manifests, refer toohello following articles:

*TODO: Application parameters
*TODO: Security, Principals, RunAs, SecurityAccessPolicy
*TODO: Service Templates
-->



## <a name="next-steps"></a><span data-ttu-id="a30e3-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a30e3-185">Next steps</span></span>
<span data-ttu-id="a30e3-186">[封裝應用程式](service-fabric-package-apps.md)並使其準備 toodeploy。</span><span class="sxs-lookup"><span data-stu-id="a30e3-186">[Package an application](service-fabric-package-apps.md) and make it ready toodeploy.</span></span>

<span data-ttu-id="a30e3-187">[部署和移除應用程式][ 10]描述如何 toouse PowerShell toomanage 應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="a30e3-187">[Deploy and remove applications][10] describes how toouse PowerShell toomanage application instances.</span></span>

<span data-ttu-id="a30e3-188">[管理應用程式參數的多個環境][ 11]描述如何 tooconfigure 參數和環境變數不同的應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="a30e3-188">[Managing application parameters for multiple environments][11] describes how tooconfigure parameters and environment variables for different application instances.</span></span>

<span data-ttu-id="a30e3-189">[設定您的應用程式的安全性原則][ 12]描述 toorun 下安全性原則 toorestrict 存取服務的方式。</span><span class="sxs-lookup"><span data-stu-id="a30e3-189">[Configure security policies for your application][12] describes how toorun services under security policies toorestrict access.</span></span>

<span data-ttu-id="a30e3-190">[應用程式主控模型][13]說明已部署之服務的複本 (或執行個體) 與服務主機處理序之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="a30e3-190">[Application hosting models][13] describe relationship between replicas (or instances) of a deployed service and service-host process.</span></span>

<!--Image references-->
[appmodel-diagram]: ./media/service-fabric-application-model/application-model.png
[cluster-imagestore-apptypes]: ./media/service-fabric-application-model/cluster-imagestore-apptypes.png
[cluster-application-instances]: media/service-fabric-application-model/cluster-application-instances.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
[13]: service-fabric-hosting-model.md
