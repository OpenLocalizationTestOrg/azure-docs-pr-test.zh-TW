---
title: "aaaService 網狀架構和部署的容器，在 Linux 中 |Microsoft 文件"
description: "Service Fabric 和 hello 使用 Linux 容器 toodeploy 微服務應用程式。 本文說明 Service Fabric 提供容器和如何 toodeploy Linux 容器映像到叢集中的 hello 功能"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 4ba99103-6064-429d-ba17-82861b6ddb11
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: msfussell
ms.openlocfilehash: e28f99a145b0594d871b0ec0566233a7ad235ce8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-linux-container-tooservice-fabric"></a><span data-ttu-id="3b900-104">部署 Linux 容器 tooService 網狀架構</span><span class="sxs-lookup"><span data-stu-id="3b900-104">Deploy a Linux container tooService Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3b900-105">部署 Windows 容器</span><span class="sxs-lookup"><span data-stu-id="3b900-105">Deploy Windows Container</span></span>](service-fabric-deploy-container.md)
> * [<span data-ttu-id="3b900-106">部署 Linux 容器</span><span class="sxs-lookup"><span data-stu-id="3b900-106">Deploy Linux Container</span></span>](service-fabric-deploy-container-linux.md)
>
>

<span data-ttu-id="3b900-107">本文將引導您在 Linux 上的 Docker 容器中建置容器化服務。</span><span class="sxs-lookup"><span data-stu-id="3b900-107">This article walks you through building containerized services in Docker containers on Linux.</span></span>

<span data-ttu-id="3b900-108">Service Fabric 有數個容器功能可協助您建置由容器化微服務組成的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3b900-108">Service Fabric has several container capabilities that help you with building applications that are composed of microservices that are containerized.</span></span> <span data-ttu-id="3b900-109">這些服務稱為容器化服務。</span><span class="sxs-lookup"><span data-stu-id="3b900-109">These services are called containerized services.</span></span>

<span data-ttu-id="3b900-110">hello 功能包括：</span><span class="sxs-lookup"><span data-stu-id="3b900-110">hello capabilities include;</span></span>

* <span data-ttu-id="3b900-111">容器映像部署和啟用</span><span class="sxs-lookup"><span data-stu-id="3b900-111">Container image deployment and activation</span></span>
* <span data-ttu-id="3b900-112">資源管理</span><span class="sxs-lookup"><span data-stu-id="3b900-112">Resource governance</span></span>
* <span data-ttu-id="3b900-113">儲存機制驗證</span><span class="sxs-lookup"><span data-stu-id="3b900-113">Repository authentication</span></span>
* <span data-ttu-id="3b900-114">容器連接埠 toohost 連接埠對應</span><span class="sxs-lookup"><span data-stu-id="3b900-114">Container port toohost port mapping</span></span>
* <span data-ttu-id="3b900-115">容器至容器的探索及通訊</span><span class="sxs-lookup"><span data-stu-id="3b900-115">Container-to-container discovery and communication</span></span>
* <span data-ttu-id="3b900-116">能力 tooconfigure 並設定環境變數</span><span class="sxs-lookup"><span data-stu-id="3b900-116">Ability tooconfigure and set environment variables</span></span>

## <a name="packaging-a-docker-container-with-yeoman"></a><span data-ttu-id="3b900-117">使用 Yeoman 封裝 Docker 容器</span><span class="sxs-lookup"><span data-stu-id="3b900-117">Packaging a docker container with yeoman</span></span>
<span data-ttu-id="3b900-118">當封裝在 Linux 上的容器，您可以選擇任一 toouse yeoman 範本或[手動建立 hello 應用程式封裝](#manually)。</span><span class="sxs-lookup"><span data-stu-id="3b900-118">When packaging a container on Linux, you can choose either toouse a yeoman template or [create hello application package manually](#manually).</span></span>

<span data-ttu-id="3b900-119">Service Fabric 應用程式可以包含一個或多個容器，每個都有特定角色中傳送嗨應用程式的功能。</span><span class="sxs-lookup"><span data-stu-id="3b900-119">A Service Fabric application can contain one or more containers, each with a specific role in delivering hello application's functionality.</span></span> <span data-ttu-id="3b900-120">hello Service Fabric SDK for Linux 包含[Yeoman](http://yeoman.io/)產生器，可讓您輕鬆 toocreate 您的應用程式並加入容器映像。</span><span class="sxs-lookup"><span data-stu-id="3b900-120">hello Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy toocreate your application and add a container image.</span></span> <span data-ttu-id="3b900-121">讓我們使用具有單一的 Docker 容器的應用程式呼叫 Yeoman toocreate *SimpleContainerApp*。</span><span class="sxs-lookup"><span data-stu-id="3b900-121">Let's use Yeoman toocreate an application with a single Docker container called *SimpleContainerApp*.</span></span> <span data-ttu-id="3b900-122">您可以稍後新增更多服務，藉由編輯 hello 產生資訊清單檔案。</span><span class="sxs-lookup"><span data-stu-id="3b900-122">You can add more services later by editing hello generated manifest files.</span></span>

## <a name="install-docker-on-your-development-box"></a><span data-ttu-id="3b900-123">在您的開發電腦上安裝 Docker</span><span class="sxs-lookup"><span data-stu-id="3b900-123">Install Docker on your development box</span></span>

<span data-ttu-id="3b900-124">Hello 執行的下列命令 tooinstall Linux 開發機器上的 docker （如果您在 OSX 上使用 hello vagrant 映像，docker 已安裝）：</span><span class="sxs-lookup"><span data-stu-id="3b900-124">Run hello following commands tooinstall docker on your Linux development box (if you are using hello vagrant image on OSX, docker is already installed):</span></span>

```bash
    sudo apt-get install wget
    wget -qO- https://get.docker.io/ | sh
```

## <a name="create-hello-application"></a><span data-ttu-id="3b900-125">建立 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="3b900-125">Create hello application</span></span>
1. <span data-ttu-id="3b900-126">在終端機中，輸入 `yo azuresfcontainer`。</span><span class="sxs-lookup"><span data-stu-id="3b900-126">In a terminal, type `yo azuresfcontainer`.</span></span>
2. <span data-ttu-id="3b900-127">為應用程式命名，例如 mycontainerap</span><span class="sxs-lookup"><span data-stu-id="3b900-127">Name your application - for example, mycontainerap</span></span>
3. <span data-ttu-id="3b900-128">提供從 DockerHub 儲存機制的 hello 容器映像 hello URL。</span><span class="sxs-lookup"><span data-stu-id="3b900-128">Provide hello URL for hello container image from a DockerHub repo.</span></span> <span data-ttu-id="3b900-129">hello 映像參數會採用 hello 表單 [儲存機制] / [映像名稱]</span><span class="sxs-lookup"><span data-stu-id="3b900-129">hello image parameter takes hello form [repo]/[image name]</span></span>
4. <span data-ttu-id="3b900-130">如果 hello 映像沒有定義，為工作負載進入點，則您需要 tooexplicitly 輸入的命令以逗號分隔一組指定命令 toorun hello 容器，將會保留在啟動之後執行的 hello 容器內。</span><span class="sxs-lookup"><span data-stu-id="3b900-130">If hello image does not have a workload entry-point defined, then you need tooexplicitly specify input commands with a comma-delimited set of commands toorun inside hello container, which will keep hello container running after startup.</span></span>

![容器的 Service Fabric Yeoman 產生器][sf-yeoman]

## <a name="deploy-hello-application"></a><span data-ttu-id="3b900-132">部署 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="3b900-132">Deploy hello application</span></span>

### <a name="using-xplat-cli"></a><span data-ttu-id="3b900-133">使用 XPlat CLI</span><span class="sxs-lookup"><span data-stu-id="3b900-133">Using XPlat CLI</span></span>
<span data-ttu-id="3b900-134">建置 hello 應用程式之後，您可以使用 Azure CLI hello toohello 本機叢集對它進行部署。</span><span class="sxs-lookup"><span data-stu-id="3b900-134">Once hello application is built, you can deploy it toohello local cluster using hello Azure CLI.</span></span>

1. <span data-ttu-id="3b900-135">Toohello 本機 Service Fabric 叢集連線。</span><span class="sxs-lookup"><span data-stu-id="3b900-135">Connect toohello local Service Fabric cluster.</span></span>

    ```bash
    azure servicefabric cluster connect
    ```

2. <span data-ttu-id="3b900-136">使用 hello 安裝指令碼，提供在 hello 範本 toocopy hello 應用程式封裝 toohello 叢集映像存放區、 註冊 hello 應用程式類型，以及建立 hello 應用程式的執行個體。</span><span class="sxs-lookup"><span data-stu-id="3b900-136">Use hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

    ```bash
    ./install.sh
    ```

3. <span data-ttu-id="3b900-137">開啟瀏覽器，並瀏覽 tooService Fabric 總管在 http://localhost:19080 總管 (hello 私用 ip 的 hello VM，如果在 Mac OS X 使用 Vagrant 取代 localhost)。</span><span class="sxs-lookup"><span data-stu-id="3b900-137">Open a browser and navigate tooService Fabric Explorer at http://localhost:19080/Explorer (replace localhost with hello private IP of hello VM if using Vagrant on Mac OS X).</span></span>
4. <span data-ttu-id="3b900-138">展開 [hello 應用程式] 節點，請注意，現在您的應用程式類型的項目，另一個用於 hello 該類型的第一個執行個體。</span><span class="sxs-lookup"><span data-stu-id="3b900-138">Expand hello Applications node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>
5. <span data-ttu-id="3b900-139">使用 hello 解除安裝指令碼 hello 範本 toodelete hello 應用程式執行個體中所提供，並取消登錄 hello 應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="3b900-139">Use hello uninstall script provided in hello template toodelete hello application instance and unregister hello application type.</span></span>

    ```bash
    ./uninstall.sh
    ```

### <a name="using-azure-cli-20"></a><span data-ttu-id="3b900-140">使用 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3b900-140">Using Azure CLI 2.0</span></span>

<span data-ttu-id="3b900-141">請參閱 hello 參考文件管理[應用程式生命週期使用 hello Azure CLI 2.0](service-fabric-application-lifecycle-azure-cli-2-0.md)。</span><span class="sxs-lookup"><span data-stu-id="3b900-141">See hello reference doc on managing an [application life cycle using hello Azure CLI 2.0](service-fabric-application-lifecycle-azure-cli-2-0.md).</span></span>

<span data-ttu-id="3b900-142">範例應用程式， [GitHub 上的簽出 hello Service Fabric 容器程式碼範例](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="3b900-142">For an example application, [checkout hello Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>

## <a name="adding-more-services-tooan-existing-application"></a><span data-ttu-id="3b900-143">新增更多服務 tooan 現有應用程式</span><span class="sxs-lookup"><span data-stu-id="3b900-143">Adding more services tooan existing application</span></span>

<span data-ttu-id="3b900-144">tooadd 另一個容器服務 tooan 應用程式使用已建立`yo`，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="3b900-144">tooadd another container service tooan application already created using `yo`, perform hello following steps:</span></span>

1. <span data-ttu-id="3b900-145">變更 hello 現有應用程式的根目錄 toohello。</span><span class="sxs-lookup"><span data-stu-id="3b900-145">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="3b900-146">例如， `cd ~/YeomanSamples/MyApplication`，如果`MyApplication`是 hello Yeoman 所建立的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3b900-146">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="3b900-147">執行 `yo azuresfcontainer:AddService`</span><span class="sxs-lookup"><span data-stu-id="3b900-147">Run `yo azuresfcontainer:AddService`</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a><span data-ttu-id="3b900-148">手動封裝和部署容器映像</span><span class="sxs-lookup"><span data-stu-id="3b900-148">Manually package and deploy a container image</span></span>
<span data-ttu-id="3b900-149">hello 程序手動封裝進行容器化的服務根據 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3b900-149">hello process of manually packaging a containerized service is based on hello following steps:</span></span>

1. <span data-ttu-id="3b900-150">發行 hello 容器 tooyour 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="3b900-150">Publish hello containers tooyour repository.</span></span>
2. <span data-ttu-id="3b900-151">建立 hello 封裝目錄結構。</span><span class="sxs-lookup"><span data-stu-id="3b900-151">Create hello package directory structure.</span></span>
3. <span data-ttu-id="3b900-152">編輯 hello 服務資訊清單檔。</span><span class="sxs-lookup"><span data-stu-id="3b900-152">Edit hello service manifest file.</span></span>
4. <span data-ttu-id="3b900-153">編輯 hello 應用程式資訊清單檔案。</span><span class="sxs-lookup"><span data-stu-id="3b900-153">Edit hello application manifest file.</span></span>

## <a name="deploy-and-activate-a-container-image"></a><span data-ttu-id="3b900-154">部署和啟用容器映像</span><span class="sxs-lookup"><span data-stu-id="3b900-154">Deploy and activate a container image</span></span>
<span data-ttu-id="3b900-155">在 hello Service Fabric[應用程式模型](service-fabric-application-model.md)，容器代表複本會放在哪一種多個服務應用程式主機。</span><span class="sxs-lookup"><span data-stu-id="3b900-155">In hello Service Fabric [application model](service-fabric-application-model.md), a container represents an application host in which multiple service replicas are placed.</span></span> <span data-ttu-id="3b900-156">toodeploy 並啟動容器，put 的 hello 名稱 hello 容器映像到`ContainerHost`hello 服務資訊清單中的項目。</span><span class="sxs-lookup"><span data-stu-id="3b900-156">toodeploy and activate a container, put hello name of hello container image into a `ContainerHost` element in hello service manifest.</span></span>

<span data-ttu-id="3b900-157">在 hello 服務資訊清單中，加入`ContainerHost`hello 進入點。</span><span class="sxs-lookup"><span data-stu-id="3b900-157">In hello service manifest, add a `ContainerHost` for hello entry point.</span></span> <span data-ttu-id="3b900-158">然後組 hello `ImageName` toobe hello 名稱 hello 容器儲存機制和映像。</span><span class="sxs-lookup"><span data-stu-id="3b900-158">Then set hello `ImageName` toobe hello name of hello container repository and image.</span></span> <span data-ttu-id="3b900-159">hello 下列部分的資訊清單示範如何呼叫 toodeploy hello 容器`myimage:v1`從儲存機制稱為`myrepo`:</span><span class="sxs-lookup"><span data-stu-id="3b900-159">hello following partial manifest shows an example of how toodeploy hello container called `myimage:v1` from a repository called `myrepo`:</span></span>

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

<span data-ttu-id="3b900-160">您可以提供輸入的命令，藉由指定選擇性的 hello`Commands`組逗號分隔的命令 toorun hello 容器內的項目。</span><span class="sxs-lookup"><span data-stu-id="3b900-160">You can provide input commands by specifying hello optional `Commands` element with a comma-delimited set of commands toorun inside hello container.</span></span>

> [!NOTE]
> <span data-ttu-id="3b900-161">如果 hello 映像沒有定義，為工作負載進入點，則您需要 tooexplicitly 指定內輸入的命令`Commands`組逗號分隔的命令 toorun hello 容器，將會保留執行的 hello 容器內的項目啟動。</span><span class="sxs-lookup"><span data-stu-id="3b900-161">If hello image does not have a workload entry-point defined, then you need tooexplicitly specify input commands inside `Commands` element with a comma-delimited set of commands toorun inside hello container, which will keep hello container running after startup.</span></span>

## <a name="understand-resource-governance"></a><span data-ttu-id="3b900-162">了解資源管理</span><span class="sxs-lookup"><span data-stu-id="3b900-162">Understand resource governance</span></span>
<span data-ttu-id="3b900-163">資源管理機制是，限制 hello 容器的 hello 資源 hello 容器的功能可以使用 hello 主機上。</span><span class="sxs-lookup"><span data-stu-id="3b900-163">Resource governance is a capability of hello container that restricts hello resources that hello container can use on hello host.</span></span> <span data-ttu-id="3b900-164">hello `ResourceGovernancePolicy`，其中指定 hello 應用程式資訊清單中的就是使用的 toodeclare 資源限制，服務程式碼封裝。</span><span class="sxs-lookup"><span data-stu-id="3b900-164">hello `ResourceGovernancePolicy`, which is specified in hello application manifest is used toodeclare resource limits for a service code package.</span></span> <span data-ttu-id="3b900-165">您可以設定資源限制 hello 下列資源：</span><span class="sxs-lookup"><span data-stu-id="3b900-165">Resource limits can be set for hello following resources:</span></span>

* <span data-ttu-id="3b900-166">記憶體</span><span class="sxs-lookup"><span data-stu-id="3b900-166">Memory</span></span>
* <span data-ttu-id="3b900-167">MemorySwap</span><span class="sxs-lookup"><span data-stu-id="3b900-167">MemorySwap</span></span>
* <span data-ttu-id="3b900-168">CpuShares (CPU 相對權數)</span><span class="sxs-lookup"><span data-stu-id="3b900-168">CpuShares (CPU relative weight)</span></span>
* <span data-ttu-id="3b900-169">MemoryReservationInMB</span><span class="sxs-lookup"><span data-stu-id="3b900-169">MemoryReservationInMB</span></span>  
* <span data-ttu-id="3b900-170">BlkioWeight (BlockIO 相對權數)。</span><span class="sxs-lookup"><span data-stu-id="3b900-170">BlkioWeight (BlockIO relative weight).</span></span>

> [!NOTE]
> <span data-ttu-id="3b900-171">在未來版本中，會加入支援指定特定的區塊 IO 限制，例如 IOP、讀取/寫入 BPS 及其他限制。</span><span class="sxs-lookup"><span data-stu-id="3b900-171">In a future release, support for specifying specific block IO limits such as IOPs, read/write BPS, and others will be included.</span></span>
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

## <a name="authenticate-a-repository"></a><span data-ttu-id="3b900-172">驗證儲存機制</span><span class="sxs-lookup"><span data-stu-id="3b900-172">Authenticate a repository</span></span>
<span data-ttu-id="3b900-173">toodownload 容器，您可能必須 tooprovide 登入認證 toohello 容器儲存機制。</span><span class="sxs-lookup"><span data-stu-id="3b900-173">toodownload a container, you might have tooprovide sign-in credentials toohello container repository.</span></span> <span data-ttu-id="3b900-174">hello 登入認證，在 hello 應用程式資訊清單中指定會使用的 toospecify hello 登入資訊或下載 hello 容器映像從 hello 映像儲存機制的 SSH 金鑰。</span><span class="sxs-lookup"><span data-stu-id="3b900-174">hello sign-in credentials, specified in hello application manifest, are used toospecify hello sign-in information, or SSH key, for downloading hello container image from hello image repository.</span></span> <span data-ttu-id="3b900-175">hello 下列範例將示範名為帳戶*TestUser*以及 hello 密碼以純文字 (*不*建議使用):</span><span class="sxs-lookup"><span data-stu-id="3b900-175">hello following example shows an account called *TestUser* along with hello password in clear text (*not* recommended):</span></span>

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

<span data-ttu-id="3b900-176">我們建議您在使用已部署 toohello 機器的憑證來加密 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="3b900-176">We recommend that you encrypt hello password by using a certificate that's deployed toohello machine.</span></span>

<span data-ttu-id="3b900-177">hello 下列範例將示範名為帳戶*TestUser*、 其中 hello 密碼加密所使用的憑證稱為*MyCert*。</span><span class="sxs-lookup"><span data-stu-id="3b900-177">hello following example shows an account called *TestUser*, where hello password was encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="3b900-178">您可以使用 hello `Invoke-ServiceFabricEncryptText` PowerShell 命令 toocreate hello 密碼加密文字 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="3b900-178">You can use hello `Invoke-ServiceFabricEncryptText` PowerShell command toocreate hello secret cipher text for hello password.</span></span> <span data-ttu-id="3b900-179">如需詳細資訊，請參閱 hello 文章[管理 Service Fabric 應用程式中的機密](service-fabric-application-secret-management.md)。</span><span class="sxs-lookup"><span data-stu-id="3b900-179">For more information, see hello article [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md).</span></span>

<span data-ttu-id="3b900-180">hello hello 憑證私密金鑰用 toodecrypt hello 密碼必須是已部署的 toohello 本機電腦的頻外方法中。</span><span class="sxs-lookup"><span data-stu-id="3b900-180">hello private key of hello certificate that's used toodecrypt hello password must be deployed toohello local machine in an out-of-band method.</span></span> <span data-ttu-id="3b900-181">(在 Azure 中，這個方法就是 Azure Resource Manager。)然後，當 Service Fabric 部署 hello 服務封裝 toohello 機器，它可以解密 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="3b900-181">(In Azure, this method is Azure Resource Manager.) Then, when Service Fabric deploys hello service package toohello machine, it can decrypt hello secret.</span></span> <span data-ttu-id="3b900-182">藉由使用 hello 密碼以及 hello 帳戶名稱，它可以再向 hello 容器儲存機制。</span><span class="sxs-lookup"><span data-stu-id="3b900-182">By using hello secret along with hello account name, it can then authenticate with hello container repository.</span></span>

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

## <a name="configure-container-port-to-host-port-mapping"></a><span data-ttu-id="3b900-183">設定容器連接埠至主機連接埠的對應</span><span class="sxs-lookup"><span data-stu-id="3b900-183">Configure container port-to-host port mapping</span></span>
<span data-ttu-id="3b900-184">您也可以指定與 hello 容器設定主機使用的連接埠 toocommunicate `PortBinding` hello 應用程式資訊清單中。</span><span class="sxs-lookup"><span data-stu-id="3b900-184">You can configure a host port used toocommunicate with hello container by specifying a `PortBinding` in hello application manifest.</span></span> <span data-ttu-id="3b900-185">hello 連接埠繫結對應 hello 連接埠 toowhich hello 服務會接聽內部 hello 主機上的 hello 容器 tooa 通訊埠。</span><span class="sxs-lookup"><span data-stu-id="3b900-185">hello port binding maps hello port toowhich hello service is listening inside hello container tooa port on hello host.</span></span>

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

## <a name="configure-container-to-container-discovery-and-communication"></a><span data-ttu-id="3b900-186">設定容器至容器的探索及通訊</span><span class="sxs-lookup"><span data-stu-id="3b900-186">Configure container-to-container discovery and communication</span></span>
<span data-ttu-id="3b900-187">使用 hello`PortBinding`原則，您可以將對應的容器連接埠 tooan `Endpoint` hello 服務資訊清單中。</span><span class="sxs-lookup"><span data-stu-id="3b900-187">By using hello `PortBinding` policy, you can map a container port tooan `Endpoint` in hello service manifest.</span></span> <span data-ttu-id="3b900-188">hello 端點`Endpoint1`可以指定固定通訊埠 （例如，連接埠 80）。</span><span class="sxs-lookup"><span data-stu-id="3b900-188">hello endpoint `Endpoint1` can specify a fixed port (for example, port 80).</span></span> <span data-ttu-id="3b900-189">也可以指定任何連接埠，在此情況下針對您選擇 hello 叢集應用程式連接埠範圍的隨機連接埠。</span><span class="sxs-lookup"><span data-stu-id="3b900-189">It can also specify no port at all, in which case a random port from hello cluster's application port range is chosen for you.</span></span>

<span data-ttu-id="3b900-190">如果您指定端點，使用 hello `Endpoint` hello 客體容器，Service Fabric 服務資訊清單中的標記可以自動發佈此端點 toohello 命名服務。</span><span class="sxs-lookup"><span data-stu-id="3b900-190">If you specify an endpoint, using hello `Endpoint` tag in hello service manifest of a guest container, Service Fabric can automatically publish this endpoint toohello Naming service.</span></span> <span data-ttu-id="3b900-191">因此，hello 叢集中執行的其他服務可以探索使用 hello REST 查詢以解析此容器。</span><span class="sxs-lookup"><span data-stu-id="3b900-191">Other services that are running in hello cluster can thus discover this container using hello REST queries for resolving.</span></span>

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

<span data-ttu-id="3b900-192">以 hello 命名服務註冊，步驟很容易在 hello 程式碼中的容器-容器通訊您容器內使用 hello[反向 proxy](service-fabric-reverseproxy.md)。</span><span class="sxs-lookup"><span data-stu-id="3b900-192">By registering with hello Naming service, you can easily do container-to-container communication in hello code within your container by using hello [reverse proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="3b900-193">通訊是由提供 hello 反向 proxy http 接聽連接埠和 hello 名稱要與 toocommunicate 視為環境變數的 hello 服務執行。</span><span class="sxs-lookup"><span data-stu-id="3b900-193">Communication is performed by providing hello reverse proxy http listening port and hello name of hello services that you want toocommunicate with as environment variables.</span></span> <span data-ttu-id="3b900-194">如需詳細資訊，請參閱 hello 下一節。</span><span class="sxs-lookup"><span data-stu-id="3b900-194">For more information, see hello next section.</span></span>

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="3b900-195">設定環境變數</span><span class="sxs-lookup"><span data-stu-id="3b900-195">Configure and set environment variables</span></span>
<span data-ttu-id="3b900-196">環境變數可以指定每個程式碼封裝中的 hello 服務資訊，同時在容器中部署的服務或服務與處理程序/客體可執行檔部署。</span><span class="sxs-lookup"><span data-stu-id="3b900-196">Environment variables can be specified for each code package in hello service manifest, both for services that are deployed in containers or for services that are deployed as processes/guest executables.</span></span> <span data-ttu-id="3b900-197">這些環境變數的值可以覆寫，特別是在 hello 應用程式資訊清單或做為應用程式參數的部署期間指定。</span><span class="sxs-lookup"><span data-stu-id="3b900-197">These environment variable values can be overridden specifically in hello application manifest or specified during deployment as application parameters.</span></span>

<span data-ttu-id="3b900-198">hello 下列服務資訊清單 XML 程式碼片段示範如何的範例程式碼封裝的 toospecify 環境變數：</span><span class="sxs-lookup"><span data-stu-id="3b900-198">hello following service manifest XML snippet shows an example of how toospecify environment variables for a code package:</span></span>

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

<span data-ttu-id="3b900-199">這些環境變數會覆寫 hello 應用程式層級資訊清單：</span><span class="sxs-lookup"><span data-stu-id="3b900-199">These environment variables can be overridden at hello application manifest level:</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

<span data-ttu-id="3b900-200">在 hello 前一個範例中，我們已指定明確的值為 hello`HttpGateway`環境變數 (19000)，而我們將設定為 hello 值`BackendServiceName`參數透過 hello`[BackendSvc]`應用程式參數。</span><span class="sxs-lookup"><span data-stu-id="3b900-200">In hello previous example, we specified an explicit value for hello `HttpGateway` environment variable (19000), while we set hello value for `BackendServiceName` parameter via hello `[BackendSvc]` application parameter.</span></span> <span data-ttu-id="3b900-201">這些設定可讓您 toospecify hello 值`BackendServiceName`時部署 hello 應用程式和 hello 資訊清單中沒有固定的值的值。</span><span class="sxs-lookup"><span data-stu-id="3b900-201">These settings enable you toospecify hello value for `BackendServiceName`value when you deploy hello application and not have a fixed value in hello manifest.</span></span>

## <a name="complete-examples-for-application-and-service-manifest"></a><span data-ttu-id="3b900-202">應用程式和服務資訊清單的完整範例</span><span class="sxs-lookup"><span data-stu-id="3b900-202">Complete examples for application and service manifest</span></span>

<span data-ttu-id="3b900-203">以下是應用程式資訊清單：</span><span class="sxs-lookup"><span data-stu-id="3b900-203">An example application manifest follows:</span></span>

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

<span data-ttu-id="3b900-204">（在 hello 前面應用程式資訊清單中指定） 的範例服務資訊清單如下：</span><span class="sxs-lookup"><span data-stu-id="3b900-204">An example service manifest (specified in hello preceding application manifest) follows:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="3b900-205">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3b900-205">Next steps</span></span>
<span data-ttu-id="3b900-206">既然您已部署的容器化的服務，了解如何 toomanage 藉由讀取週期[Service Fabric 應用程式生命週期](service-fabric-application-lifecycle.md)。</span><span class="sxs-lookup"><span data-stu-id="3b900-206">Now that you have deployed a containerized service, learn how toomanage its lifecycle by reading [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span></span>

* [<span data-ttu-id="3b900-207">Service Fabric 和容器的概觀</span><span class="sxs-lookup"><span data-stu-id="3b900-207">Overview of Service Fabric and containers</span></span>](service-fabric-containers-overview.md)
* [<span data-ttu-id="3b900-208">互動使用 hello Azure CLI Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="3b900-208">Interacting with Service Fabric clusters using hello Azure CLI</span></span>](service-fabric-azure-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-deploy-container-linux/sf-container-yeoman1.png

## <a name="related-articles"></a><span data-ttu-id="3b900-209">相關文章</span><span class="sxs-lookup"><span data-stu-id="3b900-209">Related articles</span></span>

* [<span data-ttu-id="3b900-210">開始使用 Service Fabric 和 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3b900-210">Getting started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
* [<span data-ttu-id="3b900-211">開始使用 Service Fabric XPlat CLI</span><span class="sxs-lookup"><span data-stu-id="3b900-211">Getting started with Service Fabric XPlat CLI</span></span>](service-fabric-azure-cli.md)
