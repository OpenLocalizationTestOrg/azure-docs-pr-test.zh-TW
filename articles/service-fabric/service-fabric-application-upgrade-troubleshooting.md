---
title: "疑難排解應用程式升級 | Microsoft Docs"
description: "本文涵蓋升級 Service Fabric 應用程式的一些常見問題，以及解決方式。"
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
ms.openlocfilehash: f7f6bc0c29e2b43fbc8e451c5a4a50110b78349e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-application-upgrades"></a><span data-ttu-id="e60ee-103">疑難排解應用程式升級</span><span class="sxs-lookup"><span data-stu-id="e60ee-103">Troubleshoot application upgrades</span></span>
<span data-ttu-id="e60ee-104">本文涵蓋升級 Azure Service Fabric 應用程式的一些常見問題，以及解決方式。</span><span class="sxs-lookup"><span data-stu-id="e60ee-104">This article covers some of the common issues around upgrading an Azure Service Fabric application and how to resolve them.</span></span>

## <a name="troubleshoot-a-failed-application-upgrade"></a><span data-ttu-id="e60ee-105">疑難排解失敗的應用程式升級</span><span class="sxs-lookup"><span data-stu-id="e60ee-105">Troubleshoot a failed application upgrade</span></span>
<span data-ttu-id="e60ee-106">當升級失敗時， **Get-ServiceFabricApplicationUpgrade** 命令的輸出會包含偵錯失敗的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="e60ee-106">When an upgrade fails, the output of the **Get-ServiceFabricApplicationUpgrade** command contains additional information for debugging the failure.</span></span>  <span data-ttu-id="e60ee-107">下列清單指定如何使用其他資訊︰</span><span class="sxs-lookup"><span data-stu-id="e60ee-107">The following list specifies how the additional information can be used:</span></span>

1. <span data-ttu-id="e60ee-108">識別失敗類型。</span><span class="sxs-lookup"><span data-stu-id="e60ee-108">Identify the failure type.</span></span>
2. <span data-ttu-id="e60ee-109">識別失敗原因。</span><span class="sxs-lookup"><span data-stu-id="e60ee-109">Identify the failure reason.</span></span>
3. <span data-ttu-id="e60ee-110">隔離一或多個失敗元件以便進一步調查。</span><span class="sxs-lookup"><span data-stu-id="e60ee-110">Isolate one or more failing components for further investigation.</span></span>

<span data-ttu-id="e60ee-111">當 Service Fabric 偵測到失敗，就會提供此資訊，不論 **FailureAction** 是回復或暫停升級。</span><span class="sxs-lookup"><span data-stu-id="e60ee-111">This information is available when Service Fabric detects the failure regardless of whether the **FailureAction** is to roll back or suspend the upgrade.</span></span>

### <a name="identify-the-failure-type"></a><span data-ttu-id="e60ee-112">識別失敗類型</span><span class="sxs-lookup"><span data-stu-id="e60ee-112">Identify the failure type</span></span>
<span data-ttu-id="e60ee-113">在 **Get-ServiceFabricApplicationUpgrade** 的輸出中，**FailureTimestampUtc** 會識別 Service Fabric 偵測升級失敗以及觸發 **FailureAction** 的時間戳記 (UTC)。</span><span class="sxs-lookup"><span data-stu-id="e60ee-113">In the output of **Get-ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** identifies the timestamp (in UTC) at which an upgrade failure was detected by Service Fabric and **FailureAction** was triggered.</span></span> <span data-ttu-id="e60ee-114">**FailureReason** 會識別失敗的三個可能高階原因之一：</span><span class="sxs-lookup"><span data-stu-id="e60ee-114">**FailureReason** identifies one of three potential high-level causes of the failure:</span></span>

1. <span data-ttu-id="e60ee-115">UpgradeDomainTimeout - 指出特定的升級網域花太多時間完成且 **UpgradeDomainTimeout** 過期。</span><span class="sxs-lookup"><span data-stu-id="e60ee-115">UpgradeDomainTimeout - Indicates that a particular upgrade domain took too long to complete and **UpgradeDomainTimeout** expired.</span></span>
2. <span data-ttu-id="e60ee-116">OverallUpgradeTimeout - 指出整體升級花太多時間完成且 **UpgradeTimeout** 過期。</span><span class="sxs-lookup"><span data-stu-id="e60ee-116">OverallUpgradeTimeout - Indicates that the overall upgrade took too long to complete and **UpgradeTimeout** expired.</span></span>
3. <span data-ttu-id="e60ee-117">HealthCheck - 指出升級更新網域之後，根據指定的健康狀態原則，應用程式仍然健康狀態不良，且 **HealthCheckRetryTimeout** 過期。</span><span class="sxs-lookup"><span data-stu-id="e60ee-117">HealthCheck - Indicates that after upgrading an update domain, the application remained unhealthy according to the specified health policies and **HealthCheckRetryTimeout** expired.</span></span>

<span data-ttu-id="e60ee-118">這些項目只有在升級失敗且啟動回復時，才會出現在輸出中。</span><span class="sxs-lookup"><span data-stu-id="e60ee-118">These entries only show up in the output when the upgrade fails and starts rolling back.</span></span> <span data-ttu-id="e60ee-119">視失敗的類型而定，會顯示進一步的資訊。</span><span class="sxs-lookup"><span data-stu-id="e60ee-119">Further information is displayed depending on the type of the failure.</span></span>

### <a name="investigate-upgrade-timeouts"></a><span data-ttu-id="e60ee-120">調查升級逾時</span><span class="sxs-lookup"><span data-stu-id="e60ee-120">Investigate upgrade timeouts</span></span>
<span data-ttu-id="e60ee-121">升級逾時失敗通常是由服務可用性問題造成的。</span><span class="sxs-lookup"><span data-stu-id="e60ee-121">Upgrade timeout failures are most commonly caused by service availability issues.</span></span> <span data-ttu-id="e60ee-122">本段落下面的輸出是典型的升級，其中服務複本或執行個體無法在新的程式碼版本中啟動。</span><span class="sxs-lookup"><span data-stu-id="e60ee-122">The output following this paragraph is typical of upgrades where service replicas or instances fail to start in the new code version.</span></span> <span data-ttu-id="e60ee-123">**UpgradeDomainProgressAtFailure** 欄位在失敗時擷取任何擱置中升級工作的快照集。</span><span class="sxs-lookup"><span data-stu-id="e60ee-123">The **UpgradeDomainProgressAtFailure** field captures a snapshot of any pending upgrade work at the time of failure.</span></span>

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

<span data-ttu-id="e60ee-124">在此範例中，升級網域 MYUD1 的升級失敗，且兩個資料分割 (744c8d9f-1d26-417e-a60e-cd48f5c098f0 和 4b43f4d8-b26b-424e-9307-7a7a62e79750) 已停滯。</span><span class="sxs-lookup"><span data-stu-id="e60ee-124">In this example, the upgrade failed at upgrade domain *MYUD1* and two partitions (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* and *4b43f4d8-b26b-424e-9307-7a7a62e79750*) were stuck.</span></span> <span data-ttu-id="e60ee-125">資料分割因為執行階段無法將主要複本 (WaitForPrimaryPlacement) 放在在目標節點 Node1 和 Node4 上而停滯。</span><span class="sxs-lookup"><span data-stu-id="e60ee-125">The partitions were stuck because the runtime was unable to place primary replicas (*WaitForPrimaryPlacement*) on target nodes *Node1* and *Node4*.</span></span>

<span data-ttu-id="e60ee-126">**Get-ServiceFabricNode** 命令可以用來確認這兩個節點都在升級網域 *MYUD1*中。</span><span class="sxs-lookup"><span data-stu-id="e60ee-126">The **Get-ServiceFabricNode** command can be used to verify that these two nodes are in upgrade domain *MYUD1*.</span></span> <span data-ttu-id="e60ee-127">UpgradePhase 指出 PostUpgradeSafetyCheck，表示這些安全檢查是在升級網域中的所有節點完成升級之後發生。</span><span class="sxs-lookup"><span data-stu-id="e60ee-127">The *UpgradePhase* says *PostUpgradeSafetyCheck*, which means that these safety checks are occurring after all nodes in the upgrade domain have finished upgrading.</span></span> <span data-ttu-id="e60ee-128">這些資訊全都指向應用程式程式碼新版本的潛在問題。</span><span class="sxs-lookup"><span data-stu-id="e60ee-128">All this information points to a potential issue with the new version of the application code.</span></span> <span data-ttu-id="e60ee-129">最常見的問題是開啟或升級至主要程式碼路徑的服務錯誤。</span><span class="sxs-lookup"><span data-stu-id="e60ee-129">The most common issues are service errors in the open or promotion to primary code paths.</span></span>

<span data-ttu-id="e60ee-130">PreUpgradeSafetyCheck 的 UpgradePhase 表示在執行升級之前準備升級網域有問題。</span><span class="sxs-lookup"><span data-stu-id="e60ee-130">An *UpgradePhase* of *PreUpgradeSafetyCheck* means there were issues preparing the upgrade domain before it was performed.</span></span> <span data-ttu-id="e60ee-131">此案例中最常見的問題是關閉主要程式碼路徑或從其中降級的服務錯誤。</span><span class="sxs-lookup"><span data-stu-id="e60ee-131">The most common issues in this case are service errors in the close or demotion from primary code paths.</span></span>

<span data-ttu-id="e60ee-132">目前的 UpgradeState 是 RollingBackCompleted，因此原始升級必須以回復 FailureAction 執行，這樣會自動在失敗時回復升級。</span><span class="sxs-lookup"><span data-stu-id="e60ee-132">The current **UpgradeState** is *RollingBackCompleted*, so the original upgrade must have been performed with a rollback **FailureAction**, which automatically rolled back the upgrade upon failure.</span></span> <span data-ttu-id="e60ee-133">如果原始升級以手動 **FailureAction**執行，則升級會處於暫止狀態，以允許應用程式的即時偵錯。</span><span class="sxs-lookup"><span data-stu-id="e60ee-133">If the original upgrade was performed with a manual **FailureAction**, then the upgrade would instead be in a suspended state to allow live debugging of the application.</span></span>

### <a name="investigate-health-check-failures"></a><span data-ttu-id="e60ee-134">調查健康狀態檢查失敗</span><span class="sxs-lookup"><span data-stu-id="e60ee-134">Investigate health check failures</span></span>
<span data-ttu-id="e60ee-135">升級網域中的所有節點完成升級並通過所有安全檢查之後，各種問題都可能觸發健康狀態檢查失敗。</span><span class="sxs-lookup"><span data-stu-id="e60ee-135">Health check failures can be triggered by various issues that can happen after all nodes in an upgrade domain finish upgrading and passing all safety checks.</span></span> <span data-ttu-id="e60ee-136">本段落下面的輸出是由於失敗的健康狀態檢查的典型升級失敗。</span><span class="sxs-lookup"><span data-stu-id="e60ee-136">The output following this paragraph is typical of an upgrade failure due to failed health checks.</span></span> <span data-ttu-id="e60ee-137">**UnhealthyEvaluations** 欄位會根據指定的 [健康狀態原則](service-fabric-health-introduction.md)，擷取升級時失敗的健康狀態檢查的快照集。</span><span class="sxs-lookup"><span data-stu-id="e60ee-137">The **UnhealthyEvaluations** field captures a snapshot of health checks that failed at the time of the upgrade according to the specified [health policy](service-fabric-health-introduction.md).</span></span>

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

<span data-ttu-id="e60ee-138">調查健康狀態檢查失敗時，首先需要了解 Service Fabric 健康狀態模型。</span><span class="sxs-lookup"><span data-stu-id="e60ee-138">Investigating health check failures first requires an understanding of the Service Fabric health model.</span></span> <span data-ttu-id="e60ee-139">但是即使沒有這類深入了解，我們可以看到兩個服務的健康狀態不良：fabric:/DemoApp/Svc3 和 fabric:/DemoApp/Svc2，以及錯誤健康狀態報告 (在本例中為"InjectedFault")。</span><span class="sxs-lookup"><span data-stu-id="e60ee-139">But even without such an in-depth understanding, we can see that two services are unhealthy: *fabric:/DemoApp/Svc3* and *fabric:/DemoApp/Svc2*, along with the error health reports ("InjectedFault" in this case).</span></span> <span data-ttu-id="e60ee-140">在此範例中，4 個服務中有 2 個服務健康狀態不良，低於預設目標 0% 健康狀態不良 (*MaxPercentUnhealthyServices*)。</span><span class="sxs-lookup"><span data-stu-id="e60ee-140">In this example, two out of four services are unhealthy, which is below the default target of 0% unhealthy (*MaxPercentUnhealthyServices*).</span></span>

<span data-ttu-id="e60ee-141">升級是因啟動升級時手動指定 **FailureAction** 失敗而暫止。</span><span class="sxs-lookup"><span data-stu-id="e60ee-141">The upgrade was suspended upon failing by specifying a **FailureAction** of manual when starting the upgrade.</span></span> <span data-ttu-id="e60ee-142">此模式可讓我們在採取任何進一步動作之前，在失敗的狀態下調查即時系統。</span><span class="sxs-lookup"><span data-stu-id="e60ee-142">This mode allows us to investigate the live system in the failed state before taking any further action.</span></span>

### <a name="recover-from-a-suspended-upgrade"></a><span data-ttu-id="e60ee-143">從暫止升級復原</span><span class="sxs-lookup"><span data-stu-id="e60ee-143">Recover from a suspended upgrade</span></span>
<span data-ttu-id="e60ee-144">使用回復的 **FailureAction**，因為升級會自動在失敗時回復，所以不需要復原。</span><span class="sxs-lookup"><span data-stu-id="e60ee-144">With a rollback **FailureAction**, there is no recovery needed since the upgrade automatically rolls back upon failing.</span></span> <span data-ttu-id="e60ee-145">使用手動 **FailureAction**，有數個復原選項：</span><span class="sxs-lookup"><span data-stu-id="e60ee-145">With a manual **FailureAction**, there are several recovery options:</span></span>

1.  <span data-ttu-id="e60ee-146">觸發回復</span><span class="sxs-lookup"><span data-stu-id="e60ee-146">trigger a rollback</span></span>
2. <span data-ttu-id="e60ee-147">以手動方式繼續進行升級的其餘部分</span><span class="sxs-lookup"><span data-stu-id="e60ee-147">Proceed through the remainder of the upgrade manually</span></span>
3. <span data-ttu-id="e60ee-148">繼續監視的升級</span><span class="sxs-lookup"><span data-stu-id="e60ee-148">Resume the monitored upgrade</span></span>

<span data-ttu-id="e60ee-149">**Start-ServiceFabricApplicationRollback** 命令可以在任何時候用來啟動回復應用程式。</span><span class="sxs-lookup"><span data-stu-id="e60ee-149">The **Start-ServiceFabricApplicationRollback** command can be used at any time to start rolling back the application.</span></span> <span data-ttu-id="e60ee-150">一旦命令成功傳回，回復要求就已在系統中註冊並隨即啟動。</span><span class="sxs-lookup"><span data-stu-id="e60ee-150">Once the command returns successfully, the rollback request has been registered in the system and starts shortly thereafter.</span></span>

<span data-ttu-id="e60ee-151">**Resume-ServiceFabricApplicationUpgrade** 命令可以用來以手動方式繼續升級的其餘部分，一次一個升級網域。</span><span class="sxs-lookup"><span data-stu-id="e60ee-151">The **Resume-ServiceFabricApplicationUpgrade** command can be used to proceed through the remainder of the upgrade manually, one upgrade domain at a time.</span></span> <span data-ttu-id="e60ee-152">在此模式中，系統只會執行安全檢查。</span><span class="sxs-lookup"><span data-stu-id="e60ee-152">In this mode, only safety checks are performed by the system.</span></span> <span data-ttu-id="e60ee-153">不會執行其他健康狀態檢查。</span><span class="sxs-lookup"><span data-stu-id="e60ee-153">No more health checks are performed.</span></span> <span data-ttu-id="e60ee-154">此命令只能在 UpgradeState 顯示 RollingForwardPending 時使用，表示目前升級網域已完成升級，但是下一個升級網域尚未啟動 (擱置中)。</span><span class="sxs-lookup"><span data-stu-id="e60ee-154">This command can only be used when the *UpgradeState* shows *RollingForwardPending*, which means that the current upgrade domain has finished upgrading but the next one has not started (pending).</span></span>

<span data-ttu-id="e60ee-155">**Update-ServiceFabricApplicationUpgrade** 命令可以用來繼續監視的升級，並且執行安全和健康狀態檢查。</span><span class="sxs-lookup"><span data-stu-id="e60ee-155">The **Update-ServiceFabricApplicationUpgrade** command can be used to resume the monitored upgrade with both safety and health checks being performed.</span></span>

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

<span data-ttu-id="e60ee-156">升級會從上一次暫止的升級網域繼續，並使用相同的升級參數和健康狀態原則。</span><span class="sxs-lookup"><span data-stu-id="e60ee-156">The upgrade continues from the upgrade domain where it was last suspended and use the same upgrade parameters and health policies as before.</span></span> <span data-ttu-id="e60ee-157">如有需要，繼續升級時，上述輸出中顯示的任何升級參數和健康狀態原則都可以在相同命令中變更。</span><span class="sxs-lookup"><span data-stu-id="e60ee-157">If needed, any of the upgrade parameters and health policies shown in the preceding output can be changed in the same command when the upgrade resumes.</span></span> <span data-ttu-id="e60ee-158">在此範例中，升級以監視模式繼續，參數和健康狀態原則維持不變。</span><span class="sxs-lookup"><span data-stu-id="e60ee-158">In this example, the upgrade was resumed in Monitored mode, with the parameters and the health policies unchanged.</span></span>

## <a name="further-troubleshooting"></a><span data-ttu-id="e60ee-159">進一步疑難排解</span><span class="sxs-lookup"><span data-stu-id="e60ee-159">Further troubleshooting</span></span>
### <a name="service-fabric-is-not-following-the-specified-health-policies"></a><span data-ttu-id="e60ee-160">Service Fabric 不遵循指定的健康狀態原則。</span><span class="sxs-lookup"><span data-stu-id="e60ee-160">Service Fabric is not following the specified health policies</span></span>
<span data-ttu-id="e60ee-161">可能的原因 1：</span><span class="sxs-lookup"><span data-stu-id="e60ee-161">Possible Cause 1:</span></span>

<span data-ttu-id="e60ee-162">Service Fabric 將所有百分比轉譯為健康狀態評估的實體 (例如複本、資料分割和服務) 實際數目，並且一律無條件進位到實體整數。</span><span class="sxs-lookup"><span data-stu-id="e60ee-162">Service Fabric translates all percentages into actual numbers of entities (for example, replicas, partitions, and services) for health evaluation and always rounds up to whole entities.</span></span> <span data-ttu-id="e60ee-163">例如，如果最大值 MaxPercentUnhealthyReplicasPerPartition 是 21%，而且有 5 個複本，則 Service Fabric 允許最多 2 個狀況不良的複本 (亦即 `Math.Ceiling (5*0.21)`)。</span><span class="sxs-lookup"><span data-stu-id="e60ee-163">For example, if the maximum *MaxPercentUnhealthyReplicasPerPartition* is 21% and there are five replicas, then Service Fabric allows up to two unhealthy replicas (that is,`Math.Ceiling (5*0.21)`).</span></span> <span data-ttu-id="e60ee-164">因此，健康狀態原則應該據此設定。</span><span class="sxs-lookup"><span data-stu-id="e60ee-164">Thus, health policies should be set accordingly.</span></span>

<span data-ttu-id="e60ee-165">可能的原因 2：</span><span class="sxs-lookup"><span data-stu-id="e60ee-165">Possible Cause 2:</span></span>

<span data-ttu-id="e60ee-166">健康狀態原則是以服務總計的百分比指定，而不是根據特定服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="e60ee-166">Health policies are specified in terms of percentages of total services and not specific service instances.</span></span> <span data-ttu-id="e60ee-167">例如，在升級之前，如果應用程式有四個服務執行個體 A、B、C 和 D，其中服務 D 健康狀態不良，但是對應用程式沒有顯著影響。</span><span class="sxs-lookup"><span data-stu-id="e60ee-167">For example, before an upgrade, if an application has four service instances A, B, C, and D, where service D is unhealthy but with little impact to the application.</span></span> <span data-ttu-id="e60ee-168">我們想要在升級期間略過已知健康狀態不良的服務 D，並將參數 *MaxPercentUnhealthyServices* 設為 25%，假設只有 A、B 和 C 需要是健康狀態良好。</span><span class="sxs-lookup"><span data-stu-id="e60ee-168">We want to ignore the known unhealthy service D during upgrade and set the parameter *MaxPercentUnhealthyServices* to be 25%, assuming only A, B, and C need to be healthy.</span></span>

<span data-ttu-id="e60ee-169">不過，在升級期間，D 會在 C 健康狀態不良時變成健康狀態良好。</span><span class="sxs-lookup"><span data-stu-id="e60ee-169">However, during the upgrade, D may become healthy while C becomes unhealthy.</span></span> <span data-ttu-id="e60ee-170">升級仍然會成功，因為只有 25% 的服務是健康狀態不良。</span><span class="sxs-lookup"><span data-stu-id="e60ee-170">The upgrade would still succeed because only 25% of the services are unhealthy.</span></span> <span data-ttu-id="e60ee-171">但是，由於是 C 意外變成健康狀態不良而不是 D，所以可能會造成非預期的錯誤。在此情況下，D 應該被模式化為與 A、B 和 C 不同的服務類型。因為健康狀態原則是根據每個服務類型指定，所以可以對不同的服務套用不同的健康狀態不良百分比臨界值。</span><span class="sxs-lookup"><span data-stu-id="e60ee-171">However, it might result in unanticipated errors due to C being unexpectedly unhealthy instead of D. In this situation, D should be modeled as a different service type from A, B, and C. Since health policies are specified per service type, different unhealthy percentage thresholds can be applied to different services.</span></span> 

### <a name="i-did-not-specify-a-health-policy-for-application-upgrade-but-the-upgrade-still-fails-for-some-time-outs-that-i-never-specified"></a><span data-ttu-id="e60ee-172">我未對應用程式升級指定健康狀態原則，但是升級還是因為我從未指定的逾時而失敗</span><span class="sxs-lookup"><span data-stu-id="e60ee-172">I did not specify a health policy for application upgrade, but the upgrade still fails for some time-outs that I never specified</span></span>
<span data-ttu-id="e60ee-173">當未對升級要求提供健康狀態原則時，會從目前應用程式版本的 *ApplicationManifest.xml* 取用。</span><span class="sxs-lookup"><span data-stu-id="e60ee-173">When health policies aren't provided to the upgrade request, they are taken from the *ApplicationManifest.xml* of the current application version.</span></span> <span data-ttu-id="e60ee-174">例如，如果將應用程式 X 從 1.0 版升級至 2.0 版，則會使用為 1.0 版指定的應用程式健康狀態原則。</span><span class="sxs-lookup"><span data-stu-id="e60ee-174">For example, if you're upgrading Application X from version 1.0 to version 2.0, application health policies specified for in version 1.0 are used.</span></span> <span data-ttu-id="e60ee-175">如果應該對升級使用不同的健康狀態原則，則需要指定原則做為應用程式升級 API 呼叫的一部分。</span><span class="sxs-lookup"><span data-stu-id="e60ee-175">If a different health policy should be used for the upgrade, then the policy needs to be specified as part of the application upgrade API call.</span></span> <span data-ttu-id="e60ee-176">指定為 API 呼叫一部分的原則只適用於升級期間。</span><span class="sxs-lookup"><span data-stu-id="e60ee-176">The policies specified as part of the API call only apply during the upgrade.</span></span> <span data-ttu-id="e60ee-177">完成升級後，會使用 *ApplicationManifest.xml* 中指定的原則。</span><span class="sxs-lookup"><span data-stu-id="e60ee-177">Once the upgrade is complete, the policies specified in the *ApplicationManifest.xml* are used.</span></span>

### <a name="incorrect-time-outs-are-specified"></a><span data-ttu-id="e60ee-178">指定了不正確的逾時</span><span class="sxs-lookup"><span data-stu-id="e60ee-178">Incorrect time-outs are specified</span></span>
<span data-ttu-id="e60ee-179">您可能想要知道當逾時設定不一致時會發生什麼情況。</span><span class="sxs-lookup"><span data-stu-id="e60ee-179">You may have wondered about what happens when time-outs are set inconsistently.</span></span> <span data-ttu-id="e60ee-180">例如，您的 UpgradeTimeout 小於 UpgradeDomainTimeout。</span><span class="sxs-lookup"><span data-stu-id="e60ee-180">For example, you may have an *UpgradeTimeout* that's less than the *UpgradeDomainTimeout*.</span></span> <span data-ttu-id="e60ee-181">答案是會傳回錯誤。</span><span class="sxs-lookup"><span data-stu-id="e60ee-181">The answer is that an error is returned.</span></span> <span data-ttu-id="e60ee-182">如果 UpgradeDomainTimeout 小於 HealthCheckWaitDuration 和 HealthCheckRetryTimeout 的總和，或如果 UpgradeDomainTimeout 小於 HealthCheckWaitDuration 和 HealthCheckStableDuration 的總和，則會傳回錯誤。</span><span class="sxs-lookup"><span data-stu-id="e60ee-182">Errors are returned if the *UpgradeDomainTimeout* is less than the sum of *HealthCheckWaitDuration* and *HealthCheckRetryTimeout*, or if *UpgradeDomainTimeout* is less than the sum of *HealthCheckWaitDuration* and *HealthCheckStableDuration*.</span></span>

### <a name="my-upgrades-are-taking-too-long"></a><span data-ttu-id="e60ee-183">我的升級耗費太多時間</span><span class="sxs-lookup"><span data-stu-id="e60ee-183">My upgrades are taking too long</span></span>
<span data-ttu-id="e60ee-184">升級完成的時間取決於健康狀態檢查和指定的逾時。</span><span class="sxs-lookup"><span data-stu-id="e60ee-184">The time for an upgrade to complete depends on the health checks and time-outs specified.</span></span> <span data-ttu-id="e60ee-185">健康狀態檢查和逾時則取決於花多少時間來複製、部署及穩定應用程式。</span><span class="sxs-lookup"><span data-stu-id="e60ee-185">Health checks and time-outs depend on how long it takes to copy, deploy, and stabilize the application.</span></span> <span data-ttu-id="e60ee-186">使用逾時太過激烈，可能表示會有更多失敗的升級，因此建議保守地從較長的逾時開始。</span><span class="sxs-lookup"><span data-stu-id="e60ee-186">Being too aggressive with time-outs might mean more failed upgrades, so we recommend starting conservatively with longer time-outs.</span></span>

<span data-ttu-id="e60ee-187">以下是逾時與升級時間之間的互動方式快速複習：</span><span class="sxs-lookup"><span data-stu-id="e60ee-187">Here's a quick refresher on how the time-outs interact with the upgrade times:</span></span>

<span data-ttu-id="e60ee-188">升級網域的升級完成時間無法快於 HealthCheckWaitDuration  +  HealthCheckStableDuration。</span><span class="sxs-lookup"><span data-stu-id="e60ee-188">Upgrades for an upgrade domain cannot complete faster than *HealthCheckWaitDuration* + *HealthCheckStableDuration*.</span></span>

<span data-ttu-id="e60ee-189">升級失敗發生時間無法快於 HealthCheckWaitDuration  +  HealthCheckRetryTimeout。</span><span class="sxs-lookup"><span data-stu-id="e60ee-189">Upgrade failure cannot occur faster than *HealthCheckWaitDuration* + *HealthCheckRetryTimeout*.</span></span>

<span data-ttu-id="e60ee-190">升級網域的升級時間受到 *UpgradeDomainTimeout*限制。</span><span class="sxs-lookup"><span data-stu-id="e60ee-190">The upgrade time for an upgrade domain is limited by *UpgradeDomainTimeout*.</span></span>  <span data-ttu-id="e60ee-191">如果 HealthCheckRetryTimeout 和 HealthCheckStableDuration 兩者都為非零且應用程式的健康狀態會保持來回切換，則升級最終會在 UpgradeDomainTimeout 逾時。</span><span class="sxs-lookup"><span data-stu-id="e60ee-191">If *HealthCheckRetryTimeout* and *HealthCheckStableDuration* are both non-zero and the health of the application keeps switching back and forth, then the upgrade eventually times out on *UpgradeDomainTimeout*.</span></span> <span data-ttu-id="e60ee-192">*UpgradeDomainTimeout* 就會開始倒數計時。</span><span class="sxs-lookup"><span data-stu-id="e60ee-192">*UpgradeDomainTimeout* starts counting down once the upgrade for the current upgrade domain begins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e60ee-193">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e60ee-193">Next steps</span></span>
<span data-ttu-id="e60ee-194">[使用 Visual Studio 升級您的應用程式](service-fabric-application-upgrade-tutorial.md) 將引導您完成使用 Visual Studio 進行應用程式升級的步驟。</span><span class="sxs-lookup"><span data-stu-id="e60ee-194">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>

<span data-ttu-id="e60ee-195">[使用 PowerShell 升級您的應用程式](service-fabric-application-upgrade-tutorial-powershell.md) 將引導您完成使用 PowerShell 進行應用程式升級的步驟。</span><span class="sxs-lookup"><span data-stu-id="e60ee-195">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>

<span data-ttu-id="e60ee-196">使用 [升級參數](service-fabric-application-upgrade-parameters.md)來控制您應用程式的升級方式。</span><span class="sxs-lookup"><span data-stu-id="e60ee-196">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>

<span data-ttu-id="e60ee-197">了解如何使用 [資料序列化](service-fabric-application-upgrade-data-serialization.md)，以讓您的應用程式升級相容。</span><span class="sxs-lookup"><span data-stu-id="e60ee-197">Make your application upgrades compatible by learning how to use [Data Serialization](service-fabric-application-upgrade-data-serialization.md).</span></span>

<span data-ttu-id="e60ee-198">參考 [進階主題](service-fabric-application-upgrade-advanced.md)，以了解如何在升級您的應用程式時使用進階功能。</span><span class="sxs-lookup"><span data-stu-id="e60ee-198">Learn how to use advanced functionality while upgrading your application by referring to [Advanced Topics](service-fabric-application-upgrade-advanced.md).</span></span>
