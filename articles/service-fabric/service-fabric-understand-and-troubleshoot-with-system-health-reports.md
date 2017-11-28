---
title: "系統健康情況報告與 aaaTroubleshoot |Microsoft 文件"
description: "描述 Azure Service Fabric 元件和其使用方式所傳送的疑難排解叢集或應用程式問題的 hello 健康情況報告。"
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
ms.openlocfilehash: c77a6cdd0440ce5d354cd8760f40151f674a3529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-system-health-reports-tootroubleshoot"></a><span data-ttu-id="3764f-103">使用系統健全狀況報表 tootroubleshoot</span><span class="sxs-lookup"><span data-stu-id="3764f-103">Use system health reports tootroubleshoot</span></span>
<span data-ttu-id="3764f-104">Azure Service Fabric 元件報表 hello 現成 hello 叢集中的所有實體。</span><span class="sxs-lookup"><span data-stu-id="3764f-104">Azure Service Fabric components report out of hello box on all entities in hello cluster.</span></span> <span data-ttu-id="3764f-105">hello[健全狀況存放區](service-fabric-health-introduction.md#health-store)會建立和刪除 hello 系統報表基礎的實體。</span><span class="sxs-lookup"><span data-stu-id="3764f-105">hello [health store](service-fabric-health-introduction.md#health-store) creates and deletes entities based on hello system reports.</span></span> <span data-ttu-id="3764f-106">它也會將這些實體組織為階層以擷取實體的互動。</span><span class="sxs-lookup"><span data-stu-id="3764f-106">It also organizes them in a hierarchy that captures entity interactions.</span></span>

> [!NOTE]
> <span data-ttu-id="3764f-107">toounderstand 健全狀況相關的概念，深入了解在[服務網狀架構健全狀況模型](service-fabric-health-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="3764f-107">toounderstand health-related concepts, read more at [Service Fabric health model](service-fabric-health-introduction.md).</span></span>
> 
> 

<span data-ttu-id="3764f-108">系統健康狀態報告可讓您全盤掌握叢集和應用程式功能，並透過健康狀態標記問題。</span><span class="sxs-lookup"><span data-stu-id="3764f-108">System health reports provide visibility into cluster and application functionality and flag issues through health.</span></span> <span data-ttu-id="3764f-109">應用程式和服務，實體實作，且從 hello Service Fabric 觀點來看運作正確，請確認系統健康情況報告。</span><span class="sxs-lookup"><span data-stu-id="3764f-109">For applications and services, system health reports verify that entities are implemented and are behaving correctly from hello Service Fabric perspective.</span></span> <span data-ttu-id="3764f-110">hello 報表沒有提供任何顯示的 hello 服務 hello 商務邏輯和偵測無回應的處理程序的健全狀況監視。</span><span class="sxs-lookup"><span data-stu-id="3764f-110">hello reports do not provide any health monitoring of hello business logic of hello service or detection of hung processes.</span></span> <span data-ttu-id="3764f-111">使用者服務可以擴充資訊特定 tootheir 邏輯與 hello 健全狀況資料。</span><span class="sxs-lookup"><span data-stu-id="3764f-111">User services can enrich hello health data with information specific tootheir logic.</span></span>

> [!NOTE]
> <span data-ttu-id="3764f-112">只會顯示 watchdogs 健康情況報告*之後*hello 系統元件建立實體。</span><span class="sxs-lookup"><span data-stu-id="3764f-112">Watchdogs health reports are visible only *after* hello system components create an entity.</span></span> <span data-ttu-id="3764f-113">刪除實體時，hello 健全狀況存放區會自動刪除所有與其相關聯的健康情況報告。</span><span class="sxs-lookup"><span data-stu-id="3764f-113">When an entity is deleted, hello health store automatically deletes all health reports associated with it.</span></span> <span data-ttu-id="3764f-114">hello 也是如此建立 hello 實體的新執行個體時 （例如，建立新的可設定狀態的持續性的服務複本執行個體）。</span><span class="sxs-lookup"><span data-stu-id="3764f-114">hello same is true when a new instance of hello entity is created (for example, a new stateful persisted service replica instance is created).</span></span> <span data-ttu-id="3764f-115">刪除或清除從 hello 存放區與 hello 舊的執行個體相關聯的所有報表。</span><span class="sxs-lookup"><span data-stu-id="3764f-115">All reports associated with hello old instance are deleted and cleaned up from hello store.</span></span>
> 
> 

<span data-ttu-id="3764f-116">hello 系統元件報告，藉以 hello 來源，以 hello 開頭"**系統。**"</span><span class="sxs-lookup"><span data-stu-id="3764f-116">hello system component reports are identified by hello source, which starts with hello "**System.**"</span></span> <span data-ttu-id="3764f-117">。</span><span class="sxs-lookup"><span data-stu-id="3764f-117">prefix.</span></span> <span data-ttu-id="3764f-118">Watchdogs 無法使用相同的前置詞及其來源，hello，因為報表內含無效的參數會遭到拒絕。</span><span class="sxs-lookup"><span data-stu-id="3764f-118">Watchdogs can't use hello same prefix for their sources, as reports with invalid parameters are rejected.</span></span>
<span data-ttu-id="3764f-119">讓我們來看一些系統回報 toounderstand 觸發它們，並它們代表如何 toocorrect hello 可能的問題。</span><span class="sxs-lookup"><span data-stu-id="3764f-119">Let's look at some system reports toounderstand what triggers them and how toocorrect hello possible issues they represent.</span></span>

> [!NOTE]
> <span data-ttu-id="3764f-120">Service Fabric 會繼續 tooadd 報表感興趣的改善掌握 hello 叢集和應用程式中發生的狀況。</span><span class="sxs-lookup"><span data-stu-id="3764f-120">Service Fabric continues tooadd reports on conditions of interest that improve visibility into what is happening in hello cluster and application.</span></span> <span data-ttu-id="3764f-121">也可以增強現有的報表含有詳細 toohelp hello 對問題進行疑難排解更快。</span><span class="sxs-lookup"><span data-stu-id="3764f-121">Existing reports can also be enhanced with more details toohelp troubleshoot hello problem faster.</span></span>
> 
> 

## <a name="cluster-system-health-reports"></a><span data-ttu-id="3764f-122">叢集系統健康狀態報告</span><span class="sxs-lookup"><span data-stu-id="3764f-122">Cluster system health reports</span></span>
<span data-ttu-id="3764f-123">hello health store 中自動建立 hello 叢集健全狀況的實體。</span><span class="sxs-lookup"><span data-stu-id="3764f-123">hello cluster health entity is created automatically in hello health store.</span></span> <span data-ttu-id="3764f-124">如果一切正常運作，則不會有系統報告。</span><span class="sxs-lookup"><span data-stu-id="3764f-124">If everything works properly, it doesn't have a system report.</span></span>

### <a name="neighborhood-loss"></a><span data-ttu-id="3764f-125">網路上的芳鄰遺失</span><span class="sxs-lookup"><span data-stu-id="3764f-125">Neighborhood loss</span></span>
<span data-ttu-id="3764f-126">**System.Federation** 偵測到網路上的芳鄰遺失時，即會回報錯誤。</span><span class="sxs-lookup"><span data-stu-id="3764f-126">**System.Federation** reports an error when it detects a neighborhood loss.</span></span> <span data-ttu-id="3764f-127">hello 報表會從個別節點，而且 hello 節點識別碼會包含在 hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="3764f-127">hello report is from individual nodes, and hello node ID is included in hello property name.</span></span> <span data-ttu-id="3764f-128">如果 hello 整個 Service Fabric 環形將會遺失一個上的芳鄰，您通常可以預期兩個事件 （兩端 hello 間距報表）。</span><span class="sxs-lookup"><span data-stu-id="3764f-128">If one neighborhood is lost in hello entire Service Fabric ring, you can typically expect two events (both sides of hello gap report).</span></span> <span data-ttu-id="3764f-129">如果有多個網路上的芳鄰遺失，將會產生更多的事件。</span><span class="sxs-lookup"><span data-stu-id="3764f-129">If more neighborhoods are lost, there are more events.</span></span>

<span data-ttu-id="3764f-130">hello 報表指定 hello 時間 toolive hello 全域租用逾時。</span><span class="sxs-lookup"><span data-stu-id="3764f-130">hello report specifies hello global lease timeout as hello time toolive.</span></span> <span data-ttu-id="3764f-131">hello 報表重新傳送 hello TTL 持續時間的每個半只要 hello 條件維持使用中。</span><span class="sxs-lookup"><span data-stu-id="3764f-131">hello report is resent every half of hello TTL duration for as long as hello condition remains active.</span></span> <span data-ttu-id="3764f-132">到期時，會自動移除 hello 事件。</span><span class="sxs-lookup"><span data-stu-id="3764f-132">hello event is automatically removed when it expires.</span></span> <span data-ttu-id="3764f-133">卸除過期的行為可確保，hello 報表是從 hello health store 正確地清除，即使 hello reporting 節點已關閉。</span><span class="sxs-lookup"><span data-stu-id="3764f-133">Remove when expired behavior ensures that hello report is cleaned up from hello health store correctly, even if hello reporting node is down.</span></span>

* <span data-ttu-id="3764f-134">**SourceId**：System.Federation</span><span class="sxs-lookup"><span data-stu-id="3764f-134">**SourceId**: System.Federation</span></span>
* <span data-ttu-id="3764f-135">**Property**：以 **Neighborhood** 為開頭且包含節點資訊</span><span class="sxs-lookup"><span data-stu-id="3764f-135">**Property**: Starts with **Neighborhood** and includes node information</span></span>
* <span data-ttu-id="3764f-136">**後續步驟**： 調查 hello 上的芳鄰 為何遺失 （例如，叢集節點之間的核取 hello 通訊）。</span><span class="sxs-lookup"><span data-stu-id="3764f-136">**Next steps**: Investigate why hello neighborhood is lost (for example, check hello communication between cluster nodes).</span></span>

## <a name="node-system-health-reports"></a><span data-ttu-id="3764f-137">節點系統健康狀態報告</span><span class="sxs-lookup"><span data-stu-id="3764f-137">Node system health reports</span></span>
<span data-ttu-id="3764f-138">**System.FM**，這代表 hello Failover Manager service、 管理叢集節點的相關資訊的 hello 授權單位。</span><span class="sxs-lookup"><span data-stu-id="3764f-138">**System.FM**, which represents hello Failover Manager service, is hello authority that manages information about cluster nodes.</span></span> <span data-ttu-id="3764f-139">每個節點都應該有一份來自 System.FM 的報告，以顯示其狀態。</span><span class="sxs-lookup"><span data-stu-id="3764f-139">Each node should have one report from System.FM showing its state.</span></span> <span data-ttu-id="3764f-140">移除 hello 節點狀態時，會移除 hello 節點實體 (請參閱[RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync))。</span><span class="sxs-lookup"><span data-stu-id="3764f-140">hello node entities are removed when hello node state is removed (see [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).</span></span>

### <a name="node-updown"></a><span data-ttu-id="3764f-141">節點運作中/關閉</span><span class="sxs-lookup"><span data-stu-id="3764f-141">Node up/down</span></span>
<span data-ttu-id="3764f-142">Hello 節點加入 hello 信號 （已啟動並執行） 時，System.FM 會回報為 [確定]。</span><span class="sxs-lookup"><span data-stu-id="3764f-142">System.FM reports as OK when hello node joins hello ring (it's up and running).</span></span> <span data-ttu-id="3764f-143">Hello 節點貨車 hello 信號時，它會報告錯誤 (已關閉，請升級或只是因為它失敗)。</span><span class="sxs-lookup"><span data-stu-id="3764f-143">It reports an error when hello node departs hello ring (it's down, either for upgrading or simply because it has failed).</span></span> <span data-ttu-id="3764f-144">部署中的實體與 System.FM 節點報告相互關聯 hello 健全狀況存放區所建立的 hello 健全狀況階層會採取的動作。</span><span class="sxs-lookup"><span data-stu-id="3764f-144">hello health hierarchy built by hello health store takes action on deployed entities in correlation with System.FM node reports.</span></span> <span data-ttu-id="3764f-145">它會考慮 hello 節點虛擬已部署的所有實體的父系。</span><span class="sxs-lookup"><span data-stu-id="3764f-145">It considers hello node a virtual parent of all deployed entities.</span></span> <span data-ttu-id="3764f-146">如果 hello 節點報告為向上 System.FM，hello 與相同執行個體與 hello 與 hello 實體相關聯的執行個體，該節點上部署的 hello 實體會公開透過查詢。</span><span class="sxs-lookup"><span data-stu-id="3764f-146">hello deployed entities on that node are exposed through queries if hello node is reported as up by System.FM, with hello same instance as hello instance associated with hello entities.</span></span> <span data-ttu-id="3764f-147">當 System.FM 報告該 hello 節點已關閉或重新啟動 （的新執行個體） 時，hello 健全狀況存放區會自動清除在於只有 hello 節點關閉或 hello hello 節點的上一個執行個體上部署的 hello 實體。</span><span class="sxs-lookup"><span data-stu-id="3764f-147">When System.FM reports that hello node is down or restarted (a new instance), hello health store automatically cleans up hello deployed entities that can exist only on hello down node or on hello previous instance of hello node.</span></span>

* <span data-ttu-id="3764f-148">**SourceId**：System.FM</span><span class="sxs-lookup"><span data-stu-id="3764f-148">**SourceId**: System.FM</span></span>
* <span data-ttu-id="3764f-149">**Property**：State</span><span class="sxs-lookup"><span data-stu-id="3764f-149">**Property**: State</span></span>
* <span data-ttu-id="3764f-150">**後續步驟**： 如果 hello 節點已關閉升級，它應該恢復一旦已升級。</span><span class="sxs-lookup"><span data-stu-id="3764f-150">**Next steps**: If hello node is down for an upgrade, it should come back up once it has been upgraded.</span></span> <span data-ttu-id="3764f-151">在此情況下，hello 健全狀況狀態應該切換後 tooOK。</span><span class="sxs-lookup"><span data-stu-id="3764f-151">In this case, hello health state should switch back tooOK.</span></span> <span data-ttu-id="3764f-152">如果 hello 節點不會再次發生，否則便會失敗，hello 問題，需要較多調查。</span><span class="sxs-lookup"><span data-stu-id="3764f-152">If hello node doesn't come back or it fails, hello problem needs more investigation.</span></span>

<span data-ttu-id="3764f-153">hello 下例健全狀況狀態為 [確定] 節點的 hello System.FM 事件一同顯示：</span><span class="sxs-lookup"><span data-stu-id="3764f-153">hello following example shows hello System.FM event with a health state of OK for node up:</span></span>

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


### <a name="certificate-expiration"></a><span data-ttu-id="3764f-154">憑證到期</span><span class="sxs-lookup"><span data-stu-id="3764f-154">Certificate expiration</span></span>
<span data-ttu-id="3764f-155">**System.FabricNode** hello 節點所使用的憑證即將到期時，回報警告。</span><span class="sxs-lookup"><span data-stu-id="3764f-155">**System.FabricNode** reports a warning when certificates used by hello node are near expiration.</span></span> <span data-ttu-id="3764f-156">每個節點有三個憑證：**Certificate_cluster**、**Certificate_server** 及 **Certificate_default_client**。</span><span class="sxs-lookup"><span data-stu-id="3764f-156">There are three certificates per node: **Certificate_cluster**, **Certificate_server**, and **Certificate_default_client**.</span></span> <span data-ttu-id="3764f-157">至少兩週後 hello 到期時，hello 報表健全狀況狀態是 [確定]。</span><span class="sxs-lookup"><span data-stu-id="3764f-157">When hello expiration is at least two weeks away, hello report health state is OK.</span></span> <span data-ttu-id="3764f-158">在兩週內 hello 到期時，hello 報表類型是一個警告。</span><span class="sxs-lookup"><span data-stu-id="3764f-158">When hello expiration is within two weeks, hello report type is a warning.</span></span> <span data-ttu-id="3764f-159">這些事件的 TTL 是無限的以及當節點離開叢集 hello 中予以移除。</span><span class="sxs-lookup"><span data-stu-id="3764f-159">TTL of these events is infinite, and they are removed when a node leaves hello cluster.</span></span>

* <span data-ttu-id="3764f-160">**SourceId**：System.FabricNode</span><span class="sxs-lookup"><span data-stu-id="3764f-160">**SourceId**: System.FabricNode</span></span>
* <span data-ttu-id="3764f-161">**屬性**： 開頭**憑證**和包含 hello 憑證類型的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="3764f-161">**Property**: Starts with **Certificate** and contains more information about hello certificate type</span></span>
* <span data-ttu-id="3764f-162">**後續步驟**： 更新 hello 憑證是否即將到期。</span><span class="sxs-lookup"><span data-stu-id="3764f-162">**Next steps**: Update hello certificates if they are near expiration.</span></span>

### <a name="load-capacity-violation"></a><span data-ttu-id="3764f-163">負載容量違規</span><span class="sxs-lookup"><span data-stu-id="3764f-163">Load capacity violation</span></span>
<span data-ttu-id="3764f-164">hello Service Fabric 負載平衡器會回報警告。 當它偵測到節點容量違規。</span><span class="sxs-lookup"><span data-stu-id="3764f-164">hello Service Fabric Load Balancer reports a warning when it detects a node capacity violation.</span></span>

* <span data-ttu-id="3764f-165">**SourceId**：System.PLB</span><span class="sxs-lookup"><span data-stu-id="3764f-165">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="3764f-166">**Property**：以 **Capacity** 為開頭</span><span class="sxs-lookup"><span data-stu-id="3764f-166">**Property**: Starts with **Capacity**</span></span>
* <span data-ttu-id="3764f-167">**後續步驟**: hello 節點上檢查所提供的度量和檢視 hello 目前容量。</span><span class="sxs-lookup"><span data-stu-id="3764f-167">**Next steps**: Check provided metrics and view hello current capacity on hello node.</span></span>

## <a name="application-system-health-reports"></a><span data-ttu-id="3764f-168">應用程式系統健康狀態報告</span><span class="sxs-lookup"><span data-stu-id="3764f-168">Application system health reports</span></span>
<span data-ttu-id="3764f-169">**System.CM**，這代表 hello 叢集管理員服務，是 hello 授權管理應用程式的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="3764f-169">**System.CM**, which represents hello Cluster Manager service, is hello authority that manages information about an application.</span></span>

### <a name="state"></a><span data-ttu-id="3764f-170">State</span><span class="sxs-lookup"><span data-stu-id="3764f-170">State</span></span>
<span data-ttu-id="3764f-171">System.CM 報告為 [確定] 時已建立或更新 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3764f-171">System.CM reports as OK when hello application has been created or updated.</span></span> <span data-ttu-id="3764f-172">它會通知 hello 健全狀況存放區刪除 hello 應用程式後，使它可以從存放區中移除。</span><span class="sxs-lookup"><span data-stu-id="3764f-172">It informs hello health store when hello application has been deleted, so that it can be removed from store.</span></span>

* <span data-ttu-id="3764f-173">**SourceId**：System.CM</span><span class="sxs-lookup"><span data-stu-id="3764f-173">**SourceId**: System.CM</span></span>
* <span data-ttu-id="3764f-174">**Property**：State</span><span class="sxs-lookup"><span data-stu-id="3764f-174">**Property**: State</span></span>
* <span data-ttu-id="3764f-175">**後續步驟**： 如果已建立或更新 hello 應用程式，它應該包含 hello 叢集管理員健康情況報告。</span><span class="sxs-lookup"><span data-stu-id="3764f-175">**Next steps**: If hello application has been created or updated, it should include hello Cluster Manager health report.</span></span> <span data-ttu-id="3764f-176">否則，請檢查 hello hello 應用程式狀態，藉由發出查詢 (例如，hello PowerShell cmdlet **Get ServiceFabricApplication ApplicationName *applicationName***)。</span><span class="sxs-lookup"><span data-stu-id="3764f-176">Otherwise, check hello state of hello application by issuing a query (for example, hello PowerShell cmdlet **Get-ServiceFabricApplication -ApplicationName *applicationName***).</span></span>

<span data-ttu-id="3764f-177">hello 下列範例示範 hello 狀態事件在 hello **fabric: / WordCount**應用程式：</span><span class="sxs-lookup"><span data-stu-id="3764f-177">hello following example shows hello state event on hello **fabric:/WordCount** application:</span></span>

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

## <a name="service-system-health-reports"></a><span data-ttu-id="3764f-178">服務系統健康狀態報告</span><span class="sxs-lookup"><span data-stu-id="3764f-178">Service system health reports</span></span>
<span data-ttu-id="3764f-179">**System.FM**，這代表 hello Failover Manager service、 管理服務的相關資訊的 hello 授權單位。</span><span class="sxs-lookup"><span data-stu-id="3764f-179">**System.FM**, which represents hello Failover Manager service, is hello authority that manages information about services.</span></span>

### <a name="state"></a><span data-ttu-id="3764f-180">State</span><span class="sxs-lookup"><span data-stu-id="3764f-180">State</span></span>
<span data-ttu-id="3764f-181">System.FM 做為 [確定] 時，回報 hello 服務已經建立完成。</span><span class="sxs-lookup"><span data-stu-id="3764f-181">System.FM reports as OK when hello service has been created.</span></span> <span data-ttu-id="3764f-182">Hello 服務已被刪除時，從 hello health store 刪除 hello 實體。</span><span class="sxs-lookup"><span data-stu-id="3764f-182">It deletes hello entity from hello health store when hello service has been deleted.</span></span>

* <span data-ttu-id="3764f-183">**SourceId**：System.FM</span><span class="sxs-lookup"><span data-stu-id="3764f-183">**SourceId**: System.FM</span></span>
* <span data-ttu-id="3764f-184">**Property**：State</span><span class="sxs-lookup"><span data-stu-id="3764f-184">**Property**: State</span></span>

<span data-ttu-id="3764f-185">hello 下列範例示範 hello 狀態事件在 hello 服務**fabric: / WordCount/WordCountWebService**:</span><span class="sxs-lookup"><span data-stu-id="3764f-185">hello following example shows hello state event on hello service **fabric:/WordCount/WordCountWebService**:</span></span>

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

### <a name="service-correlation-error"></a><span data-ttu-id="3764f-186">服務相互關聯錯誤</span><span class="sxs-lookup"><span data-stu-id="3764f-186">Service correlation error</span></span>
<span data-ttu-id="3764f-187">**System.PLB**偵測到更新服務 toobe 相互關聯的另一個服務會建立同質鏈結時報告錯誤。</span><span class="sxs-lookup"><span data-stu-id="3764f-187">**System.PLB** reports an error when it detects that updating a service toobe correlated with another service creates an affinity chain.</span></span> <span data-ttu-id="3764f-188">當成功更新時，會清除 hello 報表。</span><span class="sxs-lookup"><span data-stu-id="3764f-188">hello report is cleared when successful update happens.</span></span>

* <span data-ttu-id="3764f-189">**SourceId**：System.PLB</span><span class="sxs-lookup"><span data-stu-id="3764f-189">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="3764f-190">**屬性**︰ServiceDescription</span><span class="sxs-lookup"><span data-stu-id="3764f-190">**Property**: ServiceDescription</span></span>
* <span data-ttu-id="3764f-191">**後續步驟**： 核取 hello 相互關聯的服務描述。</span><span class="sxs-lookup"><span data-stu-id="3764f-191">**Next steps**: Check hello correlated service descriptions.</span></span>

## <a name="partition-system-health-reports"></a><span data-ttu-id="3764f-192">分割區系統健康狀態報告</span><span class="sxs-lookup"><span data-stu-id="3764f-192">Partition system health reports</span></span>
<span data-ttu-id="3764f-193">**System.FM**，這代表 hello Failover Manager service、 管理的服務資料分割的相關資訊的 hello 授權單位。</span><span class="sxs-lookup"><span data-stu-id="3764f-193">**System.FM**, which represents hello Failover Manager service, is hello authority that manages information about service partitions.</span></span>

### <a name="state"></a><span data-ttu-id="3764f-194">State</span><span class="sxs-lookup"><span data-stu-id="3764f-194">State</span></span>
<span data-ttu-id="3764f-195">System.FM 報告為 [確定] 時已建立 hello 磁碟分割，且狀況良好。</span><span class="sxs-lookup"><span data-stu-id="3764f-195">System.FM reports as OK when hello partition has been created and is healthy.</span></span> <span data-ttu-id="3764f-196">Hello 資料分割會刪除時，從 hello health store 刪除 hello 實體。</span><span class="sxs-lookup"><span data-stu-id="3764f-196">It deletes hello entity from hello health store when hello partition is deleted.</span></span>

<span data-ttu-id="3764f-197">如果 hello 分割低於 hello 最小複本計數，它會報告錯誤。</span><span class="sxs-lookup"><span data-stu-id="3764f-197">If hello partition is below hello minimum replica count, it reports an error.</span></span> <span data-ttu-id="3764f-198">如果 hello 分割不低於 hello 最小複本計數，但它低於 hello 目標複本計數，它會回報警告。</span><span class="sxs-lookup"><span data-stu-id="3764f-198">If hello partition is not below hello minimum replica count, but it is below hello target replica count, it reports a warning.</span></span> <span data-ttu-id="3764f-199">如果 hello 磁碟分割在仲裁遺失，System.FM 報告錯誤。</span><span class="sxs-lookup"><span data-stu-id="3764f-199">If hello partition is in quorum loss, System.FM reports an error.</span></span>

<span data-ttu-id="3764f-200">Hello 重新設定所花費的時間超出預期，以及當 hello 組建所花費的時間比預期時，其他重要事件會包含警告。</span><span class="sxs-lookup"><span data-stu-id="3764f-200">Other important events include a warning when hello reconfiguration takes longer than expected and when hello build takes longer than expected.</span></span> <span data-ttu-id="3764f-201">hello 組建及重新設定的 hello 預期時間皆可設定依據服務案例。</span><span class="sxs-lookup"><span data-stu-id="3764f-201">hello expected times for hello build and reconfiguration are configurable based on service scenarios.</span></span> <span data-ttu-id="3764f-202">例如，如果服務的狀態，例如 SQL Database tb hello 建置時間長於只需要編寫小量狀態的服務。</span><span class="sxs-lookup"><span data-stu-id="3764f-202">For example, if a service has a terabyte of state, such as SQL Database, hello build takes longer than for a service with a small amount of state.</span></span>

* <span data-ttu-id="3764f-203">**SourceId**：System.FM</span><span class="sxs-lookup"><span data-stu-id="3764f-203">**SourceId**: System.FM</span></span>
* <span data-ttu-id="3764f-204">**Property**：State</span><span class="sxs-lookup"><span data-stu-id="3764f-204">**Property**: State</span></span>
* <span data-ttu-id="3764f-205">**後續步驟**： 如果 hello 健全狀況狀態不是 [確定]，則可能的一些複本尚未建立、 開啟，或升級 tooprimary 或次要資料庫正確。</span><span class="sxs-lookup"><span data-stu-id="3764f-205">**Next steps**: If hello health state is not OK, it's possible that some replicas have not been created, opened, or promoted tooprimary or secondary correctly.</span></span> <span data-ttu-id="3764f-206">在許多情況下，hello 根本原因是服務中的錯誤 hello 開啟或變更角色實作。</span><span class="sxs-lookup"><span data-stu-id="3764f-206">In many instances, hello root cause is a service bug in hello open or change-role implementation.</span></span>

<span data-ttu-id="3764f-207">下列範例中的 hello 顯示狀況良好的磁碟分割：</span><span class="sxs-lookup"><span data-stu-id="3764f-207">hello following example shows a healthy partition:</span></span>

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

<span data-ttu-id="3764f-208">hello 下列範例顯示 hello 低於目標複本計數的資料分割的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="3764f-208">hello following example shows hello health of a partition that is below target replica count.</span></span> <span data-ttu-id="3764f-209">hello 下一個步驟是 tooget hello 資料分割說明，其中顯示設定的方式： **MinReplicaSetSize**是三個和**TargetReplicaSetSize**為 7 個。</span><span class="sxs-lookup"><span data-stu-id="3764f-209">hello next step is tooget hello partition description, which shows how it is configured: **MinReplicaSetSize** is three and **TargetReplicaSetSize** is seven.</span></span> <span data-ttu-id="3764f-210">然後取得 hello 叢集中的節點數目 hello： 五個。</span><span class="sxs-lookup"><span data-stu-id="3764f-210">Then get hello number of nodes in hello cluster: five.</span></span> <span data-ttu-id="3764f-211">因此在此情況下，兩個複本不能放因為複本的 hello 目標數目高於 hello 可用的節點數目。</span><span class="sxs-lookup"><span data-stu-id="3764f-211">So in this case, two replicas can't be placed because hello target number of replicas is higher than hello number of nodes available.</span></span>

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
                        Description           : hello Load Balancer was unable toofind a placement for one or more of hello Service's Replicas:
                        Secondary replica could not be placed due toohello following constraints and properties:  
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

### <a name="replica-constraint-violation"></a><span data-ttu-id="3764f-212">複本條件約束違規</span><span class="sxs-lookup"><span data-stu-id="3764f-212">Replica constraint violation</span></span>
<span data-ttu-id="3764f-213">**System.PLB** 偵測到複本條件約束違規，且無法安置所有磁碟分割複本時，就會回報警告。</span><span class="sxs-lookup"><span data-stu-id="3764f-213">**System.PLB** reports a warning if it detects a replica constraint violation and can't place all partition replicas.</span></span> <span data-ttu-id="3764f-214">hello 報表詳細資料會顯示哪些條件約束，且屬性防止 hello 複本位置。</span><span class="sxs-lookup"><span data-stu-id="3764f-214">hello report details show which constraints and properties prevent hello replica placement.</span></span>

* <span data-ttu-id="3764f-215">**SourceId**：System.PLB</span><span class="sxs-lookup"><span data-stu-id="3764f-215">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="3764f-216">**Property**：以 **ReplicaConstraintViolation** 為開頭</span><span class="sxs-lookup"><span data-stu-id="3764f-216">**Property**: Starts with **ReplicaConstraintViolation**</span></span>

## <a name="replica-system-health-reports"></a><span data-ttu-id="3764f-217">複本系統健康狀態報告</span><span class="sxs-lookup"><span data-stu-id="3764f-217">Replica system health reports</span></span>
<span data-ttu-id="3764f-218">**System.RA**，代表 hello 重新設定代理程式元件，為 hello 進行授權 hello 複本狀態。</span><span class="sxs-lookup"><span data-stu-id="3764f-218">**System.RA**, which represents hello reconfiguration agent component, is hello authority for hello replica state.</span></span>

### <a name="state"></a><span data-ttu-id="3764f-219">State</span><span class="sxs-lookup"><span data-stu-id="3764f-219">State</span></span>
<span data-ttu-id="3764f-220">**System.RA** hello 複本建立後會報告 [確定]。</span><span class="sxs-lookup"><span data-stu-id="3764f-220">**System.RA** reports OK when hello replica has been created.</span></span>

* <span data-ttu-id="3764f-221">**SourceId**：System.RA</span><span class="sxs-lookup"><span data-stu-id="3764f-221">**SourceId**: System.RA</span></span>
* <span data-ttu-id="3764f-222">**Property**：State</span><span class="sxs-lookup"><span data-stu-id="3764f-222">**Property**: State</span></span>

<span data-ttu-id="3764f-223">下列範例中的 hello 顯示狀況良好的複本：</span><span class="sxs-lookup"><span data-stu-id="3764f-223">hello following example shows a healthy replica:</span></span>

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

### <a name="replica-open-status"></a><span data-ttu-id="3764f-224">複本開啟狀態</span><span class="sxs-lookup"><span data-stu-id="3764f-224">Replica open status</span></span>
<span data-ttu-id="3764f-225">hello API 呼叫叫用時，此健全狀況報告 hello 描述包含 hello 開始時間 （國際標準時間）。</span><span class="sxs-lookup"><span data-stu-id="3764f-225">hello description of this health report contains hello start time (Coordinated Universal Time) when hello API call was invoked.</span></span>

<span data-ttu-id="3764f-226">**System.RA**會回報警告。 如果開啟的 hello 複本所花費的時間比設定的 hello 期間 (預設： 30 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="3764f-226">**System.RA** reports a warning if hello replica open takes longer than hello configured period (default: 30 minutes).</span></span> <span data-ttu-id="3764f-227">如果 hello API，將會影響服務可用性，hello 報表就會發出速度 （可設定的間隔，預設值是 30 秒為單位）。</span><span class="sxs-lookup"><span data-stu-id="3764f-227">If hello API impacts service availability, hello report is issued much faster (a configurable interval, with a default of 30 seconds).</span></span> <span data-ttu-id="3764f-228">hello 測量的時間會包含 hello hello 複寫器開啟與 hello 服務開啟花費的時間。</span><span class="sxs-lookup"><span data-stu-id="3764f-228">hello time measured includes hello time taken for hello replicator open and hello service open.</span></span> <span data-ttu-id="3764f-229">如果開啟 hello hello 屬性變更 tooOK 完成。</span><span class="sxs-lookup"><span data-stu-id="3764f-229">hello property changes tooOK if hello open completes.</span></span>

* <span data-ttu-id="3764f-230">**SourceId**：System.RA</span><span class="sxs-lookup"><span data-stu-id="3764f-230">**SourceId**: System.RA</span></span>
* <span data-ttu-id="3764f-231">**Property**服務上的狀態事件： **ReplicaOpenStatus**</span><span class="sxs-lookup"><span data-stu-id="3764f-231">**Property**: **ReplicaOpenStatus**</span></span>
* <span data-ttu-id="3764f-232">**後續步驟**： 如果 hello 健全狀況狀態不確定，請調查為何開啟 hello 複本所花費的時間超出預期。</span><span class="sxs-lookup"><span data-stu-id="3764f-232">**Next steps**: If hello health state is not OK, investigate why hello replica open takes longer than expected.</span></span>

### <a name="slow-service-api-call"></a><span data-ttu-id="3764f-233">緩慢服務 API 呼叫</span><span class="sxs-lookup"><span data-stu-id="3764f-233">Slow service API call</span></span>
<span data-ttu-id="3764f-234">**System.RAP**和**System.Replicator**如果呼叫 toohello 使用者服務程式碼所花費的時間比設定的 hello 時間會報告警告。</span><span class="sxs-lookup"><span data-stu-id="3764f-234">**System.RAP** and **System.Replicator** report a warning if a call toohello user service code takes longer than hello configured time.</span></span> <span data-ttu-id="3764f-235">hello 呼叫完成時，會清除 hello 警告。</span><span class="sxs-lookup"><span data-stu-id="3764f-235">hello warning is cleared when hello call completes.</span></span>

* <span data-ttu-id="3764f-236">**SourceId**：System.RAP 或 System.Replicator</span><span class="sxs-lookup"><span data-stu-id="3764f-236">**SourceId**: System.RAP or System.Replicator</span></span>
* <span data-ttu-id="3764f-237">**屬性**: hello hello 緩慢 API 名稱。</span><span class="sxs-lookup"><span data-stu-id="3764f-237">**Property**: hello name of hello slow API.</span></span> <span data-ttu-id="3764f-238">hello 描述可提供更多詳細 hello 時間 hello 應用程式開發介面已暫止。</span><span class="sxs-lookup"><span data-stu-id="3764f-238">hello description provides more details about hello time hello API has been pending.</span></span>
* <span data-ttu-id="3764f-239">**後續步驟**： 調查為何 hello 呼叫所花費的時間超出預期。</span><span class="sxs-lookup"><span data-stu-id="3764f-239">**Next steps**: Investigate why hello call takes longer than expected.</span></span>

<span data-ttu-id="3764f-240">hello 下列範例會顯示資料分割在仲裁遺失和 hello 調查步驟完成 toofigure 找出原因。</span><span class="sxs-lookup"><span data-stu-id="3764f-240">hello following example shows a partition in quorum loss, and hello investigation steps done toofigure out why.</span></span> <span data-ttu-id="3764f-241">其中一個 hello 複本有警告健全狀況狀態，因此您會取得其健全狀況。</span><span class="sxs-lookup"><span data-stu-id="3764f-241">One of hello replicas has a warning health state, so you get its health.</span></span> <span data-ttu-id="3764f-242">它會顯示 hello 服務作業所花費的時間超出預期，System.RAP 所報告的事件。</span><span class="sxs-lookup"><span data-stu-id="3764f-242">It shows that hello service operation takes longer than expected, an event reported by System.RAP.</span></span> <span data-ttu-id="3764f-243">收到這項資訊之後，hello 下一個步驟是 toolook hello 服務程式碼，並那里調查。</span><span class="sxs-lookup"><span data-stu-id="3764f-243">After this information is received, hello next step is toolook at hello service code and investigate there.</span></span> <span data-ttu-id="3764f-244">此案例中，hello **RunAsync** hello 具狀態服務實作會擲回未處理的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="3764f-244">For this case, hello **RunAsync** implementation of hello stateful service throws an unhandled exception.</span></span> <span data-ttu-id="3764f-245">回收處理 hello 複本，因此您可能不會看見 hello 警告狀態中的任何複本。</span><span class="sxs-lookup"><span data-stu-id="3764f-245">hello replicas are recycling, so you may not see any replicas in hello warning state.</span></span> <span data-ttu-id="3764f-246">您可以再試一次取得 hello 健全狀況狀態，並尋找任何差異 hello 複本識別碼。</span><span class="sxs-lookup"><span data-stu-id="3764f-246">You can retry getting hello health state and look for any differences in hello replica ID.</span></span> <span data-ttu-id="3764f-247">在某些情況下，hello 重試次數可讓您找出線索。</span><span class="sxs-lookup"><span data-stu-id="3764f-247">In certain cases, hello retries can give you clues.</span></span>

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

<span data-ttu-id="3764f-248">當您啟動 hello 偵錯工具之下 hello 錯誤的應用程式時，hello 診斷事件視窗會顯示 hello RunAsync 從擲回的例外狀況：</span><span class="sxs-lookup"><span data-stu-id="3764f-248">When you start hello faulty application under hello debugger, hello diagnostic events windows show hello exception thrown from RunAsync:</span></span>

![Visual Studio 2015 診斷事件：RunAsync 在 fabric:/HelloWorldStatefulApplication 中失敗。][1]

<span data-ttu-id="3764f-250">Visual Studio 2015 診斷事件：RunAsync 在 **fabric:/HelloWorldStatefulApplication**中失敗。</span><span class="sxs-lookup"><span data-stu-id="3764f-250">Visual Studio 2015 diagnostic events: RunAsync failure in **fabric:/HelloWorldStatefulApplication**.</span></span>

[1]: ./media/service-fabric-understand-and-troubleshoot-with-system-health-reports/servicefabric-health-vs-runasync-exception.png


### <a name="replication-queue-full"></a><span data-ttu-id="3764f-251">複寫佇列已滿</span><span class="sxs-lookup"><span data-stu-id="3764f-251">Replication queue full</span></span>
<span data-ttu-id="3764f-252">**System.Replicator** hello 複寫佇列已滿時，回報警告。</span><span class="sxs-lookup"><span data-stu-id="3764f-252">**System.Replicator** reports a warning when hello replication queue is full.</span></span> <span data-ttu-id="3764f-253">在主要 hello 複寫佇列通常會變成完整因為一或多個次要複本緩慢 tooacknowledge 作業。</span><span class="sxs-lookup"><span data-stu-id="3764f-253">On hello primary, replication queue usually becomes full because one or more secondary replicas are slow tooacknowledge operations.</span></span> <span data-ttu-id="3764f-254">在次要 hello，這通常發生於 hello 服務會緩慢 tooapply hello 作業。</span><span class="sxs-lookup"><span data-stu-id="3764f-254">On hello secondary, this usually happens when hello service is slow tooapply hello operations.</span></span> <span data-ttu-id="3764f-255">無法再完整 hello 佇列時，會清除 hello 警告。</span><span class="sxs-lookup"><span data-stu-id="3764f-255">hello warning is cleared when hello queue is no longer full.</span></span>

* <span data-ttu-id="3764f-256">**SourceId**：System.Replicator</span><span class="sxs-lookup"><span data-stu-id="3764f-256">**SourceId**: System.Replicator</span></span>
* <span data-ttu-id="3764f-257">**屬性**: **PrimaryReplicationQueueStatus**或**SecondaryReplicationQueueStatus**，端視 hello 複本角色</span><span class="sxs-lookup"><span data-stu-id="3764f-257">**Property**: **PrimaryReplicationQueueStatus** or **SecondaryReplicationQueueStatus**, depending on hello replica role</span></span>

### <a name="slow-naming-operations"></a><span data-ttu-id="3764f-258">緩慢的命名作業</span><span class="sxs-lookup"><span data-stu-id="3764f-258">Slow Naming operations</span></span>
<span data-ttu-id="3764f-259">**System.NamingService** 會報告其主要複本的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="3764f-259">**System.NamingService** reports health on its primary replica when a Naming operation takes longer than acceptable.</span></span> <span data-ttu-id="3764f-260">命名作業的範例為 [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) 或 [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync)。</span><span class="sxs-lookup"><span data-stu-id="3764f-260">Examples of Naming operations are [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) or [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync).</span></span> <span data-ttu-id="3764f-261">在 FabricClient 下可以找到更多方法，例如在[服務管理方法](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient)或[屬性管理方法](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient)底下。</span><span class="sxs-lookup"><span data-stu-id="3764f-261">More methods can be found under FabricClient, for example under [service management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) or [property management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).</span></span>

> [!NOTE]
> <span data-ttu-id="3764f-262">hello 命名服務解析 hello 叢集中的服務名稱 tooa 位置，並可讓使用者 toomanage 服務名稱和屬性。</span><span class="sxs-lookup"><span data-stu-id="3764f-262">hello Naming service resolves service names tooa location in hello cluster and enables users toomanage service names and properties.</span></span> <span data-ttu-id="3764f-263">它是 Service Fabric 資料分割保存的服務。</span><span class="sxs-lookup"><span data-stu-id="3764f-263">It is a Service Fabric partitioned persisted service.</span></span> <span data-ttu-id="3764f-264">Hello 分割區之一代表 hello 授權擁有者，其中包含所有服務網狀架構名稱和服務的相關中繼資料。</span><span class="sxs-lookup"><span data-stu-id="3764f-264">One of hello partitions represents hello Authority Owner, which contains metadata about all Service Fabric names and services.</span></span> <span data-ttu-id="3764f-265">hello Service Fabric 名稱不對應的 toodifferent 資料分割，稱為名稱的擁有者資料分割，因此 hello 服務是可延伸。</span><span class="sxs-lookup"><span data-stu-id="3764f-265">hello Service Fabric names are mapped toodifferent partitions, called Name Owner partitions, so hello service is extensible.</span></span> <span data-ttu-id="3764f-266">深入了解 [命名服務](service-fabric-architecture.md)。</span><span class="sxs-lookup"><span data-stu-id="3764f-266">Read more about [Naming service](service-fabric-architecture.md).</span></span>
> 
> 

<span data-ttu-id="3764f-267">當命名作業花費的時間超出預期時，hello 作業都將標示 hello 警告報告*hello 命名服務資料分割的主要複本做 hello 作業*。</span><span class="sxs-lookup"><span data-stu-id="3764f-267">When a Naming operation takes longer than expected, hello operation is flagged with a Warning report on hello *primary replica of hello Naming service partition that serves hello operation*.</span></span> <span data-ttu-id="3764f-268">如果 hello 作業順利完成，hello 警告會清除。</span><span class="sxs-lookup"><span data-stu-id="3764f-268">If hello operation completes successfully, hello Warning is cleared.</span></span> <span data-ttu-id="3764f-269">Hello 作業完成，發生錯誤時，如果 hello 健康情況報告包含關於 hello 錯誤詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3764f-269">If hello operation completes with an error, hello health report includes details about hello error.</span></span>

* <span data-ttu-id="3764f-270">**SourceId**：System.NamingService</span><span class="sxs-lookup"><span data-stu-id="3764f-270">**SourceId**: System.NamingService</span></span>
* <span data-ttu-id="3764f-271">**屬性**： 以字首開始**Duration_**並識別 hello 很慢的作業和作業套用在哪一個 hello hello 服務網狀架構名稱。</span><span class="sxs-lookup"><span data-stu-id="3764f-271">**Property**: Starts with prefix **Duration_** and identifies hello slow operation and hello Service Fabric name on which hello operation is applied.</span></span> <span data-ttu-id="3764f-272">例如，如果在名稱網狀架構建立服務: / MyApp/MyService 費時過久，hello 屬性是 Duration_AOCreateService.fabric:/MyApp/MyService。</span><span class="sxs-lookup"><span data-stu-id="3764f-272">For example, if create service at name fabric:/MyApp/MyService takes too long, hello property is Duration_AOCreateService.fabric:/MyApp/MyService.</span></span> <span data-ttu-id="3764f-273">AO 點 toohello hello 命名資料分割，這個名稱和作業的角色。</span><span class="sxs-lookup"><span data-stu-id="3764f-273">AO points toohello role of hello Naming partition for this name and operation.</span></span>
* <span data-ttu-id="3764f-274">**後續步驟**： 核取 hello 命名作業失敗的原因。</span><span class="sxs-lookup"><span data-stu-id="3764f-274">**Next steps**: Check why hello Naming operation fails.</span></span> <span data-ttu-id="3764f-275">每個作業都可能有不同的根本原因。</span><span class="sxs-lookup"><span data-stu-id="3764f-275">Each operation can have different root causes.</span></span> <span data-ttu-id="3764f-276">例如，刪除服務可能會卡在節點上，因為 hello 應用程式主機會保留因 tooa 使用者 bug hello 服務程式碼中的節點上損毀。</span><span class="sxs-lookup"><span data-stu-id="3764f-276">For example, delete service may be stuck on a node because hello application host keeps crashing on a node due tooa user bug in hello service code.</span></span>

<span data-ttu-id="3764f-277">hello 下列範例會示範建立服務作業。</span><span class="sxs-lookup"><span data-stu-id="3764f-277">hello following example shows a create service operation.</span></span> <span data-ttu-id="3764f-278">hello 作業花費的時間超過設定的 hello 持續時間。</span><span class="sxs-lookup"><span data-stu-id="3764f-278">hello operation took longer than hello configured duration.</span></span> <span data-ttu-id="3764f-279">AO 重試，並將傳送工作 tooNO。</span><span class="sxs-lookup"><span data-stu-id="3764f-279">AO retries and sends work tooNO.</span></span> <span data-ttu-id="3764f-280">逾時沒有完成的 hello 最後一個作業。</span><span class="sxs-lookup"><span data-stu-id="3764f-280">NO completed hello last operation with Timeout.</span></span> <span data-ttu-id="3764f-281">在此情況下，hello 相同的複本是主要 hello AO 和任何角色。</span><span class="sxs-lookup"><span data-stu-id="3764f-281">In this case, hello same replica is primary for both hello AO and NO roles.</span></span>

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
                        Description           : hello AOCreateService started at 2016-04-29 20:39:08.677 is taking longer than 30.000.
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
                        Description           : hello NOCreateService started at 2016-04-29 20:39:08.689 completed with FABRIC_E_TIMEOUT in more than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM
```

## <a name="deployedapplication-system-health-reports"></a><span data-ttu-id="3764f-282">DeployedApplication 系統健康狀態報告</span><span class="sxs-lookup"><span data-stu-id="3764f-282">DeployedApplication system health reports</span></span>
<span data-ttu-id="3764f-283">**System.Hosting** hello 授權單位上已部署的實體。</span><span class="sxs-lookup"><span data-stu-id="3764f-283">**System.Hosting** is hello authority on deployed entities.</span></span>

### <a name="activation"></a><span data-ttu-id="3764f-284">啟用</span><span class="sxs-lookup"><span data-stu-id="3764f-284">Activation</span></span>
<span data-ttu-id="3764f-285">System.Hosting 做為 [確定] 時，回報應用程式已成功啟動 hello 節點上。</span><span class="sxs-lookup"><span data-stu-id="3764f-285">System.Hosting reports as OK when an application has been successfully activated on hello node.</span></span> <span data-ttu-id="3764f-286">否則，它會報告錯誤。</span><span class="sxs-lookup"><span data-stu-id="3764f-286">Otherwise, it reports an error.</span></span>

* <span data-ttu-id="3764f-287">**SourceId**：System.Hosting</span><span class="sxs-lookup"><span data-stu-id="3764f-287">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="3764f-288">**屬性**： 啟動過程中，包括 hello 首度發行版本</span><span class="sxs-lookup"><span data-stu-id="3764f-288">**Property**: Activation, including hello rollout version</span></span>
* <span data-ttu-id="3764f-289">**後續步驟**: hello 應用程式是否處於狀況不良，調查 hello 啟動失敗的原因。</span><span class="sxs-lookup"><span data-stu-id="3764f-289">**Next steps**: If hello application is unhealthy, investigate why hello activation failed.</span></span>

<span data-ttu-id="3764f-290">hello 下列範例顯示成功的啟用：</span><span class="sxs-lookup"><span data-stu-id="3764f-290">hello following example shows successful activation:</span></span>

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
                                     Description           : hello application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a><span data-ttu-id="3764f-291">下載</span><span class="sxs-lookup"><span data-stu-id="3764f-291">Download</span></span>
<span data-ttu-id="3764f-292">**System.Hosting**報告錯誤，如 hello 應用程式套件下載失敗。</span><span class="sxs-lookup"><span data-stu-id="3764f-292">**System.Hosting** reports an error if hello application package download fails.</span></span>

* <span data-ttu-id="3764f-293">**SourceId**：System.Hosting</span><span class="sxs-lookup"><span data-stu-id="3764f-293">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="3764f-294">**Property**：**Download:*RolloutVersion***</span><span class="sxs-lookup"><span data-stu-id="3764f-294">**Property**: **Download:*RolloutVersion***</span></span>
* <span data-ttu-id="3764f-295">**後續步驟**： 調查 hello 下載 hello 節點上失敗的原因。</span><span class="sxs-lookup"><span data-stu-id="3764f-295">**Next steps**: Investigate why hello download failed on hello node.</span></span>

## <a name="deployedservicepackage-system-health-reports"></a><span data-ttu-id="3764f-296">DeployedServicePackage 系統健康狀態報告</span><span class="sxs-lookup"><span data-stu-id="3764f-296">DeployedServicePackage system health reports</span></span>
<span data-ttu-id="3764f-297">**System.Hosting** hello 授權單位上已部署的實體。</span><span class="sxs-lookup"><span data-stu-id="3764f-297">**System.Hosting** is hello authority on deployed entities.</span></span>

### <a name="service-package-activation"></a><span data-ttu-id="3764f-298">服務封裝啟用</span><span class="sxs-lookup"><span data-stu-id="3764f-298">Service package activation</span></span>
<span data-ttu-id="3764f-299">System.Hosting 報告為 [確定] hello 節點上的 hello 服務封裝啟用是否成功。</span><span class="sxs-lookup"><span data-stu-id="3764f-299">System.Hosting reports as OK if hello service package activation on hello node is successful.</span></span> <span data-ttu-id="3764f-300">否則，它會報告錯誤。</span><span class="sxs-lookup"><span data-stu-id="3764f-300">Otherwise, it reports an error.</span></span>

* <span data-ttu-id="3764f-301">**SourceId**：System.Hosting</span><span class="sxs-lookup"><span data-stu-id="3764f-301">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="3764f-302">**Property**：Activation</span><span class="sxs-lookup"><span data-stu-id="3764f-302">**Property**: Activation</span></span>
* <span data-ttu-id="3764f-303">**後續步驟**： 調查 hello 啟動失敗的原因。</span><span class="sxs-lookup"><span data-stu-id="3764f-303">**Next steps**: Investigate why hello activation failed.</span></span>

### <a name="code-package-activation"></a><span data-ttu-id="3764f-304">程式碼封裝啟用</span><span class="sxs-lookup"><span data-stu-id="3764f-304">Code package activation</span></span>
<span data-ttu-id="3764f-305">**System.Hosting** hello 啟用成功時的每個程式碼封裝報告為 [確定]。</span><span class="sxs-lookup"><span data-stu-id="3764f-305">**System.Hosting** reports as OK for each code package if hello activation is successful.</span></span> <span data-ttu-id="3764f-306">如果 hello 啟用失敗，它會報告警告設定。</span><span class="sxs-lookup"><span data-stu-id="3764f-306">If hello activation fails, it reports a warning as configured.</span></span> <span data-ttu-id="3764f-307">如果**CodePackage**失敗 tooactivate 或終止時發生大於設定的 hello **CodePackageHealthErrorThreshold**，裝載報告錯誤。</span><span class="sxs-lookup"><span data-stu-id="3764f-307">If **CodePackage** fails tooactivate or terminates with an error greater than hello configured **CodePackageHealthErrorThreshold**, hosting reports an error.</span></span> <span data-ttu-id="3764f-308">如果服務封裝包含多個程式碼封裝，就會針對每個封裝產生啟用報告。</span><span class="sxs-lookup"><span data-stu-id="3764f-308">If a service package contains multiple code packages, an activation report is generated for each one.</span></span>

* <span data-ttu-id="3764f-309">**SourceId**：System.Hosting</span><span class="sxs-lookup"><span data-stu-id="3764f-309">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="3764f-310">**屬性**： 使用 hello 前置詞**CodePackageActivation**和包含 hello 名稱 hello 程式碼封裝以及 hello 進入點為 **CodePackageActivation:*CodePackageName*:*SetupEntryPoint/EntryPoint** * (例如， **CodePackageActivation:Code:SetupEntryPoint**)</span><span class="sxs-lookup"><span data-stu-id="3764f-310">**Property**: Uses hello prefix **CodePackageActivation** and contains hello name of hello code package and hello entry point as **CodePackageActivation:*CodePackageName*:*SetupEntryPoint/EntryPoint*** (for example, **CodePackageActivation:Code:SetupEntryPoint**)</span></span>

### <a name="service-type-registration"></a><span data-ttu-id="3764f-311">服務類型註冊</span><span class="sxs-lookup"><span data-stu-id="3764f-311">Service type registration</span></span>
<span data-ttu-id="3764f-312">**System.Hosting**回報為 [確定]，如果已成功登錄 hello 服務類型。</span><span class="sxs-lookup"><span data-stu-id="3764f-312">**System.Hosting** reports as OK if hello service type has been registered successfully.</span></span> <span data-ttu-id="3764f-313">它會報告錯誤，如果 hello 註冊未完成的時間 (依使用的設定**ServiceTypeRegistrationTimeout**)。</span><span class="sxs-lookup"><span data-stu-id="3764f-313">It reports an error if hello registration wasn't done in time (as configured by using **ServiceTypeRegistrationTimeout**).</span></span> <span data-ttu-id="3764f-314">如果 hello 執行階段已關閉，hello 服務類型是 hello 節點從取消註冊，並裝載會回報警告。</span><span class="sxs-lookup"><span data-stu-id="3764f-314">If hello runtime is closed, hello service type is unregistered from hello node and Hosting reports a warning.</span></span>

* <span data-ttu-id="3764f-315">**SourceId**：System.Hosting</span><span class="sxs-lookup"><span data-stu-id="3764f-315">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="3764f-316">**屬性**： 使用 hello 前置詞**ServiceTypeRegistration**和包含 hello 服務型別名稱 (例如， **ServiceTypeRegistration:FileStoreServiceType**)</span><span class="sxs-lookup"><span data-stu-id="3764f-316">**Property**: Uses hello prefix **ServiceTypeRegistration** and contains hello service type name (for example, **ServiceTypeRegistration:FileStoreServiceType**)</span></span>

<span data-ttu-id="3764f-317">下列範例中的 hello 顯示狀況良好的已部署的服務封裝：</span><span class="sxs-lookup"><span data-stu-id="3764f-317">hello following example shows a healthy deployed service package:</span></span>

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
                             Description           : hello ServicePackage was activated successfully.
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
                             Description           : hello CodePackage was activated successfully.
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
                             Description           : hello ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a><span data-ttu-id="3764f-318">下載</span><span class="sxs-lookup"><span data-stu-id="3764f-318">Download</span></span>
<span data-ttu-id="3764f-319">**System.Hosting**報告錯誤，如 hello 服務封裝下載失敗。</span><span class="sxs-lookup"><span data-stu-id="3764f-319">**System.Hosting** reports an error if hello service package download fails.</span></span>

* <span data-ttu-id="3764f-320">**SourceId**：System.Hosting</span><span class="sxs-lookup"><span data-stu-id="3764f-320">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="3764f-321">**Property**：**Download:*RolloutVersion***</span><span class="sxs-lookup"><span data-stu-id="3764f-321">**Property**: **Download:*RolloutVersion***</span></span>
* <span data-ttu-id="3764f-322">**後續步驟**： 調查 hello 下載 hello 節點上失敗的原因。</span><span class="sxs-lookup"><span data-stu-id="3764f-322">**Next steps**: Investigate why hello download failed on hello node.</span></span>

### <a name="upgrade-validation"></a><span data-ttu-id="3764f-323">升級驗證</span><span class="sxs-lookup"><span data-stu-id="3764f-323">Upgrade validation</span></span>
<span data-ttu-id="3764f-324">**System.Hosting**報告錯誤，如果 hello 升級期間執行的驗證失敗，或如果 hello hello 節點上升級會失敗。</span><span class="sxs-lookup"><span data-stu-id="3764f-324">**System.Hosting** reports an error if validation during hello upgrade fails or if hello upgrade fails on hello node.</span></span>

* <span data-ttu-id="3764f-325">**SourceId**：System.Hosting</span><span class="sxs-lookup"><span data-stu-id="3764f-325">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="3764f-326">**屬性**： 使用 hello 前置詞**FabricUpgradeValidation**且包含 hello 升級版本</span><span class="sxs-lookup"><span data-stu-id="3764f-326">**Property**: Uses hello prefix **FabricUpgradeValidation** and contains hello upgrade version</span></span>
* <span data-ttu-id="3764f-327">**描述**： 點 toohello 發生的錯誤</span><span class="sxs-lookup"><span data-stu-id="3764f-327">**Description**: Points toohello error encountered</span></span>

## <a name="next-steps"></a><span data-ttu-id="3764f-328">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3764f-328">Next steps</span></span>
[<span data-ttu-id="3764f-329">檢視 Service Fabric 健康狀態報告</span><span class="sxs-lookup"><span data-stu-id="3764f-329">View Service Fabric health reports</span></span>](service-fabric-view-entities-aggregated-health.md)

[<span data-ttu-id="3764f-330">Tooreport 並檢查服務健全狀況</span><span class="sxs-lookup"><span data-stu-id="3764f-330">How tooreport and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="3764f-331">在本機上監視及診斷服務</span><span class="sxs-lookup"><span data-stu-id="3764f-331">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="3764f-332">Service Fabric 應用程式升級</span><span class="sxs-lookup"><span data-stu-id="3764f-332">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

