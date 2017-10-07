---
title: "應用程式升級主題 aaaAdvanced |Microsoft 文件"
description: "本文涵蓋有關 tooupgrading Service Fabric 應用程式的某些進階的主題。"
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
ms.openlocfilehash: bdaf3db6209c574d39f57e0bf9951fad5ad1cbec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-advanced-topics"></a><span data-ttu-id="91f37-103">Service Fabric 應用程式升級：進階主題</span><span class="sxs-lookup"><span data-stu-id="91f37-103">Service Fabric application upgrade: advanced topics</span></span>
## <a name="adding-or-removing-services-during-an-application-upgrade"></a><span data-ttu-id="91f37-104">在應用程式升級期間加入或移除服務</span><span class="sxs-lookup"><span data-stu-id="91f37-104">Adding or removing services during an application upgrade</span></span>
<span data-ttu-id="91f37-105">如果以升級加入 tooan 應用程式已經部署，並發行新的服務，就會 hello 新服務加入的 toohello 部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="91f37-105">If a new service is added tooan application that is already deployed, and published as an upgrade, hello new service is added toohello deployed application.</span></span>  <span data-ttu-id="91f37-106">這類升級不會影響任何 hello 服務已經過 hello 應用程式的一部分。</span><span class="sxs-lookup"><span data-stu-id="91f37-106">Such an upgrade does not affect any of hello services that were already part of hello application.</span></span> <span data-ttu-id="91f37-107">不過，已加入的 hello 服務的執行個體必須啟動 hello 新服務 toobe 作用中 (使用 hello `New-ServiceFabricService` cmdlet)。</span><span class="sxs-lookup"><span data-stu-id="91f37-107">However, an instance of hello service that was added must be started for hello new service toobe active (using hello `New-ServiceFabricService` cmdlet).</span></span>

<span data-ttu-id="91f37-108">服務也可從應用程式以升級的方式移除。</span><span class="sxs-lookup"><span data-stu-id="91f37-108">Services can also be removed from an application as part of an upgrade.</span></span> <span data-ttu-id="91f37-109">不過，必須停止 hello 要刪除服務的所有目前的執行個體繼續執行 hello 升級 (使用 hello `Remove-ServiceFabricService` cmdlet)。</span><span class="sxs-lookup"><span data-stu-id="91f37-109">However, all current instances of hello to-be-deleted service must be stopped before proceeding with hello upgrade (using hello `Remove-ServiceFabricService` cmdlet).</span></span>

## <a name="manual-upgrade-mode"></a><span data-ttu-id="91f37-110">手動升級模式</span><span class="sxs-lookup"><span data-stu-id="91f37-110">Manual upgrade mode</span></span>
> [!NOTE]
> <span data-ttu-id="91f37-111">hello 未受監視的手動模式只應該考量失敗或已暫停的升級。</span><span class="sxs-lookup"><span data-stu-id="91f37-111">hello unmonitored manual mode should be considered only for a failed or suspended upgrade.</span></span> <span data-ttu-id="91f37-112">hello 受監視的模式是 hello 建議 Service Fabric 應用程式的升級模式。</span><span class="sxs-lookup"><span data-stu-id="91f37-112">hello monitored mode is hello recommended upgrade mode for Service Fabric applications.</span></span>
>
>

<span data-ttu-id="91f37-113">Azure Service Fabric 提供多個升級模式 toosupport 開發和生產叢集。</span><span class="sxs-lookup"><span data-stu-id="91f37-113">Azure Service Fabric provides multiple upgrade modes toosupport development and production clusters.</span></span> <span data-ttu-id="91f37-114">選擇的部署選項可能會因不同的環境而不同。</span><span class="sxs-lookup"><span data-stu-id="91f37-114">Deployment options chosen may be different for different environments.</span></span>

<span data-ttu-id="91f37-115">受監視的 hello 輪流應用程式升級為 hello 最常見升級的 toouse hello 實際執行環境中。</span><span class="sxs-lookup"><span data-stu-id="91f37-115">hello monitored rolling application upgrade is hello most typical upgrade toouse in hello production environment.</span></span> <span data-ttu-id="91f37-116">當 hello 升級指定原則時，Service Fabric 可確保 hello 應用程式狀況良好，才 hello 升級會繼續執行。</span><span class="sxs-lookup"><span data-stu-id="91f37-116">When hello upgrade policy is specified, Service Fabric ensures that hello application is healthy before hello upgrade proceeds.</span></span>

 <span data-ttu-id="91f37-117">hello 應用程式系統管理員可以使用 hello 手動復原應用程式升級模式 toohave 的完整控制權 hello 升級進度 hello 透過各種 「 升級 」 網域。</span><span class="sxs-lookup"><span data-stu-id="91f37-117">hello application administrator can use hello manual rolling application upgrade mode toohave total control over hello upgrade progress through hello various upgrade domains.</span></span> <span data-ttu-id="91f37-118">自訂或複雜的健全狀況評估原則是必要的或發生非傳統升級時，此模式非常有用 （例如，hello 應用程式已在資料遺失）。</span><span class="sxs-lookup"><span data-stu-id="91f37-118">This mode is useful when a customized or complex health evaluation policy is required, or a non-conventional upgrade is happening (for example, hello application is already in data loss).</span></span>

<span data-ttu-id="91f37-119">最後，hello 自動化的應用程式輪流升級是適用於開發或測試環境 tooprovide 快速的反覆項目循環期間服務開發。</span><span class="sxs-lookup"><span data-stu-id="91f37-119">Finally, hello automated rolling application upgrade is useful for development or testing environments tooprovide a fast iteration cycle during service development.</span></span>

## <a name="change-toomanual-upgrade-mode"></a><span data-ttu-id="91f37-120">變更 toomanual 升級模式</span><span class="sxs-lookup"><span data-stu-id="91f37-120">Change toomanual upgrade mode</span></span>
<span data-ttu-id="91f37-121">**手動**-hello 目前 UD 和變更 hello 停止 hello 應用程式升級升級模式 tooUnmonitored 手冊。</span><span class="sxs-lookup"><span data-stu-id="91f37-121">**Manual**--Stop hello application upgrade at hello current UD and change hello upgrade mode tooUnmonitored Manual.</span></span> <span data-ttu-id="91f37-122">hello 系統管理員必須 toomanually 呼叫**MoveNextApplicationUpgradeDomainAsync**以 hello tooproceed 升級，或藉由初始化新的升級觸發復原。</span><span class="sxs-lookup"><span data-stu-id="91f37-122">hello administrator needs toomanually call **MoveNextApplicationUpgradeDomainAsync** tooproceed with hello upgrade or trigger a rollback by initiating a new upgrade.</span></span> <span data-ttu-id="91f37-123">一旦 hello 升級進入 hello 手動模式時，它會保持在 hello 手動模式起始新的升級之前。</span><span class="sxs-lookup"><span data-stu-id="91f37-123">Once hello upgrade enters into hello Manual mode, it stays in hello Manual mode until a new upgrade is initiated.</span></span> <span data-ttu-id="91f37-124">hello **GetApplicationUpgradeProgressAsync**命令會傳回網狀架構\_應用程式\_升級\_狀態\_循環\_向前\_擱置。</span><span class="sxs-lookup"><span data-stu-id="91f37-124">hello **GetApplicationUpgradeProgressAsync** command returns FABRIC\_APPLICATION\_UPGRADE\_STATE\_ROLLING\_FORWARD\_PENDING.</span></span>

## <a name="upgrade-with-a-diff-package"></a><span data-ttu-id="91f37-125">使用差異封裝進行升級</span><span class="sxs-lookup"><span data-stu-id="91f37-125">Upgrade with a diff package</span></span>
<span data-ttu-id="91f37-126">Service Fabric 應用程式可以藉由佈建完整、獨立式應用程式封裝來升級。</span><span class="sxs-lookup"><span data-stu-id="91f37-126">A Service Fabric application can be upgraded by provisioning with a full, self-contained application package.</span></span> <span data-ttu-id="91f37-127">也可以使用包含唯一的 hello 更新應用程式檔案的差異比對封裝來升級應用程式，hello 更新應用程式資訊清單和 hello 服務資訊清單檔案。</span><span class="sxs-lookup"><span data-stu-id="91f37-127">An application can also be upgraded by using a diff package that contains only hello updated application files, hello updated application manifest, and hello service manifest files.</span></span>

<span data-ttu-id="91f37-128">完整的應用程式套件包含所有 hello 檔案需要 toostart 和執行 Service Fabric 應用程式。</span><span class="sxs-lookup"><span data-stu-id="91f37-128">A full application package contains all hello files necessary toostart and run a Service Fabric application.</span></span> <span data-ttu-id="91f37-129">Diff 封裝包含只有 hello hello 最後一個佈建與 hello 目前升級時，之間變更的檔案加上 hello 完整的應用程式資訊清單和 hello 服務資訊清單檔案。</span><span class="sxs-lookup"><span data-stu-id="91f37-129">A diff package contains only hello files that changed between hello last provision and hello current upgrade, plus hello full application manifest and hello service manifest files.</span></span> <span data-ttu-id="91f37-130">Hello 應用程式資訊清單或 hello 組建版面配置中找不到的服務資訊清單中的任何參考搜尋 hello 映像存放區中。</span><span class="sxs-lookup"><span data-stu-id="91f37-130">Any reference in hello application manifest or service manifest that can't be found in hello build layout is searched for in hello image store.</span></span>

<span data-ttu-id="91f37-131">完整的應用程式套件所需的應用程式 toohello 叢集 hello 第一次安裝。</span><span class="sxs-lookup"><span data-stu-id="91f37-131">Full application packages are required for hello first installation of an application toohello cluster.</span></span> <span data-ttu-id="91f37-132">後續更新可以是完整應用程式封裝或差異封裝。</span><span class="sxs-lookup"><span data-stu-id="91f37-132">Subsequent updates can be either a full application package or a diff package.</span></span>

<span data-ttu-id="91f37-133">有時候使用差異封裝也是很好的選擇：</span><span class="sxs-lookup"><span data-stu-id="91f37-133">Occasions when using a diff package would be a good choice:</span></span>

* <span data-ttu-id="91f37-134">當您有大型應用程式封裝參考數個服務資訊清單檔案及/或數個程式碼封裝、組態封裝或資料封裝時，最好使用差異封裝。</span><span class="sxs-lookup"><span data-stu-id="91f37-134">A diff package is preferred when you have a large application package that references several service manifest files and/or several code packages, config packages, or data packages.</span></span>
* <span data-ttu-id="91f37-135">您有部署系統，直接從您的應用程式建置程序產生 hello 組建版面配置時，最好使用差異封裝。</span><span class="sxs-lookup"><span data-stu-id="91f37-135">A diff package is preferred when you have a deployment system that generates hello build layout directly from your application build process.</span></span> <span data-ttu-id="91f37-136">在此情況下，雖然 hello 碼未變更，新建立的組件會得到不同的總和檢查碼。</span><span class="sxs-lookup"><span data-stu-id="91f37-136">In this case, even though hello code hasn't changed, newly built assemblies get a different checksum.</span></span> <span data-ttu-id="91f37-137">使用完整的應用程式封裝需要您 tooupdate hello 版本所有的程式碼封裝。</span><span class="sxs-lookup"><span data-stu-id="91f37-137">Using a full application package would require you tooupdate hello version on all code packages.</span></span> <span data-ttu-id="91f37-138">使用 差異比對封裝，您僅提供變更的 hello 檔案及 hello hello 版本已變更的資訊清單的檔案。</span><span class="sxs-lookup"><span data-stu-id="91f37-138">Using a diff package, you only provide hello files that changed and hello manifest files where hello version has changed.</span></span>

<span data-ttu-id="91f37-139">使用 Visual Studio 升級應用程式時，便會自動發行 hello 差異封裝。</span><span class="sxs-lookup"><span data-stu-id="91f37-139">When an application is upgraded using Visual Studio, hello diff package is published automatically.</span></span> <span data-ttu-id="91f37-140">手動 hello toocreate 差異比對封裝的應用程式資訊清單中，與 hello 服務資訊清單必須加以更新，但只有變更的 hello 封裝應該包含在 hello 最終的應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="91f37-140">toocreate a diff package manually, hello application manifest, and hello service manifests must be updated, but only hello changed packages should be included in hello final application package.</span></span>

<span data-ttu-id="91f37-141">例如，讓我們開始 hello 下列應用程式 （為了便於了解所提供的版本號碼）：</span><span class="sxs-lookup"><span data-stu-id="91f37-141">For example, let's start with hello following application (version numbers provided for ease of understanding):</span></span>

```text
app1           1.0.0
  service1     1.0.0
    code       1.0.0
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

<span data-ttu-id="91f37-142">現在，假設您想要 tooupdate 只有 hello 程式碼封裝的 service1 使用差異比對封裝使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="91f37-142">Now, let's assume you wanted tooupdate only hello code package of service1 using a diff package using PowerShell.</span></span> <span data-ttu-id="91f37-143">現在，您更新的應用程式具有下列資料夾結構的 hello:</span><span class="sxs-lookup"><span data-stu-id="91f37-143">Now, your updated application has hello following folder structure:</span></span>

```text
app1           2.0.0      <-- new version
  service1     2.0.0      <-- new version
    code       2.0.0      <-- new version
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

<span data-ttu-id="91f37-144">在此情況下，您更新應用程式資訊清單 too2.0.0 hello 和 hello 服務 service1 tooreflect hello 程式碼封裝更新資訊清單。</span><span class="sxs-lookup"><span data-stu-id="91f37-144">In this case, you update hello application manifest too2.0.0, and hello service manifest for service1 tooreflect hello code package update.</span></span> <span data-ttu-id="91f37-145">應用程式套件的 hello 資料夾中會有下列結構的 hello:</span><span class="sxs-lookup"><span data-stu-id="91f37-145">hello folder for your application package would have hello following structure:</span></span>

```text
app1/
  service1/
    code/
```

## <a name="next-steps"></a><span data-ttu-id="91f37-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="91f37-146">Next steps</span></span>
<span data-ttu-id="91f37-147">[使用 Visual Studio 升級您的應用程式](service-fabric-application-upgrade-tutorial.md) 將引導您完成使用 Visual Studio 進行應用程式升級的步驟。</span><span class="sxs-lookup"><span data-stu-id="91f37-147">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>

<span data-ttu-id="91f37-148">[使用 PowerShell 升級您的應用程式](service-fabric-application-upgrade-tutorial-powershell.md) 將引導您完成使用 PowerShell 進行應用程式升級的步驟。</span><span class="sxs-lookup"><span data-stu-id="91f37-148">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>

<span data-ttu-id="91f37-149">使用 [升級參數](service-fabric-application-upgrade-parameters.md)來控制您應用程式的升級方式。</span><span class="sxs-lookup"><span data-stu-id="91f37-149">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>

<span data-ttu-id="91f37-150">讓應用程式升級相容所學習如何 toouse[資料序列化](service-fabric-application-upgrade-data-serialization.md)。</span><span class="sxs-lookup"><span data-stu-id="91f37-150">Make your application upgrades compatible by learning how toouse [Data Serialization](service-fabric-application-upgrade-data-serialization.md).</span></span>

<span data-ttu-id="91f37-151">藉由參考 toohello 步驟中的修正應用程式升級的一般問題[疑難排解應用程式升級](service-fabric-application-upgrade-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="91f37-151">Fix common problems in application upgrades by referring toohello steps in [Troubleshooting Application Upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>
