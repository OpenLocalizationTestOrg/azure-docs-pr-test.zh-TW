---
title: "Azure Service Fabric 應用程式部署 | Microsoft Docs"
description: "如何使用 PowerShell 部署和移除 Service Fabric 中的應用程式。"
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
ms.openlocfilehash: edef23a8cdab7fd0bef54456f0caabb9db273bf9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-and-remove-applications-using-powershell"></a><span data-ttu-id="feac8-103">使用 PowerShell 部署與移除應用程式</span><span class="sxs-lookup"><span data-stu-id="feac8-103">Deploy and remove applications using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="feac8-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="feac8-104">PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
> * [<span data-ttu-id="feac8-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="feac8-105">Visual Studio</span></span>](service-fabric-publish-app-remote-cluster.md)
> * [<span data-ttu-id="feac8-106">FabricClient API</span><span class="sxs-lookup"><span data-stu-id="feac8-106">FabricClient APIs</span></span>](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

<span data-ttu-id="feac8-107">[封裝應用程式類型][10]後，即可將它部署至 Azure Service Fabric 叢集中。</span><span class="sxs-lookup"><span data-stu-id="feac8-107">Once an [application type has been packaged][10], it's ready for deployment into an Azure Service Fabric cluster.</span></span> <span data-ttu-id="feac8-108">部署涉及下列三個步驟：</span><span class="sxs-lookup"><span data-stu-id="feac8-108">Deployment involves the following three steps:</span></span>

1. <span data-ttu-id="feac8-109">將應用程式封裝上傳至映像存放區</span><span class="sxs-lookup"><span data-stu-id="feac8-109">Upload the application package to the image store</span></span>
2. <span data-ttu-id="feac8-110">註冊應用程式類型</span><span class="sxs-lookup"><span data-stu-id="feac8-110">Register the application type</span></span>
3. <span data-ttu-id="feac8-111">建立應用程式執行個體</span><span class="sxs-lookup"><span data-stu-id="feac8-111">Create the application instance</span></span>

<span data-ttu-id="feac8-112">在應用程式中部署且個體開始在叢集中執行之後，您就可以刪除應用程式執行個體和其應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="feac8-112">After an application is deployed and an instance is running in the cluster, you can delete the application instance and its application type.</span></span> <span data-ttu-id="feac8-113">從叢集完全移除應用程式需要執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="feac8-113">To completely remove an application from the cluster involves the following steps:</span></span>

1. <span data-ttu-id="feac8-114">移除 (或刪除) 執行中的應用程式執行個體</span><span class="sxs-lookup"><span data-stu-id="feac8-114">Remove (or delete) the running application instance</span></span>
2. <span data-ttu-id="feac8-115">取消註冊不再需要的應用程式類型</span><span class="sxs-lookup"><span data-stu-id="feac8-115">Unregister the application type if you no longer need it</span></span>
3. <span data-ttu-id="feac8-116">移除映像存放區中的應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="feac8-116">Remove the application package from the image store</span></span>

<span data-ttu-id="feac8-117">如果您在本機開發叢集上使用 [Visual Studio 部署和偵錯應用程式](service-fabric-publish-app-remote-cluster.md)，則先前所有步驟都會透過 PowerShell 指令碼自動處理。</span><span class="sxs-lookup"><span data-stu-id="feac8-117">If you use [Visual Studio for deploying and debugging applications](service-fabric-publish-app-remote-cluster.md) on your local development cluster, all the preceding steps are handled automatically through a PowerShell script.</span></span>  <span data-ttu-id="feac8-118">在應用程式專案的 [指令碼] 資料夾中可找到這個指令碼。</span><span class="sxs-lookup"><span data-stu-id="feac8-118">This script is found in the *Scripts* folder of the application project.</span></span> <span data-ttu-id="feac8-119">本文提供該指令碼的背景資料，讓您可以在 Visual Studio 之外執行相同的作業。</span><span class="sxs-lookup"><span data-stu-id="feac8-119">This article provides background on what that script is doing so that you can perform the same operations outside of Visual Studio.</span></span> 
 
## <a name="connect-to-the-cluster"></a><span data-ttu-id="feac8-120">連接到叢集</span><span class="sxs-lookup"><span data-stu-id="feac8-120">Connect to the cluster</span></span>
<span data-ttu-id="feac8-121">執行本文中的任何 PowerShell 命令之前，請一律透過使用 [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) 連接至 Service Fabric 叢集的方式啟動。</span><span class="sxs-lookup"><span data-stu-id="feac8-121">Before you run any PowerShell commands in this article, always start by using [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) to connect to the Service Fabric cluster.</span></span> <span data-ttu-id="feac8-122">若要連線至本機開發叢集，請執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="feac8-122">To connect to the local development cluster, run the following:</span></span>

```powershell
PS C:\>Connect-ServiceFabricCluster
```

<span data-ttu-id="feac8-123">針對連線至遠端叢集，或連線至使用 Azure Active Directory、X509 憑證或 Windows Active Directory 保護的叢集，如需相關的範例，請參閱[連線至安全的叢集](service-fabric-connect-to-secure-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="feac8-123">For examples of connecting to a remote cluster or cluster secured using Azure Active Directory, X509 certificates, or Windows Active Directory see [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

## <a name="upload-the-application-package"></a><span data-ttu-id="feac8-124">上傳應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="feac8-124">Upload the application package</span></span>
<span data-ttu-id="feac8-125">上傳應用程式封裝會將它放在一個可由內部 Service Fabric 元件存取的位置。</span><span class="sxs-lookup"><span data-stu-id="feac8-125">Uploading the application package puts it in a location that's accessible by internal Service Fabric components.</span></span>
<span data-ttu-id="feac8-126">如果您想要在本機確認應用程式封裝，使用 [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="feac8-126">If you want to verify the application package locally, use the [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="feac8-127">[Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) 命令會將應用程式封裝上傳至叢集映像存放區。</span><span class="sxs-lookup"><span data-stu-id="feac8-127">The [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command uploads the application package to the cluster image store.</span></span>
<span data-ttu-id="feac8-128">**Get ImageStoreConnectionStringFromClusterManifest** Cmdlet 是 Service Fabric SDK PowerShell 模組的一部分，可用來取得映像存放區連接字串。</span><span class="sxs-lookup"><span data-stu-id="feac8-128">The **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of the Service Fabric SDK PowerShell module, is used to get the image store connection string.</span></span>  <span data-ttu-id="feac8-129">若要匯入 SDK 模組，請執行︰</span><span class="sxs-lookup"><span data-stu-id="feac8-129">To import the SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="feac8-130">假設您在 Visual Studio 2015 中建置並封裝名為 *MyApplication* 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="feac8-130">Suppose you build and package an application named *MyApplication* in Visual Studio 2015.</span></span> <span data-ttu-id="feac8-131">根據預設，ApplicationManifest.xml 中列出的應用程式類型名稱會是 "MyApplicationType"。</span><span class="sxs-lookup"><span data-stu-id="feac8-131">By default, the application type name listed in the ApplicationManifest.xml is "MyApplicationType".</span></span>  <span data-ttu-id="feac8-132">應用程式封裝 (其中包含必要的應用程式資訊清單、服務資訊清單和程式碼/組態/資料封裝) 位於 *C:\Users\<username\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug*。</span><span class="sxs-lookup"><span data-stu-id="feac8-132">The application package, which contains the necessary application manifest, service manifests, and code/config/data packages, is located in *C:\Users\<username\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug*.</span></span> 

<span data-ttu-id="feac8-133">下列命令會列出應用程式封裝的內容︰</span><span class="sxs-lookup"><span data-stu-id="feac8-133">The following command lists the contents of the application package:</span></span>

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

<span data-ttu-id="feac8-134">如果應用程式封裝是大型且/或有許多檔案，您可以[壓縮](service-fabric-package-apps.md#compress-a-package)。</span><span class="sxs-lookup"><span data-stu-id="feac8-134">If the application package is large and/or has many files, you can [compress it](service-fabric-package-apps.md#compress-a-package).</span></span> <span data-ttu-id="feac8-135">壓縮會減少檔案大小和數目。</span><span class="sxs-lookup"><span data-stu-id="feac8-135">The compression reduces the size and the number of files.</span></span>
<span data-ttu-id="feac8-136">副作用是註冊和取消註冊應用程式類型會比較快。</span><span class="sxs-lookup"><span data-stu-id="feac8-136">The side effect is that registering and un-registering the application type are faster.</span></span> <span data-ttu-id="feac8-137">目前上傳時間可能會變慢，特別是當您包含壓縮封裝的時間。</span><span class="sxs-lookup"><span data-stu-id="feac8-137">Upload time may be slower currently, especially if you include the time to compress the package.</span></span> 

<span data-ttu-id="feac8-138">若要壓縮封裝，請使用相同的 [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) 命令。</span><span class="sxs-lookup"><span data-stu-id="feac8-138">To compress a package, use the same [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command.</span></span> <span data-ttu-id="feac8-139">壓縮可與上傳分開進行，方法為使用 `SkipCopy` 旗標，或是與上傳作業共同進行。</span><span class="sxs-lookup"><span data-stu-id="feac8-139">Compression can be done separate from upload, by using the `SkipCopy` flag, or together with the upload operation.</span></span> <span data-ttu-id="feac8-140">在壓縮封裝上套用壓縮為無作業。</span><span class="sxs-lookup"><span data-stu-id="feac8-140">Applying compression on a compressed package is no-op.</span></span>
<span data-ttu-id="feac8-141">若要將已壓縮的封裝解壓縮，請使用相同的 [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) 命令搭配 `UncompressPackage` 參數。</span><span class="sxs-lookup"><span data-stu-id="feac8-141">To uncompress a compressed package, use the same [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command with the `UncompressPackage` switch.</span></span>

<span data-ttu-id="feac8-142">下列 Cmdlet 會在不將封裝複製到映像存放區的情況下壓縮封裝。</span><span class="sxs-lookup"><span data-stu-id="feac8-142">The following cmdlet compresses the package without copying it to the image store.</span></span> <span data-ttu-id="feac8-143">該套件現在包含 `Code` 及 `Config` 封裝的 ZIP 壓縮檔案。</span><span class="sxs-lookup"><span data-stu-id="feac8-143">The package now includes zipped files for the `Code` and `Config` packages.</span></span> <span data-ttu-id="feac8-144">應用程式和服務資訊清單不會壓縮，因為有許多內部作業都需要它們 (例如特定驗證的封裝共用、應用程式類型名稱及版本擷取)。</span><span class="sxs-lookup"><span data-stu-id="feac8-144">The application and the service manifests are not zipped, because they are needed for many internal operations (like package sharing, application type name and version extraction for certain validations).</span></span> <span data-ttu-id="feac8-145">對資訊清單進行壓縮，將會使這些作業效率不佳。</span><span class="sxs-lookup"><span data-stu-id="feac8-145">Zipping the manifests would make these operations inefficient.</span></span>

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

<span data-ttu-id="feac8-146">針對大型應用程式封裝，壓縮會很花時間。</span><span class="sxs-lookup"><span data-stu-id="feac8-146">For large application packages, the compression takes time.</span></span> <span data-ttu-id="feac8-147">為了獲得最佳結果，請使用快速的 SSD 磁碟機。</span><span class="sxs-lookup"><span data-stu-id="feac8-147">For best results, use a fast SSD drive.</span></span> <span data-ttu-id="feac8-148">壓縮時間和已壓縮封裝的大小也會根據封裝內容而有所不同。</span><span class="sxs-lookup"><span data-stu-id="feac8-148">The compression times and the size of the compressed package also differ based on the package content.</span></span>
<span data-ttu-id="feac8-149">例如，以下是一些封裝的壓縮統計資料，其顯示初始和壓縮的封裝大小，以壓縮時間。</span><span class="sxs-lookup"><span data-stu-id="feac8-149">For example, here is compression statistics for some packages, which show the initial and the compressed package size, with the compression time.</span></span>

|<span data-ttu-id="feac8-150">初始大小 (MB)</span><span class="sxs-lookup"><span data-stu-id="feac8-150">Initial size (MB)</span></span>|<span data-ttu-id="feac8-151">檔案計數</span><span class="sxs-lookup"><span data-stu-id="feac8-151">File count</span></span>|<span data-ttu-id="feac8-152">壓縮時間</span><span class="sxs-lookup"><span data-stu-id="feac8-152">Compression Time</span></span>|<span data-ttu-id="feac8-153">壓縮的封裝大小 (MB)</span><span class="sxs-lookup"><span data-stu-id="feac8-153">Compressed package size (MB)</span></span>|
|----------------:|---------:|---------------:|---------------------------:|
|<span data-ttu-id="feac8-154">100</span><span class="sxs-lookup"><span data-stu-id="feac8-154">100</span></span>|<span data-ttu-id="feac8-155">100</span><span class="sxs-lookup"><span data-stu-id="feac8-155">100</span></span>|<span data-ttu-id="feac8-156">00:00:03.3547592</span><span class="sxs-lookup"><span data-stu-id="feac8-156">00:00:03.3547592</span></span>|<span data-ttu-id="feac8-157">60</span><span class="sxs-lookup"><span data-stu-id="feac8-157">60</span></span>|
|<span data-ttu-id="feac8-158">512</span><span class="sxs-lookup"><span data-stu-id="feac8-158">512</span></span>|<span data-ttu-id="feac8-159">100</span><span class="sxs-lookup"><span data-stu-id="feac8-159">100</span></span>|<span data-ttu-id="feac8-160">00:00:16.3850303</span><span class="sxs-lookup"><span data-stu-id="feac8-160">00:00:16.3850303</span></span>|<span data-ttu-id="feac8-161">307</span><span class="sxs-lookup"><span data-stu-id="feac8-161">307</span></span>|
|<span data-ttu-id="feac8-162">1024</span><span class="sxs-lookup"><span data-stu-id="feac8-162">1024</span></span>|<span data-ttu-id="feac8-163">500</span><span class="sxs-lookup"><span data-stu-id="feac8-163">500</span></span>|<span data-ttu-id="feac8-164">00:00:32.5907950</span><span class="sxs-lookup"><span data-stu-id="feac8-164">00:00:32.5907950</span></span>|<span data-ttu-id="feac8-165">615</span><span class="sxs-lookup"><span data-stu-id="feac8-165">615</span></span>|
|<span data-ttu-id="feac8-166">2048</span><span class="sxs-lookup"><span data-stu-id="feac8-166">2048</span></span>|<span data-ttu-id="feac8-167">1000</span><span class="sxs-lookup"><span data-stu-id="feac8-167">1000</span></span>|<span data-ttu-id="feac8-168">00:01:04.3775554</span><span class="sxs-lookup"><span data-stu-id="feac8-168">00:01:04.3775554</span></span>|<span data-ttu-id="feac8-169">1231</span><span class="sxs-lookup"><span data-stu-id="feac8-169">1231</span></span>|
|<span data-ttu-id="feac8-170">5012</span><span class="sxs-lookup"><span data-stu-id="feac8-170">5012</span></span>|<span data-ttu-id="feac8-171">100</span><span class="sxs-lookup"><span data-stu-id="feac8-171">100</span></span>|<span data-ttu-id="feac8-172">00:02:45.2951288</span><span class="sxs-lookup"><span data-stu-id="feac8-172">00:02:45.2951288</span></span>|<span data-ttu-id="feac8-173">3074</span><span class="sxs-lookup"><span data-stu-id="feac8-173">3074</span></span>|

<span data-ttu-id="feac8-174">一旦壓縮封裝後，可以視需要將它上傳到一或多個 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="feac8-174">Once a package is compressed, it can be uploaded to one or multiple Service Fabric clusters as needed.</span></span> <span data-ttu-id="feac8-175">已壓縮及未壓縮套件的部署機制皆相同。</span><span class="sxs-lookup"><span data-stu-id="feac8-175">The deployment mechanism is same for compressed and uncompressed packages.</span></span> <span data-ttu-id="feac8-176">如果封裝已壓縮，它會以壓縮的形式儲存在叢集映像存放區中，並在應用程式執行之前於節點上解壓縮。</span><span class="sxs-lookup"><span data-stu-id="feac8-176">If the package is compressed, it is stored as such in the cluster image store and it's uncompressed on the node before the application is run.</span></span>


<span data-ttu-id="feac8-177">下列範例會將套件上傳至映像存放區中的 "MyApplicationV1" 資料夾︰</span><span class="sxs-lookup"><span data-stu-id="feac8-177">The following example uploads the package to the image store, into a folder named "MyApplicationV1":</span></span>

```powershell
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)) -TimeoutSec 1800
```

<span data-ttu-id="feac8-178">**Get ImageStoreConnectionStringFromClusterManifest** Cmdlet 是 Service Fabric SDK PowerShell 模組的一部分，可用來取得映像存放區連接字串。</span><span class="sxs-lookup"><span data-stu-id="feac8-178">The **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of the Service Fabric SDK PowerShell module, is used to get the image store connection string.</span></span>  <span data-ttu-id="feac8-179">若要匯入 SDK 模組，請執行︰</span><span class="sxs-lookup"><span data-stu-id="feac8-179">To import the SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="feac8-180">如果您未指定 -ApplicationPackagePathInImageStore 參數，應用程式套件會複製到映像存放區中的 "Debug" 資料夾。</span><span class="sxs-lookup"><span data-stu-id="feac8-180">If you do not specify the *-ApplicationPackagePathInImageStore* parameter, the application package is copied into the "Debug" folder in the image store.</span></span>

<span data-ttu-id="feac8-181">上傳封裝的時間會根據多個因素而有所不同。</span><span class="sxs-lookup"><span data-stu-id="feac8-181">The time it takes to upload a package differs depending on multiple factors.</span></span> <span data-ttu-id="feac8-182">這些因素有些是封裝中的檔案數目、封裝大小和檔案大小。</span><span class="sxs-lookup"><span data-stu-id="feac8-182">Some of these factors are the number of files in the package, the package size, and the file sizes.</span></span> <span data-ttu-id="feac8-183">在來源電腦及 Service Fabric 叢集之間的網路速度也會影響上傳時間。</span><span class="sxs-lookup"><span data-stu-id="feac8-183">The network speed between the source machine and the Service Fabric cluster also impacts the upload time.</span></span> <span data-ttu-id="feac8-184">[Copy-servicefabricapplicationpackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) 的預設逾時值為 30 分鐘。</span><span class="sxs-lookup"><span data-stu-id="feac8-184">The default timeout for [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) is 30 minutes.</span></span>
<span data-ttu-id="feac8-185">根據所述的因素，您可能必須增加逾時。</span><span class="sxs-lookup"><span data-stu-id="feac8-185">Depending on the described factors, you may have to increase the timeout.</span></span> <span data-ttu-id="feac8-186">如果要在複製呼叫中壓縮封裝，您需要同時考慮壓縮時間。</span><span class="sxs-lookup"><span data-stu-id="feac8-186">If you are compressing the package in the copy call, you need to also consider the compression time.</span></span>

<span data-ttu-id="feac8-187">請參閱[了解映像存放區連接字串](service-fabric-image-store-connection-string.md)，以取得有關映像存放區和映像存放區連接字串的補充資訊。</span><span class="sxs-lookup"><span data-stu-id="feac8-187">See [Understand the image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about the image store and image store connection string.</span></span>

## <a name="register-the-application-package"></a><span data-ttu-id="feac8-188">註冊應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="feac8-188">Register the application package</span></span>
<span data-ttu-id="feac8-189">註冊應用程式套件時，應用程式類型和應用程式資訊清單中宣告的版本可供使用。</span><span class="sxs-lookup"><span data-stu-id="feac8-189">The application type and version declared in the application manifest become available for use when the application package is registered.</span></span> <span data-ttu-id="feac8-190">系統會讀取在上一個步驟上傳的套件，請確認套件、處理套件內容，然後將處理過的套件複製至內部系統位置。</span><span class="sxs-lookup"><span data-stu-id="feac8-190">The system reads the package uploaded in the previous step, verifies the package, processes the package contents, and copies the processed package to an internal system location.</span></span>  

<span data-ttu-id="feac8-191">執行 [Register-servicefabricapplicationtype](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) Cmdlet，將應用程式類型註冊在叢集，使它可供部署使用︰</span><span class="sxs-lookup"><span data-stu-id="feac8-191">Run the [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet to register the application type in the cluster and make it available for deployment:</span></span>

```powershell
PS C:\> Register-ServiceFabricApplicationType MyApplicationV1
Register application type succeeded
```

<span data-ttu-id="feac8-192">"MyApplicationV1" 是應用程式套件所在映像存放區中的資料夾。</span><span class="sxs-lookup"><span data-stu-id="feac8-192">"MyApplicationV1" is the folder in the image store where the application package is located.</span></span> <span data-ttu-id="feac8-193">名稱為 "MyApplicationType" 和版本為 "1.0.0" (兩者都在應用程式資訊清單中) 的應用程式類型，現在已註冊在叢集中。</span><span class="sxs-lookup"><span data-stu-id="feac8-193">The application type with name "MyApplicationType" and version "1.0.0" (both are found in the application manifest) is now registered in the cluster.</span></span>

<span data-ttu-id="feac8-194">[Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) 命令只有在系統成功註冊應用程式封裝之後才會返回。</span><span class="sxs-lookup"><span data-stu-id="feac8-194">The [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) command returns only after the system has successfully registered the application package.</span></span> <span data-ttu-id="feac8-195">註冊所需時間取決於應用程式封裝的大小和內容。</span><span class="sxs-lookup"><span data-stu-id="feac8-195">How long registration takes depends on the size and contents of the application package.</span></span> <span data-ttu-id="feac8-196">**-TimeoutSec** 參數可在必要時用來提供較長的逾時 (預設逾時為 60 秒)。</span><span class="sxs-lookup"><span data-stu-id="feac8-196">If needed, the **-TimeoutSec** parameter can be used to supply a longer timeout (the default timeout is 60 seconds).</span></span>

<span data-ttu-id="feac8-197">如果您有大型應用程式套件或如果您遇到逾時，使用 **-Async** 參數。</span><span class="sxs-lookup"><span data-stu-id="feac8-197">If you have a large application package or if you are experiencing timeouts, use the **-Async** parameter.</span></span> <span data-ttu-id="feac8-198">當叢集接受暫存器命令時會傳回此命令，並視需要繼續處理。</span><span class="sxs-lookup"><span data-stu-id="feac8-198">The command returns when the cluster accepts the register command, and the processing continues as needed.</span></span>
<span data-ttu-id="feac8-199">[Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) 命令會列出所有成功註冊的應用程式類型版本和其註冊狀態。</span><span class="sxs-lookup"><span data-stu-id="feac8-199">The [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="feac8-200">您可以使用此命令以判斷何時會完成註冊。</span><span class="sxs-lookup"><span data-stu-id="feac8-200">You can use this command to determine when the registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="create-the-application"></a><span data-ttu-id="feac8-201">建立應用程式</span><span class="sxs-lookup"><span data-stu-id="feac8-201">Create the application</span></span>
<span data-ttu-id="feac8-202">您可以使用 [New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) Cmdlet，從任何已成功註冊的應用程式類型版本，將應用程式具現化。</span><span class="sxs-lookup"><span data-stu-id="feac8-202">You can instantiate an application from any application type version that has been registered successfully by using the [New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="feac8-203">每個應用程式名稱的開頭必須為 "fabric:" 配置，而且必須是每個應用程式執行個體的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="feac8-203">The name of each application must start with the *"fabric:"* scheme and must be unique for each application instance.</span></span> <span data-ttu-id="feac8-204">如果已在目標應用程式類型的應用程式資訊清單中定義預設服務，也會一併建立這些服務。</span><span class="sxs-lookup"><span data-stu-id="feac8-204">Any default services defined in the application manifest of the target application type are also created.</span></span>

```powershell
PS C:\> New-ServiceFabricApplication fabric:/MyApp MyApplicationType 1.0.0

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationParameters  : {}
```
<span data-ttu-id="feac8-205">多個應用程式執行個體可以針對任何指定的已註冊應用程式類型版本來建立。</span><span class="sxs-lookup"><span data-stu-id="feac8-205">Multiple application instances can be created for any given version of a registered application type.</span></span> <span data-ttu-id="feac8-206">每個應用程式執行個體將在隔離狀態下執行，包含本身的工作目錄和程序。</span><span class="sxs-lookup"><span data-stu-id="feac8-206">Each application instance runs in isolation, with its own work directory and process.</span></span>

<span data-ttu-id="feac8-207">若要查看哪些具名的應用程式和服務正在叢集中執行，請執行 [Get-servicefabricapplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) 和 [Get-servicefabricservice](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) Cmdlet︰</span><span class="sxs-lookup"><span data-stu-id="feac8-207">To see which named apps and services are running in the cluster, run the [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) and [Get-ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) cmdlets:</span></span>

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

## <a name="remove-an-application"></a><span data-ttu-id="feac8-208">移除應用程式</span><span class="sxs-lookup"><span data-stu-id="feac8-208">Remove an application</span></span>
<span data-ttu-id="feac8-209">當不再需要應用程式執行個體時，您可以使用 [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) Cmdlet，依名稱永久移除它。</span><span class="sxs-lookup"><span data-stu-id="feac8-209">When an application instance is no longer needed, you can permanently remove it by name using the [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="feac8-210">[Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) 也會自動移除屬於應用程式的所有服務，永久地移除所有服務狀態。</span><span class="sxs-lookup"><span data-stu-id="feac8-210">[Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) automatically removes all services that belong to the application as well, permanently removing all service state.</span></span> 

> [!WARNING]
> <span data-ttu-id="feac8-211">此作業無法回復，且應用程式狀態無法復原。</span><span class="sxs-lookup"><span data-stu-id="feac8-211">This operation cannot be reversed, and application state cannot be recovered.</span></span>

```powershell
PS C:\> Remove-ServiceFabricApplication fabric:/MyApp

Confirm
Continue with this operation?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):
Remove application instance succeeded

PS C:\> Get-ServiceFabricApplication
```

## <a name="unregister-an-application-type"></a><span data-ttu-id="feac8-212">取消註冊應用程式類型</span><span class="sxs-lookup"><span data-stu-id="feac8-212">Unregister an application type</span></span>
<span data-ttu-id="feac8-213">當不再需要應用程式類型的特定版本時，您應該使用 [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) Cmdlet 取消註冊該應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="feac8-213">When a particular version of an application type is no longer needed, you should unregister the application type using the [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="feac8-214">取消註冊未使用的應用程式類型會釋放映像存放區已使用的儲存空間。</span><span class="sxs-lookup"><span data-stu-id="feac8-214">Unregistering unused application types releases storage space used by the image store.</span></span> <span data-ttu-id="feac8-215">只要沒有對應的應用程式針對應用程式類型進行具現化，且沒有擱置中的應用程式升級進行參考該類性，便可取消註冊該應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="feac8-215">An application type can be unregistered as long as no applications are instantiated against it and no pending application upgrades are referencing it.</span></span>

<span data-ttu-id="feac8-216">執行 [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) Cmdlet，查看目前註冊在叢集中的應用程式類型：</span><span class="sxs-lookup"><span data-stu-id="feac8-216">Run [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) to see the application types currently registered in the cluster:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

<span data-ttu-id="feac8-217">執行 [Unregister-servicefabricapplicationtype](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps)，取消註冊特定應用程式類型︰</span><span class="sxs-lookup"><span data-stu-id="feac8-217">Run [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) to unregister a specific application type:</span></span>

```powershell
PS C:\> Unregister-ServiceFabricApplicationType MyApplicationType 1.0.0
```

## <a name="remove-an-application-package-from-the-image-store"></a><span data-ttu-id="feac8-218">從映像存放區移除應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="feac8-218">Remove an application package from the image store</span></span>
<span data-ttu-id="feac8-219">當不再需要應用程式封裝時，您可以從映像存放區刪除它，以釋放系統資源。</span><span class="sxs-lookup"><span data-stu-id="feac8-219">When an application package is no longer needed, you can delete it from the image store to free up system resources.</span></span>

```powershell
PS C:\>Remove-ServiceFabricApplicationPackage -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest))
```

## <a name="troubleshooting"></a><span data-ttu-id="feac8-220">疑難排解</span><span class="sxs-lookup"><span data-stu-id="feac8-220">Troubleshooting</span></span>
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a><span data-ttu-id="feac8-221">Copy-ServiceFabricApplicationPackage 要求 ImageStoreConnectionString</span><span class="sxs-lookup"><span data-stu-id="feac8-221">Copy-ServiceFabricApplicationPackage asks for an ImageStoreConnectionString</span></span>
<span data-ttu-id="feac8-222">Service Fabric SDK 環境應已正確設定預設值。</span><span class="sxs-lookup"><span data-stu-id="feac8-222">The Service Fabric SDK environment should already have the correct defaults set up.</span></span> <span data-ttu-id="feac8-223">但若有需要，所有命令的 ImageStoreConnectionString都應符合 Service Fabric 叢集正在使用的值。</span><span class="sxs-lookup"><span data-stu-id="feac8-223">But if needed, the ImageStoreConnectionString for all commands should match the value that the Service Fabric cluster is using.</span></span> <span data-ttu-id="feac8-224">您可以在使用 [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) 和 Get-ImageStoreConnectionStringFromClusterManifest 命令擷取的叢集資訊清單 ImageStoreConnectionString 中找到此值：</span><span class="sxs-lookup"><span data-stu-id="feac8-224">You can find the ImageStoreConnectionString in the cluster manifest, retrieved using the [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) and Get-ImageStoreConnectionStringFromClusterManifest commands:</span></span>

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

<span data-ttu-id="feac8-225">**Get ImageStoreConnectionStringFromClusterManifest** Cmdlet 是 Service Fabric SDK PowerShell 模組的一部分，可用來取得映像存放區連接字串。</span><span class="sxs-lookup"><span data-stu-id="feac8-225">The **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of the Service Fabric SDK PowerShell module, is used to get the image store connection string.</span></span>  <span data-ttu-id="feac8-226">若要匯入 SDK 模組，請執行︰</span><span class="sxs-lookup"><span data-stu-id="feac8-226">To import the SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="feac8-227">會在叢集資訊清單中找到 ImageStoreConnectionString：</span><span class="sxs-lookup"><span data-stu-id="feac8-227">The ImageStoreConnectionString is found in the cluster manifest:</span></span>

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

<span data-ttu-id="feac8-228">請參閱[了解映像存放區連接字串](service-fabric-image-store-connection-string.md)，以取得有關映像存放區和映像存放區連接字串的補充資訊。</span><span class="sxs-lookup"><span data-stu-id="feac8-228">See [Understand the image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about the image store and image store connection string.</span></span>

### <a name="deploy-large-application-package"></a><span data-ttu-id="feac8-229">部署大型應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="feac8-229">Deploy large application package</span></span>
<span data-ttu-id="feac8-230">問題︰大型應用程式封裝 (GB 的順序) 的 [Copy-servicefabricapplicationpackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) 逾時。</span><span class="sxs-lookup"><span data-stu-id="feac8-230">Issue: [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) times out for a large application package (order of GB).</span></span>
<span data-ttu-id="feac8-231">請嘗試︰</span><span class="sxs-lookup"><span data-stu-id="feac8-231">Try:</span></span>
- <span data-ttu-id="feac8-232">使用`TimeoutSec`參數指定 [Copy-servicefabricapplicationpackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) 命令的較大逾時。</span><span class="sxs-lookup"><span data-stu-id="feac8-232">Specify a larger timeout for [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command, with `TimeoutSec` parameter.</span></span> <span data-ttu-id="feac8-233">此逾時預設為 30 分鐘。</span><span class="sxs-lookup"><span data-stu-id="feac8-233">By default, the timeout is 30 minutes.</span></span>
- <span data-ttu-id="feac8-234">檢查來源電腦與叢集之間的網路連線。</span><span class="sxs-lookup"><span data-stu-id="feac8-234">Check the network connection between your source machine and cluster.</span></span> <span data-ttu-id="feac8-235">如果連線速度變慢，請考慮使用更佳網路連線的電腦。</span><span class="sxs-lookup"><span data-stu-id="feac8-235">If the connection is slow, consider using a machine with a better network connection.</span></span>
<span data-ttu-id="feac8-236">如果用戶端電腦與叢集在不同的區域中，請考慮使用與叢集接近或相同區域中的用戶端電腦。</span><span class="sxs-lookup"><span data-stu-id="feac8-236">If the client machine is in another region than the cluster, consider using a client machine in a closer or same region as the cluster.</span></span>
- <span data-ttu-id="feac8-237">請檢查是否到達外部節流。</span><span class="sxs-lookup"><span data-stu-id="feac8-237">Check if you are hitting external throttling.</span></span> <span data-ttu-id="feac8-238">例如，當映像存放區設定為使用 Azure 儲存體時，上傳可能受到節流控制。</span><span class="sxs-lookup"><span data-stu-id="feac8-238">For example, when the image store is configured to use azure storage, upload may be throttled.</span></span>

<span data-ttu-id="feac8-239">問題︰上傳封裝順利完成，但 [Register-servicefabricapplicationtype](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) 逾時。</span><span class="sxs-lookup"><span data-stu-id="feac8-239">Issue: Upload package completed successfully, but [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) times out.</span></span>
<span data-ttu-id="feac8-240">請嘗試︰</span><span class="sxs-lookup"><span data-stu-id="feac8-240">Try:</span></span>
- <span data-ttu-id="feac8-241">複製到映像存放區之前[壓縮封裝](service-fabric-package-apps.md#compress-a-package)。</span><span class="sxs-lookup"><span data-stu-id="feac8-241">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store.</span></span>
<span data-ttu-id="feac8-242">壓縮會減少檔案的大小和數目，而後者則可減少資料傳輸量和 Service Fabric 必須執行的工作。</span><span class="sxs-lookup"><span data-stu-id="feac8-242">The compression reduces the size and the number of files, which in turn reduces the amount of traffic and work that Service Fabric must perform.</span></span> <span data-ttu-id="feac8-243">上傳作業可能會變慢 (尤其是如果您包含壓縮時間)，但註冊和取消註冊應用程式類型會比較快。</span><span class="sxs-lookup"><span data-stu-id="feac8-243">The upload operation may be slower (especially if you include the compression time), but register and un-register the application type are faster.</span></span>
- <span data-ttu-id="feac8-244">使用 `TimeoutSec` 參數指定 [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) 的較大逾時。</span><span class="sxs-lookup"><span data-stu-id="feac8-244">Specify a larger timeout for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) with `TimeoutSec` parameter.</span></span>
- <span data-ttu-id="feac8-245">指定 [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) 的 `Async` 參數。</span><span class="sxs-lookup"><span data-stu-id="feac8-245">Specify `Async` switch for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span></span> <span data-ttu-id="feac8-246">當叢集接受命令時會傳回此命令，而且會繼續以非同步方式進行應用程式類型的註冊。</span><span class="sxs-lookup"><span data-stu-id="feac8-246">The command returns when the cluster accepts the command and the registration of the application type continues asynchronously.</span></span> <span data-ttu-id="feac8-247">基於這個理由，在此情況下不需要指定較高的逾時。</span><span class="sxs-lookup"><span data-stu-id="feac8-247">For this reason, there is no need to specify a higher timeout in this case.</span></span> <span data-ttu-id="feac8-248">[Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) 命令會列出所有成功註冊的應用程式類型版本和其註冊狀態。</span><span class="sxs-lookup"><span data-stu-id="feac8-248">The [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="feac8-249">您可以使用此命令以判斷何時會完成註冊。</span><span class="sxs-lookup"><span data-stu-id="feac8-249">You can use this command to determine when the registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

### <a name="deploy-application-package-with-many-files"></a><span data-ttu-id="feac8-250">部署具有很多檔案的應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="feac8-250">Deploy application package with many files</span></span>
<span data-ttu-id="feac8-251">問題︰具有很多檔案的應用程式封裝 (以千計的順序) [Register-servicefabricapplicationtype](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) 的逾時。</span><span class="sxs-lookup"><span data-stu-id="feac8-251">Issue: [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) times out for an application package with many files (order of thousands).</span></span>
<span data-ttu-id="feac8-252">請嘗試︰</span><span class="sxs-lookup"><span data-stu-id="feac8-252">Try:</span></span>
- <span data-ttu-id="feac8-253">複製到映像存放區之前[壓縮封裝](service-fabric-package-apps.md#compress-a-package)。</span><span class="sxs-lookup"><span data-stu-id="feac8-253">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store.</span></span> <span data-ttu-id="feac8-254">壓縮會減少檔案的數目。</span><span class="sxs-lookup"><span data-stu-id="feac8-254">The compression reduces the number of files.</span></span>
- <span data-ttu-id="feac8-255">使用 `TimeoutSec` 參數指定 [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) 的較大逾時。</span><span class="sxs-lookup"><span data-stu-id="feac8-255">Specify a larger timeout for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) with `TimeoutSec` parameter.</span></span>
- <span data-ttu-id="feac8-256">指定 [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) 的 `Async` 參數。</span><span class="sxs-lookup"><span data-stu-id="feac8-256">Specify `Async` switch for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span></span> <span data-ttu-id="feac8-257">當叢集接受命令時會傳回此命令，而且會繼續以非同步方式進行應用程式類型的註冊。</span><span class="sxs-lookup"><span data-stu-id="feac8-257">The command returns when the cluster accepts the command and the registration of the application type continues asynchronously.</span></span>
<span data-ttu-id="feac8-258">基於這個理由，在此情況下不需要指定較高的逾時。</span><span class="sxs-lookup"><span data-stu-id="feac8-258">For this reason, there is no need to specify a higher timeout in this case.</span></span> <span data-ttu-id="feac8-259">[Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) 命令會列出所有成功註冊的應用程式類型版本和其註冊狀態。</span><span class="sxs-lookup"><span data-stu-id="feac8-259">The [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="feac8-260">您可以使用此命令以判斷何時會完成註冊。</span><span class="sxs-lookup"><span data-stu-id="feac8-260">You can use this command to determine when the registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="next-steps"></a><span data-ttu-id="feac8-261">後續步驟</span><span class="sxs-lookup"><span data-stu-id="feac8-261">Next steps</span></span>
[<span data-ttu-id="feac8-262">Service Fabric 應用程式升級</span><span class="sxs-lookup"><span data-stu-id="feac8-262">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="feac8-263">Service Fabric 健康狀態簡介</span><span class="sxs-lookup"><span data-stu-id="feac8-263">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)

[<span data-ttu-id="feac8-264">診斷和疑難排解 Service Fabric 服務</span><span class="sxs-lookup"><span data-stu-id="feac8-264">Diagnose and troubleshoot a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="feac8-265">在 Service Fabric 中模型化應用程式</span><span class="sxs-lookup"><span data-stu-id="feac8-265">Model an application in Service Fabric</span></span>](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before the slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
