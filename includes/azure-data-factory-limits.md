資料處理站是具有下列位置 toomake 確定彼此的工作負載會受到保護客戶的訂閱中的預設限制 hello 的多租用戶服務。 許多 hello 限制可以輕鬆地引發 toohello 最大限制註冊訂用帳戶之連絡支援人員。

| **Resource** | **預設限制** | **上限** |
| --- | --- | --- |
| Azure 訂用帳戶中的 Data Factory |50 |[請連絡支援人員](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| 資料處理站中的管線 |2500 |[請連絡支援人員](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| 資料處理站中的資料集 |5000 |[請連絡支援人員](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| 每個資料集的並行配量 |10 |10 |
| 管線物件的每個物件位元組大小<sup>1</sup> |200 KB |200 KB |
| 資料集和已連結服務的每個物件位元組大小<sup>1</sup> |100 KB |2000 KB |
| 訂用帳戶中的 HDInsight 隨選叢集核心<sup>2</sup> |60 |[請連絡支援人員](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| 雲端資料移動單位 <sup>3</sup> |32 |[請連絡支援人員](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| 管線活動執行的重試計數 |1000 |MaxInt (32 位元) |

<sup>1</sup>管線、 資料集和連結的服務物件代表您工作負載的邏輯群組。 限制這些物件不相關資料，您可以移動，並與 hello Azure Data Factory 服務處理的 tooamount。 資料處理站是設計的 tooscale toohandle pb 計的資料。

<sup>2</sup>隨 HDInsight 核心會配置超出 hello 訂用帳戶包含 hello 資料 factory。 如此一來，超過限制的 hello 為的 hello Data Factory 強制執行在隨選 HDInsight 核心的核心限制，而且不同於您的 Azure 訂用帳戶相關聯的 hello 核心限制。

<sup>3</sup> 雲端資料移動單位 (DMU) 正用於雲端到雲端複製作業。 它是量值，表示 hello 電源 （CPU、 記憶體和網路資源配置的組合） 的 Data Factory 中的單一單位。 在某些情況下，利用更多 DMU 可以達到更高的複製輸送量。 請參閱太[雲端資料移動的單位](../articles/data-factory/data-factory-copy-activity-performance.md#cloud-data-movement-units)詳細資料 區段。

| **Resource** | **預設下限** | **下限** |
| --- | --- | --- |
| 排程間隔 |15 Minuten |15 Minuten |
| 重試嘗試間的間隔 |1 秒 |1 秒 |
| 重試逾時值 |1 秒 |1 秒 |

### <a name="web-service-call-limits"></a>Web 服務呼叫限制
Azure Resource Manager 有 API 呼叫限制。 您可以在 hello 速率進行 API 呼叫[Azure 資源管理員 API 限制](../articles/azure-subscription-service-limits.md#resource-group-limits)。
