## <a name="specifying-structure-definition-for-rectangular-datasets"></a>指定矩形資料集的結構定義
hello hello 資料集 JSON 結構區段是**選擇性**矩形的資料表 （資料列和資料行） 區段，並包含 hello 資料表的資料行集合。 您將使用類型轉換的其中一個提供的類型資訊或執行資料行對應 hello 結構 > 一節。 hello 下列各節說明這些功能的詳細資料。 

每個資料行包含下列屬性的 hello:

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 名稱 |Hello 資料行名稱。 |是 |
| 類型 |Hello 資料行資料類型。 有關何時應指定類型資訊的詳細資訊，請參閱下文類型轉換的部份 |否 |
| culture |.NET 基礎類型指定且為.NET 型別 Datetime 或 Datetimeoffset 時使用的文化特性 toobe。 預設值為 “en-us”。 |否 |
| format |格式化字串 toobe 時指定了型別，且是 Datetime 或 Datetimeoffset 的.NET 類型使用。 |否 |

hello 下列範例顯示一份含有三個資料行的使用者識別碼、 名稱和 lastlogindate 的 hello 結構區段 JSON。

```json
"structure": 
[
    { "name": "userid"},
    { "name": "name"},
    { "name": "lastlogindate"}
],
```

請使用下列指導方針時 hello tooinclude 「 結構 」 資訊和 hello 中的哪些 tooinclude**結構**> 一節。

* **結構化的資料來源的**商店以及 hello 資料本身 （SQL Server、 Oracle、 Azure 資料表等這類來源），您應該指定 hello 「 結構 」 一節，只有當您想執行的特定的資料行對應的資料結構描述和類型資訊toospecific 中接收和其名稱的資料行的來源資料行不 hello 相同 （請參閱以下的資料行對應一節中的詳細資料）。 
  
    如上面所述，hello 類型資訊是選擇性的 「 結構 」 一節。 結構化的來源類型資訊已可使用 hello 資料存放區中的資料集定義的一部分，因此您不應該包含型別資訊包括 hello 「 結構 」 一節時。
* **讀取的資料來源 (特別是 Azure blob) 的結構描述**您可以選擇 toostore 資料，而不儲存任何結構描述或型別資訊與 hello 資料。 這些類型的資料來源中 hello 遵循 2 的情況下應包含 「 結構 」:
  * 您想 toodo 資料行對應。
  * 複製活動中的來源 hello 資料集時，您可以提供 「 結構 」 中的類型資訊和資料處理站將用於轉換 toonative 類型 hello 接收的此類型資訊。 請參閱[從 Azure Blob 中移動資料 tooand](../articles/data-factory/data-factory-azure-blob-connector.md)文件以取得詳細資訊。

### <a name="supported-net-based-types"></a>支援 .NET 型的類型
資料處理站支援 hello 遵循符合 CLS 標準的.NET 為基礎來讀取的資料來源，例如 Azure blob 上的結構描述提供 「 結構 」 中的類型資訊的型別值。

* Int16
* Int32 
* Int64
* 單一
* 兩倍
* 十進位
* Byte[]
* Bool
* String 
* Guid
* Datetime
* Datetimeoffset
* Timespan 

Datetime 和 Datetimeoffset 您也可以選擇指定"culture"&"format"字串 toofacilitate 剖析自訂的日期時間字串。 請參閱下方的類型轉換範例。

