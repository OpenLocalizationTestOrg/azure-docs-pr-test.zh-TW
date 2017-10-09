---
title: "aaaChange Azure Service Fabric 叢集設定 |Microsoft 文件"
description: "本文說明 hello 網狀架構設定和 hello fabric 升級原則，您可以自訂。"
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: 
ms.assetid: 7ced36bf-bd3f-474f-a03a-6ebdbc9677e2
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: chackdan
ms.openlocfilehash: a8b125f7b4a02547cf4bcf2c936d0c7f1686c1a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="customize-service-fabric-cluster-settings-and-fabric-upgrade-policy"></a>自訂 Service Fabric 叢集設定和網狀架構升級原則
這份文件會告訴您如何 toocustomize hello 各種網狀架構設定和 Service Fabric 叢集的 hello fabric 升級原則。 您可以自訂它們在 hello 入口網站或使用 Azure Resource Manager 範本。

> [!NOTE]
> 並非所有的設定可透過 hello 入口網站。 下面所列的設定不是可透過 hello 入口網站使用自訂 Azure Resource Manager 範本。
> 

## <a name="customizing-service-fabric-cluster-settings-using-azure-resource-manager-templates"></a>使用 Azure Resource Manager 範本自訂 Service Fabric 叢集設定
hello 執行下列步驟說明如何 tooadd 新設定*MaxDiskQuotaInMB* toohello*診斷*> 一節。

1. 移 toohttps://resources.azure.com
2. 展開瀏覽 tooyour 訂用帳戶的訂閱]-> [的資源群組]-> [Microsoft.ServiceFabric]-> [您的叢集名稱
3. 在 hello 右上角，選取 「 讀取/寫入 」
4. 選取 [編輯]，並更新 hello `fabricSettings` JSON 元素並加入新項目

```
      {
        "name": "Diagnostics",
        "parameters": [
          {
            "name": "MaxDiskQuotaInMB",
            "value": "65536"
          }
        ]
      }
```

## <a name="fabric-settings-that-you-can-customize"></a>您可以自訂的網狀架構設定
以下是您可以自訂的 hello 網狀架構設定：

### <a name="section-name-diagnostics"></a>區段名稱：Diagnostics
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| ConsumerInstances |String |hello DCA 取用者執行個體清單。 |
| ProducerInstances |String |hello DCA 產生者執行個體清單。 |
| AppEtwTraceDeletionAgeInDays |整數，預設值為 3 |天數，在此時間過後便會刪除含有應用程式 ETW 追蹤的舊有 ETL 檔案。 |
| AppDiagnosticStoreAccessRequiresImpersonation |布林值，預設值為 true |不論模擬時，需要存取診斷儲存代表 hello 應用程式。 |
| MaxDiskQuotaInMB |整數，預設值為 65536 |Windows Fabric 記錄檔的磁碟配額 (MB)。 |
| DiskFullSafetySpaceInMB |整數，預設值為 1024 |剩餘的磁碟空間 MB tooprotect 從 DCA 使用中。 |
| ApplicationLogsFormatVersion |整數，預設值為 0 |應用程式記錄格式的版本。 支援的值為 0 和 1。 第 1 版包含從 hello ETW 事件記錄比 0 版本的多個欄位。 |
| ClusterId |String |hello 的 hello 叢集的唯一識別碼。 這會產生建立 hello 叢集時。 |
| EnableTelemetry |布林值，預設值為 true |這將要 tooenable，或停用遙測。 |
| EnableCircularTraceSession |布林值，預設值為 false |旗標會指出是否應使用循環追蹤工作階段。 |

### <a name="section-name-traceetw"></a>區段名稱︰Trace/Etw
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| Level |整數，預設值為 4 |追蹤 etw 層級可以接受值 1、2、3、4。 支援的 toobe 您必須保持 4 hello 追蹤層級 |

### <a name="section-name-performancecounterlocalstore"></a>區段名稱︰PerformanceCounterLocalStore
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| IsEnabled |布林值，預設值為 true |旗標會指出是否啟用本機節點的效能計數器收集。 |
| SamplingIntervalInSeconds |整數，預設值為 60 |所要收集之效能計數器的取樣間隔。 |
| Counters |String |效能計數器 toocollect 的逗號分隔清單。 |
| MaxCounterBinaryFileSizeInMB |整數，預設值為 1 |每個效能計數器之二進位檔案的大小上限 (MB)。 |
| NewCounterBinaryFileCreationIntervalInMinutes |整數，預設值為 10 |間隔上限 (秒)，在此時間過後便會建立新的效能計數器二進位檔案。 |

### <a name="section-name-setup"></a>區段名稱︰Setup
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| FabricDataRoot |string |Service Fabric 資料的根目錄。 預設為 Azure d:\svcfab |
| FabricLogRoot |string |Service Fabric 記錄的根目錄。 這是放置 SF 記錄和追蹤的位置。 |
| ServiceRunAsAccountName |String |hello 下方的 toorun fabric 主機服務的帳戶名稱。 |
| ServiceStartupType |String |hello hello fabric 主機服務的啟動類型。 |
| SkipFirewallConfiguration |布林值，預設值為 false |指定是否需要 toobe 防火牆設定或不下設 hello 系統。 這只有當您使用 Windows 防火牆時才適用。 如果您使用協力廠商防火牆，然後您必須開啟 hello 系統與應用程式 toouse hello 連接埠 |

### <a name="section-name-transactionalreplicator"></a>區段名稱︰TransactionalReplicator
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| MaxCopyQueueSize |單位，預設值為 16384 |這是 hello 最大值定義 hello hello 佇列由複寫作業所維護的初始大小。 請注意，此值必須是 2 的乘冪。 如果在執行階段 hello 佇列成長 toothis 大小作業將會 hello 主要和次要複寫程式之間進行節流處理。 |
| BatchAcknowledgementInterval | 時間 (秒)，預設值為 0.015 | 以秒為單位指定時間範圍。 決定 hello hello 接收操作，才能傳回通知後的複寫器等候的時間量。 在此期間內收到其他作業將會有]-> [減少網路流量，但可能降低 hello 輸送量 hello 複寫器的單一訊息中傳回其通知。 |
| MaxReplicationMessageSize |單位，預設值為 52428800 | 複寫作業的訊息大小上限。 預設值為 50 MB。 |
| ReplicatorAddress |字串，預設值為 "localhost:0" | hello 形式的字串-'IP:Port' hello Windows Fabric 複寫器 tooestablish 連線順序 toosend/接收作業中的其他複本所使用的端點。 |
| InitialPrimaryReplicationQueueSize |單位，預設值為 64 | 此值會定義 hello hello 佇列以維護主要 hello hello 複寫作業的初始大小。 請注意，此值必須是 2 的乘冪。|
| MaxPrimaryReplicationQueueSize |單位，預設值為 8192 |這是 hello hello 主要複寫佇列中可能存在的作業數目上限。 請注意，此值必須是 2 的乘冪。 |
| MaxPrimaryReplicationQueueMemorySize |單位，預設值為 0 |這是 hello hello 主要複寫佇列，以位元組為單位的最大的值。 |
| InitialSecondaryReplicationQueueSize |單位，預設值為 64 |這個值會定義 hello 的 hello 佇列中維護次要 hello hello 複寫作業的初始大小。 請注意，此值必須是 2 的乘冪。 |
| MaxSecondaryReplicationQueueSize |單位，預設值為 16384 |這是 hello hello 次要複寫佇列中可能存在的作業數目上限。 請注意，此值必須是 2 的乘冪。 |
| MaxSecondaryReplicationQueueMemorySize |單位，預設值為 0 |這是 hello hello 次要複寫佇列，以位元組為單位的最大的值。 |
| SecondaryClearAcknowledgedOperations |布林值，預設值為 false |Bool 控制是否 hello hello 次要複寫器的作業會清除它們會認可 toohello 主要 （排清的 toohello 磁碟）。 此 tooTRUE 可能會導致 hello 新主要複本時容錯移轉之後趕上複本額外的磁碟讀取的設定。 |
| MaxMetadataSizeInKB |整數，預設值為 4 |Hello 記錄資料流中繼資料的大小上限。 |
| MaxRecordSizeInKB |單位，預設值為 1024 | 記錄資料流記錄的大小上限。 |
| CheckpointThresholdInMB |整數，預設值為 50 |當 hello 記錄檔使用量超過此值時，將會起始檢查點。 |
| MaxAccumulatedBackupLogSizeInMB |整數，預設值為 800 |指定備份記錄鏈中備份記錄檔的最大累積大小 (MB)。 累加式的備份要求 hello 增量備份仍會產生自 hello 相關完整備份 toobe 大於此大小導致累積的 hello 備份記錄檔備份記錄檔將會失敗。 在這種情況下，使用者會是需要的 tootake 完整備份。 |
| MaxWriteQueueDepthInKB |整數，預設值為 0 | 最大值 Int 寫入佇列深度該 hello 核心記錄器可作為以 kb 為單位指定與這個複本有關聯的 hello 記錄檔。 此值為 hello 的核心記錄器更新期間可能未處理的位元組數目上限。 針對 hello 核心記錄器 toocompute，適當的值或 4 的倍數，則可能為 0。 |
| SharedLogId |String |共用記錄識別碼。 此參數是 GUID，每個共用記錄的這個參數都應該是唯一的。 |
| SharedLogPath |String |路徑 toohello 共用記錄檔。 如果此值為空白則會使用 hello 共用記錄檔。 |
| SlowApiMonitoringDuration |時間 (秒)，預設值為 300 | 指定 API 的持續時間，在此時間過後便會引發警告健康狀態事件。|
| MinLogSizeInMB |整數，預設值為 0 |Hello 交易記錄大小下限。 hello 記錄都不允許此設定下方 tootruncate tooa 大小。 0 表示該 hello 複寫器將會決定根據 tooother 設定 hello 最小的記錄檔大小。 增加這個值會增加 hello 可能會進行部分複製和增量備份之後截斷降低相關的記錄檔記錄的機會。 |

### <a name="section-name-fabricclient"></a>區段名稱︰FabricClient
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| NodeAddresses |字串，預設值為 "" |可以是使用的 toocommunicate 以 hello hello 命名服務的不同節點上的位址 （連接字串） 的集合。 一開始 hello 隨機選取其中一個 hello 位址的用戶端連線。 如果提供一個以上的連接字串，而連線失敗，因為發生通訊或逾時錯誤。hello 用戶端會切換 toouse hello 下一個位址循序。 重試語意，請參閱 hello 命名服務位址重試 > 章節，如需詳細資訊。 |
| ConnectionInitializationTimeout |時間 (秒)，預設值為 2 |以秒為單位指定時間範圍。 每次用戶端的連線逾時間隔會嘗試 tooopen 連接 toohello 閘道。 |
| PartitionLocationCacheLimit |整數，預設值為 100000 |針對 service 解析快取的資料分割數目 （設定 too0 代表無限制）。 |
| ServiceChangePollInterval |時間 (秒)，預設值為 120 |以秒為單位指定時間範圍。 從已註冊的服務變更通知回呼的 hello 用戶端 toohello 閘道變更 hello 連續輪詢服務之間的間隔。 |
| KeepAliveIntervalInSeconds |整數，預設值為 20 |hello 間隔在哪一個 hello FabricClient 傳輸傳送保持運作訊息 toohello 閘道。 若為 0，keepAlive 會停用。 必須是正值。 |
| HealthOperationTimeout |時間 (秒)，預設值為 120 |以秒為單位指定時間範圍。 hello 報告訊息等候傳送 tooHealth 管理員。 |
| HealthReportSendInterval |時間 (秒)，預設值為 30 |以秒為單位指定時間範圍。 hello 間隔在哪一個報表的元件傳送累積健全狀況報告 tooHealth 管理員。 |
| HealthReportRetrySendInterval |時間 (秒)，預設值為 30 |以秒為單位指定時間範圍。 hello 間隔在哪一個報表的元件重新傳送的累積健全狀況報告 tooHealth 管理員。 |
| RetryBackoffInterval |時間 (秒)，預設值為 3 |以秒為單位指定時間範圍。 hello 撤退間隔後再重試 hello 作業。 |
| MaxFileSenderThreads |單位，預設值為 10 |hello 的檔案，以平行方式傳送的最大數目。 |

### <a name="section-name-common"></a>區段名稱︰Common
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| PerfMonitorInterval |時間 (秒)，預設值為 1 |以秒為單位指定時間範圍。 效能監視間隔。 設定 too0 或負數值停用監視。 |

### <a name="section-name-healthmanager"></a>區段名稱︰HealthManager
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| EnableApplicationTypeHealthEvaluation |布林值，預設值為 false |叢集健康狀態評估原則︰啟用每一應用程式類型的健康狀態評估。 |

### <a name="section-name-fabricnode"></a>區段名稱︰FabricNode
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| StateTraceInterval |時間 (秒)，預設值為 300 |以秒為單位指定時間範圍。 用於追蹤每個節點上，並在 FM/FMM 上的節點上的節點狀態的 hello 間隔。 |

### <a name="section-name-nodedomainids"></a>區段名稱︰NodeDomainIds
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| UpgradeDomainId |字串，預設值為 "" |描述 hello 節點所屬的升級網域。 |
| PropertyGroup |NodeFaultDomainIdCollection |描述的節點屬於 hello 容錯網域。 透過描述 hello hello hello 資料中心內的節點位置的 URI 定義 hello 容錯網域。  容錯網域 Uri 是 hello 的格式化 fd: / fd/後面接著在 URI 路徑片段。|

### <a name="section-name-nodeproperties"></a>區段名稱︰NodeProperties
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| PropertyGroup |NodePropertyCollectionMap |節點屬性的字串索引鍵/值組集合。 |

### <a name="section-name-nodecapacities"></a>區段名稱︰NodeCapacities
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| PropertyGroup |NodeCapacityCollectionMap |不同計量的節點容量集合。 |

### <a name="section-name-fabricnode"></a>區段名稱︰FabricNode
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| StartApplicationPortRange |整數，預設值為 0 |受裝載子系統 hello 應用程式連接埠的開頭。 若主控內的 EndpointFilteringEnabled 為 true，則需要此參數。 |
| EndApplicationPortRange |整數，預設值為 0 |（不含） 結尾的受主控子系統 hello 應用程式連接埠。 若主控內的 EndpointFilteringEnabled 為 true，則需要此參數。 |
| ClusterX509StoreName |字串，預設值為 "My" |包含用來保護叢集間通訊之叢集憑證的 X.509 憑證存放區名稱。 |
| ClusterX509FindType |字串，預設值為 "FindByThumbprint" |指出如何 toosearch hello 存放區中的叢集憑證指定 ClusterX509StoreName 支援的值:"FindByThumbprint";「 FindBySubjectName 」 與 「 FindBySubjectName";當有多個相符項目。會使用其中一個 hello 最遠到期 hello。 |
| ClusterX509FindValue |字串，預設值為 "" |搜尋篩選器值使用 toolocate 叢集憑證。 |
| ClusterX509FindValueSecondary |字串，預設值為 "" |搜尋篩選器值使用 toolocate 叢集憑證。 |
| ServerAuthX509StoreName |字串，預設值為 "My" |包含入場服務之伺服器憑證的 X.509 憑證存放區名稱。 |
| ServerAuthX509FindType |字串，預設值為 "FindByThumbprint" |指出 hello 存放區中的伺服器憑證的 toosearch ServerAuthX509StoreName 支援值所指定的方式： FindByThumbprint;FindBySubjectName。 |
| ServerAuthX509FindValue |字串，預設值為 "" |搜尋篩選器值使用 toolocate 伺服器憑證。 |
| ServerAuthX509FindValueSecondary |字串，預設值為 "" |搜尋篩選器值使用 toolocate 伺服器憑證。 |
| ClientAuthX509StoreName |字串，預設值為 "My" |Hello X.509 憑證存放區名稱包含預設系統管理員角色 FabricClient 的憑證。 |
| ClientAuthX509FindType |字串，預設值為 "FindByThumbprint" |指出 hello 存放區中憑證的 toosearch ClientAuthX509StoreName 支援值所指定的方式： FindByThumbprint;FindBySubjectName。 |
| ClientAuthX509FindValue |字串，預設值為 "" | 使用預設系統管理員角色 FabricClient toolocate 憑證搜尋篩選值。 |
| ClientAuthX509FindValueSecondary |字串，預設值為 "" |使用預設系統管理員角色 FabricClient toolocate 憑證搜尋篩選值。 |
| UserRoleClientX509StoreName |字串，預設值為 "My" |Hello X.509 憑證存放區名稱包含預設使用者角色 FabricClient 的憑證。 |
| UserRoleClientX509FindType |字串，預設值為 "FindByThumbprint" |指出 hello 存放區中憑證的 toosearch UserRoleClientX509StoreName 支援值所指定的方式： FindByThumbprint;FindBySubjectName。 |
| UserRoleClientX509FindValue |字串，預設值為 "" |使用預設使用者角色 FabricClient toolocate 憑證搜尋篩選值。 |
| UserRoleClientX509FindValueSecondary |字串，預設值為 "" |使用預設使用者角色 FabricClient toolocate 憑證搜尋篩選值。 |

### <a name="section-name-paas"></a>區段名稱：Paas
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| ClusterId |字串，預設值為 "" |網狀架構用來保護組態的 X509 憑證存放區。 |

### <a name="section-name-fabrichost"></a>區段名稱︰FabricHost
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| StopTimeout |時間 (秒)，預設值為 300 |以秒為單位指定時間範圍。 hello 託管的服務啟用; 逾時停用和升級。 |
| StartTimeout |時間 (秒)，預設值為 300 |以秒為單位指定時間範圍。 fabricactivationmanager 的啟動逾時。 |
| ActivationRetryBackoffInterval |時間 (秒)，預設值為 5 |以秒為單位指定時間範圍。 輪詢間隔失敗 hello 系統上的每個啟用失敗; 每個連續的啟用會重試總 toohello MaxActivationFailureCount 的 hello 啟用。 hello 每一次嘗試的重試間隔是持續啟用失敗，以及 hello 啟用撤退間隔的產品。 |
| ActivationMaxRetryInterval |時間 (秒)，預設值為 300 |以秒為單位指定時間範圍。 啟用的重試間隔上限。 在每個連續失敗 hello 重試間隔計算為最小值 (ActivationMaxRetryInterval;連續失敗次數 * ActivationRetryBackoffInterval)。 |
| ActivationMaxFailureCount |整數，預設值為 10 |這是 hello 計數上限，系統會重試失敗的啟用後才放棄。 |
| EnableServiceFabricAutomaticUpdates |布林值，預設值為 false |這是透過 Windows Update tooenable 網狀架構自動更新。 |
| EnableServiceFabricBaseUpgrade |布林值，預設值為 false |這是 tooenable 基底伺服器更新。 |
| EnableRestartManagement |布林值，預設值為 false |這是 tooenable 伺服器重新啟動。 |


### <a name="section-name-failovermanager"></a>區段名稱︰FailoverManager
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| UserReplicaRestartWaitDuration |時間 (秒)，預設值為 60.0 * 30 |以秒為單位指定時間範圍。 保存的複本時效能降低。Windows Fabric 等待這段期間的 hello 複本 toocome 備份建立新的取代複本 （這需要 hello 狀態的複本） 之前。 |
| QuorumLossWaitDuration |時間 (秒)，預設值為 MaxValue |以秒為單位指定時間範圍。 這是我們允許在遺失仲裁的狀態資料分割 toobe hello 最大持續時間。 如果 hello 分割區仍在遺失仲裁之後這個持續時間。hello 資料分割會從仲裁遺失復原考慮過 hello 下為遺失的複本。 請注意，這可能會造成資料遺失。 |
| UserStandByReplicaKeepDuration |時間 (秒)，預設值為 3600.0 * 24 * 7 |以秒為單位指定時間範圍。 當保存的複本從停止運作狀態恢復過來，它可能已被取代。 這個計時器會決定多久 hello FM 會保留 hello 待命的複本，然後再將它捨棄。 |
| UserMaxStandByReplicaCount |整數，預設值為 1 |hello 預設最大數目的 hello 系統的 StandBy 複本保持使用者的服務。 |

### <a name="section-name-namingservice"></a>區段名稱︰NamingService
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| TargetReplicaSetSize |整數，預設值為 7 |hello 命名服務存放區的每個資料分割設定 hello 複本數目。 增加複本集增加 hello 層級的 hello 命名服務存放區; 中的 hello 資訊的可靠性的 hello 數目減少 hello 資訊的 hello 變更將會遺失節點失敗; 因為Windows Fabric 和 hello 一段時間的負載增加的成本花費 tooperform 更新 toohello 命名的資料。|
|MinReplicaSetSize | 整數，預設值為 3 | hello 命名服務複本的最小的數目所需 toowrite toocomplete 更新。 如果有較少的複本比這個 hello 系統 hello 可靠性系統中的作用中複本還原之前，就會拒絕更新 toohello 命名服務存放區。 這個值應該不會超過 hello TargetReplicaSetSize。 |
|ReplicaRestartWaitDuration | 時間 (秒)，預設值為 (60.0 * 30)| 以秒為單位指定時間範圍。 當命名服務複本停止運作時，此計時器就會啟動。  Hello FM 過期時，就會開始 tooreplace hello 複本，也就是關閉 （不會還視為它們遺失）。 |
|QuorumLossWaitDuration | 時間 (秒)，預設值為 MaxValue | 以秒為單位指定時間範圍。 當命名服務進入仲裁遺失狀態時，此計時器就會啟動。  Hello FM 過期時，會考慮 hello 下為遺失; 的複本然後嘗試 toorecover 仲裁。 請注意，這可能會導致資料遺失。 |
|StandByReplicaKeepDuration | 時間 (秒)，預設值為 3600.0 * 2 | 以秒為單位指定時間範圍。 當命名服務複本從停止運作狀態恢復過來，它可能已被取代。  這個計時器會決定多久 hello FM 會保留 hello 待命的複本，然後再將它捨棄。 |
|PlacementConstraints | 字串，預設值為 "" | 位置條件約束的 hello 命名服務。 |
|ServiceDescriptionCacheLimit | 整數，預設值為 0 | hello 維護 hello LRU 服務描述級快取中的項目數目上限 hello 命名 Store 服務 （設定 too0 代表無限制）。 |
|RepairInterval | 時間 (秒)，預設值為 5 | 以秒為單位指定時間範圍。 中的 hello 命名 hello 授權擁有者和名稱的擁有者之間的不一致修復會開始的間隔。 |
|MaxNamingServiceHealthReports | 整數，預設值為 10 | hello 緩慢命名存放區的作業數目上限會一次服務狀況不良的報表。 若為 0，則會傳送所有緩慢作業。 |
| MaxMessageSize |整數，預設值為 4*1024*1024 |hello 訊息大小上限為用戶端節點通訊時使用命名的。 DOS 攻擊減輕，預設值為 4MB。 |
| MaxFileOperationTimeout |時間 (秒)，預設值為 30 |以秒為單位指定時間範圍。 允許檔案存放區的服務作業 hello 最大逾時。 指定較大逾時值的要求會遭到拒絕。 |
| MaxOperationTimeout |時間 (秒)，預設值為 600 |以秒為單位指定時間範圍。 允許用戶端作業 hello 最大逾時。 指定較大逾時值的要求會遭到拒絕。 |
| MaxClientConnections |整數，預設值為 1000 |hello 最多允許每個閘道的用戶端連線的數目。 |
| ServiceNotificationTimeout |時間 (秒)，預設值為 30 |以秒為單位指定時間範圍。 使用傳遞服務通知 toohello 用戶端時的 hello 逾時。 |
| MaxOutstandingNotificationsPerClient |整數，預設值為 1000 |hello 閘道已強制關閉 hello 的用戶端註冊之前未完成的通知數目上限。 |
| MaxIndexedEmptyPartitions |整數，預設值為 1000 |hello 空的分割區將會保留最大索引同步處理重新連線的用戶端 hello 通知的快取中。 任何超過此數目的空白分割區會移除 hello 查閱版本遞增的索引。 重新連線用戶端仍可以同步處理，並可接收遺漏空的分割區更新;但是 hello 同步處理通訊協定會變成更耗費資源。 |
| GatewayServiceDescriptionCacheLimit |整數，預設值為 0 |hello 維護 hello LRU 服務描述級快取中的項目數目上限 hello 命名閘道 （設定 too0 代表無限制）。 |
| PartitionCount |整數，預設值為 3 |hello hello 命名服務存放區 toobe 建立的資料分割數目。 每個資料分割擁有單一資料分割索引鍵對應 tooits 索引;因此資料分割索引鍵 [0;PartitionCount) 存在。 Hello 日益增加的命名服務資料分割會增加 hello 小數位數 hello 命名服務可在執行藉由降低 hello 平均量持有的任何備份複本的資料集;增加資源的情況的成本 (因為 PartitionCount * 必須維護 ReplicaSetSize 服務複本)。|

### <a name="section-name-runas"></a>區段名稱：RunAs
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| RunAsAccountName |字串，預設值為 "" |指出 hello RunAs 帳戶名稱。 "DomainUser" 或 "ManagedServiceAccount" 帳戶類型才需要此參數。 有效值為 "domain\user" 或 "user@domain"。 |
|RunAsAccountType|字串，預設值為 "" |指出 hello RunAs 帳戶類型。 任何 RunAs 區段皆需要此參數。有效值為 "DomainUser/NetworkService/ManagedServiceAccount/LocalSystem"。|
|RunAsPassword|字串，預設值為 "" |指出 hello RunAs 帳戶密碼。 "DomainUser" 帳戶類型才需要此參數。 |

### <a name="section-name-runasfabric"></a>區段名稱︰RunAs_Fabric
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| RunAsAccountName |字串，預設值為 "" |指出 hello RunAs 帳戶名稱。 "DomainUser" 或 "ManagedServiceAccount" 帳戶類型才需要此參數。 有效值為 "domain\user" 或 "user@domain"。 |
|RunAsAccountType|字串，預設值為 "" |指出 hello RunAs 帳戶類型。 任何 RunAs 區段皆需要此參數。有效值為 "LocalUser/DomainUser/NetworkService/ManagedServiceAccount/LocalSystem"。 |
|RunAsPassword|字串，預設值為 "" |指出 hello RunAs 帳戶密碼。 "DomainUser" 帳戶類型才需要此參數。 |

### <a name="section-name-runashttpgateway"></a>區段名稱：RunAs_HttpGateway
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| RunAsAccountName |字串，預設值為 "" |指出 hello RunAs 帳戶名稱。 "DomainUser" 或 "ManagedServiceAccount" 帳戶類型才需要此參數。 有效值為 "domain\user" 或 "user@domain"。 |
|RunAsAccountType|字串，預設值為 "" |指出 hello RunAs 帳戶類型。 任何 RunAs 區段皆需要此參數。有效值為 "LocalUser/DomainUser/NetworkService/ManagedServiceAccount/LocalSystem"。 |
|RunAsPassword|字串，預設值為 "" |指出 hello RunAs 帳戶密碼。 "DomainUser" 帳戶類型才需要此參數。 |

### <a name="section-name-runasdca"></a>區段名稱：RunAs_DCA
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| RunAsAccountName |字串，預設值為 "" |指出 hello RunAs 帳戶名稱。 "DomainUser" 或 "ManagedServiceAccount" 帳戶類型才需要此參數。 有效值為 "domain\user" 或 "user@domain"。 |
|RunAsAccountType|字串，預設值為 "" |指出 hello RunAs 帳戶類型。 任何 RunAs 區段皆需要此參數。有效值為 "LocalUser/DomainUser/NetworkService/ManagedServiceAccount/LocalSystem"。 |
|RunAsPassword|字串，預設值為 "" |指出 hello RunAs 帳戶密碼。 "DomainUser" 帳戶類型才需要此參數。 |

### <a name="section-name-httpgateway"></a>區段名稱：HttpGateway
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
|IsEnabled|布林值，預設值為 false | 啟用/停用 hello httpgateway。 預設為停用 Httpgateway，此組態需要 toobe 組 tooenable 它。 |
|ActiveListeners |單位，預設值為 50 | 讀取 toopost toohello http 伺服器佇列數目。 這會控制 hello hello HttpGateway 可以滿足的並行要求數目。 |
|MaxEntityBodySize |單位，預設值為 4194304 |  提供 hello hello 內容可預期的 http 要求的大小上限。 預設值為 4 MB。 若要求的主體大小大於此值，Httpgateway 會將要求判為失敗。 讀取區塊大小下限為 4096 個位元組。 因此，這有 toobe > = 4096。 |
|HttpGatewayHealthReportSendInterval |時間 (秒)，預設值為 30 | 以秒為單位指定時間範圍。 在哪一個 hello Http 閘道會傳送 hello 間隔累積健全狀況報表 tooHealth 管理員。 |

### <a name="section-name-ktllogger"></a>區段名稱︰KtlLogger
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
|AutomaticMemoryConfiguration |整數，預設值為 1 | 指出如果 hello 記憶體設定應該自動與動態設定旗標。 如果零然後 hello 記憶體組態設定會直接使用，不會變更基礎系統條件。 如果一個 hello 記憶體設定會自動設定，且可能會變更根據系統的條件。 |
|WriteBufferMemoryPoolMinimumInKB |整數，預設值為 8388608 |hello 數 KB tooinitially 配置 hello 寫入緩衝區的記憶體集區。 使用 0 tooindicate 沒有限制預設應該與下列 SharedLogSizeInMB 一致。 |
|WriteBufferMemoryPoolMaximumInKB | 整數，預設值為 0 |寫入緩衝區的記憶體集區 toogrow 最多的 KB tooallow hello 的 hello 次數。 使用 0 tooindicate 沒有限制。 |
|MaximumDestagingWriteOutstandingInKB | 整數，預設值為 0 | hello 數 KB tooallow hello 共用記錄 tooadvance 前面 hello 專用的記錄檔。 使用 0 tooindicate 沒有限制。
|SharedLogPath |字串，預設值為 "" | 路徑和檔案名稱 toolocation tooplace 共用的記錄的容器。 使用 "" 可使用位於網狀架構資料根目錄下的預設路徑。 |
|SharedLogId |字串，預設值為 "" |共用記錄容器的唯一 GUID。 若使用位於網狀架構資料根目錄下的預設路徑，則使用 ""。 |
|SharedLogSizeInMB |整數，預設值為 8192 | hello MB tooallocate 在 hello 共用的記錄的容器數目。 |

### <a name="section-name-applicationgatewayhttp"></a>區段名稱︰ApplicationGateway/Http
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
|IsEnabled |布林值，預設值為 false | 啟用/停用 hello HttpApplicationGateway。 預設為停用 HttpApplicationGateway，此組態需要 toobe 組 tooenable 它。 |
|NumberOfParallelOperations | 單位，預設值為 5000 | 讀取 toopost toohello http 伺服器佇列數目。 這會控制 hello hello HttpGateway 可以滿足的並行要求數目。 |
|DefaultHttpRequestTimeout |以秒為單位的時間。 預設值為 120 |以秒為單位指定時間範圍。  在 hello http 應用程式閘道處理 hello http 要求提供 hello 預設要求逾時。 |
|ResolveServiceBackoffInterval |時間 (秒)，預設值為 5 |以秒為單位指定時間範圍。  提供預設的 hello 撤退間隔後再重試失敗的解析服務作業。 |
|BodyChunkSize |單位，預設值為 16384 |  提供 hello hello 區塊以位元組為單位使用大小 tooread hello 主體。 |
|GatewayAuthCredentialType |字串，預設值為 "None" | 指出在 hello http 應用程式閘道端點有效值的安全性認證 toouse hello 類型是 「 無 / X509。 |
|GatewayX509CertificateStoreName |字串，預設值為 "My" | 包含 http 應用程式閘道之憑證的 X.509 憑證存放區名稱。 |
|GatewayX509CertificateFindType |字串，預設值為 "FindByThumbprint" | 指出 hello 存放區中憑證的 toosearch GatewayX509CertificateStoreName 支援值所指定的方式： FindByThumbprint;FindBySubjectName。 |
|GatewayX509CertificateFindValue | 字串，預設值為 "" | 搜尋篩選器值使用 toolocate hello http 應用程式閘道的憑證。 此憑證 hello https 端點上設定，也可以使用的 tooverify hello 身分識別的 hello 應用程式如果 hello 服務所需。 首先會查閱 FindValue，如果不存在，則會查閱 FindValueSecondary。 |
|GatewayX509CertificateFindValueSecondary | 字串，預設值為 "" |搜尋篩選器值使用 toolocate hello http 應用程式閘道的憑證。 此憑證 hello https 端點上設定，也可以使用的 tooverify hello 身分識別的 hello 應用程式如果 hello 服務所需。 首先會查閱 FindValue，如果不存在，則會查閱 FindValueSecondary。|

### <a name="section-name-management"></a>區段名稱︰Management
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| ImageStoreConnectionString |SecureString | 連接字串 toohello ImageStore 的根。 |
| ImageStoreMinimumTransferBPS | 整數，預設值為 1024 |hello ImageStore hello 叢集之間的最小傳輸速率。 當存取 hello 外部 ImageStore 時，這個值會是使用的 toodetermine hello 逾時。 更多時間來從 hello 叢集 toodownload 若 ImageStore hello 叢集之間的 hello 延遲很高的 tooallow hello 外部 ImageStore 僅變更此值。 |
|AzureStorageMaxWorkerThreads | 整數，預設值為 25 | hello 的平行背景工作執行緒數目上限。 |
|AzureStorageMaxConnections | 整數，預設值為 5000 | hello 並行連線 tooazure 儲存體的數目上限。 |
|AzureStorageOperationTimeout | 時間 (秒)，預設值為 6000 | 以秒為單位指定時間範圍。 Xstore 作業 toocomplete 逾時。 |
|ImageCachingEnabled | 布林值，預設值為 true | 此設定可讓我們 tooenable 或停用快取。 |
|DisableChecksumValidation | 布林值，預設值為 false | 此設定可讓我們 tooenable，或停用應用程式佈建期間的總和檢查碼驗證。 |
|DisableServerSideCopy | 布林值，預設值為 false | 此設定啟用或停用伺服器端副本 hello ImageStore 上應用程式套件，在應用程式佈建。 |

### <a name="section-name-healthmanagerclusterhealthpolicy"></a>區段名稱︰HealthManager/ClusterHealthPolicy
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| ConsiderWarningAsError |布林值，預設值為 false |叢集健康狀態評估原則︰將警告視為錯誤處理。 |
| MaxPercentUnhealthyNodes | 整數，預設值為 0 |叢集健全狀況評估原則： 最大狀況不良節點百分比允許 hello 叢集 toobe 狀況良好。 |
| MaxPercentUnhealthyApplications | 整數，預設值為 0 |叢集健全狀況評估原則： 狀況不良應用程式的最大百分比允許 hello 叢集 toobe 狀況良好。 |
|MaxPercentDeltaUnhealthyNodes | 整數，預設值為 10 |叢集升級健全狀況評估原則： 最大差異的狀況不良節點百分比允許 hello 叢集 toobe 狀況良好。 |
|MaxPercentUpgradeDomainDeltaUnhealthyNodes | 整數，預設值為 15 |叢集升級健全狀況評估原則： 的升級網域中的狀況不良節點之差異的最大百分比允許 hello 叢集 toobe 狀況良好。|

### <a name="section-name-faultanalysisservice"></a>區段名稱︰FaultAnalysisService
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| TargetReplicaSetSize |整數，預設值為 0 |NOT_PLATFORM_UNIX_START hello FaultAnalysisService 的 TargetReplicaSetSize。 |
| MinReplicaSetSize |整數，預設值為 0 |hello FaultAnalysisService 的 MinReplicaSetSize。 |
| ReplicaRestartWaitDuration |時間 (秒)，預設值為 60 分鐘|以秒為單位指定時間範圍。 hello FaultAnalysisService 的 ReplicaRestartWaitDuration。 |
| QuorumLossWaitDuration | 時間 (秒)，預設值為 MaxValue |以秒為單位指定時間範圍。 hello FaultAnalysisService 的 QuorumLossWaitDuration。 |
| StandByReplicaKeepDuration| 時間 (秒)，預設值為 (60*24*7) 分鐘 |以秒為單位指定時間範圍。 hello FaultAnalysisService 的 StandByReplicaKeepDuration。 |
| PlacementConstraints | 字串，預設值為 ""| hello FaultAnalysisService 的 PlacementConstraints。 |
| StoredActionCleanupIntervalInSeconds | 整數，預設值為 3600 |這是頻率 hello 存放區將會清除。  只有處於終止狀態且在至少 CompletedActionKeepDurationInSeconds 秒前完成的動作會遭到移除。 |
| CompletedActionKeepDurationInSeconds | 整數，預設值為 604800 | 這是大約多少時間 tookeep 動作中的終端機的狀態。  這也取決於 StoredActionCleanupIntervalInSeconds;因為 hello 工作 toocleanup 只會對該間隔。 604800 為 7 天。 |
| StoredChaosEventCleanupIntervalInSeconds | 整數，預設值為 3600 |這是頻率 hello 存放區會稽核的清除。如果事件的 hello 數目超過 30000;hello 清除會開始運作。 |

### <a name="section-name-filestoreservice"></a>區段名稱︰FileStoreService
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| NamingOperationTimeout |時間 (秒)，預設值為 60 |以秒為單位指定時間範圍。 hello 執行命名作業逾時。 |
| QueryOperationTimeout | 時間 (秒)，預設值為 60 |以秒為單位指定時間範圍。 hello 執行查詢作業逾時。 |
| MaxCopyOperationThreads | 單位，預設值為 0 | hello 平行的檔案數目上限該次要資料庫可以從主要複製。 '0' == 核心數目。 |
| MaxFileOperationThreads | 單位，預設值為 100 | hello 平行執行緒允許 tooperform FileOperations （複製/移動），在主要 hello 的數目上限。 '0' == 核心數目。 |
| MaxStoreOperations | 單位，預設值為 4096 |hello 平行的存放區的交易作業在主要伺服器上允許的數目上限。 '0' == 核心數目。 |
| MaxRequestProcessingThreads | 單位，預設值為 200 |hello 平行執行緒的數目上限 tooprocess 要求中允許 hello 主要。 '0' == 核心數目。 |
| MaxSecondaryFileCopyFailureThreshold | 單位，預設值為 25| hello hello 後才放棄次要上的檔案複製重試的數目上限。 |
| AnonymousAccessEnabled | 布林值，預設值為 true |啟用/停用匿名存取 toohello FileStoreService 共用。 |
| PrimaryAccountType | 字串，預設值為 "" |hello 主要的 hello 主體 tooACL hello FileStoreService AccountType 共用。 |
| PrimaryAccountUserName | 字串，預設值為 "" |hello 主要帳戶 hello 主體 tooACL hello FileStoreService 共用的使用者名稱。 |
| PrimaryAccountUserPassword | SecureString，預設值為空白 |hello 主要帳戶密碼的 hello 主體 tooACL hello FileStoreService 共用。 |
| FileStoreService | PrimaryAccountNTLMPasswordSecret | SecureString，預設值為空白 | 做為種子 toogenerated 相同 hello 密碼密碼時使用 NTLM 驗證的密碼。 |
| PrimaryAccountNTLMX509StoreLocation | 字串，預設值為 "LocalMachine"| hello hello X509 憑證存放區位置用於 toogenerate HMAC hello PrimaryAccountNTLMPasswordSecret 使用 NTLM 驗證時。 |
| PrimaryAccountNTLMX509StoreName | 字串，預設值為 "MY"| hello hello X509 憑證存放區名稱用於 toogenerate HMAC hello PrimaryAccountNTLMPasswordSecret 使用 NTLM 驗證時。 |
| PrimaryAccountNTLMX509Thumbprint | 字串，預設值為 ""|hello X509 憑證的指紋，hello 用於 toogenerate HMAC hello PrimaryAccountNTLMPasswordSecret 使用 NTLM 驗證時。 |
| SecondaryAccountType | 字串，預設值為 ""| hello 次要的 hello 主體 tooACL hello FileStoreService AccountType 共用。 |
| SecondaryAccountUserName | 字串，預設值為 ""| hello 次要帳戶 hello 主體 tooACL hello FileStoreService 共用的使用者名稱。 |
| SecondaryAccountUserPassword | SecureString，預設值為空白 |hello 次要帳戶密碼的 hello 主體 tooACL hello FileStoreService 共用。  |
| SecondaryAccountNTLMPasswordSecret | SecureString，預設值為空白 | 做為種子 toogenerated 相同 hello 密碼密碼時使用 NTLM 驗證的密碼。 |
| SecondaryAccountNTLMX509StoreLocation | 字串，預設值為 "LocalMachine" |hello hello X509 憑證存放區位置用於 toogenerate HMAC hello SecondaryAccountNTLMPasswordSecret 使用 NTLM 驗證時。 |
| SecondaryAccountNTLMX509StoreName | 字串，預設值為 "MY" |hello hello X509 憑證存放區名稱用於 toogenerate HMAC hello SecondaryAccountNTLMPasswordSecret 使用 NTLM 驗證時。 |
| SecondaryAccountNTLMX509Thumbprint | 字串，預設值為 ""| hello X509 憑證的指紋，hello 用於 toogenerate HMAC hello SecondaryAccountNTLMPasswordSecret 使用 NTLM 驗證時。 |

### <a name="section-name-imagestoreservice"></a>區段名稱︰ImageStoreService
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| 已啟用 |布林值，預設值為 false |hello ImageStoreService 啟用旗標。 |
| TargetReplicaSetSize | 整數，預設值為 7 |hello ImageStoreService 的 TargetReplicaSetSize。 |
| MinReplicaSetSize | 整數，預設值為 3 |hello ImageStoreService 的 MinReplicaSetSize。 |
| ReplicaRestartWaitDuration | 時間 (秒)，預設值為 60.0 * 30 | 以秒為單位指定時間範圍。 hello ImageStoreService 的 ReplicaRestartWaitDuration。 |
| QuorumLossWaitDuration | 時間 (秒)，預設值為 MaxValue | 以秒為單位指定時間範圍。 hello ImageStoreService 的 QuorumLossWaitDuration。 |
| StandByReplicaKeepDuration | 時間 (秒)，預設值為 3600.0 * 2 | 以秒為單位指定時間範圍。 hello ImageStoreService 的 StandByReplicaKeepDuration。 |
| PlacementConstraints | 字串，預設值為 "" | hello ImageStoreService 的 PlacementConstraints。 |
| ClientUploadTimeout | 時間 (秒)，預設值為 1800 |以秒為單位指定時間範圍。 逾時值的最上層的上傳要求 tooImage Store 服務。 |
| ClientCopyTimeout | 時間 (秒)，預設值為 1800 | 以秒為單位指定時間範圍。 逾時值的最上層的複製要求 tooImage Store 服務。 |
| ClientDownloadTimeout | 時間 (秒)，預設值為 1800 | 以秒為單位指定時間範圍。 逾時值的最上層的下載要求 tooImage Store 服務 |
| ClientListTimeout | 時間 (秒)，預設值為 600 | 以秒為單位指定時間範圍。 最上層清單中的逾時值要求 tooImage Store 服務。 |
| ClientDefaultTimeout | 時間 (秒)，預設值為 180 | 以秒為單位指定時間範圍。 所有非-上傳/非-下載要求的逾時值 （例如存在; 刪除） tooImage Store 服務。 |

### <a name="section-name-imagestoreclient"></a>區段名稱︰ImageStoreClient
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| ClientUploadTimeout |時間 (秒)，預設值為 1800 | 以秒為單位指定時間範圍。 逾時值的最上層的上傳要求 tooImage Store 服務。 |
| ClientCopyTimeout | 時間 (秒)，預設值為 1800 | 以秒為單位指定時間範圍。 逾時值的最上層的複製要求 tooImage Store 服務。 |
|ClientDownloadTimeout | 時間 (秒)，預設值為 1800 | 以秒為單位指定時間範圍。 逾時值的最上層的下載要求 tooImage Store 服務。 |
|ClientListTimeout | 時間 (秒)，預設值為 600 |以秒為單位指定時間範圍。 最上層清單中的逾時值要求 tooImage Store 服務。 |
|ClientDefaultTimeout | 時間 (秒)，預設值為 180 | 以秒為單位指定時間範圍。 所有非-上傳/非-下載要求的逾時值 （例如存在; 刪除） tooImage Store 服務。 |

### <a name="section-name-tokenvalidationservice"></a>區段名稱︰TokenValidationService
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| 提供者 |字串，預設值為 "DSTS" |以逗號分隔清單的權杖驗證提供者 tooenable (有效的提供者： DSTS;AAD)。 目前只能隨時啟用單一提供者。 |

### <a name="section-name-upgradeorchestrationservice"></a>區段名稱︰UpgradeOrchestrationService
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| TargetReplicaSetSize |整數，預設值為 0 |hello UpgradeOrchestrationService 的 TargetReplicaSetSize。 |
| MinReplicaSetSize |整數，預設值為 0 | hello UpgradeOrchestrationService 的 MinReplicaSetSize。
| ReplicaRestartWaitDuration | 時間 (秒)，預設值為 60 分鐘| 以秒為單位指定時間範圍。 hello UpgradeOrchestrationService 的 ReplicaRestartWaitDuration。 |
| QuorumLossWaitDuration | 時間 (秒)，預設值為 MaxValue | 以秒為單位指定時間範圍。 hello UpgradeOrchestrationService 的 QuorumLossWaitDuration。 |
| StandByReplicaKeepDuration | 時間 (秒)，預設值為 60*24*7 分鐘 | 以秒為單位指定時間範圍。 hello UpgradeOrchestrationService 的 StandByReplicaKeepDuration。 |
| PlacementConstraints | 字串，預設值為 "" | hello UpgradeOrchestrationService 的 PlacementConstraints。 |
| AutoupgradeEnabled | 布林值，預設值為 true | 以目標狀態檔案為基礎的自動輪詢和升級動作。 |
| UpgradeApprovalRequired | 布林值，預設值為 false | 設定 toomake 程式碼升級需要系統管理員核准，才能繼續。 |

### <a name="section-name-upgradeservice"></a>區段名稱︰UpgradeService
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| PlacementConstraints |字串，預設值為 "" |hello PlacementConstraints 升級服務。 |
| TargetReplicaSetSize | 整數，預設值為 3 | hello UpgradeService 的 TargetReplicaSetSize。 |
| MinReplicaSetSize | 整數，預設值為 2 | hello UpgradeService 的 MinReplicaSetSize。 |
| CoordinatorType | 字串，預設值為 "WUTest"| hello UpgradeService 的 CoordinatorType。 |
| BaseUrl | 字串，預設值為 "" |UpgradeService 的 BaseUrl。 |
| ClusterId | 字串，預設值為 "" | UpgradeService 的 ClusterId。 |
| X509StoreName | 字串，預設值為 "My"| UpgradeService 的 X509StoreName。 |
| X509StoreLocation | 字串，預設值為 "" | UpgradeService 的 X509StoreLocation。 |
| X509FindType | 字串，預設值為 ""| UpgradeService 的 X509FindType。 |
| X509FindValue | 字串，預設值為 "" | UpgradeService 的 X509FindValue。 |
| X509SecondaryFindValue | 字串，預設值為 "" | UpgradeService 的 X509SecondaryFindValue。 |
| OnlyBaseUpgrade | 布林值，預設值為 false | UpgradeService 的 OnlyBaseUpgrade。 |
| TestCabFolder | 字串，預設值為 "" | UpgradeService 的 TestCabFolder。 |

### <a name="section-name-securityclientaccess"></a>區段名稱︰Security/ClientAccess
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| CreateName |字串，預設值為 "Admin" |命名 URI 建立的安全性組態。 |
| DeleteName |字串，預設值為 "Admin" |命名 URI 刪除的安全性組態。 |
| PropertyWriteBatch |字串，預設值為 "Admin" |命名屬性寫入作業的安全性組態。 |
| CreateService |字串，預設值為 "Admin" | 服務建立的安全性組態。 |
| CreateServiceFromTemplate |字串，預設值為 "Admin" |從範本建立服務的安全性組態。 |
| UpdateService |字串，預設值為 "Admin" |服務更新的安全性組態。 |
| DeleteService  |字串，預設值為 "Admin" |服務刪除的安全性組態。 |
| ProvisionApplicationType |字串，預設值為 "Admin" | 應用程式類型佈建的安全性組態。 |
| CreateApplication |字串，預設值為 "Admin" | 應用程式建立的安全性組態。 |
| DeleteApplication |字串，預設值為 "Admin" | 應用程式刪除的安全性組態。 |
| UpgradeApplication |字串，預設值為 "Admin" | 用於啟動或中斷應用程式升級的安全性組態。 |
| RollbackApplicationUpgrade |字串，預設值為 "Admin" | 用於復原應用程式升級的安全性組態。 |
| UnprovisionApplicationType |字串，預設值為 "Admin" | 應用程式類型取消佈建的安全性組態。 |
| MoveNextUpgradeDomain |字串，預設值為 "Admin" | 用於以明確的「升級網域」繼續進行應用程式升級的安全性組態。 |
| ReportUpgradeHealth |字串，預設值為 "Admin" | 繼續目前的升級進度 hello 與應用程式升級的安全性設定。 |
| ReportHealth |字串，預設值為 "Admin" | 用於報告健康狀態的安全性組態。 |
| ProvisionFabric |字串，預設值為 "Admin" | MSI 和/或叢集資訊清單佈建的安全性組態。 |
| UpgradeFabric |字串，預設值為 "Admin" | 用於啟動叢集升級的安全性組態。 |
| RollbackFabricUpgrade |字串，預設值為 "Admin" | 用於復原叢集升級的安全性組態。 |
| UnprovisionFabric |字串，預設值為 "Admin" | MSI 和/或叢集資訊清單取消佈建的安全性組態。 |
| MoveNextFabricUpgradeDomain |字串，預設值為 "Admin" | 用於以明確的「升級網域」繼續進行叢集升級的安全性組態。 |
| ReportFabricUpgradeHealth |字串，預設值為 "Admin" | 繼續叢集升級與 hello 目前升級進行安全性設定。 |
| StartInfrastructureTask |字串，預設值為 "Admin" | 用於啟動基礎結構工作的安全性組態。 |
| FinishInfrastructureTask |字串，預設值為 "Admin" | 用於完成基礎結構工作的安全性組態。 |
| ActivateNode |字串，預設值為 "Admin" | 用於啟用節點的安全性組態。 |
| DeactivateNode |字串，預設值為 "Admin" | 用於停用節點的安全性組態。 |
| DeactivateNodesBatch |字串，預設值為 "Admin" | 用於停用多個節點的安全性組態。 |
| RemoveNodeDeactivations |字串，預設值為 "Admin" | 用於將停用多個節點之作業還原的安全性組態。 |
| GetNodeDeactivationStatus |字串，預設值為 "Admin" | 用於檢查停用狀態的安全性組態。 |
| NodeStateRemoved |字串，預設值為 "Admin" | 用於報告節點狀態已遭移除的安全性組態。 |
| RecoverPartition |字串，預設值為 "Admin" | 用於復原資料分割的安全性組態。 |
| RecoverPartitions |字串，預設值為 "Admin" | 用於復原資料分割的安全性組態。 |
| RecoverServicePartitions |字串，預設值為 "Admin" | 用於復原服務資料分割的安全性組態。 |
| RecoverSystemPartitions |字串，預設值為 "Admin" | 用於復原系統服務資料分割的安全性組態。 |
| ReportFault |字串，預設值為 "Admin" | 用於報告錯誤的安全性組態。 |
| InvokeInfrastructureCommand |字串，預設值為 "Admin" | 基礎結構工作管理命令的安全性組態。 |
| FileContent |字串，預設值為 "Admin" | 映像的安全性設定會儲存用戶端檔案傳輸 (外部 toocluster)。 |
| FileDownload |字串，預設值為 "Admin" | 映像存放區用戶端檔案下載起始 (外部 toocluster) 的安全性設定。 |
| InternalList |字串，預設值為 "Admin" | 映像存放區用戶端檔案列出作業 (內部) 的安全性組態。 |
| 刪除 |字串，預設值為 "Admin" | 映像存放區用戶端刪除作業的安全性組態。 |
| 上傳 |字串，預設值為 "Admin" | 映像存放區用戶端上傳作業的安全性組態。 |
| GetStagingLocation |字串，預設值為 "Admin" | 映像存放區用戶端預備位置擷取的安全性組態。 |
| GetStoreLocation |字串，預設值為 "Admin" | 映像存放區用戶端存放區位置擷取的安全性組態。 |
| NodeControl |字串，預設值為 "Admin" | 用於啟動、停止和重新啟動節點的安全性組態。 |
| CodePackageControl |字串，預設值為 "Admin" | 用於重新啟動程式碼套件的安全性組態。 |
| UnreliableTransportControl |字串，預設值為 "Admin" | 用於新增和移除行為的不可靠傳輸。 |
| MoveReplicaControl |字串，預設值為 "Admin" | 移動複本。 |
| PredeployPackageToNode |字串，預設值為 "Admin" | 預先部署 API。 |
| StartPartitionDataLoss |字串，預設值為 "Admin" | 會在資料分割上引發資料遺失。 |
| StartPartitionQuorumLoss |字串，預設值為 "Admin" | 會在資料分割上引發仲裁遺失。 |
| StartPartitionRestart |字串，預設值為 "Admin" | 同時會重新啟動部分或所有 hello 磁碟分割的複本。 |
| CancelTestCommand |字串，預設值為 "Admin" | 取消傳輸中的特定 TestCommand。 |
| StartChaos |字串，預設值為 "Admin" | 啟動尚未啟動的混亂。 |
| StopChaos |字串，預設值為 "Admin" | 停止已啟動的混亂。 |
| StartNodeTransition |字串，預設值為 "Admin" | 用於啟動節點轉換的安全性組態。 |
| StartClusterConfigurationUpgrade |字串，預設值為 "Admin" | 在資料分割上引發 StartClusterConfigurationUpgrade。 |
| GetUpgradesPendingApproval |字串，預設值為 "Admin" | 在資料分割上引發 GetUpgradesPendingApproval。 |
| StartApprovedUpgrades |字串，預設值為 "Admin" | 在資料分割上引發 StartApprovedUpgrades。 |
| Ping |字串，預設值為 "Admin\|\|User" | 用於 Ping 用戶端的安全性組態。 |
| 查詢 |字串，預設值為 "Admin\|\|User" | 查詢的安全性組態。 |
| NameExists |字串，預設值為 "Admin\|\|User" | 命名 URI 存在檢查的安全性組態。 |
| EnumerateSubnames |字串，預設值為 "Admin\|\|User" | 命名 URI 列舉的安全性組態。 |
| EnumerateProperties |字串，預設值為 "Admin\|\|User" | 命名屬性列舉的安全性組態。 |
| PropertyReadBatch |字串，預設值為 "Admin\|\|User" | 命名屬性讀取作業的安全性組態。 |
| GetServiceDescription |字串，預設值為 "Admin\|\|User" | 用於長時間輪詢服務通知和讀取服務描述的安全性組態。 |
| ResolveService |字串，預設值為 "Admin\|\|User" | 抱怨型服務解析的安全性組態。 |
| ResolveNameOwner |字串，預設值為 "Admin\|\|User" | 用於解析命名 URI 擁有者的安全性組態。 |
| ResolvePartition |字串，預設值為 "Admin\|\|User" | 用於解析系統服務的安全性組態。 |
| ServiceNotifications |字串，預設值為 "Admin\|\|User" | 事件型服務通知的安全性組態。 |
| PrefixResolveService |字串，預設值為 "Admin\|\|User" | 抱怨型服務前置詞解析的安全性組態。 |
| GetUpgradeStatus |字串，預設值為 "Admin\|\|User" | 用於輪詢應用程式升級狀態的安全性組態。 |
| GetFabricUpgradeStatus |字串，預設值為 "Admin\|\|User" | 用於輪詢叢集升級狀態的安全性組態。 |
| InvokeInfrastructureQuery |字串，預設值為 "Admin\|\|User" | 用於查詢基礎結構工作的安全性組態。 |
| 列出 |字串，預設值為 "Admin\|\|User" | 映像存放區用戶端檔案列出作業的安全性組態。 |
| ResetPartitionLoad |字串，預設值為 "Admin\|\|User" | 用於重設 failoverUnit 負載的安全性組態。 |
| ToggleVerboseServicePlacementHealthReporting | 字串，預設值為 "Admin\|\|User" | 用於切換詳細 ServicePlacement HealthReporting 的安全性組態。 |
| GetPartitionDataLossProgress | 字串，預設值為 "Admin\|\|User" | 提取 hello 進行叫用資料遺失的 api 呼叫。 |
| GetPartitionQuorumLossProgress | 字串，預設值為 "Admin\|\|User" | 提取 hello 進行叫用仲裁遺失 api 呼叫。 |
| GetPartitionRestartProgress | 字串，預設值為 "Admin\|\|User" | 提取 hello 進行重新啟動資料分割的 api 呼叫。 |
| GetChaosReport | 字串，預設值為 "Admin\|\|User" | 擷取給定的時間範圍內的 hello 狀態的混亂。 |
| GetNodeTransitionProgress | 字串，預設值為 "Admin\|\|User" | 用於取得節點轉換命令進度的安全性組態。 |
| GetClusterConfigurationUpgradeStatus | 字串，預設值為 "Admin\|\|User" | 在資料分割上引發 GetClusterConfigurationUpgradeStatus。 |
| GetClusterConfiguration | 字串，預設值為 "Admin\|\|User" | 在資料分割上引發 GetClusterConfiguration。 |

### <a name="section-name-reconfigurationagent"></a>區段名稱：ReconfigurationAgent
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| ApplicationUpgradeMaxReplicaCloseDuration | 時間 (秒)，預設值為 900 |以秒為單位指定時間範圍。 hello 的 hello 系統都會結束有停留在關閉的複本的服務主機之前將等候的持續時間。 |
| ServiceApiHealthDuration | 時間 (秒)，預設值為 30 分鐘 | 以秒為單位指定時間範圍。 ServiceApiHealthDuration 定義執行我們等候的時間服務 API toorun 之前我們回報狀況不良。 |
| ServiceReconfigurationApiHealthDuration | 時間 (秒)，預設值為 30 | 以秒為單位指定時間範圍。 ServiceReconfigurationApiHealthDuration 定義多久 hello 中重新設定的服務之前會回報為狀況不良。 |
| PeriodicApiSlowTraceInterval | 時間 (秒)，預設值為 5 分鐘 | 以秒為單位指定時間範圍。 PeriodicApiSlowTraceInterval 定義的速度較慢的 API 呼叫將會閃爍而重新追蹤 hello API 監視器的 hello 間隔。 |
| NodeDeactivationMaxReplicaCloseDuration | 時間 (秒)，預設值為 900 | 以秒為單位指定時間範圍。 終止封鎖節點停用的服務主機之前 hello toowait 最大時間。 |
| FabricUpgradeMaxReplicaCloseDuration | 時間 (秒)，預設值為 900 | 以秒為單位指定時間範圍。 之前終止服務主機的未關閉的複本會等候 hello 最大持續期限遠端協助。 |
| IsDeactivationInfoEnabled | 布林值，預設值為 true | 決定遠端協助會使用停用資訊讓您執行這項設定應該設定 tootrue 正在升級的現有叢集的新叢集的主要重新選擇如何，請參閱 hello 版本資訊 tooenable 這。 |

### <a name="section-name-placementandloadbalancing"></a>區段名稱︰PlacementAndLoadBalancing
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| TraceCRMReasons |布林值，預設值為 true |指定是否 crm tootrace 原因而發出的移動 toohello 操作事件通道。 |
| ValidatePlacementConstraint | 布林值，預設值為 true | 指定服務的 ServiceDescription 更新時，驗證 hello PlacementConstraint 運算式服務。 |
| PlacementConstraintValidationCacheSize | 整數，預設值為 10000 | 限制 hello hello 資料表用於快速驗證及位置條件約束運算式的快取的大小。 |
|VerboseHealthReportLimit | 整數，預設值為 20 | 定義複本的健全狀況警告報告為它 （如果已啟用詳細資訊的健康狀況報告） 之前，未放置的 toogo 的 hello 次數。 |
|ConstraintViolationHealthReportLimit | 整數，預設值為 50 | 定義 hello 次數條件約束違反複本 toobe 持續 unfixed 之前會進行診斷，並會發出健康情況報告。 |
|DetailedConstraintViolationHealthReportLimit | 整數，預設值為 200 | 定義條件約束違反複本具有 toobe 持續 unfixed 之前會進行診斷和詳細健全狀況報表所發出的 hello 次數。 |
|DetailedVerboseHealthReportLimit | 整數，預設值為 200 | 定義未放置的複本已 toobe 持續 unplaced 之前會發出報表的詳細健全狀況的 hello 次數。 |
|ConsecutiveDroppedMovementsHealthReportLimit | 整數，預設值為 20 | 定義 hello ResourceBalancer 發行動作會卸除之前會進行診斷，並會發出警告健全狀況的連續時間的數目。 負數︰不會在此狀況下發出任何警告。 |
|DetailedNodeListLimit | 整數，預設值為 15 | 在放置複本報告的 hello 定義 hello 每個條件約束 tooinclude 之前截斷節點數目。 |
|DetailedPartitionListLimit | 整數，預設值為 15 | 在 [診斷] 定義每個診斷的項目，如條件約束 tooinclude 之前截斷的資料分割的 hello 的數目。 |
|DetailedDiagnosticsInfoListLimit | 整數，預設值為 15 | 每個條件約束 tooinclude 診斷中的截斷之前定義 hello 診斷 （的詳細資訊） 的項目數目。|
|PLBRefreshGap | 時間 (秒)，預設值為 1 | 以秒為單位指定時間範圍。 定義 hello 最小 PLB 再次重新整理狀態之前，必須經過的時間量。 |
|MinPlacementInterval | 時間 (秒)，預設值為 1 | 以秒為單位指定時間範圍。 定義 hello 最小必須傳遞兩個連續的放置重試回合之前的時間量。 |
|MinConstraintCheckInterval | 時間 (秒)，預設值為 1 | 以秒為單位指定時間範圍。 定義 hello 最少兩個連續的條件約束檢查重試回合之前，必須經過的時間。 |
|MinLoadBalancingInterval | 時間 (秒)，預設值為 5 | 以秒為單位指定時間範圍。 定義 hello 最小必須傳遞兩個連續的平衡回合之前的時間量。 |
|BalancingDelayAfterNodeDown | 時間 (秒)，預設值為 120 |以秒為單位指定時間範圍。 在節點關閉事件之後，不要在此期間啟動平衡活動。 |
|BalancingDelayAfterNewNode | 時間 (秒)，預設值為 120 |以秒為單位指定時間範圍。 在新增節點之後，不要在此期間啟動平衡活動。 |
|ConstraintFixPartialDelayAfterNodeDown | 時間 (秒)，預設值為 120 | 以秒為單位指定時間範圍。 在節點關閉事件之後，不要在此期間修正 FaultDomain 和 UpgradeDomain 條件約束違規。 |
|ConstraintFixPartialDelayAfterNewNode | 時間 (秒)，預設值為 120 | 以秒為單位指定時間範圍。 在新增節點之後，不要在此期間修正 FaultDomain 和 UpgradeDomain 條件約束違規。 |
|GlobalMovementThrottleThreshold | 單位，預設值為 1000 | 移動中允許的最大數目在過去的 hello hello 平衡階段 GlobalMovementThrottleCountingInterval 所指定的間隔。 |
|GlobalMovementThrottleThresholdForPlacement | 單位，預設值為 0 | 最大數目的移動中放置階段中允許 hello 過去 GlobalMovementThrottleCountingInterval.0 所指定的間隔表示沒有限制。|
|GlobalMovementThrottleThresholdForBalancing | 單位，預設值為 0 | 移動 hello 過去在平衡階段中允許的最大數目 GlobalMovementThrottleCountingInterval 所指定的間隔。 0 表示沒有限制。 |
|GlobalMovementThrottleCountingInterval | 時間 (秒)，預設值為 600 | 以秒為單位指定時間範圍。 表示 hello hello 長度超過每個網域 （搭配 GlobalMovementThrottleThreshold） 的複本移動哪些 tootrack 的間隔。 您可以將 too0 tooignore 全域完全節流。 |
|MovementPerPartitionThrottleThreshold | 單位，預設值為 50 | 無平衡相關移動會發生資料分割，如果 hello 數目平衡該分割的複本相關的移動已達到或超過 MovementPerFailoverUnitThrottleThreshold hello 過去中所指定的間隔MovementPerPartitionThrottleCountingInterval。 |
|MovementPerPartitionThrottleCountingInterval | 時間 (秒)，預設值為 600 | 以秒為單位指定時間範圍。 表示 hello hello 長度超過間隔哪些 tootrack 複本移動每個資料分割 （以及 MovementPerPartitionThrottleThreshold 使用）。 |
|PlacementSearchTimeout | 時間 (秒)，預設值為 0.5 | 以秒為單位指定時間範圍。 在放置服務時，至少搜尋這麼長的時間再傳回結果。 |
|UseMoveCostReports | 布林值，預設值為 false | 指示 hello LB tooignore hello 成本的項目 hello 計分函式。產生可能的大型更平衡放置移動的數目。 |
|PreventTransientOvercommit | 布林值，預設值為 false | 決定應該 PLB 立即計算將釋放的 hello 起始移動的資源。 根據預設。PLB 可以起始移出和移動中的 hello 過量使用可以建立暫時性的相同節點上。 設定此參數 tootrue 會造成這些種類的 overcommits，視磁碟重組 (也稱為 placementWithMove) 將會停用。 |
|InBuildThrottlingEnabled | 布林值，預設值為 false | 判斷是否啟用 hello 中建置節流。 |
|InBuildThrottlingAssociatedMetric | 字串，預設值為 "" | hello 相關聯這項調整流速的度量的名稱。 |
|InBuildThrottlingGlobalMaxValue | 整數，預設值為 0 |hello 全域允許的組建中複本的最大數目。 |
|SwapPrimaryThrottlingEnabled | 布林值，預設值為 false| 判斷是否啟用 hello 交換主要節流。 |
|SwapPrimaryThrottlingAssociatedMetric | 字串，預設值為 ""| hello 相關聯這項調整流速的度量的名稱。 |
|SwapPrimaryThrottlingGlobalMaxValue | 整數，預設值為 0 | hello 允許全域的交換主要複本的最大數目。 |
|PlacementConstraintPriority | 整數，預設值為 0 | 決定位置條件約束 hello 優先權： 0： 硬碟;1： 軟性。負數： 忽略。 |
|PreferredLocationConstraintPriority | 整數，預設值為 2| 決定想要的位置限制式 hello 優先權： 0： 硬碟;1： 軟性。2： 最佳化。負數： 忽略 |
|CapacityConstraintPriority | 整數，預設值為 0 | 決定容量限制 hello 優先權： 0： 硬碟;1： 軟性。負數： 忽略。 |
|AffinityConstraintPriority | 整數，預設值為 0 | 決定親和性條件約束 hello 優先權： 0： 硬碟;1： 軟性。負數： 忽略。 |
|FaultDomainConstraintPriority | 整數，預設值為 0 | 決定錯誤網域條件約束 hello 優先權： 0： 硬碟;1： 軟性。負數： 忽略。 |
|UpgradeDomainConstraintPriority | 整數，預設值為 1| 決定升級網域條件約束 hello 優先權： 0： 硬碟;1： 軟性。負數： 忽略。 |
|ScaleoutCountConstraintPriority | 整數，預設值為 0 | 決定範圍外計數限制式 hello 優先權： 0： 硬碟;1： 軟性。負數： 忽略。 |
|ApplicationCapacityConstraintPriority | 整數，預設值為 0 | 決定容量限制 hello 優先權： 0： 硬碟;1： 軟性。負數： 忽略。 |
|MoveParentToFixAffinityViolation | 布林值，預設值為 false | 設定決定如果父複本可以移動 toofix 親和性條件約束。|
|MoveExistingReplicaForPlacement | 布林值，預設值為 true |設定用來決定是否在放置期間 toomove 現有複本。 |
|UseSeparateSecondaryLoad | 布林值，預設值為 true | 決定是否使用不同的次要負載的設定。 |
|PlaceChildWithoutParent | 布林值，預設值為 true | 決定當父系複本皆未運作時，是否可以放置子服務複本的設定。 |
|PartiallyPlaceServices | 布林值，預設值為 true | 決定當叢集中的所有服務複本適合使用的節點有限時，是要「全都或全不」放置。|
|InterruptBalancingForAllFailoverUnitUpdates | 布林值，預設值為 false | 決定任何類型的容錯移轉單元更新是否應中斷快速或緩慢的平衡執行。 若指定 "false"，當 FailoverUnit 符合下列條件時，平衡執行將會中斷︰已建立/已刪除、有遺漏的複本、變更了主要複本位置或變更了複本數目。 若為 FailoverUnit 符合下列條件的其他情況下，平衡執行則不會中斷︰有額外的複本、變更了任何複本旗標、只變更了資料分割版本或任何其他情況。 |

### <a name="section-name-security"></a>區段名稱︰Security
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| ClusterProtectionLevel |None 或 EncryptAndSign |不安全的叢集為 None (預設值)，安全的叢集為 EncryptAndSign。 |

### <a name="section-name-hosting"></a>區段名稱：Hosting
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| ServiceTypeRegistrationTimeout |時間 (秒)，預設值為 300 |Hello ServiceType toobe 向網狀架構所允許的最大時間 |
| ServiceTypeDisableFailureThreshold |整數，預設值為 1 |這是 hello 閾值 hello FailoverManager (FM) 之後的失敗計數通知 toodisable hello 服務類型，該節點並再試一次用於放置的不同節點上。 |
| ActivationRetryBackoffInterval |時間 (秒)，預設值為 5 |每個啟用失敗; 上的輪詢間隔每個持續啟用失敗時，hello 系統重試 hello 向上 toohello MaxActivationFailureCount 的啟用。 hello 每一次嘗試的重試間隔是持續啟用失敗，以及 hello 啟用撤退間隔的產品。 |
| ActivationMaxRetryInterval |時間 (秒)，預設值為 300 |每個持續啟用失敗時，hello 系統重試 hello 向上 tooActivationMaxFailureCount 的啟用。 ActivationMaxRetryInterval 指定每次啟用失敗之後在重試之前等待的時間間隔 |
| ActivationMaxFailureCount |整數，預設值為 10 |系統在放棄之前重試失敗啟用的次數 |

### <a name="section-name-failovermanager"></a>區段名稱︰FailoverManager
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| PeriodicLoadPersistInterval |時間 (秒)，預設值為 10 |這會決定頻率 hello FM 檢查新的負載報告 |

### <a name="section-name-federation"></a>區段名稱︰Federation
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| LeaseDuration |時間 (秒)，預設值為 30 |節點與其相鄰節點之間的租用持續時間。 |
| LeaseDurationAcrossFaultDomain |時間 (秒)，預設值為 30 |所有容錯網域的節點與其相鄰節點之間的租用持續時間。 |

### <a name="section-name-clustermanager"></a>區段名稱︰ClusterManager
| **參數** | **允許的值** | **指引或簡短描述** |
| --- | --- | --- |
| UpgradeStatusPollInterval |時間 (秒)，預設值為 60 |hello 應用程式升級狀態的輪詢頻率。 這個值會決定 hello 更新任何 GetApplicationUpgradeProgress 呼叫率 |
| UpgradeHealthCheckInterval |時間 (秒)，預設值為 60 |在受監視應用程式升級期間檢查 hello 健全狀況狀態的頻率 |
| FabricUpgradeStatusPollInterval |時間 (秒)，預設值為 60 |hello Fabric 升級狀態的輪詢頻率。 這個值會決定 hello 更新任何 GetFabricUpgradeProgress 呼叫率 |
| FabricUpgradeHealthCheckInterval |時間 (秒)，預設值為 60 |健全狀況狀態檢查期間監視的 Fabric 升級的 hello 頻率 |
|InfrastructureTaskProcessingInterval | 時間 (秒)，預設值為 10 |以秒為單位指定時間範圍。 hello hello 基礎結構工作處理的狀態機器使用的處理間隔。 |
|TargetReplicaSetSize |整數，預設值為 7 |hello ClusterManager 的 TargetReplicaSetSize。 |
|MinReplicaSetSize |整數，預設值為 3 |hello ClusterManager 的 MinReplicaSetSize。 |
|ReplicaRestartWaitDuration |時間 (秒)，預設值為 (60.0 * 30)|以秒為單位指定時間範圍。 hello ClusterManager 的 ReplicaRestartWaitDuration。 |
|QuorumLossWaitDuration |時間 (秒)，預設值為 MaxValue | 以秒為單位指定時間範圍。 hello ClusterManager 的 QuorumLossWaitDuration。 |
|StandByReplicaKeepDuration | 時間 (秒)，預設值為 (3600.0 * 2)|以秒為單位指定時間範圍。 hello ClusterManager 的 StandByReplicaKeepDuration。 |
|PlacementConstraints | 字串，預設值為 "" |hello ClusterManager 的 PlacementConstraints。 |
|SkipRollbackUpdateDefaultService | 布林值，預設值為 false |hello CM 將應用程式升級復原期間，略過還原的已更新的預設服務。 |
|EnableDefaultServicesUpgrade | 布林值，預設值為 false |在應用程式升級期間啟用預設服務升級作業。 在升級之後，將會覆寫預設的服務描述。 |
|InfrastructureTaskHealthCheckWaitDuration |時間 (秒)，預設值為 0| 以秒為單位指定時間範圍。 hello 開始之後的後續處理基礎結構工作健康情況檢查之前的時間 toowait 數量。 |
|InfrastructureTaskHealthCheckStableDuration | 時間 (秒)，預設值為 0| 以秒為單位指定時間範圍。 後續處理工作的基礎結構工作成功完成之前，會檢查時間 tooobserve 連續傳遞健康情況的 hello 數量。 若觀察到失敗的健康狀態檢查將會重設此計時器。 |
|InfrastructureTaskHealthCheckRetryTimeout | 時間 (秒)，預設值為 60 |以秒為單位指定時間範圍。 hello 時間 toospend 重試失敗的健全狀況檢查時的後續處理基礎結構工作數量。 若觀察到已通過的健康狀態檢查將會重設此計時器。 |
|ImageBuilderTimeoutBuffer |時間 (秒)，預設值為 3 |以秒為單位指定時間範圍。 hello 時間 tooallow 映像產生器特定的逾時錯誤 tooreturn toohello 用戶端數量。 如果這個緩衝區太小。然後 hello 用戶端 hello 伺服器之前逾時，並取得泛型的逾時錯誤。 |
|MinOperationTimeout | 時間 (秒)，預設值為 60 |以秒為單位指定時間範圍。 hello 在內部處理 ClusterManager 上的作業的最小通用逾時。 |
|MaxOperationTimeout |時間 (秒)，預設值為 MaxValue | 以秒為單位指定時間範圍。 hello 在內部處理 ClusterManager 上的作業的最大通用逾時。 |
|MaxTimeoutRetryBuffer | 時間 (秒)，預設值為 600 |以秒為單位指定時間範圍。 hello 最大作業逾時在內部重試到期時 tootimeouts 是<Original Timeout>  +  <MaxTimeoutRetryBuffer>。 會以 MinOperationTimeout 增量來加上額外的逾時。 |
|MaxCommunicationTimeout |時間 (秒)，預設值為 600 |以秒為單位指定時間範圍。 （也就是; hello ClusterManager 和其他系統服務之間的內部通訊的最大逾時值命名服務。容錯移轉管理員和等等）。 此逾時值應小於全域 MaxOperationTimeout (因為每個用戶端作業的系統元件之間可能會有多個通訊)。 |
|MaxDataMigrationTimeout |時間 (秒)，預設值為 600 |以秒為單位指定時間範圍。 Fabric 升級後隨同 hello 資料移轉的復原作業的最大逾時值。 |
|MaxOperationRetryDelay |時間 (秒)，預設值為 5| 以秒為單位指定時間範圍。 hello，發生失敗時，內部重試延遲上限。 |
|ReplicaSetCheckTimeoutRollbackOverride |時間 (秒)，預設值為 1200 | 以秒為單位指定時間範圍。 如果 ReplicaSetCheckTimeout 設定 toohello DWORD; 最大值然後它會覆寫此組態進行回復的 hello hello 值。 用於向前復原的 hello 值絕不會被覆寫。 |
|ImageBuilderJobQueueThrottle |整數，預設值為 10 |Image Builder Proxy 作業佇列對於應用程式要求的執行緒計數節流。 |

## <a name="next-steps"></a>後續步驟
如需有關叢集管理的詳細資訊，請參閱下列文件︰

[新增、變換、移除 Azure 叢集的憑證 ](service-fabric-cluster-security-update-certs-azure.md) 

