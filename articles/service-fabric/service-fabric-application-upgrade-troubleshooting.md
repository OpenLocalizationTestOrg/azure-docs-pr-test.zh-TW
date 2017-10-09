---
title: "aaaTroubleshooting 應用程式升級 |Microsoft 文件"
description: "本文章涵蓋一些常見的問題解決升級 Service Fabric 應用程式以及如何 tooresolve 它們。"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 19ad152e-ec50-4327-9f19-065c875c003c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 0f56fa61db9b4e32824623f162dc1bfe7fda0f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-application-upgrades"></a><span data-ttu-id="73fbd-103">疑難排解應用程式升級</span><span class="sxs-lookup"><span data-stu-id="73fbd-103">Troubleshoot application upgrades</span></span>
<span data-ttu-id="73fbd-104">本文章涵蓋 hello 常見的問題解決升級 Azure Service Fabric 應用程式以及如何 tooresolve 它們。</span><span class="sxs-lookup"><span data-stu-id="73fbd-104">This article covers some of hello common issues around upgrading an Azure Service Fabric application and how tooresolve them.</span></span>

## <a name="troubleshoot-a-failed-application-upgrade"></a><span data-ttu-id="73fbd-105">疑難排解失敗的應用程式升級</span><span class="sxs-lookup"><span data-stu-id="73fbd-105">Troubleshoot a failed application upgrade</span></span>
<span data-ttu-id="73fbd-106">當升級失敗時，輸出 hello hello **Get ServiceFabricApplicationUpgrade**命令包含偵錯 hello 失敗的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="73fbd-106">When an upgrade fails, hello output of hello **Get-ServiceFabricApplicationUpgrade** command contains additional information for debugging hello failure.</span></span>  <span data-ttu-id="73fbd-107">hello 下列清單會指定如何使用 hello 的其他資訊：</span><span class="sxs-lookup"><span data-stu-id="73fbd-107">hello following list specifies how hello additional information can be used:</span></span>

1. <span data-ttu-id="73fbd-108">識別 hello 失敗類型。</span><span class="sxs-lookup"><span data-stu-id="73fbd-108">Identify hello failure type.</span></span>
2. <span data-ttu-id="73fbd-109">識別 hello 失敗原因。</span><span class="sxs-lookup"><span data-stu-id="73fbd-109">Identify hello failure reason.</span></span>
3. <span data-ttu-id="73fbd-110">隔離一或多個失敗元件以便進一步調查。</span><span class="sxs-lookup"><span data-stu-id="73fbd-110">Isolate one or more failing components for further investigation.</span></span>

<span data-ttu-id="73fbd-111">這項資訊時，使用 Service Fabric 來偵測 hello 不論是否 hello **FailureAction** tooroll 後或暫停 hello 升級。</span><span class="sxs-lookup"><span data-stu-id="73fbd-111">This information is available when Service Fabric detects hello failure regardless of whether hello **FailureAction** is tooroll back or suspend hello upgrade.</span></span>

### <a name="identify-hello-failure-type"></a><span data-ttu-id="73fbd-112">識別 hello 失敗類型</span><span class="sxs-lookup"><span data-stu-id="73fbd-112">Identify hello failure type</span></span>
<span data-ttu-id="73fbd-113">中的 hello 輸出**Get ServiceFabricApplicationUpgrade**， **FailureTimestampUtc**識別 hello 時間戳記 （UTC) 在升級的失敗偵測到的 Service Fabric 和**FailureAction**觸發。</span><span class="sxs-lookup"><span data-stu-id="73fbd-113">In hello output of **Get-ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** identifies hello timestamp (in UTC) at which an upgrade failure was detected by Service Fabric and **FailureAction** was triggered.</span></span> <span data-ttu-id="73fbd-114">**失敗原因**識別其中三個潛在高層級失敗原因的 hello:</span><span class="sxs-lookup"><span data-stu-id="73fbd-114">**FailureReason** identifies one of three potential high-level causes of hello failure:</span></span>

1. <span data-ttu-id="73fbd-115">UpgradeDomainTimeout-表示特定的升級網域花費太長 toocomplete 和**UpgradeDomainTimeout**過期。</span><span class="sxs-lookup"><span data-stu-id="73fbd-115">UpgradeDomainTimeout - Indicates that a particular upgrade domain took too long toocomplete and **UpgradeDomainTimeout** expired.</span></span>
2. <span data-ttu-id="73fbd-116">OverallUpgradeTimeout-指出整體升級該 hello 花費太長 toocomplete 和**UpgradeTimeout**過期。</span><span class="sxs-lookup"><span data-stu-id="73fbd-116">OverallUpgradeTimeout - Indicates that hello overall upgrade took too long toocomplete and **UpgradeTimeout** expired.</span></span>
3. <span data-ttu-id="73fbd-117">在升級之後更新網域，hello 應用程式維持狀況不良的健全狀況檢查時發生-表示根據 toohello 指定健全狀況原則和**HealthCheckRetryTimeout**過期。</span><span class="sxs-lookup"><span data-stu-id="73fbd-117">HealthCheck - Indicates that after upgrading an update domain, hello application remained unhealthy according toohello specified health policies and **HealthCheckRetryTimeout** expired.</span></span>

<span data-ttu-id="73fbd-118">這些項目才會顯示在 hello 輸出時 hello 升級失敗，並開始復原。</span><span class="sxs-lookup"><span data-stu-id="73fbd-118">These entries only show up in hello output when hello upgrade fails and starts rolling back.</span></span> <span data-ttu-id="73fbd-119">根據 hello hello 失敗類型而定，會顯示進一步的資訊。</span><span class="sxs-lookup"><span data-stu-id="73fbd-119">Further information is displayed depending on hello type of hello failure.</span></span>

### <a name="investigate-upgrade-timeouts"></a><span data-ttu-id="73fbd-120">調查升級逾時</span><span class="sxs-lookup"><span data-stu-id="73fbd-120">Investigate upgrade timeouts</span></span>
<span data-ttu-id="73fbd-121">升級逾時失敗通常是由服務可用性問題造成的。</span><span class="sxs-lookup"><span data-stu-id="73fbd-121">Upgrade timeout failures are most commonly caused by service availability issues.</span></span> <span data-ttu-id="73fbd-122">遵循本段 hello 輸出是典型的升級服務複本或執行個體失敗 toostart hello 新版程式碼中。</span><span class="sxs-lookup"><span data-stu-id="73fbd-122">hello output following this paragraph is typical of upgrades where service replicas or instances fail toostart in hello new code version.</span></span> <span data-ttu-id="73fbd-123">hello **UpgradeDomainProgressAtFailure**欄位擷取的任何暫止的升級工作，在 hello 發生失敗時的快照集。</span><span class="sxs-lookup"><span data-stu-id="73fbd-123">hello **UpgradeDomainProgressAtFailure** field captures a snapshot of any pending upgrade work at hello time of failure.</span></span>

```
PS D:\temp> Get-ServiceFabricApplicationUpgrade fabric:/DemoApp

ApplicationName                : fabric:/DemoApp
ApplicationTypeName            : DemoAppType
TargetApplicationTypeVersion   : v2
ApplicationParameters          : {}
StartTimestampUtc              : 4/14/2015 9:26:38 PM
FailureTimestampUtc            : 4/14/2015 9:27:05 PM
FailureReason                  : UpgradeDomainTimeout
UpgradeDomainProgressAtFailure : MYUD1

                                 NodeName            : Node4
                                 UpgradePhase        : PostUpgradeSafetyCheck
                                 PendingSafetyChecks :
                                     WaitForPrimaryPlacement - PartitionId: 744c8d9f-1d26-417e-a60e-cd48f5c098f0

                                 NodeName            : Node1
                                 UpgradePhase        : PostUpgradeSafetyCheck
                                 PendingSafetyChecks :
                                     WaitForPrimaryPlacement - PartitionId: 4b43f4d8-b26b-424e-9307-7a7a62e79750
UpgradeState                   : RollingBackCompleted
UpgradeDuration                : 00:00:46
CurrentUpgradeDomainDuration   : 00:00:00
NextUpgradeDomain              :
UpgradeDomainsStatus           : { "MYUD1" = "Completed";
                                 "MYUD2" = "Completed";
                                 "MYUD3" = "Completed" }
UpgradeKind                    : Rolling
RollingUpgradeMode             : UnmonitoredAuto
ForceRestart                   : False
UpgradeReplicaSetCheckTimeout  : 00:00:00
```

<span data-ttu-id="73fbd-124">在此範例中，hello 升級失敗，在升級網域*MYUD1*和兩個資料分割 (*744c8d9f-1d26-417e-a60e-cd48f5c098f0*和*4b43f4d8-b26b-424e-9307-7a7a62e79750*) 已當機。</span><span class="sxs-lookup"><span data-stu-id="73fbd-124">In this example, hello upgrade failed at upgrade domain *MYUD1* and two partitions (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* and *4b43f4d8-b26b-424e-9307-7a7a62e79750*) were stuck.</span></span> <span data-ttu-id="73fbd-125">hello 資料分割所卡 hello 執行階段因為無法 tooplace 主要複本 (*WaitForPrimaryPlacement*) 目標節點上*Node1*和*Node4*。</span><span class="sxs-lookup"><span data-stu-id="73fbd-125">hello partitions were stuck because hello runtime was unable tooplace primary replicas (*WaitForPrimaryPlacement*) on target nodes *Node1* and *Node4*.</span></span>

<span data-ttu-id="73fbd-126">hello **Get ServiceFabricNode**命令可以使用這兩個節點都升級網域中的 tooverify *MYUD1*。</span><span class="sxs-lookup"><span data-stu-id="73fbd-126">hello **Get-ServiceFabricNode** command can be used tooverify that these two nodes are in upgrade domain *MYUD1*.</span></span> <span data-ttu-id="73fbd-127">hello *UpgradePhase*指出*PostUpgradeSafetyCheck*，這表示在 hello 升級網域中的所有節點都完成升級後發生的這些安全檢查。</span><span class="sxs-lookup"><span data-stu-id="73fbd-127">hello *UpgradePhase* says *PostUpgradeSafetyCheck*, which means that these safety checks are occurring after all nodes in hello upgrade domain have finished upgrading.</span></span> <span data-ttu-id="73fbd-128">這項資訊點 tooa hello hello 應用程式程式碼的新版本的潛在問題。</span><span class="sxs-lookup"><span data-stu-id="73fbd-128">All this information points tooa potential issue with hello new version of hello application code.</span></span> <span data-ttu-id="73fbd-129">hello 最常見的問題是 hello 開啟或升級 tooprimary 程式碼路徑中的服務錯誤。</span><span class="sxs-lookup"><span data-stu-id="73fbd-129">hello most common issues are service errors in hello open or promotion tooprimary code paths.</span></span>

<span data-ttu-id="73fbd-130">*UpgradePhase*的*PreUpgradeSafetyCheck*表示有一些問題它執行前準備 hello 升級網域。</span><span class="sxs-lookup"><span data-stu-id="73fbd-130">An *UpgradePhase* of *PreUpgradeSafetyCheck* means there were issues preparing hello upgrade domain before it was performed.</span></span> <span data-ttu-id="73fbd-131">hello 最常見的問題在此情況下會關閉 hello 或降級，從主要的程式碼路徑中的服務錯誤。</span><span class="sxs-lookup"><span data-stu-id="73fbd-131">hello most common issues in this case are service errors in hello close or demotion from primary code paths.</span></span>

<span data-ttu-id="73fbd-132">目前的 hello **UpgradeState**是*RollingBackCompleted*，因此 hello 原始升級必須已執行並回復**FailureAction**，它會自動回復在失敗後的 hello 升級。</span><span class="sxs-lookup"><span data-stu-id="73fbd-132">hello current **UpgradeState** is *RollingBackCompleted*, so hello original upgrade must have been performed with a rollback **FailureAction**, which automatically rolled back hello upgrade upon failure.</span></span> <span data-ttu-id="73fbd-133">如果可以使用手動執行 hello 原始升級**FailureAction**，然後 hello 升級會改為在暫停的狀態 tooallow 即時 hello 應用程式的偵錯。</span><span class="sxs-lookup"><span data-stu-id="73fbd-133">If hello original upgrade was performed with a manual **FailureAction**, then hello upgrade would instead be in a suspended state tooallow live debugging of hello application.</span></span>

### <a name="investigate-health-check-failures"></a><span data-ttu-id="73fbd-134">調查健康狀態檢查失敗</span><span class="sxs-lookup"><span data-stu-id="73fbd-134">Investigate health check failures</span></span>
<span data-ttu-id="73fbd-135">升級網域中的所有節點完成升級並通過所有安全檢查之後，各種問題都可能觸發健康狀態檢查失敗。</span><span class="sxs-lookup"><span data-stu-id="73fbd-135">Health check failures can be triggered by various issues that can happen after all nodes in an upgrade domain finish upgrading and passing all safety checks.</span></span> <span data-ttu-id="73fbd-136">遵循本段 hello 輸出是典型的升級失敗，因為 toofailed 健康情況檢查。</span><span class="sxs-lookup"><span data-stu-id="73fbd-136">hello output following this paragraph is typical of an upgrade failure due toofailed health checks.</span></span> <span data-ttu-id="73fbd-137">hello **UnhealthyEvaluations**欄位擷取快照集的健康情況檢查失敗時，根據指定的 toohello hello 升級的 hello[健全狀況原則](service-fabric-health-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="73fbd-137">hello **UnhealthyEvaluations** field captures a snapshot of health checks that failed at hello time of hello upgrade according toohello specified [health policy](service-fabric-health-introduction.md).</span></span>

```
PS D:\temp> Get-ServiceFabricApplicationUpgrade fabric:/DemoApp

ApplicationName                         : fabric:/DemoApp
ApplicationTypeName                     : DemoAppType
TargetApplicationTypeVersion            : v4
ApplicationParameters                   : {}
StartTimestampUtc                       : 4/24/2015 2:42:31 AM
UpgradeState                            : RollingForwardPending
UpgradeDuration                         : 00:00:27
CurrentUpgradeDomainDuration            : 00:00:27
NextUpgradeDomain                       : MYUD2
UpgradeDomainsStatus                    : { "MYUD1" = "Completed";
                                          "MYUD2" = "Pending";
                                          "MYUD3" = "Pending" }
UnhealthyEvaluations                    :
                                          Unhealthy services: 50% (2/4), ServiceType='PersistedServiceType', MaxPercentUnhealthyServices=0%.

                                          Unhealthy service: ServiceName='fabric:/DemoApp/Svc3', AggregatedHealthState='Error'.

                                              Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                              Unhealthy partition: PartitionId='3a9911f6-a2e5-452d-89a8-09271e7e49a8', AggregatedHealthState='Error'.

                                                  Error event: SourceId='Replica', Property='InjectedFault'.

                                          Unhealthy service: ServiceName='fabric:/DemoApp/Svc2', AggregatedHealthState='Error'.

                                              Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                              Unhealthy partition: PartitionId='744c8d9f-1d26-417e-a60e-cd48f5c098f0', AggregatedHealthState='Error'.

                                                  Error event: SourceId='Replica', Property='InjectedFault'.

UpgradeKind                             : Rolling
RollingUpgradeMode                      : Monitored
FailureAction                           : Manual
ForceRestart                            : False
UpgradeReplicaSetCheckTimeout           : 49710.06:28:15
HealthCheckWaitDuration                 : 00:00:00
HealthCheckStableDuration               : 00:00:10
HealthCheckRetryTimeout                 : 00:00:10
UpgradeDomainTimeout                    : 10675199.02:48:05.4775807
UpgradeTimeout                          : 10675199.02:48:05.4775807
ConsiderWarningAsError                  :
MaxPercentUnhealthyPartitionsPerService :
MaxPercentUnhealthyReplicasPerPartition :
MaxPercentUnhealthyServices             :
MaxPercentUnhealthyDeployedApplications :
ServiceTypeHealthPolicyMap              :
```

<span data-ttu-id="73fbd-138">調查健全狀況檢查失敗需要先了解 hello 服務網狀架構健全狀況模型。</span><span class="sxs-lookup"><span data-stu-id="73fbd-138">Investigating health check failures first requires an understanding of hello Service Fabric health model.</span></span> <span data-ttu-id="73fbd-139">但即使沒有這類深入了解，我們可以看到兩個服務的狀況不良： *fabric: / demoapp 來/Svc3*和*網狀架構: / demoapp 來/Svc2*，以及 hello 錯誤健全狀況報表 (「 InjectedFault「 在此情況下）。</span><span class="sxs-lookup"><span data-stu-id="73fbd-139">But even without such an in-depth understanding, we can see that two services are unhealthy: *fabric:/DemoApp/Svc3* and *fabric:/DemoApp/Svc2*, along with hello error health reports ("InjectedFault" in this case).</span></span> <span data-ttu-id="73fbd-140">在此範例中，四個兩個服務是狀況不良，這是低於 0%狀況不良的 hello 預設目標 (*MaxPercentUnhealthyServices*)。</span><span class="sxs-lookup"><span data-stu-id="73fbd-140">In this example, two out of four services are unhealthy, which is below hello default target of 0% unhealthy (*MaxPercentUnhealthyServices*).</span></span>

<span data-ttu-id="73fbd-141">hello 升級暫止容錯時藉由指定**FailureAction**的手動時啟動 hello 升級。</span><span class="sxs-lookup"><span data-stu-id="73fbd-141">hello upgrade was suspended upon failing by specifying a **FailureAction** of manual when starting hello upgrade.</span></span> <span data-ttu-id="73fbd-142">此模式可讓我們 tooinvestigate hello 即時系統在 hello 失敗狀態之前採取任何進一步的動作。</span><span class="sxs-lookup"><span data-stu-id="73fbd-142">This mode allows us tooinvestigate hello live system in hello failed state before taking any further action.</span></span>

### <a name="recover-from-a-suspended-upgrade"></a><span data-ttu-id="73fbd-143">從暫止升級復原</span><span class="sxs-lookup"><span data-stu-id="73fbd-143">Recover from a suspended upgrade</span></span>
<span data-ttu-id="73fbd-144">並回復**FailureAction**，沒有任何因為 hello 升級會自動回復在失敗時所需的復原。</span><span class="sxs-lookup"><span data-stu-id="73fbd-144">With a rollback **FailureAction**, there is no recovery needed since hello upgrade automatically rolls back upon failing.</span></span> <span data-ttu-id="73fbd-145">使用手動 **FailureAction**，有數個復原選項：</span><span class="sxs-lookup"><span data-stu-id="73fbd-145">With a manual **FailureAction**, there are several recovery options:</span></span>

1.  <span data-ttu-id="73fbd-146">觸發回復</span><span class="sxs-lookup"><span data-stu-id="73fbd-146">trigger a rollback</span></span>
2. <span data-ttu-id="73fbd-147">手動繼續執行其餘部分 hello hello 升級</span><span class="sxs-lookup"><span data-stu-id="73fbd-147">Proceed through hello remainder of hello upgrade manually</span></span>
3. <span data-ttu-id="73fbd-148">繼續 hello 監視升級</span><span class="sxs-lookup"><span data-stu-id="73fbd-148">Resume hello monitored upgrade</span></span>

<span data-ttu-id="73fbd-149">hello**開始 ServiceFabricApplicationRollback**命令可在任何時間 toostart，回復 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="73fbd-149">hello **Start-ServiceFabricApplicationRollback** command can be used at any time toostart rolling back hello application.</span></span> <span data-ttu-id="73fbd-150">Hello 命令會傳回成功，hello 復原要求 hello 系統中已註冊後不久之後啟動。</span><span class="sxs-lookup"><span data-stu-id="73fbd-150">Once hello command returns successfully, hello rollback request has been registered in hello system and starts shortly thereafter.</span></span>

<span data-ttu-id="73fbd-151">hello **Resume-servicefabricapplicationupgrade**命令可以用 tooproceed hello 其餘部分的 hello 透過手動升級一個升級網域，一次。</span><span class="sxs-lookup"><span data-stu-id="73fbd-151">hello **Resume-ServiceFabricApplicationUpgrade** command can be used tooproceed through hello remainder of hello upgrade manually, one upgrade domain at a time.</span></span> <span data-ttu-id="73fbd-152">在此模式中，唯一的安全性檢查會執行 hello 系統。</span><span class="sxs-lookup"><span data-stu-id="73fbd-152">In this mode, only safety checks are performed by hello system.</span></span> <span data-ttu-id="73fbd-153">不會執行其他健康狀態檢查。</span><span class="sxs-lookup"><span data-stu-id="73fbd-153">No more health checks are performed.</span></span> <span data-ttu-id="73fbd-154">此命令只可用時 hello *UpgradeState*顯示*RollingForwardPending*，這表示該 hello 目前升級網域升級已完成，但 hello 接下來一個啟動 （擱置）。</span><span class="sxs-lookup"><span data-stu-id="73fbd-154">This command can only be used when hello *UpgradeState* shows *RollingForwardPending*, which means that hello current upgrade domain has finished upgrading but hello next one has not started (pending).</span></span>

<span data-ttu-id="73fbd-155">hello**更新 ServiceFabricApplicationUpgrade**命令可以使用的 tooresume hello 監視升級的安全性和健全狀況檢查正在執行。</span><span class="sxs-lookup"><span data-stu-id="73fbd-155">hello **Update-ServiceFabricApplicationUpgrade** command can be used tooresume hello monitored upgrade with both safety and health checks being performed.</span></span>

```
PS D:\temp> Update-ServiceFabricApplicationUpgrade fabric:/DemoApp -UpgradeMode Monitored

UpgradeMode                             : Monitored
ForceRestart                            :
UpgradeReplicaSetCheckTimeout           :
FailureAction                           :
HealthCheckWaitDuration                 :
HealthCheckStableDuration               :
HealthCheckRetryTimeout                 :
UpgradeTimeout                          :
UpgradeDomainTimeout                    :
ConsiderWarningAsError                  :
MaxPercentUnhealthyPartitionsPerService :
MaxPercentUnhealthyReplicasPerPartition :
MaxPercentUnhealthyServices             :
MaxPercentUnhealthyDeployedApplications :
ServiceTypeHealthPolicyMap              :

PS D:\temp>
```

<span data-ttu-id="73fbd-156">hello 升級會繼續從上次已中暫止的 hello 升級網域和使用 hello 參數和健全狀況原則之前，相同升級。</span><span class="sxs-lookup"><span data-stu-id="73fbd-156">hello upgrade continues from hello upgrade domain where it was last suspended and use hello same upgrade parameters and health policies as before.</span></span> <span data-ttu-id="73fbd-157">如有需要 hello hello 升級繼續時，相同命令中就可以變更任何 hello 升級參數和健全狀況原則 hello 前面輸出所示。</span><span class="sxs-lookup"><span data-stu-id="73fbd-157">If needed, any of hello upgrade parameters and health policies shown in hello preceding output can be changed in hello same command when hello upgrade resumes.</span></span> <span data-ttu-id="73fbd-158">在此範例中，hello 升級已繼續在受監視模式中，使用 hello 參數和不變的 hello 健康原則。</span><span class="sxs-lookup"><span data-stu-id="73fbd-158">In this example, hello upgrade was resumed in Monitored mode, with hello parameters and hello health policies unchanged.</span></span>

## <a name="further-troubleshooting"></a><span data-ttu-id="73fbd-159">進一步疑難排解</span><span class="sxs-lookup"><span data-stu-id="73fbd-159">Further troubleshooting</span></span>
### <a name="service-fabric-is-not-following-hello-specified-health-policies"></a><span data-ttu-id="73fbd-160">Service Fabric 不遵循 hello 指定健全狀況原則</span><span class="sxs-lookup"><span data-stu-id="73fbd-160">Service Fabric is not following hello specified health policies</span></span>
<span data-ttu-id="73fbd-161">可能的原因 1：</span><span class="sxs-lookup"><span data-stu-id="73fbd-161">Possible Cause 1:</span></span>

<span data-ttu-id="73fbd-162">Service Fabric 的健全狀況評估轉譯實際的實體 （例如複本、 資料分割，與服務） 的數字為所有的百分比，一律會無條件進位 toowhole 實體。</span><span class="sxs-lookup"><span data-stu-id="73fbd-162">Service Fabric translates all percentages into actual numbers of entities (for example, replicas, partitions, and services) for health evaluation and always rounds up toowhole entities.</span></span> <span data-ttu-id="73fbd-163">例如，如果 hello 最大*MaxPercentUnhealthyReplicasPerPartition*是 21%且有五個複本，然後 Service Fabric 允許 tootwo 狀況不良的複本 (也就是`Math.Ceiling (5*0.21)`)。</span><span class="sxs-lookup"><span data-stu-id="73fbd-163">For example, if hello maximum *MaxPercentUnhealthyReplicasPerPartition* is 21% and there are five replicas, then Service Fabric allows up tootwo unhealthy replicas (that is,`Math.Ceiling (5*0.21)`).</span></span> <span data-ttu-id="73fbd-164">因此，健康狀態原則應該據此設定。</span><span class="sxs-lookup"><span data-stu-id="73fbd-164">Thus, health policies should be set accordingly.</span></span>

<span data-ttu-id="73fbd-165">可能的原因 2：</span><span class="sxs-lookup"><span data-stu-id="73fbd-165">Possible Cause 2:</span></span>

<span data-ttu-id="73fbd-166">健康狀態原則是以服務總計的百分比指定，而不是根據特定服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="73fbd-166">Health policies are specified in terms of percentages of total services and not specific service instances.</span></span> <span data-ttu-id="73fbd-167">例如，再升級時，如果應用程式有四個服務執行個體 A、 B、 C 以及 D，，其中服務 D 是狀況不良，但以小的影響 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="73fbd-167">For example, before an upgrade, if an application has four service instances A, B, C, and D, where service D is unhealthy but with little impact toohello application.</span></span> <span data-ttu-id="73fbd-168">我們想要在升級和設定 hello 參數期間知道狀況不良服務 D 的 tooignore hello *MaxPercentUnhealthyServices* toobe 25%，假設 A、 B 和 C 需要 toobe 狀況良好。</span><span class="sxs-lookup"><span data-stu-id="73fbd-168">We want tooignore hello known unhealthy service D during upgrade and set hello parameter *MaxPercentUnhealthyServices* toobe 25%, assuming only A, B, and C need toobe healthy.</span></span>

<span data-ttu-id="73fbd-169">不過，hello 在升級期間，D 時可能變成狀況良好 C 會變為狀況不良。</span><span class="sxs-lookup"><span data-stu-id="73fbd-169">However, during hello upgrade, D may become healthy while C becomes unhealthy.</span></span> <span data-ttu-id="73fbd-170">hello 升級仍然會成功，因為只有 25%的 hello 服務均狀況不良。</span><span class="sxs-lookup"><span data-stu-id="73fbd-170">hello upgrade would still succeed because only 25% of hello services are unhealthy.</span></span> <span data-ttu-id="73fbd-171">不過，它可能會導致非預期的錯誤到期 tooC 被意外狀況不良，而不是 d。在此情況下，D 應該會模式化為不同的服務類型 a、 B 和 c。健全狀況原則會指定每個服務類型，因為不同的狀況不良百分比閾值可套用的 toodifferent 服務。</span><span class="sxs-lookup"><span data-stu-id="73fbd-171">However, it might result in unanticipated errors due tooC being unexpectedly unhealthy instead of D. In this situation, D should be modeled as a different service type from A, B, and C. Since health policies are specified per service type, different unhealthy percentage thresholds can be applied toodifferent services.</span></span> 

### <a name="i-did-not-specify-a-health-policy-for-application-upgrade-but-hello-upgrade-still-fails-for-some-time-outs-that-i-never-specified"></a><span data-ttu-id="73fbd-172">我未指定應用程式升級的健全狀況原則，但永遠不會指定某些逾時的 hello 升級仍失敗</span><span class="sxs-lookup"><span data-stu-id="73fbd-172">I did not specify a health policy for application upgrade, but hello upgrade still fails for some time-outs that I never specified</span></span>
<span data-ttu-id="73fbd-173">當健全狀況原則不提供 toohello 升級要求時，它們取自 hello *ApplicationManifest.xml* hello 目前應用程式版本。</span><span class="sxs-lookup"><span data-stu-id="73fbd-173">When health policies aren't provided toohello upgrade request, they are taken from hello *ApplicationManifest.xml* of hello current application version.</span></span> <span data-ttu-id="73fbd-174">例如，如果您要升級應用程式 X 的 1.0 版 tooversion 2.0，會使用在 1.0 版中指定的應用程式健全狀況原則。</span><span class="sxs-lookup"><span data-stu-id="73fbd-174">For example, if you're upgrading Application X from version 1.0 tooversion 2.0, application health policies specified for in version 1.0 are used.</span></span> <span data-ttu-id="73fbd-175">如果應使用不同的健全狀況原則 hello 升級，hello 原則需要 toobe hello 應用程式升級的 API 呼叫中指定。</span><span class="sxs-lookup"><span data-stu-id="73fbd-175">If a different health policy should be used for hello upgrade, then hello policy needs toobe specified as part of hello application upgrade API call.</span></span> <span data-ttu-id="73fbd-176">hello hello API 呼叫中指定的原則僅適用於 hello 升級期間。</span><span class="sxs-lookup"><span data-stu-id="73fbd-176">hello policies specified as part of hello API call only apply during hello upgrade.</span></span> <span data-ttu-id="73fbd-177">在 hello hello 升級完成之後，請指定 hello 原則*ApplicationManifest.xml*可用。</span><span class="sxs-lookup"><span data-stu-id="73fbd-177">Once hello upgrade is complete, hello policies specified in hello *ApplicationManifest.xml* are used.</span></span>

### <a name="incorrect-time-outs-are-specified"></a><span data-ttu-id="73fbd-178">指定了不正確的逾時</span><span class="sxs-lookup"><span data-stu-id="73fbd-178">Incorrect time-outs are specified</span></span>
<span data-ttu-id="73fbd-179">您可能想要知道當逾時設定不一致時會發生什麼情況。</span><span class="sxs-lookup"><span data-stu-id="73fbd-179">You may have wondered about what happens when time-outs are set inconsistently.</span></span> <span data-ttu-id="73fbd-180">例如，您可能必須*UpgradeTimeout*低於 hello *UpgradeDomainTimeout*。</span><span class="sxs-lookup"><span data-stu-id="73fbd-180">For example, you may have an *UpgradeTimeout* that's less than hello *UpgradeDomainTimeout*.</span></span> <span data-ttu-id="73fbd-181">hello 辦法就是會傳回錯誤。</span><span class="sxs-lookup"><span data-stu-id="73fbd-181">hello answer is that an error is returned.</span></span> <span data-ttu-id="73fbd-182">會傳回錯誤，如果 hello *UpgradeDomainTimeout*小於 hello 總和*HealthCheckWaitDuration*和*HealthCheckRetryTimeout*，或如果*UpgradeDomainTimeout*小於 hello 總和*HealthCheckWaitDuration*和*HealthCheckStableDuration*。</span><span class="sxs-lookup"><span data-stu-id="73fbd-182">Errors are returned if hello *UpgradeDomainTimeout* is less than hello sum of *HealthCheckWaitDuration* and *HealthCheckRetryTimeout*, or if *UpgradeDomainTimeout* is less than hello sum of *HealthCheckWaitDuration* and *HealthCheckStableDuration*.</span></span>

### <a name="my-upgrades-are-taking-too-long"></a><span data-ttu-id="73fbd-183">我的升級耗費太多時間</span><span class="sxs-lookup"><span data-stu-id="73fbd-183">My upgrades are taking too long</span></span>
<span data-ttu-id="73fbd-184">升級的 toocomplete hello 時間取決於 hello 健全狀況檢查和指定的逾時。</span><span class="sxs-lookup"><span data-stu-id="73fbd-184">hello time for an upgrade toocomplete depends on hello health checks and time-outs specified.</span></span> <span data-ttu-id="73fbd-185">健全狀況檢查和逾時依存於 toocopy 要花多久、 部署和穩定化 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="73fbd-185">Health checks and time-outs depend on how long it takes toocopy, deploy, and stabilize hello application.</span></span> <span data-ttu-id="73fbd-186">使用逾時太過激烈，可能表示會有更多失敗的升級，因此建議保守地從較長的逾時開始。</span><span class="sxs-lookup"><span data-stu-id="73fbd-186">Being too aggressive with time-outs might mean more failed upgrades, so we recommend starting conservatively with longer time-outs.</span></span>

<span data-ttu-id="73fbd-187">以下是快速的重新整理程式在 hello 逾時與 hello 升級時間之間的互動方式：</span><span class="sxs-lookup"><span data-stu-id="73fbd-187">Here's a quick refresher on how hello time-outs interact with hello upgrade times:</span></span>

<span data-ttu-id="73fbd-188">升級網域的升級完成時間無法快於 HealthCheckWaitDuration  +  HealthCheckStableDuration。</span><span class="sxs-lookup"><span data-stu-id="73fbd-188">Upgrades for an upgrade domain cannot complete faster than *HealthCheckWaitDuration* + *HealthCheckStableDuration*.</span></span>

<span data-ttu-id="73fbd-189">升級失敗發生時間無法快於 HealthCheckWaitDuration  +  HealthCheckRetryTimeout。</span><span class="sxs-lookup"><span data-stu-id="73fbd-189">Upgrade failure cannot occur faster than *HealthCheckWaitDuration* + *HealthCheckRetryTimeout*.</span></span>

<span data-ttu-id="73fbd-190">hello 的升級網域升級時間受限於*UpgradeDomainTimeout*。</span><span class="sxs-lookup"><span data-stu-id="73fbd-190">hello upgrade time for an upgrade domain is limited by *UpgradeDomainTimeout*.</span></span>  <span data-ttu-id="73fbd-191">如果*HealthCheckRetryTimeout*和*HealthCheckStableDuration*兩者都為非零，則 hello 升級最後會逾時上hellohello應用程式的健全狀況會保留，來回切換*UpgradeDomainTimeout*。</span><span class="sxs-lookup"><span data-stu-id="73fbd-191">If *HealthCheckRetryTimeout* and *HealthCheckStableDuration* are both non-zero and hello health of hello application keeps switching back and forth, then hello upgrade eventually times out on *UpgradeDomainTimeout*.</span></span> <span data-ttu-id="73fbd-192">*UpgradeDomainTimeout*啟動一次向下計數 hello 升級，如 hello 目前升級網域會開始。</span><span class="sxs-lookup"><span data-stu-id="73fbd-192">*UpgradeDomainTimeout* starts counting down once hello upgrade for hello current upgrade domain begins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="73fbd-193">後續步驟</span><span class="sxs-lookup"><span data-stu-id="73fbd-193">Next steps</span></span>
<span data-ttu-id="73fbd-194">[使用 Visual Studio 升級您的應用程式](service-fabric-application-upgrade-tutorial.md) 將引導您完成使用 Visual Studio 進行應用程式升級的步驟。</span><span class="sxs-lookup"><span data-stu-id="73fbd-194">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>

<span data-ttu-id="73fbd-195">[使用 PowerShell 升級您的應用程式](service-fabric-application-upgrade-tutorial-powershell.md) 將引導您完成使用 PowerShell 進行應用程式升級的步驟。</span><span class="sxs-lookup"><span data-stu-id="73fbd-195">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>

<span data-ttu-id="73fbd-196">使用 [升級參數](service-fabric-application-upgrade-parameters.md)來控制您應用程式的升級方式。</span><span class="sxs-lookup"><span data-stu-id="73fbd-196">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>

<span data-ttu-id="73fbd-197">讓應用程式升級相容所學習如何 toouse[資料序列化](service-fabric-application-upgrade-data-serialization.md)。</span><span class="sxs-lookup"><span data-stu-id="73fbd-197">Make your application upgrades compatible by learning how toouse [Data Serialization](service-fabric-application-upgrade-data-serialization.md).</span></span>

<span data-ttu-id="73fbd-198">了解 toouse 把太升級您的應用程式時所進階的功能[進階主題](service-fabric-application-upgrade-advanced.md)。</span><span class="sxs-lookup"><span data-stu-id="73fbd-198">Learn how toouse advanced functionality while upgrading your application by referring too[Advanced Topics](service-fabric-application-upgrade-advanced.md).</span></span>
