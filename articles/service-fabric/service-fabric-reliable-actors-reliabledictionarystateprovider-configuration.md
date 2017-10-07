---
title: "在 Azure microservices aaaChange ReliableDictionaryActorStateProvider 設定 |Microsoft 文件"
description: "了解設定 ReliableDictionaryActorStateProvider 類型的 Azure Service Fabric 可設定狀態的動作項目。"
services: Service-Fabric
documentationcenter: .net
author: sumukhs
manager: timlt
editor: 
ms.assetid: 79b48ffa-2474-4f1c-a857-3471f9590ded
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: sumukhs
ms.openlocfilehash: 44c85a41c90a17669ba874401d7921c94e7be9ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-reliable-actors--reliabledictionaryactorstateprovider"></a>設定 Reliable Actors - ReliableDictionaryActorStateProvider
您可以藉由變更產生 hello Visual Studio 封裝根目錄下 hello 指定執行者的 hello Config 資料夾中的 hello settings.xml 檔修改 ReliableDictionaryActorStateProvider hello 預設組態。

hello Azure Service Fabric 執行階段會尋找 hello settings.xml 檔案中的預先定義的區段名稱，並時都會佔用掉 hello 組態值建立 hello 基礎執行階段元件。

> [!NOTE]
> 請勿**不**刪除或修改的設定產生 hello Visual Studio 方案中的 hello settings.xml 檔案中的 hello hello 的區段名稱。
> 
> 

也有一些會影響 ReliableDictionaryActorStateProvider hello 組態的全域設定。

## <a name="global-configuration"></a>全域組態
hello hello KtlLogger 區段下的 hello 叢集的叢集資訊清單中指定 hello 全域組態。 它可讓 hello 共用記錄檔位置和大小加上 hello 全域記憶體限制 hello 記錄器所使用的設定。 請注意，hello 叢集資訊清單中的變更會影響所有的服務，使用 ReliableDictionaryActorStateProvider 和可靠的可設定狀態服務。

hello 叢集資訊清單是單一的 XML 檔案包含設定及套用 tooall 節點和 hello 叢集中的服務組態。 hello 檔案通常稱為 ClusterManifest.xml。 您可以看到您的叢集使用 hello Get ServiceFabricClusterManifest powershell 命令的 hello 叢集資訊清單。

### <a name="configuration-names"></a>組態名稱
| 名稱 | 單位 | 預設值 | 備註 |
| --- | --- | --- | --- |
| WriteBufferMemoryPoolMinimumInKB |KB |8388608 |最小數目為 hello 登入程式的核心模式中的 KB tooallocate 寫入緩衝區的記憶體集區。 此記憶體集區用來快取寫入 toodisk 之前的狀態資訊。 |
| WriteBufferMemoryPoolMaximumInKB |KB |沒有限制 |大小上限 toowhich hello 登入程式寫入緩衝區的記憶體集區可以成長。 |
| SharedLogId |GUID |"" |指定唯一的 GUID toouse 識別 hello 預設共用使用記錄檔及其服務的特定組態中未指定 hello SharedLogId hello 叢集中所有節點上所有可靠的服務。 如果有指定 SharedLogId，則也必須指定 SharedLogPath。 |
| SharedLogPath |完整路徑名稱 |"" |指定 hello hello 共用其服務的特定組態中未指定 hello SharedLogPath hello 叢集中所有節點上所有可靠的服務所使用的記錄檔所在的完整的路徑。 不過，如果有指定 SharedLogPath，則也必須指定 SharedLogId。 |
| SharedLogSizeInMB |MB |8192 |指定 hello 數 mb 的磁碟空間 toostatically 配置 hello 共用記錄。 hello 值必須是 2048年或更大。 |

### <a name="sample-cluster-manifest-section"></a>範例叢集資訊清單一節
```xml
   <Section Name="KtlLogger">
     <Parameter Name="WriteBufferMemoryPoolMinimumInKB" Value="8192" />
     <Parameter Name="WriteBufferMemoryPoolMaximumInKB" Value="8192" />
     <Parameter Name="SharedLogId" Value="{7668BB54-FE9C-48ed-81AC-FF89E60ED2EF}"/>
     <Parameter Name="SharedLogPath" Value="f:\SharedLog.Log"/>
     <Parameter Name="SharedLogSizeInMB" Value="16383"/>
   </Section>
```

### <a name="remarks"></a>備註
hello 記錄器已全域的集區，從可用 tooall 可靠的服務節點上的快取在寫入 toohello 專用的 hello 可靠的服務複本相關聯的記錄之前的狀態資料的未分頁的核心記憶體配置的記憶體。 hello 集區大小是由 hello WriteBufferMemoryPoolMinimumInKB 和 WriteBufferMemoryPoolMaximumInKB 設定控制。 WriteBufferMemoryPoolMinimumInKB 指定同時 hello 這個記憶體集區的初始大小和 hello 最低大小 toowhich hello 記憶體集區可能會縮小。 WriteBufferMemoryPoolMaximumInKB 是 hello 最大大小 toowhich hello 記憶體集區可能會成長。 開啟每個可靠的服務複本可能會依總 tooWriteBufferMemoryPoolMaximumInKB 系統決定量增加 hello hello 記憶體集區的大小。 如果沒有從 hello 記憶體集區超出可用的記憶體需求，有可用的記憶體為止，將會延遲記憶體的要求。 因此如果 hello 寫入緩衝區的記憶體集區太小的特定組態，然後可能會犧牲效能。

hello SharedLogId 和 SharedLogPath 設定為一律使用一起 toodefine hello GUID 和 hello 預設位置共用記錄檔中的 hello 叢集中所有節點。 hello 共用記錄檔用於可靠 hello 特定服務的 hello settings.xml 中未指定 hello 設定的所有服務。 為了達到最佳效能，共用的記錄檔應該置於只適用於共用 hello 記錄檔案 tooreduce 競爭的磁碟。

SharedLogSizeInMB 指定 hello 的磁碟空間 toopreallocate hello 共用記錄檔的所有節點上。  SharedLogId 和 SharedLogPath 不需要 toobe SharedLogSizeInMB toobe 指定的順序指定。

## <a name="replicator-security-configuration"></a>複寫器安全性組態
複寫器的安全性設定是在複寫期間所使用的 toosecure hello 通訊通道。 這表示服務無法看到彼此的複寫流量，確保 hello 資料，則高可用性也是安全。
依預設，空白的安全性組態區段會妨礙複寫安全性。

### <a name="section-name"></a>區段名稱
&lt;ActorName&gt;ServiceReplicatorSecurityConfig

## <a name="replicator-configuration"></a>複寫器組態
複寫器設定是使用的 tooconfigure hello 複寫器，其負責針對建立複寫，並將保存 hello 狀態儲存在本機高可靠 hello 動作項目狀態提供者狀態。
hello 預設設定由 hello Visual Studio 範本所產生，並應已足夠。 本節討論有關可用 tootune hello 複寫器的其他組態。

### <a name="section-name"></a>區段名稱
&lt;ActorName&gt;ServiceReplicatorConfig

### <a name="configuration-names"></a>組態名稱
| 名稱 | 單位 | 預設值 | 備註 |
| --- | --- | --- | --- |
| BatchAcknowledgementInterval |秒 |0.015 |一段時間的哪些 hello 複寫器在 hello 次要等候接收之前傳送回認可 toohello 主要的作業之後。 傳送作業在此時間間隔內處理的任何其他通知 toobe 會以一個回應傳送。 |
| ReplicatorEndpoint |N/A |無預設值--必要的參數 |IP 位址和連接埠 hello 主要/次要複寫器都會使用 toocommunicate，而其他購 hello 複本集中。 這應該參考 hello 服務資訊清單中的 TCP 資源端點。 請參閱太[服務資訊清單資源](service-fabric-service-manifest-resources.md)tooread 深入了解服務資訊清單中定義端點資源。 |
| MaxReplicationMessageSize |位元組 |50 MB |單一訊息可傳輸的複寫資料大小上限。 |
| MaxPrimaryReplicationQueueSize |作業數目 |8192 |Hello 主要佇列中的作業數目上限。 作業釋放 hello 主要複寫器接收到所有的 hello 次要購自之後。 此值必須大於 64 且為 2 的乘冪。 |
| MaxSecondaryReplicationQueueSize |作業數目 |16384 |Hello 次要佇列中的作業數目上限。 透過持續性讓狀態成為高可用性後，系統便會釋放作業。 此值必須大於 64 且為 2 的乘冪。 |
| CheckpointThresholdInMB |MB |200 |之後，便檢查點 hello 狀態的記錄檔空間量。 |
| MaxRecordSizeInKB |KB |1024 |Hello 複寫器的最大記錄大小可能會撰寫 hello 記錄檔中。 此值必須是 4 的倍數且大於 16。 |
| OptimizeLogForLowerDiskUsage |Boolean |true |若為 true，hello 記錄設定，這樣 hello 複本的專用的記錄檔由使用 NTFS 疏鬆檔案。 這可減少 hello 實際的磁碟空間使用量的 hello 檔案。 若為 false，會建立 hello 檔案具有固定配置，並提供 hello 最佳的寫入效能。 |
| SharedLogId |GUID |"" |指定識別 hello 與這個複本中使用共用的記錄檔的唯一 guid toouse。 服務通常不應使用此設定。 不過，如果有指定 SharedLogId，則也必須指定 SharedLogPath。 |
| SharedLogPath |完整路徑名稱 |"" |指定 hello 將在其中建立此複本 hello 共用的記錄檔的完整的路徑。 服務通常不應使用此設定。 不過，如果有指定 SharedLogPath，則也必須指定 SharedLogId。 |

## <a name="sample-configuration-file"></a>範例組態檔
```xml
<?xml version="1.0" encoding="utf-8"?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Section Name="MyActorServiceReplicatorConfig">
      <Parameter Name="ReplicatorEndpoint" Value="MyActorServiceReplicatorEndpoint" />
      <Parameter Name="BatchAcknowledgementInterval" Value="0.05"/>
      <Parameter Name="CheckpointThresholdInMB" Value="180" />
   </Section>
   <Section Name="MyActorServiceReplicatorSecurityConfig">
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

## <a name="remarks"></a>備註
hello BatchAcknowledgementInterval 參數控制複寫延遲。 值 '0' 會導致 hello 最低可能延遲，輸送量的 hello 成本 （如需收條訊息必須傳送和處理，每個包含較少的通知）。
hello BatchAcknowledgementInterval，hello 值越大 hello 較高的 hello 整體複寫輸送量，在 hello 成本較高的作業延遲。 這會直接轉譯 toohello 延遲的交易認可。

hello CheckpointThresholdInMB 參數控制項 hello 的磁碟空間量的 hello 複寫器可以在 hello 複本專用的記錄檔中使用 toostore 狀態資訊。 增加 hello 預設可能會導致新的複本加入 toohello 組時更快速的重新組態時間比此 tooa 較高值。 這是因為 toohello 部分狀態傳輸就會發生因為 toohello 可用性的 hello 記錄檔中的作業的詳細歷程記錄。 這可能會當機之後增加複本的 hello 復原時間。

如果您設定 OptimizeForLowerDiskUsage tootrue，記錄檔空間會過度佈建，讓作用中複本可以儲存詳細狀態資訊在其記錄檔，而非作用中複本則會使用較少的磁碟空間。 這使得可能 toohost 節點上的多個複本。 如果您設定 OptimizeForLowerDiskUsage toofalse，hello 狀態資訊就會更快速地寫入 toohello 記錄檔。

hello MaxRecordSizeInKB 設定可定義 hello hello 複寫器可以寫入 hello 記錄檔中記錄的大小上限。 在大部分情況下，hello 預設 1024 KB 記錄大小是最佳的。 不過，如果 hello 服務會造成較大資料的項目 toobe hello 狀態資訊的一部分，則此值可能需要增加 toobe。 沒有為較小的記錄使用只會 hello hello 較小的記錄所需的空間微乎其微 MaxRecordSizeInKB 小於 1024年的好處。 我們預期此值會需要 toobe 只在少數情況下變更。

hello SharedLogId 和 SharedLogPath 設定為一律使用一起 toomake hello 節點的服務使用個別的共用記錄從 hello 共用記錄檔。 為了最佳的效率，請儘可能與許多服務應該指定 hello 共用相同記錄檔。 共用的記錄檔應該放 hello 的共用記錄檔，而 tooreduce 頭移動量比較競爭只適用於在磁碟上。 我們預期會需要 toobe 只在少數情況下變更這些值。

