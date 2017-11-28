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
# <a name="how-toocontainerize-your-service-fabric-reliable-services-and-reliable-actors-preview"></a><span data-ttu-id="1b22f-104">Toocontainerize 您服務的網狀架構 Reliable Services 如何與可靠的動作項目 （預覽）</span><span class="sxs-lookup"><span data-stu-id="1b22f-104">How toocontainerize your Service Fabric Reliable Services and Reliable Actors (Preview)</span></span>

<span data-ttu-id="1b22f-105">Service Fabric 支援將 Service Fabric 微服務 (Reliable Services 和 Reliable Actors 型服務) 容器化。</span><span class="sxs-lookup"><span data-stu-id="1b22f-105">Service Fabric supports containerizing Service Fabric microservices (Reliable Services, and Reliable Actor based services).</span></span> <span data-ttu-id="1b22f-106">如需詳細資訊，請參閱 [Service Fabric 容器](service-fabric-containers-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="1b22f-106">For more information, see [service fabric containers](service-fabric-containers-overview.md).</span></span>


 <span data-ttu-id="1b22f-107">這項功能處於預覽狀態，本文章提供 hello 各種步驟 tooget 您容器內執行的服務。</span><span class="sxs-lookup"><span data-stu-id="1b22f-107">This feature is in preview and this article provides hello various steps tooget your service running inside a container.</span></span>  

> [!NOTE]
> <span data-ttu-id="1b22f-108">此功能目前只能預覽，尚未在生產環境中受到支援。</span><span class="sxs-lookup"><span data-stu-id="1b22f-108">This feature is in preview and is not supported in production.</span></span> <span data-ttu-id="1b22f-109">此功能目前僅適用於 Windows。</span><span class="sxs-lookup"><span data-stu-id="1b22f-109">Currently this feature only works for Windows.</span></span>

## <a name="steps-toocontainerize-your-service-fabric-application"></a><span data-ttu-id="1b22f-110">步驟 toocontainerize 服務網狀架構應用程式</span><span class="sxs-lookup"><span data-stu-id="1b22f-110">Steps toocontainerize your Service Fabric Application</span></span>

1. <span data-ttu-id="1b22f-111">在 Visual Studio 中開啟 Service Fabric 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1b22f-111">Open your Service Fabric application in Visual Studio.</span></span>

2. <span data-ttu-id="1b22f-112">將類別加入[SFBinaryLoader.cs](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/code/SFBinaryLoaderForContainers/SFBinaryLoader.cs) tooyour 專案。</span><span class="sxs-lookup"><span data-stu-id="1b22f-112">Add class [SFBinaryLoader.cs](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/code/SFBinaryLoaderForContainers/SFBinaryLoader.cs) tooyour project.</span></span> <span data-ttu-id="1b22f-113">此類別中的 hello 程式碼位在容器內執行時 helper toocorrectly 負載 hello Service Fabric 執行階段二進位檔在您的應用程式內。</span><span class="sxs-lookup"><span data-stu-id="1b22f-113">hello code in this class is a helper toocorrectly load hello Service Fabric runtime binaries inside your application when running inside a container.</span></span>

3. <span data-ttu-id="1b22f-114">針對每個程式碼封裝，您會希望 toocontainerize，初始化 hello 載入器在 hello 程式進入點。</span><span class="sxs-lookup"><span data-stu-id="1b22f-114">For each code package you would like toocontainerize, initialize hello loader at hello program entry point.</span></span> <span data-ttu-id="1b22f-115">加入下列程式碼片段 tooyour 程式進入點檔 hello 中顯示 hello 靜態建構函式。</span><span class="sxs-lookup"><span data-stu-id="1b22f-115">Add hello static constructor shown in hello following code snippet tooyour program entry point file.</span></span>

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

4. <span data-ttu-id="1b22f-116">建置和[封裝](service-fabric-package-apps.md#Package-App)您的專案。</span><span class="sxs-lookup"><span data-stu-id="1b22f-116">Build and [package](service-fabric-package-apps.md#Package-App) your project.</span></span> <span data-ttu-id="1b22f-117">toobuild 和建立封裝，以滑鼠右鍵按一下方案總管 中的 hello 應用程式專案並選擇 hello**封裝**命令。</span><span class="sxs-lookup"><span data-stu-id="1b22f-117">toobuild and create a package, right-click hello application project in Solution Explorer and choose hello **Package** command.</span></span>

5. <span data-ttu-id="1b22f-118">針對每個程式碼封裝中，您需要 toocontainerize，執行 hello PowerShell 指令碼[CreateDockerPackage.ps1](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/scripts/CodePackageToDockerPackage/CreateDockerPackage.ps1)。</span><span class="sxs-lookup"><span data-stu-id="1b22f-118">For every code package you need toocontainerize, run hello PowerShell script [CreateDockerPackage.ps1](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/scripts/CodePackageToDockerPackage/CreateDockerPackage.ps1).</span></span> <span data-ttu-id="1b22f-119">hello 用法如下所示：</span><span class="sxs-lookup"><span data-stu-id="1b22f-119">hello usage is as follows:</span></span>
  ```powershell
    $codePackagePath = 'Path toohello code package toocontainerize.'
    $dockerPackageOutputDirectoryPath = 'Output path for hello generated docker folder.'
    $applicationExeName = 'Name of hello ode package executable.'
    CreateDockerPackage.ps1 -CodePackageDirectoryPath $codePackagePath -DockerPackageOutputDirectoryPath $dockerPackageOutputDirectoryPath -ApplicationExeName $applicationExeName
 ```
  <span data-ttu-id="1b22f-120">hello 指令碼會建立在 $dockerPackageOutputDirectoryPath Docker 成品 資料夾。</span><span class="sxs-lookup"><span data-stu-id="1b22f-120">hello script creates a folder with Docker artifacts at $dockerPackageOutputDirectoryPath.</span></span> <span data-ttu-id="1b22f-121">修改產生的 hello Dockerfile tooexpose 任何連接埠，執行安裝指令碼等等，根據您的需求。</span><span class="sxs-lookup"><span data-stu-id="1b22f-121">Modify hello generated Dockerfile tooexpose any ports, run setup scripts etc. based on your needs.</span></span>

6. <span data-ttu-id="1b22f-122">接下來您需要太[建置](service-fabric-get-started-containers.md#Build-Containers)和[發送](service-fabric-get-started-containers.md#Push-Containers)您 Docker 容器封裝 tooyour 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="1b22f-122">Next you need too[build](service-fabric-get-started-containers.md#Build-Containers) and [push](service-fabric-get-started-containers.md#Push-Containers) your Docker container package tooyour repository.</span></span>

7. <span data-ttu-id="1b22f-123">修改 hello ApplicationManifest.xml 和 ServiceManifest.xml tooadd 容器映像、 儲存機制資訊、 登錄驗證和連接埠-主控件對應。</span><span class="sxs-lookup"><span data-stu-id="1b22f-123">Modify hello ApplicationManifest.xml and ServiceManifest.xml tooadd your container image, repository information, registry authentication, and port-to-host mapping.</span></span> <span data-ttu-id="1b22f-124">修改 hello 資訊清單，請參閱[建立 Azure Service Fabric 容器應用程式](service-fabric-get-started-containers.md)。</span><span class="sxs-lookup"><span data-stu-id="1b22f-124">For modifying hello manifests, see [Create an Azure Service Fabric container application](service-fabric-get-started-containers.md).</span></span> <span data-ttu-id="1b22f-125">hello 服務資訊清單需求 toobe 取代對應的容器映像中的 hello 程式碼封裝定義。</span><span class="sxs-lookup"><span data-stu-id="1b22f-125">hello code package definition in hello service manifest needs toobe replaced with corresponding container image.</span></span> <span data-ttu-id="1b22f-126">請確定 toochange hello EntryPoint tooa ContainerHost 型別。</span><span class="sxs-lookup"><span data-stu-id="1b22f-126">Make sure toochange hello EntryPoint tooa ContainerHost type.</span></span>

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

8. <span data-ttu-id="1b22f-127">加入您的複寫器和服務端點的 hello 到主機的連接埠對應。</span><span class="sxs-lookup"><span data-stu-id="1b22f-127">Add hello port-to-host mapping for your replicator and service endpoint.</span></span> <span data-ttu-id="1b22f-128">Service Fabric 執行階段指派這些連接埠，因為 hello ContainerPort 設定 toozero toouse hello 分派對應的連接埠。</span><span class="sxs-lookup"><span data-stu-id="1b22f-128">Since both these ports are assigned at runtime by Service Fabric, hello ContainerPort is set toozero toouse hello assigned port for mapping.</span></span>

 ```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="0" EndpointRef="ServiceEndpoint"/>
    <PortBinding ContainerPort="0" EndpointRef="ReplicatorEndpoint"/>
  </ContainerHostPolicies>
</Policies>
 ```

9. <span data-ttu-id="1b22f-129">tootest 此應用程式，您需要 toodeploy 它 tooa 叢集中執行版本 5.7 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="1b22f-129">tootest this application, you need toodeploy it tooa cluster that is running version 5.7 or higher.</span></span> <span data-ttu-id="1b22f-130">此外，您需要 tooedit，並更新 hello 叢集設定 tooenable 這項預覽功能。</span><span class="sxs-lookup"><span data-stu-id="1b22f-130">In addition, you need tooedit and update hello cluster settings tooenable this preview feature.</span></span> <span data-ttu-id="1b22f-131">在這個步驟 hello[文章](service-fabric-cluster-fabric-settings.md)tooadd hello 設定顯示在下一步。</span><span class="sxs-lookup"><span data-stu-id="1b22f-131">Follow hello steps in this [article](service-fabric-cluster-fabric-settings.md) tooadd hello setting shown next.</span></span>
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
10. <span data-ttu-id="1b22f-132">下一步[部署](service-fabric-deploy-remove-applications.md)hello 編輯應用程式封裝 toothis 叢集。</span><span class="sxs-lookup"><span data-stu-id="1b22f-132">Next [deploy](service-fabric-deploy-remove-applications.md) hello edited application package toothis cluster.</span></span>

<span data-ttu-id="1b22f-133">現在，您的叢集中應該會有正在執行的容器化 Service Fabric 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1b22f-133">You should now have a containerized Service Fabric application running your cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b22f-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1b22f-134">Next steps</span></span>
* <span data-ttu-id="1b22f-135">深入了解如何[在 Service Fabric 上執行容器](service-fabric-get-started-containers.md)。</span><span class="sxs-lookup"><span data-stu-id="1b22f-135">Learn more about running [containers on Service Fabric](service-fabric-get-started-containers.md).</span></span>
* <span data-ttu-id="1b22f-136">深入了解 hello Service Fabric[應用程式生命週期](service-fabric-application-lifecycle.md)。</span><span class="sxs-lookup"><span data-stu-id="1b22f-136">Learn about hello Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
