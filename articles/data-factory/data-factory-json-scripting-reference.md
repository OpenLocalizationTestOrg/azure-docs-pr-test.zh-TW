---
title: "aaaAzure Data Factory-JSON 指令碼參考 |Microsoft 文件"
description: "提供 Data Factory 實體的 JSON 結構描述。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 813fd752bb0ecb1b513d022b9f302325105dac31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---json-scripting-reference"></a>Azure Data Factory - JSON 指令碼參考
本文提供 JSON 結構描述和範例來定義 Azure Data Factory 實體 (管線、活動、資料集和連結服務)。  

## <a name="pipeline"></a>管線 
如需管線定義 hello 高階結構如下所示： 

```json
{
  "name": "SamplePipeline",
  "properties": {
    "description": "Describe what pipeline does",
    "activities": [
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

下表描述 hello 管線 JSON 定義中的 hello 屬性：

| 屬性 | 說明 | 必要
-------- | ----------- | --------
| 名稱 | Hello 管線的名稱。 指定代表 hello 活動的 hello 動作的名稱或管線是設定的 toodo<br/><ul><li>字元數目上限︰260</li><li>開頭必須為字母、數字或底線 (_)</li><li>不允許使用下列字元：“.”、“+”、“?”、“/”、“<”、”>”、”*”、”%”、”&”、”:”、”\\”</li></ul> |是 |
| 說明 |描述使用何種 hello 活動或管線做為文字 | 否 |
| 活動 | 包含活動清單。 | 是 |
| start |開始日期-時間 hello 管線。 必須使用 [ISO 格式](http://en.wikipedia.org/wiki/ISO_8601)。 例如︰2014-10-14T16:32:41。 <br/><br/>很可能 toospecify 本地時間，例如預估時間。 範例如下︰`2016-02-27T06:00:00**-05:00`，這是 6 AM EST。<br/><br/>hello 開始和結束屬性一起指定 hello 管線的作用期間。 輸出配量只會在作用中期間內產生。 |否<br/><br/>如果您指定 hello 結束屬性的值，您必須指定 hello 開始屬性值。<br/><br/>hello 開始和結束時間可以是空的 toocreate 管線。 您必須指定這兩個值的作用中期間 hello 管線 toorun tooset。 如果您未指定開始和結束時間時建立管線，您可以設定它們使用 hello 組 AzureRmDataFactoryPipelineActivePeriod 指令程式更新版本。 |
| end |結束日期與時間 hello 管線。 如果已指定，則必須使用 ISO 格式。 例如：2014-10-14T17:32:41 <br/><br/>很可能 toospecify 本地時間，例如預估時間。 範例如下︰`2016-02-27T06:00:00**-05:00`，這是 6 AM EST。<br/><br/>toorun hello 管線無限期地指定 9999-09-09 hello hello end 屬性的值。 |否 <br/><br/>如果您指定 hello 開始屬性的值，您必須指定 hello end 屬性的值。<br/><br/>請參閱備註 hello**啟動**屬性。 |
| isPaused |如果組 tootrue hello 管線不會執行。 預設值 = false。 您可以使用這個屬性 tooenable 或停用。 |否 |
| pipelineMode |hello 管線的可執行的排程 hello 方法。 允許的值包括：scheduled (預設值)、onetime。<br/><br/>排程' 表示該 hello 管線 tooits 作用期間 （開始和結束時間），根據指定的時間間隔執行。 '一次' 表示該 hello 管線只執行一次。 目前，Onetime 管線在建立之後即無法進行修改/更新。 如需 onetime 設定的詳細資料，請參閱 [Onetime 管線](data-factory-create-pipelines.md#onetime-pipeline)。 |否 |
| expirationTime |長時間後建立的 hello 管線有效，且應保持已佈建。 如果它沒有任何作用中、 失敗，或暫止執行，hello 管線則會自動刪除到達 hello 到期時間。 |否 |


## <a name="activity"></a>活動 
hello 管線定義 （活動項目） 中活動的高階結構如下所示：

```json
{
    "name": "ActivityName",
    "description": "description", 
    "type": "<ActivityType>",
    "inputs":  "[]",
    "outputs":  "[]",
    "linkedServiceName": "MyLinkedService",
    "typeProperties":
    {

    },
    "policy":
    {
    }
    "scheduler":
    {
    }
}
```

下列表格說明 hello 活動 JSON 定義中的 hello 屬性：

| Tag | 說明 | 必要 |
| --- | --- | --- |
| 名稱 |Hello 活動名稱。 指定代表 hello 動作 hello 活動的名稱設定 toodo<br/><ul><li>字元數目上限︰260</li><li>開頭必須為字母、數字或底線 (_)</li><li>不允許使用下列字元：“.”、“+”、“?”、“/”、“<”、”>”、”*”、”%”、”&”、”:”、”\\”</li></ul> |是 |
| 說明 |描述用於 hello 活動的文字。 |是 |
| 類型 |指定 hello hello 活動型別。 請參閱 hello[資料存放區](#data-stores)和[資料轉換活動](#data-transformation-activities)區段的不同類型的活動。 |是 |
| 輸入 |Hello 活動所使用的輸入的資料表<br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |是 |
| 輸出 |使用的 hello 活動的輸出的資料表。<br/><br/>`// one output table`<br/>`"outputs":  [ { "name": “outputtable1” } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": “outputtable1” }, { "name": “outputtable2” }  ],` |是 |
| linkedServiceName |Hello 活動所使用的 hello 連結服務名稱。 <br/><br/>活動可能會要求您指定連結 toohello 必要的運算環境的 hello 連結服務。 |對於 HDInsight 活動、Azure Machine Learning 活動和預存程序活動而言為必要。 <br/><br/>否：所有其他 |
| typeProperties |Hello typeProperties > 一節中的屬性取決於 hello 活動的類型。 |否 |
| 原則 |影響 hello hello 活動執行階段行為的原則。 如果未指定，則會使用預設原則。 |否 |
| scheduler |「 排程器 」 屬性是使用的 toodefine 預期 hello 活動的排程。 及其子屬性會 hello 與 hello hello 於相同[可用性屬性集中](data-factory-create-datasets.md#dataset-availability)。 |否 |

### <a name="policies"></a>原則
特別是當處理資料表的 hello 配量時，原則會影響 hello 執行階段行為的活動。 下表中的 hello 提供 hello 詳細資料。

| 屬性 | 允許的值 | 預設值 | 說明 |
| --- | --- | --- | --- |
| 並行 |整數  <br/><br/>最大值：10 |1 |並行執行的 hello 活動的數目。<br/><br/>它決定不同配量上可能發生的平行活動執行的 hello 次數。 例如，如果活動需要透過 toogo 大量可用的資料，具有較大的並行值就會加快 hello 資料處理。 |
| executionPriorityOrder |NewestFirst<br/><br/>OldestFirst |OldestFirst |判斷正在處理的資料配量順序 hello。<br/><br/>例如，如果您有 2 個配量 (一個發生在下午 4 點，另一個發生在下午 5 點)，而兩者都暫停執行。 如果您設定 hello executionpriorityorder 設 toobe NewestFirst，會先處理下午 5 點的 hello 配量。 同樣地如果您設定 hello executionpriorityorder 設 toobe OldestFIrst，然後在下午 4 點 hello 配量會處理。 |
| retry |整數 <br/><br/>最大值可以是 10 |0 |Hello hello 配量的資料處理之前的重試的數目會標示為失敗。 資料配量的活動執行會重試總 toohello 指定重試計數。 hello 重試會儘速 hello 失敗後進行。 |
| timeout |TimeSpan |00:00:00 |Hello 活動的逾時。 範例︰00:10:00 (意指逾時 10 分鐘)<br/><br/>如果未指定值，或為 0，hello 逾時是無限的。<br/><br/>如果配量的 hello 資料處理時間超過 hello 逾時值，則會取消，並 hello 系統會嘗試 tooretry hello 處理。 hello 重試次數取決於 hello 重試屬性。 發生逾時，hello 狀態會設定 tooTimedOut。 |
| delay |TimeSpan |00:00:00 |指定 hello hello 配量開始的資料處理之前的延遲。<br/><br/>hello 延遲 hello 預期執行時間過去後，會啟動 hello 執行之活動的資料配量。<br/><br/>範例︰00:10:00 (意指延遲 10 分鐘) |
| longRetry |整數 <br/><br/>最大值：10 |1 |hello 的長時間重試次數 hello 配量執行失敗。<br/><br/>多個 longRetry 嘗試之間以 longRetryInterval 隔開。 因此，如果您需要 toospecify 重試嘗試之間的時間，請使用 longRetry。 如果指定 Retry 和 longRetry，每個 longRetry 嘗試包含重試次數和 hello 最大嘗試次數為重試 * longRetry。<br/><br/>例如，如果我們有下列 hello 活動原則中的設定的 hello:<br/>Retry：3<br/>longRetry：2<br/>longRetryInterval：01:00:00<br/><br/>假設有一個配量 tooexecute （等待狀態），就會失敗的每次 hello 活動執行。 一開始會有 3 次連續執行嘗試。 每次嘗試之後, hello 配量狀態會是 Retry。 前 3 的嘗試次數已超過之後，hello 配量狀態就會是 LongRetry。<br/><br/>一個小時 (也就是 longRetryInteval 的值) 之後，會有另一組 3 次連續執行嘗試。 之後，hello 配量狀態會變成 Failed，而且會嘗試重試。 因此全部已進行 6 次嘗試。<br/><br/>如果執行成功，hello 配量狀態就會是 Ready，無需重試嘗試。<br/><br/>在位置相依的資料到達在不具決定性的時間或 hello 整體環境穩定底下的資料處理發生的情況下可用 longRetry。 在這種情況下，逐一進行重試可能無法幫助，這樣導致 hello 的時間間隔之後想要的輸出。<br/><br/>提醒：請勿設定較大的 longRetry 或 longRetryInterval 值。 較大的值通常表示其他系統問題。 |
| longRetryInterval |TimeSpan |00:00:00 |hello 長時間重試嘗試之間的延遲 |

### <a name="typeproperties-section"></a>typeProperties 區段
hello typeProperties 區段是不同的每個活動。 轉換活動都只是 hello 類型屬性。 如需在管線中定義轉換活動的 JSON 範例，請參閱本文中的[資料轉換活動](#data-transformation-activities)一節。 

**複製活動**hello typeProperties > 一節中有兩個子區段：**來源**和**接收**。 請參閱[資料存放區](#data-stores)區段在本文中針對 JSON 範例 toouse 資料將儲存為來源及/或接收的方式，顯示。 

### <a name="sample-copy-pipeline"></a>範例複製管線
在下列範例管線 hello，沒有一個活動的型別**複製**在 hello**活動**> 一節。 在此範例中，hello[複製活動](data-factory-data-movement-activities.md)將資料從 Azure Blob 儲存體 tooan Azure SQL database 複製。 

```json
{
  "name": "CopyPipeline",
  "properties": {
    "description": "Copy data from a blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "type": "Copy",
        "inputs": [
          {
            "name": "InputDataset"
          }
        ],
        "outputs": [
          {
            "name": "OutputDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink",
            "writeBatchSize": 10000,
            "writeBatchTimeout": "60:00:00"
          }
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

請注意下列點 hello:

* 在 [hello 活動] 區段中，沒有一個活動其**類型**設定得**複製**。
* 輸入 hello 活動設定太**InputDataset**和輸出 hello 活動設定太**OutputDataset**。
* 在 [hello **typeProperties** ] 區段中， **BlobSource**指定 hello 來源類型為和**SqlSink**指定為 hello 接收器類型。

請參閱[資料存放區](#data-stores)區段在本文中針對 JSON 範例 toouse 資料將儲存為來源及/或接收的方式，顯示。    

建立此管線的完整逐步解說，請參閱[教學課程： 將資料從 Blob 儲存體 tooSQL 資料庫複製](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。 

### <a name="sample-transformation-pipeline"></a>範例轉換管線
在下列範例管線 hello，沒有一個活動的型別**HDInsightHive**在 hello**活動**> 一節。 在此範例中，hello [HDInsight Hive 活動](data-factory-hive-activity.md)執行 Azure HDInsight Hadoop 叢集上的 Hive 指令碼檔案來轉換資料從 Azure Blob 儲存體。 

```json
{
    "name": "TransformPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "AzureStorageLinkedService",
                    "defines": {
                        "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                        "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "policy": {
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Month",
                    "interval": 1
                },
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00",
        "isPaused": false
    }
}
```

請注意下列點 hello: 

* 在 [hello 活動] 區段中，沒有一個活動其**類型**設定得**HDInsightHive**。
* hello Hive 指令碼檔案， **partitionweblogs.hql**，儲存在 hello Azure 儲存體帳戶 (由 hello scriptLinkedService，稱為**AzureStorageLinkedService**)，然後在**指令碼**hello 容器中的資料夾**adfgetstarted**。
* hello**定義**區段是做為 Hive 組態值傳遞 toohello hive 指令碼使用的 toospecify hello 執行階段設定 (例如`${hiveconf:inputtable}`， `${hiveconf:partitionedtable}`)。

如需在管線中定義轉換活動的 JSON 範例，請參閱本文中的[資料轉換活動](#data-transformation-activities)一節。

建立此管線的完整逐步解說，請參閱[教學課程： 建立第一個管線 tooprocess 資料使用 Hadoop 叢集](data-factory-build-your-first-pipeline.md)。 

## <a name="linked-service"></a>連結服務
如需連結的服務定義 hello 高階結構如下所示：

```json
{
    "name": "<name of hello linked service>",
    "properties": {
        "type": "<type of hello linked service>",
        "typeProperties": {
        }
    }
}
```

下列表格說明 hello 活動 JSON 定義中的 hello 屬性：

| 屬性 | 說明 | 必要 |
| -------- | ----------- | -------- | 
| 名稱 | Hello 連結服務名稱。 | 是 | 
| properties - type | Hello 連結服務類型。 例如︰Azure 儲存體、Azure SQL Database。 |
| typeProperties | hello typeProperties 區段具有不同的每個資料存放區或計算環境的項目。 請參閱[資料存放區](#datastores)區段中針對所有的 hello 資料存放區連結的服務和[計算環境](#compute-environments)所有 hello 計算連結的服務 |   

## <a name="dataset"></a>Dataset 
Azure Data Factory 中的資料集定義如下：

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
| 名稱 | Hello 資料集的名稱。 請參閱 [Azure Data Factory - 命名規則](data-factory-naming-rules.md) ，以了解命名規則。 |是 |NA |
| 類型 | hello 資料集的類型。 指定一個支援的 Azure Data Factory 的 hello 類型 (例如： AzureBlob、 AzureSqlTable)。 請參閱[資料存放區](#data-stores)區段中針對所有 hello 資料存放區和資料處理站所支援的資料集類型。 | 
| structure | Hello 資料集的結構描述。 它包含資料行、其類型等。 | 否 |NA |
| typeProperties | 屬性對應 toohello 選取型別。 關於支援的類型和其屬性，請參閱[資料存放區](#data-stores)一節。 |是 |NA |
| external | 布林值旗標 toospecify，是否與否，資料 factory 管線所明確產生資料集。 |否 |false |
| Availability | 定義處理期間，或者 hello 配量模型 hello 資料集的生產環境的 hello。 Hello 資料集配量模型的詳細資訊，請參閱[排程與執行](data-factory-scheduling-and-execution.md)發行項。 |是 |NA |
| 原則 |定義 hello 準則或 hello hello 資料集配量，都必須符合的條件。 <br/><br/>如需詳細資訊，請參閱 [資料集原則](#Policy) 一節。 |否 |NA |

每個資料行中 hello**結構**區段包含下列屬性的 hello:

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 名稱 |Hello 資料行名稱。 |是 |
| 類型 |Hello 資料行資料類型。  |否 |
| culture |.NET 基礎類型指定且為.NET 型別時使用的文化特性 toobe`Datetime`或`Datetimeoffset`。 預設值為 `en-us`。 |否 |
| format |格式化指定類型，並為.NET 型別時所使用的字串 toobe`Datetime`或`Datetimeoffset`。 |否 |

在下列範例的 hello，hello 資料集有三個資料行`slicetimestamp`， `projectname`，和`pageviews`，而且它們的型別： 字串、 字串和小數點分別。

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

hello 下表描述您可以使用在 hello 屬性**可用性**> 一節：

| 屬性 | 說明 | 必要 | 預設值 |
| --- | --- | --- | --- |
| frequency |指定資料集配量實際執行環境的 hello 時間單位。<br/><br/><b>支援的頻率</b>：Minute、Hour、Day、Week、Month |是 |NA |
| interval |指定頻率的倍數<br/><br/>[頻率 x 間隔] 判斷頻率 hello 產生配量。<br/><br/>如果您需要 hello 配量每小時的資料集 toobe，設定<b>頻率</b>太<b>小時</b>，和<b>間隔</b>太<b>1</b>。<br/><br/><b>請注意</b>： 如果您將 Frequency 指定為 Minute，我們建議您設定小於 15 的 hello 間隔 toono |是 |NA |
| style |指定是否應該在 hello 開始/結束 hello 間隔產生 hello 配量。<ul><li>StartOfInterval</li><li>EndOfInterval</li></ul><br/><br/>如果頻率設定 tooMonth 樣式設定 tooEndOfInterval，hello 當月最後一天產生 hello 配量。 如果 hello 樣式設定 tooStartOfInterval，hello 點產生配量 hello 當月第一日。<br/><br/>如果頻率設定 tooDay tooEndOfInterval 設定樣式時，會產生 hello 的 hello 當日的前一個小時 hello 配量。<br/><br/>如果頻率設定 tooHour 樣式設定 tooEndOfInterval，hello 配量會產生在 hello hello 小時結尾。 例如，1 PM – 2 PM 期間的配量，hello 配量會在 2 PM 產生。 |否 |EndOfInterval |
| anchorDateTime |定義中使用的排程器 toocompute 資料集配量界限時間 hello 絕對位置。 <br/><br/><b>請注意</b>： 如果 hello AnchorDateTime 具有比 hello 頻率較精細的日期部分，則 hello 更精細的部分會被忽略。 <br/><br/>例如，如果 hello<b>間隔</b>是<b>每小時</b>(頻率： hour，interval: 1) 和 hello <b>AnchorDateTime</b>包含<b>分鐘和秒鐘</b>然後 hello<b>分鐘和秒鐘</b>hello AnchorDateTime 的部分會被忽略。 |否 |01/01/0001 |
| Offset |哪些 hello 的所有資料集配量的開始與結束移位的 Timespan。 <br/><br/><b>請注意</b>: hello 結果指定 anchorDateTime 和 offset，如果是合併的 hello 移位。 |否 |NA |

下列可用性一節的 hello 指定該 hello 輸出資料集則為產生每小時 （或） 的輸入資料集是每小時可用：

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

hello**原則**資料集定義中的區段會定義 hello 準則或 hello 資料集配量的 hello 條件必須滿足。

| 原則名稱 | 說明 | 套用太| 必要 | 預設值 |
| --- | --- | --- | --- | --- |
| minimumSizeMB |驗證中的 hello 資料**Azure blob**符合 hello 最小大小需求 （以 mb 為單位）。 |Azure Blob |否 |NA |
| minimumRows |驗證中的 hello 資料**Azure SQL database**或**Azure 資料表**包含 hello 最小數目的資料列。 |<ul><li>Azure SQL Database</li><li>Azure 資料表</li></ul> |否 |NA |

**範例：**

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

除非資料集是由 Azure Data Factory 產生，否則應該標示為 **外部**。 除非正在使用活動或管線鏈結，這項設定通常適用於 toohello 輸入管線中的第一個活動。

| 名稱 | 說明 | 必要 | 預設值 |
| --- | --- | --- | --- |
| dataDelay |時間 toodelay hello hello 可用性檢查的 hello hello 指定配量的外部資料。 例如，如果 hello 資料可每小時、 hello 檢查 toosee hello 外部資料而且 hello 對應配量已備妥可以延遲使用 dataDelay。<br/><br/>僅適用於 toohello 目前的時間。  例如，如果它是 1:00 PM 現在，這個值為 10 分鐘 hello 驗證就會開始 1:10 PM。<br/><br/>此設定不會影響在 hello 過去的配量 (以配量結束的時間 + dataDelay 的配量 < 現在) 會處理沒有任何延遲。<br/><br/>時間大於 23:59 小時需要使用 hello toospecified`day.hours:minutes:seconds`格式。 例如，toospecify 24 小時，請勿使用 24:00:00。請改用 1.00:00:00。 如果您使用 24:00:00，這會視同 24 天 (24.00:00:00)。 如為 1 天又 4 小時，請指定 1:04:00:00。 |否 |0 |
| retryInterval |hello 失敗與 hello 下一次的重試嘗試之間的等待時間。 如果嘗試會失敗，retryInterval 之後便為 hello 下一步 再試一次。 <br/><br/>如果是 1:00 PM 現在，我們會開始 hello 第一次嘗試。 Hello 下次重試 hello 持續時間 toocomplete hello 第一次驗證檢查是 1 分鐘而且 hello 作業失敗，如果是在 1:00 + 1 分鐘 （持續時間） + 1 分鐘 （重試間隔） = 1: 02PM。 <br/><br/>在 hello 過去的配量，沒有任何延遲。 hello 重試會立即發生。 |否 |00:01:00 (1 分鐘) |
| retryTimeout |每次重試的 hello 逾時。<br/><br/>如果這個屬性設定 too10 分鐘 hello 驗證需求 toobe 10 分鐘內完成。 如果需花時間超過 10 分鐘 tooperform hello 驗證，hello 重試逾時。<br/><br/>如果所有嘗試都 hello 驗證都逾時，hello 配量會標示為已逾時。 |否 |00:10:00 (10 分鐘) |
| maximumRetry |次數 toocheck hello hello 外部資料可用性。 hello 允許最大值為 10。 |否 |3 |


## <a name="data-stores"></a>資料存放區
hello[連結服務](#linked-service)> 一節提供描述常見的 tooall 類型的連結服務的 JSON 元素。 本節提供有關屬於特定 tooeach 資料存放區的 JSON 元素的詳細資料。

hello[資料集](#dataset)是常見的資料集的 tooall 類型的 JSON 元素 > 一節提供描述。 本節提供有關屬於特定 tooeach 資料存放區的 JSON 元素的詳細資料。

hello[活動](#activity)是常見的活動 tooall 類型的 JSON 元素 > 一節提供描述。 本節提供有關特定 tooeach 資料存放區時，它會當做來源/接收器複製活動中使用的 JSON 元素的詳細資料。  

按一下 hello hello 存放區中，使用您感興趣 toosee hello JSON 結構描述連結的服務，資料集，以及 hello 來源/接收器 hello 複製活動的連結。

| 類別 | 資料存放區 
|:--- |:--- |
| **Azure** |[Azure Blob 儲存體](#azure-blob-storage) |
| &nbsp; |[Azure Data Lake Store](#azure-datalake-store) |
| &nbsp; |[Azure Cosmos DB](#azure-cosmos-db) |
| &nbsp; |[Azure SQL Database](#azure-sql-database) |
| &nbsp; |[Azure SQL 資料倉儲](#azure-sql-data-warehouse) |
| &nbsp; |[Azure 搜尋服務](#azure-search) |
| &nbsp; |[Azure 表格儲存體](#azure-table-storage) |
| **資料庫** |[Amazon Redshift](#amazon-redshift) |
| &nbsp; |[IBM DB2](#ibm-db2) |
| &nbsp; |[MySQL](#mysql) |
| &nbsp; |[Oracle](#oracle) |
| &nbsp; |[PostgreSQL](#postgresql) |
| &nbsp; |[SAP Business Warehouse](#sap-business-warehouse) |
| &nbsp; |[SAP HANA](#sap-hana) |
| &nbsp; |[SQL Server](#sql-server) |
| &nbsp; |[Sybase](#sybase) |
| &nbsp; |[Teradata](#teradata) |
| **NoSQL** |[Cassandra](#cassandra) |
| &nbsp; |[MongoDB](#mongodb) |
| **檔案** |[Amazon S3](#amazon-s3) |
| &nbsp; |[檔案系統](#file-system) |
| &nbsp; |[FTP](#ftp) |
| &nbsp; |[HDFS](#hdfs) |
| &nbsp; |[SFTP](#sftp) |
| **其他** |[HTTP](#http) |
| &nbsp; |[OData](#odata) |
| &nbsp; |[ODBC](#odbc) |
| &nbsp; |[Salesforce](#salesforce) |
| &nbsp; |[Web 資料表](#web-table) |

## <a name="azure-blob-storage"></a>Azure Blob 儲存體

### <a name="linked-service"></a>連結服務
有兩種連結服務類型︰Azure 儲存體連結服務和 Azure 儲存體 SAS 連結服務。

#### <a name="azure-storage-linked-service"></a>Azure 儲存體連結服務
toolink 您 Azure 儲存體帳戶 tooa 的 data factory 使用 hello**帳戶金鑰**，建立 Azure 儲存體連結服務。 toodefine Azure 儲存體連結服務，設定 hello**類型**hello 的連結服務太**AzureStorage**。 然後，您可以指定下列屬性在 hello **typeProperties** > 一節：  

| 屬性 | 說明 | 必要 |
|:--- |:--- |:--- |
| connectionString |指定所需的資訊 tooconnect tooAzure 儲存體 hello connectionString 屬性。 |是 |

##### <a name="example"></a>範例  

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

#### <a name="azure-storage-sas-linked-service"></a>Azure 儲存體 SAS 連結服務
hello Azure 儲存體 SAS 連結服務可讓您 Azure 儲存體帳戶 tooan Azure data factory toolink 使用共用存取簽章 (SAS)。 它提供 hello 資料 factory 限制/時間繫結存取 tooall/特定資源 （blob/容器） hello 儲存體中。 toolink 使用共用存取簽章、 您 Azure 儲存體帳戶 tooa data factory 建立 Azure 儲存體 SAS 連結服務。 Azure 儲存體 SAS toodefine 連結服務，設定 hello**類型**hello 的連結服務太**AzureStorageSas**。 然後，您可以指定下列屬性在 hello **typeProperties** > 一節：   

| 屬性 | 說明 | 必要 |
|:--- |:--- |:--- |
| sasUri |指定共用存取簽章 URI toohello Azure 儲存體資源，例如 blob、 容器或資料表。 |是 |

##### <a name="example"></a>範例

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

如需這些連結服務的詳細資訊，請參閱 [Azure Blob 儲存體連接器](data-factory-azure-blob-connector.md#linked-service-properties)文件。 

### <a name="dataset"></a>Dataset
toodefine Azure Blob 資料集設定 hello**類型**hello 資料集太**AzureBlob**。 然後，指定下列 Azure Blob 中 hello 的特定屬性的 hello **typeProperties** > 一節： 

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| folderPath |路徑 toohello 容器，並且在 hello blob 儲存體中的資料夾。 範例：myblobcontainer\myblobfolder\ |是 |
| fileName |Hello blob 名稱。 fileName 是選擇性的，而且區分大小寫。<br/><br/>如果您在上指定的檔名、 hello 活動 （包括複製） 運作 hello 特定 Blob。<br/><br/>若未指定檔名，複本會輸入資料集的 hello folderPath 中包含所有 Blob。<br/><br/>當檔案名稱未指定輸出資料集時，會在遵循此格式的 hello hello hello 產生檔案名稱： 資料。<Guid>.txt (例如:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |否 |
| partitionedBy |partitionedBy 是選擇性的屬性。 您可以使用它 toospecify 動態 folderPath 和 filename 時間序列資料的。 例如，folderPath 可針對每小時的資料進行參數化。 |否 |
| format | 支援下列格式類型的 hello: **TextFormat**， **JsonFormat**， **AvroFormat**， **OrcFormat**， **ParquetFormat**。 設定 hello**類型**下格式 tooone 這些值的屬性。 如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。 <br><br> 如果您想太**複製檔做為-是**之間以檔案為基礎存放區 （二進位複製），略過這兩個輸入和輸出資料集定義中的 hello 格式 > 一節。 |否 |
| compression | 指定 hello 類型和層級的 hello 資料壓縮。 支援的類型為：**GZip**、**Deflate**、**BZip2** 及 **ZipDeflate**。 支援的層級為：**Optimal** 和 **Fastest**。 如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。 |否 |

#### <a name="example"></a>範例

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


如需詳細資訊，請參閱 [Azure Blob 連接器](data-factory-azure-blob-connector.md#dataset-properties)文件。

### <a name="blobsource-in-copy-activity"></a>複製活動中的 BlobSource
如果您從 Azure Blob 儲存體複製資料，設定 hello**來源類型**的 hello 複製活動太**BlobSource**，並指定下列屬性在 hello * * 來源 * * 區段：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| 遞迴 |指出是否 hello 讀取資料以遞迴方式從 hello 子資料夾，或只能從 hello 指定的資料夾。 |True (預設值)、False |否 |

#### <a name="example-blobsource"></a>範例︰BlobSource**
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
### <a name="blobsink-in-copy-activity"></a>複製活動中的 BlobSink
如果您要複製資料 tooan Azure Blob 儲存體，請設定 hello**接收器類型**的 hello 複製活動太**BlobSink**，並指定下列屬性在 hello**接收**> 一節：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| copyBehavior |Hello 來源 BlobSource 或檔案系統時，請定義 hello 複製行為。 |<b>PreserveHierarchy</b>： 保留 hello hello 目標資料夾中的檔案階層。 hello 的來源檔案 toosource 資料夾的相對路徑會是相同 toohello 的目標檔案 tootarget 資料夾的相對路徑。<br/><br/><b>FlattenHierarchy</b>: hello 來源資料夾中的所有檔案都位於 hello 第一次層級的目標資料夾。 hello 目標檔案已自動產生的名稱。 <br/><br/><b>MergeFiles （預設值）：</b>合併 hello 來源資料夾 tooone 檔案中的所有檔案。 如果指定 hello/Blob 檔案的名稱，則 hello 合併的檔案名稱就是指定之名稱; hello否則，將會自動產生的檔案名稱。 |否 |

#### <a name="example-blobsink"></a>範例︰BlobSink

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

如需詳細資訊，請參閱 [Azure Blob 連接器](data-factory-azure-blob-connector.md#copy-activity-properties)文件。 

## <a name="azure-data-lake-store"></a>Azure Data Lake Store

### <a name="linked-service"></a>連結服務
toodefine 連結 Azure Data Lake Store 服務，hello 集 hello 類型的連結服務太**AzureDataLakeStore**，並指定下列屬性在 hello **typeProperties** > 一節：  

| 屬性 | 說明 | 必要 |
|:--- |:--- |:--- |
| 類型 | hello 類型屬性必須設定為： **AzureDataLakeStore** | 是 |
| dataLakeStoreUri | 指定 hello Azure Data Lake Store 帳戶的相關資訊。 在下列格式的 hello:`https://[accountname].azuredatalakestore.net/webhdfs/v1`或`adl://[accountname].azuredatalakestore.net/`。 | 是 |
| subscriptionId | 所屬的 azure 訂用帳戶 Id toowhich 資料湖存放區。 | 接收 (Sink) 的必要項目 |
| resourceGroupName | 所屬的 azure 資源群組名稱 toowhich 資料湖存放區。 | 接收 (Sink) 的必要項目 |
| servicePrincipalId | 指定 hello 應用程式的用戶端識別碼。 | 是 (適用於服務主體驗證) |
| servicePrincipalKey | 指定 hello 應用程式的金鑰。 | 是 (適用於服務主體驗證) |
| tenant | 指定在您的應用程式所在的 hello 租用戶資訊 (網域名稱或租用戶 ID)。 您可以透過暫留在 hello 右上角的 hello Azure 入口網站中的 hello 滑鼠擷取它。 | 是 (適用於服務主體驗證) |
| 授權 | 按一下**授權**按鈕在 hello **Data Factory 編輯器**並輸入您 hello 自動產生的授權 URL toothis 屬性指派的認證。 | 是 (適用於使用者認證驗證)|
| sessionId | 從 hello OAuth 授權工作階段的 OAuth 工作階段識別碼。 每個工作階段識別碼都是唯一的，只能使用一次。 當您使用 Data Factory 編輯器時便會自動產生此設定。 | 是 (適用於使用者認證驗證) |

#### <a name="example-using-service-principal-authentication"></a>範例：使用服務主體驗證
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info. Example: microsoft.onmicrosoft.com>"
        }
    }
}
```

#### <a name="example-using-user-credential-authentication"></a>範例︰使用使用者認證驗證
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

如需詳細資訊，請參閱 [Azure Data Lake Store 連接器](data-factory-azure-datalake-connector.md#linked-service-properties)文件。 

### <a name="dataset"></a>Dataset
toodefine Azure 資料湖存放區資料集設定 hello**類型**hello 資料集太**AzureDataLakeStore**，並指定下列屬性在 hello hello **typeProperties**> 一節： 

| 屬性 | 說明 | 必要 |
|:--- |:--- |:--- |
| folderPath |路徑 toohello 容器和資料夾在 hello Azure 資料湖存放區。 |是 |
| fileName |Hello Azure 資料湖存放區中的 hello 檔案的名稱。 fileName 是選擇性的，而且區分大小寫。 <br/><br/>如果您指定的檔名，hello 活動 （包括複製） 適用於 hello 特定檔案。<br/><br/>若未指定檔名，複本會輸入資料集的 hello folderPath 中包含所有檔案。<br/><br/>當檔案名稱未指定輸出資料集時，會在遵循此格式的 hello hello hello 產生檔案名稱： 資料。<Guid>.txt (例如:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |否 |
| partitionedBy |partitionedBy 是選擇性的屬性。 您可以使用它 toospecify 動態 folderPath 和 filename 時間序列資料的。 例如，folderPath 可針對每小時的資料進行參數化。 |否 |
| format | 支援下列格式類型的 hello: **TextFormat**， **JsonFormat**， **AvroFormat**， **OrcFormat**， **ParquetFormat**。 設定 hello**類型**下格式 tooone 這些值的屬性。 如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。 <br><br> 如果您想太**複製檔做為-是**之間以檔案為基礎存放區 （二進位複製），略過這兩個輸入和輸出資料集定義中的 hello 格式 > 一節。 |否 |
| compression | 指定 hello 類型和層級的 hello 資料壓縮。 支援的類型為：**GZip**、**Deflate**、**BZip2** 及 **ZipDeflate**。 支援的層級為：**Optimal** 和 **Fastest**。 如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。 |否 |

#### <a name="example"></a>範例
```json
{
    "name": "AzureDataLakeStoreInput",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
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

如需詳細資訊，請參閱 [Azure Data Lake Store 連接器](data-factory-azure-datalake-connector.md#dataset-properties)文件。 

### <a name="azure-data-lake-store-source-in-copy-activity"></a>複製活動中的 Azure Data Lake Store 來源
如果您從 Azure 資料湖存放區複製資料，設定 hello**來源類型**的 hello 複製活動太**AzureDataLakeStoreSource**，並指定下列屬性在 hello**來源** > 一節：

**AzureDataLakeStoreSource**支援下列屬性的 hello **typeProperties** > 一節：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| 遞迴 |指出是否 hello 讀取資料以遞迴方式從 hello 子資料夾，或只能從 hello 指定的資料夾。 |True (預設值)、False |否 |

#### <a name="example-azuredatalakestoresource"></a>範例：AzureDataLakeStoreSource

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureDakeLaketoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureDataLakeStoreInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureDataLakeStoreSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

如需詳細資訊，請參閱 [Azure Data Lake Store 連接器](data-factory-azure-datalake-connector.md#copy-activity-properties)文件。

### <a name="azure-data-lake-store-sink-in-copy-activity"></a>複製活動中的 Azure Data Lake Store 接收
如果您要複製資料 tooan Azure 資料湖存放區，請設定 hello**接收器類型**的 hello 複製活動太**AzureDataLakeStoreSink**，並指定下列屬性在 hello**接收**> 一節：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| copyBehavior |指定 hello 複製行為。 |<b>PreserveHierarchy</b>： 保留 hello hello 目標資料夾中的檔案階層。 hello 的來源檔案 toosource 資料夾的相對路徑會是相同 toohello 的目標檔案 tootarget 資料夾的相對路徑。<br/><br/><b>FlattenHierarchy</b>: hello 第一個層級的目標資料夾中建立 hello 來源資料夾中的所有檔案。 會使用自動產生的名稱建立 hello 目標檔案。<br/><br/><b>MergeFiles</b>： 合併 hello 來源資料夾 tooone 檔案中的所有檔案。 如果指定 hello/Blob 檔案的名稱，則 hello 合併的檔案名稱就是指定之名稱; hello否則，將會自動產生的檔案名稱。 |否 |

#### <a name="example-azuredatalakestoresink"></a>範例：AzureDataLakeStoreSink
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoDataLake",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureDataLakeStoreOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureDataLakeStoreSink"
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
        }]
    }
}
```

如需詳細資訊，請參閱 [Azure Data Lake Store 連接器](data-factory-azure-datalake-connector.md#copy-activity-properties)文件。 

## <a name="azure-cosmos-db"></a>Azure Cosmos DB  

### <a name="linked-service"></a>連結服務
toodefine Azure Cosmos DB 的連結服務，設定 hello**類型**hello 的連結服務太**DocumentDb**，並指定下列屬性在 hello **typeProperties**區段：  

| **屬性** | **說明** | **必要** |
| --- | --- | --- |
| connectionString |指定所需 tooconnect tooAzure Cosmos DB 資料庫的資訊。 |是 |

#### <a name="example"></a>範例

```json
{
    "name": "CosmosDBLinkedService",
    "properties": {
        "type": "DocumentDb",
        "typeProperties": {
            "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
        }
    }
}
```
如需詳細資訊，請參閱 [Azure Cosmos DB 連接器](data-factory-azure-documentdb-connector.md#linked-service-properties)一文。

### <a name="dataset"></a>Dataset
toodefine Azure Cosmos DB 資料集設定 hello**類型**hello 資料集太**DocumentDbCollection**，並指定下列屬性在 hello hello **typeProperties**區段： 

| **屬性** | **說明** | **必要** |
| --- | --- | --- |
| collectionName |Hello Azure Cosmos DB 集合的名稱。 |是 |

#### <a name="example"></a>範例

```json
{
    "name": "PersonCosmosDBTable",
    "properties": {
        "type": "DocumentDbCollection",
        "linkedServiceName": "CosmosDBLinkedService",
        "typeProperties": {
            "collectionName": "Person"
        },
        "external": true,
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```
如需詳細資訊，請參閱 [Azure Cosmos DB 連接器](data-factory-azure-documentdb-connector.md#dataset-properties)一文。

### <a name="azure-cosmos-db-collection-source-in-copy-activity"></a>複製活動中的 Azure Cosmos DB 集合來源
如果您從 Azure Cosmos DB 複製資料，設定 hello**來源類型**的 hello 複製活動太**DocumentDbCollectionSource**，並指定下列屬性在 hello**來源** > 一節：


| **屬性** | **說明** | **允許的值** | **必要** |
| --- | --- | --- | --- |
| query |指定 hello 查詢 tooread 資料。 |Azure Cosmos DB 所支援的查詢字串。 <br/><br/>範例： `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"` |否 <br/><br/>如果未指定，hello 執行的 SQL 陳述式：`select <columns defined in structure> from mycollection` |
| nestingSeparator |巢狀 hello 文件的特殊字元 tooindicate |任何字元。 <br/><br/>Azure Cosmos DB 是 JSON 文件的 NoSQL 存放區 (允許巢狀結構)。 Azure Data Factory 可讓使用者 toodenote 階層 nestingSeparator，也就是透過 「。 」 在上述範例 hello。 Hello 分隔符號 hello 複製活動會產生三個子系的元素與 hello"Name"物件第一個中間和最後一個、 相應 too"Name.First"，"Name.Middle"和"Name.Last"hello 在資料表定義。 |否 |

#### <a name="example"></a>範例

```json
{
    "name": "DocDbToBlobPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "DocumentDbCollectionSource",
                    "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
                    "nestingSeparator": "."
                },
                "sink": {
                    "type": "BlobSink",
                    "blobWriterAddHeader": true,
                    "writeBatchSize": 1000,
                    "writeBatchTimeout": "00:00:59"
                }
            },
            "inputs": [{
                "name": "PersonCosmosDBTable"
            }],
            "outputs": [{
                "name": "PersonBlobTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromCosmosDbToBlob"
        }],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00"
    }
}
```

### <a name="azure-cosmos-db-collection-sink-in-copy-activity"></a>複製活動中的 Azure Cosmos DB 集合接收器
如果您要複製資料 tooAzure Cosmos DB，請設定 hello**接收器類型**的 hello 複製活動太**DocumentDbCollectionSink**，並指定下列屬性在 hello**接收**> 一節：

| **屬性** | **說明** | **允許的值** | **必要** |
| --- | --- | --- | --- |
| nestingSeparator |需要 hello 來源資料行名稱 tooindicate 巢狀文件中的特殊字元。 <br/><br/>例如上述： `Name.First` hello 輸出資料表會產生下列 JSON 結構 hello Cosmos DB 文件中的 hello:<br/><br/>"Name": {<br/>    "First": "John"<br/>}, |為使用的 tooseparate 巢狀層級的字元。<br/><br/>預設值為 `.` (點)。 |為使用的 tooseparate 巢狀層級的字元。 <br/><br/>預設值為 `.` (點)。 |
| writeBatchSize |並行要求數目 tooAzure Cosmos DB 服務 toocreate 文件。<br/><br/>使用這個屬性來複製資料從 Azure Cosmos DB 時，您可以微調 hello 效能。 當您增加叫用 writeBatchSize，因為會傳送多個平行要求 tooAzure Cosmos DB 時，您可以預期更佳的效能。 不過，您必須先 tooavoid 節流，可擲回 hello 錯誤訊息: 「 要求率非常大 」。<br/><br/>節流是由許多因素所決定，包括文件大小、文件中的詞彙數目、目標集合的檢索原則等。複製作業，您可以使用較佳的集合 (例如，S3) toohave hello 大部分可用的輸送量 （2500 的要求單位/秒）。 |Integer |否 (預設值：5) |
| writeBatchTimeout |在逾時之前，請等待 hello 作業 toocomplete 時間。 |時間範圍<br/><br/> 範例：“00:30:00” (30 分鐘)。 |否 |

#### <a name="example"></a>範例

```json
{
    "name": "BlobToDocDbPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "DocumentDbCollectionSink",
                    "nestingSeparator": ".",
                    "writeBatchSize": 2,
                    "writeBatchTimeout": "00:00:00"
                },
                "translator": {
                    "type": "TabularTranslator",
                    "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix"
                }
            },
            "inputs": [{
                "name": "PersonBlobTableIn"
            }],
            "outputs": [{
                "name": "PersonCosmosDbTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromBlobToCosmosDb"
        }],
        "start": "2016-04-14T00:00:00",
        "end": "2016-04-15T00:00:00"
    }
}
```

如需詳細資訊，請參閱 [Azure Cosmos DB 連接器](data-factory-azure-documentdb-connector.md#copy-activity-properties)一文。

## <a name="azure-sql-database"></a>Azure SQL Database

### <a name="linked-service"></a>連結服務
Azure SQL Database toodefine 連結服務，設定 hello**類型**hello 的連結服務太**AzureSqlDatabase**，並指定下列屬性在 hello **typeProperties**> 一節：  

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| connectionString |指定所需的資訊 tooconnect toohello Azure SQL Database 執行個體 hello connectionString 屬性。 |是 |

#### <a name="example"></a>範例
```json
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

如需詳細資訊，請參閱 [Azure SQL 連接器](data-factory-azure-sql-connector.md#linked-service-properties)文件。 

### <a name="dataset"></a>Dataset
toodefine 是 Azure SQL Database 資料集，設定 hello**類型**hello 資料集太**AzureSqlTable**，並指定下列屬性在 hello hello **typeProperties**區段： 

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| tableName |參照 hello 資料表或檢視中的連結服務的 hello Azure SQL Database 執行個體的名稱。 |是 |

#### <a name="example"></a>範例

```json
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
如需詳細資訊，請參閱 [Azure SQL 連接器](data-factory-azure-sql-connector.md#dataset-properties)文件。 

### <a name="sql-source-in-copy-activity"></a>複製活動中的 SQL 來源
如果您從 Azure SQL Database 中複製資料，設定 hello**來源類型**的 hello 複製活動太**SqlSource**，並指定下列屬性在 hello**來源**區段：


| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| SqlReaderQuery |使用自訂查詢 tooread hello 的資料。 |SQL 查詢字串。 範例： `select * from MyTable`. |否 |
| sqlReaderStoredProcedureName |名稱的 hello 預存程序會從 hello 來源資料表讀取資料。 |名稱的 hello 預存程序。 |否 |
| storedProcedureParameters |Hello 參數，預存程序。 |名稱/值組。 名稱和大小寫的參數必須符合 hello 名稱和大小寫的 hello 預存程序參數。 |否 |

#### <a name="example"></a>範例

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
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
        }]
    }
}
```
如需詳細資訊，請參閱 [Azure SQL 連接器](data-factory-azure-sql-connector.md#copy-activity-properties)文件。 

### <a name="sql-sink-in-copy-activity"></a>複製活動中的 SQL 接收
如果您要複製資料 tooAzure SQL 資料庫，請設定 hello**接收器類型**的 hello 複製活動太**SqlSink**，並指定下列屬性在 hello**接收**> 一節：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| writeBatchTimeout |在逾時之前，請等待 hello 批次插入作業 toocomplete 時間。 |時間範圍<br/><br/> 範例：“00:30:00” (30 分鐘)。 |否 |
| writeBatchSize |當 hello 緩衝區大小到達叫用 writeBatchSize 時，請將資料插入 hello SQL 資料表。 |整數 (資料列數目) |否 (預設值：10000) |
| sqlWriterCleanupScript |複製活動 tooexecute 查詢指定的特定配量的資料清除。 |查詢陳述式。 |否 |
| sliceIdentifierColumnName |指定複製活動 toofill 的資料行名稱與自動產生配量識別項，也就是使用的 tooclean 何時重新執行的特定配量的資料。 |資料類型為 binary(32) 之資料行的資料行名稱。 |否 |
| sqlWriterStoredProcedureName |名稱的 hello 預存程序 upserts （更新/插入） 資料到 hello 目標資料表。 |名稱的 hello 預存程序。 |否 |
| storedProcedureParameters |Hello 參數，預存程序。 |名稱/值組。 名稱和大小寫的參數必須符合 hello 名稱和大小寫的 hello 預存程序參數。 |否 |
| sqlWriterTableType |指定用於 hello 預存程序中的資料表類型名稱 toobe。 複製活動移動 hello 資料可讓在暫存資料表與此資料表類型。 預存程序程式碼可以再合併 hello 資料會被複製現有的資料。 |資料表類型名稱。 |否 |

#### <a name="example"></a>範例

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
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
        }]
    }
}
```

如需詳細資訊，請參閱 [Azure SQL 連接器](data-factory-azure-sql-connector.md#copy-activity-properties)文件。 

## <a name="azure-sql-data-warehouse"></a>Azure SQL 資料倉儲

### <a name="linked-service"></a>連結服務
Azure SQL 資料倉儲 toodefine 連結服務，設定 hello**類型**hello 的連結服務太**AzureSqlDW**，並指定下列屬性在 hello **typeProperties**> 一節：  

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| connectionString |指定所需的資訊 tooconnect toohello Azure SQL 資料倉儲執行個體 hello connectionString 屬性。 |是 |



#### <a name="example"></a>範例

```json
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

如需詳細資訊，請參閱 [Azure SQL 資料倉儲連接器](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties)文件。 

### <a name="dataset"></a>Dataset
toodefine 是 Azure SQL 資料倉儲資料集，設定 hello**類型**hello 資料集太**AzureSqlDWTable**，並指定下列屬性在 hello hello **typeProperties**> 一節： 

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| tableName |參照 hello 資料表或檢視 hello 連結的服務的 hello Azure SQL 資料倉儲資料庫中的名稱。 |是 |

#### <a name="example"></a>範例

```json
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

如需詳細資訊，請參閱 [Azure SQL 資料倉儲連接器](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties)文件。 

### <a name="sql-dw-source-in-copy-activity"></a>複製活動中的 SQL DW 來源
如果您要從 Azure SQL 資料倉儲來複製資料，設定 hello**來源類型**的 hello 複製活動太**SqlDWSource**，並指定下列屬性在 hello**來源**> 一節：


| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| SqlReaderQuery |使用自訂查詢 tooread hello 的資料。 |SQL 查詢字串。 例如： `select * from MyTable`。 |否 |
| sqlReaderStoredProcedureName |名稱的 hello 預存程序會從 hello 來源資料表讀取資料。 |名稱的 hello 預存程序。 |否 |
| storedProcedureParameters |Hello 參數，預存程序。 |名稱/值組。 名稱和大小寫的參數必須符合 hello 名稱和大小寫的 hello 預存程序參數。 |否 |

#### <a name="example"></a>範例

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLDWtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSqlDWInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
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
        }]
    }
}
```

如需詳細資訊，請參閱 [Azure SQL 資料倉儲連接器](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)文件。 

### <a name="sql-dw-sink-in-copy-activity"></a>複製活動中的 SQL DW 接收
如果您複製資料 tooAzure SQL 資料倉儲，設定 hello**接收器類型**的 hello 複製活動太**SqlDWSink**，並指定下列屬性在 hello**接收**區段：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| sqlWriterCleanupScript |複製活動 tooexecute 查詢指定的特定配量的資料清除。 |查詢陳述式。 |否 |
| allowPolyBase |指出是否 toouse PolyBase （如果適用的話），而不是 BULKINSERT 機制。 <br/><br/> **使用 PolyBase 是建議的方式 tooload 資料到 SQL 資料倉儲的 hello。** |True <br/>FALSE (預設值) |否 |
| polyBaseSettings |一組屬性，可指定當 hello **allowPolybase**屬性設定太**true**。 |&nbsp; |否 |
| rejectValue |指定 hello 數目或百分比的 hello 查詢失敗前，可能會拒絕的資料列。 <br/><br/>深入了解 hello PolyBase 拒絕之選項的 hello**引數**區段[CREATE EXTERNAL TABLE (TRANSACT-SQL)](https://msdn.microsoft.com/library/dn935021.aspx)主題。 |0 (預設值)、1、2、… |否 |
| rejectType |指定是否要將 hello rejectValue 選項指定為常值或百分比。 |值 (預設值)、百分比 |否 |
| rejectSampleValue |決定 hello 數量的資料列 tooretrieve hello PolyBase 重新計算 hello 百分比的已拒絕的資料列之前。 |1、2、… |是，如果 **rejectType** 是 **percentage** |
| useTypeDefault |指定如何 toohandle 遺漏值中的分隔的文字檔案 PolyBase hello 文字檔案中擷取的資料時。<br/><br/>深入了解來自 hello 引數 > 一節中的這個屬性[CREATE EXTERNAL FILE FORMAT (TRANSACT-SQL)](https://msdn.microsoft.com/library/dn935026.aspx)。 |True/False (預設值為 False) |否 |
| writeBatchSize |用戶端 hello 緩衝區的大小達到叫用 writeBatchSize 時，將資料插入 hello SQL 資料表 |整數 (資料列數目) |否 (預設值：10000) |
| writeBatchTimeout |在逾時之前，請等待 hello 批次插入作業 toocomplete 時間。 |時間範圍<br/><br/> 範例：“00:30:00” (30 分鐘)。 |否 |

#### <a name="example"></a>範例

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQLDW",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlDWOutput"
            }],
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
        }]
    }
}
```

如需詳細資訊，請參閱 [Azure SQL 資料倉儲連接器](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)文件。 

## <a name="azure-search"></a>Azure 搜尋服務

### <a name="linked-service"></a>連結服務
Azure 搜尋 toodefine 連結服務，設定 hello**類型**hello 的連結服務太**AzureSearch**，並指定下列屬性在 hello **typeProperties**區段：  

| 屬性 | 說明 | 必要 |
| -------- | ----------- | -------- |
| url | Hello Azure 搜尋服務的 URL。 | 是 |
| key | Hello Azure 搜尋服務的管理金鑰。 | 是 |

#### <a name="example"></a>範例

```json
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

如需詳細資訊，請參閱 [Azure 搜尋服務連接器](data-factory-azure-search-connector.md#linked-service-properties)文件。

### <a name="dataset"></a>Dataset
toodefine Azure 搜尋資料集設定 hello**類型**hello 資料集太**AzureSearchIndex**，並指定下列屬性在 hello hello **typeProperties**區段: 

| 屬性 | 說明 | 必要 |
| -------- | ----------- | -------- |
| 類型 | hello type 屬性必須設定得**AzureSearchIndex**。| 是 |
| IndexName | Hello Azure 搜尋索引的名稱。 Data Factory 不會建立 hello 索引。 hello 索引必須存在於 Azure 搜尋中。 | 是 |

#### <a name="example"></a>範例

```json
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties": {
            "indexName": "products"
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
    }
}
```

如需詳細資訊，請參閱 [Azure 搜尋服務連接器](data-factory-azure-search-connector.md#dataset-properties)文件。

### <a name="azure-search-index-sink-in-copy-activity"></a>複製活動中的 Azure 搜尋服務索引接收
如果您要複製資料 tooan Azure 搜尋索引，請設定 hello**接收器類型**的 hello 複製活動太**AzureSearchIndexSink**，並指定下列屬性在 hello**接收**> 一節：

| 屬性 | 說明 | 允許的值 | 必要 |
| -------- | ----------- | -------------- | -------- |
| WriteBehavior | 指定是否 toomerge 或取代文件時已存在於 hello 索引。 | 合併 (預設值)<br/>上傳| 否 |
| WriteBatchSize | 將資料上傳至 hello Azure 搜尋索引，當 hello 緩衝區大小到達叫用 writeBatchSize 時。 | 1 too1，000。 預設值為 1000。 | 否 |

#### <a name="example"></a>範例

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoAzureSearchIndex",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureSearchIndexDataset"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "AzureSearchIndexSink"
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
        }]
    }
}
```

如需詳細資訊，請參閱 [Azure 搜尋服務連接器](data-factory-azure-search-connector.md#copy-activity-properties)文件。

## <a name="azure-table-storage"></a>Azure 表格儲存體

### <a name="linked-service"></a>連結服務
有兩種連結服務類型︰Azure 儲存體連結服務和 Azure 儲存體 SAS 連結服務。

#### <a name="azure-storage-linked-service"></a>Azure 儲存體連結服務
toolink 您 Azure 儲存體帳戶 tooa 的 data factory 使用 hello**帳戶金鑰**，建立 Azure 儲存體連結服務。 toodefine Azure 儲存體連結服務，設定 hello**類型**hello 的連結服務太**AzureStorage**。 然後，您可以指定下列屬性在 hello **typeProperties** > 一節：  

| 屬性 | 說明 | 必要 |
|:--- |:--- |:--- |
| 類型 |hello 類型屬性必須設定為： **AzureStorage** |是 |
| connectionString |指定所需的資訊 tooconnect tooAzure 儲存體 hello connectionString 屬性。 |是 |

**範例：**  

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

#### <a name="azure-storage-sas-linked-service"></a>Azure 儲存體 SAS 連結服務
hello Azure 儲存體 SAS 連結服務可讓您 Azure 儲存體帳戶 tooan Azure data factory toolink 使用共用存取簽章 (SAS)。 它提供 hello 資料 factory 限制/時間繫結存取 tooall/特定資源 （blob/容器） hello 儲存體中。 toolink 使用共用存取簽章、 您 Azure 儲存體帳戶 tooa data factory 建立 Azure 儲存體 SAS 連結服務。 Azure 儲存體 SAS toodefine 連結服務，設定 hello**類型**hello 的連結服務太**AzureStorageSas**。 然後，您可以指定下列屬性在 hello **typeProperties** > 一節：   

| 屬性 | 說明 | 必要 |
|:--- |:--- |:--- |
| 類型 |hello 類型屬性必須設定為： **AzureStorageSas** |是 |
| sasUri |指定共用存取簽章 URI toohello Azure 儲存體資源，例如 blob、 容器或資料表。 |是 |

**範例：**

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

如需這些連結服務的詳細資訊，請參閱 [Azure 表格儲存體連接器](data-factory-azure-table-connector.md#linked-service-properties)文件。 

### <a name="dataset"></a>Dataset
toodefine 是 Azure 資料表的資料集，設定 hello**類型**hello 資料集太**AzureTable**，並指定下列屬性在 hello hello **typeProperties** > 一節： 

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| tableName |參照的連結服務的 hello Azure 資料表的資料庫執行個體中的 hello 資料表的名稱。 |是。 當 tableName azureTableSourceQuery 沒有指定時，hello 資料表內的所有記錄都會複製的 toohello 目的地。 如果同時指定 azureTableSourceQuery，滿足 hello 查詢的 hello 資料表內的記錄將會複製的 toohello 目的地。 |

#### <a name="example"></a>範例

```json
{
    "name": "AzureTableInput",
    "properties": {
        "type": "AzureTable",
        "linkedServiceName": "StorageLinkedService",
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

如需這些連結服務的詳細資訊，請參閱 [Azure 表格儲存體連接器](data-factory-azure-table-connector.md#dataset-properties)文件。 

### <a name="azure-table-source-in-copy-activity"></a>複製活動中的 Azure 資料表來源
如果您從 Azure 資料表儲存體複製資料，設定 hello**來源類型**的 hello 複製活動太**AzureTableSource**，並指定下列屬性在 hello**來源**> 一節：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| AzureTableSourceQuery |使用自訂查詢 tooread hello 的資料。 |Azure 資料表查詢字串。 請參閱 hello 下一節中的範例。 |否。 當 tableName azureTableSourceQuery 沒有指定時，hello 資料表內的所有記錄都會複製的 toohello 目的地。 如果同時指定 azureTableSourceQuery，滿足 hello 查詢的 hello 資料表內的記錄將會複製的 toohello 目的地。 |
| azureTableSourceIgnoreTableNotFound |指出是否壓抑 hello 的資料表不存在例外狀況。 |TRUE<br/>FALSE |否 |

#### <a name="example"></a>範例

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureTabletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureTableSource",
                    "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
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
        }]
    }
}
```

如需這些連結服務的詳細資訊，請參閱 [Azure 表格儲存體連接器](data-factory-azure-table-connector.md#copy-activity-properties)文件。 

### <a name="azure-table-sink-in-copy-activity"></a>複製活動中的 Azure 資料表接收
如果您要複製資料 tooAzure 資料表儲存體，請設定 hello**接收器類型**的 hello 複製活動太**AzureTableSink**，並指定下列屬性在 hello**接收**區段：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| azureTableDefaultPartitionKeyValue |預設資料分割索引鍵值，可供 hello 接收。 |字串值。 |否 |
| azureTablePartitionKeyName |指定的值用做為資料分割索引鍵的 hello 資料行的名稱。 如果未指定，azuretabledefaultpartitionkeyvalue 會做為 hello 資料分割索引鍵。 |資料行名稱。 |否 |
| azureTableRowKeyName |指定的資料行值用做為資料列索引鍵的 hello 資料行的名稱。 如果未指定，則會針對每個資料列使用 GUID。 |資料行名稱。 |否 |
| azureTableInsertType |hello 模式 tooinsert 資料插入 Azure 資料表。<br/><br/>這個屬性控制與相符的資料分割和資料列的索引鍵的 hello 輸出資料表中的現有資料列是否具有取代或合併其值。 <br/><br/>toolearn 有關這些設定 （「 合併 」 和 「 取代 」） 的運作方式，請參閱[插入或合併實體](https://msdn.microsoft.com/library/azure/hh452241.aspx)和[插入或取代實體](https://msdn.microsoft.com/library/azure/hh452242.aspx)主題。 <br/><br> 此設定適用於在 hello 資料列層級，不 hello 資料表層級，和這兩個選項會刪除 hello 輸出資料表不存在於 hello 輸入的資料列。 |合併 (預設值)<br/>取代 |否 |
| writeBatchSize |Hello 叫用 writeBatchSize 或 writeBatchTimeout 時，請將資料插入至 hello Azure 資料表中。 |整數 (資料列數目) |否 (預設值：10000) |
| writeBatchTimeout |用戶端 hello 叫用 writeBatchSize 或 writeBatchTimeout 時，將資料插入 hello Azure 資料表 |時間範圍<br/><br/>範例：“00:20:00” (20 分鐘) |否 （預設 toostorage 用戶端預設逾時值 90 秒） |

#### <a name="example"></a>範例

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoTable",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureTableOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureTableSink",
                    "writeBatchSize": 100,
                    "writeBatchTimeout": "01:00:00"
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
        }]
    }
}
```
如需這些連結服務的詳細資訊，請參閱 [Azure 表格儲存體連接器](data-factory-azure-table-connector.md#copy-activity-properties)文件。 

## <a name="amazon-redshift"></a>Amazon RedShift

### <a name="linked-service"></a>連結服務
toodefine Amazon Redshift 連結服務，設定 hello**類型**hello 的連結服務太**AmazonRedshift**，並指定下列屬性在 hello **typeProperties**> 一節：  

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 伺服器 |IP 位址或主機名稱的 hello Amazon Redshift 伺服器。 |是 |
| 連接埠 |hello hello Amazon Redshift 伺服器 hello TCP 連接埠號碼使用 toolisten 用於用戶端連線。 |否，預設值︰5439 |
| 資料庫 |Hello Amazon Redshift 資料庫的名稱。 |是 |
| username |具有存取 toohello 資料庫使用者的名稱。 |是 |
| password |Hello 使用者帳戶的密碼。 |是 |

#### <a name="example"></a>範例

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties": {
        "type": "AmazonRedshift",
        "typeProperties": {
            "server": "<Amazon Redshift host name or IP address>",
            "port": 5439,
            "database": "<database name>",
            "username": "user",
            "password": "password"
        }
    }
}
```

如需詳細資訊，請參閱 [Amazon Redshift 連接器](#data-factory-amazon-redshift-connector.md#linked-service-properties)文件。 

### <a name="dataset"></a>Dataset
toodefine Amazon Redshift 資料集設定 hello**類型**hello 資料集太**RelationalTable**，並指定下列屬性在 hello hello **typeProperties**區段： 

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| tableName |連結服務的 hello Amazon Redshift 資料庫中的 hello 資料表名稱參考。 |否 (如果已指定 **RelationalSource** 的 **query**) |


#### <a name="example"></a>範例

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
如需詳細資訊，請參閱 [Amazon Redshift 連接器](#data-factory-amazon-redshift-connector.md#dataset-properties)文件。

### <a name="relational-source-in-copy-activity"></a>複製活動中的關聯式來源 
如果您從 Amazon Redshift 複製資料，設定 hello**來源類型**的 hello 複製活動太**RelationalSource**，並指定下列屬性在 hello**來源**區段：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| query |使用自訂查詢 tooread hello 的資料。 |SQL 查詢字串。 例如： `select * from MyTable`。 |否 (如果已指定 **dataset** 的 **tableName**) |

#### <a name="example"></a>範例

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonRedshiftInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonRedshiftToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
如需詳細資訊，請參閱 [Amazon Redshift 連接器](#data-factory-amazon-redshift-connector.md#copy-activity-properties)文件。

## <a name="ibm-db2"></a>IBM DB2

### <a name="linked-service"></a>連結服務
toodefine IBM DB2 連結服務，設定 hello**類型**hello 的連結服務太**OnPremisesDB2**，並指定下列屬性在 hello **typeProperties** > 一節：  

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 伺服器 |Hello DB2 伺服器的名稱。 |是 |
| 資料庫 |Hello DB2 資料庫的名稱。 |是 |
| 結構描述 |Hello hello 資料庫中的結構描述名稱。 hello 結構描述名稱會區分大小寫。 |否 |
| authenticationType |Tooconnect toohello DB2 資料庫使用的驗證類型。 可能的值為：匿名、基本和 Windows。 |是 |
| username |如果您使用基本或 Windows 驗證，請指定使用者名稱。 |否 |
| password |指定 hello hello 使用者名稱所指定的使用者帳戶的密碼。 |否 |
| gatewayName |Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello 在內部部署 DB2 資料庫。 |是 |

#### <a name="example"></a>範例
```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
如需詳細資訊，請參閱 [IBM DB2 連接器](#data-factory-onprem-db2-connector.md#linked-service-properties)文件。

### <a name="dataset"></a>Dataset
toodefine DB2 資料集，設定 hello**類型**hello 資料集太**RelationalTable**，並指定下列屬性在 hello hello **typeProperties** > 一節：

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| tableName |參照的連結服務的 hello DB2 資料庫執行個體中的 hello 資料表的名稱。 hello tableName 是區分大小寫。 |否 (如果已指定 **RelationalSource** 的 **query**) 

#### <a name="example"></a>範例
```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

如需詳細資訊，請參閱 [IBM DB2 連接器](#data-factory-onprem-db2-connector.md#dataset-properties)文件。

### <a name="relational-source-in-copy-activity"></a>複製活動中的關聯式來源
如果您從 IBM DB2 複製資料，設定 hello**來源類型**的 hello 複製活動太**RelationalSource**，並指定下列屬性在 hello**來源**> 一節：


| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| query |使用自訂查詢 tooread hello 的資料。 |SQL 查詢字串。 例如： `"query": "select * from "MySchema"."MyTable""`。 |否 (如果已指定 **dataset** 的 **tableName**) |

#### <a name="example"></a>範例
```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"Orders\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "Db2DataSet"
            }],
            "outputs": [{
                "name": "AzureBlobDb2DataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "Db2ToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
如需詳細資訊，請參閱 [IBM DB2 連接器](#data-factory-onprem-db2-connector.md#copy-activity-properties)文件。

## <a name="mysql"></a>MySQL

### <a name="linked-service"></a>連結服務
toodefine MySQL 連結服務，設定 hello**類型**hello 的連結服務太**OnPremisesMySql**，並指定下列屬性在 hello **typeProperties** > 一節：  

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 伺服器 |Hello MySQL 伺服器的名稱。 |是 |
| 資料庫 |Hello MySQL 資料庫的名稱。 |是 |
| 結構描述 |Hello hello 資料庫中的結構描述名稱。 |否 |
| authenticationType |Tooconnect toohello MySQL 資料庫使用的驗證類型。 可能的值為：`Basic`。 |是 |
| username |指定使用者名稱 tooconnect toohello MySQL 資料庫。 |是 |
| password |指定您所指定的 hello 使用者帳戶的密碼。 |是 |
| gatewayName |Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello 在內部部署 MySQL 資料庫。 |是 |

#### <a name="example"></a>範例

```json
{
    "name": "OnPremMySqlLinkedService",
    "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
            "server": "<server name>",
            "database": "<database name>",
            "schema": "<schema name>",
            "authenticationType": "<authentication type>",
            "userName": "<user name>",
            "password": "<password>",
            "gatewayName": "<gateway>"
        }
    }
}
```

如需詳細資訊，請參閱 [MySQL 連接器](data-factory-onprem-mysql-connector.md#linked-service-properties)文件。 

### <a name="dataset"></a>Dataset
toodefine MySQL 資料集設定 hello**類型**hello 資料集太**RelationalTable**，並指定下列屬性在 hello hello **typeProperties** > 一節： 

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| tableName |在 hello MySQL 資料庫連結的服務參考的執行個體中的 hello 資料表的名稱。 |否 (如果已指定 **RelationalSource** 的 **query**) |

#### <a name="example"></a>範例

```json
{
    "name": "MySqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremMySqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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
如需詳細資訊，請參閱 [MySQL 連接器](data-factory-onprem-mysql-connector.md#dataset-properties)文件。 

### <a name="relational-source-in-copy-activity"></a>複製活動中的關聯式來源
如果您從 MySQL 資料庫複製資料，設定 hello**來源類型**的 hello 複製活動太**RelationalSource**，並指定下列屬性在 hello**來源**區段：


| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| query |使用自訂查詢 tooread hello 的資料。 |SQL 查詢字串。 例如： `select * from MyTable`。 |否 (如果已指定 **dataset** 的 **tableName**) |


#### <a name="example"></a>範例
```json
{
    "name": "CopyMySqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MySqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobMySqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MySqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

如需詳細資訊，請參閱 [MySQL 連接器](data-factory-onprem-mysql-connector.md#copy-activity-properties)文件。 

## <a name="oracle"></a>Oracle 

### <a name="linked-service"></a>連結服務
toodefine Oracle 連結服務，設定 hello**類型**hello 的連結服務太**OnPremisesOracle**，並指定下列屬性在 hello **typeProperties**區段：  

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| driverType | 指定從哪一個驅動程式 toouse toocopy 資料 / tooOracle 資料庫。 允許的值為 **Microsoft** 或 **ODP** (預設值)。 如需驅動程式詳細資料，請參閱[支援的版本和安裝](#supported-versions-and-installation)一節。 | 否 |
| connectionString | 指定所需的資訊 tooconnect toohello Oracle 資料庫執行個體 hello connectionString 屬性。 | 是 |
| gatewayName | Hello 閘道名稱，是使用的 tooconnect toohello 在內部部署 Oracle 伺服器 |是 |

#### <a name="example"></a>範例
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString": "Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

如需詳細資訊，請參閱 [Oracle 連接器](data-factory-onprem-oracle-connector.md#linked-service-properties)文件。

### <a name="dataset"></a>Dataset
toodefine Oracle 資料集設定 hello**類型**hello 資料集太**OracleTable**，並指定下列屬性在 hello hello **typeProperties** > 一節： 

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| tableName |Hello hello 連結的服務的 Oracle 資料庫中的 hello 資料表名稱參考。 |否 (如果已指定 **OracleSource** 的 **oracleReaderQuery**) |

#### <a name="example"></a>範例

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2016-02-27T12:00:00",
            "frequency": "Hour"
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
如需詳細資訊，請參閱 [Oracle 連接器](data-factory-onprem-oracle-connector.md#dataset-properties)文件。

### <a name="oracle-source-in-copy-activity"></a>複製活動中的 Oracle 來源
如果您從 Oracle 資料庫複製資料，設定 hello**來源類型**的 hello 複製活動太**OracleSource**，並指定下列屬性在 hello**來源**區段：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| oracleReaderQuery |使用自訂查詢 tooread hello 的資料。 |SQL 查詢字串。 例如：`select * from MyTable` <br/><br/>如果未指定，hello 執行的 SQL 陳述式：`select * from MyTable` |否 (如果已指定 **dataset** 的 **tableName**) |

#### <a name="example"></a>範例

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "OracletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " OracleInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "OracleSource",
                    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
        }]
    }
}
```

如需詳細資訊，請參閱 [Oracle 連接器](data-factory-onprem-oracle-connector.md#copy-activity-properties)文件。

### <a name="oracle-sink-in-copy-activity"></a>複製活動中的 Oracle 接收
如果您要複製資料 tooam Oracle 資料庫，請設定 hello**接收器類型**的 hello 複製活動太**OracleSink**，並指定下列屬性在 hello**接收**> 一節：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| writeBatchTimeout |在逾時之前，請等待 hello 批次插入作業 toocomplete 時間。 |時間範圍<br/><br/> 範例：00:30:00 (30 分鐘)。 |否 |
| writeBatchSize |當 hello 緩衝區大小到達叫用 writeBatchSize 時，請將資料插入 hello SQL 資料表。 |整數 (資料列數目) |否 (預設值：100) |
| sqlWriterCleanupScript |複製活動 tooexecute 查詢指定的特定配量的資料清除。 |查詢陳述式。 |否 |
| sliceIdentifierColumnName |指定資料行名稱複製活動 toofill 與自動產生配量識別項，也就是使用的 tooclean 何時重新執行的特定配量的資料。 |資料類型為 binary(32) 之資料行的資料行名稱。 |否 |

#### <a name="example"></a>範例
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-05T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoOracle",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "OracleOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "OracleSink"
                }
            },
            "scheduler": {
                "frequency": "Day",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
如需詳細資訊，請參閱 [Oracle 連接器](data-factory-onprem-oracle-connector.md#copy-activity-properties)文件。

## <a name="postgresql"></a>PostgreSQL

### <a name="linked-service"></a>連結服務
toodefine PostgreSQL 連結服務，設定 hello**類型**hello 的連結服務太**OnPremisesPostgreSql**，並指定下列屬性在 hello **typeProperties**> 一節：  

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 伺服器 |Hello PostgreSQL 伺服器的名稱。 |是 |
| 資料庫 |Hello PostgreSQL 資料庫的名稱。 |是 |
| 結構描述 |Hello hello 資料庫中的結構描述名稱。 hello 結構描述名稱會區分大小寫。 |否 |
| authenticationType |Tooconnect toohello PostgreSQL 資料庫使用的驗證類型。 可能的值為：匿名、基本和 Windows。 |是 |
| username |如果您使用基本或 Windows 驗證，請指定使用者名稱。 |否 |
| password |指定 hello hello 使用者名稱所指定的使用者帳戶的密碼。 |否 |
| gatewayName |Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello 在內部部署 PostgreSQL 資料庫。 |是 |

#### <a name="example"></a>範例

```json
{
    "name": "OnPremPostgreSqlLinkedService",
    "properties": {
        "type": "OnPremisesPostgreSql",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
如需詳細資訊，請參閱 [PostgreSQL 連接器](data-factory-onprem-postgresql-connector.md#linked-service-properties)文件。

### <a name="dataset"></a>Dataset
toodefine PostgreSQL 資料集設定 hello**類型**hello 資料集太**RelationalTable**，並指定下列屬性在 hello hello **typeProperties** > 一節： 

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| tableName |Hello PostgreSQL 資料庫連結的服務參考的執行個體中的 hello 資料表的名稱。 hello tableName 是區分大小寫。 |否 (如果已指定 **RelationalSource** 的 **query**) |

#### <a name="example"></a>範例
```json
{
    "name": "PostgreSqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremPostgreSqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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
如需詳細資訊，請參閱 [PostgreSQL 連接器](data-factory-onprem-postgresql-connector.md#dataset-properties)文件。

### <a name="relational-source-in-copy-activity"></a>複製活動中的關聯式來源
如果您從 PostgreSQL 資料庫複製資料，設定 hello**來源類型**的 hello 複製活動太**RelationalSource**，並指定下列屬性在 hello**來源**> 一節：


| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| query |使用自訂查詢 tooread hello 的資料。 |SQL 查詢字串。 例如："query": "select * from \"MySchema\".\"MyTable\""。 |否 (如果已指定 **dataset** 的 **tableName**) |

#### <a name="example"></a>範例

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"public\".\"usstates\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "PostgreSqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobPostgreSqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "PostgreSqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

如需詳細資訊，請參閱 [PostgreSQL 連接器](data-factory-onprem-postgresql-connector.md#copy-activity-properties)文件。

## <a name="sap-business-warehouse"></a>SAP Business Warehouse


### <a name="linked-service"></a>連結服務
toodefine SAP Business 倉儲 (BW) 連結服務，設定 hello**類型**hello 的連結服務太**SapBw**，並指定下列屬性在 hello **typeProperties**> 一節：  

屬性 | 說明 | 允許的值 | 必要
-------- | ----------- | -------------- | --------
伺服器 | 執行個體所在的 hello SAP BW 的 hello 伺服器的名稱。 | 字串 | 是
systemNumber | Hello SAP BW 系統的系統編號。 | 以字串表示的二位數十進位數字。 | 是
clientId | Hello W SAP 系統中的 hello 用戶端的用戶端識別碼。 | 以字串表示的三位數十進位數字。 | 是
username | Hello 使用者具有存取 toohello SAP 伺服器的名稱 | 字串 | 是
password | Hello 使用者密碼。 | 字串 | 是
gatewayName | Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello 在內部部署 SAP BW 的執行個體。 | 字串 | 是
encryptedCredential | hello 加密認證的字串。 | 字串 | 否

#### <a name="example"></a>範例

```json
{
    "name": "SapBwLinkedService",
    "properties": {
        "type": "SapBw",
        "typeProperties": {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

如需詳細資訊，請參閱 [SAP Business Warehouse 連接器](data-factory-sap-business-warehouse-connector.md#linked-service-properties)文件。 

### <a name="dataset"></a>Dataset
toodefine SAP BW 資料集設定 hello**類型**hello 資料集太**RelationalTable**。 支援的型別 hello SAP BW 資料集沒有特定型別的屬性**RelationalTable**。  

#### <a name="example"></a>範例

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
如需詳細資訊，請參閱 [SAP Business Warehouse 連接器](data-factory-sap-business-warehouse-connector.md#dataset-properties)文件。 

### <a name="relational-source-in-copy-activity"></a>複製活動中的關聯式來源
如果您要從 SAP Business Warehouse 來複製資料，設定 hello**來源類型**的 hello 複製活動太**RelationalSource**，並指定下列屬性在 hello**來源**> 一節：


| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| query | 指定 hello MDX 查詢 tooread 資料從 hello SAP BW 的執行個體。 | MDX 查詢。 | 是 |

#### <a name="example"></a>範例

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<MDX query for SAP BW>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapBwDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapBwToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

如需詳細資訊，請參閱 [SAP Business Warehouse 連接器](data-factory-sap-business-warehouse-connector.md#copy-activity-properties)文件。 

## <a name="sap-hana"></a>SAP HANA

### <a name="linked-service"></a>連結服務
SAP HANA toodefine 連結服務，設定 hello**類型**hello 的連結服務太**SapHana**，並指定下列屬性在 hello **typeProperties** > 一節：  

屬性 | 說明 | 允許的值 | 必要
-------- | ----------- | -------------- | --------
伺服器 | 執行個體所在的 hello SAP HANA hello 伺服器的名稱。 如果您的伺服器使用自訂連接埠，指定 `server:port`。 | 字串 | 是
authenticationType | 驗證類型。 | 字串。 "Basic" 或 "Windows" | 是 
username | Hello 使用者具有存取 toohello SAP 伺服器的名稱 | 字串 | 是
password | Hello 使用者密碼。 | 字串 | 是
gatewayName | Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello 在內部部署 SAP HANA 的執行個體。 | 字串 | 是
encryptedCredential | hello 加密認證的字串。 | 字串 | 否

#### <a name="example"></a>範例

```json
{
    "name": "SapHanaLinkedService",
    "properties": {
        "type": "SapHana",
        "typeProperties": {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```
如需詳細資訊，請參閱 [SAP HANA 連接器](data-factory-sap-hana-connector.md#linked-service-properties)文件。
 
### <a name="dataset"></a>Dataset
toodefine SAP HANA 資料集設定 hello**類型**hello 資料集太**RelationalTable**。 支援的型別 hello SAP HANA 資料集沒有特定型別的屬性**RelationalTable**。 

#### <a name="example"></a>範例

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
如需詳細資訊，請參閱 [SAP HANA 連接器](data-factory-sap-hana-connector.md#dataset-properties)文件。 

### <a name="relational-source-in-copy-activity"></a>複製活動中的關聯式來源
如果您從 SAP HANA 資料存放區複製資料，設定 hello**來源類型**的 hello 複製活動太**RelationalSource**，並指定下列屬性在 hello**來源**> 一節：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| query | 指定 hello SQL 查詢 tooread 資料從 hello SAP HANA 執行個體。 | SQL 查詢。 | 是 |


#### <a name="example"></a>範例


```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<SQL Query for HANA>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapHanaDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapHanaToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

如需詳細資訊，請參閱 [SAP HANA 連接器](data-factory-sap-hana-connector.md#copy-activity-properties)文件。


## <a name="sql-server"></a>SQL Server

### <a name="linked-service"></a>連結服務
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

```json
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a>範例：用於 SQL 驗證的 JSON

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a>範例：用於 Windows 驗證的 JSON

如果未指定使用者名稱和密碼，閘道會使用這些 tooimpersonate hello 指定的使用者帳戶 tooconnect toohello 在內部部署 SQL Server 資料庫。 否則，閘道會直接與 hello 的閘道 （其啟動帳戶） 的安全性內容連線 toohello SQL Server。

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
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

如需詳細資訊，請參閱 [SQL Server 連接器](data-factory-sqlserver-connector.md#linked-service-properties)文件。 

### <a name="dataset"></a>Dataset
toodefine SQL Server 資料集設定 hello**類型**hello 資料集太**SqlServerTable**，並指定下列屬性在 hello hello **typeProperties** > 一節： 

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| tableName |參照 hello 資料表或檢視中的連結服務的 hello 的 SQL Server 資料庫執行個體的名稱。 |是 |

#### <a name="example"></a>範例
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

如需詳細資訊，請參閱 [SQL Server 連接器](data-factory-sqlserver-connector.md#dataset-properties)文件。 

### <a name="sql-source-in-copy-activity"></a>複製活動中的 Sql 來源
如果您從 SQL Server 資料庫複製資料，設定 hello**來源類型**的 hello 複製活動太**SqlSource**，並指定下列屬性在 hello**來源**區段：


| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| SqlReaderQuery |使用自訂查詢 tooread hello 的資料。 |SQL 查詢字串。 例如： `select * from MyTable`。 從 hello hello 輸入資料集所參考的資料庫，可以參考多個資料表。 如果未指定，hello 執行的 SQL 陳述式： select from MyTable。 |否 |
| sqlReaderStoredProcedureName |名稱的 hello 預存程序會從 hello 來源資料表讀取資料。 |名稱的 hello 預存程序。 |否 |
| storedProcedureParameters |Hello 參數，預存程序。 |名稱/值組。 名稱和大小寫的參數必須符合 hello 名稱和大小寫的 hello 預存程序參數。 |否 |

如果 hello **sqlReaderQuery**指定 hello SqlSource，hello 複製活動會針對 hello 的 SQL Server 資料庫來源 tooget hello 資料執行此查詢。

或者，您可以指定預存程序，藉由指定 hello **sqlReaderStoredProcedureName**和**storedProcedureParameters** （如果 hello 預存程序會採用參數）。

如果您未指定 sqlReaderQuery 或 sqlReaderStoredProcedureName，hello hello 結構區段中定義的資料行是使用的 toobuild select 查詢 toorun 針對 hello 的 SQL Server 資料庫。 如果您不需要 hello 資料集定義 hello 結構，所有資料行選取的 hello 資料表。

> [!NOTE]
> 當您使用**sqlReaderStoredProcedureName**，您仍然需要 toospecify 值 hello **tableName** hello 資料集 JSON 中的屬性。 雖然目前尚未針對此資料表來進行驗證。


#### <a name="example"></a>範例
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
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
        }]
    }
}
```

在此範例中， **sqlReaderQuery** hello SqlSource 指定。 hello 複製活動會針對 hello 的 SQL Server 資料庫來源 tooget hello 資料執行此查詢。 或者，您可以指定預存程序，藉由指定 hello **sqlReaderStoredProcedureName**和**storedProcedureParameters** （如果 hello 預存程序會採用參數）。 hello sqlReaderQuery 參考 hello hello 輸入資料集所參考的資料庫內的多個資料表。 它不是設定為 hello 資料集的 tableName typeProperty 有限的 tooonly hello 資料表。

如果您未指定 sqlReaderQuery 或 sqlReaderStoredProcedureName，hello hello 結構區段中定義的資料行是使用的 toobuild select 查詢 toorun 針對 hello 的 SQL Server 資料庫。 如果您不需要 hello 資料集定義 hello 結構，所有資料行選取的 hello 資料表。

如需詳細資訊，請參閱 [SQL Server 連接器](data-factory-sqlserver-connector.md#copy-activity-properties)文件。 

### <a name="sql-sink-in-copy-activity"></a>複製活動中的 Sql 接收
如果您要複製資料 tooa SQL Server 資料庫，請設定 hello**接收器類型**的 hello 複製活動太**SqlSink**，並指定下列屬性在 hello**接收**> 一節：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| writeBatchTimeout |在逾時之前，請等待 hello 批次插入作業 toocomplete 時間。 |時間範圍<br/><br/> 範例：“00:30:00” (30 分鐘)。 |否 |
| writeBatchSize |當 hello 緩衝區大小到達叫用 writeBatchSize 時，請將資料插入 hello SQL 資料表。 |整數 (資料列數目) |否 (預設值：10000) |
| sqlWriterCleanupScript |複製活動 tooexecute 查詢指定的特定配量的資料清除。 如需詳細資訊，請參閱 [可重複性](#repeatability-during-copy) 一節。 |查詢陳述式。 |否 |
| sliceIdentifierColumnName |指定資料行名稱複製活動 toofill 與自動產生配量識別項，也就是使用的 tooclean 何時重新執行的特定配量的資料。 如需詳細資訊，請參閱 [可重複性](#repeatability-during-copy) 一節。 |資料類型為 binary(32) 之資料行的資料行名稱。 |否 |
| sqlWriterStoredProcedureName |名稱的 hello 預存程序 upserts （更新/插入） 資料到 hello 目標資料表。 |名稱的 hello 預存程序。 |否 |
| storedProcedureParameters |Hello 參數，預存程序。 |名稱/值組。 名稱和大小寫的參數必須符合 hello 名稱和大小寫的 hello 預存程序參數。 |否 |
| sqlWriterTableType |指定資料表類型名稱 toobe hello 預存程序中使用。 複製活動移動 hello 資料可讓在暫存資料表與此資料表類型。 預存程序程式碼可以再合併 hello 資料會被複製現有的資料。 |資料表類型名稱。 |否 |

#### <a name="example"></a>範例
hello 管線包含複製活動的設定的 toouse 這些輸入和輸出資料集，而排程的 toorun 每小時。 在 hello 管線 JSON 定義中，hello**來源**類型設定得**BlobSource**和**接收**類型設定得**SqlSink**。

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": " SqlServerOutput "
            }],
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
        }]
    }
}
```

如需詳細資訊，請參閱 [SQL Server 連接器](data-factory-sqlserver-connector.md#copy-activity-properties)文件。 

## <a name="sybase"></a>Sybase

### <a name="linked-service"></a>連結服務
toodefine Sybase 連結服務，設定 hello**類型**hello 的連結服務太**OnPremisesSybase**，並指定下列屬性在 hello **typeProperties**區段：  

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 伺服器 |Hello Sybase 伺服器的名稱。 |是 |
| 資料庫 |Hello Sybase 資料庫的名稱。 |是 |
| 結構描述 |Hello hello 資料庫中的結構描述名稱。 |否 |
| authenticationType |Tooconnect toohello Sybase 資料庫使用的驗證類型。 可能的值為：匿名、基本和 Windows。 |是 |
| username |如果您使用基本或 Windows 驗證，請指定使用者名稱。 |否 |
| password |指定 hello hello 使用者名稱所指定的使用者帳戶的密碼。 |否 |
| gatewayName |Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello 在內部部署 Sybase 資料庫。 |是 |

#### <a name="example"></a>範例
```json
{
    "name": "OnPremSybaseLinkedService",
    "properties": {
        "type": "OnPremisesSybase",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

如需詳細資訊，請參閱 [Sybase 連接器](data-factory-onprem-sybase-connector.md#linked-service-properties)文件。 

### <a name="dataset"></a>Dataset
toodefine Sybase 資料集設定 hello**類型**hello 資料集太**RelationalTable**，並指定下列屬性在 hello hello **typeProperties** > 一節： 

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| tableName |Hello Sybase 資料庫連結的服務參考的執行個體中的 hello 資料表的名稱。 |否 (如果已指定 **RelationalSource** 的 **query**) |

#### <a name="example"></a>範例

```json
{
    "name": "SybaseDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremSybaseLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

如需詳細資訊，請參閱 [Sybase 連接器](data-factory-onprem-sybase-connector.md#dataset-properties)文件。 

### <a name="relational-source-in-copy-activity"></a>複製活動中的關聯式來源
如果您從 Sybase 資料庫複製資料，設定 hello**來源類型**的 hello 複製活動太**RelationalSource**，並指定下列屬性在 hello**來源**區段：


| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| query |使用自訂查詢 tooread hello 的資料。 |SQL 查詢字串。 例如： `select * from MyTable`。 |否 (如果已指定 **dataset** 的 **tableName**) |

#### <a name="example"></a>範例

```json
{
    "name": "CopySybaseToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from DBA.Orders"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "SybaseDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobSybaseDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SybaseToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

如需詳細資訊，請參閱 [Sybase 連接器](data-factory-onprem-sybase-connector.md#copy-activity-properties)文件。

## <a name="teradata"></a>Teradata

### <a name="linked-service"></a>連結服務
toodefine Teradata 連結服務，設定 hello**類型**hello 的連結服務太**OnPremisesTeradata**，並指定下列屬性在 hello **typeProperties**區段：  

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 伺服器 |Hello Teradata 伺服器的名稱。 |是 |
| authenticationType |Tooconnect toohello Teradata 資料庫使用的驗證類型。 可能的值為：匿名、基本和 Windows。 |是 |
| username |如果您使用基本或 Windows 驗證，請指定使用者名稱。 |否 |
| password |指定 hello hello 使用者名稱所指定的使用者帳戶的密碼。 |否 |
| gatewayName |Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello 在內部部署 Teradata 資料庫。 |是 |

#### <a name="example"></a>範例
```json
{
    "name": "OnPremTeradataLinkedService",
    "properties": {
        "type": "OnPremisesTeradata",
        "typeProperties": {
            "server": "<server>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

如需詳細資訊，請參閱 [Teradata 連接器](data-factory-onprem-teradata-connector.md#linked-service-properties)文件。

### <a name="dataset"></a>Dataset
toodefine Teradata Blob 資料集設定 hello**類型**hello 資料集太**RelationalTable**。 目前沒有任何支援 hello Teradata 資料集的類型屬性。 

#### <a name="example"></a>範例
```json
{
    "name": "TeradataDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremTeradataLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

如需詳細資訊，請參閱 [Teradata 連接器](data-factory-onprem-teradata-connector.md#dataset-properties)文件。

### <a name="relational-source-in-copy-activity"></a>複製活動中的關聯式來源
如果您要從 Teradata 資料庫來複製資料，設定 hello**來源類型**的 hello 複製活動太**RelationalSource**，並指定下列屬性在 hello**來源**> 一節：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| query |使用自訂查詢 tooread hello 的資料。 |SQL 查詢字串。 例如： `select * from MyTable`。 |是 |

#### <a name="example"></a>範例

```json
{
    "name": "CopyTeradataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', SliceStart, SliceEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "TeradataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobTeradataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "TeradataToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "isPaused": false
    }
}
```

如需詳細資訊，請參閱 [Teradata 連接器](data-factory-onprem-teradata-connector.md#copy-activity-properties)文件。

## <a name="cassandra"></a>Cassandra


### <a name="linked-service"></a>連結服務
toodefine Cassandra 連結服務，設定 hello**類型**hello 的連結服務太**OnPremisesCassandra**，並指定下列屬性在 hello **typeProperties**區段：  

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 主機 |一或多個 Cassandra 伺服器 IP 位址或主機名稱。<br/><br/>同時指定以逗號分隔的 IP 位址或主機名稱 tooconnect tooall 伺服器清單。 |是 |
| 連接埠 |hello hello Cassandra 伺服器的 TCP 連接埠會使用用戶端連線 toolisten。 |否，預設值：9042 |
| authenticationType |基本或匿名 |是 |
| username |指定 hello 使用者帳戶的使用者名稱。 |是，如果設定 tooBasic authenticationType。 |
| password |指定 hello 使用者帳戶的密碼。 |是，如果設定 tooBasic authenticationType。 |
| gatewayName |hello hello 閘道所使用的 tooconnect toohello 內部 Cassandra 資料庫名稱。 |是 |
| encryptedCredential |加密的 hello 閘道的認證。 |否 |

#### <a name="example"></a>範例

```json
{
    "name": "CassandraLinkedService",
    "properties": {
        "type": "OnPremisesCassandra",
        "typeProperties": {
            "authenticationType": "Basic",
            "host": "<cassandra server name or IP address>",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

如需詳細資訊，請參閱 [Cassandra 連接器](data-factory-onprem-cassandra-connector.md#linked-service-properties)文件。 

### <a name="dataset"></a>Dataset
toodefine Cassandra 資料集設定 hello**類型**hello 資料集太**CassandraTable**，並指定下列屬性在 hello hello **typeProperties** > 一節： 

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| keyspace |Hello keyspace 或 Cassandra 資料庫中的結構描述的名稱。 |是 (如果未定義 **CassandraSource** 的**查詢**)。 |
| tableName |Cassandra 資料庫中的 hello 資料表的名稱。 |是 (如果未定義 **CassandraSource** 的**查詢**)。 |

#### <a name="example"></a>範例

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "<key space>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

如需詳細資訊，請參閱 [Cassandra 連接器](data-factory-onprem-cassandra-connector.md#dataset-properties)文件。 

### <a name="cassandra-source-in-copy-activity"></a>複製活動中的 SCassandra 來源
如果您從 Cassandra 複製資料，設定 hello**來源類型**的 hello 複製活動太**CassandraSource**，並指定下列屬性在 hello**來源**區段:

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| query |使用自訂查詢 tooread hello 的資料。 |SQL-92 查詢或 CQL 查詢。 請參閱 [CQL 參考資料](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html)。 <br/><br/>當使用 SQL 查詢，指定**keyspace name.table 名稱**想 tooquery toorepresent hello 資料表。 |否 (如果已定義資料集上的 tableName 和 keyspace)。 |
| consistencyLevel |hello 一致性層級指定幾個複本必須回應 tooa 讀取的要求傳回資料 toohello 用戶端應用程式之前。 Cassandra 檢查 hello 複本的指定的數目的資料 toosatisfy hello 讀取的要求。 |ONE、TWO、THREE、QUORUM、ALL、LOCAL_QUORUM、EACH_QUORUM、LOCAL_ONE。 如需詳細資訊，請參閱 [設定資料一致性](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) 。 |否。 預設值為 ONE。 |

#### <a name="example"></a>範例
  
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "CassandraInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"
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
        }]
    }
}
```

如需詳細資訊，請參閱 [Cassandra 連接器](data-factory-onprem-cassandra-connector.md#copy-activity-properties)文件。

## <a name="mongodb"></a>MongoDB

### <a name="linked-service"></a>連結服務
toodefine MongoDB 連結服務，設定 hello**類型**hello 的連結服務太**OnPremisesMongoDB**，並指定下列屬性在 hello **typeProperties**區段：  

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 伺服器 |IP 位址或主機名稱的 hello MongoDB 伺服器。 |是 |
| 連接埠 |Hello MongoDB 伺服器的 TCP 連接埠會使用用戶端連線 toolisten。 |選用，預設值︰27017 |
| authenticationType |基本或匿名。 |是 |
| username |使用者帳戶 tooaccess MongoDB。 |是 (如果使用基本驗證)。 |
| password |Hello 使用者密碼。 |是 (如果使用基本驗證)。 |
| authSource |您想 toouse toocheck 您的認證進行驗證的 hello MongoDB 資料庫的名稱。 |選用 (如果使用基本驗證)。 預設值： 使用 hello 系統管理員帳戶和 hello 使用 databaseName 屬性所指定的資料庫。 |
| databaseName |您想 tooaccess hello MongoDB 資料庫的名稱。 |是 |
| gatewayName |Hello 閘道存取 hello 資料存放區的名稱。 |是 |
| encryptedCredential |由閘道加密的認證。 |選用 |

#### <a name="example"></a>範例

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties": {
        "type": "OnPremisesMongoDb",
        "typeProperties": {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
            "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

如需詳細資訊，請參閱 [MongoDB 連接器文件](data-factory-on-premises-mongodb-connector.md#linked-service-properties)

### <a name="dataset"></a>Dataset
toodefine MongoDB 資料集設定 hello**類型**hello 資料集太**MongoDbCollection**，並指定下列屬性在 hello hello **typeProperties** > 一節： 

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| collectionName |MongoDB 資料庫中的 hello 集合的名稱。 |是 |

#### <a name="example"></a>範例

```json
{
    "name": "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

如需詳細資訊，請參閱 [MongoDB 連接器文件](data-factory-on-premises-mongodb-connector.md#dataset-properties)

#### <a name="mongodb-source-in-copy-activity"></a>複製活動中的 MongoDB 來源
如果您從 MongoDB 複製資料，設定 hello**來源類型**的 hello 複製活動太**MongoDbSource**，並指定下列屬性在 hello**來源**> 一節：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| query |使用自訂查詢 tooread hello 的資料。 |SQL-92 查詢字串。 例如： `select * from MyTable`。 |否 (如果已指定 **dataset** 的 **collectionName**) |

#### <a name="example"></a>範例

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "MongoDbSource",
                    "query": "select * from MyTable"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MongoDbInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MongoDBToAzureBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

如需詳細資訊，請參閱 [MongoDB 連接器文件](data-factory-on-premises-mongodb-connector.md#copy-activity-properties)

## <a name="amazon-s3"></a>Amazon S3


### <a name="linked-service"></a>連結服務
toodefine Amazon S3 連結服務，設定 hello**類型**hello 的連結服務太**AwsAccessKey**，並指定下列屬性在 hello **typeProperties**區段:  

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| accessKeyID |Hello 密碼的存取金鑰的識別碼。 |字串 |是 |
| secretAccessKey |hello 密碼存取金鑰本身。 |加密的密碼字串 |是 |

#### <a name="example"></a>範例
```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

如需詳細資訊，請參閱 [Amazon S3 連接器文件](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties)。

### <a name="dataset"></a>Dataset
toodefine Amazon S3 資料集，設定 hello**類型**hello 資料集太**AmazonS3**，並指定下列屬性在 hello hello **typeProperties** > 一節： 

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| bucketName |hello S3 值區的名稱。 |String |是 |
| key |hello S3 物件索引鍵。 |String |否 |
| prefix |Hello S3 物件索引鍵的前置詞。 系統會選取索引鍵以此前置詞開頭的物件。 只有當索引鍵空白時才適用。 |string |否 |
| 版本 |如果已啟用 S3 版本控制的 S3 物件 hello 版本。 |String |否 |
| format | 支援下列格式類型的 hello: **TextFormat**， **JsonFormat**， **AvroFormat**， **OrcFormat**， **ParquetFormat**。 設定 hello**類型**下格式 tooone 這些值的屬性。 如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。 <br><br> 如果您想太**複製檔做為-是**之間以檔案為基礎存放區 （二進位複製），略過這兩個輸入和輸出資料集定義中的 hello 格式 > 一節。 |否 | |
| compression | 指定 hello 類型和層級的 hello 資料壓縮。 支援的類型為：**GZip**、**Deflate**、**BZip2** 及 **ZipDeflate**。 hello 支援層級為：**最佳**和**最快**。 如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。 |否 | |


> [!NOTE]
> bucketName + 鍵指定 hello hello S3 物件其中貯體是 S3 物件 hello 根容器，而索引鍵是 hello 完整路徑 tooS3 物件位置。

#### <a name="example-sample-dataset-with-prefix"></a>範例：範例資料集 (含 prefix)

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "<S3 bucket name>",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
#### <a name="example-sample-data-set-with-version"></a>範例︰範例資料集 (含 version)

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "<S3 bucket name>",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

#### <a name="example-dynamic-paths-for-s3"></a>範例：S3 的動態路徑
在 hello 範例中，我們會使用固定的值為 hello Amazon S3 資料集中的索引鍵和 bucketName 屬性。

```json
"key": "testFolder/test.orc",
"bucketName": "<S3 bucket name>",
```

您可以使用系統變數 SliceStart 如 hello 索引鍵和 bucketName 在執行階段動態計算的 Data Factory。

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

您可以相同 hello hello 前置詞屬性的 Amazon S3 資料集。 如需支援的函式和變數清單，請參閱 [Data Factory 函式與系統變數](data-factory-functions-variables.md) 。

如需詳細資訊，請參閱 [Amazon S3 連接器文件](data-factory-amazon-simple-storage-service-connector.md#dataset-properties)。

### <a name="file-system-source-in-copy-activity"></a>複製活動中的檔案系統來源
如果您從 Amazon S3 複製資料，設定 hello**來源類型**的 hello 複製活動太**FileSystemSource**，並指定下列屬性在 hello**來源**區段:


| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| 遞迴 |指定是否 toorecursively 清單 S3 物件 hello 目錄下。 |true/false |否 |


#### <a name="example"></a>範例


```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource",
                    "recursive": true
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonS3InputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonS3ToBlob"
        }],
        "start": "2016-08-08T18:00:00",
        "end": "2016-08-08T19:00:00"
    }
}
```

如需詳細資訊，請參閱 [Amazon S3 連接器文件](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties)。

## <a name="file-system"></a>檔案系統


### <a name="linked-service"></a>連結服務
您可以連結在內部部署檔案系統 tooan Azure data factory 以 hello**在內部部署檔案伺服器**連結服務。 hello 下表提供說明屬於特定 toohello 連結在內部部署檔案伺服器服務的 JSON 元素。

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 類型 |請確定 hello type 屬性設定太**OnPremisesFileServer**。 |是 |
| 主機 |指定您想 toocopy hello 資料夾 hello 根路徑。 使用 hello 逸出字元 '\' hello 字串中的特殊字元。 如需範例，請參閱 [範例連結服務和資料集定義](#sample-linked-service-and-dataset-definitions) 。 |是 |
| userid |指定具有存取 toohello 伺服器 hello 使用者識別碼 hello。 |否 (如果您選擇 encryptedCredential) |
| password |指定 hello hello 使用者 (userid) 的密碼。 |否 (如果您選擇 encryptedCredential) |
| encryptedCredential |指定您可以藉由執行 hello 新增 AzureRmDataFactoryEncryptValue cmdlet 取得的 hello 加密認證。 |否 （如果您選擇 toospecify 使用者識別碼和密碼以純文字） |
| gatewayName |指定 hello hello 閘道的 Data Factory 應該使用 tooconnect toohello 在內部部署檔案伺服器名稱。 |是 |

#### <a name="sample-folder-path-definitions"></a>範例資料夾路徑定義 
| 案例 | 連結服務定義中的主機 | 資料集定義中的 folderPath |
| --- | --- | --- |
| 資料管理閘道電腦上的本機資料夾︰ <br/><br/>範例：D:\\\* 或 D:\folder\subfolder\\* |D:\\\\ (適用於資料管理閘道 2.0 和更新版本) <br/><br/> localhost (適用於比資料管理閘道 2.0 更早的版本) |.\\\\ 或 folder\\\\subfolder (適用於資料管理閘道 2.0 和更新版本) <br/><br/>D:\\\\ 或 D:\\\\folder\\\\subfolder (適用低於閘道 2.0 的版本) |
| 遠端共用資料夾︰ <br/><br/>範例︰\\\\myserver\\share\\\* 或 \\\\myserver\\share\\folder\\subfolder\\* |\\\\\\\\myserver\\\\share |.\\\\ 或 folder\\\\subfolder |


#### <a name="example-using-username-and-password-in-plain-text"></a>範例：使用純文字的使用者名稱和密碼

```json
{
    "Name": "OnPremisesFileServerLinkedService",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "\\\\Contosogame-Asia",
            "userid": "Admin",
            "password": "123456",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-encryptedcredential"></a>範例：使用 encryptedcredential

```json
{
    "Name": " OnPremisesFileServerLinkedService ",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "D:\\",
            "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

如需詳細資訊，請參閱[檔案系統連接器文件](data-factory-onprem-file-system-connector.md#linked-service-properties)。

### <a name="dataset"></a>Dataset
toodefine 檔案系統資料集設定 hello**類型**hello 資料集太**FileShare**，並指定下列屬性在 hello hello **typeProperties** > 一節： 

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| folderPath |指定 hello 子路徑 toohello 資料夾。 使用 hello 逸出字元 ' \' hello 字串中的特殊字元。 如需範例，請參閱 [範例連結服務和資料集定義](#sample-linked-service-and-dataset-definitions) 。<br/><br/>您可以結合此屬性與**partitionBy** toohave 資料夾路徑根據配量開始/結束日期時間。 |是 |
| fileName |在 hello 指定 hello hello 檔案名稱**folderPath**如果您想 hello 資料表 toorefer tooa 特定檔案 hello 資料夾中的。 如果您未指定任何值，這個屬性，hello 資料表會指向 tooall hello 資料夾中的檔案。<br/><br/>檔案名稱未指定輸出資料集，hello hello 產生檔案名稱時在 hello 下列格式： <br/><br/>`Data.<Guid>.txt` (例如： Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |否 |
| fileFilter |指定篩選 toobe 使用 tooselect hello folderPath 中檔案的子集，而不是所有的檔案。 <br/><br/>允許的值為︰`*` (多個字元) 和 `?` (單一字元)。<br/><br/>範例 1："fileFilter": "*.log"<br/>範例 2："fileFilter": 2016-1-?.txt"<br/><br/>請注意，fileFilter 適用於輸入 FileShare 資料集。 |否 |
| partitionedBy |您可以使用 partitionedBy toospecify 動態 folderPath/檔名，時間序列資料。 例如，folderPath 可針對每小時的資料進行參數化。 |否 |
| format | 支援下列格式類型的 hello: **TextFormat**， **JsonFormat**， **AvroFormat**， **OrcFormat**， **ParquetFormat**。 設定 hello**類型**下格式 tooone 這些值的屬性。 如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。 <br><br> 如果您想太**複製檔做為-是**之間以檔案為基礎存放區 （二進位複製），略過這兩個輸入和輸出資料集定義中的 hello 格式 > 一節。 |否 |
| compression | 指定 hello 類型和層級的 hello 資料壓縮。 支援的類型為：**GZip**、**Deflate**、**BZip2** 和 **ZipDeflate**，而支援的層級為：**最佳**和**最快**。 請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。 |否 |

> [!NOTE]
> 無法同時使用 fileName 和 fileFilter。

#### <a name="example"></a>範例

```json
{
    "name": "OnpremisesFileSystemInput",
    "properties": {
        "type": " FileShare",
        "linkedServiceName": " OnPremisesFileServerLinkedService ",
        "typeProperties": {
            "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
            "fileName": "{Hour}.csv",
            "partitionedBy": [{
                "name": "Year",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                        "format": "yyyy"
                }
            }, {
                "name": "Month",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "MM"
                }
            }, {
                "name": "Day",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "dd"
                }
            }, {
                "name": "Hour",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "HH"
                }
            }]
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

如需詳細資訊，請參閱[檔案系統連接器文件](data-factory-onprem-file-system-connector.md#dataset-properties)。

### <a name="file-system-source-in-copy-activity"></a>複製活動中的檔案系統來源
如果您從檔案系統複製資料，設定 hello**來源類型**的 hello 複製活動太**FileSystemSource**，並指定下列屬性在 hello**來源**區段：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| 遞迴 |指出是否 hello 讀取資料以遞迴方式從 hello 子資料夾，或只能從 hello 指定的資料夾。 |True/False (預設值為 False) |否 |

#### <a name="example"></a>範例

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T19:00:00",
        "description": "Pipeline for copy activity",
        "activities": [{
            "name": "OnpremisesFileSystemtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "OnpremisesFileSystemInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
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
        }]
    }
}
```
如需詳細資訊，請參閱[檔案系統連接器文件](data-factory-onprem-file-system-connector.md#copy-activity-properties)。

### <a name="file-system-sink-in-copy-activity"></a>複製活動中的檔案系統接收
如果您要複製資料 tooFile 系統，請設定 hello**接收器類型**的 hello 複製活動太**使用 FileSystemSink**，並指定下列屬性在 hello**接收**> 一節：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| copyBehavior |Hello 來源 BlobSource 或檔案系統時，請定義 hello 複製行為。 |**PreserveHierarchy:**保留 hello hello 目標資料夾中的檔案階層。 也就是說，hello hello 來源檔案 toohello 來源資料夾的相對路徑是 hello 與 hello 相對路徑的 hello 目標檔案 toohello 目標資料夾相同。<br/><br/>**FlattenHierarchy:** hello 第一個層級的目標資料夾中建立 hello 來源資料夾中的所有檔案。 會使用自動產生名稱建立 hello 目標檔案。<br/><br/>**MergeFiles:**合併 hello 來源資料夾 tooone 檔案中的所有檔案。 如果指定 hello 檔案名稱/blob 名稱，則 hello 合併的檔案名稱是 hello 指定的名稱。 否則，就會是自動產生的檔案名稱。 |否 |
auto-

#### <a name="example"></a>範例

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T20:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoOnPremisesFile",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "OnpremisesFileSystemOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "FileSystemSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 3,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

如需詳細資訊，請參閱[檔案系統連接器文件](data-factory-onprem-file-system-connector.md#copy-activity-properties)。

## <a name="ftp"></a>FTP

### <a name="linked-service"></a>連結服務
toodefine FTP 連結服務，設定 hello**類型**hello 的連結服務太**FtpServer**，並指定下列屬性在 hello **typeProperties** > 一節：  

| 屬性 | 說明 | 必要 | 預設值 |
| --- | --- | --- | --- |
| 主機 |Hello FTP 伺服器的名稱或 IP 位址 |是 |&nbsp; |
| authenticationType |指定驗證類型 |是 |基本或匿名 |
| username |使用者具有存取 toohello FTP 伺服器 |否 |&nbsp; |
| password |Hello 使用者 （使用者名稱） 的密碼 |否 |&nbsp; |
| encryptedCredential |加密的認證 tooaccess hello FTP 伺服器 |否 |&nbsp; |
| gatewayName |Hello 資料管理閘道器閘道 tooconnect tooan 名稱在內部 FTP 伺服器 |否 |&nbsp; |
| 連接埠 |哪些 hello FTP 伺服器正在接聽的連接埠 |否 |21 |
| enableSsl |指定是否 toouse FTP over SSL/TLS 通道 |否 |true |
| enableServerCertificateValidation |指定是否 tooenable 伺服器 SSL 憑證驗證時使用 FTP over SSL/TLS 通道 |否 |true |

#### <a name="example-using-anonymous-authentication"></a>範例：使用匿名驗證

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
            "typeProperties": {
            "authenticationType": "Anonymous",
            "host": "myftpserver.com"
        }
    }
}
```

#### <a name="example-using-username-and-password-in-plain-text-for-basic-authentication"></a>範例：使用純文字的使用者名稱和密碼進行基本驗證

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
    }
}
```

#### <a name="example-using-port-enablessl-enableservercertificatevalidation"></a>範例：使用 port、enableSsl、enableServerCertificateValidation

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

#### <a name="example-using-encryptedcredential-for-authentication-and-gateway"></a>範例：針對驗證和閘道使用 encryptedCredential

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
      }
}
```

如需詳細資訊，請參閱 [FTP 連接器](data-factory-ftp-connector.md#linked-service-properties)文件。

### <a name="dataset"></a>Dataset
toodefine FTP 資料集，設定 hello**類型**hello 資料集太**FileShare**，並指定下列屬性在 hello hello **typeProperties** > 一節： 

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| folderPath |子路徑 toohello 資料夾。 使用逸出字元 '\' hello 字串中的特殊字元。 如需範例，請參閱 [範例連結服務和資料集定義](#sample-linked-service-and-dataset-definitions) 。<br/><br/>您可以結合此屬性與**partitionBy** toohave 資料夾路徑根據配量開始/結束日期時間。 |是 
| fileName |在 hello 指定 hello hello 檔案名稱**folderPath**如果您想 hello 資料表 toorefer tooa 特定檔案 hello 資料夾中的。 如果您未指定任何值，這個屬性，hello 資料表會指向 tooall hello 資料夾中的檔案。<br/><br/>檔案名稱未指定輸出資料集，hello hello 產生檔案名稱會在 hello 遵循此格式： <br/><br/>Data.<Guid>.txt (範例：Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |否 |
| fileFilter |指定篩選 toobe 使用 tooselect hello folderPath 中檔案的子集，而不是所有的檔案。<br/><br/>允許的值為︰`*` (多個字元) 和 `?` (單一字元)。<br/><br/>範例 1：`"fileFilter": "*.log"`<br/>範例 2：`"fileFilter": 2016-1-?.txt"`<br/><br/> fileFilter 適用於輸入 FileShare 資料集。 這個屬性不支援使用 HDFS。 |否 |
| partitionedBy |partitionedBy 可以是使用的 toospecify 動態 folderPath，時間序列資料的檔案名稱。 例如，folderPath 可針對每小時的資料進行參數化。 |否 |
| format | 支援下列格式類型的 hello: **TextFormat**， **JsonFormat**， **AvroFormat**， **OrcFormat**， **ParquetFormat**。 設定 hello**類型**下格式 tooone 這些值的屬性。 如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。 <br><br> 如果您想太**複製檔做為-是**之間以檔案為基礎存放區 （二進位複製），略過這兩個輸入和輸出資料集定義中的 hello 格式 > 一節。 |否 |
| compression | 指定 hello 類型和層級的 hello 資料壓縮。 支援的類型為：**GZip**、**Deflate**、**BZip2** 和 **ZipDeflate**，而支援的層級為：**最佳**和**最快**。 如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。 |否 |
| useBinaryTransfer |指定是否使用二進位傳輸模式。 二進位模式為 true，ASCII 則為 false。 預設值：True。 只有在相關聯的連結服務類型的類型為 FtpServer 時，才可以使用這個屬性。 |否 |

> [!NOTE]
> 無法同時使用檔名和 fileFilter。

#### <a name="example"></a>範例

```json
{
    "name": "FTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "FTPLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
            "fileName": "test.csv",
            "useBinaryTransfer": true
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

如需詳細資訊，請參閱 [FTP 連接器](data-factory-ftp-connector.md#dataset-properties)文件。

### <a name="file-system-source-in-copy-activity"></a>複製活動中的檔案系統來源
如果您從 FTP 伺服器複製資料，設定 hello**來源類型**的 hello 複製活動太**FileSystemSource**，並指定下列屬性在 hello**來源**區段：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| 遞迴 |指出是否 hello 讀取資料以遞迴方式從 hello 子資料夾，或只能從 hello 指定的資料夾。 |True/False (預設值為 False) |否 |

#### <a name="example"></a>範例

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
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
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00",
        "end": "2016-08-24T19:00:00"
    }
}
```

如需詳細資訊，請參閱 [FTP 連接器](data-factory-ftp-connector.md#copy-activity-properties)文件。


## <a name="hdfs"></a>HDFS

### <a name="linked-service"></a>連結服務
toodefine HDFS 連結服務，設定 hello**類型**hello 的連結服務太**Hdfs**，並指定下列屬性在 hello **typeProperties** > 一節：  

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 類型 |hello 類型屬性必須設定為： **Hdfs** |是 |
| Url |URL toohello HDFS |是 |
| authenticationType |匿名或 Windows。 <br><br> toouse **Kerberos 驗證**HDFS 連接器，請參閱太[本節](#use-kerberos-authentication-for-hdfs-connector)在內部部署環境 tooset 據此。 |是 |
| userName |Windows 驗證的使用者名稱。 |是 (適用於 Windows 驗證) |
| password |Windows 驗證的密碼。 |是 (適用於 Windows 驗證) |
| gatewayName |Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello HDFS。 |是 |
| encryptedCredential |[新 AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) hello 存取認證的輸出。 |否 |

#### <a name="example-using-anonymous-authentication"></a>範例：使用匿名驗證

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-windows-authentication"></a>範例：使用 Windows 驗證

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

如需詳細資訊，請參閱 [HDFS 連接器](#data-factory-hdfs-connector.md#linked-service-properties)文件。 

### <a name="dataset"></a>Dataset
toodefine HDFS 資料集設定 hello**類型**hello 資料集太**FileShare**，並指定下列屬性在 hello hello **typeProperties** > 一節： 

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| folderPath |路徑 toohello 資料夾。 範例： `myfolder`<br/><br/>使用逸出字元 '\' hello 字串中的特殊字元。 例如︰若為 folder\subfolder，請指定 folder\\\\subfolder；若為 d:\samplefolder，請指定 d:\\\\samplefolder。<br/><br/>您可以結合此屬性與**partitionBy** toohave 資料夾路徑根據配量開始/結束日期時間。 |是 |
| fileName |在 hello 指定 hello hello 檔案名稱**folderPath**如果您想 hello 資料表 toorefer tooa 特定檔案 hello 資料夾中的。 如果您未指定任何值，這個屬性，hello 資料表會指向 tooall hello 資料夾中的檔案。<br/><br/>檔案名稱未指定輸出資料集，hello hello 產生檔案名稱會在 hello 遵循此格式： <br/><br/>Data<Guid>.txt (例如：Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |否 |
| partitionedBy |partitionedBy 可以是使用的 toospecify 動態 folderPath，時間序列資料的檔案名稱。 範例：folderPath 可針對每小時的資料進行參數化。 |否 |
| format | 支援下列格式類型的 hello: **TextFormat**， **JsonFormat**， **AvroFormat**， **OrcFormat**， **ParquetFormat**。 設定 hello**類型**下格式 tooone 這些值的屬性。 如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。 <br><br> 如果您想太**複製檔做為-是**之間以檔案為基礎存放區 （二進位複製），略過這兩個輸入和輸出資料集定義中的 hello 格式 > 一節。 |否 |
| compression | 指定 hello 類型和層級的 hello 資料壓縮。 支援的類型為：**GZip**、**Deflate**、**BZip2** 及 **ZipDeflate**。 支援的層級為：**Optimal** 和 **Fastest**。 如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。 |否 |

> [!NOTE]
> 無法同時使用檔名和 fileFilter。

#### <a name="example"></a>範例

```json
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

如需詳細資訊，請參閱 [HDFS 連接器](#data-factory-hdfs-connector.md#dataset-properties)文件。 

### <a name="file-system-source-in-copy-activity"></a>複製活動中的檔案系統來源
如果您從 HDFS 中複製資料，設定 hello**來源類型**的 hello 複製活動太**FileSystemSource**，並指定下列屬性在 hello**來源**> 一節：

**FileSystemSource**支援 hello 下列屬性：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| 遞迴 |指出是否 hello 讀取資料以遞迴方式從 hello 子資料夾，或只能從 hello 指定的資料夾。 |True/False (預設值為 False) |否 |

#### <a name="example"></a>範例

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "HdfsToBlobCopy",
            "inputs": [{
                "name": "InputDataset"
            }],
            "outputs": [{
                "name": "OutputDataset"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

如需詳細資訊，請參閱 [HDFS 連接器](#data-factory-hdfs-connector.md#copy-activity-properties)文件。

## <a name="sftp"></a>SFTP


### <a name="linked-service"></a>連結服務
toodefine SFTP 連結服務，設定 hello**類型**hello 的連結服務太**Sftp**，並指定下列屬性在 hello **typeProperties** > 一節：  

| 屬性 | 說明 | 必要 |
| --- | --- | --- | --- |
| 主機 | Hello SFTP 伺服器的名稱或 IP 位址。 |是 |
| 連接埠 |哪些 hello SFTP 伺服器正在接聽連接埠。 hello 預設值是： 21 |否 |
| authenticationType |指定驗證類型。 允許的值︰**Basic**、**SshPublicKey**。 <br><br> 請參閱太[使用基本驗證](#using-basic-authentication)和[使用 SSH 公開金鑰驗證](#using-ssh-public-key-authentication)分別區段上多個屬性和 JSON 範例。 |是 |
| skipHostKeyValidation | 指定是否 tooskip 主機金鑰的驗證。 | 否。 hello 預設值： false |
| hostKeyFingerprint | 指定 hello 指紋 hello 主索引鍵。 | 是如果 hello `skipHostKeyValidation` toofalse 設定。  |
| gatewayName |名稱的 hello 資料管理閘道器 tooconnect tooan 內部 SFTP 伺服器。 | 如果從內部部署 SFTP 伺服器複製資料，則為 [是]。 |
| encryptedCredential | 加密的認證 tooaccess hello SFTP 伺服器。 自動產生複製精靈] 或 [hello ClickOnce 快顯對話方塊中指定基本驗證 （使用者名稱 + 密碼） 或 SshPublicKey 驗證 （使用者名稱 + 私用金鑰的路徑或內容） 時。 | 否。 僅當從內部部署 SFTP 伺服器複製資料時才套用。 |

#### <a name="example-using-basic-authentication"></a>範例：使用基本驗證

toouse 基本驗證時，設定`authenticationType`為`Basic`，並指定下列屬性，除了 hello SFTP 連接器 hello 最後一節中導入的泛型的 hello:

| 屬性 | 說明 | 必要 |
| --- | --- | --- | --- |
| username | 具有存取 toohello SFTP 伺服器的使用者。 |是 |
| password | Hello 使用者 （使用者名稱） 的密碼。 | 是 |

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<SFTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a>範例：採用加密認證的基本驗證**

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="using-ssh-public-key-authentication"></a>使用 SSH 公用金鑰驗證：**

toouse 基本驗證時，設定`authenticationType`為`SshPublicKey`，並指定下列屬性，除了 hello SFTP 連接器 hello 最後一節中導入的泛型的 hello:

| 屬性 | 說明 | 必要 |
| --- | --- | --- | --- |
| username |使用者具有存取 toohello SFTP 伺服器 |是 |
| privateKeyPath | 指定絕對路徑 toohello 私密金鑰檔案可以存取該閘道。 | 指定任一個 hello`privateKeyPath`或`privateKeyContent`。 <br><br> 僅當從內部部署 SFTP 伺服器複製資料時才套用。 |
| privateKeyContent | Hello 私用的索引鍵內容的序列化的字串。 hello 複製精靈可以讀取 hello 私密金鑰檔案，並自動擷取 hello 私用的索引鍵內容。 如果您使用任何其他工具/SDK，請改為使用 hello privateKeyPath 屬性。 | 指定任一個 hello`privateKeyPath`或`privateKeyContent`。 |
| passPhrase | 指定 hello 傳遞片語/密碼 toodecrypt hello 私密金鑰如果 hello 金鑰檔受複雜密碼。 | [是] 如果 hello 私密金鑰檔案受複雜密碼。 |

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a>範例︰使用私密金鑰內容的 SshPublicKey 驗證**

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

如需詳細資訊，請參閱 [SFTP 連接器](data-factory-sftp-connector.md#linked-service-properties)文件。 

### <a name="dataset"></a>Dataset
toodefine SFTP 資料集設定 hello**類型**hello 資料集太**FileShare**，並指定下列屬性在 hello hello **typeProperties** > 一節： 

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| folderPath |子路徑 toohello 資料夾。 使用逸出字元 '\' hello 字串中的特殊字元。 如需範例，請參閱 [範例連結服務和資料集定義](#sample-linked-service-and-dataset-definitions) 。<br/><br/>您可以結合此屬性與**partitionBy** toohave 資料夾路徑根據配量開始/結束日期時間。 |是 |
| fileName |在 hello 指定 hello hello 檔案名稱**folderPath**如果您想 hello 資料表 toorefer tooa 特定檔案 hello 資料夾中的。 如果您未指定任何值，這個屬性，hello 資料表會指向 tooall hello 資料夾中的檔案。<br/><br/>檔案名稱未指定輸出資料集，hello hello 產生檔案名稱會在 hello 遵循此格式： <br/><br/>Data.<Guid>.txt (範例：Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |否 |
| fileFilter |指定篩選 toobe 使用 tooselect hello folderPath 中檔案的子集，而不是所有的檔案。<br/><br/>允許的值為︰`*` (多個字元) 和 `?` (單一字元)。<br/><br/>範例 1：`"fileFilter": "*.log"`<br/>範例 2：`"fileFilter": 2016-1-?.txt"`<br/><br/> fileFilter 適用於輸入 FileShare 資料集。 這個屬性不支援使用 HDFS。 |否 |
| partitionedBy |partitionedBy 可以是使用的 toospecify 動態 folderPath，時間序列資料的檔案名稱。 例如，folderPath 可針對每小時的資料進行參數化。 |否 |
| format | 支援下列格式類型的 hello: **TextFormat**， **JsonFormat**， **AvroFormat**， **OrcFormat**， **ParquetFormat**。 設定 hello**類型**下格式 tooone 這些值的屬性。 如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。 <br><br> 如果您想太**複製檔做為-是**之間以檔案為基礎存放區 （二進位複製），略過這兩個輸入和輸出資料集定義中的 hello 格式 > 一節。 |否 |
| compression | 指定 hello 類型和層級的 hello 資料壓縮。 支援的類型為：**GZip**、**Deflate**、**BZip2** 及 **ZipDeflate**。 支援的層級為：**Optimal** 和 **Fastest**。 如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。 |否 |
| useBinaryTransfer |指定是否使用二進位傳輸模式。 二進位模式為 true，ASCII 則為 false。 預設值：True。 只有在相關聯的連結服務類型的類型為 FtpServer 時，才可以使用這個屬性。 |否 |

> [!NOTE]
> 無法同時使用檔名和 fileFilter。

#### <a name="example"></a>範例

```json
{
    "name": "SFTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "SftpLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
            "fileName": "test.csv"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

如需詳細資訊，請參閱 [SFTP 連接器](data-factory-sftp-connector.md#dataset-properties)文件。 

### <a name="file-system-source-in-copy-activity"></a>複製活動中的檔案系統來源
如果您從 SFTP 來源複製資料，設定 hello**來源類型**的 hello 複製活動太**FileSystemSource**，並指定下列屬性在 hello**來源**區段：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| 遞迴 |指出是否 hello 讀取資料以遞迴方式從 hello 子資料夾，或只能從 hello 指定的資料夾。 |True/False (預設值為 False) |否 |



#### <a name="example"></a>範例

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
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
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2017-02-20T18:00:00",
        "end": "2017-02-20T19:00:00"
    }
}
```

如需詳細資訊，請參閱 [SFTP 連接器](data-factory-sftp-connector.md#copy-activity-properties)文件。


## <a name="http"></a>HTTP

### <a name="linked-service"></a>連結服務
toodefine HTTP 連結服務，設定 hello**類型**hello 的連結服務太**Http**，並指定下列屬性在 hello **typeProperties** > 一節：  

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| url | 基底 URL toohello Web 伺服器 | 是 |
| authenticationType | 指定 hello 驗證類型。 允許的值為︰**匿名**、**基本**、**摘要**、**Windows**、**ClientCertificate**。 <br><br> 請參閱 「 toosections 上多個屬性和 JSON 範例此表格下方的驗證類型分別。 | 是 |
| enableServerCertificateValidation | 指定是否 tooenable 伺服器 SSL 憑證驗證，是否來源是 HTTPS 的網頁伺服器 | 否，預設值是 True |
| gatewayName | 名稱的 hello 資料管理閘道器 tooconnect tooan 內部 HTTP 的來源。 | 如果從內部部署 HTTP 來源複製資料，則為是。 |
| encryptedCredential | 加密的認證 tooaccess hello HTTP 端點。 自動產生複製精靈] 或 [hello ClickOnce 快顯對話方塊以設定 hello 驗證資訊。 | 否。 僅當從內部部署 HTTP 伺服器複製資料時才套用。 |

#### <a name="example-using-basic-digest-or-windows-authentication"></a>範例︰使用基本、摘要或 Windows 驗證
設定`authenticationType`為`Basic`， `Digest`，或`Windows`，並指定 hello 除了 hello HTTP 連接器泛型的上方導入了下列屬性：

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| username | 使用者名稱 tooaccess hello HTTP 端點。 | 是 |
| password | Hello 使用者 （使用者名稱） 的密碼。 | 是 |

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "basic",
            "url": "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

#### <a name="example-using-clientcertificate-authentication"></a>範例：使用 ClientCertificate 驗證

toouse 基本驗證時，設定`authenticationType`為`ClientCertificate`，並指定 hello 除了 hello HTTP 連接器泛型的上方導入了下列屬性：

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| embeddedCertData | hello Base64 編碼內容的 hello 個人資訊交換 (PFX) 檔案的二進位資料。 | 指定任一個 hello`embeddedCertData`或`certThumbprint`。 |
| certThumbprint | hello hello 憑證已安裝在閘道機器的憑證存放區上的憑證指紋。 僅當從內部部署 HTTP 來源複製資料時才套用。 | 指定任一個 hello`embeddedCertData`或`certThumbprint`。 |
| password | Hello 憑證相關聯的密碼。 | 否 |

如果您使用`certThumbprint`安裝適用於驗證和 hello 憑證的 hello hello 本機電腦的個人存放區中，您需要 toogrant hello 的讀取權限 toohello 閘道服務：

1. 啟動 Microsoft Management Console (MMC)。 新增 hello**憑證**嵌入式管理單元的目標 hello**本機電腦**。
2. 展開 [憑證]，[個人]，然後按一下 [憑證]。
3. Hello 個人存放區中的 hello 憑證上按一下滑鼠右鍵，然後選取**所有工作**->**管理私用金鑰...**
3. 在 hello**安全性**索引標籤上，新增 hello 資料管理閘道主機服務執行使用 hello 讀取權限 toohello 憑證的使用者帳戶。  

**範例： 使用用戶端憑證：**此連結服務連結資料 factory tooan 內部 HTTP web 伺服器。 它會使用與資料管理閘道器安裝 hello 機器已安裝的用戶端憑證。

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"
        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a>範例︰在檔案中使用用戶端憑證
此連結服務連結資料 factory tooan 內部 HTTP web 伺服器。 它會使用資料管理閘道器安裝 hello 機器上的用戶端憑證檔案。

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

如需詳細資訊，請參閱 [HTTP 連接器](data-factory-http-connector.md#linked-service-properties)文件。

### <a name="dataset"></a>Dataset
toodefine HTTP 資料集，設定 hello**類型**hello 資料集太**Http**，並指定下列屬性在 hello hello **typeProperties** > 一節： 

| 屬性 | 說明 | 必要 |
|:--- |:--- |:--- |
| relativeUrl | 包含 hello 資料的相對 URL toohello 資源。 若未指定路徑，則會使用連結的 hello 服務定義中指定的唯一 hello URL。 <br><br> tooconstruct 動態 URL，您可以使用[Data Factory 函數和系統變數](data-factory-functions-variables.md)，範例： `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`。 | 否 |
| requestMethod | HTTP 方法。 允許的值為 **GET** 或 **POST**。 | 否。 預設值為 `GET`。 |
| additionalHeaders | 其他 HTTP 要求標頭。 | 否 |
| requestBody | HTTP 要求的內文。 | 否 |
| format | 如果您想 toosimply **hello 資料擷取 HTTP 端點以-為**而不剖析它，請略過此格式設定。 <br><br> 如果您希望 tooparse hello HTTP 回應內容進行複製時，支援下列格式類型的 hello: **TextFormat**， **JsonFormat**， **AvroFormat**， **OrcFormat**， **ParquetFormat**。 如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。 |否 |
| compression | 指定 hello 類型和層級的 hello 資料壓縮。 支援的類型為：**GZip**、**Deflate**、**BZip2** 及 **ZipDeflate**。 支援的層級為：**Optimal** 和 **Fastest**。 如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。 |否 |

#### <a name="example-using-hello-get-default-method"></a>範例： 使用 hello GET （預設值） 方法

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

#### <a name="example-using-hello-post-method"></a>範例： 使用 hello POST 方法

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
            "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
如需詳細資訊，請參閱 [HTTP 連接器](data-factory-http-connector.md#dataset-properties)文件。

### <a name="http-source-in-copy-activity"></a>複製活動中的 HTTP 來源
如果您從 HTTP 來源複製資料，設定 hello**來源類型**的 hello 複製活動太**HttpSource**，並指定下列屬性在 hello**來源**> 一節：

| 屬性 | 說明 | 必要 |
| -------- | ----------- | -------- |
| httpRequestTimeout | hello 回應 hello HTTP 要求 tooget 的逾時 (TimeSpan)。 它是 hello 逾時 tooget 回應時，不 hello 逾時 tooread 回應資料。 | 否。 預設值：00:01:40 |


#### <a name="example"></a>範例

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "HttpSourceToAzureBlob",
            "description": "Copy from an HTTP source tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "HttpSourceDataInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "HttpSource"
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
        }]
    }
}
```

如需詳細資訊，請參閱 [HTTP 連接器](data-factory-http-connector.md#copy-activity-properties)文件。

## <a name="odata"></a>OData

### <a name="linked-service"></a>連結服務
toodefine OData 連結的服務，設定 hello**類型**hello 的連結服務太**OData**，並指定下列屬性在 hello **typeProperties** > 一節：  

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| url |Hello OData 服務的 Url。 |是 |
| authenticationType |Tooconnect toohello OData 來源使用的驗證類型。 <br/><br/> 若為雲端 OData，可能的值為 Anonymous、Basic 和 OAuth (請注意，Azure Data Factory 目前僅支援 Azure Active Directory 架構的 OAuth)。 <br/><br/> 若為內部部署 OData，可能的值為 Anonymous、Basic 和 Windows。 |是 |
| username |如果您要使用 Basic 驗證，請指定使用者名稱。 |是 (只在您使用基本驗證時) |
| password |指定 hello hello 使用者名稱所指定的使用者帳戶的密碼。 |是 (只在您使用基本驗證時) |
| authorizedCredential |如果您使用 OAuth 時，按一下**授權**按鈕 hello 資料 Factory 複製精靈或編輯器中，輸入您的認證，然後 hello 這個屬性的值將會自動產生。 |是 (只有在您使用 OAuth 驗證時) |
| gatewayName |Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello 在內部部署 OData 服務。 只在要從內部部署 OData 來源複製資料時才指定。 |否 |

#### <a name="example---using-basic-authentication"></a>範例 - 使用基本驗證
```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Basic",
            "username": "username",
            "password": "password"
        }
    }
}
```

#### <a name="example---using-anonymous-authentication"></a>範例 - 使用匿名驗證

```json
{
    "name": "ODataLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        }
    }
}
```

#### <a name="example---using-windows-authentication-accessing-on-premises-odata-source"></a>範例 - 使用 Windows 驗證存取內部部署 OData 來源

```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "<endpoint of on-premises OData source, for example, Dynamics CRM>",
            "authenticationType": "Windows",
            "username": "domain\\user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example---using-oauth-authentication-accessing-cloud-odata-source"></a>範例 - 使用 OAuth 驗證存取雲端 OData 來源
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of cloud OData source, for example, https://<tenant>.crm.dynamics.com/XRMServices/2011/OrganizationData.svc>",
            "authenticationType": "OAuth",
            "authorizedCredential": "<auto generated by clicking hello Authorize button on UI>"
        }
    }
}
```

如需詳細資訊，請參閱 [OData 連接器](data-factory-odata-connector.md#linked-service-properties)文件。

### <a name="dataset"></a>Dataset
toodefine OData 資料集設定 hello**類型**hello 資料集太**ODataResource**，並指定下列屬性在 hello hello **typeProperties** > 一節： 

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 路徑 |路徑 toohello OData 資源 |否 |

#### <a name="example"></a>範例

```json
{
    "name": "ODataDataset",
    "properties": {
        "type": "ODataResource",
        "typeProperties": {
            "path": "Products"
        },
        "linkedServiceName": "ODataLinkedService",
        "structure": [],
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3
        }
    }
}
```

如需詳細資訊，請參閱 [OData 連接器](data-factory-odata-connector.md#dataset-properties)文件。

### <a name="relational-source-in-copy-activity"></a>複製活動中的關聯式來源
如果您從 OData 來源複製資料，設定 hello**來源類型**的 hello 複製活動太**RelationalSource**，並指定下列屬性在 hello**來源**區段：

| 屬性 | 說明 | 範例 | 必要 |
| --- | --- | --- | --- |
| query |使用自訂查詢 tooread hello 的資料。 |「?$select=Name, Description&$top=5」 |否 |

#### <a name="example"></a>範例

```json
{
    "name": "CopyODataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "?$select=Name, Description&$top=5"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "ODataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobODataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "ODataToBlob"
        }],
        "start": "2017-02-01T18:00:00",
        "end": "2017-02-03T19:00:00"
    }
}
```

如需詳細資訊，請參閱 [OData 連接器](data-factory-odata-connector.md#copy-activity-properties)文件。


## <a name="odbc"></a>ODBC


### <a name="linked-service"></a>連結服務
toodefine ODBC 連結服務，設定 hello**類型**hello 的連結服務太**OnPremisesOdbc**，並指定下列屬性在 hello **typeProperties** > 一節：  

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| connectionString |hello 非存取認證部分 hello 連接字串和選擇性的加密認證。 請參閱下列各節的 hello 範例。 |是 |
| 認證 |hello 存取認證的 hello 驅動程式特有的屬性值的格式指定的連接字串部分。 範例：“Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”。 |否 |
| authenticationType |Tooconnect toohello ODBC 資料存放區使用的驗證類型。 可能的值為：Anonymous 和 Basic。 |是 |
| username |如果您要使用 Basic 驗證，請指定使用者名稱。 |否 |
| password |指定 hello hello 使用者名稱所指定的使用者帳戶的密碼。 |否 |
| gatewayName |Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello ODBC 資料存放區。 |是 |

#### <a name="example---using-basic-authentication"></a>範例 - 使用基本驗證

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```
#### <a name="example---using-basic-authentication-with-encrypted-credentials"></a>範例 - 使用基本驗證搭配加密認證
您可以加密使用 hello hello 認證[新增 AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) （1.0 版本的 Azure PowerShell） 指令程式或[New-azuredatafactoryencryptvalue](https://msdn.microsoft.com/library/dn834940.aspx) （0.9 或更早版本的 helloAzure PowerShell)。  

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-anonymous-authentication"></a>範例：使用匿名驗證

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

如需詳細資訊，請參閱 [ODBC 連接器](data-factory-odbc-connector.md#linked-service-properties)文件。 

### <a name="dataset"></a>Dataset
toodefine ODBC 資料集設定 hello**類型**hello 資料集太**RelationalTable**，並指定下列屬性在 hello hello **typeProperties** > 一節： 

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| tableName |Hello ODBC 資料存放區中的 hello 資料表的名稱。 |是 |


#### <a name="example"></a>範例

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "ODBCLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

如需詳細資訊，請參閱 [ODBC 連接器](data-factory-odbc-connector.md#dataset-properties)文件。 

### <a name="relational-source-in-copy-activity"></a>複製活動中的關聯式來源
如果您從 ODBC 資料存放區複製資料，設定 hello**來源類型**的 hello 複製活動太**RelationalSource**，並指定下列屬性在 hello**來源**區段：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| query |使用自訂查詢 tooread hello 的資料。 |SQL 查詢字串。 例如： `select * from MyTable`。 |是 |

#### <a name="example"></a>範例

```json
{
    "name": "CopyODBCToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "OdbcDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobOdbcDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "OdbcToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
``` 

如需詳細資訊，請參閱 [ODBC 連接器](data-factory-odbc-connector.md#copy-activity-properties)文件。

## <a name="salesforce"></a>Salesforce


### <a name="linked-service"></a>連結服務
toodefine Salesforce 連結服務，設定 hello**類型**hello 的連結服務太**Salesforce**，並指定下列屬性在 hello **typeProperties** > 一節：  

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| environmentUrl | 指定 hello URL 的 Salesforce 執行個體。 <br><br> - 預設值為 " https://login.salesforce.com "。 <br> -從沙箱，toocopy 資料指定"https://test.salesforce.com"。 <br> -toocopy 資料從自訂網域，指定，例如，"https://[domain].my.salesforce.com"。 |否 |
| username |指定 hello 使用者帳戶的使用者名稱。 |是 |
| password |指定 hello 使用者帳戶的密碼。 |是 |
| securityToken |指定 hello 使用者帳戶的安全性權杖。 請參閱[取得安全性權杖](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm)如需有關指示 tooreset 取得安全性權杖。 一般情況下，請參閱關於安全性權杖的 toolearn[安全性和 hello API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm)。 |是 |

#### <a name="example"></a>範例

```json
{
    "name": "SalesforceLinkedService",
    "properties": {
        "type": "Salesforce",
        "typeProperties": {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```

如需詳細資訊，請參閱 [Salesforce 連接器](data-factory-salesforce-connector.md#linked-service-properties)文件。 

### <a name="dataset"></a>Dataset
toodefine Salesforce 資料集設定 hello**類型**hello 資料集太**RelationalTable**，並指定下列屬性在 hello hello **typeProperties** > 一節： 

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| tableName |在 Salesforce 中的 hello 資料表的名稱。 |否 (如果已指定 **RelationalSource** 的 **query**) |

#### <a name="example"></a>範例

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

如需詳細資訊，請參閱 [Salesforce 連接器](data-factory-salesforce-connector.md#dataset-properties)文件。 

### <a name="relational-source-in-copy-activity"></a>複製活動中的關聯式來源
如果您從 Salesforce 複製資料，設定 hello**來源類型**的 hello 複製活動太**RelationalSource**，並指定下列屬性在 hello**來源**區段：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| query |使用自訂查詢 tooread hello 的資料。 |SQL-92 查詢或 [Salesforce 物件查詢語言 (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) 查詢。 例如：`select * from MyTable__c`。 |否 (如果 hello **tableName**的 hello**資料集**指定) |

#### <a name="example"></a>範例  



```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "SalesforceInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"
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
        }]
    }
}
```

> [!IMPORTANT]
> hello"__c"hello API 名稱部分所需的任何自訂的物件。

如需詳細資訊，請參閱 [Salesforce 連接器](data-factory-salesforce-connector.md#copy-activity-properties)文件。 

## <a name="web-data"></a>Web 資料 

### <a name="linked-service"></a>連結服務
toodefine Web 連結服務，設定 hello**類型**hello 的連結服務太**Web**，並指定下列屬性在 hello **typeProperties** > 一節：  

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| Url |URL toohello Web 來源 |是 |
| authenticationType |匿名。 |是 |
 

#### <a name="example"></a>範例


```json
{
    "name": "web",
    "properties": {
        "type": "Web",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "url": "https://en.wikipedia.org/wiki/"
        }
    }
}
```

如需詳細資訊，請參閱 [Web 資料表連接器](data-factory-web-table-connector.md#linked-service-properties)文件。 

### <a name="dataset"></a>Dataset
toodefine Web 資料集設定 hello**類型**hello 資料集太**WebTable**，並指定下列屬性在 hello hello **typeProperties** > 一節： 

| 屬性 | 說明 | 必要 |
|:--- |:--- |:--- |
| 類型 |hello 資料集的類型。 必須設定得**WebTable** |是 |
| 路徑 |相對 URL toohello 資源包含 hello 資料表。 |否。 若未指定路徑，則會使用連結的 hello 服務定義中指定的唯一 hello URL。 |
| index |hello hello 資源中的 hello 資料表的索引。 請參閱[Get 索引的資料表中的 HTML 網頁的](#get-index-of-a-table-in-an-html-page)> 一節步驟 toogetting 索引的 HTML 網頁中的資料表。 |是 |

#### <a name="example"></a>範例

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

如需詳細資訊，請參閱 [Web 資料表連接器](data-factory-web-table-connector.md#dataset-properties)文件。 

### <a name="web-source-in-copy-activity"></a>複製活動中的 Web 來源
如果您從 web 資料表複製資料，設定 hello**來源類型**的 hello 複製活動太**WebSource**。 目前，當複製活動中的 hello 來源屬於型別**WebSource**，支援任何其他屬性。

#### <a name="example"></a>範例

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "WebTableToAzureBlob",
            "description": "Copy from a Web table tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "WebTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "WebSource"
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
        }]
    }
}
```

如需詳細資訊，請參閱 [Web 資料表連接器](data-factory-web-table-connector.md#copy-activity-properties)文件。 

## <a name="compute-environments"></a>計算環境
hello 下表列出支援的 Data Factory 和 hello 轉換活動可以在其上執行的 hello 運算環境。 按一下 hello 連結 hello 計算您所感興趣 toosee hello JSON 結構描述的連結的服務 toolink 它 tooa 資料 factory。 

| 計算環境 | 活動 |
| --- | --- |
| [隨選 HDInsight 叢集](#on-demand-azure-hdinsight-cluster)或[您自己的 HDInsight 叢集](#existing-azure-hdinsight-cluster) |[.NET 自訂活動](#net-custom-activity)、[Hive 活動](#hdinsight-hive-activity)、[Pig 活動](#hdinsight-pig-acitivity、[MapReduce 活動](#hdinsight-mapreduce-activity)、[Hadoop 串流活動](#hdinsight-streaming-activityd)、[Spark 活動](#hdinsight-spark-activity) |
| [Azure Batch](#azure-batch) |[.NET 自訂活動](#net-custom-activity) |
| [Azure Machine Learning](#azure-machine-learning) | [Machine Learning 批次執行活動](#machine-learning-batch-execution-activity)、[Machine Learning 更新資源活動](#machine-learning-update-resource-activity) |
| [Azure Data Lake Analytics](#azure-data-lake-analytics) |[Data Lake Analytics U-SQL](#data-lake-analytics-u-sql-activity) |
| [Azure SQL Database](#azure-sql-database-1)、[Azure SQL 資料倉儲](#azure-sql-data-warehouse-1)、[SQL Server](#sql-server-1) |[預存程序](#stored-procedure-activity) |

## <a name="on-demand-azure-hdinsight-cluster"></a>隨選 Azure HDInsight 叢集
hello Azure Data Factory 服務會自動建立 Windows/Linux 為基礎-隨選 HDInsight 叢集 tooprocess 資料。 hello 叢集建立在 hello 與 hello 叢集與 hello 儲存體帳戶 （hello JSON 中的 linkedServiceName 屬性） 相同的區域相關聯。 您可以執行下列轉換活動上這項連結服務的 hello: [.NET 自訂活動](#net-custom-activity)， [Hive 活動](#hdinsight-hive-activity)，[Pig 活動] (#hdinsight pig-活動， [MapReduce 活動](#hdinsight-mapreduce-activity)， [Hadoop 串流活動](#hdinsight-streaming-activityd)，[二手活動](#hdinsight-spark-activity)。 

### <a name="linked-service"></a>連結服務 
下表中的 hello 提供 hello 屬性視 HDInsight 連結服務的 hello Azure JSON 定義中所使用的說明。

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 類型 |hello 類型屬性應該設定太**HDInsightOnDemand**。 |是 |
| clusterSize |背景工作/資料 hello 叢集中的節點數目。 以及您為此屬性指定的背景工作角色節點的 hello 數目的 2 個前端節點建立 hello HDInsight 叢集。 hello 節點有大小有 4 個核心，因此 4 的背景工作節點叢集會採用 24 個核心的 Standard_D3 (4\*4 = 16 個核心的背景工作節點，再加上 2\*4 = 8 個核心的前端節點)。 請參閱[HDInsight 叢集建立 Linux Hadoop](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) hello Standard_D3 層的詳細資料。 |是 |
| timetolive |hello 允許 hello 隨選 HDInsight 叢集的閒置時間。 指定多久 hello 隨選 HDInsight 叢集會保持運作如果 hello 叢集中沒有其他作用中的工作執行的活動完成後。<br/><br/>例如，如果在 6 分鐘和 timetolive 執行的活動是設定 too5 分鐘，hello 叢集會保持運作 5 分鐘之後 hello 6 分鐘處理 hello 活動執行。 如果另一個執行的活動與 hello 6 分鐘視窗執行時，處理 hello 相同叢集中。<br/><br/>建立隨選 HDInsight 叢集是昂貴的作業 （可能需要一些時間），因此使用這項設定的 data factory 所需的 tooimprove 效能重複使用隨選 HDInsight 叢集。<br/><br/>如果您設定 timetolive 值 too0，只要執行的 hello 活動處理，會刪除 hello 叢集。 在 hello 相反地，如果您設定較高的值，hello 叢集可能保持閒置不必要地產生高成本。 因此，很重要，您會設定 hello 適當的值，根據您的需求。<br/><br/>多個管線可以共用 hello hello 隨選 HDInsight 叢集的同一個執行個體，如果適當地設定 hello timetolive 屬性值 |是 |
| 版本 |Hello HDInsight 叢集的版本。 如需詳細資訊，請參閱 [Azure Data Factory 中支援的 HDInsight 版本](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory)。 |否 |
| linkedServiceName |Azure 儲存體連結服務 toobe hello 視叢集使用的儲存及處理資料。 <p>目前，您無法建立使用 Azure 資料湖存放區為 hello 存放裝置的隨 HDInsight 叢集。 如果您想要從 HDInsight 處理 Azure 資料湖存放區中的 toostore hello 結果資料，請使用 hello Azure Blob 儲存體 toohello Azure Data Lake Store 複製活動 toocopy hello 資料。</p>  | 是 |
| additionalLinkedServiceNames |指定額外的儲存體帳戶的 hello HDInsight 連結服務，以便 hello Data Factory 服務可以代表您註冊它們。 |否 |
| osType |作業系統的類型。 允許的值為：Windows (預設值) 和 linux |否 |
| hcatalogLinkedServiceName |該點 toohello HCatalog 資料庫服務的 Azure SQL 連結的 hello 名稱。 hello 隨選 HDInsight 叢集會建立使用 hello Azure SQL database 當做 hello 中繼存放區。 |否 |

### <a name="json-example"></a>JSON 範例
下列 JSON hello 定義以 Linux 為基礎的隨選 HDInsight 連結服務。 hello Data Factory 服務會自動建立**linux**時處理資料配量的 HDInsight 叢集。 

```json
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "StorageLinkedService"
        }
    }
}
```

如需詳細資訊，請參閱[計算連結服務](data-factory-compute-linked-services.md)一文。 

## <a name="existing-azure-hdinsight-cluster"></a>現有的 Azure HDInsight 叢集
您可以使用 Data Factory 建立 Azure HDInsight 連結服務 tooregister HDInsight 叢集。 您可以執行資料轉換活動遵循這項連結服務的 hello: [.NET 自訂活動](#net-custom-activity)， [Hive 活動](#hdinsight-hive-activity)，[Pig 活動] (#hdinsight pig-活動， [MapReduce活動](#hdinsight-mapreduce-activity)， [Hadoop 串流活動](#hdinsight-streaming-activityd)，[二手活動](#hdinsight-spark-activity)。 

### <a name="linked-service"></a>連結服務
hello 下表提供使用 Azure HDInsight 連結服務的 hello Azure JSON 定義中的 hello 屬性的說明。

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 類型 |hello 類型屬性應該設定太**HDInsight**。 |是 |
| clusterUri |hello hello HDInsight 叢集的 URI。 |是 |
| username |指定的 hello 使用者 toobe hello 名稱使用 tooconnect tooan 現有 HDInsight 叢集。 |是 |
| password |指定 hello 使用者帳戶的密碼。 |是 |
| linkedServiceName | Hello HDInsight 叢集供 hello 參照 toohello Azure blob 儲存體的 Azure 儲存體連結服務的名稱。 <p>目前，您無法針對此屬性指定 Azure Data Lake Store 連結服務。 如果 hello HDInsight 叢集已存取 toohello 資料湖存放區，您可能會存取 hello Azure 資料湖存放區中的資料從 Hive/Pig 指令碼。 </p>  |是 |

如需支援的 HDInsight 叢集版本，請參閱[支援的 HDInsight 版本](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory)。 

#### <a name="json-example"></a>JSON 範例

```json
{
    "name": "HDInsightLinkedService",
    "properties": {
        "type": "HDInsight",
        "typeProperties": {
            "clusterUri": " https://<hdinsightclustername>.azurehdinsight.net/",
            "userName": "admin",
            "password": "<password>",
            "linkedServiceName": "MyHDInsightStoragelinkedService"
        }
    }
}
```

## <a name="azure-batch"></a>Azure Batch
您可以使用 data factory 建立 Azure 批次連結服務 tooregister 批次集區的虛擬機器 (Vm)。 您可以使用 Azure Batch 或 Azure HDInsight 執行 .NET 自訂活動。 您可以在此連結服務上執行 [.NET 自訂活動](#net-custom-activity)。 

### <a name="linked-service"></a>連結服務
hello 下表提供使用 Azure Batch 連結服務的 hello Azure JSON 定義中的 hello 屬性的說明。

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 類型 |hello 類型屬性應該設定太**AzureBatch**。 |是 |
| accountName |Hello Azure Batch 帳戶的名稱。 |是 |
| accessKey |Hello Azure Batch 帳戶存取金鑰。 |是 |
| poolName |Hello 集區的虛擬機器名稱。 |是 |
| linkedServiceName |Hello 與此 Azure Batch 連結服務相關聯的 Azure 儲存體連結服務的名稱。 這項連結的服務用於暫存檔案需要 toorun hello 活動與 hello 活動執行記錄的儲存。 |是 |


#### <a name="json-example"></a>JSON 範例

```json
{
    "name": "AzureBatchLinkedService",
    "properties": {
        "type": "AzureBatch",
        "typeProperties": {
            "accountName": "<Azure Batch account name>",
            "accessKey": "<Azure Batch account key>",
            "poolName": "<Azure Batch pool name>",
            "linkedServiceName": "<Specify associated storage linked service reference here>"
        }
    }
}
```

## <a name="azure-machine-learning"></a>Azure Machine Learning
建立 Azure Machine Learning 連結服務 tooregister Machine Learning 批次評分端點使用 data factory。 您可以在此連結服務上執行兩個資料轉換活動︰[Machine Learning 批次執行活動](#machine-learning-batch-execution-activity)、[Machine Learning 更新資源活動](#machine-learning-update-resource-activity)。 

### <a name="linked-service"></a>連結服務
hello 下表提供使用 Azure Machine Learning 連結服務的 hello Azure JSON 定義中的 hello 屬性的說明。

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 類型 |hello 類型屬性應該設定為： **AzureML**。 |是 |
| mlEndpoint |hello 批次評分 URL。 |是 |
| apiKey |hello 發行工作區模型的 API。 |是 |

#### <a name="json-example"></a>JSON 範例

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://[batch scoring endpoint]/jobs",
            "apiKey": "<apikey>"
        }
    }
}
```

## <a name="azure-data-lake-analytics"></a>Azure Data Lake Analytics
您建立**Azure Data Lake Analytics**之前使用 hello 連結服務 toolink Azure Data Lake Analytics 計算服務 tooan Azure data factory[資料 Lake Analytics U-SQL 活動](data-factory-usql-activity.md)管線中.

### <a name="linked-service"></a>連結服務

下表中的 hello 提供 hello 屬性連結 Azure Data Lake Analytics 服務的 hello JSON 定義中所使用的說明。 

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 類型 |hello 類型屬性應該設定為： **AzureDataLakeAnalytics**。 |是 |
| accountName |Azure Data Lake Analytics 帳戶名稱。 |是 |
| dataLakeAnalyticsUri |Azure Data Lake Analytics URI。 |否 |
| 授權 |按一下之後，就會自動擷取授權碼**授權**hello Data Factory 編輯器和完成 hello OAuth 登入 按鈕。 |是 |
| subscriptionId |Azure 訂用帳戶識別碼 |否 （如果未指定，訂用帳戶的資料處理站可用的 hello）。 |
| resourceGroupName |Azure 資源群組名稱 |否 （如果未指定，資源群組的資料處理站可用的 hello）。 |
| sessionId |從 hello OAuth 授權工作階段的工作階段識別碼。 每個工作階段識別碼都是唯一的，只能使用一次。 當您使用 hello Data Factory 編輯器時，這個識別碼是自動產生。 |是 |


#### <a name="json-example"></a>JSON 範例
下列範例中的 hello 提供 JSON 定義連結的 Azure 資料湖分析服務。

```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "<account name>",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>",
            "subscriptionId": "<subscription id>",
            "resourceGroupName": "<resource group name>"
        }
    }
}
```

## <a name="azure-sql-database"></a>Azure SQL Database
您建立 Azure SQL 連結服務，並使用它搭配 hello[預存程序活動](#stored-procedure-activity)tooinvoke 從 Data Factory 管線的預存程序。 

### <a name="linked-service"></a>連結服務
Azure SQL Database toodefine 連結服務，設定 hello**類型**hello 的連結服務太**AzureSqlDatabase**，並指定下列屬性在 hello **typeProperties**> 一節：  

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| connectionString |指定所需的資訊 tooconnect toohello Azure SQL Database 執行個體 hello connectionString 屬性。 |是 |

#### <a name="json-example"></a>JSON 範例

```json
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

如需此連結服務的詳細資料，請參閱 [Azure SQL 連接器](data-factory-azure-sql-connector.md#linked-service-properties) 一文。

## <a name="azure-sql-data-warehouse"></a>Azure SQL 資料倉儲
您建立連結的 Azure SQL 資料倉儲服務，並使用它搭配 hello[預存程序活動](data-factory-stored-proc-activity.md)tooinvoke 從 Data Factory 管線的預存程序。 

### <a name="linked-service"></a>連結服務
Azure SQL 資料倉儲 toodefine 連結服務，設定 hello**類型**hello 的連結服務太**AzureSqlDW**，並指定下列屬性在 hello **typeProperties**> 一節：  

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| connectionString |指定所需的資訊 tooconnect toohello Azure SQL 資料倉儲執行個體 hello connectionString 屬性。 |是 |

#### <a name="json-example"></a>JSON 範例

```json
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

如需詳細資訊，請參閱 [Azure SQL 資料倉儲連接器](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties)文件。 

## <a name="sql-server"></a>SQL Server 
建立連結的 SQL Server 服務，並使用以 hello[預存程序活動](data-factory-stored-proc-activity.md)tooinvoke 從 Data Factory 管線的預存程序。 

### <a name="linked-service"></a>連結服務
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


#### <a name="example-json-for-using-sql-authentication"></a>範例：用於 SQL 驗證的 JSON

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a>範例：用於 Windows 驗證的 JSON

如果未指定使用者名稱和密碼，閘道會使用這些 tooimpersonate hello 指定的使用者帳戶 tooconnect toohello 在內部部署 SQL Server 資料庫。 否則，閘道會直接與 hello 的閘道 （其啟動帳戶） 的安全性內容連線 toohello SQL Server。

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
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

如需詳細資訊，請參閱 [SQL Server 連接器](data-factory-sqlserver-connector.md#linked-service-properties)文件。

## <a name="data-transformation-activities"></a>資料轉換活動

活動 | 說明
-------- | -----------
[HDInsight Hive 活動](#hdinsight-hive-activity) | hello HDInsight Hive 活動 Data Factory 管線中執行您自己的 Hive 查詢或隨 Windows/linux 的 HDInsight 叢集。 
[HDInsight Pig 活動](#hdinsight-pig-activity) | hello HDInsight Pig 活動 Data Factory 管線中執行您自己的 Pig 查詢或隨 Windows/linux 的 HDInsight 叢集。
[HDInsight MapReduce 活動](#hdinsight-mapreduce-activity) | hello HDInsight MapReduce 活動 Data Factory 管線中執行您自己的 MapReduce 程式或隨 Windows/linux 的 HDInsight 叢集。
[HDInsight 串流活動](#hdinsight-streaming-activity) | Data Factory 管線中的 hello HDInsight 串流活動執行您自己的 Hadoop 串流程式或隨 Windows/linux 的 HDInsight 叢集。
[HDInsight Spark 活動](#hdinsight-spark-activity) | hello HDInsight Spark Data Factory 管線中的活動執行您自己的 HDInsight 叢集上的 Spark 程式。 
[Machine Learning Batch 執行活動](#machine-learning-batch-execution-activity) | Azure Data Factory 可讓您 tooeasily 建立管線，使用已發行的 Azure Machine Learning web 服務的預測分析。 使用 Azure Data Factory 管線中的 hello 批次執行活動，您可以叫用批次中的 hello 資料機器學習 web 服務 toomake 的預測。 
[Machine Learning 更新資源活動](#machine-learning-update-resource-activity) | 經過一段時間，在 hello 計分實驗需要 toobe 重新定型使用全新的機器學習中的 hello 預測模型的輸入資料集。 您完成定型之後，您會想要計分 web 服務以 hello tooupdate hello 重新定型機器學習模型。 您可以使用 hello 更新資源活動 tooupdate hello web 服務與 hello 新定型模型。
[預存程序活動](#stored-procedure-activity) | 您可以使用 Data Factory 管線 tooinvoke 其中一種 hello 下列資料存放區預存程序中的 hello 預存程序活動： Azure SQL Database、 Azure SQL 資料倉儲，在您企業中的 SQL Server 資料庫或 Azure VM。 
[Data Lake Analytics U-SQL 活動](#data-lake-analytics-u-sql-activity) | Data Lake Analytics U-SQL 活動會在 Azure Data Lake Analytics 叢集上執行 U-SQL 指令碼。  
[.NET 自訂活動](#net-custom-activity) | 如果您需要 tootransform 資料不支援的 Data Factory 的方式，您可以建立您自己的資料處理邏輯的自訂活動，並使用 hello 管線中的 hello 活動。 您可以設定 hello 自訂.NET 活動 toorun 使用 Azure Batch 服務或 Azure HDInsight 叢集。 

     
## <a name="hdinsight-hive-activity"></a>HDInsight Hive 活動
您可以指定下列屬性 Hive 活動 JSON 定義中的 hello。 hello hello 活動的型別屬性必須是： **HDInsightHive**。 您必須先建立 HDInsight 連結服務，並指定它 hello 名稱做為 hello 值**linkedServiceName**屬性。 hello 支援下列屬性在 hello **typeProperties**區段，當您設定活動 tooHDInsightHive hello 類型：

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| script |指定內嵌 hello Hive 指令碼 |否 |
| 指令碼路徑 |存放區 hello Hive 指令碼在 Azure blob 儲存體，並提供 hello 路徑 toohello 檔案。 使用 'script' 或 'scriptPath' 屬性。 兩者無法同時使用。 hello 檔案名稱是區分大小寫。 |否 |
| 定義 |指定參數做為索引鍵/值組內使用 'hiveconf' hello Hive 指令碼參考 |否 |

這些類型的屬性是特定 toohello Hive 活動。 （外部 hello typeProperties 區段） 的其他屬性都支援所有活動。   

### <a name="json-example"></a>JSON 範例
下列 JSON hello 管線中定義 HDInsight Hive 活動。  

```json
{
    "name": "Hive Activity",
    "description": "description",
    "type": "HDInsightHive",
    "inputs": [
      {
        "name": "input tables"
      }
    ],
    "outputs": [
      {
        "name": "output tables"
      }
    ],
    "linkedServiceName": "MyHDInsightLinkedService",
    "typeProperties": {
      "script": "Hive script",
      "scriptPath": "<pathtotheHivescriptfileinAzureblobstorage>",
      "defines": {
        "param1": "param1Value"
      }
    },
   "scheduler": {
      "frequency": "Day",
      "interval": 1
    }
}
```

如需詳細資訊，請參閱 [Hive 活動](data-factory-hive-activity.md)文件。 

## <a name="hdinsight-pig-activity"></a>HDInsight Pig 活動
您可以指定下列屬性 Pig 活動 JSON 定義中的 hello。 hello hello 活動的型別屬性必須是： **HDInsightPig**。 您必須先建立 HDInsight 連結服務，並指定它 hello 名稱做為 hello 值**linkedServiceName**屬性。 hello 支援下列屬性在 hello **typeProperties**區段，當您設定活動 tooHDInsightPig hello 類型： 

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| script |指定 hello Pig 指令碼內嵌 |否 |
| 指令碼路徑 |在 Azure blob 儲存體中儲存 hello Pig 指令碼，並提供 hello 路徑 toohello 檔案。 使用 'script' 或 'scriptPath' 屬性。 兩者無法同時使用。 hello 檔案名稱是區分大小寫。 |否 |
| 定義 |指定參數做為索引鍵/值組內 hello Pig 指令碼參考 |否 |

這些類型的屬性是特定 toohello Pig 活動。 （外部 hello typeProperties 區段） 的其他屬性都支援所有活動。   

### <a name="json-example"></a>JSON 範例

```json
{
    "name": "HiveActivitySamplePipeline",
      "properties": {
    "activities": [
        {
            "name": "Pig Activity",
            "description": "description",
            "type": "HDInsightPig",
            "inputs": [
                  {
                    "name": "input tables"
                  }
            ],
            "outputs": [
                  {
                    "name": "output tables"
                  }
            ],
            "linkedServiceName": "MyHDInsightLinkedService",
            "typeProperties": {
                  "script": "Pig script",
                  "scriptPath": "<pathtothePigscriptfileinAzureblobstorage>",
                  "defines": {
                    "param1": "param1Value"
                  }
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
    ]
  }
}
```

如需詳細資訊，請參閱 [Pig 活動](#data-factory-pig-activity.md)文件。 

## <a name="hdinsight-mapreduce-activity"></a>HDInsight MapReduce 活動
您可以指定下列屬性 MapReduce 活動 JSON 定義中的 hello。 hello hello 活動的型別屬性必須是： **HDInsightMapReduce**。 您必須先建立 HDInsight 連結服務，並指定它 hello 名稱做為 hello 值**linkedServiceName**屬性。 hello 支援下列屬性在 hello **typeProperties**區段，當您設定活動 tooHDInsightMapReduce hello 類型： 

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| jarLinkedService | 連結 hello 包含 hello JAR 檔案的 Azure 儲存體服務的 hello 的名稱。 | 是 |
| jarFilePath | 在 hello Azure 儲存體 toohello JAR 檔案路徑。 | 是 | 
| className | Hello hello JAR 檔案中的主要類別的名稱。 | 是 | 
| arguments | Hello MapReduce 程式以逗號分隔的引數清單。 在執行階段，您會看到幾個額外的引數 (例如： mapreduce.job.tags) 從 hello MapReduce 架構。 toodifferentiate hello MapReduce 引數時，您的引數，請考慮使用選項和值做為引數中 hello 下列範例所示 (-s，-輸入、--輸出等，是後面緊跟著其值的選項) | 否 | 

### <a name="json-example"></a>JSON 範例

```json
{
    "name": "MahoutMapReduceSamplePipeline",
    "properties": {
        "description": "Sample Pipeline tooRun a Mahout Custom Map Reduce Jar. This job calculates an Item Similarity Matrix toodetermine hello similarity between two items",
        "activities": [
            {
                "type": "HDInsightMapReduce",
                "typeProperties": {
                    "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
                    "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
                    "jarLinkedService": "StorageLinkedService",
                    "arguments": ["-s", "SIMILARITY_LOGLIKELIHOOD", "--input", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/input", "--output", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/output/", "--maxSimilaritiesPerItem", "500", "--tempDir", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/temp/mahout"]
                },
                "inputs": [
                    {
                        "name": "MahoutInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "MahoutOutput"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "MahoutActivity",
                "description": "Custom Map Reduce toogenerate Mahout result",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00",
        "end": "2017-01-04T00:00:00"
    }
}
```

如需詳細資訊，請參閱 [MapReduce 活動](data-factory-map-reduce.md)文件。 

## <a name="hdinsight-streaming-activity"></a>HDInsight 串流活動
您可以指定下列屬性 Hadoop 串流活動 JSON 定義中的 hello。 hello hello 活動的型別屬性必須是： **HDInsightStreaming**。 您必須先建立 HDInsight 連結服務，並指定它 hello 名稱做為 hello 值**linkedServiceName**屬性。 hello 支援下列屬性在 hello **typeProperties**區段，當您設定活動 tooHDInsightStreaming hello 類型： 

| 屬性 | 說明 | 
| --- | --- |
| mapper | Hello 對應工具可執行檔的名稱。 在 hello 範例 cat.exe 會是 hello 對應工具可執行檔。| 
| reducer | Hello 減壓器可執行檔的名稱。 在 hello 範例 wc.exe 是 hello 減壓器可執行檔。 | 
| input | 輸入的檔 （包括位置） hello 對應工具。 在 hello 範例: 「 wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample 是 blob 容器，hello 範例/data/Gutenberg 是 hello 資料夾，而 davinci.txt 是 hello blob。 |
| output | 輸出檔 （包括位置） hello 減壓器。 hello hello Hadoop 串流工作輸出寫入 toohello 針對此屬性指定的位置。 |
| filePaths | Hello 對應工具和減壓器可執行檔的路徑。 在 hello 範例:"adfsample/example/apps/wc.exe"，adfsample 是 hello blob 容器，example/apps 是 hello 資料夾和 wc.exe 是可執行檔的 hello。 | 
| fileLinkedService | Azure 儲存體連結代表 hello hello hello filePaths 區段中指定的檔案所在的 Azure 儲存體服務。 | 
| arguments | Hello MapReduce 程式以逗號分隔的引數清單。 在執行階段，您會看到幾個額外的引數 (例如： mapreduce.job.tags) 從 hello MapReduce 架構。 toodifferentiate hello MapReduce 引數時，您的引數，請考慮使用選項和值做為引數中 hello 下列範例所示 (-s，-輸入、--輸出等，是後面緊跟著其值的選項) | 
| getDebugInfo | 選擇性元素。 當它設定為 tooFailure 時，只在失敗下載 hello 記錄檔。 當它設定為 tooAll 時，無論 hello 執行狀態永遠下載記錄檔。 | 

> [!NOTE]
> 您必須指定 hello Hadoop 資料流活動的輸出資料集**輸出**屬性。 此資料集可以是只的空資料集是必要的 toodrive hello 管線排程 （每小時、 每天、 等等）。 如果 hello 活動不接受輸入，您可以略過指定 hello 活動的輸入資料集**輸入**屬性。  

## <a name="json-example"></a>JSON 範例

```json
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": ["<nameofthecluster>/example/apps/wc.exe","<nameofthecluster>/example/apps/cat.exe"],
                    "fileLinkedService": "StorageLinkedService",
                    "getDebugInfo": "Failure"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-04T00:00:00",
        "end": "2014-01-05T00:00:00"
    }
}
```

如需詳細資訊，請參閱 [Hadoop 串流活動](data-factory-hadoop-streaming-activity.md)文件。 

## <a name="hdinsight-spark-activity"></a>HDInsight Spark 活動
您可以指定下列屬性的 Spark 活動 JSON 定義中的 hello。 hello hello 活動的型別屬性必須是： **HDInsightSpark**。 您必須先建立 HDInsight 連結服務，並指定它 hello 名稱做為 hello 值**linkedServiceName**屬性。 hello 支援下列屬性在 hello **typeProperties**區段，當您設定活動 tooHDInsightSpark hello 類型： 

| 屬性 | 說明 | 必要 |
| -------- | ----------- | -------- |
| rootPath | hello Azure Blob 容器，並包含 hello Spark 檔案的資料夾。 hello 檔案名稱是區分大小寫。 | 是 |
| entryFilePath | 相對路徑 toohello 的 hello Spark 程式碼/封裝的根資料夾。 | 是 |
| className | 應用程式的 Java/Spark 主要類別 | 否 | 
| arguments | 命令列引數 toohello Spark 程式的清單。 | 否 | 
| proxyUser | hello 使用者帳戶 tooimpersonate tooexecute hello Spark 程式 | 否 | 
| sparkConfig | Spark 組態屬性。 | 否 | 
| getDebugInfo | 指定當 hello Spark 記錄檔會複製的 toohello HDInsight 叢集所使用的 Azure 儲存體 （或） sparkJobLinkedService 所指定。 允許的值︰None、Always 或 Failure。 預設值：None。 | 否 | 
| sparkJobLinkedService | hello Azure 儲存體連結服務的 hello Spark 工作檔案、 相依性，以及記錄檔。  如果您未指定此屬性的值，則會使用 hello 與 HDInsight 叢集相關聯的儲存體。 | 否 |

### <a name="json-example"></a>JSON 範例

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-05T00:00:00",
        "end": "2017-02-06T00:00:00"
    }
}
```
請注意下列點 hello: 

- hello**類型**屬性設定太**HDInsightSpark**。
- hello **rootPath**設定得**adfspark\\pyFiles** adfspark 所在 hello Azure Blob 容器和 pyFiles 是正常的資料夾，該容器中。 在此範例中，hello Azure Blob 儲存體是 hello 與 hello Spark 叢集相關聯的其中一個。 您可以上傳 hello 檔案 tooa 不同的 Azure 儲存體。 如果您這樣做，請建立 Azure 儲存體連結服務 toolink 該儲存體帳戶 toohello 資料 factory。 然後，指定 hello hello 連結服務名稱做為 hello 值**sparkJobLinkedService**屬性。 請參閱[Spark 活動屬性](#spark-activity-properties)如需詳細資訊，這個屬性，而且支援 hello Spark 活動的其他內容。
- hello **entryFilePath**設定 toohello **test.py**，這是 hello python 檔案。 
- hello **getDebugInfo**屬性設定太**永遠**，這表示 hello 記錄檔一律會產生 （成功或失敗）。  

    > [!IMPORTANT]
    > 我們建議您沒有設定這個屬性 tooAlways 加在生產環境中，除非您疑難排解問題。 
- hello**輸出**區段具有一個輸出資料集。 您必須指定輸出資料集，即使 hello spark 程式不會產生任何輸出。 hello 輸出資料集的磁碟機 hello 排程 hello 管線 （每小時、 每天、 等等）。

如需 hello 活動的詳細資訊，請參閱[Spark 活動](data-factory-spark.md)發行項。  

## <a name="machine-learning-batch-execution-activity"></a>Machine Learning 批次執行活動
您可以指定下列屬性，Azure ML 批次執行活動 JSON 定義中的 hello。 hello hello 活動的型別屬性必須是： **AzureMLBatchExecution**。 您必須建立 Azure 機器學習連結的服務第一次，並指定做為 hello 值的 hello 目的**linkedServiceName**屬性。 hello 支援下列屬性在 hello **typeProperties**區段，當您設定活動 tooAzureMLBatchExecution hello 類型：

屬性 | 說明 | 必要 
-------- | ----------- | --------
webServiceInput | hello 資料集 toobe 傳遞做為輸入 hello Azure ML web 服務。 此資料集也必須包含 hello 輸入 hello 活動中。 |使用 webServiceInput 或 webServiceInputs。 | 
webServiceInputs | 指定資料集 toobe 傳遞做為輸入 hello Azure ML web 服務。 如果 hello web 服務接受多個輸入，使用 hello webServiceInputs 屬性而不是使用 hello webServiceInput 屬性。 資料集所參考的 hello **webServiceInputs**也必須包含在 hello 活動**輸入**。 | 使用 webServiceInput 或 webServiceInputs。 | 
webServiceOutputs | 已被指派為輸出 hello Azure ML web 服務的 hello 資料集。 hello web 服務傳回此資料集的輸出資料。 | 是 | 
globalParameters | 在此區段指定 hello web 服務參數的值。 | 否 | 

### <a name="json-example"></a>JSON 範例
在此範例中，hello 活動具有 hello 資料集**MLSqlInput**做為輸入和**MLSqlOutput**做為 hello 輸出。 hello **MLSqlInput**被當做輸入的 toohello web 服務，方法是使用 hello **webServiceInput** JSON 屬性。 hello **MLSqlOutput**被當做輸出 toohello Web 服務，方法是使用 hello **webServiceOutputs** JSON 屬性。 

```json
{
   "name": "MLWithSqlReaderSqlWriter",
   "properties": {
      "description": "Azure ML model with sql azure reader/writer",
      "activities": [{
         "name": "MLSqlReaderSqlWriterActivity",
         "type": "AzureMLBatchExecution",
         "description": "test",
         "inputs": [ { "name": "MLSqlInput" }],
         "outputs": [ { "name": "MLSqlOutput" } ],
         "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
         "typeProperties":
         {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
               "output1": "MLSqlOutput"
            },
            "globalParameters": {
               "Database server name": "<myserver>.database.windows.net",
               "Database name": "<database>",
               "Server user account name": "<user name>",
               "Server user account password": "<password>"
            }              
         },
         "policy": {
            "concurrency": 1,
            "executionPriorityOrder": "NewestFirst",
            "retry": 1,
            "timeout": "02:00:00"
         }
      }],
      "start": "2016-02-13T00:00:00",
       "end": "2016-02-14T00:00:00"
   }
}
```

在 hello JSON 範例中，hello 部署 Azure 機器學習 Web 服務會使用讀取器和寫入器模組 tooread/寫入資料，從 / tooan Azure SQL Database。 此 Web 服務會公開下列四個參數的 hello： 資料庫伺服器名稱、 資料庫名稱、 伺服器使用者帳戶名稱，以及伺服器的使用者帳戶密碼。

> [!NOTE]
> 只有輸入及輸出的 hello AzureMLBatchExecution 活動可以傳遞為參數 toohello Web 服務。 例如，在 JSON 片段上方 hello，MLSqlInput 是輸入的 toohello AzureMLBatchExecution 活動，以透過 webServiceInput 參數當做輸入的 toohello Web 服務。

## <a name="machine-learning-update-resource-activity"></a>Machine Learning 更新資源活動
您可以指定下列屬性，Azure ML 更新資源活動 JSON 定義中的 hello。 hello hello 活動的型別屬性必須是： **AzureMLUpdateResource**。 您必須建立 Azure 機器學習連結的服務第一次，並指定做為 hello 值的 hello 目的**linkedServiceName**屬性。 hello 支援下列屬性在 hello **typeProperties**區段，當您設定活動 tooAzureMLUpdateResource hello 類型：

屬性 | 說明 | 必要 
-------- | ----------- | --------
trainedModelName | Hello 的名稱重新定型模型。 | 是 |  
trainedModelDatasetName | 資料集指標的 toohello ilearner 做為檔案，hello 定型作業所傳回。 | 是 | 

### <a name="json-example"></a>JSON 範例
hello 管線有兩個活動： **AzureMLBatchExecution**和**AzureMLUpdateResource**。 hello Azure ML 批次執行的活動會接受做為輸入的 hello 定型資料，並產生 ilearner 做為檔案，做為輸出。 hello 活動與 hello 輸入培訓資料叫用 hello 訓練 web 服務 （定型實驗公開為 web 服務），並從 hello webservice 接收 hello ilearner 做為檔。 hello placeholderBlob 是所需的 hello Azure Data Factory 服務 toorun hello 管線只要 dummy 輸出資料集。


```json
{
    "name": "pipeline",
    "properties": {
        "activities": [
            {
                "name": "retraining",
                "type": "AzureMLBatchExecution",
                "inputs": [
                    {
                        "name": "trainingData"
                    }
                ],
                "outputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "typeProperties": {
                    "webServiceInput": "trainingData",
                    "webServiceOutputs": {
                        "output1": "trainedModelBlob"
                    }              
                 },
                "linkedServiceName": "trainingEndpoint",
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            },
            {
                "type": "AzureMLUpdateResource",
                "typeProperties": {
                    "trainedModelName": "trained model",
                    "trainedModelDatasetName" :  "trainedModelBlob"
                },
                "inputs": [{ "name": "trainedModelBlob" }],
                "outputs": [{ "name": "placeholderBlob" }],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "AzureML Update Resource",
                "linkedServiceName": "updatableScoringEndpoint2"
            }
        ],
        "start": "2016-02-13T00:00:00",
        "end": "2016-02-14T00:00:00"
    }
}
```

## <a name="data-lake-analytics-u-sql-activity"></a>Data Lake Analytics U-SQL 活動
您可以指定下列屬性 U-SQL 活動 JSON 定義中的 hello。 hello hello 活動的型別屬性必須是： **DataLakeAnalyticsU SQL**。 您必須建立連結的 Azure 資料湖分析服務，並指定它 hello 名稱做為 hello 值**linkedServiceName**屬性。 hello 支援下列屬性在 hello **typeProperties**區段，當您設定活動 tooDataLakeAnalyticsU SQL hello 類型： 

| 屬性 | 說明 | 必要 |
|:--- |:--- |:--- |
| scriptPath |路徑 toofolder 包含 hello U-SQL 指令碼。 Hello 檔案的名稱會區分大小寫。 |否 (如果您使用指令碼) |
| scriptLinkedService |連結包含 hello 指令碼 toohello 資料 factory 的 hello 儲存體連結的服務 |否 (如果您使用指令碼) |
| script |指定內嵌指令碼而不是指定 scriptPath 和 scriptLinkedService。 例如："script": "CREATE DATABASE test"。 |否 (如果您使用 scriptPath 和 scriptLinkedService) |
| degreeOfParallelism |hello 的節點數目上限，同時使用 toorun hello 作業。 |否 |
| 優先順序 |決定從所有已排入佇列的作業應該選取的 toorun 第一次。 hello 低 hello 數字，hello hello 優先順序越高。 |否 |
| 參數 |Hello U-SQL 指令碼的參數 |否 |

### <a name="json-example"></a>JSON 範例

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This pipeline computes events for en-gb locale and date less than Feb 19, 2012.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00",
        "end": "2015-08-08T01:00:00",
        "isPaused": false
    }
}
```

如需詳細資訊，請參閱 [Data Lake Analytics U-SQL 活動](data-factory-usql-activity.md)。 

## <a name="stored-procedure-activity"></a>預存程序活動
您可以指定下列屬性的預存程序活動 JSON 定義中的 hello。 hello hello 活動的型別屬性必須是： **SqlServerStoredProcedure**。 您必須建立一個 hello 遵循連結的服務，並指定 hello hello 連結服務名稱做為 hello 值**linkedServiceName**屬性：

- SQL Server 
- Azure SQL Database
- Azure SQL 資料倉儲

hello 支援下列屬性在 hello **typeProperties**區段，當您設定活動 tooSqlServerStoredProcedure hello 類型：

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| storedProcedureName |指定 hello Azure SQL database 或 Azure SQL 資料倉儲由 hello 輸出資料表中使用的 hello 連結服務中的 hello hello 預存程序名稱。 |是 |
| storedProcedureParameters |指定預存程序參數的值。 如果您需要 toopass null 參數，使用 hello 語法:"param1": null （所有大小寫）。 請參閱下列有關使用這個屬性的範例 toolearn hello。 |否 |

如果您指定的輸入資料集，它必須可用 （處於 [就緒]' 的狀態） hello 預存程序活動 toorun。 hello 輸入資料集無法取用 hello 預存程序中，做為參數。 起始 hello 預存程序活動之前，它是只使用的 toocheck hello 相依性。 您必須指定預存程序活動的輸出資料集。 

輸出資料集指定 hello**排程**hello 預存程序活動 （每小時、 每週、 每月等）。 hello 輸出資料集必須使用**連結服務**參考 tooan Azure SQL Database 或 Azure SQL 資料倉儲或您想在其中 hello toorun 預存程序的 SQL Server 資料庫。 hello 輸出資料集可以做為方法 toopass hello hello 預存程序的結果進行後續處理另一個活動 ([鏈結活動](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) hello 管線中。 不過，Data Factory 不會自動寫入預存程序 toothis 資料集的 hello 輸出。 它是 hello 預存程序 hello 輸出資料集指向該寫入 tooa SQL 資料表。 在某些情況下，可以是 hello 輸出資料集**空資料集**，用僅執行 hello toospecify hello 排程預存程序活動。  

### <a name="json-example"></a>JSON 範例

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                    }
                },
                "outputs": [{ "name": "sprocsampleout" }],
                "name": "SprocActivitySample"
            }
        ],
         "start": "2016-08-02T00:00:00",
         "end": "2016-08-02T05:00:00",
        "isPaused": false
    }
}
```

如需詳細資訊，請參閱[預存程序活動](data-factory-stored-proc-activity.md)。 

## <a name="net-custom-activity"></a>.NET 自訂活動
您可以指定下列屬性.NET 自訂活動 JSON 定義中的 hello。 hello hello 活動的型別屬性必須是： **DotNetActivity**。 您必須建立 Azure HDInsight 連結服務或 Azure 批次連結服務，並指定 hello hello 連結服務名稱做為 hello 值**linkedServiceName**屬性。 hello 支援下列屬性在 hello **typeProperties**區段，當您設定活動 tooDotNetActivity hello 類型：
 
| 屬性 | 說明 | 必要 |
|:--- |:--- |:--- |
| AssemblyName | Hello 組件名稱。 在 hello 範例很： **MyDotnetActivity.dll**。 | 是 |
| EntryPoint |Hello 類別可實作 hello IDotNetActivity 介面的名稱。 在 hello 範例很： **MyDotNetActivityNS.MyDotNetActivity**其中 MyDotNetActivityNS 是 hello 命名空間且 MyDotNetActivity hello 類別。  | 是 | 
| PackageLinkedService | Hello 點 toohello blob 儲存體包含 hello 自訂活動的 zip 檔案的 Azure 儲存體連結服務的名稱。 在 hello 範例很： **AzureStorageLinkedService**。| 是 |
| PackageFile | Hello zip 檔案的名稱。 在 hello 範例很： **customactivitycontainer/MyDotNetActivity.zip**。 | 是 |
| extendedProperties | 您可以定義及傳遞 toohello.NET 程式碼的擴充的屬性。 在此範例中，hello **SliceStart**變數設定為 tooa 根據 hello SliceStart 系統變數的值。 | 否 | 

### <a name="json-example"></a>JSON 範例

```json
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "AzureBatchLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00",
    "end": "2016-11-16T05:00:00",
    "isPaused": false
  }
}
```

如需詳細資訊，請參閱[在 Data Factory 中使用自訂活動](data-factory-use-custom-activities.md)文件。 

## <a name="next-steps"></a>後續步驟
請參閱下列教學課程的 hello: 

- [教學課程：建立具有複製活動的管線](data-factory-copy-activity-tutorial-using-azure-portal.md)
- [教學課程：建立具有 Hive 活動的管線](data-factory-build-your-first-pipeline-using-editor.md)