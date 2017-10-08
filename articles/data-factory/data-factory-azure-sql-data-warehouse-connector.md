---
title: "aaaCopy 資料從 Azure SQL 資料倉儲的 / |Microsoft 文件"
description: "深入了解如何使用 Azure Data Factory 的 Azure SQL 資料倉儲中的 toocopy 資料"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: d90fa9bd-4b79-458a-8d40-e896835cfd4a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 75bfcf3c99844fc1297ca500107da23cf875e41f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-data-warehouse-using-azure-data-factory"></a>從 Azure SQL 資料倉儲使用 Azure Data Factory 複製資料 tooand
本文說明如何 toouse hello Azure Data Factory toomove 資料從 Azure SQL 資料倉儲中的複製活動。 它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。  

> [!TIP]
> tooachieve 最佳效能，使用 PolyBase tooload 資料到 Azure SQL 資料倉儲。 hello[使用 PolyBase tooload 資料到 Azure SQL 資料倉儲](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse)> 一節有詳細資料。 如需使用案例的逐步解說，請參閱[使用 Azure Data Factory 在 15 分鐘內將 1 TB 載入至 Azure SQL 資料倉儲](data-factory-load-sql-data-warehouse.md)。

## <a name="supported-scenarios"></a>支援的案例
您可以將資料複製**從 Azure SQL 資料倉儲**toohello 下列資料存放區：

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

您可以將資料複製下列資料存放區的 hello **tooAzure SQL 資料倉儲**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!TIP]
> 從 SQL Server 或 Azure SQL Database tooAzure 複製資料時 SQL 資料倉儲，如果 hello 資料表不存在於 hello 目的地存放區，資料處理站可以自動建立 hello 資料表在 SQL 資料倉儲中使用 hello 來源中的 hello hello 資料表結構描述資料存放區。 請參閱[自動建立資料表](#auto-table-creation)以取得詳細資料。

## <a name="supported-authentication-type"></a>支援的驗證類型
Azure SQL 資料倉儲連接器支援基本驗證。

## <a name="getting-started"></a>開始使用
您可以藉由使用不同的工具/API，建立內含複製活動的管線，以將資料移進/移出「Azure SQL 資料倉儲」。

最簡單方式 toocreate hello 管線可將資料從 Azure SQL 資料倉儲複製是 toouse hello 複製資料精靈 」。 請參閱[教學課程： 將資料載入 SQL 資料倉儲與 Data Factory](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。

您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。 請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。

無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:

1. 建立 **Data Factory**。 資料處理站可包含一或多個管線。 
2. 建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。 例如，如果您從 Azure blob 儲存體 tooan Azure SQL 資料倉儲中複製資料，您建立兩個連結的服務 toolink 您的 Azure 儲存體帳戶和 Azure SQL 資料倉儲 tooyour 資料 factory。 連結的服務是特定 tooAzure SQL 資料倉儲的內容，請參閱[連結服務屬性](#linked-service-properties)> 一節。 
3. 建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。 在 hello hello 最後一個步驟中所述的範例中，您可以建立資料集 toospecify hello blob 容器和包含 hello 輸入的資料的資料夾。 而且，您建立另一個資料集 toospecify hello 資料表保存 hello 資料複製 hello blob 儲存體中的 hello Azure SQL 資料倉儲中。 如為特定 tooAzure SQL 資料倉儲的資料集屬性，請參閱[資料集屬性](#dataset-properties)> 一節。
4. 建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。 在先前所述 hello 範例中，您使用 BlobSource 作為來源和 SqlDWSink 做為接收器 hello 複製活動。 同樣地，如果您要複製 Azure SQL 資料倉儲 tooAzure Blob 儲存體，您使用 SqlDWSource 和 BlobSink hello 複製活動中。 複製活動是特定 tooAzure SQL 資料倉儲的屬性，請參閱[複製活動屬性](#copy-activity-properties)> 一節。 如需如何 toouse 的資料存放區做為來源或接收的詳細資訊，按一下 hello hello 資料存放區上一節中的連結。

當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。 當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。  如需使用的 toocopy 資料至 azure 或從 Azure SQL 資料倉儲的 Data Factory 實體的 JSON 定義的範例，請參閱[JSON 範例](#json-examples-for-copying-data-to-and-from-sql-data-warehouse)本文一節。

hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooAzure SQL 資料倉儲的 JSON 屬性的詳細資料：

## <a name="linked-service-properties"></a>連結服務屬性
下表中的 hello 提供 JSON 項目特定 tooAzure SQL 資料倉儲連結服務的描述。

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 類型 |hello 類型屬性必須設定為： **AzureSqlDW** |是 |
| connectionString |指定所需的資訊 tooconnect toohello Azure SQL 資料倉儲執行個體 hello connectionString 屬性。 僅支援基本驗證。 |是 |

> [!IMPORTANT]
> 設定[Azure SQL Database 防火牆](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure)太 hello 資料庫伺服器和[允許 Azure 服務 tooaccess hello 伺服器](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure)。 此外，如果您要從內部部署資料來源與資料處理站閘道外部 Azure 包括複製資料 tooAzure SQL 資料倉儲，設定正在傳送資料 tooAzure SQL 資料倉儲的 hello 機器的適當 IP 位址範圍。

## <a name="dataset-properties"></a>資料集屬性
區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。 資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。

hello typeProperties 章節是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置的相關資訊。 hello **typeProperties** hello 資料集的類型 > 一節**AzureSqlDWTable**具有下列屬性的 hello:

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| tableName |參照 hello 資料表或檢視 hello 連結的服務的 hello Azure SQL 資料倉儲資料庫中的名稱。 |是 |

## <a name="copy-activity-properties"></a>複製活動屬性
區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。 屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。

> [!NOTE]
> hello 複製活動會採用只有 1 個輸入，並產生一個輸出。

而 hello 活動 hello typeProperties 區段中可用的屬性會隨每個活動類型。 複製活動它們而異的來源與接收的 hello 類型。

### <a name="sqldwsource"></a>SqlDWSource
當來源屬於型別**SqlDWSource**中的下列屬性的 hello 可用**typeProperties** > 一節：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| SqlReaderQuery |使用自訂查詢 tooread hello 的資料。 |SQL 查詢字串。 例如：select * from MyTable。 |否 |
| sqlReaderStoredProcedureName |名稱的 hello 預存程序會從 hello 來源資料表讀取資料。 |名稱的 hello 預存程序。 hello 最後一個 SQL 陳述式必須在 hello 預存程序中的 SELECT 陳述式。 |否 |
| storedProcedureParameters |Hello 參數，預存程序。 |名稱/值組。 名稱和大小寫的參數必須符合 hello 名稱和大小寫的 hello 預存程序參數。 |否 |

如果 hello **sqlReaderQuery**指定 hello SqlDWSource，hello 複製活動與 hello Azure SQL 資料倉儲來源 tooget hello 資料執行此查詢。

或者，您可以指定預存程序，藉由指定 hello **sqlReaderStoredProcedureName**和**storedProcedureParameters** （如果 hello 預存程序會採用參數）。

如果您未指定 sqlReaderQuery 或 sqlReaderStoredProcedureName，hello hello 資料集 JSON hello 結構區段中定義的資料行是使用的 toobuild 針對 hello Azure SQL 資料倉儲查詢 toorun。 範例：`select column1, column2 from mytable`. 如果您不需要 hello 資料集定義 hello 結構，所有資料行選取的 hello 資料表。

#### <a name="sqldwsource-example"></a>SqlDWSource 範例

```JSON
"source": {
    "type": "SqlDWSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```
**hello 預存程序定義：**

```SQL
CREATE PROCEDURE CopyTestSrcStoredProcedureWithParameters
(
    @stringData varchar(20),
    @identifier int
)
AS
SET NOCOUNT ON;
BEGIN
     select *
     from dbo.UnitTestSrcTable
     where dbo.UnitTestSrcTable.stringData != stringData
    and dbo.UnitTestSrcTable.identifier != identifier
END
GO
```

### <a name="sqldwsink"></a>管線
**SqlDWSink**支援 hello 下列屬性：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| sqlWriterCleanupScript |複製活動 tooexecute 查詢指定的特定配量的資料清除。 如需詳細資訊，請參閱 [可重複性](#repeatability-during-copy)一節。 |查詢陳述式。 |否 |
| allowPolyBase |指出是否 toouse PolyBase （如果適用的話），而不是 BULKINSERT 機制。 <br/><br/> **使用 PolyBase 是建議的方式 tooload 資料到 SQL 資料倉儲的 hello。** 請參閱[使用 PolyBase tooload 資料到 Azure SQL 資料倉儲](#use-polybase-to-load-data-into-azure-sql-data-warehouse)條件約束和詳細資料 > 一節。 |True <br/>FALSE (預設值) |否 |
| polyBaseSettings |一組屬性，可指定當 hello **allowPolybase**屬性設定太**true**。 |&nbsp; |否 |
| rejectValue |指定 hello 數目或百分比的 hello 查詢失敗前，可能會拒絕的資料列。 <br/><br/>深入了解 hello PolyBase 拒絕之選項的 hello**引數**區段[CREATE EXTERNAL TABLE (TRANSACT-SQL)](https://msdn.microsoft.com/library/dn935021.aspx)主題。 |0 (預設值)、1、2、… |否 |
| rejectType |指定是否要將 hello rejectValue 選項指定為常值或百分比。 |值 (預設值)、百分比 |否 |
| rejectSampleValue |決定 hello 數量的資料列 tooretrieve hello PolyBase 重新計算 hello 百分比的已拒絕的資料列之前。 |1、2、… |是，如果 **rejectType** 是 **percentage** |
| useTypeDefault |指定如何 toohandle 遺漏值中的分隔的文字檔案 PolyBase hello 文字檔案中擷取的資料時。<br/><br/>深入了解來自 hello 引數 > 一節中的這個屬性[CREATE EXTERNAL FILE FORMAT (TRANSACT-SQL)](https://msdn.microsoft.com/library/dn935026.aspx)。 |True/False (預設值為 False) |否 |
| writeBatchSize |用戶端 hello 緩衝區的大小達到叫用 writeBatchSize 時，將資料插入 hello SQL 資料表 |整數 (資料列數目) |否 (預設值：10000) |
| writeBatchTimeout |在逾時之前，請等待 hello 批次插入作業 toocomplete 時間。 |時間範圍<br/><br/> 範例：“00:30:00” (30 分鐘)。 |否 |

#### <a name="sqldwsink-example"></a>SqlDWSink 範例

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true
}
```

## <a name="use-polybase-tooload-data-into-azure-sql-data-warehouse"></a>使用 PolyBase tooload 資料到 Azure SQL 資料倉儲
使用 [PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide) 是以高輸送量將大量資料載入 Azure SQL 資料倉儲的有效方法。 您可以看到 hello 輸送量較大提高而不是 hello 預設 BULKINSERT 機制使用 PolyBase。 請參閱[複製效能參考編號](data-factory-copy-activity-performance.md#performance-reference)了解詳細的比較。 如需使用案例的逐步解說，請參閱[使用 Azure Data Factory 在 15 分鐘內將 1 TB 載入至 Azure SQL 資料倉儲](data-factory-load-sql-data-warehouse.md)。

* 如果您的來源資料位於**Azure Blob 或 Azure Data Lake Store**，和 hello 格式相容，使用 PolyBase，您可以直接複製的 tooAzure 使用 PolyBase 的 SQL 資料倉儲。 請參閱**[使用 PolyBase 直接複製](#direct-copy-using-polybase)**了解詳細資料。
* 如果您的來源資料存放區和格式不原本支援 PolyBase，您可以使用 hello **[接移的複本，使用 PolyBase](#staged-copy-using-polybase)** 改用功能。 它也提供更佳的輸送量會自動將 hello 資料轉換成 PolyBase 相容的格式，並將 hello 資料儲存在 Azure Blob 儲存體。 然後，它會將資料載入 SQL 資料倉儲。

設定 hello`allowPolyBase`屬性太**true** hello 遵循範例中的 Azure Data Factory toouse PolyBase toocopy 資料到 Azure SQL 資料倉儲中所示。 當您設定 allowPolyBase tootrue 時，您可以指定 PolyBase 特定屬性使用 hello`polyBaseSettings`屬性群組。 請參閱 hello [SqlDWSink](#SqlDWSink)如需詳細資訊，您可以使用 polyBaseSettings 屬性 > 一節。

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true,
    "polyBaseSettings":
    {
        "rejectType": "percentage",
        "rejectValue": 10.0,
        "rejectSampleValue": 100,
        "useTypeDefault": true
    }
}
```

### <a name="direct-copy-using-polybase"></a>使用 PolyBase 直接複製
SQL 資料倉儲 PolyBase 直接支援 Azure Blob 和 Azure Data Lake Store (使用服務主體) 做為來源與特定檔案格式需求。 如果您的來源資料符合本節所述的 hello 準則，您可以直接從來源資料存放區 tooAzure 使用 PolyBase 的 SQL 資料倉儲中複製。 否則，您可以使用 [使用 PolyBase 分段複製](#staged-copy-using-polybase)。

> [!TIP]
> 從資料倉儲的資料湖存放區 tooSQL toocopy 資料有效，進一步了解從[Azure Data Factory 可讓它使用 SQL 資料倉儲中的資料湖存放區時，即使資料更容易及方便 toouncover insights](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/)。

如果不符合 hello 需求，Azure Data Factory 會檢查 hello 設定，並自動回復 toohello BULKINSERT hello 資料移動機制。

1. 「來源已連結服務」的類型為：AzureStorage 或具備服務主題驗證的 AzureDataLakeStore。  
2. hello**輸入資料集**的型別： **AzureBlob**或**AzureDataLakeStore**，和 hello 底下的格式類型`type`屬性是**OrcFormat**，或**TextFormat**以 hello 的設定：

   1. `rowDelimiter` 必須是 **\n**。
   2. `nullValue`設定得**空字串**("")，或`treatEmptyAsNull`設定得**true**。
   3. `encodingName`設定得**utf-8**，也就是**預設**值。
   4. 未指定 `escapeChar`、`quoteChar`、`firstRowAsHeader` 和 `skipLineCount`。
   5. `compression` 可以是「無壓縮」、**GZip** 或 **Deflate**。

    ```JSON
    "typeProperties": {
       "folderPath": "<blobpath>",
       "format": {
           "type": "TextFormat",     
           "columnDelimiter": "<any delimiter>",
           "rowDelimiter": "\n",       
           "nullValue": "",           
           "encodingName": "utf-8"    
       },
       "compression": {  
           "type": "GZip",  
           "level": "Optimal"  
       }  
    },
    ```

3. 沒有任何`skipHeaderLineCount`底下**BlobSource**或**AzureDataLakeStore** hello 管線中的複製活動。
4. 沒有任何`sliceIdentifierColumnName`底下**SqlDWSink** hello 管線中的複製活動。 (PolyBase 保證所有資料都已更新，或在單一執行未更新任何項目。 tooachieve**重複性**，您可以使用`sqlWriterCleanupScript`)。
5. 沒有任何`columnMapping`用於複製活動中相關聯的 hello。

### <a name="staged-copy-using-polybase"></a>使用 PolyBase 分段複製
當您的來源資料不符合 hello 上一節中導入的 hello 準則時，您可以啟用透過暫時臨時 Azure Blob 儲存體 （不能是進階儲存體） 複製資料。 在此情況下，Azure Data Factory 自動 hello 資料 toomeet 資料格式需求 PolyBase，然後再使用 PolyBase tooload 資料到 SQL 資料倉儲上執行轉換，並在上次清除暫存資料從 hello Blob 儲存體。 如需透過暫存 Azure Blob 複製資料通常如何運作的詳細資訊，請參閱 [分段複製](data-factory-copy-activity-performance.md#staged-copy) 。

> [!NOTE]
> 當複製資料的內部資料儲存到 Azure SQL 資料倉儲使用 PolyBase，而且準備後，如果您的資料管理閘道器版本低於 2.4，JRE (Java Runtime Environment) 需要您的閘道機器的來源資料是使用的 tootransform成適當格式。 建議您升級閘道 toohello 的最新 tooavoid 這類相依性。
>

此功能 toouse，建立[Azure 儲存體連結服務](data-factory-azure-blob-connector.md#azure-storage-linked-service)參考 toohello 具有 hello 過渡版的 blob 儲存體的 Azure 儲存體帳戶，然後指定 hello`enableStaging`和`stagingSettings`hello 複製活動的屬性hello，下列程式碼所示：

```json
"activities":[  
{
    "name": "Sample copy activity from SQL Server tooSQL Data Warehouse via PolyBase",
    "type": "Copy",
    "inputs": [{ "name": "OnpremisesSQLServerInput" }],
    "outputs": [{ "name": "AzureSQLDWOutput" }],
    "typeProperties": {
        "source": {
            "type": "SqlSource",
        },
        "sink": {
            "type": "SqlDwSink",
            "allowPolyBase": true
        },
        "enableStaging": true,
        "stagingSettings": {
            "linkedServiceName": "MyStagingBlob"
        }
    }
}
]
```

## <a name="best-practices-when-using-polybase"></a>使用 PolyBase 時的最佳作法
hello 下列各節提供額外的最佳作法 toohello 中提及的[Azure SQL 資料倉儲的最佳作法](../sql-data-warehouse/sql-data-warehouse-best-practices.md)。

### <a name="required-database-permission"></a>必要的資料庫權限
它 toouse PolyBase，需要 hello 使用者正在使用的 tooload 資料到 SQL 資料倉儲具有 hello [「 控制 」 權限](https://msdn.microsoft.com/library/ms191291.aspx)hello 目標資料庫上。 其中一種方式是 tooadd 的 tooachieve"db_owner 」 角色的成員身分的使用者。 深入了解如何 toodo，依照[本節](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization)。

### <a name="row-size-and-data-type-limitation"></a>資料列大小和資料類型限制
Polybase 載入受到 tooloading 資料列都小於**1MB**而且無法載入 tooVARCHR(MAX)，nvarchar （max） 或 varbinary （max）。 請參閱太[這裡](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads)。

如果您有來源資料與資料列的大小大於 1 MB，您可能為每一個函數 hello 最大資料列大小未超過 hello 限制的數個小型的垂直想 toosplit hello 來源資料表。 使用 PolyBase 和 Azure SQL 資料倉儲中合併在一起，可以接著載入 hello 較小的資料表。

### <a name="sql-data-warehouse-resource-class"></a>SQL 資料倉儲資源類別
tooachieve 最佳可能輸送量，請考慮 tooassign 較大資源類別 toohello 使用者正在使用 tooload 資料到透過 PolyBase 的 SQL 資料倉儲。 深入了解如何 toodo，依照[變更使用者資源類別範例](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example)。

### <a name="tablename-in-azure-sql-data-warehouse"></a>Azure SQL 資料倉儲中的 tableName
hello 下表提供的範例如何 toospecify hello **tableName**中資料集的結構描述和資料表名稱的各種組合的 JSON 屬性。

| DB 結構描述 | 資料表名稱 | tableName JSON 屬性 |
| --- | --- | --- |
| dbo |MyTable |MyTable 或 dbo.MyTable 或 [dbo].[MyTable] |
| dbo1 |MyTable |dbo1.MyTable 或 [dbo1].[MyTable] |
| dbo |My.Table |[My.Table] 或 [dbo].[My.Table] |
| dbo1 |My.Table |[dbo1].[My.Table] |

如果您看到下列錯誤 hello，它可能與您指定 hello tableName 屬性 hello 值的問題。 請參閱 hello 表 hello hello tableName JSON 屬性的正確方式 toospecify 值。  

```
Type=System.Data.SqlClient.SqlException,Message=Invalid object name 'stg.Account_test'.,Source=.Net SqlClient Data Provider
```

### <a name="columns-with-default-values"></a>包含預設值的資料行
PolyBase Data Factory 中的功能只接受目前 hello 與 hello 目標資料表的資料行數目相同。 假設您有內含四個資料行的資料表，且其中一個資料行已使用預設值進行定義。 hello 輸入的資料應仍包含四個資料行。 提供 3 個資料行的輸入資料集，會產生錯誤類似 toohello 下列訊息：

```
All columns of hello table must be specified in hello INSERT BULK statement.
```
NULL 值是一種特殊形式的預設值。 如果 hello 資料行是可為 null，hello 輸入中的資料 （blob) 針對該資料行可能是空白 （無法遺漏 hello 輸入資料集）。 PolyBase hello Azure SQL 資料倉儲中將它們都是 NULL。  

## <a name="auto-table-creation"></a>自動建立資料表
如果您使用複製精靈 toocopy 資料從 SQL Server 或 Azure SQL Database tooAzure SQL 資料倉儲與 hello 資料表對應 toohello 來源資料表不存在 hello 目的地存放區中，資料處理站可以在自動建立 hello 資料表 hello使用 hello 來源資料表的結構描述的資料倉儲。

Data Factory 建立 hello 目的地存放區中的 hello 資料表相同的 hello 與資料表 hello 來源資料存放區中的名稱。 hello 資料行的資料類型會選擇根據 hello 下列型別對應。 如有需要它會執行類型轉換 toofix 來源和目的地存放區之間任何不相容。 它也會使用循環配置資源資料表散發。

| 來源 SQL Database 資料行類型 | 目的地 SQL DW 資料行類型 (大小限制) |
| --- | --- |
| int | int |
| BigInt | BigInt |
| SmallInt | SmallInt |
| TinyInt | TinyInt |
| Bit | Bit |
| 十進位 | 十進位 |
| 數值 | 十進位 |
| Float | Float |
| Money | Money |
| Real | Real |
| SmallMoney | SmallMoney |
| Binary | Binary |
| Varbinary | Varbinary （向上 too8000) |
| Date | 日期 |
| DateTime | DateTime |
| DateTime2 | DateTime2 |
| 時間 | 時間 |
| Datetimeoffset | Datetimeoffset |
| SmallDateTime | SmallDateTime |
| 文字 | Varchar （向上 too8000) |
| NText | NVarChar （向上 too4000) |
| 映像 | VarBinary （向上 too8000) |
| UniqueIdentifier | UniqueIdentifier |
| Char | Char |
| NChar | NChar |
| VarChar | VarChar （向上 too8000) |
| NVarChar | NVarChar （向上 too4000) |
| xml | Varchar （向上 too8000) |

[!INCLUDE [data-factory-type-repeatability-for-sql-sources](../../includes/data-factory-type-repeatability-for-sql-sources.md)]

## <a name="type-mapping-for-azure-sql-data-warehouse"></a>Azure SQL 資料倉儲的類型對應
Hello 中所述[資料移動活動](data-factory-data-movement-activities.md)發行項，複製活動會執行自動類型轉換來源類型 toosink 類型以 hello 遵循 2 步驟方法：

1. 從原生的來源類型 too.NET 類型轉換
2. 從.NET 型別 toonative 接收器類型轉換

當您從 Azure SQL 資料倉儲 & 太移動資料，hello 下列的對應會使用從 SQL 型別 too.NET 類型，反之亦然。

hello 對應是相同 hello [ADO.NET 的 SQL Server 資料類型對應](https://msdn.microsoft.com/library/cc716729.aspx)。

| SQL Server Database Engine 類型 | .NET Framework 類型 |
| --- | --- |
| bigint |Int64 |
| binary |Byte[] |
| bit |Boolean |
| char |String、Char[] |
| 日期 |DateTime |
| DateTime |DateTime |
| datetime2 |DateTime |
| Datetimeoffset |Datetimeoffset |
| 十進位 |十進位 |
| FILESTREAM 屬性 (varbinary(max)) |Byte[] |
| Float |兩倍 |
| image |Byte[] |
| int |Int32 |
| money |十進位 |
| nchar |String、Char[] |
| ntext |String、Char[] |
| numeric |十進位 |
| nvarchar |String、Char[] |
| real |單一 |
| rowversion |Byte[] |
| smalldatetime |DateTime |
| smallint |Int16 |
| smallmoney |十進位 |
| sql_variant |物件 * |
| 文字 |String、Char[] |
| 分析 |時間範圍 |
| timestamp |Byte[] |
| tinyint |位元組 |
| uniqueidentifier |Guid |
| varbinary |Byte[] |
| varchar |String、Char[] |
| xml |xml |

您也可以將對應從來源資料集 toocolumns 接收 hello 複製活動定義中的資料集的資料行。 如需詳細資料，請參閱[在 Azure Data Factory 中對應資料集資料行](data-factory-map-columns.md)。

## <a name="json-examples-for-copying-data-tooand-from-sql-data-warehouse"></a>從 SQL 資料倉儲中複製資料 tooand JSON 範例
hello 下列範例會提供範例 JSON 定義您可以藉由使用 toocreate 管線[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)或[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。 它們會顯示如何從 Azure SQL 資料倉儲和 Azure Blob 儲存體 toocopy 資料 tooand。 不過，資料可以複製**直接**從任何來源 tooany hello 接收所述的[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。

### <a name="example-copy-data-from-azure-sql-data-warehouse-tooazure-blob"></a>範例： 將資料複製 Azure SQL 資料倉儲 tooAzure Blob
hello 範例會定義下列 Data Factory 實體的 hello:

1. [AzureSqlDW](#linked-service-properties)類型的連結服務。
2. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。
3. [AzureSqlDWTable](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。
4. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。
5. 具有使用 [SqlDWSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。

hello 範例將時間序列 （每小時、 每日等等） 資料從 Azure SQL 資料倉儲資料庫 tooa blob 中的資料表的每個小時。 這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。

**Azure SQL 資料倉儲連結服務：**

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
**Azure Blob 儲存體連結服務：**

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
**Azure SQL 資料倉儲輸入資料集：**

hello 範例假設您已建立資料表"MyTable"Azure SQL 資料倉儲中，而且包含稱為"timestampcolumn 「 時間序列資料的資料行。

設定"external":"true"會通知 hello Data Factory 服務的 hello 集外部 toohello 資料處理站，且不產生 hello data factory 中的活動時。

```JSON
{
  "name": "AzureSqlDWInput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```
**Azure Blob 輸出資料集：**

資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。 hello blob 的 hello 資料夾路徑會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。 hello 資料夾路徑會使用 hello 開始時間的年、 月、 日和小時部分。

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**管線中使用 SqlDWSource 和 BlobSink 的複製活動：**

hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。 在 hello 管線 JSON 定義中，hello**來源**類型設定得**SqlDWSource**和**接收**類型設定得**BlobSink**。 指定 hello SQL 查詢**SqlReaderQuery**屬性選取 hello 資料在過去小時 toocopy hello。

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLDWtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSqlDWInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlDWSource",
            "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "BlobSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```
> [!NOTE]
> 在 hello 範例**sqlReaderQuery** hello SqlDWSource 指定。 hello 複製活動會針對 hello Azure SQL 資料倉儲來源 tooget hello 資料執行此查詢。
>
> 或者，您可以指定預存程序，藉由指定 hello **sqlReaderStoredProcedureName**和**storedProcedureParameters** （如果 hello 預存程序會採用參數）。
>
> 如果您未指定 sqlReaderQuery 或 sqlReaderStoredProcedureName，hello hello 資料集 JSON hello 結構區段中定義的資料行是使用的 toobuild 查詢 (選取 column1、 column2 從 mytable) toorun 針對 hello Azure SQL 資料倉儲。 如果您不需要 hello 資料集定義 hello 結構，所有資料行選取的 hello 資料表。
>
>

### <a name="example-copy-data-from-azure-blob-tooazure-sql-data-warehouse"></a>範例： 將資料從 Azure Blob tooAzure SQL 資料倉儲中複製
hello 範例會定義下列 Data Factory 實體的 hello:

1. [AzureSqlDW](#linked-service-properties)類型的連結服務。
2. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。
3. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。
4. [AzureSqlDWTable](#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。
5. 具有使用 [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) 和 [SqlDWSink](#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。

hello 範例時間序列資料 （每小時、 每天、 等等） 從 Azure blob tooa 資料表複製 Azure SQL 資料倉儲資料庫中的每個小時。 這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。

**Azure SQL 資料倉儲連結服務：**

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
**Azure Blob 儲存體連結服務：**

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
**Azure Blob 輸入資料集：**

每小時從新的 Blob 挑選資料 (頻率：小時，間隔：1)。 hello 資料夾路徑和檔案名稱 hello blob 會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。 年、 月和日的部分 hello 開始時間，會使用 hello 資料夾路徑和檔案名稱會使用 hello hello 開始時間的小時部分。 "external":"true"的設定會在這個資料表是外部 toohello 資料處理站，而不產生 hello data factory 中的活動時通知 hello Data Factory 服務。

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```
**Azure SQL 資料倉儲輸出資料集：**

hello 範例複製 Azure SQL 資料倉儲中名為"MyTable"的資料 tooa 資料表。 在具有 Azure SQL 資料倉儲中建立 hello 資料表如預期般 hello Blob CSV 檔案 toocontain hello 相同數目的資料行。 新的資料列會加入 toohello 資料表的每個小時。

```JSON
{
  "name": "AzureSqlDWOutput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
**具有 BlobSource 和 SqlDWSink 的管線中複製活動：**

hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。 在 hello 管線 JSON 定義中，hello**來源**類型設定得**BlobSource**和**接收**類型設定得**SqlDWSink**。

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQLDW",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlDWOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlDWSink",
            "allowPolyBase": true
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```
如需逐步解說，請參閱 hello，請參閱[Azure SQL 資料倉儲將在 15 分鐘與 Azure Data Factory 載入 1TB](data-factory-load-sql-data-warehouse.md)和[載入資料有 Azure Data Factory](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) hello Azure SQL 資料倉儲中的發行項文件。

## <a name="performance-and-tuning"></a>效能和微調
請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。
