---
title: "應用程式升級：升級參數 | Microsoft Docs"
description: "描述參數相關的 tooupgrading Service Fabric 應用程式，包括健康情況檢查 tooperform 和原則 tooautomatically 復原 hello 升級。"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: a4170ac6-192e-44a8-b93d-7e39c92a347e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: abd0ba48c223be9aa0909c7a0100ba5986430db3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-upgrade-parameters"></a>應用程式升級參數
本文說明的 hello Azure Service Fabric 應用程式的升級期間 hello 適用於各種不同的參數。 hello 參數包括 hello 名稱和版本的 hello 應用程式。 它們是控制 hello 逾時和 hello 升級期間所套用的健康情況檢查的參數，而且它們會指定必須在升級失敗時套用的 hello 原則。

<br>

| 參數 | 說明 |
| --- | --- |
| ApplicationName |正在升級的 hello 應用程式名稱。 範例：fabric:/VisualObjects、fabric:/ClusterMonitor |
| TargetApplicationTypeVersion |hello hello hello 升級目標的應用程式類型版本。 |
| FailureAction |hello hello 升級失敗時，Service Fabric 所採取的動作。 hello 應用程式可能已回復 toohello 更新前版本 （復原），或 hello 升級可能會停止在 hello 目前升級網域。 在 hello 後者的情況下，hello 升級模式也會變更的 tooManual。 允許的值為回復和手動。 |
| HealthCheckWaitDurationSec |Service Fabric 評估 hello hello 應用程式的健全狀況之前 （以秒為單位） hello 升級後的 hello 時間 toowait 完成 hello 升級網域上。 這段期間也可視為 hello 時間應該先執行應用程式，它可以視為狀況良好。 如果通過 hello 健全狀況檢查，hello 升級程序會繼續 toohello 下一個升級網域。  如果 hello 健全狀況檢查失敗時，Service Fabric 等候一段時間 (hello UpgradeHealthCheckInterval) 後再重試一次，直到達到 HealthCheckRetryTimeout hello 的 hello 健全狀況檢查。 hello 預設和建議的值為 0 秒。 |
| HealthCheckRetryTimeoutSec |hello 持續時間 （以秒為單位），Service Fabric 會繼續 tooperform 宣告 hello 升級為失敗之前的健全狀況評估。 hello 預設值為 600 秒。 此期間會在達到 HealthCheckWaitDuration 之後開始計算。 在此 HealthCheckRetryTimeout，Service Fabric 可能會執行多個健全狀況檢查的 hello 應用程式健全狀況。 hello 預設值為 10 分鐘，而且應該適當地自訂應用程式。 |
| HealthCheckStableDurationSec |hello 的持續時間 （以秒為單位） tooverify hello 應用程式之前移動下一個升級網域 toohello 穩定或完成 hello 升級。 這個等候持續時間之後執行 hello 健全狀況檢查的健全狀況使用的 tooprevent 未偵測到變更。 hello 預設值為 120 秒，並應該適當地自訂應用程式。 |
| UpgradeDomainTimeoutSec |升級單一升級網域的時間上限 (以秒為單位)。 如果達到此逾時，hello 升級就會停止，並繼續根據 UpgradeFailureAction hello 設定。 hello 預設值絕不會是 （無限時），而且應該適當地自訂應用程式。 |
| UpgradeTimeout |逾時 （以秒為單位），適用於 hello 整個升級。 如果達到此逾時，hello 升級停駐點，並觸發 UpgradeFailureAction。 hello 預設值絕不會是 （無限時），而且應該適當地自訂應用程式。 |
| UpgradeHealthCheckInterval |會檢查 hello hello 健全狀況狀態的頻率。 Hello hello ClusterManager 區段中指定這個參數*叢集**資訊清單*，而且未指定 hello 升級 cmdlet 的一部分。 hello 預設值為 60 秒。 |

<br>

## <a name="service-health-evaluation-during-application-upgrade"></a>應用程式升級期間的服務健康狀態評估
<br>
hello 健全狀況評估準則是選擇性的。 如果未指定 hello 健全狀況評估準則，開始升級時，Service Fabric 使用 hello hello ApplicationManifest.xml hello 應用程式執行個體中指定的應用程式健全狀況原則。

<br>

| 參數 | 說明 |
| --- | --- |
| ConsiderWarningAsError |預設值為 False。 評估 hello hello 升級期間的應用程式的健全狀況時，請將視為錯誤的 hello hello 應用程式的警告健全狀況事件。 根據預設，Service Fabric 不會評估警告健全狀況事件 toobe 失敗 （錯誤），因此 hello 升級可以繼續執行，即使有警告事件。 |
| MaxPercentUnhealthyDeployedApplications |預設值和建議值為 0。 指定已部署應用程式的 hello 最大數目 (請參閱 hello[健全狀況 > 一節](service-fabric-health-introduction.md)) 的狀況不良之前可以 hello 應用程式會被視為狀況不良且失敗 hello 升級。 此參數定義 hello 應用程式健全狀況 hello 節點上，並可協助在升級期間偵測問題。 通常，hello 複本 hello 應用程式獲得負載平衡 toohello 其他節點，可讓 hello 應用程式 tooappear 狀況良好，進而 hello 升級 tooproceed。 藉由指定嚴格的 MaxPercentUnhealthyDeployedApplications 健全狀況，Service Fabric 可以快速地偵測 hello 應用程式套件有問題，並協助產生快速升級失敗。 |
| MaxPercentUnhealthyServices |預設值和建議值為 0。 指定 hello 應用程式會被視為狀況不良，而且失敗 hello 升級前可保留其狀況不良的 hello 應用程式執行個體中的 hello 的服務數目上限。 |
| MaxPercentUnhealthyPartitionsPerService |預設值和建議值為 0。 指定 hello 服務視為狀況不良之前可能處於不健全狀況服務中的 hello 資料分割數目上限。 |
| MaxPercentUnhealthyReplicasPerPartition |預設值和建議值為 0。 指定 hello 分割區視為狀況不良之前可以處於狀況不良的資料分割中的 hello 複本數目上限。 |
| UpgradeReplicaSetCheckTimeout |**無狀態服務**-單一升級網域內 Service Fabric 嘗試 tooensure hello 服務的其他執行個體可用。 如果一個以上的 hello 目標執行個體計數，Service Fabric 會等候多個執行個體 toobe 可用總 tooa 最大逾時值。 透過 hello UpgradeReplicaSetCheckTimeout 屬性會指定這個逾時值。 如果 hello 逾時到期，Service Fabric 會繼續執行 hello 升級時，無論 hello 服務執行個體數目。 如果其中一個 hello 目標執行個體計數，Service Fabric 不會等待，然後進行立即 hello 升級。 **具狀態服務**-單一升級網域內 Service Fabric 嘗試 hello 複本的 tooensure 集有仲裁。 Service Fabric 等候仲裁 toobe 可用總 tooa 最大逾時值 （hello UpgradeReplicaSetCheckTimeout 屬性所指定）。 如果 hello 逾時到期，Service Fabric 會繼續執行 hello 升級時，不論仲裁。 此設定在向前回復時是設定為永不 (無限)，向後回復時則為 900 秒。 |
| ForceRestart |如果您更新的組態或資料套件而無須更新 hello 服務程式碼時，只有當設定 tootrue hello ForceRestart 屬性，會重新啟動 hello 服務。 Hello 更新完成時，Service Fabric 通知 hello 服務新設定的封裝資料可供使用。 hello 服務會負責套用 hello 變更。 如有必要，hello 服務可以自行重新啟動。 |

<br>
<br>
hello MaxPercentUnhealthyServices、 MaxPercentUnhealthyPartitionsPerService 及 MaxPercentUnhealthyReplicasPerPartition 條件可以指定每個應用程式執行個體的服務類型。 設定這些參數個別服務可讓應用程式 toocontain 不同服務使用不同的評估原則的型別。 例如，特定應用程式執行個體的無狀態閘道器服務類型，可以有與可設定狀態的引擎服務類型不同的 MaxPercentUnhealthyPartitionsPerService。

## <a name="next-steps"></a>後續步驟
[使用 Visual Studio 升級您的應用程式](service-fabric-application-upgrade-tutorial.md) 將引導您完成使用 Visual Studio 進行應用程式升級的步驟。

[使用 PowerShell 升級您的應用程式](service-fabric-application-upgrade-tutorial-powershell.md) 將引導您完成使用 PowerShell 進行應用程式升級的步驟。

[在 Linux 上使用 Service Fabric CLI 升級應用程式](service-fabric-application-lifecycle-sfctl.md#upgrade-application)會引導您完成使用 Service Fabric CLI 升級應用程式的步驟。

[使用 Service Fabric Eclipse 外掛程式升級應用程式](service-fabric-get-started-eclipse.md#upgrade-your-service-fabric-java-application)

讓應用程式升級相容所學習如何 toouse[資料序列化](service-fabric-application-upgrade-data-serialization.md)。

了解 toouse 把太升級您的應用程式時所進階的功能[進階主題](service-fabric-application-upgrade-advanced.md)。

藉由參考 toohello 步驟中的修正應用程式升級的一般問題[疑難排解應用程式升級](service-fabric-application-upgrade-troubleshooting.md)。
