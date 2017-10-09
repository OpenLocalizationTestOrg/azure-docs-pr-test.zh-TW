---
title: "aaaAzure Service Fabric 應用程式部署 |Microsoft 文件"
description: "如何使用 PowerShell 的 Service Fabric toodeploy 及移除應用程式。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b120ffbf-f1e3-4b26-a492-347c29f8f66b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: ryanwi
ms.openlocfilehash: 3de9c6a937ee7b29bf9ec86d6e9e631487797507
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-powershell"></a><span data-ttu-id="cccfd-103">使用 PowerShell 部署與移除應用程式</span><span class="sxs-lookup"><span data-stu-id="cccfd-103">Deploy and remove applications using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cccfd-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cccfd-104">PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
> * [<span data-ttu-id="cccfd-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cccfd-105">Visual Studio</span></span>](service-fabric-publish-app-remote-cluster.md)
> * [<span data-ttu-id="cccfd-106">FabricClient API</span><span class="sxs-lookup"><span data-stu-id="cccfd-106">FabricClient APIs</span></span>](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

<span data-ttu-id="cccfd-107">[封裝應用程式類型][10]後，即可將它部署至 Azure Service Fabric 叢集中。</span><span class="sxs-lookup"><span data-stu-id="cccfd-107">Once an [application type has been packaged][10], it's ready for deployment into an Azure Service Fabric cluster.</span></span> <span data-ttu-id="cccfd-108">部署包含下列三個步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="cccfd-108">Deployment involves hello following three steps:</span></span>

1. <span data-ttu-id="cccfd-109">上傳 hello 應用程式封裝 toohello 映像存放區</span><span class="sxs-lookup"><span data-stu-id="cccfd-109">Upload hello application package toohello image store</span></span>
2. <span data-ttu-id="cccfd-110">註冊 hello 應用程式類型</span><span class="sxs-lookup"><span data-stu-id="cccfd-110">Register hello application type</span></span>
3. <span data-ttu-id="cccfd-111">建立 hello 應用程式執行個體</span><span class="sxs-lookup"><span data-stu-id="cccfd-111">Create hello application instance</span></span>

<span data-ttu-id="cccfd-112">部署應用程式的執行個體正在執行中 hello 叢集後，您可以刪除 hello 應用程式執行個體和其應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="cccfd-112">After an application is deployed and an instance is running in hello cluster, you can delete hello application instance and its application type.</span></span> <span data-ttu-id="cccfd-113">toocompletely 移除從 hello 叢集中的應用程式牽涉到 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="cccfd-113">toocompletely remove an application from hello cluster involves hello following steps:</span></span>

1. <span data-ttu-id="cccfd-114">移除 （或刪除） 執行應用程式執行個體的 hello</span><span class="sxs-lookup"><span data-stu-id="cccfd-114">Remove (or delete) hello running application instance</span></span>
2. <span data-ttu-id="cccfd-115">如果您不再需要取消註冊 hello 應用程式類型</span><span class="sxs-lookup"><span data-stu-id="cccfd-115">Unregister hello application type if you no longer need it</span></span>
3. <span data-ttu-id="cccfd-116">移除 hello 映像存放區中的 hello 應用程式套件</span><span class="sxs-lookup"><span data-stu-id="cccfd-116">Remove hello application package from hello image store</span></span>

<span data-ttu-id="cccfd-117">如果您使用[用於部署和偵錯應用程式的 Visual Studio](service-fabric-publish-app-remote-cluster.md)在本機開發叢集上，所有 hello 前面的步驟都是透過 PowerShell 指令碼會自動處理。</span><span class="sxs-lookup"><span data-stu-id="cccfd-117">If you use [Visual Studio for deploying and debugging applications](service-fabric-publish-app-remote-cluster.md) on your local development cluster, all hello preceding steps are handled automatically through a PowerShell script.</span></span>  <span data-ttu-id="cccfd-118">此指令碼位於 hello*指令碼*hello 應用程式專案的資料夾。</span><span class="sxs-lookup"><span data-stu-id="cccfd-118">This script is found in hello *Scripts* folder of hello application project.</span></span> <span data-ttu-id="cccfd-119">這篇文章提供背景資訊，讓您可以執行，該指令碼內容正在進行 hello Visual Studio 之外，相同的作業。</span><span class="sxs-lookup"><span data-stu-id="cccfd-119">This article provides background on what that script is doing so that you can perform hello same operations outside of Visual Studio.</span></span> 
 
## <a name="connect-toohello-cluster"></a><span data-ttu-id="cccfd-120">Toohello 叢集連線</span><span class="sxs-lookup"><span data-stu-id="cccfd-120">Connect toohello cluster</span></span>
<span data-ttu-id="cccfd-121">在本文中執行任何 PowerShell 命令之前，一律使用啟動[Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) tooconnect toohello Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="cccfd-121">Before you run any PowerShell commands in this article, always start by using [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) tooconnect toohello Service Fabric cluster.</span></span> <span data-ttu-id="cccfd-122">tooconnect toohello 本機開發叢集，請執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="cccfd-122">tooconnect toohello local development cluster, run hello following:</span></span>

```powershell
PS C:\>Connect-ServiceFabricCluster
```

<span data-ttu-id="cccfd-123">如需範例連接 tooa 遠端叢集或叢集使用 Azure Active Directory，X509 保護的憑證或 Windows Active Directory，請參閱[連接 tooa 安全叢集](service-fabric-connect-to-secure-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="cccfd-123">For examples of connecting tooa remote cluster or cluster secured using Azure Active Directory, X509 certificates, or Windows Active Directory see [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

## <a name="upload-hello-application-package"></a><span data-ttu-id="cccfd-124">上傳 hello 應用程式套件</span><span class="sxs-lookup"><span data-stu-id="cccfd-124">Upload hello application package</span></span>
<span data-ttu-id="cccfd-125">正在上傳的 hello 應用程式封裝會將它放在內部的 Service Fabric 元件所存取的位置。</span><span class="sxs-lookup"><span data-stu-id="cccfd-125">Uploading hello application package puts it in a location that's accessible by internal Service Fabric components.</span></span>
<span data-ttu-id="cccfd-126">如果您想 tooverify hello 應用程式封裝在本機，使用 hello[測試 ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="cccfd-126">If you want tooverify hello application package locally, use hello [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="cccfd-127">hello[複製 ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps)命令上傳 hello 應用程式封裝 toohello 叢集映像存放區。</span><span class="sxs-lookup"><span data-stu-id="cccfd-127">hello [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command uploads hello application package toohello cluster image store.</span></span>
<span data-ttu-id="cccfd-128">hello **Get ImageStoreConnectionStringFromClusterManifest** cmdlet，這是 hello Service Fabric SDK PowerShell 模組的一部分，是使用的 tooget hello 映像儲存連接字串。</span><span class="sxs-lookup"><span data-stu-id="cccfd-128">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="cccfd-129">tooimport hello SDK 模組，執行：</span><span class="sxs-lookup"><span data-stu-id="cccfd-129">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="cccfd-130">假設您在 Visual Studio 2015 中建置並封裝名為 *MyApplication* 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="cccfd-130">Suppose you build and package an application named *MyApplication* in Visual Studio 2015.</span></span> <span data-ttu-id="cccfd-131">根據預設，hello hello ApplicationManifest.xml 中列出的應用程式類型名稱是"MyApplicationType"。</span><span class="sxs-lookup"><span data-stu-id="cccfd-131">By default, hello application type name listed in hello ApplicationManifest.xml is "MyApplicationType".</span></span>  <span data-ttu-id="cccfd-132">hello 應用程式封裝，其中包含 hello 必要的應用程式資訊清單、 服務資訊清單，以及程式碼/config/資料的封裝，位於*C:\Users\<username\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug*。</span><span class="sxs-lookup"><span data-stu-id="cccfd-132">hello application package, which contains hello necessary application manifest, service manifests, and code/config/data packages, is located in *C:\Users\<username\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug*.</span></span> 

<span data-ttu-id="cccfd-133">hello 下列命令會列出 hello hello 應用程式封裝內容：</span><span class="sxs-lookup"><span data-stu-id="cccfd-133">hello following command lists hello contents of hello application package:</span></span>

```powershell
PS C:\> $path = 'C:\Users\<user\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug'
PS C:\> tree /f $path
Folder PATH listing for volume OSDisk
Volume serial number is 0459-2393
C:\USERS\USER\DOCUMENTS\VISUAL STUDIO 2015\PROJECTS\MYAPPLICATION\MYAPPLICATION\PKG\DEBUG
│   ApplicationManifest.xml
│
└───Stateless1Pkg
    │   ServiceManifest.xml
    │
    ├───Code
    │       Microsoft.ServiceFabric.Data.dll
    │       Microsoft.ServiceFabric.Data.Interfaces.dll
    │       Microsoft.ServiceFabric.Internal.dll
    │       Microsoft.ServiceFabric.Internal.Strings.dll
    │       Microsoft.ServiceFabric.Services.dll
    │       ServiceFabricServiceModel.dll
    │       Stateless1.exe
    │       Stateless1.exe.config
    │       Stateless1.pdb
    │       System.Fabric.dll
    │       System.Fabric.Strings.dll
    │
    └───Config
            Settings.xml
```

<span data-ttu-id="cccfd-134">如果 hello 應用程式套件很大且/或有許多檔案，您可以[壓縮](service-fabric-package-apps.md#compress-a-package)。</span><span class="sxs-lookup"><span data-stu-id="cccfd-134">If hello application package is large and/or has many files, you can [compress it](service-fabric-package-apps.md#compress-a-package).</span></span> <span data-ttu-id="cccfd-135">hello 壓縮會減少 hello 大小和檔案的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="cccfd-135">hello compression reduces hello size and hello number of files.</span></span>
<span data-ttu-id="cccfd-136">hello 副作用就是該註冊和取消註冊 hello 應用程式類型為更快。</span><span class="sxs-lookup"><span data-stu-id="cccfd-136">hello side effect is that registering and un-registering hello application type are faster.</span></span> <span data-ttu-id="cccfd-137">上傳時間可能較慢目前，特別是當您包含 hello 階段 toocompress hello 封裝。</span><span class="sxs-lookup"><span data-stu-id="cccfd-137">Upload time may be slower currently, especially if you include hello time toocompress hello package.</span></span> 

<span data-ttu-id="cccfd-138">toocompress 封裝時，使用 hello 相同[複製 ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps)命令。</span><span class="sxs-lookup"><span data-stu-id="cccfd-138">toocompress a package, use hello same [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command.</span></span> <span data-ttu-id="cccfd-139">壓縮可以個別從完成上傳、 使用 hello`SkipCopy`旗標，或與 hello 一起上傳作業。</span><span class="sxs-lookup"><span data-stu-id="cccfd-139">Compression can be done separate from upload, by using hello `SkipCopy` flag, or together with hello upload operation.</span></span> <span data-ttu-id="cccfd-140">在壓縮封裝上套用壓縮為無作業。</span><span class="sxs-lookup"><span data-stu-id="cccfd-140">Applying compression on a compressed package is no-op.</span></span>
<span data-ttu-id="cccfd-141">toouncompress 壓縮封裝，使用 hello 相同[複製 ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps)命令與 hello`UncompressPackage`切換。</span><span class="sxs-lookup"><span data-stu-id="cccfd-141">toouncompress a compressed package, use hello same [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command with hello `UncompressPackage` switch.</span></span>

<span data-ttu-id="cccfd-142">hello 下列指令程式會壓縮 hello 封裝但不複製該項 toohello 映像存放區。</span><span class="sxs-lookup"><span data-stu-id="cccfd-142">hello following cmdlet compresses hello package without copying it toohello image store.</span></span> <span data-ttu-id="cccfd-143">hello 封裝現在包含 hello 的 zip 的檔案`Code`和`Config`封裝。</span><span class="sxs-lookup"><span data-stu-id="cccfd-143">hello package now includes zipped files for hello `Code` and `Config` packages.</span></span> <span data-ttu-id="cccfd-144">不壓縮 hello 應用程式和 hello 服務資訊清單，因為它們所需的許多內部的作業 （例如共用、 應用程式類型名稱和版本擷取針對特定的驗證封裝）。</span><span class="sxs-lookup"><span data-stu-id="cccfd-144">hello application and hello service manifests are not zipped, because they are needed for many internal operations (like package sharing, application type name and version extraction for certain validations).</span></span> <span data-ttu-id="cccfd-145">壓縮 hello 資訊清單會使這些操作效率不佳。</span><span class="sxs-lookup"><span data-stu-id="cccfd-145">Zipping hello manifests would make these operations inefficient.</span></span>

```
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -CompressPackage -SkipCopy
PS C:\> tree /f $path
Folder PATH listing for volume OSDisk
Volume serial number is 0459-2393
C:\USERS\USER\DOCUMENTS\VISUAL STUDIO 2015\PROJECTS\MYAPPLICATION\MYAPPLICATION\PKG\DEBUG
|   ApplicationManifest.xml
|
└───Stateless1Pkg
       Code.zip
       Config.zip
       ServiceManifest.xml
```

<span data-ttu-id="cccfd-146">針對大型應用程式封裝，hello 壓縮會使用時間。</span><span class="sxs-lookup"><span data-stu-id="cccfd-146">For large application packages, hello compression takes time.</span></span> <span data-ttu-id="cccfd-147">為了獲得最佳結果，請使用快速的 SSD 磁碟機。</span><span class="sxs-lookup"><span data-stu-id="cccfd-147">For best results, use a fast SSD drive.</span></span> <span data-ttu-id="cccfd-148">hello 壓縮時間和 hello hello 壓縮封裝大小也有所不同 hello 套件內容。</span><span class="sxs-lookup"><span data-stu-id="cccfd-148">hello compression times and hello size of hello compressed package also differ based on hello package content.</span></span>
<span data-ttu-id="cccfd-149">例如，以下是某些封裝，以顯示 hello 初始和 hello 與 hello 壓縮時間的壓縮的套件大小的壓縮統計資料。</span><span class="sxs-lookup"><span data-stu-id="cccfd-149">For example, here is compression statistics for some packages, which show hello initial and hello compressed package size, with hello compression time.</span></span>

|<span data-ttu-id="cccfd-150">初始大小 (MB)</span><span class="sxs-lookup"><span data-stu-id="cccfd-150">Initial size (MB)</span></span>|<span data-ttu-id="cccfd-151">檔案計數</span><span class="sxs-lookup"><span data-stu-id="cccfd-151">File count</span></span>|<span data-ttu-id="cccfd-152">壓縮時間</span><span class="sxs-lookup"><span data-stu-id="cccfd-152">Compression Time</span></span>|<span data-ttu-id="cccfd-153">壓縮的封裝大小 (MB)</span><span class="sxs-lookup"><span data-stu-id="cccfd-153">Compressed package size (MB)</span></span>|
|----------------:|---------:|---------------:|---------------------------:|
|<span data-ttu-id="cccfd-154">100</span><span class="sxs-lookup"><span data-stu-id="cccfd-154">100</span></span>|<span data-ttu-id="cccfd-155">100</span><span class="sxs-lookup"><span data-stu-id="cccfd-155">100</span></span>|<span data-ttu-id="cccfd-156">00:00:03.3547592</span><span class="sxs-lookup"><span data-stu-id="cccfd-156">00:00:03.3547592</span></span>|<span data-ttu-id="cccfd-157">60</span><span class="sxs-lookup"><span data-stu-id="cccfd-157">60</span></span>|
|<span data-ttu-id="cccfd-158">512</span><span class="sxs-lookup"><span data-stu-id="cccfd-158">512</span></span>|<span data-ttu-id="cccfd-159">100</span><span class="sxs-lookup"><span data-stu-id="cccfd-159">100</span></span>|<span data-ttu-id="cccfd-160">00:00:16.3850303</span><span class="sxs-lookup"><span data-stu-id="cccfd-160">00:00:16.3850303</span></span>|<span data-ttu-id="cccfd-161">307</span><span class="sxs-lookup"><span data-stu-id="cccfd-161">307</span></span>|
|<span data-ttu-id="cccfd-162">1024</span><span class="sxs-lookup"><span data-stu-id="cccfd-162">1024</span></span>|<span data-ttu-id="cccfd-163">500</span><span class="sxs-lookup"><span data-stu-id="cccfd-163">500</span></span>|<span data-ttu-id="cccfd-164">00:00:32.5907950</span><span class="sxs-lookup"><span data-stu-id="cccfd-164">00:00:32.5907950</span></span>|<span data-ttu-id="cccfd-165">615</span><span class="sxs-lookup"><span data-stu-id="cccfd-165">615</span></span>|
|<span data-ttu-id="cccfd-166">2048</span><span class="sxs-lookup"><span data-stu-id="cccfd-166">2048</span></span>|<span data-ttu-id="cccfd-167">1000</span><span class="sxs-lookup"><span data-stu-id="cccfd-167">1000</span></span>|<span data-ttu-id="cccfd-168">00:01:04.3775554</span><span class="sxs-lookup"><span data-stu-id="cccfd-168">00:01:04.3775554</span></span>|<span data-ttu-id="cccfd-169">1231</span><span class="sxs-lookup"><span data-stu-id="cccfd-169">1231</span></span>|
|<span data-ttu-id="cccfd-170">5012</span><span class="sxs-lookup"><span data-stu-id="cccfd-170">5012</span></span>|<span data-ttu-id="cccfd-171">100</span><span class="sxs-lookup"><span data-stu-id="cccfd-171">100</span></span>|<span data-ttu-id="cccfd-172">00:02:45.2951288</span><span class="sxs-lookup"><span data-stu-id="cccfd-172">00:02:45.2951288</span></span>|<span data-ttu-id="cccfd-173">3074</span><span class="sxs-lookup"><span data-stu-id="cccfd-173">3074</span></span>|

<span data-ttu-id="cccfd-174">一旦封裝壓縮檔，它可以上傳的 tooone 或視需要的多個 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="cccfd-174">Once a package is compressed, it can be uploaded tooone or multiple Service Fabric clusters as needed.</span></span> <span data-ttu-id="cccfd-175">hello 部署機制是相同的壓縮和未壓縮的封裝。</span><span class="sxs-lookup"><span data-stu-id="cccfd-175">hello deployment mechanism is same for compressed and uncompressed packages.</span></span> <span data-ttu-id="cccfd-176">如果 hello 封裝已壓縮，因此儲存 hello 叢集映像存放區中，而且執行 hello 應用程式之前，hello 節點上進行壓縮。</span><span class="sxs-lookup"><span data-stu-id="cccfd-176">If hello package is compressed, it is stored as such in hello cluster image store and it's uncompressed on hello node before hello application is run.</span></span>


<span data-ttu-id="cccfd-177">hello 下列範例會上傳 hello 封裝 toohello 映像存放區，名為"MyApplicationV1 」 的資料夾：</span><span class="sxs-lookup"><span data-stu-id="cccfd-177">hello following example uploads hello package toohello image store, into a folder named "MyApplicationV1":</span></span>

```powershell
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)) -TimeoutSec 1800
```

<span data-ttu-id="cccfd-178">hello **Get ImageStoreConnectionStringFromClusterManifest** cmdlet，這是 hello Service Fabric SDK PowerShell 模組的一部分，是使用的 tooget hello 映像儲存連接字串。</span><span class="sxs-lookup"><span data-stu-id="cccfd-178">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="cccfd-179">tooimport hello SDK 模組，執行：</span><span class="sxs-lookup"><span data-stu-id="cccfd-179">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="cccfd-180">如果您未指定 hello *-ApplicationPackagePathInImageStore*參數，hello 應用程式套件複製到 hello"Debug"資料夾中 hello 映像存放區中。</span><span class="sxs-lookup"><span data-stu-id="cccfd-180">If you do not specify hello *-ApplicationPackagePathInImageStore* parameter, hello application package is copied into hello "Debug" folder in hello image store.</span></span>

<span data-ttu-id="cccfd-181">hello 花的時間 tooupload 封裝多個因素而有所不同。</span><span class="sxs-lookup"><span data-stu-id="cccfd-181">hello time it takes tooupload a package differs depending on multiple factors.</span></span> <span data-ttu-id="cccfd-182">這些因素有些 hello 中 hello 封裝、 hello 封裝大小，以及 hello 檔案大小的檔案數目。</span><span class="sxs-lookup"><span data-stu-id="cccfd-182">Some of these factors are hello number of files in hello package, hello package size, and hello file sizes.</span></span> <span data-ttu-id="cccfd-183">hello hello 來源電腦與 hello Service Fabric 叢集之間的網路速度也會影響 hello 上傳時間。</span><span class="sxs-lookup"><span data-stu-id="cccfd-183">hello network speed between hello source machine and hello Service Fabric cluster also impacts hello upload time.</span></span> <span data-ttu-id="cccfd-184">hello 預設逾時[複製 ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps)為 30 分鐘。</span><span class="sxs-lookup"><span data-stu-id="cccfd-184">hello default timeout for [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) is 30 minutes.</span></span>
<span data-ttu-id="cccfd-185">視 hello 所述的因素，您可能必須 tooincrease hello 逾時。</span><span class="sxs-lookup"><span data-stu-id="cccfd-185">Depending on hello described factors, you may have tooincrease hello timeout.</span></span> <span data-ttu-id="cccfd-186">如果您壓縮 hello hello 複製呼叫中的封裝，您需要 tooalso 考慮 hello 壓縮時間。</span><span class="sxs-lookup"><span data-stu-id="cccfd-186">If you are compressing hello package in hello copy call, you need tooalso consider hello compression time.</span></span>

<span data-ttu-id="cccfd-187">請參閱[hello 映像存放區連接字串了解](service-fabric-image-store-connection-string.md)如需關於 hello 映像存放區，以及映像存放區連接字串的補充資訊。</span><span class="sxs-lookup"><span data-stu-id="cccfd-187">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

## <a name="register-hello-application-package"></a><span data-ttu-id="cccfd-188">註冊 hello 應用程式套件</span><span class="sxs-lookup"><span data-stu-id="cccfd-188">Register hello application package</span></span>
<span data-ttu-id="cccfd-189">hello 應用程式類型和版本 hello 註冊 hello 應用程式封裝時變成可供使用的應用程式資訊清單中宣告。</span><span class="sxs-lookup"><span data-stu-id="cccfd-189">hello application type and version declared in hello application manifest become available for use when hello application package is registered.</span></span> <span data-ttu-id="cccfd-190">hello 系統讀取 hello 封裝上傳 hello 上一個步驟中，會驗證 hello 封裝、 處理 hello 套件內容，以及複製 hello 處理封裝 tooan 內部系統位置。</span><span class="sxs-lookup"><span data-stu-id="cccfd-190">hello system reads hello package uploaded in hello previous step, verifies hello package, processes hello package contents, and copies hello processed package tooan internal system location.</span></span>  

<span data-ttu-id="cccfd-191">執行 hello[暫存器 ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet tooregister hello hello 叢集中的應用程式類型，並使其可供部署：</span><span class="sxs-lookup"><span data-stu-id="cccfd-191">Run hello [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet tooregister hello application type in hello cluster and make it available for deployment:</span></span>

```powershell
PS C:\> Register-ServiceFabricApplicationType MyApplicationV1
Register application type succeeded
```

<span data-ttu-id="cccfd-192">「 MyApplicationV1 」 是 hello hello 應用程式封裝所在位置的映像存放區中的 hello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="cccfd-192">"MyApplicationV1" is hello folder in hello image store where hello application package is located.</span></span> <span data-ttu-id="cccfd-193">hello 應用程式類型具有名稱"MyApplicationType"和"1.0.0 版 」 （兩者都在 hello 應用程式資訊清單中找到） 現在會 hello 叢集中註冊。</span><span class="sxs-lookup"><span data-stu-id="cccfd-193">hello application type with name "MyApplicationType" and version "1.0.0" (both are found in hello application manifest) is now registered in hello cluster.</span></span>

<span data-ttu-id="cccfd-194">hello[暫存器 ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) hello 系統已成功註冊的 hello 應用程式封裝之後，才會傳回命令。</span><span class="sxs-lookup"><span data-stu-id="cccfd-194">hello [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) command returns only after hello system has successfully registered hello application package.</span></span> <span data-ttu-id="cccfd-195">時間長度，註冊會取決於 hello 大小和 hello 應用程式套件的內容。</span><span class="sxs-lookup"><span data-stu-id="cccfd-195">How long registration takes depends on hello size and contents of hello application package.</span></span> <span data-ttu-id="cccfd-196">如有需要 hello **-TimeoutSec**參數可以是使用的 toosupply 較長逾時 （hello 預設逾時為 60 秒）。</span><span class="sxs-lookup"><span data-stu-id="cccfd-196">If needed, hello **-TimeoutSec** parameter can be used toosupply a longer timeout (hello default timeout is 60 seconds).</span></span>

<span data-ttu-id="cccfd-197">如果您有大型應用程式套件，或者如果您遇到逾時，使用 hello **-Async**參數。</span><span class="sxs-lookup"><span data-stu-id="cccfd-197">If you have a large application package or if you are experiencing timeouts, use hello **-Async** parameter.</span></span> <span data-ttu-id="cccfd-198">hello 叢集接受 hello 註冊命令，並視需要 hello 處理作業會繼續時，就會傳回 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="cccfd-198">hello command returns when hello cluster accepts hello register command, and hello processing continues as needed.</span></span>
<span data-ttu-id="cccfd-199">hello [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps)命令列出所有已成功註冊應用程式類型版本及其註冊狀態。</span><span class="sxs-lookup"><span data-stu-id="cccfd-199">hello [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="cccfd-200">您可以使用這個命令 toodetermine hello 註冊完成。</span><span class="sxs-lookup"><span data-stu-id="cccfd-200">You can use this command toodetermine when hello registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="create-hello-application"></a><span data-ttu-id="cccfd-201">建立 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="cccfd-201">Create hello application</span></span>
<span data-ttu-id="cccfd-202">您可以從已成功註冊使用 hello 任何應用程式類型版本的應用程式具現化[新增 ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="cccfd-202">You can instantiate an application from any application type version that has been registered successfully by using hello [New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="cccfd-203">每個應用程式的 hello 名稱必須以 hello 開頭*"fabric:"*配置，而且必須是唯一的每個應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="cccfd-203">hello name of each application must start with hello *"fabric:"* scheme and must be unique for each application instance.</span></span> <span data-ttu-id="cccfd-204">也會建立任何 hello hello 目標應用程式類型的應用程式資訊清單中定義的預設服務。</span><span class="sxs-lookup"><span data-stu-id="cccfd-204">Any default services defined in hello application manifest of hello target application type are also created.</span></span>

```powershell
PS C:\> New-ServiceFabricApplication fabric:/MyApp MyApplicationType 1.0.0

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationParameters  : {}
```
<span data-ttu-id="cccfd-205">多個應用程式執行個體可以針對任何指定的已註冊應用程式類型版本來建立。</span><span class="sxs-lookup"><span data-stu-id="cccfd-205">Multiple application instances can be created for any given version of a registered application type.</span></span> <span data-ttu-id="cccfd-206">每個應用程式執行個體將在隔離狀態下執行，包含本身的工作目錄和程序。</span><span class="sxs-lookup"><span data-stu-id="cccfd-206">Each application instance runs in isolation, with its own work directory and process.</span></span>

<span data-ttu-id="cccfd-207">toosee 名為應用程式和服務正在執行 hello 的 hello 叢集中[Get ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication)和[Get ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="cccfd-207">toosee which named apps and services are running in hello cluster, run hello [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) and [Get-ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) cmdlets:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplication  

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Ok
ApplicationParameters  : {}

PS C:\> Get-ServiceFabricApplication | Get-ServiceFabricService

ServiceName            : fabric:/MyApp/Stateless1
ServiceKind            : Stateless
ServiceTypeName        : Stateless1Type
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
ServiceStatus          : Active
HealthState            : Ok
```

## <a name="remove-an-application"></a><span data-ttu-id="cccfd-208">移除應用程式</span><span class="sxs-lookup"><span data-stu-id="cccfd-208">Remove an application</span></span>
<span data-ttu-id="cccfd-209">當不再需要應用程式執行個體時，您可以永久移除它的名稱使用 hello[移除 ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="cccfd-209">When an application instance is no longer needed, you can permanently remove it by name using hello [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="cccfd-210">[移除 ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps)會自動移除屬於 toohello 應用程式以及，永久移除所有的服務狀態的所有服務。</span><span class="sxs-lookup"><span data-stu-id="cccfd-210">[Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) automatically removes all services that belong toohello application as well, permanently removing all service state.</span></span> 

> [!WARNING]
> <span data-ttu-id="cccfd-211">此作業無法回復，且應用程式狀態無法復原。</span><span class="sxs-lookup"><span data-stu-id="cccfd-211">This operation cannot be reversed, and application state cannot be recovered.</span></span>

```powershell
PS C:\> Remove-ServiceFabricApplication fabric:/MyApp

Confirm
Continue with this operation?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):
Remove application instance succeeded

PS C:\> Get-ServiceFabricApplication
```

## <a name="unregister-an-application-type"></a><span data-ttu-id="cccfd-212">取消註冊應用程式類型</span><span class="sxs-lookup"><span data-stu-id="cccfd-212">Unregister an application type</span></span>
<span data-ttu-id="cccfd-213">當不再需要特定版本的應用程式類型時，您應該取消註冊 hello 應用程式類型使用 hello[取消註冊 ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="cccfd-213">When a particular version of an application type is no longer needed, you should unregister hello application type using hello [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="cccfd-214">取消登錄未使用的應用程式類型版本所使用儲存空間 hello 映像存放區。</span><span class="sxs-lookup"><span data-stu-id="cccfd-214">Unregistering unused application types releases storage space used by hello image store.</span></span> <span data-ttu-id="cccfd-215">只要沒有對應的應用程式針對應用程式類型進行具現化，且沒有擱置中的應用程式升級進行參考該類性，便可取消註冊該應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="cccfd-215">An application type can be unregistered as long as no applications are instantiated against it and no pending application upgrades are referencing it.</span></span>

<span data-ttu-id="cccfd-216">執行[Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) toosee hello 應用程式類型目前已登錄在 hello 叢集中：</span><span class="sxs-lookup"><span data-stu-id="cccfd-216">Run [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) toosee hello application types currently registered in hello cluster:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

<span data-ttu-id="cccfd-217">執行[取消註冊 ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) toounregister 特定應用程式類型：</span><span class="sxs-lookup"><span data-stu-id="cccfd-217">Run [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) toounregister a specific application type:</span></span>

```powershell
PS C:\> Unregister-ServiceFabricApplicationType MyApplicationType 1.0.0
```

## <a name="remove-an-application-package-from-hello-image-store"></a><span data-ttu-id="cccfd-218">移除 hello 映像存放區中的應用程式套件</span><span class="sxs-lookup"><span data-stu-id="cccfd-218">Remove an application package from hello image store</span></span>
<span data-ttu-id="cccfd-219">當不再需要的應用程式封裝時，您可以將它刪除 hello 映像存放區 toofree 系統資源。</span><span class="sxs-lookup"><span data-stu-id="cccfd-219">When an application package is no longer needed, you can delete it from hello image store toofree up system resources.</span></span>

```powershell
PS C:\>Remove-ServiceFabricApplicationPackage -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest))
```

## <a name="troubleshooting"></a><span data-ttu-id="cccfd-220">疑難排解</span><span class="sxs-lookup"><span data-stu-id="cccfd-220">Troubleshooting</span></span>
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a><span data-ttu-id="cccfd-221">Copy-ServiceFabricApplicationPackage 要求 ImageStoreConnectionString</span><span class="sxs-lookup"><span data-stu-id="cccfd-221">Copy-ServiceFabricApplicationPackage asks for an ImageStoreConnectionString</span></span>
<span data-ttu-id="cccfd-222">hello Service Fabric SDK 環境應該已經有 hello 正確設定預設值。</span><span class="sxs-lookup"><span data-stu-id="cccfd-222">hello Service Fabric SDK environment should already have hello correct defaults set up.</span></span> <span data-ttu-id="cccfd-223">但所有命令的 hello ImageStoreConnectionString 如有需要應符合 hello 值該 hello Service Fabric 叢集所使用。</span><span class="sxs-lookup"><span data-stu-id="cccfd-223">But if needed, hello ImageStoreConnectionString for all commands should match hello value that hello Service Fabric cluster is using.</span></span> <span data-ttu-id="cccfd-224">您可以在 hello 叢集資訊清單中找到 hello ImageStoreConnectionString 使用 hello 擷取[Get ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps)和 Get ImageStoreConnectionStringFromClusterManifest 命令：</span><span class="sxs-lookup"><span data-stu-id="cccfd-224">You can find hello ImageStoreConnectionString in hello cluster manifest, retrieved using hello [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) and Get-ImageStoreConnectionStringFromClusterManifest commands:</span></span>

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

<span data-ttu-id="cccfd-225">hello **Get ImageStoreConnectionStringFromClusterManifest** cmdlet，這是 hello Service Fabric SDK PowerShell 模組的一部分，是使用的 tooget hello 映像儲存連接字串。</span><span class="sxs-lookup"><span data-stu-id="cccfd-225">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="cccfd-226">tooimport hello SDK 模組，執行：</span><span class="sxs-lookup"><span data-stu-id="cccfd-226">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="cccfd-227">hello ImageStoreConnectionString hello 叢集資訊清單中找到：</span><span class="sxs-lookup"><span data-stu-id="cccfd-227">hello ImageStoreConnectionString is found in hello cluster manifest:</span></span>

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

<span data-ttu-id="cccfd-228">請參閱[hello 映像存放區連接字串了解](service-fabric-image-store-connection-string.md)如需關於 hello 映像存放區，以及映像存放區連接字串的補充資訊。</span><span class="sxs-lookup"><span data-stu-id="cccfd-228">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

### <a name="deploy-large-application-package"></a><span data-ttu-id="cccfd-229">部署大型應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="cccfd-229">Deploy large application package</span></span>
<span data-ttu-id="cccfd-230">問題︰大型應用程式封裝 (GB 的順序) 的 [Copy-servicefabricapplicationpackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) 逾時。</span><span class="sxs-lookup"><span data-stu-id="cccfd-230">Issue: [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) times out for a large application package (order of GB).</span></span>
<span data-ttu-id="cccfd-231">請嘗試︰</span><span class="sxs-lookup"><span data-stu-id="cccfd-231">Try:</span></span>
- <span data-ttu-id="cccfd-232">使用`TimeoutSec`參數指定 [Copy-servicefabricapplicationpackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) 命令的較大逾時。</span><span class="sxs-lookup"><span data-stu-id="cccfd-232">Specify a larger timeout for [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command, with `TimeoutSec` parameter.</span></span> <span data-ttu-id="cccfd-233">根據預設，hello 逾時為 30 分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="cccfd-233">By default, hello timeout is 30 minutes.</span></span>
- <span data-ttu-id="cccfd-234">請檢查您的來源電腦與叢集之間的 hello 網路連線。</span><span class="sxs-lookup"><span data-stu-id="cccfd-234">Check hello network connection between your source machine and cluster.</span></span> <span data-ttu-id="cccfd-235">如果 hello 連接相當緩慢，請考慮使用較佳的網路連線的機器。</span><span class="sxs-lookup"><span data-stu-id="cccfd-235">If hello connection is slow, consider using a machine with a better network connection.</span></span>
<span data-ttu-id="cccfd-236">如果 hello 用戶端電腦 hello 叢集以外的另一個區域中，請考慮在接近或相同區域內的用戶端電腦使用為 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="cccfd-236">If hello client machine is in another region than hello cluster, consider using a client machine in a closer or same region as hello cluster.</span></span>
- <span data-ttu-id="cccfd-237">請檢查是否到達外部節流。</span><span class="sxs-lookup"><span data-stu-id="cccfd-237">Check if you are hitting external throttling.</span></span> <span data-ttu-id="cccfd-238">例如，設定的 toouse azure 儲存體 hello 映像存放區時，可能會進行節流處理上傳。</span><span class="sxs-lookup"><span data-stu-id="cccfd-238">For example, when hello image store is configured toouse azure storage, upload may be throttled.</span></span>

<span data-ttu-id="cccfd-239">問題︰上傳封裝順利完成，但 [Register-servicefabricapplicationtype](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) 逾時。請嘗試︰</span><span class="sxs-lookup"><span data-stu-id="cccfd-239">Issue: Upload package completed successfully, but [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) times out. Try:</span></span>
- <span data-ttu-id="cccfd-240">[壓縮 hello 封裝](service-fabric-package-apps.md#compress-a-package)複製 toohello 映像存放區之前。</span><span class="sxs-lookup"><span data-stu-id="cccfd-240">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span>
<span data-ttu-id="cccfd-241">hello 壓縮會減少 hello 大小，必須執行 hello 檔案數目，而後者可減少流量的 hello 數量和使用該服務的網狀架構。</span><span class="sxs-lookup"><span data-stu-id="cccfd-241">hello compression reduces hello size and hello number of files, which in turn reduces hello amount of traffic and work that Service Fabric must perform.</span></span> <span data-ttu-id="cccfd-242">hello 上傳作業可能會變慢 （特別是如果您包含 hello 壓縮時間），但註冊和取消註冊 hello 應用程式類型時，速度加快。</span><span class="sxs-lookup"><span data-stu-id="cccfd-242">hello upload operation may be slower (especially if you include hello compression time), but register and un-register hello application type are faster.</span></span>
- <span data-ttu-id="cccfd-243">使用 `TimeoutSec` 參數指定 [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) 的較大逾時。</span><span class="sxs-lookup"><span data-stu-id="cccfd-243">Specify a larger timeout for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) with `TimeoutSec` parameter.</span></span>
- <span data-ttu-id="cccfd-244">指定 [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) 的 `Async` 參數。</span><span class="sxs-lookup"><span data-stu-id="cccfd-244">Specify `Async` switch for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span></span> <span data-ttu-id="cccfd-245">hello 叢集接受 hello 命令並 hello 應用程式類型的 hello 註冊會以非同步方式繼續時，就會傳回 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="cccfd-245">hello command returns when hello cluster accepts hello command and hello registration of hello application type continues asynchronously.</span></span> <span data-ttu-id="cccfd-246">基於這個理由，沒有任何需要 toospecify 較高的逾時在此情況下。</span><span class="sxs-lookup"><span data-stu-id="cccfd-246">For this reason, there is no need toospecify a higher timeout in this case.</span></span> <span data-ttu-id="cccfd-247">hello [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps)命令列出所有已成功註冊應用程式類型版本及其註冊狀態。</span><span class="sxs-lookup"><span data-stu-id="cccfd-247">hello [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="cccfd-248">您可以使用這個命令 toodetermine hello 註冊完成。</span><span class="sxs-lookup"><span data-stu-id="cccfd-248">You can use this command toodetermine when hello registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

### <a name="deploy-application-package-with-many-files"></a><span data-ttu-id="cccfd-249">部署具有很多檔案的應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="cccfd-249">Deploy application package with many files</span></span>
<span data-ttu-id="cccfd-250">問題︰具有很多檔案的應用程式封裝 (以千計的順序) [Register-servicefabricapplicationtype](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) 的逾時。</span><span class="sxs-lookup"><span data-stu-id="cccfd-250">Issue: [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) times out for an application package with many files (order of thousands).</span></span>
<span data-ttu-id="cccfd-251">請嘗試︰</span><span class="sxs-lookup"><span data-stu-id="cccfd-251">Try:</span></span>
- <span data-ttu-id="cccfd-252">[壓縮 hello 封裝](service-fabric-package-apps.md#compress-a-package)複製 toohello 映像存放區之前。</span><span class="sxs-lookup"><span data-stu-id="cccfd-252">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span> <span data-ttu-id="cccfd-253">hello 壓縮會減少檔案的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="cccfd-253">hello compression reduces hello number of files.</span></span>
- <span data-ttu-id="cccfd-254">使用 `TimeoutSec` 參數指定 [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) 的較大逾時。</span><span class="sxs-lookup"><span data-stu-id="cccfd-254">Specify a larger timeout for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) with `TimeoutSec` parameter.</span></span>
- <span data-ttu-id="cccfd-255">指定 [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) 的 `Async` 參數。</span><span class="sxs-lookup"><span data-stu-id="cccfd-255">Specify `Async` switch for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span></span> <span data-ttu-id="cccfd-256">hello 叢集接受 hello 命令並 hello 應用程式類型的 hello 註冊會以非同步方式繼續時，就會傳回 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="cccfd-256">hello command returns when hello cluster accepts hello command and hello registration of hello application type continues asynchronously.</span></span>
<span data-ttu-id="cccfd-257">基於這個理由，沒有任何需要 toospecify 較高的逾時在此情況下。</span><span class="sxs-lookup"><span data-stu-id="cccfd-257">For this reason, there is no need toospecify a higher timeout in this case.</span></span> <span data-ttu-id="cccfd-258">hello [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps)命令列出所有已成功註冊應用程式類型版本及其註冊狀態。</span><span class="sxs-lookup"><span data-stu-id="cccfd-258">hello [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="cccfd-259">您可以使用這個命令 toodetermine hello 註冊完成。</span><span class="sxs-lookup"><span data-stu-id="cccfd-259">You can use this command toodetermine when hello registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="next-steps"></a><span data-ttu-id="cccfd-260">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cccfd-260">Next steps</span></span>
[<span data-ttu-id="cccfd-261">Service Fabric 應用程式升級</span><span class="sxs-lookup"><span data-stu-id="cccfd-261">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="cccfd-262">Service Fabric 健康狀態簡介</span><span class="sxs-lookup"><span data-stu-id="cccfd-262">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)

[<span data-ttu-id="cccfd-263">診斷和疑難排解 Service Fabric 服務</span><span class="sxs-lookup"><span data-stu-id="cccfd-263">Diagnose and troubleshoot a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="cccfd-264">在 Service Fabric 中模型化應用程式</span><span class="sxs-lookup"><span data-stu-id="cccfd-264">Model an application in Service Fabric</span></span>](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
