---
title: "aaaCreate/排程管線、 Data Factory 中的鏈結活動 |Microsoft 文件"
description: "了解在資料管線，在 Azure Data Factory toomove toocreate 和轉換資料。 建立資料驅動型工作流程 tooproduce 準備 toouse 資訊。"
keywords: "資料管線, 資料導向工作流程"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 13b137c7-1033-406f-aea7-b66f25b313c0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/12/2017
ms.author: shlo
ms.openlocfilehash: 4a0fc20f98ce6453c16955e97fddb891926c173a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="pipelines-and-activities-in-azure-data-factory"></a>Azure Data Factory 中的管線及活動
這篇文章可協助您了解管線和 Azure Data Factory 中的活動，並針對您的資料移動和資料處理的案例中使用 tooconstruct 端對端資料驅動型工作流程。  

> [!NOTE]
> 本文假設您已經完成[簡介 tooAzure Data Factory](data-factory-introduction.md)。 如果您沒有建立 Data Factory 的實作經驗，瀏覽[資料轉換教學課程](data-factory-build-your-first-pipeline.md)和/或[資料移動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)將可協助您進一步了解這篇文章。  

## <a name="overview"></a>概觀
資料處理站可以有一或多個管線。 管線是一起執行某個工作的活動所組成的邏輯群組。 在管線中的 hello 活動定義動作 tooperform 對您的資料。 例如，您可能會使用複製活動 toocopy 資料從內部部署 SQL Server tooan Azure Blob 儲存體。 然後，使用 Azure HDInsight 叢集 tooprocess/轉換資料執行 Hive 指令碼，從 hello blob 儲存體 tooproduce 輸出資料的 Hive 活動。 最後，使用第二個複製活動 toocopy hello 輸出資料 tooan Azure SQL 資料倉儲內建報表方案的商業智慧 (BI) 之上。 

一個活動可以接受零個或多個輸入[資料集](data-factory-create-datasets.md)，並且會產生一個或多個輸出[資料集](data-factory-create-datasets.md)。 hello 下圖顯示 hello 管線、 活動和資料集之間的關聯性 Data Factory 中： 

![管線、活動及資料集之間的關聯性](media/data-factory-create-pipelines/relationship-pipeline-activity-dataset.png)

管線可讓您 toomanage 活動為一組，而不是每個個別。 比方說，您可以部署、 排程、 暫停和繼續管線，而不是分別處理 hello 管線中的活動。

Data Factory 支援兩種活動類型︰資料移動活動和資料轉換活動。 每個活動可以有零個或多個輸入[資料集](data-factory-create-datasets.md)，並且會產生一個或多個輸出資料集。

輸入資料集代表 hello hello 管線中活動的輸入和輸出資料集代表 hello hello 活動的輸出。 資料集可識別資料表、檔案、資料夾和文件等各種資料存放區中的資料。 建立資料集之後，您可以將其與管線中的活動搭配使用。 例如，資料集可以是複製活動或 HDInsightHive 活動的輸入/輸出資料集。 如需有關資料集的詳細資訊，請參閱 [Azure Data Factory 中的資料集](data-factory-create-datasets.md)一文。

### <a name="data-movement-activities"></a>資料移動活動
Data Factory 中的複製活動會將資料從來源資料存放區 tooa 接收資料存放區。 Data Factory 支援下列資料存放區的 hello。 從任何來源的資料可以寫入 tooany 接收。 按一下 [資料存放區 toolearn 如何 toocopy 資料 tooand 從該存放區。

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> 資料存放區使用 * 可在內部部署或 Azure IaaS 上，因此需要您 tooinstall[資料管理閘道器](data-factory-data-management-gateway.md)在內部部署/Azure IaaS 電腦上。

如需詳細資訊，請參閱[資料移動活動](data-factory-data-movement-activities.md)文章。

### <a name="data-transformation-activities"></a>資料轉換活動
[!INCLUDE [data-factory-transformation-activities](../../includes/data-factory-transformation-activities.md)]

如需詳細資訊，請參閱[資料轉換活動](data-factory-data-transformation-activities.md)文章。

### <a name="custom-net-activities"></a>自訂 .NET 活動 
如果您需要 toomove 資料/從資料存放區 hello 複製活動的不支援，或使用您自己的邏輯轉換資料、 建立**自訂.NET 活動**。 如需有關建立及使用自訂活動的詳細資料，請參閱 [在 Azure Data Factory 管線中使用自訂活動](data-factory-use-custom-activities.md)。

## <a name="schedule-pipelines"></a>建立管線排程
管線僅在其「開始」時間與「結束」時間之間有作用。 它不會執行 hello 開始時間之前或之後 hello 結束時間。 如果 hello 管線已暫停，它不會執行而不受限於其開始和結束時間。 為管線 toorun，它應該暫停。 請參閱[排程與執行](data-factory-scheduling-and-execution.md)toounderstand 排程和執行 Azure Data Factory 中運作的方式。

## <a name="pipeline-json"></a>管線 JSON
讓我們來深入探討如何定義 JSON 格式的管線。 管線的 hello 泛型結構如下所示：

```json
{
    "name": "PipelineName",
    "properties": 
    {
        "description" : "pipeline description",
        "activities":
        [

        ],
        "start": "<start date-time>",
        "end": "<end date-time>",
        "isPaused": true/false,
        "pipelineMode": "scheduled/onetime",
        "expirationTime": "15.00:00:00",
        "datasets": 
        [
        ]
    }
}
```

| Tag | 說明 | 必要 |
| --- | --- | --- |
| 名稱 |Hello 管線的名稱。 指定代表 hello 管線的 hello 動作的名稱執行。 <br/><ul><li>字元數目上限︰260</li><li>開頭必須為字母、數字或底線 (_)</li><li>不允許使用下列字元：“.”、“+”、“?”、“/”、“<”、”>”、”*”、”%”、”&”、”:”、”\\”</li></ul> |是 |
| 說明 | 指定描述用於何種 hello 管線的 hello 文字。 |是 |
| 活動 | hello**活動**區段都可以擁有定義於其中的一個或多個活動。 請參閱 hello hello 活動 JSON 項目的詳細資料的下一節。 | 是 |  
| start | 開始日期-時間 hello 管線。 必須使用 [ISO 格式](http://en.wikipedia.org/wiki/ISO_8601)。 例如： `2016-10-14T16:32:41Z`。 <br/><br/>很可能 toospecify 本地時間，例如預估時間。 範例如下︰`2016-02-27T06:00:00-05:00`，這是美加東部標準時間上午 6 點。<br/><br/>hello 開始和結束屬性一起指定 hello 管線的作用期間。 輸出配量只會在作用中期間內產生。 |否<br/><br/>如果您指定 hello 結束屬性的值，您必須指定 hello 開始屬性值。<br/><br/>hello 開始和結束時間可以是空的 toocreate 管線。 您必須指定這兩個值的作用中期間 hello 管線 toorun tooset。 如果您未指定開始和結束時間時建立管線，您可以設定它們使用 hello 組 AzureRmDataFactoryPipelineActivePeriod 指令程式更新版本。 |
| end | 結束日期與時間 hello 管線。 如果已指定，則必須使用 ISO 格式。 例如：`2016-10-14T17:32:41Z` <br/><br/>很可能 toospecify 本地時間，例如預估時間。 範例如下︰`2016-02-27T06:00:00-05:00`，這是 6 AM EST。<br/><br/>toorun hello 管線無限期地指定 9999-09-09 hello hello end 屬性的值。 <br/><br/> 管線僅在其開始時間與結束時間之間有作用。 它不會執行 hello 開始時間之前或之後 hello 結束時間。 如果 hello 管線已暫停，它不會執行而不受限於其開始和結束時間。 為管線 toorun，它應該暫停。 請參閱[排程與執行](data-factory-scheduling-and-execution.md)toounderstand 排程和執行 Azure Data Factory 中運作的方式。 |否 <br/><br/>如果您指定 hello 開始屬性的值，您必須指定 hello end 屬性的值。<br/><br/>請參閱備註 hello**啟動**屬性。 |
| isPaused | 如果組 tootrue，hello 管線不會執行。 它已經在 hello 暫停狀態。 預設值 = false。 您可以使用這個屬性 tooenable 或停用管線。 |否 |
| pipelineMode | hello 管線的可執行的排程 hello 方法。 允許的值包括：scheduled (預設值)、onetime。<br/><br/>排程' 表示該 hello 管線 tooits 作用期間 （開始和結束時間），根據指定的時間間隔執行。 '一次' 表示該 hello 管線只執行一次。 目前，Onetime 管線在建立之後即無法進行修改/更新。 如需 onetime 設定的詳細資料，請參閱 [Onetime 管線](#onetime-pipeline)。 |否 |
| expirationTime | 持續時間在建立後的 hello[單次管線](#onetime-pipeline)有效，且應保持已佈建。 如果它沒有任何作用中、 失敗，或執行時，擱置 hello 管線就會自動刪除一次到達 hello 到期時間。 hello 預設值：`"expirationTime": "3.00:00:00"`|否 |
| 資料集 |資料集 toobe hello 管線中定義的活動所使用的清單。 這個屬性可以是使用的 toodefine 特定 toothis 管線，而且未在 hello 資料 factory 中定義的資料集。 此管線內定義的資料集只有此管線才能使用，並無法共用。 如需詳細資訊，請參閱 [範圍資料集](data-factory-create-datasets.md#scoped-datasets) 。 |否 |

## <a name="activity-json"></a>活動 JSON
hello**活動**區段都可以擁有定義於其中的一個或多個活動。 每個活動有下列最上層結構 hello:

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
    },
    "scheduler":
    {
    }
}
```

下表描述屬性在 hello 活動 JSON 定義中：

| Tag | 說明 | 必要 |
| --- | --- | --- |
| 名稱 | Hello 活動名稱。 指定代表 hello hello 活動都會執行的動作的名稱。 <br/><ul><li>字元數目上限︰260</li><li>開頭必須為字母、數字或底線 (_)</li><li>不允許使用下列字元：“.”、“+”、“?”、“/”、“<”、”>”、”*”、”%”、”&”、”:”、”\\”</li></ul> |是 |
| 說明 | 描述什麼 hello 活動，或用於文字 |是 |
| 類型 | Hello 活動的型別。 請參閱 hello[資料移動活動](#data-movement-activities)和[資料轉換活動](#data-transformation-activities)區段的不同類型的活動。 |是 |
| 輸入 |Hello 活動所使用的輸入的資料表<br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |是 |
| 輸出 |使用的 hello 活動的輸出的資料表。<br/><br/>`// one output table`<br/>`"outputs":  [ { "name": "outputtable1" } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": "outputtable1" }, { "name": "outputtable2" }  ],` |是 |
| linkedServiceName |Hello 活動所使用的 hello 連結服務名稱。 <br/><br/>活動可能會要求您指定連結 toohello 必要的運算環境的 hello 連結服務。 |是：適用於 HDInsight 活動和 Azure Machine Learning Batch 評分活動  <br/><br/>否：所有其他 |
| typeProperties |屬性在 hello **typeProperties**區段取決於 hello 活動的類型。 toosee 類型屬性的活動中，按一下 hello 前一節中的連結 toohello 活動。 | 否 |
| 原則 |影響 hello hello 活動執行階段行為的原則。 如果未指定，則會使用預設原則。 |否 |
| scheduler | 「 排程器 」 屬性是使用的 toodefine 預期 hello 活動的排程。 及其子屬性會 hello 與 hello hello 於相同[可用性屬性集中](data-factory-create-datasets.md#dataset-availability)。 |否 |


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

## <a name="sample-copy-pipeline"></a>範例複製管線
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
    "start": "2016-07-12T00:00:00Z",
    "end": "2016-07-13T00:00:00Z"
  }
} 
```

請注意下列點 hello:

* 在 [hello 活動] 區段中，沒有一個活動其**類型**設定得**複製**。
* 輸入 hello 活動設定太**InputDataset**和輸出 hello 活動設定太**OutputDataset**。 若要了解如何以 JSON 定義資料集，請參閱[資料集](data-factory-create-datasets.md)一文。 
* 在 [hello **typeProperties** ] 區段中， **BlobSource**指定 hello 來源類型為和**SqlSink**指定為 hello 接收器類型。 在 [hello[資料移動活動](#data-movement-activities)區段中，按一下的 hello 資料存放區，您要 toouse 做為來源或接收器 toolearn 了解從該資料存放區移動資料。 

建立此管線的完整逐步解說，請參閱[教學課程： 將資料從 Blob 儲存體 tooSQL 資料庫複製](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。 

## <a name="sample-transformation-pipeline"></a>範例轉換管線
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
        "start": "2016-04-01T00:00:00Z",
        "end": "2016-04-02T00:00:00Z",
        "isPaused": false
    }
}
```

請注意下列點 hello: 

* 在 [hello 活動] 區段中，沒有一個活動其**類型**設定得**HDInsightHive**。
* hello Hive 指令碼檔案， **partitionweblogs.hql**，儲存在 hello Azure 儲存體帳戶 (由 hello scriptLinkedService，稱為**AzureStorageLinkedService**)，然後在**指令碼**hello 容器中的資料夾**adfgetstarted**。
* hello`defines`區段是做為 Hive 組態值傳遞 toohello hive 指令碼使用的 toospecify hello 執行階段設定 (例如`${hiveconf:inputtable}`， `${hiveconf:partitionedtable}`)。

hello **typeProperties**區段是不同的每個轉換活動。 轉換活動，支援的型別屬性的相關 toolearn 按一下 hello hello 轉換活動[資料轉換活動](#data-transformation-activities)資料表。 

建立此管線的完整逐步解說，請參閱[教學課程： 建立第一個管線 tooprocess 資料使用 Hadoop 叢集](data-factory-build-your-first-pipeline.md)。 

## <a name="multiple-activities-in-a-pipeline"></a>管線中的多個活動
hello 先前兩個範例管線有一個活動。 您可以在一個管線中包含多個活動。  

如果您在管線中有多個活動和活動的輸出不是另一個活動的輸入，hello 活動可能會以平行方式執行，hello 活動的輸入的資料配量是否準備。 

您可以將鏈結兩個活動擁有 hello 輸出資料集，一個活動與 hello hello 的輸入資料集的其他活動。 hello 第二個活動執行只 hello 第一次一個成功完成。

![鏈結中 hello 活動相同管線](./media/data-factory-create-pipelines/chaining-one-pipeline.png)

在此範例中，hello 管線有兩個活動： Activity1 和 Activity2。 hello Activity1 接受做為輸入 Dataset1，然後產生輸出 Dataset2。 hello 活動會採用做為輸入 Dataset2，並產生輸出 Dataset3。 因為 Activity1 hello 輸出 (Dataset2) Activity2 hello 輸入，hello Activity2 hello 活動順利完成之後，才會執行，並產生 hello Dataset2 配量。 如果 hello Activity1 因故失敗，而且不會產生 hello Dataset2 配量，hello 活動 2 不會執行該配量 (例如： 9 AM too10 AM)。 

您可以將不同管線中的活動建立鏈結。

![兩個管線中的鏈結活動](./media/data-factory-create-pipelines/chaining-two-pipelines.png)

在此範例中，Pipeline1 只有一個活動，此活動是以 Dataset1 作為輸入，並產生 Dataset2 作為輸出。 hello Pipeline2 也有一個採用 Dataset2 和當做輸入 Dataset3 做為輸出的活動。 

如需詳細資訊，請參閱 [排程和執行](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)。 

## <a name="create-and-monitor-pipelines"></a>建立和監視管線
您可以使用下列其中一項工具或 SDK 來建立管線。 

- 複製精靈 
- Azure 入口網站
- Visual Studio
- Azure PowerShell
- Azure Resource Manager 範本
- REST API
- .NET API

請參閱下列逐步教學課程使用其中一個工具或 Sdk 建立管線的 hello。
 
- [使用資料轉換活動來建置管線](data-factory-build-your-first-pipeline.md)
- [使用資料移動活動來建置管線](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

一旦建立/部署管線，您可以管理和監視您所使用的管線 hello Azure 入口網站的刀鋒視窗或監視和管理應用程式。 請參閱下列主題逐步指示的 hello。 

- [使用 Azure 入口網站刀鋒視窗來監視和管理管線](data-factory-monitor-manage-pipelines.md)
- [使用監視與管理應用程式來監視和管理管線](data-factory-monitor-manage-app.md)


## <a name="onetime-pipeline"></a>Onetime 管線
您可以建立和定期排程管線 toorun (例如： 每小時或每天) 內 hello 開始與結束 hello 管線定義中指定的時間。 如需詳細資訊，請參閱 [排程活動](#scheduling-and-execution) 。 您也可以建立只執行一次的管線。 toodo 所以，您可以設定 hello **pipelineMode** hello 中的屬性太管線定義**一次**hello 下列 JSON 範例所示。 hello 這個屬性的預設值是**排程**。

```json
{
    "name": "CopyPipeline",
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
                        "name": "InputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ]
                "name": "CopyActivity-0"
            }
        ]
        "pipelineMode": "OneTime"
    }
}
```

請注意 hello 下列：

* **啟動**和**結束**hello 管線的時間都不指定。
* **可用性**資料集為指定的輸入和輸出 (**頻率**和**間隔**)，即使 Data Factory 不會使用 hello 值。  
* 圖表檢視不會顯示一次性管線。 這是設計的行為。
* 一次性管線無法更新。 您可以複製單次管線，將它重新命名、 更新屬性，並部署 toocreate 另一個。


## <a name="next-steps"></a>後續步驟
- 如需有關資料集的詳細資訊，請參閱[建立資料集](data-factory-create-datasets.md)一文。 
- 如需有關管線的排程和執行方式的詳細資訊，請參閱 [Azure Data Factory 中的排程和執行](data-factory-scheduling-and-execution.md)一文。 
  

