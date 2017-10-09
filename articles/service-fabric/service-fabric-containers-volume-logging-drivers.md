---
title: "服務網狀架構 Docker 撰寫預覽 aaaAzure |Microsoft 文件"
description: "Azure Service Fabric 接受 Docker Compose 格式 toomake 它更容易使用 Service Fabric tooorchestrate exsiting 容器。 這項支援目前只能預覽。"
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
ms.openlocfilehash: 824044fd698f0ed94c4212722bc82187905315dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-volume-plugins-and-logging-drivers-for-your-container"></a>指定容器的磁碟區外掛程式和記錄驅動程式

Service Fabric 支援為容器服務指定 [Docker 磁碟區外掛程式](https://docs.docker.com/engine/extend/plugins_volume/)和 [Docker 記錄驅動程式](https://docs.docker.com/engine/admin/logging/overview/)。 hello 外掛程式 hello 應用程式資訊清單中指定下列資訊清單的 hello 中所示：


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

在上述範例中的 hello，hello`Source`標記 hello`Volume`參考 toohello 來源資料夾。 hello 來源資料夾可能是 hello hello 容器或永續性的遠端存放區所裝載的 VM 中的資料夾。 hello`Destination`標記是 hello 的 hello 位置`Source`對應的 toowithin hello 執行容器。 

指定磁碟區外掛程式，Service Fabric 會自動建立使用指定的 hello 參數 hello 磁碟區。 hello`Source`標記是 hello 名稱 hello 磁碟區與 hello`Driver`標記指定 hello 磁碟區的驅動程式的外掛程式。 您可以指定選項，使用 hello`DriverOption`標記 hello 下列程式碼片段所示：

```xml
<Volume Source="myvolume1" Destination="c:\testmountlocation4" Driver="azurefile" IsReadOnly="true">
           <DriverOption Name="share" Value="models"/>
</Volume>
```

如果指定 Docker 記錄驅動程式，則是必要 toodeploy hello 叢集中的代理程式 （或容器） toohandle hello 記錄。  hello`DriverOption`標記可以用的 toospecify 記錄驅動程式選項以及。

請參閱下列文章 toodeploy 容器 tooa Service Fabric 叢集 toohello:


[將容器部署在 Service Fabric 上](service-fabric-deploy-container.md)

