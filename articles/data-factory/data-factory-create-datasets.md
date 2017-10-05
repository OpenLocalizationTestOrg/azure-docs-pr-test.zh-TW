---
title: "在 Azure Data Factory 中建立資料集 | Microsoft Docs"
description: "了解如何透過使用位移和 anchorDateTime 等屬性的範例，在 Azure Data Factory 中建立資料集。"
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
ms.openlocfilehash: 6fd58edd830df8ea3f77a68e8dfcaf6de055b17c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="datasets-in-azure-data-factory"></a><span data-ttu-id="4e6cf-104">Azure Data Factory 中的資料集</span><span class="sxs-lookup"><span data-stu-id="4e6cf-104">Datasets in Azure Data Factory</span></span>
<span data-ttu-id="4e6cf-105">本文說明什麼是資料集、如何以 JSON 格式定義它們，以及如何在 Azure Data Factory 管線中使用它們。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-105">This article describes what datasets are, how they are defined in JSON format, and how they are used in Azure Data Factory pipelines.</span></span> <span data-ttu-id="4e6cf-106">它提供有關資料集 JSON 定義中每個區段 (例如 structure、availability 及 policy) 的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-106">It provides details about each section (for example, structure, availability, and policy) in the dataset JSON definition.</span></span> <span data-ttu-id="4e6cf-107">本文也提供在資料集 JSON 定義中使用 **offset**、**anchorDateTime** 及 **style** 屬性的範例。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-107">The article also provides examples for using the **offset**, **anchorDateTime**, and **style** properties in a dataset JSON definition.</span></span>

> [!NOTE]
> <span data-ttu-id="4e6cf-108">如果您不熟悉 Data Factory，請參閱 [Azure Data Factory 簡介](data-factory-introduction.md)來概略了解。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-108">If you are new to Data Factory, see [Introduction to Azure Data Factory](data-factory-introduction.md) for an overview.</span></span> <span data-ttu-id="4e6cf-109">如果您沒有建立 Data Factory 的實作經驗，可以閱讀[資料轉換教學課程](data-factory-build-your-first-pipeline.md)和[資料移動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)來進一步了解。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-109">If you do not have hands-on experience with creating data factories, you can gain a better understanding by reading the [data transformation tutorial](data-factory-build-your-first-pipeline.md) and the [data movement tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

## <a name="overview"></a><span data-ttu-id="4e6cf-110">概觀</span><span class="sxs-lookup"><span data-stu-id="4e6cf-110">Overview</span></span>
<span data-ttu-id="4e6cf-111">資料處理站可以有一或多個管線。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-111">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="4e6cf-112">「管線」是一起執行某個工作的「活動」所組成的邏輯群組。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-112">A **pipeline** is a logical grouping of **activities** that together perform a task.</span></span> <span data-ttu-id="4e6cf-113">管線中的活動會定義要在資料上執行的動作。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-113">The activities in a pipeline define actions to perform on your data.</span></span> <span data-ttu-id="4e6cf-114">例如，您可以使用複製活動將資料從內部部署 SQL Server 複製到 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-114">For example, you might use a copy activity to copy data from an on-premises SQL Server to Azure Blob storage.</span></span> <span data-ttu-id="4e6cf-115">接著，您可以使用在 Azure HDInsight 叢集上執行 Hive 指令碼的 Hive 活動，來處理來自 Blob 儲存體的資料以產生輸出資料。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-115">Then, you might use a Hive activity that runs a Hive script on an Azure HDInsight cluster to process data from Blob storage to produce output data.</span></span> <span data-ttu-id="4e6cf-116">最後，您可以使用第二個複製活動將輸出資料複製到「Azure SQL 資料倉儲」，以在該處建置商業智慧 (BI) 報表解決方案。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-116">Finally, you might use a second copy activity to copy the output data to Azure SQL Data Warehouse, on top of which business intelligence (BI) reporting solutions are built.</span></span> <span data-ttu-id="4e6cf-117">如需有關管線和活動的詳細資訊，請參閱 [Azure Data Factory 中的管線及活動](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-117">For more information about pipelines and activities, see [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md).</span></span>

<span data-ttu-id="4e6cf-118">一個活動可以接受零個或多個輸入「資料集」，並且會產生一個或多個輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-118">An activity can take zero or more input **datasets**, and produce one or more output datasets.</span></span> <span data-ttu-id="4e6cf-119">輸入資料集代表管線中活動的輸入，輸出資料集則代表活動的輸出。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-119">An input dataset represents the input for an activity in the pipeline, and an output dataset represents the output for the activity.</span></span> <span data-ttu-id="4e6cf-120">資料集可識別資料表、檔案、資料夾和文件等各種資料存放區中的資料。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-120">Datasets identify data within different data stores, such as tables, files, folders, and documents.</span></span> <span data-ttu-id="4e6cf-121">例如，Azure Blob 資料集會指定管線應從中讀取資料之 Blob 儲存體中的 Blob 容器和資料夾。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-121">For example, an Azure Blob dataset specifies the blob container and folder in Blob storage from which the pipeline should read the data.</span></span> 

<span data-ttu-id="4e6cf-122">在您建立資料集之前，請先建立一個「已連結的服務」，以將資料存放區連結到 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-122">Before you create a dataset, create a **linked service** to link your data store to the data factory.</span></span> <span data-ttu-id="4e6cf-123">已連結的服務非常類似連接字串，可定義 Data Factory 連接到外部資源所需的連線資訊。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-123">Linked services are much like connection strings, which define the connection information needed for Data Factory to connect to external resources.</span></span> <span data-ttu-id="4e6cf-124">資料集可識別已連結的資料存放區內的資料，例如 SQL 資料表、檔案、資料夾及文件。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-124">Datasets identify data within the linked data stores, such as SQL tables, files, folders, and documents.</span></span> <span data-ttu-id="4e6cf-125">例如，「Azure 儲存體」已連結服務會將儲存體帳戶連結到 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-125">For example, an Azure Storage linked service links a storage account to the data factory.</span></span> <span data-ttu-id="4e6cf-126">Azure Blob 資料集代表包含要處理之輸入 Blob 的 Blob 容器和資料夾。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-126">An Azure Blob dataset represents the blob container and the folder that contains the input blobs to be processed.</span></span> 

<span data-ttu-id="4e6cf-127">以下是一個範例案例。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-127">Here is a sample scenario.</span></span> <span data-ttu-id="4e6cf-128">若要將資料從 Blob 儲存體複製到 SQL Database，您需建立兩個已連結的服務：「Azure 儲存體」和 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-128">To copy data from Blob storage to a SQL database, you create two linked services: Azure Storage and Azure SQL Database.</span></span> <span data-ttu-id="4e6cf-129">接著，建立兩個資料集：Azure Blob 資料集 (此資料集參考「Azure 儲存體」已連結服務) 和「Azure SQL 資料表」資料集 (此資料集參考 Azure SQL Database 已連結服務)。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-129">Then, create two datasets: Azure Blob dataset (which refers to the Azure Storage linked service) and Azure SQL Table dataset (which refers to the Azure SQL Database linked service).</span></span> <span data-ttu-id="4e6cf-130">「Azure 儲存體」和 Azure SQL Database 已連結服務包含 Data Factory 在執行階段分別用來連接到「Azure 儲存體」和 Azure SQL Database 的連接字串。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-130">The Azure Storage and Azure SQL Database linked services contain connection strings that Data Factory uses at runtime to connect to your Azure Storage and Azure SQL Database, respectively.</span></span> <span data-ttu-id="4e6cf-131">Azure Blob 資料集會指定包含 Blob 儲存體中輸入 Blob 的 Blob 容器和 Blob 資料夾。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-131">The Azure Blob dataset specifies the blob container and blob folder that contains the input blobs in your Blob storage.</span></span> <span data-ttu-id="4e6cf-132">「Azure SQL 資料表」資料集會指定作為資料複製目的地的 SQL Database 中 SQL 資料表。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-132">The Azure SQL Table dataset specifies the SQL table in your SQL database to which the data is to be copied.</span></span>

<span data-ttu-id="4e6cf-133">下圖顯示 Data Factory 中管線、活動、資料集及已連結服務之間的關聯性：</span><span class="sxs-lookup"><span data-stu-id="4e6cf-133">The following diagram shows the relationships among pipeline, activity, dataset, and linked service in Data Factory:</span></span> 

![管線、活動、資料集、已連結的服務之間的關聯性](media/data-factory-create-datasets/relationship-between-data-factory-entities.png)

## <a name="dataset-json"></a><span data-ttu-id="4e6cf-135">資料集 JSON</span><span class="sxs-lookup"><span data-stu-id="4e6cf-135">Dataset JSON</span></span>
<span data-ttu-id="4e6cf-136">Data Factory 中的資料集會以 JSON 格式定義如下：</span><span class="sxs-lookup"><span data-stu-id="4e6cf-136">A dataset in Data Factory is defined in JSON format as follows:</span></span>

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag to indicate external data. only for input datasets>,
        "linkedServiceName": "<Name of the linked service that refers to a data store.>",
        "structure": [
            {
                "name": "<Name of the column>",
                "type": "<Name of the type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies the time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies the interval within the defined frequency. For example, frequency set to 'Hour' and interval set to 1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

<span data-ttu-id="4e6cf-137">下表描述上述 JSON 的屬性：</span><span class="sxs-lookup"><span data-stu-id="4e6cf-137">The following table describes properties in the above JSON:</span></span>   

| <span data-ttu-id="4e6cf-138">屬性</span><span class="sxs-lookup"><span data-stu-id="4e6cf-138">Property</span></span> | <span data-ttu-id="4e6cf-139">說明</span><span class="sxs-lookup"><span data-stu-id="4e6cf-139">Description</span></span> | <span data-ttu-id="4e6cf-140">必要</span><span class="sxs-lookup"><span data-stu-id="4e6cf-140">Required</span></span> | <span data-ttu-id="4e6cf-141">預設值</span><span class="sxs-lookup"><span data-stu-id="4e6cf-141">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4e6cf-142">名稱</span><span class="sxs-lookup"><span data-stu-id="4e6cf-142">name</span></span> |<span data-ttu-id="4e6cf-143">資料集的名稱。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-143">Name of the dataset.</span></span> <span data-ttu-id="4e6cf-144">請參閱 [Azure Data Factory - 命名規則](data-factory-naming-rules.md) ，以了解命名規則。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-144">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="4e6cf-145">是</span><span class="sxs-lookup"><span data-stu-id="4e6cf-145">Yes</span></span> |<span data-ttu-id="4e6cf-146">NA</span><span class="sxs-lookup"><span data-stu-id="4e6cf-146">NA</span></span> |
| <span data-ttu-id="4e6cf-147">類型</span><span class="sxs-lookup"><span data-stu-id="4e6cf-147">type</span></span> |<span data-ttu-id="4e6cf-148">資料集的類型。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-148">Type of the dataset.</span></span> <span data-ttu-id="4e6cf-149">指定 Data Factory 支援的其中一種類型 (例如︰AzureBlob、AzureSqlTable)。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-149">Specify one of the types supported by Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <br/><br/><span data-ttu-id="4e6cf-150">如需詳細資料，請參閱[資料集類型](#Type)。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-150">For details, see [Dataset type](#Type).</span></span> |<span data-ttu-id="4e6cf-151">是</span><span class="sxs-lookup"><span data-stu-id="4e6cf-151">Yes</span></span> |<span data-ttu-id="4e6cf-152">NA</span><span class="sxs-lookup"><span data-stu-id="4e6cf-152">NA</span></span> |
| <span data-ttu-id="4e6cf-153">structure</span><span class="sxs-lookup"><span data-stu-id="4e6cf-153">structure</span></span> |<span data-ttu-id="4e6cf-154">資料集的結構描述。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-154">Schema of the dataset.</span></span><br/><br/><span data-ttu-id="4e6cf-155">如需詳細資料，請參閱[資料集結構](#Structure)。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-155">For details, see [Dataset structure](#Structure).</span></span> |<span data-ttu-id="4e6cf-156">否</span><span class="sxs-lookup"><span data-stu-id="4e6cf-156">No</span></span> |<span data-ttu-id="4e6cf-157">NA</span><span class="sxs-lookup"><span data-stu-id="4e6cf-157">NA</span></span> |
| <span data-ttu-id="4e6cf-158">typeProperties</span><span class="sxs-lookup"><span data-stu-id="4e6cf-158">typeProperties</span></span> | <span data-ttu-id="4e6cf-159">每個類型 (例如：Azure Blob、Azure SQL 資料表) 的類型屬性都不同。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-159">The type properties are different for each type (for example: Azure Blob, Azure SQL table).</span></span> <span data-ttu-id="4e6cf-160">如需有關支援的類型及其屬性的詳細資料，請參閱[資料集類型](#Type)。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-160">For details on the supported types and their properties, see [Dataset type](#Type).</span></span> |<span data-ttu-id="4e6cf-161">是</span><span class="sxs-lookup"><span data-stu-id="4e6cf-161">Yes</span></span> |<span data-ttu-id="4e6cf-162">NA</span><span class="sxs-lookup"><span data-stu-id="4e6cf-162">NA</span></span> |
| <span data-ttu-id="4e6cf-163">external</span><span class="sxs-lookup"><span data-stu-id="4e6cf-163">external</span></span> | <span data-ttu-id="4e6cf-164">用來指定資料集是否由 Data Factory 管線明確產生的布林值旗標。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-164">Boolean flag to specify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> <span data-ttu-id="4e6cf-165">如果活動的輸入資料集不是由目前的管線所產生，請將此旗標設定為 true。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-165">If the input dataset for an activity is not produced by the current pipeline, set this flag to true.</span></span> <span data-ttu-id="4e6cf-166">請針對管線中第一個活動的輸入資料集，將此旗標設定為 true。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-166">Set this flag to true for the input dataset of the first activity in the pipeline.</span></span>  |<span data-ttu-id="4e6cf-167">否</span><span class="sxs-lookup"><span data-stu-id="4e6cf-167">No</span></span> |<span data-ttu-id="4e6cf-168">false</span><span class="sxs-lookup"><span data-stu-id="4e6cf-168">false</span></span> |
| <span data-ttu-id="4e6cf-169">Availability</span><span class="sxs-lookup"><span data-stu-id="4e6cf-169">availability</span></span> | <span data-ttu-id="4e6cf-170">定義處理時段 (例如每小時或每天) 或用於產生資料集的切割模型。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-170">Defines the processing window (for example, hourly or daily) or the slicing model for the dataset production.</span></span> <span data-ttu-id="4e6cf-171">活動執行取用和產生的每個資料單位稱為資料配量。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-171">Each unit of data consumed and produced by an activity run is called a data slice.</span></span> <span data-ttu-id="4e6cf-172">如果將輸出資料集的可用性設定為每天 (frequency - Day，interval - 1)，就會每天產生配量。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-172">If the availability of an output dataset is set to daily (frequency - Day, interval - 1), a slice is produced daily.</span></span> <br/><br/><span data-ttu-id="4e6cf-173">如需詳細資料，請參閱[資料集可用性](#Availability)。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-173">For details, see [Dataset availability](#Availability).</span></span> <br/><br/><span data-ttu-id="4e6cf-174">如需有關資料集切割模型的詳細資料，請參閱[排程和執行](data-factory-scheduling-and-execution.md)一文。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-174">For details on the dataset slicing model, see the [Scheduling and execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="4e6cf-175">是</span><span class="sxs-lookup"><span data-stu-id="4e6cf-175">Yes</span></span> |<span data-ttu-id="4e6cf-176">NA</span><span class="sxs-lookup"><span data-stu-id="4e6cf-176">NA</span></span> |
| <span data-ttu-id="4e6cf-177">原則</span><span class="sxs-lookup"><span data-stu-id="4e6cf-177">policy</span></span> |<span data-ttu-id="4e6cf-178">定義資料集配量必須符合的準則或條件。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-178">Defines the criteria or the condition that the dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="4e6cf-179">如需詳細資料，請參閱[資料集原則](#Policy)一節。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-179">For details, see the [Dataset policy](#Policy) section.</span></span> |<span data-ttu-id="4e6cf-180">否</span><span class="sxs-lookup"><span data-stu-id="4e6cf-180">No</span></span> |<span data-ttu-id="4e6cf-181">NA</span><span class="sxs-lookup"><span data-stu-id="4e6cf-181">NA</span></span> |

## <a name="dataset-example"></a><span data-ttu-id="4e6cf-182">資料集範例</span><span class="sxs-lookup"><span data-stu-id="4e6cf-182">Dataset example</span></span>
<span data-ttu-id="4e6cf-183">在下列範例中，資料集代表 SQL Database 中名為 **MyTable** 的資料表。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-183">In the following example, the dataset represents a table named **MyTable** in a SQL database.</span></span>

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

<span data-ttu-id="4e6cf-184">請注意下列幾點：</span><span class="sxs-lookup"><span data-stu-id="4e6cf-184">Note the following points:</span></span>

* <span data-ttu-id="4e6cf-185">**type** 是設定為 AzureSqlTable。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-185">**type** is set to AzureSqlTable.</span></span>
* <span data-ttu-id="4e6cf-186">**tableName** 類型屬性 (AzureSqlTable 類型特定) 是設定為 MyTable。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-186">**tableName** type property (specific to AzureSqlTable type) is set to MyTable.</span></span>
* <span data-ttu-id="4e6cf-187">**linkedServiceName** 係指 AzureSqlDatabase 類型的已連結服務，在接下來的 JSON 程式碼片段中將會定義。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-187">**linkedServiceName** refers to a linked service of type AzureSqlDatabase, which is defined in the next JSON snippet.</span></span> 
* <span data-ttu-id="4e6cf-188">**availability frequency** 是設定為 Day，**interval** 是設定為 1。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-188">**availability frequency** is set to Day, and **interval** is set to 1.</span></span> <span data-ttu-id="4e6cf-189">這意謂著會每天產生資料集配量。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-189">This means that the dataset slice is produced daily.</span></span>  

<span data-ttu-id="4e6cf-190">**AzureSqlLinkedService** 定義如下︰</span><span class="sxs-lookup"><span data-stu-id="4e6cf-190">**AzureSqlLinkedService** is defined as follows:</span></span>

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

<span data-ttu-id="4e6cf-191">在上述 JSON 程式碼片段中：</span><span class="sxs-lookup"><span data-stu-id="4e6cf-191">In the preceding JSON snippet:</span></span>

* <span data-ttu-id="4e6cf-192">**type** 是設定為 AzureSqlDatabase。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-192">**type** is set to AzureSqlDatabase.</span></span>
* <span data-ttu-id="4e6cf-193">**connectionString** 類型屬性會指定用以連接到 SQL Database 的資訊。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-193">**connectionString** type property specifies information to connect to a SQL database.</span></span>  

<span data-ttu-id="4e6cf-194">如您所見，已連結的服務會定義如何連接到 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-194">As you can see, the linked service defines how to connect to a SQL database.</span></span> <span data-ttu-id="4e6cf-195">資料集會定義使用哪個資料表作為管線中活動的輸入和輸出。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-195">The dataset defines what table is used as an input and output for the activity in a pipeline.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="4e6cf-196">除非資料集是由管線所產生，否則應該標示為「外部」。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-196">Unless a dataset is being produced by the pipeline, it should be marked as **external**.</span></span> <span data-ttu-id="4e6cf-197">此設定通常會套用至管線中第一個活動的輸入。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-197">This setting generally applies to inputs of first activity in a pipeline.</span></span>   


## <span data-ttu-id="4e6cf-198"><a name="Type"></a> 資料集類型</span><span class="sxs-lookup"><span data-stu-id="4e6cf-198"><a name="Type"></a> Dataset type</span></span>
<span data-ttu-id="4e6cf-199">資料集的類型取決於您所使用的資料存放區。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-199">The type of the dataset depends on the data store you use.</span></span> <span data-ttu-id="4e6cf-200">如需 Data Factory 所支援的資料存放區清單，請參閱下表。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-200">See the following table for a list of data stores supported by Data Factory.</span></span> <span data-ttu-id="4e6cf-201">按一下某個資料存放區，即可了解如何為該資料存放區建立已連結的服務和資料集。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-201">Click a data store to learn how to create a linked service and a dataset for that data store.</span></span>

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> <span data-ttu-id="4e6cf-202">帶有 * 的資料存放區可以位於內部部署環境或 Azure 基礎結構即服務 (IaaS) 上。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-202">Data stores with * can be on-premises or on Azure infrastructure as a service (IaaS).</span></span> <span data-ttu-id="4e6cf-203">這些資料存放區會要求您安裝[資料管理閘道](data-factory-data-management-gateway.md)。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-203">These data stores require you to install [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>

<span data-ttu-id="4e6cf-204">在上一節的範例中，資料集的類型是設定為 **AzureSqlTable**。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-204">In the example in the previous section, the type of the dataset is set to **AzureSqlTable**.</span></span> <span data-ttu-id="4e6cf-205">同樣地，針對 Azure Blob 資料集，資料集的類型是設定為 **AzureBlob**，如以下 JSON 所示：</span><span class="sxs-lookup"><span data-stu-id="4e6cf-205">Similarly, for an Azure Blob dataset, the type of the dataset is set to **AzureBlob**, as shown in the following JSON:</span></span>

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

## <span data-ttu-id="4e6cf-206"><a name="Structure"></a>資料集結構</span><span class="sxs-lookup"><span data-stu-id="4e6cf-206"><a name="Structure"></a>Dataset structure</span></span>
<span data-ttu-id="4e6cf-207">**structure** 區段是選擇性區段。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-207">The **structure** section is optional.</span></span> <span data-ttu-id="4e6cf-208">它可透過包含資料行之名稱和資料類型的集合，定義資料集的結構描述。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-208">It defines the schema of the dataset by containing a collection of names and data types of columns.</span></span> <span data-ttu-id="4e6cf-209">您可以使用 structure 區段來提供類型資訊，此資訊會用來轉換類型並將資料行從來源對應到目的地。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-209">You use the structure section to provide type information that is used to convert types and map columns from the source to the destination.</span></span> <span data-ttu-id="4e6cf-210">在下列範例中，資料集有三個資料行︰`slicetimestamp`、`projectname` 及 `pageviews`。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-210">In the following example, the dataset has three columns: `slicetimestamp`, `projectname`, and `pageviews`.</span></span> <span data-ttu-id="4e6cf-211">它們的類型分別是 String、String 及 Decimal。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-211">They are of type String, String, and Decimal, respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="4e6cf-212">structure 中的每個資料行都包含下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="4e6cf-212">Each column in the structure contains the following properties:</span></span>

| <span data-ttu-id="4e6cf-213">屬性</span><span class="sxs-lookup"><span data-stu-id="4e6cf-213">Property</span></span> | <span data-ttu-id="4e6cf-214">說明</span><span class="sxs-lookup"><span data-stu-id="4e6cf-214">Description</span></span> | <span data-ttu-id="4e6cf-215">必要</span><span class="sxs-lookup"><span data-stu-id="4e6cf-215">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4e6cf-216">名稱</span><span class="sxs-lookup"><span data-stu-id="4e6cf-216">name</span></span> |<span data-ttu-id="4e6cf-217">資料行的名稱。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-217">Name of the column.</span></span> |<span data-ttu-id="4e6cf-218">是</span><span class="sxs-lookup"><span data-stu-id="4e6cf-218">Yes</span></span> |
| <span data-ttu-id="4e6cf-219">類型</span><span class="sxs-lookup"><span data-stu-id="4e6cf-219">type</span></span> |<span data-ttu-id="4e6cf-220">資料行的資料類型。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-220">Data type of the column.</span></span>  |<span data-ttu-id="4e6cf-221">否</span><span class="sxs-lookup"><span data-stu-id="4e6cf-221">No</span></span> |
| <span data-ttu-id="4e6cf-222">culture</span><span class="sxs-lookup"><span data-stu-id="4e6cf-222">culture</span></span> |<span data-ttu-id="4e6cf-223">當類型為 .NET 類型 (`Datetime` 或 `Datetimeoffset`) 時，所要使用的 .NET 型文化特性。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-223">.NET-based culture to be used when the type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="4e6cf-224">預設值為 `en-us`。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-224">The default is `en-us`.</span></span> |<span data-ttu-id="4e6cf-225">否</span><span class="sxs-lookup"><span data-stu-id="4e6cf-225">No</span></span> |
| <span data-ttu-id="4e6cf-226">format</span><span class="sxs-lookup"><span data-stu-id="4e6cf-226">format</span></span> |<span data-ttu-id="4e6cf-227">當類型為 .NET 類型 (`Datetime` 或 `Datetimeoffset`) 時，所要使用的格式字串。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-227">Format string to be used when the type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="4e6cf-228">否</span><span class="sxs-lookup"><span data-stu-id="4e6cf-228">No</span></span> |

<span data-ttu-id="4e6cf-229">下列方針可協助您判斷何時要包括 structure 資訊，以及在 **structure** 區段中要包含哪些資訊。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-229">The following guidelines help you determine when to include structure information, and what to include in the **structure** section.</span></span>

* <span data-ttu-id="4e6cf-230">**針對結構化資料來源**，請只有在您想要將來源資料行對應到接收資料行且其名稱不相同時，才指定 structure 區段。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-230">**For structured data sources**, specify the structure section only if you want map source columns to sink columns, and their names are not the same.</span></span> <span data-ttu-id="4e6cf-231">這類結構化資料來源會將資料結構描述和類型資訊與資料本身儲存在一起。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-231">This kind of structured data source stores data schema and type information along with the data itself.</span></span> <span data-ttu-id="4e6cf-232">結構化資料來源的範例包括 SQL Server、Oracle 及 Azure 資料表。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-232">Examples of structured data sources include SQL Server, Oracle, and Azure table.</span></span> 
  
    <span data-ttu-id="4e6cf-233">由於結構化資料來源已經有可用的類型資訊，因此當您包含 structure 區段時，便不應包含類型資訊。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-233">As type information is already available for structured data sources, you should not include type information when you do include the structure section.</span></span>
* <span data-ttu-id="4e6cf-234">**針對在讀取時驗證結構描述 (schema on read) 的資料來源 (具體而言即 Blob 儲存體)**，您可以選擇儲存資料，而不將任何結構描述或類型資訊與資料儲存在一起。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-234">**For schema on read data sources (specifically Blob storage)**, you can choose to store data without storing any schema or type information with the data.</span></span> <span data-ttu-id="4e6cf-235">針對這些類型的資料來源，當您想要將來源資料行與接收資料行對應時，請包含 structure。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-235">For these types of data sources, include structure when you want to map source columns to sink columns.</span></span> <span data-ttu-id="4e6cf-236">當資料集是複製活動的輸入，並且來源資料集的資料類型應該轉換成接收器的原生類型時，也請包含 structure。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-236">Also include structure when the dataset is an input for a copy activity, and data types of source dataset should be converted to native types for the sink.</span></span> 
    
    <span data-ttu-id="4e6cf-237">Data Factory 支援使用下列值在 structure 中提供類型資訊：**Int16、Int32、Int64、Single、Double、Decimal、Byte[]、Boolean、String、Guid、Datetime、Datetimeoffset 及 Timespan**。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-237">Data Factory supports the following values for providing type information in structure: **Int16, Int32, Int64, Single, Double, Decimal, Byte[], Boolean, String, Guid, Datetime, Datetimeoffset, and Timespan**.</span></span> <span data-ttu-id="4e6cf-238">這些值是符合 Common Language Specification (CLS) 規範的 .NET 型類型值。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-238">These values are Common Language Specification (CLS)-compliant, .NET-based type values.</span></span>

<span data-ttu-id="4e6cf-239">Data Factory 會在將資料從來源資料存放區移到接收資料存放區時，自動執行類型轉換。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-239">Data Factory automatically performs type conversions when moving data from a source data store to a sink data store.</span></span> 
  

## <a name="dataset-availability"></a><span data-ttu-id="4e6cf-240">資料集可用性</span><span class="sxs-lookup"><span data-stu-id="4e6cf-240">Dataset availability</span></span>
<span data-ttu-id="4e6cf-241">資料集中的 **availability** 區段會定義資料集的處理時段 (例如每小時、每天或每週)。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-241">The **availability** section in a dataset defines the processing window (for example, hourly, daily, or weekly) for the dataset.</span></span> <span data-ttu-id="4e6cf-242">如需有關活動時段的詳細資訊，請參閱[排程和執行](data-factory-scheduling-and-execution.md)。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-242">For more information about activity windows, see [Scheduling and execution](data-factory-scheduling-and-execution.md).</span></span>

<span data-ttu-id="4e6cf-243">下列 availability 區段指定會每小時產生輸出資料集，或每小時會有可用的輸入資料集：</span><span class="sxs-lookup"><span data-stu-id="4e6cf-243">The following availability section specifies that the output dataset is either produced hourly, or the input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="4e6cf-244">如果管線有下列開始和結束時間：</span><span class="sxs-lookup"><span data-stu-id="4e6cf-244">If the pipeline has the following start and end times:</span></span>  

```json
    "start": "2016-08-25T00:00:00Z",
    "end": "2016-08-25T05:00:00Z",
```

<span data-ttu-id="4e6cf-245">輸出資料集會在管線的開始和結束時間內每小時產生。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-245">The output dataset is produced hourly within the pipeline start and end times.</span></span> <span data-ttu-id="4e6cf-246">因此，這個管線會產生五個資料集配量，每個活動時段 (上午 12 點 - 上午 1 點、上午 1 點 - 上午 2 點、上午 2 點 - 上午 3 點、上午 3 點 - 上午 4 點、上午 4 點 - 上午 5 點) 各一個資料集。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-246">Therefore, there are five dataset slices produced by this pipeline, one for each activity window (12 AM - 1 AM, 1 AM - 2 AM, 2 AM - 3 AM, 3 AM - 4 AM, 4 AM - 5 AM).</span></span> 

<span data-ttu-id="4e6cf-247">下表描述您可以在 [可用性] 區段中使用的屬性：</span><span class="sxs-lookup"><span data-stu-id="4e6cf-247">The following table describes properties you can use in the availability section:</span></span>

| <span data-ttu-id="4e6cf-248">屬性</span><span class="sxs-lookup"><span data-stu-id="4e6cf-248">Property</span></span> | <span data-ttu-id="4e6cf-249">說明</span><span class="sxs-lookup"><span data-stu-id="4e6cf-249">Description</span></span> | <span data-ttu-id="4e6cf-250">必要</span><span class="sxs-lookup"><span data-stu-id="4e6cf-250">Required</span></span> | <span data-ttu-id="4e6cf-251">預設值</span><span class="sxs-lookup"><span data-stu-id="4e6cf-251">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4e6cf-252">frequency</span><span class="sxs-lookup"><span data-stu-id="4e6cf-252">frequency</span></span> |<span data-ttu-id="4e6cf-253">指定資料集配量生產的時間單位。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-253">Specifies the time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="4e6cf-254"><b>支援的頻率</b>：Minute、Hour、Day、Week、Month</span><span class="sxs-lookup"><span data-stu-id="4e6cf-254"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="4e6cf-255">是</span><span class="sxs-lookup"><span data-stu-id="4e6cf-255">Yes</span></span> |<span data-ttu-id="4e6cf-256">NA</span><span class="sxs-lookup"><span data-stu-id="4e6cf-256">NA</span></span> |
| <span data-ttu-id="4e6cf-257">interval</span><span class="sxs-lookup"><span data-stu-id="4e6cf-257">interval</span></span> |<span data-ttu-id="4e6cf-258">指定頻率的倍數。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-258">Specifies a multiplier for frequency.</span></span><br/><br/><span data-ttu-id="4e6cf-259">「頻率 x 間隔」會決定產生配量的頻率。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-259">"Frequency x interval" determines how often the slice is produced.</span></span> <span data-ttu-id="4e6cf-260">例如，如果您需要將資料集以每小時為單位來切割，請將 <b>frequency</b> 設定為 <b>Hour</b>，將 <b>interval</b> 設定為 <b>1</b>。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-260">For example, if you need the dataset to be sliced on an hourly basis, you set <b>frequency</b> to <b>Hour</b>, and <b>interval</b> to <b>1</b>.</span></span><br/><br/><span data-ttu-id="4e6cf-261">請注意，如果您將 **frequency** 指定為 **Minute**，則應該將 interval 設定為不小於 15。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-261">Note that if you specify **frequency** as **Minute**, you should set the interval to no less than 15.</span></span> |<span data-ttu-id="4e6cf-262">是</span><span class="sxs-lookup"><span data-stu-id="4e6cf-262">Yes</span></span> |<span data-ttu-id="4e6cf-263">NA</span><span class="sxs-lookup"><span data-stu-id="4e6cf-263">NA</span></span> |
| <span data-ttu-id="4e6cf-264">style</span><span class="sxs-lookup"><span data-stu-id="4e6cf-264">style</span></span> |<span data-ttu-id="4e6cf-265">指定應該在間隔的開始還是結束時產生配量。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-265">Specifies whether the slice should be produced at the start or end of the interval.</span></span><ul><li><span data-ttu-id="4e6cf-266">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="4e6cf-266">StartOfInterval</span></span></li><li><span data-ttu-id="4e6cf-267">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="4e6cf-267">EndOfInterval</span></span></li></ul><span data-ttu-id="4e6cf-268">如果將 **frequency** 設定為 **Month**，並將 **style** 設定為 **EndOfInterval**，就會在當月的最後一天產生配量。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-268">If **frequency** is set to **Month**, and **style** is set to **EndOfInterval**, the slice is produced on the last day of month.</span></span> <span data-ttu-id="4e6cf-269">如果將 **style** 設定為 **StartOfInterval**，則會在當月的第一天產生配量。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-269">If **style** is set to **StartOfInterval**, the slice is produced on the first day of month.</span></span><br/><br/><span data-ttu-id="4e6cf-270">如果將 **frequency** 設定為 **Day**，並將 **style** 設定為 **EndOfInterval**，就會在當天的最後一小時產生配量。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-270">If **frequency** is set to **Day**, and **style** is set to **EndOfInterval**, the slice is produced in the last hour of the day.</span></span><br/><br/><span data-ttu-id="4e6cf-271">如果 **frequency** 設定為 **Hour**，並將 **style** 設定為 **EndOfInterval**，則會在該小時結束時產生配量。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-271">If **frequency** is set to **Hour**, and **style** is set to **EndOfInterval**, the slice is produced at the end of the hour.</span></span> <span data-ttu-id="4e6cf-272">例如，就下午 1 點 - 2 點期間的配量而言，會在下午 2 點產生配量。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-272">For example, for a slice for the 1 PM - 2 PM period, the slice is produced at 2 PM.</span></span> |<span data-ttu-id="4e6cf-273">否</span><span class="sxs-lookup"><span data-stu-id="4e6cf-273">No</span></span> |<span data-ttu-id="4e6cf-274">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="4e6cf-274">EndOfInterval</span></span> |
| <span data-ttu-id="4e6cf-275">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="4e6cf-275">anchorDateTime</span></span> |<span data-ttu-id="4e6cf-276">定義排程器用來計算資料集配量界限的時間絕對位置。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-276">Defines the absolute position in time used by the scheduler to compute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="4e6cf-277">請注意，如果此屬性有比所指定頻率更細微的日期部分，則系統會忽略那些更細微的部分。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-277">Note that if this propoerty has date parts that are more granular than the specified frequency, the more granular parts are ignored.</span></span> <span data-ttu-id="4e6cf-278">例如，如果 **interval** 為 **hourly** (frequency: hour 且 interval: 1)，而且 **anchorDateTime** 包含**分鐘和秒鐘**，則系統會忽略 **anchorDateTime** 的分鐘和秒鐘部分。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-278">For example, if the **interval** is **hourly** (frequency: hour and interval: 1), and the **anchorDateTime** contains **minutes and seconds**, then the minutes and seconds parts of **anchorDateTime** are ignored.</span></span> |<span data-ttu-id="4e6cf-279">否</span><span class="sxs-lookup"><span data-stu-id="4e6cf-279">No</span></span> |<span data-ttu-id="4e6cf-280">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="4e6cf-280">01/01/0001</span></span> |
| <span data-ttu-id="4e6cf-281">Offset</span><span class="sxs-lookup"><span data-stu-id="4e6cf-281">offset</span></span> |<span data-ttu-id="4e6cf-282">所有資料集配量的開始和結束移位所依據的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-282">Timespan by which the start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="4e6cf-283">請注意，如果同時指定 **anchorDateTime** 和 **offset**，則結果會是合併的位移。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-283">Note that if both **anchorDateTime** and **offset** are specified, the result is the combined shift.</span></span> |<span data-ttu-id="4e6cf-284">否</span><span class="sxs-lookup"><span data-stu-id="4e6cf-284">No</span></span> |<span data-ttu-id="4e6cf-285">NA</span><span class="sxs-lookup"><span data-stu-id="4e6cf-285">NA</span></span> |

### <a name="offset-example"></a><span data-ttu-id="4e6cf-286">位移範例</span><span class="sxs-lookup"><span data-stu-id="4e6cf-286">offset example</span></span>
<span data-ttu-id="4e6cf-287">根據預設，每日 (`"frequency": "Day", "interval": 1`) 配量的開始時間是「國際標准時間」(UTC) 上午 12 點 (午夜)。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-287">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM (midnight) Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="4e6cf-288">如果您希望將開始時間改為 UTC 時間上午 6 點，請依照下列程式碼片段所示設定位移：</span><span class="sxs-lookup"><span data-stu-id="4e6cf-288">If you want the start time to be 6 AM UTC time instead, set the offset as shown in the following snippet:</span></span> 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a><span data-ttu-id="4e6cf-289">anchorDateTime 範例</span><span class="sxs-lookup"><span data-stu-id="4e6cf-289">anchorDateTime example</span></span>
<span data-ttu-id="4e6cf-290">在下列範例中，會每隔 23 小時產生一次資料集。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-290">In the following example, the dataset is produced once every 23 hours.</span></span> <span data-ttu-id="4e6cf-291">第一個配量會在 **anchorDateTime** 所指定的時間 (已設定為 `2017-04-19T08:00:00` (UTC)) 開始。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-291">The first slice starts at the time specified by **anchorDateTime**, which is set to `2017-04-19T08:00:00` (UTC).</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a><span data-ttu-id="4e6cf-292">位移/樣式範例</span><span class="sxs-lookup"><span data-stu-id="4e6cf-292">offset/style example</span></span>
<span data-ttu-id="4e6cf-293">下列資料集是每月資料集，會在每月 3 號的上午 8:00 (`3.08:00:00`) 產生：</span><span class="sxs-lookup"><span data-stu-id="4e6cf-293">The following dataset is monthly, and is produced on the 3rd of every month at 8:00 AM (`3.08:00:00`):</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

## <span data-ttu-id="4e6cf-294"><a name="Policy"></a>資料集原則</span><span class="sxs-lookup"><span data-stu-id="4e6cf-294"><a name="Policy"></a>Dataset policy</span></span>
<span data-ttu-id="4e6cf-295">資料集定義中的 **policy** 區段會定義資料集配量必須符合的準則或條件。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-295">The **policy** section in the dataset definition defines the criteria or the condition that the dataset slices must fulfill.</span></span>

### <a name="validation-policies"></a><span data-ttu-id="4e6cf-296">驗證原則</span><span class="sxs-lookup"><span data-stu-id="4e6cf-296">Validation policies</span></span>
| <span data-ttu-id="4e6cf-297">原則名稱</span><span class="sxs-lookup"><span data-stu-id="4e6cf-297">Policy name</span></span> | <span data-ttu-id="4e6cf-298">說明</span><span class="sxs-lookup"><span data-stu-id="4e6cf-298">Description</span></span> | <span data-ttu-id="4e6cf-299">適用於</span><span class="sxs-lookup"><span data-stu-id="4e6cf-299">Applied to</span></span> | <span data-ttu-id="4e6cf-300">必要</span><span class="sxs-lookup"><span data-stu-id="4e6cf-300">Required</span></span> | <span data-ttu-id="4e6cf-301">預設值</span><span class="sxs-lookup"><span data-stu-id="4e6cf-301">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="4e6cf-302">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="4e6cf-302">minimumSizeMB</span></span> |<span data-ttu-id="4e6cf-303">驗證「Azure Blob 儲存體」中的資料是否符合大小下限需求 (以 MB 為單位)。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-303">Validates that the data in **Azure Blob storage** meets the minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="4e6cf-304">Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="4e6cf-304">Azure Blob storage</span></span> |<span data-ttu-id="4e6cf-305">否</span><span class="sxs-lookup"><span data-stu-id="4e6cf-305">No</span></span> |<span data-ttu-id="4e6cf-306">NA</span><span class="sxs-lookup"><span data-stu-id="4e6cf-306">NA</span></span> |
| <span data-ttu-id="4e6cf-307">minimumRows</span><span class="sxs-lookup"><span data-stu-id="4e6cf-307">minimumRows</span></span> |<span data-ttu-id="4e6cf-308">驗證 **Azure SQL Database** 或 **Azure 資料表**中的資料是否包含最小的資料列數。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-308">Validates that the data in an **Azure SQL database** or an **Azure table** contains the minimum number of rows.</span></span> |<ul><li><span data-ttu-id="4e6cf-309">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="4e6cf-309">Azure SQL database</span></span></li><li><span data-ttu-id="4e6cf-310">Azure 資料表</span><span class="sxs-lookup"><span data-stu-id="4e6cf-310">Azure table</span></span></li></ul> |<span data-ttu-id="4e6cf-311">否</span><span class="sxs-lookup"><span data-stu-id="4e6cf-311">No</span></span> |<span data-ttu-id="4e6cf-312">NA</span><span class="sxs-lookup"><span data-stu-id="4e6cf-312">NA</span></span> |

#### <a name="examples"></a><span data-ttu-id="4e6cf-313">範例</span><span class="sxs-lookup"><span data-stu-id="4e6cf-313">Examples</span></span>
<span data-ttu-id="4e6cf-314">**minimumSizeMB：**</span><span class="sxs-lookup"><span data-stu-id="4e6cf-314">**minimumSizeMB:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="4e6cf-315">**minimumRows：**</span><span class="sxs-lookup"><span data-stu-id="4e6cf-315">**minimumRows:**</span></span>

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

### <a name="external-datasets"></a><span data-ttu-id="4e6cf-316">外部資料集</span><span class="sxs-lookup"><span data-stu-id="4e6cf-316">External datasets</span></span>
<span data-ttu-id="4e6cf-317">外部資料集是並非由 Data Factory 中的執行中管線所產生的資料集。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-317">External datasets are the ones that are not produced by a running pipeline in the data factory.</span></span> <span data-ttu-id="4e6cf-318">如果資料集標示為**外部**，則可定義 **ExternalData** 原則來影響資料集配量可用性的行為。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-318">If the dataset is marked as **external**, the **ExternalData** policy may be defined to influence the behavior of the dataset slice availability.</span></span>

<span data-ttu-id="4e6cf-319">除非資料集是由 Data Factory 所產生，否則應該標示為「外部」。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-319">Unless a dataset is being produced by Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="4e6cf-320">除非會使用活動或管線鏈結，否則此設定通常會套用到管線中第一個活動的輸入。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-320">This setting generally applies to the inputs of first activity in a pipeline, unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="4e6cf-321">名稱</span><span class="sxs-lookup"><span data-stu-id="4e6cf-321">Name</span></span> | <span data-ttu-id="4e6cf-322">說明</span><span class="sxs-lookup"><span data-stu-id="4e6cf-322">Description</span></span> | <span data-ttu-id="4e6cf-323">必要</span><span class="sxs-lookup"><span data-stu-id="4e6cf-323">Required</span></span> | <span data-ttu-id="4e6cf-324">預設值</span><span class="sxs-lookup"><span data-stu-id="4e6cf-324">Default value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4e6cf-325">dataDelay</span><span class="sxs-lookup"><span data-stu-id="4e6cf-325">dataDelay</span></span> |<span data-ttu-id="4e6cf-326">要延遲所指定配量之外部資料可用性檢查的時間。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-326">The time to delay the check on the availability of the external data for the given slice.</span></span> <span data-ttu-id="4e6cf-327">例如，您可以使用此設定來延遲每小時檢查。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-327">For example, you can delay an hourly check by using this setting.</span></span><br/><br/><span data-ttu-id="4e6cf-328">此設定僅適用於當前的時間。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-328">The setting only applies to the present time.</span></span>  <span data-ttu-id="4e6cf-329">例如，如果現在時間是下午 1:00，且此值是 10 分鐘，驗證就會在下午 1:10 開始。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-329">For example, if it is 1:00 PM right now and this value is 10 minutes, the validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="4e6cf-330">請注意，此設定不會影響過去的配量。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-330">Note that this setting does not affect slices in the past.</span></span> <span data-ttu-id="4e6cf-331">針對**配量結束時間** + **dataDelay** < **現在**的配量，處理時將不會有任何延遲。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-331">Slices with **Slice End Time** + **dataDelay** < **Now** are processed without any delay.</span></span><br/><br/><span data-ttu-id="4e6cf-332">時間如果大於 23:59 小時，應該使用 `day.hours:minutes:seconds` 格式來指定。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-332">Times greater than 23:59 hours should be specified by using the `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="4e6cf-333">例如，若要指定 24 小時，不要使用 24:00:00。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-333">For example, to specify 24 hours, don't use 24:00:00.</span></span> <span data-ttu-id="4e6cf-334">請改用 1.00:00:00。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-334">Instead, use 1.00:00:00.</span></span> <span data-ttu-id="4e6cf-335">如果您使用 24:00:00，這會視同 24 天 (24.00:00:00)。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-335">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="4e6cf-336">如為 1 天又 4 小時，請指定 1:04:00:00。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-336">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="4e6cf-337">否</span><span class="sxs-lookup"><span data-stu-id="4e6cf-337">No</span></span> |<span data-ttu-id="4e6cf-338">0</span><span class="sxs-lookup"><span data-stu-id="4e6cf-338">0</span></span> |
| <span data-ttu-id="4e6cf-339">retryInterval</span><span class="sxs-lookup"><span data-stu-id="4e6cf-339">retryInterval</span></span> |<span data-ttu-id="4e6cf-340">失敗與下一次嘗試之間的等待時間。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-340">The wait time between a failure and the next attempt.</span></span> <span data-ttu-id="4e6cf-341">此設定適用於當前的時間。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-341">This setting applies to present time.</span></span> <span data-ttu-id="4e6cf-342">如果上一次嘗試失敗，則下一次嘗試將會在 **retryInterval** 期間之後。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-342">If the previous try failed, the next try is after the **retryInterval** period.</span></span> <br/><br/><span data-ttu-id="4e6cf-343">如果現在是下午 1:00，我們會開始第一次嘗試。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-343">If it is 1:00 PM right now, we begin the first try.</span></span> <span data-ttu-id="4e6cf-344">如果完成第一次驗證檢查的持續時間是 1 分鐘且作業失敗，則下一次重試會在 1:00 + 1 分鐘 (持續時間) + 1 分鐘 (重試間隔) = 下午 1:02。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-344">If the duration to complete the first validation check is 1 minute and the operation failed, the next retry is at 1:00 + 1min (duration) + 1min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="4e6cf-345">若是過去的配量，則不會有任何延遲。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-345">For slices in the past, there is no delay.</span></span> <span data-ttu-id="4e6cf-346">重試會立即發生。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-346">The retry happens immediately.</span></span> |<span data-ttu-id="4e6cf-347">否</span><span class="sxs-lookup"><span data-stu-id="4e6cf-347">No</span></span> |<span data-ttu-id="4e6cf-348">00:01:00 (1 分鐘)</span><span class="sxs-lookup"><span data-stu-id="4e6cf-348">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="4e6cf-349">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="4e6cf-349">retryTimeout</span></span> |<span data-ttu-id="4e6cf-350">每次重試嘗試的逾時。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-350">The timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="4e6cf-351">如果此屬性是設定為 10 分鐘，則應該在 10 分鐘內完成驗證。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-351">If this property is set to 10 minutes, the validation should be completed within 10 minutes.</span></span> <span data-ttu-id="4e6cf-352">如果花超過 10 分鐘來執行驗證，則重試會逾時。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-352">If it takes longer than 10 minutes to perform the validation, the retry times out.</span></span><br/><br/><span data-ttu-id="4e6cf-353">如果所有驗證嘗試都逾時，配量就會標示為 **TimedOut**。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-353">If all attempts for the validation time out, the slice is marked as **TimedOut**.</span></span> |<span data-ttu-id="4e6cf-354">否</span><span class="sxs-lookup"><span data-stu-id="4e6cf-354">No</span></span> |<span data-ttu-id="4e6cf-355">00:10:00 (10 分鐘)</span><span class="sxs-lookup"><span data-stu-id="4e6cf-355">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="4e6cf-356">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="4e6cf-356">maximumRetry</span></span> |<span data-ttu-id="4e6cf-357">檢查外部資料可用性的次數。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-357">The number of times to check for the availability of the external data.</span></span> <span data-ttu-id="4e6cf-358">允許的最大值為 10。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-358">The maximum allowed value is 10.</span></span> |<span data-ttu-id="4e6cf-359">否</span><span class="sxs-lookup"><span data-stu-id="4e6cf-359">No</span></span> |<span data-ttu-id="4e6cf-360">3</span><span class="sxs-lookup"><span data-stu-id="4e6cf-360">3</span></span> |


## <a name="create-datasets"></a><span data-ttu-id="4e6cf-361">建立資料集</span><span class="sxs-lookup"><span data-stu-id="4e6cf-361">Create datasets</span></span>
<span data-ttu-id="4e6cf-362">您可以使用下列其中一項工具或 SDK 來建立資料集：</span><span class="sxs-lookup"><span data-stu-id="4e6cf-362">You can create datasets by using one of these tools or SDKs:</span></span> 

- <span data-ttu-id="4e6cf-363">複製精靈</span><span class="sxs-lookup"><span data-stu-id="4e6cf-363">Copy Wizard</span></span> 
- <span data-ttu-id="4e6cf-364">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="4e6cf-364">Azure portal</span></span>
- <span data-ttu-id="4e6cf-365">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4e6cf-365">Visual Studio</span></span>
- <span data-ttu-id="4e6cf-366">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e6cf-366">PowerShell</span></span>
- <span data-ttu-id="4e6cf-367">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="4e6cf-367">Azure Resource Manager template</span></span>
- <span data-ttu-id="4e6cf-368">REST API</span><span class="sxs-lookup"><span data-stu-id="4e6cf-368">REST API</span></span>
- <span data-ttu-id="4e6cf-369">.NET API</span><span class="sxs-lookup"><span data-stu-id="4e6cf-369">.NET API</span></span>

<span data-ttu-id="4e6cf-370">如需使用上述其中一項工具或 SDK 來建立管線和資料集的逐步指示，請參閱下列教學課程：</span><span class="sxs-lookup"><span data-stu-id="4e6cf-370">See the following tutorials for step-by-step instructions for creating pipelines and datasets by using one of these tools or SDKs:</span></span>
 
- [<span data-ttu-id="4e6cf-371">使用資料轉換活動來建置管線</span><span class="sxs-lookup"><span data-stu-id="4e6cf-371">Build a pipeline with a data transformation activity</span></span>](data-factory-build-your-first-pipeline.md)
- [<span data-ttu-id="4e6cf-372">使用資料移動活動來建置管線</span><span class="sxs-lookup"><span data-stu-id="4e6cf-372">Build a pipeline with a data movement activity</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

<span data-ttu-id="4e6cf-373">建置及部署管線之後，您便可以使用 Azure 入口網站刀鋒視窗或「監視與管理」應用程式，來管理及監視管線。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-373">After a pipeline is created and deployed, you can manage and monitor your pipelines by using the Azure portal blades, or the Monitoring and Management app.</span></span> <span data-ttu-id="4e6cf-374">如需逐步指示，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="4e6cf-374">See the following topics for step-by-step instructions:</span></span> 

- [<span data-ttu-id="4e6cf-375">使用 Azure 入口網站刀鋒視窗來監視和管理管線</span><span class="sxs-lookup"><span data-stu-id="4e6cf-375">Monitor and manage pipelines by using Azure portal blades</span></span>](data-factory-monitor-manage-pipelines.md)
- [<span data-ttu-id="4e6cf-376">使用監視及管理應用程式，以監視和管理管線</span><span class="sxs-lookup"><span data-stu-id="4e6cf-376">Monitor and manage pipelines by using the Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)


## <a name="scoped-datasets"></a><span data-ttu-id="4e6cf-377">範圍資料集</span><span class="sxs-lookup"><span data-stu-id="4e6cf-377">Scoped datasets</span></span>
<span data-ttu-id="4e6cf-378">您可以使用 **datasets** 屬性來建立範圍設定為管線的資料集。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-378">You can create datasets that are scoped to a pipeline by using the **datasets** property.</span></span> <span data-ttu-id="4e6cf-379">這些資料集僅供此管線內的活動使用，不供其他管線中的活動使用。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-379">These datasets can only be used by activities within this pipeline, not by activities in other pipelines.</span></span> <span data-ttu-id="4e6cf-380">下列範例會定義一個管線，此管線具有兩個要在管線內使用的資料集 (InputDataset-rdc 和 OutputDataset-rdc)。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-380">The following example defines a pipeline with two datasets (InputDataset-rdc and OutputDataset-rdc) to be used within the pipeline.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="4e6cf-381">只有單次管線 (**pipelineMode** 已設定為 **OneTime**) 才支援範圍資料集。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-381">Scoped datasets are supported only with one-time pipelines (where **pipelineMode** is set to **OneTime**).</span></span> <span data-ttu-id="4e6cf-382">如需詳細資訊，請參閱 [一次性管線](data-factory-create-pipelines.md#onetime-pipeline) 。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-382">See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details.</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="4e6cf-383">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4e6cf-383">Next steps</span></span>
- <span data-ttu-id="4e6cf-384">如需有關管線的詳細資訊，請參閱[建立管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-384">For more information about pipelines, see [Create pipelines](data-factory-create-pipelines.md).</span></span> 
- <span data-ttu-id="4e6cf-385">如需有關管線的排程和執行方式的詳細資訊，請參閱 [Azure Data Factory 中的排程和執行](data-factory-scheduling-and-execution.md)。</span><span class="sxs-lookup"><span data-stu-id="4e6cf-385">For more information about how pipelines are scheduled and executed, see [Scheduling and execution in Azure Data Factory](data-factory-scheduling-and-execution.md).</span></span> 
