---
title: "aaaHow tooview Azure Service Fabric 實體的彙總健全狀況 |Microsoft 文件"
description: "描述如何 tooquery，檢視，並評估 Azure Service Fabric 實體的彙總健全狀況，透過健全狀況查詢和一般的查詢。"
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: fa34c52d-3a74-4b90-b045-ad67afa43fe5
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: add810551cac26d2b4ff81b57d94ddd780c2cc2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="view-service-fabric-health-reports"></a><span data-ttu-id="ab101-103">檢視 Service Fabric 健康狀態報告</span><span class="sxs-lookup"><span data-stu-id="ab101-103">View Service Fabric health reports</span></span>
<span data-ttu-id="ab101-104">Azure Service Fabric 導入了由健康情況實體組成的[健康情況模型](service-fabric-health-introduction.md)，系統元件和看門狗可以在其上回報所監視的本機情況。</span><span class="sxs-lookup"><span data-stu-id="ab101-104">Azure Service Fabric introduces a [health model](service-fabric-health-introduction.md) with health entities on which system components and watchdogs can report local conditions that they are monitoring.</span></span> <span data-ttu-id="ab101-105">hello[健全狀況存放區](service-fabric-health-introduction.md#health-store)彙總所有健全狀況資料 toodetermine 實體是否狀況良好。</span><span class="sxs-lookup"><span data-stu-id="ab101-105">hello [health store](service-fabric-health-introduction.md#health-store) aggregates all health data toodetermine whether entities are healthy.</span></span>

<span data-ttu-id="ab101-106">hello 叢集會自動填入傳送嗨系統元件的健康情況報告。</span><span class="sxs-lookup"><span data-stu-id="ab101-106">hello cluster is automatically populated with health reports sent by hello system components.</span></span> <span data-ttu-id="ab101-107">深入了解在[使用系統健康情況報告 tootroubleshoot](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)。</span><span class="sxs-lookup"><span data-stu-id="ab101-107">Read more at [Use system health reports tootroubleshoot](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).</span></span>

<span data-ttu-id="ab101-108">Service Fabric 提供多個方式 tooget hello 彙總健全狀況的 hello 實體：</span><span class="sxs-lookup"><span data-stu-id="ab101-108">Service Fabric provides multiple ways tooget hello aggregated health of hello entities:</span></span>

* <span data-ttu-id="ab101-109">[Service Fabric 總管](service-fabric-visualizing-your-cluster.md) 或其他視覺效果工具</span><span class="sxs-lookup"><span data-stu-id="ab101-109">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) or other visualization tools</span></span>
* <span data-ttu-id="ab101-110">健康情況查詢 (透過 PowerShell、API 或 REST)</span><span class="sxs-lookup"><span data-stu-id="ab101-110">Health queries (through PowerShell, API, or REST)</span></span>
* <span data-ttu-id="ab101-111">一般查詢傳回一份含健全狀況作為其中 hello 內容 （透過 PowerShell、 API 或 REST） 的實體</span><span class="sxs-lookup"><span data-stu-id="ab101-111">General queries that return a list of entities that have health as one of hello properties (through PowerShell, API, or REST)</span></span>

<span data-ttu-id="ab101-112">這些選項，讓我們 toodemonstrate 本機叢集使用五個節點和 hello [fabric: / WordCount 應用程式](http://aka.ms/servicefabric-wordcountapp)。</span><span class="sxs-lookup"><span data-stu-id="ab101-112">toodemonstrate these options, let's use a local cluster with five nodes and hello [fabric:/WordCount application](http://aka.ms/servicefabric-wordcountapp).</span></span> <span data-ttu-id="ab101-113">hello **fabric: / WordCount**應用程式包含兩個預設的服務，可設定狀態之型別的服務`WordCountServiceType`，與無狀態服務型別的`WordCountWebServiceType`。</span><span class="sxs-lookup"><span data-stu-id="ab101-113">hello **fabric:/WordCount** application contains two default services, a stateful service of type `WordCountServiceType`, and a stateless service of type `WordCountWebServiceType`.</span></span> <span data-ttu-id="ab101-114">我變更 hello `ApplicationManifest.xml` toorequire 七 hello 可設定狀態的服務和一個資料分割的目標複本。</span><span class="sxs-lookup"><span data-stu-id="ab101-114">I changed hello `ApplicationManifest.xml` toorequire seven target replicas for hello stateful service and one partition.</span></span> <span data-ttu-id="ab101-115">因為 hello 叢集中只有五個節點，hello 系統元件會報告警告 hello 服務磁碟分割上，所以下列 hello 目標的計數。</span><span class="sxs-lookup"><span data-stu-id="ab101-115">Because there are only five nodes in hello cluster, hello system components report a warning on hello service partition because it is below hello target count.</span></span>

```xml
<Service Name="WordCountService">
<<<<<<< HEAD
    <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="3">
      <UniformInt64Partition PartitionCount="1" LowKey="1" HighKey="26" />
    </StatefulService>
=======
  <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="2">
    <UniformInt64Partition PartitionCount="[WordCountService_PartitionCount]" LowKey="1" HighKey="26" />
  </StatefulService>
>>>>>>> 5e84dbdd8e45a5d6b36f435a550b7433b873bf11
</Service>
```

## <a name="health-in-service-fabric-explorer"></a><span data-ttu-id="ab101-116">Service Fabric 總管中的健康情況</span><span class="sxs-lookup"><span data-stu-id="ab101-116">Health in Service Fabric Explorer</span></span>
<span data-ttu-id="ab101-117">Service Fabric 總管提供 hello 叢集的視覺化檢視。</span><span class="sxs-lookup"><span data-stu-id="ab101-117">Service Fabric Explorer provides a visual view of hello cluster.</span></span> <span data-ttu-id="ab101-118">在下面的 hello 影像，您可以看到：</span><span class="sxs-lookup"><span data-stu-id="ab101-118">In hello image below, you can see that:</span></span>

* <span data-ttu-id="ab101-119">hello 應用程式**fabric: / WordCount**是紅色 （在錯誤），因為它所報告的錯誤事件**MyWatchdog** hello 屬性**可用性**。</span><span class="sxs-lookup"><span data-stu-id="ab101-119">hello application **fabric:/WordCount** is red (in error) because it has an error event reported by **MyWatchdog** for hello property **Availability**.</span></span>
* <span data-ttu-id="ab101-120">應用程式的其中一個服務 **fabric:/WordCount/WordCountService** 是黃色 (警告)。</span><span class="sxs-lookup"><span data-stu-id="ab101-120">One of its services, **fabric:/WordCount/WordCountService** is yellow (in warning).</span></span> <span data-ttu-id="ab101-121">hello 服務已設定有七個複本，且 hello 叢集有五個節點，讓兩個 repicas 不放。</span><span class="sxs-lookup"><span data-stu-id="ab101-121">hello service is configured with seven replicas and hello cluster has five nodes, so two repicas can't be placed.</span></span> <span data-ttu-id="ab101-122">雖然它不會顯示以下，hello 服務資料分割是黃色由於系統報告`System.FM`說`Partition is below target replica or instance count`。</span><span class="sxs-lookup"><span data-stu-id="ab101-122">Although it's not shown here, hello service partition is yellow because of a system report from `System.FM` saying that `Partition is below target replica or instance count`.</span></span> <span data-ttu-id="ab101-123">hello 黃色的資料分割的觸發程序 hello 黃色的服務。</span><span class="sxs-lookup"><span data-stu-id="ab101-123">hello yellow partition triggers hello yellow service.</span></span>
* <span data-ttu-id="ab101-124">hello 叢集是紅色的因為 hello 紅色應用程式。</span><span class="sxs-lookup"><span data-stu-id="ab101-124">hello cluster is red because of hello red application.</span></span>

<span data-ttu-id="ab101-125">hello 評估使用從 hello 叢集資訊清單和應用程式資訊清單的預設原則。</span><span class="sxs-lookup"><span data-stu-id="ab101-125">hello evaluation uses default policies from hello cluster manifest and application manifest.</span></span> <span data-ttu-id="ab101-126">它們是嚴格的原則，不容許任何失敗。</span><span class="sxs-lookup"><span data-stu-id="ab101-126">They are strict policies and do not tolerate any failure.</span></span>

<span data-ttu-id="ab101-127">Service Fabric 總管 hello 叢集的檢視：</span><span class="sxs-lookup"><span data-stu-id="ab101-127">View of hello cluster with Service Fabric Explorer:</span></span>

![Service Fabric 總管 hello 叢集的檢視。][1]

[1]: ./media/service-fabric-view-entities-aggregated-health/servicefabric-explorer-cluster-health.png


> [!NOTE]
> <span data-ttu-id="ab101-129">深入了解 [Service Fabric 總管](service-fabric-visualizing-your-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="ab101-129">Read more about [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

## <a name="health-queries"></a><span data-ttu-id="ab101-130">健康情況查詢</span><span class="sxs-lookup"><span data-stu-id="ab101-130">Health queries</span></span>
<span data-ttu-id="ab101-131">服務網狀架構會公開為每個支援的 hello 的健康狀態查詢[實體類型](service-fabric-health-introduction.md#health-entities-and-hierarchy)。</span><span class="sxs-lookup"><span data-stu-id="ab101-131">Service Fabric exposes health queries for each of hello supported [entity types](service-fabric-health-introduction.md#health-entities-and-hierarchy).</span></span> <span data-ttu-id="ab101-132">可以透過 hello 上使用方法的 API 來存取[FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet)，PowerShell cmdlet 和 REST。</span><span class="sxs-lookup"><span data-stu-id="ab101-132">They can be accessed through hello API, using methods on [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="ab101-133">這些查詢會傳回有關 hello 實體的完整健全狀況資訊： hello 彙總健全狀況狀態、 實體健全狀況事件、 子健全狀況狀態 （如果適用的話）、 健康情況不良的評估 （當 hello 實體並非狀況良好） 和子系的健全狀況統計資料 （當適用）。</span><span class="sxs-lookup"><span data-stu-id="ab101-133">These queries return complete health information about hello entity: hello aggregated health state, entity health events, child health states (when applicable), unhealthy evaluations (when hello entity is not healthy), and children health statistics (when applicable).</span></span>

> [!NOTE]
> <span data-ttu-id="ab101-134">健康實體會傳回完整擴展 hello health store 中時。</span><span class="sxs-lookup"><span data-stu-id="ab101-134">A health entity is returned when it is fully populated in hello health store.</span></span> <span data-ttu-id="ab101-135">hello 實體必須是作用中 （不會刪除），並具有系統報告。</span><span class="sxs-lookup"><span data-stu-id="ab101-135">hello entity must be active (not deleted) and have a system report.</span></span> <span data-ttu-id="ab101-136">其父代上的實體 hello 階層鏈結也必須有系統的報表。</span><span class="sxs-lookup"><span data-stu-id="ab101-136">Its parent entities on hello hierarchy chain must also have system reports.</span></span> <span data-ttu-id="ab101-137">Hello 健全狀況不符合上述任何情況，如果查詢傳回[FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception)與[FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` ，它會顯示 hello 實體不會傳回原因。</span><span class="sxs-lookup"><span data-stu-id="ab101-137">If any of these conditions are not satisfied, hello health queries return a [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) with [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` that shows why hello entity is not returned.</span></span>
>
>

<span data-ttu-id="ab101-138">hello 健康狀態查詢數目必須傳入 hello 實體識別碼 hello 實體類型而定。</span><span class="sxs-lookup"><span data-stu-id="ab101-138">hello health queries must pass in hello entity identifier, which depends on hello entity type.</span></span> <span data-ttu-id="ab101-139">hello 查詢接受選用的健全狀況原則參數。</span><span class="sxs-lookup"><span data-stu-id="ab101-139">hello queries accept optional health policy parameters.</span></span> <span data-ttu-id="ab101-140">如果未不指定任何健全狀況原則，hello[健全狀況原則](service-fabric-health-introduction.md#health-policies)hello 叢集或應用程式資訊清單用來進行評估。</span><span class="sxs-lookup"><span data-stu-id="ab101-140">If no health policies are specified, hello [health policies](service-fabric-health-introduction.md#health-policies) from hello cluster or application manifest are used for evaluation.</span></span> <span data-ttu-id="ab101-141">如果 hello 資訊清單不包含的健全狀況原則定義，hello 預設健全狀況原則可用來評估。</span><span class="sxs-lookup"><span data-stu-id="ab101-141">If hello manifests don't contain a definition for health policies, hello default health policies are used for evaluation.</span></span> <span data-ttu-id="ab101-142">hello 預設健全狀況原則不能容許的任何失敗。</span><span class="sxs-lookup"><span data-stu-id="ab101-142">hello default health policies do not tolerate any failures.</span></span> <span data-ttu-id="ab101-143">hello 查詢也接受篩選條件傳回只有部分的子系或事件-hello 的尊重 hello 指定的篩選。</span><span class="sxs-lookup"><span data-stu-id="ab101-143">hello queries also accept filters for returning only partial children or events--hello ones that respect hello specified filters.</span></span> <span data-ttu-id="ab101-144">另一個篩選器允許排除 hello 子系統計資料。</span><span class="sxs-lookup"><span data-stu-id="ab101-144">Another filter allows excluding hello children statistics.</span></span>

> [!NOTE]
> <span data-ttu-id="ab101-145">因此 hello 訊息回覆縮小 hello 伺服器端，會套用 hello 輸出篩選器。</span><span class="sxs-lookup"><span data-stu-id="ab101-145">hello output filters are applied on hello server side, so hello message reply size is reduced.</span></span> <span data-ttu-id="ab101-146">我們建議您使用 hello 輸出篩選器 toolimit hello 資料傳回，而非 hello 用戶端上套用篩選。</span><span class="sxs-lookup"><span data-stu-id="ab101-146">We recommended that you use hello output filters toolimit hello data returned, rather than apply filters on hello client side.</span></span>
>
>

<span data-ttu-id="ab101-147">實體的健康狀態包含︰</span><span class="sxs-lookup"><span data-stu-id="ab101-147">An entity's health contains:</span></span>

* <span data-ttu-id="ab101-148">hello hello 實體彙總健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="ab101-148">hello aggregated health state of hello entity.</span></span> <span data-ttu-id="ab101-149">實體健全狀況報表、 子系的健全狀況狀態 （如果適用的話），以及健康原則為基礎的 hello 健全狀況存放區，藉以計算。</span><span class="sxs-lookup"><span data-stu-id="ab101-149">Computed by hello health store based on entity health reports, child health states (when applicable), and health policies.</span></span> <span data-ttu-id="ab101-150">深入了解 [實體健康情況評估](service-fabric-health-introduction.md#health-evaluation)。</span><span class="sxs-lookup"><span data-stu-id="ab101-150">Read more about [entity health evaluation](service-fabric-health-introduction.md#health-evaluation).</span></span>  
* <span data-ttu-id="ab101-151">hello hello 實體上的健全狀況事件。</span><span class="sxs-lookup"><span data-stu-id="ab101-151">hello health events on hello entity.</span></span>
* <span data-ttu-id="ab101-152">hello 集合的所有子系可以有子系的 hello 實體的健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="ab101-152">hello collection of health states of all children for hello entities that can have children.</span></span> <span data-ttu-id="ab101-153">包含實體識別碼及其 hello 彙總健全狀況狀態的 hello 健全狀態。</span><span class="sxs-lookup"><span data-stu-id="ab101-153">hello health states contain entity identifiers and hello aggregated health state.</span></span> <span data-ttu-id="ab101-154">為子系，tooget 完整健全狀況為 hello 子實體型別呼叫 hello 查詢健全狀況，並傳入 hello 子系識別碼。</span><span class="sxs-lookup"><span data-stu-id="ab101-154">tooget complete health for a child, call hello query health for hello child entity type and pass in hello child identifier.</span></span>
* <span data-ttu-id="ab101-155">如果 hello 實體並非狀況良好，hello 狀況不良的評估，該點 toohello 報告，會觸發 hello hello 實體狀態。</span><span class="sxs-lookup"><span data-stu-id="ab101-155">hello unhealthy evaluations that point toohello report that triggered hello state of hello entity, if hello entity is not healthy.</span></span> <span data-ttu-id="ab101-156">hello 評估是遞迴式的其中包含觸發目前的健全狀況狀態的 hello 子系健康情況評估。</span><span class="sxs-lookup"><span data-stu-id="ab101-156">hello evaluations are recursive, containing hello children health evaluations that triggered current health state.</span></span> <span data-ttu-id="ab101-157">例如，看門狗回報了複本錯誤。</span><span class="sxs-lookup"><span data-stu-id="ab101-157">For example, a watchdog reported an error against a replica.</span></span> <span data-ttu-id="ab101-158">hello 應用程式健全狀況顯示狀況不良評估 tooan 狀況不良服務; 到期hello 服務是由於 tooa 錯誤; 中的資料分割的狀況不良hello 資料分割會處於狀況不良，因為發生錯誤; tooa 複本hello 複本為狀況不良到期 toohello 監視錯誤健全狀況報表。</span><span class="sxs-lookup"><span data-stu-id="ab101-158">hello application health shows an unhealthy evaluation due tooan unhealthy service; hello service is unhealthy due tooa partition in error; hello partition is unhealthy due tooa replica in error; hello replica is unhealthy due toohello watchdog error health report.</span></span>
* <span data-ttu-id="ab101-159">hello 的所有子系類型有子系的 hello 實體的健全狀況統計資料。</span><span class="sxs-lookup"><span data-stu-id="ab101-159">hello health statistics for all children types of hello entities that have children.</span></span> <span data-ttu-id="ab101-160">例如，叢集健全狀況顯示 hello 總數應用程式、 服務、 資料分割和複本，並部署 hello 叢集中的實體。</span><span class="sxs-lookup"><span data-stu-id="ab101-160">For example, cluster health shows hello total number of applications, services, partitions, replicas, and deployed entities in hello cluster.</span></span> <span data-ttu-id="ab101-161">服務健全狀況顯示 hello 總數資料分割和複本 hello 底下指定的服務。</span><span class="sxs-lookup"><span data-stu-id="ab101-161">Service health shows hello total number of partitions and replicas under hello specified service.</span></span>

## <a name="get-cluster-health"></a><span data-ttu-id="ab101-162">取得叢集健康情況</span><span class="sxs-lookup"><span data-stu-id="ab101-162">Get cluster health</span></span>
<span data-ttu-id="ab101-163">會傳回 hello hello 叢集中實體的健全狀況，並包含 hello 健全狀況狀態的應用程式和節點 （hello 叢集的子系）。</span><span class="sxs-lookup"><span data-stu-id="ab101-163">Returns hello health of hello cluster entity and contains hello health states of applications and nodes (children of hello cluster).</span></span> <span data-ttu-id="ab101-164">輸入：</span><span class="sxs-lookup"><span data-stu-id="ab101-164">Input:</span></span>

* <span data-ttu-id="ab101-165">[選用] hello 叢集健全狀況原則會使用 tooevaluate hello 節點和 hello 叢集事件。</span><span class="sxs-lookup"><span data-stu-id="ab101-165">[Optional] hello cluster health policy used tooevaluate hello nodes and hello cluster events.</span></span>
* <span data-ttu-id="ab101-166">[選用] hello 應用程式健全狀況原則對應 hello 健康原則使用 toooverride hello 應用程式資訊清單的原則。</span><span class="sxs-lookup"><span data-stu-id="ab101-166">[Optional] hello application health policy map, with hello health policies used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="ab101-167">[選用]事件、 節點及指定感興趣的項目，且傳回 hello 結果 （例如，只，錯誤或警告和錯誤） 中的應用程式的篩選條件。</span><span class="sxs-lookup"><span data-stu-id="ab101-167">[Optional] Filters for events, nodes, and applications that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="ab101-168">所有的事件、 節點和應用程式會使用的 tooevaluate hello 實體彙總健全狀況，不論 hello 篩選器。</span><span class="sxs-lookup"><span data-stu-id="ab101-168">All events, nodes, and applications are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="ab101-169">[選用]篩選 tooexclude 健全狀況統計資料。</span><span class="sxs-lookup"><span data-stu-id="ab101-169">[Optional] Filter tooexclude health statistics.</span></span>
* <span data-ttu-id="ab101-170">[選用]篩選 tooinclude fabric: / 系統健全狀況統計資料中的 hello 健全狀況統計資料。</span><span class="sxs-lookup"><span data-stu-id="ab101-170">[Optional] Filter tooinclude fabric:/System health statistics in hello health statistics.</span></span> <span data-ttu-id="ab101-171">僅適用於未排除 hello 健全狀況統計資料。</span><span class="sxs-lookup"><span data-stu-id="ab101-171">Only applicable when hello health statistics are not excluded.</span></span> <span data-ttu-id="ab101-172">根據預設，hello 健全狀況統計資料會包含使用者應用程式和不 hello 系統應用程式的統計資料。</span><span class="sxs-lookup"><span data-stu-id="ab101-172">By default, hello health statistics include only statistics for user applications and not hello System application.</span></span>

### <a name="api"></a><span data-ttu-id="ab101-173">API</span><span class="sxs-lookup"><span data-stu-id="ab101-173">API</span></span>
<span data-ttu-id="ab101-174">tooget 叢集健全狀況，請建立`FabricClient`和呼叫 hello [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync)方法上的其**HealthManager**。</span><span class="sxs-lookup"><span data-stu-id="ab101-174">tooget cluster health, create a `FabricClient` and call hello [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) method on its **HealthManager**.</span></span>

<span data-ttu-id="ab101-175">hello 下列呼叫會取得 hello 叢集健全狀況：</span><span class="sxs-lookup"><span data-stu-id="ab101-175">hello following call gets hello cluster health:</span></span>

```csharp
ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync();
```

<span data-ttu-id="ab101-176">hello 下列程式碼使用自訂的叢集健全狀況原則取得 hello 叢集健全狀況和篩選的節點和應用程式。</span><span class="sxs-lookup"><span data-stu-id="ab101-176">hello following code gets hello cluster health by using a custom cluster health policy and filters for nodes and applications.</span></span> <span data-ttu-id="ab101-177">它會指定 hello 健全狀況統計資料包括 hello fabric: / 系統的統計資料。</span><span class="sxs-lookup"><span data-stu-id="ab101-177">It specifies that hello health statistics include hello fabric:/System statistics.</span></span> <span data-ttu-id="ab101-178">它會建立[ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription)，其中包含 hello 輸入的資訊。</span><span class="sxs-lookup"><span data-stu-id="ab101-178">It creates [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), which contains hello input information.</span></span>

```csharp
var policy = new ClusterHealthPolicy()
{
    MaxPercentUnhealthyNodes = 20
};
var nodesFilter = new NodeHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error | HealthStateFilter.Warning
};
var applicationsFilter = new ApplicationHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error
};
var healthStatisticsFilter = new ClusterHealthStatisticsFilter()
{
    ExcludeHealthStatistics = false,
    IncludeSystemApplicationHealthStatistics = true
};
var queryDescription = new ClusterHealthQueryDescription()
{
    HealthPolicy = policy,
    ApplicationsFilter = applicationsFilter,
    NodesFilter = nodesFilter,
    HealthStatisticsFilter = healthStatisticsFilter
};

ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="ab101-179">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ab101-179">PowerShell</span></span>
<span data-ttu-id="ab101-180">hello cmdlet tooget hello 叢集健全狀況是[Get ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth)。</span><span class="sxs-lookup"><span data-stu-id="ab101-180">hello cmdlet tooget hello cluster health is [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth).</span></span> <span data-ttu-id="ab101-181">首先，使用 hello 連線 toohello 叢集[Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="ab101-181">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="ab101-182">hello hello 叢集狀態已有五個節點、 hello 系統應用程式，且 fabric: / WordCount 設定中所述。</span><span class="sxs-lookup"><span data-stu-id="ab101-182">hello state of hello cluster is five nodes, hello system application, and fabric:/WordCount configured as described.</span></span>

<span data-ttu-id="ab101-183">hello 下列指令程式會使用預設的健全狀況原則，以取得叢集健全狀況。</span><span class="sxs-lookup"><span data-stu-id="ab101-183">hello following cmdlet gets cluster health by using default health policies.</span></span> <span data-ttu-id="ab101-184">hello 彙總健全狀況狀態為警告，因為 hello fabric: / WordCount 應用程式處於警告。</span><span class="sxs-lookup"><span data-stu-id="ab101-184">hello aggregated health state is warning, because hello fabric:/WordCount application is in warning.</span></span> <span data-ttu-id="ab101-185">請注意 hello 狀況不良的評估 hello 條件觸發 hello 彙總健全狀況所提供的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ab101-185">Note how hello unhealthy evaluations provide details on hello conditions that triggered hello aggregated health.</span></span>

```xml
PS D:\ServiceFabric> Get-ServiceFabricClusterHealth


AggregatedHealthState   : Warning
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Warning'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                          
                          
NodeHealthStates        : 
                          NodeName              : _Node_4
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_3
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_2
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_1
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_0
                          AggregatedHealthState : Ok
                          
ApplicationHealthStates : 
                          ApplicationName       : fabric:/System
                          AggregatedHealthState : Ok
                          
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Warning
                          
HealthEvents            : None
HealthStatistics        : 
                          Node                  : 5 Ok, 0 Warning, 0 Error
                          Replica               : 6 Ok, 0 Warning, 0 Error
                          Partition             : 1 Ok, 1 Warning, 0 Error
                          Service               : 1 Ok, 1 Warning, 0 Error
                          DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                          DeployedApplication   : 5 Ok, 0 Warning, 0 Error
                          Application           : 0 Ok, 1 Warning, 0 Error
```

<span data-ttu-id="ab101-186">hello 下列 PowerShell cmdlet 會取得 hello hello 叢集健全狀況所使用的自訂應用程式原則。</span><span class="sxs-lookup"><span data-stu-id="ab101-186">hello following PowerShell cmdlet gets hello health of hello cluster by using a custom application policy.</span></span> <span data-ttu-id="ab101-187">它會篩選結果 tooget 只有應用程式和錯誤或警告中的節點。</span><span class="sxs-lookup"><span data-stu-id="ab101-187">It filters results tooget only applications and nodes in error or warning.</span></span> <span data-ttu-id="ab101-188">因此不會傳回任何節點，因為全部都狀況良好。</span><span class="sxs-lookup"><span data-stu-id="ab101-188">As a result, no nodes are returned, as they are all healthy.</span></span> <span data-ttu-id="ab101-189">只有 hello fabric: / WordCount 應用程式會尊重 hello 應用程式篩選器。</span><span class="sxs-lookup"><span data-stu-id="ab101-189">Only hello fabric:/WordCount application respects hello applications filter.</span></span> <span data-ttu-id="ab101-190">因為 hello 自訂原則會指定 tooconsider 警告 hello 網狀架構的錯誤為: / WordCount 應用程式，hello 應用程式會評估為錯誤，並且是 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="ab101-190">Because hello custom policy specifies tooconsider warnings as errors for hello fabric:/WordCount application, hello application is evaluated as in error, and so is hello cluster.</span></span>

```powershell
PS D:\ServiceFabric> $appHealthPolicy = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicy
$appHealthPolicy.ConsiderWarningAsError = $true
$appHealthPolicyMap = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicyMap
$appUri1 = New-Object -TypeName System.Uri -ArgumentList "fabric:/WordCount"
$appHealthPolicyMap.Add($appUri1, $appHealthPolicy)
Get-ServiceFabricClusterHealth -ApplicationHealthPolicyMap $appHealthPolicyMap -ApplicationsFilter "Warning,Error" -NodesFilter "Warning,Error" -ExcludeHealthStatistics


AggregatedHealthState   : Error
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Error'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                          
                          
NodeHealthStates        : None
ApplicationHealthStates : 
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Error
                          
HealthEvents            : None
```

### <a name="rest"></a><span data-ttu-id="ab101-191">REST</span><span class="sxs-lookup"><span data-stu-id="ab101-191">REST</span></span>
<span data-ttu-id="ab101-192">您可以取得叢集健全狀況與[GET 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster)或[POST 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy)包含 hello 本文中所述的健全狀況原則。</span><span class="sxs-lookup"><span data-stu-id="ab101-192">You can get cluster health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-node-health"></a><span data-ttu-id="ab101-193">取得節點的健康情況</span><span class="sxs-lookup"><span data-stu-id="ab101-193">Get node health</span></span>
<span data-ttu-id="ab101-194">會傳回 hello 節點實體的健全狀況，並包含報告 hello 節點上的 hello 健康狀態事件。</span><span class="sxs-lookup"><span data-stu-id="ab101-194">Returns hello health of a node entity and contains hello health events reported on hello node.</span></span> <span data-ttu-id="ab101-195">輸入：</span><span class="sxs-lookup"><span data-stu-id="ab101-195">Input:</span></span>

* <span data-ttu-id="ab101-196">[必要] hello 節點識別 hello 節點的名稱。</span><span class="sxs-lookup"><span data-stu-id="ab101-196">[Required] hello node name that identifies hello node.</span></span>
* <span data-ttu-id="ab101-197">[選用] hello 叢集健全狀況原則設定會用 tooevaluate 健全狀況。</span><span class="sxs-lookup"><span data-stu-id="ab101-197">[Optional] hello cluster health policy settings used tooevaluate health.</span></span>
* <span data-ttu-id="ab101-198">[選用]指定感興趣的項目，且傳回 hello 結果 （例如，只，錯誤或警告和錯誤） 中的事件篩選條件。</span><span class="sxs-lookup"><span data-stu-id="ab101-198">[Optional] Filters for events that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="ab101-199">所有事件都都使用的 tooevaluate hello 實體彙總健全狀況，不論 hello 篩選器。</span><span class="sxs-lookup"><span data-stu-id="ab101-199">All events are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>

### <a name="api"></a><span data-ttu-id="ab101-200">API</span><span class="sxs-lookup"><span data-stu-id="ab101-200">API</span></span>
<span data-ttu-id="ab101-201">tooget 節點健全狀況 hello API，透過建立`FabricClient`和呼叫 hello [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync)其 HealthManager 上的方法。</span><span class="sxs-lookup"><span data-stu-id="ab101-201">tooget node health through hello API, create a `FabricClient` and call hello [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="ab101-202">hello 下列程式碼會取得 hello hello 指定的節點名稱的節點健全狀況：</span><span class="sxs-lookup"><span data-stu-id="ab101-202">hello following code gets hello node health for hello specified node name:</span></span>

```csharp
NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(nodeName);
```

<span data-ttu-id="ab101-203">hello 下列程式碼會取得 hello 節點健全狀況 hello 事件篩選器和自訂原則中指定節點名稱，以及傳遞[NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span><span class="sxs-lookup"><span data-stu-id="ab101-203">hello following code gets hello node health for hello specified node name and passes in events filter and custom policy through [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span></span>

```csharp
var queryDescription = new NodeHealthQueryDescription(nodeName)
{
    HealthPolicy = new ClusterHealthPolicy() {  ConsiderWarningAsError = true },
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.Warning },
};

NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="ab101-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ab101-204">PowerShell</span></span>
<span data-ttu-id="ab101-205">hello cmdlet tooget hello 節點健全狀況是[Get ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth)。</span><span class="sxs-lookup"><span data-stu-id="ab101-205">hello cmdlet tooget hello node health is [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth).</span></span> <span data-ttu-id="ab101-206">首先，使用 hello 連線 toohello 叢集[Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="ab101-206">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>
<span data-ttu-id="ab101-207">hello 下列指令程式會使用預設的健全狀況原則取得 hello 節點健全狀況：</span><span class="sxs-lookup"><span data-stu-id="ab101-207">hello following cmdlet gets hello node health by using default health policies:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNodeHealth _Node_1


NodeName              : _Node_1
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 3
                        SentAt                : 7/13/2017 4:39:23 PM
                        ReceivedAt            : 7/13/2017 4:40:47 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 4:40:47 PM, LastWarning = 1/1/0001 12:00:00 AM
```

<span data-ttu-id="ab101-208">hello 下列 cmdlet 會取得所有節點的 hello 健全狀況 hello 叢集中：</span><span class="sxs-lookup"><span data-stu-id="ab101-208">hello following cmdlet gets hello health of all nodes in hello cluster:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNode | Get-ServiceFabricNodeHealth | select NodeName, AggregatedHealthState | ft -AutoSize

NodeName AggregatedHealthState
-------- ---------------------
_Node_4                     Ok
_Node_3                     Ok
_Node_2                     Ok
_Node_1                     Ok
_Node_0                     Ok
```

### <a name="rest"></a><span data-ttu-id="ab101-209">REST</span><span class="sxs-lookup"><span data-stu-id="ab101-209">REST</span></span>
<span data-ttu-id="ab101-210">您可以取得節點健全狀況與[GET 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node)或[POST 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy)包含 hello 本文中所述的健全狀況原則。</span><span class="sxs-lookup"><span data-stu-id="ab101-210">You can get node health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-application-health"></a><span data-ttu-id="ab101-211">取得應用程式健康情況</span><span class="sxs-lookup"><span data-stu-id="ab101-211">Get application health</span></span>
<span data-ttu-id="ab101-212">傳回 hello 應用程式的實體健全的狀況。</span><span class="sxs-lookup"><span data-stu-id="ab101-212">Returns hello health of an application entity.</span></span> <span data-ttu-id="ab101-213">它包含 hello hello 部署應用程式和服務的子節點的健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="ab101-213">It contains hello health states of hello deployed application and service children.</span></span> <span data-ttu-id="ab101-214">輸入：</span><span class="sxs-lookup"><span data-stu-id="ab101-214">Input:</span></span>

* <span data-ttu-id="ab101-215">[必要] hello 應用程式名稱 (URI) 可識別 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ab101-215">[Required] hello application name (URI) that identifies hello application.</span></span>
* <span data-ttu-id="ab101-216">[選用] hello 應用程式健全狀況原則會使用 toooverride hello 應用程式資訊清單的原則。</span><span class="sxs-lookup"><span data-stu-id="ab101-216">[Optional] hello application health policy used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="ab101-217">[選用]篩選事件、 服務和已部署的應用程式所指定的項目感興趣，且在 hello 結果 （例如，只，錯誤或警告和錯誤） 傳回。</span><span class="sxs-lookup"><span data-stu-id="ab101-217">[Optional] Filters for events, services, and deployed applications that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="ab101-218">所有的事件、 服務和已部署應用程式會使用的 tooevaluate hello 實體彙總健全狀況，不論 hello 篩選器。</span><span class="sxs-lookup"><span data-stu-id="ab101-218">All events, services, and deployed applications are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="ab101-219">[選用]篩選 tooexclude hello 健全狀況統計資料。</span><span class="sxs-lookup"><span data-stu-id="ab101-219">[Optional] Filter tooexclude hello health statistics.</span></span> <span data-ttu-id="ab101-220">如果未指定，hello 健全狀況統計資料包括 hello 確定、 警告和錯誤的應用程式的所有子系計數： 服務資料分割，複本部署的應用程式，及部署服務套件。</span><span class="sxs-lookup"><span data-stu-id="ab101-220">If not specified, hello health statistics include hello ok, warning, and error count for all application children: services, partitions, replicas, deployed applications, and deployed service packages.</span></span>

### <a name="api"></a><span data-ttu-id="ab101-221">API</span><span class="sxs-lookup"><span data-stu-id="ab101-221">API</span></span>
<span data-ttu-id="ab101-222">tooget 應用程式健全狀況，建立`FabricClient`和呼叫 hello [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync)其 HealthManager 上的方法。</span><span class="sxs-lookup"><span data-stu-id="ab101-222">tooget application health, create a `FabricClient` and call hello [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="ab101-223">hello 下列程式碼會取得 hello hello 指定應用程式名稱 (URI) 的應用程式健全狀況：</span><span class="sxs-lookup"><span data-stu-id="ab101-223">hello following code gets hello application health for hello specified application name (URI):</span></span>

```csharp
ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(applicationName);
```

<span data-ttu-id="ab101-224">hello 下列程式碼取得 hello hello 指定應用程式名稱 (URI) 的應用程式健全狀況與篩選器，並透過指定的自訂原則[ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription)。</span><span class="sxs-lookup"><span data-stu-id="ab101-224">hello following code gets hello application health for hello specified application name (URI), with filters and custom policies specified via [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).</span></span>

```csharp
HealthStateFilter warningAndErrors = HealthStateFilter.Error | HealthStateFilter.Warning;
var serviceTypePolicy = new ServiceTypeHealthPolicy()
{
    MaxPercentUnhealthyPartitionsPerService = 0,
    MaxPercentUnhealthyReplicasPerPartition = 5,
    MaxPercentUnhealthyServices = 0,
};
var policy = new ApplicationHealthPolicy()
{
    ConsiderWarningAsError = false,
    DefaultServiceTypeHealthPolicy = serviceTypePolicy,
    MaxPercentUnhealthyDeployedApplications = 0,
};

var queryDescription = new ApplicationHealthQueryDescription(applicationName)
{
    HealthPolicy = policy,
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = warningAndErrors },
    ServicesFilter = new ServiceHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
    DeployedApplicationsFilter = new DeployedApplicationHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
};

ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="ab101-225">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ab101-225">PowerShell</span></span>
<span data-ttu-id="ab101-226">hello cmdlet tooget hello 應用程式健全狀況是[Get ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps)。</span><span class="sxs-lookup"><span data-stu-id="ab101-226">hello cmdlet tooget hello application health is [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="ab101-227">首先，使用 hello 連線 toohello 叢集[Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="ab101-227">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="ab101-228">hello 下列 cmdlet 會傳回 hello 健全狀況的 hello **fabric: / WordCount**應用程式：</span><span class="sxs-lookup"><span data-stu-id="ab101-228">hello following cmdlet returns hello health of hello **fabric:/WordCount** application:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Warning
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountWebService
                                  AggregatedHealthState : Ok
                                  
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Warning
                                  
DeployedApplicationHealthStates : 
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_4
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_3
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_0
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_2
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_1
                                  AggregatedHealthState : Ok
                                  
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/13/2017 5:57:05 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
                                  
HealthStatistics                : 
                                  Replica               : 6 Ok, 0 Warning, 0 Error
                                  Partition             : 1 Ok, 1 Warning, 0 Error
                                  Service               : 1 Ok, 1 Warning, 0 Error
                                  DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                                  DeployedApplication   : 5 Ok, 0 Warning, 0 Error
```

<span data-ttu-id="ab101-229">下列 PowerShell 指令程式將自訂原則中的 hello。</span><span class="sxs-lookup"><span data-stu-id="ab101-229">hello following PowerShell cmdlet passes in custom policies.</span></span> <span data-ttu-id="ab101-230">它也會篩選子系和事件。</span><span class="sxs-lookup"><span data-stu-id="ab101-230">It also filters children and events.</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth -ApplicationName fabric:/WordCount -ConsiderWarningAsError $true -ServicesFilter Error -EventsFilter Error -DeployedApplicationsFilter Error -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Error
                                  
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

### <a name="rest"></a><span data-ttu-id="ab101-231">REST</span><span class="sxs-lookup"><span data-stu-id="ab101-231">REST</span></span>
<span data-ttu-id="ab101-232">您可以取得與應用程式健全狀況[GET 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application)或[POST 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy)包含 hello 本文中所述的健全狀況原則。</span><span class="sxs-lookup"><span data-stu-id="ab101-232">You can get application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-service-health"></a><span data-ttu-id="ab101-233">取得服務健康情況</span><span class="sxs-lookup"><span data-stu-id="ab101-233">Get service health</span></span>
<span data-ttu-id="ab101-234">傳回 hello 健全狀況服務實體。</span><span class="sxs-lookup"><span data-stu-id="ab101-234">Returns hello health of a service entity.</span></span> <span data-ttu-id="ab101-235">它包含 hello 資料分割健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="ab101-235">It contains hello partition health states.</span></span> <span data-ttu-id="ab101-236">輸入：</span><span class="sxs-lookup"><span data-stu-id="ab101-236">Input:</span></span>

* <span data-ttu-id="ab101-237">[必要] hello 服務名稱 (URI)，識別 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="ab101-237">[Required] hello service name (URI) that identifies hello service.</span></span>
* <span data-ttu-id="ab101-238">[選用] hello 應用程式健全狀況原則會使用 toooverride hello 應用程式資訊清單的原則。</span><span class="sxs-lookup"><span data-stu-id="ab101-238">[Optional] hello application health policy used toooverride hello application manifest policy.</span></span>
* <span data-ttu-id="ab101-239">[選用]事件和指定感興趣的項目，且傳回 hello 結果 （例如，只，錯誤或警告和錯誤） 中的資料分割的篩選條件。</span><span class="sxs-lookup"><span data-stu-id="ab101-239">[Optional] Filters for events and partitions that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="ab101-240">所有事件和資料分割都是使用的 tooevaluate hello 實體彙總健全狀況，不論 hello 篩選器。</span><span class="sxs-lookup"><span data-stu-id="ab101-240">All events and partitions are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="ab101-241">[選用]篩選 tooexclude 健全狀況統計資料。</span><span class="sxs-lookup"><span data-stu-id="ab101-241">[Optional] Filter tooexclude health statistics.</span></span> <span data-ttu-id="ab101-242">如果未指定，確定 hello 健全狀況統計資料顯示 hello、 警告和錯誤的所有資料分割和複本 hello 服務的計數。</span><span class="sxs-lookup"><span data-stu-id="ab101-242">If not specified, hello health statistics show hello ok, warning, and error count for all partitions and replicas of hello service.</span></span>

### <a name="api"></a><span data-ttu-id="ab101-243">API</span><span class="sxs-lookup"><span data-stu-id="ab101-243">API</span></span>
<span data-ttu-id="ab101-244">tooget 服務健全狀況 hello API，透過建立`FabricClient`和呼叫 hello [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync)其 HealthManager 上的方法。</span><span class="sxs-lookup"><span data-stu-id="ab101-244">tooget service health through hello API, create a `FabricClient` and call hello [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="ab101-245">hello 下列範例會取得具有指定的服務名稱 (URI) 的服務的 hello 健全狀況：</span><span class="sxs-lookup"><span data-stu-id="ab101-245">hello following example gets hello health of a service with specified service name (URI):</span></span>

```charp
ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(serviceName);
```

<span data-ttu-id="ab101-246">hello 下列程式碼會取得 hello 服務健全狀況 hello 指定的服務名稱 (URI)，指定篩選器和自訂原則透過[ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span><span class="sxs-lookup"><span data-stu-id="ab101-246">hello following code gets hello service health for hello specified service name (URI), specifying filters and custom policy via [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span></span>

```csharp
var queryDescription = new ServiceHealthQueryDescription(serviceName)
{
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.All },
    PartitionsFilter = new PartitionHealthStatesFilter() { HealthStateFilterValue = HealthStateFilter.Error },
};

ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="ab101-247">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ab101-247">PowerShell</span></span>
<span data-ttu-id="ab101-248">hello cmdlet tooget hello 服務健全狀況是[Get ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth)。</span><span class="sxs-lookup"><span data-stu-id="ab101-248">hello cmdlet tooget hello service health is [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth).</span></span> <span data-ttu-id="ab101-249">首先，使用 hello 連線 toohello 叢集[Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="ab101-249">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="ab101-250">hello 下列指令程式會使用預設的健全狀況原則取得 hello 服務健全狀況：</span><span class="sxs-lookup"><span data-stu-id="ab101-250">hello following cmdlet gets hello service health by using default health policies:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricServiceHealth -ServiceName fabric:/WordCount/WordCountService


ServiceName           : fabric:/WordCount/WordCountService
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                        
                        Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                        
                            Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
PartitionHealthStates : 
                        PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                        AggregatedHealthState : Warning
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 15
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
                        Partition             : 0 Ok, 1 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="ab101-251">REST</span><span class="sxs-lookup"><span data-stu-id="ab101-251">REST</span></span>
<span data-ttu-id="ab101-252">您可以取得服務健全狀況與[GET 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service)或[POST 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy)包含 hello 本文中所述的健全狀況原則。</span><span class="sxs-lookup"><span data-stu-id="ab101-252">You can get service health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-partition-health"></a><span data-ttu-id="ab101-253">取得分割區健康情況</span><span class="sxs-lookup"><span data-stu-id="ab101-253">Get partition health</span></span>
<span data-ttu-id="ab101-254">傳回的資料分割實體的 hello 健全狀況。</span><span class="sxs-lookup"><span data-stu-id="ab101-254">Returns hello health of a partition entity.</span></span> <span data-ttu-id="ab101-255">它包含 hello 複本健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="ab101-255">It contains hello replica health states.</span></span> <span data-ttu-id="ab101-256">輸入：</span><span class="sxs-lookup"><span data-stu-id="ab101-256">Input:</span></span>

* <span data-ttu-id="ab101-257">[必要] hello 資料分割識別碼 (GUID)，識別 hello 資料分割。</span><span class="sxs-lookup"><span data-stu-id="ab101-257">[Required] hello partition ID (GUID) that identifies hello partition.</span></span>
* <span data-ttu-id="ab101-258">[選用] hello 應用程式健全狀況原則會使用 toooverride hello 應用程式資訊清單的原則。</span><span class="sxs-lookup"><span data-stu-id="ab101-258">[Optional] hello application health policy used toooverride hello application manifest policy.</span></span>
* <span data-ttu-id="ab101-259">[選用]篩選條件的事件及指定感興趣的項目，且傳回 hello 結果 （例如，只，錯誤或警告和錯誤） 中的複本。</span><span class="sxs-lookup"><span data-stu-id="ab101-259">[Optional] Filters for events and replicas that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="ab101-260">所有的事件和複本都是使用的 tooevaluate hello 實體彙總健全狀況，不論 hello 篩選器。</span><span class="sxs-lookup"><span data-stu-id="ab101-260">All events and replicas are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="ab101-261">[選用]篩選 tooexclude 健全狀況統計資料。</span><span class="sxs-lookup"><span data-stu-id="ab101-261">[Optional] Filter tooexclude health statistics.</span></span> <span data-ttu-id="ab101-262">如果未指定，hello 健全狀況統計資料會顯示幾個複本處於 [確定]、 警告和錯誤狀態。</span><span class="sxs-lookup"><span data-stu-id="ab101-262">If not specified, hello health statistics show how many replicas are in ok, warning, and error states.</span></span>

### <a name="api"></a><span data-ttu-id="ab101-263">API</span><span class="sxs-lookup"><span data-stu-id="ab101-263">API</span></span>
<span data-ttu-id="ab101-264">tooget 資料分割的健全狀況 hello API，透過建立`FabricClient`和呼叫 hello [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync)其 HealthManager 上的方法。</span><span class="sxs-lookup"><span data-stu-id="ab101-264">tooget partition health through hello API, create a `FabricClient` and call hello [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="ab101-265">toospecify 選擇性參數，建立[PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription)。</span><span class="sxs-lookup"><span data-stu-id="ab101-265">toospecify optional parameters, create [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).</span></span>

```csharp
PartitionHealth partitionHealth = await fabricClient.HealthManager.GetPartitionHealthAsync(partitionId);
```

### <a name="powershell"></a><span data-ttu-id="ab101-266">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ab101-266">PowerShell</span></span>
<span data-ttu-id="ab101-267">hello cmdlet tooget hello 資料分割健全狀況是[Get ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth)。</span><span class="sxs-lookup"><span data-stu-id="ab101-267">hello cmdlet tooget hello partition health is [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth).</span></span> <span data-ttu-id="ab101-268">首先，使用 hello 連線 toohello 叢集[Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="ab101-268">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="ab101-269">hello 下列 cmdlet 會取得所有資料分割的 hello hello 健全狀況**fabric: / WordCount/WordCountService**服務也已經篩選掉複本健全狀況狀態：</span><span class="sxs-lookup"><span data-stu-id="ab101-269">hello following cmdlet gets hello health for all partitions of hello **fabric:/WordCount/WordCountService** service and filters out replica health states:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 72
                        SentAt                : 7/13/2017 5:57:29 PM
                        ReceivedAt            : 7/13/2017 5:57:48 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/P RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/S RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Ok->Warning = 7/13/2017 5:57:48 PM, LastError = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131444445174851664
                        SentAt                : 7/13/2017 6:35:17 PM
                        ReceivedAt            : 7/13/2017 6:35:18 PM
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
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/13/2017 5:57:48 PM, LastOk = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="ab101-270">REST</span><span class="sxs-lookup"><span data-stu-id="ab101-270">REST</span></span>
<span data-ttu-id="ab101-271">您可以取得與資料分割健全狀況[GET 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition)或[POST 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy)包含 hello 本文中所述的健全狀況原則。</span><span class="sxs-lookup"><span data-stu-id="ab101-271">You can get partition health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-replica-health"></a><span data-ttu-id="ab101-272">取得複本健康情況</span><span class="sxs-lookup"><span data-stu-id="ab101-272">Get replica health</span></span>
<span data-ttu-id="ab101-273">傳回 hello 的可設定狀態的服務複本或無狀態服務執行個體的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="ab101-273">Returns hello health of a stateful service replica or a stateless service instance.</span></span> <span data-ttu-id="ab101-274">輸入：</span><span class="sxs-lookup"><span data-stu-id="ab101-274">Input:</span></span>

* <span data-ttu-id="ab101-275">[必要] hello 資料分割識別碼 (GUID) 和複本識別碼，可識別 hello 複本。</span><span class="sxs-lookup"><span data-stu-id="ab101-275">[Required] hello partition ID (GUID) and replica ID that identifies hello replica.</span></span>
* <span data-ttu-id="ab101-276">[選用] hello 應用程式健全狀況原則的參數使用 toooverride hello 應用程式資訊清單的原則。</span><span class="sxs-lookup"><span data-stu-id="ab101-276">[Optional] hello application health policy parameters used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="ab101-277">[選用]指定感興趣的項目，且傳回 hello 結果 （例如，只，錯誤或警告和錯誤） 中的事件篩選條件。</span><span class="sxs-lookup"><span data-stu-id="ab101-277">[Optional] Filters for events that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="ab101-278">所有事件都都使用的 tooevaluate hello 實體彙總健全狀況，不論 hello 篩選器。</span><span class="sxs-lookup"><span data-stu-id="ab101-278">All events are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>

### <a name="api"></a><span data-ttu-id="ab101-279">API</span><span class="sxs-lookup"><span data-stu-id="ab101-279">API</span></span>
<span data-ttu-id="ab101-280">tooget hello 複本健全狀況 hello API，透過建立`FabricClient`和呼叫 hello [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync)其 HealthManager 上的方法。</span><span class="sxs-lookup"><span data-stu-id="ab101-280">tooget hello replica health through hello API, create a `FabricClient` and call hello [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) method on its HealthManager.</span></span> <span data-ttu-id="ab101-281">進階參數，使用 toospecify [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription)。</span><span class="sxs-lookup"><span data-stu-id="ab101-281">toospecify advanced parameters, use [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).</span></span>

```csharp
ReplicaHealth replicaHealth = await fabricClient.HealthManager.GetReplicaHealthAsync(partitionId, replicaId);
```

### <a name="powershell"></a><span data-ttu-id="ab101-282">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ab101-282">PowerShell</span></span>
<span data-ttu-id="ab101-283">hello cmdlet tooget hello 複本健全狀況是[Get ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth)。</span><span class="sxs-lookup"><span data-stu-id="ab101-283">hello cmdlet tooget hello replica health is [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth).</span></span> <span data-ttu-id="ab101-284">首先，使用 hello 連線 toohello 叢集[Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="ab101-284">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="ab101-285">hello 下列 cmdlet 會取得 hello hello hello 服務的所有資料分割的主要複本的健全狀況：</span><span class="sxs-lookup"><span data-stu-id="ab101-285">hello following cmdlet gets hello health of hello primary replica for all partitions of hello service:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a><span data-ttu-id="ab101-286">REST</span><span class="sxs-lookup"><span data-stu-id="ab101-286">REST</span></span>
<span data-ttu-id="ab101-287">您可以取得複本健全狀況與[GET 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica)或[POST 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy)包含 hello 本文中所述的健全狀況原則。</span><span class="sxs-lookup"><span data-stu-id="ab101-287">You can get replica health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-deployed-application-health"></a><span data-ttu-id="ab101-288">取得已部署應用程式的健康情況</span><span class="sxs-lookup"><span data-stu-id="ab101-288">Get deployed application health</span></span>
<span data-ttu-id="ab101-289">傳回 hello 部署在實體節點上的應用程式的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="ab101-289">Returns hello health of an application deployed on a node entity.</span></span> <span data-ttu-id="ab101-290">它包含部署的 hello 服務封裝健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="ab101-290">It contains hello deployed service package health states.</span></span> <span data-ttu-id="ab101-291">輸入：</span><span class="sxs-lookup"><span data-stu-id="ab101-291">Input:</span></span>

* <span data-ttu-id="ab101-292">[必要] hello 應用程式名稱 (URI) 和節點名稱 （字串），識別 hello 部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="ab101-292">[Required] hello application name (URI) and node name (string) that identify hello deployed application.</span></span>
* <span data-ttu-id="ab101-293">[選用] hello 應用程式健全狀況原則會使用 toooverride hello 應用程式資訊清單的原則。</span><span class="sxs-lookup"><span data-stu-id="ab101-293">[Optional] hello application health policy used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="ab101-294">[選用]事件和指定感興趣的項目，且傳回 hello 結果 （例如，只，錯誤或警告和錯誤） 中的已部署的服務封裝的篩選條件。</span><span class="sxs-lookup"><span data-stu-id="ab101-294">[Optional] Filters for events and deployed service packages that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="ab101-295">所有事件和部署的服務封裝都是使用的 tooevaluate hello 實體彙總健全狀況，不論 hello 篩選器。</span><span class="sxs-lookup"><span data-stu-id="ab101-295">All events and deployed service packages are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="ab101-296">[選用]篩選 tooexclude 健全狀況統計資料。</span><span class="sxs-lookup"><span data-stu-id="ab101-296">[Optional] Filter tooexclude health statistics.</span></span> <span data-ttu-id="ab101-297">如果未指定，hello 健全狀況統計資料會顯示 [確定]、 警告和錯誤健全狀況狀態的已部署的服務套件 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="ab101-297">If not specified, hello health statistics show hello number of deployed service packages in ok, warning, and error health states.</span></span>

### <a name="api"></a><span data-ttu-id="ab101-298">API</span><span class="sxs-lookup"><span data-stu-id="ab101-298">API</span></span>
<span data-ttu-id="ab101-299">tooget hello 健全狀況的 hello API，透過在節點上部署的應用程式建立`FabricClient`和呼叫 hello [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync)其 HealthManager 上的方法。</span><span class="sxs-lookup"><span data-stu-id="ab101-299">tooget hello health of an application deployed on a node through hello API, create a `FabricClient` and call hello [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="ab101-300">toospecify 選擇性參數，請使用[DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription)。</span><span class="sxs-lookup"><span data-stu-id="ab101-300">toospecify optional parameters, use [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).</span></span>

```csharp
DeployedApplicationHealth health = await fabricClient.HealthManager.GetDeployedApplicationHealthAsync(
    new DeployedApplicationHealthQueryDescription(applicationName, nodeName));
```

### <a name="powershell"></a><span data-ttu-id="ab101-301">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ab101-301">PowerShell</span></span>
<span data-ttu-id="ab101-302">hello cmdlet tooget hello 部署應用程式健全狀況是[Get ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps)。</span><span class="sxs-lookup"><span data-stu-id="ab101-302">hello cmdlet tooget hello deployed application health is [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="ab101-303">首先，使用 hello 連線 toohello 叢集[Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="ab101-303">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="ab101-304">toofind 出應用程式的部署位置執行[Get ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps)並查看 hello 部署應用程式的子系。</span><span class="sxs-lookup"><span data-stu-id="ab101-304">toofind out where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at hello deployed application children.</span></span>

<span data-ttu-id="ab101-305">hello 下列 cmdlet 會取得 hello 健全狀況的 hello **fabric: / WordCount**上部署的應用程式**_Node_2**。</span><span class="sxs-lookup"><span data-stu-id="ab101-305">hello following cmdlet gets hello health of hello **fabric:/WordCount** application deployed on **_Node_2**.</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplicationHealth -ApplicationName fabric:/WordCount -NodeName _Node_0


ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_0
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
                                     ServiceManifestName   : WordCountWebServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131444422261848308
                                     SentAt                : 7/13/2017 5:57:06 PM
                                     ReceivedAt            : 7/13/2017 5:57:17 PM
                                     TTL                   : Infinite
                                     Description           : hello application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/13/2017 5:57:17 PM, LastWarning = 1/1/0001 12:00:00 AM
                                     
HealthStatistics                   : 
                                     DeployedServicePackage : 2 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="ab101-306">REST</span><span class="sxs-lookup"><span data-stu-id="ab101-306">REST</span></span>
<span data-ttu-id="ab101-307">您可以取得部署的應用程式健全狀況[GET 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application)或[POST 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy)包含 hello 本文中所述的健全狀況原則。</span><span class="sxs-lookup"><span data-stu-id="ab101-307">You can get deployed application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-deployed-service-package-health"></a><span data-ttu-id="ab101-308">取得已部署服務封裝的健康情況</span><span class="sxs-lookup"><span data-stu-id="ab101-308">Get deployed service package health</span></span>
<span data-ttu-id="ab101-309">傳回 hello 已部署的服務套件實體健全的狀況。</span><span class="sxs-lookup"><span data-stu-id="ab101-309">Returns hello health of a deployed service package entity.</span></span> <span data-ttu-id="ab101-310">輸入：</span><span class="sxs-lookup"><span data-stu-id="ab101-310">Input:</span></span>

* <span data-ttu-id="ab101-311">[必要] hello 應用程式名稱 (URI)、 節點名稱 （字串） 和服務資訊清單的名稱 （字串），識別 hello 部署服務封裝。</span><span class="sxs-lookup"><span data-stu-id="ab101-311">[Required] hello application name (URI), node name (string), and service manifest name (string) that identify hello deployed service package.</span></span>
* <span data-ttu-id="ab101-312">[選用] hello 應用程式健全狀況原則會使用 toooverride hello 應用程式資訊清單的原則。</span><span class="sxs-lookup"><span data-stu-id="ab101-312">[Optional] hello application health policy used toooverride hello application manifest policy.</span></span>
* <span data-ttu-id="ab101-313">[選用]指定感興趣的項目，且傳回 hello 結果 （例如，只，錯誤或警告和錯誤） 中的事件篩選條件。</span><span class="sxs-lookup"><span data-stu-id="ab101-313">[Optional] Filters for events that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="ab101-314">所有事件都都使用的 tooevaluate hello 實體彙總健全狀況，不論 hello 篩選器。</span><span class="sxs-lookup"><span data-stu-id="ab101-314">All events are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>

### <a name="api"></a><span data-ttu-id="ab101-315">API</span><span class="sxs-lookup"><span data-stu-id="ab101-315">API</span></span>
<span data-ttu-id="ab101-316">tooget hello hello API，透過已部署的服務封裝健全狀況建立`FabricClient`和呼叫 hello [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync)其 HealthManager 上的方法。</span><span class="sxs-lookup"><span data-stu-id="ab101-316">tooget hello health of a deployed service package through hello API, create a `FabricClient` and call hello [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) method on its HealthManager.</span></span> <span data-ttu-id="ab101-317">toospecify 選擇性參數，請使用[DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription)。</span><span class="sxs-lookup"><span data-stu-id="ab101-317">toospecify optional parameters, use [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).</span></span>

```csharp
DeployedServicePackageHealth health = await fabricClient.HealthManager.GetDeployedServicePackageHealthAsync(
    new DeployedServicePackageHealthQueryDescription(applicationName, nodeName, serviceManifestName));
```

### <a name="powershell"></a><span data-ttu-id="ab101-318">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ab101-318">PowerShell</span></span>
<span data-ttu-id="ab101-319">hello cmdlet tooget hello 部署服務封裝健全狀況是[Get ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth)。</span><span class="sxs-lookup"><span data-stu-id="ab101-319">hello cmdlet tooget hello deployed service package health is [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth).</span></span> <span data-ttu-id="ab101-320">首先，使用 hello 連線 toohello 叢集[Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="ab101-320">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="ab101-321">執行應用程式部署所在的 toosee [Get ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps)並查看部署的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ab101-321">toosee where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at hello deployed applications.</span></span> <span data-ttu-id="ab101-322">服務封裝中的應用程式，查看在 hello toosee 部署服務封裝的子系在 hello [Get ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps)輸出。</span><span class="sxs-lookup"><span data-stu-id="ab101-322">toosee which service packages are in an application, look at hello deployed service package children in hello [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) output.</span></span>

<span data-ttu-id="ab101-323">hello 下列 cmdlet 會取得 hello 健全狀況的 hello **WordCountServicePkg**服務封裝的 hello **fabric: / WordCount**上部署的應用程式**_Node_2**。</span><span class="sxs-lookup"><span data-stu-id="ab101-323">hello following cmdlet gets hello health of hello **WordCountServicePkg** service package of hello **fabric:/WordCount** application deployed on **_Node_2**.</span></span> <span data-ttu-id="ab101-324">hello 實體具有**System.Hosting**成功的服務封裝和項目點啟動，並註冊成功的服務類型的報表。</span><span class="sxs-lookup"><span data-stu-id="ab101-324">hello entity has **System.Hosting** reports for successful service-package and entry-point activation, and successful service-type registration.</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplication -ApplicationName fabric:/WordCount -NodeName _Node_2 | Get-ServiceFabricDeployedServicePackageHealth -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_2
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131444422267693359
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131444422267903345
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131444422272458374
                             SentAt                : 7/13/2017 5:57:07 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a><span data-ttu-id="ab101-325">REST</span><span class="sxs-lookup"><span data-stu-id="ab101-325">REST</span></span>
<span data-ttu-id="ab101-326">您可以取得已部署的服務封裝健全狀況與[GET 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package)或[POST 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy)包含 hello 本文中所述的健全狀況原則。</span><span class="sxs-lookup"><span data-stu-id="ab101-326">You can get deployed service package health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="health-chunk-queries"></a><span data-ttu-id="ab101-327">健全狀況區塊查詢</span><span class="sxs-lookup"><span data-stu-id="ab101-327">Health chunk queries</span></span>
<span data-ttu-id="ab101-328">hello 健全狀況區塊的查詢可以傳回多層級的叢集子系 （遞迴），每個輸入篩選器。</span><span class="sxs-lookup"><span data-stu-id="ab101-328">hello health chunk queries can return multi-level cluster children (recursively), per input filters.</span></span> <span data-ttu-id="ab101-329">它支援進階的篩選器可讓很大的彈性選擇 hello 子系 toobe 傳回。</span><span class="sxs-lookup"><span data-stu-id="ab101-329">It supports advanced filters that allow a lot of flexibility in choosing hello children toobe returned.</span></span> <span data-ttu-id="ab101-330">hello 篩選條件可以指定子系，hello 唯一識別碼或其他群組識別碼和/或健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="ab101-330">hello filters can specify children by hello unique identifier or by other group identifiers and/or health states.</span></span> <span data-ttu-id="ab101-331">根據預設，沒有子系是包含在內，但不要的 toohealth 命令永遠包含第一層子系。</span><span class="sxs-lookup"><span data-stu-id="ab101-331">By default, no children are included, as opposed toohealth commands that always include first-level children.</span></span>

<span data-ttu-id="ab101-332">hello[健康狀態查詢](service-fabric-view-entities-aggregated-health.md#health-queries)傳回的只是第一層子系的 hello 指定每個必要的篩選條件的實體。</span><span class="sxs-lookup"><span data-stu-id="ab101-332">hello [health queries](service-fabric-view-entities-aggregated-health.md#health-queries) return only first-level children of hello specified entity per required filters.</span></span> <span data-ttu-id="ab101-333">tooget hello 子系的 hello 子系，您必須呼叫其他健全狀況 Api 針對每個感興趣的實體。</span><span class="sxs-lookup"><span data-stu-id="ab101-333">tooget hello children of hello children, you must call additional health APIs for each entity of interest.</span></span> <span data-ttu-id="ab101-334">同樣地，tooget hello 健全狀況的特定實體，您必須呼叫一個健全狀況 API 所需的每個實體。</span><span class="sxs-lookup"><span data-stu-id="ab101-334">Similarly, tooget hello health of specific entities, you must call one health API for each desired entity.</span></span> <span data-ttu-id="ab101-335">hello 區塊查詢進階篩選可讓您 toorequest hello 訊息大小和 hello 訊息數目降到最低的一個查詢中感興趣的多個項目。</span><span class="sxs-lookup"><span data-stu-id="ab101-335">hello chunk query advanced filtering allows you toorequest multiple items of interest in one query, minimizing hello message size and hello number of messages.</span></span>

<span data-ttu-id="ab101-336">hello 值 hello 區塊查詢的是，您可以在單一呼叫中的多個叢集實體 （潛在所有叢集實體開始必要的根） 取得健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="ab101-336">hello value of hello chunk query is that you can get health state for more cluster entities (potentially all cluster entities starting at required root) in one call.</span></span> <span data-ttu-id="ab101-337">您可以如下表示複雜的健全狀況查詢︰</span><span class="sxs-lookup"><span data-stu-id="ab101-337">You can express complex health query such as:</span></span>

* <span data-ttu-id="ab101-338">只傳回發生錯誤的應用程式，以及針對這些應用程式，包含所有發生警告或錯誤的服務。</span><span class="sxs-lookup"><span data-stu-id="ab101-338">Return only applications in error, and for those applications include all services in warning or error.</span></span> <span data-ttu-id="ab101-339">針對傳回的服務，包含所有分割。</span><span class="sxs-lookup"><span data-stu-id="ab101-339">For returned services, include all partitions.</span></span>
* <span data-ttu-id="ab101-340">傳回只有四個應用程式，其名稱所指定的 hello 健全狀況。</span><span class="sxs-lookup"><span data-stu-id="ab101-340">Return only hello health of four applications, specified by their names.</span></span>
* <span data-ttu-id="ab101-341">傳回只 hello 健全狀況所需的應用程式類型的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ab101-341">Return only hello health of applications of a desired application type.</span></span>
* <span data-ttu-id="ab101-342">傳回單一節點上所有已部署的實體。</span><span class="sxs-lookup"><span data-stu-id="ab101-342">Return all deployed entities on a node.</span></span> <span data-ttu-id="ab101-343">傳回所有的應用程式、 hello 指定節點上已部署的所有應用程式和所有部署的 hello 服務封裝，該節點上。</span><span class="sxs-lookup"><span data-stu-id="ab101-343">Returns all applications, all deployed applications on hello specified node and all hello deployed service packages on that node.</span></span>
* <span data-ttu-id="ab101-344">傳回所有發生錯誤的複本。</span><span class="sxs-lookup"><span data-stu-id="ab101-344">Return all replicas in error.</span></span> <span data-ttu-id="ab101-345">傳回所有應用程式、服務、磁碟分割，以及只傳回發生錯誤的複本。</span><span class="sxs-lookup"><span data-stu-id="ab101-345">Returns all applications, services, partitions, and only replicas in error.</span></span>
* <span data-ttu-id="ab101-346">傳回所有應用程式。</span><span class="sxs-lookup"><span data-stu-id="ab101-346">Return all applications.</span></span> <span data-ttu-id="ab101-347">針對指定的服務，包含所有分割。</span><span class="sxs-lookup"><span data-stu-id="ab101-347">For a specified service, include all partitions.</span></span>

<span data-ttu-id="ab101-348">目前，hello 健全狀況區塊查詢公開只 for hello 叢集實體。</span><span class="sxs-lookup"><span data-stu-id="ab101-348">Currently, hello health chunk query is exposed only for hello cluster entity.</span></span> <span data-ttu-id="ab101-349">它會傳回叢集健全狀況區塊，其中包含︰</span><span class="sxs-lookup"><span data-stu-id="ab101-349">It returns a cluster health chunk, which contains:</span></span>

* <span data-ttu-id="ab101-350">hello 叢集彙總健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="ab101-350">hello cluster aggregated health state.</span></span>
* <span data-ttu-id="ab101-351">hello 健全狀況狀態區塊的節點清單尊重輸入篩選器。</span><span class="sxs-lookup"><span data-stu-id="ab101-351">hello health state chunk list of nodes that respect input filters.</span></span>
* <span data-ttu-id="ab101-352">hello 健全狀況狀態的區塊清單尊重輸入篩選器的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ab101-352">hello health state chunk list of applications that respect input filters.</span></span> <span data-ttu-id="ab101-353">每個應用程式健全狀況狀態區塊尊重輸入篩選器和尊重 hello 篩選條件的所有已部署應用程式區塊清單的所有服務都包含區塊清單。</span><span class="sxs-lookup"><span data-stu-id="ab101-353">Each application health state chunk contains a chunk list with all services that respect input filters and a chunk list with all deployed applications that respect hello filters.</span></span> <span data-ttu-id="ab101-354">相同的 hello 的服務和已部署的應用程式的子系。</span><span class="sxs-lookup"><span data-stu-id="ab101-354">Same for hello children of services and deployed applications.</span></span> <span data-ttu-id="ab101-355">如此一來，hello 叢集中的所有實體可能會都傳回要求，以階層方式。</span><span class="sxs-lookup"><span data-stu-id="ab101-355">This way, all entities in hello cluster can be potentially returned if requested, in a hierarchical fashion.</span></span>

### <a name="cluster-health-chunk-query"></a><span data-ttu-id="ab101-356">叢集健全狀況區塊查詢</span><span class="sxs-lookup"><span data-stu-id="ab101-356">Cluster health chunk query</span></span>
<span data-ttu-id="ab101-357">會傳回 hello hello 叢集中實體的健全狀況，並包含必要的子系的 hello 階層的健全狀況狀態的區塊。</span><span class="sxs-lookup"><span data-stu-id="ab101-357">Returns hello health of hello cluster entity and contains hello hierarchical health state chunks of required children.</span></span> <span data-ttu-id="ab101-358">輸入：</span><span class="sxs-lookup"><span data-stu-id="ab101-358">Input:</span></span>

* <span data-ttu-id="ab101-359">[選用] hello 叢集健全狀況原則會使用 tooevaluate hello 節點和 hello 叢集事件。</span><span class="sxs-lookup"><span data-stu-id="ab101-359">[Optional] hello cluster health policy used tooevaluate hello nodes and hello cluster events.</span></span>
* <span data-ttu-id="ab101-360">[選用] hello 應用程式健全狀況原則對應 hello 健康原則使用 toooverride hello 應用程式資訊清單的原則。</span><span class="sxs-lookup"><span data-stu-id="ab101-360">[Optional] hello application health policy map, with hello health policies used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="ab101-361">[選用]節點和指定感興趣的項目，且傳回 hello 結果中的應用程式的篩選條件。</span><span class="sxs-lookup"><span data-stu-id="ab101-361">[Optional] Filters for nodes and applications that specify which entries are of interest and should be returned in hello result.</span></span> <span data-ttu-id="ab101-362">hello 篩選特定 tooan 實體/群組的實體或適用 tooall 該層級的實體。</span><span class="sxs-lookup"><span data-stu-id="ab101-362">hello filters are specific tooan entity/group of entities or are applicable tooall entities at that level.</span></span> <span data-ttu-id="ab101-363">hello 篩選器清單可以包含一個一般篩選器和/或特定的識別項 toofine 資料粒度實體 hello 查詢所傳回的篩選。</span><span class="sxs-lookup"><span data-stu-id="ab101-363">hello list of filters can contain one general filter and/or filters for specific identifiers toofine-grain entities returned by hello query.</span></span> <span data-ttu-id="ab101-364">如果是空的預設不會傳回 hello 子系。</span><span class="sxs-lookup"><span data-stu-id="ab101-364">If empty, hello children are not returned by default.</span></span>
  <span data-ttu-id="ab101-365">深入了解在 hello 篩選[NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter)和[ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter)。</span><span class="sxs-lookup"><span data-stu-id="ab101-365">Read more about hello filters at [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) and [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter).</span></span> <span data-ttu-id="ab101-366">hello 應用程式篩選器可遞迴指定進階的篩選器的子系。</span><span class="sxs-lookup"><span data-stu-id="ab101-366">hello application filters can recursively specify advanced filters for children.</span></span>

<span data-ttu-id="ab101-367">hello 區塊結果包含尊重 hello 篩選的 hello 子系。</span><span class="sxs-lookup"><span data-stu-id="ab101-367">hello chunk result includes hello children that respect hello filters.</span></span>

<span data-ttu-id="ab101-368">目前，hello 區塊查詢不會傳回處於狀況不良的評估或實體的事件。</span><span class="sxs-lookup"><span data-stu-id="ab101-368">Currently, hello chunk query does not return unhealthy evaluations or entity events.</span></span> <span data-ttu-id="ab101-369">可以使用現有叢集健全狀況查詢 hello 取得額外資訊。</span><span class="sxs-lookup"><span data-stu-id="ab101-369">That extra information can be obtained using hello existing cluster health query.</span></span>

### <a name="api"></a><span data-ttu-id="ab101-370">API</span><span class="sxs-lookup"><span data-stu-id="ab101-370">API</span></span>
<span data-ttu-id="ab101-371">tooget 叢集健全狀況區塊中，建立`FabricClient`和呼叫 hello [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync)方法上的其**HealthManager**。</span><span class="sxs-lookup"><span data-stu-id="ab101-371">tooget cluster health chunk, create a `FabricClient` and call hello [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) method on its **HealthManager**.</span></span> <span data-ttu-id="ab101-372">您可以傳入[ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) toodescribe 健全狀況原則和進階篩選器。</span><span class="sxs-lookup"><span data-stu-id="ab101-372">You can pass in [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) toodescribe health policies and advanced filters.</span></span>

<span data-ttu-id="ab101-373">hello 下列程式碼取得叢集健全狀況區塊與進階篩選器。</span><span class="sxs-lookup"><span data-stu-id="ab101-373">hello following code gets cluster health chunk with advanced filters.</span></span>

```csharp
var queryDescription = new ClusterHealthChunkQueryDescription();
queryDescription.ApplicationFilters.Add(new ApplicationHealthStateFilter()
    {
        // Return applications only if they are in error
        HealthStateFilter = HealthStateFilter.Error
    });

// Return all replicas
var wordCountServiceReplicaFilter = new ReplicaHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };

// Return all replicas and all partitions
var wordCountServicePartitionFilter = new PartitionHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };
wordCountServicePartitionFilter.ReplicaFilters.Add(wordCountServiceReplicaFilter);

// For specific service, return all partitions and all replicas
var wordCountServiceFilter = new ServiceHealthStateFilter()
{
    ServiceNameFilter = new Uri("fabric:/WordCount/WordCountService"),
};
wordCountServiceFilter.PartitionFilters.Add(wordCountServicePartitionFilter);

// Application filter: for specific application, return no services except hello ones of interest
var wordCountApplicationFilter = new ApplicationHealthStateFilter()
    {
        // Always return fabric:/WordCount application
        ApplicationNameFilter = new Uri("fabric:/WordCount"),
    };
wordCountApplicationFilter.ServiceFilters.Add(wordCountServiceFilter);

queryDescription.ApplicationFilters.Add(wordCountApplicationFilter);

var result = await fabricClient.HealthManager.GetClusterHealthChunkAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="ab101-374">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ab101-374">PowerShell</span></span>
<span data-ttu-id="ab101-375">hello cmdlet tooget hello 叢集健全狀況是[Get ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk)。</span><span class="sxs-lookup"><span data-stu-id="ab101-375">hello cmdlet tooget hello cluster health is [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk).</span></span> <span data-ttu-id="ab101-376">首先，使用 hello 連線 toohello 叢集[Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="ab101-376">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="ab101-377">hello 下列程式碼會取得節點只有當它們位於除了特定的節點，一律會傳回錯誤。</span><span class="sxs-lookup"><span data-stu-id="ab101-377">hello following code gets nodes only if they are in Error except for a specific node, which should always be returned.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$nodeFilter1 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{HealthStateFilter=$errorFilter}
$nodeFilter2 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{NodeNameFilter="_Node_1";HealthStateFilter=$allFilter}
# Create node filter list that will be passed in hello cmdlet
$nodeFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.NodeHealthStateFilter]
$nodeFilters.Add($nodeFilter1)
$nodeFilters.Add($nodeFilter2)

Get-ServiceFabricClusterHealthChunk -NodeFilters $nodeFilters


HealthState                  : Warning
NodeHealthStateChunks        : 
                               TotalCount            : 1
                               
                               NodeName              : _Node_1
                               HealthState           : Ok
                               
ApplicationHealthStateChunks : None
```

<span data-ttu-id="ab101-378">hello 下列 cmdlet 會取得叢集區塊與應用程式篩選器。</span><span class="sxs-lookup"><span data-stu-id="ab101-378">hello following cmdlet gets cluster chunk with application filters.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

# All replicas
$replicaFilter = New-Object System.Fabric.Health.ReplicaHealthStateFilter -Property @{HealthStateFilter=$allFilter}

# All partitions
$partitionFilter = New-Object System.Fabric.Health.PartitionHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$partitionFilter.ReplicaFilters.Add($replicaFilter)

# For WordCountService, return all partitions and all replicas
$svcFilter1 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{ServiceNameFilter="fabric:/WordCount/WordCountService"}
$svcFilter1.PartitionFilters.Add($partitionFilter)

$svcFilter2 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{HealthStateFilter=$errorFilter}

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{ApplicationNameFilter="fabric:/WordCount"}
$appFilter.ServiceFilters.Add($svcFilter1)
$appFilter.ServiceFilters.Add($svcFilter2)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)

Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 1
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               ServiceHealthStateChunks : 
                                TotalCount            : 1
                               
                                ServiceName           : fabric:/WordCount/WordCountService
                                HealthState           : Error
                                PartitionHealthStateChunks : 
                                    TotalCount            : 1
                               
                                    PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                                    HealthState           : Error
                                    ReplicaHealthStateChunks : 
                                        TotalCount            : 5
                               
                                        ReplicaOrInstanceId   : 131444422293118720
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293118721
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113678
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113679
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422260002646
                                        HealthState           : Error
```

<span data-ttu-id="ab101-379">hello 下列 cmdlet 會傳回已部署的所有實體節點上。</span><span class="sxs-lookup"><span data-stu-id="ab101-379">hello following cmdlet returns all deployed entities on a node.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$dspFilter = New-Object System.Fabric.Health.DeployedServicePackageHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$daFilter =  New-Object System.Fabric.Health.DeployedApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter;NodeNameFilter="_Node_2"}
$daFilter.DeployedServicePackageFilters.Add($dspFilter)

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$appFilter.DeployedApplicationFilters.Add($daFilter)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)
Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 2
                               
                               ApplicationName       : fabric:/System
                               HealthState           : Ok
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : FAS
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
                               
                               
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : WordCountServicePkg
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
```

### <a name="rest"></a><span data-ttu-id="ab101-380">REST</span><span class="sxs-lookup"><span data-stu-id="ab101-380">REST</span></span>
<span data-ttu-id="ab101-381">您可以取得叢集健全狀況區塊與[GET 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks)或[POST 要求](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster)內含健全狀況原則和 hello 本文所述的進階篩選器。</span><span class="sxs-lookup"><span data-stu-id="ab101-381">You can get cluster health chunk with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) that includes health policies and advanced filters described in hello body.</span></span>

## <a name="general-queries"></a><span data-ttu-id="ab101-382">一般查詢</span><span class="sxs-lookup"><span data-stu-id="ab101-382">General queries</span></span>
<span data-ttu-id="ab101-383">一般查詢會傳回指定類型的 Service Fabric 實體清單。</span><span class="sxs-lookup"><span data-stu-id="ab101-383">General queries return a list of Service Fabric entities of a specified type.</span></span> <span data-ttu-id="ab101-384">這些元素會公開透過 hello 應用程式開發介面 (透過 hello 方法上**FabricClient.QueryManager**)、 PowerShell cmdlet 和 REST。</span><span class="sxs-lookup"><span data-stu-id="ab101-384">They are exposed through hello API (via hello methods on **FabricClient.QueryManager**), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="ab101-385">這些查詢會從多個元件彙總子查詢。</span><span class="sxs-lookup"><span data-stu-id="ab101-385">These queries aggregate subqueries from multiple components.</span></span> <span data-ttu-id="ab101-386">其中一個為 hello[健全狀況存放區](service-fabric-health-introduction.md#health-store)，其中會填入 hello 彙總的每個查詢結果的健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="ab101-386">One of them is hello [health store](service-fabric-health-introduction.md#health-store), which populates hello aggregated health state for each query result.</span></span>  

> [!NOTE]
> <span data-ttu-id="ab101-387">一般查詢傳回 hello 實體 hello 彙總健全狀況狀態，並且不包含豐富的健全狀況資料。</span><span class="sxs-lookup"><span data-stu-id="ab101-387">General queries return hello aggregated health state of hello entity and do not contain rich health data.</span></span> <span data-ttu-id="ab101-388">如果實體未正常運作，您可以追蹤健全狀況查詢 tooget 所有其健全狀況資訊，包括事件、 子健全狀況狀態和狀況不良的評估。</span><span class="sxs-lookup"><span data-stu-id="ab101-388">If an entity is not healthy, you can follow up with health queries tooget all its health information, including events, child health states, and unhealthy evaluations.</span></span>
>
>

<span data-ttu-id="ab101-389">如果一般查詢會傳回實體的未知的健全狀況狀態，則可能該 hello 健全狀況存放區不會有完整的 hello 實體的資料。</span><span class="sxs-lookup"><span data-stu-id="ab101-389">If general queries return an unknown health state for an entity, it's possible that hello health store doesn't have complete data about hello entity.</span></span> <span data-ttu-id="ab101-390">此外，也可以為子查詢 toohello 健全狀況存放區未成功 （例如，發生通訊錯誤，或 hello 健全狀況存放區已節流處理）。</span><span class="sxs-lookup"><span data-stu-id="ab101-390">It's also possible that a subquery toohello health store wasn't successful (for example, there was a communication error, or hello health store was throttled).</span></span> <span data-ttu-id="ab101-391">追蹤 hello 實體的健全狀況查詢。</span><span class="sxs-lookup"><span data-stu-id="ab101-391">Follow up with a health query for hello entity.</span></span> <span data-ttu-id="ab101-392">如果 hello 子查詢發生暫時性錯誤，例如網路問題，此待處理的查詢可能會成功。</span><span class="sxs-lookup"><span data-stu-id="ab101-392">If hello subquery encountered transient errors, such as network issues, this follow-up query may succeed.</span></span> <span data-ttu-id="ab101-393">它也可以提供更多詳細資料從 hello health store 有關 hello 實體未公開的原因。</span><span class="sxs-lookup"><span data-stu-id="ab101-393">It may also give you more details from hello health store about why hello entity is not exposed.</span></span>

<span data-ttu-id="ab101-394">hello 包含查詢**HealthState**的實體包括：</span><span class="sxs-lookup"><span data-stu-id="ab101-394">hello queries that contain **HealthState** for entities are:</span></span>

* <span data-ttu-id="ab101-395">節點清單： hello 叢集中 （分頁） 傳回 hello 清單節點。</span><span class="sxs-lookup"><span data-stu-id="ab101-395">Node list: Returns hello list nodes in hello cluster (paged).</span></span>
  * <span data-ttu-id="ab101-396">API： [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span><span class="sxs-lookup"><span data-stu-id="ab101-396">API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span></span>
  * <span data-ttu-id="ab101-397">PowerShell：Get-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="ab101-397">PowerShell: Get-ServiceFabricNode</span></span>
* <span data-ttu-id="ab101-398">應用程式清單： 傳回 hello （分頁） hello 叢集中的應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="ab101-398">Application list: Returns hello list of applications in hello cluster (paged).</span></span>
  * <span data-ttu-id="ab101-399">API： [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="ab101-399">API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span></span>
  * <span data-ttu-id="ab101-400">PowerShell：Get-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="ab101-400">PowerShell: Get-ServiceFabricApplication</span></span>
* <span data-ttu-id="ab101-401">服務清單: （分頁） 的應用程式中的服務傳回 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="ab101-401">Service list: Returns hello list of services in an application (paged).</span></span>
  * <span data-ttu-id="ab101-402">API： [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span><span class="sxs-lookup"><span data-stu-id="ab101-402">API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span></span>
  * <span data-ttu-id="ab101-403">PowerShell：Get-ServiceFabricService</span><span class="sxs-lookup"><span data-stu-id="ab101-403">PowerShell: Get-ServiceFabricService</span></span>
* <span data-ttu-id="ab101-404">資料分割清單: （分頁） 服務中的資料分割傳回 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="ab101-404">Partition list: Returns hello list of partitions in a service (paged).</span></span>
  * <span data-ttu-id="ab101-405">API： [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span><span class="sxs-lookup"><span data-stu-id="ab101-405">API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span></span>
  * <span data-ttu-id="ab101-406">PowerShell：Get-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="ab101-406">PowerShell: Get-ServiceFabricPartition</span></span>
* <span data-ttu-id="ab101-407">複本清單： 傳回 hello 份資料分割 （分頁） 中的複本。</span><span class="sxs-lookup"><span data-stu-id="ab101-407">Replica list: Returns hello list of replicas in a partition (paged).</span></span>
  * <span data-ttu-id="ab101-408">API： [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span><span class="sxs-lookup"><span data-stu-id="ab101-408">API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span></span>
  * <span data-ttu-id="ab101-409">PowerShell：Get-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="ab101-409">PowerShell: Get-ServiceFabricReplica</span></span>
* <span data-ttu-id="ab101-410">部署應用程式清單： 傳回 hello 清單的節點上已部署的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ab101-410">Deployed application list: Returns hello list of deployed applications on a node.</span></span>
  * <span data-ttu-id="ab101-411">API： [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="ab101-411">API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span></span>
  * <span data-ttu-id="ab101-412">PowerShell：Get-ServiceFabricDeployedApplication</span><span class="sxs-lookup"><span data-stu-id="ab101-412">PowerShell: Get-ServiceFabricDeployedApplication</span></span>
* <span data-ttu-id="ab101-413">部署服務套件清單： 傳回 hello 服務中的封裝清單部署的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ab101-413">Deployed service package list: Returns hello list of service packages in a deployed application.</span></span>
  * <span data-ttu-id="ab101-414">API： [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span><span class="sxs-lookup"><span data-stu-id="ab101-414">API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span></span>
  * <span data-ttu-id="ab101-415">PowerShell：Get-ServiceFabricDeployedApplication</span><span class="sxs-lookup"><span data-stu-id="ab101-415">PowerShell: Get-ServiceFabricDeployedApplication</span></span>

> [!NOTE]
> <span data-ttu-id="ab101-416">某些 hello 查詢傳回分頁的結果。</span><span class="sxs-lookup"><span data-stu-id="ab101-416">Some of hello queries return paged results.</span></span> <span data-ttu-id="ab101-417">hello 傳回這些查詢是清單衍生自[PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1)。</span><span class="sxs-lookup"><span data-stu-id="ab101-417">hello return of these queries is a list derived from [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1).</span></span> <span data-ttu-id="ab101-418">如果 hello 結果未納入一則訊息，只會傳回頁並 ContinuationToken，可以追蹤列舉的停止處。</span><span class="sxs-lookup"><span data-stu-id="ab101-418">If hello results do not fit a message, only a page is returned and a ContinuationToken that tracks where enumeration stopped.</span></span> <span data-ttu-id="ab101-419">繼續 toocall hello 相同查詢，並傳入 hello 接續 token，從 hello 先前查詢 tooget 下一個結果。</span><span class="sxs-lookup"><span data-stu-id="ab101-419">Continue toocall hello same query and pass in hello continuation token from hello previous query tooget next results.</span></span>
>
>

### <a name="examples"></a><span data-ttu-id="ab101-420">範例</span><span class="sxs-lookup"><span data-stu-id="ab101-420">Examples</span></span>
<span data-ttu-id="ab101-421">hello 下列程式碼會取得 hello 狀況不良的應用程式中 hello 叢集：</span><span class="sxs-lookup"><span data-stu-id="ab101-421">hello following code gets hello unhealthy applications in hello cluster:</span></span>

```csharp
var applications = fabricClient.QueryManager.GetApplicationListAsync().Result.Where(
  app => app.HealthState == HealthState.Error);
```

<span data-ttu-id="ab101-422">hello 下列 cmdlet 會取得 hello hello 網狀架構的應用程式詳細資料: / WordCount 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ab101-422">hello following cmdlet gets hello application details for hello fabric:/WordCount application.</span></span> <span data-ttu-id="ab101-423">請注意，健康情況狀態為警告。</span><span class="sxs-lookup"><span data-stu-id="ab101-423">Notice that health state is at warning.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplication -ApplicationName fabric:/WordCount

ApplicationName        : fabric:/WordCount
ApplicationTypeName    : WordCount
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Warning
ApplicationParameters  : { "WordCountWebService_InstanceCount" = "1";
                         "_WFDebugParams_" = "[{"ServiceManifestName":"WordCountWebServicePkg","CodePackageName":"Code","EntryPointType":"Main","Debug
                         ExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {74f7e5d5-71a9-47e2-a8cd-1878ec4734f1} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"},{"ServiceManifestName":"WordCountServicePkg","CodeP
                         ackageName":"Code","EntryPointType":"Main","DebugExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {2ab462e6-e0d1-4fda-a844-972f561fe751} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"}]" }
```

<span data-ttu-id="ab101-424">hello 下列 cmdlet 會取得 hello 服務健全狀況狀態，錯誤為：</span><span class="sxs-lookup"><span data-stu-id="ab101-424">hello following cmdlet gets hello services with a health state of error:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplication | Get-ServiceFabricService | where {$_.HealthState -eq "Error"}


ServiceName            : fabric:/WordCount/WordCountService
ServiceKind            : Stateful
ServiceTypeName        : WordCountServiceType
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
HasPersistedState      : True
ServiceStatus          : Active
HealthState            : Error
```

## <a name="cluster-and-application-upgrades"></a><span data-ttu-id="ab101-425">叢集和應用程式升級</span><span class="sxs-lookup"><span data-stu-id="ab101-425">Cluster and application upgrades</span></span>
<span data-ttu-id="ab101-426">監視在升級期間的 hello 叢集和應用程式，Service Fabric 會檢查所有項目維持良好健康情況 tooensure。</span><span class="sxs-lookup"><span data-stu-id="ab101-426">During a monitored upgrade of hello cluster and application, Service Fabric checks health tooensure that everything remains healthy.</span></span> <span data-ttu-id="ab101-427">如果實體是使用 設定健全狀況原則評估為狀況不良，hello 升級適用於升級特定原則 toodetermine hello 下一個動作。</span><span class="sxs-lookup"><span data-stu-id="ab101-427">If an entity is unhealthy as evaluated by using configured health policies, hello upgrade applies upgrade-specific policies toodetermine hello next action.</span></span> <span data-ttu-id="ab101-428">hello 升級可能會暫停的 tooallow 使用者互動 （例如修正錯誤條件或變更原則），或它可能會自動回復 toohello 良好舊版。</span><span class="sxs-lookup"><span data-stu-id="ab101-428">hello upgrade may be paused tooallow user interaction (such as fixing error conditions or changing policies), or it may automatically roll back toohello previous good version.</span></span>

<span data-ttu-id="ab101-429">期間*叢集*升級，您可以取得 hello 叢集的升級狀態。</span><span class="sxs-lookup"><span data-stu-id="ab101-429">During a *cluster* upgrade, you can get hello cluster upgrade status.</span></span> <span data-ttu-id="ab101-430">hello 升級狀態包括狀況不良的評估，哪一個點 toowhat 狀況不良 hello 叢集中。</span><span class="sxs-lookup"><span data-stu-id="ab101-430">hello upgrade status includes unhealthy evaluations, which point toowhat is unhealthy in hello cluster.</span></span> <span data-ttu-id="ab101-431">如果 hello 升級回復 toohealth 問題到期，hello 升級狀態會記住 hello 上次狀況不良的原因。</span><span class="sxs-lookup"><span data-stu-id="ab101-431">If hello upgrade is rolled back due toohealth issues, hello upgrade status remembers hello last unhealthy reasons.</span></span> <span data-ttu-id="ab101-432">這項資訊可協助系統管理員調查 hello 升級復原或停止之後發生錯誤的原因。</span><span class="sxs-lookup"><span data-stu-id="ab101-432">This information can help administrators investigate what went wrong after hello upgrade rolled back or stopped.</span></span>

<span data-ttu-id="ab101-433">同樣地，在下列期間*應用程式*升級，任何處於狀況不良的評估中所包含 hello 應用程式升級狀態。</span><span class="sxs-lookup"><span data-stu-id="ab101-433">Similarly, during an *application* upgrade, any unhealthy evaluations are contained in hello application upgrade status.</span></span>

<span data-ttu-id="ab101-434">hello 下列範例示範 hello 應用程式升級狀態為已修改光纖: / WordCount 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ab101-434">hello following shows hello application upgrade status for a modified fabric:/WordCount application.</span></span> <span data-ttu-id="ab101-435">監視程式回報了它其中一個複本的錯誤。</span><span class="sxs-lookup"><span data-stu-id="ab101-435">A watchdog reported an error on one of its replicas.</span></span> <span data-ttu-id="ab101-436">hello 升級循環，因為未遵守 hello 健康情況檢查。</span><span class="sxs-lookup"><span data-stu-id="ab101-436">hello upgrade is rolling back because hello health checks are not respected.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationUpgrade fabric:/WordCount

ApplicationName               : fabric:/WordCount
ApplicationTypeName           : WordCount
TargetApplicationTypeVersion  : 1.0.0.0
ApplicationParameters         : {}
StartTimestampUtc             : 4/21/2017 5:23:26 PM
FailureTimestampUtc           : 4/21/2017 5:23:37 PM
FailureReason                 : HealthCheck
UpgradeState                  : RollingBackInProgress
UpgradeDuration               : 00:00:23
CurrentUpgradeDomainDuration  : 00:00:00
CurrentUpgradeDomainProgress  : UD1

                                NodeName            : _Node_1
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_2
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_3
                                UpgradePhase        : PreUpgradeSafetyCheck
                                PendingSafetyChecks :
                                EnsurePartitionQuorum - PartitionId: 30db5be6-4e20-4698-8185-4bd7ca744020
NextUpgradeDomain             : UD2
UpgradeDomainsStatus          : { "UD1" = "Completed";
                                "UD2" = "Pending";
                                "UD3" = "Pending";
                                "UD4" = "Pending" }
UnhealthyEvaluations          :
                                Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.

                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.

                                      Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                      Unhealthy partition: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b', AggregatedHealthState='Error'.

                                          Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.

                                          Unhealthy replica: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b',
                                  ReplicaOrInstanceId='131031502346844058', AggregatedHealthState='Error'.

                                              Error event: SourceId='DiskWatcher', Property='Disk'.

UpgradeKind                   : Rolling
RollingUpgradeMode            : UnmonitoredAuto
ForceRestart                  : False
UpgradeReplicaSetCheckTimeout : 00:15:00
```

<span data-ttu-id="ab101-437">深入了解 hello [Service Fabric 應用程式升級](service-fabric-application-upgrade.md)。</span><span class="sxs-lookup"><span data-stu-id="ab101-437">Read more about hello [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="use-health-evaluations-tootroubleshoot"></a><span data-ttu-id="ab101-438">使用健全狀況評估 tootroubleshoot</span><span class="sxs-lookup"><span data-stu-id="ab101-438">Use health evaluations tootroubleshoot</span></span>
<span data-ttu-id="ab101-439">Hello 叢集或應用程式發生問題時，看看 hello 叢集或應用程式健全狀況 toopinpoint 錯誤。</span><span class="sxs-lookup"><span data-stu-id="ab101-439">Whenever there is an issue with hello cluster or an application, look at hello cluster or application health toopinpoint what is wrong.</span></span> <span data-ttu-id="ab101-440">hello 狀況不良的評估會提供有關哪些觸發的 hello 目前狀況不良狀態詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ab101-440">hello unhealthy evaluations provide details about what triggered hello current unhealthy state.</span></span> <span data-ttu-id="ab101-441">如果需要您可以切入至狀況不良的子實體 tooidentify hello 根本原因。</span><span class="sxs-lookup"><span data-stu-id="ab101-441">If you need to, you can drill down into unhealthy child entities tooidentify hello root cause.</span></span>

<span data-ttu-id="ab101-442">例如，將應用程式視為健康情況不良，因為有其中一個複本的錯誤報告。</span><span class="sxs-lookup"><span data-stu-id="ab101-442">For example, consider an application unhealthy because there is an error report on one of its replicas.</span></span> <span data-ttu-id="ab101-443">hello 下列 Powershell 指令程式會顯示 hello 狀況不良的評估：</span><span class="sxs-lookup"><span data-stu-id="ab101-443">hello following Powershell cmdlet shows hello unhealthy evaluations:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount -EventsFilter None -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.
                                  
                                        Unhealthy replica: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', ReplicaOrInstanceId='131444422260002646', AggregatedHealthState='Error'.
                                  
                                            Error event: SourceId='MyWatchdog', Property='Memory'.
                                  
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

<span data-ttu-id="ab101-444">您可以查看 hello 複本 tooget 的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="ab101-444">You can look at hello replica tooget more information:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricReplicaHealth -ReplicaOrInstanceId 131444422260002646 -PartitionId af2e3e44-a8f8-45ac-9f31-4093eb897600


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Error
UnhealthyEvaluations  : 
                        Error event: SourceId='MyWatchdog', Property='Memory'.
                        
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
                        SourceId              : MyWatchdog
                        Property              : Memory
                        HealthState           : Error
                        SequenceNumber        : 131444451657749403
                        SentAt                : 7/13/2017 6:46:05 PM
                        ReceivedAt            : 7/13/2017 6:46:05 PM
                        TTL                   : Infinite
                        Description           : 
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 7/13/2017 6:46:05 PM, LastOk = 1/1/0001 12:00:00 AM
```

> [!NOTE]
> <span data-ttu-id="ab101-445">hello 狀況不良的評估顯示 hello 第一個原因 hello 實體被評估 toocurrent 健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="ab101-445">hello unhealthy evaluations show hello first reason hello entity is evaluated toocurrent health state.</span></span> <span data-ttu-id="ab101-446">可能有多個觸發此狀態下，其他事件，但不是會反映在 hello 評估。</span><span class="sxs-lookup"><span data-stu-id="ab101-446">There may be multiple other events that trigger this state, but they are not be reflected in hello evaluations.</span></span> <span data-ttu-id="ab101-447">tooget 的詳細資訊，向下切入至 hello 健全狀況實體 toofigure hello 叢集中的 hello 處於不健全狀況報表。</span><span class="sxs-lookup"><span data-stu-id="ab101-447">tooget more information, drill down into hello health entities toofigure out all hello unhealthy reports in hello cluster.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="ab101-448">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ab101-448">Next steps</span></span>
[<span data-ttu-id="ab101-449">使用系統健全狀況報表 tootroubleshoot</span><span class="sxs-lookup"><span data-stu-id="ab101-449">Use system health reports tootroubleshoot</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[<span data-ttu-id="ab101-450">新增自訂 Service Fabric 健康狀態報告</span><span class="sxs-lookup"><span data-stu-id="ab101-450">Add custom Service Fabric health reports</span></span>](service-fabric-report-health.md)

[<span data-ttu-id="ab101-451">Tooreport 並檢查服務健全狀況</span><span class="sxs-lookup"><span data-stu-id="ab101-451">How tooreport and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="ab101-452">在本機上監視及診斷服務</span><span class="sxs-lookup"><span data-stu-id="ab101-452">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="ab101-453">Service Fabric 應用程式升級</span><span class="sxs-lookup"><span data-stu-id="ab101-453">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)
