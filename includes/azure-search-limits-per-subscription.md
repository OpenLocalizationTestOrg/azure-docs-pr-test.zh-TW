您可以建立多個訂用帳戶，佈建於特定一層，允許在每一層的服務的 hello 數目只受限於每個內的服務。 比方說，您可以建立在 hello 基本層 too12 服務和其他的 12 服務內 hello hello S1 層相同訂用帳戶。 如需各層的詳細資訊，請參閱[選擇 Azure 搜尋服務的 SKU 或階層](../articles/search/search-sku-tier.md)。

最大服務限制可以視要求引發。 如果您需要更多的連絡 Azure 支援服務內 hello 相同訂用帳戶。

| 資源 | 免費 | 基本 | S1 | S2 | S3 | S3 HD <sup>1</sup> |
| --- | --- | --- | --- | --- | --- | --- |
| 服務數目上限 |1 |12 |12 |6 |6 |6 |
| SU 中的最大調整規模 <sup>2</sup> |N/A <sup>3</sup> |3 SU <sup>4</sup> |36 SU |36 SU |36 SU |36 SU |

<sup>1</sup> S3 HD 目前不支援[索引子](../articles/search/search-indexer-overview.md)。 

<sup>2</sup> 搜尋單位 (SU) 是可計費單位，會以*複本*或*資料分割*形式配置。 您需要這兩種資源才能進行儲存、編製索引及查詢作業。 深入了解如何搜尋單位計算，加上保持在 hello 最大限制，請參閱有效組合的圖表 toolearn[調整 查詢和索引的工作負載的資源層級](../articles/search/search-capacity-planning.md)。 

<sup>3</sup> [免費] 是以多個訂閱者所使用的共用資源為依據。 在這一層，沒有個別訂閱者專用的資源。 基於這個理由，最大調整規模會標示為不適用。

<sup>4</sup> [基本] 具有一個固定的磁碟分割。 在這一層，會使用額外的 SU 為增加的查詢工作負載配置更多複本。

