| 資源 | 預設限制 |
| --- | --- |
| 每一訂用帳戶的儲存體帳戶數目 |200<sup>1</sup> |
| 儲存體帳戶容量上限 |500 TB<sup>2</sup> |
| 每一儲存體帳戶的 Blob 容器、Blob、檔案共用、資料表、佇列、實體或訊息的數目上限 |沒有限制 |
| 單一 Blob 容器、資料表或佇列的大小上限 |與儲存體帳戶容量上限相同 |
| 區塊 Blob 或附加 Blob 中的區塊數目上限 |50,000 |
| 區塊 blob 中的區塊大小上限 |100 MB |
| 區塊 blob 的大小上限 |50,000 X 100 MB (約為 4.75 TB) |
| 附加 Blob 中的區塊大小上限 |4 MB |
| 附加 Blob 的大小上限 |50,000 x 4 MB (約為 195 GB) |
| 分頁 blob 的大小上限 |8 TB |
| 資料表實體的大小上限 |1 MB |
| 資料表實體中屬性的數目上限 |252 |
| 佇列中訊息的大小上限 |64 KB |
| 檔案共用的大小上限 |5 TB |
| 檔案共用中檔案的大小上限 |1 TB |
| 檔案共用中的檔案數目上限 |僅限制為 hello hello 檔案共用 5TB 總容量 |
| 每個共用的最大 IOPS |1000 |
| 檔案共用中的檔案數目上限 |僅限制為 hello hello 檔案共用 5TB 總容量 |
| 每個容器、檔案共用、資料表或佇列的預存存取原則的最大數目 |5 |
| 每一儲存體帳戶的要求率上限 |Blob: 每秒 20,000 要求<sup>2</sup> blob 的任何有效的大小 （受限於只能 hello 帳戶入口/出口限制） <br />檔案︰每個檔案共用 1000 IOPS (大小 8 KB) <br />佇列：每秒 20000 則訊息 (假設 1 KB 訊息大小)<br />資料表：每秒 20000 則交易 (假設 1 KB 實體大小) |
| 單一 Blob 的目標輸送量 |每秒要求總 too60 每秒 （含） 以上 too500 MB |
| 單一佇列的目標輸送量 (1 KB 訊息) |每秒 too2000 訊息 |
| 單一資料表分割的目標輸送量 (1 KB 實體) |總秒 too2000 實體 |
| 單一檔案共用的目標輸送量 |向上 too60 每秒 MB |
| 每一儲存體帳戶的輸入上限<sup>3</sup> (美國地區) |如果啟用 GRS/ZRS<sup>4</sup>，則為 10 Gbps，LRS 為 20 Gbps<sup>2</sup> |
| 每一儲存體帳戶的輸出上限<sup>3</sup> (美國地區) |如果啟用 RA-GRS/GRS/ZRS<sup>4</sup>，則為 20 Gbps，LRS 為 30 Gbps<sup>2</sup> |
| 每一儲存體帳戶的輸入上限<sup>3</sup> (非美國地區) |如果啟用 GRS/ZRS<sup>4</sup>，則為 5 Gbps，LRS 為 10 Gbps<sup>2</sup> |
| 每一儲存體帳戶的輸出上限<sup>3</sup> (非美國地區) |如果啟用 RA-GRS/GRS/ZRS<sup>4</sup>，則為 10 Gbps，LRS 為 15 Gbps<sup>2</sup> |

<sup>1</sup>這包括標準和進階儲存體帳戶。 如果您需要超過 200 個儲存體帳戶，請透過 [Azure 支援](https://azure.microsoft.com/support/faq/)提出要求。 hello Azure 儲存體小組將檢閱您的商務案例，並可能核准 too250 儲存體帳戶。 

<sup>2</sup> tooget 您標準儲存體帳戶 toogrow 過去 hello 公告的容量、 輸入/輸出和要求的速率限制，請透過要求[Azure 支援](https://azure.microsoft.com/support/faq/)。 hello Azure 儲存體小組會檢閱 hello 要求，並可能核准較高的限制，以案例為基礎。

<sup>3</sup>*輸入*參考 tooall 資料 （要求） 傳送 tooa 儲存體帳戶。 *輸出*是指從儲存體帳戶接收的 tooall 資料 （回應）。  

<sup>4</sup>Azure 儲存體複寫選項包括：
* **RA-GRS**：讀取權限異地備援儲存體。 如果已啟用 RA-GRS，hello 次要位置的輸出目標是相同 toothose hello 主要位置。
* **GRS**：異地備援儲存體。 
* **ZRS**：區域備援儲存體。 僅適用於區塊 Blob。 
* **LRS**：本地備援儲存體。 


