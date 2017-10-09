---
title: "aaaService 網狀架構和部署容器 |Microsoft 文件"
description: "Service Fabric 和 hello 使用容器 toodeploy 微服務應用程式。 本文說明 Service Fabric 提供容器和如何 toodeploy Windows 容器映像到叢集中的 hello 功能。"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 799cc9ad-32fd-486e-a6b6-efff6b13622d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/16/2017
ms.author: msfussell
ms.openlocfilehash: 8b6540579641474f21b8712b56049c7d177bec26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-windows-container-tooservice-fabric"></a><span data-ttu-id="65fae-104">部署 Windows 容器 tooService 網狀架構</span><span class="sxs-lookup"><span data-stu-id="65fae-104">Deploy a Windows container tooService Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="65fae-105">部署 Windows 容器</span><span class="sxs-lookup"><span data-stu-id="65fae-105">Deploy Windows Container</span></span>](service-fabric-deploy-container.md)
> * [<span data-ttu-id="65fae-106">部署 Docker 容器</span><span class="sxs-lookup"><span data-stu-id="65fae-106">Deploy Docker Container</span></span>](service-fabric-deploy-container-linux.md)
> 
> 

<span data-ttu-id="65fae-107">這篇文章會引導您建立 Windows 容器中的容器化的服務的 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="65fae-107">This article walks you through hello process of building containerized services in Windows containers.</span></span>

<span data-ttu-id="65fae-108">Service Fabric 有數個功能可協助您建置由容器內執行之微服務組成的應用程式。</span><span class="sxs-lookup"><span data-stu-id="65fae-108">Service Fabric has several capabilities that help you with building applications that are composed of microservices running inside containers.</span></span> 

<span data-ttu-id="65fae-109">hello 功能包括：</span><span class="sxs-lookup"><span data-stu-id="65fae-109">hello capabilities include:</span></span>

* <span data-ttu-id="65fae-110">容器映像部署和啟用</span><span class="sxs-lookup"><span data-stu-id="65fae-110">Container image deployment and activation</span></span>
* <span data-ttu-id="65fae-111">資源管理</span><span class="sxs-lookup"><span data-stu-id="65fae-111">Resource governance</span></span>
* <span data-ttu-id="65fae-112">儲存機制驗證</span><span class="sxs-lookup"><span data-stu-id="65fae-112">Repository authentication</span></span>
* <span data-ttu-id="65fae-113">容器連接埠至主機連接埠的對應</span><span class="sxs-lookup"><span data-stu-id="65fae-113">Container port-to-host port mapping</span></span>
* <span data-ttu-id="65fae-114">容器至容器的探索及通訊</span><span class="sxs-lookup"><span data-stu-id="65fae-114">Container-to-container discovery and communication</span></span>
* <span data-ttu-id="65fae-115">能力 tooconfigure 並設定環境變數</span><span class="sxs-lookup"><span data-stu-id="65fae-115">Ability tooconfigure and set environment variables</span></span>

<span data-ttu-id="65fae-116">讓我們看看您要封裝包含在您的應用程式容器化的服務 toobe 時，每個功能的運作方式。</span><span class="sxs-lookup"><span data-stu-id="65fae-116">Let's look at how each of capabilities works when you're packaging a containerized service toobe included in your application.</span></span>

## <a name="package-a-windows-container"></a><span data-ttu-id="65fae-117">封裝 Windows 容器</span><span class="sxs-lookup"><span data-stu-id="65fae-117">Package a Windows container</span></span>
<span data-ttu-id="65fae-118">當您封裝的容器時，您可以選擇 toouse Visual Studio 專案範本或[手動建立 hello 應用程式封裝](#manually)。</span><span class="sxs-lookup"><span data-stu-id="65fae-118">When you package a container, you can choose toouse either a Visual Studio project template or [create hello application package manually](#manually).</span></span>  <span data-ttu-id="65fae-119">當您使用 Visual Studio，hello 應用程式封裝的結構，並為您建立資訊清單檔案的 hello 新的專案範本。</span><span class="sxs-lookup"><span data-stu-id="65fae-119">When you use Visual Studio, hello application package structure and manifest files are created by hello New Project template for you.</span></span>

> [!TIP]
> <span data-ttu-id="65fae-120">最簡單方式 toopackage hello 現有的容器映像服務是 toouse Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="65fae-120">hello easiest way toopackage an existing container image into a service is toouse Visual Studio.</span></span>

## <a name="use-visual-studio-toopackage-an-existing-container-image"></a><span data-ttu-id="65fae-121">使用 Visual Studio toopackage 現有的容器映像</span><span class="sxs-lookup"><span data-stu-id="65fae-121">Use Visual Studio toopackage an existing container image</span></span>
<span data-ttu-id="65fae-122">Visual Studio 提供 Service Fabric 服務範本 toohelp 部署容器 tooa Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="65fae-122">Visual Studio provides a Service Fabric service template toohelp you deploy a container tooa Service Fabric cluster.</span></span>

1. <span data-ttu-id="65fae-123">選擇 [檔案]  >  [新增專案]，然後建立 Service Fabric 應用程式。</span><span class="sxs-lookup"><span data-stu-id="65fae-123">Choose **File** > **New Project**, and create a Service Fabric application.</span></span>
2. <span data-ttu-id="65fae-124">選擇**客體容器**作為 hello 服務範本。</span><span class="sxs-lookup"><span data-stu-id="65fae-124">Choose **Guest Container** as hello service template.</span></span>
3. <span data-ttu-id="65fae-125">選擇**映像名稱**並提供您的容器儲存機制中的 hello 路徑 toohello 映像。</span><span class="sxs-lookup"><span data-stu-id="65fae-125">Choose **Image Name** and provide hello path toohello image in your container repository.</span></span> <span data-ttu-id="65fae-126">例如，https://hub.docker.com 中的 `myrepo/myimage:v1`</span><span class="sxs-lookup"><span data-stu-id="65fae-126">For example, `myrepo/myimage:v1` in https://hub.docker.com</span></span>
4. <span data-ttu-id="65fae-127">指定服務的名稱，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="65fae-127">Give your service a name, and click **OK**.</span></span>
5. <span data-ttu-id="65fae-128">如果您容器化的服務端點需要通訊，您現在可以新增 hello 通訊協定、 連接埠和型別 toohello ServiceManifest.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="65fae-128">If your containerized service needs an endpoint for communication, you can now add hello protocol, port, and type toohello ServiceManifest.xml file.</span></span> <span data-ttu-id="65fae-129">例如：</span><span class="sxs-lookup"><span data-stu-id="65fae-129">For example:</span></span> 
     
    `<Endpoint Name="MyContainerServiceEndpoint" Protocol="http" Port="80" UriScheme="http" PathSuffix="myapp/" Type="Input" />`
    
    <span data-ttu-id="65fae-130">藉由提供 hello `UriScheme`，Service Fabric 會自動以 hello 的發現能力命名服務註冊 hello 容器端點。</span><span class="sxs-lookup"><span data-stu-id="65fae-130">By providing hello `UriScheme`, Service Fabric automatically registers hello container endpoint with hello Naming service for discoverability.</span></span> <span data-ttu-id="65fae-131">hello 連接埠可以固定的 （如同 hello 前面範例所示） 或動態配置。</span><span class="sxs-lookup"><span data-stu-id="65fae-131">hello port can either be fixed (as shown in hello preceding example) or dynamically allocated.</span></span> <span data-ttu-id="65fae-132">如果您未指定連接埠，會以動態方式配置從 hello 應用程式連接埠範圍 （如同發生與任何服務）。</span><span class="sxs-lookup"><span data-stu-id="65fae-132">If you don't specify a port, it is dynamically allocated from hello application port range (as would happen with any service).</span></span>
    <span data-ttu-id="65fae-133">您也需要 tooconfigure hello 容器 toohost 連接埠對應藉由指定`PortBinding`hello 應用程式資訊清單中的原則。</span><span class="sxs-lookup"><span data-stu-id="65fae-133">You also need tooconfigure hello container toohost port mapping by specifying a `PortBinding` policy in hello application manifest.</span></span> <span data-ttu-id="65fae-134">如需詳細資訊，請參閱[設定容器 toohost 連接埠對應](#Portsection)。</span><span class="sxs-lookup"><span data-stu-id="65fae-134">For more information, see [Configure container toohost port mapping](#Portsection).</span></span>
6. <span data-ttu-id="65fae-135">如果您的容器需要資源管理，則請新增 `ResourceGovernancePolicy`。</span><span class="sxs-lookup"><span data-stu-id="65fae-135">If your container needs resource governance then add a `ResourceGovernancePolicy`.</span></span>
8. <span data-ttu-id="65fae-136">如果您的容器需要 tooauthenticate 與私用儲存機制，然後新增`RepositoryCredentials`。</span><span class="sxs-lookup"><span data-stu-id="65fae-136">If your container needs tooauthenticate with a private repository, then add `RepositoryCredentials`.</span></span>
7. <span data-ttu-id="65fae-137">如果您沒有啟用容器支援執行 Windows Server 2016 電腦上，您可以使用 hello 封裝和發行動作 toodeploy tooyour 本機叢集。</span><span class="sxs-lookup"><span data-stu-id="65fae-137">If you are running on a Windows Server 2016 machine with container support enabled, you can use hello package and publish action toodeploy tooyour local cluster.</span></span> 
8. <span data-ttu-id="65fae-138">準備就緒時，您可以發行 hello 應用程式 tooa 遠端叢集，或檢查 hello 方案 toosource 控制項中。</span><span class="sxs-lookup"><span data-stu-id="65fae-138">When ready, you can publish hello application tooa remote cluster or check in hello solution toosource control.</span></span> 

<span data-ttu-id="65fae-139">例如，簽出 hello [GitHub 上的 Service Fabric 容器程式碼範例](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="65fae-139">For an example, checkout hello [Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>

## <a name="creating-a-windows-server-2016-cluster"></a><span data-ttu-id="65fae-140">建立 Windows Server 2016 叢集</span><span class="sxs-lookup"><span data-stu-id="65fae-140">Creating a Windows Server 2016 cluster</span></span>
<span data-ttu-id="65fae-141">toodeploy 容器化的應用程式時，您需要的 toocreate 啟用容器支援執行 Windows Server 2016 的叢集。</span><span class="sxs-lookup"><span data-stu-id="65fae-141">toodeploy your containerized application, you need toocreate a cluster running Windows Server 2016 with container support enabled.</span></span> <span data-ttu-id="65fae-142">您的叢集可能會在本機執行，或透過 Azure Resource Manager 部署在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="65fae-142">Your cluster may be running locally, or deployed via Azure Resource Manager in Azure.</span></span> 

<span data-ttu-id="65fae-143">toodeploy 叢集中使用 Azure 資源管理員 中，選擇 hello**與容器的 Windows Server 2016**映像在 Azure 中的選項。</span><span class="sxs-lookup"><span data-stu-id="65fae-143">toodeploy a cluster using Azure Resource Manager, choose hello **Windows Server 2016 with Containers** image option in Azure.</span></span> <span data-ttu-id="65fae-144">請參閱 hello 文章[使用 Azure Resource Manager 建立 Service Fabric 叢集](service-fabric-cluster-creation-via-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="65fae-144">See hello article [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="65fae-145">請確定您使用下列 Azure 資源管理員設定的 hello:</span><span class="sxs-lookup"><span data-stu-id="65fae-145">Ensure that you use hello following Azure Resource Manager settings:</span></span>

```xml
"vmImageOffer": { "type": "string","defaultValue": "WindowsServer"     },
"vmImageSku": { "defaultValue": "2016-Datacenter-with-Containers","type": "string"     },
"vmImageVersion": { "defaultValue": "latest","type": "string"     },  
```
<span data-ttu-id="65fae-146">您也可以使用 hello[五個節點的 Azure Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype)toocreate 叢集。</span><span class="sxs-lookup"><span data-stu-id="65fae-146">You can also use hello [Five Node Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) toocreate a cluster.</span></span> <span data-ttu-id="65fae-147">或者，閱讀社群中的[部落格文章](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html)以了解如何使用 Service Fabric 和 Windows 容器。</span><span class="sxs-lookup"><span data-stu-id="65fae-147">Alternatively read a community [blog post](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) on using Service Fabric and Windows containers.</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a><span data-ttu-id="65fae-148">手動封裝和部署容器映像</span><span class="sxs-lookup"><span data-stu-id="65fae-148">Manually package and deploy a container image</span></span>
<span data-ttu-id="65fae-149">hello 程序手動封裝進行容器化的服務根據 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="65fae-149">hello process of manually packaging a containerized service is based on hello following steps:</span></span>

1. <span data-ttu-id="65fae-150">發行 hello 容器 tooyour 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="65fae-150">Publish hello containers tooyour repository.</span></span>
2. <span data-ttu-id="65fae-151">建立 hello 封裝目錄結構。</span><span class="sxs-lookup"><span data-stu-id="65fae-151">Create hello package directory structure.</span></span>
3. <span data-ttu-id="65fae-152">編輯 hello 服務資訊清單檔。</span><span class="sxs-lookup"><span data-stu-id="65fae-152">Edit hello service manifest file.</span></span>
4. <span data-ttu-id="65fae-153">編輯 hello 應用程式資訊清單檔案。</span><span class="sxs-lookup"><span data-stu-id="65fae-153">Edit hello application manifest file.</span></span>

## <a name="deploy-and-activate-a-container-image"></a><span data-ttu-id="65fae-154">部署和啟用容器映像</span><span class="sxs-lookup"><span data-stu-id="65fae-154">Deploy and activate a container image</span></span>
<span data-ttu-id="65fae-155">在 hello Service Fabric[應用程式模型](service-fabric-application-model.md)，容器代表複本會放在哪一種多個服務應用程式主機。</span><span class="sxs-lookup"><span data-stu-id="65fae-155">In hello Service Fabric [application model](service-fabric-application-model.md), a container represents an application host in which multiple service replicas are placed.</span></span> <span data-ttu-id="65fae-156">toodeploy 並啟動容器，put 的 hello 名稱 hello 容器映像到`ContainerHost`hello 服務資訊清單中的項目。</span><span class="sxs-lookup"><span data-stu-id="65fae-156">toodeploy and activate a container, put hello name of hello container image into a `ContainerHost` element in hello service manifest.</span></span>

<span data-ttu-id="65fae-157">在 hello 服務資訊清單中，加入`ContainerHost`hello 進入點。</span><span class="sxs-lookup"><span data-stu-id="65fae-157">In hello service manifest, add a `ContainerHost` for hello entry point.</span></span> <span data-ttu-id="65fae-158">然後組 hello `ImageName` toobe hello 名稱 hello 容器儲存機制和映像。</span><span class="sxs-lookup"><span data-stu-id="65fae-158">Then set hello `ImageName` toobe hello name of hello container repository and image.</span></span> <span data-ttu-id="65fae-159">hello 下列部分的資訊清單示範如何呼叫 toodeploy hello 容器`myimage:v1`從儲存機制稱為`myrepo`:</span><span class="sxs-lookup"><span data-stu-id="65fae-159">hello following partial manifest shows an example of how toodeploy hello container called `myimage:v1` from a repository called `myrepo`:</span></span>

```xml
    <CodePackage Name="Code" Version="1.0">
        <EntryPoint>
          <ContainerHost>
            <ImageName>myrepo/myimage:v1</ImageName>
            <Commands></Commands>
          </ContainerHost>
        </EntryPoint>
    </CodePackage>
```

<span data-ttu-id="65fae-160">您可以指定啟動 hello hello 容器時的選擇性命令 toorun`Commands`項目。</span><span class="sxs-lookup"><span data-stu-id="65fae-160">You can specify optional commands toorun upon starting hello container under hello `Commands` element.</span></span> <span data-ttu-id="65fae-161">若有多個命令，用逗號分隔它們。</span><span class="sxs-lookup"><span data-stu-id="65fae-161">For multiple commands, comma-delimit them.</span></span> 

## <a name="understand-resource-governance"></a><span data-ttu-id="65fae-162">了解資源管理</span><span class="sxs-lookup"><span data-stu-id="65fae-162">Understand resource governance</span></span>
<span data-ttu-id="65fae-163">資源管理機制是，限制 hello 容器的 hello 資源 hello 容器的功能可以使用 hello 主機上。</span><span class="sxs-lookup"><span data-stu-id="65fae-163">Resource governance is a capability of hello container that restricts hello resources that hello container can use on hello host.</span></span> <span data-ttu-id="65fae-164">hello `ResourceGovernancePolicy`，其中指定 hello 應用程式資訊清單中的就是使用的 toodeclare 資源限制，服務程式碼封裝。</span><span class="sxs-lookup"><span data-stu-id="65fae-164">hello `ResourceGovernancePolicy`, which is specified in hello application manifest is used toodeclare resource limits for a service code package.</span></span> <span data-ttu-id="65fae-165">您可以設定資源限制 hello 下列資源：</span><span class="sxs-lookup"><span data-stu-id="65fae-165">Resource limits can be set for hello following resources:</span></span>

* <span data-ttu-id="65fae-166">記憶體</span><span class="sxs-lookup"><span data-stu-id="65fae-166">Memory</span></span>
* <span data-ttu-id="65fae-167">MemorySwap</span><span class="sxs-lookup"><span data-stu-id="65fae-167">MemorySwap</span></span>
* <span data-ttu-id="65fae-168">CpuShares (CPU 相對權數)</span><span class="sxs-lookup"><span data-stu-id="65fae-168">CpuShares (CPU relative weight)</span></span>
* <span data-ttu-id="65fae-169">MemoryReservationInMB</span><span class="sxs-lookup"><span data-stu-id="65fae-169">MemoryReservationInMB</span></span>  
* <span data-ttu-id="65fae-170">BlkioWeight (BlockIO 相對權數)。</span><span class="sxs-lookup"><span data-stu-id="65fae-170">BlkioWeight (BlockIO relative weight).</span></span>

> [!NOTE]
> <span data-ttu-id="65fae-171">我們規劃在未來支援指定特定的區塊 IO 限制，例如 IOP、讀取/寫入 BPS 及其他限制。</span><span class="sxs-lookup"><span data-stu-id="65fae-171">Support for specifying specific block IO limits such as IOPs, read/write BPS, and others are planned for a future release.</span></span>
> 
> 

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ResourceGovernancePolicy CodePackageRef="FrontendService.Code" CpuShares="500"
            MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
        </Policies>
    </ServiceManifestImport>
```

## <a name="authenticate-a-repository"></a><span data-ttu-id="65fae-172">驗證儲存機制</span><span class="sxs-lookup"><span data-stu-id="65fae-172">Authenticate a repository</span></span>
<span data-ttu-id="65fae-173">toodownload 容器，您可能必須 tooprovide 登入認證 toohello 容器儲存機制。</span><span class="sxs-lookup"><span data-stu-id="65fae-173">toodownload a container, you might have tooprovide sign-in credentials toohello container repository.</span></span> <span data-ttu-id="65fae-174">hello 登入認證，在 hello 應用程式資訊清單中指定會使用的 toospecify hello 登入資訊或下載 hello 容器映像從 hello 映像儲存機制的 SSH 金鑰。</span><span class="sxs-lookup"><span data-stu-id="65fae-174">hello sign-in credentials, specified in hello application manifest, are used toospecify hello sign-in information, or SSH key, for downloading hello container image from hello image repository.</span></span> <span data-ttu-id="65fae-175">hello 下列範例將示範名為帳戶*TestUser*以及 hello 密碼以純文字 (*不*建議使用):</span><span class="sxs-lookup"><span data-stu-id="65fae-175">hello following example shows an account called *TestUser* along with hello password in clear text (*not* recommended):</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="12345" PasswordEncrypted="false"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

<span data-ttu-id="65fae-176">我們建議您在使用已部署 toohello 機器的憑證來加密 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="65fae-176">We recommend that you encrypt hello password by using a certificate that's deployed toohello machine.</span></span>

<span data-ttu-id="65fae-177">hello 下列範例將示範名為帳戶*TestUser*、 其中 hello 密碼加密所使用的憑證稱為*MyCert*。</span><span class="sxs-lookup"><span data-stu-id="65fae-177">hello following example shows an account called *TestUser*, where hello password was encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="65fae-178">您可以使用 hello `Invoke-ServiceFabricEncryptText` PowerShell 命令 toocreate hello 密碼加密文字 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="65fae-178">You can use hello `Invoke-ServiceFabricEncryptText` PowerShell command toocreate hello secret cipher text for hello password.</span></span> <span data-ttu-id="65fae-179">如需詳細資訊，請參閱 hello 文章[管理 Service Fabric 應用程式中的機密](service-fabric-application-secret-management.md)。</span><span class="sxs-lookup"><span data-stu-id="65fae-179">For more information, see hello article [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md).</span></span>

<span data-ttu-id="65fae-180">hello hello 憑證私密金鑰用 toodecrypt hello 密碼必須是已部署的 toohello 本機電腦的頻外方法中。</span><span class="sxs-lookup"><span data-stu-id="65fae-180">hello private key of hello certificate that's used toodecrypt hello password must be deployed toohello local machine in an out-of-band method.</span></span> <span data-ttu-id="65fae-181">(在 Azure 中，這個方法就是 Azure Resource Manager。)然後，當 Service Fabric 部署 hello 服務封裝 toohello 機器，它可以解密 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="65fae-181">(In Azure, this method is Azure Resource Manager.) Then, when Service Fabric deploys hello service package toohello machine, it can decrypt hello secret.</span></span> <span data-ttu-id="65fae-182">藉由使用 hello 密碼以及 hello 帳戶名稱，它可以再向 hello 容器儲存機制。</span><span class="sxs-lookup"><span data-stu-id="65fae-182">By using hello secret along with hello account name, it can then authenticate with hello container repository.</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="[Put encrypted password here using MyCert certificate ]" PasswordEncrypted="true"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <span data-ttu-id="65fae-183"><a name ="Portsection"></a>設定容器 toohost 連接埠對應</span><span class="sxs-lookup"><span data-stu-id="65fae-183"><a name ="Portsection"></a> Configure container toohost port mapping</span></span>
<span data-ttu-id="65fae-184">您也可以指定與 hello 容器設定主機使用的連接埠 toocommunicate `PortBinding` hello 應用程式資訊清單中。</span><span class="sxs-lookup"><span data-stu-id="65fae-184">You can configure a host port used toocommunicate with hello container by specifying a `PortBinding` in hello application manifest.</span></span> <span data-ttu-id="65fae-185">hello 連接埠繫結對應 hello 連接埠 toowhich hello 服務會接聽內部 hello 主機上的 hello 容器 tooa 通訊埠。</span><span class="sxs-lookup"><span data-stu-id="65fae-185">hello port binding maps hello port toowhich hello service is listening inside hello container tooa port on hello host.</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <a name="configure-container-to-container-discovery-and-communication"></a><span data-ttu-id="65fae-186">設定容器至容器的探索及通訊</span><span class="sxs-lookup"><span data-stu-id="65fae-186">Configure container-to-container discovery and communication</span></span>
<span data-ttu-id="65fae-187">您可以使用 hello`PortBinding`元素 toomap hello 服務資訊清單中的容器連接埠 tooan 端點。</span><span class="sxs-lookup"><span data-stu-id="65fae-187">You can use hello `PortBinding` element toomap a container port tooan endpoint in hello service manifest.</span></span> <span data-ttu-id="65fae-188">在下列範例的 hello，hello 端點`Endpoint1`8905 指定固定通訊埠。</span><span class="sxs-lookup"><span data-stu-id="65fae-188">In hello following example, hello endpoint `Endpoint1` specifies a fixed port, 8905.</span></span> <span data-ttu-id="65fae-189">也可以指定任何連接埠，在此情況下針對您選擇 hello 叢集應用程式連接埠範圍的隨機連接埠。</span><span class="sxs-lookup"><span data-stu-id="65fae-189">It can also specify no port at all, in which case a random port from hello cluster's application port range is chosen for you.</span></span>


```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```
<span data-ttu-id="65fae-190">如果您指定端點，使用 hello `Endpoint` hello 客體容器，Service Fabric 服務資訊清單中的標記可以自動發佈此端點 toohello 命名服務。</span><span class="sxs-lookup"><span data-stu-id="65fae-190">If you specify an endpoint, using hello `Endpoint` tag in hello service manifest of a guest container, Service Fabric can automatically publish this endpoint toohello Naming service.</span></span> <span data-ttu-id="65fae-191">因此，hello 叢集中執行的其他服務可以探索使用 hello REST 查詢以解析此容器。</span><span class="sxs-lookup"><span data-stu-id="65fae-191">Other services that are running in hello cluster can thus discover this container using hello REST queries for resolving.</span></span>

<span data-ttu-id="65fae-192">註冊以 hello 命名服務後，您可以執行容器的容器通訊您容器內使用 hello[反向 proxy](service-fabric-reverseproxy.md)。</span><span class="sxs-lookup"><span data-stu-id="65fae-192">By registering with hello Naming service, you can perform container-to-container communication within your container by using hello [reverse proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="65fae-193">通訊是由提供 hello 反向 proxy http 接聽連接埠和 hello 名稱要與 toocommunicate 視為環境變數的 hello 服務執行。</span><span class="sxs-lookup"><span data-stu-id="65fae-193">Communication is performed by providing hello reverse proxy http listening port and hello name of hello services that you want toocommunicate with as environment variables.</span></span> <span data-ttu-id="65fae-194">如需詳細資訊，請參閱 hello 下一節。</span><span class="sxs-lookup"><span data-stu-id="65fae-194">For more information, see hello next section.</span></span> 

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="65fae-195">設定環境變數</span><span class="sxs-lookup"><span data-stu-id="65fae-195">Configure and set environment variables</span></span>
<span data-ttu-id="65fae-196">環境變數可以指定每個程式碼封裝 hello 服務資訊清單中。</span><span class="sxs-lookup"><span data-stu-id="65fae-196">Environment variables can be specified for each code package in hello service manifest.</span></span> <span data-ttu-id="65fae-197">所有服務都有這項功能，無論是部署為容器或處理程序或來賓可執行檔。</span><span class="sxs-lookup"><span data-stu-id="65fae-197">This feature is available for all services irrespective of whether they are deployed as containers or processes or guest executables.</span></span> <span data-ttu-id="65fae-198">您可以覆寫資訊清單 hello 應用程式中的值，或做為應用程式參數的部署期間指定這些環境變數。</span><span class="sxs-lookup"><span data-stu-id="65fae-198">You can override environment variable values in hello application manifest or specify them during deployment as application parameters.</span></span>

<span data-ttu-id="65fae-199">hello 下列服務資訊清單 XML 程式碼片段示範如何的範例程式碼封裝的 toospecify 環境變數：</span><span class="sxs-lookup"><span data-stu-id="65fae-199">hello following service manifest XML snippet shows an example of how toospecify environment variables for a code package:</span></span>

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>a guest executable service in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
    </ServiceManifest>
```

<span data-ttu-id="65fae-200">這些環境變數會覆寫 hello 應用程式層級資訊清單：</span><span class="sxs-lookup"><span data-stu-id="65fae-200">These environment variables can be overridden at hello application manifest level:</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

<span data-ttu-id="65fae-201">在 hello 前一個範例中，我們已指定明確的值為 hello`HttpGateway`環境變數 (19000)，而我們將設定為 hello 值`BackendServiceName`參數透過 hello`[BackendSvc]`應用程式參數。</span><span class="sxs-lookup"><span data-stu-id="65fae-201">In hello previous example, we specified an explicit value for hello `HttpGateway` environment variable (19000), while we set hello value for `BackendServiceName` parameter via hello `[BackendSvc]` application parameter.</span></span> <span data-ttu-id="65fae-202">這些設定可讓您 toospecify hello 值`BackendServiceName`時部署 hello 應用程式和 hello 資訊清單中沒有固定的值的值。</span><span class="sxs-lookup"><span data-stu-id="65fae-202">These settings enable you toospecify hello value for `BackendServiceName`value when you deploy hello application and not have a fixed value in hello manifest.</span></span>

## <a name="configure-isolation-mode"></a><span data-ttu-id="65fae-203">設定隔離模式</span><span class="sxs-lookup"><span data-stu-id="65fae-203">Configure isolation mode</span></span>

<span data-ttu-id="65fae-204">Windows 支援兩種容器隔離模式 - 處理序和 Hyper-V。</span><span class="sxs-lookup"><span data-stu-id="65fae-204">Windows supports two isolation modes for containers - process and Hyper-V.</span></span>  <span data-ttu-id="65fae-205">Hello 處理序隔離模式中，所有的 hello 容器上執行 hello 相同主機電腦共用 hello 核心與 hello 主機。</span><span class="sxs-lookup"><span data-stu-id="65fae-205">With hello process isolation mode, all hello containers running on hello same host machine share hello kernel with hello host.</span></span> <span data-ttu-id="65fae-206">Hello HYPER-V 隔離模式中，hello 核心會隔離每個 HYPER-V 容器與 hello 容器主機之間。</span><span class="sxs-lookup"><span data-stu-id="65fae-206">With hello Hyper-V isolation mode, hello kernels are isolated between each Hyper-V container and hello container host.</span></span> <span data-ttu-id="65fae-207">指定在 hello hello 隔離模式`ContainerHostPolicies`hello 應用程式資訊清單檔中的標記。</span><span class="sxs-lookup"><span data-stu-id="65fae-207">hello isolation mode is specified in hello `ContainerHostPolicies` tag in hello application manifest file.</span></span>  <span data-ttu-id="65fae-208">hello 隔離模式可指定為`process`， `hyperv`，和`default`。</span><span class="sxs-lookup"><span data-stu-id="65fae-208">hello isolation modes that can be specified are `process`, `hyperv`, and `default`.</span></span> <span data-ttu-id="65fae-209">hello`default`太預設隔離模式`process`Windows 伺服器上裝載，且預設值太`hyperv`Windows 10 主機上。</span><span class="sxs-lookup"><span data-stu-id="65fae-209">hello `default` isolation mode defaults too`process` on Windows Server hosts, and defaults too`hyperv` on Windows 10 hosts.</span></span>  <span data-ttu-id="65fae-210">hello 下列程式碼片段示範如何指定 hello 應用程式資訊清單檔中的 hello 隔離模式。</span><span class="sxs-lookup"><span data-stu-id="65fae-210">hello following snippet shows how hello isolation mode is specified in hello application manifest file.</span></span>

```xml
   <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv">
```


## <a name="complete-examples-for-application-and-service-manifest"></a><span data-ttu-id="65fae-211">應用程式和服務資訊清單的完整範例</span><span class="sxs-lookup"><span data-stu-id="65fae-211">Complete examples for application and service manifest</span></span>

<span data-ttu-id="65fae-212">以下是應用程式資訊清單：</span><span class="sxs-lookup"><span data-stu-id="65fae-212">An example application manifest follows:</span></span>

```xml
    <ApplicationManifest ApplicationTypeName="SimpleContainerApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>A simple service container application</Description>
        <Parameters>
            <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
            <Parameter Name="BackEndSvcName" DefaultValue="bkend"></Parameter>
        </Parameters>
        <ServiceManifestImport>
            <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
            <EnvironmentOverrides CodePackageRef="FrontendService.Code">
                <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvcName]"/>
                <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
            </EnvironmentOverrides>
            <Policies>
                <ResourceGovernancePolicy CodePackageRef="Code" CpuShares="500" MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
                <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                    <RepositoryCredentials AccountName="username" Password="****" PasswordEncrypted="true"/>
                    <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
                </ContainerHostPolicies>
            </Policies>
        </ServiceManifestImport>
    </ApplicationManifest>
```

<span data-ttu-id="65fae-213">（在 hello 前面應用程式資訊清單中指定） 的範例服務資訊清單如下：</span><span class="sxs-lookup"><span data-stu-id="65fae-213">An example service manifest (specified in hello preceding application manifest) follows:</span></span>

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description> A service that implements a stateless front end in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
        <ConfigPackage Name="FrontendService.Config" Version="1.0" />
        <DataPackage Name="FrontendService.Data" Version="1.0" />
        <Resources>
            <Endpoints>
                <Endpoint Name="Endpoint1" UriScheme="http" Port="80" Protocol="http"/>
            </Endpoints>
        </Resources>
    </ServiceManifest>
```

## <a name="next-steps"></a><span data-ttu-id="65fae-214">後續步驟</span><span class="sxs-lookup"><span data-stu-id="65fae-214">Next steps</span></span>
<span data-ttu-id="65fae-215">既然您已部署的容器化的服務，了解如何 toomanage 藉由讀取週期[Service Fabric 應用程式生命週期](service-fabric-application-lifecycle.md)。</span><span class="sxs-lookup"><span data-stu-id="65fae-215">Now that you have deployed a containerized service, learn how toomanage its lifecycle by reading [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span></span>

* [<span data-ttu-id="65fae-216">Service Fabric 和容器的概觀</span><span class="sxs-lookup"><span data-stu-id="65fae-216">Overview of Service Fabric and containers</span></span>](service-fabric-containers-overview.md)
* <span data-ttu-id="65fae-217">如需範例，請查看 [GitHub 上的 Service Fabric 容器程式碼範例](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="65fae-217">For an example, checkout [Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>
