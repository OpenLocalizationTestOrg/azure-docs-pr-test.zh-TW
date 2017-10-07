---
title: "aaaManage 服務網狀架構中的多個環境 |Microsoft 文件"
description: "Service Fabric 應用程式可以執行的叢集大小介於一個機器 toothousands 的機器。 在某些情況下，您會想 tooconfigure 以不同的方式為這些不同環境的應用程式。 本文件涵蓋如何 toodefine 不同的應用程式參數，每個環境。"
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: f406eac9-7271-4c37-a0d3-0a2957b60537
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: mikkelhegn
ms.openlocfilehash: 2b3327e0e1a3bbd35a50835e720619f308b1b501
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-application-parameters-for-multiple-environments"></a><span data-ttu-id="bb55a-105">管理多個環境的應用程式參數</span><span class="sxs-lookup"><span data-stu-id="bb55a-105">Manage application parameters for multiple environments</span></span>
<span data-ttu-id="bb55a-106">您可以從一個 toomany 千分位機器的任何位置使用，以建立 Azure Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="bb55a-106">You can create Azure Service Fabric clusters by using anywhere from one toomany thousands of machines.</span></span> <span data-ttu-id="bb55a-107">應用程式二進位檔可以透過此各式各樣的環境，必須修改才能執行，而您通常想 tooconfigure hello 應用程式不同，根據您要部署至電腦的 hello 數目而定。</span><span class="sxs-lookup"><span data-stu-id="bb55a-107">While application binaries can run without modification across this wide spectrum of environments, you often want tooconfigure hello application differently, depending on hello number of machines you're deploying to.</span></span>

<span data-ttu-id="bb55a-108">簡單來說，請考慮無狀態服務的 `InstanceCount` 。</span><span class="sxs-lookup"><span data-stu-id="bb55a-108">As a simple example, consider `InstanceCount` for a stateless service.</span></span> <span data-ttu-id="bb55a-109">當您在 Azure 中執行應用程式時，您通常會想 tooset 此參數 toohello 特殊值為"-1"。</span><span class="sxs-lookup"><span data-stu-id="bb55a-109">When you are running applications in Azure, you generally want tooset this parameter toohello special value of "-1".</span></span> <span data-ttu-id="bb55a-110">此組態可確保您的服務 hello 叢集 （或 hello 節點類型，如果您已設定放置條件約束中的每個節點） 中的每個節點上執行。</span><span class="sxs-lookup"><span data-stu-id="bb55a-110">This configuration ensures that your service is running on every node in hello cluster (or every node in hello node type if you have set a placement constraint).</span></span> <span data-ttu-id="bb55a-111">不過，此設定不是適用於單一電腦叢集因為您不能有多個相同接聽 hello 的處理序在單一機器上的端點。</span><span class="sxs-lookup"><span data-stu-id="bb55a-111">However, this configuration is not suitable for a single-machine cluster since you cannot have multiple processes listening on hello same endpoint on a single machine.</span></span> <span data-ttu-id="bb55a-112">相反地，您通常設定`InstanceCount`太"1 的"。</span><span class="sxs-lookup"><span data-stu-id="bb55a-112">Instead, you typically set `InstanceCount` too"1".</span></span>

## <a name="specifying-environment-specific-parameters"></a><span data-ttu-id="bb55a-113">指定環境特有的參數</span><span class="sxs-lookup"><span data-stu-id="bb55a-113">Specifying environment-specific parameters</span></span>
<span data-ttu-id="bb55a-114">hello 方案 toothis 組態問題是一組參數的預設服務和應用程式參數檔案，以填入這些參數的值指定的環境。</span><span class="sxs-lookup"><span data-stu-id="bb55a-114">hello solution toothis configuration issue is a set of parameterized default services and application parameter files that fill in those parameter values for a given environment.</span></span> <span data-ttu-id="bb55a-115">預設的服務和應用程式參數設定於 hello 應用程式，但服務資訊清單。</span><span class="sxs-lookup"><span data-stu-id="bb55a-115">Default services and application parameters are configured in hello application and service manifests.</span></span> <span data-ttu-id="bb55a-116">hello hello ServiceManifest.xml 和 ApplicationManifest.xml 檔案的結構描述定義會隨 hello Service Fabric SDK 和工具太*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="bb55a-116">hello schema definition for hello ServiceManifest.xml and ApplicationManifest.xml files is installed with hello Service Fabric SDK and tools too*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

### <a name="default-services"></a><span data-ttu-id="bb55a-117">預設服務</span><span class="sxs-lookup"><span data-stu-id="bb55a-117">Default services</span></span>
<span data-ttu-id="bb55a-118">Service Fabric 應用程式是由服務執行個體集合所組成。</span><span class="sxs-lookup"><span data-stu-id="bb55a-118">Service Fabric applications are made up of a collection of service instances.</span></span> <span data-ttu-id="bb55a-119">在正在 toocreate 空白的應用程式可能然後動態地建立所有服務執行個體，大部分的應用程式會有一組時，應該一律建立 hello 應用程式具現化的核心服務。</span><span class="sxs-lookup"><span data-stu-id="bb55a-119">While it is possible for you toocreate an empty application and then create all service instances dynamically, most applications have a set of core services that should always be created when hello application is instantiated.</span></span> <span data-ttu-id="bb55a-120">這些是參考的 tooas 「 預設服務 」。</span><span class="sxs-lookup"><span data-stu-id="bb55a-120">These are referred tooas "default services".</span></span> <span data-ttu-id="bb55a-121">指定在 hello 應用程式資訊清單，其中含有包含方括號中的每個環境設定的預留位置：</span><span class="sxs-lookup"><span data-stu-id="bb55a-121">They are specified in hello application manifest, with placeholders for per-environment configuration included in square brackets:</span></span>

```xml
  <DefaultServices>
      <Service Name="Stateful1">
          <StatefulService
              ServiceTypeName="Stateful1Type"
              TargetReplicaSetSize="[Stateful1_TargetReplicaSetSize]"
              MinReplicaSetSize="[Stateful1_MinReplicaSetSize]">

              <UniformInt64Partition
                  PartitionCount="[Stateful1_PartitionCount]"
                  LowKey="-9223372036854775808"
                  HighKey="9223372036854775807"
              />
        </StatefulService>
    </Service>
  </DefaultServices>
```

<span data-ttu-id="bb55a-122">每個具名參數的 hello 必須定義在 hello hello 應用程式資訊清單參數項目：</span><span class="sxs-lookup"><span data-stu-id="bb55a-122">Each of hello named parameters must be defined within hello Parameters element of hello application manifest:</span></span>

```xml
    <Parameters>
        <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
        <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
        <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
    </Parameters>
```

<span data-ttu-id="bb55a-123">hello DefaultValue 屬性指定 hello 值 toobe hello 缺乏更特定參數用於指定的環境。</span><span class="sxs-lookup"><span data-stu-id="bb55a-123">hello DefaultValue attribute specifies hello value toobe used in hello absence of a more-specific parameter for a given environment.</span></span>

> [!NOTE]
> <span data-ttu-id="bb55a-124">並非所有的服務執行個體參數都適用於每個環境組態。</span><span class="sxs-lookup"><span data-stu-id="bb55a-124">Not all service instance parameters are suitable for per-environment configuration.</span></span> <span data-ttu-id="bb55a-125">在 hello 上述範例中，hello LowKey，HighKey hello 服務資料分割配置的值必須明確定義 hello 服務的所有執行個體因為 hello 資料分割範圍是 hello 資料定義域而言不 hello 環境的函式。</span><span class="sxs-lookup"><span data-stu-id="bb55a-125">In hello example above, hello LowKey and HighKey values for hello service's partitioning scheme are explicitly defined for all instances of hello service since hello partition range is a function of hello data domain, not hello environment.</span></span>
> 
> 

### <a name="per-environment-service-configuration-settings"></a><span data-ttu-id="bb55a-126">每個環境的服務組態設定</span><span class="sxs-lookup"><span data-stu-id="bb55a-126">Per-environment service configuration settings</span></span>
<span data-ttu-id="bb55a-127">hello [Service Fabric 應用程式模型](service-fabric-application-model.md)啟用 services tooinclude 設定封裝包含在執行階段可讀取的自訂金鑰-值組。</span><span class="sxs-lookup"><span data-stu-id="bb55a-127">hello [Service Fabric application model](service-fabric-application-model.md) enables services tooinclude configuration packages that contain custom key-value pairs that are readable at run time.</span></span> <span data-ttu-id="bb55a-128">這些設定的 hello 值可以也來區別環境藉由指定`ConfigOverride`hello 應用程式資訊清單中。</span><span class="sxs-lookup"><span data-stu-id="bb55a-128">hello values of these settings can also be differentiated by environment by specifying a `ConfigOverride` in hello application manifest.</span></span>

<span data-ttu-id="bb55a-129">假設您有下列 hello 的 hello Config\Settings.xml 檔案中設定的 hello`Stateful1`服務：</span><span class="sxs-lookup"><span data-stu-id="bb55a-129">Suppose that you have hello following setting in hello Config\Settings.xml file for hello `Stateful1` service:</span></span>

```xml
  <Section Name="MyConfigSection">
     <Parameter Name="MaxQueueSize" Value="25" />
  </Section>
```
<span data-ttu-id="bb55a-130">toooverride 對特定的應用程式環境，這個值建立`ConfigOverride`當您匯入 hello hello 應用程式資訊清單中的服務資訊清單。</span><span class="sxs-lookup"><span data-stu-id="bb55a-130">toooverride this value for a specific application/environment pair, create a `ConfigOverride` when you import hello service manifest in hello application manifest.</span></span>

```xml
  <ConfigOverrides>
     <ConfigOverride Name="Config">
        <Settings>
           <Section Name="MyConfigSection">
              <Parameter Name="MaxQueueSize" Value="[Stateful1_MaxQueueSize]" />
           </Section>
        </Settings>
     </ConfigOverride>
  </ConfigOverrides>
```
<span data-ttu-id="bb55a-131">接著可如上所示，依照環境設定此參數。</span><span class="sxs-lookup"><span data-stu-id="bb55a-131">This parameter can then be configured by environment as shown above.</span></span> <span data-ttu-id="bb55a-132">您可以藉由宣告它 hello 參數 hello 應用程式資訊清單區段中和在 hello 應用程式參數檔案中指定環境特定值。</span><span class="sxs-lookup"><span data-stu-id="bb55a-132">You can do this by declaring it in hello parameters section of hello application manifest and specifying environment-specific values in hello application parameter files.</span></span>

> [!NOTE]
> <span data-ttu-id="bb55a-133">在服務組態設定的 hello 情況下，有三個位置的索引鍵的 hello 值可以設定的位置： hello 服務組態的封裝、 hello 應用程式資訊清單和 hello 應用程式參數檔案。</span><span class="sxs-lookup"><span data-stu-id="bb55a-133">In hello case of service configuration settings, there are three places where hello value of a key can be set: hello service configuration package, hello application manifest, and hello application parameter file.</span></span> <span data-ttu-id="bb55a-134">Service Fabric 會一律選擇 hello 應用程式參數檔案從第一次 （如果有指定），然後 hello 應用程式資訊清單，並最後 hello 組態封裝。</span><span class="sxs-lookup"><span data-stu-id="bb55a-134">Service Fabric will always choose from hello application parameter file first (if specified), then hello application manifest, and finally hello configuration package.</span></span>
> 
> 

### <a name="setting-and-using-environment-variables"></a><span data-ttu-id="bb55a-135">設定及使用環境變數</span><span class="sxs-lookup"><span data-stu-id="bb55a-135">Setting and using environment variables</span></span> 
<span data-ttu-id="bb55a-136">您可以指定和 hello ServiceManifest.xml 檔案中設定環境變數，然後覆寫這些每個執行個體為基礎的 hello ApplicationManifest.xml 檔案中。</span><span class="sxs-lookup"><span data-stu-id="bb55a-136">You can specify and set environment variables in hello ServiceManifest.xml file and then override these in hello ApplicationManifest.xml file on a per instance basis.</span></span>
<span data-ttu-id="bb55a-137">hello 下面範例是兩個環境變數，設定一個值，並會覆寫其他 hello。</span><span class="sxs-lookup"><span data-stu-id="bb55a-137">hello example below shows two environment variables, one with a value set and hello other is overridden.</span></span> <span data-ttu-id="bb55a-138">您可以使用應用程式參數 tooset 環境變數中的值 hello 相同方式，這些已用來設定覆寫。</span><span class="sxs-lookup"><span data-stu-id="bb55a-138">You can use application parameters tooset environment variables values in hello same way that these were used for config overrides.</span></span>

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
<span data-ttu-id="bb55a-139">hello ApplicationManifest.xml 中，參考 hello 程式碼封裝在 hello 與 hello ServiceManifest 中的 toooverride hello 環境變數`EnvironmentOverrides`項目。</span><span class="sxs-lookup"><span data-stu-id="bb55a-139">toooverride hello environment variables in hello ApplicationManifest.xml, reference hello code package in hello ServiceManifest with hello `EnvironmentOverrides` element.</span></span>

```xml
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="FrontEndServicePkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="MyCode">
      <EnvironmentVariable Name="MyEnvVariable" Value="mydata"/>
    </EnvironmentOverrides>
  </ServiceManifestImport>
 ``` 
 <span data-ttu-id="bb55a-140">建立名為服務執行個體的 hello 之後您可以從程式碼存取 hello 環境變數。</span><span class="sxs-lookup"><span data-stu-id="bb55a-140">Once hello named service instance is created you can access hello environment variables from code.</span></span> <span data-ttu-id="bb55a-141">例如在 C# 中，您可以設定下列 hello</span><span class="sxs-lookup"><span data-stu-id="bb55a-141">e.g. In C# you can do hello following</span></span>

```csharp
    string EnvVariable = Environment.GetEnvironmentVariable("MyEnvVariable");
```

### <a name="service-fabric-environment-variables"></a><span data-ttu-id="bb55a-142">Service Fabric 環境變數</span><span class="sxs-lookup"><span data-stu-id="bb55a-142">Service Fabric environment variables</span></span>
<span data-ttu-id="bb55a-143">Service Fabric 具有已針對每個服務執行個體設定的內建環境變數。</span><span class="sxs-lookup"><span data-stu-id="bb55a-143">Service Fabric has built in environment variables set for each service instance.</span></span> <span data-ttu-id="bb55a-144">hello 的環境變數的完整清單是下面其中 hello 粗體會於 hello 是您將使用您的服務，在 hello 其他正在 Service Fabric 執行階段使用。</span><span class="sxs-lookup"><span data-stu-id="bb55a-144">hello full list of environment variables is below, where hello ones in bold are hello ones that you will use in your service, hello other being used by Service Fabric runtime.</span></span> 

* <span data-ttu-id="bb55a-145">Fabric_ApplicationHostId</span><span class="sxs-lookup"><span data-stu-id="bb55a-145">Fabric_ApplicationHostId</span></span>
* <span data-ttu-id="bb55a-146">Fabric_ApplicationHostType</span><span class="sxs-lookup"><span data-stu-id="bb55a-146">Fabric_ApplicationHostType</span></span>
* <span data-ttu-id="bb55a-147">Fabric_ApplicationId</span><span class="sxs-lookup"><span data-stu-id="bb55a-147">Fabric_ApplicationId</span></span>
* <span data-ttu-id="bb55a-148">**Fabric_ApplicationName**</span><span class="sxs-lookup"><span data-stu-id="bb55a-148">**Fabric_ApplicationName**</span></span>
* <span data-ttu-id="bb55a-149">Fabric_CodePackageInstanceId</span><span class="sxs-lookup"><span data-stu-id="bb55a-149">Fabric_CodePackageInstanceId</span></span>
* <span data-ttu-id="bb55a-150">**Fabric_CodePackageName**</span><span class="sxs-lookup"><span data-stu-id="bb55a-150">**Fabric_CodePackageName**</span></span>
* <span data-ttu-id="bb55a-151">**Fabric_Endpoint_[YourServiceName]TypeEndpoint**</span><span class="sxs-lookup"><span data-stu-id="bb55a-151">**Fabric_Endpoint_[YourServiceName]TypeEndpoint**</span></span>
* <span data-ttu-id="bb55a-152">**Fabric_Folder_App_Log**</span><span class="sxs-lookup"><span data-stu-id="bb55a-152">**Fabric_Folder_App_Log**</span></span>
* <span data-ttu-id="bb55a-153">**Fabric_Folder_App_Temp**</span><span class="sxs-lookup"><span data-stu-id="bb55a-153">**Fabric_Folder_App_Temp**</span></span>
* <span data-ttu-id="bb55a-154">**Fabric_Folder_App_Work**</span><span class="sxs-lookup"><span data-stu-id="bb55a-154">**Fabric_Folder_App_Work**</span></span>
* <span data-ttu-id="bb55a-155">**Fabric_Folder_Application**</span><span class="sxs-lookup"><span data-stu-id="bb55a-155">**Fabric_Folder_Application**</span></span>
* <span data-ttu-id="bb55a-156">Fabric_NodeId</span><span class="sxs-lookup"><span data-stu-id="bb55a-156">Fabric_NodeId</span></span>
* <span data-ttu-id="bb55a-157">**Fabric_NodeIPOrFQDN**</span><span class="sxs-lookup"><span data-stu-id="bb55a-157">**Fabric_NodeIPOrFQDN**</span></span>
* <span data-ttu-id="bb55a-158">**Fabric_NodeName**</span><span class="sxs-lookup"><span data-stu-id="bb55a-158">**Fabric_NodeName**</span></span>
* <span data-ttu-id="bb55a-159">Fabric_RuntimeConnectionAddress</span><span class="sxs-lookup"><span data-stu-id="bb55a-159">Fabric_RuntimeConnectionAddress</span></span>
* <span data-ttu-id="bb55a-160">Fabric_ServicePackageInstanceId</span><span class="sxs-lookup"><span data-stu-id="bb55a-160">Fabric_ServicePackageInstanceId</span></span>
* <span data-ttu-id="bb55a-161">Fabric_ServicePackageName</span><span class="sxs-lookup"><span data-stu-id="bb55a-161">Fabric_ServicePackageName</span></span>
* <span data-ttu-id="bb55a-162">Fabric_ServicePackageVersionInstance</span><span class="sxs-lookup"><span data-stu-id="bb55a-162">Fabric_ServicePackageVersionInstance</span></span>
* <span data-ttu-id="bb55a-163">FabricPackageFileName</span><span class="sxs-lookup"><span data-stu-id="bb55a-163">FabricPackageFileName</span></span>

<span data-ttu-id="bb55a-164">hello 程式碼 belows 示範如何 toolist hello Service Fabric 環境變數</span><span class="sxs-lookup"><span data-stu-id="bb55a-164">hello code belows shows how toolist hello Service Fabric environment variables</span></span>
 ```csharp
    foreach (DictionaryEntry de in Environment.GetEnvironmentVariables())
    {
        if (de.Key.ToString().StartsWith("Fabric"))
        {
            Console.WriteLine(" Environment variable {0} = {1}", de.Key, de.Value);
        }
    }
```
<span data-ttu-id="bb55a-165">hello 以下是範例呼叫的應用程式類型的環境變數`GuestExe.Application`與服務類型呼叫`FrontEndService`在本機開發電腦上執行時。</span><span class="sxs-lookup"><span data-stu-id="bb55a-165">hello following are examples of environment variables for an application type called `GuestExe.Application` with a service type called `FrontEndService` when run on your local dev machine.</span></span>

* <span data-ttu-id="bb55a-166">**Fabric_ApplicationName = fabric:/GuestExe.Application**</span><span class="sxs-lookup"><span data-stu-id="bb55a-166">**Fabric_ApplicationName = fabric:/GuestExe.Application**</span></span>
* <span data-ttu-id="bb55a-167">**Fabric_CodePackageName = Code**</span><span class="sxs-lookup"><span data-stu-id="bb55a-167">**Fabric_CodePackageName = Code**</span></span>
* <span data-ttu-id="bb55a-168">**Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**</span><span class="sxs-lookup"><span data-stu-id="bb55a-168">**Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**</span></span>
* <span data-ttu-id="bb55a-169">**Fabric_NodeIPOrFQDN = localhost**</span><span class="sxs-lookup"><span data-stu-id="bb55a-169">**Fabric_NodeIPOrFQDN = localhost**</span></span>
* <span data-ttu-id="bb55a-170">**Fabric_NodeName = _Node_2**</span><span class="sxs-lookup"><span data-stu-id="bb55a-170">**Fabric_NodeName = _Node_2**</span></span>

### <a name="application-parameter-files"></a><span data-ttu-id="bb55a-171">應用程式參數檔案</span><span class="sxs-lookup"><span data-stu-id="bb55a-171">Application parameter files</span></span>
<span data-ttu-id="bb55a-172">hello Service Fabric 應用程式專案可以包含一或多個應用程式參數檔案。</span><span class="sxs-lookup"><span data-stu-id="bb55a-172">hello Service Fabric application project can include one or more application parameter files.</span></span> <span data-ttu-id="bb55a-173">每個定義 hello 特定參數的值 hello hello 應用程式資訊清單中所定義：</span><span class="sxs-lookup"><span data-stu-id="bb55a-173">Each of them defines hello specific values for hello parameters that are defined in hello application manifest:</span></span>

```xml
    <!-- ApplicationParameters\Local.xml -->

    <Application Name="fabric:/Application1" xmlns="http://schemas.microsoft.com/2011/01/fabric">
        <Parameters>
            <Parameter Name ="Stateful1_MinReplicaSetSize" Value="3" />
            <Parameter Name="Stateful1_PartitionCount" Value="1" />
            <Parameter Name="Stateful1_TargetReplicaSetSize" Value="3" />
        </Parameters>
    </Application>
```
<span data-ttu-id="bb55a-174">根據預設，新的應用程式有三個應用程式參數檔案，名稱分別是 Local.1Node.xml、Local.5Node.xml、Cloud.xml：</span><span class="sxs-lookup"><span data-stu-id="bb55a-174">By default, a new application includes three application parameter files, named Local.1Node.xml, Local.5Node.xml, and Cloud.xml:</span></span>

![方案總管中的應用程式參數檔案][app-parameters-solution-explorer]

<span data-ttu-id="bb55a-176">toocreate 參數檔案，只要複製和貼上現有並為它提供新名稱。</span><span class="sxs-lookup"><span data-stu-id="bb55a-176">toocreate a parameter file, simply copy and paste an existing one and give it a new name.</span></span>

## <a name="identifying-environment-specific-parameters-during-deployment"></a><span data-ttu-id="bb55a-177">在部署期間識別環境特有的參數</span><span class="sxs-lookup"><span data-stu-id="bb55a-177">Identifying environment-specific parameters during deployment</span></span>
<span data-ttu-id="bb55a-178">在部署階段，您會需要 toochoose hello 適當的參數檔案 tooapply 與您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="bb55a-178">At deployment time, you need toochoose hello appropriate parameter file tooapply with your application.</span></span> <span data-ttu-id="bb55a-179">您可以透過 Visual Studio 中的 hello 發行對話方塊，或透過 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="bb55a-179">You can do this through hello Publish dialog in Visual Studio or through PowerShell.</span></span>

### <a name="deploy-from-visual-studio"></a><span data-ttu-id="bb55a-180">從 Visual Studio 部署</span><span class="sxs-lookup"><span data-stu-id="bb55a-180">Deploy from Visual Studio</span></span>
<span data-ttu-id="bb55a-181">當您在 Visual Studio 發行您的應用程式時，您可以選擇從 hello 參數可用檔案清單。</span><span class="sxs-lookup"><span data-stu-id="bb55a-181">You can choose from hello list of available parameter files when you publish your application in Visual Studio.</span></span>

![在 hello 發行對話方塊中選擇參數檔案][publishdialog]

### <a name="deploy-from-powershell"></a><span data-ttu-id="bb55a-183">從 PowerShell 部署</span><span class="sxs-lookup"><span data-stu-id="bb55a-183">Deploy from PowerShell</span></span>
<span data-ttu-id="bb55a-184">hello `Deploy-FabricApplication.ps1` hello 應用程式專案範本中所包含的 PowerShell 指令碼接受做為參數的發行設定檔和 hello PublishProfile 包含參考 toohello 應用程式參數檔案。</span><span class="sxs-lookup"><span data-stu-id="bb55a-184">hello `Deploy-FabricApplication.ps1` PowerShell script included in hello application project template accepts a publish profile as a parameter and hello PublishProfile contains a reference toohello application parameters file.</span></span>

  ```PowerShell
    ./Deploy-FabricApplication -ApplicationPackagePath <app_package_path> -PublishProfileFile <publishprofile_path>
  ```

## <a name="next-steps"></a><span data-ttu-id="bb55a-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bb55a-185">Next steps</span></span>
<span data-ttu-id="bb55a-186">toolearn 進一步了解一些 hello 核心概念，本主題中所討論，請參閱 「 hello [Service Fabric 的技術概觀](service-fabric-technical-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="bb55a-186">toolearn more about some of hello core concepts that are discussed in this topic, see hello [Service Fabric technical overview](service-fabric-technical-overview.md).</span></span> <span data-ttu-id="bb55a-187">如需 Visual Studio 中其他可用的應用程式管理功能的相關資訊，請參閱 [在 Visual Studio 中管理 Service Fabric 應用程式](service-fabric-manage-application-in-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="bb55a-187">For information about other app management capabilities that are available in Visual Studio, see [Manage your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span></span>

<!-- Image references -->

[publishdialog]: ./media/service-fabric-manage-multiple-environment-app-configuration/publish-dialog-choose-app-config.png
[app-parameters-solution-explorer]:./media/service-fabric-manage-multiple-environment-app-configuration/app-parameters-in-solution-explorer.png
