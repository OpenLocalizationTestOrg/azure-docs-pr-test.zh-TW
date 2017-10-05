---
title: "Azure Service Fabric 修補程式協調流程應用程式 | Microsoft Docs"
description: "在 Service Fabric 叢集上將作業系統修補自動化的應用程式。"
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
ms.openlocfilehash: 2c5842822e347113e388d570f6ae603a313944d6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="patch-the-windows-operating-system-in-your-service-fabric-cluster"></a><span data-ttu-id="ababa-103">修補 Service Fabric 叢集中的 Windows 作業系統</span><span class="sxs-lookup"><span data-stu-id="ababa-103">Patch the Windows operating system in your Service Fabric cluster</span></span>

<span data-ttu-id="ababa-104">修補程式協調流程應用程式是 Azure Service Fabric 應用程式，可在 Azure 的 Service Fabric 叢集上將作業系統修補自動化，而不需要停機。</span><span class="sxs-lookup"><span data-stu-id="ababa-104">The patch orchestration application is an Azure Service Fabric application that automates operating system patching on a Service Fabric cluster on Azure without downtime.</span></span>

<span data-ttu-id="ababa-105">修補程式協調流程應用程式提供下列功能：</span><span class="sxs-lookup"><span data-stu-id="ababa-105">The patch orchestration app provides the following:</span></span>

- <span data-ttu-id="ababa-106">**自動化的作業系統更新安裝**。</span><span class="sxs-lookup"><span data-stu-id="ababa-106">**Automatic operating system update installation**.</span></span> <span data-ttu-id="ababa-107">會自動下載並安裝作業系統更新。</span><span class="sxs-lookup"><span data-stu-id="ababa-107">Operating system updates are automatically downloaded and installed.</span></span> <span data-ttu-id="ababa-108">會視需要重新啟動叢集節點，而不需要叢集停機。</span><span class="sxs-lookup"><span data-stu-id="ababa-108">Cluster nodes are rebooted as needed without cluster downtime.</span></span>

- <span data-ttu-id="ababa-109">**叢集感知的修補和健康情況整合**。</span><span class="sxs-lookup"><span data-stu-id="ababa-109">**Cluster-aware patching and health integration**.</span></span> <span data-ttu-id="ababa-110">套用更新時，修補程式協調流程應用程式會監視叢集節點的健康情況。</span><span class="sxs-lookup"><span data-stu-id="ababa-110">While applying updates, the patch orchestration app monitors the health of the cluster nodes.</span></span> <span data-ttu-id="ababa-111">叢集節點一次只能升級一個節點，或一次升級一個網域。</span><span class="sxs-lookup"><span data-stu-id="ababa-111">Cluster nodes are upgraded one node at a time or one upgrade domain at a time.</span></span> <span data-ttu-id="ababa-112">如果因修補程序而造成叢集的健康情況下降，修補就會停止，防止問題繼續惡化。</span><span class="sxs-lookup"><span data-stu-id="ababa-112">If the health of the cluster goes down due to the patching process, patching is stopped to prevent aggravating the problem.</span></span>

## <a name="internal-details-of-the-app"></a><span data-ttu-id="ababa-113">應用程式的內部詳細資料</span><span class="sxs-lookup"><span data-stu-id="ababa-113">Internal details of the app</span></span>

<span data-ttu-id="ababa-114">修補程式協調流程應用程式包含下列子元件︰</span><span class="sxs-lookup"><span data-stu-id="ababa-114">The patch orchestration app is composed of the following subcomponents:</span></span>

- <span data-ttu-id="ababa-115">**協調器服務**︰是具狀態服務，負責：</span><span class="sxs-lookup"><span data-stu-id="ababa-115">**Coordinator Service**: This stateful service is responsible for:</span></span>
    - <span data-ttu-id="ababa-116">協調整個叢集上的 Windows Update 作業。</span><span class="sxs-lookup"><span data-stu-id="ababa-116">Coordinating the Windows Update job on the entire cluster.</span></span>
    - <span data-ttu-id="ababa-117">儲存已完成之 Windows Update 作業的結果。</span><span class="sxs-lookup"><span data-stu-id="ababa-117">Storing the result of completed Windows Update operations.</span></span>
- <span data-ttu-id="ababa-118">**節點代理程式服務**︰是無狀態服務，在所有 Service Fabric 叢集節點上執行。</span><span class="sxs-lookup"><span data-stu-id="ababa-118">**Node Agent Service**: This stateless service runs on all Service Fabric cluster nodes.</span></span> <span data-ttu-id="ababa-119">此服務負責：</span><span class="sxs-lookup"><span data-stu-id="ababa-119">The service is responsible for:</span></span>
    - <span data-ttu-id="ababa-120">啟動節點代理程式 NTService。</span><span class="sxs-lookup"><span data-stu-id="ababa-120">Bootstrapping the Node Agent NTService.</span></span>
    - <span data-ttu-id="ababa-121">監視節點代理程式 NTService。</span><span class="sxs-lookup"><span data-stu-id="ababa-121">Monitoring the Node Agent NTService.</span></span>
- <span data-ttu-id="ababa-122">**節點代理程式 NTService**：在較高層級權限 (系統) 執行的 Windows NT 服務。</span><span class="sxs-lookup"><span data-stu-id="ababa-122">**Node Agent NTService**: This Windows NT service runs at a higher-level privilege (SYSTEM).</span></span> <span data-ttu-id="ababa-123">相比之下，節點代理程式服務和協調器服務則是在較低層級權限 (網路服務) 執行。</span><span class="sxs-lookup"><span data-stu-id="ababa-123">In contrast, the Node Agent Service and the Coordinator Service run at a lower-level privilege (NETWORK SERVICE).</span></span> <span data-ttu-id="ababa-124">此服務會負責執行下列所有叢集節點上的 Windows Update 作業：</span><span class="sxs-lookup"><span data-stu-id="ababa-124">The service is responsible for performing the following Windows Update jobs on all the cluster nodes:</span></span>
    - <span data-ttu-id="ababa-125">將節點上的自動 Windows Update 停用。</span><span class="sxs-lookup"><span data-stu-id="ababa-125">Disabling automatic Windows Update on the node.</span></span>
    - <span data-ttu-id="ababa-126">根據使用者提供的原則下載並安裝 Windows Update。</span><span class="sxs-lookup"><span data-stu-id="ababa-126">Downloading and installing Windows Update according to the policy the user has provided.</span></span>
    - <span data-ttu-id="ababa-127">在 Windows Update 安裝後重新啟動機器。</span><span class="sxs-lookup"><span data-stu-id="ababa-127">Restarting the machine post Windows Update installation.</span></span>
    - <span data-ttu-id="ababa-128">將 Windows Update 的結果上傳至協調器服務。</span><span class="sxs-lookup"><span data-stu-id="ababa-128">Uploading the results of Windows updates to the Coordinator Service.</span></span>
    - <span data-ttu-id="ababa-129">萬一耗盡所有重試之後作業還是失敗，就報告健康情況報告。</span><span class="sxs-lookup"><span data-stu-id="ababa-129">Reporting health reports in case an operation has failed after exhausting all retries.</span></span>

> [!NOTE]
> <span data-ttu-id="ababa-130">修補程式協調流程應用程式是使用 Service Fabric 的修復管理器系統服務，將節點停用或啟用以及執行健康情況檢查。</span><span class="sxs-lookup"><span data-stu-id="ababa-130">The patch orchestration app uses the Service Fabric repair manager system service to disable or enable the node and perform health checks.</span></span> <span data-ttu-id="ababa-131">修補程式協調流程應用程式所建立的修復工作會追蹤每個節點的 Windows Update 進度。</span><span class="sxs-lookup"><span data-stu-id="ababa-131">The repair task created by the patch orchestration app tracks the Windows Update progress for each node.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ababa-132">必要條件</span><span class="sxs-lookup"><span data-stu-id="ababa-132">Prerequisites</span></span>

### <a name="minimum-supported-service-fabric-runtime-version"></a><span data-ttu-id="ababa-133">支援的最低 Service Fabric 執行階段版本</span><span class="sxs-lookup"><span data-stu-id="ababa-133">Minimum supported Service Fabric runtime version</span></span>

#### <a name="azure-clusters"></a><span data-ttu-id="ababa-134">Azure 叢集</span><span class="sxs-lookup"><span data-stu-id="ababa-134">Azure clusters</span></span>
<span data-ttu-id="ababa-135">修補程式協調流程應用程式必須在具有 Service Fabric 執行階段 5.5 版或更新版本的 Azure 叢集上執行。</span><span class="sxs-lookup"><span data-stu-id="ababa-135">The patch orchestration app must be run on Azure clusters that have Service Fabric runtime version v5.5 or later.</span></span>

#### <a name="standalone-on-premises-clusters"></a><span data-ttu-id="ababa-136">獨立的內部部署叢集</span><span class="sxs-lookup"><span data-stu-id="ababa-136">Standalone on-premises Clusters</span></span>
<span data-ttu-id="ababa-137">修補程式協調流程應用程式必須在具有 Service Fabric 執行階段 5.6 版或更新版本的獨立叢集上執行。</span><span class="sxs-lookup"><span data-stu-id="ababa-137">The patch orchestration app must be run on Standalone clusters that have Service Fabric runtime version v5.6 or later.</span></span>

### <a name="enable-the-repair-manager-service-if-its-not-running-already"></a><span data-ttu-id="ababa-138">啟用修復管理器服務 (如果尚未執行中)</span><span class="sxs-lookup"><span data-stu-id="ababa-138">Enable the repair manager service (if it's not running already)</span></span>

<span data-ttu-id="ababa-139">叢集必須啟用修復管理器系統服務，修補程式協調流程應用程式才能執行。</span><span class="sxs-lookup"><span data-stu-id="ababa-139">The patch orchestration app requires the repair manager system service to be enabled on the cluster.</span></span>

#### <a name="azure-clusters"></a><span data-ttu-id="ababa-140">Azure 叢集</span><span class="sxs-lookup"><span data-stu-id="ababa-140">Azure clusters</span></span>

<span data-ttu-id="ababa-141">銀級耐久性層中的 Azure 叢集依預設會啟用修復管理器。</span><span class="sxs-lookup"><span data-stu-id="ababa-141">Azure clusters in the silver durability tier have the repair manager service enabled by default.</span></span> <span data-ttu-id="ababa-142">金級耐久性層中的 Azure 叢集可能會或也可能不會啟用修復管理器，取決於這些叢集的建立時間。</span><span class="sxs-lookup"><span data-stu-id="ababa-142">Azure clusters in the gold durability tier might or might not have the repair manager service enabled, depending on when those clusters were created.</span></span> <span data-ttu-id="ababa-143">銅級耐久性層中的 Azure 叢集依預設不會啟用修復管理器服務。</span><span class="sxs-lookup"><span data-stu-id="ababa-143">Azure clusters in the bronze durability tier, by default, do not have the repair manager service enabled.</span></span> <span data-ttu-id="ababa-144">如果已啟用服務，可以在 Service Fabric Explorer 的系統服務區段中看到它正在執行。</span><span class="sxs-lookup"><span data-stu-id="ababa-144">If the service is already enabled, you can see it running in the system services section in the Service Fabric Explorer.</span></span>

##### <a name="azure-portal"></a><span data-ttu-id="ababa-145">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="ababa-145">Azure portal</span></span>
<span data-ttu-id="ababa-146">您可以在設定叢集時從 Azure 入口網站啟用修復管理員。</span><span class="sxs-lookup"><span data-stu-id="ababa-146">You can enable repair manager from Azure portal at the time of setting up of cluster.</span></span> <span data-ttu-id="ababa-147">在叢集設定時選取 `Add on features` 下的 `Include Repair Manager` 選項。</span><span class="sxs-lookup"><span data-stu-id="ababa-147">Select `Include Repair Manager` option under `Add on features` at the time of Cluster configuration.</span></span>
<span data-ttu-id="ababa-148">![從 Azure 入口網站啟用修復管理員的映像](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)</span><span class="sxs-lookup"><span data-stu-id="ababa-148">![Image of Enabling Repair Manager from Azure portal](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)</span></span>

##### <a name="azure-resource-manager-template"></a><span data-ttu-id="ababa-149">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="ababa-149">Azure Resource Manager template</span></span>
<span data-ttu-id="ababa-150">或者，您可以使用 [Azure Resource Manager 範本](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm)在新的和現有的 Service Fabric 叢集上啟用修復管理員。</span><span class="sxs-lookup"><span data-stu-id="ababa-150">Alternatively you can use the [Azure Resource Manager template](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) to enable the repair manager service on new and existing Service Fabric clusters.</span></span> <span data-ttu-id="ababa-151">取得您想要部署之叢集的範本。</span><span class="sxs-lookup"><span data-stu-id="ababa-151">Get the template for the cluster that you want to deploy.</span></span> <span data-ttu-id="ababa-152">您可以使用範例範本或建立自訂的 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="ababa-152">You can either use the sample templates or create a custom Resource Manager template.</span></span> 

<span data-ttu-id="ababa-153">若要使用 [Azure Resource Manager 範本](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm)啟用修復管理員服務：</span><span class="sxs-lookup"><span data-stu-id="ababa-153">To enable the repair manager service using [Azure Resource Manager template](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):</span></span>

1. <span data-ttu-id="ababa-154">首先，檢查 `Microsoft.ServiceFabric/clusters` 資源的 `apiversion` 是否已設定為 `2017-07-01-preview`，如下列程式碼片段所示。</span><span class="sxs-lookup"><span data-stu-id="ababa-154">First check that the `apiversion` is set to `2017-07-01-preview` for the `Microsoft.ServiceFabric/clusters` resource, as shown in the following snippet.</span></span> <span data-ttu-id="ababa-155">如果不是，您就需要將 `apiVersion` 更新為 `2017-07-01-preview` 值：</span><span class="sxs-lookup"><span data-stu-id="ababa-155">If it is different, then you need to update the `apiVersion` to the value `2017-07-01-preview`:</span></span>

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. <span data-ttu-id="ababa-156">立即啟用修復管理器服務，方法是在 `fabricSettings` 區段之後新增下列 `addonFeatures` 區段：</span><span class="sxs-lookup"><span data-stu-id="ababa-156">Now enable the repair manager service by adding the following `addonFeatures` section after the `fabricSettings` section:</span></span>

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. <span data-ttu-id="ababa-157">一旦您使用這些變更將叢集範本進行更新之後，將它們加以套用，使升級完成。</span><span class="sxs-lookup"><span data-stu-id="ababa-157">After you have updated your cluster template with these changes, apply them and let the upgrade finish.</span></span> <span data-ttu-id="ababa-158">您現在可以看到修復管理器系統服務在您的叢集中執行。</span><span class="sxs-lookup"><span data-stu-id="ababa-158">You can now see the repair manager system service running in your cluster.</span></span> <span data-ttu-id="ababa-159">它在 Service Fabric Explorer 的系統服務區段中叫作 `fabric:/System/RepairManagerService`。</span><span class="sxs-lookup"><span data-stu-id="ababa-159">It is called `fabric:/System/RepairManagerService` in the system services section in the Service Fabric Explorer.</span></span> 

### <a name="standalone-on-premises-clusters"></a><span data-ttu-id="ababa-160">獨立的內部部署叢集</span><span class="sxs-lookup"><span data-stu-id="ababa-160">Standalone on-premises clusters</span></span>

<span data-ttu-id="ababa-161">您可以使用[獨立 Windows 叢集的組態設定](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest)在新的和現有的 Service Fabric 叢集上啟用修復管理器。</span><span class="sxs-lookup"><span data-stu-id="ababa-161">You can use the [Configuration settings for standalone Windows cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) to enable the repair manager service on new and existing Service Fabric cluster.</span></span>

<span data-ttu-id="ababa-162">啟用修復管理器服務：</span><span class="sxs-lookup"><span data-stu-id="ababa-162">To enable the repair manager service:</span></span>

1. <span data-ttu-id="ababa-163">首先，檢查[一般叢集設定](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations)中的 `apiversion` 是否已設定為 `04-2017` 或更高版本：</span><span class="sxs-lookup"><span data-stu-id="ababa-163">First check that the `apiversion` in [General cluster configurations](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) is set to `04-2017` or higher:</span></span>

    ```json
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "04-2017",
        ...
    }
    ```

2. <span data-ttu-id="ababa-164">立即啟用修復管理器服務，方法是在 `fabricSettings` 區段之後新增下列 `addonFeaturres` 區段，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ababa-164">Now enable repair manager service by adding the following `addonFeaturres` section after the `fabricSettings` section as shown below:</span></span>

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. <span data-ttu-id="ababa-165">以這些變更更新您的叢集資訊清單，使用更新後的叢集資訊清單[建立新叢集](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server)或[升級叢集設定](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration)。</span><span class="sxs-lookup"><span data-stu-id="ababa-165">Update your cluster manifest with these changes, using the updated cluster manifest [create a new cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) or [upgrade the cluster configuration](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration).</span></span> <span data-ttu-id="ababa-166">叢集開始以更新的資訊清單執行後，您現在可以在 Service Fabric Explorer 的系統服務區段下，看到修復管理器系統服務 (亦稱為 `fabric:/System/RepairManagerService`) 在叢集中執行。</span><span class="sxs-lookup"><span data-stu-id="ababa-166">Once the cluster is running with updated cluster manifest, you can now see the repair manager system service running in your cluster, which is called `fabric:/System/RepairManagerService`, under system services section in the Service Fabric explorer.</span></span>

### <a name="disable-automatic-windows-update-on-all-nodes"></a><span data-ttu-id="ababa-167">停用所有節點上的自動 Windows Update</span><span class="sxs-lookup"><span data-stu-id="ababa-167">Disable automatic Windows Update on all nodes</span></span>

<span data-ttu-id="ababa-168">自動 Windows Update 可能會導致可用性遺失，因為在相同時間重新啟動多個叢集節點。</span><span class="sxs-lookup"><span data-stu-id="ababa-168">Automatic Windows updates might lead to availability loss because multiple cluster nodes can restart at the same time.</span></span> <span data-ttu-id="ababa-169">依預設，修補程式協調流程應用程式會在每個叢集節點上嘗試將自動 Windows Update 停用。</span><span class="sxs-lookup"><span data-stu-id="ababa-169">The patch orchestration app, by default, tries to disable the automatic Windows Update on each cluster node.</span></span> <span data-ttu-id="ababa-170">不過，如果設定是由系統管理員或群組原則所管理，建議將 Windows Update 原則明確地設定為「下載前先通知」。</span><span class="sxs-lookup"><span data-stu-id="ababa-170">However, if the settings are managed by an administrator or group policy, we recommend setting the Windows Update policy to “Notify before Download” explicitly.</span></span>

### <a name="optional-enable-azure-diagnostics"></a><span data-ttu-id="ababa-171">選擇性：啟用 Azure 診斷</span><span class="sxs-lookup"><span data-stu-id="ababa-171">Optional: Enable Azure Diagnostics</span></span>

<span data-ttu-id="ababa-172">執行 Service Fabric 執行階段版本 `5.6.220.9494` 和以上版本的叢集，會收集修補程式協調流程應用程式記錄作為 Service Fabric 記錄的一部分。</span><span class="sxs-lookup"><span data-stu-id="ababa-172">Clusters running Service Fabric runtime version `5.6.220.9494` and above collect patch orchestration app logs as part of Service Fabric logs.</span></span>
<span data-ttu-id="ababa-173">如果您的叢集是在 Service Fabric 執行階段 `5.6.220.9494` 版和以上版本執行，您可以略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="ababa-173">You can skip this step if your cluster is running on Service Fabric runtime version `5.6.220.9494` and above.</span></span>

<span data-ttu-id="ababa-174">對於執行 Service Fabric 執行階段 `5.6.220.9494` 以下版本的叢集，只會在每個叢集節點的本機收集修補程式協調流程應用程式記錄。</span><span class="sxs-lookup"><span data-stu-id="ababa-174">For clusters running Service Fabric runtime version less than `5.6.220.9494`, logs for the patch orchestration app are collected locally on each of the cluster nodes.</span></span>
<span data-ttu-id="ababa-175">我們建議您設定 Azure 診斷，將所有節點的記錄上傳到中央位置。</span><span class="sxs-lookup"><span data-stu-id="ababa-175">We recommend that you configure Azure Diagnostics to upload logs from all nodes to a central location.</span></span>

<span data-ttu-id="ababa-176">如需啟用 Azure 診斷的詳細資訊，請參閱[使用 Azure 診斷收集記錄](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad)。</span><span class="sxs-lookup"><span data-stu-id="ababa-176">For information on enabling Azure Diagnostics, see [Collect logs by using Azure Diagnostics](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).</span></span>

<span data-ttu-id="ababa-177">產生的修補程式協調流程應用程式的記錄，具有下列的固定提供者識別碼：</span><span class="sxs-lookup"><span data-stu-id="ababa-177">Logs for the patch orchestration app are generated on the following fixed provider IDs:</span></span>

- <span data-ttu-id="ababa-178">e39b723c-590c-4090-abb0-11e3e6616346</span><span class="sxs-lookup"><span data-stu-id="ababa-178">e39b723c-590c-4090-abb0-11e3e6616346</span></span>
- <span data-ttu-id="ababa-179">fc0028ff-bfdc-499f-80dc-ed922c52c5e9</span><span class="sxs-lookup"><span data-stu-id="ababa-179">fc0028ff-bfdc-499f-80dc-ed922c52c5e9</span></span>
- <span data-ttu-id="ababa-180">24afa313-0d3b-4c7c-b485-1047fd964b60</span><span class="sxs-lookup"><span data-stu-id="ababa-180">24afa313-0d3b-4c7c-b485-1047fd964b60</span></span>
- <span data-ttu-id="ababa-181">05dc046c-60e9-4ef7-965e-91660adffa68</span><span class="sxs-lookup"><span data-stu-id="ababa-181">05dc046c-60e9-4ef7-965e-91660adffa68</span></span>

<span data-ttu-id="ababa-182">在 Resource Manager 範本中，移至 `WadCfg` 下的 `EtwEventSourceProviderConfiguration` 區段，並新增下列項目：</span><span class="sxs-lookup"><span data-stu-id="ababa-182">In Resource Manager template goto `EtwEventSourceProviderConfiguration` section under `WadCfg` and add the following entries:</span></span>

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
> <span data-ttu-id="ababa-183">如果 Service Fabric 叢集有多種節點類型，則必須在所有的 `WadCfg` 區段新增上述區段。</span><span class="sxs-lookup"><span data-stu-id="ababa-183">If your Service Fabric cluster has multiple node types, then the previous section must be added for all the `WadCfg` sections.</span></span>

## <a name="download-the-app-package"></a><span data-ttu-id="ababa-184">下載安裝套件</span><span class="sxs-lookup"><span data-stu-id="ababa-184">Download the app package</span></span>

<span data-ttu-id="ababa-185">從[下載連結](https://go.microsoft.com/fwlink/P/?linkid=849590)下載應用程式。</span><span class="sxs-lookup"><span data-stu-id="ababa-185">Download the application from the [download link](https://go.microsoft.com/fwlink/P/?linkid=849590).</span></span>

## <a name="configure-the-app"></a><span data-ttu-id="ababa-186">設定應用程式</span><span class="sxs-lookup"><span data-stu-id="ababa-186">Configure the app</span></span>

<span data-ttu-id="ababa-187">您可以設定修補程式協調流程應用程式的行為以符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="ababa-187">The behavior of the patch orchestration app can be configured to meet your needs.</span></span> <span data-ttu-id="ababa-188">在應用程式建立或更新期間傳入應用程式參數，將預設值加以覆寫。</span><span class="sxs-lookup"><span data-stu-id="ababa-188">Override the default values by passing in the application parameter during application creation or update.</span></span> <span data-ttu-id="ababa-189">在 `Start-ServiceFabricApplicationUpgrade` 或 `New-ServiceFabricApplication` Cmdlet 中指定 `ApplicationParameter`，即可提供應用程式參數。</span><span class="sxs-lookup"><span data-stu-id="ababa-189">Application parameters can be provided by specifying `ApplicationParameter` to the `Start-ServiceFabricApplicationUpgrade` or `New-ServiceFabricApplication` cmdlets.</span></span>

|<span data-ttu-id="ababa-190">**參數**</span><span class="sxs-lookup"><span data-stu-id="ababa-190">**Parameter**</span></span>        |<span data-ttu-id="ababa-191">**類型**</span><span class="sxs-lookup"><span data-stu-id="ababa-191">**Type**</span></span>                          | <span data-ttu-id="ababa-192">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="ababa-192">**Details**</span></span>|
|:-|-|-|
|<span data-ttu-id="ababa-193">MaxResultsToCache</span><span class="sxs-lookup"><span data-stu-id="ababa-193">MaxResultsToCache</span></span>    |<span data-ttu-id="ababa-194">long</span><span class="sxs-lookup"><span data-stu-id="ababa-194">Long</span></span>                              | <span data-ttu-id="ababa-195">Windows Update 結果的最大數目，應加以快取。</span><span class="sxs-lookup"><span data-stu-id="ababa-195">Maximum number of Windows Update results, which should be cached.</span></span> <br><span data-ttu-id="ababa-196">預設值為 3000，是基於以下假設：</span><span class="sxs-lookup"><span data-stu-id="ababa-196">Default value is 3000 assuming the:</span></span> <br> <span data-ttu-id="ababa-197">- 節點數目 20。</span><span class="sxs-lookup"><span data-stu-id="ababa-197">- Number of nodes is 20.</span></span> <br> <span data-ttu-id="ababa-198">- 每個月在節點上發生的更新數目為 5。</span><span class="sxs-lookup"><span data-stu-id="ababa-198">- Number of updates happening on a node per month is five.</span></span> <br> <span data-ttu-id="ababa-199">- 每個作業的結果數目可為 10。</span><span class="sxs-lookup"><span data-stu-id="ababa-199">- Number of results per operation can be 10.</span></span> <br> <span data-ttu-id="ababa-200">- 過去 3 個月的結果皆加以儲存。</span><span class="sxs-lookup"><span data-stu-id="ababa-200">- Results for the past three months should be stored.</span></span> |
|<span data-ttu-id="ababa-201">TaskApprovalPolicy</span><span class="sxs-lookup"><span data-stu-id="ababa-201">TaskApprovalPolicy</span></span>   |<span data-ttu-id="ababa-202">例舉</span><span class="sxs-lookup"><span data-stu-id="ababa-202">Enum</span></span> <br> <span data-ttu-id="ababa-203">{ NodeWise, UpgradeDomainWise }</span><span class="sxs-lookup"><span data-stu-id="ababa-203">{ NodeWise, UpgradeDomainWise }</span></span>                          |<span data-ttu-id="ababa-204">TaskApprovalPolicy 會指出協調器服務在 Service Fabric 叢集節點中用來安裝 Windows 更新的原則。</span><span class="sxs-lookup"><span data-stu-id="ababa-204">TaskApprovalPolicy indicates the policy that is to be used by the Coordinator Service to install Windows updates across the Service Fabric cluster nodes.</span></span><br>                         <span data-ttu-id="ababa-205">允許的值包括：</span><span class="sxs-lookup"><span data-stu-id="ababa-205">Allowed values are:</span></span> <br>                                                           <span data-ttu-id="ababa-206"><b>NodeWise</b>。</span><span class="sxs-lookup"><span data-stu-id="ababa-206"><b>NodeWise</b>.</span></span> <span data-ttu-id="ababa-207">一次只會在一個節點上安裝 Windows Update。</span><span class="sxs-lookup"><span data-stu-id="ababa-207">Windows Update is installed one node at a time.</span></span> <br>                                                           <span data-ttu-id="ababa-208"><b>UpgradeDomainWise</b>。</span><span class="sxs-lookup"><span data-stu-id="ababa-208"><b>UpgradeDomainWise</b>.</span></span> <span data-ttu-id="ababa-209">一次只會在一個升級網域上安裝 Windows Update。</span><span class="sxs-lookup"><span data-stu-id="ababa-209">Windows Update is installed one upgrade domain at a time.</span></span> <span data-ttu-id="ababa-210">(最多，屬於升級網域的所有節點都可以進行 Windows Update。)</span><span class="sxs-lookup"><span data-stu-id="ababa-210">(At the maximum, all the nodes belonging to an upgrade domain can go for Windows Update.)</span></span>
|<span data-ttu-id="ababa-211">LogsDiskQuotaInMB</span><span class="sxs-lookup"><span data-stu-id="ababa-211">LogsDiskQuotaInMB</span></span>   |<span data-ttu-id="ababa-212">long</span><span class="sxs-lookup"><span data-stu-id="ababa-212">Long</span></span>  <br> <span data-ttu-id="ababa-213">(預設值︰1024)</span><span class="sxs-lookup"><span data-stu-id="ababa-213">(Default: 1024)</span></span>               |<span data-ttu-id="ababa-214">修補程式協調流程應用程式記錄的大小上限 (以 MB 為單位)，可在節點上本機保留。</span><span class="sxs-lookup"><span data-stu-id="ababa-214">Maximum size of patch orchestration app logs in MB, which can be persisted locally on nodes.</span></span>
| <span data-ttu-id="ababa-215">WUQuery</span><span class="sxs-lookup"><span data-stu-id="ababa-215">WUQuery</span></span>               | <span data-ttu-id="ababa-216">字串</span><span class="sxs-lookup"><span data-stu-id="ababa-216">string</span></span><br><span data-ttu-id="ababa-217">(預設值："IsInstalled=0")</span><span class="sxs-lookup"><span data-stu-id="ababa-217">(Default: "IsInstalled=0")</span></span>                | <span data-ttu-id="ababa-218">用以取得 Windows 更新的查詢。</span><span class="sxs-lookup"><span data-stu-id="ababa-218">Query to get Windows updates.</span></span> <span data-ttu-id="ababa-219">如需詳細資訊，請參閱 [WuQuery](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx)。</span><span class="sxs-lookup"><span data-stu-id="ababa-219">For more information, see [WuQuery.](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx)</span></span>
| <span data-ttu-id="ababa-220">InstallWindowsOSOnlyUpdates</span><span class="sxs-lookup"><span data-stu-id="ababa-220">InstallWindowsOSOnlyUpdates</span></span> | <span data-ttu-id="ababa-221">Bool</span><span class="sxs-lookup"><span data-stu-id="ababa-221">Bool</span></span> <br> <span data-ttu-id="ababa-222">(預設值︰True)</span><span class="sxs-lookup"><span data-stu-id="ababa-222">(default: True)</span></span>                 | <span data-ttu-id="ababa-223">這個旗標可讓您安裝 Windows 作業系統更新。</span><span class="sxs-lookup"><span data-stu-id="ababa-223">This flag allows Windows operating system updates to be installed.</span></span>            |
| <span data-ttu-id="ababa-224">WUOperationTimeOutInMinutes</span><span class="sxs-lookup"><span data-stu-id="ababa-224">WUOperationTimeOutInMinutes</span></span> | <span data-ttu-id="ababa-225">int</span><span class="sxs-lookup"><span data-stu-id="ababa-225">Int</span></span> <br><span data-ttu-id="ababa-226">(預設值︰90)</span><span class="sxs-lookup"><span data-stu-id="ababa-226">(Default: 90)</span></span>                   | <span data-ttu-id="ababa-227">指定任何 Windows Update 作業的逾時 (搜尋或下載或安裝)。</span><span class="sxs-lookup"><span data-stu-id="ababa-227">Specifies the timeout for any Windows Update operation (search or download or install).</span></span> <span data-ttu-id="ababa-228">如果作業未在指定的逾時內完成，它就會中止。</span><span class="sxs-lookup"><span data-stu-id="ababa-228">If the operation is not completed within the specified timeout, it is aborted.</span></span>       |
| <span data-ttu-id="ababa-229">WURescheduleCount</span><span class="sxs-lookup"><span data-stu-id="ababa-229">WURescheduleCount</span></span>     | <span data-ttu-id="ababa-230">int</span><span class="sxs-lookup"><span data-stu-id="ababa-230">Int</span></span> <br> <span data-ttu-id="ababa-231">(預設值︰5)</span><span class="sxs-lookup"><span data-stu-id="ababa-231">(Default: 5)</span></span>                  | <span data-ttu-id="ababa-232">如果作業持續失敗，服務會將 Windows Update 重新排程的次數上限。</span><span class="sxs-lookup"><span data-stu-id="ababa-232">The maximum number of times the service reschedules the Windows update in case an operation fails persistently.</span></span>          |
| <span data-ttu-id="ababa-233">WURescheduleTimeInMinutes</span><span class="sxs-lookup"><span data-stu-id="ababa-233">WURescheduleTimeInMinutes</span></span> | <span data-ttu-id="ababa-234">int</span><span class="sxs-lookup"><span data-stu-id="ababa-234">Int</span></span> <br><span data-ttu-id="ababa-235">(預設值︰30)</span><span class="sxs-lookup"><span data-stu-id="ababa-235">(Default: 30)</span></span> | <span data-ttu-id="ababa-236">如果作業持續失敗，服務會將 Windows Update 重新排程的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="ababa-236">The interval at which the service reschedules the Windows update in case failure persists.</span></span> |
| <span data-ttu-id="ababa-237">WUFrequency</span><span class="sxs-lookup"><span data-stu-id="ababa-237">WUFrequency</span></span>           | <span data-ttu-id="ababa-238">以逗號分隔的字串 (預設值︰"Weekly, Wednesday, 7:00:00")</span><span class="sxs-lookup"><span data-stu-id="ababa-238">Comma-separated string (Default: "Weekly, Wednesday, 7:00:00")</span></span>     | <span data-ttu-id="ababa-239">安裝 Windows Update 的頻率。</span><span class="sxs-lookup"><span data-stu-id="ababa-239">The frequency for installing Windows Update.</span></span> <span data-ttu-id="ababa-240">格式與可能的值如下：</span><span class="sxs-lookup"><span data-stu-id="ababa-240">The format and possible values are:</span></span> <br><span data-ttu-id="ababa-241">-   Monthly, DD,HH:MM:SS，例如 Monthly, 5,12:22:32。</span><span class="sxs-lookup"><span data-stu-id="ababa-241">-   Monthly, DD,HH:MM:SS, for example, Monthly, 5,12:22:32.</span></span> <br> <span data-ttu-id="ababa-242">-   Weekly, DAY,HH:MM:SS，例如 Weekly, Tuesday, 12:22:32。</span><span class="sxs-lookup"><span data-stu-id="ababa-242">-   Weekly, DAY,HH:MM:SS, for example, Weekly, Tuesday, 12:22:32.</span></span>  <br> <span data-ttu-id="ababa-243">-   Daily, HH:MM:SS，例如 Daily, 12:22:32。</span><span class="sxs-lookup"><span data-stu-id="ababa-243">-   Daily, HH:MM:SS, for example, Daily, 12:22:32.</span></span>  <br> <span data-ttu-id="ababa-244">-  None 表示不應該進行 Windows Update。</span><span class="sxs-lookup"><span data-stu-id="ababa-244">-  None indicates that Windows Update shouldn't be done.</span></span>  <br><br> <span data-ttu-id="ababa-245">請注意，所有時間都是 UTC 格式。</span><span class="sxs-lookup"><span data-stu-id="ababa-245">Note that all the times are in UTC.</span></span>|
| <span data-ttu-id="ababa-246">AcceptWindowsUpdateEula</span><span class="sxs-lookup"><span data-stu-id="ababa-246">AcceptWindowsUpdateEula</span></span> | <span data-ttu-id="ababa-247">Bool</span><span class="sxs-lookup"><span data-stu-id="ababa-247">Bool</span></span> <br><span data-ttu-id="ababa-248">(預設值︰true)</span><span class="sxs-lookup"><span data-stu-id="ababa-248">(Default: true)</span></span> | <span data-ttu-id="ababa-249">藉由設定這個旗標，應用程式會代表電腦的擁有者接受 Windows Update 的使用者授權合約 (EULA)。</span><span class="sxs-lookup"><span data-stu-id="ababa-249">By setting this flag, the application accepts the End-User License Agreement for Windows Update on behalf of the owner of the machine.</span></span>              |

> [!TIP]
> <span data-ttu-id="ababa-250">如果需要 Windows Update 立即發生，請將 `WUFrequency` 設定為相對於應用程式部署的時間。</span><span class="sxs-lookup"><span data-stu-id="ababa-250">If you want Windows Update to happen immediately, set `WUFrequency` relative to the application deployment time.</span></span> <span data-ttu-id="ababa-251">例如，假設您的測試叢集有五個節點，計劃於大約下午 5:00 UTC 部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="ababa-251">For example, suppose that you have a five-node test cluster and plan to deploy the app at around 5:00 PM UTC.</span></span> <span data-ttu-id="ababa-252">如果您假設應用程式的升級或部署最多會花費 30 分鐘的時間，則將 WUFrequency 設定為 "Daily, 17:30:00"。</span><span class="sxs-lookup"><span data-stu-id="ababa-252">If you assume that the application upgrade or deployment takes 30 minutes at the maximum, set the WUFrequency as "Daily, 17:30:00."</span></span>

## <a name="deploy-the-app"></a><span data-ttu-id="ababa-253">部署應用程式</span><span class="sxs-lookup"><span data-stu-id="ababa-253">Deploy the app</span></span>

1. <span data-ttu-id="ababa-254">完成準備叢集的所有必要條件步驟。</span><span class="sxs-lookup"><span data-stu-id="ababa-254">Finish all the prerequisite steps to prepare the cluster.</span></span>
2. <span data-ttu-id="ababa-255">部署修補程式協調流程應用程式，和任何其他 Service Fabric 應用程式一樣。</span><span class="sxs-lookup"><span data-stu-id="ababa-255">Deploy the patch orchestration app like any other Service Fabric app.</span></span> <span data-ttu-id="ababa-256">您可以使用 PowerShell 部署此應用程式。</span><span class="sxs-lookup"><span data-stu-id="ababa-256">You can deploy the app by using PowerShell.</span></span> <span data-ttu-id="ababa-257">請遵循[使用 PowerShell 部署與移除應用程式](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications)中的步驟。</span><span class="sxs-lookup"><span data-stu-id="ababa-257">Follow the steps in [Deploy and remove applications using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span></span>
3. <span data-ttu-id="ababa-258">若要在部署時設定應用程式，可將 `ApplicationParamater` 傳遞給 `New-ServiceFabricApplication` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="ababa-258">To configure the application at the time of deployment, pass the `ApplicationParamater` to the `New-ServiceFabricApplication` cmdlet.</span></span> <span data-ttu-id="ababa-259">為了您的方便，我們提供了 Deploy.ps1 指令碼以及我們的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ababa-259">For your convenience, we’ve provided the script Deploy.ps1 along with the application.</span></span> <span data-ttu-id="ababa-260">若要使用指令碼：</span><span class="sxs-lookup"><span data-stu-id="ababa-260">To use the script:</span></span>

    - <span data-ttu-id="ababa-261">使用 `Connect-ServiceFabricCluster` 連線至 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="ababa-261">Connect to a Service Fabric cluster by using `Connect-ServiceFabricCluster`.</span></span>
    - <span data-ttu-id="ababa-262">利用適當的 `ApplicationParameter` 值執行 Powershell 指令碼 Deploy.ps1。</span><span class="sxs-lookup"><span data-stu-id="ababa-262">Execute the PowerShell script Deploy.ps1 with the appropriate `ApplicationParameter` value.</span></span>

> [!NOTE]
> <span data-ttu-id="ababa-263">將指令碼和應用程式資料夾 PatchOrchestrationApplication 保存在同一個目錄中。</span><span class="sxs-lookup"><span data-stu-id="ababa-263">Keep the script and the application folder PatchOrchestrationApplication in the same directory.</span></span>

## <a name="upgrade-the-app"></a><span data-ttu-id="ababa-264">升級應用程式</span><span class="sxs-lookup"><span data-stu-id="ababa-264">Upgrade the app</span></span>

<span data-ttu-id="ababa-265">若要使用 PowerShell 將現有的修補程式協調流程應用程式進行升級，請遵循[使用 PowerShell 升級 Service Fabric應用程式](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell)中的步驟。</span><span class="sxs-lookup"><span data-stu-id="ababa-265">To upgrade an existing patch orchestration app by using PowerShell, follow the steps in [Service Fabric application upgrade using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).</span></span>

## <a name="remove-the-app"></a><span data-ttu-id="ababa-266">移除應用程式</span><span class="sxs-lookup"><span data-stu-id="ababa-266">Remove the app</span></span>

<span data-ttu-id="ababa-267">若要移除應用程式，請遵循[使用 PowerShell 部署與移除應用程式](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications)中的步驟。</span><span class="sxs-lookup"><span data-stu-id="ababa-267">To remove the application, follow the steps in [Deploy and remove applications using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span></span>

<span data-ttu-id="ababa-268">為了您的方便，我們提供了 Undeploy.ps1 指令碼以及我們的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ababa-268">For your convenience, we've provided the script Undeploy.ps1 along with the application.</span></span> <span data-ttu-id="ababa-269">若要使用指令碼：</span><span class="sxs-lookup"><span data-stu-id="ababa-269">To use the script:</span></span>

  - <span data-ttu-id="ababa-270">使用 ```Connect-ServiceFabricCluster``` 連線至 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="ababa-270">Connect to a Service Fabric cluster by using ```Connect-ServiceFabricCluster```.</span></span>

  - <span data-ttu-id="ababa-271">執行 Powershell 指令碼 Undeploy.ps1。</span><span class="sxs-lookup"><span data-stu-id="ababa-271">Execute the PowerShell script Undeploy.ps1.</span></span>

> [!NOTE]
> <span data-ttu-id="ababa-272">將指令碼和應用程式資料夾 PatchOrchestrationApplication 保存在同一個目錄中。</span><span class="sxs-lookup"><span data-stu-id="ababa-272">Keep the script and the application folder PatchOrchestrationApplication in the same directory.</span></span>

## <a name="view-the-windows-update-results"></a><span data-ttu-id="ababa-273">檢視 Windows Update 結果</span><span class="sxs-lookup"><span data-stu-id="ababa-273">View the Windows Update results</span></span>

<span data-ttu-id="ababa-274">修補程式協調流程應用程式會公開 REST API，以向使用者顯示歷程記錄的結果。</span><span class="sxs-lookup"><span data-stu-id="ababa-274">The patch orchestration app exposes REST APIs to display the historical results to the user.</span></span> <span data-ttu-id="ababa-275">JSON 結果的範例：</span><span class="sxs-lookup"><span data-stu-id="ababa-275">An example of the result JSON:</span></span>
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
            "Description": "A security issue has been identified in a Microsoft software product that could affect your system. You can help protect your system by installing this update from Microsoft. For a complete listing of the issues that are included in this update, see the associated Microsoft Knowledge Base article. After you install this update, you may have to restart your system.",
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
<span data-ttu-id="ababa-276">如果尚未排程更新，JSON 結果會是空的。</span><span class="sxs-lookup"><span data-stu-id="ababa-276">If no update is scheduled yet, the result JSON is empty.</span></span>

<span data-ttu-id="ababa-277">登入叢集，查詢 Windows Update 的結果。</span><span class="sxs-lookup"><span data-stu-id="ababa-277">Log in to the cluster to query Windows Update results.</span></span> <span data-ttu-id="ababa-278">接著，找出主要協調器服務的複本位址，然後點閱瀏覽器的 URL：http://&lt;REPLICA-IP&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1/GetWindowsUpdateResults。</span><span class="sxs-lookup"><span data-stu-id="ababa-278">Then find out the replica address for the primary of the Coordinator Service, and hit the URL from the browser: http://&lt;REPLICA-IP&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1/GetWindowsUpdateResults.</span></span>

<span data-ttu-id="ababa-279">協調器服務的 REST 端點具有動態連接埠。</span><span class="sxs-lookup"><span data-stu-id="ababa-279">The REST endpoint for the Coordinator Service has a dynamic port.</span></span> <span data-ttu-id="ababa-280">若要知道確切 URL，請查看 Service Fabric Explorer。</span><span class="sxs-lookup"><span data-stu-id="ababa-280">To check the exact URL, refer to the Service Fabric Explorer.</span></span> <span data-ttu-id="ababa-281">例如，可在 `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults` 找到結果。</span><span class="sxs-lookup"><span data-stu-id="ababa-281">For example, the results are available at `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.</span></span>

![REST 端點的圖片](media/service-fabric-patch-orchestration-application/Rest_Endpoint.png)


<span data-ttu-id="ababa-283">如果在叢集上啟用反向 Proxy，您也可以從叢集外部存取 URL。</span><span class="sxs-lookup"><span data-stu-id="ababa-283">If the reverse proxy is enabled on the cluster, you can access the URL from outside of the cluster as well.</span></span>
<span data-ttu-id="ababa-284">需要點閱的端點為 http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults。</span><span class="sxs-lookup"><span data-stu-id="ababa-284">The endpoint that needs to be hit is http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.</span></span>

<span data-ttu-id="ababa-285">若要啟用叢集的反向 Proxy，請遵循 [Azure Service Fabric 中的反向 Proxy](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) 中的步驟。</span><span class="sxs-lookup"><span data-stu-id="ababa-285">To enable the reverse proxy on the cluster, follow the steps in [Reverse proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).</span></span> 

> 
> [!WARNING]
> <span data-ttu-id="ababa-286">設定反向 Proxy 之後，叢集中公開 HTTP 端點的所有微服務就能從叢集外部尋址。</span><span class="sxs-lookup"><span data-stu-id="ababa-286">After the reverse proxy is configured, all micro services in the cluster that expose an HTTP endpoint are addressable from outside the cluster.</span></span>

## <a name="diagnosticshealth-events"></a><span data-ttu-id="ababa-287">診斷/健康情況事件</span><span class="sxs-lookup"><span data-stu-id="ababa-287">Diagnostics/health events</span></span>

### <a name="collect-patch-orchestration-app-logs"></a><span data-ttu-id="ababa-288">收集修補程式協調流程應用程式記錄</span><span class="sxs-lookup"><span data-stu-id="ababa-288">Collect patch orchestration app logs</span></span>

<span data-ttu-id="ababa-289">收集修補程式協調流程應用程式的記錄，是執行階段版本 `5.6.220.9494` 及以上版本作為 Service Fabric 記錄的一部分。</span><span class="sxs-lookup"><span data-stu-id="ababa-289">Patch orchestration app logs are collected as part of Service Fabric logs from runtime version `5.6.220.9494` and above.</span></span>
<span data-ttu-id="ababa-290">至於執行 Service Fabric 執行階段 `5.6.220.9494` 以下版本的叢集，可使用下列方法收集記錄。</span><span class="sxs-lookup"><span data-stu-id="ababa-290">For clusters running Service Fabric runtime version less than `5.6.220.9494`, logs can be collected by using one of the following methods.</span></span>

#### <a name="locally-on-each-node"></a><span data-ttu-id="ababa-291">本機的每個節點上</span><span class="sxs-lookup"><span data-stu-id="ababa-291">Locally on each node</span></span>

<span data-ttu-id="ababa-292">如果 Service Fabric 執行階段版本小於 `5.6.220.9494`，則只會在每個 Service Fabric 叢集節點的本機收集記錄。</span><span class="sxs-lookup"><span data-stu-id="ababa-292">Logs are collected locally on each Service Fabric cluster node if Service Fabric runtime version is less than `5.6.220.9494`.</span></span> <span data-ttu-id="ababa-293">存取記錄的位置為 \[Service Fabric\_Installation\_Drive\]:\\PatchOrchestrationApplication\\logs。</span><span class="sxs-lookup"><span data-stu-id="ababa-293">The location to access the logs is \[Service Fabric\_Installation\_Drive\]:\\PatchOrchestrationApplication\\logs.</span></span>

<span data-ttu-id="ababa-294">例如︰如果 Service Fabric 是安裝在 D 磁碟機上，則路徑為 D:\\PatchOrchestrationApplication\\logs。</span><span class="sxs-lookup"><span data-stu-id="ababa-294">For example, if Service Fabric is installed on drive D, the path is D:\\PatchOrchestrationApplication\\logs.</span></span>

#### <a name="central-location"></a><span data-ttu-id="ababa-295">中央位置</span><span class="sxs-lookup"><span data-stu-id="ababa-295">Central location</span></span>

<span data-ttu-id="ababa-296">如果 Azure 診斷設為必要條件步驟的一部分，就可在 Azure 儲存體中使用修補程式協調流程應用程式的記錄。</span><span class="sxs-lookup"><span data-stu-id="ababa-296">If Azure Diagnostics is configured as part of prerequisite steps, logs for the patch orchestration app are available in Azure Storage.</span></span>

### <a name="health-reports"></a><span data-ttu-id="ababa-297">健康狀態報告</span><span class="sxs-lookup"><span data-stu-id="ababa-297">Health reports</span></span>

<span data-ttu-id="ababa-298">修補程式協調流程應用程式在下列情況下也會發佈協調器服務或節點代理程式服務的健康情況報告：</span><span class="sxs-lookup"><span data-stu-id="ababa-298">The patch orchestration app also publishes health reports against the Coordinator Service or the Node Agent Service in the following cases:</span></span>

#### <a name="a-windows-update-operation-failed"></a><span data-ttu-id="ababa-299">Windows Update 作業失敗</span><span class="sxs-lookup"><span data-stu-id="ababa-299">A Windows Update operation failed</span></span>

<span data-ttu-id="ababa-300">如果節點上的 Windows Update 作業失敗，就會產生節點代理程式服務的健康情況報告。</span><span class="sxs-lookup"><span data-stu-id="ababa-300">If a Windows Update operation fails on a node, a health report is generated against the Node Agent Service.</span></span> <span data-ttu-id="ababa-301">健康情況報告的詳細資料中包含有問題的節點名稱。</span><span class="sxs-lookup"><span data-stu-id="ababa-301">Details of the health report contain the problematic node name.</span></span>

<span data-ttu-id="ababa-302">在有問題的節點上順利完成修補後，系統會自動清除報告。</span><span class="sxs-lookup"><span data-stu-id="ababa-302">After patching is successfully completed on the problematic node, the report is automatically cleared.</span></span>

#### <a name="the-node-agent-ntservice-is-down"></a><span data-ttu-id="ababa-303">節點代理程式 NTService 關閉</span><span class="sxs-lookup"><span data-stu-id="ababa-303">The Node Agent NTService is down</span></span>

<span data-ttu-id="ababa-304">如果節點上的節點代理程式 NTService 關閉，就會產生節點代理程式服務的警告等級健康情況報告。</span><span class="sxs-lookup"><span data-stu-id="ababa-304">If the Node Agent NTService is down on a node, a warning-level health report is generated against the Node Agent Service.</span></span>

#### <a name="the-repair-manager-service-is-not-enabled"></a><span data-ttu-id="ababa-305">修復管理器服務未啟用</span><span class="sxs-lookup"><span data-stu-id="ababa-305">The repair manager service is not enabled</span></span>

<span data-ttu-id="ababa-306">如果在叢集上找不到修復管理器服務，就會產生協調器服務的警告等級健康情況報告。</span><span class="sxs-lookup"><span data-stu-id="ababa-306">If the repair manager service is not found on the cluster, a warning-level health report is generated for the Coordinator Service.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="ababa-307">常見問題集</span><span class="sxs-lookup"><span data-stu-id="ababa-307">Frequently asked questions</span></span>

<span data-ttu-id="ababa-308">問：</span><span class="sxs-lookup"><span data-stu-id="ababa-308">Q.</span></span> <span data-ttu-id="ababa-309">**當修補程式協調流程應用程式執行時，為什麼我看到叢集處於錯誤狀態？**</span><span class="sxs-lookup"><span data-stu-id="ababa-309">**Why do I see my cluster in an error state when the patch orchestration app is running?**</span></span>

<span data-ttu-id="ababa-310">A.</span><span class="sxs-lookup"><span data-stu-id="ababa-310">A.</span></span> <span data-ttu-id="ababa-311">在安裝程序期間，修補程式協調流程應用程式會停用或重新啟動節點，而這可能會導致叢集暫時關閉的健康情況。</span><span class="sxs-lookup"><span data-stu-id="ababa-311">During the installation process, the patch orchestration app disables or restarts nodes, which can temporarily result in the health of the cluster going down.</span></span>

<span data-ttu-id="ababa-312">根據應用程式的原則，可能是一個節點在修補作業期間關閉，「或是」整個升級網域同時關閉。</span><span class="sxs-lookup"><span data-stu-id="ababa-312">Based on the policy for the application, either one node can go down during a patching operation *or* an entire upgrade domain can go down simultaneously.</span></span>

<span data-ttu-id="ababa-313">Windows Update 安裝結束時，在重新啟動前會重新啟用節點。</span><span class="sxs-lookup"><span data-stu-id="ababa-313">By the end of the Windows Update installation, the nodes are reenabled post restart.</span></span>

<span data-ttu-id="ababa-314">在下列範例中，因為兩個節點關閉，且違反 MaxPercentageUnhealthNodes 原則，叢集會暫時進入錯誤狀態。</span><span class="sxs-lookup"><span data-stu-id="ababa-314">In the following example, the cluster went to an error state temporarily because two nodes were down and the MaxPercentageUnhealthNodes policy was violated.</span></span> <span data-ttu-id="ababa-315">錯誤是暫時性的，直到修補作業進行中為止。</span><span class="sxs-lookup"><span data-stu-id="ababa-315">The error is temporary until the patching operation is ongoing.</span></span>

![健康情況不良之叢集的圖片](media/service-fabric-patch-orchestration-application/MaxPercentage_causing_unhealthy_cluster.png)

<span data-ttu-id="ababa-317">如果問題持續發生，請參閱〈疑難排解〉一節。</span><span class="sxs-lookup"><span data-stu-id="ababa-317">If the issue persists, refer to the Troubleshooting section.</span></span>

<span data-ttu-id="ababa-318">問：</span><span class="sxs-lookup"><span data-stu-id="ababa-318">Q.</span></span> <span data-ttu-id="ababa-319">**修補程式協調流程應用程式處於警告狀態**</span><span class="sxs-lookup"><span data-stu-id="ababa-319">**Patch orchestration app is in warning state**</span></span>

<span data-ttu-id="ababa-320">A.</span><span class="sxs-lookup"><span data-stu-id="ababa-320">A.</span></span> <span data-ttu-id="ababa-321">檢查針對應用程式所公佈的健康情況報告，是否為根本原因。</span><span class="sxs-lookup"><span data-stu-id="ababa-321">Check to see if a health report posted against the application is the root cause.</span></span> <span data-ttu-id="ababa-322">警告通常包含問題的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ababa-322">Usually, the warning contains details of the problem.</span></span> <span data-ttu-id="ababa-323">如果是暫時性的問題，應用程式預期會從這個狀態中自動復原。</span><span class="sxs-lookup"><span data-stu-id="ababa-323">If the issue is transient, the application is expected to auto-recover from this state.</span></span>

<span data-ttu-id="ababa-324">問：</span><span class="sxs-lookup"><span data-stu-id="ababa-324">Q.</span></span> <span data-ttu-id="ababa-325">**如果我的叢集健康情況不良，我可以做什麼？我需要採取緊急作業系統更新嗎？**</span><span class="sxs-lookup"><span data-stu-id="ababa-325">**What can I do if my cluster is unhealthy and I need to do an urgent operating system update?**</span></span>

<span data-ttu-id="ababa-326">A.</span><span class="sxs-lookup"><span data-stu-id="ababa-326">A.</span></span> <span data-ttu-id="ababa-327">當叢集健康情況不良時，修補程式協調流程應用程式就不會安裝更新。</span><span class="sxs-lookup"><span data-stu-id="ababa-327">The patch orchestration app does not install updates while the cluster is unhealthy.</span></span> <span data-ttu-id="ababa-328">請嘗試使叢集處於良好的健康情況，以便將修補程式協調流程應用程式工作流程解除封鎖。</span><span class="sxs-lookup"><span data-stu-id="ababa-328">Try to bring your cluster to a healthy state to unblock the patch orchestration app workflow.</span></span>

<span data-ttu-id="ababa-329">問：</span><span class="sxs-lookup"><span data-stu-id="ababa-329">Q.</span></span> <span data-ttu-id="ababa-330">**為什麼跨叢集修補的執行時間這麼久？**</span><span class="sxs-lookup"><span data-stu-id="ababa-330">**Why does patching across clusters take so long to run?**</span></span>

<span data-ttu-id="ababa-331">A.</span><span class="sxs-lookup"><span data-stu-id="ababa-331">A.</span></span> <span data-ttu-id="ababa-332">修補程式協調流程應用程式所花費的時間大部分是取決於下列因素︰</span><span class="sxs-lookup"><span data-stu-id="ababa-332">The time needed by the patch orchestration app is mostly dependent on the following factors:</span></span>

- <span data-ttu-id="ababa-333">協調器服務的原則。</span><span class="sxs-lookup"><span data-stu-id="ababa-333">The policy of the Coordinator Service.</span></span> 
  - <span data-ttu-id="ababa-334">預設原則 `NodeWise` 的結果是一次只修補一個節點。</span><span class="sxs-lookup"><span data-stu-id="ababa-334">The default policy, `NodeWise`, results in patching only one node at a time.</span></span> <span data-ttu-id="ababa-335">特別是在叢集較大的情況下，建議您使用 `UpgradeDomainWise` 原則以更快速修補多個叢集。</span><span class="sxs-lookup"><span data-stu-id="ababa-335">Especially in the case of bigger clusters, we recommend that you use the `UpgradeDomainWise` policy to achieve faster patching across clusters.</span></span>
- <span data-ttu-id="ababa-336">適用於下載和安裝的更新數目。</span><span class="sxs-lookup"><span data-stu-id="ababa-336">The number of updates available for download and installation.</span></span> 
- <span data-ttu-id="ababa-337">下載並安裝更新時所需的平均時間，不應該超過幾個小時。</span><span class="sxs-lookup"><span data-stu-id="ababa-337">The average time needed to download and install an update, which should not exceed a couple of hours.</span></span>
- <span data-ttu-id="ababa-338">VM 和網路頻寬的效能。</span><span class="sxs-lookup"><span data-stu-id="ababa-338">The performance of the VM and network bandwidth.</span></span>

<span data-ttu-id="ababa-339">問：</span><span class="sxs-lookup"><span data-stu-id="ababa-339">Q.</span></span> <span data-ttu-id="ababa-340">**為什麼看到 Windows Update 結果中的某些更新是透過 REST API 取得，而不是電腦上的 Windows Update 歷程記錄下？**</span><span class="sxs-lookup"><span data-stu-id="ababa-340">**Why do I see some updates in Windows Update results obtained via REST api's, but not under the Windows Update history on machine?**</span></span>

<span data-ttu-id="ababa-341">A.</span><span class="sxs-lookup"><span data-stu-id="ababa-341">A.</span></span> <span data-ttu-id="ababa-342">某些產品更新需要簽入其各自的更新/修補歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="ababa-342">Some product updates need to be checked in their respective update/patch history.</span></span> <span data-ttu-id="ababa-343">例如：Windows Defender 更新不會顯示在 Windows Server 2016 上的 Windows Update 歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="ababa-343">Eg: Windows Defender updates do not show up in Windows Update history on Windows Server 2016.</span></span>

## <a name="disclaimers"></a><span data-ttu-id="ababa-344">免責聲明</span><span class="sxs-lookup"><span data-stu-id="ababa-344">Disclaimers</span></span>

- <span data-ttu-id="ababa-345">修補程式協調流程應用程式會代表使用者接受 Windows Update 的使用者授權合約 (EULA)。</span><span class="sxs-lookup"><span data-stu-id="ababa-345">The patch orchestration app accepts the End-User License Agreement of Windows Update on behalf of the user.</span></span> <span data-ttu-id="ababa-346">可在應用程式的設定中選擇性地將此設定關閉。</span><span class="sxs-lookup"><span data-stu-id="ababa-346">Optionally, the setting can be turned off in the configuration of the application.</span></span>

- <span data-ttu-id="ababa-347">修補程式協調流程應用程式會收集遙測來追蹤使用情形和效能。</span><span class="sxs-lookup"><span data-stu-id="ababa-347">The patch orchestration app collects telemetry to track usage and performance.</span></span> <span data-ttu-id="ababa-348">應用程式的遙測會遵循 Service Fabric 執行階段遙測設定 (預設為開啟) 的設定。</span><span class="sxs-lookup"><span data-stu-id="ababa-348">The application’s telemetry follows the setting of the Service Fabric runtime’s telemetry setting (which is on by default).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="ababa-349">疑難排解</span><span class="sxs-lookup"><span data-stu-id="ababa-349">Troubleshooting</span></span>

### <a name="a-node-is-not-coming-back-to-up-state"></a><span data-ttu-id="ababa-350">節點不會回到開啟狀態</span><span class="sxs-lookup"><span data-stu-id="ababa-350">A node is not coming back to up state</span></span>

<span data-ttu-id="ababa-351">**節點可能會卡在停用中狀態，因為**：</span><span class="sxs-lookup"><span data-stu-id="ababa-351">**The node might be stuck in a disabling state because**:</span></span>

<span data-ttu-id="ababa-352">安全性檢查擱置。</span><span class="sxs-lookup"><span data-stu-id="ababa-352">A safety check is pending.</span></span> <span data-ttu-id="ababa-353">若要補救這種情況，請確定有足夠多健康情況良好的節點。</span><span class="sxs-lookup"><span data-stu-id="ababa-353">To remedy this situation, ensure that enough nodes are available in a healthy state.</span></span>

<span data-ttu-id="ababa-354">**節點可能會卡在已停用狀態，因為**：</span><span class="sxs-lookup"><span data-stu-id="ababa-354">**The node might be stuck in a disabled state because**:</span></span>

- <span data-ttu-id="ababa-355">已將節點手動停用。</span><span class="sxs-lookup"><span data-stu-id="ababa-355">The node was disabled manually.</span></span>
- <span data-ttu-id="ababa-356">因為 Azure 基礎結構作業正在進行中而導致節點停用。</span><span class="sxs-lookup"><span data-stu-id="ababa-356">The node was disabled due to an ongoing Azure infrastructure job.</span></span>
- <span data-ttu-id="ababa-357">修補程式協調流程應用程式已暫時將節點停用，以修補節點。</span><span class="sxs-lookup"><span data-stu-id="ababa-357">The node was disabled temporarily by the patch orchestration app to patch the node.</span></span>

<span data-ttu-id="ababa-358">**節點可能會卡在關閉狀態，因為**：</span><span class="sxs-lookup"><span data-stu-id="ababa-358">**The node might be stuck in a down state because**:</span></span>

- <span data-ttu-id="ababa-359">已手動將節點置於關閉狀態。</span><span class="sxs-lookup"><span data-stu-id="ababa-359">The node was put in a down state manually.</span></span>
- <span data-ttu-id="ababa-360">節點正在重新啟動 (可能是由修補程式協調流程應用程式觸發)。</span><span class="sxs-lookup"><span data-stu-id="ababa-360">The node is undergoing a restart (which might be triggered by the patch orchestration app).</span></span>
- <span data-ttu-id="ababa-361">由於 VM 或機器故障或網路連線問題，使節點關閉。</span><span class="sxs-lookup"><span data-stu-id="ababa-361">The node is down due to a faulty VM or machine or network connectivity issues.</span></span>

### <a name="updates-were-skipped-on-some-nodes"></a><span data-ttu-id="ababa-362">已略過某些節點上的更新</span><span class="sxs-lookup"><span data-stu-id="ababa-362">Updates were skipped on some nodes</span></span>

<span data-ttu-id="ababa-363">修補程式協調流程應用程式會根據重新排定的原則，嘗試安裝 Windows Update。</span><span class="sxs-lookup"><span data-stu-id="ababa-363">The patch orchestration app tries to install a Windows update according to the rescheduling policy.</span></span> <span data-ttu-id="ababa-364">服務會根據應用程式原則，嘗試復原節點並略過更新。</span><span class="sxs-lookup"><span data-stu-id="ababa-364">The service tries to recover the node and skip the update according to the application policy.</span></span>

<span data-ttu-id="ababa-365">在這種情況下，系統會針對節點代理程式服務產生警告等級的健康情況報告。</span><span class="sxs-lookup"><span data-stu-id="ababa-365">In such a case, a warning-level health report is generated against the Node Agent Service.</span></span> <span data-ttu-id="ababa-366">Windows Update 的結果也包含可能的失敗原因。</span><span class="sxs-lookup"><span data-stu-id="ababa-366">The result for Windows Update also contains the possible reason for the failure.</span></span>

### <a name="the-health-of-the-cluster-goes-to-error-while-the-update-installs"></a><span data-ttu-id="ababa-367">開始安裝更新時，叢集的健康情況出現錯誤</span><span class="sxs-lookup"><span data-stu-id="ababa-367">The health of the cluster goes to error while the update installs</span></span>

<span data-ttu-id="ababa-368">錯誤的 Windows Update 會損及特定節點或升級網域上應用程式或叢集的健康情況。</span><span class="sxs-lookup"><span data-stu-id="ababa-368">A faulty Windows update can bring down the health of an application or cluster on a particular node or upgrade domain.</span></span> <span data-ttu-id="ababa-369">修補程式協調流程應用程式會中止所有後續的 Windows Update作業，直到叢集恢復良好健康情況。</span><span class="sxs-lookup"><span data-stu-id="ababa-369">The patch orchestration app discontinues any subsequent Windows Update operation until the cluster is healthy again.</span></span>

<span data-ttu-id="ababa-370">系統管理員必須介入，判斷應用程式或叢集為何因為 Windows Update 變成健康情況不良。</span><span class="sxs-lookup"><span data-stu-id="ababa-370">An administrator must intervene and determine why the application or cluster became unhealthy due to Windows Update.</span></span>

## <a name="release-notes-"></a><span data-ttu-id="ababa-371">版本資訊：</span><span class="sxs-lookup"><span data-stu-id="ababa-371">Release Notes :</span></span>

### <a name="version-110"></a><span data-ttu-id="ababa-372">1.1.0 版</span><span class="sxs-lookup"><span data-stu-id="ababa-372">Version 1.1.0</span></span>
- <span data-ttu-id="ababa-373">公開版本</span><span class="sxs-lookup"><span data-stu-id="ababa-373">Public release</span></span>

### <a name="version-111"></a><span data-ttu-id="ababa-374">1.1.1 版</span><span class="sxs-lookup"><span data-stu-id="ababa-374">Version 1.1.1</span></span>
- <span data-ttu-id="ababa-375">修正 SetupEntryPoint of NodeAgentService 中的錯誤，該錯誤導致無法安裝 NodeAgentNTService。</span><span class="sxs-lookup"><span data-stu-id="ababa-375">Fixed a bug in SetupEntryPoint of NodeAgentService that prevented installation of NodeAgentNTService.</span></span>

### <a name="version-120-latest"></a><span data-ttu-id="ababa-376">1.2.0 版 (最新)</span><span class="sxs-lookup"><span data-stu-id="ababa-376">Version 1.2.0 (Latest)</span></span>

- <span data-ttu-id="ababa-377">關於系統重新啟動工作流程的錯誤修正。</span><span class="sxs-lookup"><span data-stu-id="ababa-377">Bug fixes around system restart workflow.</span></span>
- <span data-ttu-id="ababa-378">由於準備修復工作期間健康情況檢查未如預期般發生，而在 RM 工作建立時進行的錯誤修正。</span><span class="sxs-lookup"><span data-stu-id="ababa-378">Bug fix in creation of RM tasks due to which health check during preparing repair tasks wasn't happening as expected.</span></span>
- <span data-ttu-id="ababa-379">將 Windows 服務 POANodeSvc 的啟動模式從自動變更為延遲自動。</span><span class="sxs-lookup"><span data-stu-id="ababa-379">Changed the startup mode for windows service POANodeSvc from auto to delayed-auto.</span></span>
