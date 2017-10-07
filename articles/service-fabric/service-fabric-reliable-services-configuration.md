---
title: "aaaConfigure 可靠 Azure microservices |Microsoft 文件"
description: "深入了解在 Azure Service Fabric 中設定具狀態的 Reliable Services。"
services: Service-Fabric
documentationcenter: .net
author: sumukhs
manager: timlt
editor: vturecek
ms.assetid: 9f72373d-31dd-41e3-8504-6e0320a11f0e
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: sumukhs
ms.openlocfilehash: 1e9c2890b62890a777561f25c04dc0fd11db9f1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-stateful-reliable-services"></a>設定具狀態可靠服務
有兩組組態設定可供 Reliable Services 使用。 Hello 其他集是特定 tooa 特定可靠的服務時，全域 hello 叢集中所有可靠的服務的一組。

## <a name="global-configuration"></a>全域組態
hello hello KtlLogger 區段下的 hello 叢集的叢集資訊清單中，已指定 hello 全域可靠的服務組態。 它可讓 hello 共用記錄檔位置和大小加上 hello 全域記憶體限制 hello 記錄器所使用的設定。 hello 叢集資訊清單是單一的 XML 檔案包含設定及套用 tooall 節點和 hello 叢集中的服務組態。 hello 檔案通常稱為 ClusterManifest.xml。 您可以看到您的叢集使用 hello Get ServiceFabricClusterManifest powershell 命令的 hello 叢集資訊清單。

### <a name="configuration-names"></a>組態名稱
| 名稱 | 單位 | 預設值 | 備註 |
| --- | --- | --- | --- |
| WriteBufferMemoryPoolMinimumInKB |KB |8388608 |最小數目為 hello 登入程式的核心模式中的 KB tooallocate 寫入緩衝區的記憶體集區。 此記憶體集區用來快取寫入 toodisk 之前的狀態資訊。 |
| WriteBufferMemoryPoolMaximumInKB |KB |沒有限制 |大小上限 toowhich hello 登入程式寫入緩衝區的記憶體集區可以成長。 |
| SharedLogId |GUID |"" |指定唯一的 GUID toouse 識別 hello 預設共用使用記錄檔及其服務的特定組態中未指定 hello SharedLogId hello 叢集中所有節點上所有可靠的服務。 如果有指定 SharedLogId，則也必須指定 SharedLogPath。 |
| SharedLogPath |完整路徑名稱 |"" |指定 hello hello 共用其服務的特定組態中未指定 hello SharedLogPath hello 叢集中所有節點上所有可靠的服務所使用的記錄檔所在的完整的路徑。 不過，如果有指定 SharedLogPath，則也必須指定 SharedLogId。 |
| SharedLogSizeInMB |MB |8192 |指定 hello 數 mb 的磁碟空間 toostatically 配置 hello 共用記錄。 hello 值必須是 2048年或更大。 |

在 Azure ARM 或內部部署的 JSON 範本，hello 下面範例會顯示如何 toochange hello hello 共用的交易記錄檔，取得會建立 tooback 可設定狀態服務的任何可靠的集合。

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="sample-local-developer-cluster-manifest-section"></a>範例本機開發人員叢集資訊清單區段
如果您想 toochange 這對本機開發環境，您會需要 tooedit hello 本機 clustermanifest.xml 檔案。

```xml
   <Section Name="KtlLogger">
     <Parameter Name="SharedLogSizeInMB" Value="4096"/>
     <Parameter Name="WriteBufferMemoryPoolMinimumInKB" Value="8192" />
     <Parameter Name="WriteBufferMemoryPoolMaximumInKB" Value="8192" />
     <Parameter Name="SharedLogId" Value="{7668BB54-FE9C-48ed-81AC-FF89E60ED2EF}"/>
     <Parameter Name="SharedLogPath" Value="f:\SharedLog.Log"/>
   </Section>
```

### <a name="remarks"></a>備註
hello 記錄器已全域的集區，從可用 tooall 可靠的服務節點上的快取在寫入 toohello 專用的 hello 可靠的服務複本相關聯的記錄之前的狀態資料的未分頁的核心記憶體配置的記憶體。 hello 集區大小是由 hello WriteBufferMemoryPoolMinimumInKB 和 WriteBufferMemoryPoolMaximumInKB 設定控制。 WriteBufferMemoryPoolMinimumInKB 指定同時 hello 這個記憶體集區的初始大小和 hello 最低大小 toowhich hello 記憶體集區可能會縮小。 WriteBufferMemoryPoolMaximumInKB 是 hello 最大大小 toowhich hello 記憶體集區可能會成長。 開啟每個可靠的服務複本可能會依總 tooWriteBufferMemoryPoolMaximumInKB 系統決定量增加 hello hello 記憶體集區的大小。 如果沒有從 hello 記憶體集區超出可用的記憶體需求，有可用的記憶體為止，將會延遲記憶體的要求。 因此如果 hello 寫入緩衝區的記憶體集區太小的特定組態，然後可能會犧牲效能。

hello SharedLogId 和 SharedLogPath 設定為一律使用一起 toodefine hello GUID 和 hello 預設位置共用記錄檔中的 hello 叢集中所有節點。 hello 共用記錄檔用於可靠 hello 特定服務的 hello settings.xml 中未指定 hello 設定的所有服務。 為了達到最佳效能，共用的記錄檔應該置於只適用於共用 hello 記錄檔案 tooreduce 競爭的磁碟。

SharedLogSizeInMB 指定 hello 的磁碟空間 toopreallocate hello 共用記錄檔的所有節點上。  SharedLogId 和 SharedLogPath 不需要 toobe SharedLogSizeInMB toobe 指定的順序指定。

## <a name="service-specific-configuration"></a>服務特定組態
您可以使用 hello 組態封裝 （組態） 來修改可設定狀態的可靠服務的預設組態或 hello 服務實作 （程式碼）。

* **Config** -透過 hello 設定封裝的組態藉由變更產生 hello Microsoft Visual Studio 封裝根目錄下 hello 應用程式中的每個服務的 hello Config 資料夾中的 hello Settings.xml 檔案達成。
* **程式碼**-透過程式碼的組態藉由建立 hello 適當的選項集搭配使用 ReliableStateManagerConfiguration 物件 ReliableStateManager 達成。

根據預設，hello Azure Service Fabric 執行階段會尋找 hello Settings.xml 檔案中的預先定義的區段名稱，而且時都會佔用掉 hello 組態值建立 hello 基礎執行階段元件。

> [!NOTE]
> 請勿**不**刪除的設定，除非您計劃 tooconfigure 您的服務，透過程式碼會產生 hello Visual Studio 方案中的 hello Settings.xml 檔案中的 hello hello 的區段名稱。
> 重新命名 hello 組態封裝或區段名稱設定 hello ReliableStateManager 時將需要變更程式碼。
> 
> 

### <a name="replicator-security-configuration"></a>複寫器安全性組態
複寫器的安全性設定是在複寫期間所使用的 toosecure hello 通訊通道。 這表示，服務將不會彼此的複寫流量，確保 hello 資料，則高可用性也安全的能 toosee。 依預設，空白的安全性組態區段會妨礙複寫安全性。

### <a name="default-section-name"></a>預設區段名稱
ReplicatorSecurityConfig

> [!NOTE]
> toochange 此區段的名稱，覆寫 hello replicatorSecuritySectionName 參數 toohello ReliableStateManagerConfiguration 建構函式建立此服務的 hello ReliableStateManager 時。
> 
> 

### <a name="replicator-configuration"></a>複寫器組態
複寫器的組態設定 hello 複寫器，其負責針對建立複寫，並將保存 hello 狀態儲存在本機高可靠 hello 可設定狀態 Reliable Service 的狀態。
hello 預設設定由 hello Visual Studio 範本所產生，並應已足夠。 本節討論有關可用 tootune hello 複寫器的其他組態。

### <a name="default-section-name"></a>預設區段名稱
ReplicatorConfig

> [!NOTE]
> toochange 此區段的名稱，覆寫 hello replicatorSettingsSectionName 參數 toohello ReliableStateManagerConfiguration 建構函式建立此服務的 hello ReliableStateManager 時。
> 
> 

### <a name="configuration-names"></a>組態名稱
| 名稱 | 單位 | 預設值 | 備註 |
| --- | --- | --- | --- |
| BatchAcknowledgementInterval |秒 |0.015 |一段時間的哪些 hello 複寫器在 hello 次要等候接收之前傳送回認可 toohello 主要的作業之後。 傳送作業在此時間間隔內處理的任何其他通知 toobe 會以一個回應傳送。 |
| ReplicatorEndpoint |N/A |無預設值--必要的參數 |IP 位址和連接埠 hello 主要/次要複寫器都會使用 toocommunicate，而其他購 hello 複本集中。 這應該參考 hello 服務資訊清單中的 TCP 資源端點。 請參閱太[服務資訊清單資源](service-fabric-service-manifest-resources.md)tooread 深入了解服務資訊清單中定義端點資源。 |
| MaxPrimaryReplicationQueueSize |作業數目 |8192 |Hello 主要佇列中的作業數目上限。 作業釋放 hello 主要複寫器接收到所有的 hello 次要購自之後。 此值必須大於 64 且為 2 的乘冪。 |
| MaxSecondaryReplicationQueueSize |作業數目 |16384 |Hello 次要佇列中的作業數目上限。 透過持續性讓狀態成為高可用性後，系統便會釋放作業。 此值必須大於 64 且為 2 的乘冪。 |
| CheckpointThresholdInMB |MB |50 |之後，便檢查點 hello 狀態的記錄檔空間量。 |
| MaxRecordSizeInKB |KB |1024 |Hello 複寫器的最大記錄大小可能會撰寫 hello 記錄檔中。 此值必須是 4 的倍數且大於 16。 |
| MinLogSizeInMB |MB |0 (系統判定) |Hello 交易記錄大小下限。 hello 記錄都不允許此設定下方 tootruncate tooa 大小。 0 表示該 hello 複寫器將會決定 hello 最小的記錄檔大小。 增加這個值會增加 hello 可能會進行部分複製和增量備份之後截斷降低相關的記錄檔記錄的機會。 |
| TruncationThresholdFactor |因素 |2 |決定在 hello 記錄檔的大小，將會觸發截斷。 截斷臨界值是以 MinLogSizeInMB 乘以 TruncationThresholdFactor 來決定。 TruncationThresholdFactor 必須大於 1。 MinLogSizeInMB 乘以 TruncationThresholdFactor 必須小於 MaxStreamSizeInMB。 |
| ThrottlingThresholdFactor |因素 |4 |決定在 hello 記錄檔的大小，hello 複本會開始進行節流處理。 節流閾值 (MB) 是以 Max((MinLogSizeInMB * ThrottlingThresholdFactor),(CheckpointThresholdInMB * ThrottlingThresholdFactor)) 來決定。 節流臨界值 (MB) 必須大於截斷臨界值 (MB)。 截斷臨界值 (MB) 必須小於 MaxStreamSizeInMB。 |
| MaxAccumulatedBackupLogSizeInMB |MB |800 |指定備份記錄鏈中備份記錄檔的最大累積大小 (MB)。 累加式的備份要求 hello 增量備份仍會產生自 hello 相關完整備份 toobe 大於此大小導致累積的 hello 備份記錄檔備份記錄檔將會失敗。 在這種情況下，使用者會是需要的 tootake 完整備份。 |
| SharedLogId |GUID |"" |指定唯一的 GUID toouse 識別 hello 與這個複本中使用共用的記錄檔。 服務通常不應使用此設定。 不過，如果有指定 SharedLogId，則也必須指定 SharedLogPath。 |
| SharedLogPath |完整路徑名稱 |"" |指定 hello 將在其中建立此複本 hello 共用的記錄檔的完整的路徑。 服務通常不應使用此設定。 不過，如果有指定 SharedLogPath，則也必須指定 SharedLogId。 |
| SlowApiMonitoringDuration |秒 |300 |設定 hello 監視受管理的 API 呼叫的間隔。 範例︰使用者提供的備份回呼函式。 Hello 間隔時間經過之後，警告健全狀況報表將會傳送 toohello 健全狀況管理員。 |

### <a name="sample-configuration-via-code"></a>透過程式碼的範例組態
```csharp
class Program
{
    /// <summary>
    /// This is hello entry point of hello service host process.
    /// </summary>
    static void Main()
    {
        ServiceRuntime.RegisterServiceAsync("HelloWorldStatefulType",
            context => new HelloWorldStateful(context, 
                new ReliableStateManager(context, 
        new ReliableStateManagerConfiguration(
                        new ReliableStateManagerReplicatorSettings()
            {
                RetryInterval = TimeSpan.FromSeconds(3)
                        }
            )))).GetAwaiter().GetResult();
    }
}    
```
```csharp
class MyStatefulService : StatefulService
{
    public MyStatefulService(StatefulServiceContext context, IReliableStateManagerReplica stateManager)
        : base(context, stateManager)
    { }
    ...
}
```


### <a name="sample-configuration-file"></a>範例組態檔
```xml
<?xml version="1.0" encoding="utf-8"?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Section Name="ReplicatorConfig">
      <Parameter Name="ReplicatorEndpoint" Value="ReplicatorEndpoint" />
      <Parameter Name="BatchAcknowledgementInterval" Value="0.05"/>
      <Parameter Name="CheckpointThresholdInMB" Value="512" />
   </Section>
   <Section Name="ReplicatorSecurityConfig">
      <Parameter Name="CredentialType" Value="X509" />
      <Parameter Name="FindType" Value="FindByThumbprint" />
      <Parameter Name="FindValue" Value="9d c9 06 b1 69 dc 4f af fd 16 97 ac 78 1e 80 67 90 74 9d 2f" />
      <Parameter Name="StoreLocation" Value="LocalMachine" />
      <Parameter Name="StoreName" Value="My" />
      <Parameter Name="ProtectionLevel" Value="EncryptAndSign" />
      <Parameter Name="AllowedCommonNames" Value="My-Test-SAN1-Alice,My-Test-SAN1-Bob" />
   </Section>
</Settings>
```


### <a name="remarks"></a>備註
BatchAcknowledgementInterval 會控制複寫延遲性。 值 '0' 會導致 hello 最低可能延遲，輸送量的 hello 成本 （如需收條訊息必須傳送和處理，每個包含較少的通知）。
hello BatchAcknowledgementInterval，hello 值越大 hello 較高的 hello 整體複寫輸送量，在 hello 成本較高的作業延遲。 這會直接轉譯 toohello 延遲的交易認可。

hello CheckpointThresholdInMB 控制項 hello hello 複寫器的磁碟空間量值可以在 hello 複本專用的記錄檔中使用 toostore 狀態資訊。 增加 hello 預設可能會導致新的複本加入 toohello 組時更快速的重新組態時間比此 tooa 較高值。 這是因為 toohello 部分狀態傳輸就會發生因為 toohello 可用性的 hello 記錄檔中的作業的詳細歷程記錄。 這可能會當機之後增加複本的 hello 復原時間。

hello MaxRecordSizeInKB 設定可定義 hello hello 複寫器可以寫入 hello 記錄檔中記錄的大小上限。 在大部分情況下，hello 預設 1024 KB 記錄大小是最佳的。 不過，如果 hello 服務會造成較大資料的項目 toobe hello 狀態資訊的一部分，則此值可能需要增加 toobe。 沒有為較小的記錄使用只會 hello hello 較小的記錄所需的空間微乎其微 MaxRecordSizeInKB 小於 1024年的好處。 我們預期此值會需要 toobe 中只有少數的情況下變更。

hello SharedLogId 和 SharedLogPath 設定為一律使用一起 toomake hello 節點的服務使用個別的共用記錄從 hello 共用記錄檔。 為了最佳的效率，請儘可能與許多服務應該指定 hello 共用相同記錄檔。 共用的記錄檔應該放只適用於共用 hello 記錄檔案 tooreduce 頭移動量比較競爭的磁碟上。 我們預期此值會需要 toobe 中只有少數的情況下變更。

## <a name="next-steps"></a>後續步驟
* [在 Visual Studio 中偵錯 Service Fabric 應用程式](service-fabric-debugging-your-application.md)
* [可靠的服務的開發人員參考資料](https://msdn.microsoft.com/library/azure/dn706529.aspx)

