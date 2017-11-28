---
title: "Azure Service Fabric Docker Compose 預覽 | Microsoft Docs"
description: "Azure Service Fabric 接受 Docker Compose 格式，讓您能更輕鬆地使用 Service Fabric 協調現有容器。 這項支援目前只能預覽。"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: b12ef95add6347621f7d4865fac46568f91a1e12
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="specifying-volume-plugins-and-logging-drivers-for-your-container"></a><span data-ttu-id="ba6b8-104">指定容器的磁碟區外掛程式和記錄驅動程式</span><span class="sxs-lookup"><span data-stu-id="ba6b8-104">Specifying volume plugins and logging drivers for your container</span></span>

<span data-ttu-id="ba6b8-105">Service Fabric 支援為容器服務指定 [Docker 磁碟區外掛程式](https://docs.docker.com/engine/extend/plugins_volume/)和 [Docker 記錄驅動程式](https://docs.docker.com/engine/admin/logging/overview/)。</span><span class="sxs-lookup"><span data-stu-id="ba6b8-105">Service Fabric supports specifying [Docker volume plugins](https://docs.docker.com/engine/extend/plugins_volume/) and [Docker logging drivers](https://docs.docker.com/engine/admin/logging/overview/) for your container service.</span></span> <span data-ttu-id="ba6b8-106">外掛程式是在應用程式資訊清單中指定，如下列資訊清單中所示：</span><span class="sxs-lookup"><span data-stu-id="ba6b8-106">The plugins are specified in the application manifest as shown in the following manifest:</span></span>


```xml
?xml version="1.0" encoding="UTF-8"?>
<ApplicationManifest ApplicationTypeName="WinNodeJsApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <Description>Calculator Application</Description>
    <Parameters>
        <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
      <Parameter Name="MyCpuShares" DefaultValue="3"></Parameter>
    </Parameters>
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="NodeServicePackage" ServiceManifestVersion="1.0"/>
     <Policies>
       <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv"> 
        <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
        <RepositoryCredentials PasswordEncrypted="false" Password="****" AccountName="test"/>
        <LogConfig Driver="etwlogs" >
          <DriverOption Name="test" Value="vale"/>
        </LogConfig>
        <Volume Source="c:\workspace" Destination="c:\testmountlocation1" IsReadOnly="false"></Volume>
        <Volume Source="d:\myfolder" Destination="c:\testmountlocation2" IsReadOnly="true"> </Volume>
        <Volume Source="myexternalvolume" Destination="c:\testmountlocation3" Driver="sf" IsReadOnly="true"></Volume>
       </ContainerHostPolicies>
   </Policies>
    </ServiceManifestImport>
    <ServiceTemplates>
        <StatelessService ServiceTypeName="StatelessNodeService" InstanceCount="5">
            <SingletonPartition></SingletonPartition>
        </StatelessService>
    </ServiceTemplates>
</ApplicationManifest>
```

<span data-ttu-id="ba6b8-107">在上述範例中，`Volume` 的 `Source` 標記指的是來源資料夾。</span><span class="sxs-lookup"><span data-stu-id="ba6b8-107">In the preceding example, the `Source` tag for the `Volume` refers to the source folder.</span></span> <span data-ttu-id="ba6b8-108">來源資料夾可以是裝載容器或持續性遠端存放區的 VM 中的資料夾。</span><span class="sxs-lookup"><span data-stu-id="ba6b8-108">The source folder could be a folder in the VM that hosts the containers or a persistent remote store.</span></span> <span data-ttu-id="ba6b8-109">`Destination` 標記是 `Source` 在執行容器內所對應的位置。</span><span class="sxs-lookup"><span data-stu-id="ba6b8-109">The `Destination` tag is the location that the `Source` is mapped to within the running container.</span></span> 

<span data-ttu-id="ba6b8-110">指定磁碟區外掛程式時，Service Fabric 會使用指定的參數自動建立磁碟區。</span><span class="sxs-lookup"><span data-stu-id="ba6b8-110">When specifying a volume plugin, Service Fabric automatically creates the volume using the parameters specified.</span></span> <span data-ttu-id="ba6b8-111">`Source` 標記是磁碟區的名稱，而 `Driver` 標記會指定磁碟區驅動程式的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="ba6b8-111">The `Source` tag is the name of the volume, and the `Driver` tag specifies the volume driver plugin.</span></span> <span data-ttu-id="ba6b8-112">您可以使用 `DriverOption` 標記指定選項，如下列程式碼片段所示：</span><span class="sxs-lookup"><span data-stu-id="ba6b8-112">Options can be specified using the `DriverOption` tag as shown in the following snippet:</span></span>

```xml
<Volume Source="myvolume1" Destination="c:\testmountlocation4" Driver="azurefile" IsReadOnly="true">
           <DriverOption Name="share" Value="models"/>
</Volume>
```

<span data-ttu-id="ba6b8-113">如果指定了 Docker 記錄驅動程式，就必須在叢集中部署代理程式 (或容器) 來處理記錄檔。</span><span class="sxs-lookup"><span data-stu-id="ba6b8-113">If a Docker log driver is specified, it is necessary to deploy agents (or containers) to handle the logs in the cluster.</span></span>  <span data-ttu-id="ba6b8-114">`DriverOption` 標記也可用來指定記錄驅動程式選項。</span><span class="sxs-lookup"><span data-stu-id="ba6b8-114">The `DriverOption` tag can be used to specify log driver options as well.</span></span>

<span data-ttu-id="ba6b8-115">請參閱下列文章將容器部署至 Service Fabric 叢集：</span><span class="sxs-lookup"><span data-stu-id="ba6b8-115">Refer to the following articles to deploy containers to a Service Fabric cluster:</span></span>


[<span data-ttu-id="ba6b8-116">將容器部署在 Service Fabric 上</span><span class="sxs-lookup"><span data-stu-id="ba6b8-116">Deploy a container on Service Fabric</span></span>](service-fabric-deploy-container.md)

