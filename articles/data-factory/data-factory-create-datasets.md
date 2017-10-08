---
title: "aaaCreate Azure Data Factory 中的資料集 |Microsoft 文件"
description: "了解如何在 Azure Data Factory，使用這類屬性的範例使用的 toocreate 資料集的位移和 anchorDateTime。"
keywords: "建立資料集, 資料集範例, 位移範例"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 0614cd24-2ff0-49d3-9301-06052fd4f92a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: shlo
ms.openlocfilehash: 181859ed250595d756df73e9ebcac08d9e7184c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="datasets-in-azure-data-factory"></a>Azure Data Factory 中的資料集
本文說明什麼是資料集、如何以 JSON 格式定義它們，以及如何在 Azure Data Factory 管線中使用它們。 它提供有關每個區段 （例如，結構、 可用性和原則） 的詳細資料 hello 資料集 JSON 定義中。 hello 發行項也提供範例使用 hello**位移**， **anchorDateTime**，和**樣式**資料集 JSON 定義中的屬性。

> [!NOTE]
> 如果您是新 tooData 處理站，請參閱[簡介 tooAzure Data Factory](data-factory-introduction.md)的概觀。 如果您沒有建立 data factory 的實際操作體驗，您可以進一步了解所讀取的 hello[資料轉換的教學課程](data-factory-build-your-first-pipeline.md)和 hello[資料移動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。 

## <a name="overview"></a>概觀
資料處理站可以有一或多個管線。 「管線」是一起執行某個工作的「活動」所組成的邏輯群組。 在管線中的 hello 活動定義動作 tooperform 對您的資料。 例如，您可能會使用複製活動 toocopy 資料從內部部署 SQL Server tooAzure Blob 儲存體。 然後，您可以使用 Azure HDInsight 叢集 tooprocess 資料執行 Hive 指令碼，從 Blob 儲存體 tooproduce 輸出資料的 Hive 活動。 最後，您可能會使用第二個複製活動 toocopy hello 輸出資料 tooAzure SQL 資料倉儲、 報告建置方案的商業智慧 (BI) 之上。 如需有關管線和活動的詳細資訊，請參閱 [Azure Data Factory 中的管線及活動](data-factory-create-pipelines.md)。

一個活動可以接受零個或多個輸入「資料集」，並且會產生一個或多個輸出資料集。 輸入資料集代表 hello hello 管線中活動的輸入和輸出資料集代表 hello hello 活動的輸出。 資料集可識別資料表、檔案、資料夾和文件等各種資料存放區中的資料。 比方說，Azure Blob 資料集指定 hello blob 容器和資料夾從哪些 hello 管線應該讀取 hello 資料的 Blob 儲存體中。 

您建立資料集之前，先建立**連結服務**toolink 資料儲存 toohello 資料 factory。 連結的服務非常類似連接字串，定義所需的 Data Factory tooconnect tooexternal 資源 hello 連接資訊中。 資料集來識別連結的 hello 資料存放區，例如 SQL 資料表、 檔案、 資料夾和文件內的資料。 例如，Azure 儲存體連結服務的連結儲存體帳戶 toohello data factory。 Azure Blob 資料集代表 hello blob 容器，並包含處理 hello 輸入的 blob toobe hello 資料夾。 

以下是一個範例案例。 從 Blob 儲存體 tooa SQL database 的 toocopy 資料，建立兩個連結的服務： Azure 儲存體和 Azure SQL Database。 接著，建立兩個資料集： Azure Blob 資料集 （也就是 toohello Azure 儲存體連結服務） 和 Azure SQL 資料表的資料集 （也就是 toohello 連結的 Azure SQL Database 服務）。 hello Azure 儲存體和 Azure SQL Database 已連結的服務包含 Data Factory 分別使用在執行階段 tooconnect tooyour Azure 儲存體和 Azure SQL Database 的連接字串。 hello Azure Blob 資料集指定 hello blob 容器，並包含您的 Blob 儲存體中的 hello 輸入的 blob 的 blob 資料夾。 hello Azure SQL 資料表的資料集指定 SQL 資料庫 toowhich hello 資料中的 hello SQL 資料表 toobe 複製。

hello 下圖顯示 hello 管線、 活動、 資料集和連結的服務之間的關聯性 Data Factory 中： 

![管線、活動、資料集、已連結的服務之間的關聯性](media/data-factory-create-datasets/relationship-between-data-factory-entities.png)

## <a name="dataset-json"></a>資料集 JSON
Data Factory 中的資料集會以 JSON 格式定義如下：

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag tooindicate external data. only for input datasets>,
        "linkedServiceName": "<Name of hello linked service that refers tooa data store.>",
        "structure": [
            {
                "name": "<Name of hello column>",
                "type": "<Name of hello type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies hello time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies hello interval within hello defined frequency. For example, frequency set too'Hour' and interval set too1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

hello 下表描述上方 JSON hello 中的屬性：   

| 屬性 | 說明 | 必要 | 預設值 |
| --- | --- | --- | --- |
| 名稱 |Hello 資料集的名稱。 請參閱 [Azure Data Factory - 命名規則](data-factory-naming-rules.md) ，以了解命名規則。 |是 |NA |
| 類型 |hello 資料集的類型。 指定一個支援的 Data Factory 的 hello 類型 (例如： AzureBlob、 AzureSqlTable)。 <br/><br/>如需詳細資料，請參閱[資料集類型](#Type)。 |是 |NA |
| structure |Hello 資料集的結構描述。<br/><br/>如需詳細資料，請參閱[資料集結構](#Structure)。 |否 |NA |
| typeProperties | hello 類型屬性都不同的每個型別 (例如： Azure Blob、 Azure SQL 資料表)。 如需支援的 hello 類型和其屬性的詳細資訊，請參閱[資料集類型](#Type)。 |是 |NA |
| external | 布林值旗標 toospecify，是否與否，資料 factory 管線所明確產生資料集。 Hello 活動的輸入資料集不產生 hello 目前的管線時，如果設定此旗標 tootrue。 Hello 管線中設定這個旗標 tootrue，hello hello 第一個活動的輸入資料集。  |否 |false |
| Availability | 定義處理期間，（比方說，每小時或每天） hello 或 hello 配量 hello 資料集實際執行的模型。 活動執行取用和產生的每個資料單位稱為資料配量。 如果輸出資料集中的 hello 可用性集 toodaily （頻率為一天，間隔為 1），每天產生配量。 <br/><br/>如需詳細資料，請參閱[資料集可用性](#Availability)。 <br/><br/>如需詳細資訊，hello 資料集上配量模型，請參閱 hello[排程與執行](data-factory-scheduling-and-execution.md)發行項。 |是 |NA |
| 原則 |定義 hello 準則或 hello hello 資料集配量，都必須符合的條件。 <br/><br/>如需詳細資訊，請參閱 hello[資料集原則](#Policy)> 一節。 |否 |NA |

## <a name="dataset-example"></a>資料集範例
在下列範例的 hello，hello 資料集代表名為的資料表**MyTable** SQL 資料庫中。

```json
{
    "name": "DatasetSample",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties":
        {
            "tableName": "MyTable"
        },
        "availability":
        {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

請注意下列點 hello:

* **型別**tooAzureSqlTable 設定。
* **tableName** type 屬性 （特定 tooAzureSqlTable 類型） 設定 tooMyTable。
* **linkedServiceName**參考 tooa 連結服務類型 AzureSqlDatabase hello 下一步的 JSON 片段中定義。 
* **可用性頻率**設定 tooDay，和**間隔**too1 設定。 這表示每天產生該 hello 資料集配量。  

**AzureSqlLinkedService** 定義如下︰

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>@<servername>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

在 hello 前面 JSON 片段：

* **型別**tooAzureSqlDatabase 設定。
* **connectionString**型別屬性會指定資訊 tooconnect tooa SQL 資料庫。  

如您所見，hello 連結的服務定義如何 tooconnect tooa SQL 資料庫。 hello 資料集定義哪些資料表是用做為輸入和輸出管線中的 hello 活動。   

> [!IMPORTANT]
> 除非正在 hello 管線所產生的資料集，應該標記為**外部**。 此設定通常適用於 tooinputs 的管線中的第一個活動。   


## <a name="Type"></a> 資料集類型
hello 資料集的 hello 類型取決於您使用的 hello 資料存放區。 請參閱下表取得一份資料存放區支援的 Data Factory 的 hello。 按一下 資料存放區 toolearn 如何 toocreate 連結的服務，以及該資料的資料集存放區。

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> 帶有 * 的資料存放區可以位於內部部署環境或 Azure 基礎結構即服務 (IaaS) 上。 這些資料存放區會要求您 tooinstall[資料管理閘道器](data-factory-data-management-gateway.md)。

在 hello hello 前一節中的範例，hello 類型 hello 資料集的設定太**AzureSqlTable**。 同樣地，如果是 Azure Blob 資料集，hello 類型 hello 資料集的設定太**AzureBlob**、 hello 下列 JSON 中所示：

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

## <a name="Structure"></a>資料集結構
hello**結構**區段是選擇性的。 它會定義 hello hello 資料集的結構描述所包含集合的名稱和資料行的資料類型。 您使用 hello 結構區段 tooprovide 型別資訊，是使用的 tooconvert 類型，從 hello 來源 toohello 目的地的對應資料行。 在下列範例的 hello，hello 資料集有三個資料行： `slicetimestamp`， `projectname`，和`pageviews`。 它們的類型分別是 String、String 及 Decimal。

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

Hello 結構中的每個資料行包含下列屬性的 hello:

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 名稱 |Hello 資料行名稱。 |是 |
| 類型 |Hello 資料行資料類型。  |否 |
| culture |.Hello 類型為.NET 型別時使用的網路基礎的文化特性 toobe:`Datetime`或`Datetimeoffset`。 hello 預設值是`en-us`。 |否 |
| format |格式化字串 toobe hello 類型為.NET 型別時使用：`Datetime`或`Datetimeoffset`。 |否 |

hello 下列指導方針協助您判斷當 tooinclude 結構的詳細資訊，以及在 hello 哪些 tooinclude**結構**> 一節。

* **結構化的資料來源的**，只有當您想要將來源資料行 toosink 資料行對應，而且其名稱不是 hello 相同指定 hello 結構 > 一節。 這種結構化的資料來源會儲存以及 hello 資料本身的資料結構描述和類型資訊。 結構化資料來源的範例包括 SQL Server、Oracle 及 Azure 資料表。 
  
    因為型別資訊已提供結構化的資料來源，您不應該包含型別資訊包括 hello 結構區段時。
* **在讀取的資料來源 （特別是 Blob 儲存） 上的結構描述**，您可以選擇 toostore 資料，而不儲存任何結構描述或型別資訊與 hello 資料。 當您想 toomap 來源資料行 toosink 資料行時，針對這些類型的資料來源，包含結構。 Hello 資料集是複製活動中，輸入，來源資料集的資料類型應該是 hello 接收已轉換的 toonative 類型時，也包含結構。 
    
    Data Factory 支援下列值，提供類型資訊，在結構中的 hello: **Int16、 Int32、 Int64、 單一、 Double、 Decimal、 位元組 []、 布林值、 字串、 Guid、 Datetime、 Datetimeoffset 和 Timespan**。 這些值是符合 Common Language Specification (CLS) 規範的 .NET 型類型值。

Data Factory 會移動資料的來源資料的資料存放區 tooa 接收資料存放區時，會自動執行類型轉換。 
  

## <a name="dataset-availability"></a>資料集可用性
hello**可用性**資料集中的區段會定義 hello 處理 視窗 （例如，每小時、 每天或每週） hello 資料集。 如需有關活動時段的詳細資訊，請參閱[排程和執行](data-factory-scheduling-and-execution.md)。

下列可用性一節的 hello 指定 hello 輸出資料集可能是產生每小時、 或 hello 輸入資料集為每小時可用：

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

如果 hello 管線有 hello 遵循開始和結束時間：  

```json
    "start": "2016-08-25T00:00:00Z",
    "end": "2016-08-25T05:00:00Z",
```

hello 輸出資料集則會產生每小時 hello 管線內開始和結束時間。 因此，這個管線會產生五個資料集配量，每個活動時段 (上午 12 點 - 上午 1 點、上午 1 點 - 上午 2 點、上午 2 點 - 上午 3 點、上午 3 點 - 上午 4 點、上午 4 點 - 上午 5 點) 各一個資料集。 

hello 下表描述您可以使用 hello 可用性一節中的屬性：

| 屬性 | 說明 | 必要 | 預設值 |
| --- | --- | --- | --- |
| frequency |指定資料集配量實際執行環境的 hello 時間單位。<br/><br/><b>支援的頻率</b>：Minute、Hour、Day、Week、Month |是 |NA |
| interval |指定頻率的倍數。<br/><br/>[頻率 x 間隔] 判斷頻率 hello 產生配量。 例如，如果您需要 hello 配量每小時的資料集 toobe，您將<b>頻率</b>太<b>小時</b>，和<b>間隔</b>太<b>1</b>。<br/><br/>請注意，如果您指定**頻率**為**分鐘**，您應該設定 hello 間隔 toono 小於 15。 |是 |NA |
| style |指定是否應該在 hello 開頭或結尾 hello 間隔產生 hello 配量。<ul><li>StartOfInterval</li><li>EndOfInterval</li></ul>如果**頻率**設定得**月份**，和**樣式**設定得**為 EndOfInterval**，hello 當月最後一天產生 hello 配量。 如果**樣式**設定得**StartOfInterval**，hello 配量會產生 hello 上個月的第一天。<br/><br/>如果**頻率**設定得**天**，和**樣式**設定得**為 EndOfInterval**，hello 配量會產生在 hello 的 hello 當日的前一個小時。<br/><br/>如果**頻率**設定得**小時**，和**樣式**設定得**為 EndOfInterval**，hello 配量會產生在 hello hello 小時結尾。 比方說，hello 下午 1-2 PM 期間的配量，hello 配量會在 2 PM 產生。 |否 |EndOfInterval |
| anchorDateTime |定義中的 hello 排程器 toocompute 資料集配量界限所使用的時間 hello 絕對位置。 <br/><br/>請注意，如果此 propoerty 具有比 hello 指定頻率，較精細的日期部分 hello 更精細的部分會被忽略。 例如，如果 hello**間隔**是**每小時**(頻率： hour，interval: 1)，和 hello **anchorDateTime**包含**分鐘和秒鐘**，然後 hello 分鐘和秒鐘部分**anchorDateTime**都會被忽略。 |否 |01/01/0001 |
| Offset |哪些 hello 的所有資料集配量的開始與結束移位的 Timespan。 <br/><br/>請注意，如果兩個**anchorDateTime**和**位移**指定，hello 結果是 hello 合併移位。 |否 |NA |

### <a name="offset-example"></a>位移範例
根據預設，每日 (`"frequency": "Day", "interval": 1`) 配量的開始時間是「國際標准時間」(UTC) 上午 12 點 (午夜)。 如果要改為 hello 開始時間 toobe 上午 6 點 UTC 時間，將設定 hello 位移 hello 下列程式碼片段所示： 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a>anchorDateTime 範例
在下列範例的 hello，hello 資料集，會產生一次每 23 的小時。 hello 第一個配量開始所指定的 hello 時間**anchorDateTime**，太設定`2017-04-19T08:00:00`(UTC)。

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a>位移/樣式範例
hello 下列資料集是每月，並會在產生 hello 在 8:00 AM 每月的第 3 (`3.08:00:00`):

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

## <a name="Policy"></a>資料集原則
hello**原則**hello 資料集定義中的區段會定義 hello 準則或 hello 資料集配量的 hello 條件必須滿足。

### <a name="validation-policies"></a>驗證原則
| 原則名稱 | 說明 | 套用太| 必要 | 預設值 |
| --- | --- | --- | --- | --- |
| minimumSizeMB |驗證中的 hello 資料**Azure Blob 儲存體**符合 hello 最小大小需求 （以 mb 為單位）。 |Azure Blob 儲存體 |否 |NA |
| minimumRows |驗證中的 hello 資料**Azure SQL database**或**Azure 資料表**包含 hello 最小數目的資料列。 |<ul><li>Azure SQL Database</li><li>Azure 資料表</li></ul> |否 |NA |

#### <a name="examples"></a>範例
**minimumSizeMB：**

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

**minimumRows：**

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

### <a name="external-datasets"></a>外部資料集
外部資料集是 hello 不由 hello data factory 中執行的管線所產生的項目。 如果 hello 資料集標示為**外部**，hello **ExternalData**原則可能是已定義的 tooinfluence hello 行為 hello 資料集配量的可用性。

除非資料集是由 Data Factory 所產生，否則應該標示為「外部」。 除非正在使用活動或管線鏈結，這項設定通常適用於 toohello 輸入管線中的第一個活動。

| 名稱 | 說明 | 必要 | 預設值 |
| --- | --- | --- | --- |
| dataDelay |hello hello hello 的外部資料可用性檢查 toodelay hello hello 時間指定配量。 例如，您可以使用此設定來延遲每小時檢查。<br/><br/>hello 設定僅適用於 toohello 目前的時間。  例如，如果它是 1:00 PM 現在，這個值為 10 分鐘 hello 驗證就會開始 1:10 PM。<br/><br/>請注意這項設定不會影響在 hello 過去的配量。 針對**配量結束時間** + **dataDelay** < **現在**的配量，處理時將不會有任何延遲。<br/><br/>應該使用 hello 指定時間大於 23:59 小時`day.hours:minutes:seconds`格式。 例如，toospecify 24 小時，請勿使用 24:00:00。 請改用 1.00:00:00。 如果您使用 24:00:00，這會視同 24 天 (24.00:00:00)。 如為 1 天又 4 小時，請指定 1:04:00:00。 |否 |0 |
| retryInterval |hello 失敗與 hello 的下一次嘗試之間的等待時間。 此設定適用於 toopresent 時間。 如果 hello 先前嘗試失敗，hello 下一次嘗試之後 hello **retryInterval**期間。 <br/><br/>如果是 1:00 PM 現在，我們會開始 hello 第一次嘗試。 Hello 下次重試 hello 持續時間 toocomplete hello 第一次驗證檢查是 1 分鐘而且 hello 作業失敗，如果是在 1:00 + 1 分鐘 （持續時間） + 1 分鐘 （重試間隔） = 1: 02PM。 <br/><br/>在 hello 過去的配量，沒有任何延遲。 hello 重試會立即發生。 |否 |00:01:00 (1 分鐘) |
| retryTimeout |每次重試的 hello 逾時。<br/><br/>如果這個屬性設定 too10 分鐘 hello 驗證必須在 10 分鐘內完成。 如果需花時間超過 10 分鐘 tooperform hello 驗證，hello 重試逾時。<br/><br/>如果所有都 hello 驗證逾時，嘗試都 hello 配量會標示為**TimedOut**。 |否 |00:10:00 (10 分鐘) |
| maximumRetry |hello 次數 toocheck hello hello 外部資料可用性。 hello 最大允許值為 10。 |否 |3 |


## <a name="create-datasets"></a>建立資料集
您可以使用下列其中一項工具或 SDK 來建立資料集： 

- 複製精靈 
- Azure 入口網站
- Visual Studio
- PowerShell
- Azure Resource Manager 範本
- REST API
- .NET API

請參閱下列逐步教學課程使用其中一個工具或 Sdk 來建立管線和資料集的 hello:
 
- [使用資料轉換活動來建置管線](data-factory-build-your-first-pipeline.md)
- [使用資料移動活動來建置管線](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

建立及部署管線之後，您可以管理和監視您所使用的管線 hello Azure 入口網站的刀鋒視窗或 hello 監視和管理應用程式。 請參閱下列主題逐步指示的 hello: 

- [使用 Azure 入口網站刀鋒視窗來監視和管理管線](data-factory-monitor-manage-pipelines.md)
- [監視和管理使用 hello 監視和管理應用程式的管線](data-factory-monitor-manage-app.md)


## <a name="scoped-datasets"></a>範圍資料集
您可以建立資料集範圍的 tooa 管線使用 hello**資料集**屬性。 這些資料集僅供此管線內的活動使用，不供其他管線中的活動使用。 hello 下列範例會定義具有兩個資料集 （InputDataset rdc 和 OutputDataset rdc） toobe hello 管線中使用的管線。  

> [!IMPORTANT]
> 單次管線只能搭配支援的已設定領域的資料集 (其中**pipelineMode**設定得**OneTime**)。 如需詳細資訊，請參閱 [一次性管線](data-factory-create-pipelines.md#onetime-pipeline) 。
>
>

```json
{
    "name": "CopyPipeline-rdc",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-rdc"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-rdc"
                    }
                ],
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1,
                    "style": "StartOfInterval"
                },
                "name": "CopyActivity-0"
            }
        ],
        "start": "2016-02-28T00:00:00Z",
        "end": "2016-02-28T00:00:00Z",
        "isPaused": false,
        "pipelineMode": "OneTime",
        "expirationTime": "15.00:00:00",
        "datasets": [
            {
                "name": "InputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "InputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/input",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": true,
                    "policy": {}
                }
            },
            {
                "name": "OutputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "OutputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/output",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": false,
                    "policy": {}
                }
            }
        ]
    }
}
```

## <a name="next-steps"></a>後續步驟
- 如需有關管線的詳細資訊，請參閱[建立管線](data-factory-create-pipelines.md)。 
- 如需有關管線的排程和執行方式的詳細資訊，請參閱 [Azure Data Factory 中的排程和執行](data-factory-scheduling-and-execution.md)。 
