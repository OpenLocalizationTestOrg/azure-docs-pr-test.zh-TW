## <a name="what-is-table-storage"></a>什麼是資料表儲存體
Azure 資料表儲存體可儲存大量的結構化資料。 hello 服務是可接受的 NoSQL 資料存放區驗證呼叫從內部和外部 hello Azure 雲端。 Azure 資料表很適合儲存結構化、非關聯式資料。 資料表儲存體的一般用途包括：

* 儲存好幾 TB 的結構化資料，足以供應 Web 規模的應用程式所需
* 儲存資料集，不需要複雜的聯結、外部索引鍵或預存程序，還可以反正規化以加速存取
* 使用叢集索引來快速查詢資料
* 存取 WCF 資料服務.NET 程式庫搭配使用 hello OData 通訊協定和 LINQ 查詢的資料

您可以使用資料表儲存體 toostore 和查詢很大的結構化、 非關聯式資料集，而且您的資料表會延展需求增加時。

## <a name="table-storage-concepts"></a>資料表儲存體概念
資料表儲存體包含下列元件的 hello:

![資料表儲存體元件圖表][Table1]

* **URL 格式：**程式碼使用此位址格式來定位帳戶中的資料表：   
  http://`<storage account>`.table.core.windows.net/`<table>`  
  
  您可以解決 Azure 資料表直接使用此位址以 hello OData 通訊協定。 如需詳細資訊，請參閱 [OData.org][OData.org]。
* **儲存體帳戶：**所有存取的 tooAzure 是儲存體透過儲存體帳戶。 如需關於儲存體帳戶容量的詳細資訊，請參閱＜ [Azure 儲存體延展性和效能目標](../articles/storage/common/storage-scalability-targets.md) ＞(英文)。
* **資料表**：資料表是一組實體。 資料表不強制規定實體的結構描述，這表示單一資料表包含的實體可以有幾組不同的屬性。 hello 儲存體帳戶可以包含的資料表數目只會受到 hello 儲存體帳戶容量限制。
* **實體**： 實體是一組屬性，類似 tooa 資料庫資料列。 實體可以是 up too1MB 的大小。
* **屬性**：屬性是名稱/值組。 每個實體可以包含 too252 屬性 toostore 資料。 每個實體也有 3 個系統屬性，可指定資料分割索引鍵、資料列索引鍵和時間戳記。 Hello 可以更快速地查詢並在不可部分完成的作業中插入/更新相同資料分割索引鍵的實體。 實體的資料列索引鍵是資料分割內的唯一識別碼。

如需有關命名的資料表和屬性的詳細資訊，請參閱[了解 hello 表格服務資料模型](/rest/api/storageservices/Understanding-the-Table-Service-Data-Model)。

[Table1]: ./media/storage-table-concepts-include/table1.png
[OData.org]: http://www.odata.org/
