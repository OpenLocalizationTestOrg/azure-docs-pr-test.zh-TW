---
title: "aaaCopy 資料從 Azure SQL Database 的 / |Microsoft 文件"
description: "深入了解如何從 Azure SQL Database 使用 Azure Data Factory 的/toocopy 資料。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 484f735b-8464-40ba-a9fc-820e6553159e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: d2ff16191afb028da75699c5e4d0bb310538db0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-database-using-azure-data-factory"></a>從 Azure SQL Database 使用 Azure Data Factory 複製資料 tooand
本文說明 toouse 中從 Azure SQL Database 的 Azure Data Factory toomove 資料 tooand hello 複製活動的方式。 它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。  

## <a name="supported-scenarios"></a>支援的案例
您可以將資料複製**從 Azure SQL Database** toohello 下列資料存放區：

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

您可以將資料複製下列資料存放區的 hello **tooAzure SQL Database**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-authentication-type"></a>支援的驗證類型
Azure SQL Database 連接器支援基本驗證。

## <a name="getting-started"></a>開始使用
您可以藉由使用不同的工具/API，建立內含複製活動的管線，以將資料移進/移出 Azure SQL Database。

最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。 請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。

您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。 請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。 

無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello: 

1. 建立 **Data Factory**。 資料處理站可包含一或多個管線。 
2. 建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。 例如，如果您從 Azure blob 儲存體 tooan Azure SQL database 中複製資料，您建立兩個連結的服務 toolink 您的 Azure 儲存體帳戶和 Azure SQL database tooyour 資料 factory。 連結的服務是特定 tooAzure SQL 資料庫的內容，請參閱[連結服務屬性](#linked-service-properties)> 一節。 
3. 建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。 在 hello hello 最後一個步驟中所述的範例中，您可以建立資料集 toospecify hello blob 容器和包含 hello 輸入的資料的資料夾。 而且，您保存 hello 資料複製 hello blob 儲存體中的 hello Azure SQL database 中建立另一個資料集 toospecify hello SQL 資料表。 資料集是特定 tooAzure 資料湖存放區的屬性，請參閱[資料集屬性](#dataset-properties)> 一節。
4. 建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。 在先前所述 hello 範例中，您使用 BlobSource 作為來源與 SqlSink 做為接收器 hello 複製活動。 同樣地，如果您要複製 Azure SQL Database tooAzure Blob 儲存體，您使用 SqlSource 和 BlobSink hello 複製活動中。 特定 tooAzure SQL Database 複製活動內容，請參閱[複製活動屬性](#copy-activity-properties)> 一節。 如需如何 toouse 的資料存放區做為來源或接收的詳細資訊，按一下 hello hello 資料存放區上一節中的連結。

當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。 當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。  如需使用的 toocopy 資料至 azure 或從 Azure SQL Database 的 Data Factory 實體的 JSON 定義的範例，請參閱[JSON 範例](#json-examples-for-copying-data-to-and-from-sql-database)本文一節。 

hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooAzure SQL Database 的 JSON 屬性的詳細資料： 

## <a name="linked-service-properties"></a>連結服務屬性
Azure SQL 連結服務連結的 Azure SQL database tooyour 資料 factory。 hello 下表提供的 JSON 元素特定 tooAzure SQL 連結服務。

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 類型 |hello 類型屬性必須設定為： **AzureSqlDatabase** |是 |
| connectionString |指定所需的資訊 tooconnect toohello Azure SQL Database 執行個體 hello connectionString 屬性。 僅支援基本驗證。 |是 |

> [!IMPORTANT]
> 設定[Azure SQL Database 防火牆](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure)太 hello 資料庫伺服器[允許 Azure 服務 tooaccess hello 伺服器](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure)。 此外，如果您要從內部部署資料來源與資料處理站閘道外部 Azure 包括複製資料 tooAzure SQL 資料庫，設定正在傳送資料 tooAzure SQL Database 的 hello 機器的適當 IP 位址範圍。

## <a name="dataset-properties"></a>資料集屬性
資料集 toorepresent toospecify Azure SQL database 中的輸入或輸出資料，設定 hello hello 資料集的類型屬性： **AzureSqlTable**。 設定 hello **linkedServiceName**屬性 hello 資料集 toohello 名稱 hello Azure SQL 連結服務。  

區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。 資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。

hello typeProperties 章節是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置的相關資訊。 hello **typeProperties** hello 資料集的類型 > 一節**AzureSqlTable**具有下列屬性的 hello:

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| tableName |參照 hello 資料表或檢視中的連結服務的 hello Azure SQL Database 執行個體的名稱。 |是 |

## <a name="copy-activity-properties"></a>複製活動屬性
區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。 屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。

> [!NOTE]
> hello 複製活動會採用只有 1 個輸入，並產生一個輸出。

而 hello 中可用屬性**typeProperties** hello 活動的區段會隨每個活動類型。 複製活動它們而異的來源與接收的 hello 類型。

如果您要移動資料從 Azure SQL database，您設定 hello 來源類型 hello 複製活動中太**SqlSource**。 同樣地，如果您要移動資料 tooan Azure SQL database，您設定 hello 接收器類型 hello 複製活動中太**SqlSink**。 本節提供 SqlSource 和 SqlSink 支援的屬性清單。

### <a name="sqlsource"></a>SqlSource
複製活動中，當 hello 來源的類型為**SqlSource**中的下列屬性的 hello 可用**typeProperties** > 一節：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| SqlReaderQuery |使用自訂查詢 tooread hello 的資料。 |SQL 查詢字串。 範例： `select * from MyTable`. |否 |
| sqlReaderStoredProcedureName |名稱的 hello 預存程序會從 hello 來源資料表讀取資料。 |名稱的 hello 預存程序。 hello 最後一個 SQL 陳述式必須在 hello 預存程序中的 SELECT 陳述式。 |否 |
| storedProcedureParameters |Hello 參數，預存程序。 |名稱/值組。 名稱和大小寫的參數必須符合 hello 名稱和大小寫的 hello 預存程序參數。 |否 |

如果 hello **sqlReaderQuery**指定 hello SqlSource，hello 複製活動會針對 hello Azure SQL Database 來源 tooget hello 資料執行此查詢。 或者，您可以指定預存程序，藉由指定 hello **sqlReaderStoredProcedureName**和**storedProcedureParameters** （如果 hello 預存程序會採用參數）。

如果您未指定 sqlReaderQuery 或 sqlReaderStoredProcedureName，hello hello 資料集 JSON hello 結構區段中定義的資料行是使用的 toobuild 查詢 (`select column1, column2 from mytable`) toorun 針對 hello Azure SQL Database。 如果您不需要 hello 資料集定義 hello 結構，所有資料行選取的 hello 資料表。

> [!NOTE]
> 當您使用**sqlReaderStoredProcedureName**，您仍然需要 toospecify 值 hello **tableName** hello 資料集 JSON 中的屬性。 雖然目前尚未針對此資料表來進行驗證。
>
>

### <a name="sqlsource-example"></a>SqlSource 範例

```JSON
"source": {
    "type": "SqlSource",
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

### <a name="sqlsink"></a>管線
**SqlSink**支援 hello 下列屬性：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| writeBatchTimeout |在逾時之前，請等待 hello 批次插入作業 toocomplete 時間。 |時間範圍<br/><br/> 範例：“00:30:00” (30 分鐘)。 |否 |
| writeBatchSize |當 hello 緩衝區大小到達叫用 writeBatchSize 時，請將資料插入 hello SQL 資料表。 |整數 (資料列數目) |否 (預設值：10000) |
| sqlWriterCleanupScript |複製活動 tooexecute 查詢指定的特定配量的資料清除。 如需詳細資訊，請參閱[可重複複製](#repeatable-copy)。 |查詢陳述式。 |否 |
| sliceIdentifierColumnName |指定複製活動 toofill 的資料行名稱與自動產生配量識別項，也就是使用的 tooclean 何時重新執行的特定配量的資料。 如需詳細資訊，請參閱[可重複複製](#repeatable-copy)。 |資料類型為 binary(32) 之資料行的資料行名稱。 |否 |
| sqlWriterStoredProcedureName |名稱的 hello 預存程序 upserts （更新/插入） 資料到 hello 目標資料表。 |名稱的 hello 預存程序。 |否 |
| storedProcedureParameters |Hello 參數，預存程序。 |名稱/值組。 名稱和大小寫的參數必須符合 hello 名稱和大小寫的 hello 預存程序參數。 |否 |
| sqlWriterTableType |指定用於 hello 預存程序中的資料表類型名稱 toobe。 複製活動移動 hello 資料可讓在暫存資料表與此資料表類型。 預存程序程式碼可以再合併 hello 資料會被複製現有的資料。 |資料表類型名稱。 |否 |

#### <a name="sqlsink-example"></a>SqlSink 範例

```JSON
"sink": {
    "type": "SqlSink",
    "writeBatchSize": 1000000,
    "writeBatchTimeout": "00:05:00",
    "sqlWriterStoredProcedureName": "CopyTestStoredProcedureWithParameters",
    "sqlWriterTableType": "CopyTestTableType",
    "storedProcedureParameters": {
        "identifier": { "value": "1", "type": "Int" },
        "stringData": { "value": "str1" },
        "decimalData": { "value": "1", "type": "Decimal" }
    }
}
```

## <a name="json-examples-for-copying-data-tooand-from-sql-database"></a>從 SQL Database 中複製資料 tooand JSON 範例
hello 下列範例會提供範例 JSON 定義您可以藉由使用 toocreate 管線[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)或[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。 它們會顯示如何從 Azure SQL Database 和 Azure Blob 儲存體 toocopy 資料 tooand。 不過，資料可以複製**直接**從任何來源 tooany hello 接收所述的[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。

### <a name="example-copy-data-from-azure-sql-database-tooazure-blob"></a>範例： 將資料複製 Azure SQL Database tooAzure Blob
hello 相同定義下列 Data Factory 實體的 hello:

1. [AzureSqlDatabase](#linked-service-properties)類型的連結服務。
2. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。
3. [AzureSqlTable](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。
4. [Azure Blob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。
5. 具有使用 [SqlSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之「複製活動」的[管線](data-factory-create-pipelines.md)。

hello 範例時間序列資料 （每小時、 每天、 等等） 資料表中的複製 Azure SQL database tooa blob 中的每個小時。 這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。  

**Azure SQL Database 已連結的服務：**

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
請參閱 hello [Azure SQL 連結服務](#linked-service)hello 清單支援這項連結服務屬性 > 一節。

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
請參閱 hello [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) hello 清單支援這項連結服務屬性的發行項。


**Azure SQL 輸入資料集：**

hello 範例假設您已建立資料表"MyTable"Azure SQL 中，而且包含稱為 「 timestampcolumn 「 時間序列資料的資料行。

設定"external":"true"會通知 hello Azure Data Factory 服務的 hello 集外部 toohello 資料處理站，且不產生 hello data factory 中的活動時。

```JSON
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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

請參閱 hello [Azure SQL 資料集型別屬性](#dataset)一節，以 hello 清單支援這個 dataset 類型的屬性。  

**Azure Blob 輸出資料集：**

資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。 hello blob 的 hello 資料夾路徑會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。 hello 資料夾路徑會使用 hello 開始時間的年、 月、 日和小時部分。

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}/",
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
請參閱 hello [Azure Blob 資料集型別屬性](data-factory-azure-blob-connector.md#dataset-properties)一節，以 hello 清單支援這個 dataset 類型的屬性。  

**具有 SQL 來源和 Blob 接收器的管線中複製活動：**

hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。 在 hello 管線 JSON 定義中，hello**來源**類型設定得**SqlSource**和**接收**類型設定得**BlobSink**。 指定 hello SQL 查詢**SqlReaderQuery**屬性選取 hello 資料在過去小時 toocopy hello。

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
在 hello 範例**sqlReaderQuery** hello SqlSource 指定。 hello 複製活動會針對 hello Azure SQL Database 來源 tooget hello 資料執行此查詢。 或者，您可以指定預存程序，藉由指定 hello **sqlReaderStoredProcedureName**和**storedProcedureParameters** （如果 hello 預存程序會採用參數）。

如果您未指定 sqlReaderQuery 或 sqlReaderStoredProcedureName，hello hello 資料集 JSON hello 結構區段中定義的資料行是使用的 toobuild hello Azure SQL Database 針對查詢 toorun。 例如： `select column1, column2 from mytable`。 如果您不需要 hello 資料集定義 hello 結構，所有資料行選取的 hello 資料表。

請參閱 hello [Sql 來源](#sqlsource)區段和[BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) hello 支援 SqlSource 和 BlobSink 屬性的清單。

### <a name="example-copy-data-from-azure-blob-tooazure-sql-database"></a>範例： 將資料從 Azure Blob tooAzure SQL Database 中複製
hello 範例會定義下列 Data Factory 實體的 hello:  

1. [AzureSqlDatabase](#linked-service-properties)類型的連結服務。
2. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。
3. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。
4. [AzureSqlTable](#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。
5. 具有使用 [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) 和 [SqlSink](#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。

hello 範例時間序列資料 （每小時、 每天、 等等） 從 Azure blob tooa 資料表複製 Azure SQL database 中的每個小時。 這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。

**Azure SQL 連結服務：**

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
請參閱 hello [Azure SQL 連結服務](#linked-service)hello 清單支援這項連結服務屬性 > 一節。

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
請參閱 hello [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) hello 清單支援這項連結服務屬性的發行項。


**Azure Blob 輸入資料集：**

每小時從新的 Blob 挑選資料 (頻率：小時，間隔：1)。 hello 資料夾路徑和檔案名稱 hello blob 會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。 年、 月和日的部分 hello 開始時間，會使用 hello 資料夾路徑和檔案名稱會使用 hello hello 開始時間的小時部分。 "external":"true"的設定會在這個資料表是外部 toohello 資料處理站，而不產生 hello data factory 中的活動時通知 hello Data Factory 服務。

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
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
請參閱 hello [Azure Blob 資料集型別屬性](data-factory-azure-blob-connector.md#dataset-properties)一節，以 hello 清單支援這個 dataset 類型的屬性。

**Azure SQL Database 輸出資料集：**

hello 範例會將名為"MyTable"中 Azure SQL 資料 tooa 資料表複製。 建立 hello 資料表與 Azure SQL 中如預期般 hello Blob CSV 檔案 toocontain hello 相同數目的資料行。 新的資料列會加入 toohello 資料表的每個小時。

```JSON
{
  "name": "AzureSqlOutput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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
請參閱 hello [Azure SQL 資料集型別屬性](#dataset)一節，以 hello 清單支援這個 dataset 類型的屬性。

**具有 Blob 來源和 SQL 接收器的管線中複製活動：**

hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。 在 hello 管線 JSON 定義中，hello**來源**類型設定得**BlobSource**和**接收**類型設定得**SqlSink**。

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlSink"
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
請參閱 hello [Sql 接收](#sqlsink)區段和[BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) hello 支援 SqlSink 和 BlobSource 屬性的清單。

## <a name="identity-columns-in-hello-target-database"></a>Hello 目標資料庫中的識別資料行
本節提供的範例資料複製到來源資料表沒有識別資料行的 tooa 目的地資料表之 identity 資料行。

**來源資料表：**

```SQL
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
**目的地資料表：**

```SQL
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```
請注意該 hello 目標資料表有識別資料行。

**來源資料集 JSON 定義**

```JSON
{
    "name": "SampleSource",
    "properties": {
        "type": " SqlServerTable",
        "linkedServiceName": "TestIdentitySQL",
        "typeProperties": {
            "tableName": "SourceTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```
**目的地資料集 JSON 定義**

```JSON
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "type": "AzureSqlTable",
        "linkedServiceName": "TestIdentitySQLSource",
        "typeProperties": {
            "tableName": "TargetTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }    
}
```

請注意，您的來源資料表與目標資料表的結構描述不同 (目標資料表有一個具有身分識別的額外資料行)。 在此案例中，您需要 toospecify**結構**hello 目標資料集定義，其中不包括 hello 識別資料行中的屬性。

## <a name="invoke-stored-procedure-from-sql-sink"></a>從 SQL 接收器叫用預存程序
如需在管線的複製活動中從 SQL 接收器叫用預存程序的範例，請參閱[在複製活動中叫用 SQL 接收器的預存程序](data-factory-invoke-stored-procedure-from-copy-activity.md)一文。 

## <a name="type-mapping-for-azure-sql-database"></a>Azure SQL Database 的類型對應
Hello 中所述[資料移動活動](data-factory-data-movement-activities.md)複製活動的文件以 hello 遵循 2 步驟方法執行從來源類型 toosink 類型的自動類型轉換：

1. 從原生的來源類型 too.NET 類型轉換
2. 從.NET 型別 toonative 接收器類型轉換

當您從 Azure SQL Database 中移動資料 tooand，hello 下列的對應會使用從 SQL 型別 too.NET 類型，反之亦然。 hello 對應是相同 hello ADO.NET 的 SQL Server 資料類型對應。

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

## <a name="map-source-toosink-columns"></a>將來源 toosink 資料行對應
toolearn 對應中之資料行來源的資料集 toocolumns 中接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。

## <a name="repeatable-copy"></a>可重複複製
當複製資料 tooSQL 伺服器資料庫，hello 複製活動將預設附加 toohello 接收資料表。 相反地，請參閱 tooperform UPSERT[可重複寫入 tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink)發行項。 

複製資料時從關聯式資料存放區，請注意 tooavoid 重複性非預期的結果。 在 Azure Data Factory 中，您可以手動重新執行配量。 您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。 當其中一個方式，重新執行配量時，您需要 toomake 確定的 hello 相同的資料如何讀取無論執行多次的配量。 請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)。

## <a name="performance-and-tuning"></a>效能和微調
請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。
