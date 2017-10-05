---
title: "對 Azure Service Fabric 應用程式進行封裝 | Microsoft Docs"
description: "如何在將 Service Fabric 應用程式部署至叢集之前對它進行封裝。"
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
ms.openlocfilehash: 486a27d7ca576c8fe1552c02eb24ece6b8bb2ba8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="package-an-application"></a><span data-ttu-id="0b8db-103">封裝應用程式</span><span class="sxs-lookup"><span data-stu-id="0b8db-103">Package an application</span></span>
<span data-ttu-id="0b8db-104">本文說明如何對 Service Fabric 應用程式進行封裝，並使其準備好進行部署。</span><span class="sxs-lookup"><span data-stu-id="0b8db-104">This article describes how to package a Service Fabric application and make it ready for deployment.</span></span>

## <a name="package-layout"></a><span data-ttu-id="0b8db-105">封裝版面配置</span><span class="sxs-lookup"><span data-stu-id="0b8db-105">Package layout</span></span>
<span data-ttu-id="0b8db-106">應用程式資訊清單、一或多個服務資訊清單及其他必要的封裝檔案必須以特定的配置組織後，才能部署到 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="0b8db-106">The application manifest, one or more service manifests, and other necessary package files must be organized in a specific layout for deployment into a Service Fabric cluster.</span></span> <span data-ttu-id="0b8db-107">在本文中的範例資訊清單必須組織成下列目錄結構：</span><span class="sxs-lookup"><span data-stu-id="0b8db-107">The example manifests in this article would need to be organized in the following directory structure:</span></span>

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

<span data-ttu-id="0b8db-108">命名資料夾以符合每個對應元素的 **名稱** 屬性。</span><span class="sxs-lookup"><span data-stu-id="0b8db-108">The folders are named to match the **Name** attributes of each corresponding element.</span></span> <span data-ttu-id="0b8db-109">例如，如果服務資訊清單包含名稱為 **MyCodeA** 和 **MyCodeB** 的兩個程式碼封裝，則同名的兩個資料夾會包含每個程式碼封裝所需的二進位檔。</span><span class="sxs-lookup"><span data-stu-id="0b8db-109">For example, if the service manifest contained two code packages with the names **MyCodeA** and **MyCodeB**, then two folders with the same names would contain the necessary binaries for each code package.</span></span>

## <a name="use-setupentrypoint"></a><span data-ttu-id="0b8db-110">使用 SetupEntryPoint</span><span class="sxs-lookup"><span data-stu-id="0b8db-110">Use SetupEntryPoint</span></span>
<span data-ttu-id="0b8db-111">使用 **SetupEntryPoint** 的一般案例，是當您必須在服務啟動之前執行可執行檔，或必須使用提高的權限來執行作業時。</span><span class="sxs-lookup"><span data-stu-id="0b8db-111">Typical scenarios for using **SetupEntryPoint** are when you need to run an executable before the service starts or you need to perform an operation with elevated privileges.</span></span> <span data-ttu-id="0b8db-112">例如：</span><span class="sxs-lookup"><span data-stu-id="0b8db-112">For example:</span></span>

* <span data-ttu-id="0b8db-113">設定及初始化服務可執行檔需要的環境變數。</span><span class="sxs-lookup"><span data-stu-id="0b8db-113">Setting up and initializing environment variables that the service executable needs.</span></span> <span data-ttu-id="0b8db-114">這不僅限於透過 Service Fabric 程式設計模型撰寫的可執行檔。</span><span class="sxs-lookup"><span data-stu-id="0b8db-114">It is not limited to only executables written via the Service Fabric programming models.</span></span> <span data-ttu-id="0b8db-115">例如，npm.exe 部署 node.js 應用程式，需要設定某些環境變數。</span><span class="sxs-lookup"><span data-stu-id="0b8db-115">For example, npm.exe needs some environment variables configured for deploying a node.js application.</span></span>
* <span data-ttu-id="0b8db-116">透過安裝安全性憑證設定存取控制。</span><span class="sxs-lookup"><span data-stu-id="0b8db-116">Setting up access control by installing security certificates.</span></span>

<span data-ttu-id="0b8db-117">如需有關如何設定 **SetupEntryPoint** 的詳細資訊，請參閱[設定服務設定進入點的原則](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="0b8db-117">For more information on how to configure the **SetupEntryPoint**, see [Configure the policy for a service setup entry point](service-fabric-application-runas-security.md)</span></span>

<a id="Package-App"></a>
## <a name="configure"></a><span data-ttu-id="0b8db-118">設定</span><span class="sxs-lookup"><span data-stu-id="0b8db-118">Configure</span></span>
### <a name="build-a-package-by-using-visual-studio"></a><span data-ttu-id="0b8db-119">使用 Visual Studio 建置封裝</span><span class="sxs-lookup"><span data-stu-id="0b8db-119">Build a package by using Visual Studio</span></span>
<span data-ttu-id="0b8db-120">如果您使用 Visual Studio 2015 來建立您的應用程式，您可以使用 [封裝] 命令來自動建立符合上述版面配置的封裝。</span><span class="sxs-lookup"><span data-stu-id="0b8db-120">If you use Visual Studio 2015 to create your application, you can use the Package command to automatically create a package that matches the layout described above.</span></span>

<span data-ttu-id="0b8db-121">若要建立封裝，請以滑鼠右鍵按一下方案總管中的應用程式專案，然後選擇 [封裝] 命令，如下所示：</span><span class="sxs-lookup"><span data-stu-id="0b8db-121">To create a package, right-click the application project in Solution Explorer and choose the Package command, as shown below:</span></span>

![使用 Visual Studio 封裝應用程式][vs-package-command]

<span data-ttu-id="0b8db-123">封裝完成時，您會在 [輸出]  視窗中找到封裝的位置。</span><span class="sxs-lookup"><span data-stu-id="0b8db-123">When packaging is complete, you can find the location of the package in the **Output** window.</span></span> <span data-ttu-id="0b8db-124">當您在 Visual Studio 中部署或偵錯應用程式時，封裝步驟會自動執行。</span><span class="sxs-lookup"><span data-stu-id="0b8db-124">The packaging step occurs automatically when you deploy or debug your application in Visual Studio.</span></span>

### <a name="build-a-package-by-command-line"></a><span data-ttu-id="0b8db-125">透過命令列建置封裝</span><span class="sxs-lookup"><span data-stu-id="0b8db-125">Build a package by command line</span></span>
<span data-ttu-id="0b8db-126">使用 `msbuild.exe` 以程式設計方式封裝您的應用程式也是可行的。</span><span class="sxs-lookup"><span data-stu-id="0b8db-126">It is also possible to programmatically package up your application using `msbuild.exe`.</span></span> <span data-ttu-id="0b8db-127">深究其背後的原理，由於 Visual Studio 執行它，因此輸出也會相同。</span><span class="sxs-lookup"><span data-stu-id="0b8db-127">Under the hood, Visual Studio is running it so the output is same.</span></span>

```shell
D:\Temp> msbuild HelloWorld.sfproj /t:Package
```

## <a name="test-the-package"></a><span data-ttu-id="0b8db-128">測試封裝</span><span class="sxs-lookup"><span data-stu-id="0b8db-128">Test the package</span></span>
<span data-ttu-id="0b8db-129">您可以使用 [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) 命令，透過 PowerShell 在本機上驗證封裝結構。</span><span class="sxs-lookup"><span data-stu-id="0b8db-129">You can verify the package structure locally through PowerShell by using the [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) command.</span></span>
<span data-ttu-id="0b8db-130">此命令會檢查有無資訊清單剖析問題，並驗證所有參考。</span><span class="sxs-lookup"><span data-stu-id="0b8db-130">This command checks for manifest parsing issues and verify all references.</span></span> <span data-ttu-id="0b8db-131">這個命令只會驗證封裝中目錄與檔案的結構正確性。</span><span class="sxs-lookup"><span data-stu-id="0b8db-131">This command only verifies the structural correctness of the directories and files in the package.</span></span>
<span data-ttu-id="0b8db-132">除了檢查所有必要檔案是否都在之外，它不會驗證任何程式碼或資料封裝內容。</span><span class="sxs-lookup"><span data-stu-id="0b8db-132">It doesn't verify any of the code or data package contents beyond checking that all necessary files are present.</span></span>

```
PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
False
Test-ServiceFabricApplicationPackage : The EntryPoint MySetup.bat is not found.
FileName: C:\Users\servicefabric\AppData\Local\Temp\TestApplicationPackage_7195781181\nrri205a.e2h\MyApplicationType\MyServiceManifest\ServiceManifest.xml
```

<span data-ttu-id="0b8db-133">這個錯誤顯示程式碼封裝中遺漏服務資訊清單 *SetupEntryPoint* 中參考的 **MySetup.bat** 檔案。</span><span class="sxs-lookup"><span data-stu-id="0b8db-133">This error shows that the *MySetup.bat* file referenced in the service manifest **SetupEntryPoint** is missing from the code package.</span></span> <span data-ttu-id="0b8db-134">加入遺漏的檔案之後，應用程式驗證就會通過：</span><span class="sxs-lookup"><span data-stu-id="0b8db-134">After the missing file is added, the application verification passes:</span></span>

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

<span data-ttu-id="0b8db-135">如果您的應用程式已定義[應用程式參數](service-fabric-manage-multiple-environment-app-configuration.md)，您可以在 [Test-ServiceFabricApplicationPackage (英文)](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) 中傳遞它們以進行適當的驗證。</span><span class="sxs-lookup"><span data-stu-id="0b8db-135">If your application has [application parameters](service-fabric-manage-multiple-environment-app-configuration.md) defined, you can pass them in [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) for proper validation.</span></span>

<span data-ttu-id="0b8db-136">如果您知道將部署應用程式的叢集，建議您傳送 `ImageStoreConnectionString` 參數。</span><span class="sxs-lookup"><span data-stu-id="0b8db-136">If you know the cluster where the application will be deployed, it is recommended you pass in the `ImageStoreConnectionString` parameter.</span></span> <span data-ttu-id="0b8db-137">在此情況下，該封裝也會針對已在叢集中執行的舊版應用程式進行驗證。</span><span class="sxs-lookup"><span data-stu-id="0b8db-137">In this case, the package is also validated against previous versions of the application that are already running in the cluster.</span></span> <span data-ttu-id="0b8db-138">例如，驗證可以偵測具有相同版本但不同內容的封裝是否已經部署。</span><span class="sxs-lookup"><span data-stu-id="0b8db-138">For example, the validation can detect whether a package with the same version but different content was already deployed.</span></span>  

<span data-ttu-id="0b8db-139">一旦應用程式已完成封裝並通過驗證，請根據檔案的大小及數目，評估是否需要壓縮。</span><span class="sxs-lookup"><span data-stu-id="0b8db-139">Once the application is packaged correctly and passes validation, evaluate based on the size and the number of files if compression is needed.</span></span>

## <a name="compress-a-package"></a><span data-ttu-id="0b8db-140">壓縮封裝</span><span class="sxs-lookup"><span data-stu-id="0b8db-140">Compress a package</span></span>
<span data-ttu-id="0b8db-141">當封裝很大或有許多檔案時，您可以壓縮它以加快部署速度。</span><span class="sxs-lookup"><span data-stu-id="0b8db-141">When a package is large or has many files, you can compress it for faster deployment.</span></span> <span data-ttu-id="0b8db-142">壓縮會減少檔案數目並降低封裝大小。</span><span class="sxs-lookup"><span data-stu-id="0b8db-142">Compression reduces the number of files and the package size.</span></span>
<span data-ttu-id="0b8db-143">就已壓縮的應用程式套件而言，[上傳應用程式套件](service-fabric-deploy-remove-applications.md#upload-the-application-package)可能比上傳未壓縮的套件需要花費更多的時間 (特別是如果將壓縮時間也計算在內的話)，但在[註冊](service-fabric-deploy-remove-applications.md#register-the-application-package)和[取消應用程式類型註冊](service-fabric-deploy-remove-applications.md#unregister-an-application-type)方面，已壓縮的應用程式套件所花費的時間則較短。</span><span class="sxs-lookup"><span data-stu-id="0b8db-143">For a compressed application package, [Uploading the application package](service-fabric-deploy-remove-applications.md#upload-the-application-package) may take longer compared to uploading the uncompressed package (specially if compression time is factored in), but [registering](service-fabric-deploy-remove-applications.md#register-the-application-package) and [un-registering the application type](service-fabric-deploy-remove-applications.md#unregister-an-application-type) are faster for a compressed application package.</span></span>

<span data-ttu-id="0b8db-144">已壓縮和未壓縮套件的部署機制都相同。</span><span class="sxs-lookup"><span data-stu-id="0b8db-144">The deployment mechanism is same for compressed and uncompressed packages.</span></span> <span data-ttu-id="0b8db-145">如果封裝已壓縮，它會以壓縮的形式儲存在叢集映像存放區中，並在應用程式執行之前於節點上解壓縮。</span><span class="sxs-lookup"><span data-stu-id="0b8db-145">If the package is compressed, it is stored as such in the cluster image store and it's uncompressed on the node before the application is run.</span></span>
<span data-ttu-id="0b8db-146">壓縮會將有效的 Service Fabric 封裝以壓縮的版本取代。</span><span class="sxs-lookup"><span data-stu-id="0b8db-146">The compression replaces the valid Service Fabric package with the compressed version.</span></span> <span data-ttu-id="0b8db-147">該資料夾必須允許寫入權限。</span><span class="sxs-lookup"><span data-stu-id="0b8db-147">The folder must allow write permissions.</span></span> <span data-ttu-id="0b8db-148">在已經壓縮的封裝上執行壓縮將不會產生任何變化。</span><span class="sxs-lookup"><span data-stu-id="0b8db-148">Running compression on an already compressed package yields no changes.</span></span>

<span data-ttu-id="0b8db-149">您可以執行 PowerShell 命令 [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps)，並搭配 `CompressPackage` 參數來壓縮封裝。</span><span class="sxs-lookup"><span data-stu-id="0b8db-149">You can compress a package by running the Powershell command [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) with `CompressPackage` switch.</span></span> <span data-ttu-id="0b8db-150">您可以使用相同的命令，並搭配 `UncompressPackage` 參數來將封裝解壓縮。</span><span class="sxs-lookup"><span data-stu-id="0b8db-150">You can uncompress the package with the same command, using `UncompressPackage` switch.</span></span>

<span data-ttu-id="0b8db-151">下列命令會在不將封裝複製到映像存放區的情況下壓縮封裝。</span><span class="sxs-lookup"><span data-stu-id="0b8db-151">The following command compresses the package without copying it to the image store.</span></span> <span data-ttu-id="0b8db-152">您可以在不搭配 `SkipCopy` 旗標的情況下使用 [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps)，視需求將壓縮的封裝複製到一或多個 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="0b8db-152">You can copy a compressed package to one or more Service Fabric clusters, as needed, using [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) without the `SkipCopy` flag.</span></span>
<span data-ttu-id="0b8db-153">該套件現在包含 `code`、`config` 及 `data` 套件的 ZIP 壓縮檔案。</span><span class="sxs-lookup"><span data-stu-id="0b8db-153">The package now includes zipped files for the `code`, `config`, and `data` packages.</span></span> <span data-ttu-id="0b8db-154">應用程式資訊清單和服務資訊清單不會壓縮，因為有許多內部作業都需要它們 (例如特定驗證的封裝共用、應用程式類型名稱及版本擷取)。</span><span class="sxs-lookup"><span data-stu-id="0b8db-154">The application manifest and the service manifests are not zipped, because they are needed for many internal operations (like package sharing, application type name and version extraction for certain validations).</span></span>
<span data-ttu-id="0b8db-155">對資訊清單進行壓縮，將會使這些作業效率不佳。</span><span class="sxs-lookup"><span data-stu-id="0b8db-155">Zipping the manifests would make these operations inefficient.</span></span>

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

<span data-ttu-id="0b8db-156">除此之外，您可以使用 [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps)，同時壓縮並複製封裝。</span><span class="sxs-lookup"><span data-stu-id="0b8db-156">Alternatively, you can compress and copy the package with [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) in one step.</span></span>
<span data-ttu-id="0b8db-157">如果封裝很大，請提供足夠的逾時，使封裝可以完成壓縮並上傳至叢集。</span><span class="sxs-lookup"><span data-stu-id="0b8db-157">If the package is large, provide a high enough timeout to allow time for both the package compression and the upload to the cluster.</span></span>
```
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -ApplicationPackagePathInImageStore MyApplicationType -ImageStoreConnectionString fabric:ImageStore -CompressPackage -TimeoutSec 5400
```

<span data-ttu-id="0b8db-158">Service Fabric 會在內部針對驗證計算應用程式封裝的總和檢查碼。</span><span class="sxs-lookup"><span data-stu-id="0b8db-158">Internally, Service Fabric computes checksums for the application packages for validation.</span></span> <span data-ttu-id="0b8db-159">使用壓縮時，會針對每個封裝的壓縮版本計算總和檢查碼。</span><span class="sxs-lookup"><span data-stu-id="0b8db-159">When using compression, the checksums are computed on the zipped versions of each package.</span></span>
<span data-ttu-id="0b8db-160">若您已複製應用程式套件的未壓縮版本，而想要將壓縮用於同一個套件，您就必須變更 `code`、`config` 和 `data` 套件的版本，以避免總和檢查碼不符。</span><span class="sxs-lookup"><span data-stu-id="0b8db-160">If you copied an uncompressed version of your application package, and you want to use compression for the same package, you must change the versions of the `code`, `config`, and `data` packages to avoid checksum mismatch.</span></span> <span data-ttu-id="0b8db-161">若封裝未變更，則您可不變更版本而使用 [差異佈建](service-fabric-application-upgrade-advanced.md)。</span><span class="sxs-lookup"><span data-stu-id="0b8db-161">If the packages are unchanged, instead of changing the version, you can use [diff provisioning](service-fabric-application-upgrade-advanced.md).</span></span> <span data-ttu-id="0b8db-162">使用此選項時，請勿包含未變更的套件，而是要從服務資訊清單參考它。</span><span class="sxs-lookup"><span data-stu-id="0b8db-162">With this option, do not include the unchanged package instead reference it from the service manifest.</span></span>

<span data-ttu-id="0b8db-163">同樣地，若您已上傳封裝的壓縮版本，且想要使用未壓縮的封裝，則您必須更新版本以避免總和檢查碼不符。</span><span class="sxs-lookup"><span data-stu-id="0b8db-163">Similarly, if you uploaded a compressed version of the package and you want to use an uncompressed package, you must update the versions to avoid the checksum mismatch.</span></span>

<span data-ttu-id="0b8db-164">封裝現已正確完成封裝、驗證及壓縮 (若有需要)，因此已準備好[部署](service-fabric-deploy-remove-applications.md)至一或多個 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="0b8db-164">The package is now packaged correctly, validated, and compressed (if needed), so it is ready for [deployment](service-fabric-deploy-remove-applications.md) to one or more Service Fabric clusters.</span></span>

### <a name="compress-packages-when-deploying-using-visual-studio"></a><span data-ttu-id="0b8db-165">使用 Visual Studio 進行部署時壓縮套件</span><span class="sxs-lookup"><span data-stu-id="0b8db-165">Compress packages when deploying using Visual Studio</span></span>
<span data-ttu-id="0b8db-166">您可以將 `CopyPackageParameters` 元素新增到發行設定檔，並將 `CompressPackage` 屬性設定為 `true`，來指示 Visual Studio 在部署時壓縮套件。</span><span class="sxs-lookup"><span data-stu-id="0b8db-166">You can instruct Visual Studio to compress packages on deployment, by adding the `CopyPackageParameters` element to your publish profile, and set the `CompressPackage` attribute to `true`.</span></span>

``` xml
    <PublishProfile xmlns="http://schemas.microsoft.com/2015/05/fabrictools">
        <ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com" />
        <ApplicationParameterFile Path="..\ApplicationParameters\Cloud.xml" />
        <CopyPackageParameters CompressPackage="true"/>
    </PublishProfile>
```

## <a name="next-steps"></a><span data-ttu-id="0b8db-167">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0b8db-167">Next steps</span></span>
<span data-ttu-id="0b8db-168">[部署與移除應用程式][10]說明如何使用 PowerShell 來管理應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="0b8db-168">[Deploy and remove applications][10] describes how to use PowerShell to manage application instances</span></span>

<span data-ttu-id="0b8db-169">[管理多個環境的應用程式參數][11]說明如何為不同的應用程式執行個體設定參數和環境變數。</span><span class="sxs-lookup"><span data-stu-id="0b8db-169">[Managing application parameters for multiple environments][11] describes how to configure parameters and environment variables for different application instances.</span></span>

<span data-ttu-id="0b8db-170">[設定應用程式的安全性原則][12]說明如何依據安全性原則執行服務來限制存取。</span><span class="sxs-lookup"><span data-stu-id="0b8db-170">[Configure security policies for your application][12] describes how to run services under security policies to restrict access.</span></span>

<!--Image references-->
[vs-package-command]: ./media/service-fabric-package-apps/vs-package-command.png

<!--Link references--In actual articles, you only need a single period before the slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
