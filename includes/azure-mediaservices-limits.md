>[!NOTE]
>如需不固定的資源，您可能會尋求 hello 配額 toobe 引發，開啟支援票證。 請勿**不**tooobtain 較高的限制，嘗試建立額外的 Azure Media Services 帳戶。

| 資源 | 預設限制 | 
| --- | --- | 
| 在單一訂用帳戶的 Azure 媒體服務 (AMS) 帳戶 | 25 (固定) |
| 每個 AMS 帳戶的媒體保留單元 (RU) |25 (S1, S2)<br/>10 (S3) <sup>(1)</sup> | 
| 每個 AMS 帳戶的作業 | 50,000<sup>(2)</sup> |
| 每個作業的鏈結工作 | 30 (固定) |
| 每個 AMS 帳戶的資產 | 1,000,000|
| 每個工作的資產 | 50 |
| 每個作業的資產 | 100 |
| 一次與資產相關聯的唯一定位器 | 5<sup>(4)</sup> |
| 每個 AMS 帳戶的即時通道  |5|
| 每個通道中已停止狀態的程式  |50|
| 每個通道中執行中的程式  |3|
| 每個 AMS 帳戶執行中的串流端點|2|
| 每個串流端點的資料流單位  |10 |
| 儲存體帳戶 | 1,000<sup>(5)</sup> (固定) |
| 原則 | 1,000,000<sup>(6)</sup> |
| 檔案大小| 在某些情況下沒有限制 hello 來處理媒體服務中支援的最大檔案大小。 <sup>7</sup> |
  
<sup>1</sup> 印度西部無法使用 S3 RU。 如果 hello 客戶變更 hello 類型 （例如，從 S2 tooS1)，則會重設 hello max RU 限制。 

<sup>2</sup> 這個數目包括佇列、已完成、作用中和已取消的工作。 不包含已刪除的工作。 您可以刪除 hello 舊作業步驟使用**IJob.Delete**或 hello**刪除**HTTP 要求。

啟動年 4 月 1，2017，超過 90 天您帳戶中的任何工作記錄將會自動刪除，以及其相關聯的工作記錄，即使 hello 的總記錄數低於 hello 配額上限。 如果您需要 tooarchive hello 作業/工作資訊時，您可以使用所述的 hello 碼[這裡](../articles/media-services/media-services-dotnet-manage-entities.md)。

<sup>3</sup>時提出要求 toolist 工作項目，最多 1000 個會傳回每個要求。 如果您需要 tookeep 追蹤所有提交作業，如中所述，您可以使用 top/skip [OData 系統查詢選項](http://msdn.microsoft.com/library/gg309461.aspx)。

<sup>4</sup> 定位器並非設計來管理每個使用者的存取控制。 toogive 不同的存取權限 tooindividual 使用者使用數位版權管理 (DRM) 解決方案。 如需詳細資訊，請參閱 [本節](../articles/media-services/media-services-content-protection-overview.md) 。

<sup>5</sup> hello 儲存體帳戶必須是從 hello 相同的 Azure 訂用帳戶。

<sup>6</sup> 對於不同的 AMS 原則 (例如 Locator 原則或 ContentKeyAuthorizationPolicy) 有 1,000,000 個原則的限制。 

>[!NOTE]
> 您應該使用 hello 如果一律使用相同的原則識別碼 hello 相同天 / 存取權限 / 等等。如需詳細資訊與範例，請參閱[本節](../articles/media-services/media-services-dotnet-manage-entities.md#limit-access-policies)。

<sup>7</sup>如果您要上傳內容 tooan 資產中 Azure Media Services 與 hello 意圖 tooprocess 使用我們的服務中的 hello 媒體處理器之一 （也就是編碼器諸如標準媒體編碼器和媒體編碼器高階工作流程或分析引擎像正面偵測器），則您應該留意 hello hello 最大大小的條件約束。 

自 2017 年 15 hello 支援單一 blob 的最大大小是 195 TB-使用檔案 largers 超過此限制，您的工作將會失敗。 我們正在努力修正 tooaddress 這項限制。 此外，hello 的 hello 資產，如下所示為 hello 最大大小的條件約束。

| 媒體保留單元類型 | 檔案輸入大小 (GB)| 
| --- | --- | 
|S1 | 325|
|S2 | 640|
|S3 | 260|
