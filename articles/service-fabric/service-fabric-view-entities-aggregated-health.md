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
# <a name="view-service-fabric-health-reports"></a>檢視 Service Fabric 健康狀態報告
Azure Service Fabric 導入了由健康情況實體組成的[健康情況模型](service-fabric-health-introduction.md)，系統元件和看門狗可以在其上回報所監視的本機情況。 hello[健全狀況存放區](service-fabric-health-introduction.md#health-store)彙總所有健全狀況資料 toodetermine 實體是否狀況良好。

hello 叢集會自動填入傳送嗨系統元件的健康情況報告。 深入了解在[使用系統健康情況報告 tootroubleshoot](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)。

Service Fabric 提供多個方式 tooget hello 彙總健全狀況的 hello 實體：

* [Service Fabric 總管](service-fabric-visualizing-your-cluster.md) 或其他視覺效果工具
* 健康情況查詢 (透過 PowerShell、API 或 REST)
* 一般查詢傳回一份含健全狀況作為其中 hello 內容 （透過 PowerShell、 API 或 REST） 的實體

這些選項，讓我們 toodemonstrate 本機叢集使用五個節點和 hello [fabric: / WordCount 應用程式](http://aka.ms/servicefabric-wordcountapp)。 hello **fabric: / WordCount**應用程式包含兩個預設的服務，可設定狀態之型別的服務`WordCountServiceType`，與無狀態服務型別的`WordCountWebServiceType`。 我變更 hello `ApplicationManifest.xml` toorequire 七 hello 可設定狀態的服務和一個資料分割的目標複本。 因為 hello 叢集中只有五個節點，hello 系統元件會報告警告 hello 服務磁碟分割上，所以下列 hello 目標的計數。

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

## <a name="health-in-service-fabric-explorer"></a>Service Fabric 總管中的健康情況
Service Fabric 總管提供 hello 叢集的視覺化檢視。 在下面的 hello 影像，您可以看到：

* hello 應用程式**fabric: / WordCount**是紅色 （在錯誤），因為它所報告的錯誤事件**MyWatchdog** hello 屬性**可用性**。
* 應用程式的其中一個服務 **fabric:/WordCount/WordCountService** 是黃色 (警告)。 hello 服務已設定有七個複本，且 hello 叢集有五個節點，讓兩個 repicas 不放。 雖然它不會顯示以下，hello 服務資料分割是黃色由於系統報告`System.FM`說`Partition is below target replica or instance count`。 hello 黃色的資料分割的觸發程序 hello 黃色的服務。
* hello 叢集是紅色的因為 hello 紅色應用程式。

hello 評估使用從 hello 叢集資訊清單和應用程式資訊清單的預設原則。 它們是嚴格的原則，不容許任何失敗。

Service Fabric 總管 hello 叢集的檢視：

![Service Fabric 總管 hello 叢集的檢視。][1]

[1]: ./media/service-fabric-view-entities-aggregated-health/servicefabric-explorer-cluster-health.png


> [!NOTE]
> 深入了解 [Service Fabric 總管](service-fabric-visualizing-your-cluster.md)。
>
>

## <a name="health-queries"></a>健康情況查詢
服務網狀架構會公開為每個支援的 hello 的健康狀態查詢[實體類型](service-fabric-health-introduction.md#health-entities-and-hierarchy)。 可以透過 hello 上使用方法的 API 來存取[FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet)，PowerShell cmdlet 和 REST。 這些查詢會傳回有關 hello 實體的完整健全狀況資訊： hello 彙總健全狀況狀態、 實體健全狀況事件、 子健全狀況狀態 （如果適用的話）、 健康情況不良的評估 （當 hello 實體並非狀況良好） 和子系的健全狀況統計資料 （當適用）。

> [!NOTE]
> 健康實體會傳回完整擴展 hello health store 中時。 hello 實體必須是作用中 （不會刪除），並具有系統報告。 其父代上的實體 hello 階層鏈結也必須有系統的報表。 Hello 健全狀況不符合上述任何情況，如果查詢傳回[FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception)與[FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` ，它會顯示 hello 實體不會傳回原因。
>
>

hello 健康狀態查詢數目必須傳入 hello 實體識別碼 hello 實體類型而定。 hello 查詢接受選用的健全狀況原則參數。 如果未不指定任何健全狀況原則，hello[健全狀況原則](service-fabric-health-introduction.md#health-policies)hello 叢集或應用程式資訊清單用來進行評估。 如果 hello 資訊清單不包含的健全狀況原則定義，hello 預設健全狀況原則可用來評估。 hello 預設健全狀況原則不能容許的任何失敗。 hello 查詢也接受篩選條件傳回只有部分的子系或事件-hello 的尊重 hello 指定的篩選。 另一個篩選器允許排除 hello 子系統計資料。

> [!NOTE]
> 因此 hello 訊息回覆縮小 hello 伺服器端，會套用 hello 輸出篩選器。 我們建議您使用 hello 輸出篩選器 toolimit hello 資料傳回，而非 hello 用戶端上套用篩選。
>
>

實體的健康狀態包含︰

* hello hello 實體彙總健全狀況狀態。 實體健全狀況報表、 子系的健全狀況狀態 （如果適用的話），以及健康原則為基礎的 hello 健全狀況存放區，藉以計算。 深入了解 [實體健康情況評估](service-fabric-health-introduction.md#health-evaluation)。  
* hello hello 實體上的健全狀況事件。
* hello 集合的所有子系可以有子系的 hello 實體的健全狀況狀態。 包含實體識別碼及其 hello 彙總健全狀況狀態的 hello 健全狀態。 為子系，tooget 完整健全狀況為 hello 子實體型別呼叫 hello 查詢健全狀況，並傳入 hello 子系識別碼。
* 如果 hello 實體並非狀況良好，hello 狀況不良的評估，該點 toohello 報告，會觸發 hello hello 實體狀態。 hello 評估是遞迴式的其中包含觸發目前的健全狀況狀態的 hello 子系健康情況評估。 例如，看門狗回報了複本錯誤。 hello 應用程式健全狀況顯示狀況不良評估 tooan 狀況不良服務; 到期hello 服務是由於 tooa 錯誤; 中的資料分割的狀況不良hello 資料分割會處於狀況不良，因為發生錯誤; tooa 複本hello 複本為狀況不良到期 toohello 監視錯誤健全狀況報表。
* hello 的所有子系類型有子系的 hello 實體的健全狀況統計資料。 例如，叢集健全狀況顯示 hello 總數應用程式、 服務、 資料分割和複本，並部署 hello 叢集中的實體。 服務健全狀況顯示 hello 總數資料分割和複本 hello 底下指定的服務。

## <a name="get-cluster-health"></a>取得叢集健康情況
會傳回 hello hello 叢集中實體的健全狀況，並包含 hello 健全狀況狀態的應用程式和節點 （hello 叢集的子系）。 輸入：

* [選用] hello 叢集健全狀況原則會使用 tooevaluate hello 節點和 hello 叢集事件。
* [選用] hello 應用程式健全狀況原則對應 hello 健康原則使用 toooverride hello 應用程式資訊清單的原則。
* [選用]事件、 節點及指定感興趣的項目，且傳回 hello 結果 （例如，只，錯誤或警告和錯誤） 中的應用程式的篩選條件。 所有的事件、 節點和應用程式會使用的 tooevaluate hello 實體彙總健全狀況，不論 hello 篩選器。
* [選用]篩選 tooexclude 健全狀況統計資料。
* [選用]篩選 tooinclude fabric: / 系統健全狀況統計資料中的 hello 健全狀況統計資料。 僅適用於未排除 hello 健全狀況統計資料。 根據預設，hello 健全狀況統計資料會包含使用者應用程式和不 hello 系統應用程式的統計資料。

### <a name="api"></a>API
tooget 叢集健全狀況，請建立`FabricClient`和呼叫 hello [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync)方法上的其**HealthManager**。

hello 下列呼叫會取得 hello 叢集健全狀況：

```csharp
ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync();
```

hello 下列程式碼使用自訂的叢集健全狀況原則取得 hello 叢集健全狀況和篩選的節點和應用程式。 它會指定 hello 健全狀況統計資料包括 hello fabric: / 系統的統計資料。 它會建立[ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription)，其中包含 hello 輸入的資訊。

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

### <a name="powershell"></a>PowerShell
hello cmdlet tooget hello 叢集健全狀況是[Get ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth)。 首先，使用 hello 連線 toohello 叢集[Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet。

hello hello 叢集狀態已有五個節點、 hello 系統應用程式，且 fabric: / WordCount 設定中所述。

hello 下列指令程式會使用預設的健全狀況原則，以取得叢集健全狀況。 hello 彙總健全狀況狀態為警告，因為 hello fabric: / WordCount 應用程式處於警告。 請注意 hello 狀況不良的評估 hello 條件觸發 hello 彙總健全狀況所提供的詳細資料。

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

hello 下列 PowerShell cmdlet 會取得 hello hello 叢集健全狀況所使用的自訂應用程式原則。 它會篩選結果 tooget 只有應用程式和錯誤或警告中的節點。 因此不會傳回任何節點，因為全部都狀況良好。 只有 hello fabric: / WordCount 應用程式會尊重 hello 應用程式篩選器。 因為 hello 自訂原則會指定 tooconsider 警告 hello 網狀架構的錯誤為: / WordCount 應用程式，hello 應用程式會評估為錯誤，並且是 hello 叢集。

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

### <a name="rest"></a>REST
您可以取得叢集健全狀況與[GET 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster)或[POST 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy)包含 hello 本文中所述的健全狀況原則。

## <a name="get-node-health"></a>取得節點的健康情況
會傳回 hello 節點實體的健全狀況，並包含報告 hello 節點上的 hello 健康狀態事件。 輸入：

* [必要] hello 節點識別 hello 節點的名稱。
* [選用] hello 叢集健全狀況原則設定會用 tooevaluate 健全狀況。
* [選用]指定感興趣的項目，且傳回 hello 結果 （例如，只，錯誤或警告和錯誤） 中的事件篩選條件。 所有事件都都使用的 tooevaluate hello 實體彙總健全狀況，不論 hello 篩選器。

### <a name="api"></a>API
tooget 節點健全狀況 hello API，透過建立`FabricClient`和呼叫 hello [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync)其 HealthManager 上的方法。

hello 下列程式碼會取得 hello hello 指定的節點名稱的節點健全狀況：

```csharp
NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(nodeName);
```

hello 下列程式碼會取得 hello 節點健全狀況 hello 事件篩選器和自訂原則中指定節點名稱，以及傳遞[NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):

```csharp
var queryDescription = new NodeHealthQueryDescription(nodeName)
{
    HealthPolicy = new ClusterHealthPolicy() {  ConsiderWarningAsError = true },
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.Warning },
};

NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
hello cmdlet tooget hello 節點健全狀況是[Get ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth)。 首先，使用 hello 連線 toohello 叢集[Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet。
hello 下列指令程式會使用預設的健全狀況原則取得 hello 節點健全狀況：

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

hello 下列 cmdlet 會取得所有節點的 hello 健全狀況 hello 叢集中：

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

### <a name="rest"></a>REST
您可以取得節點健全狀況與[GET 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node)或[POST 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy)包含 hello 本文中所述的健全狀況原則。

## <a name="get-application-health"></a>取得應用程式健康情況
傳回 hello 應用程式的實體健全的狀況。 它包含 hello hello 部署應用程式和服務的子節點的健全狀況狀態。 輸入：

* [必要] hello 應用程式名稱 (URI) 可識別 hello 應用程式。
* [選用] hello 應用程式健全狀況原則會使用 toooverride hello 應用程式資訊清單的原則。
* [選用]篩選事件、 服務和已部署的應用程式所指定的項目感興趣，且在 hello 結果 （例如，只，錯誤或警告和錯誤） 傳回。 所有的事件、 服務和已部署應用程式會使用的 tooevaluate hello 實體彙總健全狀況，不論 hello 篩選器。
* [選用]篩選 tooexclude hello 健全狀況統計資料。 如果未指定，hello 健全狀況統計資料包括 hello 確定、 警告和錯誤的應用程式的所有子系計數： 服務資料分割，複本部署的應用程式，及部署服務套件。

### <a name="api"></a>API
tooget 應用程式健全狀況，建立`FabricClient`和呼叫 hello [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync)其 HealthManager 上的方法。

hello 下列程式碼會取得 hello hello 指定應用程式名稱 (URI) 的應用程式健全狀況：

```csharp
ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(applicationName);
```

hello 下列程式碼取得 hello hello 指定應用程式名稱 (URI) 的應用程式健全狀況與篩選器，並透過指定的自訂原則[ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription)。

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

### <a name="powershell"></a>PowerShell
hello cmdlet tooget hello 應用程式健全狀況是[Get ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps)。 首先，使用 hello 連線 toohello 叢集[Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet。

hello 下列 cmdlet 會傳回 hello 健全狀況的 hello **fabric: / WordCount**應用程式：

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

下列 PowerShell 指令程式將自訂原則中的 hello。 它也會篩選子系和事件。

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

### <a name="rest"></a>REST
您可以取得與應用程式健全狀況[GET 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application)或[POST 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy)包含 hello 本文中所述的健全狀況原則。

## <a name="get-service-health"></a>取得服務健康情況
傳回 hello 健全狀況服務實體。 它包含 hello 資料分割健全狀況狀態。 輸入：

* [必要] hello 服務名稱 (URI)，識別 hello 服務。
* [選用] hello 應用程式健全狀況原則會使用 toooverride hello 應用程式資訊清單的原則。
* [選用]事件和指定感興趣的項目，且傳回 hello 結果 （例如，只，錯誤或警告和錯誤） 中的資料分割的篩選條件。 所有事件和資料分割都是使用的 tooevaluate hello 實體彙總健全狀況，不論 hello 篩選器。
* [選用]篩選 tooexclude 健全狀況統計資料。 如果未指定，確定 hello 健全狀況統計資料顯示 hello、 警告和錯誤的所有資料分割和複本 hello 服務的計數。

### <a name="api"></a>API
tooget 服務健全狀況 hello API，透過建立`FabricClient`和呼叫 hello [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync)其 HealthManager 上的方法。

hello 下列範例會取得具有指定的服務名稱 (URI) 的服務的 hello 健全狀況：

```charp
ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(serviceName);
```

hello 下列程式碼會取得 hello 服務健全狀況 hello 指定的服務名稱 (URI)，指定篩選器和自訂原則透過[ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):

```csharp
var queryDescription = new ServiceHealthQueryDescription(serviceName)
{
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.All },
    PartitionsFilter = new PartitionHealthStatesFilter() { HealthStateFilterValue = HealthStateFilter.Error },
};

ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
hello cmdlet tooget hello 服務健全狀況是[Get ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth)。 首先，使用 hello 連線 toohello 叢集[Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet。

hello 下列指令程式會使用預設的健全狀況原則取得 hello 服務健全狀況：

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

### <a name="rest"></a>REST
您可以取得服務健全狀況與[GET 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service)或[POST 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy)包含 hello 本文中所述的健全狀況原則。

## <a name="get-partition-health"></a>取得分割區健康情況
傳回的資料分割實體的 hello 健全狀況。 它包含 hello 複本健全狀況狀態。 輸入：

* [必要] hello 資料分割識別碼 (GUID)，識別 hello 資料分割。
* [選用] hello 應用程式健全狀況原則會使用 toooverride hello 應用程式資訊清單的原則。
* [選用]篩選條件的事件及指定感興趣的項目，且傳回 hello 結果 （例如，只，錯誤或警告和錯誤） 中的複本。 所有的事件和複本都是使用的 tooevaluate hello 實體彙總健全狀況，不論 hello 篩選器。
* [選用]篩選 tooexclude 健全狀況統計資料。 如果未指定，hello 健全狀況統計資料會顯示幾個複本處於 [確定]、 警告和錯誤狀態。

### <a name="api"></a>API
tooget 資料分割的健全狀況 hello API，透過建立`FabricClient`和呼叫 hello [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync)其 HealthManager 上的方法。 toospecify 選擇性參數，建立[PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription)。

```csharp
PartitionHealth partitionHealth = await fabricClient.HealthManager.GetPartitionHealthAsync(partitionId);
```

### <a name="powershell"></a>PowerShell
hello cmdlet tooget hello 資料分割健全狀況是[Get ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth)。 首先，使用 hello 連線 toohello 叢集[Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet。

hello 下列 cmdlet 會取得所有資料分割的 hello hello 健全狀況**fabric: / WordCount/WordCountService**服務也已經篩選掉複本健全狀況狀態：

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

### <a name="rest"></a>REST
您可以取得與資料分割健全狀況[GET 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition)或[POST 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy)包含 hello 本文中所述的健全狀況原則。

## <a name="get-replica-health"></a>取得複本健康情況
傳回 hello 的可設定狀態的服務複本或無狀態服務執行個體的健全狀況。 輸入：

* [必要] hello 資料分割識別碼 (GUID) 和複本識別碼，可識別 hello 複本。
* [選用] hello 應用程式健全狀況原則的參數使用 toooverride hello 應用程式資訊清單的原則。
* [選用]指定感興趣的項目，且傳回 hello 結果 （例如，只，錯誤或警告和錯誤） 中的事件篩選條件。 所有事件都都使用的 tooevaluate hello 實體彙總健全狀況，不論 hello 篩選器。

### <a name="api"></a>API
tooget hello 複本健全狀況 hello API，透過建立`FabricClient`和呼叫 hello [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync)其 HealthManager 上的方法。 進階參數，使用 toospecify [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription)。

```csharp
ReplicaHealth replicaHealth = await fabricClient.HealthManager.GetReplicaHealthAsync(partitionId, replicaId);
```

### <a name="powershell"></a>PowerShell
hello cmdlet tooget hello 複本健全狀況是[Get ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth)。 首先，使用 hello 連線 toohello 叢集[Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet。

hello 下列 cmdlet 會取得 hello hello hello 服務的所有資料分割的主要複本的健全狀況：

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

### <a name="rest"></a>REST
您可以取得複本健全狀況與[GET 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica)或[POST 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy)包含 hello 本文中所述的健全狀況原則。

## <a name="get-deployed-application-health"></a>取得已部署應用程式的健康情況
傳回 hello 部署在實體節點上的應用程式的健全狀況。 它包含部署的 hello 服務封裝健全狀況狀態。 輸入：

* [必要] hello 應用程式名稱 (URI) 和節點名稱 （字串），識別 hello 部署應用程式。
* [選用] hello 應用程式健全狀況原則會使用 toooverride hello 應用程式資訊清單的原則。
* [選用]事件和指定感興趣的項目，且傳回 hello 結果 （例如，只，錯誤或警告和錯誤） 中的已部署的服務封裝的篩選條件。 所有事件和部署的服務封裝都是使用的 tooevaluate hello 實體彙總健全狀況，不論 hello 篩選器。
* [選用]篩選 tooexclude 健全狀況統計資料。 如果未指定，hello 健全狀況統計資料會顯示 [確定]、 警告和錯誤健全狀況狀態的已部署的服務套件 hello 數目。

### <a name="api"></a>API
tooget hello 健全狀況的 hello API，透過在節點上部署的應用程式建立`FabricClient`和呼叫 hello [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync)其 HealthManager 上的方法。 toospecify 選擇性參數，請使用[DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription)。

```csharp
DeployedApplicationHealth health = await fabricClient.HealthManager.GetDeployedApplicationHealthAsync(
    new DeployedApplicationHealthQueryDescription(applicationName, nodeName));
```

### <a name="powershell"></a>PowerShell
hello cmdlet tooget hello 部署應用程式健全狀況是[Get ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps)。 首先，使用 hello 連線 toohello 叢集[Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet。 toofind 出應用程式的部署位置執行[Get ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps)並查看 hello 部署應用程式的子系。

hello 下列 cmdlet 會取得 hello 健全狀況的 hello **fabric: / WordCount**上部署的應用程式**_Node_2**。

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

### <a name="rest"></a>REST
您可以取得部署的應用程式健全狀況[GET 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application)或[POST 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy)包含 hello 本文中所述的健全狀況原則。

## <a name="get-deployed-service-package-health"></a>取得已部署服務封裝的健康情況
傳回 hello 已部署的服務套件實體健全的狀況。 輸入：

* [必要] hello 應用程式名稱 (URI)、 節點名稱 （字串） 和服務資訊清單的名稱 （字串），識別 hello 部署服務封裝。
* [選用] hello 應用程式健全狀況原則會使用 toooverride hello 應用程式資訊清單的原則。
* [選用]指定感興趣的項目，且傳回 hello 結果 （例如，只，錯誤或警告和錯誤） 中的事件篩選條件。 所有事件都都使用的 tooevaluate hello 實體彙總健全狀況，不論 hello 篩選器。

### <a name="api"></a>API
tooget hello hello API，透過已部署的服務封裝健全狀況建立`FabricClient`和呼叫 hello [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync)其 HealthManager 上的方法。 toospecify 選擇性參數，請使用[DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription)。

```csharp
DeployedServicePackageHealth health = await fabricClient.HealthManager.GetDeployedServicePackageHealthAsync(
    new DeployedServicePackageHealthQueryDescription(applicationName, nodeName, serviceManifestName));
```

### <a name="powershell"></a>PowerShell
hello cmdlet tooget hello 部署服務封裝健全狀況是[Get ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth)。 首先，使用 hello 連線 toohello 叢集[Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet。 執行應用程式部署所在的 toosee [Get ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps)並查看部署的 hello 應用程式。 服務封裝中的應用程式，查看在 hello toosee 部署服務封裝的子系在 hello [Get ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps)輸出。

hello 下列 cmdlet 會取得 hello 健全狀況的 hello **WordCountServicePkg**服務封裝的 hello **fabric: / WordCount**上部署的應用程式**_Node_2**。 hello 實體具有**System.Hosting**成功的服務封裝和項目點啟動，並註冊成功的服務類型的報表。

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

### <a name="rest"></a>REST
您可以取得已部署的服務封裝健全狀況與[GET 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package)或[POST 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy)包含 hello 本文中所述的健全狀況原則。

## <a name="health-chunk-queries"></a>健全狀況區塊查詢
hello 健全狀況區塊的查詢可以傳回多層級的叢集子系 （遞迴），每個輸入篩選器。 它支援進階的篩選器可讓很大的彈性選擇 hello 子系 toobe 傳回。 hello 篩選條件可以指定子系，hello 唯一識別碼或其他群組識別碼和/或健全狀況狀態。 根據預設，沒有子系是包含在內，但不要的 toohealth 命令永遠包含第一層子系。

hello[健康狀態查詢](service-fabric-view-entities-aggregated-health.md#health-queries)傳回的只是第一層子系的 hello 指定每個必要的篩選條件的實體。 tooget hello 子系的 hello 子系，您必須呼叫其他健全狀況 Api 針對每個感興趣的實體。 同樣地，tooget hello 健全狀況的特定實體，您必須呼叫一個健全狀況 API 所需的每個實體。 hello 區塊查詢進階篩選可讓您 toorequest hello 訊息大小和 hello 訊息數目降到最低的一個查詢中感興趣的多個項目。

hello 值 hello 區塊查詢的是，您可以在單一呼叫中的多個叢集實體 （潛在所有叢集實體開始必要的根） 取得健全狀況狀態。 您可以如下表示複雜的健全狀況查詢︰

* 只傳回發生錯誤的應用程式，以及針對這些應用程式，包含所有發生警告或錯誤的服務。 針對傳回的服務，包含所有分割。
* 傳回只有四個應用程式，其名稱所指定的 hello 健全狀況。
* 傳回只 hello 健全狀況所需的應用程式類型的應用程式。
* 傳回單一節點上所有已部署的實體。 傳回所有的應用程式、 hello 指定節點上已部署的所有應用程式和所有部署的 hello 服務封裝，該節點上。
* 傳回所有發生錯誤的複本。 傳回所有應用程式、服務、磁碟分割，以及只傳回發生錯誤的複本。
* 傳回所有應用程式。 針對指定的服務，包含所有分割。

目前，hello 健全狀況區塊查詢公開只 for hello 叢集實體。 它會傳回叢集健全狀況區塊，其中包含︰

* hello 叢集彙總健全狀況狀態。
* hello 健全狀況狀態區塊的節點清單尊重輸入篩選器。
* hello 健全狀況狀態的區塊清單尊重輸入篩選器的應用程式。 每個應用程式健全狀況狀態區塊尊重輸入篩選器和尊重 hello 篩選條件的所有已部署應用程式區塊清單的所有服務都包含區塊清單。 相同的 hello 的服務和已部署的應用程式的子系。 如此一來，hello 叢集中的所有實體可能會都傳回要求，以階層方式。

### <a name="cluster-health-chunk-query"></a>叢集健全狀況區塊查詢
會傳回 hello hello 叢集中實體的健全狀況，並包含必要的子系的 hello 階層的健全狀況狀態的區塊。 輸入：

* [選用] hello 叢集健全狀況原則會使用 tooevaluate hello 節點和 hello 叢集事件。
* [選用] hello 應用程式健全狀況原則對應 hello 健康原則使用 toooverride hello 應用程式資訊清單的原則。
* [選用]節點和指定感興趣的項目，且傳回 hello 結果中的應用程式的篩選條件。 hello 篩選特定 tooan 實體/群組的實體或適用 tooall 該層級的實體。 hello 篩選器清單可以包含一個一般篩選器和/或特定的識別項 toofine 資料粒度實體 hello 查詢所傳回的篩選。 如果是空的預設不會傳回 hello 子系。
  深入了解在 hello 篩選[NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter)和[ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter)。 hello 應用程式篩選器可遞迴指定進階的篩選器的子系。

hello 區塊結果包含尊重 hello 篩選的 hello 子系。

目前，hello 區塊查詢不會傳回處於狀況不良的評估或實體的事件。 可以使用現有叢集健全狀況查詢 hello 取得額外資訊。

### <a name="api"></a>API
tooget 叢集健全狀況區塊中，建立`FabricClient`和呼叫 hello [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync)方法上的其**HealthManager**。 您可以傳入[ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) toodescribe 健全狀況原則和進階篩選器。

hello 下列程式碼取得叢集健全狀況區塊與進階篩選器。

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

### <a name="powershell"></a>PowerShell
hello cmdlet tooget hello 叢集健全狀況是[Get ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk)。 首先，使用 hello 連線 toohello 叢集[Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet。

hello 下列程式碼會取得節點只有當它們位於除了特定的節點，一律會傳回錯誤。

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

hello 下列 cmdlet 會取得叢集區塊與應用程式篩選器。

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

hello 下列 cmdlet 會傳回已部署的所有實體節點上。

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

### <a name="rest"></a>REST
您可以取得叢集健全狀況區塊與[GET 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks)或[POST 要求](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster)內含健全狀況原則和 hello 本文所述的進階篩選器。

## <a name="general-queries"></a>一般查詢
一般查詢會傳回指定類型的 Service Fabric 實體清單。 這些元素會公開透過 hello 應用程式開發介面 (透過 hello 方法上**FabricClient.QueryManager**)、 PowerShell cmdlet 和 REST。 這些查詢會從多個元件彙總子查詢。 其中一個為 hello[健全狀況存放區](service-fabric-health-introduction.md#health-store)，其中會填入 hello 彙總的每個查詢結果的健全狀況狀態。  

> [!NOTE]
> 一般查詢傳回 hello 實體 hello 彙總健全狀況狀態，並且不包含豐富的健全狀況資料。 如果實體未正常運作，您可以追蹤健全狀況查詢 tooget 所有其健全狀況資訊，包括事件、 子健全狀況狀態和狀況不良的評估。
>
>

如果一般查詢會傳回實體的未知的健全狀況狀態，則可能該 hello 健全狀況存放區不會有完整的 hello 實體的資料。 此外，也可以為子查詢 toohello 健全狀況存放區未成功 （例如，發生通訊錯誤，或 hello 健全狀況存放區已節流處理）。 追蹤 hello 實體的健全狀況查詢。 如果 hello 子查詢發生暫時性錯誤，例如網路問題，此待處理的查詢可能會成功。 它也可以提供更多詳細資料從 hello health store 有關 hello 實體未公開的原因。

hello 包含查詢**HealthState**的實體包括：

* 節點清單： hello 叢集中 （分頁） 傳回 hello 清單節點。
  * API： [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)
  * PowerShell：Get-ServiceFabricNode
* 應用程式清單： 傳回 hello （分頁） hello 叢集中的應用程式清單。
  * API： [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)
  * PowerShell：Get-ServiceFabricApplication
* 服務清單: （分頁） 的應用程式中的服務傳回 hello 清單。
  * API： [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)
  * PowerShell：Get-ServiceFabricService
* 資料分割清單: （分頁） 服務中的資料分割傳回 hello 清單。
  * API： [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)
  * PowerShell：Get-ServiceFabricPartition
* 複本清單： 傳回 hello 份資料分割 （分頁） 中的複本。
  * API： [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)
  * PowerShell：Get-ServiceFabricReplica
* 部署應用程式清單： 傳回 hello 清單的節點上已部署的應用程式。
  * API： [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)
  * PowerShell：Get-ServiceFabricDeployedApplication
* 部署服務套件清單： 傳回 hello 服務中的封裝清單部署的應用程式。
  * API： [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)
  * PowerShell：Get-ServiceFabricDeployedApplication

> [!NOTE]
> 某些 hello 查詢傳回分頁的結果。 hello 傳回這些查詢是清單衍生自[PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1)。 如果 hello 結果未納入一則訊息，只會傳回頁並 ContinuationToken，可以追蹤列舉的停止處。 繼續 toocall hello 相同查詢，並傳入 hello 接續 token，從 hello 先前查詢 tooget 下一個結果。
>
>

### <a name="examples"></a>範例
hello 下列程式碼會取得 hello 狀況不良的應用程式中 hello 叢集：

```csharp
var applications = fabricClient.QueryManager.GetApplicationListAsync().Result.Where(
  app => app.HealthState == HealthState.Error);
```

hello 下列 cmdlet 會取得 hello hello 網狀架構的應用程式詳細資料: / WordCount 應用程式。 請注意，健康情況狀態為警告。

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

hello 下列 cmdlet 會取得 hello 服務健全狀況狀態，錯誤為：

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

## <a name="cluster-and-application-upgrades"></a>叢集和應用程式升級
監視在升級期間的 hello 叢集和應用程式，Service Fabric 會檢查所有項目維持良好健康情況 tooensure。 如果實體是使用 設定健全狀況原則評估為狀況不良，hello 升級適用於升級特定原則 toodetermine hello 下一個動作。 hello 升級可能會暫停的 tooallow 使用者互動 （例如修正錯誤條件或變更原則），或它可能會自動回復 toohello 良好舊版。

期間*叢集*升級，您可以取得 hello 叢集的升級狀態。 hello 升級狀態包括狀況不良的評估，哪一個點 toowhat 狀況不良 hello 叢集中。 如果 hello 升級回復 toohealth 問題到期，hello 升級狀態會記住 hello 上次狀況不良的原因。 這項資訊可協助系統管理員調查 hello 升級復原或停止之後發生錯誤的原因。

同樣地，在下列期間*應用程式*升級，任何處於狀況不良的評估中所包含 hello 應用程式升級狀態。

hello 下列範例示範 hello 應用程式升級狀態為已修改光纖: / WordCount 應用程式。 監視程式回報了它其中一個複本的錯誤。 hello 升級循環，因為未遵守 hello 健康情況檢查。

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

深入了解 hello [Service Fabric 應用程式升級](service-fabric-application-upgrade.md)。

## <a name="use-health-evaluations-tootroubleshoot"></a>使用健全狀況評估 tootroubleshoot
Hello 叢集或應用程式發生問題時，看看 hello 叢集或應用程式健全狀況 toopinpoint 錯誤。 hello 狀況不良的評估會提供有關哪些觸發的 hello 目前狀況不良狀態詳細資料。 如果需要您可以切入至狀況不良的子實體 tooidentify hello 根本原因。

例如，將應用程式視為健康情況不良，因為有其中一個複本的錯誤報告。 hello 下列 Powershell 指令程式會顯示 hello 狀況不良的評估：

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

您可以查看 hello 複本 tooget 的詳細資訊：

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
> hello 狀況不良的評估顯示 hello 第一個原因 hello 實體被評估 toocurrent 健全狀況狀態。 可能有多個觸發此狀態下，其他事件，但不是會反映在 hello 評估。 tooget 的詳細資訊，向下切入至 hello 健全狀況實體 toofigure hello 叢集中的 hello 處於不健全狀況報表。
>
>

## <a name="next-steps"></a>後續步驟
[使用系統健全狀況報表 tootroubleshoot](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[新增自訂 Service Fabric 健康狀態報告](service-fabric-report-health.md)

[Tooreport 並檢查服務健全狀況](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[在本機上監視及診斷服務](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Service Fabric 應用程式升級](service-fabric-application-upgrade.md)
