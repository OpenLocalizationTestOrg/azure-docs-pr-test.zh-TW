---
title: "aaaData Factory 函式和系統變數 |Microsoft 文件"
description: "提供 Azure Data Factory 函式與系統變數清單"
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
services: data-factory
ms.assetid: b6b3c2ae-b0e8-4e28-90d8-daf20421660d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: d2936c2821797947bb37d9775226a6c19c4b8ab9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---functions-and-system-variables"></a>Azure Data Factory - 函式與系統變數
本文提供 Azure Data Factory 支援之函式和變數的相關資訊。

## <a name="data-factory-system-variables"></a>Data Factory 系統變數
| 變數名稱 | 說明 | 物件範圍 | JSON 範圍和使用案例 |
| --- | --- | --- | --- |
| WindowStart |目前活動執行時段的時間間隔開始 |活動 |<ol><li>指定資料選取範圍查詢。 請參閱 hello 中參考的連接器文件[資料移動活動](data-factory-data-movement-activities.md)發行項。</li> |
| WindowEnd |目前活動執行時段的時間間隔結束 |活動 |與 WindowStart 相同。 |
| SliceStart |所產生之資料配量的時間間隔開始 |活動<br/>資料集 |<ol><li>指定使用 [Azure Blob](data-factory-azure-blob-connector.md) 和[檔案系統資料集](data-factory-onprem-file-system-connector.md)時的動態資料夾路徑與檔案名稱。</li><li>使用 Data Factory 函式在活動輸入集合中指定輸入相依性。</li></ol> |
| SliceEnd |目前資料配量的時間間隔結束。 |活動<br/>資料集 |與 SliceStart 相同。 |

> [!NOTE]
> 目前資料 factory 需要該 hello 排程中指定的 hello 活動與 hello 排程 hello 輸出資料集中的可用性中指定完全相符。 因此，WindowStart、 WindowEnd，SliceStart 和 SliceEnd 一律對應 toohello 相同時間週期和單一輸出配量。
> 

### <a name="example-for-using-a-system-variable"></a>使用系統變數的範例
在下列範例中，年、 月、 日和時間的 hello **SliceStart**會擷取至不同的變數，可供**folderPath**和**fileName**屬性。

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

## <a name="data-factory-functions"></a>Data Factory 函式
您可以使用 data factory，以及系統變數中的函式 hello 下列用途：

1. 指定資料選取項目查詢 (請參閱 hello 所參考的連接器文件[資料移動活動](data-factory-data-movement-activities.md)發行項。
   
   hello 資料 factory 函式的語法 tooinvoke:  **$$ <function>** 資料選取項目查詢和在 hello 活動和資料集中的其他屬性。  
2. 使用 Data Factory 函式在活動輸入集合中指定輸入相依性。
   
    指定輸入相依性運算式不需要 $$。     

在下列範例中，hello **sqlReaderQuery** hello 所傳回的 tooa 值指派給屬性的 JSON 檔案中`Text.Format`函式。 此範例也會使用系統變數，名為**WindowStart**，代表 hello hello 活動執行視窗開始時間。

```json
{
    "Type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
}
```

請參閱說明可使用的各種格式化選項 (例如：ay 與 yyyy) 的[自訂日期和時間格式字串](https://msdn.microsoft.com/library/8kb3ddd4.aspx)主題。 

### <a name="functions"></a>Functions
hello 下表列出所有 Azure Data Factory 中的 hello 函式：

| 類別 | 函式 | 參數 | 說明 |
| --- | --- | --- | --- |
| 時間 |AddHours(X,Y) |X：DateTime  <br/><br/>Y：int |將 Y 小時 toohello 特定時間 X。 <br/><br/>範例： `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM` |
| 時間 |AddMinutes(X,Y) |X：DateTime  <br/><br/>Y：int |將 Y 分鐘 tooX。<br/><br/>範例： `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM` |
| 時間 |StartOfHour(X) |X：DateTime  |取得 hello 啟動 X hello 小時元件所代表的 hello 小時的時間。 <br/><br/>範例： `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM` |
| 日期 |AddDays(X,Y) |X：DateTime <br/><br/>Y：int |將 Y 天 tooX。 <br/><br/>範例：9/15/2013 12:00:00 PM + 2 天 = 9/17/2013 12:00:00 PM。<br/><br/>您也可以藉由將 Y 指定為負數來減去天。<br/><br/>範例：`9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`. |
| 日期 |AddMonths(X,Y) |X：DateTime <br/><br/>Y：int |將 Y 個月 tooX。<br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`。<br/><br/>您也可以藉由將 Y 指定為負數來減去月份。<br/><br/>範例：`9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.|
| 日期 |AddQuarters(X,Y) |X：DateTime  <br/><br/>Y：int |將 Y * 3 個月 tooX。<br/><br/>範例： `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM` |
| 日期 |AddWeeks(X,Y) |X：DateTime <br/><br/>Y：int |將 Y * 7 天 tooX<br/><br/>範例：9/15/2013 12:00:00 PM + 1 週 = 9/22/2013 12:00:00 PM<br/><br/>您也可以藉由將 Y 指定為負數來減去週。<br/><br/>範例：`9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`. |
| 日期 |AddYears(X,Y) |X：DateTime <br/><br/>Y：int |將 Y 年 tooX。<br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 year = 9/15/2014 12:00:00 PM`<br/><br/>您也可以藉由將 Y 指定為負數來減去年。<br/><br/>範例：`9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`. |
| 日期 |Day(X) |X：DateTime  |取得 X 的 hello 日期元件。<br/><br/>範例：`Day of 9/15/2013 12:00:00 PM is 9`. |
| 日期 |DayOfWeek(X) |X：DateTime  |取得 X 的星期幾元件 hello 日期。<br/><br/>範例：`DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`. |
| 日期 |DayOfYear(X) |X：DateTime  |取得 X hello 年度元件所代表的 hello 年中的 hello 一天。<br/><br/>範例：<br/>`12/1/2015: day 335 of 2015`<br/>`12/31/2015: day 365 of 2015`<br/>`12/31/2016: day 366 of 2016 (Leap Year)` |
| 日期 |DaysInMonth(X) |X：DateTime  |取得參數 X 的 hello 月份元件所代表的 hello 月份中的 hello 日期。<br/><br/>範例：`DaysInMonth of 9/15/2013 are 30 since there are 30 days in hello September month`. |
| 日期 |EndOfDay(X) |X：DateTime  |取得 hello 日期-時間表示 hello X hello 日期 （日期元件） 的結尾。<br/><br/>範例：`EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`. |
| 日期 |EndOfMonth(X) |X：DateTime  |取得參數 X 的月份元件所代表的 hello 月份 hello 末端。 <br/><br/>範例： `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` （日期，代表 hello 九月份結束的時間） |
| Date |StartOfDay(X) |X：DateTime  |取得參數 X 的 hello 日期元件所代表的 hello 天 hello 開頭。<br/><br/>範例：`StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`. |
| DateTime |From(X) |X：字串 |剖析字串 X tooa 日期時間。 |
| DateTime |Ticks(X) |X：DateTime  |取得 hello 刻度 hello 參數 X 的屬性。一個刻度等於 100 奈秒。 hello 這個屬性的值代表 hello 0001 年 1 月 1 日的 12:00:00 午夜以來已經過的刻度數目。 |
| 文字 |Format(X) |X：字串變數 |格式 hello 文字 (使用`\\'`組合 tooescape`'`字元)。|

> [!IMPORTANT]
> 當使用另一個函式內的函式時，您不需要 toouse  **$$**  hello 內部函式的前置詞。 例如：$$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' and RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)). 在此範例中，注意 **$$** 前置詞不能用於 hello **Time.AddHours**函式。 

#### <a name="example"></a>範例
在 hello hello Hive 活動的下列範例中，輸入和輸出參數會決定使用 hello`Text.Format`函式和 SliceStart 系統變數。 

```json  
{
    "name": "HiveActivitySamplePipeline",
        "properties": {
    "activities": [
            {
            "name": "HiveActivitySample",
            "type": "HDInsightHive",
            "inputs": [
                    {
                    "name": "HiveSampleIn"
                    }
            ],
            "outputs": [
                    {
                    "name": "HiveSampleOut"
                }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "typeproperties": {
                    "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Input": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                    },
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                }
            }
            }
    ]
    }
}
```

### <a name="example-2"></a>範例 2

在下列範例的 hello，hello 的 hello 預存程序活動由使用 hello 文字的日期時間參數。 格式函式和 hello SliceStart 變數。 

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
                "outputs": [
                    {
                        "name": "sprocsampleout"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
            "start": "2016-08-02T00:00:00Z",
            "end": "2016-08-02T05:00:00Z",
        "isPaused": false
    }
}
```

### <a name="example-3"></a>範例 3
tooread 前一天，而不是由 hello SliceStart，天資料使用 hello AddDays 函式 hello 下列範例所示： 

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-01-01T08:00:00",
        "end": "2017-01-01T11:00:00",
        "description": "hive activity",
        "activities": [
            {
                "name": "SampleHiveActivity",
                "inputs": [
                    {
                        "name": "MyAzureBlobInput",
                        "startTime": "Date.AddDays(SliceStart, -1)",
                        "endTime": "Date.AddDays(SliceEnd, -1)"
                    }
                ],
                "outputs": [
                    {
                        "name": "MyAzureBlobOutput"
                    }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adftutorial\\hivequery.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Year": "$$Text.Format('{0:yyyy}',WindowsStart)",
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

請參閱說明可使用的各種格式化選項 (例如：yy 與 yyyy) 的 [自訂日期和時間格式字串](https://msdn.microsoft.com/library/8kb3ddd4.aspx) 主題。 

