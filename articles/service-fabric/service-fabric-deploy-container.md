---
title: "Service Fabric 和部署容器 | Microsoft Docs"
description: "Service Fabric 及使用容器來部署微服務應用程式。 本文說明 Service Fabric 為容器提供的功能，以及如何將 Windows 容器映像部署至叢集。"
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
ms.openlocfilehash: 25d6b056421e71fa70ed20a39589f77dbbc25c69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-windows-container-to-service-fabric"></a><span data-ttu-id="4b14b-104">將 Windows 容器部署至 Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4b14b-104">Deploy a Windows container to Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4b14b-105">部署 Windows 容器</span><span class="sxs-lookup"><span data-stu-id="4b14b-105">Deploy Windows Container</span></span>](service-fabric-deploy-container.md)
> * [<span data-ttu-id="4b14b-106">部署 Docker 容器</span><span class="sxs-lookup"><span data-stu-id="4b14b-106">Deploy Docker Container</span></span>](service-fabric-deploy-container-linux.md)
> 
> 

<span data-ttu-id="4b14b-107">本文將引導您在 Windows 容器中建置容器化服務的程序。</span><span class="sxs-lookup"><span data-stu-id="4b14b-107">This article walks you through the process of building containerized services in Windows containers.</span></span>

<span data-ttu-id="4b14b-108">Service Fabric 有數個功能可協助您建置由容器內執行之微服務組成的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4b14b-108">Service Fabric has several capabilities that help you with building applications that are composed of microservices running inside containers.</span></span> 

<span data-ttu-id="4b14b-109">功能包括：</span><span class="sxs-lookup"><span data-stu-id="4b14b-109">The capabilities include:</span></span>

* <span data-ttu-id="4b14b-110">容器映像部署和啟用</span><span class="sxs-lookup"><span data-stu-id="4b14b-110">Container image deployment and activation</span></span>
* <span data-ttu-id="4b14b-111">資源管理</span><span class="sxs-lookup"><span data-stu-id="4b14b-111">Resource governance</span></span>
* <span data-ttu-id="4b14b-112">儲存機制驗證</span><span class="sxs-lookup"><span data-stu-id="4b14b-112">Repository authentication</span></span>
* <span data-ttu-id="4b14b-113">容器連接埠至主機連接埠的對應</span><span class="sxs-lookup"><span data-stu-id="4b14b-113">Container port-to-host port mapping</span></span>
* <span data-ttu-id="4b14b-114">容器至容器的探索及通訊</span><span class="sxs-lookup"><span data-stu-id="4b14b-114">Container-to-container discovery and communication</span></span>
* <span data-ttu-id="4b14b-115">能夠設定環境變數</span><span class="sxs-lookup"><span data-stu-id="4b14b-115">Ability to configure and set environment variables</span></span>

<span data-ttu-id="4b14b-116">讓我們看看將容器化服務封裝納入應用程式時，每項功能如何運作。</span><span class="sxs-lookup"><span data-stu-id="4b14b-116">Let's look at how each of capabilities works when you're packaging a containerized service to be included in your application.</span></span>

## <a name="package-a-windows-container"></a><span data-ttu-id="4b14b-117">封裝 Windows 容器</span><span class="sxs-lookup"><span data-stu-id="4b14b-117">Package a Windows container</span></span>
<span data-ttu-id="4b14b-118">在封裝容器時，您可以選擇使用 Visual Studio 專案範本，或是[手動建立應用程式套件](#manually)。</span><span class="sxs-lookup"><span data-stu-id="4b14b-118">When you package a container, you can choose to use either a Visual Studio project template or [create the application package manually](#manually).</span></span>  <span data-ttu-id="4b14b-119">當您使用 Visual Studio 時，「新增專案」範本會為您建立應用程式套件結構和資訊清單檔案。</span><span class="sxs-lookup"><span data-stu-id="4b14b-119">When you use Visual Studio, the application package structure and manifest files are created by the New Project template for you.</span></span>

> [!TIP]
> <span data-ttu-id="4b14b-120">將現有的容器映像封裝到服務中的最簡單方式就是使用 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="4b14b-120">The easiest way to package an existing container image into a service is to use Visual Studio.</span></span>

## <a name="use-visual-studio-to-package-an-existing-container-image"></a><span data-ttu-id="4b14b-121">使用 Visual Studio 封裝現有容器映像</span><span class="sxs-lookup"><span data-stu-id="4b14b-121">Use Visual Studio to package an existing container image</span></span>
<span data-ttu-id="4b14b-122">Visual Studio 提供一個 Service Fabric 服務範本，可協助您將容器部署到 Service Fabric 叢集中。</span><span class="sxs-lookup"><span data-stu-id="4b14b-122">Visual Studio provides a Service Fabric service template to help you deploy a container to a Service Fabric cluster.</span></span>

1. <span data-ttu-id="4b14b-123">選擇 [檔案]  >  [新增專案]，然後建立 Service Fabric 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4b14b-123">Choose **File** > **New Project**, and create a Service Fabric application.</span></span>
2. <span data-ttu-id="4b14b-124">選擇 [客體容器] 作為服務範本。</span><span class="sxs-lookup"><span data-stu-id="4b14b-124">Choose **Guest Container** as the service template.</span></span>
3. <span data-ttu-id="4b14b-125">選擇 [映像名稱] 並提供該映像在您的容器存放庫中的路徑。</span><span class="sxs-lookup"><span data-stu-id="4b14b-125">Choose **Image Name** and provide the path to the image in your container repository.</span></span> <span data-ttu-id="4b14b-126">例如，https://hub.docker.com 中的 `myrepo/myimage:v1`</span><span class="sxs-lookup"><span data-stu-id="4b14b-126">For example, `myrepo/myimage:v1` in https://hub.docker.com</span></span>
4. <span data-ttu-id="4b14b-127">指定服務的名稱，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="4b14b-127">Give your service a name, and click **OK**.</span></span>
5. <span data-ttu-id="4b14b-128">如果容器化服務需要一個用來進行通訊的端點，您現在便可在 ServiceManifest.xml 檔案中新增通訊協定、連接埠及類型。</span><span class="sxs-lookup"><span data-stu-id="4b14b-128">If your containerized service needs an endpoint for communication, you can now add the protocol, port, and type to the ServiceManifest.xml file.</span></span> <span data-ttu-id="4b14b-129">例如：</span><span class="sxs-lookup"><span data-stu-id="4b14b-129">For example:</span></span> 
     
    `<Endpoint Name="MyContainerServiceEndpoint" Protocol="http" Port="80" UriScheme="http" PathSuffix="myapp/" Type="Input" />`
    
    <span data-ttu-id="4b14b-130">提供 `UriScheme`，Service Fabric 就會自動向「命名」服務註冊容器端點以供搜尋。</span><span class="sxs-lookup"><span data-stu-id="4b14b-130">By providing the `UriScheme`, Service Fabric automatically registers the container endpoint with the Naming service for discoverability.</span></span> <span data-ttu-id="4b14b-131">連接埠可以固定 (如同上述範例所示) 或動態配置。</span><span class="sxs-lookup"><span data-stu-id="4b14b-131">The port can either be fixed (as shown in the preceding example) or dynamically allocated.</span></span> <span data-ttu-id="4b14b-132">如果您沒有指定連接埠，則會動態配置應用程式連接埠範圍 (任何服務皆如此)。</span><span class="sxs-lookup"><span data-stu-id="4b14b-132">If you don't specify a port, it is dynamically allocated from the application port range (as would happen with any service).</span></span>
    <span data-ttu-id="4b14b-133">您還需要在應用程式資訊清單中指定 `PortBinding` 來設定容器至主機連接埠的對應。</span><span class="sxs-lookup"><span data-stu-id="4b14b-133">You also need to configure the container to host port mapping by specifying a `PortBinding` policy in the application manifest.</span></span> <span data-ttu-id="4b14b-134">如需詳細資訊，請參閱[設定容器至主機的對應](#Portsection)。</span><span class="sxs-lookup"><span data-stu-id="4b14b-134">For more information, see [Configure container to host port mapping](#Portsection).</span></span>
6. <span data-ttu-id="4b14b-135">如果您的容器需要資源管理，則請新增 `ResourceGovernancePolicy`。</span><span class="sxs-lookup"><span data-stu-id="4b14b-135">If your container needs resource governance then add a `ResourceGovernancePolicy`.</span></span>
8. <span data-ttu-id="4b14b-136">如果您的容器需要向私人存放庫進行驗證，則新增 `RepositoryCredentials`。</span><span class="sxs-lookup"><span data-stu-id="4b14b-136">If your container needs to authenticate with a private repository, then add `RepositoryCredentials`.</span></span>
7. <span data-ttu-id="4b14b-137">如果是在已啟用容器支援的 Windows Server 2016 機器上執行，可以使用封裝和發佈動作來部署至您的本機叢集。</span><span class="sxs-lookup"><span data-stu-id="4b14b-137">If you are running on a Windows Server 2016 machine with container support enabled, you can use the package and publish action to deploy to your local cluster.</span></span> 
8. <span data-ttu-id="4b14b-138">準備好時，即可將應用程式發佈至遠端叢集，或將方案簽入到原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="4b14b-138">When ready, you can publish the application to a remote cluster or check in the solution to source control.</span></span> 

<span data-ttu-id="4b14b-139">如需範例，請查看 [GitHub 上的 Service Fabric 容器程式碼範例](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="4b14b-139">For an example, checkout the [Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>

## <a name="creating-a-windows-server-2016-cluster"></a><span data-ttu-id="4b14b-140">建立 Windows Server 2016 叢集</span><span class="sxs-lookup"><span data-stu-id="4b14b-140">Creating a Windows Server 2016 cluster</span></span>
<span data-ttu-id="4b14b-141">若要部署容器化應用程式，您必須建立執行 Windows Server 2016 並已啟用容器支援的叢集。</span><span class="sxs-lookup"><span data-stu-id="4b14b-141">To deploy your containerized application, you need to create a cluster running Windows Server 2016 with container support enabled.</span></span> <span data-ttu-id="4b14b-142">您的叢集可能會在本機執行，或透過 Azure Resource Manager 部署在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="4b14b-142">Your cluster may be running locally, or deployed via Azure Resource Manager in Azure.</span></span> 

<span data-ttu-id="4b14b-143">若要使用 Azure Resource Manager 部署叢集，選擇 Azure 中的 [含容器的 Windows Server 2016] 映像。</span><span class="sxs-lookup"><span data-stu-id="4b14b-143">To deploy a cluster using Azure Resource Manager, choose the **Windows Server 2016 with Containers** image option in Azure.</span></span> <span data-ttu-id="4b14b-144">請參閱文章[使用 Azure Resource Manager 來建立 Service Fabric 叢集](service-fabric-cluster-creation-via-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="4b14b-144">See the article [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="4b14b-145">確定您是使用下列 Azure Resource Manager 設定：</span><span class="sxs-lookup"><span data-stu-id="4b14b-145">Ensure that you use the following Azure Resource Manager settings:</span></span>

```xml
"vmImageOffer": { "type": "string","defaultValue": "WindowsServer"     },
"vmImageSku": { "defaultValue": "2016-Datacenter-with-Containers","type": "string"     },
"vmImageVersion": { "defaultValue": "latest","type": "string"     },  
```
<span data-ttu-id="4b14b-146">您也可以使用[五個節點的 Azure Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype)建立叢集。</span><span class="sxs-lookup"><span data-stu-id="4b14b-146">You can also use the [Five Node Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) to create a cluster.</span></span> <span data-ttu-id="4b14b-147">或者，閱讀社群中的[部落格文章](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html)以了解如何使用 Service Fabric 和 Windows 容器。</span><span class="sxs-lookup"><span data-stu-id="4b14b-147">Alternatively read a community [blog post](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) on using Service Fabric and Windows containers.</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a><span data-ttu-id="4b14b-148">手動封裝和部署容器映像</span><span class="sxs-lookup"><span data-stu-id="4b14b-148">Manually package and deploy a container image</span></span>
<span data-ttu-id="4b14b-149">手動封裝容器化服務的程序是基於下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4b14b-149">The process of manually packaging a containerized service is based on the following steps:</span></span>

1. <span data-ttu-id="4b14b-150">將容器發佈至儲存機制。</span><span class="sxs-lookup"><span data-stu-id="4b14b-150">Publish the containers to your repository.</span></span>
2. <span data-ttu-id="4b14b-151">建立封裝目錄結構。</span><span class="sxs-lookup"><span data-stu-id="4b14b-151">Create the package directory structure.</span></span>
3. <span data-ttu-id="4b14b-152">編輯服務資訊清單檔。</span><span class="sxs-lookup"><span data-stu-id="4b14b-152">Edit the service manifest file.</span></span>
4. <span data-ttu-id="4b14b-153">編輯應用程式資訊清單檔。</span><span class="sxs-lookup"><span data-stu-id="4b14b-153">Edit the application manifest file.</span></span>

## <a name="deploy-and-activate-a-container-image"></a><span data-ttu-id="4b14b-154">部署和啟用容器映像</span><span class="sxs-lookup"><span data-stu-id="4b14b-154">Deploy and activate a container image</span></span>
<span data-ttu-id="4b14b-155">在 Service Fabric [應用程式模型](service-fabric-application-model.md)中，容器代表多個服務複本所在的應用程式主機。</span><span class="sxs-lookup"><span data-stu-id="4b14b-155">In the Service Fabric [application model](service-fabric-application-model.md), a container represents an application host in which multiple service replicas are placed.</span></span> <span data-ttu-id="4b14b-156">若要部署和啟用容器，請在服務資訊清單的 `ContainerHost` 元素中輸入容器映像的名稱。</span><span class="sxs-lookup"><span data-stu-id="4b14b-156">To deploy and activate a container, put the name of the container image into a `ContainerHost` element in the service manifest.</span></span>

<span data-ttu-id="4b14b-157">在服務資訊清單中，新增 `ContainerHost` 作為進入點。</span><span class="sxs-lookup"><span data-stu-id="4b14b-157">In the service manifest, add a `ContainerHost` for the entry point.</span></span> <span data-ttu-id="4b14b-158">然後將 `ImageName` 設為容器儲存機制和映像的名稱。</span><span class="sxs-lookup"><span data-stu-id="4b14b-158">Then set the `ImageName` to be the name of the container repository and image.</span></span> <span data-ttu-id="4b14b-159">下列的局部資訊清單示範如何從名為 `myrepo` 的儲存機制，部署名為 `myimage:v1` 的容器：</span><span class="sxs-lookup"><span data-stu-id="4b14b-159">The following partial manifest shows an example of how to deploy the container called `myimage:v1` from a repository called `myrepo`:</span></span>

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

<span data-ttu-id="4b14b-160">啟動容器時，可以在 `Commands` 下指定要執行的選用命令。</span><span class="sxs-lookup"><span data-stu-id="4b14b-160">You can specify optional commands to run upon starting the container under the `Commands` element.</span></span> <span data-ttu-id="4b14b-161">若有多個命令，用逗號分隔它們。</span><span class="sxs-lookup"><span data-stu-id="4b14b-161">For multiple commands, comma-delimit them.</span></span> 

## <a name="understand-resource-governance"></a><span data-ttu-id="4b14b-162">了解資源管理</span><span class="sxs-lookup"><span data-stu-id="4b14b-162">Understand resource governance</span></span>
<span data-ttu-id="4b14b-163">資源管理是容器的功能，可限制容器在主機上可使用的資源。</span><span class="sxs-lookup"><span data-stu-id="4b14b-163">Resource governance is a capability of the container that restricts the resources that the container can use on the host.</span></span> <span data-ttu-id="4b14b-164">應用程式資訊清單中指定的 `ResourceGovernancePolicy` 是用於宣告服務程式碼套件的資源限制。</span><span class="sxs-lookup"><span data-stu-id="4b14b-164">The `ResourceGovernancePolicy`, which is specified in the application manifest is used to declare resource limits for a service code package.</span></span> <span data-ttu-id="4b14b-165">可為以下資源設定限制：</span><span class="sxs-lookup"><span data-stu-id="4b14b-165">Resource limits can be set for the following resources:</span></span>

* <span data-ttu-id="4b14b-166">記憶體</span><span class="sxs-lookup"><span data-stu-id="4b14b-166">Memory</span></span>
* <span data-ttu-id="4b14b-167">MemorySwap</span><span class="sxs-lookup"><span data-stu-id="4b14b-167">MemorySwap</span></span>
* <span data-ttu-id="4b14b-168">CpuShares (CPU 相對權數)</span><span class="sxs-lookup"><span data-stu-id="4b14b-168">CpuShares (CPU relative weight)</span></span>
* <span data-ttu-id="4b14b-169">MemoryReservationInMB</span><span class="sxs-lookup"><span data-stu-id="4b14b-169">MemoryReservationInMB</span></span>  
* <span data-ttu-id="4b14b-170">BlkioWeight (BlockIO 相對權數)。</span><span class="sxs-lookup"><span data-stu-id="4b14b-170">BlkioWeight (BlockIO relative weight).</span></span>

> [!NOTE]
> <span data-ttu-id="4b14b-171">我們規劃在未來支援指定特定的區塊 IO 限制，例如 IOP、讀取/寫入 BPS 及其他限制。</span><span class="sxs-lookup"><span data-stu-id="4b14b-171">Support for specifying specific block IO limits such as IOPs, read/write BPS, and others are planned for a future release.</span></span>
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

## <a name="authenticate-a-repository"></a><span data-ttu-id="4b14b-172">驗證儲存機制</span><span class="sxs-lookup"><span data-stu-id="4b14b-172">Authenticate a repository</span></span>
<span data-ttu-id="4b14b-173">若要下載容器，您可能必須提供容器儲存機制的登入認證。</span><span class="sxs-lookup"><span data-stu-id="4b14b-173">To download a container, you might have to provide sign-in credentials to the container repository.</span></span> <span data-ttu-id="4b14b-174">於應用程式資訊清單中指定的登入認證，是用於指定從映像儲存機制下載容器映像所需的登入資訊 (或 SSH 金鑰)。</span><span class="sxs-lookup"><span data-stu-id="4b14b-174">The sign-in credentials, specified in the application manifest, are used to specify the sign-in information, or SSH key, for downloading the container image from the image repository.</span></span> <span data-ttu-id="4b14b-175">下列範例顯示名為 TestUser  的帳戶及純文字密碼 (「不」建議使用)：</span><span class="sxs-lookup"><span data-stu-id="4b14b-175">The following example shows an account called *TestUser* along with the password in clear text (*not* recommended):</span></span>

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

<span data-ttu-id="4b14b-176">我們建議使用部署至電腦的憑證將密碼加密。</span><span class="sxs-lookup"><span data-stu-id="4b14b-176">We recommend that you encrypt the password by using a certificate that's deployed to the machine.</span></span>

<span data-ttu-id="4b14b-177">下列範例顯示名為 TestUser 的帳戶，其密碼以名為 MyCert 的憑證加密。</span><span class="sxs-lookup"><span data-stu-id="4b14b-177">The following example shows an account called *TestUser*, where the password was encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="4b14b-178">您可以使用 `Invoke-ServiceFabricEncryptText` Powershell 命令來建立密碼的加密文字。</span><span class="sxs-lookup"><span data-stu-id="4b14b-178">You can use the `Invoke-ServiceFabricEncryptText` PowerShell command to create the secret cipher text for the password.</span></span> <span data-ttu-id="4b14b-179">如需詳細資訊，請參閱[管理 Service Fabric 應用程式中的密碼](service-fabric-application-secret-management.md)。</span><span class="sxs-lookup"><span data-stu-id="4b14b-179">For more information, see the article [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md).</span></span>

<span data-ttu-id="4b14b-180">用於解密密碼的憑證私密金鑰必須以頻外方法部署到本機電腦。</span><span class="sxs-lookup"><span data-stu-id="4b14b-180">The private key of the certificate that's used to decrypt the password must be deployed to the local machine in an out-of-band method.</span></span> <span data-ttu-id="4b14b-181">(在 Azure 中，這個方法就是 Azure Resource Manager。)然後，當 Service Fabric 將服務套件部署到電腦時，它可以解密密碼。</span><span class="sxs-lookup"><span data-stu-id="4b14b-181">(In Azure, this method is Azure Resource Manager.) Then, when Service Fabric deploys the service package to the machine, it can decrypt the secret.</span></span> <span data-ttu-id="4b14b-182">搭配使用帳戶名稱和密碼，之後可以用它向容器儲存機制提供驗證。</span><span class="sxs-lookup"><span data-stu-id="4b14b-182">By using the secret along with the account name, it can then authenticate with the container repository.</span></span>

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

## <span data-ttu-id="4b14b-183"><a name ="Portsection"></a> 設定容器至主機連接埠的對應</span><span class="sxs-lookup"><span data-stu-id="4b14b-183"><a name ="Portsection"></a> Configure container to host port mapping</span></span>
<span data-ttu-id="4b14b-184">您可以在應用程式資訊清單中指定 `PortBinding`，以設定用來與容器通訊的主機連接埠。</span><span class="sxs-lookup"><span data-stu-id="4b14b-184">You can configure a host port used to communicate with the container by specifying a `PortBinding` in the application manifest.</span></span> <span data-ttu-id="4b14b-185">連接埠繫結會將服務在容器內接聽的連接埠，對應至主機上的連接埠。</span><span class="sxs-lookup"><span data-stu-id="4b14b-185">The port binding maps the port to which the service is listening inside the container to a port on the host.</span></span>

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

## <a name="configure-container-to-container-discovery-and-communication"></a><span data-ttu-id="4b14b-186">設定容器至容器的探索及通訊</span><span class="sxs-lookup"><span data-stu-id="4b14b-186">Configure container-to-container discovery and communication</span></span>
<span data-ttu-id="4b14b-187">您可以使用 `PortBinding` 元素將容器連接埠對應至服務資訊清單中的端點。</span><span class="sxs-lookup"><span data-stu-id="4b14b-187">You can use the `PortBinding` element to map a container port to an endpoint in the service manifest.</span></span> <span data-ttu-id="4b14b-188">在下列範例中，端點 `Endpoint1` 指定固定的連接埠 8905。</span><span class="sxs-lookup"><span data-stu-id="4b14b-188">In the following example, the endpoint `Endpoint1` specifies a fixed port, 8905.</span></span> <span data-ttu-id="4b14b-189">也可以完全不指定連接埠，在此情況下，將從叢集的應用程式連接埠範圍內為您選擇隨機連接埠。</span><span class="sxs-lookup"><span data-stu-id="4b14b-189">It can also specify no port at all, in which case a random port from the cluster's application port range is chosen for you.</span></span>


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
<span data-ttu-id="4b14b-190">如果您在來賓容器的服務資訊清單中使用 `Endpoint` 標記指定端點，Service Fabric 可以自動將此端點發佈至命名服務。</span><span class="sxs-lookup"><span data-stu-id="4b14b-190">If you specify an endpoint, using the `Endpoint` tag in the service manifest of a guest container, Service Fabric can automatically publish this endpoint to the Naming service.</span></span> <span data-ttu-id="4b14b-191">因此，在叢集中執行的其他服務都可以使用用於解析的 REST 查詢找到這個容器。</span><span class="sxs-lookup"><span data-stu-id="4b14b-191">Other services that are running in the cluster can thus discover this container using the REST queries for resolving.</span></span>

<span data-ttu-id="4b14b-192">向命名服務註冊，可讓您在容器內利用[反向 Proxy](service-fabric-reverseproxy.md) 執行容器對容器的通訊。</span><span class="sxs-lookup"><span data-stu-id="4b14b-192">By registering with the Naming service, you can perform container-to-container communication within your container by using the [reverse proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="4b14b-193">將 http 接聽連接埠和您想要與之通訊的服務名稱提供給反向 Proxy，並將這些都設為環境變數，便可進行通訊。</span><span class="sxs-lookup"><span data-stu-id="4b14b-193">Communication is performed by providing the reverse proxy http listening port and the name of the services that you want to communicate with as environment variables.</span></span> <span data-ttu-id="4b14b-194">如需詳細資訊，請參閱下一節。</span><span class="sxs-lookup"><span data-stu-id="4b14b-194">For more information, see the next section.</span></span> 

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="4b14b-195">設定環境變數</span><span class="sxs-lookup"><span data-stu-id="4b14b-195">Configure and set environment variables</span></span>
<span data-ttu-id="4b14b-196">可以為服務資訊清單中的每個程式碼套件指定環境變數。</span><span class="sxs-lookup"><span data-stu-id="4b14b-196">Environment variables can be specified for each code package in the service manifest.</span></span> <span data-ttu-id="4b14b-197">所有服務都有這項功能，無論是部署為容器或處理程序或來賓可執行檔。</span><span class="sxs-lookup"><span data-stu-id="4b14b-197">This feature is available for all services irrespective of whether they are deployed as containers or processes or guest executables.</span></span> <span data-ttu-id="4b14b-198">您可以覆寫應用程式資訊清單中環境變數的值，或在部署期間將它們指定為應用程式參數。</span><span class="sxs-lookup"><span data-stu-id="4b14b-198">You can override environment variable values in the application manifest or specify them during deployment as application parameters.</span></span>

<span data-ttu-id="4b14b-199">下列服務資訊清單 XML 程式碼片段示範如何指定程式碼封裝的環境變數：</span><span class="sxs-lookup"><span data-stu-id="4b14b-199">The following service manifest XML snippet shows an example of how to specify environment variables for a code package:</span></span>

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

<span data-ttu-id="4b14b-200">在應用程式資訊清單層級上可覆寫這些環境變數︰</span><span class="sxs-lookup"><span data-stu-id="4b14b-200">These environment variables can be overridden at the application manifest level:</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

<span data-ttu-id="4b14b-201">在以上範例中，我們為 `HttpGateway` 環境變數指定明確的值 (19000)，而 `BackendServiceName` 參數的值是透過 `[BackendSvc]` 應用程式參數來設定。</span><span class="sxs-lookup"><span data-stu-id="4b14b-201">In the previous example, we specified an explicit value for the `HttpGateway` environment variable (19000), while we set the value for `BackendServiceName` parameter via the `[BackendSvc]` application parameter.</span></span> <span data-ttu-id="4b14b-202">這些設定可讓您在部署應用程式時指定 `BackendServiceName` 的值，而在資訊清單中沒有固定的值。</span><span class="sxs-lookup"><span data-stu-id="4b14b-202">These settings enable you to specify the value for `BackendServiceName`value when you deploy the application and not have a fixed value in the manifest.</span></span>

## <a name="configure-isolation-mode"></a><span data-ttu-id="4b14b-203">設定隔離模式</span><span class="sxs-lookup"><span data-stu-id="4b14b-203">Configure isolation mode</span></span>

<span data-ttu-id="4b14b-204">Windows 支援兩種容器隔離模式 - 處理序和 Hyper-V。</span><span class="sxs-lookup"><span data-stu-id="4b14b-204">Windows supports two isolation modes for containers - process and Hyper-V.</span></span>  <span data-ttu-id="4b14b-205">在處理序隔離模式中，在相同主機電腦上執行的所有容器都與主機共用核心。</span><span class="sxs-lookup"><span data-stu-id="4b14b-205">With the process isolation mode, all the containers running on the same host machine share the kernel with the host.</span></span> <span data-ttu-id="4b14b-206">在 Hyper-V 隔離模式中，會在每個 Hyper-V 容器與容器主機之間隔離核心。</span><span class="sxs-lookup"><span data-stu-id="4b14b-206">With the Hyper-V isolation mode, the kernels are isolated between each Hyper-V container and the container host.</span></span> <span data-ttu-id="4b14b-207">隔離模式是在應用程式資訊清單檔中的 `ContainerHostPolicies` 標記指定。</span><span class="sxs-lookup"><span data-stu-id="4b14b-207">The isolation mode is specified in the `ContainerHostPolicies` tag in the application manifest file.</span></span>  <span data-ttu-id="4b14b-208">可以指定的隔離模式有 `process`、`hyperv` 和 `default`。</span><span class="sxs-lookup"><span data-stu-id="4b14b-208">The isolation modes that can be specified are `process`, `hyperv`, and `default`.</span></span> <span data-ttu-id="4b14b-209">Windows Server 主機上的 `default` 隔離模式預設為 `process`，Windows 10 主機上的預設值則為 `hyperv`。</span><span class="sxs-lookup"><span data-stu-id="4b14b-209">The `default` isolation mode defaults to `process` on Windows Server hosts, and defaults to `hyperv` on Windows 10 hosts.</span></span>  <span data-ttu-id="4b14b-210">下列程式碼片段顯示如何在應用程式資訊清單檔中指定隔離模式。</span><span class="sxs-lookup"><span data-stu-id="4b14b-210">The following snippet shows how the isolation mode is specified in the application manifest file.</span></span>

```xml
   <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv">
```


## <a name="complete-examples-for-application-and-service-manifest"></a><span data-ttu-id="4b14b-211">應用程式和服務資訊清單的完整範例</span><span class="sxs-lookup"><span data-stu-id="4b14b-211">Complete examples for application and service manifest</span></span>

<span data-ttu-id="4b14b-212">以下是應用程式資訊清單：</span><span class="sxs-lookup"><span data-stu-id="4b14b-212">An example application manifest follows:</span></span>

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

<span data-ttu-id="4b14b-213">以下是服務資訊清單 (在之前的應用程式資訊清單中指定) 的範例：</span><span class="sxs-lookup"><span data-stu-id="4b14b-213">An example service manifest (specified in the preceding application manifest) follows:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="4b14b-214">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4b14b-214">Next steps</span></span>
<span data-ttu-id="4b14b-215">現在您已部署容器化的服務，可以開始了解如何讀取 [Service Fabric 應用程式生命週期](service-fabric-application-lifecycle.md)並管理其生命週期。</span><span class="sxs-lookup"><span data-stu-id="4b14b-215">Now that you have deployed a containerized service, learn how to manage its lifecycle by reading [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span></span>

* [<span data-ttu-id="4b14b-216">Service Fabric 和容器的概觀</span><span class="sxs-lookup"><span data-stu-id="4b14b-216">Overview of Service Fabric and containers</span></span>](service-fabric-containers-overview.md)
* <span data-ttu-id="4b14b-217">如需範例，請查看 [GitHub 上的 Service Fabric 容器程式碼範例](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="4b14b-217">For an example, checkout [Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>
