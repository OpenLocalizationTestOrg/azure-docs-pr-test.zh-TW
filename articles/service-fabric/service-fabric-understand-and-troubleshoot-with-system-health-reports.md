---
title: "使用系統健康狀態報告進行疑難排解 | Microsoft 疑難排解"
description: "描述針對 Azure Service Fabric 元件及其使用量所傳送的健康狀態報告，以便對叢集或應用程式問題進行疑難排解。"
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 52574ea7-eb37-47e0-a20a-101539177625
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: 54e20146b2f1e0ca6153b66319be70c6f7c2fb59
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="use-system-health-reports-to-troubleshoot"></a><span data-ttu-id="a3b4c-103">使用系統健康狀態報告進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="a3b4c-103">Use system health reports to troubleshoot</span></span>
<span data-ttu-id="a3b4c-104">Azure Service Fabric 元件會針對叢集中的所有實體提供現成的報告。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-104">Azure Service Fabric components report out of the box on all entities in the cluster.</span></span> <span data-ttu-id="a3b4c-105">[健康狀態資料存放區](service-fabric-health-introduction.md#health-store) 會根據系統報告來建立和刪除實體。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-105">The [health store](service-fabric-health-introduction.md#health-store) creates and deletes entities based on the system reports.</span></span> <span data-ttu-id="a3b4c-106">它也會將這些實體組織為階層以擷取實體的互動。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-106">It also organizes them in a hierarchy that captures entity interactions.</span></span>

> [!NOTE]
> <span data-ttu-id="a3b4c-107">若要了解健康狀態相關概念，請詳細閱讀 [Service Fabric 健康狀態模型](service-fabric-health-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-107">To understand health-related concepts, read more at [Service Fabric health model](service-fabric-health-introduction.md).</span></span>
> 
> 

<span data-ttu-id="a3b4c-108">系統健康狀態報告可讓您全盤掌握叢集和應用程式功能，並透過健康狀態標記問題。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-108">System health reports provide visibility into cluster and application functionality and flag issues through health.</span></span> <span data-ttu-id="a3b4c-109">系統健康狀態報告會針對應用程式和服務來確認實體是否已實作，以及從 Service Fabric 的角度來確認其是行為是否正確。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-109">For applications and services, system health reports verify that entities are implemented and are behaving correctly from the Service Fabric perspective.</span></span> <span data-ttu-id="a3b4c-110">報告並不會監控任何服務商務邏輯的健康情況，也不會偵測是否有無回應的處理程序。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-110">The reports do not provide any health monitoring of the business logic of the service or detection of hung processes.</span></span> <span data-ttu-id="a3b4c-111">使用者服務可使用其邏輯的特定資訊讓健康情況資料更豐富。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-111">User services can enrich the health data with information specific to their logic.</span></span>

> [!NOTE]
> <span data-ttu-id="a3b4c-112">監視程式健康狀態報告只有在系統元件建立實體「之後」才會顯示。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-112">Watchdogs health reports are visible only *after* the system components create an entity.</span></span> <span data-ttu-id="a3b4c-113">刪除實體時，健康狀態資料存放區會自動刪除所有與其相關聯的健康狀態報告。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-113">When an entity is deleted, the health store automatically deletes all health reports associated with it.</span></span> <span data-ttu-id="a3b4c-114">建立實體之新執行個體時的處理方式也一樣 (例如，建立新的具狀態持續性服務複本執行個體)。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-114">The same is true when a new instance of the entity is created (for example, a new stateful persisted service replica instance is created).</span></span> <span data-ttu-id="a3b4c-115">所有與舊執行個體相關聯的報告都會從存放區刪除及清除。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-115">All reports associated with the old instance are deleted and cleaned up from the store.</span></span>
> 
> 

<span data-ttu-id="a3b4c-116">系統元件報告將由來源識別，它會以 **System.** 前置詞做為開頭</span><span class="sxs-lookup"><span data-stu-id="a3b4c-116">The system component reports are identified by the source, which starts with the "**System.**"</span></span> <span data-ttu-id="a3b4c-117">。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-117">prefix.</span></span> <span data-ttu-id="a3b4c-118">看門狗不能對來源使用相同的前置詞，因為含有無效參數的報告會遭到拒絕。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-118">Watchdogs can't use the same prefix for their sources, as reports with invalid parameters are rejected.</span></span>
<span data-ttu-id="a3b4c-119">讓我們來看看部分系統報告，了解何者觸發了它們，以及如何修正它們所代表的可能問題。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-119">Let's look at some system reports to understand what triggers them and how to correct the possible issues they represent.</span></span>

> [!NOTE]
> <span data-ttu-id="a3b4c-120">Service Fabric 會繼續以感興趣的條件來新增報告，藉此改善叢集和應用程式中狀況的可見性。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-120">Service Fabric continues to add reports on conditions of interest that improve visibility into what is happening in the cluster and application.</span></span> <span data-ttu-id="a3b4c-121">更多詳細資料也可以增強現有的報告，有助於更快排解疑難問題。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-121">Existing reports can also be enhanced with more details to help troubleshoot the problem faster.</span></span>
> 
> 

## <a name="cluster-system-health-reports"></a><span data-ttu-id="a3b4c-122">叢集系統健康狀態報告</span><span class="sxs-lookup"><span data-stu-id="a3b4c-122">Cluster system health reports</span></span>
<span data-ttu-id="a3b4c-123">健康狀態資料存放區中會自動建立叢集健康狀態實體。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-123">The cluster health entity is created automatically in the health store.</span></span> <span data-ttu-id="a3b4c-124">如果一切正常運作，則不會有系統報告。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-124">If everything works properly, it doesn't have a system report.</span></span>

### <a name="neighborhood-loss"></a><span data-ttu-id="a3b4c-125">網路上的芳鄰遺失</span><span class="sxs-lookup"><span data-stu-id="a3b4c-125">Neighborhood loss</span></span>
<span data-ttu-id="a3b4c-126">**System.Federation** 偵測到網路上的芳鄰遺失時，即會回報錯誤。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-126">**System.Federation** reports an error when it detects a neighborhood loss.</span></span> <span data-ttu-id="a3b4c-127">報告來自各別的節點，且節點識別碼會包含於屬性名稱中。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-127">The report is from individual nodes, and the node ID is included in the property name.</span></span> <span data-ttu-id="a3b4c-128">如果整個 Service Fabric 環形中有一個網路上的芳鄰遺失，您通常可預期會產生兩個事件 (間距的兩端都會報告)。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-128">If one neighborhood is lost in the entire Service Fabric ring, you can typically expect two events (both sides of the gap report).</span></span> <span data-ttu-id="a3b4c-129">如果有多個網路上的芳鄰遺失，將會產生更多的事件。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-129">If more neighborhoods are lost, there are more events.</span></span>

<span data-ttu-id="a3b4c-130">報告會將全域租用逾時指定為存留時間。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-130">The report specifies the global lease timeout as the time to live.</span></span> <span data-ttu-id="a3b4c-131">只要條件仍在作用中，就會在每半個 TTL 期間重新傳送一次報告。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-131">The report is resent every half of the TTL duration for as long as the condition remains active.</span></span> <span data-ttu-id="a3b4c-132">事件到期時會自動移除。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-132">The event is automatically removed when it expires.</span></span> <span data-ttu-id="a3b4c-133">到期時移除的行為可確保正確地從健康狀態資料存放區清除報告，即使報告節點已關閉也不例外。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-133">Remove when expired behavior ensures that the report is cleaned up from the health store correctly, even if the reporting node is down.</span></span>

* <span data-ttu-id="a3b4c-134">**SourceId**：System.Federation</span><span class="sxs-lookup"><span data-stu-id="a3b4c-134">**SourceId**: System.Federation</span></span>
* <span data-ttu-id="a3b4c-135">**Property**：以 **Neighborhood** 為開頭且包含節點資訊</span><span class="sxs-lookup"><span data-stu-id="a3b4c-135">**Property**: Starts with **Neighborhood** and includes node information</span></span>
* <span data-ttu-id="a3b4c-136">**後續步驟**：調查網路上的芳鄰遺失的原因 (例如，檢查叢集節點之間的通訊)。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-136">**Next steps**: Investigate why the neighborhood is lost (for example, check the communication between cluster nodes).</span></span>

## <a name="node-system-health-reports"></a><span data-ttu-id="a3b4c-137">節點系統健康狀態報告</span><span class="sxs-lookup"><span data-stu-id="a3b4c-137">Node system health reports</span></span>
<span data-ttu-id="a3b4c-138">**System.FM**(代表容錯移轉管理員服務) 是管理叢集節點相關資訊的授權單位。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-138">**System.FM**, which represents the Failover Manager service, is the authority that manages information about cluster nodes.</span></span> <span data-ttu-id="a3b4c-139">每個節點都應該有一份來自 System.FM 的報告，以顯示其狀態。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-139">Each node should have one report from System.FM showing its state.</span></span> <span data-ttu-id="a3b4c-140">移除節點狀態時會移除節點實體 (請參閱 [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync))。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-140">The node entities are removed when the node state is removed (see [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).</span></span>

### <a name="node-updown"></a><span data-ttu-id="a3b4c-141">節點運作中/關閉</span><span class="sxs-lookup"><span data-stu-id="a3b4c-141">Node up/down</span></span>
<span data-ttu-id="a3b4c-142">當節點加入環形時，System.FM 會回報為 OK (節點已啟動且正在運作中)。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-142">System.FM reports as OK when the node joins the ring (it's up and running).</span></span> <span data-ttu-id="a3b4c-143">當節點離開環形時，則會回報錯誤 (節點已關閉進行升級，或只是發生故障)。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-143">It reports an error when the node departs the ring (it's down, either for upgrading or simply because it has failed).</span></span> <span data-ttu-id="a3b4c-144">由健康狀態資料存放區建置的健康狀態階層會根據 System.FM 節點報告，對部署的實體採取行動。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-144">The health hierarchy built by the health store takes action on deployed entities in correlation with System.FM node reports.</span></span> <span data-ttu-id="a3b4c-145">它會將節點視為所有已部署實體的虛擬父系。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-145">It considers the node a virtual parent of all deployed entities.</span></span> <span data-ttu-id="a3b4c-146">如果 System.FM 回報指出該節點已啟動，且其執行個體與實體相關聯的執行個體相同，則該節點上已部署的實體將會透過查詢公開。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-146">The deployed entities on that node are exposed through queries if the node is reported as up by System.FM, with the same instance as the instance associated with the entities.</span></span> <span data-ttu-id="a3b4c-147">當 System.FM 回報節點已關閉或重新啟動 (新執行個體) 時，健康狀態資料存放區會自動清除僅能存在於已關閉節點或先前的節點執行個體上的已部署實體。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-147">When System.FM reports that the node is down or restarted (a new instance), the health store automatically cleans up the deployed entities that can exist only on the down node or on the previous instance of the node.</span></span>

* <span data-ttu-id="a3b4c-148">**SourceId**：System.FM</span><span class="sxs-lookup"><span data-stu-id="a3b4c-148">**SourceId**: System.FM</span></span>
* <span data-ttu-id="a3b4c-149">**Property**：State</span><span class="sxs-lookup"><span data-stu-id="a3b4c-149">**Property**: State</span></span>
* <span data-ttu-id="a3b4c-150">**後續步驟**：如果節點已關閉來進行升級，應該會在升級後重新啟動。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-150">**Next steps**: If the node is down for an upgrade, it should come back up once it has been upgraded.</span></span> <span data-ttu-id="a3b4c-151">在這種情況下，健康情況應切換回 OK。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-151">In this case, the health state should switch back to OK.</span></span> <span data-ttu-id="a3b4c-152">如果節點沒有重新啟動或故障，就需要進一步調查問題。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-152">If the node doesn't come back or it fails, the problem needs more investigation.</span></span>

<span data-ttu-id="a3b4c-153">以下範例說明帶有 OK (代表節點已啟動) 健全狀況狀態的 System.FM 事件：</span><span class="sxs-lookup"><span data-stu-id="a3b4c-153">The following example shows the System.FM event with a health state of OK for node up:</span></span>

```powershell
PS C:\> Get-ServiceFabricNodeHealth  _Node_0

NodeName              : _Node_0
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 8
                        SentAt                : 7/14/2017 4:54:51 PM
                        ReceivedAt            : 7/14/2017 4:55:14 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```


### <a name="certificate-expiration"></a><span data-ttu-id="a3b4c-154">憑證到期</span><span class="sxs-lookup"><span data-stu-id="a3b4c-154">Certificate expiration</span></span>
<span data-ttu-id="a3b4c-155">**System.FabricNode** 會回報警告。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-155">**System.FabricNode** reports a warning when certificates used by the node are near expiration.</span></span> <span data-ttu-id="a3b4c-156">每個節點有三個憑證：**Certificate_cluster**、**Certificate_server** 及 **Certificate_default_client**。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-156">There are three certificates per node: **Certificate_cluster**, **Certificate_server**, and **Certificate_default_client**.</span></span> <span data-ttu-id="a3b4c-157">如果過期時間至少超過兩週，報告健康狀態就是 OK。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-157">When the expiration is at least two weeks away, the report health state is OK.</span></span> <span data-ttu-id="a3b4c-158">如果過期時間是在兩週內，則報告類型會是 Warning。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-158">When the expiration is within two weeks, the report type is a warning.</span></span> <span data-ttu-id="a3b4c-159">這些事件的 TTL 是無限制的，只有節點離開叢集時才會被移除。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-159">TTL of these events is infinite, and they are removed when a node leaves the cluster.</span></span>

* <span data-ttu-id="a3b4c-160">**SourceId**：System.FabricNode</span><span class="sxs-lookup"><span data-stu-id="a3b4c-160">**SourceId**: System.FabricNode</span></span>
* <span data-ttu-id="a3b4c-161">**Property**：以 **Certificate** 為開頭，且包含關於憑證類型的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="a3b4c-161">**Property**: Starts with **Certificate** and contains more information about the certificate type</span></span>
* <span data-ttu-id="a3b4c-162">**後續步驟**：如果憑證即將到期，請更新憑證。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-162">**Next steps**: Update the certificates if they are near expiration.</span></span>

### <a name="load-capacity-violation"></a><span data-ttu-id="a3b4c-163">負載容量違規</span><span class="sxs-lookup"><span data-stu-id="a3b4c-163">Load capacity violation</span></span>
<span data-ttu-id="a3b4c-164">當 Service Fabric Load Balancer 偵測到節點容量違規時，就會回報警告。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-164">The Service Fabric Load Balancer reports a warning when it detects a node capacity violation.</span></span>

* <span data-ttu-id="a3b4c-165">**SourceId**：System.PLB</span><span class="sxs-lookup"><span data-stu-id="a3b4c-165">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="a3b4c-166">**Property**：以 **Capacity** 為開頭</span><span class="sxs-lookup"><span data-stu-id="a3b4c-166">**Property**: Starts with **Capacity**</span></span>
* <span data-ttu-id="a3b4c-167">**後續步驟**：檢查提供的計量，並在節點上檢視目前容量。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-167">**Next steps**: Check provided metrics and view the current capacity on the node.</span></span>

## <a name="application-system-health-reports"></a><span data-ttu-id="a3b4c-168">應用程式系統健康狀態報告</span><span class="sxs-lookup"><span data-stu-id="a3b4c-168">Application system health reports</span></span>
<span data-ttu-id="a3b4c-169">**System.CM**(代表叢集管理員服務) 是管理應用程式相關資訊的授權單位。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-169">**System.CM**, which represents the Cluster Manager service, is the authority that manages information about an application.</span></span>

### <a name="state"></a><span data-ttu-id="a3b4c-170">State</span><span class="sxs-lookup"><span data-stu-id="a3b4c-170">State</span></span>
<span data-ttu-id="a3b4c-171">已建立或更新應用程式時，System.CM 會回報為 OK。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-171">System.CM reports as OK when the application has been created or updated.</span></span> <span data-ttu-id="a3b4c-172">已刪除應用程式時，它會通知健康狀態資料存放區，以便從存放區將它移除。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-172">It informs the health store when the application has been deleted, so that it can be removed from store.</span></span>

* <span data-ttu-id="a3b4c-173">**SourceId**：System.CM</span><span class="sxs-lookup"><span data-stu-id="a3b4c-173">**SourceId**: System.CM</span></span>
* <span data-ttu-id="a3b4c-174">**Property**：State</span><span class="sxs-lookup"><span data-stu-id="a3b4c-174">**Property**: State</span></span>
* <span data-ttu-id="a3b4c-175">**後續步驟**：如果已建立或更新應用程式，它就應該包含叢集管理員健康情況報告。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-175">**Next steps**: If the application has been created or updated, it should include the Cluster Manager health report.</span></span> <span data-ttu-id="a3b4c-176">否則，請發出查詢 (例如 PowerShell Cmdlet **Get-ServiceFabricApplication -ApplicationName *applicationName***) 以檢查應用程式狀態。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-176">Otherwise, check the state of the application by issuing a query (for example, the PowerShell cmdlet **Get-ServiceFabricApplication -ApplicationName *applicationName***).</span></span>

<span data-ttu-id="a3b4c-177">以下範例說明 **fabric:/WordCount** 應用程式上的狀態事件：</span><span class="sxs-lookup"><span data-stu-id="a3b4c-177">The following example shows the state event on the **fabric:/WordCount** application:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationHealth fabric:/WordCount -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics

ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Ok
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/14/2017 4:55:10 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
```

## <a name="service-system-health-reports"></a><span data-ttu-id="a3b4c-178">服務系統健康狀態報告</span><span class="sxs-lookup"><span data-stu-id="a3b4c-178">Service system health reports</span></span>
<span data-ttu-id="a3b4c-179">**System.FM**(代表容錯移轉管理員服務) 是管理服務相關資訊的授權單位。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-179">**System.FM**, which represents the Failover Manager service, is the authority that manages information about services.</span></span>

### <a name="state"></a><span data-ttu-id="a3b4c-180">State</span><span class="sxs-lookup"><span data-stu-id="a3b4c-180">State</span></span>
<span data-ttu-id="a3b4c-181">已建立服務時，System.FM 會回報為 OK。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-181">System.FM reports as OK when the service has been created.</span></span> <span data-ttu-id="a3b4c-182">已刪除服務時，它會從健康狀態資料存放區刪除實體。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-182">It deletes the entity from the health store when the service has been deleted.</span></span>

* <span data-ttu-id="a3b4c-183">**SourceId**：System.FM</span><span class="sxs-lookup"><span data-stu-id="a3b4c-183">**SourceId**: System.FM</span></span>
* <span data-ttu-id="a3b4c-184">**Property**：State</span><span class="sxs-lookup"><span data-stu-id="a3b4c-184">**Property**: State</span></span>

<span data-ttu-id="a3b4c-185">以下範例說明 **fabric:/WordCount/WordCountWebService** 服務上的狀態事件：</span><span class="sxs-lookup"><span data-stu-id="a3b4c-185">The following example shows the state event on the service **fabric:/WordCount/WordCountWebService**:</span></span>

```powershell
PS C:\> Get-ServiceFabricServiceHealth fabric:/WordCount/WordCountWebService -ExcludeHealthStatistics


ServiceName           : fabric:/WordCount/WordCountWebService
AggregatedHealthState : Ok
PartitionHealthStates : 
                        PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
                        AggregatedHealthState : Ok
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 14
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="service-correlation-error"></a><span data-ttu-id="a3b4c-186">服務相互關聯錯誤</span><span class="sxs-lookup"><span data-stu-id="a3b4c-186">Service correlation error</span></span>
<span data-ttu-id="a3b4c-187">**System.PLB** 會在偵測到更新要與其他服務相互關聯的服務建立同質鏈結時，就會回報錯誤。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-187">**System.PLB** reports an error when it detects that updating a service to be correlated with another service creates an affinity chain.</span></span> <span data-ttu-id="a3b4c-188">更新成功時，就會清除報告。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-188">The report is cleared when successful update happens.</span></span>

* <span data-ttu-id="a3b4c-189">**SourceId**：System.PLB</span><span class="sxs-lookup"><span data-stu-id="a3b4c-189">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="a3b4c-190">**屬性**︰ServiceDescription</span><span class="sxs-lookup"><span data-stu-id="a3b4c-190">**Property**: ServiceDescription</span></span>
* <span data-ttu-id="a3b4c-191">**後續步驟**：檢查相互關聯的服務說明。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-191">**Next steps**: Check the correlated service descriptions.</span></span>

## <a name="partition-system-health-reports"></a><span data-ttu-id="a3b4c-192">分割區系統健康狀態報告</span><span class="sxs-lookup"><span data-stu-id="a3b4c-192">Partition system health reports</span></span>
<span data-ttu-id="a3b4c-193">**System.FM**(代表容錯移轉管理員服務) 是管理服務分割區相關資訊的授權單位。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-193">**System.FM**, which represents the Failover Manager service, is the authority that manages information about service partitions.</span></span>

### <a name="state"></a><span data-ttu-id="a3b4c-194">State</span><span class="sxs-lookup"><span data-stu-id="a3b4c-194">State</span></span>
<span data-ttu-id="a3b4c-195">已建立分割區且其狀況良好時，System.FM 會回報為 OK。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-195">System.FM reports as OK when the partition has been created and is healthy.</span></span> <span data-ttu-id="a3b4c-196">刪除分割區時，它會從健康狀態資料存放區刪除實體。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-196">It deletes the entity from the health store when the partition is deleted.</span></span>

<span data-ttu-id="a3b4c-197">如果分割區低於最小複本計數，它會回報錯誤。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-197">If the partition is below the minimum replica count, it reports an error.</span></span> <span data-ttu-id="a3b4c-198">如果分割區高於最小複本計數，但低於目標複本計數，則會回報警告。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-198">If the partition is not below the minimum replica count, but it is below the target replica count, it reports a warning.</span></span> <span data-ttu-id="a3b4c-199">如果分割區處於仲裁遺失狀態，System.FM 會回報錯誤。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-199">If the partition is in quorum loss, System.FM reports an error.</span></span>

<span data-ttu-id="a3b4c-200">其他重要事件包括：當重新設定花費的時間比預期長，或者建置的時間比預期長，則會回報警告。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-200">Other important events include a warning when the reconfiguration takes longer than expected and when the build takes longer than expected.</span></span> <span data-ttu-id="a3b4c-201">建置和重新設定的預計時間可根據服務案來例設定。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-201">The expected times for the build and reconfiguration are configurable based on service scenarios.</span></span> <span data-ttu-id="a3b4c-202">例如，如果服務擁有 1 TB 的狀態 (例如 SQL Database)，則建置的時間會比只有少量狀態的服務更長。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-202">For example, if a service has a terabyte of state, such as SQL Database, the build takes longer than for a service with a small amount of state.</span></span>

* <span data-ttu-id="a3b4c-203">**SourceId**：System.FM</span><span class="sxs-lookup"><span data-stu-id="a3b4c-203">**SourceId**: System.FM</span></span>
* <span data-ttu-id="a3b4c-204">**Property**：State</span><span class="sxs-lookup"><span data-stu-id="a3b4c-204">**Property**: State</span></span>
* <span data-ttu-id="a3b4c-205">**後續步驟**：如果健康狀態不是 OK，有可能是因為部分複本並沒有正確建立、開啟、提升為主要或次要的複本。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-205">**Next steps**: If the health state is not OK, it's possible that some replicas have not been created, opened, or promoted to primary or secondary correctly.</span></span> <span data-ttu-id="a3b4c-206">在許多情況下，根本原因是在開啟或變更角色實作時發生服務錯誤。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-206">In many instances, the root cause is a service bug in the open or change-role implementation.</span></span>

<span data-ttu-id="a3b4c-207">以下範例顯示狀況良好的分割區：</span><span class="sxs-lookup"><span data-stu-id="a3b4c-207">The following example shows a healthy partition:</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountWebService | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics -ReplicasFilter None

PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
AggregatedHealthState : Ok
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 70
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Partition is healthy.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

<span data-ttu-id="a3b4c-208">以下範例顯示分割區的健全狀況低於目標複本計數。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-208">The following example shows the health of a partition that is below target replica count.</span></span> <span data-ttu-id="a3b4c-209">後續步驟是取得分割區說明，它將說明設定方式：**MinReplicaSetSize** 為三，**TargetReplicaSetSize** 為七。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-209">The next step is to get the partition description, which shows how it is configured: **MinReplicaSetSize** is three and **TargetReplicaSetSize** is seven.</span></span> <span data-ttu-id="a3b4c-210">接著取得叢集中的節點數：五。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-210">Then get the number of nodes in the cluster: five.</span></span> <span data-ttu-id="a3b4c-211">因此，在此情況下，無法放置兩個複本，因為複本的目標數目大於可用節點的數目。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-211">So in this case, two replicas can't be placed because the target number of replicas is higher than the number of nodes available.</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None -ExcludeHealthStatistics


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 123
                        SentAt                : 7/14/2017 4:55:39 PM
                        ReceivedAt            : 7/14/2017 4:55:44 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/S RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/P RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:55:44 PM, LastOk = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131445250939703027
                        SentAt                : 7/14/2017 4:58:13 PM
                        ReceivedAt            : 7/14/2017 4:58:14 PM
                        TTL                   : 00:01:05
                        Description           : The Load Balancer was unable to find a placement for one or more of the Service's Replicas:
                        Secondary replica could not be placed due to the following constraints and properties:  
                        TargetReplicaSetSize: 7
                        Placement Constraint: N/A
                        Parent Service: N/A
                        
                        Constraint Elimination Sequence:
                        Existing Secondary Replicas eliminated 4 possible node(s) for placement -- 1/5 node(s) remain.
                        Existing Primary Replica eliminated 1 possible node(s) for placement -- 0/5 node(s) remain.
                        
                        Nodes Eliminated By Constraints:
                        
                        Existing Secondary Replicas -- Nodes with Partition's Existing Secondary Replicas/Instances:
                        --
                        FaultDomain:fd:/4 NodeName:_Node_4 NodeType:NodeType4 UpgradeDomain:4 UpgradeDomain: ud:/4 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/3 NodeName:_Node_3 NodeType:NodeType3 UpgradeDomain:3 UpgradeDomain: ud:/3 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:56:14 PM, LastOk = 1/1/0001 12:00:00 AM

PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | select MinReplicaSetSize,TargetReplicaSetSize

MinReplicaSetSize TargetReplicaSetSize
----------------- --------------------
                2                    7                        

PS C:\> @(Get-ServiceFabricNode).Count
5
```

### <a name="replica-constraint-violation"></a><span data-ttu-id="a3b4c-212">複本條件約束違規</span><span class="sxs-lookup"><span data-stu-id="a3b4c-212">Replica constraint violation</span></span>
<span data-ttu-id="a3b4c-213">**System.PLB** 偵測到複本條件約束違規，且無法安置所有磁碟分割複本時，就會回報警告。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-213">**System.PLB** reports a warning if it detects a replica constraint violation and can't place all partition replicas.</span></span> <span data-ttu-id="a3b4c-214">報告詳細資料會顯示哪些條件約束和屬性導致無法安置複本。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-214">The report details show which constraints and properties prevent the replica placement.</span></span>

* <span data-ttu-id="a3b4c-215">**SourceId**：System.PLB</span><span class="sxs-lookup"><span data-stu-id="a3b4c-215">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="a3b4c-216">**Property**：以 **ReplicaConstraintViolation** 為開頭</span><span class="sxs-lookup"><span data-stu-id="a3b4c-216">**Property**: Starts with **ReplicaConstraintViolation**</span></span>

## <a name="replica-system-health-reports"></a><span data-ttu-id="a3b4c-217">複本系統健康狀態報告</span><span class="sxs-lookup"><span data-stu-id="a3b4c-217">Replica system health reports</span></span>
<span data-ttu-id="a3b4c-218">**System.RA**(代表重新設定代理程式元件) 是複本狀態的授權單位。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-218">**System.RA**, which represents the reconfiguration agent component, is the authority for the replica state.</span></span>

### <a name="state"></a><span data-ttu-id="a3b4c-219">State</span><span class="sxs-lookup"><span data-stu-id="a3b4c-219">State</span></span>
<span data-ttu-id="a3b4c-220">**System.RA** 會在複本建立後回報 OK。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-220">**System.RA** reports OK when the replica has been created.</span></span>

* <span data-ttu-id="a3b4c-221">**SourceId**：System.RA</span><span class="sxs-lookup"><span data-stu-id="a3b4c-221">**SourceId**: System.RA</span></span>
* <span data-ttu-id="a3b4c-222">**Property**：State</span><span class="sxs-lookup"><span data-stu-id="a3b4c-222">**Property**: State</span></span>

<span data-ttu-id="a3b4c-223">以下範例顯示狀況良好的複本：</span><span class="sxs-lookup"><span data-stu-id="a3b4c-223">The following example shows a healthy replica:</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422293118721
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131445248920273536
                        SentAt                : 7/14/2017 4:54:52 PM
                        ReceivedAt            : 7/14/2017 4:55:13 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_0
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:13 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="replica-open-status"></a><span data-ttu-id="a3b4c-224">複本開啟狀態</span><span class="sxs-lookup"><span data-stu-id="a3b4c-224">Replica open status</span></span>
<span data-ttu-id="a3b4c-225">叫用 API 呼叫時，此健康情況報告的說明會包含開始時間 (國際標準時間)。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-225">The description of this health report contains the start time (Coordinated Universal Time) when the API call was invoked.</span></span>

<span data-ttu-id="a3b4c-226">**System.RA** 會回報警告。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-226">**System.RA** reports a warning if the replica open takes longer than the configured period (default: 30 minutes).</span></span> <span data-ttu-id="a3b4c-227">如果 API 影響服務可用性，則報告發出速度就會快上許多 (可設定的間隔，預設值 30 秒)。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-227">If the API impacts service availability, the report is issued much faster (a configurable interval, with a default of 30 seconds).</span></span> <span data-ttu-id="a3b4c-228">測量的時間包含複寫器開啟及服務開啟所花費的時間。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-228">The time measured includes the time taken for the replicator open and the service open.</span></span> <span data-ttu-id="a3b4c-229">如果開啟完成，則屬性會變更為 OK。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-229">The property changes to OK if the open completes.</span></span>

* <span data-ttu-id="a3b4c-230">**SourceId**：System.RA</span><span class="sxs-lookup"><span data-stu-id="a3b4c-230">**SourceId**: System.RA</span></span>
* <span data-ttu-id="a3b4c-231">**Property**服務上的狀態事件： **ReplicaOpenStatus**</span><span class="sxs-lookup"><span data-stu-id="a3b4c-231">**Property**: **ReplicaOpenStatus**</span></span>
* <span data-ttu-id="a3b4c-232">**後續步驟**：如果健康狀態不是 OK，請調查複本開啟所花費的時間超過預期的原因。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-232">**Next steps**: If the health state is not OK, investigate why the replica open takes longer than expected.</span></span>

### <a name="slow-service-api-call"></a><span data-ttu-id="a3b4c-233">緩慢服務 API 呼叫</span><span class="sxs-lookup"><span data-stu-id="a3b4c-233">Slow service API call</span></span>
<span data-ttu-id="a3b4c-234">如果呼叫使用者服務程式碼所花費的時間超過設定的時間，**System.RAP** 和 **System.Replicator** 就會回報警告。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-234">**System.RAP** and **System.Replicator** report a warning if a call to the user service code takes longer than the configured time.</span></span> <span data-ttu-id="a3b4c-235">當呼叫完成時，警告就會被清除。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-235">The warning is cleared when the call completes.</span></span>

* <span data-ttu-id="a3b4c-236">**SourceId**：System.RAP 或 System.Replicator</span><span class="sxs-lookup"><span data-stu-id="a3b4c-236">**SourceId**: System.RAP or System.Replicator</span></span>
* <span data-ttu-id="a3b4c-237">**Property**：緩慢 API 的名稱。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-237">**Property**: The name of the slow API.</span></span> <span data-ttu-id="a3b4c-238">該說明會提供有關 API 擱置時間的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-238">The description provides more details about the time the API has been pending.</span></span>
* <span data-ttu-id="a3b4c-239">**後續步驟**：調查呼叫所花費時間超過預期的原因。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-239">**Next steps**: Investigate why the call takes longer than expected.</span></span>

<span data-ttu-id="a3b4c-240">下列範例說明處於仲裁遺失狀態的分割區，以及調查原因時需進行的步驟。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-240">The following example shows a partition in quorum loss, and the investigation steps done to figure out why.</span></span> <span data-ttu-id="a3b4c-241">若其中一個複本的健康狀態為 Warning，您就會取得其健康狀態。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-241">One of the replicas has a warning health state, so you get its health.</span></span> <span data-ttu-id="a3b4c-242">它會顯示服務作業所花費的時間超過預期 (由 System.RAP 回報的事件)。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-242">It shows that the service operation takes longer than expected, an event reported by System.RAP.</span></span> <span data-ttu-id="a3b4c-243">接收到此資訊之後，下一個步驟就是查看服務程式碼並詳加調查。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-243">After this information is received, the next step is to look at the service code and investigate there.</span></span> <span data-ttu-id="a3b4c-244">在此情況下，具狀態服務的 **RunAsync** 實作會擲回未處理的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-244">For this case, the **RunAsync** implementation of the stateful service throws an unhandled exception.</span></span> <span data-ttu-id="a3b4c-245">因為複本會進行回收，所以您可能不會看到任何處於警告狀態的複本。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-245">The replicas are recycling, so you may not see any replicas in the warning state.</span></span> <span data-ttu-id="a3b4c-246">您可以嘗試重新取得健康狀態，然後查看複本識別碼中是否有任何差異。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-246">You can retry getting the health state and look for any differences in the replica ID.</span></span> <span data-ttu-id="a3b4c-247">在某些情況下，重試可讓您得到一些線索。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-247">In certain cases, the retries can give you clues.</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
AggregatedHealthState : Error
UnhealthyEvaluations  :
                        Error event: SourceId='System.FM', Property='State'.

ReplicaHealthStates   :
                        ReplicaId             : 130743748372546446
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746168084332
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746195428808
                        AggregatedHealthState : Warning

                        ReplicaId             : 130743746195428807
                        AggregatedHealthState : Ok

HealthEvents          :
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Error
                        SequenceNumber        : 182
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:31 PM
                        TTL                   : Infinite
                        Description           : Partition is in quorum loss.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 4/24/2015 6:51:31 PM

PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful

PartitionId            : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
PartitionKind          : Int64Range
PartitionLowKey        : -9223372036854775808
PartitionHighKey       : 9223372036854775807
PartitionStatus        : InQuorumLoss
LastQuorumLossDuration : 00:00:13
MinReplicaSetSize      : 3
TargetReplicaSetSize   : 3
HealthState            : Error
DataLossNumber         : 130743746152927699
ConfigurationNumber    : 227633266688

PS C:\> Get-ServiceFabricReplica 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

ReplicaId           : 130743746195428808
ReplicaAddress      : PartitionId: 72a0fb3e-53ec-44f2-9983-2f272aca3e38, ReplicaId: 130743746195428808
ReplicaRole         : Primary
NodeName            : Node.3
ReplicaStatus       : Ready
LastInBuildDuration : 00:00:01
HealthState         : Warning

PS C:\> Get-ServiceFabricReplicaHealth 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
ReplicaId             : 130743746195428808
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.RAP', Property='ServiceOpenOperationDuration', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 130743756170185892
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:33 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/24/2015 7:00:33 PM

                        SourceId              : System.RAP
                        Property              : ServiceOpenOperationDuration
                        HealthState           : Warning
                        SequenceNumber        : 130743756399407044
                        SentAt                : 4/24/2015 7:00:39 PM
                        ReceivedAt            : 4/24/2015 7:00:59 PM
                        TTL                   : Infinite
                        Description           : Start Time (UTC): 2015-04-24 19:00:17.019
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Warning = 4/24/2015 7:00:59 PM
```

<span data-ttu-id="a3b4c-248">當您在偵錯工具中啟動錯誤的應用程式時，[診斷事件] 視窗會顯示從 RunAsync 所擲回的例外狀況：</span><span class="sxs-lookup"><span data-stu-id="a3b4c-248">When you start the faulty application under the debugger, the diagnostic events windows show the exception thrown from RunAsync:</span></span>

![Visual Studio 2015 診斷事件：RunAsync 在 fabric:/HelloWorldStatefulApplication 中失敗。][1]

<span data-ttu-id="a3b4c-250">Visual Studio 2015 診斷事件：RunAsync 在 **fabric:/HelloWorldStatefulApplication**中失敗。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-250">Visual Studio 2015 diagnostic events: RunAsync failure in **fabric:/HelloWorldStatefulApplication**.</span></span>

[1]: ./media/service-fabric-understand-and-troubleshoot-with-system-health-reports/servicefabric-health-vs-runasync-exception.png


### <a name="replication-queue-full"></a><span data-ttu-id="a3b4c-251">複寫佇列已滿</span><span class="sxs-lookup"><span data-stu-id="a3b4c-251">Replication queue full</span></span>
<span data-ttu-id="a3b4c-252">**System.Replicator** 會在複寫佇列已滿時回報警告。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-252">**System.Replicator** reports a warning when the replication queue is full.</span></span> <span data-ttu-id="a3b4c-253">在主要資料庫上，複寫佇列通常會因為一或多個次要複本太慢認可作業而排滿。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-253">On the primary, replication queue usually becomes full because one or more secondary replicas are slow to acknowledge operations.</span></span> <span data-ttu-id="a3b4c-254">在次要複本上，這通常是因為服務緩慢而無法套用作業所造成。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-254">On the secondary, this usually happens when the service is slow to apply the operations.</span></span> <span data-ttu-id="a3b4c-255">當佇列有空間時，警告就會被清除。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-255">The warning is cleared when the queue is no longer full.</span></span>

* <span data-ttu-id="a3b4c-256">**SourceId**：System.Replicator</span><span class="sxs-lookup"><span data-stu-id="a3b4c-256">**SourceId**: System.Replicator</span></span>
* <span data-ttu-id="a3b4c-257">**Property**：**PrimaryReplicationQueueStatus** 或 **SecondaryReplicationQueueStatus** (根據複本角色而定)</span><span class="sxs-lookup"><span data-stu-id="a3b4c-257">**Property**: **PrimaryReplicationQueueStatus** or **SecondaryReplicationQueueStatus**, depending on the replica role</span></span>

### <a name="slow-naming-operations"></a><span data-ttu-id="a3b4c-258">緩慢的命名作業</span><span class="sxs-lookup"><span data-stu-id="a3b4c-258">Slow Naming operations</span></span>
<span data-ttu-id="a3b4c-259">**System.NamingService** 會報告其主要複本的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-259">**System.NamingService** reports health on its primary replica when a Naming operation takes longer than acceptable.</span></span> <span data-ttu-id="a3b4c-260">命名作業的範例為 [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) 或 [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync)。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-260">Examples of Naming operations are [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) or [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync).</span></span> <span data-ttu-id="a3b4c-261">在 FabricClient 下可以找到更多方法，例如在[服務管理方法](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient)或[屬性管理方法](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient)底下。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-261">More methods can be found under FabricClient, for example under [service management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) or [property management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).</span></span>

> [!NOTE]
> <span data-ttu-id="a3b4c-262">命名服務會將服務名稱解析至叢集中的位置，並可讓使用者能夠管理服務名稱和屬性。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-262">The Naming service resolves service names to a location in the cluster and enables users to manage service names and properties.</span></span> <span data-ttu-id="a3b4c-263">它是 Service Fabric 資料分割保存的服務。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-263">It is a Service Fabric partitioned persisted service.</span></span> <span data-ttu-id="a3b4c-264">其中一個分割區代表「授權擁有者」，內含所有 Service Fabric 名稱和服務的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-264">One of the partitions represents the Authority Owner, which contains metadata about all Service Fabric names and services.</span></span> <span data-ttu-id="a3b4c-265">Service Fabric 名稱會對應至不同的資料分割 (稱為「名稱擁有者資料分割」)，讓服務可以擴充。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-265">The Service Fabric names are mapped to different partitions, called Name Owner partitions, so the service is extensible.</span></span> <span data-ttu-id="a3b4c-266">深入了解 [命名服務](service-fabric-architecture.md)。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-266">Read more about [Naming service](service-fabric-architecture.md).</span></span>
> 
> 

<span data-ttu-id="a3b4c-267">命名作業所花費的時間超出預期，在 *負責處理該作業的命名服務資料分割的主要複本*上，該作業會標幟警告報表。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-267">When a Naming operation takes longer than expected, the operation is flagged with a Warning report on the *primary replica of the Naming service partition that serves the operation*.</span></span> <span data-ttu-id="a3b4c-268">如果作業順利完成，就會清除警告。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-268">If the operation completes successfully, the Warning is cleared.</span></span> <span data-ttu-id="a3b4c-269">如果作業完成但發生錯誤，健全狀況報告會包含錯誤的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-269">If the operation completes with an error, the health report includes details about the error.</span></span>

* <span data-ttu-id="a3b4c-270">**SourceId**：System.NamingService</span><span class="sxs-lookup"><span data-stu-id="a3b4c-270">**SourceId**: System.NamingService</span></span>
* <span data-ttu-id="a3b4c-271">**Property**：以 **Duration_** 前置詞開始，識別緩慢作業和套用該作業的 Service Fabric 名稱。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-271">**Property**: Starts with prefix **Duration_** and identifies the slow operation and the Service Fabric name on which the operation is applied.</span></span> <span data-ttu-id="a3b4c-272">例如，如果在名稱網狀架構建立 /MyApp/MyService 服務花太多時間，其 Property 就是 Duration_AOCreateService.fabric:/MyApp/MyService。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-272">For example, if create service at name fabric:/MyApp/MyService takes too long, the property is Duration_AOCreateService.fabric:/MyApp/MyService.</span></span> <span data-ttu-id="a3b4c-273">AO 指向這個名稱和作業的命名資料分割的角色。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-273">AO points to the role of the Naming partition for this name and operation.</span></span>
* <span data-ttu-id="a3b4c-274">**後續步驟**︰檢查命名作業失敗的原因。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-274">**Next steps**: Check why the Naming operation fails.</span></span> <span data-ttu-id="a3b4c-275">每個作業都可能有不同的根本原因。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-275">Each operation can have different root causes.</span></span> <span data-ttu-id="a3b4c-276">例如，由於服務程式碼中的使用者錯誤造成節點上的應用程式主機持續當機，使刪除服務會卡在節點上。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-276">For example, delete service may be stuck on a node because the application host keeps crashing on a node due to a user bug in the service code.</span></span>

<span data-ttu-id="a3b4c-277">以下範例顯示一個建立服務作業。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-277">The following example shows a create service operation.</span></span> <span data-ttu-id="a3b4c-278">作業所花費的時間超過設定的期間。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-278">The operation took longer than the configured duration.</span></span> <span data-ttu-id="a3b4c-279">AO 重試，並將工作傳送到 NO。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-279">AO retries and sends work to NO.</span></span> <span data-ttu-id="a3b4c-280">NO 逾時完成最後一個作業。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-280">NO completed the last operation with Timeout.</span></span> <span data-ttu-id="a3b4c-281">在此情況中，AO 和 NO 角色有相同的主要複本。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-281">In this case, the same replica is primary for both the AO and NO roles.</span></span>

```powershell
PartitionId           : 00000000-0000-0000-0000-000000001000
ReplicaId             : 131064359253133577
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.NamingService', Property='Duration_AOCreateService.fabric:/MyApp/MyService', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131064359308715535
                        SentAt                : 4/29/2016 8:38:50 PM
                        ReceivedAt            : 4/29/2016 8:39:08 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 4/29/2016 8:39:08 PM, LastWarning = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_AOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064359526778775
                        SentAt                : 4/29/2016 8:39:12 PM
                        ReceivedAt            : 4/29/2016 8:39:38 PM
                        TTL                   : 00:05:00
                        Description           : The AOCreateService started at 2016-04-29 20:39:08.677 is taking longer than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_NOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064360657607311
                        SentAt                : 4/29/2016 8:41:05 PM
                        ReceivedAt            : 4/29/2016 8:41:08 PM
                        TTL                   : 00:00:15
                        Description           : The NOCreateService started at 2016-04-29 20:39:08.689 completed with FABRIC_E_TIMEOUT in more than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM
```

## <a name="deployedapplication-system-health-reports"></a><span data-ttu-id="a3b4c-282">DeployedApplication 系統健康狀態報告</span><span class="sxs-lookup"><span data-stu-id="a3b4c-282">DeployedApplication system health reports</span></span>
<span data-ttu-id="a3b4c-283">**System.Hosting** 是已部署實體的授權單位。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-283">**System.Hosting** is the authority on deployed entities.</span></span>

### <a name="activation"></a><span data-ttu-id="a3b4c-284">啟用</span><span class="sxs-lookup"><span data-stu-id="a3b4c-284">Activation</span></span>
<span data-ttu-id="a3b4c-285">當應用程式在節點上成功啟用時，System.Hosting 會回報為 OK。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-285">System.Hosting reports as OK when an application has been successfully activated on the node.</span></span> <span data-ttu-id="a3b4c-286">否則，它會報告錯誤。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-286">Otherwise, it reports an error.</span></span>

* <span data-ttu-id="a3b4c-287">**SourceId**：System.Hosting</span><span class="sxs-lookup"><span data-stu-id="a3b4c-287">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="a3b4c-288">**Property**：Activation，包括首度發行版本</span><span class="sxs-lookup"><span data-stu-id="a3b4c-288">**Property**: Activation, including the rollout version</span></span>
* <span data-ttu-id="a3b4c-289">**後續步驟**：如果應用程式的狀況不佳，請調查啟用失敗的原因。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-289">**Next steps**: If the application is unhealthy, investigate why the activation failed.</span></span>

<span data-ttu-id="a3b4c-290">以下範例顯示成功啟用的情況：</span><span class="sxs-lookup"><span data-stu-id="a3b4c-290">The following example shows successful activation:</span></span>

```powershell
PS C:\> Get-ServiceFabricDeployedApplicationHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ExcludeHealthStatistics

ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_1
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_1
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131445249083836329
                                     SentAt                : 7/14/2017 4:55:08 PM
                                     ReceivedAt            : 7/14/2017 4:55:14 PM
                                     TTL                   : Infinite
                                     Description           : The application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a><span data-ttu-id="a3b4c-291">下載</span><span class="sxs-lookup"><span data-stu-id="a3b4c-291">Download</span></span>
<span data-ttu-id="a3b4c-292">**System.Hosting** 會回報錯誤。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-292">**System.Hosting** reports an error if the application package download fails.</span></span>

* <span data-ttu-id="a3b4c-293">**SourceId**：System.Hosting</span><span class="sxs-lookup"><span data-stu-id="a3b4c-293">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="a3b4c-294">**Property**：**Download:*RolloutVersion***</span><span class="sxs-lookup"><span data-stu-id="a3b4c-294">**Property**: **Download:*RolloutVersion***</span></span>
* <span data-ttu-id="a3b4c-295">**後續步驟**：調查節點上下載失敗的原因。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-295">**Next steps**: Investigate why the download failed on the node.</span></span>

## <a name="deployedservicepackage-system-health-reports"></a><span data-ttu-id="a3b4c-296">DeployedServicePackage 系統健康狀態報告</span><span class="sxs-lookup"><span data-stu-id="a3b4c-296">DeployedServicePackage system health reports</span></span>
<span data-ttu-id="a3b4c-297">**System.Hosting** 是已部署實體的授權單位。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-297">**System.Hosting** is the authority on deployed entities.</span></span>

### <a name="service-package-activation"></a><span data-ttu-id="a3b4c-298">服務封裝啟用</span><span class="sxs-lookup"><span data-stu-id="a3b4c-298">Service package activation</span></span>
<span data-ttu-id="a3b4c-299">如果節點上的服務封裝成功啟用，System.Hosting 會回報為 OK。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-299">System.Hosting reports as OK if the service package activation on the node is successful.</span></span> <span data-ttu-id="a3b4c-300">否則，它會報告錯誤。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-300">Otherwise, it reports an error.</span></span>

* <span data-ttu-id="a3b4c-301">**SourceId**：System.Hosting</span><span class="sxs-lookup"><span data-stu-id="a3b4c-301">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="a3b4c-302">**Property**：Activation</span><span class="sxs-lookup"><span data-stu-id="a3b4c-302">**Property**: Activation</span></span>
* <span data-ttu-id="a3b4c-303">**後續步驟**：調查啟用失敗的原因。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-303">**Next steps**: Investigate why the activation failed.</span></span>

### <a name="code-package-activation"></a><span data-ttu-id="a3b4c-304">程式碼封裝啟用</span><span class="sxs-lookup"><span data-stu-id="a3b4c-304">Code package activation</span></span>
<span data-ttu-id="a3b4c-305">**System.Hosting** 會針對每個程式碼封裝回報 OK。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-305">**System.Hosting** reports as OK for each code package if the activation is successful.</span></span> <span data-ttu-id="a3b4c-306">如果啟用失敗，它會依設定回報警告。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-306">If the activation fails, it reports a warning as configured.</span></span> <span data-ttu-id="a3b4c-307">如果 **CodePackage** 無法啟用，或者因為錯誤數超過 **CodePackageHealthErrorThreshold** 的設定而結束，則 Hosting 會回報錯誤。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-307">If **CodePackage** fails to activate or terminates with an error greater than the configured **CodePackageHealthErrorThreshold**, hosting reports an error.</span></span> <span data-ttu-id="a3b4c-308">如果服務封裝包含多個程式碼封裝，就會針對每個封裝產生啟用報告。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-308">If a service package contains multiple code packages, an activation report is generated for each one.</span></span>

* <span data-ttu-id="a3b4c-309">**SourceId**：System.Hosting</span><span class="sxs-lookup"><span data-stu-id="a3b4c-309">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="a3b4c-310">**Property**：使用前置詞 **CodePackageActivation**，並以 **CodePackageActivation:*CodePackageName*:*SetupEntryPoint/EntryPoint*** 形式 (例如 **CodePackageActivation:Code:SetupEntryPoint**) 包含程式碼封裝的名稱和進入點</span><span class="sxs-lookup"><span data-stu-id="a3b4c-310">**Property**: Uses the prefix **CodePackageActivation** and contains the name of the code package and the entry point as **CodePackageActivation:*CodePackageName*:*SetupEntryPoint/EntryPoint*** (for example, **CodePackageActivation:Code:SetupEntryPoint**)</span></span>

### <a name="service-type-registration"></a><span data-ttu-id="a3b4c-311">服務類型註冊</span><span class="sxs-lookup"><span data-stu-id="a3b4c-311">Service type registration</span></span>
<span data-ttu-id="a3b4c-312">**System.Hosting** 會回報為 OK。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-312">**System.Hosting** reports as OK if the service type has been registered successfully.</span></span> <span data-ttu-id="a3b4c-313">如果註冊未及時完成 (使用 **ServiceTypeRegistrationTimeout**來設定)，則會回報錯誤。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-313">It reports an error if the registration wasn't done in time (as configured by using **ServiceTypeRegistrationTimeout**).</span></span> <span data-ttu-id="a3b4c-314">如果執行階段已關閉，則會從節點取消註冊服務類型，且主機會回報警告。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-314">If the runtime is closed, the service type is unregistered from the node and Hosting reports a warning.</span></span>

* <span data-ttu-id="a3b4c-315">**SourceId**：System.Hosting</span><span class="sxs-lookup"><span data-stu-id="a3b4c-315">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="a3b4c-316">**Property**：使用前置詞 **ServiceTypeRegistration**，並包含服務類型名稱 (例如，**ServiceTypeRegistration:FileStoreServiceType**)</span><span class="sxs-lookup"><span data-stu-id="a3b4c-316">**Property**: Uses the prefix **ServiceTypeRegistration** and contains the service type name (for example, **ServiceTypeRegistration:FileStoreServiceType**)</span></span>

<span data-ttu-id="a3b4c-317">以下顯示顯示狀況良好的已部署服務封裝：</span><span class="sxs-lookup"><span data-stu-id="a3b4c-317">The following example shows a healthy deployed service package:</span></span>

```powershell
PS C:\> Get-ServiceFabricDeployedServicePackageHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_1
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131445249084026346
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : The ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131445249084306362
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : The CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131445249088096842
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : The ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a><span data-ttu-id="a3b4c-318">下載</span><span class="sxs-lookup"><span data-stu-id="a3b4c-318">Download</span></span>
<span data-ttu-id="a3b4c-319">**System.Hosting** 會回報錯誤。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-319">**System.Hosting** reports an error if the service package download fails.</span></span>

* <span data-ttu-id="a3b4c-320">**SourceId**：System.Hosting</span><span class="sxs-lookup"><span data-stu-id="a3b4c-320">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="a3b4c-321">**Property**：**Download:*RolloutVersion***</span><span class="sxs-lookup"><span data-stu-id="a3b4c-321">**Property**: **Download:*RolloutVersion***</span></span>
* <span data-ttu-id="a3b4c-322">**後續步驟**：調查節點上下載失敗的原因。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-322">**Next steps**: Investigate why the download failed on the node.</span></span>

### <a name="upgrade-validation"></a><span data-ttu-id="a3b4c-323">升級驗證</span><span class="sxs-lookup"><span data-stu-id="a3b4c-323">Upgrade validation</span></span>
<span data-ttu-id="a3b4c-324">**System.Hosting** 會回報錯誤。</span><span class="sxs-lookup"><span data-stu-id="a3b4c-324">**System.Hosting** reports an error if validation during the upgrade fails or if the upgrade fails on the node.</span></span>

* <span data-ttu-id="a3b4c-325">**SourceId**：System.Hosting</span><span class="sxs-lookup"><span data-stu-id="a3b4c-325">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="a3b4c-326">**Property**：使用 **FabricUpgradeValidation** 前置詞，並包含升級版本</span><span class="sxs-lookup"><span data-stu-id="a3b4c-326">**Property**: Uses the prefix **FabricUpgradeValidation** and contains the upgrade version</span></span>
* <span data-ttu-id="a3b4c-327">**Description**：指出發生的錯誤</span><span class="sxs-lookup"><span data-stu-id="a3b4c-327">**Description**: Points to the error encountered</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3b4c-328">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a3b4c-328">Next steps</span></span>
[<span data-ttu-id="a3b4c-329">檢視 Service Fabric 健康狀態報告</span><span class="sxs-lookup"><span data-stu-id="a3b4c-329">View Service Fabric health reports</span></span>](service-fabric-view-entities-aggregated-health.md)

[<span data-ttu-id="a3b4c-330">如何回報和檢查服務健全狀況</span><span class="sxs-lookup"><span data-stu-id="a3b4c-330">How to report and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="a3b4c-331">在本機上監視及診斷服務</span><span class="sxs-lookup"><span data-stu-id="a3b4c-331">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="a3b4c-332">Service Fabric 應用程式升級</span><span class="sxs-lookup"><span data-stu-id="a3b4c-332">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

