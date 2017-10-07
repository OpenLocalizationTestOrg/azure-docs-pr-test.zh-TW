---
title: "aaaHow toocontainerize 您 Azure Service Fabric microservices （預覽）"
description: "Azure Service Fabric 已加入新的功能 toocontainerize Service Fabric microservices。 此功能目前為預覽狀態。"
services: service-fabric
documentationcenter: .net
author: anmolah
manager: anmolah
editor: anmolah
ms.assetid: 0b41efb3-4063-4600-89f5-b077ea81fa3a
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/04/2017
ms.author: anmola
ms.openlocfilehash: 6edaff73c0828707c7fa736669ba8084663d31ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocontainerize-your-service-fabric-reliable-services-and-reliable-actors-preview"></a>Toocontainerize 您服務的網狀架構 Reliable Services 如何與可靠的動作項目 （預覽）

Service Fabric 支援將 Service Fabric 微服務 (Reliable Services 和 Reliable Actors 型服務) 容器化。 如需詳細資訊，請參閱 [Service Fabric 容器](service-fabric-containers-overview.md)。


 這項功能處於預覽狀態，本文章提供 hello 各種步驟 tooget 您容器內執行的服務。  

> [!NOTE]
> 此功能目前只能預覽，尚未在生產環境中受到支援。 此功能目前僅適用於 Windows。

## <a name="steps-toocontainerize-your-service-fabric-application"></a>步驟 toocontainerize 服務網狀架構應用程式

1. 在 Visual Studio 中開啟 Service Fabric 應用程式。

2. 將類別加入[SFBinaryLoader.cs](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/code/SFBinaryLoaderForContainers/SFBinaryLoader.cs) tooyour 專案。 此類別中的 hello 程式碼位在容器內執行時 helper toocorrectly 負載 hello Service Fabric 執行階段二進位檔在您的應用程式內。

3. 針對每個程式碼封裝，您會希望 toocontainerize，初始化 hello 載入器在 hello 程式進入點。 加入下列程式碼片段 tooyour 程式進入點檔 hello 中顯示 hello 靜態建構函式。

  ```csharp
  namespace MyApplication
  {
      internal static class Program
      {
          static Program()
          {
              SFBinaryLoader.Initialize();
          }

          /// <summary>
          /// This is hello entry point of hello service host process.
          /// </summary>
          private static void Main()
          {
  ```

4. 建置和[封裝](service-fabric-package-apps.md#Package-App)您的專案。 toobuild 和建立封裝，以滑鼠右鍵按一下方案總管 中的 hello 應用程式專案並選擇 hello**封裝**命令。

5. 針對每個程式碼封裝中，您需要 toocontainerize，執行 hello PowerShell 指令碼[CreateDockerPackage.ps1](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/scripts/CodePackageToDockerPackage/CreateDockerPackage.ps1)。 hello 用法如下所示：
  ```powershell
    $codePackagePath = 'Path toohello code package toocontainerize.'
    $dockerPackageOutputDirectoryPath = 'Output path for hello generated docker folder.'
    $applicationExeName = 'Name of hello ode package executable.'
    CreateDockerPackage.ps1 -CodePackageDirectoryPath $codePackagePath -DockerPackageOutputDirectoryPath $dockerPackageOutputDirectoryPath -ApplicationExeName $applicationExeName
 ```
  hello 指令碼會建立在 $dockerPackageOutputDirectoryPath Docker 成品 資料夾。 修改產生的 hello Dockerfile tooexpose 任何連接埠，執行安裝指令碼等等，根據您的需求。

6. 接下來您需要太[建置](service-fabric-get-started-containers.md#Build-Containers)和[發送](service-fabric-get-started-containers.md#Push-Containers)您 Docker 容器封裝 tooyour 儲存機制。

7. 修改 hello ApplicationManifest.xml 和 ServiceManifest.xml tooadd 容器映像、 儲存機制資訊、 登錄驗證和連接埠-主控件對應。 修改 hello 資訊清單，請參閱[建立 Azure Service Fabric 容器應用程式](service-fabric-get-started-containers.md)。 hello 服務資訊清單需求 toobe 取代對應的容器映像中的 hello 程式碼封裝定義。 請確定 toochange hello EntryPoint tooa ContainerHost 型別。

  ```xml
<!-- Code package is your service executable. -->
<CodePackage Name="Code" Version="1.0.0">
  <EntryPoint>
    <!-- Follow this link for more information about deploying Windows containers tooService Fabric: https://aka.ms/sfguestcontainers -->
    <ContainerHost>
      <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
    </ContainerHost>
  </EntryPoint>
  <!-- Pass environment variables tooyour container: -->    
</CodePackage>
  ```

8. 加入您的複寫器和服務端點的 hello 到主機的連接埠對應。 Service Fabric 執行階段指派這些連接埠，因為 hello ContainerPort 設定 toozero toouse hello 分派對應的連接埠。

 ```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="0" EndpointRef="ServiceEndpoint"/>
    <PortBinding ContainerPort="0" EndpointRef="ReplicatorEndpoint"/>
  </ContainerHostPolicies>
</Policies>
 ```

9. tootest 此應用程式，您需要 toodeploy 它 tooa 叢集中執行版本 5.7 或更高版本。 此外，您需要 tooedit，並更新 hello 叢集設定 tooenable 這項預覽功能。 在這個步驟 hello[文章](service-fabric-cluster-fabric-settings.md)tooadd hello 設定顯示在下一步。
```
      {
        "name": "Hosting",
        "parameters": [
          {
            "name": "FabricContainerAppsEnabled",
            "value": "true"
          }
        ]
      }
```
10. 下一步[部署](service-fabric-deploy-remove-applications.md)hello 編輯應用程式封裝 toothis 叢集。

現在，您的叢集中應該會有正在執行的容器化 Service Fabric 應用程式。

## <a name="next-steps"></a>後續步驟
* 深入了解如何[在 Service Fabric 上執行容器](service-fabric-get-started-containers.md)。
* 深入了解 hello Service Fabric[應用程式生命週期](service-fabric-application-lifecycle.md)。
