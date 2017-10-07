---
title: "從內部部署 SQL Server tooSQL Azure 與 Azure Data Factory aaaMove 資料 |Microsoft 文件"
description: "設定撰寫兩個一起移動資料採每日資料庫內部部署與在 hello 雲端的資料移轉活動 ADF 管線。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 36837c83-2015-48be-b850-c4346aa5ae8a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 7f7e78c7a84a259539221d3235b76bb5a3cf9866
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-sql-server-toosql-azure-with-azure-data-factory"></a>將資料從內部部署 SQL server tooSQL Azure 與 Azure Data Factory 移
本主題說明如何透過 Azure Blob 儲存體使用內部部署 SQL Server 資料庫 tooa SQL Azure 資料庫的 toomove 資料 hello Azure 資料處理站 (ADF)。

摘要說明各種選項移動資料 tooan Azure SQL Database 的資料表，請參閱[移動資料 tooan Azure SQL Database 的 Azure Machine Learning](machine-learning-data-science-move-sql-azure.md)。

## <a name="intro"></a>何謂 ADF 簡介： 以及何時應該使用的 toomigrate 資料？
Azure Data Factory 是完全受管理的雲端架構資料整合服務會協調及自動 hello 移動和轉換資料。 hello hello ADF 模型中的重要概念是管線。 管線是活動的邏輯群組，其中每個定義 hello 動作 tooperform hello 包含的資料在資料集內。 連結的服務會使用的 toodefine hello 資訊所需的 Data Factory tooconnect toohello 資料資源。

ADF，與現有的資料處理服務可以組合成是高度可用且管理 hello 雲端中的資料管線。 這些資料管線可以排程的 tooingest、 準備、 轉換、 分析和發行資料時，而且 ADF 管理和協調 hello 複雜資料和處理的相依性。 方案可以快速地建置及部署中的 hello 雲端中，連接越來越多的內部部署和雲端資料來源。

請考慮使用 ADF：

* 當需求 toobe 持續移轉存取兩者的混合式案例中的資料在內部部署和雲端資源
* 當 hello 資料交易性或需求 toobe 修改，或有商務邏輯加入 tooit 時移轉。

ADF 允許 hello 排程和監視使用簡單的 JSON 指令碼管理 hello 定期執行的資料移動作業。 ADF 也有其他功能，例如支援複雜作業。 如需有關 ADF 的詳細資訊，請參閱 hello 文件，網址[Azure 資料處理站 (ADF)](https://azure.microsoft.com/services/data-factory/)。

## <a name="scenario"></a>hello 案例
我們設定了 ADF 管線來組成兩個資料移轉活動。 一起它們之間移動資料每天在內部部署 SQL database 和 Azure SQL Database hello 雲端中。 hello 兩個活動包括：

* 將資料從內部部署 SQL Server 資料庫 tooan Azure Blob 儲存體帳戶複製
* 從 hello Azure Blob 儲存體帳戶 tooan Azure SQL Database 中複製資料。

> [!NOTE]
> hello 示此處已經過修改從 hello hello ADF 小組所提供的教學課程的詳細步驟：[在內部部署來源和資料管理閘道與雲端之間移動資料](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)參考該主題的 toohello 相關章節在適當時提供。
>
>

## <a name="prereqs"></a>必要條件
本教學課程假設您有：

* **Azure 訂用帳戶**。 如果您沒有訂用帳戶，可以註冊 [免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* **Azure 儲存體帳戶**。 您可以使用 Azure 儲存體帳戶將 hello 資料儲存在本教學課程。 如果您沒有 Azure 儲存體帳戶，請參閱 hello[建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)發行項。 建立 hello 儲存體帳戶之後，您會需要 tooobtain hello 帳戶使用 tooaccess hello 儲存體金鑰。 請參閱 [管理儲存體存取金鑰](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys)。
* 存取 tooan **Azure SQL Database**。 如果您必須設定 Azure SQL Database，hello tpoic[開始使用 Microsoft Azure SQL Database](../sql-database/sql-database-get-started.md)如何提供有關 tooprovision Azure SQL Database 的新執行個體。
* 已在本機上安裝和設定 **Azure PowerShell** 。 如需指示，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。

> [!NOTE]
> 此程序使用 hello [Azure 入口網站](https://portal.azure.com/)。
>
>

## <a name="upload-data"></a>上傳 hello 資料 tooyour 內部部署 SQL Server
我們使用 hello [NYC 計程車資料集](http://chriswhong.com/open-data/foil_nyc_taxi/)toodemonstrate hello 移轉程序。 hello NYC 計程車資料集可供使用，如同該文章，在 Azure blob 儲存體中所註明[NYC 計程車資料](http://www.andresmh.com/nyctaxitrips/)。 hello 資料有兩個檔案、 hello trip_data.csv 檔案，其中包含路線詳細資料和 hello trip_far.csv 檔案，其中包含針對每個往返支付 hello 價位的詳細資料。 這些檔案的範例和說明都會在 [NYC 計程車車程資料集說明](machine-learning-data-science-process-sql-walkthrough.md#dataset)中提供。

您可以調整此處提供您自己的資料集 tooa hello 程序，或遵循 hello 步驟所述使用 hello NYC 計程車資料集。 tooupload hello NYC 計程車資料集在內部部署 SQL Server 資料庫，請遵循 hello 程序中所述[大量匯入資料到 SQL Server 資料庫](machine-learning-data-science-process-sql-walkthrough.md#dbload)。 這些指示適用於 SQL Server 在 Azure 虛擬機器上，但是 hello 程序上傳內部部署 SQL Server 是的 toohello hello 相同。

## <a name="create-adf"></a> 建立 Azure Data Factory
hello 指示用於建立新的 Azure Data Factory 和資源群組中 hello [Azure 入口網站](https://portal.azure.com/)提供[建立 Azure Data Factory](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory)。 名稱 hello ADF m_pdoctemplate *adfdsp*與名稱 hello 資源群組建立*adfdsprg*。

## <a name="install-and-configure-up-hello-data-management-gateway"></a>安裝和設定 hello 資料管理閘道器
tooenable 管線在內部部署 SQL Server 與 Azure data factory toowork，您需要 tooadd 它做為連結的服務 toohello 資料 factory。 toocreate 在內部部署 SQL server 的連結服務，您必須：

* 下載並安裝到 hello 在內部部署電腦上的 Microsoft 資料管理閘道器。
* 設定 hello 在內部部署資料來源 toouse hello 閘道的 hello 連結服務。

hello 資料管理閘道器序列化和還原序列化 hello hello 其裝載所在的電腦上的來源和接收資料。

如需關於資料管理閘道的設定指示及詳細資料，請參閱 [利用資料管理閘道在內部部署來源和雲端之間移動資料](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)

## <a name="adflinkedservices"></a>建立連結的服務 tooconnect toohello 資料資源
連結的服務定義所需的 Azure Data Factory tooconnect tooa 資料資源的 hello 資訊。 hello 用於建立連結的服務的逐步程序中提供[建立連結的服務](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services)。

此案例中的三個資源都必須使用連結服務。

1. [內部部署 SQL Server 的連結服務](#adf-linked-service-onprem-sql)
2. [Azure Blob 儲存體的連結服務](#adf-linked-service-blob-store)
3. [Azure SQL Database 的連結服務](#adf-linked-service-azure-sql)

### <a name="adf-linked-service-onprem-sql"></a>內部部署 SQL Server 資料庫的連結服務
hello toocreate hello 連結的服務內部部署 SQL Server:

* 按一下 hello**資料存放區**在 Azure 傳統入口網站上的 hello ADF 登陸頁面
* 選取**SQL** ，然後輸入 hello *username*和*密碼*認證 hello 內部部署 SQL Server。 您需要為 tooenter hello servername**完整的 servername 反斜線執行個體名稱 (servername\instancename)**。 名稱 hello 連結服務*adfonpremsql*。

### <a name="adf-linked-service-blob-store"></a>Blob 的連結服務
toocreate hello hello Azure Blob 儲存體帳戶的連結的服務：

* 按一下 hello**資料存放區**在 Azure 傳統入口網站上的 hello ADF 登陸頁面
* 選取 [Azure 儲存體帳戶] 
* 輸入 hello Azure Blob 儲存體帳戶金鑰和容器名稱。 名稱 hello 連結的服務*adfds*。

### <a name="adf-linked-service-azure-sql"></a>Azure SQL Database 的連結服務
toocreate hello hello Azure SQL Database 的連結的服務：

* 按一下 hello**資料存放區**在 Azure 傳統入口網站上的 hello ADF 登陸頁面
* 選取**Azure SQL** ，然後輸入 hello *username*和*密碼*hello Azure SQL Database 的認證。 hello *username*必須指定為* user@servername *。   

## <a name="adf-tables"></a>定義和建立資料表 toospecify tooaccess hello 資料集的方式
建立以 hello 下列指令碼為基礎的程序指定 hello 結構、 位置和可用性的 hello 資料集的資料表。 JSON 檔案是使用的 toodefine hello 資料表。 如需有關這些檔案的 hello 結構的詳細資訊，請參閱[資料集](../data-factory/data-factory-create-datasets.md)。

> [!NOTE]
> 您應該執行 hello `Add-AzureAccount` cmdlet 然後才執行 hello[新增 AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) hello 權限的 Azure 訂用帳戶的 cmdlet tooconfirm 選取 hello 命令執行。 如需此 Cmdlet 的文件，請參閱 [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0)。
>
>

hello 資料表中的 hello JSON 型定義，會使用下列名稱的 hello:

* hello**資料表名稱**hello 在內部部署 SQL server 是*nyctaxi_data*
* hello**容器名稱**在 hello Azure Blob 儲存體帳戶是*containername*  

此 ADF 管線所需的三個資料表定義為：

1. [SQL 內部部署資料表](#adf-table-onprem-sql)
2. [Blob 資料表 ](#adf-table-blob-store)
3. [SQL Azure 資料表](#adf-table-azure-sql)

> [!NOTE]
> 這些程序會使用 Azure PowerShell toodefine，並建立 hello ADF 活動。 但是，這些工作也可以完成使用 hello Azure 入口網站。 如需詳細資訊，請參閱[建立資料集](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets)。
>
>

### <a name="adf-table-onprem-sql"></a>SQL 內部部署資料表
hello hello 資料表定義內部 hello 下列 JSON 檔案中指定 SQL Server:

        {
            "name": "OnPremSQLTable",
            "properties":
            {
                "location":
                {
                "type": "OnPremisesSqlServerTableLocation",
                "tableName": "nyctaxi_data",
                "linkedServiceName": "adfonpremsql"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1,   
                "waitOnExternal":
                {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
                }

                }
            }
        }

hello 資料行名稱，並沒有包含在內。 您可以子選取 hello 資料行名稱上的命令包含以下 (詳細資料] 核取 hello [ADF 文件](../data-factory/data-factory-data-movement-activities.md)主題。

將 hello hello 資料表 JSON 定義複製到檔案，稱為*onpremtabledef.json*檔案，並將它儲存 tooa 已知位置 (這裡假設 toobe *C:\temp\onpremtabledef.json*)。 建立下列 Azure PowerShell cmdlet 的 hello 與 ADF hello 資料表：

    New-AzureDataFactoryTable -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp –File C:\temp\onpremtabledef.json


### <a name="adf-table-blob-store"></a>Blob 資料表
Hello 的 hello 資料表定義輸出 blob 位置中 （這會對應 hello 內嵌的資料從內部部署 tooAzure blob） 的 hello 下列：

        {
            "name": "OutputBlobTable",
            "properties":
            {
                "location":
                {
                "type": "AzureBlobLocation",
                "folderPath": "containername",
                "format":
                {
                "type": "TextFormat",
                "columnDelimiter": "\t"
                },
                "linkedServiceName": "adfds"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1
                }
            }
        }

將 hello hello 資料表 JSON 定義複製到檔案，稱為*bloboutputtabledef.json*檔案，並將它儲存 tooa 已知位置 (這裡假設 toobe *C:\temp\bloboutputtabledef.json*)。 建立下列 Azure PowerShell cmdlet 的 hello 與 ADF hello 資料表：

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\bloboutputtabledef.json  

### <a name="adf-table-azure-sq"></a>SQL Azure 資料表
SQL Azure 輸出的 hello 的 hello 資料表定義位於 hello 下列 （此結構描述對應來自 hello blob 的 hello 資料）：

    {
        "name": "OutputSQLAzureTable",
        "properties":
        {
            "structure":
            [
                { "name": "column1", type": "String"},
                { "name": "column2", type": "String"}                
            ],
            "location":
            {
                "type": "AzureSqlTableLocation",
                "tableName": "your_db_name",
                "linkedServiceName": "adfdssqlazure_linked_servicename"
            },
            "availability":
            {
                "frequency": "Day",
                "interval": 1            
            }
        }
    }

將 hello hello 資料表 JSON 定義複製到檔案，稱為*AzureSqlTable.json*檔案，並將它儲存 tooa 已知位置 (這裡假設 toobe *C:\temp\AzureSqlTable.json*)。 建立下列 Azure PowerShell cmdlet 的 hello 與 ADF hello 資料表：

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\AzureSqlTable.json  


## <a name="adf-pipeline"></a>定義和建立 hello 管線
指定屬於 toohello hello 活動管線，並且使用下列指令碼為基礎的程序的 hello 建立 hello 管線。 在 JSON 檔案是使用的 toodefine hello 管線屬性。

* hello 指令碼會假設該 hello**管線名稱**是*AMLDSProcessPipeline*。
* 也請注意，我們設定的每日為基礎，並使用 hello 預設執行 hello 工作時間 (12 am UTC) 上執行的 hello 管線 toobe hello 週期性。

> [!NOTE]
> hello 下列程序使用 Azure PowerShell toodefine 並建立 hello ADF 管線。 但是，此工作也可以透過 Azure 入口網站來完成。 如需詳細資訊，請參閱[建立管線](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline)。
>
>

使用 hello 資料表定義前面，提供 hello 管線定義 hello ADF 的指定方式如下：

        {
            "name": "AMLDSProcessPipeline",
            "properties":
            {
                "description" : "This pipeline has one Copy activity that copies data from an on-premises SQL tooAzure blob",
                 "activities":
                [
                    {
                        "name": "CopyFromSQLtoBlob",
                        "description": "Copy data from on-premises SQL server tooblob",     
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OnPremSQLTable"} ],
                        "outputs": [ {"name": "OutputBlobTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "SqlSource",
                                "sqlReaderQuery": "select * from nyctaxi_data"
                            },
                            "sink":
                            {
                                "type": "BlobSink"
                            }   
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 0,
                            "timeout": "01:00:00"
                        }       

                     },

                    {
                        "name": "CopyFromBlobtoSQLAzure",
                        "description": "Push data tooSql Azure",        
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OutputBlobTable"} ],
                        "outputs": [ {"name": "OutputSQLAzureTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "BlobSource"
                            },
                            "sink":
                            {
                                "type": "SqlSink",
                                "WriteBatchTimeout": "00:5:00",                
                            }            
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 2,
                            "timeout": "02:00:00"
                        }
                     }
                ]
            }
        }

將 hello 管線的此 JSON 定義複製到檔案，稱為*pipelinedef.json*檔案，並將它儲存 tooa 已知位置 (這裡假設 toobe *C:\temp\pipelinedef.json*)。 建立下列 Azure PowerShell cmdlet 的 hello 與 ADF hello 管線：

    New-AzureDataFactoryPipeline  -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\pipelinedef.json

確認您可以看到 hello 管線在 hello ADF hello Azure 傳統入口網站中的顯示如下所示 （當您按一下 hello 圖表）

![ADF 管線](media/machine-learning-data-science-move-sql-azure-adf/DJP1kji.png)

## <a name="adf-pipeline-start"></a>啟動 hello 管線
hello 管線現在可以執行使用 hello 下列命令：

    Set-AzureDataFactoryPipelineActivePeriod -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp -StartDateTime startdateZ –EndDateTime enddateZ –Name AMLDSProcessPipeline

hello *startdate*和*enddate*需要 toobe 取代為您想要的 hello 管線 toorun hello 實際日期的參數值。

一旦 hello 管線執行時，您應該能夠 toosee hello 資料都會顯示在所選 hello blob，每日的一個檔案的 hello 容器。

請注意，我們不運用相當 hello 以累加方式 ADF toopipe 資料所提供的功能。 如需有關如何 toodo 這和其他功能提供的 ADF，請參閱 hello [ADF 文件](https://azure.microsoft.com/services/data-factory/)。
