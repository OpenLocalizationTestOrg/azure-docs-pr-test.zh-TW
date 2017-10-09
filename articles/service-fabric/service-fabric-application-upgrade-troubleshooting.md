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
# <a name="troubleshoot-application-upgrades"></a>疑難排解應用程式升級
本文章涵蓋 hello 常見的問題解決升級 Azure Service Fabric 應用程式以及如何 tooresolve 它們。

## <a name="troubleshoot-a-failed-application-upgrade"></a>疑難排解失敗的應用程式升級
當升級失敗時，輸出 hello hello **Get ServiceFabricApplicationUpgrade**命令包含偵錯 hello 失敗的其他資訊。  hello 下列清單會指定如何使用 hello 的其他資訊：

1. 識別 hello 失敗類型。
2. 識別 hello 失敗原因。
3. 隔離一或多個失敗元件以便進一步調查。

這項資訊時，使用 Service Fabric 來偵測 hello 不論是否 hello **FailureAction** tooroll 後或暫停 hello 升級。

### <a name="identify-hello-failure-type"></a>識別 hello 失敗類型
中的 hello 輸出**Get ServiceFabricApplicationUpgrade**， **FailureTimestampUtc**識別 hello 時間戳記 （UTC) 在升級的失敗偵測到的 Service Fabric 和**FailureAction**觸發。 **失敗原因**識別其中三個潛在高層級失敗原因的 hello:

1. UpgradeDomainTimeout-表示特定的升級網域花費太長 toocomplete 和**UpgradeDomainTimeout**過期。
2. OverallUpgradeTimeout-指出整體升級該 hello 花費太長 toocomplete 和**UpgradeTimeout**過期。
3. 在升級之後更新網域，hello 應用程式維持狀況不良的健全狀況檢查時發生-表示根據 toohello 指定健全狀況原則和**HealthCheckRetryTimeout**過期。

這些項目才會顯示在 hello 輸出時 hello 升級失敗，並開始復原。 根據 hello hello 失敗類型而定，會顯示進一步的資訊。

### <a name="investigate-upgrade-timeouts"></a>調查升級逾時
升級逾時失敗通常是由服務可用性問題造成的。 遵循本段 hello 輸出是典型的升級服務複本或執行個體失敗 toostart hello 新版程式碼中。 hello **UpgradeDomainProgressAtFailure**欄位擷取的任何暫止的升級工作，在 hello 發生失敗時的快照集。

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

在此範例中，hello 升級失敗，在升級網域*MYUD1*和兩個資料分割 (*744c8d9f-1d26-417e-a60e-cd48f5c098f0*和*4b43f4d8-b26b-424e-9307-7a7a62e79750*) 已當機。 hello 資料分割所卡 hello 執行階段因為無法 tooplace 主要複本 (*WaitForPrimaryPlacement*) 目標節點上*Node1*和*Node4*。

hello **Get ServiceFabricNode**命令可以使用這兩個節點都升級網域中的 tooverify *MYUD1*。 hello *UpgradePhase*指出*PostUpgradeSafetyCheck*，這表示在 hello 升級網域中的所有節點都完成升級後發生的這些安全檢查。 這項資訊點 tooa hello hello 應用程式程式碼的新版本的潛在問題。 hello 最常見的問題是 hello 開啟或升級 tooprimary 程式碼路徑中的服務錯誤。

*UpgradePhase*的*PreUpgradeSafetyCheck*表示有一些問題它執行前準備 hello 升級網域。 hello 最常見的問題在此情況下會關閉 hello 或降級，從主要的程式碼路徑中的服務錯誤。

目前的 hello **UpgradeState**是*RollingBackCompleted*，因此 hello 原始升級必須已執行並回復**FailureAction**，它會自動回復在失敗後的 hello 升級。 如果可以使用手動執行 hello 原始升級**FailureAction**，然後 hello 升級會改為在暫停的狀態 tooallow 即時 hello 應用程式的偵錯。

### <a name="investigate-health-check-failures"></a>調查健康狀態檢查失敗
升級網域中的所有節點完成升級並通過所有安全檢查之後，各種問題都可能觸發健康狀態檢查失敗。 遵循本段 hello 輸出是典型的升級失敗，因為 toofailed 健康情況檢查。 hello **UnhealthyEvaluations**欄位擷取快照集的健康情況檢查失敗時，根據指定的 toohello hello 升級的 hello[健全狀況原則](service-fabric-health-introduction.md)。

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

調查健全狀況檢查失敗需要先了解 hello 服務網狀架構健全狀況模型。 但即使沒有這類深入了解，我們可以看到兩個服務的狀況不良： *fabric: / demoapp 來/Svc3*和*網狀架構: / demoapp 來/Svc2*，以及 hello 錯誤健全狀況報表 (「 InjectedFault「 在此情況下）。 在此範例中，四個兩個服務是狀況不良，這是低於 0%狀況不良的 hello 預設目標 (*MaxPercentUnhealthyServices*)。

hello 升級暫止容錯時藉由指定**FailureAction**的手動時啟動 hello 升級。 此模式可讓我們 tooinvestigate hello 即時系統在 hello 失敗狀態之前採取任何進一步的動作。

### <a name="recover-from-a-suspended-upgrade"></a>從暫止升級復原
並回復**FailureAction**，沒有任何因為 hello 升級會自動回復在失敗時所需的復原。 使用手動 **FailureAction**，有數個復原選項：

1.  觸發回復
2. 手動繼續執行其餘部分 hello hello 升級
3. 繼續 hello 監視升級

hello**開始 ServiceFabricApplicationRollback**命令可在任何時間 toostart，回復 hello 應用程式。 Hello 命令會傳回成功，hello 復原要求 hello 系統中已註冊後不久之後啟動。

hello **Resume-servicefabricapplicationupgrade**命令可以用 tooproceed hello 其餘部分的 hello 透過手動升級一個升級網域，一次。 在此模式中，唯一的安全性檢查會執行 hello 系統。 不會執行其他健康狀態檢查。 此命令只可用時 hello *UpgradeState*顯示*RollingForwardPending*，這表示該 hello 目前升級網域升級已完成，但 hello 接下來一個啟動 （擱置）。

hello**更新 ServiceFabricApplicationUpgrade**命令可以使用的 tooresume hello 監視升級的安全性和健全狀況檢查正在執行。

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

hello 升級會繼續從上次已中暫止的 hello 升級網域和使用 hello 參數和健全狀況原則之前，相同升級。 如有需要 hello hello 升級繼續時，相同命令中就可以變更任何 hello 升級參數和健全狀況原則 hello 前面輸出所示。 在此範例中，hello 升級已繼續在受監視模式中，使用 hello 參數和不變的 hello 健康原則。

## <a name="further-troubleshooting"></a>進一步疑難排解
### <a name="service-fabric-is-not-following-hello-specified-health-policies"></a>Service Fabric 不遵循 hello 指定健全狀況原則
可能的原因 1：

Service Fabric 的健全狀況評估轉譯實際的實體 （例如複本、 資料分割，與服務） 的數字為所有的百分比，一律會無條件進位 toowhole 實體。 例如，如果 hello 最大*MaxPercentUnhealthyReplicasPerPartition*是 21%且有五個複本，然後 Service Fabric 允許 tootwo 狀況不良的複本 (也就是`Math.Ceiling (5*0.21)`)。 因此，健康狀態原則應該據此設定。

可能的原因 2：

健康狀態原則是以服務總計的百分比指定，而不是根據特定服務執行個體。 例如，再升級時，如果應用程式有四個服務執行個體 A、 B、 C 以及 D，，其中服務 D 是狀況不良，但以小的影響 toohello 應用程式。 我們想要在升級和設定 hello 參數期間知道狀況不良服務 D 的 tooignore hello *MaxPercentUnhealthyServices* toobe 25%，假設 A、 B 和 C 需要 toobe 狀況良好。

不過，hello 在升級期間，D 時可能變成狀況良好 C 會變為狀況不良。 hello 升級仍然會成功，因為只有 25%的 hello 服務均狀況不良。 不過，它可能會導致非預期的錯誤到期 tooC 被意外狀況不良，而不是 d。在此情況下，D 應該會模式化為不同的服務類型 a、 B 和 c。健全狀況原則會指定每個服務類型，因為不同的狀況不良百分比閾值可套用的 toodifferent 服務。 

### <a name="i-did-not-specify-a-health-policy-for-application-upgrade-but-hello-upgrade-still-fails-for-some-time-outs-that-i-never-specified"></a>我未指定應用程式升級的健全狀況原則，但永遠不會指定某些逾時的 hello 升級仍失敗
當健全狀況原則不提供 toohello 升級要求時，它們取自 hello *ApplicationManifest.xml* hello 目前應用程式版本。 例如，如果您要升級應用程式 X 的 1.0 版 tooversion 2.0，會使用在 1.0 版中指定的應用程式健全狀況原則。 如果應使用不同的健全狀況原則 hello 升級，hello 原則需要 toobe hello 應用程式升級的 API 呼叫中指定。 hello hello API 呼叫中指定的原則僅適用於 hello 升級期間。 在 hello hello 升級完成之後，請指定 hello 原則*ApplicationManifest.xml*可用。

### <a name="incorrect-time-outs-are-specified"></a>指定了不正確的逾時
您可能想要知道當逾時設定不一致時會發生什麼情況。 例如，您可能必須*UpgradeTimeout*低於 hello *UpgradeDomainTimeout*。 hello 辦法就是會傳回錯誤。 會傳回錯誤，如果 hello *UpgradeDomainTimeout*小於 hello 總和*HealthCheckWaitDuration*和*HealthCheckRetryTimeout*，或如果*UpgradeDomainTimeout*小於 hello 總和*HealthCheckWaitDuration*和*HealthCheckStableDuration*。

### <a name="my-upgrades-are-taking-too-long"></a>我的升級耗費太多時間
升級的 toocomplete hello 時間取決於 hello 健全狀況檢查和指定的逾時。 健全狀況檢查和逾時依存於 toocopy 要花多久、 部署和穩定化 hello 應用程式。 使用逾時太過激烈，可能表示會有更多失敗的升級，因此建議保守地從較長的逾時開始。

以下是快速的重新整理程式在 hello 逾時與 hello 升級時間之間的互動方式：

升級網域的升級完成時間無法快於 HealthCheckWaitDuration  +  HealthCheckStableDuration。

升級失敗發生時間無法快於 HealthCheckWaitDuration  +  HealthCheckRetryTimeout。

hello 的升級網域升級時間受限於*UpgradeDomainTimeout*。  如果*HealthCheckRetryTimeout*和*HealthCheckStableDuration*兩者都為非零，則 hello 升級最後會逾時上hellohello應用程式的健全狀況會保留，來回切換*UpgradeDomainTimeout*。 *UpgradeDomainTimeout*啟動一次向下計數 hello 升級，如 hello 目前升級網域會開始。

## <a name="next-steps"></a>後續步驟
[使用 Visual Studio 升級您的應用程式](service-fabric-application-upgrade-tutorial.md) 將引導您完成使用 Visual Studio 進行應用程式升級的步驟。

[使用 PowerShell 升級您的應用程式](service-fabric-application-upgrade-tutorial-powershell.md) 將引導您完成使用 PowerShell 進行應用程式升級的步驟。

使用 [升級參數](service-fabric-application-upgrade-parameters.md)來控制您應用程式的升級方式。

讓應用程式升級相容所學習如何 toouse[資料序列化](service-fabric-application-upgrade-data-serialization.md)。

了解 toouse 把太升級您的應用程式時所進階的功能[進階主題](service-fabric-application-upgrade-advanced.md)。
