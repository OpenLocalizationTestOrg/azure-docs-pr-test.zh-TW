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
# <a name="datasets-in-azure-data-factory"></a><span data-ttu-id="8c88c-104">Azure Data Factory 中的資料集</span><span class="sxs-lookup"><span data-stu-id="8c88c-104">Datasets in Azure Data Factory</span></span>
<span data-ttu-id="8c88c-105">本文說明什麼是資料集、如何以 JSON 格式定義它們，以及如何在 Azure Data Factory 管線中使用它們。</span><span class="sxs-lookup"><span data-stu-id="8c88c-105">This article describes what datasets are, how they are defined in JSON format, and how they are used in Azure Data Factory pipelines.</span></span> <span data-ttu-id="8c88c-106">它提供有關每個區段 （例如，結構、 可用性和原則） 的詳細資料 hello 資料集 JSON 定義中。</span><span class="sxs-lookup"><span data-stu-id="8c88c-106">It provides details about each section (for example, structure, availability, and policy) in hello dataset JSON definition.</span></span> <span data-ttu-id="8c88c-107">hello 發行項也提供範例使用 hello**位移**， **anchorDateTime**，和**樣式**資料集 JSON 定義中的屬性。</span><span class="sxs-lookup"><span data-stu-id="8c88c-107">hello article also provides examples for using hello **offset**, **anchorDateTime**, and **style** properties in a dataset JSON definition.</span></span>

> [!NOTE]
> <span data-ttu-id="8c88c-108">如果您是新 tooData 處理站，請參閱[簡介 tooAzure Data Factory](data-factory-introduction.md)的概觀。</span><span class="sxs-lookup"><span data-stu-id="8c88c-108">If you are new tooData Factory, see [Introduction tooAzure Data Factory](data-factory-introduction.md) for an overview.</span></span> <span data-ttu-id="8c88c-109">如果您沒有建立 data factory 的實際操作體驗，您可以進一步了解所讀取的 hello[資料轉換的教學課程](data-factory-build-your-first-pipeline.md)和 hello[資料移動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="8c88c-109">If you do not have hands-on experience with creating data factories, you can gain a better understanding by reading hello [data transformation tutorial](data-factory-build-your-first-pipeline.md) and hello [data movement tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

## <a name="overview"></a><span data-ttu-id="8c88c-110">概觀</span><span class="sxs-lookup"><span data-stu-id="8c88c-110">Overview</span></span>
<span data-ttu-id="8c88c-111">資料處理站可以有一或多個管線。</span><span class="sxs-lookup"><span data-stu-id="8c88c-111">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="8c88c-112">「管線」是一起執行某個工作的「活動」所組成的邏輯群組。</span><span class="sxs-lookup"><span data-stu-id="8c88c-112">A **pipeline** is a logical grouping of **activities** that together perform a task.</span></span> <span data-ttu-id="8c88c-113">在管線中的 hello 活動定義動作 tooperform 對您的資料。</span><span class="sxs-lookup"><span data-stu-id="8c88c-113">hello activities in a pipeline define actions tooperform on your data.</span></span> <span data-ttu-id="8c88c-114">例如，您可能會使用複製活動 toocopy 資料從內部部署 SQL Server tooAzure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="8c88c-114">For example, you might use a copy activity toocopy data from an on-premises SQL Server tooAzure Blob storage.</span></span> <span data-ttu-id="8c88c-115">然後，您可以使用 Azure HDInsight 叢集 tooprocess 資料執行 Hive 指令碼，從 Blob 儲存體 tooproduce 輸出資料的 Hive 活動。</span><span class="sxs-lookup"><span data-stu-id="8c88c-115">Then, you might use a Hive activity that runs a Hive script on an Azure HDInsight cluster tooprocess data from Blob storage tooproduce output data.</span></span> <span data-ttu-id="8c88c-116">最後，您可能會使用第二個複製活動 toocopy hello 輸出資料 tooAzure SQL 資料倉儲、 報告建置方案的商業智慧 (BI) 之上。</span><span class="sxs-lookup"><span data-stu-id="8c88c-116">Finally, you might use a second copy activity toocopy hello output data tooAzure SQL Data Warehouse, on top of which business intelligence (BI) reporting solutions are built.</span></span> <span data-ttu-id="8c88c-117">如需有關管線和活動的詳細資訊，請參閱 [Azure Data Factory 中的管線及活動](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="8c88c-117">For more information about pipelines and activities, see [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md).</span></span>

<span data-ttu-id="8c88c-118">一個活動可以接受零個或多個輸入「資料集」，並且會產生一個或多個輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="8c88c-118">An activity can take zero or more input **datasets**, and produce one or more output datasets.</span></span> <span data-ttu-id="8c88c-119">輸入資料集代表 hello hello 管線中活動的輸入和輸出資料集代表 hello hello 活動的輸出。</span><span class="sxs-lookup"><span data-stu-id="8c88c-119">An input dataset represents hello input for an activity in hello pipeline, and an output dataset represents hello output for hello activity.</span></span> <span data-ttu-id="8c88c-120">資料集可識別資料表、檔案、資料夾和文件等各種資料存放區中的資料。</span><span class="sxs-lookup"><span data-stu-id="8c88c-120">Datasets identify data within different data stores, such as tables, files, folders, and documents.</span></span> <span data-ttu-id="8c88c-121">比方說，Azure Blob 資料集指定 hello blob 容器和資料夾從哪些 hello 管線應該讀取 hello 資料的 Blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="8c88c-121">For example, an Azure Blob dataset specifies hello blob container and folder in Blob storage from which hello pipeline should read hello data.</span></span> 

<span data-ttu-id="8c88c-122">您建立資料集之前，先建立**連結服務**toolink 資料儲存 toohello 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="8c88c-122">Before you create a dataset, create a **linked service** toolink your data store toohello data factory.</span></span> <span data-ttu-id="8c88c-123">連結的服務非常類似連接字串，定義所需的 Data Factory tooconnect tooexternal 資源 hello 連接資訊中。</span><span class="sxs-lookup"><span data-stu-id="8c88c-123">Linked services are much like connection strings, which define hello connection information needed for Data Factory tooconnect tooexternal resources.</span></span> <span data-ttu-id="8c88c-124">資料集來識別連結的 hello 資料存放區，例如 SQL 資料表、 檔案、 資料夾和文件內的資料。</span><span class="sxs-lookup"><span data-stu-id="8c88c-124">Datasets identify data within hello linked data stores, such as SQL tables, files, folders, and documents.</span></span> <span data-ttu-id="8c88c-125">例如，Azure 儲存體連結服務的連結儲存體帳戶 toohello data factory。</span><span class="sxs-lookup"><span data-stu-id="8c88c-125">For example, an Azure Storage linked service links a storage account toohello data factory.</span></span> <span data-ttu-id="8c88c-126">Azure Blob 資料集代表 hello blob 容器，並包含處理 hello 輸入的 blob toobe hello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="8c88c-126">An Azure Blob dataset represents hello blob container and hello folder that contains hello input blobs toobe processed.</span></span> 

<span data-ttu-id="8c88c-127">以下是一個範例案例。</span><span class="sxs-lookup"><span data-stu-id="8c88c-127">Here is a sample scenario.</span></span> <span data-ttu-id="8c88c-128">從 Blob 儲存體 tooa SQL database 的 toocopy 資料，建立兩個連結的服務： Azure 儲存體和 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="8c88c-128">toocopy data from Blob storage tooa SQL database, you create two linked services: Azure Storage and Azure SQL Database.</span></span> <span data-ttu-id="8c88c-129">接著，建立兩個資料集： Azure Blob 資料集 （也就是 toohello Azure 儲存體連結服務） 和 Azure SQL 資料表的資料集 （也就是 toohello 連結的 Azure SQL Database 服務）。</span><span class="sxs-lookup"><span data-stu-id="8c88c-129">Then, create two datasets: Azure Blob dataset (which refers toohello Azure Storage linked service) and Azure SQL Table dataset (which refers toohello Azure SQL Database linked service).</span></span> <span data-ttu-id="8c88c-130">hello Azure 儲存體和 Azure SQL Database 已連結的服務包含 Data Factory 分別使用在執行階段 tooconnect tooyour Azure 儲存體和 Azure SQL Database 的連接字串。</span><span class="sxs-lookup"><span data-stu-id="8c88c-130">hello Azure Storage and Azure SQL Database linked services contain connection strings that Data Factory uses at runtime tooconnect tooyour Azure Storage and Azure SQL Database, respectively.</span></span> <span data-ttu-id="8c88c-131">hello Azure Blob 資料集指定 hello blob 容器，並包含您的 Blob 儲存體中的 hello 輸入的 blob 的 blob 資料夾。</span><span class="sxs-lookup"><span data-stu-id="8c88c-131">hello Azure Blob dataset specifies hello blob container and blob folder that contains hello input blobs in your Blob storage.</span></span> <span data-ttu-id="8c88c-132">hello Azure SQL 資料表的資料集指定 SQL 資料庫 toowhich hello 資料中的 hello SQL 資料表 toobe 複製。</span><span class="sxs-lookup"><span data-stu-id="8c88c-132">hello Azure SQL Table dataset specifies hello SQL table in your SQL database toowhich hello data is toobe copied.</span></span>

<span data-ttu-id="8c88c-133">hello 下圖顯示 hello 管線、 活動、 資料集和連結的服務之間的關聯性 Data Factory 中：</span><span class="sxs-lookup"><span data-stu-id="8c88c-133">hello following diagram shows hello relationships among pipeline, activity, dataset, and linked service in Data Factory:</span></span> 

![管線、活動、資料集、已連結的服務之間的關聯性](media/data-factory-create-datasets/relationship-between-data-factory-entities.png)

## <a name="dataset-json"></a><span data-ttu-id="8c88c-135">資料集 JSON</span><span class="sxs-lookup"><span data-stu-id="8c88c-135">Dataset JSON</span></span>
<span data-ttu-id="8c88c-136">Data Factory 中的資料集會以 JSON 格式定義如下：</span><span class="sxs-lookup"><span data-stu-id="8c88c-136">A dataset in Data Factory is defined in JSON format as follows:</span></span>

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

<span data-ttu-id="8c88c-137">hello 下表描述上方 JSON hello 中的屬性：</span><span class="sxs-lookup"><span data-stu-id="8c88c-137">hello following table describes properties in hello above JSON:</span></span>   

| <span data-ttu-id="8c88c-138">屬性</span><span class="sxs-lookup"><span data-stu-id="8c88c-138">Property</span></span> | <span data-ttu-id="8c88c-139">說明</span><span class="sxs-lookup"><span data-stu-id="8c88c-139">Description</span></span> | <span data-ttu-id="8c88c-140">必要</span><span class="sxs-lookup"><span data-stu-id="8c88c-140">Required</span></span> | <span data-ttu-id="8c88c-141">預設值</span><span class="sxs-lookup"><span data-stu-id="8c88c-141">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8c88c-142">名稱</span><span class="sxs-lookup"><span data-stu-id="8c88c-142">name</span></span> |<span data-ttu-id="8c88c-143">Hello 資料集的名稱。</span><span class="sxs-lookup"><span data-stu-id="8c88c-143">Name of hello dataset.</span></span> <span data-ttu-id="8c88c-144">請參閱 [Azure Data Factory - 命名規則](data-factory-naming-rules.md) ，以了解命名規則。</span><span class="sxs-lookup"><span data-stu-id="8c88c-144">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="8c88c-145">是</span><span class="sxs-lookup"><span data-stu-id="8c88c-145">Yes</span></span> |<span data-ttu-id="8c88c-146">NA</span><span class="sxs-lookup"><span data-stu-id="8c88c-146">NA</span></span> |
| <span data-ttu-id="8c88c-147">類型</span><span class="sxs-lookup"><span data-stu-id="8c88c-147">type</span></span> |<span data-ttu-id="8c88c-148">hello 資料集的類型。</span><span class="sxs-lookup"><span data-stu-id="8c88c-148">Type of hello dataset.</span></span> <span data-ttu-id="8c88c-149">指定一個支援的 Data Factory 的 hello 類型 (例如： AzureBlob、 AzureSqlTable)。</span><span class="sxs-lookup"><span data-stu-id="8c88c-149">Specify one of hello types supported by Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <br/><br/><span data-ttu-id="8c88c-150">如需詳細資料，請參閱[資料集類型](#Type)。</span><span class="sxs-lookup"><span data-stu-id="8c88c-150">For details, see [Dataset type](#Type).</span></span> |<span data-ttu-id="8c88c-151">是</span><span class="sxs-lookup"><span data-stu-id="8c88c-151">Yes</span></span> |<span data-ttu-id="8c88c-152">NA</span><span class="sxs-lookup"><span data-stu-id="8c88c-152">NA</span></span> |
| <span data-ttu-id="8c88c-153">structure</span><span class="sxs-lookup"><span data-stu-id="8c88c-153">structure</span></span> |<span data-ttu-id="8c88c-154">Hello 資料集的結構描述。</span><span class="sxs-lookup"><span data-stu-id="8c88c-154">Schema of hello dataset.</span></span><br/><br/><span data-ttu-id="8c88c-155">如需詳細資料，請參閱[資料集結構](#Structure)。</span><span class="sxs-lookup"><span data-stu-id="8c88c-155">For details, see [Dataset structure](#Structure).</span></span> |<span data-ttu-id="8c88c-156">否</span><span class="sxs-lookup"><span data-stu-id="8c88c-156">No</span></span> |<span data-ttu-id="8c88c-157">NA</span><span class="sxs-lookup"><span data-stu-id="8c88c-157">NA</span></span> |
| <span data-ttu-id="8c88c-158">typeProperties</span><span class="sxs-lookup"><span data-stu-id="8c88c-158">typeProperties</span></span> | <span data-ttu-id="8c88c-159">hello 類型屬性都不同的每個型別 (例如： Azure Blob、 Azure SQL 資料表)。</span><span class="sxs-lookup"><span data-stu-id="8c88c-159">hello type properties are different for each type (for example: Azure Blob, Azure SQL table).</span></span> <span data-ttu-id="8c88c-160">如需支援的 hello 類型和其屬性的詳細資訊，請參閱[資料集類型](#Type)。</span><span class="sxs-lookup"><span data-stu-id="8c88c-160">For details on hello supported types and their properties, see [Dataset type](#Type).</span></span> |<span data-ttu-id="8c88c-161">是</span><span class="sxs-lookup"><span data-stu-id="8c88c-161">Yes</span></span> |<span data-ttu-id="8c88c-162">NA</span><span class="sxs-lookup"><span data-stu-id="8c88c-162">NA</span></span> |
| <span data-ttu-id="8c88c-163">external</span><span class="sxs-lookup"><span data-stu-id="8c88c-163">external</span></span> | <span data-ttu-id="8c88c-164">布林值旗標 toospecify，是否與否，資料 factory 管線所明確產生資料集。</span><span class="sxs-lookup"><span data-stu-id="8c88c-164">Boolean flag toospecify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> <span data-ttu-id="8c88c-165">Hello 活動的輸入資料集不產生 hello 目前的管線時，如果設定此旗標 tootrue。</span><span class="sxs-lookup"><span data-stu-id="8c88c-165">If hello input dataset for an activity is not produced by hello current pipeline, set this flag tootrue.</span></span> <span data-ttu-id="8c88c-166">Hello 管線中設定這個旗標 tootrue，hello hello 第一個活動的輸入資料集。</span><span class="sxs-lookup"><span data-stu-id="8c88c-166">Set this flag tootrue for hello input dataset of hello first activity in hello pipeline.</span></span>  |<span data-ttu-id="8c88c-167">否</span><span class="sxs-lookup"><span data-stu-id="8c88c-167">No</span></span> |<span data-ttu-id="8c88c-168">false</span><span class="sxs-lookup"><span data-stu-id="8c88c-168">false</span></span> |
| <span data-ttu-id="8c88c-169">Availability</span><span class="sxs-lookup"><span data-stu-id="8c88c-169">availability</span></span> | <span data-ttu-id="8c88c-170">定義處理期間，（比方說，每小時或每天） hello 或 hello 配量 hello 資料集實際執行的模型。</span><span class="sxs-lookup"><span data-stu-id="8c88c-170">Defines hello processing window (for example, hourly or daily) or hello slicing model for hello dataset production.</span></span> <span data-ttu-id="8c88c-171">活動執行取用和產生的每個資料單位稱為資料配量。</span><span class="sxs-lookup"><span data-stu-id="8c88c-171">Each unit of data consumed and produced by an activity run is called a data slice.</span></span> <span data-ttu-id="8c88c-172">如果輸出資料集中的 hello 可用性集 toodaily （頻率為一天，間隔為 1），每天產生配量。</span><span class="sxs-lookup"><span data-stu-id="8c88c-172">If hello availability of an output dataset is set toodaily (frequency - Day, interval - 1), a slice is produced daily.</span></span> <br/><br/><span data-ttu-id="8c88c-173">如需詳細資料，請參閱[資料集可用性](#Availability)。</span><span class="sxs-lookup"><span data-stu-id="8c88c-173">For details, see [Dataset availability](#Availability).</span></span> <br/><br/><span data-ttu-id="8c88c-174">如需詳細資訊，hello 資料集上配量模型，請參閱 hello[排程與執行](data-factory-scheduling-and-execution.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="8c88c-174">For details on hello dataset slicing model, see hello [Scheduling and execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="8c88c-175">是</span><span class="sxs-lookup"><span data-stu-id="8c88c-175">Yes</span></span> |<span data-ttu-id="8c88c-176">NA</span><span class="sxs-lookup"><span data-stu-id="8c88c-176">NA</span></span> |
| <span data-ttu-id="8c88c-177">原則</span><span class="sxs-lookup"><span data-stu-id="8c88c-177">policy</span></span> |<span data-ttu-id="8c88c-178">定義 hello 準則或 hello hello 資料集配量，都必須符合的條件。</span><span class="sxs-lookup"><span data-stu-id="8c88c-178">Defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="8c88c-179">如需詳細資訊，請參閱 hello[資料集原則](#Policy)> 一節。</span><span class="sxs-lookup"><span data-stu-id="8c88c-179">For details, see hello [Dataset policy](#Policy) section.</span></span> |<span data-ttu-id="8c88c-180">否</span><span class="sxs-lookup"><span data-stu-id="8c88c-180">No</span></span> |<span data-ttu-id="8c88c-181">NA</span><span class="sxs-lookup"><span data-stu-id="8c88c-181">NA</span></span> |

## <a name="dataset-example"></a><span data-ttu-id="8c88c-182">資料集範例</span><span class="sxs-lookup"><span data-stu-id="8c88c-182">Dataset example</span></span>
<span data-ttu-id="8c88c-183">在下列範例的 hello，hello 資料集代表名為的資料表**MyTable** SQL 資料庫中。</span><span class="sxs-lookup"><span data-stu-id="8c88c-183">In hello following example, hello dataset represents a table named **MyTable** in a SQL database.</span></span>

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

<span data-ttu-id="8c88c-184">請注意下列點 hello:</span><span class="sxs-lookup"><span data-stu-id="8c88c-184">Note hello following points:</span></span>

* <span data-ttu-id="8c88c-185">**型別**tooAzureSqlTable 設定。</span><span class="sxs-lookup"><span data-stu-id="8c88c-185">**type** is set tooAzureSqlTable.</span></span>
* <span data-ttu-id="8c88c-186">**tableName** type 屬性 （特定 tooAzureSqlTable 類型） 設定 tooMyTable。</span><span class="sxs-lookup"><span data-stu-id="8c88c-186">**tableName** type property (specific tooAzureSqlTable type) is set tooMyTable.</span></span>
* <span data-ttu-id="8c88c-187">**linkedServiceName**參考 tooa 連結服務類型 AzureSqlDatabase hello 下一步的 JSON 片段中定義。</span><span class="sxs-lookup"><span data-stu-id="8c88c-187">**linkedServiceName** refers tooa linked service of type AzureSqlDatabase, which is defined in hello next JSON snippet.</span></span> 
* <span data-ttu-id="8c88c-188">**可用性頻率**設定 tooDay，和**間隔**too1 設定。</span><span class="sxs-lookup"><span data-stu-id="8c88c-188">**availability frequency** is set tooDay, and **interval** is set too1.</span></span> <span data-ttu-id="8c88c-189">這表示每天產生該 hello 資料集配量。</span><span class="sxs-lookup"><span data-stu-id="8c88c-189">This means that hello dataset slice is produced daily.</span></span>  

<span data-ttu-id="8c88c-190">**AzureSqlLinkedService** 定義如下︰</span><span class="sxs-lookup"><span data-stu-id="8c88c-190">**AzureSqlLinkedService** is defined as follows:</span></span>

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

<span data-ttu-id="8c88c-191">在 hello 前面 JSON 片段：</span><span class="sxs-lookup"><span data-stu-id="8c88c-191">In hello preceding JSON snippet:</span></span>

* <span data-ttu-id="8c88c-192">**型別**tooAzureSqlDatabase 設定。</span><span class="sxs-lookup"><span data-stu-id="8c88c-192">**type** is set tooAzureSqlDatabase.</span></span>
* <span data-ttu-id="8c88c-193">**connectionString**型別屬性會指定資訊 tooconnect tooa SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="8c88c-193">**connectionString** type property specifies information tooconnect tooa SQL database.</span></span>  

<span data-ttu-id="8c88c-194">如您所見，hello 連結的服務定義如何 tooconnect tooa SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="8c88c-194">As you can see, hello linked service defines how tooconnect tooa SQL database.</span></span> <span data-ttu-id="8c88c-195">hello 資料集定義哪些資料表是用做為輸入和輸出管線中的 hello 活動。</span><span class="sxs-lookup"><span data-stu-id="8c88c-195">hello dataset defines what table is used as an input and output for hello activity in a pipeline.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="8c88c-196">除非正在 hello 管線所產生的資料集，應該標記為**外部**。</span><span class="sxs-lookup"><span data-stu-id="8c88c-196">Unless a dataset is being produced by hello pipeline, it should be marked as **external**.</span></span> <span data-ttu-id="8c88c-197">此設定通常適用於 tooinputs 的管線中的第一個活動。</span><span class="sxs-lookup"><span data-stu-id="8c88c-197">This setting generally applies tooinputs of first activity in a pipeline.</span></span>   


## <span data-ttu-id="8c88c-198"><a name="Type"></a> 資料集類型</span><span class="sxs-lookup"><span data-stu-id="8c88c-198"><a name="Type"></a> Dataset type</span></span>
<span data-ttu-id="8c88c-199">hello 資料集的 hello 類型取決於您使用的 hello 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="8c88c-199">hello type of hello dataset depends on hello data store you use.</span></span> <span data-ttu-id="8c88c-200">請參閱下表取得一份資料存放區支援的 Data Factory 的 hello。</span><span class="sxs-lookup"><span data-stu-id="8c88c-200">See hello following table for a list of data stores supported by Data Factory.</span></span> <span data-ttu-id="8c88c-201">按一下 資料存放區 toolearn 如何 toocreate 連結的服務，以及該資料的資料集存放區。</span><span class="sxs-lookup"><span data-stu-id="8c88c-201">Click a data store toolearn how toocreate a linked service and a dataset for that data store.</span></span>

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> <span data-ttu-id="8c88c-202">帶有 * 的資料存放區可以位於內部部署環境或 Azure 基礎結構即服務 (IaaS) 上。</span><span class="sxs-lookup"><span data-stu-id="8c88c-202">Data stores with * can be on-premises or on Azure infrastructure as a service (IaaS).</span></span> <span data-ttu-id="8c88c-203">這些資料存放區會要求您 tooinstall[資料管理閘道器](data-factory-data-management-gateway.md)。</span><span class="sxs-lookup"><span data-stu-id="8c88c-203">These data stores require you tooinstall [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>

<span data-ttu-id="8c88c-204">在 hello hello 前一節中的範例，hello 類型 hello 資料集的設定太**AzureSqlTable**。</span><span class="sxs-lookup"><span data-stu-id="8c88c-204">In hello example in hello previous section, hello type of hello dataset is set too**AzureSqlTable**.</span></span> <span data-ttu-id="8c88c-205">同樣地，如果是 Azure Blob 資料集，hello 類型 hello 資料集的設定太**AzureBlob**、 hello 下列 JSON 中所示：</span><span class="sxs-lookup"><span data-stu-id="8c88c-205">Similarly, for an Azure Blob dataset, hello type of hello dataset is set too**AzureBlob**, as shown in hello following JSON:</span></span>

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

## <span data-ttu-id="8c88c-206"><a name="Structure"></a>資料集結構</span><span class="sxs-lookup"><span data-stu-id="8c88c-206"><a name="Structure"></a>Dataset structure</span></span>
<span data-ttu-id="8c88c-207">hello**結構**區段是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="8c88c-207">hello **structure** section is optional.</span></span> <span data-ttu-id="8c88c-208">它會定義 hello hello 資料集的結構描述所包含集合的名稱和資料行的資料類型。</span><span class="sxs-lookup"><span data-stu-id="8c88c-208">It defines hello schema of hello dataset by containing a collection of names and data types of columns.</span></span> <span data-ttu-id="8c88c-209">您使用 hello 結構區段 tooprovide 型別資訊，是使用的 tooconvert 類型，從 hello 來源 toohello 目的地的對應資料行。</span><span class="sxs-lookup"><span data-stu-id="8c88c-209">You use hello structure section tooprovide type information that is used tooconvert types and map columns from hello source toohello destination.</span></span> <span data-ttu-id="8c88c-210">在下列範例的 hello，hello 資料集有三個資料行： `slicetimestamp`， `projectname`，和`pageviews`。</span><span class="sxs-lookup"><span data-stu-id="8c88c-210">In hello following example, hello dataset has three columns: `slicetimestamp`, `projectname`, and `pageviews`.</span></span> <span data-ttu-id="8c88c-211">它們的類型分別是 String、String 及 Decimal。</span><span class="sxs-lookup"><span data-stu-id="8c88c-211">They are of type String, String, and Decimal, respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="8c88c-212">Hello 結構中的每個資料行包含下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="8c88c-212">Each column in hello structure contains hello following properties:</span></span>

| <span data-ttu-id="8c88c-213">屬性</span><span class="sxs-lookup"><span data-stu-id="8c88c-213">Property</span></span> | <span data-ttu-id="8c88c-214">說明</span><span class="sxs-lookup"><span data-stu-id="8c88c-214">Description</span></span> | <span data-ttu-id="8c88c-215">必要</span><span class="sxs-lookup"><span data-stu-id="8c88c-215">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8c88c-216">名稱</span><span class="sxs-lookup"><span data-stu-id="8c88c-216">name</span></span> |<span data-ttu-id="8c88c-217">Hello 資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="8c88c-217">Name of hello column.</span></span> |<span data-ttu-id="8c88c-218">是</span><span class="sxs-lookup"><span data-stu-id="8c88c-218">Yes</span></span> |
| <span data-ttu-id="8c88c-219">類型</span><span class="sxs-lookup"><span data-stu-id="8c88c-219">type</span></span> |<span data-ttu-id="8c88c-220">Hello 資料行資料類型。</span><span class="sxs-lookup"><span data-stu-id="8c88c-220">Data type of hello column.</span></span>  |<span data-ttu-id="8c88c-221">否</span><span class="sxs-lookup"><span data-stu-id="8c88c-221">No</span></span> |
| <span data-ttu-id="8c88c-222">culture</span><span class="sxs-lookup"><span data-stu-id="8c88c-222">culture</span></span> |<span data-ttu-id="8c88c-223">.Hello 類型為.NET 型別時使用的網路基礎的文化特性 toobe:`Datetime`或`Datetimeoffset`。</span><span class="sxs-lookup"><span data-stu-id="8c88c-223">.NET-based culture toobe used when hello type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="8c88c-224">hello 預設值是`en-us`。</span><span class="sxs-lookup"><span data-stu-id="8c88c-224">hello default is `en-us`.</span></span> |<span data-ttu-id="8c88c-225">否</span><span class="sxs-lookup"><span data-stu-id="8c88c-225">No</span></span> |
| <span data-ttu-id="8c88c-226">format</span><span class="sxs-lookup"><span data-stu-id="8c88c-226">format</span></span> |<span data-ttu-id="8c88c-227">格式化字串 toobe hello 類型為.NET 型別時使用：`Datetime`或`Datetimeoffset`。</span><span class="sxs-lookup"><span data-stu-id="8c88c-227">Format string toobe used when hello type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="8c88c-228">否</span><span class="sxs-lookup"><span data-stu-id="8c88c-228">No</span></span> |

<span data-ttu-id="8c88c-229">hello 下列指導方針協助您判斷當 tooinclude 結構的詳細資訊，以及在 hello 哪些 tooinclude**結構**> 一節。</span><span class="sxs-lookup"><span data-stu-id="8c88c-229">hello following guidelines help you determine when tooinclude structure information, and what tooinclude in hello **structure** section.</span></span>

* <span data-ttu-id="8c88c-230">**結構化的資料來源的**，只有當您想要將來源資料行 toosink 資料行對應，而且其名稱不是 hello 相同指定 hello 結構 > 一節。</span><span class="sxs-lookup"><span data-stu-id="8c88c-230">**For structured data sources**, specify hello structure section only if you want map source columns toosink columns, and their names are not hello same.</span></span> <span data-ttu-id="8c88c-231">這種結構化的資料來源會儲存以及 hello 資料本身的資料結構描述和類型資訊。</span><span class="sxs-lookup"><span data-stu-id="8c88c-231">This kind of structured data source stores data schema and type information along with hello data itself.</span></span> <span data-ttu-id="8c88c-232">結構化資料來源的範例包括 SQL Server、Oracle 及 Azure 資料表。</span><span class="sxs-lookup"><span data-stu-id="8c88c-232">Examples of structured data sources include SQL Server, Oracle, and Azure table.</span></span> 
  
    <span data-ttu-id="8c88c-233">因為型別資訊已提供結構化的資料來源，您不應該包含型別資訊包括 hello 結構區段時。</span><span class="sxs-lookup"><span data-stu-id="8c88c-233">As type information is already available for structured data sources, you should not include type information when you do include hello structure section.</span></span>
* <span data-ttu-id="8c88c-234">**在讀取的資料來源 （特別是 Blob 儲存） 上的結構描述**，您可以選擇 toostore 資料，而不儲存任何結構描述或型別資訊與 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="8c88c-234">**For schema on read data sources (specifically Blob storage)**, you can choose toostore data without storing any schema or type information with hello data.</span></span> <span data-ttu-id="8c88c-235">當您想 toomap 來源資料行 toosink 資料行時，針對這些類型的資料來源，包含結構。</span><span class="sxs-lookup"><span data-stu-id="8c88c-235">For these types of data sources, include structure when you want toomap source columns toosink columns.</span></span> <span data-ttu-id="8c88c-236">Hello 資料集是複製活動中，輸入，來源資料集的資料類型應該是 hello 接收已轉換的 toonative 類型時，也包含結構。</span><span class="sxs-lookup"><span data-stu-id="8c88c-236">Also include structure when hello dataset is an input for a copy activity, and data types of source dataset should be converted toonative types for hello sink.</span></span> 
    
    <span data-ttu-id="8c88c-237">Data Factory 支援下列值，提供類型資訊，在結構中的 hello: **Int16、 Int32、 Int64、 單一、 Double、 Decimal、 位元組 []、 布林值、 字串、 Guid、 Datetime、 Datetimeoffset 和 Timespan**。</span><span class="sxs-lookup"><span data-stu-id="8c88c-237">Data Factory supports hello following values for providing type information in structure: **Int16, Int32, Int64, Single, Double, Decimal, Byte[], Boolean, String, Guid, Datetime, Datetimeoffset, and Timespan**.</span></span> <span data-ttu-id="8c88c-238">這些值是符合 Common Language Specification (CLS) 規範的 .NET 型類型值。</span><span class="sxs-lookup"><span data-stu-id="8c88c-238">These values are Common Language Specification (CLS)-compliant, .NET-based type values.</span></span>

<span data-ttu-id="8c88c-239">Data Factory 會移動資料的來源資料的資料存放區 tooa 接收資料存放區時，會自動執行類型轉換。</span><span class="sxs-lookup"><span data-stu-id="8c88c-239">Data Factory automatically performs type conversions when moving data from a source data store tooa sink data store.</span></span> 
  

## <a name="dataset-availability"></a><span data-ttu-id="8c88c-240">資料集可用性</span><span class="sxs-lookup"><span data-stu-id="8c88c-240">Dataset availability</span></span>
<span data-ttu-id="8c88c-241">hello**可用性**資料集中的區段會定義 hello 處理 視窗 （例如，每小時、 每天或每週） hello 資料集。</span><span class="sxs-lookup"><span data-stu-id="8c88c-241">hello **availability** section in a dataset defines hello processing window (for example, hourly, daily, or weekly) for hello dataset.</span></span> <span data-ttu-id="8c88c-242">如需有關活動時段的詳細資訊，請參閱[排程和執行](data-factory-scheduling-and-execution.md)。</span><span class="sxs-lookup"><span data-stu-id="8c88c-242">For more information about activity windows, see [Scheduling and execution](data-factory-scheduling-and-execution.md).</span></span>

<span data-ttu-id="8c88c-243">下列可用性一節的 hello 指定 hello 輸出資料集可能是產生每小時、 或 hello 輸入資料集為每小時可用：</span><span class="sxs-lookup"><span data-stu-id="8c88c-243">hello following availability section specifies that hello output dataset is either produced hourly, or hello input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="8c88c-244">如果 hello 管線有 hello 遵循開始和結束時間：</span><span class="sxs-lookup"><span data-stu-id="8c88c-244">If hello pipeline has hello following start and end times:</span></span>  

```json
    "start": "2016-08-25T00:00:00Z",
    "end": "2016-08-25T05:00:00Z",
```

<span data-ttu-id="8c88c-245">hello 輸出資料集則會產生每小時 hello 管線內開始和結束時間。</span><span class="sxs-lookup"><span data-stu-id="8c88c-245">hello output dataset is produced hourly within hello pipeline start and end times.</span></span> <span data-ttu-id="8c88c-246">因此，這個管線會產生五個資料集配量，每個活動時段 (上午 12 點 - 上午 1 點、上午 1 點 - 上午 2 點、上午 2 點 - 上午 3 點、上午 3 點 - 上午 4 點、上午 4 點 - 上午 5 點) 各一個資料集。</span><span class="sxs-lookup"><span data-stu-id="8c88c-246">Therefore, there are five dataset slices produced by this pipeline, one for each activity window (12 AM - 1 AM, 1 AM - 2 AM, 2 AM - 3 AM, 3 AM - 4 AM, 4 AM - 5 AM).</span></span> 

<span data-ttu-id="8c88c-247">hello 下表描述您可以使用 hello 可用性一節中的屬性：</span><span class="sxs-lookup"><span data-stu-id="8c88c-247">hello following table describes properties you can use in hello availability section:</span></span>

| <span data-ttu-id="8c88c-248">屬性</span><span class="sxs-lookup"><span data-stu-id="8c88c-248">Property</span></span> | <span data-ttu-id="8c88c-249">說明</span><span class="sxs-lookup"><span data-stu-id="8c88c-249">Description</span></span> | <span data-ttu-id="8c88c-250">必要</span><span class="sxs-lookup"><span data-stu-id="8c88c-250">Required</span></span> | <span data-ttu-id="8c88c-251">預設值</span><span class="sxs-lookup"><span data-stu-id="8c88c-251">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8c88c-252">frequency</span><span class="sxs-lookup"><span data-stu-id="8c88c-252">frequency</span></span> |<span data-ttu-id="8c88c-253">指定資料集配量實際執行環境的 hello 時間單位。</span><span class="sxs-lookup"><span data-stu-id="8c88c-253">Specifies hello time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="8c88c-254"><b>支援的頻率</b>：Minute、Hour、Day、Week、Month</span><span class="sxs-lookup"><span data-stu-id="8c88c-254"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="8c88c-255">是</span><span class="sxs-lookup"><span data-stu-id="8c88c-255">Yes</span></span> |<span data-ttu-id="8c88c-256">NA</span><span class="sxs-lookup"><span data-stu-id="8c88c-256">NA</span></span> |
| <span data-ttu-id="8c88c-257">interval</span><span class="sxs-lookup"><span data-stu-id="8c88c-257">interval</span></span> |<span data-ttu-id="8c88c-258">指定頻率的倍數。</span><span class="sxs-lookup"><span data-stu-id="8c88c-258">Specifies a multiplier for frequency.</span></span><br/><br/><span data-ttu-id="8c88c-259">[頻率 x 間隔] 判斷頻率 hello 產生配量。</span><span class="sxs-lookup"><span data-stu-id="8c88c-259">"Frequency x interval" determines how often hello slice is produced.</span></span> <span data-ttu-id="8c88c-260">例如，如果您需要 hello 配量每小時的資料集 toobe，您將<b>頻率</b>太<b>小時</b>，和<b>間隔</b>太<b>1</b>。</span><span class="sxs-lookup"><span data-stu-id="8c88c-260">For example, if you need hello dataset toobe sliced on an hourly basis, you set <b>frequency</b> too<b>Hour</b>, and <b>interval</b> too<b>1</b>.</span></span><br/><br/><span data-ttu-id="8c88c-261">請注意，如果您指定**頻率**為**分鐘**，您應該設定 hello 間隔 toono 小於 15。</span><span class="sxs-lookup"><span data-stu-id="8c88c-261">Note that if you specify **frequency** as **Minute**, you should set hello interval toono less than 15.</span></span> |<span data-ttu-id="8c88c-262">是</span><span class="sxs-lookup"><span data-stu-id="8c88c-262">Yes</span></span> |<span data-ttu-id="8c88c-263">NA</span><span class="sxs-lookup"><span data-stu-id="8c88c-263">NA</span></span> |
| <span data-ttu-id="8c88c-264">style</span><span class="sxs-lookup"><span data-stu-id="8c88c-264">style</span></span> |<span data-ttu-id="8c88c-265">指定是否應該在 hello 開頭或結尾 hello 間隔產生 hello 配量。</span><span class="sxs-lookup"><span data-stu-id="8c88c-265">Specifies whether hello slice should be produced at hello start or end of hello interval.</span></span><ul><li><span data-ttu-id="8c88c-266">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="8c88c-266">StartOfInterval</span></span></li><li><span data-ttu-id="8c88c-267">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="8c88c-267">EndOfInterval</span></span></li></ul><span data-ttu-id="8c88c-268">如果**頻率**設定得**月份**，和**樣式**設定得**為 EndOfInterval**，hello 當月最後一天產生 hello 配量。</span><span class="sxs-lookup"><span data-stu-id="8c88c-268">If **frequency** is set too**Month**, and **style** is set too**EndOfInterval**, hello slice is produced on hello last day of month.</span></span> <span data-ttu-id="8c88c-269">如果**樣式**設定得**StartOfInterval**，hello 配量會產生 hello 上個月的第一天。</span><span class="sxs-lookup"><span data-stu-id="8c88c-269">If **style** is set too**StartOfInterval**, hello slice is produced on hello first day of month.</span></span><br/><br/><span data-ttu-id="8c88c-270">如果**頻率**設定得**天**，和**樣式**設定得**為 EndOfInterval**，hello 配量會產生在 hello 的 hello 當日的前一個小時。</span><span class="sxs-lookup"><span data-stu-id="8c88c-270">If **frequency** is set too**Day**, and **style** is set too**EndOfInterval**, hello slice is produced in hello last hour of hello day.</span></span><br/><br/><span data-ttu-id="8c88c-271">如果**頻率**設定得**小時**，和**樣式**設定得**為 EndOfInterval**，hello 配量會產生在 hello hello 小時結尾。</span><span class="sxs-lookup"><span data-stu-id="8c88c-271">If **frequency** is set too**Hour**, and **style** is set too**EndOfInterval**, hello slice is produced at hello end of hello hour.</span></span> <span data-ttu-id="8c88c-272">比方說，hello 下午 1-2 PM 期間的配量，hello 配量會在 2 PM 產生。</span><span class="sxs-lookup"><span data-stu-id="8c88c-272">For example, for a slice for hello 1 PM - 2 PM period, hello slice is produced at 2 PM.</span></span> |<span data-ttu-id="8c88c-273">否</span><span class="sxs-lookup"><span data-stu-id="8c88c-273">No</span></span> |<span data-ttu-id="8c88c-274">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="8c88c-274">EndOfInterval</span></span> |
| <span data-ttu-id="8c88c-275">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="8c88c-275">anchorDateTime</span></span> |<span data-ttu-id="8c88c-276">定義中的 hello 排程器 toocompute 資料集配量界限所使用的時間 hello 絕對位置。</span><span class="sxs-lookup"><span data-stu-id="8c88c-276">Defines hello absolute position in time used by hello scheduler toocompute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="8c88c-277">請注意，如果此 propoerty 具有比 hello 指定頻率，較精細的日期部分 hello 更精細的部分會被忽略。</span><span class="sxs-lookup"><span data-stu-id="8c88c-277">Note that if this propoerty has date parts that are more granular than hello specified frequency, hello more granular parts are ignored.</span></span> <span data-ttu-id="8c88c-278">例如，如果 hello**間隔**是**每小時**(頻率： hour，interval: 1)，和 hello **anchorDateTime**包含**分鐘和秒鐘**，然後 hello 分鐘和秒鐘部分**anchorDateTime**都會被忽略。</span><span class="sxs-lookup"><span data-stu-id="8c88c-278">For example, if hello **interval** is **hourly** (frequency: hour and interval: 1), and hello **anchorDateTime** contains **minutes and seconds**, then hello minutes and seconds parts of **anchorDateTime** are ignored.</span></span> |<span data-ttu-id="8c88c-279">否</span><span class="sxs-lookup"><span data-stu-id="8c88c-279">No</span></span> |<span data-ttu-id="8c88c-280">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="8c88c-280">01/01/0001</span></span> |
| <span data-ttu-id="8c88c-281">Offset</span><span class="sxs-lookup"><span data-stu-id="8c88c-281">offset</span></span> |<span data-ttu-id="8c88c-282">哪些 hello 的所有資料集配量的開始與結束移位的 Timespan。</span><span class="sxs-lookup"><span data-stu-id="8c88c-282">Timespan by which hello start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="8c88c-283">請注意，如果兩個**anchorDateTime**和**位移**指定，hello 結果是 hello 合併移位。</span><span class="sxs-lookup"><span data-stu-id="8c88c-283">Note that if both **anchorDateTime** and **offset** are specified, hello result is hello combined shift.</span></span> |<span data-ttu-id="8c88c-284">否</span><span class="sxs-lookup"><span data-stu-id="8c88c-284">No</span></span> |<span data-ttu-id="8c88c-285">NA</span><span class="sxs-lookup"><span data-stu-id="8c88c-285">NA</span></span> |

### <a name="offset-example"></a><span data-ttu-id="8c88c-286">位移範例</span><span class="sxs-lookup"><span data-stu-id="8c88c-286">offset example</span></span>
<span data-ttu-id="8c88c-287">根據預設，每日 (`"frequency": "Day", "interval": 1`) 配量的開始時間是「國際標准時間」(UTC) 上午 12 點 (午夜)。</span><span class="sxs-lookup"><span data-stu-id="8c88c-287">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM (midnight) Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="8c88c-288">如果要改為 hello 開始時間 toobe 上午 6 點 UTC 時間，將設定 hello 位移 hello 下列程式碼片段所示：</span><span class="sxs-lookup"><span data-stu-id="8c88c-288">If you want hello start time toobe 6 AM UTC time instead, set hello offset as shown in hello following snippet:</span></span> 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a><span data-ttu-id="8c88c-289">anchorDateTime 範例</span><span class="sxs-lookup"><span data-stu-id="8c88c-289">anchorDateTime example</span></span>
<span data-ttu-id="8c88c-290">在下列範例的 hello，hello 資料集，會產生一次每 23 的小時。</span><span class="sxs-lookup"><span data-stu-id="8c88c-290">In hello following example, hello dataset is produced once every 23 hours.</span></span> <span data-ttu-id="8c88c-291">hello 第一個配量開始所指定的 hello 時間**anchorDateTime**，太設定`2017-04-19T08:00:00`(UTC)。</span><span class="sxs-lookup"><span data-stu-id="8c88c-291">hello first slice starts at hello time specified by **anchorDateTime**, which is set too`2017-04-19T08:00:00` (UTC).</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a><span data-ttu-id="8c88c-292">位移/樣式範例</span><span class="sxs-lookup"><span data-stu-id="8c88c-292">offset/style example</span></span>
<span data-ttu-id="8c88c-293">hello 下列資料集是每月，並會在產生 hello 在 8:00 AM 每月的第 3 (`3.08:00:00`):</span><span class="sxs-lookup"><span data-stu-id="8c88c-293">hello following dataset is monthly, and is produced on hello 3rd of every month at 8:00 AM (`3.08:00:00`):</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

## <span data-ttu-id="8c88c-294"><a name="Policy"></a>資料集原則</span><span class="sxs-lookup"><span data-stu-id="8c88c-294"><a name="Policy"></a>Dataset policy</span></span>
<span data-ttu-id="8c88c-295">hello**原則**hello 資料集定義中的區段會定義 hello 準則或 hello 資料集配量的 hello 條件必須滿足。</span><span class="sxs-lookup"><span data-stu-id="8c88c-295">hello **policy** section in hello dataset definition defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span>

### <a name="validation-policies"></a><span data-ttu-id="8c88c-296">驗證原則</span><span class="sxs-lookup"><span data-stu-id="8c88c-296">Validation policies</span></span>
| <span data-ttu-id="8c88c-297">原則名稱</span><span class="sxs-lookup"><span data-stu-id="8c88c-297">Policy name</span></span> | <span data-ttu-id="8c88c-298">說明</span><span class="sxs-lookup"><span data-stu-id="8c88c-298">Description</span></span> | <span data-ttu-id="8c88c-299">套用太</span><span class="sxs-lookup"><span data-stu-id="8c88c-299">Applied too</span></span>| <span data-ttu-id="8c88c-300">必要</span><span class="sxs-lookup"><span data-stu-id="8c88c-300">Required</span></span> | <span data-ttu-id="8c88c-301">預設值</span><span class="sxs-lookup"><span data-stu-id="8c88c-301">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="8c88c-302">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="8c88c-302">minimumSizeMB</span></span> |<span data-ttu-id="8c88c-303">驗證中的 hello 資料**Azure Blob 儲存體**符合 hello 最小大小需求 （以 mb 為單位）。</span><span class="sxs-lookup"><span data-stu-id="8c88c-303">Validates that hello data in **Azure Blob storage** meets hello minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="8c88c-304">Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="8c88c-304">Azure Blob storage</span></span> |<span data-ttu-id="8c88c-305">否</span><span class="sxs-lookup"><span data-stu-id="8c88c-305">No</span></span> |<span data-ttu-id="8c88c-306">NA</span><span class="sxs-lookup"><span data-stu-id="8c88c-306">NA</span></span> |
| <span data-ttu-id="8c88c-307">minimumRows</span><span class="sxs-lookup"><span data-stu-id="8c88c-307">minimumRows</span></span> |<span data-ttu-id="8c88c-308">驗證中的 hello 資料**Azure SQL database**或**Azure 資料表**包含 hello 最小數目的資料列。</span><span class="sxs-lookup"><span data-stu-id="8c88c-308">Validates that hello data in an **Azure SQL database** or an **Azure table** contains hello minimum number of rows.</span></span> |<ul><li><span data-ttu-id="8c88c-309">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="8c88c-309">Azure SQL database</span></span></li><li><span data-ttu-id="8c88c-310">Azure 資料表</span><span class="sxs-lookup"><span data-stu-id="8c88c-310">Azure table</span></span></li></ul> |<span data-ttu-id="8c88c-311">否</span><span class="sxs-lookup"><span data-stu-id="8c88c-311">No</span></span> |<span data-ttu-id="8c88c-312">NA</span><span class="sxs-lookup"><span data-stu-id="8c88c-312">NA</span></span> |

#### <a name="examples"></a><span data-ttu-id="8c88c-313">範例</span><span class="sxs-lookup"><span data-stu-id="8c88c-313">Examples</span></span>
<span data-ttu-id="8c88c-314">**minimumSizeMB：**</span><span class="sxs-lookup"><span data-stu-id="8c88c-314">**minimumSizeMB:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="8c88c-315">**minimumRows：**</span><span class="sxs-lookup"><span data-stu-id="8c88c-315">**minimumRows:**</span></span>

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

### <a name="external-datasets"></a><span data-ttu-id="8c88c-316">外部資料集</span><span class="sxs-lookup"><span data-stu-id="8c88c-316">External datasets</span></span>
<span data-ttu-id="8c88c-317">外部資料集是 hello 不由 hello data factory 中執行的管線所產生的項目。</span><span class="sxs-lookup"><span data-stu-id="8c88c-317">External datasets are hello ones that are not produced by a running pipeline in hello data factory.</span></span> <span data-ttu-id="8c88c-318">如果 hello 資料集標示為**外部**，hello **ExternalData**原則可能是已定義的 tooinfluence hello 行為 hello 資料集配量的可用性。</span><span class="sxs-lookup"><span data-stu-id="8c88c-318">If hello dataset is marked as **external**, hello **ExternalData** policy may be defined tooinfluence hello behavior of hello dataset slice availability.</span></span>

<span data-ttu-id="8c88c-319">除非資料集是由 Data Factory 所產生，否則應該標示為「外部」。</span><span class="sxs-lookup"><span data-stu-id="8c88c-319">Unless a dataset is being produced by Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="8c88c-320">除非正在使用活動或管線鏈結，這項設定通常適用於 toohello 輸入管線中的第一個活動。</span><span class="sxs-lookup"><span data-stu-id="8c88c-320">This setting generally applies toohello inputs of first activity in a pipeline, unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="8c88c-321">名稱</span><span class="sxs-lookup"><span data-stu-id="8c88c-321">Name</span></span> | <span data-ttu-id="8c88c-322">說明</span><span class="sxs-lookup"><span data-stu-id="8c88c-322">Description</span></span> | <span data-ttu-id="8c88c-323">必要</span><span class="sxs-lookup"><span data-stu-id="8c88c-323">Required</span></span> | <span data-ttu-id="8c88c-324">預設值</span><span class="sxs-lookup"><span data-stu-id="8c88c-324">Default value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8c88c-325">dataDelay</span><span class="sxs-lookup"><span data-stu-id="8c88c-325">dataDelay</span></span> |<span data-ttu-id="8c88c-326">hello hello hello 的外部資料可用性檢查 toodelay hello hello 時間指定配量。</span><span class="sxs-lookup"><span data-stu-id="8c88c-326">hello time toodelay hello check on hello availability of hello external data for hello given slice.</span></span> <span data-ttu-id="8c88c-327">例如，您可以使用此設定來延遲每小時檢查。</span><span class="sxs-lookup"><span data-stu-id="8c88c-327">For example, you can delay an hourly check by using this setting.</span></span><br/><br/><span data-ttu-id="8c88c-328">hello 設定僅適用於 toohello 目前的時間。</span><span class="sxs-lookup"><span data-stu-id="8c88c-328">hello setting only applies toohello present time.</span></span>  <span data-ttu-id="8c88c-329">例如，如果它是 1:00 PM 現在，這個值為 10 分鐘 hello 驗證就會開始 1:10 PM。</span><span class="sxs-lookup"><span data-stu-id="8c88c-329">For example, if it is 1:00 PM right now and this value is 10 minutes, hello validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="8c88c-330">請注意這項設定不會影響在 hello 過去的配量。</span><span class="sxs-lookup"><span data-stu-id="8c88c-330">Note that this setting does not affect slices in hello past.</span></span> <span data-ttu-id="8c88c-331">針對**配量結束時間** + **dataDelay** < **現在**的配量，處理時將不會有任何延遲。</span><span class="sxs-lookup"><span data-stu-id="8c88c-331">Slices with **Slice End Time** + **dataDelay** < **Now** are processed without any delay.</span></span><br/><br/><span data-ttu-id="8c88c-332">應該使用 hello 指定時間大於 23:59 小時`day.hours:minutes:seconds`格式。</span><span class="sxs-lookup"><span data-stu-id="8c88c-332">Times greater than 23:59 hours should be specified by using hello `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="8c88c-333">例如，toospecify 24 小時，請勿使用 24:00:00。</span><span class="sxs-lookup"><span data-stu-id="8c88c-333">For example, toospecify 24 hours, don't use 24:00:00.</span></span> <span data-ttu-id="8c88c-334">請改用 1.00:00:00。</span><span class="sxs-lookup"><span data-stu-id="8c88c-334">Instead, use 1.00:00:00.</span></span> <span data-ttu-id="8c88c-335">如果您使用 24:00:00，這會視同 24 天 (24.00:00:00)。</span><span class="sxs-lookup"><span data-stu-id="8c88c-335">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="8c88c-336">如為 1 天又 4 小時，請指定 1:04:00:00。</span><span class="sxs-lookup"><span data-stu-id="8c88c-336">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="8c88c-337">否</span><span class="sxs-lookup"><span data-stu-id="8c88c-337">No</span></span> |<span data-ttu-id="8c88c-338">0</span><span class="sxs-lookup"><span data-stu-id="8c88c-338">0</span></span> |
| <span data-ttu-id="8c88c-339">retryInterval</span><span class="sxs-lookup"><span data-stu-id="8c88c-339">retryInterval</span></span> |<span data-ttu-id="8c88c-340">hello 失敗與 hello 的下一次嘗試之間的等待時間。</span><span class="sxs-lookup"><span data-stu-id="8c88c-340">hello wait time between a failure and hello next attempt.</span></span> <span data-ttu-id="8c88c-341">此設定適用於 toopresent 時間。</span><span class="sxs-lookup"><span data-stu-id="8c88c-341">This setting applies toopresent time.</span></span> <span data-ttu-id="8c88c-342">如果 hello 先前嘗試失敗，hello 下一次嘗試之後 hello **retryInterval**期間。</span><span class="sxs-lookup"><span data-stu-id="8c88c-342">If hello previous try failed, hello next try is after hello **retryInterval** period.</span></span> <br/><br/><span data-ttu-id="8c88c-343">如果是 1:00 PM 現在，我們會開始 hello 第一次嘗試。</span><span class="sxs-lookup"><span data-stu-id="8c88c-343">If it is 1:00 PM right now, we begin hello first try.</span></span> <span data-ttu-id="8c88c-344">Hello 下次重試 hello 持續時間 toocomplete hello 第一次驗證檢查是 1 分鐘而且 hello 作業失敗，如果是在 1:00 + 1 分鐘 （持續時間） + 1 分鐘 （重試間隔） = 1: 02PM。</span><span class="sxs-lookup"><span data-stu-id="8c88c-344">If hello duration toocomplete hello first validation check is 1 minute and hello operation failed, hello next retry is at 1:00 + 1min (duration) + 1min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="8c88c-345">在 hello 過去的配量，沒有任何延遲。</span><span class="sxs-lookup"><span data-stu-id="8c88c-345">For slices in hello past, there is no delay.</span></span> <span data-ttu-id="8c88c-346">hello 重試會立即發生。</span><span class="sxs-lookup"><span data-stu-id="8c88c-346">hello retry happens immediately.</span></span> |<span data-ttu-id="8c88c-347">否</span><span class="sxs-lookup"><span data-stu-id="8c88c-347">No</span></span> |<span data-ttu-id="8c88c-348">00:01:00 (1 分鐘)</span><span class="sxs-lookup"><span data-stu-id="8c88c-348">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="8c88c-349">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="8c88c-349">retryTimeout</span></span> |<span data-ttu-id="8c88c-350">每次重試的 hello 逾時。</span><span class="sxs-lookup"><span data-stu-id="8c88c-350">hello timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="8c88c-351">如果這個屬性設定 too10 分鐘 hello 驗證必須在 10 分鐘內完成。</span><span class="sxs-lookup"><span data-stu-id="8c88c-351">If this property is set too10 minutes, hello validation should be completed within 10 minutes.</span></span> <span data-ttu-id="8c88c-352">如果需花時間超過 10 分鐘 tooperform hello 驗證，hello 重試逾時。</span><span class="sxs-lookup"><span data-stu-id="8c88c-352">If it takes longer than 10 minutes tooperform hello validation, hello retry times out.</span></span><br/><br/><span data-ttu-id="8c88c-353">如果所有都 hello 驗證逾時，嘗試都 hello 配量會標示為**TimedOut**。</span><span class="sxs-lookup"><span data-stu-id="8c88c-353">If all attempts for hello validation time out, hello slice is marked as **TimedOut**.</span></span> |<span data-ttu-id="8c88c-354">否</span><span class="sxs-lookup"><span data-stu-id="8c88c-354">No</span></span> |<span data-ttu-id="8c88c-355">00:10:00 (10 分鐘)</span><span class="sxs-lookup"><span data-stu-id="8c88c-355">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="8c88c-356">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="8c88c-356">maximumRetry</span></span> |<span data-ttu-id="8c88c-357">hello 次數 toocheck hello hello 外部資料可用性。</span><span class="sxs-lookup"><span data-stu-id="8c88c-357">hello number of times toocheck for hello availability of hello external data.</span></span> <span data-ttu-id="8c88c-358">hello 最大允許值為 10。</span><span class="sxs-lookup"><span data-stu-id="8c88c-358">hello maximum allowed value is 10.</span></span> |<span data-ttu-id="8c88c-359">否</span><span class="sxs-lookup"><span data-stu-id="8c88c-359">No</span></span> |<span data-ttu-id="8c88c-360">3</span><span class="sxs-lookup"><span data-stu-id="8c88c-360">3</span></span> |


## <a name="create-datasets"></a><span data-ttu-id="8c88c-361">建立資料集</span><span class="sxs-lookup"><span data-stu-id="8c88c-361">Create datasets</span></span>
<span data-ttu-id="8c88c-362">您可以使用下列其中一項工具或 SDK 來建立資料集：</span><span class="sxs-lookup"><span data-stu-id="8c88c-362">You can create datasets by using one of these tools or SDKs:</span></span> 

- <span data-ttu-id="8c88c-363">複製精靈</span><span class="sxs-lookup"><span data-stu-id="8c88c-363">Copy Wizard</span></span> 
- <span data-ttu-id="8c88c-364">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="8c88c-364">Azure portal</span></span>
- <span data-ttu-id="8c88c-365">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8c88c-365">Visual Studio</span></span>
- <span data-ttu-id="8c88c-366">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c88c-366">PowerShell</span></span>
- <span data-ttu-id="8c88c-367">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="8c88c-367">Azure Resource Manager template</span></span>
- <span data-ttu-id="8c88c-368">REST API</span><span class="sxs-lookup"><span data-stu-id="8c88c-368">REST API</span></span>
- <span data-ttu-id="8c88c-369">.NET API</span><span class="sxs-lookup"><span data-stu-id="8c88c-369">.NET API</span></span>

<span data-ttu-id="8c88c-370">請參閱下列逐步教學課程使用其中一個工具或 Sdk 來建立管線和資料集的 hello:</span><span class="sxs-lookup"><span data-stu-id="8c88c-370">See hello following tutorials for step-by-step instructions for creating pipelines and datasets by using one of these tools or SDKs:</span></span>
 
- [<span data-ttu-id="8c88c-371">使用資料轉換活動來建置管線</span><span class="sxs-lookup"><span data-stu-id="8c88c-371">Build a pipeline with a data transformation activity</span></span>](data-factory-build-your-first-pipeline.md)
- [<span data-ttu-id="8c88c-372">使用資料移動活動來建置管線</span><span class="sxs-lookup"><span data-stu-id="8c88c-372">Build a pipeline with a data movement activity</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

<span data-ttu-id="8c88c-373">建立及部署管線之後，您可以管理和監視您所使用的管線 hello Azure 入口網站的刀鋒視窗或 hello 監視和管理應用程式。</span><span class="sxs-lookup"><span data-stu-id="8c88c-373">After a pipeline is created and deployed, you can manage and monitor your pipelines by using hello Azure portal blades, or hello Monitoring and Management app.</span></span> <span data-ttu-id="8c88c-374">請參閱下列主題逐步指示的 hello:</span><span class="sxs-lookup"><span data-stu-id="8c88c-374">See hello following topics for step-by-step instructions:</span></span> 

- [<span data-ttu-id="8c88c-375">使用 Azure 入口網站刀鋒視窗來監視和管理管線</span><span class="sxs-lookup"><span data-stu-id="8c88c-375">Monitor and manage pipelines by using Azure portal blades</span></span>](data-factory-monitor-manage-pipelines.md)
- [<span data-ttu-id="8c88c-376">監視和管理使用 hello 監視和管理應用程式的管線</span><span class="sxs-lookup"><span data-stu-id="8c88c-376">Monitor and manage pipelines by using hello Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)


## <a name="scoped-datasets"></a><span data-ttu-id="8c88c-377">範圍資料集</span><span class="sxs-lookup"><span data-stu-id="8c88c-377">Scoped datasets</span></span>
<span data-ttu-id="8c88c-378">您可以建立資料集範圍的 tooa 管線使用 hello**資料集**屬性。</span><span class="sxs-lookup"><span data-stu-id="8c88c-378">You can create datasets that are scoped tooa pipeline by using hello **datasets** property.</span></span> <span data-ttu-id="8c88c-379">這些資料集僅供此管線內的活動使用，不供其他管線中的活動使用。</span><span class="sxs-lookup"><span data-stu-id="8c88c-379">These datasets can only be used by activities within this pipeline, not by activities in other pipelines.</span></span> <span data-ttu-id="8c88c-380">hello 下列範例會定義具有兩個資料集 （InputDataset rdc 和 OutputDataset rdc） toobe hello 管線中使用的管線。</span><span class="sxs-lookup"><span data-stu-id="8c88c-380">hello following example defines a pipeline with two datasets (InputDataset-rdc and OutputDataset-rdc) toobe used within hello pipeline.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="8c88c-381">單次管線只能搭配支援的已設定領域的資料集 (其中**pipelineMode**設定得**OneTime**)。</span><span class="sxs-lookup"><span data-stu-id="8c88c-381">Scoped datasets are supported only with one-time pipelines (where **pipelineMode** is set too**OneTime**).</span></span> <span data-ttu-id="8c88c-382">如需詳細資訊，請參閱 [一次性管線](data-factory-create-pipelines.md#onetime-pipeline) 。</span><span class="sxs-lookup"><span data-stu-id="8c88c-382">See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details.</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="8c88c-383">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8c88c-383">Next steps</span></span>
- <span data-ttu-id="8c88c-384">如需有關管線的詳細資訊，請參閱[建立管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="8c88c-384">For more information about pipelines, see [Create pipelines](data-factory-create-pipelines.md).</span></span> 
- <span data-ttu-id="8c88c-385">如需有關管線的排程和執行方式的詳細資訊，請參閱 [Azure Data Factory 中的排程和執行](data-factory-scheduling-and-execution.md)。</span><span class="sxs-lookup"><span data-stu-id="8c88c-385">For more information about how pipelines are scheduled and executed, see [Scheduling and execution in Azure Data Factory](data-factory-scheduling-and-execution.md).</span></span> 
