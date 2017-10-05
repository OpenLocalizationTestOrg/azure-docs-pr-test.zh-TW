---
title: "指定 Service Fabric 服務端點 | Microsoft Docs"
description: "如何在服務資訊清單中描述端點資源，包括如何設定 HTTPS 端點"
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
ms.openlocfilehash: 08141edfbc8be9bf7bf303419e1e482d5f884860
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="specify-resources-in-a-service-manifest"></a><span data-ttu-id="2e9bb-103">在服務資訊清單中指定資源</span><span class="sxs-lookup"><span data-stu-id="2e9bb-103">Specify resources in a service manifest</span></span>
## <a name="overview"></a><span data-ttu-id="2e9bb-104">Overview</span><span class="sxs-lookup"><span data-stu-id="2e9bb-104">Overview</span></span>
<span data-ttu-id="2e9bb-105">服務資訊清單可宣告/變更服務使用的資源，且不需變更已編譯的程式碼。</span><span class="sxs-lookup"><span data-stu-id="2e9bb-105">The service manifest allows resources that are used by the service to be declared/changed without changing the compiled code.</span></span> <span data-ttu-id="2e9bb-106">Azure Service Fabric 支援針對服務的端點資源組態。</span><span class="sxs-lookup"><span data-stu-id="2e9bb-106">Azure Service Fabric supports configuration of endpoint resources for the service.</span></span> <span data-ttu-id="2e9bb-107">透過應用程式資訊清單中的 SecurityGroup，即可控制存取服務資訊清單中的指定資源。</span><span class="sxs-lookup"><span data-stu-id="2e9bb-107">The access to the resources that are specified in the service manifest can be controlled via the SecurityGroup in the application manifest.</span></span> <span data-ttu-id="2e9bb-108">資源宣告可讓您在部署階段變更這些資源，也就是服務不需要導入新的組態機制。</span><span class="sxs-lookup"><span data-stu-id="2e9bb-108">The declaration of resources allows these resources to be changed at deployment time, meaning the service doesn't need to introduce a new configuration mechanism.</span></span> <span data-ttu-id="2e9bb-109">ServiceManifest.xml 檔案的結構描述定義是和 Service Fabric SDK 及工具一起安裝在 *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*。</span><span class="sxs-lookup"><span data-stu-id="2e9bb-109">The schema definition for the ServiceManifest.xml file is installed with the Service Fabric SDK and tools to *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

## <a name="endpoints"></a><span data-ttu-id="2e9bb-110">端點</span><span class="sxs-lookup"><span data-stu-id="2e9bb-110">Endpoints</span></span>
<span data-ttu-id="2e9bb-111">在服務資訊清單中定義端點資源時，若沒有明確指定連接埠，Service Fabric 會從保留的應用程式連接埠範圍指派連接埠。</span><span class="sxs-lookup"><span data-stu-id="2e9bb-111">When an endpoint resource is defined in the service manifest, Service Fabric assigns ports from the reserved application port range when a port isn't specified explicitly.</span></span> <span data-ttu-id="2e9bb-112">例如，請看本段落之後提供的資訊清單片段中所指定的端點 *ServiceEndpoint1* 。</span><span class="sxs-lookup"><span data-stu-id="2e9bb-112">For example, look at the endpoint *ServiceEndpoint1* specified in the manifest snippet provided after this paragraph.</span></span> <span data-ttu-id="2e9bb-113">此外，服務也可以在資源中要求特定連接埠。</span><span class="sxs-lookup"><span data-stu-id="2e9bb-113">Additionally, services can also request a specific port in a resource.</span></span> <span data-ttu-id="2e9bb-114">不同的連接埠號碼可以指派給在不同叢集節點上執行的服務複本，而在同一節點上執行的服務複本可以共用連接埠。</span><span class="sxs-lookup"><span data-stu-id="2e9bb-114">Service replicas running on different cluster nodes can be assigned different port numbers, while replicas of a service running on the same node share the port.</span></span> <span data-ttu-id="2e9bb-115">然後服務複本就可以在需要時使用這些連接埠進行複寫和接聽用戶端要求。</span><span class="sxs-lookup"><span data-stu-id="2e9bb-115">The service replicas can then use these ports as needed for replication and listening for client requests.</span></span>

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
    <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
    <Endpoint Name="ServiceEndpoint3" Protocol="https"/>
  </Endpoints>
</Resources>
```

<span data-ttu-id="2e9bb-116">請參閱 [設定具狀態的 Reliable Services](service-fabric-reliable-services-configuration.md) ，從設定封裝設定檔 (settings.xml) 深入了解參考端點。</span><span class="sxs-lookup"><span data-stu-id="2e9bb-116">Refer to [Configuring stateful Reliable Services](service-fabric-reliable-services-configuration.md) to read more about referencing endpoints from the config package settings file (settings.xml).</span></span>

## <a name="example-specifying-an-http-endpoint-for-your-service"></a><span data-ttu-id="2e9bb-117">範例：指定服務的 HTTP 端點</span><span class="sxs-lookup"><span data-stu-id="2e9bb-117">Example: specifying an HTTP endpoint for your service</span></span>
<span data-ttu-id="2e9bb-118">以下服務資訊清單在 &lt;Resources&gt; 項目中定義了一個 TCP 端點資源和兩個 HTTP 端點資源。</span><span class="sxs-lookup"><span data-stu-id="2e9bb-118">The following service manifest defines one TCP endpoint resource and two HTTP endpoint resources in the &lt;Resources&gt; element.</span></span>

<span data-ttu-id="2e9bb-119">Service Fabric 會自動將 HTTP 端點處理為 ACL。</span><span class="sxs-lookup"><span data-stu-id="2e9bb-119">HTTP endpoints are automatically ACL'd by Service Fabric.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="Stateful1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is the name of your ServiceType.
         This name must match the string used in the RegisterServiceType call in Program.cs. -->
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

  <!-- Config package is the contents of the Config directoy under PackageRoot that contains an
       independently updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by the communication listener to obtain the port number on which to
           listen. Note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
      <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
      <Endpoint Name="ServiceEndpoint3" Protocol="https"/>

      <!-- This endpoint is used by the replicator for replicating the state of your service.
           This endpoint is configured through the ReplicatorSettings config section in the Settings.xml
           file under the ConfigPackage. -->
      <Endpoint Name="ReplicatorEndpoint" />
    </Endpoints>
  </Resources>
</ServiceManifest>
```

## <a name="example-specifying-an-https-endpoint-for-your-service"></a><span data-ttu-id="2e9bb-120">範例：指定服務的 HTTPS 端點</span><span class="sxs-lookup"><span data-stu-id="2e9bb-120">Example: specifying an HTTPS endpoint for your service</span></span>
<span data-ttu-id="2e9bb-121">HTTPS 通訊協定提供伺服器驗證，也能用於加密用戶端-伺服器通訊。</span><span class="sxs-lookup"><span data-stu-id="2e9bb-121">The HTTPS protocol provides server authentication and is also used for encrypting client-server communication.</span></span> <span data-ttu-id="2e9bb-122">若要在 Service Fabric 服務上啟用 HTTPS，請在服務資訊清單的 [資源] -> [端點] -> [端點] 區段指定通訊協定，如先前針對 *ServiceEndpoint3* 端點所示。</span><span class="sxs-lookup"><span data-stu-id="2e9bb-122">To enable HTTPS on your Service Fabric service, specify the protocol in the *Resources -> Endpoints -> Endpoint* section of the service manifest, as shown earlier for the endpoint *ServiceEndpoint3*.</span></span>

> [!NOTE]
> <span data-ttu-id="2e9bb-123">服務的通訊協定不能在應用程式升級期間變更。</span><span class="sxs-lookup"><span data-stu-id="2e9bb-123">A service’s protocol cannot be changed during application upgrade.</span></span> <span data-ttu-id="2e9bb-124">如果它在升級期間變更，將會發生中斷變更。</span><span class="sxs-lookup"><span data-stu-id="2e9bb-124">If it is changed during upgrade, it is a breaking change.</span></span>
> 
> 

<span data-ttu-id="2e9bb-125">以下是您必須為 HTTPS 設定的範例 ApplicationManifest。</span><span class="sxs-lookup"><span data-stu-id="2e9bb-125">Here is an example ApplicationManifest that you need to set for HTTPS.</span></span> <span data-ttu-id="2e9bb-126">您必須提供憑證的指紋。</span><span class="sxs-lookup"><span data-stu-id="2e9bb-126">The thumbprint for your certificate must be provided.</span></span> <span data-ttu-id="2e9bb-127">EndpointRef 是在您設定 HTTPS 通訊協定的 ServiceManifest 中 EndpointResource 的參考。</span><span class="sxs-lookup"><span data-stu-id="2e9bb-127">The EndpointRef is a reference to EndpointResource in ServiceManifest, for which you set the HTTPS protocol.</span></span> <span data-ttu-id="2e9bb-128">您可以加入一個以上的 EndpointCertificate。</span><span class="sxs-lookup"><span data-stu-id="2e9bb-128">You can add more than one EndpointCertificate.</span></span>  

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
  <!-- Import the ServiceManifest from the ServicePackage. The ServiceManifestName and ServiceManifestVersion
       should match the Name and Version attributes of the ServiceManifest element defined in the
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateful1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <Policies>
      <EndpointBindingPolicy CertificateRef="TestCert1" EndpointRef="ServiceEndpoint3"/>
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- The section below creates instances of service types when an instance of this
         application type is created. You can also create one or more instances of service type by using the
         Service Fabric PowerShell module.

         The attribute ServiceTypeName below must match the name defined in the imported ServiceManifest.xml file. -->
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

## <a name="overriding-endpoints-in-servicemanifestxml"></a><span data-ttu-id="2e9bb-129">在 ServiceManifest.xml 中覆寫端點</span><span class="sxs-lookup"><span data-stu-id="2e9bb-129">Overriding Endpoints in ServiceManifest.xml</span></span>

<span data-ttu-id="2e9bb-130">在 ApplicationManifest 中，新增 ResourceOverrides 區段，可成為 ConfigOverrides 區段的同層級。</span><span class="sxs-lookup"><span data-stu-id="2e9bb-130">In the ApplicationManifest add a ResourceOverrides section which will be a sibling to ConfigOverrides section.</span></span> <span data-ttu-id="2e9bb-131">在本節中，您可以在服務資訊清單中指定的資源區段中指定 [端點] 區段的覆寫。</span><span class="sxs-lookup"><span data-stu-id="2e9bb-131">In this section you can specify the override for the Endpoints section in the resources section specified in the Service manifest.</span></span>

<span data-ttu-id="2e9bb-132">若要使用 ApplicationParameters 覆寫 ServiceManifest 中的端點，請變更 Secretscertificate，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2e9bb-132">In order to override EndPoint in ServiceManifest using ApplicationParameters change the ApplicationManifest as following:</span></span>

<span data-ttu-id="2e9bb-133">在 ServiceManifestImport 區段中，新增新的區段 "ResourceOverrides"</span><span class="sxs-lookup"><span data-stu-id="2e9bb-133">In the ServiceManifestImport section add a new section "ResourceOverrides"</span></span>

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

<span data-ttu-id="2e9bb-134">在參數中新增下列項目：</span><span class="sxs-lookup"><span data-stu-id="2e9bb-134">In the Parameters add below:</span></span>

```xml
  <Parameters>
    <Parameter Name="Port" DefaultValue="" />
    <Parameter Name="Protocol" DefaultValue="" />
    <Parameter Name="Type" DefaultValue="" />
    <Parameter Name="Port1" DefaultValue="" />
    <Parameter Name="Protocol1" DefaultValue="" />
  </Parameters>
```

<span data-ttu-id="2e9bb-135">部署應用程式時，現在您可以傳入這些值作為 ApplicationParameters，例如：</span><span class="sxs-lookup"><span data-stu-id="2e9bb-135">While deploying the application now you can pass in these values as ApplicationParameters for example:</span></span>

```powershell
PS C:\> New-ServiceFabricApplication -ApplicationName fabric:/myapp -ApplicationTypeName "AppType" -ApplicationTypeVersion "1.0.0" -ApplicationParameter @{Port='1001'; Protocol='https'; Type='Input'; Port1='2001'; Protocol='http'}
```

<span data-ttu-id="2e9bb-136">注意：如果提供給 ApplicationParameters 的值為空白，我們要回到 ServiceManifest 中提供的預設值，來取得對應的 EndPointName。</span><span class="sxs-lookup"><span data-stu-id="2e9bb-136">Note: If the values provide for the ApplicationParameters is empty we go back to the default value provided in the ServiceManifest for the corresponding EndPointName.</span></span>

<span data-ttu-id="2e9bb-137">例如：</span><span class="sxs-lookup"><span data-stu-id="2e9bb-137">For example:</span></span>

<span data-ttu-id="2e9bb-138">如果在您指定的 ServiceManifest 中</span><span class="sxs-lookup"><span data-stu-id="2e9bb-138">If in the ServiceManifest you specified</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Name="ServiceEndpoint1" Protocol="tcp"/>
    </Endpoints>
  </Resources>
```

<span data-ttu-id="2e9bb-139">且應用程式參數的 Port1 和 Protocol1 值是 Null 或空白。</span><span class="sxs-lookup"><span data-stu-id="2e9bb-139">And the Port1 and Protocol1 value for Application parameters is null or empty.</span></span> <span data-ttu-id="2e9bb-140">連接埠仍是由 ServiceFabric 決定。</span><span class="sxs-lookup"><span data-stu-id="2e9bb-140">The port is still decided by ServiceFabric.</span></span> <span data-ttu-id="2e9bb-141">且通訊協定將 tcp。</span><span class="sxs-lookup"><span data-stu-id="2e9bb-141">And the Protocol will tcp.</span></span>

<span data-ttu-id="2e9bb-142">假設您指定錯誤的值。</span><span class="sxs-lookup"><span data-stu-id="2e9bb-142">Suppose you specify a wrong value.</span></span> <span data-ttu-id="2e9bb-143">類似於您指定的字串值 "Foo" 而非 int 的連接埠。New-ServiceFabricApplication 命令將會失敗，並出現錯誤：在區段 'ResourceOverrides' 中名稱為 'ServiceEndpoint1' 屬性 'Port1' 的覆寫參數無效。</span><span class="sxs-lookup"><span data-stu-id="2e9bb-143">Like for Port you specified a string value "Foo" instead of an int.  New-ServiceFabricApplication command will fail with an error : The override parameter with name 'ServiceEndpoint1' attribute 'Port1' in section 'ResourceOverrides' is invalid.</span></span> <span data-ttu-id="2e9bb-144">指定的值是 'Foo'，而所需為 'int'。</span><span class="sxs-lookup"><span data-stu-id="2e9bb-144">The value specified is 'Foo' and required is 'int'.</span></span>
