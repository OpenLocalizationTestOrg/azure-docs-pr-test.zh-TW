---
title: "aaaSQL 伺服器預存程序活動"
description: "了解您可以使用 hello SQL Server 預存程序活動 tooinvoke 從 Data Factory 管線中的 Azure SQL Database 或 Azure SQL 資料倉儲的預存程序。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1c46ed69-4049-44ec-9b46-e90e964a4a8e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: spelluru
ms.openlocfilehash: 9116f80eefc59d95e866b2ba1de2feb1bdc4b1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-stored-procedure-activity"></a>SQL Server 預存程序活動
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Hive 活動](data-factory-hive-activity.md) 
> * [Pig 活動](data-factory-pig-activity.md)
> * [MapReduce 活動](data-factory-map-reduce.md)
> * [Hadoop 串流活動](data-factory-hadoop-streaming-activity.md)
> * [Spark 活動](data-factory-spark.md)
> * [Machine Learning Batch 執行活動](data-factory-azure-ml-batch-execution-activity.md)
> * [Machine Learning 更新資源活動](data-factory-azure-ml-update-resource-activity.md)
> * [預存程序活動](data-factory-stored-proc-activity.md)
> * [Data Lake Analytics U-SQL 活動](data-factory-usql-activity.md)
> * [.NET 自訂活動](data-factory-use-custom-activities.md)

## <a name="overview"></a>概觀
您使用 Data Factory 中的資料轉換活動[管線](data-factory-create-pipelines.md)tootransform 和程序到預測和深入觀點的未經處理資料。 hello 預存程序活動是的 Data Factory 支援的 hello 轉換活動。 這篇文章是根據 hello[資料轉換活動](data-factory-data-transformation-activities.md)發行項，其呈現的資料轉換和 Data Factory 中的 hello 支援轉換活動的一般概觀。

您可以使用其中一種 hello 下列資料的預存程序儲存在您企業中或在 Azure 虛擬機器 (VM) 上的 hello 預存程序活動 tooinvoke: 

- Azure SQL Database
- Azure SQL 資料倉儲
- SQL Server Database。  如果您使用 SQL Server 時，資料管理閘道上安裝相同機器主機 hello 資料庫，或在不同電腦上具有存取 toohello 資料庫 hello。 資料管理閘道是一套透過安全且可管理的方式，將內部部署/Azure VM 上的資料來源連結至雲端服務的元件。 如需詳細資訊，請參閱[資料管理閘道](data-factory-data-management-gateway.md)文章。

> [!IMPORTANT]
> 當將資料複製到 Azure SQL Database 或 SQL Server，您可以設定 hello **SqlSink**在複製活動 tooinvoke 預存程序使用 hello **sqlWriterStoredProcedureName**屬性。 如需詳細資訊，請參閱[從複製活動叫用預存程序](data-factory-invoke-stored-procedure-from-copy-activity.md)。 如需有關 hello 屬性的詳細資訊，請參閱下列連接器文件： [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties)， [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties)。 不支援在使用複製活動將資料複製到「Azure SQL 資料倉儲」時叫用預存程序。 但是，您可以使用 SQL 資料倉儲中的 hello 預存程序活動 tooinvoke 預存程序。 
>  
> 當從 Azure SQL Database 或 SQL Server 或 Azure SQL 資料倉儲中複製資料，您可以設定**SqlSource**在複製活動 tooinvoke 使用 hello hello 來源資料庫中的預存程序 tooread 資料**sqlReaderStoredProcedureName**屬性。 如需詳細資訊，請參閱下列連接器的發行項的 hello: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties)， [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties)， [Azure SQL 資料倉儲](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)          


下列逐步解說會使用 hello hello 管線 tooinvoke Azure SQL database 中的預存程序中的預存程序活動。 

## <a name="walkthrough"></a>逐步介紹
### <a name="sample-table-and-stored-procedure"></a>範例資料表與預存程序
1. 建立 hello 遵循**資料表**中使用 SQL Server Management Studio 或其他任何工具，您可以輕鬆地與您 Azure SQL Database。 hello datetimestamp 資料行是 hello 日期和時間時產生 hello 相對應的識別碼。

    ```SQL
    CREATE TABLE dbo.sampletable
    (
        Id uniqueidentifier,
        datetimestamp nvarchar(127)
    )
    GO

    CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable(Id);
    GO
    ```
    識別碼 hello 唯一識別但 hello datetimestamp 資料行是 hello 日期和時間時產生 hello 相對應的識別碼。
    
    ![範例資料](./media/data-factory-stored-proc-activity/sample-data.png)

    在此範例中，hello 預存程序是在 Azure SQL Database。 Hello 預存程序是在 Azure SQL 資料倉儲和 SQL Server 資料庫中，如果 hello 方法相似。 對於 SQL Server 資料庫中，您必須安裝[資料管理閘道](data-factory-data-management-gateway.md)。
2. 建立 hello 遵循**預存程序**，將資料插入 toohello**範例資料表**。

    ```SQL
    CREATE PROCEDURE sp_sample @DateTime nvarchar(127)
    AS

    BEGIN
        INSERT INTO [sampletable]
        VALUES (newid(), @DateTime)
    END
    ```

   > [!IMPORTANT]
   > **名稱**和**大小寫**hello 的參數 （在此範例中的日期時間） 必須符合的 hello 管線/活動 JSON 中指定的參數。 在 hello 預存程序定義中，確定 **@**  hello 參數做為前置字元。

### <a name="create-a-data-factory"></a>建立 Data Factory
1. 登入太[Azure 入口網站](https://portal.azure.com/)。
2. 按一下**新增**hello 左窗格中，按一下 **智慧 + 分析**，然後按一下**Data Factory**。

    ![新增 Data Factory](media/data-factory-stored-proc-activity/new-data-factory.png)    
3. 在 hello**新的 data factory**刀鋒視窗中，輸入**SProcDF** hello 名稱。 Azure Data Factory 名稱必須是**全域唯一的**。 您需要 tooprefix hello hello data factory 名稱與您的名稱，tooenable hello 成功建立 hello factory。

   ![新增 Data Factory](media/data-factory-stored-proc-activity/new-data-factory-blade.png)         
4. 選取您的 **Azure 訂用帳戶**。
5. 如**資源群組**，執行下列步驟的 hello 其中一項：
   1. 按一下**建立新**，然後輸入 hello 資源群組的名稱。
   2. 按一下 [使用現有的] 並選取現有的資源群組。  
6. 選取 hello**位置**hello data factory。
7. 選取**Pin toodashboard** ，讓您能夠查看 hello 資料 factory hello 儀表板上登入的下一次。
8. 按一下**建立**上 hello**新的 data factory**刀鋒視窗。
9. 您會看到 hello hello 中建立的資料處理站**儀表板**的 hello Azure 入口網站。 已成功建立 hello 資料處理站之後，您會看到 hello 資料 factory 頁面上，它會顯示 hello hello data factory 的內容。

   ![Data Factory 首頁](media/data-factory-stored-proc-activity/data-factory-home-page.png)

### <a name="create-an-azure-sql-linked-service"></a>建立 Azure SQL 連結服務
建立 hello 資料處理站之後, 您可以建立連結您的 Azure SQL 資料庫，其中包含 hello 範例資料表的資料表和 sp_sample 預存程序、 tooyour 資料處理站的 Azure SQL 連結服務。

1. 按一下**作者及部署**上 hello **Data Factory**刀鋒伺服器**SProcDF** toolaunch hello Data Factory 編輯器。
2. 按一下**新建資料存放區**在 hello 命令列，然後選擇  **Azure SQL Database**。 您應該會看到 hello JSON 指令碼來建立 Azure SQL 連結服務 hello 編輯器中。

   ![新增資料存放區](media/data-factory-stored-proc-activity/new-data-store.png)
3. 在 hello JSON 指令碼，進行下列變更 hello:

   1. 取代`<servername>`hello Azure SQL Database 伺服器名稱。
   2. 取代`<databasename>`hello 資料庫建立 hello 資料表和 hello 與預存程序。
   3. 取代`<username@servername>`hello 使用者帳戶具有存取 toohello 資料庫。
   4. 取代`<password>`hello hello 使用者帳戶的密碼。

      ![新增資料存放區](media/data-factory-stored-proc-activity/azure-sql-linked-service.png)
4. toodeploy hello 連結的服務中，按一下**部署**hello 命令列上。 確認您看到 hello AzureSqlLinkedService hello 樹狀結構中的檢視 hello 左側。

    ![含連結服務的樹狀檢視](media/data-factory-stored-proc-activity/tree-view.png)

### <a name="create-an-output-dataset"></a>建立輸出資料表
您必須指定預存程序活動的輸出資料集即使 hello 預存程序不會產生任何資料。 這是因為它的 hello 輸出 hello 排程 hello 活動 （頻率 hello 活動執行的每小時、 每日等） 的磁碟機的資料集。 hello 輸出資料集必須使用**連結服務**參考 tooan Azure SQL Database 或 Azure SQL 資料倉儲或您想在其中 hello toorun 預存程序的 SQL Server 資料庫。 hello 輸出資料集可以做為方法 toopass hello hello 預存程序的結果進行後續處理另一個活動 ([鏈結活動](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)hello 管線中。 不過，Data Factory 不會自動寫入預存程序 toothis 資料集的 hello 輸出。 它是 hello 預存程序 hello 輸出資料集指向該寫入 tooa SQL 資料表。 在某些情況下，可以是 hello 輸出資料集**空資料集**（點 tooa 資料表實際上不會保存 hello 的輸出資料集預存程序）。 執行 hello toospecify hello 排程預存程序活動僅用於此空的資料集。 

1. 按一下**...多個**hello 工具列上，按一下**新的資料集**，然後按一下**Azure SQL**。 **新的資料集**上 hello 命令列，並選取**Azure SQL**。

    ![含連結服務的樹狀檢視](media/data-factory-stored-proc-activity/new-dataset.png)
2. 複製/貼上下列 JSON 指令碼 toohello JSON 編輯器中的 hello。

    ```JSON
    {                
        "name": "sprocsampleout",
        "properties": {
            "type": "AzureSqlTable",
            "linkedServiceName": "AzureSqlLinkedService",
            "typeProperties": {
                "tableName": "sampletable"
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```
3. toodeploy hello 資料集，請按一下**部署**hello 命令列上。 確認您看到 hello hello 樹狀檢視中的資料集。

    ![含連結服務的樹狀檢視](media/data-factory-stored-proc-activity/tree-view-2.png)

### <a name="create-a-pipeline-with-sqlserverstoredprocedure-activity"></a>使用 SqlServerStoredProcedure 活動建立管線
現在，讓我們使用預存程序活動來建立管線。 

請注意下列屬性的 hello: 

- hello**類型**屬性設定太**SqlServerStoredProcedure**。 
- hello **storedProcedureName**在型別屬性設定太**sp_sample** （hello 名稱預存程序）。
- hello **storedProcedureParameters**區段包含一個名為**DataTime**。 名稱和 JSON 中的 hello 參數的大小寫必須符合 hello 名稱和大小寫的 hello 預存程序定義中的 hello 參數。 如果您需要傳遞 null 做為參數，使用 hello 語法： `"param1": null` （全部小寫）。
 
1. 按一下**...多個**在 hello 命令列，然後按一下**新管線**。
2. 複製/貼上下列 JSON 片段 hello:   

    ```JSON
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
             "start": "2017-04-02T00:00:00Z",
             "end": "2017-04-02T05:00:00Z",
            "isPaused": false
        }
    }
    ```
3. toodeploy hello 管線中，按一下 **部署**hello 工具列上。  

### <a name="monitor-hello-pipeline"></a>監視 hello 管線
1. 按一下**X** tooclose Data Factory 編輯器刀鋒 toonavigate 回 toohello Data Factory 刀鋒視窗中，並按一下**圖表**。

    ![圖表圖格](media/data-factory-stored-proc-activity/data-factory-diagram-tile.png)
2. 在 hello**圖表檢視**、 看見 hello 管線的概觀，以及資料集用在本教學課程。

    ![圖表圖格](media/data-factory-stored-proc-activity/data-factory-diagram-view.png)
3. 在 hello 圖表檢視中，按兩下 hello 資料集`sprocsampleout`。 您會看到 hello 配量處於就緒狀態。 因為每個小時 hello 開始時間和結束時間從 hello JSON 之間產生配量時，則應該是五個配量。

    ![圖表圖格](media/data-factory-stored-proc-activity/data-factory-slices.png)
4. 當配量處於**準備**執行狀態`select * from sampletable`hello 資料的 hello Azure SQL database tooverify 查詢 toohello 資料表中插入 hello 預存程序。

   ![輸出資料](./media/data-factory-stored-proc-activity/output.png)

   請參閱[監視器 hello 管線](data-factory-monitor-manage-pipelines.md)監視 Azure Data Factory 管線的詳細資訊。  


## <a name="specify-an-input-dataset"></a>指定輸入資料集
在 hello 逐步解說中，預存程序活動沒有任何輸入資料集。 如果您指定的輸入資料集，hello 預存程序活動才會開始執行的輸入資料集的 hello 配量處於可用 （就緒狀態）。 hello 資料集可以是外部的資料集 (hello 中另一個活動不產生的同一個管線) 或上游活動 （這項活動之前執行 hello 活動） 所產生的內部資料集。 您可以指定 hello 預存程序活動的多個輸入資料集。 如果您這樣做，hello 預存程序活動只時執行所有的 hello 輸入資料集配量中有可用 （就緒狀態）。 hello 輸入資料集無法取用 hello 預存程序中，做為參數。 起始 hello 預存程序活動之前，它是只使用的 toocheck hello 相依性。

## <a name="chaining-with-other-activities"></a>與其他活動鏈結
如果您想 toochain 上游活動與此活動，指定 hello 的 hello 上游活動的輸出做為輸入，此活動。 當您這樣做時，hello 預存程序活動不會執行直到 hello 上游活動完成而且 hello 的 hello 上游活動的輸出資料集 （在就緒狀態）。 您可以指定多個上游活動的輸出資料集為 hello 預存程序活動的輸入資料集。 當您這樣做，hello 預存程序活動在只在所有 hello 輸入資料集配量都可用時，才執行。  

在下列範例的 hello 的 hello 複製活動的 hello 輸出是： OutputDataset，也就是輸入 hello 的預存程序活動。 因此，hello 預存程序活動無法執行 hello 複製活動完成，然後再 hello OutputDataset 配量處於可用 （就緒）。 如果您指定多個輸入資料集，hello 預存程序活動不會執行直到所有 hello 輸入資料集配量中有都可用 （就緒狀態）。 hello 輸入資料集不能做為參數 toohello 預存程序活動。 

如需有關將活動鏈結的詳細資訊，請參閱[管線中的多個活動](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)

```json
{

    "name": "ADFTutorialPipeline",
    "properties": {
        "description": "Copy data from a blob tooblob",
        "activities": [
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
                "inputs": [ { "name": "InputDataset" } ],
                "outputs": [ { "name": "OutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst"
                },
                "name": "CopyFromBlobToSQL"
            },
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "SPSproc"
                },
                "inputs": [ { "name": "OutputDataset" } ],
                "outputs": [ { "name": "SQLOutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "RunStoredProcedure"
            }

        ],
        "start": "2017-04-12T00:00:00Z",
        "end": "2017-04-13T00:00:00Z",
        "isPaused": false,
    }
}
```

同樣地，toolink hello 存放區程序活動，具有**下游活動**（hello hello 預存程序活動完成後，執行），指定活動的 hello 預存程序活動與 hello 輸出資料集hello 管線中的 hello 下游活動的輸入。

> [!IMPORTANT]
> 當將資料複製到 Azure SQL Database 或 SQL Server，您可以設定 hello **SqlSink**在複製活動 tooinvoke 預存程序使用 hello **sqlWriterStoredProcedureName**屬性。 如需詳細資訊，請參閱[從複製活動叫用預存程序](data-factory-invoke-stored-procedure-from-copy-activity.md)。 如需有關 hello 屬性的詳細資訊，請參閱下列連接器的發行項的 hello: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties)， [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties)。
>  
> 當從 Azure SQL Database 或 SQL Server 或 Azure SQL 資料倉儲中複製資料，您可以設定**SqlSource**在複製活動 tooinvoke 使用 hello hello 來源資料庫中的預存程序 tooread 資料**sqlReaderStoredProcedureName**屬性。 如需詳細資訊，請參閱下列連接器的發行項的 hello: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties)， [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties)， [Azure SQL 資料倉儲](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)          

## <a name="json-format"></a>JSON 格式
以下是用於定義預存程序活動的 hello JSON 格式：

```JSON
{
    "name": "SQLSPROCActivity",
    "description": "description",
    "type": "SqlServerStoredProcedure",
    "inputs":  [ { "name": "inputtable"  } ],
    "outputs":  [ { "name": "outputtable" } ],
    "typeProperties":
    {
        "storedProcedureName": "<name of hello stored procedure>",
        "storedProcedureParameters":  
        {
            "param1": "param1Value"
            …
        }
    }
}
```

hello 下表描述這些 JSON 屬性：

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 名稱 | Hello 活動的名稱。 |是 |
| 說明 |描述用於 hello 活動的文字 |否 |
| 類型 | 必須設定為：**SqlServerStoredProcedure** | 是 |
| 輸入 | 選用。 如果您指定的輸入資料集，它必須可用 （處於 [就緒]' 的狀態） hello 預存程序活動 toorun。 hello 輸入資料集無法取用 hello 預存程序中，做為參數。 起始 hello 預存程序活動之前，它是只使用的 toocheck hello 相依性。 |否 |
| 輸出 | 您必須指定預存程序活動的輸出資料集。 輸出資料集指定 hello**排程**hello 預存程序活動 （每小時、 每週、 每月等）。 <br/><br/>hello 輸出資料集必須使用**連結服務**參考 tooan Azure SQL Database 或 Azure SQL 資料倉儲或您想在其中 hello toorun 預存程序的 SQL Server 資料庫。 <br/><br/>hello 輸出資料集可以做為方法 toopass hello hello 預存程序的結果進行後續處理另一個活動 ([鏈結活動](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)hello 管線中。 不過，Data Factory 不會自動寫入預存程序 toothis 資料集的 hello 輸出。 它是 hello 預存程序 hello 輸出資料集指向該寫入 tooa SQL 資料表。 <br/><br/>在某些情況下，可以是 hello 輸出資料集**空資料集**，用僅執行 hello toospecify hello 排程預存程序活動。 |是 |
| storedProcedureName |指定 hello Azure SQL database 或 Azure SQL 資料倉儲或 SQL Server 由 hello 輸出資料表中使用的 hello 連結服務的資料庫中的 hello hello 預存程序名稱。 |是 |
| storedProcedureParameters |指定預存程序參數的值。 如果您需要 toopass null 參數，使用 hello 語法:"param1": null （所有大小寫）。 請參閱下列有關使用這個屬性的範例 toolearn hello。 |否 |

## <a name="passing-a-static-value"></a>傳遞靜態值
現在，讓我們考慮 hello 資料表包含名稱為 '文件範例' 的靜態值中的 新增另一個名為 '案例' 的資料行。

![範例資料 2](./media/data-factory-stored-proc-activity/sample-data-2.png)

**資料表：**

```SQL
CREATE TABLE dbo.sampletable2
(
    Id uniqueidentifier,
    datetimestamp nvarchar(127),
    scenario nvarchar(127)
)
GO

CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable2(Id);
```

**預存程序：**

```SQL
CREATE PROCEDURE sp_sample2 @DateTime nvarchar(127) , @Scenario nvarchar(127)

AS

BEGIN
    INSERT INTO [sampletable2]
    VALUES (newid(), @DateTime, @Scenario)
END
```

現在，傳遞 hello**案例**hello 的參數和 hello 取值預存程序活動。 hello **typeProperties** hello 前面範例看起來像是下列程式碼片段的 hello > 一節：

```JSON
"typeProperties":
{
    "storedProcedureName": "sp_sample",
    "storedProcedureParameters":
    {
        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
        "Scenario": "Document sample"
    }
}
```

**Data Factory 資料集：**

```JSON
{
    "name": "sprocsampleout2",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "sampletable2"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Data Factory 管線**

```JSON
{
    "name": "SprocActivitySamplePipeline2",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample2",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
                        "Scenario": "Document sample"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout2"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
        "start": "2016-10-02T00:00:00Z",
        "end": "2016-10-02T05:00:00Z"
    }
}
```