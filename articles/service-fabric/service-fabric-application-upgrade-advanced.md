---
title: "進階應用程式升級主題 | Microsoft Docs"
description: "本文章涵蓋升級 Service Fabric 應用程式相關的一些進階主題。"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: e29585ff-e96f-46f4-a07f-6682bbe63281
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar;chackdan
ms.openlocfilehash: 8d3b922f3d50b645ac9db2cc879a319df1262e0a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="service-fabric-application-upgrade-advanced-topics"></a><span data-ttu-id="dd3de-103">Service Fabric 應用程式升級：進階主題</span><span class="sxs-lookup"><span data-stu-id="dd3de-103">Service Fabric application upgrade: advanced topics</span></span>
## <a name="adding-or-removing-services-during-an-application-upgrade"></a><span data-ttu-id="dd3de-104">在應用程式升級期間加入或移除服務</span><span class="sxs-lookup"><span data-stu-id="dd3de-104">Adding or removing services during an application upgrade</span></span>
<span data-ttu-id="dd3de-105">如果新服務已加入準備好部署的應用程式中並發佈為一項升級，新服務就會加入部署的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="dd3de-105">If a new service is added to an application that is already deployed, and published as an upgrade, the new service is added to the deployed application.</span></span>  <span data-ttu-id="dd3de-106">這類升級不會影響已在應用程式中的任何服務。</span><span class="sxs-lookup"><span data-stu-id="dd3de-106">Such an upgrade does not affect any of the services that were already part of the application.</span></span> <span data-ttu-id="dd3de-107">不過，必須為要開始使用的新服務啟動已加入的服務執行個體 (使用 `New-ServiceFabricService` Cmdlet)。</span><span class="sxs-lookup"><span data-stu-id="dd3de-107">However, an instance of the service that was added must be started for the new service to be active (using the `New-ServiceFabricService` cmdlet).</span></span>

<span data-ttu-id="dd3de-108">服務也可從應用程式以升級的方式移除。</span><span class="sxs-lookup"><span data-stu-id="dd3de-108">Services can also be removed from an application as part of an upgrade.</span></span> <span data-ttu-id="dd3de-109">不過，要繼續升級之前，必須先停止所要刪除服務的所有目前執行個體 (使用 `Remove-ServiceFabricService` Cmdlet)。</span><span class="sxs-lookup"><span data-stu-id="dd3de-109">However, all current instances of the to-be-deleted service must be stopped before proceeding with the upgrade (using the `Remove-ServiceFabricService` cmdlet).</span></span>

## <a name="manual-upgrade-mode"></a><span data-ttu-id="dd3de-110">手動升級模式</span><span class="sxs-lookup"><span data-stu-id="dd3de-110">Manual upgrade mode</span></span>
> [!NOTE]
> <span data-ttu-id="dd3de-111">只有對於失敗或已暫停的升級，才應該考量不受監控手動模式。</span><span class="sxs-lookup"><span data-stu-id="dd3de-111">The unmonitored manual mode should be considered only for a failed or suspended upgrade.</span></span> <span data-ttu-id="dd3de-112">監視模式是對於 Service Fabric 應用程式的建議升級模式。</span><span class="sxs-lookup"><span data-stu-id="dd3de-112">The monitored mode is the recommended upgrade mode for Service Fabric applications.</span></span>
>
>

<span data-ttu-id="dd3de-113">Azure Service Fabric 會提供多個升級模式以支援開發和生產叢集。</span><span class="sxs-lookup"><span data-stu-id="dd3de-113">Azure Service Fabric provides multiple upgrade modes to support development and production clusters.</span></span> <span data-ttu-id="dd3de-114">選擇的部署選項可能會因不同的環境而不同。</span><span class="sxs-lookup"><span data-stu-id="dd3de-114">Deployment options chosen may be different for different environments.</span></span>

<span data-ttu-id="dd3de-115">受監視輪流應用程式升級是生產環境中最常使用的升級。</span><span class="sxs-lookup"><span data-stu-id="dd3de-115">The monitored rolling application upgrade is the most typical upgrade to use in the production environment.</span></span> <span data-ttu-id="dd3de-116">指定升級原則時，Service Fabric 會確保應用程式健康狀態良好，再繼續執行升級。</span><span class="sxs-lookup"><span data-stu-id="dd3de-116">When the upgrade policy is specified, Service Fabric ensures that the application is healthy before the upgrade proceeds.</span></span>

 <span data-ttu-id="dd3de-117">應用程式系統管理員可以使用手動輪流應用程式升級模式，對於透過各種升級網域的升級程序擁有完整控制權。</span><span class="sxs-lookup"><span data-stu-id="dd3de-117">The application administrator can use the manual rolling application upgrade mode to have total control over the upgrade progress through the various upgrade domains.</span></span> <span data-ttu-id="dd3de-118">當需要自訂或複雜健康狀態評估原則時，或需要非傳統的升級 (例如，應用程式已經有資料遺失) 時，此模式非常有用。</span><span class="sxs-lookup"><span data-stu-id="dd3de-118">This mode is useful when a customized or complex health evaluation policy is required, or a non-conventional upgrade is happening (for example, the application is already in data loss).</span></span>

<span data-ttu-id="dd3de-119">最後，自動輪流應用程式升級對於開發或測試環境很有用，它會在服務開發期間提供快速反覆運算週期。</span><span class="sxs-lookup"><span data-stu-id="dd3de-119">Finally, the automated rolling application upgrade is useful for development or testing environments to provide a fast iteration cycle during service development.</span></span>

## <a name="change-to-manual-upgrade-mode"></a><span data-ttu-id="dd3de-120">變更為手動升級模式</span><span class="sxs-lookup"><span data-stu-id="dd3de-120">Change to manual upgrade mode</span></span>
<span data-ttu-id="dd3de-121">**手動**- 在目前 UD 停止應用程式升級，並將升級模式變更為「未受監視的手動模式」。</span><span class="sxs-lookup"><span data-stu-id="dd3de-121">**Manual**--Stop the application upgrade at the current UD and change the upgrade mode to Unmonitored Manual.</span></span> <span data-ttu-id="dd3de-122">系統管理員需要手動呼叫 **MoveNextApplicationUpgradeDomainAsync** 以繼續進行升級，或藉由初始化新的升級來觸發回復。</span><span class="sxs-lookup"><span data-stu-id="dd3de-122">The administrator needs to manually call **MoveNextApplicationUpgradeDomainAsync** to proceed with the upgrade or trigger a rollback by initiating a new upgrade.</span></span> <span data-ttu-id="dd3de-123">一旦升級進入手動模式，它會保持在手動模式中直到初始化新的升級。</span><span class="sxs-lookup"><span data-stu-id="dd3de-123">Once the upgrade enters into the Manual mode, it stays in the Manual mode until a new upgrade is initiated.</span></span> <span data-ttu-id="dd3de-124">**GetApplicationUpgradeProgressAsync**命令會傳回 FABRIC\_APPLICATION\_UPGRADE\_STATE\_ROLLING\_FORWARD\_PENDING。</span><span class="sxs-lookup"><span data-stu-id="dd3de-124">The **GetApplicationUpgradeProgressAsync** command returns FABRIC\_APPLICATION\_UPGRADE\_STATE\_ROLLING\_FORWARD\_PENDING.</span></span>

## <a name="upgrade-with-a-diff-package"></a><span data-ttu-id="dd3de-125">使用差異封裝進行升級</span><span class="sxs-lookup"><span data-stu-id="dd3de-125">Upgrade with a diff package</span></span>
<span data-ttu-id="dd3de-126">Service Fabric 應用程式可以藉由佈建完整、獨立式應用程式封裝來升級。</span><span class="sxs-lookup"><span data-stu-id="dd3de-126">A Service Fabric application can be upgraded by provisioning with a full, self-contained application package.</span></span> <span data-ttu-id="dd3de-127">應用程式也可以使用差異封裝升級，該封裝只包含更新的應用程式檔案，和更新的應用程式資訊清單和服務資訊清單檔案。</span><span class="sxs-lookup"><span data-stu-id="dd3de-127">An application can also be upgraded by using a diff package that contains only the updated application files, the updated application manifest, and the service manifest files.</span></span>

<span data-ttu-id="dd3de-128">完整的應用程式封裝包含啟動和執行 Service Fabric 應用程式所需的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="dd3de-128">A full application package contains all the files necessary to start and run a Service Fabric application.</span></span> <span data-ttu-id="dd3de-129">差異封裝只包含最後佈建和目前升級之間變更的檔案，以及完整的應用程式資訊清單和服務資訊清單檔案。</span><span class="sxs-lookup"><span data-stu-id="dd3de-129">A diff package contains only the files that changed between the last provision and the current upgrade, plus the full application manifest and the service manifest files.</span></span> <span data-ttu-id="dd3de-130">在應用程式資訊清單或服務資訊清單的建置版面配置中找不到的任何參考，會在映像存放區中進行搜尋。</span><span class="sxs-lookup"><span data-stu-id="dd3de-130">Any reference in the application manifest or service manifest that can't be found in the build layout is searched for in the image store.</span></span>

<span data-ttu-id="dd3de-131">第一次將應用程式安裝至叢集時需要完整的應用程式封裝。</span><span class="sxs-lookup"><span data-stu-id="dd3de-131">Full application packages are required for the first installation of an application to the cluster.</span></span> <span data-ttu-id="dd3de-132">後續更新可以是完整應用程式封裝或差異封裝。</span><span class="sxs-lookup"><span data-stu-id="dd3de-132">Subsequent updates can be either a full application package or a diff package.</span></span>

<span data-ttu-id="dd3de-133">有時候使用差異封裝也是很好的選擇：</span><span class="sxs-lookup"><span data-stu-id="dd3de-133">Occasions when using a diff package would be a good choice:</span></span>

* <span data-ttu-id="dd3de-134">當您有大型應用程式封裝參考數個服務資訊清單檔案及/或數個程式碼封裝、組態封裝或資料封裝時，最好使用差異封裝。</span><span class="sxs-lookup"><span data-stu-id="dd3de-134">A diff package is preferred when you have a large application package that references several service manifest files and/or several code packages, config packages, or data packages.</span></span>
* <span data-ttu-id="dd3de-135">當您有部署系統會直接從您的應用程式建置程序產生組建版面配置時，最好使用差異封裝。</span><span class="sxs-lookup"><span data-stu-id="dd3de-135">A diff package is preferred when you have a deployment system that generates the build layout directly from your application build process.</span></span> <span data-ttu-id="dd3de-136">在此情況下，即使程式碼沒有任何變更，新建立的組件也會有不同的總和檢查碼。</span><span class="sxs-lookup"><span data-stu-id="dd3de-136">In this case, even though the code hasn't changed, newly built assemblies get a different checksum.</span></span> <span data-ttu-id="dd3de-137">使用完整的應用程式封裝需要您在所有的程式碼封裝上更新版本。</span><span class="sxs-lookup"><span data-stu-id="dd3de-137">Using a full application package would require you to update the version on all code packages.</span></span> <span data-ttu-id="dd3de-138">使用差異封裝，您只需提供已變更的檔案和已變更版本的資訊清單檔案。</span><span class="sxs-lookup"><span data-stu-id="dd3de-138">Using a diff package, you only provide the files that changed and the manifest files where the version has changed.</span></span>

<span data-ttu-id="dd3de-139">使用 Visual Studio 升級應用程式時，會自動發佈差異封裝。</span><span class="sxs-lookup"><span data-stu-id="dd3de-139">When an application is upgraded using Visual Studio, the diff package is published automatically.</span></span> <span data-ttu-id="dd3de-140">若要手動建立差異封裝，就必須更新應用程式資訊清單和服務資訊清單，但只有變更過的封裝才要放入最終的應用程式封裝。</span><span class="sxs-lookup"><span data-stu-id="dd3de-140">To create a diff package manually, the application manifest, and the service manifests must be updated, but only the changed packages should be included in the final application package.</span></span>

<span data-ttu-id="dd3de-141">比方說，讓我們從下列應用程式開始 (為方便了解而提供版本號碼)︰</span><span class="sxs-lookup"><span data-stu-id="dd3de-141">For example, let's start with the following application (version numbers provided for ease of understanding):</span></span>

```text
app1           1.0.0
  service1     1.0.0
    code       1.0.0
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

<span data-ttu-id="dd3de-142">現在，假設您想要使用差異封裝，使用 PowerShell 只更新 service1 的程式碼封裝。</span><span class="sxs-lookup"><span data-stu-id="dd3de-142">Now, let's assume you wanted to update only the code package of service1 using a diff package using PowerShell.</span></span> <span data-ttu-id="dd3de-143">現在，更新的應用程式會有下列資料夾結構︰</span><span class="sxs-lookup"><span data-stu-id="dd3de-143">Now, your updated application has the following folder structure:</span></span>

```text
app1           2.0.0      <-- new version
  service1     2.0.0      <-- new version
    code       2.0.0      <-- new version
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

<span data-ttu-id="dd3de-144">在此情況下，您會將應用程式資訊清單更新為 2.0.0，並更新 service1 的服務資訊清單以反映程式碼封裝更新。</span><span class="sxs-lookup"><span data-stu-id="dd3de-144">In this case, you update the application manifest to 2.0.0, and the service manifest for service1 to reflect the code package update.</span></span> <span data-ttu-id="dd3de-145">應用程式封裝的資料夾會有下列結構︰</span><span class="sxs-lookup"><span data-stu-id="dd3de-145">The folder for your application package would have the following structure:</span></span>

```text
app1/
  service1/
    code/
```

## <a name="next-steps"></a><span data-ttu-id="dd3de-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dd3de-146">Next steps</span></span>
<span data-ttu-id="dd3de-147">[使用 Visual Studio 升級您的應用程式](service-fabric-application-upgrade-tutorial.md) 將引導您完成使用 Visual Studio 進行應用程式升級的步驟。</span><span class="sxs-lookup"><span data-stu-id="dd3de-147">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>

<span data-ttu-id="dd3de-148">[使用 PowerShell 升級您的應用程式](service-fabric-application-upgrade-tutorial-powershell.md) 將引導您完成使用 PowerShell 進行應用程式升級的步驟。</span><span class="sxs-lookup"><span data-stu-id="dd3de-148">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>

<span data-ttu-id="dd3de-149">使用 [升級參數](service-fabric-application-upgrade-parameters.md)來控制您應用程式的升級方式。</span><span class="sxs-lookup"><span data-stu-id="dd3de-149">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>

<span data-ttu-id="dd3de-150">了解如何使用 [資料序列化](service-fabric-application-upgrade-data-serialization.md)，以讓您的應用程式升級相容。</span><span class="sxs-lookup"><span data-stu-id="dd3de-150">Make your application upgrades compatible by learning how to use [Data Serialization](service-fabric-application-upgrade-data-serialization.md).</span></span>

<span data-ttu-id="dd3de-151">參考 [疑難排解應用程式升級](service-fabric-application-upgrade-troubleshooting.md)中的步驟，以修正應用程式升級中常見的問題。</span><span class="sxs-lookup"><span data-stu-id="dd3de-151">Fix common problems in application upgrades by referring to the steps in [Troubleshooting Application Upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>
