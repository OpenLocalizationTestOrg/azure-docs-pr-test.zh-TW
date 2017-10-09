儲存體帳戶分為兩種類型：

### <a name="general-purpose-storage-accounts"></a>一般用途的儲存體帳戶
一般用途儲存體帳戶可讓您存取 tooAzure 儲存體服務，例如資料表、 佇列、 檔案、 Blob 和 Azure 虛擬機器磁碟，在單一帳戶之下。 這種類型的儲存體帳戶有兩個效能層︰

* 標準儲存體效能層可讓您 toostore 資料表、 佇列、 檔案、 Blob 和 Azure 虛擬機器磁碟。
* 進階儲存體效能層，目前僅支援 Azure 虛擬機器磁碟。 如需進階儲存體的深入概觀，請參閱 [進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體](../articles/storage/common/storage-premium-storage.md) 。

### <a name="blob-storage-accounts"></a>Blob 儲存體帳戶
Blob 儲存體帳戶是特殊的儲存體帳戶，可將非結構化資料儲存為 Azure 儲存體中的 Blob (物件)。 Blob 儲存體帳戶是類似 tooyour 現有一般用途的儲存體帳戶，並共用所有 hello 很棒的持久性、 可用性、 延展性及效能的功能區塊 blob 包括 100 %api 的一致性使用，附加 blob。 對於只需要封鎖或附加 Blob 儲存體的應用程式，我們建議使用 Blob 儲存體帳戶。

> [!NOTE]
> Blob 儲存體帳戶僅支援區塊和附加 Blob，不支援分頁 Blob。
> 
> 

Blob 儲存體帳戶公開 hello**存取層**屬性可指定帳戶建立期間和之後視需要修改。 根據您的資料存取模式，可以指定兩種類型的存取層︰

* A**作用**表示將會更頻繁地存取 hello 儲存體帳戶中的 hello 物件的存取層。 這可讓您 toostore 資料在成本較低的存取。
* A **Cool**表示將較不常存取 hello 儲存體帳戶中的 hello 物件的存取層。 這可讓您 toostore 資料較低的資料儲存體成本。

如果沒有在 hello 使用量模式中的資料變更，您也可以切換隨時這些存取層之間。 變更 hello 存取層可能會導致產生額外費用。 如需詳細資訊，請參閱 [Blob 儲存體帳戶的價格和計費](../articles/storage/blobs/storage-blob-storage-tiers.md#pricing-and-billing) 。

如需 Blob 儲存體帳戶的詳細資訊，請參閱 [Azure Blob 儲存體：經常性存取和非經常性存取層](../articles/storage/blobs/storage-blob-storage-tiers.md)。

您可以建立儲存體帳戶之前，您必須有 Azure 訂用帳戶，也就是計劃，可讓您存取 tooa 各種 Azure 服務。 您可以利用 [免費帳戶](https://azure.microsoft.com/pricing/free-trial/)來開始使用 Azure。 一旦您決定 toopurchase 訂用帳戶方案，您可以選擇各式各樣的[購買選項](https://azure.microsoft.com/pricing/purchase-options/)。 如果您是 [MSDN 訂閱者](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)，您將取得可在 Azure 服務 (包括 Azure 儲存體) 中使用的每月免費額度。 如需批量價格的詳細資訊，請參閱 [Azure 儲存體價格 ](https://azure.microsoft.com/pricing/details/storage/) 。

如何 toocreate 儲存體帳戶，請參閱的 toolearn[建立儲存體帳戶](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account)如需詳細資訊。 您可以建立註冊 too200 唯一名稱與單一訂用帳戶的儲存體帳戶。 如需關於儲存體帳戶限制的詳細資訊，請參閱 [Azure 儲存體延展性和效能目標](../articles/storage/common/storage-scalability-targets.md) 。

