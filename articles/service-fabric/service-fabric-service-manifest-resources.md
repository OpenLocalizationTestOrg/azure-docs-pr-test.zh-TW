---
title: "aaaSpecifying Service Fabric 服務端點 |Microsoft 文件"
description: "如何在服務中的 toodescribe endpoint 資源資訊清單，包括如何 tooset 個 HTTPS 端點"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: da36cbdb-6531-4dae-88e8-a311ab71520d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: subramar
ms.openlocfilehash: a4ebee353ce5cf86583673674246094f03f368be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="specify-resources-in-a-service-manifest"></a><span data-ttu-id="04a1f-103">在服務資訊清單中指定資源</span><span class="sxs-lookup"><span data-stu-id="04a1f-103">Specify resources in a service manifest</span></span>
## <a name="overview"></a><span data-ttu-id="04a1f-104">概觀</span><span class="sxs-lookup"><span data-stu-id="04a1f-104">Overview</span></span>
<span data-ttu-id="04a1f-105">hello 服務資訊清單可讓資源所使用的 hello 服務 toobe 宣告/變更，而不需要變更 hello 編譯程式碼。</span><span class="sxs-lookup"><span data-stu-id="04a1f-105">hello service manifest allows resources that are used by hello service toobe declared/changed without changing hello compiled code.</span></span> <span data-ttu-id="04a1f-106">Azure Service Fabric 支援 hello 服務端點的組態。</span><span class="sxs-lookup"><span data-stu-id="04a1f-106">Azure Service Fabric supports configuration of endpoint resources for hello service.</span></span> <span data-ttu-id="04a1f-107">hello 服務資訊清單中指定的 hello toohello 資源可以控制透過 hello SecurityGroup hello 應用程式資訊清單中。</span><span class="sxs-lookup"><span data-stu-id="04a1f-107">hello access toohello resources that are specified in hello service manifest can be controlled via hello SecurityGroup in hello application manifest.</span></span> <span data-ttu-id="04a1f-108">hello 宣告的資源可讓變更在部署階段，這表示 hello 服務不需要新的組態機制 toointroduce 這些資源 toobe。</span><span class="sxs-lookup"><span data-stu-id="04a1f-108">hello declaration of resources allows these resources toobe changed at deployment time, meaning hello service doesn't need toointroduce a new configuration mechanism.</span></span> <span data-ttu-id="04a1f-109">hello 結構描述定義 hello ServiceManifest.xml 檔案會隨 hello Service Fabric SDK 和工具太*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*。</span><span class="sxs-lookup"><span data-stu-id="04a1f-109">hello schema definition for hello ServiceManifest.xml file is installed with hello Service Fabric SDK and tools too*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

## <a name="endpoints"></a><span data-ttu-id="04a1f-110">端點</span><span class="sxs-lookup"><span data-stu-id="04a1f-110">Endpoints</span></span>
<span data-ttu-id="04a1f-111">Hello 服務資訊清單中定義的 endpoint 資源時，Service Fabric 時，指派連接埠從 hello 保留應用程式連接埠範圍未明確指定連接埠。</span><span class="sxs-lookup"><span data-stu-id="04a1f-111">When an endpoint resource is defined in hello service manifest, Service Fabric assigns ports from hello reserved application port range when a port isn't specified explicitly.</span></span> <span data-ttu-id="04a1f-112">例如，查看 hello 端點*ServiceEndpoint1* hello 這個段落後所提供的資訊清單片段中所指定。</span><span class="sxs-lookup"><span data-stu-id="04a1f-112">For example, look at hello endpoint *ServiceEndpoint1* specified in hello manifest snippet provided after this paragraph.</span></span> <span data-ttu-id="04a1f-113">此外，服務也可以在資源中要求特定連接埠。</span><span class="sxs-lookup"><span data-stu-id="04a1f-113">Additionally, services can also request a specific port in a resource.</span></span> <span data-ttu-id="04a1f-114">複本上執行之服務的 hello 相同的節點共用 hello 連接埠時，在不同的叢集節點上執行的服務複本可以指派不同的通訊埠編號。</span><span class="sxs-lookup"><span data-stu-id="04a1f-114">Service replicas running on different cluster nodes can be assigned different port numbers, while replicas of a service running on hello same node share hello port.</span></span> <span data-ttu-id="04a1f-115">hello 服務複本可以再使用這些連接埠需要複寫與接聽用戶端要求。</span><span class="sxs-lookup"><span data-stu-id="04a1f-115">hello service replicas can then use these ports as needed for replication and listening for client requests.</span></span>

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
    <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
    <Endpoint Name="ServiceEndpoint3" Protocol="https"/>
  </Endpoints>
</Resources>
```

<span data-ttu-id="04a1f-116">參照太[設定可設定狀態的可靠服務](service-fabric-reliable-services-configuration.md)tooread 更多關於 hello 組態封裝的設定檔 (settings.xml) 從參考的端點。</span><span class="sxs-lookup"><span data-stu-id="04a1f-116">Refer too[Configuring stateful Reliable Services](service-fabric-reliable-services-configuration.md) tooread more about referencing endpoints from hello config package settings file (settings.xml).</span></span>

## <a name="example-specifying-an-http-endpoint-for-your-service"></a><span data-ttu-id="04a1f-117">範例：指定服務的 HTTP 端點</span><span class="sxs-lookup"><span data-stu-id="04a1f-117">Example: specifying an HTTP endpoint for your service</span></span>
<span data-ttu-id="04a1f-118">hello 下列服務資訊清單中，定義一個 TCP 端點資源以及兩個 HTTP 端點資源 hello&lt;資源&gt;項目。</span><span class="sxs-lookup"><span data-stu-id="04a1f-118">hello following service manifest defines one TCP endpoint resource and two HTTP endpoint resources in hello &lt;Resources&gt; element.</span></span>

<span data-ttu-id="04a1f-119">Service Fabric 會自動將 HTTP 端點處理為 ACL。</span><span class="sxs-lookup"><span data-stu-id="04a1f-119">HTTP endpoints are automatically ACL'd by Service Fabric.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="Stateful1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         This name must match hello string used in hello RegisterServiceType call in Program.cs. -->
    <StatefulServiceType ServiceTypeName="Stateful1Type" HasPersistedState="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <ExeHost>
        <Program>Stateful1.exe</Program>
      </ExeHost>
    </EntryPoint>
  </CodePackage>

  <!-- Config package is hello contents of hello Config directoy under PackageRoot that contains an
       independently updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port number on which to
           listen. Note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
      <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
      <Endpoint Name="ServiceEndpoint3" Protocol="https"/>

      <!-- This endpoint is used by hello replicator for replicating hello state of your service.
           This endpoint is configured through hello ReplicatorSettings config section in hello Settings.xml
           file under hello ConfigPackage. -->
      <Endpoint Name="ReplicatorEndpoint" />
    </Endpoints>
  </Resources>
</ServiceManifest>
```

## <a name="example-specifying-an-https-endpoint-for-your-service"></a><span data-ttu-id="04a1f-120">範例：指定服務的 HTTPS 端點</span><span class="sxs-lookup"><span data-stu-id="04a1f-120">Example: specifying an HTTPS endpoint for your service</span></span>
<span data-ttu-id="04a1f-121">hello HTTPS 通訊協定提供伺服器驗證，而且也用來加密用戶端伺服器通訊。</span><span class="sxs-lookup"><span data-stu-id="04a1f-121">hello HTTPS protocol provides server authentication and is also used for encrypting client-server communication.</span></span> <span data-ttu-id="04a1f-122">您的 Service Fabric 服務 tooenable HTTPS 指定 hello 通訊協定在 hello*資源]-> [端點]-> [端點*hello 服務資訊清單，如先前所示為 hello 端點區段*ServiceEndpoint3*.</span><span class="sxs-lookup"><span data-stu-id="04a1f-122">tooenable HTTPS on your Service Fabric service, specify hello protocol in hello *Resources -> Endpoints -> Endpoint* section of hello service manifest, as shown earlier for hello endpoint *ServiceEndpoint3*.</span></span>

> [!NOTE]
> <span data-ttu-id="04a1f-123">服務的通訊協定不能在應用程式升級期間變更。</span><span class="sxs-lookup"><span data-stu-id="04a1f-123">A service’s protocol cannot be changed during application upgrade.</span></span> <span data-ttu-id="04a1f-124">如果它在升級期間變更，將會發生中斷變更。</span><span class="sxs-lookup"><span data-stu-id="04a1f-124">If it is changed during upgrade, it is a breaking change.</span></span>
> 
> 

<span data-ttu-id="04a1f-125">以下是您需要 HTTPS tooset 範例 Secretscertificate。</span><span class="sxs-lookup"><span data-stu-id="04a1f-125">Here is an example ApplicationManifest that you need tooset for HTTPS.</span></span> <span data-ttu-id="04a1f-126">必須提供您的憑證指紋 hello。</span><span class="sxs-lookup"><span data-stu-id="04a1f-126">hello thumbprint for your certificate must be provided.</span></span> <span data-ttu-id="04a1f-127">hello EndpointRef 是的 ServiceManifest，您將設定 hello HTTPS 通訊協定中參考 tooEndpointResource。</span><span class="sxs-lookup"><span data-stu-id="04a1f-127">hello EndpointRef is a reference tooEndpointResource in ServiceManifest, for which you set hello HTTPS protocol.</span></span> <span data-ttu-id="04a1f-128">您可以加入一個以上的 EndpointCertificate。</span><span class="sxs-lookup"><span data-stu-id="04a1f-128">You can add more than one EndpointCertificate.</span></span>  

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="Application1Type"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Parameters>
    <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
    <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
    <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
  </Parameters>
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion
       should match hello Name and Version attributes of hello ServiceManifest element defined in the
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateful1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <Policies>
      <EndpointBindingPolicy CertificateRef="TestCert1" EndpointRef="ServiceEndpoint3"/>
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types when an instance of this
         application type is created. You can also create one or more instances of service type by using the
         Service Fabric PowerShell module.

         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="Stateful1">
      <StatefulService ServiceTypeName="Stateful1Type" TargetReplicaSetSize="[Stateful1_TargetReplicaSetSize]" MinReplicaSetSize="[Stateful1_ ]">
        <UniformInt64Partition PartitionCount="[Stateful1_PartitionCount]" LowKey="-9223372036854775808" HighKey="9223372036854775807" />
      </StatefulService>
    </Service>
  </DefaultServices>
  <Certificates>
    <EndpointCertificate Name="TestCert1" X509FindValue="FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF F0" X509StoreName="MY" />  
  </Certificates>
</ApplicationManifest>
```

## <a name="overriding-endpoints-in-servicemanifestxml"></a><span data-ttu-id="04a1f-129">在 ServiceManifest.xml 中覆寫端點</span><span class="sxs-lookup"><span data-stu-id="04a1f-129">Overriding Endpoints in ServiceManifest.xml</span></span>

<span data-ttu-id="04a1f-130">在 hello Secretscertificate 新增 ResourceOverrides 區段，則為同層級 tooConfigOverrides > 一節。</span><span class="sxs-lookup"><span data-stu-id="04a1f-130">In hello ApplicationManifest add a ResourceOverrides section which will be a sibling tooConfigOverrides section.</span></span> <span data-ttu-id="04a1f-131">在本節中，您可以指定 hello hello hello 服務資訊清單中指定的資源區段中的 hello 端點區段的覆寫。</span><span class="sxs-lookup"><span data-stu-id="04a1f-131">In this section you can specify hello override for hello Endpoints section in hello resources section specified in hello Service manifest.</span></span>

<span data-ttu-id="04a1f-132">順序 toooverride 使用 ApplicationParameters 變更 ServiceManifest 中的端點在 hello Secretscertificate 如下所示：</span><span class="sxs-lookup"><span data-stu-id="04a1f-132">In order toooverride EndPoint in ServiceManifest using ApplicationParameters change hello ApplicationManifest as following:</span></span>

<span data-ttu-id="04a1f-133">Hello ServiceManifestImport > 一節中加入新的區段"ResourceOverrides"</span><span class="sxs-lookup"><span data-stu-id="04a1f-133">In hello ServiceManifestImport section add a new section "ResourceOverrides"</span></span>

```xml
<ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateless1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <ResourceOverrides>
      <Endpoints>
        <Endpoint Name="ServiceEndpoint" Port="[Port]" Protocol="[Protocol]" Type="[Type]" />
        <Endpoint Name="ServiceEndpoint1" Port="[Port1]" Protocol="[Protocol1] "/>
      </Endpoints>
    </ResourceOverrides>
        <Policies>
           <EndpointBindingPolicy CertificateRef="TestCert1" EndpointRef="ServiceEndpoint"/>
        </Policies>
  </ServiceManifestImport>
```

<span data-ttu-id="04a1f-134">在 hello 下新增參數：</span><span class="sxs-lookup"><span data-stu-id="04a1f-134">In hello Parameters add below:</span></span>

```xml
  <Parameters>
    <Parameter Name="Port" DefaultValue="" />
    <Parameter Name="Protocol" DefaultValue="" />
    <Parameter Name="Type" DefaultValue="" />
    <Parameter Name="Port1" DefaultValue="" />
    <Parameter Name="Protocol1" DefaultValue="" />
  </Parameters>
```

<span data-ttu-id="04a1f-135">部署現在 hello 應用程式時您可以傳遞這些值為 ApplicationParameters 例如：</span><span class="sxs-lookup"><span data-stu-id="04a1f-135">While deploying hello application now you can pass in these values as ApplicationParameters for example:</span></span>

```powershell
PS C:\> New-ServiceFabricApplication -ApplicationName fabric:/myapp -ApplicationTypeName "AppType" -ApplicationTypeVersion "1.0.0" -ApplicationParameter @{Port='1001'; Protocol='https'; Type='Input'; Port1='2001'; Protocol='http'}
```

<span data-ttu-id="04a1f-136">注意： 如果 hello 值提供是空的 hello ApplicationParameters 我們移回 toohello 預設對應 EndPointName hello ServiceManifest 中提供的值。</span><span class="sxs-lookup"><span data-stu-id="04a1f-136">Note: If hello values provide for hello ApplicationParameters is empty we go back toohello default value provided in hello ServiceManifest for hello corresponding EndPointName.</span></span>

<span data-ttu-id="04a1f-137">例如：</span><span class="sxs-lookup"><span data-stu-id="04a1f-137">For example:</span></span>

<span data-ttu-id="04a1f-138">如果在您指定的 ServiceManifest hello</span><span class="sxs-lookup"><span data-stu-id="04a1f-138">If in hello ServiceManifest you specified</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Name="ServiceEndpoint1" Protocol="tcp"/>
    </Endpoints>
  </Resources>
```

<span data-ttu-id="04a1f-139">Hello Port1 和 Protocol1 應用程式參數的值是 null 或空白。</span><span class="sxs-lookup"><span data-stu-id="04a1f-139">And hello Port1 and Protocol1 value for Application parameters is null or empty.</span></span> <span data-ttu-id="04a1f-140">仍由 ServiceFabric 決定 hello 連接埠。</span><span class="sxs-lookup"><span data-stu-id="04a1f-140">hello port is still decided by ServiceFabric.</span></span> <span data-ttu-id="04a1f-141">而且 hello 通訊協定將 tcp。</span><span class="sxs-lookup"><span data-stu-id="04a1f-141">And hello Protocol will tcp.</span></span>

<span data-ttu-id="04a1f-142">假設您指定錯誤的值。</span><span class="sxs-lookup"><span data-stu-id="04a1f-142">Suppose you specify a wrong value.</span></span> <span data-ttu-id="04a1f-143">類似於您指定的字串值 "Foo" 而非 int 的連接埠。新 ServiceFabricApplication 命令將會失敗，發生錯誤： 在區段 'ResourceOverrides' name 'ServiceEndpoint1' 屬性 'Port1' hello 覆寫參數無效。</span><span class="sxs-lookup"><span data-stu-id="04a1f-143">Like for Port you specified a string value "Foo" instead of an int.  New-ServiceFabricApplication command will fail with an error : hello override parameter with name 'ServiceEndpoint1' attribute 'Port1' in section 'ResourceOverrides' is invalid.</span></span> <span data-ttu-id="04a1f-144">指定的 hello 值是 'Foo'，且必須是 'int'。</span><span class="sxs-lookup"><span data-stu-id="04a1f-144">hello value specified is 'Foo' and required is 'int'.</span></span>
