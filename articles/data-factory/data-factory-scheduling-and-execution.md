---
title: "aaaScheduling 使用 Data Factory 及執行 |Microsoft 文件"
description: "了解 Azure Data Factory 應用程式模型的排程和執行層面。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 088a83df-4d1b-4ac1-afb3-0787a9bd1ca5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 6114dd4896f5537c789c3b632fb90e501b694285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="data-factory-scheduling-and-execution"></a>Data Factory 排程和執行
本文說明 hello 排程和執行層面 hello Azure Data Factory 應用程式模型。 本文假設您已了解 Data Factory 應用程式模型的基本概念，包括活動、管線、連結的服務和資料集。 Azure Data Factory 的基本概念，請參閱下列文章 hello:

* [簡介 tooData Factory](data-factory-introduction.md)
* [管線](data-factory-create-pipelines.md)
* [資料集](data-factory-create-datasets.md) 

## <a name="start-and-end-times-of-pipeline"></a>管線的開始和結束時間
管線僅在其「開始」時間與「結束」時間之間有作用。 它不會執行 hello 開始時間之前或之後 hello 結束時間。 如果 hello 管線已暫停，它不會執行而不受限於其開始和結束時間。 為管線 toorun，它應該暫停。 您可以找到這些設定 （開始、 結束時，暫停） hello 管線定義中： 

```json
"start": "2017-04-01T08:00:00Z",
"end": "2017-04-01T11:00:00Z"
"isPaused": false
```

如需有關這些屬性的詳細資訊，請參閱[建立管線](data-factory-create-pipelines.md)一文。 


## <a name="specify-schedule-for-an-activity"></a>為活動指定排程
不執行 hello 管線。 它是在 hello 管線中的 hello 活動 hello 中執行的整體 hello 管線的內容。 您可以指定活動的週期性排程使用 hello**排程器**活動 JSON 的區段。 例如，您可以排定活動 toorun 每小時，如下所示：  

```json
"scheduler": {
    "frequency": "Hour",
    "interval": 1
},
```

Hello 下列圖表所示，指定活動的排程建立一系列的輪轉視窗具有在 hello 管線開始和結束時間。 輪轉時段是一系列大小固定、非重疊的連續時間間隔。 活動的這些邏輯輪轉時段稱為「活動時段」。

![活動排程器範例](media/data-factory-scheduling-and-execution/scheduler-example.png)

hello**排程器**是選擇性的活動的屬性。 如果您指定這個屬性，它必須符合您指定 hello hello 活動的輸出資料集定義中的 hello 步調。 目前，輸出資料集是哪些磁碟機 hello 排程。 因此，您必須建立輸出資料集，即使 hello 活動不會產生任何輸出。 

## <a name="specify-schedule-for-a-dataset"></a>為資料集指定排程
Data Factory 管線中的一個活動可以接受零個或多個輸入「資料集」，並且會產生一個或多個輸出資料集。 活動，您可以指定哪些 hello 輸入的資料在 hello 韻律或 hello 輸出資料以 hello 產生**可用性**hello 資料集定義中的區段。 

**頻率**在 hello**可用性**區段會指定 hello 時間單位。 hello 允許的頻率的值為： 分鐘、 小時、 天、 週和月份。 hello**間隔**hello 可用性一節中的屬性會指定頻率的倍數。 例如： 如果已設定 tooDay hello 頻率間隔設定輸出資料集的 too1，每天產生 hello 輸出資料。 如果您將 hello frequency 指定為 minute，我們建議您設定小於 15 的 hello 間隔 toono。 

在下列範例的 hello，hello 輸入的資料隨附每小時，則會每小時產生 hello 輸出資料 (`"frequency": "Hour", "interval": 1`)。 

**輸入資料集：** 

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
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


**輸出資料集**

```json
{
    "name": "AzureBlobOutput",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mypath/{Year}/{Month}/{Day}/{Hour}",
            "format": {
                "type": "TextFormat"
            },
            "partitionedBy": [
                { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
                { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" }}
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

目前，**輸出資料集的磁碟機 hello 排程**。 換句話說，hello hello 輸出資料集為指定的排程是使用的 toorun 活動執行階段。 因此，您必須建立輸出資料集，即使 hello 活動不會產生任何輸出。 如果 hello 活動不接受任何輸入，您可以略過建立 hello 輸入資料集。 

在 hello 下列管線定義，hello**排程器**屬性是使用的 toospecify hello 活動排程。 這是選用屬性。 目前，hello 排程 hello 活動必須符合 hello hello 輸出資料集為指定的排程。
 
```json
{
    "name": "SamplePipeline",
    "properties": {
        "description": "copy activity",
        "activities": [
            {
                "type": "Copy",
                "name": "AzureSQLtoBlob",
                "description": "copy activity",
                "typeProperties": {
                    "source": {
                        "type": "SqlSource",
                        "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 100000,
                        "writeBatchTimeout": "00:05:00"
                    }
                },
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
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                }
            }
        ],
        "start": "2017-04-01T08:00:00Z",
        "end": "2017-04-01T11:00:00Z"
    }
}
```

在此範例中，每小時 hello 活動執行 hello 之間開始和結束時間的 hello 管線。 hello 輸出資料會每小時產生三個小時視窗 （上午 8-9 AM，上午 9-10，以及上午 10-11 AM）。 

活動執行所取用或產生的每個資料單位稱為「資料配量」。 hello 下列圖表顯示的活動，具有一個輸入資料集和一個輸出資料集的範例： 

![可用性排程器](./media/data-factory-scheduling-and-execution/availability-scheduler.png)

hello 圖表會顯示 hello 每小時 hello 的資料配量輸入和輸出資料集。 hello 圖表顯示三個輸入的配量，準備進行處理。 hello 10 11 AM 活動正在進行中，產生 hello 10 11 AM 輸出配量。 

您可以存取使用變數與 hello 資料集 JSON 中的 hello 目前扇區相關聯的 hello 時間間隔： [SliceStart](data-factory-functions-variables.md#data-factory-system-variables)和[SliceEnd](data-factory-functions-variables.md#data-factory-system-variables)。 同樣地，您可以存取與視窗相關聯活動使用 hello WindowStart 和 WindowEnd hello 時間間隔。 hello 排程的活動必須符合 hello hello hello 活動的輸出資料集的排程。 因此，hello SliceStart 和 SliceEnd 值為 hello 相同成 WindowStart 和 WindowEnd 值分別。 如需有關這些變數的詳細資訊，請參閱 [Data Factory 函式與系統變數](data-factory-functions-variables.md#data-factory-system-variables)文章。  

您可以在活動 JSON 中針對不同用途使用這些變數。 例如，您可以使用它們 tooselect 資料從輸入和輸出資料集代表時間序列資料 (例如： 8 AM too9 AM)。 此範例也會使用**WindowStart**和**WindowEnd** tooselect 活動相關的資料執行，並將它複製 tooa blob 以適當的 hello **folderPath**。 hello **folderPath**每小時是參數化的 toohave 個別的資料夾。  

在上述範例中的 hello，指定輸入和輸出資料集的 hello 排程是 hello 相同 （每小時）。 如果 hello hello 活動的輸入資料集，可在不同的頻率，假設每隔 15 分鐘會產生此輸出資料集的 hello 活動仍會執行小時一次為 hello 輸出資料集是哪些磁碟機 hello 活動排程。 如需詳細資訊，請參閱[使用不同的頻率模型化資料集](#model-datasets-with-different-frequencies)。

## <a name="dataset-availability-and-policies"></a>資料集可用性和原則
您已經知道 hello 使用量的頻率和間隔資料集定義的 hello 可用性一節中的屬性。 有幾個會影響 hello 排程和執行活動的其他屬性。 

### <a name="dataset-availability"></a>資料集可用性 
hello 下表描述您可以使用在 hello 屬性**可用性**> 一節：

| 屬性 | 說明 | 必要 | 預設值 |
| --- | --- | --- | --- |
| frequency |指定資料集配量實際執行環境的 hello 時間單位。<br/><br/><b>支援的頻率</b>：Minute、Hour、Day、Week、Month |是 |NA |
| interval |指定頻率的倍數<br/><br/>[頻率 x 間隔] 判斷頻率 hello 產生配量。<br/><br/>如果您需要 hello 配量每小時的資料集 toobe，設定<b>頻率</b>太<b>小時</b>，和<b>間隔</b>太<b>1</b>。<br/><br/><b>請注意</b>： 如果您將 Frequency 指定為 Minute，我們建議您設定小於 15 的 hello 間隔 toono |是 |NA |
| style |指定是否應該在 hello 開始/結束 hello 間隔產生 hello 配量。<ul><li>StartOfInterval</li><li>EndOfInterval</li></ul><br/><br/>如果頻率設定 tooMonth 樣式設定 tooEndOfInterval，hello 當月最後一天產生 hello 配量。 如果 hello 樣式設定 tooStartOfInterval，hello 點產生配量 hello 當月第一日。<br/><br/>如果頻率設定 tooDay tooEndOfInterval 設定樣式時，會產生 hello 的 hello 當日的前一個小時 hello 配量。<br/><br/>如果頻率設定 tooHour 樣式設定 tooEndOfInterval，hello 配量會產生在 hello hello 小時結尾。 例如，1 PM – 2 PM 期間的配量，hello 配量會在 2 PM 產生。 |否 |EndOfInterval |
| anchorDateTime |定義中使用的排程器 toocompute 資料集配量界限時間 hello 絕對位置。 <br/><br/><b>請注意</b>： 如果 hello AnchorDateTime 具有比 hello 頻率較精細的日期部分，則 hello 更精細的部分會被忽略。 <br/><br/>例如，如果 hello<b>間隔</b>是<b>每小時</b>(頻率： hour，interval: 1) 和 hello <b>AnchorDateTime</b>包含<b>分鐘和秒鐘</b>，然後 hello<b>分鐘和秒鐘</b>hello AnchorDateTime 的部分會被忽略。 |否 |01/01/0001 |
| Offset |哪些 hello 的所有資料集配量的開始與結束移位的 Timespan。 <br/><br/><b>請注意</b>: hello 結果指定 anchorDateTime 和 offset，如果是合併的 hello 移位。 |否 |NA |

### <a name="offset-example"></a>位移範例
根據預設，每日 (`"frequency": "Day", "interval": 1`) 配量的開始時間是 UTC 時間上午 12 點 (午夜)。 如果要改為 hello 開始時間 toobe 上午 6 點 UTC 時間，將設定 hello 位移 hello 下列程式碼片段所示： 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a>anchorDateTime 範例
在下列範例的 hello，hello 資料集，會產生一次每 23 的小時。 hello 第一個配量開始 hello anchorDateTime 太設定所指定的 hello 時間`2017-04-19T08:00:00`（UTC 時間）。

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a>位移/樣式範例
hello 下列資料集的每月的資料集，且會在上午 8:00 的每個月的第 3 產生 (`3.08:00:00`):

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

### <a name="dataset-policy"></a>資料集原則
資料集，可以指定如何驗證配量執行所產生的 hello 資料供取用之前的驗證原則定義。 在這種情況下，hello 配量完成執行之後 hello 輸出配量狀態會變成太**等候**的子狀態與**驗證**。 Hello 配量會驗證之後，hello 配量狀態會變更太**準備**。 如果已產生的資料配量，但未通過 hello 驗證，不會處理下游配量相依於此配量的活動執行。 [監視和管理管線](data-factory-monitor-manage-pipelines.md)涵蓋 hello 的 Data Factory 中的資料配量的各種狀態。

hello**原則**資料集定義中的區段會定義 hello 準則或 hello 資料集配量的 hello 條件必須滿足。 hello 下表描述您可以使用在 hello 屬性**原則**> 一節：

| 原則名稱 | 說明 | 套用太| 必要 | 預設值 |
| --- | --- | --- | --- | --- |
| minimumSizeMB | 驗證中的 hello 資料**Azure blob**符合 hello 最小大小需求 （以 mb 為單位）。 |Azure Blob |否 |NA |
| minimumRows | 驗證中的 hello 資料**Azure SQL database**或**Azure 資料表**包含 hello 最小數目的資料列。 |<ul><li>Azure SQL Database</li><li>Azure 資料表</li></ul> |否 |NA |

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

**minimumRows**

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

如需有關這些屬性及範例的詳細資訊，請參閱[建立資料集](data-factory-create-datasets.md)一文。 

## <a name="activity-policies"></a>活動原則
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

如需詳細資訊，請參閱[管線](data-factory-create-pipelines.md)一文。 

## <a name="parallel-processing-of-data-slices"></a>資料配量的平行處理
您可以設定 hello hello 管線的開始日期在過去的 hello。 當您這樣做時，Data Factory 會自動計算 （背景填滿） 在過去的 hello 中的所有資料配量，並開始處理它們。 例如： 如果管線的開始日期 2017年-04-01，且 hello 目前的日期是 2017年-04-10。 如果 hello 韻律 hello 的輸出資料集是每日，則處理從 2017年-04-01 所有 hello 配量的 Data Factory 啟動 too2017-04 09 立即因為 hello 開始日期是在過去的 hello。 從 2017年-04-10 hello 配量不會處理尚未因為 hello hello 可用性一節中的樣式屬性的值為 EndOfInterval 預設值。 hello 最舊的配量處理第一個 hello 預設 executionpriorityorder 設的值是 OldestFirst。 如需 hello 樣式屬性的說明，請參閱[資料集可用性](#dataset-availability)> 一節。 如需 hello executionpriorityorder 設 > 一節的說明，請參閱 hello[活動原則](#activity-policies)> 一節。 

您可以設定平行處理所設定的 hello 後填滿的資料配量 toobe**並行**屬性在 hello**原則**hello 活動 JSON 的區段。 此屬性決定不同配量上可能發生的平行活動執行的 hello 次數。 hello hello 並行屬性的預設值為 1。 因此，預設會一次處理一個配量。 hello 最大值為 10。 當管線時必須透過大量可用的資料，具有較大的並行值 toogo 可加快 hello 資料處理。 

## <a name="rerun-a-failed-data-slice"></a>重新執行失敗的資料配量
當處理資料配量時，發生錯誤時，您可以找出 hello 處理配量使用 Azure 入口網站的刀鋒視窗或監視和管理應用程式失敗的原因。 如需詳細資訊，請參閱[使用 Azure 入口網站刀鋒視窗監視和管理管線](data-factory-monitor-manage-pipelines.md)或[監視和管理應用程式](data-factory-monitor-manage-app.md)。

請考慮下列範例會顯示兩個活動的 hello。 Activity1 和 Activity 2。 Activity1 會消耗 Dataset1 配量，並產生配量的 Dataset2，做為輸入供 Activity2 tooproduce hello 最終資料集配量。

![失敗的配量](./media/data-factory-scheduling-and-execution/failed-slice.png)

hello 張圖表顯示三個新的配量，不足時發生失敗產生項目的 hello 上午 9 10 配量的 Dataset2。 Data Factory 自動追蹤相依性 hello 時間序列資料集。 如此一來，不會啟動 hello hello 上午 9 10 下游配量執行的活動。

資料處理站的監視與管理工具可讓您 toodrill hello 診斷記錄檔到 hello 失敗的配量 tooeasily 尋找 hello 根 hello 問題會造成，，修正此問題。 修正 hello 問題之後，您可以輕鬆地開始執行 tooproduce hello 失敗配量的 hello 活動。 如需有關如何 toorerun 和了解資料配量的狀態轉換，請參閱[監視及管理使用 Azure 入口網站的刀鋒視窗的管線](data-factory-monitor-manage-pipelines.md)或[監視和管理應用程式](data-factory-monitor-manage-app.md)。

在重新執行 hello 之後的上午 9 10 配量**Dataset2**，Data Factory 啟動 hello hello 最終資料集上執行 hello 上午 9 10 相依配量。

![重新執行失敗的配量](./media/data-factory-scheduling-and-execution/rerun-failed-slice.png)

## <a name="multiple-activities-in-a-pipeline"></a>管線中的多個活動
您可以在一個管線中包含多個活動。 如果您在管線中有多個活動與 hello 輸出的活動不是另一個活動的輸入，hello 活動可能會以平行方式執行，hello 活動的輸入的資料配量是否準備。

您可以藉由設定 hello 輸出資料集的一個活動 hello 的輸入資料集的 hello 其他活動鏈結 （執行一個活動執行另一個之後） 的兩個活動。 可以在 hello hello 活動相同的管線或在不同的管線中。 hello 第一次一個成功完成時，才會執行 hello 第二個活動。

例如，請考慮下列管線有兩個活動的 hello:

1. 需要外部輸入資料集 D1 並且會產生輸出資料集 D2 的活動 A1。
2. 需要來自資料集 D2 之輸入並且會產生輸出資料集 D3 的活動 A2。

在此案例中，活動 A1 和 A2 會在 hello 相同管線。 A1 時執行 hello 外部資料可供使用且達到 hello 排程可用性頻率 hello 活動。 hello 活動 A2 時執行 hello D2 從排程配量，就可以使用且 hello 頻率排程的可用性為止。 如果沒有發生錯誤，其中一種集中 D2 hello 配量，A2 不會執行該配量直到它可用為止。

hello 相同管線會看起來像下列圖表中的 hello 與 hello 中這兩個活動的圖表檢視：

![鏈結中 hello 活動相同管線](./media/data-factory-scheduling-and-execution/chaining-one-pipeline.png)

如先前所述，hello 活動可以是不同的管線。 在這種情況下，hello 圖表檢視會看起來像下列圖表中的 hello:

![兩個管線中的鏈結活動](./media/data-factory-scheduling-and-execution/chaining-two-pipelines.png)

請參閱 hello[循序複製](#copy-sequentially)hello 附錄的範例 > 一節。

## <a name="model-datasets-with-different-frequencies"></a>使用不同的頻率模型化資料集
在 hello 範例中，輸入和輸出資料集和 hello 活動排程時段的 hello 頻率所 hello 相同。 某些情況下需要 hello 能力 tooproduce 輸出在不同的一或多個輸入 hello 頻率的頻率。 Data Factory 支援模型化這些案例。

### <a name="sample-1-produce-a-daily-output-report-for-input-data-that-is-available-every-hour"></a>範例 1：對每小時可用的輸入資料產生每日輸出報告
請設想 Azure Blob 儲存體中每小時會有來自感應器的輸入測量資料的案例。 您想要與 hello 天 tooproduce 統計資料，例如平均值、 最大值和最小值的每日彙總報表[Data Factory hive 活動](data-factory-hive-activity.md)。

以下是使用 Data Factory 模型化此案例的方式：

**輸入資料集**

hello 每小時輸入 hello 指定一天的 hello 資料夾中會卸除檔案。 輸入的可用性設定為 **小時** (頻率：小時、間隔：1)。

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
**輸出資料集**

一個輸出檔 hello 一天的資料夾中建立每一天。 輸出的可用性設定為 **日** (頻率：日、間隔：1)。

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**活動：管線中的 Hive 活動**

hello hive 指令碼會收到 hello 適當*DateTime*資訊做為參數使用 hello **WindowStart** hello 下列程式碼片段所示的變數。 hello hive 指令碼會使用此變數 tooload hello 資料 hello 正確的資料夾從 hello 日，並執行 hello 彙總 toogenerate hello 輸出。

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
        {
            "name": "SampleHiveActivity",
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
            "linkedServiceName": "HDInsightLinkedService",
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "adftutorial\\hivequery.hql",
                "scriptLinkedService": "StorageLinkedService",
                "defines": {
                    "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
                    "Month": "$$Text.Format('{0:MM}',WindowStart)",
                    "Day": "$$Text.Format('{0:dd}',WindowStart)"
                }
            },
            "scheduler": {
                "frequency": "Day",
                "interval": 1
            },            
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 2,
                "timeout": "01:00:00"
            }
         }
     ]
   }
}
```

hello 下列圖表顯示 hello 案例從資料相依性的觀點。

![資料相依性](./media/data-factory-scheduling-and-execution/data-dependency.png)

每一天的 hello 輸出配量取決於輸入資料集從 24 小時的配量。 這些相依性，以找出自動 hello 落在 hello 的輸入的資料配量的資料處理站計算相同的時間週期 hello 產生輸出配量 toobe。 如果任何 hello 24 輸入配量無法使用，則 Data Factory 會等候 hello 輸入配量 toobe 之後，再啟動 hello 每日執行的活動。

### <a name="sample-2-specify-dependency-with-expressions-and-data-factory-functions"></a>範例 2：使用運算式和 Data Factory 函數指定相依性
我們來看一下另一種案例。 假設您有處理兩個輸入資料集的 Hive 活動。 其中一個每日有新資料，但是另一個會每週取得新資料。 假設您想 toodo 聯結 hello 兩個輸入之間，每日產生的輸出。

hello 簡單的方法，在其中 Data Factory 自動找出 hello 右邊輸入分割 tooprocess 對齊 toohello 輸出資料配量的時間週期內無法運作。

您必須指定執行每個活動，如 hello Data Factory 應該使用上週的資料配量的 hello 每週的輸入資料集。 您使用 Azure Data Factory 函數中所示 hello 下列程式碼片段 tooimplement 這種行為。

**Input1：Azure Blob**

hello 的第一個輸入 hello Azure blob 的每日更新。

```json
{
  "name": "AzureBlobInputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**Input2：Azure Blob**

Input2 為 hello Azure blob，每週更新。

```json
{
  "name": "AzureBlobInputWeekly",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 7
    }
  }
}
```

**輸出：Azure Blob**

一個輸出檔每天資料夾中建立 hello hello 一天。 輸出的可用性設定得**天**(頻率： Day、 interval: 1)。

```json
{
  "name": "AzureBlobOutputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**活動：管線中的 Hive 活動**

hello hive 活動會採用 hello 兩個輸入，並產生輸出配量每一天。 您可以指定每日輸出配量 toodepend 上的 hello 前一週每週輸入配量，如下所示。

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
      {
        "name": "SampleHiveActivity",
        "inputs": [
          {
            "name": "AzureBlobInputDaily"
          },
          {
            "name": "AzureBlobInputWeekly",
            "startTime": "Date.AddDays(SliceStart, - Date.DayOfWeek(SliceStart))",
            "endTime": "Date.AddDays(SliceEnd,  -Date.DayOfWeek(SliceEnd))"  
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutputDaily"
          }
        ],
        "linkedServiceName": "HDInsightLinkedService",
        "type": "HDInsightHive",
        "typeProperties": {
          "scriptPath": "adftutorial\\hivequery.hql",
          "scriptLinkedService": "StorageLinkedService",
          "defines": {
            "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
            "Month": "$$Text.Format('{0:MM}',WindowStart)",
            "Day": "$$Text.Format('{0:dd}',WindowStart)"
          }
        },
        "scheduler": {
          "frequency": "Day",
          "interval": 1
        },            
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 2,  
          "timeout": "01:00:00"
        }
       }
     ]
   }
}
```

如需 Data Factory 所支援的函數與系統變數清單，請參閱 [Data Factory 函式與系統變數](data-factory-functions-variables.md) 。

## <a name="appendix"></a>附錄

### <a name="example-copy-sequentially"></a>範例：循序複製
它是可能 toorun 多項複製作業逐一循序/排序的方式。 例如，您可能有兩個複本活動與 hello 遵循管線 （CopyActivity1 和 CopyActivity2） 中的輸入的資料輸出資料集：   

CopyActivity1

輸入：Dataset1。 輸出：Dataset2。

CopyActivity2

輸入：Dataset2。  輸出：Dataset3。

只有 hello CopyActivity1 曾順利執行，且 Dataset2 為可用，就會執行 CopyActivity2。

以下是 hello 範例管線 JSON:

```json
{
    "name": "ChainActivities",
    "properties": {
        "description": "Run activities in sequence",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset1"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob1ToBlob2",
                "description": "Copy data from a blob tooanother"
            },
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset3"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob2ToBlob3",
                "description": "Copy data from a blob tooanother"
            }
        ],
        "start": "2016-08-25T01:00:00Z",
        "end": "2016-08-25T01:00:00Z",
        "isPaused": false
    }
}
```

請注意在 hello 範例中，指定 hello 輸出資料集的 hello 第一個複製活動 (Dataset2) 是做為輸入 hello 第二個活動。 因此，只有準備 hello 從 hello 第一個活動的輸出資料集時，才會執行 hello 第二個活動。  

在 hello 範例 CopyActivity2 可以有不同的輸入，例如 Dataset3，但您指定 Dataset2 為輸入的 tooCopyActivity2，因此直到完成 CopyActivity1 hello 活動不會執行。 例如：

CopyActivity1

輸入︰Dataset1。 輸出：Dataset2。

CopyActivity2

輸入︰Dataset3、Dataset2。 輸出︰Dataset4。

```json
{
    "name": "ChainActivities",
    "properties": {
        "description": "Run activities in sequence",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset1"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlobToBlob",
                "description": "Copy data from a blob tooanother"
            },
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset3"
                    },
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset4"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob3ToBlob4",
                "description": "Copy data from a blob tooanother"
            }
        ],
        "start": "2017-04-25T01:00:00Z",
        "end": "2017-04-25T01:00:00Z",
        "isPaused": false
    }
}
```

請注意在 hello 範例中，指定兩個輸入資料集是 hello 第二個複製活動。 當指定多個輸入時，只有 hello 第一個輸入資料集用來複製資料，但是其他資料集做為相依性。 CopyActivity2 會啟動才 hello 必須符合下列條件：

* CopyActivity1 已順利完成且 Dataset2 可供使用。 複製資料 tooDataset4 時，不會使用此資料集。 它只會用來做為 CopyActivity2 的排程相依性。   
* Dataset3 可供使用。 此資料集代表 hello 資料複製的 toohello 目的地。 
