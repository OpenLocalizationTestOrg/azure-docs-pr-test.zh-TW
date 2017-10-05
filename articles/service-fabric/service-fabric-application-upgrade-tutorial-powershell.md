---
title: "使用 PowerShell 進行 Service Fabric 應用程式升級 | Microsoft Docs"
description: "本文會逐步解說使用 PowerShell 來部署 Service Fabric 應用程式、變更程式碼及執行升級的體驗。"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 9bc75748-96b0-49ca-8d8a-41fe08398f25
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 3591ced970887d4eb5a33cec8f6951b5476d04f8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="service-fabric-application-upgrade-using-powershell"></a><span data-ttu-id="3bc6d-103">使用 PowerShell 進行 Service Fabric 應用程式升級</span><span class="sxs-lookup"><span data-stu-id="3bc6d-103">Service Fabric application upgrade using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3bc6d-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3bc6d-104">PowerShell</span></span>](service-fabric-application-upgrade-tutorial-powershell.md)
> * [<span data-ttu-id="3bc6d-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3bc6d-105">Visual Studio</span></span>](service-fabric-application-upgrade-tutorial.md)
> 
> 

<br/>

<span data-ttu-id="3bc6d-106">最常使用和建議的升級方法是監視輪流升級。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-106">The most frequently used and recommended upgrade approach is the monitored rolling upgrade.</span></span>  <span data-ttu-id="3bc6d-107">Azure Service Fabric 會根據健康狀態原則集，監視正在升級之應用程式的健康狀態。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-107">Azure Service Fabric monitors the health of the application being upgraded based on a set of health policies.</span></span> <span data-ttu-id="3bc6d-108">當更新網域 (UD) 中的應用程式升級之後，Service Fabric 會評估應用程式健康狀態，並根據健康狀態原則繼續進行下一個更新網域或讓升級失敗。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-108">Once an update domain (UD) is upgraded, Service Fabric evaluates the application health and either proceeds to the next update domain or fails the upgrade depending on the health policies.</span></span>

<span data-ttu-id="3bc6d-109">可以使用受管理或原生 API、PowerShell 或 REST，執行監視應用程式升級。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-109">A monitored application upgrade can be performed using the managed or native APIs, PowerShell, or REST.</span></span> <span data-ttu-id="3bc6d-110">如需有關使用 Visual Studio 來執行升級的說明，請參閱 [使用 Visual Studio 升級您的應用程式](service-fabric-application-upgrade-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-110">For instructions on performing an upgrade using Visual Studio, see [Upgrading your application using Visual Studio](service-fabric-application-upgrade-tutorial.md).</span></span>

<span data-ttu-id="3bc6d-111">透過 Service Fabric 監視輪流升級，應用程式系統管理員即可設定 Service Fabric 用來判斷應用程式健康狀態良好的健康狀態評估原則。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-111">With Service Fabric monitored rolling upgrades, the application administrator can configure the health evaluation policy that Service Fabric uses to determine if the application is healthy.</span></span> <span data-ttu-id="3bc6d-112">此外，系統管理員也可設定當健康狀態評估失敗時採取的動作 (例如，進行自動回復)。本節會逐步解說使用 PowerShell 對其中一個 SDK 範例進行受監視的升級。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-112">In addition, the administrator can configure the action to be taken when the health evaluation fails (for example, doing an automatic rollback.) This section walks through a monitored upgrade for one of the SDK samples that uses PowerShell.</span></span> <span data-ttu-id="3bc6d-113">下列 Microsoft Virtual Academy 影片也會逐步引導您完成應用程式升級︰<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=OrHJH66yC_6406218965">
<img src="./media/service-fabric-application-upgrade-tutorial-powershell/AppLifecycleVid.png" WIDTH="360" HEIGHT="244">
</a></center></span><span class="sxs-lookup"><span data-stu-id="3bc6d-113">The following Microsoft Virtual Academy video also walks you through an app upgrade: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=OrHJH66yC_6406218965">
<img src="./media/service-fabric-application-upgrade-tutorial-powershell/AppLifecycleVid.png" WIDTH="360" HEIGHT="244">
</a></center></span></span>

## <a name="step-1-build-and-deploy-the-visual-objects-sample"></a><span data-ttu-id="3bc6d-114">步驟 1：建置和部署視覺物件範例</span><span class="sxs-lookup"><span data-stu-id="3bc6d-114">Step 1: Build and deploy the Visual Objects sample</span></span>
<span data-ttu-id="3bc6d-115">在應用程式專案 **VisualObjectsApplication** 上按一下滑鼠右鍵，然後選取 [發佈] 命令來建置和發佈應用程式。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-115">Build and publish the application by right-clicking on the application project, **VisualObjectsApplication,** and selecting the **Publish** command.</span></span>  <span data-ttu-id="3bc6d-116">如需詳細資訊，請參閱 [Service Fabric 應用程式升級教學課程](service-fabric-application-upgrade-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-116">For more information, see [Service Fabric application upgrade tutorial](service-fabric-application-upgrade-tutorial.md).</span></span>  <span data-ttu-id="3bc6d-117">或者，您可以使用 PowerShell 來部署您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-117">Alternatively, you can use PowerShell to deploy your application.</span></span>

> [!NOTE]
> <span data-ttu-id="3bc6d-118">在 PowerShell 中使用任何 Service Fabric 命令之前，您必須先使用 `Connect-ServiceFabricCluster` Cmdlet 連接到叢集。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-118">Before any of the Service Fabric commands may be used in PowerShell, you first need to connect to the cluster by using the `Connect-ServiceFabricCluster` cmdlet.</span></span> <span data-ttu-id="3bc6d-119">同樣地，它會假設已經在本機電腦上設定叢集。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-119">Similarly, it is assumed that the Cluster has already been set up on your local machine.</span></span> <span data-ttu-id="3bc6d-120">請參閱 [設定 Service Fabric 開發環境](service-fabric-get-started.md)上的文章</span><span class="sxs-lookup"><span data-stu-id="3bc6d-120">See the article on [setting up your Service Fabric development environment](service-fabric-get-started.md).</span></span>
> 
> 

<span data-ttu-id="3bc6d-121">在 Visual Studio 中建置專案後，您可以使用 PowerShell 命令 [Copy-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/copy-servicefabricapplicationpackage) 將應用程式封裝複製到 ImageStore。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-121">After building the project in Visual Studio, you can use the PowerShell command [Copy-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/copy-servicefabricapplicationpackage) to copy the application package to the ImageStore.</span></span> <span data-ttu-id="3bc6d-122">如果您想要在本機確認應用程式套件，使用 [Test-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-122">If you want to verify the app package locally, use the [Test-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) cmdlet.</span></span> <span data-ttu-id="3bc6d-123">下一個步驟是使用 [Register-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/register-servicefabricapplicationtype) Cmdlet 將應用程式註冊至 Service Fabric 執行階段。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-123">The next step is to register the application to the Service Fabric runtime using the [Register-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/register-servicefabricapplicationtype) cmdlet.</span></span> <span data-ttu-id="3bc6d-124">最後一個步驟是使用 [New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) Cmdlet 啟動應用程式的執行個體。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-124">The final step is to start an instance of the application by using the [New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet.</span></span>  <span data-ttu-id="3bc6d-125">這三個步驟類似於在 Visual Studio 中使用 [部署]  功能表項目。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-125">These three steps are analogous to using the **Deploy** menu item in Visual Studio.</span></span>

<span data-ttu-id="3bc6d-126">現在，您可以使用 [Service Fabric Explorer 來檢視叢集與應用程式](service-fabric-visualizing-your-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-126">Now, you can use [Service Fabric Explorer to view the cluster and the application](service-fabric-visualizing-your-cluster.md).</span></span> <span data-ttu-id="3bc6d-127">該應用程式有一個 Web 服務，透過在 Internet Explorer 的網址列中輸入 [http://localhost:8081/visualobjects](http://localhost:8081/visualobjects) ，即可瀏覽至該服務。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-127">The application has a web service that can be navigated to in Internet Explorer by typing [http://localhost:8081/visualobjects](http://localhost:8081/visualobjects) in the address bar.</span></span>  <span data-ttu-id="3bc6d-128">您應該會在畫面上看到一些浮動視覺物件四處移動。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-128">You should see some floating visual objects moving around in the screen.</span></span>  <span data-ttu-id="3bc6d-129">此外，您可以使用 [Get-ServiceFabricApplication](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) 檢查應用程式狀態。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-129">Additionally, you can use [Get-ServiceFabricApplication](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) to check the application status.</span></span>

## <a name="step-2-update-the-visual-objects-sample"></a><span data-ttu-id="3bc6d-130">步驟 2：更新視覺物件範例</span><span class="sxs-lookup"><span data-stu-id="3bc6d-130">Step 2: Update the Visual Objects sample</span></span>
<span data-ttu-id="3bc6d-131">您可能會注意到在步驟 1 中已部署的版本，視覺物件不會旋轉。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-131">You might notice that with the version that was deployed in Step 1, the visual objects do not rotate.</span></span> <span data-ttu-id="3bc6d-132">讓我們將這個應用程式升級到其中的視覺物件也會旋轉的版本。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-132">Let's upgrade this application to one where the visual objects also rotate.</span></span>

<span data-ttu-id="3bc6d-133">選取 VisualObjects 解決方案內的 VisualObjects.ActorService 專案，然後開啟 StatefulVisualObjectActor.cs 檔案。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-133">Select the VisualObjects.ActorService project within the VisualObjects solution, and open the StatefulVisualObjectActor.cs file.</span></span> <span data-ttu-id="3bc6d-134">在該檔案內，瀏覽至 `MoveObject` 方法，然後將 `this.State.Move()` 標記為註解，然後將 `this.State.Move(true)` 取消註解。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-134">Within that file, navigate to the method `MoveObject`, comment out `this.State.Move()`, and uncomment `this.State.Move(true)`.</span></span> <span data-ttu-id="3bc6d-135">這項變更會在服務升級後旋轉物件。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-135">This change rotates the objects after the service is upgraded.</span></span>

<span data-ttu-id="3bc6d-136">我們也需要更新 *VisualObjects.ActorService* 專案的 **ServiceManifest.xml**檔案 (在 [PackageRoot] 底下)。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-136">We also need to update the *ServiceManifest.xml* file (under PackageRoot) of the project **VisualObjects.ActorService**.</span></span> <span data-ttu-id="3bc6d-137">請將 *ServiceManifest.xml* 檔案中的 *CodePackage* 和服務版本及對應的行更新成 2.0。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-137">Update the *CodePackage* and the service version to 2.0, and the corresponding lines in the *ServiceManifest.xml* file.</span></span>
<span data-ttu-id="3bc6d-138">您可以在對解決方案按一下滑鼠右鍵之後，使用 Visual Studio [編輯資訊清單檔案]  選項來進行資訊清單檔案變更。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-138">You can use the Visual Studio *Edit Manifest Files* option after you right-click on the solution to make the manifest file changes.</span></span>

<span data-ttu-id="3bc6d-139">進行變更之後，資訊清單應該會看起來如下 (醒目提示的部分即為所做的變更)：</span><span class="sxs-lookup"><span data-stu-id="3bc6d-139">After the changes are made, the manifest should look like the following (highlighted portions show the changes):</span></span>

```xml
<ServiceManifestName="VisualObjects.ActorService" Version="2.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

<CodePackageName="Code" Version="2.0">
```

<span data-ttu-id="3bc6d-140">現在，*ApplicationManifest.xml* 檔案 (可以在 **VisualObjects** 方案下的 **VisualObjects** 專案下找到)，會更新為 2.0 版的 **VisualObjects.ActorService** 專案。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-140">Now the *ApplicationManifest.xml* file (found under the **VisualObjects** project under the **VisualObjects** solution) is updated to version 2.0 of the **VisualObjects.ActorService** project.</span></span> <span data-ttu-id="3bc6d-141">此外，應用程式版本也會從 1.0.0.0 更新為 2.0.0.0。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-141">In addition, the Application version is updated to 2.0.0.0 from 1.0.0.0.</span></span> <span data-ttu-id="3bc6d-142">*ApplicationManifest.xml* 看起來應該類似下列程式碼片段︰</span><span class="sxs-lookup"><span data-stu-id="3bc6d-142">The *ApplicationManifest.xml* should look like the following snippet:</span></span>

```xml
<ApplicationManifestxmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="VisualObjects" ApplicationTypeVersion="2.0.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

 <ServiceManifestRefServiceManifestName="VisualObjects.ActorService" ServiceManifestVersion="2.0" />
```


<span data-ttu-id="3bc6d-143">現在只選取 [ActorService] 專案，然後以滑鼠右鍵按一下並選取 Visual Studio 中的 [組建] 選項建置專案。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-143">Now, build the project by selecting just the **ActorService** project, and then right-clicking and selecting the **Build** option in Visual Studio.</span></span> <span data-ttu-id="3bc6d-144">如果您選取 [全部重建]，因為程式碼已變更，所以您要更新所有專案的版本。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-144">If you select **Rebuild all**, you should update the versions for all projects, since the code would have changed.</span></span> <span data-ttu-id="3bc6d-145">接下來，在 [VisualObjectsApplication] 上按一下滑鼠右鍵，選取 [Service Fabric] 功能表，然後選擇 [封裝]，來封裝已更新的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-145">Next, let's package the updated application by right-clicking on ***VisualObjectsApplication***, selecting the Service Fabric Menu, and choosing **Package**.</span></span> <span data-ttu-id="3bc6d-146">這個動作會建立可部署的應用程式封裝。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-146">This action creates an application package that can be deployed.</span></span>  <span data-ttu-id="3bc6d-147">更新的應用程式已準備好進行部署。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-147">Your updated application is ready to be deployed.</span></span>

## <a name="step-3--decide-on-health-policies-and-upgrade-parameters"></a><span data-ttu-id="3bc6d-148">步驟 3：決定健康狀態原則並升級參數</span><span class="sxs-lookup"><span data-stu-id="3bc6d-148">Step 3:  Decide on health policies and upgrade parameters</span></span>
<span data-ttu-id="3bc6d-149">請您熟悉[應用程式升級參數](service-fabric-application-upgrade-parameters.md)和[升級程序](service-fabric-application-upgrade.md)，以了解套用的各種升級參數、逾時和健康狀態準則。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-149">Familiarize yourself with the [application upgrade parameters](service-fabric-application-upgrade-parameters.md) and the [upgrade process](service-fabric-application-upgrade.md) to get a good understanding of the various upgrade parameters, time-outs, and health criterion applied.</span></span> <span data-ttu-id="3bc6d-150">對於此逐步解說，服務健康狀態評估準則會設定為預設值 (和建議值)，這表示升級之後，所有服務和執行個體應該是「健康狀態良好」  。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-150">For this walkthrough, the service health evaluation criterion is set to the default (and recommended) values, which means that all services and instances should be *healthy* after the upgrade.</span></span>  

<span data-ttu-id="3bc6d-151">但是，讓我們將 *HealthCheckStableDuration* 增加為 60 秒 (如此一來，在升級繼續至下一個更新網域之前，至少有 20 秒的時間服務是健康狀態良好的)。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-151">However, let's increase the *HealthCheckStableDuration* to 60 seconds (so that the services are healthy for at least 20 seconds before the upgrade proceeds to the next update domain).</span></span>  <span data-ttu-id="3bc6d-152">同時也要將 *UpgradeDomainTimeout* 設為 1200 秒，將 *UpgradeTimeout* 設為 3000 秒。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-152">Let's also set the *UpgradeDomainTimeout* to be 1200 seconds and the *UpgradeTimeout* to be 3000 seconds.</span></span>

<span data-ttu-id="3bc6d-153">最後，我們也將 *UpgradeFailureAction* 設定為回復。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-153">Finally, let's also set the *UpgradeFailureAction* to rollback.</span></span> <span data-ttu-id="3bc6d-154">此選項要求 Service Fabric 在升級期間如果遇到任何問題時要將應用程式回復為舊版。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-154">This option requires Service Fabric to roll back the application to the previous version if it encounters any issues during the upgrade.</span></span> <span data-ttu-id="3bc6d-155">因此在啟動升級 (在步驟 4) 時，會指定下列參數︰</span><span class="sxs-lookup"><span data-stu-id="3bc6d-155">Thus, when starting the upgrade (in Step 4), the following parameters are specified:</span></span>

<span data-ttu-id="3bc6d-156">FailureAction = Rollback</span><span class="sxs-lookup"><span data-stu-id="3bc6d-156">FailureAction = Rollback</span></span>

<span data-ttu-id="3bc6d-157">HealthCheckStableDurationSec = 60</span><span class="sxs-lookup"><span data-stu-id="3bc6d-157">HealthCheckStableDurationSec = 60</span></span>

<span data-ttu-id="3bc6d-158">UpgradeDomainTimeoutSec = 1200</span><span class="sxs-lookup"><span data-stu-id="3bc6d-158">UpgradeDomainTimeoutSec = 1200</span></span>

<span data-ttu-id="3bc6d-159">UpgradeTimeout = 3000</span><span class="sxs-lookup"><span data-stu-id="3bc6d-159">UpgradeTimeout = 3000</span></span>

## <a name="step-4-prepare-application-for-upgrade"></a><span data-ttu-id="3bc6d-160">步驟 4：準備應用程式以進行升級</span><span class="sxs-lookup"><span data-stu-id="3bc6d-160">Step 4: Prepare application for upgrade</span></span>
<span data-ttu-id="3bc6d-161">現在，應用程式已建置並且準備好進行升級。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-161">Now the application is built and ready to be upgraded.</span></span> <span data-ttu-id="3bc6d-162">如果您以系統管理員身分開啟 PowerShell 視窗並且輸入 [Get-ServiceFabricApplication](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps)，它應該會讓您知道它是已部署之 **VisualObjects** 的應用程式類型 1.0.0.0。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-162">If you open up a PowerShell window as an administrator and type [Get-ServiceFabricApplication](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps), it should let you know that it is application type 1.0.0.0 of **VisualObjects** that's been deployed.</span></span>  

<span data-ttu-id="3bc6d-163">應用程式封裝儲存在以下的相對路徑，您在其中解壓縮 Service Fabric SDK - *Samples\Services\Stateful\VisualObjects\VisualObjects\obj\x64\Debug*。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-163">The application package is stored under the following relative path where you uncompressed the Service Fabric SDK - *Samples\Services\Stateful\VisualObjects\VisualObjects\obj\x64\Debug*.</span></span> <span data-ttu-id="3bc6d-164">您應該會在該目錄中找到 "Package" 資料夾，這是應用程式封裝儲存的位置。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-164">You should find a "Package" folder in that directory, where the application package is stored.</span></span> <span data-ttu-id="3bc6d-165">檢查時間戳記以確保它是最新組建 (您也可能需要適當地修改路徑)。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-165">Check the timestamps to ensure that it is the latest build (you may need to modify the paths appropriately as well).</span></span>

<span data-ttu-id="3bc6d-166">現在讓我們將更新的應用程式封裝複製到 Service Fabric ImageStore (Service Fabric 在其中儲存應用程式封裝)。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-166">Now let's copy the updated application package to the Service Fabric ImageStore (where the application packages are stored by Service Fabric).</span></span> <span data-ttu-id="3bc6d-167">參數 *ApplicationPackagePathInImageStore* 會通知 Service Fabric 可以在哪裡找到應用程式封裝。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-167">The parameter *ApplicationPackagePathInImageStore* informs Service Fabric where it can find the application package.</span></span> <span data-ttu-id="3bc6d-168">使用下列命令將更新的應用程式放在 "VisualObjects\_V2" (您可能需要再次適當地修改路徑)。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-168">We have put the updated application in "VisualObjects\_V2" with the following command (you may need to modify paths again appropriately).</span></span>

```powershell
Copy-ServiceFabricApplicationPackage  -ApplicationPackagePath .\Samples\Services\Stateful\VisualObjects\VisualObjects\obj\x64\Debug\Package
-ImageStoreConnectionString fabric:ImageStore   -ApplicationPackagePathInImageStore "VisualObjects\_V2"
```

<span data-ttu-id="3bc6d-169">下一步是向 Service Fabric 註冊此應用程式，這可以使用 [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) 命令來執行：</span><span class="sxs-lookup"><span data-stu-id="3bc6d-169">The next step is to register this application with Service Fabric, which can be performed using the [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) command:</span></span>

```powershell
Register-ServiceFabricApplicationType -ApplicationPathInImageStore "VisualObjects\_V2"
```

<span data-ttu-id="3bc6d-170">如果上述命令不成功，很可能是您需要重建所有服務。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-170">If the preceding command doesn't succeed, it is likely that you need a rebuild of all services.</span></span> <span data-ttu-id="3bc6d-171">如步驟 2 中所述，您可能也必須更新您的 WebService 版本。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-171">As mentioned in Step 2, you may have to update your WebService version as well.</span></span>

## <a name="step-5-start-the-application-upgrade"></a><span data-ttu-id="3bc6d-172">步驟 5：開始應用程式升級</span><span class="sxs-lookup"><span data-stu-id="3bc6d-172">Step 5: Start the application upgrade</span></span>
<span data-ttu-id="3bc6d-173">現在，您已準備好使用 [Start-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps)命令來啟動應用程式升級：</span><span class="sxs-lookup"><span data-stu-id="3bc6d-173">Now, we're all set to start the application upgrade by using the [Start-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) command:</span></span>

```powershell
Start-ServiceFabricApplicationUpgrade -ApplicationName fabric:/VisualObjects -ApplicationTypeVersion 2.0.0.0 -HealthCheckStableDurationSec 60 -UpgradeDomainTimeoutSec 1200 -UpgradeTimeout 3000   -FailureAction Rollback -Monitored
```


<span data-ttu-id="3bc6d-174">應用程式名稱如 *ApplicationManifest.xml* 檔案中所述。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-174">The application name is the same as it was described in the *ApplicationManifest.xml* file.</span></span> <span data-ttu-id="3bc6d-175">Service Fabric 會使用這個名稱來識別要升級哪一個應用程式。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-175">Service Fabric uses this name to identify which application is getting upgraded.</span></span> <span data-ttu-id="3bc6d-176">如果您設定的逾時太短，您可能會遇到失敗訊息，指出此問題。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-176">If you set the time-outs to be too short, you may encounter a failure message that states the problem.</span></span> <span data-ttu-id="3bc6d-177">請參閱疑難排解章節，或增加逾時。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-177">Refer to the troubleshooting section, or increase the time-outs.</span></span>

<span data-ttu-id="3bc6d-178">現在，當應用程式升級進行時，您可以使用 Service Fabric Explorer 或 [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) PowerShell 命令監視進度。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-178">Now, as the application upgrade proceeds, you can monitor it using Service Fabric Explorer, or by using the [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) PowerShell command:</span></span> 

```powershell
Get-ServiceFabricApplicationUpgrade fabric:/VisualObjects
```

<span data-ttu-id="3bc6d-179">幾分鐘後，使用上述 PowerShell 命令所取得的狀態應該會顯示所有更新網域已升級 (完成)。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-179">In a few minutes, the status that you got by using the preceding PowerShell command, should state that all update domains were upgraded (completed).</span></span> <span data-ttu-id="3bc6d-180">而且，您應該會在瀏覽器視窗中發現該視覺物件已經開始旋轉！</span><span class="sxs-lookup"><span data-stu-id="3bc6d-180">And you should find that the visual objects in your browser window have started rotating!</span></span>

<span data-ttu-id="3bc6d-181">您可以嘗試從第 2 版升級到第 3 版，或練習從第 2 版升級為第 1 版。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-181">You can try upgrading from version 2 to version 3, or from version 2 to version 1 as an exercise.</span></span> <span data-ttu-id="3bc6d-182">從第 2 版移至第 1 版也視為一種升級。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-182">Moving from version 2 to version 1 is also considered an upgrade.</span></span> <span data-ttu-id="3bc6d-183">練習逾時和健康狀態原則，讓自己更熟練。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-183">Play with time-outs and health policies to make yourself familiar with them.</span></span> <span data-ttu-id="3bc6d-184">當您部署至 Azure 叢集時，參數必須正確設定。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-184">When you are deploying to an Azure cluster, the parameters need to be set appropriately.</span></span> <span data-ttu-id="3bc6d-185">最好保守地設定逾時。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-185">It is good to set the time-outs conservatively.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3bc6d-186">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3bc6d-186">Next steps</span></span>
<span data-ttu-id="3bc6d-187">[使用 Visual Studio 升級您的應用程式](service-fabric-application-upgrade-tutorial.md) 將引導您完成使用 Visual Studio 進行應用程式升級的步驟。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-187">[Upgrading your application using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>

<span data-ttu-id="3bc6d-188">使用 [升級參數](service-fabric-application-upgrade-parameters.md)來控制您應用程式的升級方式。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-188">Control how your application upgrades by using [upgrade parameters](service-fabric-application-upgrade-parameters.md).</span></span>

<span data-ttu-id="3bc6d-189">了解如何使用 [資料序列化](service-fabric-application-upgrade-data-serialization.md)，以讓您的應用程式升級相容。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-189">Make your application upgrades compatible by learning how to use [data serialization](service-fabric-application-upgrade-data-serialization.md).</span></span>

<span data-ttu-id="3bc6d-190">參考 [進階主題](service-fabric-application-upgrade-advanced.md)，以了解如何在升級您的應用程式時使用進階功能。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-190">Learn how to use advanced functionality while upgrading your application by referring to [Advanced topics](service-fabric-application-upgrade-advanced.md).</span></span>

<span data-ttu-id="3bc6d-191">參考 [疑難排解應用程式升級](service-fabric-application-upgrade-troubleshooting.md)中的步驟，以修正應用程式升級中常見的問題。</span><span class="sxs-lookup"><span data-stu-id="3bc6d-191">Fix common problems in application upgrades by referring to the steps in [Troubleshooting application upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>

