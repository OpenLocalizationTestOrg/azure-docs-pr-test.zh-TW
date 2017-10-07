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
# <a name="use-system-health-reports-tootroubleshoot"></a>使用系統健全狀況報表 tootroubleshoot
Azure Service Fabric 元件報表 hello 現成 hello 叢集中的所有實體。 hello[健全狀況存放區](service-fabric-health-introduction.md#health-store)會建立和刪除 hello 系統報表基礎的實體。 它也會將這些實體組織為階層以擷取實體的互動。

> [!NOTE]
> toounderstand 健全狀況相關的概念，深入了解在[服務網狀架構健全狀況模型](service-fabric-health-introduction.md)。
> 
> 

系統健康狀態報告可讓您全盤掌握叢集和應用程式功能，並透過健康狀態標記問題。 應用程式和服務，實體實作，且從 hello Service Fabric 觀點來看運作正確，請確認系統健康情況報告。 hello 報表沒有提供任何顯示的 hello 服務 hello 商務邏輯和偵測無回應的處理程序的健全狀況監視。 使用者服務可以擴充資訊特定 tootheir 邏輯與 hello 健全狀況資料。

> [!NOTE]
> 只會顯示 watchdogs 健康情況報告*之後*hello 系統元件建立實體。 刪除實體時，hello 健全狀況存放區會自動刪除所有與其相關聯的健康情況報告。 hello 也是如此建立 hello 實體的新執行個體時 （例如，建立新的可設定狀態的持續性的服務複本執行個體）。 刪除或清除從 hello 存放區與 hello 舊的執行個體相關聯的所有報表。
> 
> 

hello 系統元件報告，藉以 hello 來源，以 hello 開頭"**系統。**" 。 Watchdogs 無法使用相同的前置詞及其來源，hello，因為報表內含無效的參數會遭到拒絕。
讓我們來看一些系統回報 toounderstand 觸發它們，並它們代表如何 toocorrect hello 可能的問題。

> [!NOTE]
> Service Fabric 會繼續 tooadd 報表感興趣的改善掌握 hello 叢集和應用程式中發生的狀況。 也可以增強現有的報表含有詳細 toohelp hello 對問題進行疑難排解更快。
> 
> 

## <a name="cluster-system-health-reports"></a>叢集系統健康狀態報告
hello health store 中自動建立 hello 叢集健全狀況的實體。 如果一切正常運作，則不會有系統報告。

### <a name="neighborhood-loss"></a>網路上的芳鄰遺失
**System.Federation** 偵測到網路上的芳鄰遺失時，即會回報錯誤。 hello 報表會從個別節點，而且 hello 節點識別碼會包含在 hello 屬性名稱。 如果 hello 整個 Service Fabric 環形將會遺失一個上的芳鄰，您通常可以預期兩個事件 （兩端 hello 間距報表）。 如果有多個網路上的芳鄰遺失，將會產生更多的事件。

hello 報表指定 hello 時間 toolive hello 全域租用逾時。 hello 報表重新傳送 hello TTL 持續時間的每個半只要 hello 條件維持使用中。 到期時，會自動移除 hello 事件。 卸除過期的行為可確保，hello 報表是從 hello health store 正確地清除，即使 hello reporting 節點已關閉。

* **SourceId**：System.Federation
* **Property**：以 **Neighborhood** 為開頭且包含節點資訊
* **後續步驟**： 調查 hello 上的芳鄰 為何遺失 （例如，叢集節點之間的核取 hello 通訊）。

## <a name="node-system-health-reports"></a>節點系統健康狀態報告
**System.FM**，這代表 hello Failover Manager service、 管理叢集節點的相關資訊的 hello 授權單位。 每個節點都應該有一份來自 System.FM 的報告，以顯示其狀態。 移除 hello 節點狀態時，會移除 hello 節點實體 (請參閱[RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync))。

### <a name="node-updown"></a>節點運作中/關閉
Hello 節點加入 hello 信號 （已啟動並執行） 時，System.FM 會回報為 [確定]。 Hello 節點貨車 hello 信號時，它會報告錯誤 (已關閉，請升級或只是因為它失敗)。 部署中的實體與 System.FM 節點報告相互關聯 hello 健全狀況存放區所建立的 hello 健全狀況階層會採取的動作。 它會考慮 hello 節點虛擬已部署的所有實體的父系。 如果 hello 節點報告為向上 System.FM，hello 與相同執行個體與 hello 與 hello 實體相關聯的執行個體，該節點上部署的 hello 實體會公開透過查詢。 當 System.FM 報告該 hello 節點已關閉或重新啟動 （的新執行個體） 時，hello 健全狀況存放區會自動清除在於只有 hello 節點關閉或 hello hello 節點的上一個執行個體上部署的 hello 實體。

* **SourceId**：System.FM
* **Property**：State
* **後續步驟**： 如果 hello 節點已關閉升級，它應該恢復一旦已升級。 在此情況下，hello 健全狀況狀態應該切換後 tooOK。 如果 hello 節點不會再次發生，否則便會失敗，hello 問題，需要較多調查。

hello 下例健全狀況狀態為 [確定] 節點的 hello System.FM 事件一同顯示：

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


### <a name="certificate-expiration"></a>憑證到期
**System.FabricNode** hello 節點所使用的憑證即將到期時，回報警告。 每個節點有三個憑證：**Certificate_cluster**、**Certificate_server** 及 **Certificate_default_client**。 至少兩週後 hello 到期時，hello 報表健全狀況狀態是 [確定]。 在兩週內 hello 到期時，hello 報表類型是一個警告。 這些事件的 TTL 是無限的以及當節點離開叢集 hello 中予以移除。

* **SourceId**：System.FabricNode
* **屬性**： 開頭**憑證**和包含 hello 憑證類型的詳細資訊
* **後續步驟**： 更新 hello 憑證是否即將到期。

### <a name="load-capacity-violation"></a>負載容量違規
hello Service Fabric 負載平衡器會回報警告。 當它偵測到節點容量違規。

* **SourceId**：System.PLB
* **Property**：以 **Capacity** 為開頭
* **後續步驟**: hello 節點上檢查所提供的度量和檢視 hello 目前容量。

## <a name="application-system-health-reports"></a>應用程式系統健康狀態報告
**System.CM**，這代表 hello 叢集管理員服務，是 hello 授權管理應用程式的相關資訊。

### <a name="state"></a>State
System.CM 報告為 [確定] 時已建立或更新 hello 應用程式。 它會通知 hello 健全狀況存放區刪除 hello 應用程式後，使它可以從存放區中移除。

* **SourceId**：System.CM
* **Property**：State
* **後續步驟**： 如果已建立或更新 hello 應用程式，它應該包含 hello 叢集管理員健康情況報告。 否則，請檢查 hello hello 應用程式狀態，藉由發出查詢 (例如，hello PowerShell cmdlet **Get ServiceFabricApplication ApplicationName *applicationName***)。

hello 下列範例示範 hello 狀態事件在 hello **fabric: / WordCount**應用程式：

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

## <a name="service-system-health-reports"></a>服務系統健康狀態報告
**System.FM**，這代表 hello Failover Manager service、 管理服務的相關資訊的 hello 授權單位。

### <a name="state"></a>State
System.FM 做為 [確定] 時，回報 hello 服務已經建立完成。 Hello 服務已被刪除時，從 hello health store 刪除 hello 實體。

* **SourceId**：System.FM
* **Property**：State

hello 下列範例示範 hello 狀態事件在 hello 服務**fabric: / WordCount/WordCountWebService**:

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

### <a name="service-correlation-error"></a>服務相互關聯錯誤
**System.PLB**偵測到更新服務 toobe 相互關聯的另一個服務會建立同質鏈結時報告錯誤。 當成功更新時，會清除 hello 報表。

* **SourceId**：System.PLB
* **屬性**︰ServiceDescription
* **後續步驟**： 核取 hello 相互關聯的服務描述。

## <a name="partition-system-health-reports"></a>分割區系統健康狀態報告
**System.FM**，這代表 hello Failover Manager service、 管理的服務資料分割的相關資訊的 hello 授權單位。

### <a name="state"></a>State
System.FM 報告為 [確定] 時已建立 hello 磁碟分割，且狀況良好。 Hello 資料分割會刪除時，從 hello health store 刪除 hello 實體。

如果 hello 分割低於 hello 最小複本計數，它會報告錯誤。 如果 hello 分割不低於 hello 最小複本計數，但它低於 hello 目標複本計數，它會回報警告。 如果 hello 磁碟分割在仲裁遺失，System.FM 報告錯誤。

Hello 重新設定所花費的時間超出預期，以及當 hello 組建所花費的時間比預期時，其他重要事件會包含警告。 hello 組建及重新設定的 hello 預期時間皆可設定依據服務案例。 例如，如果服務的狀態，例如 SQL Database tb hello 建置時間長於只需要編寫小量狀態的服務。

* **SourceId**：System.FM
* **Property**：State
* **後續步驟**： 如果 hello 健全狀況狀態不是 [確定]，則可能的一些複本尚未建立、 開啟，或升級 tooprimary 或次要資料庫正確。 在許多情況下，hello 根本原因是服務中的錯誤 hello 開啟或變更角色實作。

下列範例中的 hello 顯示狀況良好的磁碟分割：

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

hello 下列範例顯示 hello 低於目標複本計數的資料分割的健全狀況。 hello 下一個步驟是 tooget hello 資料分割說明，其中顯示設定的方式： **MinReplicaSetSize**是三個和**TargetReplicaSetSize**為 7 個。 然後取得 hello 叢集中的節點數目 hello： 五個。 因此在此情況下，兩個複本不能放因為複本的 hello 目標數目高於 hello 可用的節點數目。

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

### <a name="replica-constraint-violation"></a>複本條件約束違規
**System.PLB** 偵測到複本條件約束違規，且無法安置所有磁碟分割複本時，就會回報警告。 hello 報表詳細資料會顯示哪些條件約束，且屬性防止 hello 複本位置。

* **SourceId**：System.PLB
* **Property**：以 **ReplicaConstraintViolation** 為開頭

## <a name="replica-system-health-reports"></a>複本系統健康狀態報告
**System.RA**，代表 hello 重新設定代理程式元件，為 hello 進行授權 hello 複本狀態。

### <a name="state"></a>State
**System.RA** hello 複本建立後會報告 [確定]。

* **SourceId**：System.RA
* **Property**：State

下列範例中的 hello 顯示狀況良好的複本：

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

### <a name="replica-open-status"></a>複本開啟狀態
hello API 呼叫叫用時，此健全狀況報告 hello 描述包含 hello 開始時間 （國際標準時間）。

**System.RA**會回報警告。 如果開啟的 hello 複本所花費的時間比設定的 hello 期間 (預設： 30 分鐘)。 如果 hello API，將會影響服務可用性，hello 報表就會發出速度 （可設定的間隔，預設值是 30 秒為單位）。 hello 測量的時間會包含 hello hello 複寫器開啟與 hello 服務開啟花費的時間。 如果開啟 hello hello 屬性變更 tooOK 完成。

* **SourceId**：System.RA
* **Property**服務上的狀態事件： **ReplicaOpenStatus**
* **後續步驟**： 如果 hello 健全狀況狀態不確定，請調查為何開啟 hello 複本所花費的時間超出預期。

### <a name="slow-service-api-call"></a>緩慢服務 API 呼叫
**System.RAP**和**System.Replicator**如果呼叫 toohello 使用者服務程式碼所花費的時間比設定的 hello 時間會報告警告。 hello 呼叫完成時，會清除 hello 警告。

* **SourceId**：System.RAP 或 System.Replicator
* **屬性**: hello hello 緩慢 API 名稱。 hello 描述可提供更多詳細 hello 時間 hello 應用程式開發介面已暫止。
* **後續步驟**： 調查為何 hello 呼叫所花費的時間超出預期。

hello 下列範例會顯示資料分割在仲裁遺失和 hello 調查步驟完成 toofigure 找出原因。 其中一個 hello 複本有警告健全狀況狀態，因此您會取得其健全狀況。 它會顯示 hello 服務作業所花費的時間超出預期，System.RAP 所報告的事件。 收到這項資訊之後，hello 下一個步驟是 toolook hello 服務程式碼，並那里調查。 此案例中，hello **RunAsync** hello 具狀態服務實作會擲回未處理的例外狀況。 回收處理 hello 複本，因此您可能不會看見 hello 警告狀態中的任何複本。 您可以再試一次取得 hello 健全狀況狀態，並尋找任何差異 hello 複本識別碼。 在某些情況下，hello 重試次數可讓您找出線索。

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

當您啟動 hello 偵錯工具之下 hello 錯誤的應用程式時，hello 診斷事件視窗會顯示 hello RunAsync 從擲回的例外狀況：

![Visual Studio 2015 診斷事件：RunAsync 在 fabric:/HelloWorldStatefulApplication 中失敗。][1]

Visual Studio 2015 診斷事件：RunAsync 在 **fabric:/HelloWorldStatefulApplication**中失敗。

[1]: ./media/service-fabric-understand-and-troubleshoot-with-system-health-reports/servicefabric-health-vs-runasync-exception.png


### <a name="replication-queue-full"></a>複寫佇列已滿
**System.Replicator** hello 複寫佇列已滿時，回報警告。 在主要 hello 複寫佇列通常會變成完整因為一或多個次要複本緩慢 tooacknowledge 作業。 在次要 hello，這通常發生於 hello 服務會緩慢 tooapply hello 作業。 無法再完整 hello 佇列時，會清除 hello 警告。

* **SourceId**：System.Replicator
* **屬性**: **PrimaryReplicationQueueStatus**或**SecondaryReplicationQueueStatus**，端視 hello 複本角色

### <a name="slow-naming-operations"></a>緩慢的命名作業
**System.NamingService** 會報告其主要複本的健全狀況。 命名作業的範例為 [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) 或 [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync)。 在 FabricClient 下可以找到更多方法，例如在[服務管理方法](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient)或[屬性管理方法](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient)底下。

> [!NOTE]
> hello 命名服務解析 hello 叢集中的服務名稱 tooa 位置，並可讓使用者 toomanage 服務名稱和屬性。 它是 Service Fabric 資料分割保存的服務。 Hello 分割區之一代表 hello 授權擁有者，其中包含所有服務網狀架構名稱和服務的相關中繼資料。 hello Service Fabric 名稱不對應的 toodifferent 資料分割，稱為名稱的擁有者資料分割，因此 hello 服務是可延伸。 深入了解 [命名服務](service-fabric-architecture.md)。
> 
> 

當命名作業花費的時間超出預期時，hello 作業都將標示 hello 警告報告*hello 命名服務資料分割的主要複本做 hello 作業*。 如果 hello 作業順利完成，hello 警告會清除。 Hello 作業完成，發生錯誤時，如果 hello 健康情況報告包含關於 hello 錯誤詳細資料。

* **SourceId**：System.NamingService
* **屬性**： 以字首開始**Duration_**並識別 hello 很慢的作業和作業套用在哪一個 hello hello 服務網狀架構名稱。 例如，如果在名稱網狀架構建立服務: / MyApp/MyService 費時過久，hello 屬性是 Duration_AOCreateService.fabric:/MyApp/MyService。 AO 點 toohello hello 命名資料分割，這個名稱和作業的角色。
* **後續步驟**： 核取 hello 命名作業失敗的原因。 每個作業都可能有不同的根本原因。 例如，刪除服務可能會卡在節點上，因為 hello 應用程式主機會保留因 tooa 使用者 bug hello 服務程式碼中的節點上損毀。

hello 下列範例會示範建立服務作業。 hello 作業花費的時間超過設定的 hello 持續時間。 AO 重試，並將傳送工作 tooNO。 逾時沒有完成的 hello 最後一個作業。 在此情況下，hello 相同的複本是主要 hello AO 和任何角色。

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

## <a name="deployedapplication-system-health-reports"></a>DeployedApplication 系統健康狀態報告
**System.Hosting** hello 授權單位上已部署的實體。

### <a name="activation"></a>啟用
System.Hosting 做為 [確定] 時，回報應用程式已成功啟動 hello 節點上。 否則，它會報告錯誤。

* **SourceId**：System.Hosting
* **屬性**： 啟動過程中，包括 hello 首度發行版本
* **後續步驟**: hello 應用程式是否處於狀況不良，調查 hello 啟動失敗的原因。

hello 下列範例顯示成功的啟用：

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

### <a name="download"></a>下載
**System.Hosting**報告錯誤，如 hello 應用程式套件下載失敗。

* **SourceId**：System.Hosting
* **Property**：**Download:*RolloutVersion***
* **後續步驟**： 調查 hello 下載 hello 節點上失敗的原因。

## <a name="deployedservicepackage-system-health-reports"></a>DeployedServicePackage 系統健康狀態報告
**System.Hosting** hello 授權單位上已部署的實體。

### <a name="service-package-activation"></a>服務封裝啟用
System.Hosting 報告為 [確定] hello 節點上的 hello 服務封裝啟用是否成功。 否則，它會報告錯誤。

* **SourceId**：System.Hosting
* **Property**：Activation
* **後續步驟**： 調查 hello 啟動失敗的原因。

### <a name="code-package-activation"></a>程式碼封裝啟用
**System.Hosting** hello 啟用成功時的每個程式碼封裝報告為 [確定]。 如果 hello 啟用失敗，它會報告警告設定。 如果**CodePackage**失敗 tooactivate 或終止時發生大於設定的 hello **CodePackageHealthErrorThreshold**，裝載報告錯誤。 如果服務封裝包含多個程式碼封裝，就會針對每個封裝產生啟用報告。

* **SourceId**：System.Hosting
* **屬性**： 使用 hello 前置詞**CodePackageActivation**和包含 hello 名稱 hello 程式碼封裝以及 hello 進入點為 **CodePackageActivation:*CodePackageName*:*SetupEntryPoint/EntryPoint** * (例如， **CodePackageActivation:Code:SetupEntryPoint**)

### <a name="service-type-registration"></a>服務類型註冊
**System.Hosting**回報為 [確定]，如果已成功登錄 hello 服務類型。 它會報告錯誤，如果 hello 註冊未完成的時間 (依使用的設定**ServiceTypeRegistrationTimeout**)。 如果 hello 執行階段已關閉，hello 服務類型是 hello 節點從取消註冊，並裝載會回報警告。

* **SourceId**：System.Hosting
* **屬性**： 使用 hello 前置詞**ServiceTypeRegistration**和包含 hello 服務型別名稱 (例如， **ServiceTypeRegistration:FileStoreServiceType**)

下列範例中的 hello 顯示狀況良好的已部署的服務封裝：

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

### <a name="download"></a>下載
**System.Hosting**報告錯誤，如 hello 服務封裝下載失敗。

* **SourceId**：System.Hosting
* **Property**：**Download:*RolloutVersion***
* **後續步驟**： 調查 hello 下載 hello 節點上失敗的原因。

### <a name="upgrade-validation"></a>升級驗證
**System.Hosting**報告錯誤，如果 hello 升級期間執行的驗證失敗，或如果 hello hello 節點上升級會失敗。

* **SourceId**：System.Hosting
* **屬性**： 使用 hello 前置詞**FabricUpgradeValidation**且包含 hello 升級版本
* **描述**： 點 toohello 發生的錯誤

## <a name="next-steps"></a>後續步驟
[檢視 Service Fabric 健康狀態報告](service-fabric-view-entities-aggregated-health.md)

[Tooreport 並檢查服務健全狀況](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[在本機上監視及診斷服務](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Service Fabric 應用程式升級](service-fabric-application-upgrade.md)

