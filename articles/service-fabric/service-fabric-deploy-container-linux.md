---
title: "Service Fabric 以及在 Linux 中部署容器 | Microsoft Docs"
description: "Service Fabric 以及使用 Linux 容器來部署微服務應用程式。 本文說明 Service Fabric 為容器提供的功能，以及如何將 Linux 容器映像部署至叢集"
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
ms.openlocfilehash: 9dcec753e5f999a1bac07276373c0c25f89ec58d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-linux-container-to-service-fabric"></a><span data-ttu-id="d6b05-104">將 Linux 容器部署至 Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d6b05-104">Deploy a Linux container to Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d6b05-105">部署 Windows 容器</span><span class="sxs-lookup"><span data-stu-id="d6b05-105">Deploy Windows Container</span></span>](service-fabric-deploy-container.md)
> * [<span data-ttu-id="d6b05-106">部署 Linux 容器</span><span class="sxs-lookup"><span data-stu-id="d6b05-106">Deploy Linux Container</span></span>](service-fabric-deploy-container-linux.md)
>
>

<span data-ttu-id="d6b05-107">本文將引導您在 Linux 上的 Docker 容器中建置容器化服務。</span><span class="sxs-lookup"><span data-stu-id="d6b05-107">This article walks you through building containerized services in Docker containers on Linux.</span></span>

<span data-ttu-id="d6b05-108">Service Fabric 有數個容器功能可協助您建置由容器化微服務組成的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d6b05-108">Service Fabric has several container capabilities that help you with building applications that are composed of microservices that are containerized.</span></span> <span data-ttu-id="d6b05-109">這些服務稱為容器化服務。</span><span class="sxs-lookup"><span data-stu-id="d6b05-109">These services are called containerized services.</span></span>

<span data-ttu-id="d6b05-110">功能包括：</span><span class="sxs-lookup"><span data-stu-id="d6b05-110">The capabilities include;</span></span>

* <span data-ttu-id="d6b05-111">容器映像部署和啟用</span><span class="sxs-lookup"><span data-stu-id="d6b05-111">Container image deployment and activation</span></span>
* <span data-ttu-id="d6b05-112">資源管理</span><span class="sxs-lookup"><span data-stu-id="d6b05-112">Resource governance</span></span>
* <span data-ttu-id="d6b05-113">儲存機制驗證</span><span class="sxs-lookup"><span data-stu-id="d6b05-113">Repository authentication</span></span>
* <span data-ttu-id="d6b05-114">容器連接埠至主機連接埠的對應</span><span class="sxs-lookup"><span data-stu-id="d6b05-114">Container port to host port mapping</span></span>
* <span data-ttu-id="d6b05-115">容器至容器的探索及通訊</span><span class="sxs-lookup"><span data-stu-id="d6b05-115">Container-to-container discovery and communication</span></span>
* <span data-ttu-id="d6b05-116">能夠設定環境變數</span><span class="sxs-lookup"><span data-stu-id="d6b05-116">Ability to configure and set environment variables</span></span>

## <a name="packaging-a-docker-container-with-yeoman"></a><span data-ttu-id="d6b05-117">使用 Yeoman 封裝 Docker 容器</span><span class="sxs-lookup"><span data-stu-id="d6b05-117">Packaging a docker container with yeoman</span></span>
<span data-ttu-id="d6b05-118">在 Linux 上封裝容器時，您可以選擇使用 Yeoman 範本，或是[手動建立應用程式套件](#manually)。</span><span class="sxs-lookup"><span data-stu-id="d6b05-118">When packaging a container on Linux, you can choose either to use a yeoman template or [create the application package manually](#manually).</span></span>

<span data-ttu-id="d6b05-119">Service Fabric 應用程式可以包含一或多個容器，而每個容器在提供應用程式的功能時都有特定角色。</span><span class="sxs-lookup"><span data-stu-id="d6b05-119">A Service Fabric application can contain one or more containers, each with a specific role in delivering the application's functionality.</span></span> <span data-ttu-id="d6b05-120">適用於 Linux 的 Service Fabric SDK 包含 [Yeoman](http://yeoman.io/) 產生器，可讓您輕鬆建立應用程式並新增容器映像。</span><span class="sxs-lookup"><span data-stu-id="d6b05-120">The Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy to create your application and add a container image.</span></span> <span data-ttu-id="d6b05-121">讓我們使用 Yeoman 來建立具有單一 Docker 容器，名為 *SimpleContainerApp* 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d6b05-121">Let's use Yeoman to create an application with a single Docker container called *SimpleContainerApp*.</span></span> <span data-ttu-id="d6b05-122">您可以在稍後編輯產生的資訊清單檔案來新增更多服務。</span><span class="sxs-lookup"><span data-stu-id="d6b05-122">You can add more services later by editing the generated manifest files.</span></span>

## <a name="install-docker-on-your-development-box"></a><span data-ttu-id="d6b05-123">在您的開發電腦上安裝 Docker</span><span class="sxs-lookup"><span data-stu-id="d6b05-123">Install Docker on your development box</span></span>

<span data-ttu-id="d6b05-124">執行下列命令以在您的 Linux 開發電腦上安裝 Docker (如果您是使用 OSX 上的 Vagrant 映像，則 Docker 已經安裝)：</span><span class="sxs-lookup"><span data-stu-id="d6b05-124">Run the following commands to install docker on your Linux development box (if you are using the vagrant image on OSX, docker is already installed):</span></span>

```bash
    sudo apt-get install wget
    wget -qO- https://get.docker.io/ | sh
```

## <a name="create-the-application"></a><span data-ttu-id="d6b05-125">建立應用程式</span><span class="sxs-lookup"><span data-stu-id="d6b05-125">Create the application</span></span>
1. <span data-ttu-id="d6b05-126">在終端機中，輸入 `yo azuresfcontainer`。</span><span class="sxs-lookup"><span data-stu-id="d6b05-126">In a terminal, type `yo azuresfcontainer`.</span></span>
2. <span data-ttu-id="d6b05-127">為應用程式命名，例如 mycontainerap</span><span class="sxs-lookup"><span data-stu-id="d6b05-127">Name your application - for example, mycontainerap</span></span>
3. <span data-ttu-id="d6b05-128">從 DockerHub 儲存機制提供容器映像的 URL。</span><span class="sxs-lookup"><span data-stu-id="d6b05-128">Provide the URL for the container image from a DockerHub repo.</span></span> <span data-ttu-id="d6b05-129">映像參數的格式為 [儲存機制]/[映像名稱]</span><span class="sxs-lookup"><span data-stu-id="d6b05-129">The image parameter takes the form [repo]/[image name]</span></span>
4. <span data-ttu-id="d6b05-130">如果映像沒有已定義的工作負載進入點，您就必須使用一組要在容器內執行的命令 (以逗號分隔) 來明確指定輸入命令，這會讓容器在啟動後繼續執行。</span><span class="sxs-lookup"><span data-stu-id="d6b05-130">If the image does not have a workload entry-point defined, then you need to explicitly specify input commands with a comma-delimited set of commands to run inside the container, which will keep the container running after startup.</span></span>

![容器的 Service Fabric Yeoman 產生器][sf-yeoman]

## <a name="deploy-the-application"></a><span data-ttu-id="d6b05-132">部署應用程式</span><span class="sxs-lookup"><span data-stu-id="d6b05-132">Deploy the application</span></span>

### <a name="using-xplat-cli"></a><span data-ttu-id="d6b05-133">使用 XPlat CLI</span><span class="sxs-lookup"><span data-stu-id="d6b05-133">Using XPlat CLI</span></span>
<span data-ttu-id="d6b05-134">建置應用程式後，可以使用 Azure CLI 將它部署到本機叢集。</span><span class="sxs-lookup"><span data-stu-id="d6b05-134">Once the application is built, you can deploy it to the local cluster using the Azure CLI.</span></span>

1. <span data-ttu-id="d6b05-135">連接到本機 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="d6b05-135">Connect to the local Service Fabric cluster.</span></span>

    ```bash
    azure servicefabric cluster connect
    ```

2. <span data-ttu-id="d6b05-136">使用範本中所提供的安裝指令碼，將應用程式套件複製到叢集的映像存放區、註冊應用程式類型，以及建立應用程式的執行個體。</span><span class="sxs-lookup"><span data-stu-id="d6b05-136">Use the install script provided in the template to copy the application package to the cluster's image store, register the application type, and create an instance of the application.</span></span>

    ```bash
    ./install.sh
    ```

3. <span data-ttu-id="d6b05-137">開啟瀏覽器並瀏覽至位於 http://localhost:19080/Explorer 的 Service Fabric Explorer (如果在 Mac OS X 上使用 Vagrant，請以 VM 的私人 IP 取代 localhost)。</span><span class="sxs-lookup"><span data-stu-id="d6b05-137">Open a browser and navigate to Service Fabric Explorer at http://localhost:19080/Explorer (replace localhost with the private IP of the VM if using Vagrant on Mac OS X).</span></span>
4. <span data-ttu-id="d6b05-138">展開 [應用程式] 節點，請注意，您的應用程式類型現在有一個項目，而另一個則是該類型的第一個執行個體。</span><span class="sxs-lookup"><span data-stu-id="d6b05-138">Expand the Applications node and note that there is now an entry for your application type and another for the first instance of that type.</span></span>
5. <span data-ttu-id="d6b05-139">使用範本中提供的解除安裝指令碼，刪除應用程式執行個體並取消註冊應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="d6b05-139">Use the uninstall script provided in the template to delete the application instance and unregister the application type.</span></span>

    ```bash
    ./uninstall.sh
    ```

### <a name="using-azure-cli-20"></a><span data-ttu-id="d6b05-140">使用 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d6b05-140">Using Azure CLI 2.0</span></span>

<span data-ttu-id="d6b05-141">請參閱有關[使用 Azure CLI 2.0 來管理應用程式生命週期](service-fabric-application-lifecycle-azure-cli-2-0.md)的參考文件。</span><span class="sxs-lookup"><span data-stu-id="d6b05-141">See the reference doc on managing an [application life cycle using the Azure CLI 2.0](service-fabric-application-lifecycle-azure-cli-2-0.md).</span></span>

<span data-ttu-id="d6b05-142">如需範例應用程式，請[查看 GitHub 上的 Service Fabric 容器程式碼範例 (英文)](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="d6b05-142">For an example application, [checkout the Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>

## <a name="adding-more-services-to-an-existing-application"></a><span data-ttu-id="d6b05-143">將更多服務新增至現有的應用程式</span><span class="sxs-lookup"><span data-stu-id="d6b05-143">Adding more services to an existing application</span></span>

<span data-ttu-id="d6b05-144">若要將其他容器服務新增至已使用 `yo` 建立的應用程式，請執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="d6b05-144">To add another container service to an application already created using `yo`, perform the following steps:</span></span>

1. <span data-ttu-id="d6b05-145">將目錄變更為現有應用程式的根目錄。</span><span class="sxs-lookup"><span data-stu-id="d6b05-145">Change directory to the root of the existing application.</span></span>  <span data-ttu-id="d6b05-146">例如，如果 `MyApplication` 是 Yeoman 所建立的應用程式，則為 `cd ~/YeomanSamples/MyApplication`。</span><span class="sxs-lookup"><span data-stu-id="d6b05-146">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is the application created by Yeoman.</span></span>
2. <span data-ttu-id="d6b05-147">執行 `yo azuresfcontainer:AddService`</span><span class="sxs-lookup"><span data-stu-id="d6b05-147">Run `yo azuresfcontainer:AddService`</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a><span data-ttu-id="d6b05-148">手動封裝和部署容器映像</span><span class="sxs-lookup"><span data-stu-id="d6b05-148">Manually package and deploy a container image</span></span>
<span data-ttu-id="d6b05-149">手動封裝容器化服務的程序是基於下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d6b05-149">The process of manually packaging a containerized service is based on the following steps:</span></span>

1. <span data-ttu-id="d6b05-150">將容器發佈至儲存機制。</span><span class="sxs-lookup"><span data-stu-id="d6b05-150">Publish the containers to your repository.</span></span>
2. <span data-ttu-id="d6b05-151">建立封裝目錄結構。</span><span class="sxs-lookup"><span data-stu-id="d6b05-151">Create the package directory structure.</span></span>
3. <span data-ttu-id="d6b05-152">編輯服務資訊清單檔。</span><span class="sxs-lookup"><span data-stu-id="d6b05-152">Edit the service manifest file.</span></span>
4. <span data-ttu-id="d6b05-153">編輯應用程式資訊清單檔。</span><span class="sxs-lookup"><span data-stu-id="d6b05-153">Edit the application manifest file.</span></span>

## <a name="deploy-and-activate-a-container-image"></a><span data-ttu-id="d6b05-154">部署和啟用容器映像</span><span class="sxs-lookup"><span data-stu-id="d6b05-154">Deploy and activate a container image</span></span>
<span data-ttu-id="d6b05-155">在 Service Fabric [應用程式模型](service-fabric-application-model.md)中，容器代表多個服務複本所在的應用程式主機。</span><span class="sxs-lookup"><span data-stu-id="d6b05-155">In the Service Fabric [application model](service-fabric-application-model.md), a container represents an application host in which multiple service replicas are placed.</span></span> <span data-ttu-id="d6b05-156">若要部署和啟用容器，請在服務資訊清單的 `ContainerHost` 元素中輸入容器映像的名稱。</span><span class="sxs-lookup"><span data-stu-id="d6b05-156">To deploy and activate a container, put the name of the container image into a `ContainerHost` element in the service manifest.</span></span>

<span data-ttu-id="d6b05-157">在服務資訊清單中，新增 `ContainerHost` 作為進入點。</span><span class="sxs-lookup"><span data-stu-id="d6b05-157">In the service manifest, add a `ContainerHost` for the entry point.</span></span> <span data-ttu-id="d6b05-158">然後將 `ImageName` 設為容器儲存機制和映像的名稱。</span><span class="sxs-lookup"><span data-stu-id="d6b05-158">Then set the `ImageName` to be the name of the container repository and image.</span></span> <span data-ttu-id="d6b05-159">下列的局部資訊清單示範如何從名為 `myrepo` 的儲存機制，部署名為 `myimage:v1` 的容器：</span><span class="sxs-lookup"><span data-stu-id="d6b05-159">The following partial manifest shows an example of how to deploy the container called `myimage:v1` from a repository called `myrepo`:</span></span>

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

<span data-ttu-id="d6b05-160">您可以指定選擇性 `Commands` 元素，以及一組要在容器內執行的命令 (以逗號分隔)，以提供輸入命令。</span><span class="sxs-lookup"><span data-stu-id="d6b05-160">You can provide input commands by specifying the optional `Commands` element with a comma-delimited set of commands to run inside the container.</span></span>

> [!NOTE]
> <span data-ttu-id="d6b05-161">如果映像沒有已定義的工作負載進入點，您就必須在 `Commands` 元素內使用一組要在容器內執行的命令 (以逗號分隔) 來明確指定輸入命令，這會讓容器在啟動後繼續執行。</span><span class="sxs-lookup"><span data-stu-id="d6b05-161">If the image does not have a workload entry-point defined, then you need to explicitly specify input commands inside `Commands` element with a comma-delimited set of commands to run inside the container, which will keep the container running after startup.</span></span>

## <a name="understand-resource-governance"></a><span data-ttu-id="d6b05-162">了解資源管理</span><span class="sxs-lookup"><span data-stu-id="d6b05-162">Understand resource governance</span></span>
<span data-ttu-id="d6b05-163">資源管理是容器的功能，可限制容器在主機上可使用的資源。</span><span class="sxs-lookup"><span data-stu-id="d6b05-163">Resource governance is a capability of the container that restricts the resources that the container can use on the host.</span></span> <span data-ttu-id="d6b05-164">應用程式資訊清單中指定的 `ResourceGovernancePolicy` 是用於宣告服務程式碼套件的資源限制。</span><span class="sxs-lookup"><span data-stu-id="d6b05-164">The `ResourceGovernancePolicy`, which is specified in the application manifest is used to declare resource limits for a service code package.</span></span> <span data-ttu-id="d6b05-165">可為以下資源設定限制：</span><span class="sxs-lookup"><span data-stu-id="d6b05-165">Resource limits can be set for the following resources:</span></span>

* <span data-ttu-id="d6b05-166">記憶體</span><span class="sxs-lookup"><span data-stu-id="d6b05-166">Memory</span></span>
* <span data-ttu-id="d6b05-167">MemorySwap</span><span class="sxs-lookup"><span data-stu-id="d6b05-167">MemorySwap</span></span>
* <span data-ttu-id="d6b05-168">CpuShares (CPU 相對權數)</span><span class="sxs-lookup"><span data-stu-id="d6b05-168">CpuShares (CPU relative weight)</span></span>
* <span data-ttu-id="d6b05-169">MemoryReservationInMB</span><span class="sxs-lookup"><span data-stu-id="d6b05-169">MemoryReservationInMB</span></span>  
* <span data-ttu-id="d6b05-170">BlkioWeight (BlockIO 相對權數)。</span><span class="sxs-lookup"><span data-stu-id="d6b05-170">BlkioWeight (BlockIO relative weight).</span></span>

> [!NOTE]
> <span data-ttu-id="d6b05-171">在未來版本中，會加入支援指定特定的區塊 IO 限制，例如 IOP、讀取/寫入 BPS 及其他限制。</span><span class="sxs-lookup"><span data-stu-id="d6b05-171">In a future release, support for specifying specific block IO limits such as IOPs, read/write BPS, and others will be included.</span></span>
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

## <a name="authenticate-a-repository"></a><span data-ttu-id="d6b05-172">驗證儲存機制</span><span class="sxs-lookup"><span data-stu-id="d6b05-172">Authenticate a repository</span></span>
<span data-ttu-id="d6b05-173">若要下載容器，您可能必須提供容器儲存機制的登入認證。</span><span class="sxs-lookup"><span data-stu-id="d6b05-173">To download a container, you might have to provide sign-in credentials to the container repository.</span></span> <span data-ttu-id="d6b05-174">於應用程式資訊清單中指定的登入認證，是用於指定從映像儲存機制下載容器映像所需的登入資訊 (或 SSH 金鑰)。</span><span class="sxs-lookup"><span data-stu-id="d6b05-174">The sign-in credentials, specified in the application manifest, are used to specify the sign-in information, or SSH key, for downloading the container image from the image repository.</span></span> <span data-ttu-id="d6b05-175">下列範例顯示名為 TestUser  的帳戶及純文字密碼 (「不」建議使用)：</span><span class="sxs-lookup"><span data-stu-id="d6b05-175">The following example shows an account called *TestUser* along with the password in clear text (*not* recommended):</span></span>

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

<span data-ttu-id="d6b05-176">我們建議使用部署至電腦的憑證將密碼加密。</span><span class="sxs-lookup"><span data-stu-id="d6b05-176">We recommend that you encrypt the password by using a certificate that's deployed to the machine.</span></span>

<span data-ttu-id="d6b05-177">下列範例顯示名為 TestUser 的帳戶，其密碼以名為 MyCert 的憑證加密。</span><span class="sxs-lookup"><span data-stu-id="d6b05-177">The following example shows an account called *TestUser*, where the password was encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="d6b05-178">您可以使用 `Invoke-ServiceFabricEncryptText` Powershell 命令來建立密碼的加密文字。</span><span class="sxs-lookup"><span data-stu-id="d6b05-178">You can use the `Invoke-ServiceFabricEncryptText` PowerShell command to create the secret cipher text for the password.</span></span> <span data-ttu-id="d6b05-179">如需詳細資訊，請參閱[管理 Service Fabric 應用程式中的密碼](service-fabric-application-secret-management.md)。</span><span class="sxs-lookup"><span data-stu-id="d6b05-179">For more information, see the article [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md).</span></span>

<span data-ttu-id="d6b05-180">用於解密密碼的憑證私密金鑰必須以頻外方法部署到本機電腦。</span><span class="sxs-lookup"><span data-stu-id="d6b05-180">The private key of the certificate that's used to decrypt the password must be deployed to the local machine in an out-of-band method.</span></span> <span data-ttu-id="d6b05-181">(在 Azure 中，這個方法就是 Azure Resource Manager。)然後，當 Service Fabric 將服務套件部署到電腦時，它可以解密密碼。</span><span class="sxs-lookup"><span data-stu-id="d6b05-181">(In Azure, this method is Azure Resource Manager.) Then, when Service Fabric deploys the service package to the machine, it can decrypt the secret.</span></span> <span data-ttu-id="d6b05-182">搭配使用帳戶名稱和密碼，之後可以用它向容器儲存機制提供驗證。</span><span class="sxs-lookup"><span data-stu-id="d6b05-182">By using the secret along with the account name, it can then authenticate with the container repository.</span></span>

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

## <a name="configure-container-port-to-host-port-mapping"></a><span data-ttu-id="d6b05-183">設定容器連接埠至主機連接埠的對應</span><span class="sxs-lookup"><span data-stu-id="d6b05-183">Configure container port-to-host port mapping</span></span>
<span data-ttu-id="d6b05-184">您可以在應用程式資訊清單中指定 `PortBinding`，以設定用來與容器通訊的主機連接埠。</span><span class="sxs-lookup"><span data-stu-id="d6b05-184">You can configure a host port used to communicate with the container by specifying a `PortBinding` in the application manifest.</span></span> <span data-ttu-id="d6b05-185">連接埠繫結會將服務在容器內接聽的連接埠，對應至主機上的連接埠。</span><span class="sxs-lookup"><span data-stu-id="d6b05-185">The port binding maps the port to which the service is listening inside the container to a port on the host.</span></span>

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

## <a name="configure-container-to-container-discovery-and-communication"></a><span data-ttu-id="d6b05-186">設定容器至容器的探索及通訊</span><span class="sxs-lookup"><span data-stu-id="d6b05-186">Configure container-to-container discovery and communication</span></span>
<span data-ttu-id="d6b05-187">使用 `PortBinding` 原則，可以將容器連接埠對應至服務資訊清單中的 `Endpoint`。</span><span class="sxs-lookup"><span data-stu-id="d6b05-187">By using the `PortBinding` policy, you can map a container port to an `Endpoint` in the service manifest.</span></span> <span data-ttu-id="d6b05-188">端點 `Endpoint1` 可以指定固定通訊埠 (例如，連接埠 80)。</span><span class="sxs-lookup"><span data-stu-id="d6b05-188">The endpoint `Endpoint1` can specify a fixed port (for example, port 80).</span></span> <span data-ttu-id="d6b05-189">也可以完全不指定連接埠，在此情況下，將從叢集的應用程式連接埠範圍內為您選擇隨機連接埠。</span><span class="sxs-lookup"><span data-stu-id="d6b05-189">It can also specify no port at all, in which case a random port from the cluster's application port range is chosen for you.</span></span>

<span data-ttu-id="d6b05-190">如果您在來賓容器的服務資訊清單中使用 `Endpoint` 標記指定端點，Service Fabric 可以自動將此端點發佈至命名服務。</span><span class="sxs-lookup"><span data-stu-id="d6b05-190">If you specify an endpoint, using the `Endpoint` tag in the service manifest of a guest container, Service Fabric can automatically publish this endpoint to the Naming service.</span></span> <span data-ttu-id="d6b05-191">因此，在叢集中執行的其他服務都可以使用用於解析的 REST 查詢找到這個容器。</span><span class="sxs-lookup"><span data-stu-id="d6b05-191">Other services that are running in the cluster can thus discover this container using the REST queries for resolving.</span></span>

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

<span data-ttu-id="d6b05-192">向命名服務註冊，可讓您輕易地在容器內的程式碼中，利用[反向 Proxy](service-fabric-reverseproxy.md) 執行容器對容器的通訊。</span><span class="sxs-lookup"><span data-stu-id="d6b05-192">By registering with the Naming service, you can easily do container-to-container communication in the code within your container by using the [reverse proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="d6b05-193">將 http 接聽連接埠和您想要與之通訊的服務名稱提供給反向 Proxy，並將這些都設為環境變數，便可進行通訊。</span><span class="sxs-lookup"><span data-stu-id="d6b05-193">Communication is performed by providing the reverse proxy http listening port and the name of the services that you want to communicate with as environment variables.</span></span> <span data-ttu-id="d6b05-194">如需詳細資訊，請參閱下一節。</span><span class="sxs-lookup"><span data-stu-id="d6b05-194">For more information, see the next section.</span></span>

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="d6b05-195">設定環境變數</span><span class="sxs-lookup"><span data-stu-id="d6b05-195">Configure and set environment variables</span></span>
<span data-ttu-id="d6b05-196">針對部署在容器中的服務，或部署為程序/來賓執行檔的服務，您可以在服務資訊清單中為每個程式碼套件指定環境變數。</span><span class="sxs-lookup"><span data-stu-id="d6b05-196">Environment variables can be specified for each code package in the service manifest, both for services that are deployed in containers or for services that are deployed as processes/guest executables.</span></span> <span data-ttu-id="d6b05-197">這些環境變數的值可以在應用程式資訊清單中明確覆寫，或在部署期間指定為應用程式參數。</span><span class="sxs-lookup"><span data-stu-id="d6b05-197">These environment variable values can be overridden specifically in the application manifest or specified during deployment as application parameters.</span></span>

<span data-ttu-id="d6b05-198">下列服務資訊清單 XML 程式碼片段示範如何指定程式碼封裝的環境變數：</span><span class="sxs-lookup"><span data-stu-id="d6b05-198">The following service manifest XML snippet shows an example of how to specify environment variables for a code package:</span></span>

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

<span data-ttu-id="d6b05-199">在應用程式資訊清單層級上可覆寫這些環境變數︰</span><span class="sxs-lookup"><span data-stu-id="d6b05-199">These environment variables can be overridden at the application manifest level:</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

<span data-ttu-id="d6b05-200">在以上範例中，我們為 `HttpGateway` 環境變數指定明確的值 (19000)，而 `BackendServiceName` 參數的值是透過 `[BackendSvc]` 應用程式參數來設定。</span><span class="sxs-lookup"><span data-stu-id="d6b05-200">In the previous example, we specified an explicit value for the `HttpGateway` environment variable (19000), while we set the value for `BackendServiceName` parameter via the `[BackendSvc]` application parameter.</span></span> <span data-ttu-id="d6b05-201">這些設定可讓您在部署應用程式時指定 `BackendServiceName` 的值，而在資訊清單中沒有固定的值。</span><span class="sxs-lookup"><span data-stu-id="d6b05-201">These settings enable you to specify the value for `BackendServiceName`value when you deploy the application and not have a fixed value in the manifest.</span></span>

## <a name="complete-examples-for-application-and-service-manifest"></a><span data-ttu-id="d6b05-202">應用程式和服務資訊清單的完整範例</span><span class="sxs-lookup"><span data-stu-id="d6b05-202">Complete examples for application and service manifest</span></span>

<span data-ttu-id="d6b05-203">以下是應用程式資訊清單：</span><span class="sxs-lookup"><span data-stu-id="d6b05-203">An example application manifest follows:</span></span>

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

<span data-ttu-id="d6b05-204">以下是服務資訊清單 (在之前的應用程式資訊清單中指定) 的範例：</span><span class="sxs-lookup"><span data-stu-id="d6b05-204">An example service manifest (specified in the preceding application manifest) follows:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="d6b05-205">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d6b05-205">Next steps</span></span>
<span data-ttu-id="d6b05-206">現在您已部署容器化的服務，可以開始了解如何讀取 [Service Fabric 應用程式生命週期](service-fabric-application-lifecycle.md)並管理其生命週期。</span><span class="sxs-lookup"><span data-stu-id="d6b05-206">Now that you have deployed a containerized service, learn how to manage its lifecycle by reading [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span></span>

* [<span data-ttu-id="d6b05-207">Service Fabric 和容器的概觀</span><span class="sxs-lookup"><span data-stu-id="d6b05-207">Overview of Service Fabric and containers</span></span>](service-fabric-containers-overview.md)
* [<span data-ttu-id="d6b05-208">使用 Azure CLI 與 Service Fabric 叢集互動</span><span class="sxs-lookup"><span data-stu-id="d6b05-208">Interacting with Service Fabric clusters using the Azure CLI</span></span>](service-fabric-azure-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-deploy-container-linux/sf-container-yeoman1.png

## <a name="related-articles"></a><span data-ttu-id="d6b05-209">相關文章</span><span class="sxs-lookup"><span data-stu-id="d6b05-209">Related articles</span></span>

* [<span data-ttu-id="d6b05-210">開始使用 Service Fabric 和 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d6b05-210">Getting started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
* [<span data-ttu-id="d6b05-211">開始使用 Service Fabric XPlat CLI</span><span class="sxs-lookup"><span data-stu-id="d6b05-211">Getting started with Service Fabric XPlat CLI</span></span>](service-fabric-azure-cli.md)
