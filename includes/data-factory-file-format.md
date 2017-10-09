## <a name="specifying-formats"></a>指定格式
Azure Data Factory 支援下列格式類型的 hello:

* [文字格式](#specifying-textformat)
* [JSON 格式](#specifying-jsonformat)
* [Avro 格式](#specifying-avroformat)
* [ORC 格式](#specifying-orcformat)
* [Parquet 格式](#specifying-parquetformat)

### <a name="specifying-textformat"></a>指定 TextFormat
如果您想 tooparse hello 文字檔案，或以文字格式寫入 hello 資料，設定 hello `format` `type`屬性太**TextFormat**。 您也可以指定下列 hello**選擇性**屬性在 hello `format` > 一節。 請參閱[TextFormat 範例](#textformat-example)> 一節有關 tooconfigure。

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| columnDelimiter |hello 字元會在檔案中，使用 tooseparate 資料行。 您可以考慮 toouse 罕見的不可列印字元可能不存在您的資料： 例如指定"\u0001"表示開始的標題 (SOH)。 |只允許一個字元。 hello**預設**值是**逗號 （'，'）**。 <br/><br/>toouse 使用 Unicode 字元，請參閱太[Unicode 字元](https://en.wikipedia.org/wiki/List_of_Unicode_characters)tooget hello 為其對應的程式碼。 |否 |
| rowDelimiter |hello 字元用於 tooseparate 資料列檔案中。 |只允許一個字元。 hello**預設**值可以是任何 hello 讀取下列值： **["\r\n"、"\r"、"\n"]**和**"\r\n"**寫入。 |否 |
| escapeChar |hello 特殊字元都使用資料行分隔符號 tooescape hello 內容的輸入檔中。 <br/><br/>您無法同時為資料表指定 escapeChar 和 quoteChar。 |只允許一個字元。 沒有預設值。 <br/><br/>範例： 如果您以逗號 （'，'） hello 資料行分隔符號，但您想要以 hello 文字 toohave hello 逗號字元 (範例:"Hello，world")，您可以定義為 hello 逸出字元 '$'，並使用字串"Hello$，world hello 來源中。 |否 |
| quoteChar |hello 字元使用 tooquote 字串值。 hello hello 引號字元內的資料行和資料列分隔符號會視為 hello 字串值的一部分。 這個屬性是適用於 tooboth 輸入和輸出資料集。<br/><br/>您無法同時為資料表指定 escapeChar 和 quoteChar。 |只允許一個字元。 沒有預設值。 <br/><br/>比方說，如果您以逗號 （'，'） hello 資料行分隔符號，但您想要以 hello 文字 toohave 逗號字元 (範例： < Hello，world >)，您可以定義"（雙引號） hello 引號字元，並使用 hello 字串"Hello，world"hello 來源中。 |否 |
| nullValue |Toorepresent null 值使用一或多個字元。 |一或多個字元。 hello**預設**有效值**"\N"和"NULL"**在讀取和**"\N"**寫入。 |否 |
| encodingName |指定 hello 編碼名稱。 |有效的編碼名稱。 請參閱 [Encoding.EncodingName 屬性](https://msdn.microsoft.com/library/system.text.encoding.aspx)。 例如：windows-1250 或 shift_jis。 hello**預設**值是**utf-8**。 |否 |
| firstRowAsHeader |指定是否 tooconsider hello 做為標頭的第一個資料列。 對於輸入資料集，Data Factory 會讀取第一個資料列做為標頭。 對於輸出資料集，Data Factory 會寫入第一個資料列做為標頭。 <br/><br/>相關範例案例請參閱[使用 `firstRowAsHeader` 和 `skipLineCount` 的案例](#scenarios-for-using-firstrowasheader-and-skiplinecount)。 |True<br/>**False (預設值)** |否 |
| skipLineCount |從輸入檔讀取資料時，表示 hello tooskip 資料列數目。 如果未指定 skipLineCount 和 firstRowAsHeader，hello 線條會略過第一次，並 hello 標頭資訊從 hello 輸入檔讀取。 <br/><br/>相關範例案例請參閱[使用 `firstRowAsHeader` 和 `skipLineCount` 的案例](#scenarios-for-using-firstrowasheader-and-skiplinecount)。 |Integer |否 |
| treatEmptyAsNull |指定是否 tootreat null 或空字串，以 null 值時從輸入檔讀取資料。 |**True (預設值)**<br/>False |否 |

#### <a name="textformat-example"></a>TextFormat 範例
hello 下列範例顯示 hello 格式內容的某些 TextFormat。

```json
"typeProperties":
{
    "folderPath": "mycontainer/myfolder",
    "fileName": "myblobname",
    "format":
    {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";",
        "quoteChar": "\"",
        "NullValue": "NaN",
        "firstRowAsHeader": true,
        "skipLineCount": 0,
        "treatEmptyAsNull": true
    }
},
```

toouse`escapeChar`而不是`quoteChar`，取代與 hello 一行`quoteChar`以下列的 escapeChar hello:

```json
"escapeChar": "$",
```

#### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a>使用 firstRowAsHeader 和 skipLineCount 的案例
* 您要從非檔案來源 tooa 文字檔案複製，並希望 tooadd 包含 hello 結構描述中繼資料標頭的資料行 (例如： SQL 結構描述)。 指定`firstRowAsHeader`hello 輸出資料集，在此案例中為 true。
* 您要從文字檔，其中包含的標頭列 tooa 非檔案接收複製，而且想要線條的 toodrop。 指定`firstRowAsHeader`hello 輸入資料集，則為 true。
* 您要複製的文字檔案，並想 tooskip hello 開頭沒有包含任何資料或標頭資訊的幾行。 指定`skipLineCount`tooindicate hello 數行 toobe 略過。 如果 hello 檔案的其餘部分 hello 包含標頭行，您也可以指定`firstRowAsHeader`。 如果兩個`skipLineCount`和`firstRowAsHeader`和指定的會先略過 hello 行 hello 標頭資訊然後讀取 hello 輸入檔

### <a name="specifying-jsonformat"></a>指定 JsonFormat
太**匯入/匯出 JSON 檔案儲存為-至 / 從 Azure Cosmos DB**，請參閱[匯入/匯出 JSON 文件](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents)hello Azure Cosmos DB 連接器與詳細資料 > 一節。

如果您想 tooparse hello JSON 檔案，或將 JSON 格式寫入 hello 資料，設定 hello `format` `type`屬性太**JsonFormat**。 您也可以指定下列 hello**選擇性**屬性在 hello `format` > 一節。 請參閱[JsonFormat 範例](#jsonformat-example)> 一節有關 tooconfigure。

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| filePattern |表示 hello 模式，每個 JSON 檔案中儲存的資料。 允許的值為︰**setOfObjects** 和 **arrayOfObjects**。 hello**預設**值是**setOfObjects**。 關於這些模式的詳細資訊，請參閱 [JSON 檔案模式](#json-file-patterns)一節。 |否 |
| jsonNodeReference | 如果您想 tooiterate 從陣列中的 hello 物件擷取資料欄位與 hello 相同模式中，指定該陣列的 hello JSON 路徑。 從 JSON 檔案複製資料時，才支援這個屬性。 | 否 |
| jsonPathDefinition | 自訂資料行名稱 （開始使用小寫） 指定每個資料行對應的 hello JSON 路徑運算式。 從 JSON 檔案複製資料時，才支援這個屬性，您可以從物件或陣列中擷取資料。 <br/><br/> 在根物件的欄位，啟動以根 $;針對所選擇的 hello 陣列內的欄位`jsonNodeReference`屬性，開始從 hello 陣列項目。 請參閱[JsonFormat 範例](#jsonformat-example)> 一節有關 tooconfigure。 | 否 |
| encodingName |指定 hello 編碼名稱。 Hello 有效編碼名稱清單，請參閱： [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx)屬性。 例如：windows-1250 或 shift_jis。 hello**預設**值是： **utf-8**。 |否 |
| nestingSeparator |為使用的 tooseparate 巢狀層級的字元。 hello 預設值是 '。 '（點）。 |否 |

#### <a name="json-file-patterns"></a>JSON 檔案模式

複製活動可以剖析的 JSON 檔案模式如下︰

- **類型 I：setOfObjects**

    每個檔案都會包含單一物件，或以行分隔/串連的多個物件。 在輸出資料集中選擇此選項時，複製活動會產生單一 JSON 檔案，每行一個物件 (以行分隔)。

    * **單一物件 JSON 範例**

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        ```

    * **以行分隔的 JSON 範例**

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * **串連的 JSON 範例**

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        }
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
        ```

- **類型 II：arrayOfObjects**

    每個檔案都會包含物件的陣列。

    ```json
    [
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        },
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        },
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
    ]
    ```

#### <a name="jsonformat-example"></a>JsonFormat 範例

**案例 1︰從 JSON 檔案複製資料**

JSON 檔案中複製資料時，請參閱下列兩種類型的範例與 hello 泛型點 toonote:

**範例 1︰從物件和陣列擷取資料**

在此範例中，您可以預期 toosingle 表格式結果中的記錄會對應一個根 JSON 物件。 如果您有在 JSON 檔案以 hello 下列內容：  

```json
{
    "id": "ed0e4960-d9c5-11e6-85dc-d7996816aad3",
    "context": {
        "device": {
            "type": "PC"
        },
        "custom": {
            "dimensions": [
                {
                    "TargetResourceType": "Microsoft.Compute/virtualMachines"
                },
                {
                    "ResourceManagmentProcessRunId": "827f8aaa-ab72-437c-ba48-d8917a7336a3"
                },
                {
                    "OccurrenceTime": "1/13/2017 11:24:37 AM"
                }
            ]
        }
    }
}
```
而且您想的 toocopy 到 Azure SQL 中的資料表 hello 下列格式，從物件和陣列中擷取資料：

| id | deviceType | targetResourceType | resourceManagmentProcessRunId | occurrenceTime |
| --- | --- | --- | --- | --- |
| ed0e4960-d9c5-11e6-85dc-d7996816aad3 | PC | Microsoft.Compute/virtualMachines | 827f8aaa-ab72-437c-ba48-d8917a7336a3 | 1/13/2017 11:24:37 AM |

hello 與輸入資料集**JsonFormat**類型的定義如下: （與 hello 相關部分的部分定義）。 具體而言：

- `structure`區段會定義自訂的 hello 資料行名稱和 hello 對應的資料類型轉換 tootabular 資料時。 這個區段是**選擇性**除非需要 toodo 資料行對應。 如需詳細資訊，請參閱[指定矩形資料集的結構定義](#specifying-structure-definition-for-rectangular-datasets)一節。
- `jsonPathDefinition`指定每個資料行會指出其中 tooextract hello 資料 hello JSON 路徑。 從陣列 toocopy 資料，您可以使用**陣列 [x].property** tooextract 的 hello hello x 次物件，或您從給定屬性的值可以使用**陣列 [*].property** toofindhello 任何物件，其中包含這類屬性的值。

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "deviceType",
            "type": "String"
        },
        {
            "name": "targetResourceType",
            "type": "String"
        },
        {
            "name": "resourceManagmentProcessRunId",
            "type": "String"
        },
        {
            "name": "occurrenceTime",
            "type": "DateTime"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonPathDefinition": {"id": "$.id", "deviceType": "$.context.device.type", "targetResourceType": "$.context.custom.dimensions[0].TargetResourceType", "resourceManagmentProcessRunId": "$.context.custom.dimensions[1].ResourceManagmentProcessRunId", "occurrenceTime": " $.context.custom.dimensions[2].OccurrenceTime"}      
        }
    }
}
```

**範例 2： 跨套用多個具有相同模式陣列中的 hello 物件**

在此範例中，您可以預期 tootransform 一個根 JSON 物件表格式結果中的多個記錄。 如果您有在 JSON 檔案以 hello 下列內容：  

```json
{
    "ordernumber": "01",
    "orderdate": "20170122",
    "orderlines": [
        {
            "prod": "p1",
            "price": 23
        },
        {
            "prod": "p2",
            "price": 13
        },
        {
            "prod": "p3",
            "price": 231
        }
    ],
    "city": [ { "sanmateo": "No 1" } ]
}
```
您想的 toocopy 到 Azure SQL 中的資料表 hello 下列格式的扁平化 hello hello 陣列內的資料及交叉聯結使用 hello 常見的根目錄資訊和：

| ordernumber | orderdate | order_pd | order_price | city |
| --- | --- | --- | --- | --- |
| 01 | 20170122 | P1 | 23 | [{"sanmateo":"No 1"}] |
| 01 | 20170122 | P2 | 13 | [{"sanmateo":"No 1"}] |
| 01 | 20170122 | P3 | 231 | [{"sanmateo":"No 1"}] |

hello 與輸入資料集**JsonFormat**類型的定義如下: （與 hello 相關部分的部分定義）。 具體而言：

- `structure`區段會定義自訂的 hello 資料行名稱和 hello 對應的資料類型轉換 tootabular 資料時。 這個區段是**選擇性**除非需要 toodo 資料行對應。 如需詳細資訊，請參閱[指定矩形資料集的結構定義](#specifying-structure-definition-for-rectangular-datasets)一節。
- `jsonNodeReference`表示以相同模式下的 hello hello 物件的 tooiterate 和擷取資料**陣列**訂單產品線。
- `jsonPathDefinition`指定每個資料行會指出其中 tooextract hello 資料 hello JSON 路徑。 在此範例中，""、"orderdate"和"city"正在根物件具有開頭為"$"。，"order_pd"和"order_price 」 定義衍生自不含"$"。 hello 陣列項目路徑時的 JSON 路徑。

```json
"properties": {
    "structure": [
        {
            "name": "ordernumber",
            "type": "String"
        },
        {
            "name": "orderdate",
            "type": "String"
        },
        {
            "name": "order_pd",
            "type": "String"
        },
        {
            "name": "order_price",
            "type": "Int64"
        },
        {
            "name": "city",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonNodeReference": "$.orderlines",
            "jsonPathDefinition": {"ordernumber": "$.ordernumber", "orderdate": "$.orderdate", "order_pd": "prod", "order_price": "price", "city": " $.city"}         
        }
    }
}
```

**請注意下列點 hello:**

* 如果 hello`structure`和`jsonPathDefinition`中未定義 hello Data Factory 的資料集，hello 複製活動會偵測 hello 從 hello 第一個物件的結構描述，以及將扁平化 hello 整個物件。
* Hello JSON 輸入中有一個陣列，如果預設 hello 複製活動 hello 整個陣列將值轉換成字串。 您可以選擇使用 tooextract 資料`jsonNodeReference`及/或`jsonPathDefinition`，或未指定在略過它`jsonPathDefinition`。
* 如果有重複名稱在 hello 相同層級，hello 複製活動會挑選 hello 最後一個。
* 屬性名稱會區分大小寫。 名稱相同但大小寫不同的兩個屬性會被視為兩個不同的屬性。

**案例 2： 寫入資料 tooJSON 檔案**

如果您在 SQL Database 中有下列資料表︰

| id | order_date | order_price | order_by |
| --- | --- | --- | --- |
| 1 | 20170119 | 2000 | David |
| 2 | 20170120 | 3500 | Patrick |
| 3 | 20170121 | 4000 | Jason |

與每個記錄，您會預期 toowrite tooa JSON 物件中的格式如下：
```json
{
    "id": "1",
    "order": {
        "date": "20170119",
        "price": 2000,
        "customer": "David"
    }
}
```

hello 輸出資料集與**JsonFormat**類型的定義如下: （與 hello 相關部分的部分定義）。 更具體來說，`structure`區段會定義目的地檔案中的 hello 自訂屬性名稱`nestingSeparator`(預設值是"。") 將會使用的 tooidentify hello 巢狀層級從 hello 名稱。 這個區段是**選擇性**除非您想要比較的來源資料行名稱，toochange hello 屬性名稱，或是巢狀化某些 hello 屬性。

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "order.date",
            "type": "String"
        },
        {
            "name": "order.price",
            "type": "Int64"
        },
        {
            "name": "order.customer",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat"
        }
    }
}
```

### <a name="specifying-avroformat"></a>指定 AvroFormat
如果您想 tooparse hello Avro 檔案，或寫入 Avro 格式中的 hello 資料，設定 hello `format` `type`屬性太**AvroFormat**。 您不需要 toospecify hello typeProperties 區段中的 hello 格式 > 一節中的任何屬性。 範例：

```json
"format":
{
    "type": "AvroFormat",
}
```

toouse Avro 格式的 Hive 資料表中，您可以使用參照太[Apache Hive 教學課程](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe)。

請注意下列點 hello:  

* 不支援[複雜資料類型](http://avro.apache.org/docs/current/spec.html#schema_complex) (記錄、列舉、陣列、對應、等位和固定)。

### <a name="specifying-orcformat"></a>指定 OrcFormat
如果您想 tooparse hello ORC 檔案，或寫入 ORC 格式中的 hello 資料，設定 hello `format` `type`屬性太**OrcFormat**。 您不需要 toospecify hello typeProperties 區段中的 hello 格式 > 一節中的任何屬性。 範例：

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> 如果您不複製 ORC 檔案**為-是**在內部部署和雲端之間資料存放區，您需要在閘道機器上的 tooinstall hello JRE 8 (Java Runtime Environment)。 64 位元閘道需要 64 位元 JRE，而 32 位元閘道需要 32 位元 JRE。 您可以從 [這裡](http://go.microsoft.com/fwlink/?LinkId=808605)找到這兩個版本。 請選擇適當的一個 hello。
>
>

請注意下列點 hello:

* 不支援複雜資料類型 (STRUCT、MAP、LIST、UNION)
* ORC 檔案有 3 種 [壓縮相關選項](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/)︰NONE、ZLIB、SNAPPY。 Data Factory 支援以這些壓縮格式的任一項從 ORC 檔案讀取資料。 它會使用 hello 壓縮轉碼器是 hello 中繼資料 tooread hello 資料中。 不過，在撰寫 tooan ORC 檔案時，Data Factory 選擇 ZLIB，ORC hello 預設值。 目前沒有任何選項 toooverride 這種行為。

### <a name="specifying-parquetformat"></a>指定 ParquetFormat
如果您想 tooparse hello Parquet 檔案，或寫入 Parquet 格式中的 hello 資料，設定 hello `format` `type`屬性太**ParquetFormat**。 您不需要 toospecify hello typeProperties 區段中的 hello 格式 > 一節中的任何屬性。 範例：

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> 如果您不複製 Parquet 檔案**為-是**在內部部署和雲端之間資料存放區，您需要在閘道機器上的 tooinstall hello JRE 8 (Java Runtime Environment)。 64 位元閘道需要 64 位元 JRE，而 32 位元閘道需要 32 位元 JRE。 您可以從 [這裡](http://go.microsoft.com/fwlink/?LinkId=808605)找到這兩個版本。 請選擇適當的一個 hello。
>
>

請注意下列點 hello:

* 不支援複雜資料類型 (MAP、LIST)
* Parquet 檔案具有下列相關的壓縮選項的 hello: NONE、 SNAPPY、 GZIP、 和 LZO。 Data Factory 支援以這些壓縮格式的任一項從 ORC 檔案讀取資料。 它使用 hello 中繼資料 tooread hello 資料中的 hello 壓縮轉碼器。 不過，在撰寫 tooa Parquet 檔案時，Data Factory 選擇 SNAPPY，hello Parquet 格式的預設值。 目前沒有任何選項 toooverride 這種行為。
