---
title: "從 SQL Server aaaMove 資料 tooand |Microsoft 文件"
description: "了解有關如何 toomove 資料至 azure 或從 SQL Server 資料庫也就是在內部部署或 Azure VM 使用 Azure Data Factory 中。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 864ece28-93b5-4309-9873-b095bbe6fedd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jingwang
ms.openlocfilehash: f0cccf56a670e62ec893d75052a81eb26d562050
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-sql-server-on-premises-or-on-iaas-azure-vm-using-azure-data-factory"></a>移動資料 tooand 從 SQL Server 內部或 IaaS (Azure VM) 上使用 Azure Data Factory
本文說明如何 toouse hello Azure Data Factory toomove 資料從內部部署 SQL Server 資料庫中的複製活動。 它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。 

## <a name="supported-scenarios"></a>支援的案例
您可以將資料複製**從 SQL Server 資料庫**toohello 下列資料存放區：

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

您可以將資料複製下列資料存放區的 hello **tooa SQL Server 資料庫**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-sql-server-versions"></a>支援的 SQL Server 版本
複製資料，從這個 SQL Server 連接器支援 / toohello 下列版本的執行個體裝載內部或在使用 SQL 驗證和 Windows 驗證的 Azure IaaS 中： SQL Server 2016、 SQL Server 2014、 SQL Server 2012、 SQL Server 2008 R2、 SQLServer 2008、 SQL Server 2005

## <a name="enabling-connectivity"></a>啟用連線
hello 概念及所需的 Vm （基礎結構做為服務） 連線與 SQL Server 裝載內部或在 Azure IaaS 中的步驟是 hello 相同。 在這兩種情況下，您需要連線 toouse 資料管理閘道器。

請參閱[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)文章 toolearn 有關資料管理閘道器和 hello 閘道設定的逐步指示。 設定閘道器執行個體是與 SQL Server 連線的必要條件。

您可以安裝閘道時 hello 相同上內部機器或雲端的 VM 執行個體為 SQL Server hello 以提升效能，我們建議您安裝它們在不同電腦上。 在不同電腦上擁有 hello 閘道和 SQL Server 會減少資源競爭。

## <a name="getting-started"></a>開始使用
您可以建立內含複製活動的管線，使用不同的工具/API 將資料移進/移出內部部署 SQL Server 資料庫。

最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。 請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。

您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。 請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。 

無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello: 

1. 建立 **Data Factory**。 資料處理站可包含一或多個管線。 
2. 建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。 例如，如果您從 Azure blob 儲存體的 SQL Server 資料庫 tooan 複製資料，您建立兩個連結的服務 toolink 您 SQL Server 資料庫和 Azure 儲存體帳戶 tooyour 資料 factory。 對於特定 tooSQL Server 資料庫的連結的服務屬性，請參閱[連結服務屬性](#linked-service-properties)> 一節。 
3. 建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。 在 hello hello 最後一個步驟中所述的範例，您可以建立資料集 toospecify hello SQL 資料表包含 hello 輸入的資料在 SQL Server 資料庫中。 建立另一個資料集 toospecify hello blob 容器及保存 hello 資料 hello 資料夾 hello 從 SQL Server 資料庫複製。 對於特定 tooSQL Server 資料庫的資料集屬性，請參閱[資料集屬性](#dataset-properties)> 一節。
4. 建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。 在先前所述 hello 範例中，您使用 SqlSource 作為來源和 BlobSink 做為接收器 hello 複製活動。 同樣地，如果您要從 Azure Blob 儲存體 tooSQL 伺服器資料庫複製，則使用 BlobSource 和 SqlSink 的 hello 複製活動。 複製活動是特定 tooSQL 伺服器資料庫的內容，請參閱[複製活動屬性](#copy-activity-properties)> 一節。 如需如何 toouse 的資料存放區做為來源或接收的詳細資訊，按一下 hello hello 資料存放區上一節中的連結。 

當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。 當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。  如需使用的 toocopy 資料，從內部部署 SQL Server 資料庫的 Data Factory 實體的 JSON 定義的範例，請參閱[JSON 範例](#json-examples-for-copying-data-from-and-to-sql-server)本文一節。 

hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooSQL 伺服器的 JSON 屬性的詳細資料： 

## <a name="linked-service-properties"></a>連結服務屬性
您建立連結的服務型別的**OnPremisesSqlServer** toolink 在內部部署 SQL Server 資料庫 tooa 資料 factory。 下表中的 hello 提供 JSON 項目特定 tooon 內部部署 SQL Server 連結服務的描述。

下表中的 hello 提供 JSON 項目特定 tooSQL 連結的伺服器服務的描述。

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 類型 |hello 類型屬性應該設定為： **OnPremisesSqlServer**。 |是 |
| connectionString |指定所需的 connectionString 資訊 tooconnect toohello 在內部部署 SQL Server 資料庫使用 SQL 驗證或 Windows 驗證。 |是 |
| gatewayName |Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello 在內部部署 SQL Server 資料庫。 |是 |
| username |如果您使用「Windows 驗證」，請指定使用者名稱。 範例︰**domainname\\username**。 |否 |
| password |指定 hello hello 使用者名稱所指定的使用者帳戶的密碼。 |否 |

您可以加密認證使用 hello**新增 AzureRmDataFactoryEncryptValue** cmdlet 並將其用於 hello 連接字串 hello 下列範例所示 (**EncryptedCredential**屬性):  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

### <a name="samples"></a>範例
**使用 SQL 驗證的 JSON**

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties":
    {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
**使用 Windows 驗證的 JSON**

資料管理閘道會模擬 hello 指定使用者帳戶 tooconnect toohello 在內部部署 SQL Server 資料庫。 

```json
{
     "Name": " MyOnPremisesSQLDB",
     "Properties":
     {
         "type": "OnPremisesSqlServer",
         "typeProperties": {
             "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
             "username": "<domain\\username>",
             "password": "<password>",
             "gatewayName": "<gateway name>"
        }
     }
}
```

## <a name="dataset-properties"></a>資料集屬性
在 hello 範例中，您已使用的型別資料集**SqlServerTable** toorepresent SQL Server 資料庫中的資料表。  

區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。 所有資料集類型 (SQL Server、Azure Blob、Azure 資料表等) 的資料集 JSON 區段 (例如 structure、availability 及 policy) 都相似。

hello typeProperties 章節是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置的相關資訊。 hello **typeProperties** hello 資料集的類型 > 一節**SqlServerTable**具有下列屬性的 hello:

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| tableName |參照 hello 資料表或檢視中的連結服務的 hello 的 SQL Server 資料庫執行個體的名稱。 |是 |

## <a name="copy-activity-properties"></a>複製活動屬性
如果您要移動的資料從 SQL Server 資料庫，您設定 hello 來源類型 hello 複製活動中太**SqlSource**。 同樣地，如果您要移動資料 tooa SQL Server 資料庫，您設定 hello 接收器類型 hello 複製活動中太**SqlSink**。 本節提供 SqlSource 和 SqlSink 支援的屬性清單。

區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。 屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。

> [!NOTE]
> hello 複製活動會採用只有 1 個輸入，並產生一個輸出。

而 hello 活動 hello typeProperties 區段中可用的屬性會隨每個活動類型。 複製活動它們而異的來源與接收的 hello 類型。

### <a name="sqlsource"></a>SqlSource
複製活動中的來源時的型別**SqlSource**中的下列屬性的 hello 可用**typeProperties** > 一節：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| SqlReaderQuery |使用自訂查詢 tooread hello 的資料。 |SQL 查詢字串。 例如：select * from MyTable。 從 hello hello 輸入資料集所參考的資料庫，可以參考多個資料表。 如果未指定，hello 執行的 SQL 陳述式： select from MyTable。 |否 |
| sqlReaderStoredProcedureName |名稱的 hello 預存程序會從 hello 來源資料表讀取資料。 |名稱的 hello 預存程序。 hello 最後一個 SQL 陳述式必須在 hello 預存程序中的 SELECT 陳述式。 |否 |
| storedProcedureParameters |Hello 參數，預存程序。 |名稱/值組。 名稱和大小寫的參數必須符合 hello 名稱和大小寫的 hello 預存程序參數。 |否 |

如果 hello **sqlReaderQuery**指定 hello SqlSource，hello 複製活動會針對 hello 的 SQL Server 資料庫來源 tooget hello 資料執行此查詢。

或者，您可以指定預存程序，藉由指定 hello **sqlReaderStoredProcedureName**和**storedProcedureParameters** （如果 hello 預存程序會採用參數）。

如果您未指定 sqlReaderQuery 或 sqlReaderStoredProcedureName，hello hello 結構區段中定義的資料行是使用的 toobuild select 查詢 toorun 針對 hello 的 SQL Server 資料庫。 如果您不需要 hello 資料集定義 hello 結構，所有資料行選取的 hello 資料表。

> [!NOTE]
> 當您使用**sqlReaderStoredProcedureName**，您仍然需要 toospecify 值 hello **tableName** hello 資料集 JSON 中的屬性。 雖然目前尚未針對此資料表來進行驗證。

### <a name="sqlsink"></a>管線
**SqlSink**支援 hello 下列屬性：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| writeBatchTimeout |在逾時之前，請等待 hello 批次插入作業 toocomplete 時間。 |時間範圍<br/><br/> 範例：“00:30:00” (30 分鐘)。 |否 |
| writeBatchSize |當 hello 緩衝區大小到達叫用 writeBatchSize 時，請將資料插入 hello SQL 資料表。 |整數 (資料列數目) |否 (預設值：10000) |
| sqlWriterCleanupScript |複製活動 tooexecute 查詢指定的特定配量的資料清除。 如需詳細資訊，請參閱[可重複複製](#repeatable-copy)一節。 |查詢陳述式。 |否 |
| sliceIdentifierColumnName |指定資料行名稱複製活動 toofill 與自動產生配量識別項，也就是使用的 tooclean 何時重新執行的特定配量的資料。 如需詳細資訊，請參閱[可重複複製](#repeatable-copy)一節。 |資料類型為 binary(32) 之資料行的資料行名稱。 |否 |
| sqlWriterStoredProcedureName |名稱的 hello 預存程序 upserts （更新/插入） 資料到 hello 目標資料表。 |名稱的 hello 預存程序。 |否 |
| storedProcedureParameters |Hello 參數，預存程序。 |名稱/值組。 名稱和大小寫的參數必須符合 hello 名稱和大小寫的 hello 預存程序參數。 |否 |
| sqlWriterTableType |指定資料表類型名稱 toobe hello 預存程序中使用。 複製活動移動 hello 資料可讓在暫存資料表與此資料表類型。 預存程序程式碼可以再合併 hello 資料會被複製現有的資料。 |資料表類型名稱。 |否 |


## <a name="json-examples-for-copying-data-from-and-toosql-server"></a>用來複製資料與 tooSQL 伺服器 JSON 範例
hello 下列範例會提供範例 JSON 定義您可以藉由使用 toocreate 管線[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)或[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。 hello 下列範例顯示如何從 SQL Server 和 Azure Blob 儲存體 toocopy 資料 tooand。 不過，資料可以複製**直接**從任何來源 tooany hello 接收所述的[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。     

## <a name="example-copy-data-from-sql-server-tooazure-blob"></a>範例： 從 SQL Server tooAzure Blob 複製資料
下列範例會示範 hello:

1. [OnPremisesSqlServer](#linked-service-properties)類型的連結服務。
2. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。
3. [SqlServerTable](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。
4. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。
5. hello[管線](data-factory-create-pipelines.md)與使用複製活動[SqlSource](#copy-activity-properties)和[BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)。

hello 範例將時間序列資料從 SQL Server 資料表 tooan Azure blob 的每個小時。 這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。

第一個步驟中，安裝程式 hello 資料管理閘道器。 hello 中的 hello 指示[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)發行項。

**SQL Server 連結服務**
```json
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```
**Azure Blob 儲存體連結服務**

```json
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
**SQL Server 輸入資料集**

hello 範例假設您已建立資料表"MyTable"SQL Server 中，而且包含稱為"timestampcolumn 「 時間序列資料的資料行。 您可以透過 hello hello 資料集的 tableName typeProperty 必須使用相同的資料庫，使用單一資料集，但單一資料表內的多個資料表進行查詢。

設定"external":"true"會通知 Data Factory 服務的 hello 集外部 toohello 資料處理站，且不產生 hello data factory 中的活動時。

```json
{
  "name": "SqlServerInput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
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
**Azure Blob 輸出資料集**

資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。 hello blob 的 hello 資料夾路徑會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。 hello 資料夾路徑會使用 hello 開始時間的年、 月、 日和小時部分。

```json
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
**具有複製活動的管線**

hello 管線包含複製活動的設定的 toouse 這些輸入和輸出資料集，而排程的 toorun 每小時。 在 hello 管線 JSON 定義中，hello**來源**類型設定得**SqlSource**和**接收**類型設定得**BlobSink**。 指定 hello SQL 查詢**SqlReaderQuery**屬性選取 hello 資料在過去小時 toocopy hello。

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2016-06-01T18:00:00",
    "end":"2016-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
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
在此範例中， **sqlReaderQuery** hello SqlSource 指定。 hello 複製活動會針對 hello 的 SQL Server 資料庫來源 tooget hello 資料執行此查詢。 或者，您可以指定預存程序，藉由指定 hello **sqlReaderStoredProcedureName**和**storedProcedureParameters** （如果 hello 預存程序會採用參數）。 hello sqlReaderQuery 參考 hello hello 輸入資料集所參考的資料庫內的多個資料表。 它不是設定為 hello 資料集的 tableName typeProperty 有限的 tooonly hello 資料表。

如果您未指定 sqlReaderQuery 或 sqlReaderStoredProcedureName，hello hello 結構區段中定義的資料行是使用的 toobuild select 查詢 toorun 針對 hello 的 SQL Server 資料庫。 如果您不需要 hello 資料集定義 hello 結構，所有資料行選取的 hello 資料表。

請參閱 hello [Sql 來源](#sqlsource)區段和[BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) hello 支援 SqlSource 和 BlobSink 屬性的清單。

## <a name="example-copy-data-from-azure-blob-toosql-server"></a>範例： 將資料從 Azure Blob tooSQL Server 複製
下列範例會示範 hello:

1. hello 連結類型的服務[OnPremisesSqlServer](#linked-service-properties)。
2. hello 連結類型的服務[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)。
3. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。
4. [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。
5. hello[管線](data-factory-create-pipelines.md)與使用複製活動[BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties)和[SqlSink](#sql-server-copy-activity-type-properties)。

hello 範例複製時間序列資料從 Azure blob tooa SQL Server 資料表的每個小時。 這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。

**SQL Server 連結服務**

```json
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```
**Azure Blob 儲存體連結服務**

```json
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
**Azure Blob 輸入資料集**

每小時從新的 Blob 挑選資料 (頻率：小時，間隔：1)。 hello 資料夾路徑和檔案名稱 hello blob 會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。 年、 月和日的部分 hello 開始時間，會使用 hello 資料夾路徑和檔案名稱會使用 hello hello 開始時間的小時部分。 "external":"true"的設定會在該 hello 集外部 toohello 資料處理站，且不產生 hello data factory 中的活動時通知 hello Data Factory 服務。

```json
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
**SQL Server 輸出資料集**

hello 範例會將名為"MyTable"SQL Server 中的資料 tooa 資料表複製。 建立與 SQL Server 中的 hello 資料表如預期般 hello Blob CSV 檔案 toocontain hello 相同數目的資料行。 新的資料列會加入 toohello 資料表的每個小時。

```json
{
  "name": "SqlServerOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
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
**具有複製活動的管線**

hello 管線包含複製活動的設定的 toouse 這些輸入和輸出資料集，而排程的 toorun 每小時。 在 hello 管線 JSON 定義中，hello**來源**類型設定得**BlobSource**和**接收**類型設定得**SqlSink**。

```json
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
            "name": " SqlServerOutput "
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

## <a name="troubleshooting-connection-issues"></a>疑難排解連線問題
1. 設定 SQL Server tooaccept 的遠端連線。 啟動 [SQL Server Management Studio]、用滑鼠右鍵按一下 [伺服器]，然後按一下 [屬性]。 選取**連線**hello 清單和核取**允許遠端連接 toohello 伺服器**。

    ![啟用遠端連線](./media/data-factory-sqlserver-connector/AllowRemoteConnections.png)

    請參閱[設定 hello remote access 伺服器組態選項](https://msdn.microsoft.com/library/ms191464.aspx)如需詳細步驟。
2. 啟動 [SQL Server 組態管理員] 。 展開**SQL Server 網路組態**hello 的執行個體和選取**MSSQLSERVER 的通訊協定**。 您應該會看到 hello 右窗格中的通訊協定。 用滑鼠右鍵按一下 [TCP/IP]，然後按一下 [啟用] 來啟用 TCP/IP。

    ![啟用 TCP/IP](./media/data-factory-sqlserver-connector/EnableTCPProptocol.png)

    如需啟用 TCP/IP 通訊協定的詳細資料及替代方式，請參閱 [啟用或停用伺服器網路通訊協定](https://msdn.microsoft.com/library/ms191294.aspx) 。
3. 在 hello 相同的視窗中按兩下**TCP/IP** toolaunch **TCP/IP 內容**視窗。
4. 切換 toohello **IP 位址** 索引標籤。捲動 toosee **IPAll** > 一節。 記下 hello * * TCP 連接埠 * * (預設值是**1433年**)。
5. 建立**hello Windows 防火牆規則**上透過此連接埠的 hello 機器 tooallow 連入流量。  
6. **請確認連接**: tooconnect toohello 使用完整限定的名稱，SQL Server 使用 SQL Server Management Studio 從不同的電腦。 例如："<machine><domain>.corp<company>.com,1433"。

   > [!IMPORTANT]

   > 請參閱[在內部部署來源和資料管理閘道與 hello 雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)如需詳細資訊。
   >
   > 如需連接/閘道器相關問題的疑難排解秘訣，請參閱 [針對閘道問題進行疑難排解](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 。
   >
   >


## <a name="identity-columns-in-hello-target-database"></a>Hello 目標資料庫中的識別資料行
本章節提供的範例，但沒有識別資料行 tooa 目的地資料表之 identity 資料行的來源資料表中的資料複製。

**來源資料表：**

```sql
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
**目的地資料表：**

```sql
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```

請注意該 hello 目標資料表有識別資料行。

**來源資料集 JSON 定義**

```json
{
    "name": "SampleSource",
    "properties": {
        "published": false,
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

```json
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "published": false,
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

## <a name="type-mapping-for-sql-server"></a>SQL Server 的類型對應
Hello 中所述[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會執行自動類型轉換來源類型 toosink 類型以 hello 遵循 2 步驟方法：

1. 從原生的來源類型 too.NET 類型轉換
2. 從.NET 型別 toonative 接收器類型轉換

當資料移動太 & 從 SQL server hello 從 SQL 型別 too.NET 類型，反之亦然，會使用下列的對應。

hello 對應是相同 hello ADO.NET 的 SQL Server 資料類型對應。

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

## <a name="mapping-source-toosink-columns"></a>對應來源 toosink 資料行
toomap 資料行從來源資料集 toocolumns 從接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。

## <a name="repeatable-copy"></a>可重複複製
當複製資料 tooSQL 伺服器資料庫，hello 複製活動將預設附加 toohello 接收資料表。 相反地，請參閱 tooperform UPSERT[可重複寫入 tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink)發行項。 

複製資料時從關聯式資料存放區，請注意 tooavoid 重複性非預期的結果。 在 Azure Data Factory 中，您可以手動重新執行配量。 您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。 當其中一個方式，重新執行配量時，您需要 toomake 確定的 hello 相同的資料如何讀取無論執行多次的配量。 請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)。

## <a name="performance-and-tuning"></a>效能和微調
請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。
