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
# <a name="pipelines-and-activities-in-azure-data-factory"></a><span data-ttu-id="dd2e8-105">Azure Data Factory 中的管線及活動</span><span class="sxs-lookup"><span data-stu-id="dd2e8-105">Pipelines and Activities in Azure Data Factory</span></span>
<span data-ttu-id="dd2e8-106">這篇文章可協助您了解管線和 Azure Data Factory 中的活動，並針對您的資料移動和資料處理的案例中使用 tooconstruct 端對端資料驅動型工作流程。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-106">This article helps you understand pipelines and activities in Azure Data Factory and use them tooconstruct end-to-end data-driven workflows for your data movement and data processing scenarios.</span></span>  

> [!NOTE]
> <span data-ttu-id="dd2e8-107">本文假設您已經完成[簡介 tooAzure Data Factory](data-factory-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-107">This article assumes that you have gone through [Introduction tooAzure Data Factory](data-factory-introduction.md).</span></span> <span data-ttu-id="dd2e8-108">如果您沒有建立 Data Factory 的實作經驗，瀏覽[資料轉換教學課程](data-factory-build-your-first-pipeline.md)和/或[資料移動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)將可協助您進一步了解這篇文章。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-108">If you do not have hands-on-experience with creating data factories, going through [data transformation tutorial](data-factory-build-your-first-pipeline.md) and/or [data movement tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) would help you understand this article better.</span></span>  

## <a name="overview"></a><span data-ttu-id="dd2e8-109">概觀</span><span class="sxs-lookup"><span data-stu-id="dd2e8-109">Overview</span></span>
<span data-ttu-id="dd2e8-110">資料處理站可以有一或多個管線。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-110">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="dd2e8-111">管線是一起執行某個工作的活動所組成的邏輯群組。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-111">A pipeline is a logical grouping of activities that together perform a task.</span></span> <span data-ttu-id="dd2e8-112">在管線中的 hello 活動定義動作 tooperform 對您的資料。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-112">hello activities in a pipeline define actions tooperform on your data.</span></span> <span data-ttu-id="dd2e8-113">例如，您可能會使用複製活動 toocopy 資料從內部部署 SQL Server tooan Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-113">For example, you may use a copy activity toocopy data from an on-premises SQL Server tooan Azure Blob Storage.</span></span> <span data-ttu-id="dd2e8-114">然後，使用 Azure HDInsight 叢集 tooprocess/轉換資料執行 Hive 指令碼，從 hello blob 儲存體 tooproduce 輸出資料的 Hive 活動。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-114">Then, use a Hive activity that runs a Hive script on an Azure HDInsight cluster tooprocess/transform data from hello blob storage tooproduce output data.</span></span> <span data-ttu-id="dd2e8-115">最後，使用第二個複製活動 toocopy hello 輸出資料 tooan Azure SQL 資料倉儲內建報表方案的商業智慧 (BI) 之上。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-115">Finally, use a second copy activity toocopy hello output data tooan Azure SQL Data Warehouse on top of which business intelligence (BI) reporting solutions are built.</span></span> 

<span data-ttu-id="dd2e8-116">一個活動可以接受零個或多個輸入[資料集](data-factory-create-datasets.md)，並且會產生一個或多個輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-116">An activity can take zero or more input [datasets](data-factory-create-datasets.md) and produce one or more output [datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="dd2e8-117">hello 下圖顯示 hello 管線、 活動和資料集之間的關聯性 Data Factory 中：</span><span class="sxs-lookup"><span data-stu-id="dd2e8-117">hello following diagram shows hello relationship between pipeline, activity, and dataset in Data Factory:</span></span> 

![管線、活動及資料集之間的關聯性](media/data-factory-create-pipelines/relationship-pipeline-activity-dataset.png)

<span data-ttu-id="dd2e8-119">管線可讓您 toomanage 活動為一組，而不是每個個別。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-119">A pipeline allows you toomanage activities as a set instead of each one individually.</span></span> <span data-ttu-id="dd2e8-120">比方說，您可以部署、 排程、 暫停和繼續管線，而不是分別處理 hello 管線中的活動。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-120">For example, you can deploy, schedule, suspend, and resume a pipeline, instead of dealing with activities in hello pipeline independently.</span></span>

<span data-ttu-id="dd2e8-121">Data Factory 支援兩種活動類型︰資料移動活動和資料轉換活動。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-121">Data Factory supports two types of activities: data movement activities and data transformation activities.</span></span> <span data-ttu-id="dd2e8-122">每個活動可以有零個或多個輸入[資料集](data-factory-create-datasets.md)，並且會產生一個或多個輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-122">Each activity can have zero or more input [datasets](data-factory-create-datasets.md) and produce one or more output datasets.</span></span>

<span data-ttu-id="dd2e8-123">輸入資料集代表 hello hello 管線中活動的輸入和輸出資料集代表 hello hello 活動的輸出。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-123">An input dataset represents hello input for an activity in hello pipeline and an output dataset represents hello output for hello activity.</span></span> <span data-ttu-id="dd2e8-124">資料集可識別資料表、檔案、資料夾和文件等各種資料存放區中的資料。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-124">Datasets identify data within different data stores, such as tables, files, folders, and documents.</span></span> <span data-ttu-id="dd2e8-125">建立資料集之後，您可以將其與管線中的活動搭配使用。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-125">After you create a dataset, you can use it with activities in a pipeline.</span></span> <span data-ttu-id="dd2e8-126">例如，資料集可以是複製活動或 HDInsightHive 活動的輸入/輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-126">For example, a dataset can be an input/output dataset of a Copy Activity or an HDInsightHive Activity.</span></span> <span data-ttu-id="dd2e8-127">如需有關資料集的詳細資訊，請參閱 [Azure Data Factory 中的資料集](data-factory-create-datasets.md)一文。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-127">For more information about datasets, see [Datasets in Azure Data Factory](data-factory-create-datasets.md) article.</span></span>

### <a name="data-movement-activities"></a><span data-ttu-id="dd2e8-128">資料移動活動</span><span class="sxs-lookup"><span data-stu-id="dd2e8-128">Data movement activities</span></span>
<span data-ttu-id="dd2e8-129">Data Factory 中的複製活動會將資料從來源資料存放區 tooa 接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-129">Copy Activity in Data Factory copies data from a source data store tooa sink data store.</span></span> <span data-ttu-id="dd2e8-130">Data Factory 支援下列資料存放區的 hello。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-130">Data Factory supports hello following data stores.</span></span> <span data-ttu-id="dd2e8-131">從任何來源的資料可以寫入 tooany 接收。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-131">Data from any source can be written tooany sink.</span></span> <span data-ttu-id="dd2e8-132">按一下 [資料存放區 toolearn 如何 toocopy 資料 tooand 從該存放區。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-132">Click a data store toolearn how toocopy data tooand from that store.</span></span>

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> <span data-ttu-id="dd2e8-133">資料存放區使用 * 可在內部部署或 Azure IaaS 上，因此需要您 tooinstall[資料管理閘道器](data-factory-data-management-gateway.md)在內部部署/Azure IaaS 電腦上。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-133">Data stores with * can be on-premises or on Azure IaaS, and require you tooinstall [Data Management Gateway](data-factory-data-management-gateway.md) on an on-premises/Azure IaaS machine.</span></span>

<span data-ttu-id="dd2e8-134">如需詳細資訊，請參閱[資料移動活動](data-factory-data-movement-activities.md)文章。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-134">For more information, see [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span>

### <a name="data-transformation-activities"></a><span data-ttu-id="dd2e8-135">資料轉換活動</span><span class="sxs-lookup"><span data-stu-id="dd2e8-135">Data transformation activities</span></span>
[!INCLUDE [data-factory-transformation-activities](../../includes/data-factory-transformation-activities.md)]

<span data-ttu-id="dd2e8-136">如需詳細資訊，請參閱[資料轉換活動](data-factory-data-transformation-activities.md)文章。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-136">For more information, see [Data Transformation Activities](data-factory-data-transformation-activities.md) article.</span></span>

### <a name="custom-net-activities"></a><span data-ttu-id="dd2e8-137">自訂 .NET 活動</span><span class="sxs-lookup"><span data-stu-id="dd2e8-137">Custom .NET activities</span></span> 
<span data-ttu-id="dd2e8-138">如果您需要 toomove 資料/從資料存放區 hello 複製活動的不支援，或使用您自己的邏輯轉換資料、 建立**自訂.NET 活動**。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-138">If you need toomove data to/from a data store that hello Copy Activity doesn't support, or transform data using your own logic, create a **custom .NET activity**.</span></span> <span data-ttu-id="dd2e8-139">如需有關建立及使用自訂活動的詳細資料，請參閱 [在 Azure Data Factory 管線中使用自訂活動](data-factory-use-custom-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-139">For details on creating and using a custom activity, see [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md).</span></span>

## <a name="schedule-pipelines"></a><span data-ttu-id="dd2e8-140">建立管線排程</span><span class="sxs-lookup"><span data-stu-id="dd2e8-140">Schedule pipelines</span></span>
<span data-ttu-id="dd2e8-141">管線僅在其「開始」時間與「結束」時間之間有作用。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-141">A pipeline is active only between its **start** time and **end** time.</span></span> <span data-ttu-id="dd2e8-142">它不會執行 hello 開始時間之前或之後 hello 結束時間。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-142">It is not executed before hello start time or after hello end time.</span></span> <span data-ttu-id="dd2e8-143">如果 hello 管線已暫停，它不會執行而不受限於其開始和結束時間。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-143">If hello pipeline is paused, it does not get executed irrespective of its start and end time.</span></span> <span data-ttu-id="dd2e8-144">為管線 toorun，它應該暫停。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-144">For a pipeline toorun, it should not be paused.</span></span> <span data-ttu-id="dd2e8-145">請參閱[排程與執行](data-factory-scheduling-and-execution.md)toounderstand 排程和執行 Azure Data Factory 中運作的方式。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-145">See [Scheduling and Execution](data-factory-scheduling-and-execution.md) toounderstand how scheduling and execution works in Azure Data Factory.</span></span>

## <a name="pipeline-json"></a><span data-ttu-id="dd2e8-146">管線 JSON</span><span class="sxs-lookup"><span data-stu-id="dd2e8-146">Pipeline JSON</span></span>
<span data-ttu-id="dd2e8-147">讓我們來深入探討如何定義 JSON 格式的管線。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-147">Let us take a closer look on how a pipeline is defined in JSON format.</span></span> <span data-ttu-id="dd2e8-148">管線的 hello 泛型結構如下所示：</span><span class="sxs-lookup"><span data-stu-id="dd2e8-148">hello generic structure for a pipeline looks as follows:</span></span>

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

| <span data-ttu-id="dd2e8-149">Tag</span><span class="sxs-lookup"><span data-stu-id="dd2e8-149">Tag</span></span> | <span data-ttu-id="dd2e8-150">說明</span><span class="sxs-lookup"><span data-stu-id="dd2e8-150">Description</span></span> | <span data-ttu-id="dd2e8-151">必要</span><span class="sxs-lookup"><span data-stu-id="dd2e8-151">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dd2e8-152">名稱</span><span class="sxs-lookup"><span data-stu-id="dd2e8-152">name</span></span> |<span data-ttu-id="dd2e8-153">Hello 管線的名稱。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-153">Name of hello pipeline.</span></span> <span data-ttu-id="dd2e8-154">指定代表 hello 管線的 hello 動作的名稱執行。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-154">Specify a name that represents hello action that hello pipeline performs.</span></span> <br/><ul><li><span data-ttu-id="dd2e8-155">字元數目上限︰260</span><span class="sxs-lookup"><span data-stu-id="dd2e8-155">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="dd2e8-156">開頭必須為字母、數字或底線 (_)</span><span class="sxs-lookup"><span data-stu-id="dd2e8-156">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="dd2e8-157">不允許使用下列字元：“.”、“+”、“?”、“/”、“<”、”>”、”*”、”%”、”&”、”:”、”\\”</span><span class="sxs-lookup"><span data-stu-id="dd2e8-157">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="dd2e8-158">是</span><span class="sxs-lookup"><span data-stu-id="dd2e8-158">Yes</span></span> |
| <span data-ttu-id="dd2e8-159">說明</span><span class="sxs-lookup"><span data-stu-id="dd2e8-159">description</span></span> | <span data-ttu-id="dd2e8-160">指定描述用於何種 hello 管線的 hello 文字。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-160">Specify hello text describing what hello pipeline is used for.</span></span> |<span data-ttu-id="dd2e8-161">是</span><span class="sxs-lookup"><span data-stu-id="dd2e8-161">Yes</span></span> |
| <span data-ttu-id="dd2e8-162">活動</span><span class="sxs-lookup"><span data-stu-id="dd2e8-162">activities</span></span> | <span data-ttu-id="dd2e8-163">hello**活動**區段都可以擁有定義於其中的一個或多個活動。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-163">hello **activities** section can have one or more activities defined within it.</span></span> <span data-ttu-id="dd2e8-164">請參閱 hello hello 活動 JSON 項目的詳細資料的下一節。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-164">See hello next section for details about hello activities JSON element.</span></span> | <span data-ttu-id="dd2e8-165">是</span><span class="sxs-lookup"><span data-stu-id="dd2e8-165">Yes</span></span> |  
| <span data-ttu-id="dd2e8-166">start</span><span class="sxs-lookup"><span data-stu-id="dd2e8-166">start</span></span> | <span data-ttu-id="dd2e8-167">開始日期-時間 hello 管線。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-167">Start date-time for hello pipeline.</span></span> <span data-ttu-id="dd2e8-168">必須使用 [ISO 格式](http://en.wikipedia.org/wiki/ISO_8601)。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-168">Must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="dd2e8-169">例如： `2016-10-14T16:32:41Z`。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-169">For example: `2016-10-14T16:32:41Z`.</span></span> <br/><br/><span data-ttu-id="dd2e8-170">很可能 toospecify 本地時間，例如預估時間。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-170">It is possible toospecify a local time, for example an EST time.</span></span> <span data-ttu-id="dd2e8-171">範例如下︰`2016-02-27T06:00:00-05:00`，這是美加東部標準時間上午 6 點。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-171">Here is an example: `2016-02-27T06:00:00-05:00`", which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="dd2e8-172">hello 開始和結束屬性一起指定 hello 管線的作用期間。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-172">hello start and end properties together specify active period for hello pipeline.</span></span> <span data-ttu-id="dd2e8-173">輸出配量只會在作用中期間內產生。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-173">Output slices are only produced with in this active period.</span></span> |<span data-ttu-id="dd2e8-174">否</span><span class="sxs-lookup"><span data-stu-id="dd2e8-174">No</span></span><br/><br/><span data-ttu-id="dd2e8-175">如果您指定 hello 結束屬性的值，您必須指定 hello 開始屬性值。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-175">If you specify a value for hello end property, you must specify value for hello start property.</span></span><br/><br/><span data-ttu-id="dd2e8-176">hello 開始和結束時間可以是空的 toocreate 管線。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-176">hello start and end times can both be empty toocreate a pipeline.</span></span> <span data-ttu-id="dd2e8-177">您必須指定這兩個值的作用中期間 hello 管線 toorun tooset。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-177">You must specify both values tooset an active period for hello pipeline toorun.</span></span> <span data-ttu-id="dd2e8-178">如果您未指定開始和結束時間時建立管線，您可以設定它們使用 hello 組 AzureRmDataFactoryPipelineActivePeriod 指令程式更新版本。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-178">If you do not specify start and end times when creating a pipeline, you can set them using hello Set-AzureRmDataFactoryPipelineActivePeriod cmdlet later.</span></span> |
| <span data-ttu-id="dd2e8-179">end</span><span class="sxs-lookup"><span data-stu-id="dd2e8-179">end</span></span> | <span data-ttu-id="dd2e8-180">結束日期與時間 hello 管線。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-180">End date-time for hello pipeline.</span></span> <span data-ttu-id="dd2e8-181">如果已指定，則必須使用 ISO 格式。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-181">If specified must be in ISO format.</span></span> <span data-ttu-id="dd2e8-182">例如：`2016-10-14T17:32:41Z`</span><span class="sxs-lookup"><span data-stu-id="dd2e8-182">For example: `2016-10-14T17:32:41Z`</span></span> <br/><br/><span data-ttu-id="dd2e8-183">很可能 toospecify 本地時間，例如預估時間。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-183">It is possible toospecify a local time, for example an EST time.</span></span> <span data-ttu-id="dd2e8-184">範例如下︰`2016-02-27T06:00:00-05:00`，這是 6 AM EST。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-184">Here is an example: `2016-02-27T06:00:00-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="dd2e8-185">toorun hello 管線無限期地指定 9999-09-09 hello hello end 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-185">toorun hello pipeline indefinitely, specify 9999-09-09 as hello value for hello end property.</span></span> <br/><br/> <span data-ttu-id="dd2e8-186">管線僅在其開始時間與結束時間之間有作用。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-186">A pipeline is active only between its start time and end time.</span></span> <span data-ttu-id="dd2e8-187">它不會執行 hello 開始時間之前或之後 hello 結束時間。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-187">It is not executed before hello start time or after hello end time.</span></span> <span data-ttu-id="dd2e8-188">如果 hello 管線已暫停，它不會執行而不受限於其開始和結束時間。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-188">If hello pipeline is paused, it does not get executed irrespective of its start and end time.</span></span> <span data-ttu-id="dd2e8-189">為管線 toorun，它應該暫停。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-189">For a pipeline toorun, it should not be paused.</span></span> <span data-ttu-id="dd2e8-190">請參閱[排程與執行](data-factory-scheduling-and-execution.md)toounderstand 排程和執行 Azure Data Factory 中運作的方式。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-190">See [Scheduling and Execution](data-factory-scheduling-and-execution.md) toounderstand how scheduling and execution works in Azure Data Factory.</span></span> |<span data-ttu-id="dd2e8-191">否</span><span class="sxs-lookup"><span data-stu-id="dd2e8-191">No</span></span> <br/><br/><span data-ttu-id="dd2e8-192">如果您指定 hello 開始屬性的值，您必須指定 hello end 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-192">If you specify a value for hello start property, you must specify value for hello end property.</span></span><br/><br/><span data-ttu-id="dd2e8-193">請參閱備註 hello**啟動**屬性。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-193">See notes for hello **start** property.</span></span> |
| <span data-ttu-id="dd2e8-194">isPaused</span><span class="sxs-lookup"><span data-stu-id="dd2e8-194">isPaused</span></span> | <span data-ttu-id="dd2e8-195">如果組 tootrue，hello 管線不會執行。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-195">If set tootrue, hello pipeline does not run.</span></span> <span data-ttu-id="dd2e8-196">它已經在 hello 暫停狀態。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-196">It's in hello paused state.</span></span> <span data-ttu-id="dd2e8-197">預設值 = false。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-197">Default value = false.</span></span> <span data-ttu-id="dd2e8-198">您可以使用這個屬性 tooenable 或停用管線。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-198">You can use this property tooenable or disable a pipeline.</span></span> |<span data-ttu-id="dd2e8-199">否</span><span class="sxs-lookup"><span data-stu-id="dd2e8-199">No</span></span> |
| <span data-ttu-id="dd2e8-200">pipelineMode</span><span class="sxs-lookup"><span data-stu-id="dd2e8-200">pipelineMode</span></span> | <span data-ttu-id="dd2e8-201">hello 管線的可執行的排程 hello 方法。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-201">hello method for scheduling runs for hello pipeline.</span></span> <span data-ttu-id="dd2e8-202">允許的值包括：scheduled (預設值)、onetime。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-202">Allowed values are: scheduled (default), onetime.</span></span><br/><br/><span data-ttu-id="dd2e8-203">排程' 表示該 hello 管線 tooits 作用期間 （開始和結束時間），根據指定的時間間隔執行。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-203">‘Scheduled’ indicates that hello pipeline runs at a specified time interval according tooits active period (start and end time).</span></span> <span data-ttu-id="dd2e8-204">'一次' 表示該 hello 管線只執行一次。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-204">‘Onetime’ indicates that hello pipeline runs only once.</span></span> <span data-ttu-id="dd2e8-205">目前，Onetime 管線在建立之後即無法進行修改/更新。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-205">Onetime pipelines once created cannot be modified/updated currently.</span></span> <span data-ttu-id="dd2e8-206">如需 onetime 設定的詳細資料，請參閱 [Onetime 管線](#onetime-pipeline)。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-206">See [Onetime pipeline](#onetime-pipeline) for details about onetime setting.</span></span> |<span data-ttu-id="dd2e8-207">否</span><span class="sxs-lookup"><span data-stu-id="dd2e8-207">No</span></span> |
| <span data-ttu-id="dd2e8-208">expirationTime</span><span class="sxs-lookup"><span data-stu-id="dd2e8-208">expirationTime</span></span> | <span data-ttu-id="dd2e8-209">持續時間在建立後的 hello[單次管線](#onetime-pipeline)有效，且應保持已佈建。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-209">Duration of time after creation for which hello [one-time pipeline](#onetime-pipeline) is valid and should remain provisioned.</span></span> <span data-ttu-id="dd2e8-210">如果它沒有任何作用中、 失敗，或執行時，擱置 hello 管線就會自動刪除一次到達 hello 到期時間。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-210">If it does not have any active, failed, or pending runs, hello pipeline is automatically deleted once it reaches hello expiration time.</span></span> <span data-ttu-id="dd2e8-211">hello 預設值：`"expirationTime": "3.00:00:00"`</span><span class="sxs-lookup"><span data-stu-id="dd2e8-211">hello default value: `"expirationTime": "3.00:00:00"`</span></span>|<span data-ttu-id="dd2e8-212">否</span><span class="sxs-lookup"><span data-stu-id="dd2e8-212">No</span></span> |
| <span data-ttu-id="dd2e8-213">資料集</span><span class="sxs-lookup"><span data-stu-id="dd2e8-213">datasets</span></span> |<span data-ttu-id="dd2e8-214">資料集 toobe hello 管線中定義的活動所使用的清單。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-214">List of datasets toobe used by activities defined in hello pipeline.</span></span> <span data-ttu-id="dd2e8-215">這個屬性可以是使用的 toodefine 特定 toothis 管線，而且未在 hello 資料 factory 中定義的資料集。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-215">This property can be used toodefine datasets that are specific toothis pipeline and not defined within hello data factory.</span></span> <span data-ttu-id="dd2e8-216">此管線內定義的資料集只有此管線才能使用，並無法共用。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-216">Datasets defined within this pipeline can only be used by this pipeline and cannot be shared.</span></span> <span data-ttu-id="dd2e8-217">如需詳細資訊，請參閱 [範圍資料集](data-factory-create-datasets.md#scoped-datasets) 。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-217">See [Scoped datasets](data-factory-create-datasets.md#scoped-datasets) for details.</span></span> |<span data-ttu-id="dd2e8-218">否</span><span class="sxs-lookup"><span data-stu-id="dd2e8-218">No</span></span> |

## <a name="activity-json"></a><span data-ttu-id="dd2e8-219">活動 JSON</span><span class="sxs-lookup"><span data-stu-id="dd2e8-219">Activity JSON</span></span>
<span data-ttu-id="dd2e8-220">hello**活動**區段都可以擁有定義於其中的一個或多個活動。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-220">hello **activities** section can have one or more activities defined within it.</span></span> <span data-ttu-id="dd2e8-221">每個活動有下列最上層結構 hello:</span><span class="sxs-lookup"><span data-stu-id="dd2e8-221">Each activity has hello following top-level structure:</span></span>

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

<span data-ttu-id="dd2e8-222">下表描述屬性在 hello 活動 JSON 定義中：</span><span class="sxs-lookup"><span data-stu-id="dd2e8-222">Following table describes properties in hello activity JSON definition:</span></span>

| <span data-ttu-id="dd2e8-223">Tag</span><span class="sxs-lookup"><span data-stu-id="dd2e8-223">Tag</span></span> | <span data-ttu-id="dd2e8-224">說明</span><span class="sxs-lookup"><span data-stu-id="dd2e8-224">Description</span></span> | <span data-ttu-id="dd2e8-225">必要</span><span class="sxs-lookup"><span data-stu-id="dd2e8-225">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dd2e8-226">名稱</span><span class="sxs-lookup"><span data-stu-id="dd2e8-226">name</span></span> | <span data-ttu-id="dd2e8-227">Hello 活動名稱。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-227">Name of hello activity.</span></span> <span data-ttu-id="dd2e8-228">指定代表 hello hello 活動都會執行的動作的名稱。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-228">Specify a name that represents hello action that hello activity performs.</span></span> <br/><ul><li><span data-ttu-id="dd2e8-229">字元數目上限︰260</span><span class="sxs-lookup"><span data-stu-id="dd2e8-229">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="dd2e8-230">開頭必須為字母、數字或底線 (_)</span><span class="sxs-lookup"><span data-stu-id="dd2e8-230">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="dd2e8-231">不允許使用下列字元：“.”、“+”、“?”、“/”、“<”、”>”、”*”、”%”、”&”、”:”、”\\”</span><span class="sxs-lookup"><span data-stu-id="dd2e8-231">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="dd2e8-232">是</span><span class="sxs-lookup"><span data-stu-id="dd2e8-232">Yes</span></span> |
| <span data-ttu-id="dd2e8-233">說明</span><span class="sxs-lookup"><span data-stu-id="dd2e8-233">description</span></span> | <span data-ttu-id="dd2e8-234">描述什麼 hello 活動，或用於文字</span><span class="sxs-lookup"><span data-stu-id="dd2e8-234">Text describing what hello activity or is used for</span></span> |<span data-ttu-id="dd2e8-235">是</span><span class="sxs-lookup"><span data-stu-id="dd2e8-235">Yes</span></span> |
| <span data-ttu-id="dd2e8-236">類型</span><span class="sxs-lookup"><span data-stu-id="dd2e8-236">type</span></span> | <span data-ttu-id="dd2e8-237">Hello 活動的型別。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-237">Type of hello activity.</span></span> <span data-ttu-id="dd2e8-238">請參閱 hello[資料移動活動](#data-movement-activities)和[資料轉換活動](#data-transformation-activities)區段的不同類型的活動。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-238">See hello [Data Movement Activities](#data-movement-activities) and [Data Transformation Activities](#data-transformation-activities) sections for different types of activities.</span></span> |<span data-ttu-id="dd2e8-239">是</span><span class="sxs-lookup"><span data-stu-id="dd2e8-239">Yes</span></span> |
| <span data-ttu-id="dd2e8-240">輸入</span><span class="sxs-lookup"><span data-stu-id="dd2e8-240">inputs</span></span> |<span data-ttu-id="dd2e8-241">Hello 活動所使用的輸入的資料表</span><span class="sxs-lookup"><span data-stu-id="dd2e8-241">Input tables used by hello activity</span></span><br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |<span data-ttu-id="dd2e8-242">是</span><span class="sxs-lookup"><span data-stu-id="dd2e8-242">Yes</span></span> |
| <span data-ttu-id="dd2e8-243">輸出</span><span class="sxs-lookup"><span data-stu-id="dd2e8-243">outputs</span></span> |<span data-ttu-id="dd2e8-244">使用的 hello 活動的輸出的資料表。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-244">Output tables used by hello activity.</span></span><br/><br/>`// one output table`<br/>`"outputs":  [ { "name": "outputtable1" } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": "outputtable1" }, { "name": "outputtable2" }  ],` |<span data-ttu-id="dd2e8-245">是</span><span class="sxs-lookup"><span data-stu-id="dd2e8-245">Yes</span></span> |
| <span data-ttu-id="dd2e8-246">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="dd2e8-246">linkedServiceName</span></span> |<span data-ttu-id="dd2e8-247">Hello 活動所使用的 hello 連結服務名稱。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-247">Name of hello linked service used by hello activity.</span></span> <br/><br/><span data-ttu-id="dd2e8-248">活動可能會要求您指定連結 toohello 必要的運算環境的 hello 連結服務。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-248">An activity may require that you specify hello linked service that links toohello required compute environment.</span></span> |<span data-ttu-id="dd2e8-249">是：適用於 HDInsight 活動和 Azure Machine Learning Batch 評分活動 </span><span class="sxs-lookup"><span data-stu-id="dd2e8-249">Yes for HDInsight Activity and Azure Machine Learning Batch Scoring Activity</span></span> <br/><br/><span data-ttu-id="dd2e8-250">否：所有其他</span><span class="sxs-lookup"><span data-stu-id="dd2e8-250">No for all others</span></span> |
| <span data-ttu-id="dd2e8-251">typeProperties</span><span class="sxs-lookup"><span data-stu-id="dd2e8-251">typeProperties</span></span> |<span data-ttu-id="dd2e8-252">屬性在 hello **typeProperties**區段取決於 hello 活動的類型。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-252">Properties in hello **typeProperties** section depend on type of hello activity.</span></span> <span data-ttu-id="dd2e8-253">toosee 類型屬性的活動中，按一下 hello 前一節中的連結 toohello 活動。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-253">toosee type properties for an activity, click links toohello activity in hello previous section.</span></span> | <span data-ttu-id="dd2e8-254">否</span><span class="sxs-lookup"><span data-stu-id="dd2e8-254">No</span></span> |
| <span data-ttu-id="dd2e8-255">原則</span><span class="sxs-lookup"><span data-stu-id="dd2e8-255">policy</span></span> |<span data-ttu-id="dd2e8-256">影響 hello hello 活動執行階段行為的原則。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-256">Policies that affect hello run-time behavior of hello activity.</span></span> <span data-ttu-id="dd2e8-257">如果未指定，則會使用預設原則。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-257">If it is not specified, default policies are used.</span></span> |<span data-ttu-id="dd2e8-258">否</span><span class="sxs-lookup"><span data-stu-id="dd2e8-258">No</span></span> |
| <span data-ttu-id="dd2e8-259">scheduler</span><span class="sxs-lookup"><span data-stu-id="dd2e8-259">scheduler</span></span> | <span data-ttu-id="dd2e8-260">「 排程器 」 屬性是使用的 toodefine 預期 hello 活動的排程。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-260">“scheduler” property is used toodefine desired scheduling for hello activity.</span></span> <span data-ttu-id="dd2e8-261">及其子屬性會 hello 與 hello hello 於相同[可用性屬性集中](data-factory-create-datasets.md#dataset-availability)。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-261">Its subproperties are hello same as hello ones in hello [availability property in a dataset](data-factory-create-datasets.md#dataset-availability).</span></span> |<span data-ttu-id="dd2e8-262">否</span><span class="sxs-lookup"><span data-stu-id="dd2e8-262">No</span></span> |


### <a name="policies"></a><span data-ttu-id="dd2e8-263">原則</span><span class="sxs-lookup"><span data-stu-id="dd2e8-263">Policies</span></span>
<span data-ttu-id="dd2e8-264">特別是當處理資料表的 hello 配量時，原則會影響 hello 執行階段行為的活動。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-264">Policies affect hello run-time behavior of an activity, specifically when hello slice of a table is processed.</span></span> <span data-ttu-id="dd2e8-265">下表中的 hello 提供 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-265">hello following table provides hello details.</span></span>

| <span data-ttu-id="dd2e8-266">屬性</span><span class="sxs-lookup"><span data-stu-id="dd2e8-266">Property</span></span> | <span data-ttu-id="dd2e8-267">允許的值</span><span class="sxs-lookup"><span data-stu-id="dd2e8-267">Permitted values</span></span> | <span data-ttu-id="dd2e8-268">預設值</span><span class="sxs-lookup"><span data-stu-id="dd2e8-268">Default Value</span></span> | <span data-ttu-id="dd2e8-269">說明</span><span class="sxs-lookup"><span data-stu-id="dd2e8-269">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="dd2e8-270">並行</span><span class="sxs-lookup"><span data-stu-id="dd2e8-270">concurrency</span></span> |<span data-ttu-id="dd2e8-271">整數 </span><span class="sxs-lookup"><span data-stu-id="dd2e8-271">Integer</span></span> <br/><br/><span data-ttu-id="dd2e8-272">最大值：10</span><span class="sxs-lookup"><span data-stu-id="dd2e8-272">Max value: 10</span></span> |<span data-ttu-id="dd2e8-273">1</span><span class="sxs-lookup"><span data-stu-id="dd2e8-273">1</span></span> |<span data-ttu-id="dd2e8-274">並行執行的 hello 活動的數目。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-274">Number of concurrent executions of hello activity.</span></span><br/><br/><span data-ttu-id="dd2e8-275">它決定不同配量上可能發生的平行活動執行的 hello 次數。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-275">It determines hello number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="dd2e8-276">例如，如果活動需要透過 toogo 大量可用的資料，具有較大的並行值就會加快 hello 資料處理。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-276">For example, if an activity needs toogo through a large set of available data, having a larger concurrency value speeds up hello data processing.</span></span> |
| <span data-ttu-id="dd2e8-277">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="dd2e8-277">executionPriorityOrder</span></span> |<span data-ttu-id="dd2e8-278">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="dd2e8-278">NewestFirst</span></span><br/><br/><span data-ttu-id="dd2e8-279">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="dd2e8-279">OldestFirst</span></span> |<span data-ttu-id="dd2e8-280">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="dd2e8-280">OldestFirst</span></span> |<span data-ttu-id="dd2e8-281">判斷正在處理的資料配量順序 hello。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-281">Determines hello ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="dd2e8-282">例如，如果您有 2 個配量 (一個發生在下午 4 點，另一個發生在下午 5 點)，而兩者都暫停執行。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-282">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="dd2e8-283">如果您設定 hello executionpriorityorder 設 toobe NewestFirst，會先處理下午 5 點的 hello 配量。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-283">If you set hello executionPriorityOrder toobe NewestFirst, hello slice at 5 PM is processed first.</span></span> <span data-ttu-id="dd2e8-284">同樣地如果您設定 hello executionpriorityorder 設 toobe OldestFIrst，然後在下午 4 點 hello 配量會處理。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-284">Similarly if you set hello executionPriorityORder toobe OldestFIrst, then hello slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="dd2e8-285">retry</span><span class="sxs-lookup"><span data-stu-id="dd2e8-285">retry</span></span> |<span data-ttu-id="dd2e8-286">整數 </span><span class="sxs-lookup"><span data-stu-id="dd2e8-286">Integer</span></span><br/><br/><span data-ttu-id="dd2e8-287">最大值可以是 10</span><span class="sxs-lookup"><span data-stu-id="dd2e8-287">Max value can be 10</span></span> |<span data-ttu-id="dd2e8-288">0</span><span class="sxs-lookup"><span data-stu-id="dd2e8-288">0</span></span> |<span data-ttu-id="dd2e8-289">Hello hello 配量的資料處理之前的重試的數目會標示為失敗。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-289">Number of retries before hello data processing for hello slice is marked as Failure.</span></span> <span data-ttu-id="dd2e8-290">資料配量的活動執行會重試總 toohello 指定重試計數。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-290">Activity execution for a data slice is retried up toohello specified retry count.</span></span> <span data-ttu-id="dd2e8-291">hello 重試會儘速 hello 失敗後進行。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-291">hello retry is done as soon as possible after hello failure.</span></span> |
| <span data-ttu-id="dd2e8-292">timeout</span><span class="sxs-lookup"><span data-stu-id="dd2e8-292">timeout</span></span> |<span data-ttu-id="dd2e8-293">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="dd2e8-293">TimeSpan</span></span> |<span data-ttu-id="dd2e8-294">00:00:00</span><span class="sxs-lookup"><span data-stu-id="dd2e8-294">00:00:00</span></span> |<span data-ttu-id="dd2e8-295">Hello 活動的逾時。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-295">Timeout for hello activity.</span></span> <span data-ttu-id="dd2e8-296">範例︰00:10:00 (意指逾時 10 分鐘)</span><span class="sxs-lookup"><span data-stu-id="dd2e8-296">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="dd2e8-297">如果未指定值，或為 0，hello 逾時是無限的。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-297">If a value is not specified or is 0, hello timeout is infinite.</span></span><br/><br/><span data-ttu-id="dd2e8-298">如果配量的 hello 資料處理時間超過 hello 逾時值，則會取消，並 hello 系統會嘗試 tooretry hello 處理。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-298">If hello data processing time on a slice exceeds hello timeout value, it is canceled, and hello system attempts tooretry hello processing.</span></span> <span data-ttu-id="dd2e8-299">hello 重試次數取決於 hello 重試屬性。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-299">hello number of retries depends on hello retry property.</span></span> <span data-ttu-id="dd2e8-300">發生逾時，hello 狀態會設定 tooTimedOut。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-300">When timeout occurs, hello status is set tooTimedOut.</span></span> |
| <span data-ttu-id="dd2e8-301">delay</span><span class="sxs-lookup"><span data-stu-id="dd2e8-301">delay</span></span> |<span data-ttu-id="dd2e8-302">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="dd2e8-302">TimeSpan</span></span> |<span data-ttu-id="dd2e8-303">00:00:00</span><span class="sxs-lookup"><span data-stu-id="dd2e8-303">00:00:00</span></span> |<span data-ttu-id="dd2e8-304">指定 hello hello 配量開始的資料處理之前的延遲。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-304">Specify hello delay before data processing of hello slice starts.</span></span><br/><br/><span data-ttu-id="dd2e8-305">hello 延遲 hello 預期執行時間過去後，會啟動 hello 執行之活動的資料配量。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-305">hello execution of activity for a data slice is started after hello Delay is past hello expected execution time.</span></span><br/><br/><span data-ttu-id="dd2e8-306">範例︰00:10:00 (意指延遲 10 分鐘)</span><span class="sxs-lookup"><span data-stu-id="dd2e8-306">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="dd2e8-307">longRetry</span><span class="sxs-lookup"><span data-stu-id="dd2e8-307">longRetry</span></span> |<span data-ttu-id="dd2e8-308">整數 </span><span class="sxs-lookup"><span data-stu-id="dd2e8-308">Integer</span></span><br/><br/><span data-ttu-id="dd2e8-309">最大值：10</span><span class="sxs-lookup"><span data-stu-id="dd2e8-309">Max value: 10</span></span> |<span data-ttu-id="dd2e8-310">1</span><span class="sxs-lookup"><span data-stu-id="dd2e8-310">1</span></span> |<span data-ttu-id="dd2e8-311">hello 的長時間重試次數 hello 配量執行失敗。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-311">hello number of long retry attempts before hello slice execution is failed.</span></span><br/><br/><span data-ttu-id="dd2e8-312">多個 longRetry 嘗試之間以 longRetryInterval 隔開。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-312">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="dd2e8-313">因此，如果您需要 toospecify 重試嘗試之間的時間，請使用 longRetry。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-313">So if you need toospecify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="dd2e8-314">如果指定 Retry 和 longRetry，每個 longRetry 嘗試包含重試次數和 hello 最大嘗試次數為重試 * longRetry。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-314">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and hello max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="dd2e8-315">例如，如果我們有下列 hello 活動原則中的設定的 hello:</span><span class="sxs-lookup"><span data-stu-id="dd2e8-315">For example, if we have hello following settings in hello activity policy:</span></span><br/><span data-ttu-id="dd2e8-316">Retry：3</span><span class="sxs-lookup"><span data-stu-id="dd2e8-316">Retry: 3</span></span><br/><span data-ttu-id="dd2e8-317">longRetry：2</span><span class="sxs-lookup"><span data-stu-id="dd2e8-317">longRetry: 2</span></span><br/><span data-ttu-id="dd2e8-318">longRetryInterval：01:00:00</span><span class="sxs-lookup"><span data-stu-id="dd2e8-318">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="dd2e8-319">假設有一個配量 tooexecute （等待狀態），就會失敗的每次 hello 活動執行。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-319">Assume there is only one slice tooexecute (status is Waiting) and hello activity execution fails every time.</span></span> <span data-ttu-id="dd2e8-320">一開始會有 3 次連續執行嘗試。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-320">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="dd2e8-321">每次嘗試之後, hello 配量狀態會是 Retry。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-321">After each attempt, hello slice status would be Retry.</span></span> <span data-ttu-id="dd2e8-322">前 3 的嘗試次數已超過之後，hello 配量狀態就會是 LongRetry。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-322">After first 3 attempts are over, hello slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="dd2e8-323">一個小時 (也就是 longRetryInteval 的值) 之後，會有另一組 3 次連續執行嘗試。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-323">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="dd2e8-324">之後，hello 配量狀態會變成 Failed，而且會嘗試重試。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-324">After that, hello slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="dd2e8-325">因此全部已進行 6 次嘗試。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-325">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="dd2e8-326">如果執行成功，hello 配量狀態就會是 Ready，無需重試嘗試。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-326">If any execution succeeds, hello slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="dd2e8-327">在位置相依的資料到達在不具決定性的時間或 hello 整體環境穩定底下的資料處理發生的情況下可用 longRetry。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-327">longRetry may be used in situations where dependent data arrives at non-deterministic times or hello overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="dd2e8-328">在這種情況下，逐一進行重試可能無法幫助，這樣導致 hello 的時間間隔之後想要的輸出。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-328">In such cases, doing retries one after another may not help and doing so after an interval of time results in hello desired output.</span></span><br/><br/><span data-ttu-id="dd2e8-329">提醒：請勿設定較大的 longRetry 或 longRetryInterval 值。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-329">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="dd2e8-330">較大的值通常表示其他系統問題。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-330">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="dd2e8-331">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="dd2e8-331">longRetryInterval</span></span> |<span data-ttu-id="dd2e8-332">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="dd2e8-332">TimeSpan</span></span> |<span data-ttu-id="dd2e8-333">00:00:00</span><span class="sxs-lookup"><span data-stu-id="dd2e8-333">00:00:00</span></span> |<span data-ttu-id="dd2e8-334">hello 長時間重試嘗試之間的延遲</span><span class="sxs-lookup"><span data-stu-id="dd2e8-334">hello delay between long retry attempts</span></span> |

## <a name="sample-copy-pipeline"></a><span data-ttu-id="dd2e8-335">範例複製管線</span><span class="sxs-lookup"><span data-stu-id="dd2e8-335">Sample copy pipeline</span></span>
<span data-ttu-id="dd2e8-336">在下列範例管線 hello，沒有一個活動的型別**複製**在 hello**活動**> 一節。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-336">In hello following sample pipeline, there is one activity of type **Copy** in hello **activities** section.</span></span> <span data-ttu-id="dd2e8-337">在此範例中，hello[複製活動](data-factory-data-movement-activities.md)將資料從 Azure Blob 儲存體 tooan Azure SQL database 複製。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-337">In this sample, hello [copy activity](data-factory-data-movement-activities.md) copies data from an Azure Blob storage tooan Azure SQL database.</span></span> 

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

<span data-ttu-id="dd2e8-338">請注意下列點 hello:</span><span class="sxs-lookup"><span data-stu-id="dd2e8-338">Note hello following points:</span></span>

* <span data-ttu-id="dd2e8-339">在 [hello 活動] 區段中，沒有一個活動其**類型**設定得**複製**。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-339">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span>
* <span data-ttu-id="dd2e8-340">輸入 hello 活動設定太**InputDataset**和輸出 hello 活動設定太**OutputDataset**。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-340">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span> <span data-ttu-id="dd2e8-341">若要了解如何以 JSON 定義資料集，請參閱[資料集](data-factory-create-datasets.md)一文。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-341">See [Datasets](data-factory-create-datasets.md) article for defining datasets in JSON.</span></span> 
* <span data-ttu-id="dd2e8-342">在 [hello **typeProperties** ] 區段中， **BlobSource**指定 hello 來源類型為和**SqlSink**指定為 hello 接收器類型。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-342">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="dd2e8-343">在 [hello[資料移動活動](#data-movement-activities)區段中，按一下的 hello 資料存放區，您要 toouse 做為來源或接收器 toolearn 了解從該資料存放區移動資料。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-343">In hello [Data movement activities](#data-movement-activities) section, click hello data store that you want toouse as a source or a sink toolearn more about moving data to/from that data store.</span></span> 

<span data-ttu-id="dd2e8-344">建立此管線的完整逐步解說，請參閱[教學課程： 將資料從 Blob 儲存體 tooSQL 資料庫複製](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-344">For a complete walkthrough of creating this pipeline, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

## <a name="sample-transformation-pipeline"></a><span data-ttu-id="dd2e8-345">範例轉換管線</span><span class="sxs-lookup"><span data-stu-id="dd2e8-345">Sample transformation pipeline</span></span>
<span data-ttu-id="dd2e8-346">在下列範例管線 hello，沒有一個活動的型別**HDInsightHive**在 hello**活動**> 一節。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-346">In hello following sample pipeline, there is one activity of type **HDInsightHive** in hello **activities** section.</span></span> <span data-ttu-id="dd2e8-347">在此範例中，hello [HDInsight Hive 活動](data-factory-hive-activity.md)執行 Azure HDInsight Hadoop 叢集上的 Hive 指令碼檔案來轉換資料從 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-347">In this sample, hello [HDInsight Hive activity](data-factory-hive-activity.md) transforms data from an Azure Blob storage by running a Hive script file on an Azure HDInsight Hadoop cluster.</span></span> 

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

<span data-ttu-id="dd2e8-348">請注意下列點 hello:</span><span class="sxs-lookup"><span data-stu-id="dd2e8-348">Note hello following points:</span></span> 

* <span data-ttu-id="dd2e8-349">在 [hello 活動] 區段中，沒有一個活動其**類型**設定得**HDInsightHive**。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-349">In hello activities section, there is only one activity whose **type** is set too**HDInsightHive**.</span></span>
* <span data-ttu-id="dd2e8-350">hello Hive 指令碼檔案， **partitionweblogs.hql**，儲存在 hello Azure 儲存體帳戶 (由 hello scriptLinkedService，稱為**AzureStorageLinkedService**)，然後在**指令碼**hello 容器中的資料夾**adfgetstarted**。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-350">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>
* <span data-ttu-id="dd2e8-351">hello`defines`區段是做為 Hive 組態值傳遞 toohello hive 指令碼使用的 toospecify hello 執行階段設定 (例如`${hiveconf:inputtable}`， `${hiveconf:partitionedtable}`)。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-351">hello `defines` section is used toospecify hello runtime settings that are passed toohello hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span></span>

<span data-ttu-id="dd2e8-352">hello **typeProperties**區段是不同的每個轉換活動。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-352">hello **typeProperties** section is different for each transformation activity.</span></span> <span data-ttu-id="dd2e8-353">轉換活動，支援的型別屬性的相關 toolearn 按一下 hello hello 轉換活動[資料轉換活動](#data-transformation-activities)資料表。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-353">toolearn about type properties supported for a transformation activity, click hello transformation activity in hello [Data transformation activities](#data-transformation-activities) table.</span></span> 

<span data-ttu-id="dd2e8-354">建立此管線的完整逐步解說，請參閱[教學課程： 建立第一個管線 tooprocess 資料使用 Hadoop 叢集](data-factory-build-your-first-pipeline.md)。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-354">For a complete walkthrough of creating this pipeline, see [Tutorial: Build your first pipeline tooprocess data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="multiple-activities-in-a-pipeline"></a><span data-ttu-id="dd2e8-355">管線中的多個活動</span><span class="sxs-lookup"><span data-stu-id="dd2e8-355">Multiple activities in a pipeline</span></span>
<span data-ttu-id="dd2e8-356">hello 先前兩個範例管線有一個活動。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-356">hello previous two sample pipelines have only one activity in them.</span></span> <span data-ttu-id="dd2e8-357">您可以在一個管線中包含多個活動。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-357">You can have more than one activity in a pipeline.</span></span>  

<span data-ttu-id="dd2e8-358">如果您在管線中有多個活動和活動的輸出不是另一個活動的輸入，hello 活動可能會以平行方式執行，hello 活動的輸入的資料配量是否準備。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-358">If you have multiple activities in a pipeline and output of an activity is not an input of another activity, hello activities may run in parallel if input data slices for hello activities are ready.</span></span> 

<span data-ttu-id="dd2e8-359">您可以將鏈結兩個活動擁有 hello 輸出資料集，一個活動與 hello hello 的輸入資料集的其他活動。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-359">You can chain two activities by having hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="dd2e8-360">hello 第二個活動執行只 hello 第一次一個成功完成。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-360">hello second activity executes only when hello first one completes successfully.</span></span>

![鏈結中 hello 活動相同管線](./media/data-factory-create-pipelines/chaining-one-pipeline.png)

<span data-ttu-id="dd2e8-362">在此範例中，hello 管線有兩個活動： Activity1 和 Activity2。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-362">In this sample, hello pipeline has two activities: Activity1 and Activity2.</span></span> <span data-ttu-id="dd2e8-363">hello Activity1 接受做為輸入 Dataset1，然後產生輸出 Dataset2。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-363">hello Activity1 takes Dataset1 as an input and produces an output Dataset2.</span></span> <span data-ttu-id="dd2e8-364">hello 活動會採用做為輸入 Dataset2，並產生輸出 Dataset3。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-364">hello Activity takes Dataset2 as an input and produces an output Dataset3.</span></span> <span data-ttu-id="dd2e8-365">因為 Activity1 hello 輸出 (Dataset2) Activity2 hello 輸入，hello Activity2 hello 活動順利完成之後，才會執行，並產生 hello Dataset2 配量。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-365">Since hello output of Activity1 (Dataset2) is hello input of Activity2, hello Activity2 runs only after hello Activity completes successfully and produces hello Dataset2 slice.</span></span> <span data-ttu-id="dd2e8-366">如果 hello Activity1 因故失敗，而且不會產生 hello Dataset2 配量，hello 活動 2 不會執行該配量 (例如： 9 AM too10 AM)。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-366">If hello Activity1 fails for some reason and does not produce hello Dataset2 slice, hello Activity 2 does not run for that slice (for example: 9 AM too10 AM).</span></span> 

<span data-ttu-id="dd2e8-367">您可以將不同管線中的活動建立鏈結。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-367">You can also chain activities that are in different pipelines.</span></span>

![兩個管線中的鏈結活動](./media/data-factory-create-pipelines/chaining-two-pipelines.png)

<span data-ttu-id="dd2e8-369">在此範例中，Pipeline1 只有一個活動，此活動是以 Dataset1 作為輸入，並產生 Dataset2 作為輸出。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-369">In this sample, Pipeline1 has only one activity that takes Dataset1 as an input and produces Dataset2 as an output.</span></span> <span data-ttu-id="dd2e8-370">hello Pipeline2 也有一個採用 Dataset2 和當做輸入 Dataset3 做為輸出的活動。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-370">hello Pipeline2 also has only one activity that takes Dataset2 as an input and Dataset3 as an output.</span></span> 

<span data-ttu-id="dd2e8-371">如需詳細資訊，請參閱 [排程和執行](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-371">For more information, see [scheduling and execution](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

## <a name="create-and-monitor-pipelines"></a><span data-ttu-id="dd2e8-372">建立和監視管線</span><span class="sxs-lookup"><span data-stu-id="dd2e8-372">Create and monitor pipelines</span></span>
<span data-ttu-id="dd2e8-373">您可以使用下列其中一項工具或 SDK 來建立管線。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-373">You can create pipelines by using one of these tools or SDKs.</span></span> 

- <span data-ttu-id="dd2e8-374">複製精靈</span><span class="sxs-lookup"><span data-stu-id="dd2e8-374">Copy Wizard.</span></span> 
- <span data-ttu-id="dd2e8-375">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="dd2e8-375">Azure portal</span></span>
- <span data-ttu-id="dd2e8-376">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dd2e8-376">Visual Studio</span></span>
- <span data-ttu-id="dd2e8-377">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd2e8-377">Azure PowerShell</span></span>
- <span data-ttu-id="dd2e8-378">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="dd2e8-378">Azure Resource Manager template</span></span>
- <span data-ttu-id="dd2e8-379">REST API</span><span class="sxs-lookup"><span data-stu-id="dd2e8-379">REST API</span></span>
- <span data-ttu-id="dd2e8-380">.NET API</span><span class="sxs-lookup"><span data-stu-id="dd2e8-380">.NET API</span></span>

<span data-ttu-id="dd2e8-381">請參閱下列逐步教學課程使用其中一個工具或 Sdk 建立管線的 hello。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-381">See hello following tutorials for step-by-step instructions for creating pipelines by using one of these tools or SDKs.</span></span>
 
- [<span data-ttu-id="dd2e8-382">使用資料轉換活動來建置管線</span><span class="sxs-lookup"><span data-stu-id="dd2e8-382">Build a pipeline with a data transformation activity</span></span>](data-factory-build-your-first-pipeline.md)
- [<span data-ttu-id="dd2e8-383">使用資料移動活動來建置管線</span><span class="sxs-lookup"><span data-stu-id="dd2e8-383">Build a pipeline with a data movement activity</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

<span data-ttu-id="dd2e8-384">一旦建立/部署管線，您可以管理和監視您所使用的管線 hello Azure 入口網站的刀鋒視窗或監視和管理應用程式。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-384">Once a pipeline is created/deployed, you can manage and monitor your pipelines by using hello Azure portal blades or Monitor and Manage App.</span></span> <span data-ttu-id="dd2e8-385">請參閱下列主題逐步指示的 hello。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-385">See hello following topics for step-by-step instructions.</span></span> 

- <span data-ttu-id="dd2e8-386">[使用 Azure 入口網站刀鋒視窗來監視和管理管線](data-factory-monitor-manage-pipelines.md)</span><span class="sxs-lookup"><span data-stu-id="dd2e8-386">[Monitor and manage pipelines by using Azure portal blades](data-factory-monitor-manage-pipelines.md).</span></span>
- [<span data-ttu-id="dd2e8-387">使用監視與管理應用程式來監視和管理管線</span><span class="sxs-lookup"><span data-stu-id="dd2e8-387">Monitor and manage pipelines by using Monitor and Manage App</span></span>](data-factory-monitor-manage-app.md)


## <a name="onetime-pipeline"></a><span data-ttu-id="dd2e8-388">Onetime 管線</span><span class="sxs-lookup"><span data-stu-id="dd2e8-388">Onetime pipeline</span></span>
<span data-ttu-id="dd2e8-389">您可以建立和定期排程管線 toorun (例如： 每小時或每天) 內 hello 開始與結束 hello 管線定義中指定的時間。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-389">You can create and schedule a pipeline toorun periodically (for example: hourly or daily) within hello start and end times you specify in hello pipeline definition.</span></span> <span data-ttu-id="dd2e8-390">如需詳細資訊，請參閱 [排程活動](#scheduling-and-execution) 。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-390">See [Scheduling activities](#scheduling-and-execution) for details.</span></span> <span data-ttu-id="dd2e8-391">您也可以建立只執行一次的管線。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-391">You can also create a pipeline that runs only once.</span></span> <span data-ttu-id="dd2e8-392">toodo 所以，您可以設定 hello **pipelineMode** hello 中的屬性太管線定義**一次**hello 下列 JSON 範例所示。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-392">toodo so, you set hello **pipelineMode** property in hello pipeline definition too**onetime** as shown in hello following JSON sample.</span></span> <span data-ttu-id="dd2e8-393">hello 這個屬性的預設值是**排程**。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-393">hello default value for this property is **scheduled**.</span></span>

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

<span data-ttu-id="dd2e8-394">請注意 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="dd2e8-394">Note hello following:</span></span>

* <span data-ttu-id="dd2e8-395">**啟動**和**結束**hello 管線的時間都不指定。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-395">**Start** and **end** times for hello pipeline are not specified.</span></span>
* <span data-ttu-id="dd2e8-396">**可用性**資料集為指定的輸入和輸出 (**頻率**和**間隔**)，即使 Data Factory 不會使用 hello 值。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-396">**Availability** of input and output datasets is specified (**frequency** and **interval**), even though Data Factory does not use hello values.</span></span>  
* <span data-ttu-id="dd2e8-397">圖表檢視不會顯示一次性管線。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-397">Diagram view does not show one-time pipelines.</span></span> <span data-ttu-id="dd2e8-398">這是設計的行為。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-398">This behavior is by design.</span></span>
* <span data-ttu-id="dd2e8-399">一次性管線無法更新。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-399">One-time pipelines cannot be updated.</span></span> <span data-ttu-id="dd2e8-400">您可以複製單次管線，將它重新命名、 更新屬性，並部署 toocreate 另一個。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-400">You can clone a one-time pipeline, rename it, update properties, and deploy it toocreate another one.</span></span>


## <a name="next-steps"></a><span data-ttu-id="dd2e8-401">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dd2e8-401">Next Steps</span></span>
- <span data-ttu-id="dd2e8-402">如需有關資料集的詳細資訊，請參閱[建立資料集](data-factory-create-datasets.md)一文。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-402">For more information about datasets, see [Create datasets](data-factory-create-datasets.md) article.</span></span> 
- <span data-ttu-id="dd2e8-403">如需有關管線的排程和執行方式的詳細資訊，請參閱 [Azure Data Factory 中的排程和執行](data-factory-scheduling-and-execution.md)一文。</span><span class="sxs-lookup"><span data-stu-id="dd2e8-403">For more information about how pipelines are scheduled and executed, see [Scheduling and execution in Azure Data Factory](data-factory-scheduling-and-execution.md) article.</span></span> 
  

