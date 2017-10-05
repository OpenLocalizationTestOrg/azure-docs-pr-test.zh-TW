---
title: "自動化 Azure Service Fabric 應用程式管理 | Microsoft Docs"
description: "藉由使用 PowerShell 來部署、升級、測試和移除 Service Fabric 應用程式。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: f03f4294-571d-4262-8a77-cc8b481b959d
ms.service: service-fabric
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/16/2017
ms.author: ryanwi
redirect_url: /azure/service-fabric/service-fabric-deploy-remove-applications
ms.openlocfilehash: fb3c2a77ea887289eebf343e223c190781d0e4c2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="automate-the-application-lifecycle-using-powershell"></a><span data-ttu-id="ba3bb-103">使用 PowerShell 自動化應用程式生命週期</span><span class="sxs-lookup"><span data-stu-id="ba3bb-103">Automate the application lifecycle using PowerShell</span></span>
<span data-ttu-id="ba3bb-104">[Service Fabric 應用程式生命週期](service-fabric-application-lifecycle.md) 的許多層面都可以自動化。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-104">Many aspects of the [Service Fabric application lifecycle](service-fabric-application-lifecycle.md) can be automated.</span></span>  <span data-ttu-id="ba3bb-105">本文示範如何使用 Powershell，自動化部署、升級、移除和測試 Azure Service Fabric 應用程式的常見工作。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-105">This article shows how to use PowerShell to automate common tasks for deploying, upgrading, removing, and testing Azure Service Fabric applications.</span></span>  <span data-ttu-id="ba3bb-106">也可使用應用程式管理的 Managed 和 HTTP API。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-106">Managed and HTTP APIs for app management are also available.</span></span> <span data-ttu-id="ba3bb-107">如需詳細資訊，請參閱 [應用程式生命週期](service-fabric-application-lifecycle.md) 。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-107">See [app lifecycle](service-fabric-application-lifecycle.md) for more information.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="ba3bb-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="ba3bb-108">Prerequisites</span></span>
<span data-ttu-id="ba3bb-109">在您移至本文中的工作之前，請務必︰</span><span class="sxs-lookup"><span data-stu-id="ba3bb-109">Before you move on to the tasks in the article, be sure to:</span></span>

* <span data-ttu-id="ba3bb-110">熟悉 [Service Fabric 技術概觀](service-fabric-technical-overview.md)中所述的 Service Fabric 概念。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-110">Get familiar with the Service Fabric concepts described in [Technical overview of Service Fabric](service-fabric-technical-overview.md).</span></span>
* <span data-ttu-id="ba3bb-111">[安裝執行階段、SDK 和工具](service-fabric-get-started.md)，這也會安裝 **ServiceFabric** PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-111">[Install the runtime, SDK, and tools](service-fabric-get-started.md), which also installs the **ServiceFabric** PowerShell module.</span></span>
* <span data-ttu-id="ba3bb-112">[啟用 PowerShell 指令碼執行](service-fabric-get-started.md#enable-powershell-script-execution)。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-112">[Enable PowerShell script execution](service-fabric-get-started.md#enable-powershell-script-execution).</span></span>
* <span data-ttu-id="ba3bb-113">啟動本機叢集。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-113">Start a local cluster.</span></span>  <span data-ttu-id="ba3bb-114">以系統管理員身分啟動新的 PowerShell 視窗，然後從 SDK 資料夾執行叢集安裝指令碼 ︰ `& "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"`</span><span class="sxs-lookup"><span data-stu-id="ba3bb-114">Launch a new PowerShell window as an administrator and then run the cluster setup script from the SDK folder: `& "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"`</span></span>
* <span data-ttu-id="ba3bb-115">在您執行本文中的任何 PowerShell 命令之前，請先使用 [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) 連線至本機 Service Fabric 叢集：`Connect-ServiceFabricCluster localhost:19000`</span><span class="sxs-lookup"><span data-stu-id="ba3bb-115">Before you run any PowerShell commands in this article, first connect to the local Service Fabric cluster by using [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps): `Connect-ServiceFabricCluster localhost:19000`</span></span>
* <span data-ttu-id="ba3bb-116">下列工作需要 v1 應用程式封裝才能部署，並需要 v2 應用程式封裝才能進行升級。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-116">The following tasks require a v1 application package to deploy and a v2 application package for upgrade.</span></span> <span data-ttu-id="ba3bb-117">下載 [**WordCount** 範例應用程式](http://aka.ms/servicefabricsamples) (位於快速入門範例)。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-117">Download the [**WordCount** sample application](http://aka.ms/servicefabricsamples) (located in the Getting Started samples).</span></span> <span data-ttu-id="ba3bb-118">在 Visual Studio 中建置並封裝此應用程式 (以滑鼠右鍵按一下方案總管中的 [WordCount]，然後選取 [封裝])。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-118">Build and package the application in Visual Studio (right-click on **WordCount** in Solution Explorer and select **Package**).</span></span> <span data-ttu-id="ba3bb-119">將 `C:\ServiceFabricSamples\Services\WordCount\WordCount\pkg\Debug` 中的 v1 封裝複製到 `C:\Temp\WordCount`。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-119">Copy the v1 package in `C:\ServiceFabricSamples\Services\WordCount\WordCount\pkg\Debug` to `C:\Temp\WordCount`.</span></span> <span data-ttu-id="ba3bb-120">將 `C:\Temp\WordCount` 複製到 `C:\Temp\WordCountV2`，並建立 v2 應用程式封裝以便升級。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-120">Copy `C:\Temp\WordCount` to `C:\Temp\WordCountV2`, creating the v2 application package for upgrade.</span></span> <span data-ttu-id="ba3bb-121">在文字編輯器中開啟 `C:\Temp\WordCountV2\ApplicationManifest.xml`。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-121">Open `C:\Temp\WordCountV2\ApplicationManifest.xml` in a text editor.</span></span> <span data-ttu-id="ba3bb-122">在 **ApplicationManifest** 元素中，將 **ApplicationTypeVersion** 屬性從 "1.0.0" 變更為 "2.0.0" 以更新應用程式版本號碼。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-122">In the **ApplicationManifest** element, change the **ApplicationTypeVersion** attribute from "1.0.0" to "2.0.0" to update the app version number.</span></span> <span data-ttu-id="ba3bb-123">儲存已變更的 ApplicationManifest.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-123">Save the changed ApplicationManifest.xml file.</span></span>

## <a name="task-deploy-a-service-fabric-application"></a><span data-ttu-id="ba3bb-124">工作：部署 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="ba3bb-124">Task: Deploy a Service Fabric application</span></span>
<span data-ttu-id="ba3bb-125">在您建置並封裝應用程式 (或下載應用程式封裝) 之後，您可以將應用程式部署至本機 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-125">After you've built and packaged the application (or downloaded the application package), you can deploy the application into a local Service Fabric cluster.</span></span> <span data-ttu-id="ba3bb-126">部署牽涉到上傳應用程式封裝、註冊應用程式類型，以及建立應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-126">Deployment involves uploading the application package, registering the application type, and creating the application instance.</span></span> <span data-ttu-id="ba3bb-127">使用本節中的指示，將新的應用程式部署至叢集。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-127">Use the instructions in this section to deploy a new application to a cluster.</span></span>

### <a name="step-1-upload-the-application-package"></a><span data-ttu-id="ba3bb-128">步驟 1：上傳應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="ba3bb-128">Step 1: Upload the application package</span></span>
<span data-ttu-id="ba3bb-129">上傳應用程式封裝至映像存放區，會將它放在一個可存取至內部 Service Fabric 元件的位置。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-129">Uploading the application package to the image store puts it in a location accessible to internal Service Fabric components.</span></span>  <span data-ttu-id="ba3bb-130">應用程式封裝包含必要的應用程式資訊清單、服務資訊清單，以及用來建立應用程式和服務執行個體的程式碼、組態和資料封裝。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-130">The application package contains the necessary application manifest, service manifests, and code, configuration, and data package(s) to create the application and service instances.</span></span> <span data-ttu-id="ba3bb-131">如果您想要在本機確認應用程式套件，使用 [Test-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-131">If you want to verify the app package locally, use the [Test-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) cmdlet.</span></span>  <span data-ttu-id="ba3bb-132">[Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) 命令會上傳套件。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-132">The [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command uploads the package.</span></span> <span data-ttu-id="ba3bb-133">例如：</span><span class="sxs-lookup"><span data-stu-id="ba3bb-133">For example:</span></span>

```powershell
Copy-ServiceFabricApplicationPackage C:\Temp\WordCount\ -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCount
```

### <a name="step-2-register-the-application-type"></a><span data-ttu-id="ba3bb-134">步驟 2：註冊應用程式類型</span><span class="sxs-lookup"><span data-stu-id="ba3bb-134">Step 2: Register the application type</span></span>
<span data-ttu-id="ba3bb-135">註冊應用程式封裝，讓應用程式類型和應用程式資訊清單中宣告的版本可供使用。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-135">Registering the application package makes the application type and version declared in the application manifest available for use.</span></span> <span data-ttu-id="ba3bb-136">系統會讀取在步驟 1 所上傳的套件，請確認套件 (相當於在本機執行 [Test-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage))、處理套件內容，然後將處理過的套件複製到內部系統位置。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-136">The system reads the package uploaded in the step 1, verify the package (equivalent to running [Test-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) locally), process the package contents, and copy the processed package to an internal system location.</span></span>  <span data-ttu-id="ba3bb-137">執行 [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="ba3bb-137">Run the [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet:</span></span>

```powershell
Register-ServiceFabricApplicationType WordCount
```
<span data-ttu-id="ba3bb-138">若要查看在叢集中註冊的應用程式類型，請執行 [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="ba3bb-138">To see all the application types registered in the cluster, run the [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) cmdlet:</span></span>

```powershell
Get-ServiceFabricApplicationType
```

### <a name="step-3-create-the-application-instance"></a><span data-ttu-id="ba3bb-139">步驟 3：建立應用程式執行個體</span><span class="sxs-lookup"><span data-stu-id="ba3bb-139">Step 3: Create the application instance</span></span>
<span data-ttu-id="ba3bb-140">透過 [New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) 命令，應用程式可以藉由使用已成功註冊的任何應用程式類型版本來進行具現化。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-140">An application can be instantiated by using any application type version that has been registered successfully by using the [New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) command.</span></span> <span data-ttu-id="ba3bb-141">每個應用程式的名稱是在部署時宣告且開頭必須為 **fabric:** 配置，並且是每個應用程式執行個體的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-141">The name of each application is declared at deploy time and must start with the **fabric:** scheme and be unique for each application instance.</span></span> <span data-ttu-id="ba3bb-142">應用程式類型名稱和應用程式類型版本是在應用程式封裝的 **ApplicationManifest.xml** 檔案中宣告。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-142">The application type name and application type version are declared in the **ApplicationManifest.xml** file of the application package.</span></span> <span data-ttu-id="ba3bb-143">如果已在目標應用程式類型的應用程式資訊清單中定義任何預設服務，則這些服務也會一併建立。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-143">If any default services were defined in the application manifest of the target application type, then those are created at this time.</span></span>

```powershell
New-ServiceFabricApplication fabric:/WordCount WordCount 1.0.0
```

<span data-ttu-id="ba3bb-144">[Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) 命令會列出所有已成功建立的應用程式執行個體及其整體狀態。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-144">The [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) command lists all application instances that were successfully created, along with their overall status.</span></span> <span data-ttu-id="ba3bb-145">[Get-ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) 命令會列出所有已指定應用程式執行個體內成功建立的服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-145">The [Get-ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) command lists all of the service instances that were successfully created within a given application instance.</span></span> <span data-ttu-id="ba3bb-146">會列出預設的服務 (若有的話)。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-146">Default services (if any) are listed.</span></span>

```powershell
Get-ServiceFabricApplication

Get-ServiceFabricApplication | Get-ServiceFabricService
```

## <a name="task-upgrade-a-service-fabric-application"></a><span data-ttu-id="ba3bb-147">工作：升級 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="ba3bb-147">Task: Upgrade a Service Fabric application</span></span>
<span data-ttu-id="ba3bb-148">您可以使用已更新的應用程式封裝，升級先前部署的 Service Fabric 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-148">You can upgrade a previously deployed Service Fabric application with an updated application package.</span></span> <span data-ttu-id="ba3bb-149">這項工作會升級先前在「工作：部署 Service Fabric 應用程式」中部署的 WordCount 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-149">This task upgrades the WordCount application that was deployed in "Task: Deploy a Service Fabric application."</span></span> <span data-ttu-id="ba3bb-150">如需詳細資訊，請參閱 [Service Fabric 應用程式升級](service-fabric-application-upgrade.md) 。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-150">Read through [Service Fabric application upgrade](service-fabric-application-upgrade.md) for more information.</span></span>

<span data-ttu-id="ba3bb-151">為了簡化此範例的內容，在先決條件中建立的 WordCountV2 應用程式封裝只更新了應用程式版本號碼。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-151">To keep things simple for this example, only the application version number was updated in the WordCountV2 application package created in the prerequisites.</span></span> <span data-ttu-id="ba3bb-152">有一個更真實的相關案例，其涉及更新您的服務程式碼、組態或資料檔案，然後使用已更新的版本號碼重建並封裝應用程式。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-152">A more realistic scenario would involve updating your service code, configuration, or data files and then rebuilding and packaging the application with updated version numbers.</span></span>  

### <a name="step-1-upload-the-updated-application-package"></a><span data-ttu-id="ba3bb-153">步驟 1：上傳已更新的應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="ba3bb-153">Step 1: Upload the updated application package</span></span>
<span data-ttu-id="ba3bb-154">WordCount v1 應用程式已準備好進行升級。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-154">The WordCount v1 application is ready to be upgraded.</span></span> <span data-ttu-id="ba3bb-155">如果您以系統管理員身分開啟 PowerShell 視窗並且輸入[**Get-ServiceFabricApplication**](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps)，您會看到已部署 1.0.0 版的 WordCount 應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-155">If you open up a PowerShell window as administrator and type [**Get-ServiceFabricApplication**](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps), you see that version 1.0.0 of the WordCount application type is deployed.</span></span>  

<span data-ttu-id="ba3bb-156">現在將更新的應用程式封裝複製到 Service Fabric 映像存放區 (Service Fabric 在其中儲存應用程式封裝)。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-156">Now copy the updated application package to the Service Fabric image store (where the application packages are stored by Service Fabric).</span></span> <span data-ttu-id="ba3bb-157">參數 **ApplicationPackagePathInImageStore** 會通知 Service Fabric 可以在哪裡找到應用程式封裝。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-157">The parameter **ApplicationPackagePathInImageStore** informs Service Fabric where it can find the application package.</span></span> <span data-ttu-id="ba3bb-158">下列命令會將應用程式封裝複製到映像存放區中的 **WordCountV2** ：</span><span class="sxs-lookup"><span data-stu-id="ba3bb-158">The following command copies the application package to **WordCountV2** in the image store:</span></span>  

```powershell
Copy-ServiceFabricApplicationPackage C:\Temp\WordCountV2\ -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCountV2

```
### <a name="step-2-register-the-updated-application-type"></a><span data-ttu-id="ba3bb-159">步驟 2：註冊已更新的應用程式類型</span><span class="sxs-lookup"><span data-stu-id="ba3bb-159">Step 2: Register the updated application type</span></span>
<span data-ttu-id="ba3bb-160">下一步是將新版本的應用程式註冊至 Service Fabric，可以藉由使用 [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) Cmdlet 來執行：</span><span class="sxs-lookup"><span data-stu-id="ba3bb-160">The next step is to register the new version of the application with Service Fabric, which can be performed by using the [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet:</span></span>

```powershell
Register-ServiceFabricApplicationType WordCountV2
```

### <a name="step-3-start-the-upgrade"></a><span data-ttu-id="ba3bb-161">步驟 3：開始升級</span><span class="sxs-lookup"><span data-stu-id="ba3bb-161">Step 3: Start the upgrade</span></span>
<span data-ttu-id="ba3bb-162">各種升級參數、逾時和健全狀況準則可以套用至應用程式升級。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-162">Various upgrade parameters, timeouts, and health criteria can be applied to application upgrades.</span></span> <span data-ttu-id="ba3bb-163">若要深入了解，請詳閱[應用程式升級參數](service-fabric-application-upgrade-parameters.md)和[升級程序](service-fabric-application-upgrade.md)文件。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-163">Read through the [application upgrade parameters](service-fabric-application-upgrade-parameters.md) and [upgrade process](service-fabric-application-upgrade.md) documents to learn more.</span></span> <span data-ttu-id="ba3bb-164">所有服務和執行個體在升級之後都應該是「狀況良好」。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-164">All services and instances should be *healthy* after the upgrade.</span></span>  <span data-ttu-id="ba3bb-165">將 **HealthCheckStableDuration** 設定為 60 秒 (如此一來，在升級繼續至下一個升級網域之前，至少有 20 秒的時間服務是健康狀態良好的)。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-165">Set the **HealthCheckStableDuration** to 60 seconds (so that the services are healthy for at least 20 seconds before the upgrade proceeds to the next upgrade domain).</span></span>  <span data-ttu-id="ba3bb-166">同時也要將 **UpgradeDomainTimeout** 設為 1200 秒，將 **UpgradeTimeout** 設為 3000 秒。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-166">Also set the **UpgradeDomainTimeout** to 1200 seconds and the **UpgradeTimeout** to 3000 seconds.</span></span> <span data-ttu-id="ba3bb-167">最後，將 **UpgradeFailureAction** 設為**回復**，以要求 Service Fabric 在升級期間遇到任何失敗時，將應用程式回復為舊版。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-167">Finally, set the **UpgradeFailureAction** to **rollback**, which requests that Service Fabric rolls back the application to the previous version if failures are encountered during upgrade.</span></span>

<span data-ttu-id="ba3bb-168">您現在可以藉由使用 [Start-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) Cmdlet 啟動應用程式升級：</span><span class="sxs-lookup"><span data-stu-id="ba3bb-168">You can now start the application upgrade by using the [Start-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) cmdlet:</span></span>

```powershell
Start-ServiceFabricApplicationUpgrade -ApplicationName fabric:/WordCount -ApplicationTypeVersion 2.0.0 -HealthCheckStableDurationSec 60 -UpgradeDomainTimeoutSec 1200 -UpgradeTimeout 3000  -FailureAction Rollback -Monitored
```

<span data-ttu-id="ba3bb-169">請注意，應用程式名稱與先前部署的 v1.0.0 應用程式名稱相同 (fabric:/WordCount)。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-169">Note that the application name is the same as the previously deployed v1.0.0 application name (fabric:/WordCount).</span></span> <span data-ttu-id="ba3bb-170">Service Fabric 會使用這個名稱來識別要升級哪一個應用程式。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-170">Service Fabric uses this name to identify which application is getting upgraded.</span></span> <span data-ttu-id="ba3bb-171">如果您設定的逾時太短，您可能會遇到逾時失敗訊息，指出此問題。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-171">If you set the time-outs to be too short, you might encounter a time-out failure message that states the problem.</span></span> <span data-ttu-id="ba3bb-172">請參閱 [疑難排解應用程式升級](service-fabric-application-upgrade-troubleshooting.md)，或增加逾時。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-172">Refer to [Troubleshoot application upgrades](service-fabric-application-upgrade-troubleshooting.md), or increase the time-outs.</span></span>

### <a name="step-4-check-upgrade-progress"></a><span data-ttu-id="ba3bb-173">步驟 4︰檢查升級進度</span><span class="sxs-lookup"><span data-stu-id="ba3bb-173">Step 4: Check upgrade progress</span></span>
<span data-ttu-id="ba3bb-174">您可以使用 [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md)，或使用 [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) Cmdlet，監視應用程式升級進度：</span><span class="sxs-lookup"><span data-stu-id="ba3bb-174">You can monitor application upgrade progress by using [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md), or by using the [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) cmdlet:</span></span>

```powershell
Get-ServiceFabricApplicationUpgrade fabric:/WordCount
```

<span data-ttu-id="ba3bb-175">幾分鐘後，[Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) Cmdlet 會顯示已升級 (完成) 所有升級網域。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-175">In a few minutes, the [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) cmdlet shows that all upgrade domains were upgraded (completed).</span></span>

## <a name="task-test-a-service-fabric-application"></a><span data-ttu-id="ba3bb-176">工作：測試 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="ba3bb-176">Task: Test a Service Fabric application</span></span>
<span data-ttu-id="ba3bb-177">為了撰寫高品質的服務，開發人員必須能夠產生這類不可靠的基礎結構錯誤，才能測試其服務的穩定性。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-177">To write high-quality services, developers need to be able to induce unreliable infrastructure faults to test the stability of their services.</span></span> <span data-ttu-id="ba3bb-178">Service Fabric 讓開發人員可以引發錯誤動作，並且藉由使用混亂和容錯移轉的測試案例以測試失敗情況下的服務。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-178">Service Fabric gives developers the ability to induce fault actions and test services in the presence of failures by using the chaos and failover test scenarios.</span></span>  <span data-ttu-id="ba3bb-179">如需其他資訊，請詳閱[錯誤分析服務簡介](service-fabric-testability-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-179">Read through [Introduction to the Fault Analysis Service](service-fabric-testability-overview.md) for additional information.</span></span>

### <a name="step-1-run-the-chaos-test-scenario"></a><span data-ttu-id="ba3bb-180">步驟 1：執行混亂測試案例</span><span class="sxs-lookup"><span data-stu-id="ba3bb-180">Step 1: Run the chaos test scenario</span></span>
<span data-ttu-id="ba3bb-181">混亂測試案例會在整個 Service Fabric 叢集中產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-181">The chaos test scenario generates faults across the entire Service Fabric cluster.</span></span> <span data-ttu-id="ba3bb-182">此案例會壓縮錯誤，通常是將幾個月或幾年壓縮到幾小時。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-182">The scenario compresses faults generally seen over months or years to a few hours.</span></span> <span data-ttu-id="ba3bb-183">交錯錯誤和高錯誤率的組合，可以找到會在其他情形下被遺漏的極端狀況。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-183">The combination of interleaved faults with a high fault rate finds corner cases that would otherwise be missed.</span></span> <span data-ttu-id="ba3bb-184">下列範例會執行 60 分鐘的混亂測試案例。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-184">The following example runs the chaos test scenario for 60 minutes.</span></span>

```powershell
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```

### <a name="step-2-run-the-failover-test-scenario"></a><span data-ttu-id="ba3bb-185">步驟 2：執行容錯移轉測試案例</span><span class="sxs-lookup"><span data-stu-id="ba3bb-185">Step 2: Run the failover test scenario</span></span>
<span data-ttu-id="ba3bb-186">容錯移轉測試案例的目標是特定服務資料分割，而不是整個叢集，並且讓其他服務不會受到影響。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-186">The failover test scenario targets a specific service partition instead of the entire cluster, and it leaves other services unaffected.</span></span> <span data-ttu-id="ba3bb-187">案例會在您的商務邏輯執行時，在服務驗證中反覆一連串模擬的錯誤。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-187">The scenario iterates through a sequence of simulated faults in service validation while your business logic runs.</span></span> <span data-ttu-id="ba3bb-188">服務驗證中若有失敗，表示有需要進一步調查的問題。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-188">A failure in service validation indicates an issue that needs further investigation.</span></span> <span data-ttu-id="ba3bb-189">容錯移轉測試一次只會引發一個錯誤，不像混亂測試案例，會引發多個錯誤。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-189">The failover test induces only one fault at a time, as opposed to the chaos test scenario, which can induce multiple faults.</span></span> <span data-ttu-id="ba3bb-190">下列範例會對下列網狀架構執行容錯移轉測試 60 分鐘：/WordCount/WordCountService service。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-190">The following example runs the failover test for 60 minutes against the fabric:/WordCount/WordCountService service.</span></span>

```powershell
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/WordCount/WordCountService"

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindUniformInt64 -PartitionKey 1
```

## <a name="task-remove-a-service-fabric-application"></a><span data-ttu-id="ba3bb-191">工作：移除 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="ba3bb-191">Task: Remove a Service Fabric application</span></span>
<span data-ttu-id="ba3bb-192">您可以刪除已部署應用程式的執行個體，從叢集中移除已佈建的應用程式類型，以及從 ImageStore 移除應用程式封裝。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-192">You can delete an instance of a deployed application, remove the provisioned application type from the cluster, and remove the application package from the ImageStore.</span></span>

### <a name="step-1-remove-an-application-instance"></a><span data-ttu-id="ba3bb-193">步驟 1：移除應用程式執行個體</span><span class="sxs-lookup"><span data-stu-id="ba3bb-193">Step 1: Remove an application instance</span></span>
<span data-ttu-id="ba3bb-194">當不再需要應用程式執行個體時，您可以藉由使用 [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) Cmdlet 來永久移除。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-194">When an application instance is no longer needed, you can permanently remove it by using the [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="ba3bb-195">這也會自動移除屬於應用程式的所有服務，同時永久移除所有服務狀態。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-195">This also automatically removes all services belonging to the application, permanently removing all service state.</span></span> <span data-ttu-id="ba3bb-196">此作業無法回復，且應用程式狀態無法復原。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-196">This operation cannot be reversed and application state cannot be recovered.</span></span>

```powershell
Remove-ServiceFabricApplication fabric:/WordCount
```

### <a name="step-2-unregister-the-application-type"></a><span data-ttu-id="ba3bb-197">步驟 2：取消註冊應用程式類型</span><span class="sxs-lookup"><span data-stu-id="ba3bb-197">Step 2: Unregister the application type</span></span>
<span data-ttu-id="ba3bb-198">當您不再需要特定應用程式類型版本時，藉由使用 [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) Cmdlet 來取消註冊。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-198">When you no longer need a particular version of an application type, unregister it by using the [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="ba3bb-199">取消註冊未使用類型，會釋放映像存放區上應用程式封裝所使用的儲存空間。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-199">Unregistering unused types releases storage space used by the application package in the image store.</span></span> <span data-ttu-id="ba3bb-200">只要沒有對應的應用程式進行具現化，或擱置中的應用程式升級進行參考，則應用程式類型即可取消註冊。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-200">An application type can be unregistered as long as there are no applications instantiated against it or pending application upgrades referencing it.</span></span>

```powershell
Unregister-ServiceFabricApplicationType WordCount 1.0.0
```

### <a name="step-3-remove-the-application-package"></a><span data-ttu-id="ba3bb-201">步驟 3：移除應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="ba3bb-201">Step 3: Remove the application package</span></span>
<span data-ttu-id="ba3bb-202">在取消註冊應用程式類型之後，可以藉由使用 [Remove-ServiceFabricApplicationPackage](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) Cmdlet，從 ImageStore 移除應用程式封裝。</span><span class="sxs-lookup"><span data-stu-id="ba3bb-202">After the application type is unregistered, the application package can be removed from the image store by using the [Remove-ServiceFabricApplicationPackage](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span></span>

```powershell
Remove-ServiceFabricApplicationPackage -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCount
```

## <a name="next-steps"></a><span data-ttu-id="ba3bb-203">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ba3bb-203">Next steps</span></span>
[<span data-ttu-id="ba3bb-204">Service Fabric 應用程式生命週期</span><span class="sxs-lookup"><span data-stu-id="ba3bb-204">Service Fabric application lifecycle</span></span>](service-fabric-application-lifecycle.md)

[<span data-ttu-id="ba3bb-205">部署應用程式</span><span class="sxs-lookup"><span data-stu-id="ba3bb-205">Deploy an application</span></span>](service-fabric-deploy-remove-applications.md)

[<span data-ttu-id="ba3bb-206">應用程式升級</span><span class="sxs-lookup"><span data-stu-id="ba3bb-206">Application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="ba3bb-207">Azure Service Fabric Cmdlet</span><span class="sxs-lookup"><span data-stu-id="ba3bb-207">Azure Service Fabric cmdlets</span></span>](/powershell/azure/overview?view=azureservicefabricps)

