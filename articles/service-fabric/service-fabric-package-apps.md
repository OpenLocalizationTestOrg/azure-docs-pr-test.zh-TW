---
title: "aaaPackage Azure Service Fabric 應用程式 |Microsoft 文件"
description: "如何 toopackage Service Fabric 應用程式，才能部署 tooa 叢集。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: mani-ramaswamy
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: ryanwi
ms.openlocfilehash: b3918e1e25e532acdc9440855213e1fa364ea000
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="package-an-application"></a><span data-ttu-id="45f87-103">封裝應用程式</span><span class="sxs-lookup"><span data-stu-id="45f87-103">Package an application</span></span>
<span data-ttu-id="45f87-104">本文說明如何 toopackage Service Fabric 應用程式並讓它準備好進行部署。</span><span class="sxs-lookup"><span data-stu-id="45f87-104">This article describes how toopackage a Service Fabric application and make it ready for deployment.</span></span>

## <a name="package-layout"></a><span data-ttu-id="45f87-105">封裝版面配置</span><span class="sxs-lookup"><span data-stu-id="45f87-105">Package layout</span></span>
<span data-ttu-id="45f87-106">hello 應用程式資訊清單、 一個或多個服務資訊清單和其他檔案必須依照特定的版面配置，以部署至 Service Fabric 叢集所需的套件。</span><span class="sxs-lookup"><span data-stu-id="45f87-106">hello application manifest, one or more service manifests, and other necessary package files must be organized in a specific layout for deployment into a Service Fabric cluster.</span></span> <span data-ttu-id="45f87-107">本文章中的 hello 範例資訊清單需要 toobe 組織 hello 下列目錄結構中：</span><span class="sxs-lookup"><span data-stu-id="45f87-107">hello example manifests in this article would need toobe organized in hello following directory structure:</span></span>

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat
```

<span data-ttu-id="45f87-108">hello 資料夾名為 toomatch hello**名稱**屬性的每個對應的項目。</span><span class="sxs-lookup"><span data-stu-id="45f87-108">hello folders are named toomatch hello **Name** attributes of each corresponding element.</span></span> <span data-ttu-id="45f87-109">例如，如果 hello 服務資訊清單包含與 hello 名稱的兩個程式碼封裝**MyCodeA**和**MyCodeB**，則兩個資料夾都包含相同名稱的 hello 與 hello 每個程式碼所需的二進位檔封裝。</span><span class="sxs-lookup"><span data-stu-id="45f87-109">For example, if hello service manifest contained two code packages with hello names **MyCodeA** and **MyCodeB**, then two folders with hello same names would contain hello necessary binaries for each code package.</span></span>

## <a name="use-setupentrypoint"></a><span data-ttu-id="45f87-110">使用 SetupEntryPoint</span><span class="sxs-lookup"><span data-stu-id="45f87-110">Use SetupEntryPoint</span></span>
<span data-ttu-id="45f87-111">使用的典型案例**SetupEntryPoint**是當您需要 toorun hello 服務啟動之前可執行檔或需要 tooperform 使用更高權限的作業。</span><span class="sxs-lookup"><span data-stu-id="45f87-111">Typical scenarios for using **SetupEntryPoint** are when you need toorun an executable before hello service starts or you need tooperform an operation with elevated privileges.</span></span> <span data-ttu-id="45f87-112">例如：</span><span class="sxs-lookup"><span data-stu-id="45f87-112">For example:</span></span>

* <span data-ttu-id="45f87-113">設定及初始化 hello 服務可執行檔需要的環境變數。</span><span class="sxs-lookup"><span data-stu-id="45f87-113">Setting up and initializing environment variables that hello service executable needs.</span></span> <span data-ttu-id="45f87-114">不限制的 tooonly hello Service Fabric 程式設計模型透過撰寫的可執行檔。</span><span class="sxs-lookup"><span data-stu-id="45f87-114">It is not limited tooonly executables written via hello Service Fabric programming models.</span></span> <span data-ttu-id="45f87-115">例如，npm.exe 部署 node.js 應用程式，需要設定某些環境變數。</span><span class="sxs-lookup"><span data-stu-id="45f87-115">For example, npm.exe needs some environment variables configured for deploying a node.js application.</span></span>
* <span data-ttu-id="45f87-116">透過安裝安全性憑證設定存取控制。</span><span class="sxs-lookup"><span data-stu-id="45f87-116">Setting up access control by installing security certificates.</span></span>

<span data-ttu-id="45f87-117">如需有關如何 tooconfigure hello **SetupEntryPoint**，請參閱[設定服務安裝程式的進入點的 hello 原則](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="45f87-117">For more information on how tooconfigure hello **SetupEntryPoint**, see [Configure hello policy for a service setup entry point](service-fabric-application-runas-security.md)</span></span>

<a id="Package-App"></a>
## <a name="configure"></a><span data-ttu-id="45f87-118">設定</span><span class="sxs-lookup"><span data-stu-id="45f87-118">Configure</span></span>
### <a name="build-a-package-by-using-visual-studio"></a><span data-ttu-id="45f87-119">使用 Visual Studio 建置封裝</span><span class="sxs-lookup"><span data-stu-id="45f87-119">Build a package by using Visual Studio</span></span>
<span data-ttu-id="45f87-120">如果您使用 Visual Studio 2015 toocreate 您的應用程式，您可以使用 hello 命令 tooautomatically 建立符合上面所述的 hello 版面配置的封裝的封裝。</span><span class="sxs-lookup"><span data-stu-id="45f87-120">If you use Visual Studio 2015 toocreate your application, you can use hello Package command tooautomatically create a package that matches hello layout described above.</span></span>

<span data-ttu-id="45f87-121">toocreate 封裝時，以滑鼠右鍵按一下方案總管 中的 hello 應用程式專案，並選擇 hello 套件 命令，如下所示：</span><span class="sxs-lookup"><span data-stu-id="45f87-121">toocreate a package, right-click hello application project in Solution Explorer and choose hello Package command, as shown below:</span></span>

![使用 Visual Studio 封裝應用程式][vs-package-command]

<span data-ttu-id="45f87-123">封裝完成後，您可以在 hello 找到 hello 封裝的 hello 位置**輸出**視窗。</span><span class="sxs-lookup"><span data-stu-id="45f87-123">When packaging is complete, you can find hello location of hello package in hello **Output** window.</span></span> <span data-ttu-id="45f87-124">當您部署或偵錯 Visual Studio 中的應用程式時，會自動發生 hello 封裝步驟。</span><span class="sxs-lookup"><span data-stu-id="45f87-124">hello packaging step occurs automatically when you deploy or debug your application in Visual Studio.</span></span>

### <a name="build-a-package-by-command-line"></a><span data-ttu-id="45f87-125">透過命令列建置封裝</span><span class="sxs-lookup"><span data-stu-id="45f87-125">Build a package by command line</span></span>
<span data-ttu-id="45f87-126">它也是您的應用程式使用的可能 tooprogrammatically 封裝`msbuild.exe`。</span><span class="sxs-lookup"><span data-stu-id="45f87-126">It is also possible tooprogrammatically package up your application using `msbuild.exe`.</span></span> <span data-ttu-id="45f87-127">Hello 原理，Visual Studio 執行它因此 hello 輸出會相同。</span><span class="sxs-lookup"><span data-stu-id="45f87-127">Under hello hood, Visual Studio is running it so hello output is same.</span></span>

```shell
D:\Temp> msbuild HelloWorld.sfproj /t:Package
```

## <a name="test-hello-package"></a><span data-ttu-id="45f87-128">測試 hello 封裝</span><span class="sxs-lookup"><span data-stu-id="45f87-128">Test hello package</span></span>
<span data-ttu-id="45f87-129">您可以確認 hello 封裝結構，透過 PowerShell 在本機使用 hello[測試 ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps)命令。</span><span class="sxs-lookup"><span data-stu-id="45f87-129">You can verify hello package structure locally through PowerShell by using hello [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) command.</span></span>
<span data-ttu-id="45f87-130">此命令會檢查有無資訊清單剖析問題，並驗證所有參考。</span><span class="sxs-lookup"><span data-stu-id="45f87-130">This command checks for manifest parsing issues and verify all references.</span></span> <span data-ttu-id="45f87-131">此命令只會驗證 hello hello 封裝中的 hello 目錄和檔案結構的正確性。</span><span class="sxs-lookup"><span data-stu-id="45f87-131">This command only verifies hello structural correctness of hello directories and files in hello package.</span></span>
<span data-ttu-id="45f87-132">它不會驗證任何 hello 程式碼或資料封裝的內容超過檢查所有必要的檔案都存在。</span><span class="sxs-lookup"><span data-stu-id="45f87-132">It doesn't verify any of hello code or data package contents beyond checking that all necessary files are present.</span></span>

```
PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
False
Test-ServiceFabricApplicationPackage : hello EntryPoint MySetup.bat is not found.
FileName: C:\Users\servicefabric\AppData\Local\Temp\TestApplicationPackage_7195781181\nrri205a.e2h\MyApplicationType\MyServiceManifest\ServiceManifest.xml
```

<span data-ttu-id="45f87-133">這項錯誤顯示該 hello *MySetup.bat* hello 服務資訊清單中所參考的檔案**SetupEntryPoint** hello 程式碼封裝中遺漏。</span><span class="sxs-lookup"><span data-stu-id="45f87-133">This error shows that hello *MySetup.bat* file referenced in hello service manifest **SetupEntryPoint** is missing from hello code package.</span></span> <span data-ttu-id="45f87-134">加入 hello 遺失檔案之後，會將 $ hello 應用程式驗證：</span><span class="sxs-lookup"><span data-stu-id="45f87-134">After hello missing file is added, hello application verification passes:</span></span>

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │       MySetup.bat
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat

PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
True
PS D:\temp>
```

<span data-ttu-id="45f87-135">如果您的應用程式已定義[應用程式參數](service-fabric-manage-multiple-environment-app-configuration.md)，您可以在 [Test-ServiceFabricApplicationPackage (英文)](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) 中傳遞它們以進行適當的驗證。</span><span class="sxs-lookup"><span data-stu-id="45f87-135">If your application has [application parameters](service-fabric-manage-multiple-environment-app-configuration.md) defined, you can pass them in [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) for proper validation.</span></span>

<span data-ttu-id="45f87-136">如果您知道 hello 應用程式將會部署的 hello 叢集，則建議您傳入 hello`ImageStoreConnectionString`參數。</span><span class="sxs-lookup"><span data-stu-id="45f87-136">If you know hello cluster where hello application will be deployed, it is recommended you pass in hello `ImageStoreConnectionString` parameter.</span></span> <span data-ttu-id="45f87-137">在此情況下，hello 封裝也會針對舊版 hello 應用程式已在 hello 叢集中執行驗證。</span><span class="sxs-lookup"><span data-stu-id="45f87-137">In this case, hello package is also validated against previous versions of hello application that are already running in hello cluster.</span></span> <span data-ttu-id="45f87-138">例如，封裝是否可以偵測到 hello 驗證 hello 與相同的版本，但內容不同已部署。</span><span class="sxs-lookup"><span data-stu-id="45f87-138">For example, hello validation can detect whether a package with hello same version but different content was already deployed.</span></span>  

<span data-ttu-id="45f87-139">評估 hello 應用程式正確的封裝，並通過驗證，視壓縮，根據 hello 大小與 hello 檔案數目。</span><span class="sxs-lookup"><span data-stu-id="45f87-139">Once hello application is packaged correctly and passes validation, evaluate based on hello size and hello number of files if compression is needed.</span></span>

## <a name="compress-a-package"></a><span data-ttu-id="45f87-140">壓縮封裝</span><span class="sxs-lookup"><span data-stu-id="45f87-140">Compress a package</span></span>
<span data-ttu-id="45f87-141">當封裝很大或有許多檔案時，您可以壓縮它以加快部署速度。</span><span class="sxs-lookup"><span data-stu-id="45f87-141">When a package is large or has many files, you can compress it for faster deployment.</span></span> <span data-ttu-id="45f87-142">壓縮會減少 hello 的檔案數目與 hello 封裝大小。</span><span class="sxs-lookup"><span data-stu-id="45f87-142">Compression reduces hello number of files and hello package size.</span></span>
<span data-ttu-id="45f87-143">壓縮的應用程式封裝，[上傳 hello 應用程式封裝](service-fabric-deploy-remove-applications.md#upload-the-application-package)可能需要再比較的 toouploading hello 未壓縮的封裝 （特別如果壓縮時間分解出來），但[註冊](service-fabric-deploy-remove-applications.md#register-the-application-package)和[取消註冊 hello 應用程式類型](service-fabric-deploy-remove-applications.md#unregister-an-application-type)更快，壓縮的應用程式封裝。</span><span class="sxs-lookup"><span data-stu-id="45f87-143">For a compressed application package, [Uploading hello application package](service-fabric-deploy-remove-applications.md#upload-the-application-package) may take longer compared toouploading hello uncompressed package (specially if compression time is factored in), but [registering](service-fabric-deploy-remove-applications.md#register-the-application-package) and [un-registering hello application type](service-fabric-deploy-remove-applications.md#unregister-an-application-type) are faster for a compressed application package.</span></span>

<span data-ttu-id="45f87-144">hello 部署機制是相同的壓縮和未壓縮的封裝。</span><span class="sxs-lookup"><span data-stu-id="45f87-144">hello deployment mechanism is same for compressed and uncompressed packages.</span></span> <span data-ttu-id="45f87-145">如果 hello 封裝已壓縮，因此儲存 hello 叢集映像存放區中，而且執行 hello 應用程式之前，hello 節點上進行壓縮。</span><span class="sxs-lookup"><span data-stu-id="45f87-145">If hello package is compressed, it is stored as such in hello cluster image store and it's uncompressed on hello node before hello application is run.</span></span>
<span data-ttu-id="45f87-146">hello 壓縮取代 hello 壓縮版的 hello 有效 Service Fabric 封裝。</span><span class="sxs-lookup"><span data-stu-id="45f87-146">hello compression replaces hello valid Service Fabric package with hello compressed version.</span></span> <span data-ttu-id="45f87-147">hello 資料夾必須允許寫入權限。</span><span class="sxs-lookup"><span data-stu-id="45f87-147">hello folder must allow write permissions.</span></span> <span data-ttu-id="45f87-148">在已經壓縮的封裝上執行壓縮將不會產生任何變化。</span><span class="sxs-lookup"><span data-stu-id="45f87-148">Running compression on an already compressed package yields no changes.</span></span>

<span data-ttu-id="45f87-149">您可以藉由執行 hello Powershell 命令來壓縮封裝[複製 ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps)與`CompressPackage`切換。</span><span class="sxs-lookup"><span data-stu-id="45f87-149">You can compress a package by running hello Powershell command [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) with `CompressPackage` switch.</span></span> <span data-ttu-id="45f87-150">您可以解壓縮 hello 相同封裝以 hello 命令，使用`UncompressPackage`切換。</span><span class="sxs-lookup"><span data-stu-id="45f87-150">You can uncompress hello package with hello same command, using `UncompressPackage` switch.</span></span>

<span data-ttu-id="45f87-151">hello 下列命令壓縮 hello 封裝但不複製該項 toohello 映像存放區。</span><span class="sxs-lookup"><span data-stu-id="45f87-151">hello following command compresses hello package without copying it toohello image store.</span></span> <span data-ttu-id="45f87-152">您可以壓縮的封裝 tooone 或複製多個 Service Fabric 叢集，視需要使用[複製 ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps)沒有 hello`SkipCopy`旗標。</span><span class="sxs-lookup"><span data-stu-id="45f87-152">You can copy a compressed package tooone or more Service Fabric clusters, as needed, using [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) without hello `SkipCopy` flag.</span></span>
<span data-ttu-id="45f87-153">hello 封裝現在包含 hello 的 zip 的檔案`code`， `config`，和`data`封裝。</span><span class="sxs-lookup"><span data-stu-id="45f87-153">hello package now includes zipped files for hello `code`, `config`, and `data` packages.</span></span> <span data-ttu-id="45f87-154">不壓縮 hello 應用程式資訊清單和 hello 服務資訊清單，因為它們所需的許多內部的作業 （例如共用、 應用程式類型名稱和版本擷取針對特定的驗證封裝）。</span><span class="sxs-lookup"><span data-stu-id="45f87-154">hello application manifest and hello service manifests are not zipped, because they are needed for many internal operations (like package sharing, application type name and version extraction for certain validations).</span></span>
<span data-ttu-id="45f87-155">壓縮 hello 資訊清單會使這些操作效率不佳。</span><span class="sxs-lookup"><span data-stu-id="45f87-155">Zipping hello manifests would make these operations inefficient.</span></span>

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │       MySetup.bat
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -CompressPackage -SkipCopy

PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
       ServiceManifest.xml
       MyCode.zip
       MyConfig.zip
       MyData.zip

```

<span data-ttu-id="45f87-156">或者，您可以壓縮並複製 hello 封裝[複製 ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps)以一個步驟。</span><span class="sxs-lookup"><span data-stu-id="45f87-156">Alternatively, you can compress and copy hello package with [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) in one step.</span></span>
<span data-ttu-id="45f87-157">如果 hello 套件很大，提供 hello 封裝壓縮和 hello 上載 toohello 叢集夠高的逾時 tooallow 時間。</span><span class="sxs-lookup"><span data-stu-id="45f87-157">If hello package is large, provide a high enough timeout tooallow time for both hello package compression and hello upload toohello cluster.</span></span>
```
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -ApplicationPackagePathInImageStore MyApplicationType -ImageStoreConnectionString fabric:ImageStore -CompressPackage -TimeoutSec 5400
```

<span data-ttu-id="45f87-158">就內部而言，Service Fabric 計算總和檢查碼驗證的 hello 應用程式封裝。</span><span class="sxs-lookup"><span data-stu-id="45f87-158">Internally, Service Fabric computes checksums for hello application packages for validation.</span></span> <span data-ttu-id="45f87-159">當使用壓縮，hello 總和檢查碼計算 hello 壓縮每個封裝的版本上。</span><span class="sxs-lookup"><span data-stu-id="45f87-159">When using compression, hello checksums are computed on hello zipped versions of each package.</span></span>
<span data-ttu-id="45f87-160">如果您複製到未壓縮的版本，您的應用程式封裝，而且您想 hello toouse 壓縮相同的封裝，您必須變更 hello hello 版本`code`， `config`，和`data`封裝 tooavoid 總和檢查碼不符。</span><span class="sxs-lookup"><span data-stu-id="45f87-160">If you copied an uncompressed version of your application package, and you want toouse compression for hello same package, you must change hello versions of hello `code`, `config`, and `data` packages tooavoid checksum mismatch.</span></span> <span data-ttu-id="45f87-161">如果 hello 封裝不會變更，而不是變更 hello 版本，您可以使用[差異佈建](service-fabric-application-upgrade-advanced.md)。</span><span class="sxs-lookup"><span data-stu-id="45f87-161">If hello packages are unchanged, instead of changing hello version, you can use [diff provisioning](service-fabric-application-upgrade-advanced.md).</span></span> <span data-ttu-id="45f87-162">使用此選項時，不包括 hello 不變的封裝而從 hello 服務資訊清單參考它。</span><span class="sxs-lookup"><span data-stu-id="45f87-162">With this option, do not include hello unchanged package instead reference it from hello service manifest.</span></span>

<span data-ttu-id="45f87-163">同樣地，如果您上傳 hello 封裝的壓縮的版本，而且您想 toouse 未壓縮的封裝，您必須更新 hello 版本 tooavoid hello 總和檢查碼不符。</span><span class="sxs-lookup"><span data-stu-id="45f87-163">Similarly, if you uploaded a compressed version of hello package and you want toouse an uncompressed package, you must update hello versions tooavoid hello checksum mismatch.</span></span>

<span data-ttu-id="45f87-164">hello 封裝是現在正確封裝、 驗證，且壓縮的 （如有需要），讓它可供[部署](service-fabric-deploy-remove-applications.md)tooone 或多個 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="45f87-164">hello package is now packaged correctly, validated, and compressed (if needed), so it is ready for [deployment](service-fabric-deploy-remove-applications.md) tooone or more Service Fabric clusters.</span></span>

### <a name="compress-packages-when-deploying-using-visual-studio"></a><span data-ttu-id="45f87-165">使用 Visual Studio 進行部署時壓縮套件</span><span class="sxs-lookup"><span data-stu-id="45f87-165">Compress packages when deploying using Visual Studio</span></span>
<span data-ttu-id="45f87-166">您可以指示 Visual Studio toocompress 套件部署中，藉由新增 hello`CopyPackageParameters`元素 tooyour 發行設定檔，並設定 hello`CompressPackage`屬性太`true`。</span><span class="sxs-lookup"><span data-stu-id="45f87-166">You can instruct Visual Studio toocompress packages on deployment, by adding hello `CopyPackageParameters` element tooyour publish profile, and set hello `CompressPackage` attribute too`true`.</span></span>

``` xml
    <PublishProfile xmlns="http://schemas.microsoft.com/2015/05/fabrictools">
        <ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com" />
        <ApplicationParameterFile Path="..\ApplicationParameters\Cloud.xml" />
        <CopyPackageParameters CompressPackage="true"/>
    </PublishProfile>
```

## <a name="next-steps"></a><span data-ttu-id="45f87-167">後續步驟</span><span class="sxs-lookup"><span data-stu-id="45f87-167">Next steps</span></span>
<span data-ttu-id="45f87-168">[部署和移除應用程式][ 10]描述如何 toouse PowerShell toomanage 應用程式執行個體</span><span class="sxs-lookup"><span data-stu-id="45f87-168">[Deploy and remove applications][10] describes how toouse PowerShell toomanage application instances</span></span>

<span data-ttu-id="45f87-169">[管理應用程式參數的多個環境][ 11]描述如何 tooconfigure 參數和環境變數不同的應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="45f87-169">[Managing application parameters for multiple environments][11] describes how tooconfigure parameters and environment variables for different application instances.</span></span>

<span data-ttu-id="45f87-170">[設定您的應用程式的安全性原則][ 12]描述 toorun 下安全性原則 toorestrict 存取服務的方式。</span><span class="sxs-lookup"><span data-stu-id="45f87-170">[Configure security policies for your application][12] describes how toorun services under security policies toorestrict access.</span></span>

<!--Image references-->
[vs-package-command]: ./media/service-fabric-package-apps/vs-package-command.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
