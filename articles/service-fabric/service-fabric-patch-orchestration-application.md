---
title: "aaaAzure Service Fabric 修補程式的協調流程的應用程式 |Microsoft 文件"
description: "應用程式 tooautomate 作業系統修補 Service Fabric 叢集上的系統。"
services: service-fabric
documentationcenter: .net
author: novino
manager: timlt
editor: 
ms.assetid: de7dacf5-4038-434a-a265-5d0de80a9b1d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/9/2017
ms.author: nachandr
ms.openlocfilehash: fbb89aa2ea418181ee908a01850178c113c462fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="patch-hello-windows-operating-system-in-your-service-fabric-cluster"></a><span data-ttu-id="e468b-103">修補程式 hello Service Fabric 叢集中的 Windows 作業系統</span><span class="sxs-lookup"><span data-stu-id="e468b-103">Patch hello Windows operating system in your Service Fabric cluster</span></span>

<span data-ttu-id="e468b-104">hello 修補程式的協調流程是 Azure Service Fabric 應用程式可自動化 azure Service Fabric 叢集，而不需要停機修補的作業系統。</span><span class="sxs-lookup"><span data-stu-id="e468b-104">hello patch orchestration application is an Azure Service Fabric application that automates operating system patching on a Service Fabric cluster on Azure without downtime.</span></span>

<span data-ttu-id="e468b-105">hello 修補程式的協調流程的應用程式提供 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="e468b-105">hello patch orchestration app provides hello following:</span></span>

- <span data-ttu-id="e468b-106">**自動化的作業系統更新安裝**。</span><span class="sxs-lookup"><span data-stu-id="e468b-106">**Automatic operating system update installation**.</span></span> <span data-ttu-id="e468b-107">會自動下載並安裝作業系統更新。</span><span class="sxs-lookup"><span data-stu-id="e468b-107">Operating system updates are automatically downloaded and installed.</span></span> <span data-ttu-id="e468b-108">會視需要重新啟動叢集節點，而不需要叢集停機。</span><span class="sxs-lookup"><span data-stu-id="e468b-108">Cluster nodes are rebooted as needed without cluster downtime.</span></span>

- <span data-ttu-id="e468b-109">**叢集感知的修補和健康情況整合**。</span><span class="sxs-lookup"><span data-stu-id="e468b-109">**Cluster-aware patching and health integration**.</span></span> <span data-ttu-id="e468b-110">同時套用更新，hello 修補程式的協調流程的應用程式會監視 hello hello 叢集節點健全狀況。</span><span class="sxs-lookup"><span data-stu-id="e468b-110">While applying updates, hello patch orchestration app monitors hello health of hello cluster nodes.</span></span> <span data-ttu-id="e468b-111">叢集節點一次只能升級一個節點，或一次升級一個網域。</span><span class="sxs-lookup"><span data-stu-id="e468b-111">Cluster nodes are upgraded one node at a time or one upgrade domain at a time.</span></span> <span data-ttu-id="e468b-112">如果因為 toohello 修補程序關閉 hello hello 叢集健全狀況，修補是停止的 tooprevent aggravating hello 問題。</span><span class="sxs-lookup"><span data-stu-id="e468b-112">If hello health of hello cluster goes down due toohello patching process, patching is stopped tooprevent aggravating hello problem.</span></span>

## <a name="internal-details-of-hello-app"></a><span data-ttu-id="e468b-113">內部的 hello 應用程式的詳細資料</span><span class="sxs-lookup"><span data-stu-id="e468b-113">Internal details of hello app</span></span>

<span data-ttu-id="e468b-114">hello 修補程式的協調流程的應用程式包含下列子元件的 hello:</span><span class="sxs-lookup"><span data-stu-id="e468b-114">hello patch orchestration app is composed of hello following subcomponents:</span></span>

- <span data-ttu-id="e468b-115">**協調器服務**︰是具狀態服務，負責：</span><span class="sxs-lookup"><span data-stu-id="e468b-115">**Coordinator Service**: This stateful service is responsible for:</span></span>
    - <span data-ttu-id="e468b-116">Hello 整個叢集上協調 Windows Update 作業 hello。</span><span class="sxs-lookup"><span data-stu-id="e468b-116">Coordinating hello Windows Update job on hello entire cluster.</span></span>
    - <span data-ttu-id="e468b-117">儲存已完成的 Windows 更新作業的 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="e468b-117">Storing hello result of completed Windows Update operations.</span></span>
- <span data-ttu-id="e468b-118">**節點代理程式服務**︰是無狀態服務，在所有 Service Fabric 叢集節點上執行。</span><span class="sxs-lookup"><span data-stu-id="e468b-118">**Node Agent Service**: This stateless service runs on all Service Fabric cluster nodes.</span></span> <span data-ttu-id="e468b-119">hello 服務負責：</span><span class="sxs-lookup"><span data-stu-id="e468b-119">hello service is responsible for:</span></span>
    - <span data-ttu-id="e468b-120">啟動載入 hello 節點代理程式 NTService。</span><span class="sxs-lookup"><span data-stu-id="e468b-120">Bootstrapping hello Node Agent NTService.</span></span>
    - <span data-ttu-id="e468b-121">監視 hello 節點代理程式 NTService。</span><span class="sxs-lookup"><span data-stu-id="e468b-121">Monitoring hello Node Agent NTService.</span></span>
- <span data-ttu-id="e468b-122">**節點代理程式 NTService**：在較高層級權限 (系統) 執行的 Windows NT 服務。</span><span class="sxs-lookup"><span data-stu-id="e468b-122">**Node Agent NTService**: This Windows NT service runs at a higher-level privilege (SYSTEM).</span></span> <span data-ttu-id="e468b-123">相反地，hello 節點代理程式服務，在 hello 協調器服務執行的較低層級權限 （網路服務）。</span><span class="sxs-lookup"><span data-stu-id="e468b-123">In contrast, hello Node Agent Service and hello Coordinator Service run at a lower-level privilege (NETWORK SERVICE).</span></span> <span data-ttu-id="e468b-124">hello 服務負責執行下列所有 hello 叢集節點上的 Windows Update 作業 hello:</span><span class="sxs-lookup"><span data-stu-id="e468b-124">hello service is responsible for performing hello following Windows Update jobs on all hello cluster nodes:</span></span>
    - <span data-ttu-id="e468b-125">停用自動 hello 節點上的 Windows Update。</span><span class="sxs-lookup"><span data-stu-id="e468b-125">Disabling automatic Windows Update on hello node.</span></span>
    - <span data-ttu-id="e468b-126">根據 toohello 原則 hello 使用者提供下載和安裝 Windows Update。</span><span class="sxs-lookup"><span data-stu-id="e468b-126">Downloading and installing Windows Update according toohello policy hello user has provided.</span></span>
    - <span data-ttu-id="e468b-127">重新啟動 hello 機器 post Windows Update 安裝。</span><span class="sxs-lookup"><span data-stu-id="e468b-127">Restarting hello machine post Windows Update installation.</span></span>
    - <span data-ttu-id="e468b-128">正在上傳 Windows 更新 toohello 協調器服務的 hello 的結果。</span><span class="sxs-lookup"><span data-stu-id="e468b-128">Uploading hello results of Windows updates toohello Coordinator Service.</span></span>
    - <span data-ttu-id="e468b-129">萬一耗盡所有重試之後作業還是失敗，就報告健康情況報告。</span><span class="sxs-lookup"><span data-stu-id="e468b-129">Reporting health reports in case an operation has failed after exhausting all retries.</span></span>

> [!NOTE]
> <span data-ttu-id="e468b-130">hello 修補程式的協調流程的應用程式會使用 hello Service Fabric 修復管理員系統服務 toodisable 或啟用 hello 節點，執行健全狀況檢查。</span><span class="sxs-lookup"><span data-stu-id="e468b-130">hello patch orchestration app uses hello Service Fabric repair manager system service toodisable or enable hello node and perform health checks.</span></span> <span data-ttu-id="e468b-131">hello 修補程式的協調流程應用程式追蹤 hello Windows Update 進行每個節點所建立的 hello 修復工作。</span><span class="sxs-lookup"><span data-stu-id="e468b-131">hello repair task created by hello patch orchestration app tracks hello Windows Update progress for each node.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e468b-132">必要條件</span><span class="sxs-lookup"><span data-stu-id="e468b-132">Prerequisites</span></span>

### <a name="minimum-supported-service-fabric-runtime-version"></a><span data-ttu-id="e468b-133">支援的最低 Service Fabric 執行階段版本</span><span class="sxs-lookup"><span data-stu-id="e468b-133">Minimum supported Service Fabric runtime version</span></span>

#### <a name="azure-clusters"></a><span data-ttu-id="e468b-134">Azure 叢集</span><span class="sxs-lookup"><span data-stu-id="e468b-134">Azure clusters</span></span>
<span data-ttu-id="e468b-135">hello 修補程式的協調流程的應用程式必須具有 Service Fabric 執行階段版本 v5.5 的 Azure 叢集上執行或更新版本。</span><span class="sxs-lookup"><span data-stu-id="e468b-135">hello patch orchestration app must be run on Azure clusters that have Service Fabric runtime version v5.5 or later.</span></span>

#### <a name="standalone-on-premises-clusters"></a><span data-ttu-id="e468b-136">獨立的內部部署叢集</span><span class="sxs-lookup"><span data-stu-id="e468b-136">Standalone on-premises Clusters</span></span>
<span data-ttu-id="e468b-137">hello 修補程式的協調流程的應用程式必須具有 Service Fabric 執行階段版本 v5.6 獨立式叢集上執行或更新版本。</span><span class="sxs-lookup"><span data-stu-id="e468b-137">hello patch orchestration app must be run on Standalone clusters that have Service Fabric runtime version v5.6 or later.</span></span>

### <a name="enable-hello-repair-manager-service-if-its-not-running-already"></a><span data-ttu-id="e468b-138">啟用 hello 修復管理員服務 （如果它不已執行）</span><span class="sxs-lookup"><span data-stu-id="e468b-138">Enable hello repair manager service (if it's not running already)</span></span>

<span data-ttu-id="e468b-139">hello 修補程式的協調流程的應用程式需要 hello 修復管理員系統服務 toobe hello 叢集上啟用。</span><span class="sxs-lookup"><span data-stu-id="e468b-139">hello patch orchestration app requires hello repair manager system service toobe enabled on hello cluster.</span></span>

#### <a name="azure-clusters"></a><span data-ttu-id="e468b-140">Azure 叢集</span><span class="sxs-lookup"><span data-stu-id="e468b-140">Azure clusters</span></span>

<span data-ttu-id="e468b-141">Hello 銀級持久性層中的 azure 叢集都有 hello 修復管理員服務預設會啟用。</span><span class="sxs-lookup"><span data-stu-id="e468b-141">Azure clusters in hello silver durability tier have hello repair manager service enabled by default.</span></span> <span data-ttu-id="e468b-142">Hello 金級持久性層中的 azure 叢集可能會或可能沒有啟用，根據這些叢集建立時的 hello 修復管理員服務。</span><span class="sxs-lookup"><span data-stu-id="e468b-142">Azure clusters in hello gold durability tier might or might not have hello repair manager service enabled, depending on when those clusters were created.</span></span> <span data-ttu-id="e468b-143">在 hello 銅持久性層中，依預設，azure 的叢集沒有 hello 修復管理員服務已啟用。</span><span class="sxs-lookup"><span data-stu-id="e468b-143">Azure clusters in hello bronze durability tier, by default, do not have hello repair manager service enabled.</span></span> <span data-ttu-id="e468b-144">如果已啟用 hello 服務，您可以看到在 hello Service Fabric 總管 hello 系統服務 區段中執行它。</span><span class="sxs-lookup"><span data-stu-id="e468b-144">If hello service is already enabled, you can see it running in hello system services section in hello Service Fabric Explorer.</span></span>

##### <a name="azure-portal"></a><span data-ttu-id="e468b-145">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="e468b-145">Azure portal</span></span>
<span data-ttu-id="e468b-146">您可以設定叢集的 hello 次啟用修復管理員從 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="e468b-146">You can enable repair manager from Azure portal at hello time of setting up of cluster.</span></span> <span data-ttu-id="e468b-147">選取`Include Repair Manager`選項在`Add on features`在叢集組態的 hello 階段。</span><span class="sxs-lookup"><span data-stu-id="e468b-147">Select `Include Repair Manager` option under `Add on features` at hello time of Cluster configuration.</span></span>
<span data-ttu-id="e468b-148">![從 Azure 入口網站啟用修復管理員的映像](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)</span><span class="sxs-lookup"><span data-stu-id="e468b-148">![Image of Enabling Repair Manager from Azure portal](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)</span></span>

##### <a name="azure-resource-manager-template"></a><span data-ttu-id="e468b-149">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="e468b-149">Azure Resource Manager template</span></span>
<span data-ttu-id="e468b-150">或者，您可以使用 hello [Azure Resource Manager 範本](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm)tooenable hello 修復管理員服務在新的和現有的 Service Fabric 叢集上。</span><span class="sxs-lookup"><span data-stu-id="e468b-150">Alternatively you can use hello [Azure Resource Manager template](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) tooenable hello repair manager service on new and existing Service Fabric clusters.</span></span> <span data-ttu-id="e468b-151">您想 toodeploy hello 叢集取得 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="e468b-151">Get hello template for hello cluster that you want toodeploy.</span></span> <span data-ttu-id="e468b-152">您可以使用 hello 範例範本，或建立自訂的資源管理員範本。</span><span class="sxs-lookup"><span data-stu-id="e468b-152">You can either use hello sample templates or create a custom Resource Manager template.</span></span> 

<span data-ttu-id="e468b-153">tooenable hello 修復管理員服務使用[Azure Resource Manager 範本](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):</span><span class="sxs-lookup"><span data-stu-id="e468b-153">tooenable hello repair manager service using [Azure Resource Manager template](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):</span></span>

1. <span data-ttu-id="e468b-154">先檢查該 hello`apiversion`設定得`2017-07-01-preview`hello`Microsoft.ServiceFabric/clusters`資源，如下列程式碼片段的 hello 中所示。</span><span class="sxs-lookup"><span data-stu-id="e468b-154">First check that hello `apiversion` is set too`2017-07-01-preview` for hello `Microsoft.ServiceFabric/clusters` resource, as shown in hello following snippet.</span></span> <span data-ttu-id="e468b-155">如果不同，則您需要 tooupdate hello `apiVersion` toohello 值`2017-07-01-preview`:</span><span class="sxs-lookup"><span data-stu-id="e468b-155">If it is different, then you need tooupdate hello `apiVersion` toohello value `2017-07-01-preview`:</span></span>

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. <span data-ttu-id="e468b-156">現在加入 hello 下列啟用 hello 修復管理員服務`addonFeatures`後面 hello 區段`fabricSettings`> 一節：</span><span class="sxs-lookup"><span data-stu-id="e468b-156">Now enable hello repair manager service by adding hello following `addonFeatures` section after hello `fabricSettings` section:</span></span>

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. <span data-ttu-id="e468b-157">您已更新您叢集的範本，這些變更之後，套用它們，並讓 hello 升級完成。</span><span class="sxs-lookup"><span data-stu-id="e468b-157">After you have updated your cluster template with these changes, apply them and let hello upgrade finish.</span></span> <span data-ttu-id="e468b-158">您現在可以看到您的叢集中執行 hello 修復管理員系統服務。</span><span class="sxs-lookup"><span data-stu-id="e468b-158">You can now see hello repair manager system service running in your cluster.</span></span> <span data-ttu-id="e468b-159">它會呼叫`fabric:/System/RepairManagerService`hello Service Fabric 總管在 hello 系統服務 區段中。</span><span class="sxs-lookup"><span data-stu-id="e468b-159">It is called `fabric:/System/RepairManagerService` in hello system services section in hello Service Fabric Explorer.</span></span> 

### <a name="standalone-on-premises-clusters"></a><span data-ttu-id="e468b-160">獨立的內部部署叢集</span><span class="sxs-lookup"><span data-stu-id="e468b-160">Standalone on-premises clusters</span></span>

<span data-ttu-id="e468b-161">您可以使用 hello[獨立 Windows 叢集的組態設定](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest)tooenable hello 修復管理員服務在新的和現有的 Service Fabric 叢集上。</span><span class="sxs-lookup"><span data-stu-id="e468b-161">You can use hello [Configuration settings for standalone Windows cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) tooenable hello repair manager service on new and existing Service Fabric cluster.</span></span>

<span data-ttu-id="e468b-162">tooenable hello 修復管理員服務：</span><span class="sxs-lookup"><span data-stu-id="e468b-162">tooenable hello repair manager service:</span></span>

1. <span data-ttu-id="e468b-163">先檢查該 hello`apiversion`中[一般的叢集設定](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations)設定得`04-2017`或更高版本：</span><span class="sxs-lookup"><span data-stu-id="e468b-163">First check that hello `apiversion` in [General cluster configurations](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) is set too`04-2017` or higher:</span></span>

    ```json
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "04-2017",
        ...
    }
    ```

2. <span data-ttu-id="e468b-164">現在加入 hello 下列啟用修復管理員服務`addonFeaturres`後面 hello 區段`fabricSettings`區段如下所示：</span><span class="sxs-lookup"><span data-stu-id="e468b-164">Now enable repair manager service by adding hello following `addonFeaturres` section after hello `fabricSettings` section as shown below:</span></span>

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. <span data-ttu-id="e468b-165">更新您的叢集資訊清單，這些變更，使用更新的 hello 叢集資訊清單[建立新的叢集](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server)或[升級 hello 叢集設定](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration)。</span><span class="sxs-lookup"><span data-stu-id="e468b-165">Update your cluster manifest with these changes, using hello updated cluster manifest [create a new cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) or [upgrade hello cluster configuration](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration).</span></span> <span data-ttu-id="e468b-166">一旦 hello 叢集正在執行以更新的叢集資訊清單中，您現在可以看到執行中叢集，也就所謂的 hello 修復管理員系統服務`fabric:/System/RepairManagerService`下系統服務在 hello Service Fabric 總管 中的區段。</span><span class="sxs-lookup"><span data-stu-id="e468b-166">Once hello cluster is running with updated cluster manifest, you can now see hello repair manager system service running in your cluster, which is called `fabric:/System/RepairManagerService`, under system services section in hello Service Fabric explorer.</span></span>

### <a name="disable-automatic-windows-update-on-all-nodes"></a><span data-ttu-id="e468b-167">停用所有節點上的自動 Windows Update</span><span class="sxs-lookup"><span data-stu-id="e468b-167">Disable automatic Windows Update on all nodes</span></span>

<span data-ttu-id="e468b-168">Windows update 自動更新可能會導致 tooavailability 遺失，因為多個叢集節點可以重新啟動 hello 相同的時間。</span><span class="sxs-lookup"><span data-stu-id="e468b-168">Automatic Windows updates might lead tooavailability loss because multiple cluster nodes can restart at hello same time.</span></span> <span data-ttu-id="e468b-169">hello 修補程式的協調流程的應用程式，根據預設，會嘗試 toodisable hello 自動的 Windows Update，每個叢集節點上。</span><span class="sxs-lookup"><span data-stu-id="e468b-169">hello patch orchestration app, by default, tries toodisable hello automatic Windows Update on each cluster node.</span></span> <span data-ttu-id="e468b-170">不過，如果 hello 設定由系統管理員 」 或 「 群組原則管理，我們建議設定 hello 原則太"之前通知使用者下載 「 明確的 Windows Update。</span><span class="sxs-lookup"><span data-stu-id="e468b-170">However, if hello settings are managed by an administrator or group policy, we recommend setting hello Windows Update policy too“Notify before Download” explicitly.</span></span>

### <a name="optional-enable-azure-diagnostics"></a><span data-ttu-id="e468b-171">選擇性：啟用 Azure 診斷</span><span class="sxs-lookup"><span data-stu-id="e468b-171">Optional: Enable Azure Diagnostics</span></span>

<span data-ttu-id="e468b-172">執行 Service Fabric 執行階段版本 `5.6.220.9494` 和以上版本的叢集，會收集修補程式協調流程應用程式記錄作為 Service Fabric 記錄的一部分。</span><span class="sxs-lookup"><span data-stu-id="e468b-172">Clusters running Service Fabric runtime version `5.6.220.9494` and above collect patch orchestration app logs as part of Service Fabric logs.</span></span>
<span data-ttu-id="e468b-173">如果您的叢集是在 Service Fabric 執行階段 `5.6.220.9494` 版和以上版本執行，您可以略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="e468b-173">You can skip this step if your cluster is running on Service Fabric runtime version `5.6.220.9494` and above.</span></span>

<span data-ttu-id="e468b-174">叢集執行 Service Fabric 執行階段版本小於`5.6.220.9494`，記錄檔中的 hello 修補程式的協調流程的應用程式會在本機收集每個 hello 叢集節點上。</span><span class="sxs-lookup"><span data-stu-id="e468b-174">For clusters running Service Fabric runtime version less than `5.6.220.9494`, logs for hello patch orchestration app are collected locally on each of hello cluster nodes.</span></span>
<span data-ttu-id="e468b-175">我們建議您設定 Azure 診斷 tooupload 記錄檔，從所有節點 tooa 中央位置。</span><span class="sxs-lookup"><span data-stu-id="e468b-175">We recommend that you configure Azure Diagnostics tooupload logs from all nodes tooa central location.</span></span>

<span data-ttu-id="e468b-176">如需啟用 Azure 診斷的詳細資訊，請參閱[使用 Azure 診斷收集記錄](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad)。</span><span class="sxs-lookup"><span data-stu-id="e468b-176">For information on enabling Azure Diagnostics, see [Collect logs by using Azure Diagnostics](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).</span></span>

<span data-ttu-id="e468b-177">下列固定的提供者識別碼 hello 上產生記錄檔中的 hello 修補程式的協調流程的應用程式：</span><span class="sxs-lookup"><span data-stu-id="e468b-177">Logs for hello patch orchestration app are generated on hello following fixed provider IDs:</span></span>

- <span data-ttu-id="e468b-178">e39b723c-590c-4090-abb0-11e3e6616346</span><span class="sxs-lookup"><span data-stu-id="e468b-178">e39b723c-590c-4090-abb0-11e3e6616346</span></span>
- <span data-ttu-id="e468b-179">fc0028ff-bfdc-499f-80dc-ed922c52c5e9</span><span class="sxs-lookup"><span data-stu-id="e468b-179">fc0028ff-bfdc-499f-80dc-ed922c52c5e9</span></span>
- <span data-ttu-id="e468b-180">24afa313-0d3b-4c7c-b485-1047fd964b60</span><span class="sxs-lookup"><span data-stu-id="e468b-180">24afa313-0d3b-4c7c-b485-1047fd964b60</span></span>
- <span data-ttu-id="e468b-181">05dc046c-60e9-4ef7-965e-91660adffa68</span><span class="sxs-lookup"><span data-stu-id="e468b-181">05dc046c-60e9-4ef7-965e-91660adffa68</span></span>

<span data-ttu-id="e468b-182">在資源管理員範本 goto`EtwEventSourceProviderConfiguration`區段`WadCfg`並加入下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="e468b-182">In Resource Manager template goto `EtwEventSourceProviderConfiguration` section under `WadCfg` and add hello following entries:</span></span>

```json
  {
    "provider": "e39b723c-590c-4090-abb0-11e3e6616346",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
      "eventDestination": "PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "fc0028ff-bfdc-499f-80dc-ed922c52c5e9",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "24afa313-0d3b-4c7c-b485-1047fd964b60",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "05dc046c-60e9-4ef7-965e-91660adffa68",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  }
```

> [!NOTE]
> <span data-ttu-id="e468b-183">如果您的 Service Fabric 叢集具有多個節點型別，則必須為所有 hello 新增 hello 上一節`WadCfg`區段。</span><span class="sxs-lookup"><span data-stu-id="e468b-183">If your Service Fabric cluster has multiple node types, then hello previous section must be added for all hello `WadCfg` sections.</span></span>

## <a name="download-hello-app-package"></a><span data-ttu-id="e468b-184">下載 hello 應用程式套件</span><span class="sxs-lookup"><span data-stu-id="e468b-184">Download hello app package</span></span>

<span data-ttu-id="e468b-185">下載 hello 應用程式從 hello[下載連結](https://go.microsoft.com/fwlink/P/?linkid=849590)。</span><span class="sxs-lookup"><span data-stu-id="e468b-185">Download hello application from hello [download link](https://go.microsoft.com/fwlink/P/?linkid=849590).</span></span>

## <a name="configure-hello-app"></a><span data-ttu-id="e468b-186">Hello 應用程式設定</span><span class="sxs-lookup"><span data-stu-id="e468b-186">Configure hello app</span></span>

<span data-ttu-id="e468b-187">hello hello 修補程式的協調流程的應用程式的行為可以是您的需求設定的 toomeet。</span><span class="sxs-lookup"><span data-stu-id="e468b-187">hello behavior of hello patch orchestration app can be configured toomeet your needs.</span></span> <span data-ttu-id="e468b-188">在應用程式的建立或更新期間傳入 hello 應用程式參數來覆寫 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="e468b-188">Override hello default values by passing in hello application parameter during application creation or update.</span></span> <span data-ttu-id="e468b-189">可以藉由指定提供應用程式參數`ApplicationParameter`toohello`Start-ServiceFabricApplicationUpgrade`或`New-ServiceFabricApplication`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="e468b-189">Application parameters can be provided by specifying `ApplicationParameter` toohello `Start-ServiceFabricApplicationUpgrade` or `New-ServiceFabricApplication` cmdlets.</span></span>

|<span data-ttu-id="e468b-190">**參數**</span><span class="sxs-lookup"><span data-stu-id="e468b-190">**Parameter**</span></span>        |<span data-ttu-id="e468b-191">**類型**</span><span class="sxs-lookup"><span data-stu-id="e468b-191">**Type**</span></span>                          | <span data-ttu-id="e468b-192">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="e468b-192">**Details**</span></span>|
|:-|-|-|
|<span data-ttu-id="e468b-193">MaxResultsToCache</span><span class="sxs-lookup"><span data-stu-id="e468b-193">MaxResultsToCache</span></span>    |<span data-ttu-id="e468b-194">long</span><span class="sxs-lookup"><span data-stu-id="e468b-194">Long</span></span>                              | <span data-ttu-id="e468b-195">Windows Update 結果的最大數目，應加以快取。</span><span class="sxs-lookup"><span data-stu-id="e468b-195">Maximum number of Windows Update results, which should be cached.</span></span> <br><span data-ttu-id="e468b-196">預設值為 3000，是基於以下假設：</span><span class="sxs-lookup"><span data-stu-id="e468b-196">Default value is 3000 assuming the:</span></span> <br> <span data-ttu-id="e468b-197">- 節點數目 20。</span><span class="sxs-lookup"><span data-stu-id="e468b-197">- Number of nodes is 20.</span></span> <br> <span data-ttu-id="e468b-198">- 每個月在節點上發生的更新數目為 5。</span><span class="sxs-lookup"><span data-stu-id="e468b-198">- Number of updates happening on a node per month is five.</span></span> <br> <span data-ttu-id="e468b-199">- 每個作業的結果數目可為 10。</span><span class="sxs-lookup"><span data-stu-id="e468b-199">- Number of results per operation can be 10.</span></span> <br> <span data-ttu-id="e468b-200">要儲存結果的 hello 過去三個月。</span><span class="sxs-lookup"><span data-stu-id="e468b-200">- Results for hello past three months should be stored.</span></span> |
|<span data-ttu-id="e468b-201">TaskApprovalPolicy</span><span class="sxs-lookup"><span data-stu-id="e468b-201">TaskApprovalPolicy</span></span>   |<span data-ttu-id="e468b-202">例舉</span><span class="sxs-lookup"><span data-stu-id="e468b-202">Enum</span></span> <br> <span data-ttu-id="e468b-203">{ NodeWise, UpgradeDomainWise }</span><span class="sxs-lookup"><span data-stu-id="e468b-203">{ NodeWise, UpgradeDomainWise }</span></span>                          |<span data-ttu-id="e468b-204">TaskApprovalPolicy 指出是 toobe hello Service Fabric 叢集節點之間 hello 協調器服務 tooinstall Windows 更新所使用的 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="e468b-204">TaskApprovalPolicy indicates hello policy that is toobe used by hello Coordinator Service tooinstall Windows updates across hello Service Fabric cluster nodes.</span></span><br>                         <span data-ttu-id="e468b-205">允許的值包括：</span><span class="sxs-lookup"><span data-stu-id="e468b-205">Allowed values are:</span></span> <br>                                                           <span data-ttu-id="e468b-206"><b>NodeWise</b>。</span><span class="sxs-lookup"><span data-stu-id="e468b-206"><b>NodeWise</b>.</span></span> <span data-ttu-id="e468b-207">一次只會在一個節點上安裝 Windows Update。</span><span class="sxs-lookup"><span data-stu-id="e468b-207">Windows Update is installed one node at a time.</span></span> <br>                                                           <span data-ttu-id="e468b-208"><b>UpgradeDomainWise</b>。</span><span class="sxs-lookup"><span data-stu-id="e468b-208"><b>UpgradeDomainWise</b>.</span></span> <span data-ttu-id="e468b-209">一次只會在一個升級網域上安裝 Windows Update。</span><span class="sxs-lookup"><span data-stu-id="e468b-209">Windows Update is installed one upgrade domain at a time.</span></span> <span data-ttu-id="e468b-210">（在最大的 hello，所有屬於 tooan 升級網域的 hello 節點可以移 Windows update）。</span><span class="sxs-lookup"><span data-stu-id="e468b-210">(At hello maximum, all hello nodes belonging tooan upgrade domain can go for Windows Update.)</span></span>
|<span data-ttu-id="e468b-211">LogsDiskQuotaInMB</span><span class="sxs-lookup"><span data-stu-id="e468b-211">LogsDiskQuotaInMB</span></span>   |<span data-ttu-id="e468b-212">long</span><span class="sxs-lookup"><span data-stu-id="e468b-212">Long</span></span>  <br> <span data-ttu-id="e468b-213">(預設值︰1024)</span><span class="sxs-lookup"><span data-stu-id="e468b-213">(Default: 1024)</span></span>               |<span data-ttu-id="e468b-214">修補程式協調流程應用程式記錄的大小上限 (以 MB 為單位)，可在節點上本機保留。</span><span class="sxs-lookup"><span data-stu-id="e468b-214">Maximum size of patch orchestration app logs in MB, which can be persisted locally on nodes.</span></span>
| <span data-ttu-id="e468b-215">WUQuery</span><span class="sxs-lookup"><span data-stu-id="e468b-215">WUQuery</span></span>               | <span data-ttu-id="e468b-216">字串</span><span class="sxs-lookup"><span data-stu-id="e468b-216">string</span></span><br><span data-ttu-id="e468b-217">(預設值："IsInstalled=0")</span><span class="sxs-lookup"><span data-stu-id="e468b-217">(Default: "IsInstalled=0")</span></span>                | <span data-ttu-id="e468b-218">查詢 tooget Windows 更新。</span><span class="sxs-lookup"><span data-stu-id="e468b-218">Query tooget Windows updates.</span></span> <span data-ttu-id="e468b-219">如需詳細資訊，請參閱 [WuQuery](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx)。</span><span class="sxs-lookup"><span data-stu-id="e468b-219">For more information, see [WuQuery.](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx)</span></span>
| <span data-ttu-id="e468b-220">InstallWindowsOSOnlyUpdates</span><span class="sxs-lookup"><span data-stu-id="e468b-220">InstallWindowsOSOnlyUpdates</span></span> | <span data-ttu-id="e468b-221">Bool</span><span class="sxs-lookup"><span data-stu-id="e468b-221">Bool</span></span> <br> <span data-ttu-id="e468b-222">(預設值︰True)</span><span class="sxs-lookup"><span data-stu-id="e468b-222">(default: True)</span></span>                 | <span data-ttu-id="e468b-223">這個旗標可讓 Windows 作業系統安裝的系統更新 toobe。</span><span class="sxs-lookup"><span data-stu-id="e468b-223">This flag allows Windows operating system updates toobe installed.</span></span>            |
| <span data-ttu-id="e468b-224">WUOperationTimeOutInMinutes</span><span class="sxs-lookup"><span data-stu-id="e468b-224">WUOperationTimeOutInMinutes</span></span> | <span data-ttu-id="e468b-225">int</span><span class="sxs-lookup"><span data-stu-id="e468b-225">Int</span></span> <br><span data-ttu-id="e468b-226">(預設值︰90)</span><span class="sxs-lookup"><span data-stu-id="e468b-226">(Default: 90)</span></span>                   | <span data-ttu-id="e468b-227">指定 hello （搜尋或下載或安裝） 的任何 Windows Update 作業的逾時。</span><span class="sxs-lookup"><span data-stu-id="e468b-227">Specifies hello timeout for any Windows Update operation (search or download or install).</span></span> <span data-ttu-id="e468b-228">如果 hello 操作未完成內 hello 指定的逾時，它就會中止。</span><span class="sxs-lookup"><span data-stu-id="e468b-228">If hello operation is not completed within hello specified timeout, it is aborted.</span></span>       |
| <span data-ttu-id="e468b-229">WURescheduleCount</span><span class="sxs-lookup"><span data-stu-id="e468b-229">WURescheduleCount</span></span>     | <span data-ttu-id="e468b-230">int</span><span class="sxs-lookup"><span data-stu-id="e468b-230">Int</span></span> <br> <span data-ttu-id="e468b-231">(預設值︰5)</span><span class="sxs-lookup"><span data-stu-id="e468b-231">(Default: 5)</span></span>                  | <span data-ttu-id="e468b-232">hello 最大次數 hello 服務會重新排定 hello Windows update，如果操作持續失敗的作業。</span><span class="sxs-lookup"><span data-stu-id="e468b-232">hello maximum number of times hello service reschedules hello Windows update in case an operation fails persistently.</span></span>          |
| <span data-ttu-id="e468b-233">WURescheduleTimeInMinutes</span><span class="sxs-lookup"><span data-stu-id="e468b-233">WURescheduleTimeInMinutes</span></span> | <span data-ttu-id="e468b-234">int</span><span class="sxs-lookup"><span data-stu-id="e468b-234">Int</span></span> <br><span data-ttu-id="e468b-235">(預設值︰30)</span><span class="sxs-lookup"><span data-stu-id="e468b-235">(Default: 30)</span></span> | <span data-ttu-id="e468b-236">hello 間隔在哪一個 hello 服務會重新排定 hello Windows update，如果失敗持續發生。</span><span class="sxs-lookup"><span data-stu-id="e468b-236">hello interval at which hello service reschedules hello Windows update in case failure persists.</span></span> |
| <span data-ttu-id="e468b-237">WUFrequency</span><span class="sxs-lookup"><span data-stu-id="e468b-237">WUFrequency</span></span>           | <span data-ttu-id="e468b-238">以逗號分隔的字串 (預設值︰"Weekly, Wednesday, 7:00:00")</span><span class="sxs-lookup"><span data-stu-id="e468b-238">Comma-separated string (Default: "Weekly, Wednesday, 7:00:00")</span></span>     | <span data-ttu-id="e468b-239">安裝 Windows 更新的 hello 頻率。</span><span class="sxs-lookup"><span data-stu-id="e468b-239">hello frequency for installing Windows Update.</span></span> <span data-ttu-id="e468b-240">hello 格式和可能的值如下：</span><span class="sxs-lookup"><span data-stu-id="e468b-240">hello format and possible values are:</span></span> <br><span data-ttu-id="e468b-241">-   Monthly, DD,HH:MM:SS，例如 Monthly, 5,12:22:32。</span><span class="sxs-lookup"><span data-stu-id="e468b-241">-   Monthly, DD,HH:MM:SS, for example, Monthly, 5,12:22:32.</span></span> <br> <span data-ttu-id="e468b-242">-   Weekly, DAY,HH:MM:SS，例如 Weekly, Tuesday, 12:22:32。</span><span class="sxs-lookup"><span data-stu-id="e468b-242">-   Weekly, DAY,HH:MM:SS, for example, Weekly, Tuesday, 12:22:32.</span></span>  <br> <span data-ttu-id="e468b-243">-   Daily, HH:MM:SS，例如 Daily, 12:22:32。</span><span class="sxs-lookup"><span data-stu-id="e468b-243">-   Daily, HH:MM:SS, for example, Daily, 12:22:32.</span></span>  <br> <span data-ttu-id="e468b-244">-  None 表示不應該進行 Windows Update。</span><span class="sxs-lookup"><span data-stu-id="e468b-244">-  None indicates that Windows Update shouldn't be done.</span></span>  <br><br> <span data-ttu-id="e468b-245">請注意，所有的 hello 時間-utc 時區。</span><span class="sxs-lookup"><span data-stu-id="e468b-245">Note that all hello times are in UTC.</span></span>|
| <span data-ttu-id="e468b-246">AcceptWindowsUpdateEula</span><span class="sxs-lookup"><span data-stu-id="e468b-246">AcceptWindowsUpdateEula</span></span> | <span data-ttu-id="e468b-247">Bool</span><span class="sxs-lookup"><span data-stu-id="e468b-247">Bool</span></span> <br><span data-ttu-id="e468b-248">(預設值︰true)</span><span class="sxs-lookup"><span data-stu-id="e468b-248">(Default: true)</span></span> | <span data-ttu-id="e468b-249">藉由設定這個旗標，hello 應用程式會接受 hello 使用者授權合約的 Windows Update 代表 hello 的 hello 機器的擁有者。</span><span class="sxs-lookup"><span data-stu-id="e468b-249">By setting this flag, hello application accepts hello End-User License Agreement for Windows Update on behalf of hello owner of hello machine.</span></span>              |

> [!TIP]
> <span data-ttu-id="e468b-250">如果您想要 Windows Update toohappen 立即，設定`WUFrequency`相對 toohello 應用程式部署時間。</span><span class="sxs-lookup"><span data-stu-id="e468b-250">If you want Windows Update toohappen immediately, set `WUFrequency` relative toohello application deployment time.</span></span> <span data-ttu-id="e468b-251">例如，假設您有五個節點測試叢集和計劃 toodeploy hello 應用程式，在大約 5:00 PM UTC。</span><span class="sxs-lookup"><span data-stu-id="e468b-251">For example, suppose that you have a five-node test cluster and plan toodeploy hello app at around 5:00 PM UTC.</span></span> <span data-ttu-id="e468b-252">如果您假設 hello 應用程式升級或部署會在 30 分鐘 hello 最大值、 設定 hello WUFrequency 為 「 每日、 17:30:00。 」</span><span class="sxs-lookup"><span data-stu-id="e468b-252">If you assume that hello application upgrade or deployment takes 30 minutes at hello maximum, set hello WUFrequency as "Daily, 17:30:00."</span></span>

## <a name="deploy-hello-app"></a><span data-ttu-id="e468b-253">部署 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="e468b-253">Deploy hello app</span></span>

1. <span data-ttu-id="e468b-254">完成所有 hello 先決條件步驟 tooprepare hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="e468b-254">Finish all hello prerequisite steps tooprepare hello cluster.</span></span>
2. <span data-ttu-id="e468b-255">部署 hello 修補程式的協調流程應用程式，例如其他 Service Fabric 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e468b-255">Deploy hello patch orchestration app like any other Service Fabric app.</span></span> <span data-ttu-id="e468b-256">您可以使用 PowerShell 來部署 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e468b-256">You can deploy hello app by using PowerShell.</span></span> <span data-ttu-id="e468b-257">中的 hello 步驟[使用 PowerShell 部署和移除應用程式](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications)。</span><span class="sxs-lookup"><span data-stu-id="e468b-257">Follow hello steps in [Deploy and remove applications using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span></span>
3. <span data-ttu-id="e468b-258">tooconfigure hello 應用程式的部署，傳遞 hello hello 次`ApplicationParamater`toohello `New-ServiceFabricApplication` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="e468b-258">tooconfigure hello application at hello time of deployment, pass hello `ApplicationParamater` toohello `New-ServiceFabricApplication` cmdlet.</span></span> <span data-ttu-id="e468b-259">為了方便起見，我們提供了 hello 指令碼 Deploy.ps1 以及 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e468b-259">For your convenience, we’ve provided hello script Deploy.ps1 along with hello application.</span></span> <span data-ttu-id="e468b-260">toouse hello 指令碼：</span><span class="sxs-lookup"><span data-stu-id="e468b-260">toouse hello script:</span></span>

    - <span data-ttu-id="e468b-261">藉由連線 tooa Service Fabric 叢集`Connect-ServiceFabricCluster`。</span><span class="sxs-lookup"><span data-stu-id="e468b-261">Connect tooa Service Fabric cluster by using `Connect-ServiceFabricCluster`.</span></span>
    - <span data-ttu-id="e468b-262">執行含有適當 hello hello PowerShell 指令碼 Deploy.ps1`ApplicationParameter`值。</span><span class="sxs-lookup"><span data-stu-id="e468b-262">Execute hello PowerShell script Deploy.ps1 with hello appropriate `ApplicationParameter` value.</span></span>

> [!NOTE]
> <span data-ttu-id="e468b-263">Hello 中保留 hello 指令碼與 hello 應用程式資料夾 PatchOrchestrationApplication 相同的目錄。</span><span class="sxs-lookup"><span data-stu-id="e468b-263">Keep hello script and hello application folder PatchOrchestrationApplication in hello same directory.</span></span>

## <a name="upgrade-hello-app"></a><span data-ttu-id="e468b-264">升級 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="e468b-264">Upgrade hello app</span></span>

<span data-ttu-id="e468b-265">tooupgrade 現有修補程式的協調流程應用程式使用 PowerShell，請依照下列中的 hello 步驟[使用 PowerShell 的 Service Fabric 應用程式升級](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell)。</span><span class="sxs-lookup"><span data-stu-id="e468b-265">tooupgrade an existing patch orchestration app by using PowerShell, follow hello steps in [Service Fabric application upgrade using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).</span></span>

## <a name="remove-hello-app"></a><span data-ttu-id="e468b-266">移除 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="e468b-266">Remove hello app</span></span>

<span data-ttu-id="e468b-267">tooremove hello 應用程式，在後續的 hello 步驟[使用 PowerShell 部署和移除應用程式](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications)。</span><span class="sxs-lookup"><span data-stu-id="e468b-267">tooremove hello application, follow hello steps in [Deploy and remove applications using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span></span>

<span data-ttu-id="e468b-268">為了方便起見，我們提供了 hello 指令碼 Undeploy.ps1 以及 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e468b-268">For your convenience, we've provided hello script Undeploy.ps1 along with hello application.</span></span> <span data-ttu-id="e468b-269">toouse hello 指令碼：</span><span class="sxs-lookup"><span data-stu-id="e468b-269">toouse hello script:</span></span>

  - <span data-ttu-id="e468b-270">藉由連線 tooa Service Fabric 叢集```Connect-ServiceFabricCluster```。</span><span class="sxs-lookup"><span data-stu-id="e468b-270">Connect tooa Service Fabric cluster by using ```Connect-ServiceFabricCluster```.</span></span>

  - <span data-ttu-id="e468b-271">執行 PowerShell 指令碼 Undeploy.ps1 hello。</span><span class="sxs-lookup"><span data-stu-id="e468b-271">Execute hello PowerShell script Undeploy.ps1.</span></span>

> [!NOTE]
> <span data-ttu-id="e468b-272">Hello 中保留 hello 指令碼與 hello 應用程式資料夾 PatchOrchestrationApplication 相同的目錄。</span><span class="sxs-lookup"><span data-stu-id="e468b-272">Keep hello script and hello application folder PatchOrchestrationApplication in hello same directory.</span></span>

## <a name="view-hello-windows-update-results"></a><span data-ttu-id="e468b-273">檢視 hello Windows Update 結果</span><span class="sxs-lookup"><span data-stu-id="e468b-273">View hello Windows Update results</span></span>

<span data-ttu-id="e468b-274">hello 修補程式的協調流程的應用程式會公開 REST Api toodisplay hello 歷程記錄結果 toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="e468b-274">hello patch orchestration app exposes REST APIs toodisplay hello historical results toohello user.</span></span> <span data-ttu-id="e468b-275">Hello 結果 JSON 的範例：</span><span class="sxs-lookup"><span data-stu-id="e468b-275">An example of hello result JSON:</span></span>
```json
[
  {
    "NodeName": "_stg1vm_1",
    "WindowsUpdateOperationResults": [
      {
        "OperationResult": 0,
        "NodeName": "_stg1vm_1",
        "OperationTime": "2017-05-21T11:46:52.1953713Z",
        "UpdateDetails": [
          {
            "UpdateId": "7392acaf-6a85-427c-8a8d-058c25beb0d6",
            "Title": "Cumulative Security Update for Internet Explorer 11 for Windows Server 2012 R2 (KB3185319)",
            "Description": "A security issue has been identified in a Microsoft software product that could affect your system. You can help protect your system by installing this update from Microsoft. For a complete listing of hello issues that are included in this update, see hello associated Microsoft Knowledge Base article. After you install this update, you may have toorestart your system.",
            "ResultCode": 0
          }
        ],
        "OperationType": 1,
        "WindowsUpdateQuery": "IsInstalled=0",
        "WindowsUpdateFrequency": "Daily,10:00:00",
        "RebootRequired": false
      }
    ]
  },
  ...
]
```
<span data-ttu-id="e468b-276">如果沒有更新尚未排程，hello 結果 JSON 是空的。</span><span class="sxs-lookup"><span data-stu-id="e468b-276">If no update is scheduled yet, hello result JSON is empty.</span></span>

<span data-ttu-id="e468b-277">登入 toohello 叢集 tooquery Windows Update 的結果。</span><span class="sxs-lookup"><span data-stu-id="e468b-277">Log in toohello cluster tooquery Windows Update results.</span></span> <span data-ttu-id="e468b-278">找出 hello 主要的 hello 協調器服務的 hello 複本位址，然後叫用 hello 瀏覽器中的 hello URL: http://&lt;複本 IP&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1 /GetWindowsUpdateResults。</span><span class="sxs-lookup"><span data-stu-id="e468b-278">Then find out hello replica address for hello primary of hello Coordinator Service, and hit hello URL from hello browser: http://&lt;REPLICA-IP&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1/GetWindowsUpdateResults.</span></span>

<span data-ttu-id="e468b-279">hello hello 協調器服務的 REST 端點都有的動態連接埠。</span><span class="sxs-lookup"><span data-stu-id="e468b-279">hello REST endpoint for hello Coordinator Service has a dynamic port.</span></span> <span data-ttu-id="e468b-280">toocheck hello 正確 URL，請參閱 toohello Service Fabric 總管。</span><span class="sxs-lookup"><span data-stu-id="e468b-280">toocheck hello exact URL, refer toohello Service Fabric Explorer.</span></span> <span data-ttu-id="e468b-281">比方說，hello 結果位於`http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`。</span><span class="sxs-lookup"><span data-stu-id="e468b-281">For example, hello results are available at `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.</span></span>

![REST 端點的圖片](media/service-fabric-patch-orchestration-application/Rest_Endpoint.png)


<span data-ttu-id="e468b-283">如果 hello 反向 proxy 已啟用 hello 叢集上，您可以存取外部 hello 叢集中的 hello URL。</span><span class="sxs-lookup"><span data-stu-id="e468b-283">If hello reverse proxy is enabled on hello cluster, you can access hello URL from outside of hello cluster as well.</span></span>
<span data-ttu-id="e468b-284">hello 端點需要 toobe 叫用次數是 http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults。</span><span class="sxs-lookup"><span data-stu-id="e468b-284">hello endpoint that needs toobe hit is http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.</span></span>

<span data-ttu-id="e468b-285">tooenable hello 反向 proxy hello 在叢集上，請依照下列中的 hello 步驟[反向 proxy，在 Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy)。</span><span class="sxs-lookup"><span data-stu-id="e468b-285">tooenable hello reverse proxy on hello cluster, follow hello steps in [Reverse proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).</span></span> 

> 
> [!WARNING]
> <span data-ttu-id="e468b-286">Hello 反向 proxy 設定之後，所有微 hello 叢集中公開服務的 HTTP 端點都可以從 hello 叢集外定址。</span><span class="sxs-lookup"><span data-stu-id="e468b-286">After hello reverse proxy is configured, all micro services in hello cluster that expose an HTTP endpoint are addressable from outside hello cluster.</span></span>

## <a name="diagnosticshealth-events"></a><span data-ttu-id="e468b-287">診斷/健康情況事件</span><span class="sxs-lookup"><span data-stu-id="e468b-287">Diagnostics/health events</span></span>

### <a name="collect-patch-orchestration-app-logs"></a><span data-ttu-id="e468b-288">收集修補程式協調流程應用程式記錄</span><span class="sxs-lookup"><span data-stu-id="e468b-288">Collect patch orchestration app logs</span></span>

<span data-ttu-id="e468b-289">收集修補程式協調流程應用程式的記錄，是執行階段版本 `5.6.220.9494` 及以上版本作為 Service Fabric 記錄的一部分。</span><span class="sxs-lookup"><span data-stu-id="e468b-289">Patch orchestration app logs are collected as part of Service Fabric logs from runtime version `5.6.220.9494` and above.</span></span>
<span data-ttu-id="e468b-290">叢集執行 Service Fabric 執行階段版本小於`5.6.220.9494`，可以使用其中一種 hello 遵循方法收集記錄檔。</span><span class="sxs-lookup"><span data-stu-id="e468b-290">For clusters running Service Fabric runtime version less than `5.6.220.9494`, logs can be collected by using one of hello following methods.</span></span>

#### <a name="locally-on-each-node"></a><span data-ttu-id="e468b-291">本機的每個節點上</span><span class="sxs-lookup"><span data-stu-id="e468b-291">Locally on each node</span></span>

<span data-ttu-id="e468b-292">如果 Service Fabric 執行階段版本小於 `5.6.220.9494`，則只會在每個 Service Fabric 叢集節點的本機收集記錄。</span><span class="sxs-lookup"><span data-stu-id="e468b-292">Logs are collected locally on each Service Fabric cluster node if Service Fabric runtime version is less than `5.6.220.9494`.</span></span> <span data-ttu-id="e468b-293">hello 位置 tooaccess hello 記錄檔也\[Service Fabric\_安裝\_磁碟機\]:\\PatchOrchestrationApplication\\記錄檔。</span><span class="sxs-lookup"><span data-stu-id="e468b-293">hello location tooaccess hello logs is \[Service Fabric\_Installation\_Drive\]:\\PatchOrchestrationApplication\\logs.</span></span>

<span data-ttu-id="e468b-294">例如，如果 Service Fabric 安裝磁碟機 D 上，hello 路徑是 d:\\PatchOrchestrationApplication\\記錄檔。</span><span class="sxs-lookup"><span data-stu-id="e468b-294">For example, if Service Fabric is installed on drive D, hello path is D:\\PatchOrchestrationApplication\\logs.</span></span>

#### <a name="central-location"></a><span data-ttu-id="e468b-295">中央位置</span><span class="sxs-lookup"><span data-stu-id="e468b-295">Central location</span></span>

<span data-ttu-id="e468b-296">Azure 診斷設定先決條件步驟時，記錄檔中的 hello 修補程式的協調流程的應用程式可以使用 Azure 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="e468b-296">If Azure Diagnostics is configured as part of prerequisite steps, logs for hello patch orchestration app are available in Azure Storage.</span></span>

### <a name="health-reports"></a><span data-ttu-id="e468b-297">健康狀態報告</span><span class="sxs-lookup"><span data-stu-id="e468b-297">Health reports</span></span>

<span data-ttu-id="e468b-298">hello 修補程式的協調流程的應用程式也會將針對 hello 協調器服務或 hello 節點代理程式服務的健康情況報告發佈在下列情況下的 hello:</span><span class="sxs-lookup"><span data-stu-id="e468b-298">hello patch orchestration app also publishes health reports against hello Coordinator Service or hello Node Agent Service in hello following cases:</span></span>

#### <a name="a-windows-update-operation-failed"></a><span data-ttu-id="e468b-299">Windows Update 作業失敗</span><span class="sxs-lookup"><span data-stu-id="e468b-299">A Windows Update operation failed</span></span>

<span data-ttu-id="e468b-300">如果 Windows 更新作業失敗的節點上，健全狀況報表會產生針對 hello 節點代理程式服務。</span><span class="sxs-lookup"><span data-stu-id="e468b-300">If a Windows Update operation fails on a node, a health report is generated against hello Node Agent Service.</span></span> <span data-ttu-id="e468b-301">Hello 健全狀況報表的詳細資料包含 hello 有問題的節點名稱。</span><span class="sxs-lookup"><span data-stu-id="e468b-301">Details of hello health report contain hello problematic node name.</span></span>

<span data-ttu-id="e468b-302">修補 hello 有問題的節點上順利完成之後，就會自動清除 hello 報表。</span><span class="sxs-lookup"><span data-stu-id="e468b-302">After patching is successfully completed on hello problematic node, hello report is automatically cleared.</span></span>

#### <a name="hello-node-agent-ntservice-is-down"></a><span data-ttu-id="e468b-303">hello 節點代理程式 NTService 已關閉</span><span class="sxs-lookup"><span data-stu-id="e468b-303">hello Node Agent NTService is down</span></span>

<span data-ttu-id="e468b-304">如果 hello 節點代理程式 NTService 已關閉節點上，警告層級的健全狀況報表會產生針對 hello 節點代理程式服務。</span><span class="sxs-lookup"><span data-stu-id="e468b-304">If hello Node Agent NTService is down on a node, a warning-level health report is generated against hello Node Agent Service.</span></span>

#### <a name="hello-repair-manager-service-is-not-enabled"></a><span data-ttu-id="e468b-305">未啟用 hello 修復管理員服務</span><span class="sxs-lookup"><span data-stu-id="e468b-305">hello repair manager service is not enabled</span></span>

<span data-ttu-id="e468b-306">如果 hello 叢集上找不到 hello 修復管理員服務，hello 協調器服務會產生警告層級的健全狀況報表。</span><span class="sxs-lookup"><span data-stu-id="e468b-306">If hello repair manager service is not found on hello cluster, a warning-level health report is generated for hello Coordinator Service.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="e468b-307">常見問題集</span><span class="sxs-lookup"><span data-stu-id="e468b-307">Frequently asked questions</span></span>

<span data-ttu-id="e468b-308">問：</span><span class="sxs-lookup"><span data-stu-id="e468b-308">Q.</span></span> <span data-ttu-id="e468b-309">**為什麼 hello 修補程式的協調流程的應用程式執行時看到我的叢集處於錯誤狀態？**</span><span class="sxs-lookup"><span data-stu-id="e468b-309">**Why do I see my cluster in an error state when hello patch orchestration app is running?**</span></span>

<span data-ttu-id="e468b-310">A.</span><span class="sxs-lookup"><span data-stu-id="e468b-310">A.</span></span> <span data-ttu-id="e468b-311">在 hello 安裝過程中，hello 修補程式的協調流程的應用程式會停用或重新啟動節點，這可能會暫時導致停機的 hello 叢集 hello 健全狀況。</span><span class="sxs-lookup"><span data-stu-id="e468b-311">During hello installation process, hello patch orchestration app disables or restarts nodes, which can temporarily result in hello health of hello cluster going down.</span></span>

<span data-ttu-id="e468b-312">根據 hello 應用程式的 hello 原則，可能是一個節點可以向下修補作業期間*或*可以同時向下整個升級網域。</span><span class="sxs-lookup"><span data-stu-id="e468b-312">Based on hello policy for hello application, either one node can go down during a patching operation *or* an entire upgrade domain can go down simultaneously.</span></span>

<span data-ttu-id="e468b-313">Windows Update 安裝 hello hello 結束，重新啟動後的 hello 節點會重新啟用。</span><span class="sxs-lookup"><span data-stu-id="e468b-313">By hello end of hello Windows Update installation, hello nodes are reenabled post restart.</span></span>

<span data-ttu-id="e468b-314">在下列範例的 hello，hello 叢集發生 tooan 錯誤狀態暫時因為兩個節點已關閉，而且 hello MaxPercentageUnhealthNodes 原則違反了。</span><span class="sxs-lookup"><span data-stu-id="e468b-314">In hello following example, hello cluster went tooan error state temporarily because two nodes were down and hello MaxPercentageUnhealthNodes policy was violated.</span></span> <span data-ttu-id="e468b-315">hello 錯誤是暫時性的直到 hello 修補作業正在進行中。</span><span class="sxs-lookup"><span data-stu-id="e468b-315">hello error is temporary until hello patching operation is ongoing.</span></span>

![健康情況不良之叢集的圖片](media/service-fabric-patch-orchestration-application/MaxPercentage_causing_unhealthy_cluster.png)

<span data-ttu-id="e468b-317">如果 hello 問題持續發生，請參閱 toohello 疑難排解 > 一節。</span><span class="sxs-lookup"><span data-stu-id="e468b-317">If hello issue persists, refer toohello Troubleshooting section.</span></span>

<span data-ttu-id="e468b-318">問：</span><span class="sxs-lookup"><span data-stu-id="e468b-318">Q.</span></span> <span data-ttu-id="e468b-319">**修補程式協調流程應用程式處於警告狀態**</span><span class="sxs-lookup"><span data-stu-id="e468b-319">**Patch orchestration app is in warning state**</span></span>

<span data-ttu-id="e468b-320">A.</span><span class="sxs-lookup"><span data-stu-id="e468b-320">A.</span></span> <span data-ttu-id="e468b-321">請檢查 toosee，如果公佈針對 hello 應用程式的健康情況報告 hello 根本原因。</span><span class="sxs-lookup"><span data-stu-id="e468b-321">Check toosee if a health report posted against hello application is hello root cause.</span></span> <span data-ttu-id="e468b-322">通常，hello 警告包含 hello 問題的詳細的資料。</span><span class="sxs-lookup"><span data-stu-id="e468b-322">Usually, hello warning contains details of hello problem.</span></span> <span data-ttu-id="e468b-323">如果 hello 問題是暫時性的會在這個狀態中的預期的 tooauto 復原 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e468b-323">If hello issue is transient, hello application is expected tooauto-recover from this state.</span></span>

<span data-ttu-id="e468b-324">問：</span><span class="sxs-lookup"><span data-stu-id="e468b-324">Q.</span></span> <span data-ttu-id="e468b-325">**如果我的叢集狀況不良，我需要 toodo 緊急作業系統更新，我可以做什麼？**</span><span class="sxs-lookup"><span data-stu-id="e468b-325">**What can I do if my cluster is unhealthy and I need toodo an urgent operating system update?**</span></span>

<span data-ttu-id="e468b-326">A.</span><span class="sxs-lookup"><span data-stu-id="e468b-326">A.</span></span> <span data-ttu-id="e468b-327">hello 修補程式的協調流程的應用程式不會安裝更新時 hello 叢集狀況不良。</span><span class="sxs-lookup"><span data-stu-id="e468b-327">hello patch orchestration app does not install updates while hello cluster is unhealthy.</span></span> <span data-ttu-id="e468b-328">請嘗試 toobring 您叢集 tooa 狀況良好狀態 toounblock hello 修補程式的協調流程的應用程式的工作流程。</span><span class="sxs-lookup"><span data-stu-id="e468b-328">Try toobring your cluster tooa healthy state toounblock hello patch orchestration app workflow.</span></span>

<span data-ttu-id="e468b-329">問：</span><span class="sxs-lookup"><span data-stu-id="e468b-329">Q.</span></span> <span data-ttu-id="e468b-330">**為什麼沒有修補在叢集中這麼久 toorun？**</span><span class="sxs-lookup"><span data-stu-id="e468b-330">**Why does patching across clusters take so long toorun?**</span></span>

<span data-ttu-id="e468b-331">A.</span><span class="sxs-lookup"><span data-stu-id="e468b-331">A.</span></span> <span data-ttu-id="e468b-332">hello hello 修補程式的協調流程的應用程式所需的時間主要是取決於下列因素的 hello:</span><span class="sxs-lookup"><span data-stu-id="e468b-332">hello time needed by hello patch orchestration app is mostly dependent on hello following factors:</span></span>

- <span data-ttu-id="e468b-333">hello 原則 hello 協調器服務。</span><span class="sxs-lookup"><span data-stu-id="e468b-333">hello policy of hello Coordinator Service.</span></span> 
  - <span data-ttu-id="e468b-334">hello 預設原則`NodeWise`，導致修補一次只有一個節點。</span><span class="sxs-lookup"><span data-stu-id="e468b-334">hello default policy, `NodeWise`, results in patching only one node at a time.</span></span> <span data-ttu-id="e468b-335">特別是在較大叢集的 hello 案例中，我們建議您使用 hello`UpgradeDomainWise`原則 tooachieve 更快的修補程式的多個叢集。</span><span class="sxs-lookup"><span data-stu-id="e468b-335">Especially in hello case of bigger clusters, we recommend that you use hello `UpgradeDomainWise` policy tooachieve faster patching across clusters.</span></span>
- <span data-ttu-id="e468b-336">hello 可供下載和安裝的更新數目。</span><span class="sxs-lookup"><span data-stu-id="e468b-336">hello number of updates available for download and installation.</span></span> 
- <span data-ttu-id="e468b-337">hello toodownload 所需的平均時間，並安裝更新，不應超過幾個小時。</span><span class="sxs-lookup"><span data-stu-id="e468b-337">hello average time needed toodownload and install an update, which should not exceed a couple of hours.</span></span>
- <span data-ttu-id="e468b-338">hello hello VM 的效能和網路頻寬。</span><span class="sxs-lookup"><span data-stu-id="e468b-338">hello performance of hello VM and network bandwidth.</span></span>

<span data-ttu-id="e468b-339">問：</span><span class="sxs-lookup"><span data-stu-id="e468b-339">Q.</span></span> <span data-ttu-id="e468b-340">**為什麼看到某些更新 Windows Update 取得透過 REST api 的而非在 hello 機器上的 Windows Update 歷程記錄的結果中？**</span><span class="sxs-lookup"><span data-stu-id="e468b-340">**Why do I see some updates in Windows Update results obtained via REST api's, but not under hello Windows Update history on machine?**</span></span>

<span data-ttu-id="e468b-341">A.</span><span class="sxs-lookup"><span data-stu-id="e468b-341">A.</span></span> <span data-ttu-id="e468b-342">某些產品更新需要 toobe 簽入其各自的更新/修補歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="e468b-342">Some product updates need toobe checked in their respective update/patch history.</span></span> <span data-ttu-id="e468b-343">例如：Windows Defender 更新不會顯示在 Windows Server 2016 上的 Windows Update 歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="e468b-343">Eg: Windows Defender updates do not show up in Windows Update history on Windows Server 2016.</span></span>

## <a name="disclaimers"></a><span data-ttu-id="e468b-344">免責聲明</span><span class="sxs-lookup"><span data-stu-id="e468b-344">Disclaimers</span></span>

- <span data-ttu-id="e468b-345">hello 修補程式的協調流程的應用程式接受代表 hello 使用者 hello 使用者授權合約的 Windows Update。</span><span class="sxs-lookup"><span data-stu-id="e468b-345">hello patch orchestration app accepts hello End-User License Agreement of Windows Update on behalf of hello user.</span></span> <span data-ttu-id="e468b-346">（選擇性） hello 設定可以關閉 hello hello 應用程式組態中。</span><span class="sxs-lookup"><span data-stu-id="e468b-346">Optionally, hello setting can be turned off in hello configuration of hello application.</span></span>

- <span data-ttu-id="e468b-347">hello 修補程式的協調流程的應用程式會收集遙測 tootrack 使用量和效能。</span><span class="sxs-lookup"><span data-stu-id="e468b-347">hello patch orchestration app collects telemetry tootrack usage and performance.</span></span> <span data-ttu-id="e468b-348">hello 應用程式的遙測遵循 hello 設定 hello Service Fabric 執行階段的遙測設定 （預設為開啟）。</span><span class="sxs-lookup"><span data-stu-id="e468b-348">hello application’s telemetry follows hello setting of hello Service Fabric runtime’s telemetry setting (which is on by default).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="e468b-349">疑難排解</span><span class="sxs-lookup"><span data-stu-id="e468b-349">Troubleshooting</span></span>

### <a name="a-node-is-not-coming-back-tooup-state"></a><span data-ttu-id="e468b-350">節點不返回 tooup 狀態</span><span class="sxs-lookup"><span data-stu-id="e468b-350">A node is not coming back tooup state</span></span>

<span data-ttu-id="e468b-351">**hello 節點可能會卡在停用狀態，因為**:</span><span class="sxs-lookup"><span data-stu-id="e468b-351">**hello node might be stuck in a disabling state because**:</span></span>

<span data-ttu-id="e468b-352">安全性檢查擱置。</span><span class="sxs-lookup"><span data-stu-id="e468b-352">A safety check is pending.</span></span> <span data-ttu-id="e468b-353">tooremedy 這種情況下，確保足夠的節點，可在狀況良好的狀態。</span><span class="sxs-lookup"><span data-stu-id="e468b-353">tooremedy this situation, ensure that enough nodes are available in a healthy state.</span></span>

<span data-ttu-id="e468b-354">**hello 節點可能會卡在停用狀態，因為**:</span><span class="sxs-lookup"><span data-stu-id="e468b-354">**hello node might be stuck in a disabled state because**:</span></span>

- <span data-ttu-id="e468b-355">hello 節點已手動停用。</span><span class="sxs-lookup"><span data-stu-id="e468b-355">hello node was disabled manually.</span></span>
- <span data-ttu-id="e468b-356">hello 節點已停用，因為 tooan 持續的 Azure 基礎結構工作。</span><span class="sxs-lookup"><span data-stu-id="e468b-356">hello node was disabled due tooan ongoing Azure infrastructure job.</span></span>
- <span data-ttu-id="e468b-357">hello 節點已由 hello 修補程式的協調流程的應用程式 toopatch hello 節點暫時停用。</span><span class="sxs-lookup"><span data-stu-id="e468b-357">hello node was disabled temporarily by hello patch orchestration app toopatch hello node.</span></span>

<span data-ttu-id="e468b-358">**hello 節點可能會卡在關閉的狀態因為**:</span><span class="sxs-lookup"><span data-stu-id="e468b-358">**hello node might be stuck in a down state because**:</span></span>

- <span data-ttu-id="e468b-359">hello 節點以手動方式放入關閉狀態。</span><span class="sxs-lookup"><span data-stu-id="e468b-359">hello node was put in a down state manually.</span></span>
- <span data-ttu-id="e468b-360">hello 節點正在進行重新啟動 （這可能會觸發 hello 修補程式的協調流程的應用程式）。</span><span class="sxs-lookup"><span data-stu-id="e468b-360">hello node is undergoing a restart (which might be triggered by hello patch orchestration app).</span></span>
- <span data-ttu-id="e468b-361">hello 節點已關閉到期 tooa 故障 VM 或電腦或網路連線問題。</span><span class="sxs-lookup"><span data-stu-id="e468b-361">hello node is down due tooa faulty VM or machine or network connectivity issues.</span></span>

### <a name="updates-were-skipped-on-some-nodes"></a><span data-ttu-id="e468b-362">已略過某些節點上的更新</span><span class="sxs-lookup"><span data-stu-id="e468b-362">Updates were skipped on some nodes</span></span>

<span data-ttu-id="e468b-363">hello 修補程式的協調流程的應用程式會嘗試 tooinstall Windows update 相應 toohello 方法是重新排定原則。</span><span class="sxs-lookup"><span data-stu-id="e468b-363">hello patch orchestration app tries tooinstall a Windows update according toohello rescheduling policy.</span></span> <span data-ttu-id="e468b-364">hello 服務嘗試 toorecover hello 節點，並略過 hello 更新相應 toohello 應用程式原則。</span><span class="sxs-lookup"><span data-stu-id="e468b-364">hello service tries toorecover hello node and skip hello update according toohello application policy.</span></span>

<span data-ttu-id="e468b-365">在這種情況下，會產生針對 hello 節點代理程式服務的警告層級的健全狀況報表。</span><span class="sxs-lookup"><span data-stu-id="e468b-365">In such a case, a warning-level health report is generated against hello Node Agent Service.</span></span> <span data-ttu-id="e468b-366">Windows Update 的 hello 結果也會包含 hello 的 hello 失敗的可能原因。</span><span class="sxs-lookup"><span data-stu-id="e468b-366">hello result for Windows Update also contains hello possible reason for hello failure.</span></span>

### <a name="hello-health-of-hello-cluster-goes-tooerror-while-hello-update-installs"></a><span data-ttu-id="e468b-367">hello hello 叢集健全狀況 hello 更新安裝時，會 tooerror</span><span class="sxs-lookup"><span data-stu-id="e468b-367">hello health of hello cluster goes tooerror while hello update installs</span></span>

<span data-ttu-id="e468b-368">錯誤的 Windows update 可以關閉應用程式或叢集上的特定節點或升級網域的 hello 健全狀況。</span><span class="sxs-lookup"><span data-stu-id="e468b-368">A faulty Windows update can bring down hello health of an application or cluster on a particular node or upgrade domain.</span></span> <span data-ttu-id="e468b-369">hello 修補程式的協調流程的應用程式會停止任何後續的 Windows 更新作業，直到 hello 叢集恢復狀況良好。</span><span class="sxs-lookup"><span data-stu-id="e468b-369">hello patch orchestration app discontinues any subsequent Windows Update operation until hello cluster is healthy again.</span></span>

<span data-ttu-id="e468b-370">系統管理員必須介入，並判斷為什麼 hello 應用程式或叢集變成狀況不良的原因 tooWindows 更新。</span><span class="sxs-lookup"><span data-stu-id="e468b-370">An administrator must intervene and determine why hello application or cluster became unhealthy due tooWindows Update.</span></span>

## <a name="release-notes-"></a><span data-ttu-id="e468b-371">版本資訊：</span><span class="sxs-lookup"><span data-stu-id="e468b-371">Release Notes :</span></span>

### <a name="version-110"></a><span data-ttu-id="e468b-372">1.1.0 版</span><span class="sxs-lookup"><span data-stu-id="e468b-372">Version 1.1.0</span></span>
- <span data-ttu-id="e468b-373">公開版本</span><span class="sxs-lookup"><span data-stu-id="e468b-373">Public release</span></span>

### <a name="version-111"></a><span data-ttu-id="e468b-374">1.1.1 版</span><span class="sxs-lookup"><span data-stu-id="e468b-374">Version 1.1.1</span></span>
- <span data-ttu-id="e468b-375">修正 SetupEntryPoint of NodeAgentService 中的錯誤，該錯誤導致無法安裝 NodeAgentNTService。</span><span class="sxs-lookup"><span data-stu-id="e468b-375">Fixed a bug in SetupEntryPoint of NodeAgentService that prevented installation of NodeAgentNTService.</span></span>

### <a name="version-120-latest"></a><span data-ttu-id="e468b-376">1.2.0 版 (最新)</span><span class="sxs-lookup"><span data-stu-id="e468b-376">Version 1.2.0 (Latest)</span></span>

- <span data-ttu-id="e468b-377">關於系統重新啟動工作流程的錯誤修正。</span><span class="sxs-lookup"><span data-stu-id="e468b-377">Bug fixes around system restart workflow.</span></span>
- <span data-ttu-id="e468b-378">如預期般，未發生 RM 工作因為 toowhich 健全狀況檢查期間準備修復工作建立的 bug 修正。</span><span class="sxs-lookup"><span data-stu-id="e468b-378">Bug fix in creation of RM tasks due toowhich health check during preparing repair tasks wasn't happening as expected.</span></span>
- <span data-ttu-id="e468b-379">從 自動 toodelayed 自動的 windows 服務 POANodeSvc 變更的 hello 啟動模式。</span><span class="sxs-lookup"><span data-stu-id="e468b-379">Changed hello startup mode for windows service POANodeSvc from auto toodelayed-auto.</span></span>
