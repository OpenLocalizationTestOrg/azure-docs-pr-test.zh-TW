| 資源 | 預設限制 | 上限 |
| --- | --- | --- |
| 每一[訂用帳戶](../articles/billing-buy-sign-up-azure-subscription.md) VM |每個區域 10,000 個 <sup>1</sup> |每個區域 10,000 個 |
| 每一[訂用帳戶](../articles/billing-buy-sign-up-azure-subscription.md)的 VM 總計核心 |每個區域 20<sup>1</sup> 個 | 請連絡支援人員 |
| 每一[訂用帳戶](../articles/billing-buy-sign-up-azure-subscription.md)的 VM 每個系列 (Dv2、F 等等) 核心 |每個區域 20<sup>1</sup> 個 | 請連絡支援人員 |
| 每一訂用帳戶[共同管理員](../articles/billing-add-change-azure-subscription-administrator.md) |無限 |無限 |
| 每一訂用帳戶[儲存體帳戶](../articles/storage/common/storage-create-storage-account.md) |200 |200<sup>2</sup> |
| 每一訂用帳戶[資源群組](../articles/azure-resource-manager/resource-group-overview.md) |800 |800 |
| 每一訂用帳戶[可用性設定組](../articles/virtual-machines/windows/manage-availability.md#configure-multiple-virtual-machines-in-an-availability-set-for-redundancy) |每個區域 2,000 個 |每個區域 2,000 個 |
| 資源管理員 API 讀取 |每小時 15,000 個 |每小時 15,000 個 |
| 資源管理員 API 寫入 |每小時 1,200 個 |每小時 1,200 個 |
| 資源管理員 API 要求的大小 |4,194,304 個位元組 |4,194,304 個位元組 |
| 每個訂用帳戶的標籤<sup>3</sup> |無限制 |無限制 |
| 每個訂用帳戶的唯一標記計算<sup>3</sup> | 10,000 | 10,000 |
| 每一訂用帳戶[雲端服務](../articles/cloud-services/cloud-services-choose-me.md) |不適用<sup>4</sup> |不適用<sup>4</sup> |
| 每一訂用帳戶[同質群組](../articles/virtual-network/virtual-networks-migrate-to-regional-vnet.md) |不適用<sup>4</sup> |不適用<sup>4</sup> |

<sup>1</sup>預設限制會因優惠類別類型 (如免費試用、隨收隨付和系列，例如 Dv2、F、G 等等) 而有所差異。

<sup>2</sup>這包括標準和進階儲存體帳戶。 如果您需要超過 200 個儲存體帳戶，請透過 [Azure 支援](https://azure.microsoft.com/support/faq/)提出要求。 hello Azure 儲存體小組將檢閱您的商務案例，並可能核准 too250 儲存體帳戶。

<sup>3</sup>您可以套用每個訂用帳戶的標記數目不受限。 每個資源或資源群組的標記的 hello 數目是有限的 too15。 資源管理員只會傳回[唯一的標記名稱和值的清單](/rest/api/resources/tags#Tags_List)時 hello 標記數目是 10,000 或更少的 hello 訂用帳戶中。 不過，您仍然可以找資源標記時 hello 數目超過 10,000。  

<sup>4</sup>這些功能就不再需要與 Azure 資源群組，以及 hello Azure 資源管理員。

> [!NOTE]
> 虛擬機器核心有區域的總計限制，以及每個個別強制執行的大小 （Dv2、 F 等） 的序列限制某個地區的重要 tooemphasize 它。  例如，請考慮美國東部訂用帳戶的總計 VM 核心限制為 30、A 系列核心限制為 30，和 D 系列核心限制為 30。  此訂用帳戶允許 toodeploy 30 A1 Vm 或 30 D1 Vm，或組合 hello 兩個 tooexceed 30 （例如，10 A1 Vm 和 20 D1 Vm） 的核心總數。  
> <!-- -->
> 
> 

