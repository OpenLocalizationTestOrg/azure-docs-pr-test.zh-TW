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
# <a name="data-factory-scheduling-and-execution"></a><span data-ttu-id="cbe36-103">Data Factory 排程和執行</span><span class="sxs-lookup"><span data-stu-id="cbe36-103">Data Factory scheduling and execution</span></span>
<span data-ttu-id="cbe36-104">本文說明 hello 排程和執行層面 hello Azure Data Factory 應用程式模型。</span><span class="sxs-lookup"><span data-stu-id="cbe36-104">This article explains hello scheduling and execution aspects of hello Azure Data Factory application model.</span></span> <span data-ttu-id="cbe36-105">本文假設您已了解 Data Factory 應用程式模型的基本概念，包括活動、管線、連結的服務和資料集。</span><span class="sxs-lookup"><span data-stu-id="cbe36-105">This article assumes that you understand basics of Data Factory application model concepts, including activity, pipelines, linked services, and datasets.</span></span> <span data-ttu-id="cbe36-106">Azure Data Factory 的基本概念，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="cbe36-106">For basic concepts of Azure Data Factory, see hello following articles:</span></span>

* [<span data-ttu-id="cbe36-107">簡介 tooData Factory</span><span class="sxs-lookup"><span data-stu-id="cbe36-107">Introduction tooData Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="cbe36-108">管線</span><span class="sxs-lookup"><span data-stu-id="cbe36-108">Pipelines</span></span>](data-factory-create-pipelines.md)
* [<span data-ttu-id="cbe36-109">資料集</span><span class="sxs-lookup"><span data-stu-id="cbe36-109">Datasets</span></span>](data-factory-create-datasets.md) 

## <a name="start-and-end-times-of-pipeline"></a><span data-ttu-id="cbe36-110">管線的開始和結束時間</span><span class="sxs-lookup"><span data-stu-id="cbe36-110">Start and end times of pipeline</span></span>
<span data-ttu-id="cbe36-111">管線僅在其「開始」時間與「結束」時間之間有作用。</span><span class="sxs-lookup"><span data-stu-id="cbe36-111">A pipeline is active only between its **start** time and **end** time.</span></span> <span data-ttu-id="cbe36-112">它不會執行 hello 開始時間之前或之後 hello 結束時間。</span><span class="sxs-lookup"><span data-stu-id="cbe36-112">It is not executed before hello start time or after hello end time.</span></span> <span data-ttu-id="cbe36-113">如果 hello 管線已暫停，它不會執行而不受限於其開始和結束時間。</span><span class="sxs-lookup"><span data-stu-id="cbe36-113">If hello pipeline is paused, it is not executed irrespective of its start and end time.</span></span> <span data-ttu-id="cbe36-114">為管線 toorun，它應該暫停。</span><span class="sxs-lookup"><span data-stu-id="cbe36-114">For a pipeline toorun, it should not be paused.</span></span> <span data-ttu-id="cbe36-115">您可以找到這些設定 （開始、 結束時，暫停） hello 管線定義中：</span><span class="sxs-lookup"><span data-stu-id="cbe36-115">You find these settings (start, end, paused) in hello pipeline definition:</span></span> 

```json
"start": "2017-04-01T08:00:00Z",
"end": "2017-04-01T11:00:00Z"
"isPaused": false
```

<span data-ttu-id="cbe36-116">如需有關這些屬性的詳細資訊，請參閱[建立管線](data-factory-create-pipelines.md)一文。</span><span class="sxs-lookup"><span data-stu-id="cbe36-116">For more information these properties, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> 


## <a name="specify-schedule-for-an-activity"></a><span data-ttu-id="cbe36-117">為活動指定排程</span><span class="sxs-lookup"><span data-stu-id="cbe36-117">Specify schedule for an activity</span></span>
<span data-ttu-id="cbe36-118">不執行 hello 管線。</span><span class="sxs-lookup"><span data-stu-id="cbe36-118">It is not hello pipeline that is executed.</span></span> <span data-ttu-id="cbe36-119">它是在 hello 管線中的 hello 活動 hello 中執行的整體 hello 管線的內容。</span><span class="sxs-lookup"><span data-stu-id="cbe36-119">It is hello activities in hello pipeline that are executed in hello overall context of hello pipeline.</span></span> <span data-ttu-id="cbe36-120">您可以指定活動的週期性排程使用 hello**排程器**活動 JSON 的區段。</span><span class="sxs-lookup"><span data-stu-id="cbe36-120">You can specify a recurring schedule for an activity by using hello **scheduler** section of activity JSON.</span></span> <span data-ttu-id="cbe36-121">例如，您可以排定活動 toorun 每小時，如下所示：</span><span class="sxs-lookup"><span data-stu-id="cbe36-121">For example, you can schedule an activity toorun hourly as follows:</span></span>  

```json
"scheduler": {
    "frequency": "Hour",
    "interval": 1
},
```

<span data-ttu-id="cbe36-122">Hello 下列圖表所示，指定活動的排程建立一系列的輪轉視窗具有在 hello 管線開始和結束時間。</span><span class="sxs-lookup"><span data-stu-id="cbe36-122">As shown in hello following diagram, specifying a schedule for an activity creates a series of tumbling windows with in hello pipeline start and end times.</span></span> <span data-ttu-id="cbe36-123">輪轉時段是一系列大小固定、非重疊的連續時間間隔。</span><span class="sxs-lookup"><span data-stu-id="cbe36-123">Tumbling windows are a series of fixed-size non-overlapping, contiguous time intervals.</span></span> <span data-ttu-id="cbe36-124">活動的這些邏輯輪轉時段稱為「活動時段」。</span><span class="sxs-lookup"><span data-stu-id="cbe36-124">These logical tumbling windows for an activity are called **activity windows**.</span></span>

![活動排程器範例](media/data-factory-scheduling-and-execution/scheduler-example.png)

<span data-ttu-id="cbe36-126">hello**排程器**是選擇性的活動的屬性。</span><span class="sxs-lookup"><span data-stu-id="cbe36-126">hello **scheduler** property for an activity is optional.</span></span> <span data-ttu-id="cbe36-127">如果您指定這個屬性，它必須符合您指定 hello hello 活動的輸出資料集定義中的 hello 步調。</span><span class="sxs-lookup"><span data-stu-id="cbe36-127">If you do specify this property, it must match hello cadence you specify in hello definition of output dataset for hello activity.</span></span> <span data-ttu-id="cbe36-128">目前，輸出資料集是哪些磁碟機 hello 排程。</span><span class="sxs-lookup"><span data-stu-id="cbe36-128">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="cbe36-129">因此，您必須建立輸出資料集，即使 hello 活動不會產生任何輸出。</span><span class="sxs-lookup"><span data-stu-id="cbe36-129">Therefore, you must create an output dataset even if hello activity does not produce any output.</span></span> 

## <a name="specify-schedule-for-a-dataset"></a><span data-ttu-id="cbe36-130">為資料集指定排程</span><span class="sxs-lookup"><span data-stu-id="cbe36-130">Specify schedule for a dataset</span></span>
<span data-ttu-id="cbe36-131">Data Factory 管線中的一個活動可以接受零個或多個輸入「資料集」，並且會產生一個或多個輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="cbe36-131">An activity in a Data Factory pipeline can take zero or more input **datasets** and produce one or more output datasets.</span></span> <span data-ttu-id="cbe36-132">活動，您可以指定哪些 hello 輸入的資料在 hello 韻律或 hello 輸出資料以 hello 產生**可用性**hello 資料集定義中的區段。</span><span class="sxs-lookup"><span data-stu-id="cbe36-132">For an activity, you can specify hello cadence at which hello input data is available or hello output data is produced by using hello **availability** section in hello dataset definitions.</span></span> 

<span data-ttu-id="cbe36-133">**頻率**在 hello**可用性**區段會指定 hello 時間單位。</span><span class="sxs-lookup"><span data-stu-id="cbe36-133">**Frequency** in hello **availability** section specifies hello time unit.</span></span> <span data-ttu-id="cbe36-134">hello 允許的頻率的值為： 分鐘、 小時、 天、 週和月份。</span><span class="sxs-lookup"><span data-stu-id="cbe36-134">hello allowed values for frequency are: Minute, Hour, Day, Week, and Month.</span></span> <span data-ttu-id="cbe36-135">hello**間隔**hello 可用性一節中的屬性會指定頻率的倍數。</span><span class="sxs-lookup"><span data-stu-id="cbe36-135">hello **interval** property in hello availability section specifies a multiplier for frequency.</span></span> <span data-ttu-id="cbe36-136">例如： 如果已設定 tooDay hello 頻率間隔設定輸出資料集的 too1，每天產生 hello 輸出資料。</span><span class="sxs-lookup"><span data-stu-id="cbe36-136">For example: if hello frequency is set tooDay and interval is set too1 for an output dataset, hello output data is produced daily.</span></span> <span data-ttu-id="cbe36-137">如果您將 hello frequency 指定為 minute，我們建議您設定小於 15 的 hello 間隔 toono。</span><span class="sxs-lookup"><span data-stu-id="cbe36-137">If you specify hello frequency as minute, we recommend that you set hello interval toono less than 15.</span></span> 

<span data-ttu-id="cbe36-138">在下列範例的 hello，hello 輸入的資料隨附每小時，則會每小時產生 hello 輸出資料 (`"frequency": "Hour", "interval": 1`)。</span><span class="sxs-lookup"><span data-stu-id="cbe36-138">In hello following example, hello input data is available hourly and hello output data is produced hourly (`"frequency": "Hour", "interval": 1`).</span></span> 

<span data-ttu-id="cbe36-139">**輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="cbe36-139">**Input dataset:**</span></span> 

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


<span data-ttu-id="cbe36-140">**輸出資料集**</span><span class="sxs-lookup"><span data-stu-id="cbe36-140">**Output dataset**</span></span>

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

<span data-ttu-id="cbe36-141">目前，**輸出資料集的磁碟機 hello 排程**。</span><span class="sxs-lookup"><span data-stu-id="cbe36-141">Currently, **output dataset drives hello schedule**.</span></span> <span data-ttu-id="cbe36-142">換句話說，hello hello 輸出資料集為指定的排程是使用的 toorun 活動執行階段。</span><span class="sxs-lookup"><span data-stu-id="cbe36-142">In other words, hello schedule specified for hello output dataset is used toorun an activity at runtime.</span></span> <span data-ttu-id="cbe36-143">因此，您必須建立輸出資料集，即使 hello 活動不會產生任何輸出。</span><span class="sxs-lookup"><span data-stu-id="cbe36-143">Therefore, you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="cbe36-144">如果 hello 活動不接受任何輸入，您可以略過建立 hello 輸入資料集。</span><span class="sxs-lookup"><span data-stu-id="cbe36-144">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> 

<span data-ttu-id="cbe36-145">在 hello 下列管線定義，hello**排程器**屬性是使用的 toospecify hello 活動排程。</span><span class="sxs-lookup"><span data-stu-id="cbe36-145">In hello following pipeline definition, hello **scheduler** property is used toospecify schedule for hello activity.</span></span> <span data-ttu-id="cbe36-146">這是選用屬性。</span><span class="sxs-lookup"><span data-stu-id="cbe36-146">This property is optional.</span></span> <span data-ttu-id="cbe36-147">目前，hello 排程 hello 活動必須符合 hello hello 輸出資料集為指定的排程。</span><span class="sxs-lookup"><span data-stu-id="cbe36-147">Currently, hello schedule for hello activity must match hello schedule specified for hello output dataset.</span></span>
 
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

<span data-ttu-id="cbe36-148">在此範例中，每小時 hello 活動執行 hello 之間開始和結束時間的 hello 管線。</span><span class="sxs-lookup"><span data-stu-id="cbe36-148">In this example, hello activity runs hourly between hello start and end times of hello pipeline.</span></span> <span data-ttu-id="cbe36-149">hello 輸出資料會每小時產生三個小時視窗 （上午 8-9 AM，上午 9-10，以及上午 10-11 AM）。</span><span class="sxs-lookup"><span data-stu-id="cbe36-149">hello output data is produced hourly for three-hour windows (8 AM - 9 AM, 9 AM - 10 AM, and 10 AM - 11 AM).</span></span> 

<span data-ttu-id="cbe36-150">活動執行所取用或產生的每個資料單位稱為「資料配量」。</span><span class="sxs-lookup"><span data-stu-id="cbe36-150">Each unit of data consumed or produced by an activity run is called a **data slice**.</span></span> <span data-ttu-id="cbe36-151">hello 下列圖表顯示的活動，具有一個輸入資料集和一個輸出資料集的範例：</span><span class="sxs-lookup"><span data-stu-id="cbe36-151">hello following diagram shows an example of an activity with one input dataset and one output dataset:</span></span> 

![可用性排程器](./media/data-factory-scheduling-and-execution/availability-scheduler.png)

<span data-ttu-id="cbe36-153">hello 圖表會顯示 hello 每小時 hello 的資料配量輸入和輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="cbe36-153">hello diagram shows hello hourly data slices for hello input and output dataset.</span></span> <span data-ttu-id="cbe36-154">hello 圖表顯示三個輸入的配量，準備進行處理。</span><span class="sxs-lookup"><span data-stu-id="cbe36-154">hello diagram shows three input slices that are ready for processing.</span></span> <span data-ttu-id="cbe36-155">hello 10 11 AM 活動正在進行中，產生 hello 10 11 AM 輸出配量。</span><span class="sxs-lookup"><span data-stu-id="cbe36-155">hello 10-11 AM activity is in progress, producing hello 10-11 AM output slice.</span></span> 

<span data-ttu-id="cbe36-156">您可以存取使用變數與 hello 資料集 JSON 中的 hello 目前扇區相關聯的 hello 時間間隔： [SliceStart](data-factory-functions-variables.md#data-factory-system-variables)和[SliceEnd](data-factory-functions-variables.md#data-factory-system-variables)。</span><span class="sxs-lookup"><span data-stu-id="cbe36-156">You can access hello time interval associated with hello current slice in hello dataset JSON by using variables: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) and [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables).</span></span> <span data-ttu-id="cbe36-157">同樣地，您可以存取與視窗相關聯活動使用 hello WindowStart 和 WindowEnd hello 時間間隔。</span><span class="sxs-lookup"><span data-stu-id="cbe36-157">Similarly, you can access hello time interval associated with an activity window by using hello WindowStart and WindowEnd.</span></span> <span data-ttu-id="cbe36-158">hello 排程的活動必須符合 hello hello hello 活動的輸出資料集的排程。</span><span class="sxs-lookup"><span data-stu-id="cbe36-158">hello schedule of an activity must match hello schedule of hello output dataset for hello activity.</span></span> <span data-ttu-id="cbe36-159">因此，hello SliceStart 和 SliceEnd 值為 hello 相同成 WindowStart 和 WindowEnd 值分別。</span><span class="sxs-lookup"><span data-stu-id="cbe36-159">Therefore, hello SliceStart and SliceEnd values are hello same as WindowStart and WindowEnd values respectively.</span></span> <span data-ttu-id="cbe36-160">如需有關這些變數的詳細資訊，請參閱 [Data Factory 函式與系統變數](data-factory-functions-variables.md#data-factory-system-variables)文章。</span><span class="sxs-lookup"><span data-stu-id="cbe36-160">For more information on these variables, see [Data Factory functions and system variables](data-factory-functions-variables.md#data-factory-system-variables) articles.</span></span>  

<span data-ttu-id="cbe36-161">您可以在活動 JSON 中針對不同用途使用這些變數。</span><span class="sxs-lookup"><span data-stu-id="cbe36-161">You can use these variables for different purposes in your activity JSON.</span></span> <span data-ttu-id="cbe36-162">例如，您可以使用它們 tooselect 資料從輸入和輸出資料集代表時間序列資料 (例如： 8 AM too9 AM)。</span><span class="sxs-lookup"><span data-stu-id="cbe36-162">For example, you can use them tooselect data from input and output datasets representing time series data (for example: 8 AM too9 AM).</span></span> <span data-ttu-id="cbe36-163">此範例也會使用**WindowStart**和**WindowEnd** tooselect 活動相關的資料執行，並將它複製 tooa blob 以適當的 hello **folderPath**。</span><span class="sxs-lookup"><span data-stu-id="cbe36-163">This example also uses **WindowStart** and **WindowEnd** tooselect relevant data for an activity run and copy it tooa blob with hello appropriate **folderPath**.</span></span> <span data-ttu-id="cbe36-164">hello **folderPath**每小時是參數化的 toohave 個別的資料夾。</span><span class="sxs-lookup"><span data-stu-id="cbe36-164">hello **folderPath** is parameterized toohave a separate folder for every hour.</span></span>  

<span data-ttu-id="cbe36-165">在上述範例中的 hello，指定輸入和輸出資料集的 hello 排程是 hello 相同 （每小時）。</span><span class="sxs-lookup"><span data-stu-id="cbe36-165">In hello preceding example, hello schedule specified for input and output datasets is hello same (hourly).</span></span> <span data-ttu-id="cbe36-166">如果 hello hello 活動的輸入資料集，可在不同的頻率，假設每隔 15 分鐘會產生此輸出資料集的 hello 活動仍會執行小時一次為 hello 輸出資料集是哪些磁碟機 hello 活動排程。</span><span class="sxs-lookup"><span data-stu-id="cbe36-166">If hello input dataset for hello activity is available at a different frequency, say every 15 minutes, hello activity that produces this output dataset still runs once an hour as hello output dataset is what drives hello activity schedule.</span></span> <span data-ttu-id="cbe36-167">如需詳細資訊，請參閱[使用不同的頻率模型化資料集](#model-datasets-with-different-frequencies)。</span><span class="sxs-lookup"><span data-stu-id="cbe36-167">For more information, see [Model datasets with different frequencies](#model-datasets-with-different-frequencies).</span></span>

## <a name="dataset-availability-and-policies"></a><span data-ttu-id="cbe36-168">資料集可用性和原則</span><span class="sxs-lookup"><span data-stu-id="cbe36-168">Dataset availability and policies</span></span>
<span data-ttu-id="cbe36-169">您已經知道 hello 使用量的頻率和間隔資料集定義的 hello 可用性一節中的屬性。</span><span class="sxs-lookup"><span data-stu-id="cbe36-169">You have seen hello usage of frequency and interval properties in hello availability section of dataset definition.</span></span> <span data-ttu-id="cbe36-170">有幾個會影響 hello 排程和執行活動的其他屬性。</span><span class="sxs-lookup"><span data-stu-id="cbe36-170">There are a few other properties that affect hello scheduling and execution of an activity.</span></span> 

### <a name="dataset-availability"></a><span data-ttu-id="cbe36-171">資料集可用性</span><span class="sxs-lookup"><span data-stu-id="cbe36-171">Dataset availability</span></span> 
<span data-ttu-id="cbe36-172">hello 下表描述您可以使用在 hello 屬性**可用性**> 一節：</span><span class="sxs-lookup"><span data-stu-id="cbe36-172">hello following table describes properties you can use in hello **availability** section:</span></span>

| <span data-ttu-id="cbe36-173">屬性</span><span class="sxs-lookup"><span data-stu-id="cbe36-173">Property</span></span> | <span data-ttu-id="cbe36-174">說明</span><span class="sxs-lookup"><span data-stu-id="cbe36-174">Description</span></span> | <span data-ttu-id="cbe36-175">必要</span><span class="sxs-lookup"><span data-stu-id="cbe36-175">Required</span></span> | <span data-ttu-id="cbe36-176">預設值</span><span class="sxs-lookup"><span data-stu-id="cbe36-176">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cbe36-177">frequency</span><span class="sxs-lookup"><span data-stu-id="cbe36-177">frequency</span></span> |<span data-ttu-id="cbe36-178">指定資料集配量實際執行環境的 hello 時間單位。</span><span class="sxs-lookup"><span data-stu-id="cbe36-178">Specifies hello time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="cbe36-179"><b>支援的頻率</b>：Minute、Hour、Day、Week、Month</span><span class="sxs-lookup"><span data-stu-id="cbe36-179"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="cbe36-180">是</span><span class="sxs-lookup"><span data-stu-id="cbe36-180">Yes</span></span> |<span data-ttu-id="cbe36-181">NA</span><span class="sxs-lookup"><span data-stu-id="cbe36-181">NA</span></span> |
| <span data-ttu-id="cbe36-182">interval</span><span class="sxs-lookup"><span data-stu-id="cbe36-182">interval</span></span> |<span data-ttu-id="cbe36-183">指定頻率的倍數</span><span class="sxs-lookup"><span data-stu-id="cbe36-183">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="cbe36-184">[頻率 x 間隔] 判斷頻率 hello 產生配量。</span><span class="sxs-lookup"><span data-stu-id="cbe36-184">”Frequency x interval” determines how often hello slice is produced.</span></span><br/><br/><span data-ttu-id="cbe36-185">如果您需要 hello 配量每小時的資料集 toobe，設定<b>頻率</b>太<b>小時</b>，和<b>間隔</b>太<b>1</b>。</span><span class="sxs-lookup"><span data-stu-id="cbe36-185">If you need hello dataset toobe sliced on an hourly basis, you set <b>Frequency</b> too<b>Hour</b>, and <b>interval</b> too<b>1</b>.</span></span><br/><br/><span data-ttu-id="cbe36-186"><b>請注意</b>： 如果您將 Frequency 指定為 Minute，我們建議您設定小於 15 的 hello 間隔 toono</span><span class="sxs-lookup"><span data-stu-id="cbe36-186"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set hello interval toono less than 15</span></span> |<span data-ttu-id="cbe36-187">是</span><span class="sxs-lookup"><span data-stu-id="cbe36-187">Yes</span></span> |<span data-ttu-id="cbe36-188">NA</span><span class="sxs-lookup"><span data-stu-id="cbe36-188">NA</span></span> |
| <span data-ttu-id="cbe36-189">style</span><span class="sxs-lookup"><span data-stu-id="cbe36-189">style</span></span> |<span data-ttu-id="cbe36-190">指定是否應該在 hello 開始/結束 hello 間隔產生 hello 配量。</span><span class="sxs-lookup"><span data-stu-id="cbe36-190">Specifies whether hello slice should be produced at hello start/end of hello interval.</span></span><ul><li><span data-ttu-id="cbe36-191">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="cbe36-191">StartOfInterval</span></span></li><li><span data-ttu-id="cbe36-192">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="cbe36-192">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="cbe36-193">如果頻率設定 tooMonth 樣式設定 tooEndOfInterval，hello 當月最後一天產生 hello 配量。</span><span class="sxs-lookup"><span data-stu-id="cbe36-193">If Frequency is set tooMonth and style is set tooEndOfInterval, hello slice is produced on hello last day of month.</span></span> <span data-ttu-id="cbe36-194">如果 hello 樣式設定 tooStartOfInterval，hello 點產生配量 hello 當月第一日。</span><span class="sxs-lookup"><span data-stu-id="cbe36-194">If hello style is set tooStartOfInterval, hello slice is produced on hello first day of month.</span></span><br/><br/><span data-ttu-id="cbe36-195">如果頻率設定 tooDay tooEndOfInterval 設定樣式時，會產生 hello 的 hello 當日的前一個小時 hello 配量。</span><span class="sxs-lookup"><span data-stu-id="cbe36-195">If Frequency is set tooDay and style is set tooEndOfInterval, hello slice is produced in hello last hour of hello day.</span></span><br/><br/><span data-ttu-id="cbe36-196">如果頻率設定 tooHour 樣式設定 tooEndOfInterval，hello 配量會產生在 hello hello 小時結尾。</span><span class="sxs-lookup"><span data-stu-id="cbe36-196">If Frequency is set tooHour and style is set tooEndOfInterval, hello slice is produced at hello end of hello hour.</span></span> <span data-ttu-id="cbe36-197">例如，1 PM – 2 PM 期間的配量，hello 配量會在 2 PM 產生。</span><span class="sxs-lookup"><span data-stu-id="cbe36-197">For example, for a slice for 1 PM – 2 PM period, hello slice is produced at 2 PM.</span></span> |<span data-ttu-id="cbe36-198">否</span><span class="sxs-lookup"><span data-stu-id="cbe36-198">No</span></span> |<span data-ttu-id="cbe36-199">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="cbe36-199">EndOfInterval</span></span> |
| <span data-ttu-id="cbe36-200">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="cbe36-200">anchorDateTime</span></span> |<span data-ttu-id="cbe36-201">定義中使用的排程器 toocompute 資料集配量界限時間 hello 絕對位置。</span><span class="sxs-lookup"><span data-stu-id="cbe36-201">Defines hello absolute position in time used by scheduler toocompute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="cbe36-202"><b>請注意</b>： 如果 hello AnchorDateTime 具有比 hello 頻率較精細的日期部分，則 hello 更精細的部分會被忽略。</span><span class="sxs-lookup"><span data-stu-id="cbe36-202"><b>Note</b>: If hello AnchorDateTime has date parts that are more granular than hello frequency then hello more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="cbe36-203">例如，如果 hello<b>間隔</b>是<b>每小時</b>(頻率： hour，interval: 1) 和 hello <b>AnchorDateTime</b>包含<b>分鐘和秒鐘</b>，然後 hello<b>分鐘和秒鐘</b>hello AnchorDateTime 的部分會被忽略。</span><span class="sxs-lookup"><span data-stu-id="cbe36-203">For example, if hello <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and hello <b>AnchorDateTime</b> contains <b>minutes and seconds</b>, then hello <b>minutes and seconds</b> parts of hello AnchorDateTime are ignored.</span></span> |<span data-ttu-id="cbe36-204">否</span><span class="sxs-lookup"><span data-stu-id="cbe36-204">No</span></span> |<span data-ttu-id="cbe36-205">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="cbe36-205">01/01/0001</span></span> |
| <span data-ttu-id="cbe36-206">Offset</span><span class="sxs-lookup"><span data-stu-id="cbe36-206">offset</span></span> |<span data-ttu-id="cbe36-207">哪些 hello 的所有資料集配量的開始與結束移位的 Timespan。</span><span class="sxs-lookup"><span data-stu-id="cbe36-207">Timespan by which hello start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="cbe36-208"><b>請注意</b>: hello 結果指定 anchorDateTime 和 offset，如果是合併的 hello 移位。</span><span class="sxs-lookup"><span data-stu-id="cbe36-208"><b>Note</b>: If both anchorDateTime and offset are specified, hello result is hello combined shift.</span></span> |<span data-ttu-id="cbe36-209">否</span><span class="sxs-lookup"><span data-stu-id="cbe36-209">No</span></span> |<span data-ttu-id="cbe36-210">NA</span><span class="sxs-lookup"><span data-stu-id="cbe36-210">NA</span></span> |

### <a name="offset-example"></a><span data-ttu-id="cbe36-211">位移範例</span><span class="sxs-lookup"><span data-stu-id="cbe36-211">offset example</span></span>
<span data-ttu-id="cbe36-212">根據預設，每日 (`"frequency": "Day", "interval": 1`) 配量的開始時間是 UTC 時間上午 12 點 (午夜)。</span><span class="sxs-lookup"><span data-stu-id="cbe36-212">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM UTC time (midnight).</span></span> <span data-ttu-id="cbe36-213">如果要改為 hello 開始時間 toobe 上午 6 點 UTC 時間，將設定 hello 位移 hello 下列程式碼片段所示：</span><span class="sxs-lookup"><span data-stu-id="cbe36-213">If you want hello start time toobe 6 AM UTC time instead, set hello offset as shown in hello following snippet:</span></span> 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a><span data-ttu-id="cbe36-214">anchorDateTime 範例</span><span class="sxs-lookup"><span data-stu-id="cbe36-214">anchorDateTime example</span></span>
<span data-ttu-id="cbe36-215">在下列範例的 hello，hello 資料集，會產生一次每 23 的小時。</span><span class="sxs-lookup"><span data-stu-id="cbe36-215">In hello following example, hello dataset is produced once every 23 hours.</span></span> <span data-ttu-id="cbe36-216">hello 第一個配量開始 hello anchorDateTime 太設定所指定的 hello 時間`2017-04-19T08:00:00`（UTC 時間）。</span><span class="sxs-lookup"><span data-stu-id="cbe36-216">hello first slice starts at hello time specified by hello anchorDateTime, which is set too`2017-04-19T08:00:00` (UTC time).</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a><span data-ttu-id="cbe36-217">位移/樣式範例</span><span class="sxs-lookup"><span data-stu-id="cbe36-217">offset/style Example</span></span>
<span data-ttu-id="cbe36-218">hello 下列資料集的每月的資料集，且會在上午 8:00 的每個月的第 3 產生 (`3.08:00:00`):</span><span class="sxs-lookup"><span data-stu-id="cbe36-218">hello following dataset is a monthly dataset and is produced on 3rd of every month at 8:00 AM (`3.08:00:00`):</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

### <a name="dataset-policy"></a><span data-ttu-id="cbe36-219">資料集原則</span><span class="sxs-lookup"><span data-stu-id="cbe36-219">Dataset policy</span></span>
<span data-ttu-id="cbe36-220">資料集，可以指定如何驗證配量執行所產生的 hello 資料供取用之前的驗證原則定義。</span><span class="sxs-lookup"><span data-stu-id="cbe36-220">A dataset can have a validation policy defined that specifies how hello data generated by a slice execution can be validated before it is ready for consumption.</span></span> <span data-ttu-id="cbe36-221">在這種情況下，hello 配量完成執行之後 hello 輸出配量狀態會變成太**等候**的子狀態與**驗證**。</span><span class="sxs-lookup"><span data-stu-id="cbe36-221">In such cases, after hello slice has finished execution, hello output slice status is changed too**Waiting** with a substatus of **Validation**.</span></span> <span data-ttu-id="cbe36-222">Hello 配量會驗證之後，hello 配量狀態會變更太**準備**。</span><span class="sxs-lookup"><span data-stu-id="cbe36-222">After hello slices are validated, hello slice status changes too**Ready**.</span></span> <span data-ttu-id="cbe36-223">如果已產生的資料配量，但未通過 hello 驗證，不會處理下游配量相依於此配量的活動執行。</span><span class="sxs-lookup"><span data-stu-id="cbe36-223">If a data slice has been produced but did not pass hello validation, activity runs for downstream slices that depend on this slice are not processed.</span></span> <span data-ttu-id="cbe36-224">[監視和管理管線](data-factory-monitor-manage-pipelines.md)涵蓋 hello 的 Data Factory 中的資料配量的各種狀態。</span><span class="sxs-lookup"><span data-stu-id="cbe36-224">[Monitor and manage pipelines](data-factory-monitor-manage-pipelines.md) covers hello various states of data slices in Data Factory.</span></span>

<span data-ttu-id="cbe36-225">hello**原則**資料集定義中的區段會定義 hello 準則或 hello 資料集配量的 hello 條件必須滿足。</span><span class="sxs-lookup"><span data-stu-id="cbe36-225">hello **policy** section in dataset definition defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span> <span data-ttu-id="cbe36-226">hello 下表描述您可以使用在 hello 屬性**原則**> 一節：</span><span class="sxs-lookup"><span data-stu-id="cbe36-226">hello following table describes properties you can use in hello **policy** section:</span></span>

| <span data-ttu-id="cbe36-227">原則名稱</span><span class="sxs-lookup"><span data-stu-id="cbe36-227">Policy Name</span></span> | <span data-ttu-id="cbe36-228">說明</span><span class="sxs-lookup"><span data-stu-id="cbe36-228">Description</span></span> | <span data-ttu-id="cbe36-229">套用太</span><span class="sxs-lookup"><span data-stu-id="cbe36-229">Applied too</span></span>| <span data-ttu-id="cbe36-230">必要</span><span class="sxs-lookup"><span data-stu-id="cbe36-230">Required</span></span> | <span data-ttu-id="cbe36-231">預設值</span><span class="sxs-lookup"><span data-stu-id="cbe36-231">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="cbe36-232">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="cbe36-232">minimumSizeMB</span></span> | <span data-ttu-id="cbe36-233">驗證中的 hello 資料**Azure blob**符合 hello 最小大小需求 （以 mb 為單位）。</span><span class="sxs-lookup"><span data-stu-id="cbe36-233">Validates that hello data in an **Azure blob** meets hello minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="cbe36-234">Azure Blob</span><span class="sxs-lookup"><span data-stu-id="cbe36-234">Azure Blob</span></span> |<span data-ttu-id="cbe36-235">否</span><span class="sxs-lookup"><span data-stu-id="cbe36-235">No</span></span> |<span data-ttu-id="cbe36-236">NA</span><span class="sxs-lookup"><span data-stu-id="cbe36-236">NA</span></span> |
| <span data-ttu-id="cbe36-237">minimumRows</span><span class="sxs-lookup"><span data-stu-id="cbe36-237">minimumRows</span></span> | <span data-ttu-id="cbe36-238">驗證中的 hello 資料**Azure SQL database**或**Azure 資料表**包含 hello 最小數目的資料列。</span><span class="sxs-lookup"><span data-stu-id="cbe36-238">Validates that hello data in an **Azure SQL database** or an **Azure table** contains hello minimum number of rows.</span></span> |<ul><li><span data-ttu-id="cbe36-239">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="cbe36-239">Azure SQL Database</span></span></li><li><span data-ttu-id="cbe36-240">Azure 資料表</span><span class="sxs-lookup"><span data-stu-id="cbe36-240">Azure Table</span></span></li></ul> |<span data-ttu-id="cbe36-241">否</span><span class="sxs-lookup"><span data-stu-id="cbe36-241">No</span></span> |<span data-ttu-id="cbe36-242">NA</span><span class="sxs-lookup"><span data-stu-id="cbe36-242">NA</span></span> |

#### <a name="examples"></a><span data-ttu-id="cbe36-243">範例</span><span class="sxs-lookup"><span data-stu-id="cbe36-243">Examples</span></span>
<span data-ttu-id="cbe36-244">**minimumSizeMB：**</span><span class="sxs-lookup"><span data-stu-id="cbe36-244">**minimumSizeMB:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="cbe36-245">**minimumRows**</span><span class="sxs-lookup"><span data-stu-id="cbe36-245">**minimumRows**</span></span>

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

<span data-ttu-id="cbe36-246">如需有關這些屬性及範例的詳細資訊，請參閱[建立資料集](data-factory-create-datasets.md)一文。</span><span class="sxs-lookup"><span data-stu-id="cbe36-246">For more information about these properties and examples, see [Create datasets](data-factory-create-datasets.md) article.</span></span> 

## <a name="activity-policies"></a><span data-ttu-id="cbe36-247">活動原則</span><span class="sxs-lookup"><span data-stu-id="cbe36-247">Activity policies</span></span>
<span data-ttu-id="cbe36-248">特別是當處理資料表的 hello 配量時，原則會影響 hello 執行階段行為的活動。</span><span class="sxs-lookup"><span data-stu-id="cbe36-248">Policies affect hello run-time behavior of an activity, specifically when hello slice of a table is processed.</span></span> <span data-ttu-id="cbe36-249">下表中的 hello 提供 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="cbe36-249">hello following table provides hello details.</span></span>

| <span data-ttu-id="cbe36-250">屬性</span><span class="sxs-lookup"><span data-stu-id="cbe36-250">Property</span></span> | <span data-ttu-id="cbe36-251">允許的值</span><span class="sxs-lookup"><span data-stu-id="cbe36-251">Permitted values</span></span> | <span data-ttu-id="cbe36-252">預設值</span><span class="sxs-lookup"><span data-stu-id="cbe36-252">Default Value</span></span> | <span data-ttu-id="cbe36-253">說明</span><span class="sxs-lookup"><span data-stu-id="cbe36-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cbe36-254">並行</span><span class="sxs-lookup"><span data-stu-id="cbe36-254">concurrency</span></span> |<span data-ttu-id="cbe36-255">整數 </span><span class="sxs-lookup"><span data-stu-id="cbe36-255">Integer</span></span> <br/><br/><span data-ttu-id="cbe36-256">最大值：10</span><span class="sxs-lookup"><span data-stu-id="cbe36-256">Max value: 10</span></span> |<span data-ttu-id="cbe36-257">1</span><span class="sxs-lookup"><span data-stu-id="cbe36-257">1</span></span> |<span data-ttu-id="cbe36-258">並行執行的 hello 活動的數目。</span><span class="sxs-lookup"><span data-stu-id="cbe36-258">Number of concurrent executions of hello activity.</span></span><br/><br/><span data-ttu-id="cbe36-259">它決定不同配量上可能發生的平行活動執行的 hello 次數。</span><span class="sxs-lookup"><span data-stu-id="cbe36-259">It determines hello number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="cbe36-260">例如，如果活動需要透過 toogo 大量可用的資料，具有較大的並行值就會加快 hello 資料處理。</span><span class="sxs-lookup"><span data-stu-id="cbe36-260">For example, if an activity needs toogo through a large set of available data, having a larger concurrency value speeds up hello data processing.</span></span> |
| <span data-ttu-id="cbe36-261">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="cbe36-261">executionPriorityOrder</span></span> |<span data-ttu-id="cbe36-262">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="cbe36-262">NewestFirst</span></span><br/><br/><span data-ttu-id="cbe36-263">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="cbe36-263">OldestFirst</span></span> |<span data-ttu-id="cbe36-264">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="cbe36-264">OldestFirst</span></span> |<span data-ttu-id="cbe36-265">判斷正在處理的資料配量順序 hello。</span><span class="sxs-lookup"><span data-stu-id="cbe36-265">Determines hello ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="cbe36-266">例如，如果您有 2 個配量 (一個發生在下午 4 點，另一個發生在下午 5 點)，而兩者都暫停執行。</span><span class="sxs-lookup"><span data-stu-id="cbe36-266">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="cbe36-267">如果您設定 hello executionpriorityorder 設 toobe NewestFirst，會先處理下午 5 點的 hello 配量。</span><span class="sxs-lookup"><span data-stu-id="cbe36-267">If you set hello executionPriorityOrder toobe NewestFirst, hello slice at 5 PM is processed first.</span></span> <span data-ttu-id="cbe36-268">同樣地如果您設定 hello executionpriorityorder 設 toobe OldestFIrst，然後在下午 4 點 hello 配量會處理。</span><span class="sxs-lookup"><span data-stu-id="cbe36-268">Similarly if you set hello executionPriorityORder toobe OldestFIrst, then hello slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="cbe36-269">retry</span><span class="sxs-lookup"><span data-stu-id="cbe36-269">retry</span></span> |<span data-ttu-id="cbe36-270">整數 </span><span class="sxs-lookup"><span data-stu-id="cbe36-270">Integer</span></span><br/><br/><span data-ttu-id="cbe36-271">最大值可以是 10</span><span class="sxs-lookup"><span data-stu-id="cbe36-271">Max value can be 10</span></span> |<span data-ttu-id="cbe36-272">0</span><span class="sxs-lookup"><span data-stu-id="cbe36-272">0</span></span> |<span data-ttu-id="cbe36-273">Hello hello 配量的資料處理之前的重試的數目會標示為失敗。</span><span class="sxs-lookup"><span data-stu-id="cbe36-273">Number of retries before hello data processing for hello slice is marked as Failure.</span></span> <span data-ttu-id="cbe36-274">資料配量的活動執行會重試總 toohello 指定重試計數。</span><span class="sxs-lookup"><span data-stu-id="cbe36-274">Activity execution for a data slice is retried up toohello specified retry count.</span></span> <span data-ttu-id="cbe36-275">hello 重試會儘速 hello 失敗後進行。</span><span class="sxs-lookup"><span data-stu-id="cbe36-275">hello retry is done as soon as possible after hello failure.</span></span> |
| <span data-ttu-id="cbe36-276">timeout</span><span class="sxs-lookup"><span data-stu-id="cbe36-276">timeout</span></span> |<span data-ttu-id="cbe36-277">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="cbe36-277">TimeSpan</span></span> |<span data-ttu-id="cbe36-278">00:00:00</span><span class="sxs-lookup"><span data-stu-id="cbe36-278">00:00:00</span></span> |<span data-ttu-id="cbe36-279">Hello 活動的逾時。</span><span class="sxs-lookup"><span data-stu-id="cbe36-279">Timeout for hello activity.</span></span> <span data-ttu-id="cbe36-280">範例︰00:10:00 (意指逾時 10 分鐘)</span><span class="sxs-lookup"><span data-stu-id="cbe36-280">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="cbe36-281">如果未指定值，或為 0，hello 逾時是無限的。</span><span class="sxs-lookup"><span data-stu-id="cbe36-281">If a value is not specified or is 0, hello timeout is infinite.</span></span><br/><br/><span data-ttu-id="cbe36-282">如果配量的 hello 資料處理時間超過 hello 逾時值，則會取消，並 hello 系統會嘗試 tooretry hello 處理。</span><span class="sxs-lookup"><span data-stu-id="cbe36-282">If hello data processing time on a slice exceeds hello timeout value, it is canceled, and hello system attempts tooretry hello processing.</span></span> <span data-ttu-id="cbe36-283">hello 重試次數取決於 hello 重試屬性。</span><span class="sxs-lookup"><span data-stu-id="cbe36-283">hello number of retries depends on hello retry property.</span></span> <span data-ttu-id="cbe36-284">發生逾時，hello 狀態會設定 tooTimedOut。</span><span class="sxs-lookup"><span data-stu-id="cbe36-284">When timeout occurs, hello status is set tooTimedOut.</span></span> |
| <span data-ttu-id="cbe36-285">delay</span><span class="sxs-lookup"><span data-stu-id="cbe36-285">delay</span></span> |<span data-ttu-id="cbe36-286">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="cbe36-286">TimeSpan</span></span> |<span data-ttu-id="cbe36-287">00:00:00</span><span class="sxs-lookup"><span data-stu-id="cbe36-287">00:00:00</span></span> |<span data-ttu-id="cbe36-288">指定 hello hello 配量開始的資料處理之前的延遲。</span><span class="sxs-lookup"><span data-stu-id="cbe36-288">Specify hello delay before data processing of hello slice starts.</span></span><br/><br/><span data-ttu-id="cbe36-289">hello 延遲 hello 預期執行時間過去後，會啟動 hello 執行之活動的資料配量。</span><span class="sxs-lookup"><span data-stu-id="cbe36-289">hello execution of activity for a data slice is started after hello Delay is past hello expected execution time.</span></span><br/><br/><span data-ttu-id="cbe36-290">範例︰00:10:00 (意指延遲 10 分鐘)</span><span class="sxs-lookup"><span data-stu-id="cbe36-290">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="cbe36-291">longRetry</span><span class="sxs-lookup"><span data-stu-id="cbe36-291">longRetry</span></span> |<span data-ttu-id="cbe36-292">整數 </span><span class="sxs-lookup"><span data-stu-id="cbe36-292">Integer</span></span><br/><br/><span data-ttu-id="cbe36-293">最大值：10</span><span class="sxs-lookup"><span data-stu-id="cbe36-293">Max value: 10</span></span> |<span data-ttu-id="cbe36-294">1</span><span class="sxs-lookup"><span data-stu-id="cbe36-294">1</span></span> |<span data-ttu-id="cbe36-295">hello 的長時間重試次數 hello 配量執行失敗。</span><span class="sxs-lookup"><span data-stu-id="cbe36-295">hello number of long retry attempts before hello slice execution is failed.</span></span><br/><br/><span data-ttu-id="cbe36-296">多個 longRetry 嘗試之間以 longRetryInterval 隔開。</span><span class="sxs-lookup"><span data-stu-id="cbe36-296">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="cbe36-297">因此，如果您需要 toospecify 重試嘗試之間的時間，請使用 longRetry。</span><span class="sxs-lookup"><span data-stu-id="cbe36-297">So if you need toospecify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="cbe36-298">如果指定 Retry 和 longRetry，每個 longRetry 嘗試包含重試次數和 hello 最大嘗試次數為重試 * longRetry。</span><span class="sxs-lookup"><span data-stu-id="cbe36-298">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and hello max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="cbe36-299">例如，如果我們有下列 hello 活動原則中的設定的 hello:</span><span class="sxs-lookup"><span data-stu-id="cbe36-299">For example, if we have hello following settings in hello activity policy:</span></span><br/><span data-ttu-id="cbe36-300">Retry：3</span><span class="sxs-lookup"><span data-stu-id="cbe36-300">Retry: 3</span></span><br/><span data-ttu-id="cbe36-301">longRetry：2</span><span class="sxs-lookup"><span data-stu-id="cbe36-301">longRetry: 2</span></span><br/><span data-ttu-id="cbe36-302">longRetryInterval：01:00:00</span><span class="sxs-lookup"><span data-stu-id="cbe36-302">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="cbe36-303">假設有一個配量 tooexecute （等待狀態），就會失敗的每次 hello 活動執行。</span><span class="sxs-lookup"><span data-stu-id="cbe36-303">Assume there is only one slice tooexecute (status is Waiting) and hello activity execution fails every time.</span></span> <span data-ttu-id="cbe36-304">一開始會有 3 次連續執行嘗試。</span><span class="sxs-lookup"><span data-stu-id="cbe36-304">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="cbe36-305">每次嘗試之後, hello 配量狀態會是 Retry。</span><span class="sxs-lookup"><span data-stu-id="cbe36-305">After each attempt, hello slice status would be Retry.</span></span> <span data-ttu-id="cbe36-306">前 3 的嘗試次數已超過之後，hello 配量狀態就會是 LongRetry。</span><span class="sxs-lookup"><span data-stu-id="cbe36-306">After first 3 attempts are over, hello slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="cbe36-307">一個小時 (也就是 longRetryInteval 的值) 之後，會有另一組 3 次連續執行嘗試。</span><span class="sxs-lookup"><span data-stu-id="cbe36-307">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="cbe36-308">之後，hello 配量狀態會變成 Failed，而且會嘗試重試。</span><span class="sxs-lookup"><span data-stu-id="cbe36-308">After that, hello slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="cbe36-309">因此全部已進行 6 次嘗試。</span><span class="sxs-lookup"><span data-stu-id="cbe36-309">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="cbe36-310">如果執行成功，hello 配量狀態就會是 Ready，無需重試嘗試。</span><span class="sxs-lookup"><span data-stu-id="cbe36-310">If any execution succeeds, hello slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="cbe36-311">在位置相依的資料到達在不具決定性的時間或 hello 整體環境穩定底下的資料處理發生的情況下可用 longRetry。</span><span class="sxs-lookup"><span data-stu-id="cbe36-311">longRetry may be used in situations where dependent data arrives at non-deterministic times or hello overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="cbe36-312">在這種情況下，逐一進行重試可能無法幫助，這樣導致 hello 的時間間隔之後想要的輸出。</span><span class="sxs-lookup"><span data-stu-id="cbe36-312">In such cases, doing retries one after another may not help and doing so after an interval of time results in hello desired output.</span></span><br/><br/><span data-ttu-id="cbe36-313">提醒：請勿設定較大的 longRetry 或 longRetryInterval 值。</span><span class="sxs-lookup"><span data-stu-id="cbe36-313">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="cbe36-314">較大的值通常表示其他系統問題。</span><span class="sxs-lookup"><span data-stu-id="cbe36-314">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="cbe36-315">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="cbe36-315">longRetryInterval</span></span> |<span data-ttu-id="cbe36-316">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="cbe36-316">TimeSpan</span></span> |<span data-ttu-id="cbe36-317">00:00:00</span><span class="sxs-lookup"><span data-stu-id="cbe36-317">00:00:00</span></span> |<span data-ttu-id="cbe36-318">hello 長時間重試嘗試之間的延遲</span><span class="sxs-lookup"><span data-stu-id="cbe36-318">hello delay between long retry attempts</span></span> |

<span data-ttu-id="cbe36-319">如需詳細資訊，請參閱[管線](data-factory-create-pipelines.md)一文。</span><span class="sxs-lookup"><span data-stu-id="cbe36-319">For more information, see [Pipelines](data-factory-create-pipelines.md) article.</span></span> 

## <a name="parallel-processing-of-data-slices"></a><span data-ttu-id="cbe36-320">資料配量的平行處理</span><span class="sxs-lookup"><span data-stu-id="cbe36-320">Parallel processing of data slices</span></span>
<span data-ttu-id="cbe36-321">您可以設定 hello hello 管線的開始日期在過去的 hello。</span><span class="sxs-lookup"><span data-stu-id="cbe36-321">You can set hello start date for hello pipeline in hello past.</span></span> <span data-ttu-id="cbe36-322">當您這樣做時，Data Factory 會自動計算 （背景填滿） 在過去的 hello 中的所有資料配量，並開始處理它們。</span><span class="sxs-lookup"><span data-stu-id="cbe36-322">When you do so, Data Factory automatically calculates (back fills) all data slices in hello past and begins processing them.</span></span> <span data-ttu-id="cbe36-323">例如： 如果管線的開始日期 2017年-04-01，且 hello 目前的日期是 2017年-04-10。</span><span class="sxs-lookup"><span data-stu-id="cbe36-323">For example: if you create a pipeline with start date 2017-04-01 and hello current date is 2017-04-10.</span></span> <span data-ttu-id="cbe36-324">如果 hello 韻律 hello 的輸出資料集是每日，則處理從 2017年-04-01 所有 hello 配量的 Data Factory 啟動 too2017-04 09 立即因為 hello 開始日期是在過去的 hello。</span><span class="sxs-lookup"><span data-stu-id="cbe36-324">If hello cadence of hello output dataset is daily, then Data Factory starts processing all hello slices from 2017-04-01 too2017-04-09 immediately because hello start date is in hello past.</span></span> <span data-ttu-id="cbe36-325">從 2017年-04-10 hello 配量不會處理尚未因為 hello hello 可用性一節中的樣式屬性的值為 EndOfInterval 預設值。</span><span class="sxs-lookup"><span data-stu-id="cbe36-325">hello slice from 2017-04-10 is not processed yet because hello value of style property in hello availability section is EndOfInterval by default.</span></span> <span data-ttu-id="cbe36-326">hello 最舊的配量處理第一個 hello 預設 executionpriorityorder 設的值是 OldestFirst。</span><span class="sxs-lookup"><span data-stu-id="cbe36-326">hello oldest slice is processed first as hello default value of executionPriorityOrder is OldestFirst.</span></span> <span data-ttu-id="cbe36-327">如需 hello 樣式屬性的說明，請參閱[資料集可用性](#dataset-availability)> 一節。</span><span class="sxs-lookup"><span data-stu-id="cbe36-327">For a description of hello style property, see [dataset availability](#dataset-availability) section.</span></span> <span data-ttu-id="cbe36-328">如需 hello executionpriorityorder 設 > 一節的說明，請參閱 hello[活動原則](#activity-policies)> 一節。</span><span class="sxs-lookup"><span data-stu-id="cbe36-328">For a description of hello executionPriorityOrder section, see hello [activity policies](#activity-policies) section.</span></span> 

<span data-ttu-id="cbe36-329">您可以設定平行處理所設定的 hello 後填滿的資料配量 toobe**並行**屬性在 hello**原則**hello 活動 JSON 的區段。</span><span class="sxs-lookup"><span data-stu-id="cbe36-329">You can configure back-filled data slices toobe processed in parallel by setting hello **concurrency** property in hello **policy** section of hello activity JSON.</span></span> <span data-ttu-id="cbe36-330">此屬性決定不同配量上可能發生的平行活動執行的 hello 次數。</span><span class="sxs-lookup"><span data-stu-id="cbe36-330">This property determines hello number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="cbe36-331">hello hello 並行屬性的預設值為 1。</span><span class="sxs-lookup"><span data-stu-id="cbe36-331">hello default value for hello concurrency property is 1.</span></span> <span data-ttu-id="cbe36-332">因此，預設會一次處理一個配量。</span><span class="sxs-lookup"><span data-stu-id="cbe36-332">Therefore, one slice is processed at a time by default.</span></span> <span data-ttu-id="cbe36-333">hello 最大值為 10。</span><span class="sxs-lookup"><span data-stu-id="cbe36-333">hello maximum value is 10.</span></span> <span data-ttu-id="cbe36-334">當管線時必須透過大量可用的資料，具有較大的並行值 toogo 可加快 hello 資料處理。</span><span class="sxs-lookup"><span data-stu-id="cbe36-334">When a pipeline needs toogo through a large set of available data, having a larger concurrency value speeds up hello data processing.</span></span> 

## <a name="rerun-a-failed-data-slice"></a><span data-ttu-id="cbe36-335">重新執行失敗的資料配量</span><span class="sxs-lookup"><span data-stu-id="cbe36-335">Rerun a failed data slice</span></span>
<span data-ttu-id="cbe36-336">當處理資料配量時，發生錯誤時，您可以找出 hello 處理配量使用 Azure 入口網站的刀鋒視窗或監視和管理應用程式失敗的原因。</span><span class="sxs-lookup"><span data-stu-id="cbe36-336">When an error occurs while processing a data slice, you can find out why hello processing of a slice failed by using Azure portal blades or Monitor and Manage App.</span></span> <span data-ttu-id="cbe36-337">如需詳細資訊，請參閱[使用 Azure 入口網站刀鋒視窗監視和管理管線](data-factory-monitor-manage-pipelines.md)或[監視和管理應用程式](data-factory-monitor-manage-app.md)。</span><span class="sxs-lookup"><span data-stu-id="cbe36-337">See [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md) for details.</span></span>

<span data-ttu-id="cbe36-338">請考慮下列範例會顯示兩個活動的 hello。</span><span class="sxs-lookup"><span data-stu-id="cbe36-338">Consider hello following example, which shows two activities.</span></span> <span data-ttu-id="cbe36-339">Activity1 和 Activity 2。</span><span class="sxs-lookup"><span data-stu-id="cbe36-339">Activity1 and Activity 2.</span></span> <span data-ttu-id="cbe36-340">Activity1 會消耗 Dataset1 配量，並產生配量的 Dataset2，做為輸入供 Activity2 tooproduce hello 最終資料集配量。</span><span class="sxs-lookup"><span data-stu-id="cbe36-340">Activity1 consumes a slice of Dataset1 and produces a slice of Dataset2, which is consumed as an input by Activity2 tooproduce a slice of hello Final Dataset.</span></span>

![失敗的配量](./media/data-factory-scheduling-and-execution/failed-slice.png)

<span data-ttu-id="cbe36-342">hello 張圖表顯示三個新的配量，不足時發生失敗產生項目的 hello 上午 9 10 配量的 Dataset2。</span><span class="sxs-lookup"><span data-stu-id="cbe36-342">hello diagram shows that out of three recent slices, there was a failure producing hello 9-10 AM slice for Dataset2.</span></span> <span data-ttu-id="cbe36-343">Data Factory 自動追蹤相依性 hello 時間序列資料集。</span><span class="sxs-lookup"><span data-stu-id="cbe36-343">Data Factory automatically tracks dependency for hello time series dataset.</span></span> <span data-ttu-id="cbe36-344">如此一來，不會啟動 hello hello 上午 9 10 下游配量執行的活動。</span><span class="sxs-lookup"><span data-stu-id="cbe36-344">As a result, it does not start hello activity run for hello 9-10 AM downstream slice.</span></span>

<span data-ttu-id="cbe36-345">資料處理站的監視與管理工具可讓您 toodrill hello 診斷記錄檔到 hello 失敗的配量 tooeasily 尋找 hello 根 hello 問題會造成，，修正此問題。</span><span class="sxs-lookup"><span data-stu-id="cbe36-345">Data Factory monitoring and management tools allow you toodrill into hello diagnostic logs for hello failed slice tooeasily find hello root cause for hello issue and fix it.</span></span> <span data-ttu-id="cbe36-346">修正 hello 問題之後，您可以輕鬆地開始執行 tooproduce hello 失敗配量的 hello 活動。</span><span class="sxs-lookup"><span data-stu-id="cbe36-346">After you have fixed hello issue, you can easily start hello activity run tooproduce hello failed slice.</span></span> <span data-ttu-id="cbe36-347">如需有關如何 toorerun 和了解資料配量的狀態轉換，請參閱[監視及管理使用 Azure 入口網站的刀鋒視窗的管線](data-factory-monitor-manage-pipelines.md)或[監視和管理應用程式](data-factory-monitor-manage-app.md)。</span><span class="sxs-lookup"><span data-stu-id="cbe36-347">For more information on how toorerun and understand state transitions for data slices, see [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span>

<span data-ttu-id="cbe36-348">在重新執行 hello 之後的上午 9 10 配量**Dataset2**，Data Factory 啟動 hello hello 最終資料集上執行 hello 上午 9 10 相依配量。</span><span class="sxs-lookup"><span data-stu-id="cbe36-348">After you rerun hello 9-10 AM slice for **Dataset2**, Data Factory starts hello run for hello 9-10 AM dependent slice on hello final dataset.</span></span>

![重新執行失敗的配量](./media/data-factory-scheduling-and-execution/rerun-failed-slice.png)

## <a name="multiple-activities-in-a-pipeline"></a><span data-ttu-id="cbe36-350">管線中的多個活動</span><span class="sxs-lookup"><span data-stu-id="cbe36-350">Multiple activities in a pipeline</span></span>
<span data-ttu-id="cbe36-351">您可以在一個管線中包含多個活動。</span><span class="sxs-lookup"><span data-stu-id="cbe36-351">You can have more than one activity in a pipeline.</span></span> <span data-ttu-id="cbe36-352">如果您在管線中有多個活動與 hello 輸出的活動不是另一個活動的輸入，hello 活動可能會以平行方式執行，hello 活動的輸入的資料配量是否準備。</span><span class="sxs-lookup"><span data-stu-id="cbe36-352">If you have multiple activities in a pipeline and hello output of an activity is not an input of another activity, hello activities may run in parallel if input data slices for hello activities are ready.</span></span>

<span data-ttu-id="cbe36-353">您可以藉由設定 hello 輸出資料集的一個活動 hello 的輸入資料集的 hello 其他活動鏈結 （執行一個活動執行另一個之後） 的兩個活動。</span><span class="sxs-lookup"><span data-stu-id="cbe36-353">You can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="cbe36-354">可以在 hello hello 活動相同的管線或在不同的管線中。</span><span class="sxs-lookup"><span data-stu-id="cbe36-354">hello activities can be in hello same pipeline or in different pipelines.</span></span> <span data-ttu-id="cbe36-355">hello 第一次一個成功完成時，才會執行 hello 第二個活動。</span><span class="sxs-lookup"><span data-stu-id="cbe36-355">hello second activity executes only when hello first one finishes successfully.</span></span>

<span data-ttu-id="cbe36-356">例如，請考慮下列管線有兩個活動的 hello:</span><span class="sxs-lookup"><span data-stu-id="cbe36-356">For example, consider hello following case where a pipeline has two activities:</span></span>

1. <span data-ttu-id="cbe36-357">需要外部輸入資料集 D1 並且會產生輸出資料集 D2 的活動 A1。</span><span class="sxs-lookup"><span data-stu-id="cbe36-357">Activity A1 that requires external input dataset D1, and produces output dataset D2.</span></span>
2. <span data-ttu-id="cbe36-358">需要來自資料集 D2 之輸入並且會產生輸出資料集 D3 的活動 A2。</span><span class="sxs-lookup"><span data-stu-id="cbe36-358">Activity A2 that requires input from dataset D2, and produces output dataset D3.</span></span>

<span data-ttu-id="cbe36-359">在此案例中，活動 A1 和 A2 會在 hello 相同管線。</span><span class="sxs-lookup"><span data-stu-id="cbe36-359">In this scenario, activities A1 and A2 are in hello same pipeline.</span></span> <span data-ttu-id="cbe36-360">A1 時執行 hello 外部資料可供使用且達到 hello 排程可用性頻率 hello 活動。</span><span class="sxs-lookup"><span data-stu-id="cbe36-360">hello activity A1 runs when hello external data is available and hello scheduled availability frequency is reached.</span></span> <span data-ttu-id="cbe36-361">hello 活動 A2 時執行 hello D2 從排程配量，就可以使用且 hello 頻率排程的可用性為止。</span><span class="sxs-lookup"><span data-stu-id="cbe36-361">hello activity A2 runs when hello scheduled slices from D2 become available and hello scheduled availability frequency is reached.</span></span> <span data-ttu-id="cbe36-362">如果沒有發生錯誤，其中一種集中 D2 hello 配量，A2 不會執行該配量直到它可用為止。</span><span class="sxs-lookup"><span data-stu-id="cbe36-362">If there is an error in one of hello slices in dataset D2, A2 does not run for that slice until it becomes available.</span></span>

<span data-ttu-id="cbe36-363">hello 相同管線會看起來像下列圖表中的 hello 與 hello 中這兩個活動的圖表檢視：</span><span class="sxs-lookup"><span data-stu-id="cbe36-363">hello Diagram view with both activities in hello same pipeline would look like hello following diagram:</span></span>

![鏈結中 hello 活動相同管線](./media/data-factory-scheduling-and-execution/chaining-one-pipeline.png)

<span data-ttu-id="cbe36-365">如先前所述，hello 活動可以是不同的管線。</span><span class="sxs-lookup"><span data-stu-id="cbe36-365">As mentioned earlier, hello activities could be in different pipelines.</span></span> <span data-ttu-id="cbe36-366">在這種情況下，hello 圖表檢視會看起來像下列圖表中的 hello:</span><span class="sxs-lookup"><span data-stu-id="cbe36-366">In such a scenario, hello diagram view would look like hello following diagram:</span></span>

![兩個管線中的鏈結活動](./media/data-factory-scheduling-and-execution/chaining-two-pipelines.png)

<span data-ttu-id="cbe36-368">請參閱 hello[循序複製](#copy-sequentially)hello 附錄的範例 > 一節。</span><span class="sxs-lookup"><span data-stu-id="cbe36-368">See hello [copy sequentially](#copy-sequentially) section in hello appendix for an example.</span></span>

## <a name="model-datasets-with-different-frequencies"></a><span data-ttu-id="cbe36-369">使用不同的頻率模型化資料集</span><span class="sxs-lookup"><span data-stu-id="cbe36-369">Model datasets with different frequencies</span></span>
<span data-ttu-id="cbe36-370">在 hello 範例中，輸入和輸出資料集和 hello 活動排程時段的 hello 頻率所 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="cbe36-370">In hello samples, hello frequencies for input and output datasets and hello activity schedule window were hello same.</span></span> <span data-ttu-id="cbe36-371">某些情況下需要 hello 能力 tooproduce 輸出在不同的一或多個輸入 hello 頻率的頻率。</span><span class="sxs-lookup"><span data-stu-id="cbe36-371">Some scenarios require hello ability tooproduce output at a frequency different than hello frequencies of one or more inputs.</span></span> <span data-ttu-id="cbe36-372">Data Factory 支援模型化這些案例。</span><span class="sxs-lookup"><span data-stu-id="cbe36-372">Data Factory supports modeling these scenarios.</span></span>

### <a name="sample-1-produce-a-daily-output-report-for-input-data-that-is-available-every-hour"></a><span data-ttu-id="cbe36-373">範例 1：對每小時可用的輸入資料產生每日輸出報告</span><span class="sxs-lookup"><span data-stu-id="cbe36-373">Sample 1: Produce a daily output report for input data that is available every hour</span></span>
<span data-ttu-id="cbe36-374">請設想 Azure Blob 儲存體中每小時會有來自感應器的輸入測量資料的案例。</span><span class="sxs-lookup"><span data-stu-id="cbe36-374">Consider a scenario in which you have input measurement data from sensors available every hour in Azure Blob storage.</span></span> <span data-ttu-id="cbe36-375">您想要與 hello 天 tooproduce 統計資料，例如平均值、 最大值和最小值的每日彙總報表[Data Factory hive 活動](data-factory-hive-activity.md)。</span><span class="sxs-lookup"><span data-stu-id="cbe36-375">You want tooproduce a daily aggregate report with statistics such as mean, maximum, and minimum for hello day with [Data Factory hive activity](data-factory-hive-activity.md).</span></span>

<span data-ttu-id="cbe36-376">以下是使用 Data Factory 模型化此案例的方式：</span><span class="sxs-lookup"><span data-stu-id="cbe36-376">Here is how you can model this scenario with Data Factory:</span></span>

<span data-ttu-id="cbe36-377">**輸入資料集**</span><span class="sxs-lookup"><span data-stu-id="cbe36-377">**Input dataset**</span></span>

<span data-ttu-id="cbe36-378">hello 每小時輸入 hello 指定一天的 hello 資料夾中會卸除檔案。</span><span class="sxs-lookup"><span data-stu-id="cbe36-378">hello hourly input files are dropped in hello folder for hello given day.</span></span> <span data-ttu-id="cbe36-379">輸入的可用性設定為 **小時** (頻率：小時、間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="cbe36-379">Availability for input is set at **Hour** (frequency: Hour, interval: 1).</span></span>

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
<span data-ttu-id="cbe36-380">**輸出資料集**</span><span class="sxs-lookup"><span data-stu-id="cbe36-380">**Output dataset**</span></span>

<span data-ttu-id="cbe36-381">一個輸出檔 hello 一天的資料夾中建立每一天。</span><span class="sxs-lookup"><span data-stu-id="cbe36-381">One output file is created every day in hello day's folder.</span></span> <span data-ttu-id="cbe36-382">輸出的可用性設定為 **日** (頻率：日、間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="cbe36-382">Availability of output is set at **Day** (frequency: Day and interval: 1).</span></span>

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

<span data-ttu-id="cbe36-383">**活動：管線中的 Hive 活動**</span><span class="sxs-lookup"><span data-stu-id="cbe36-383">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="cbe36-384">hello hive 指令碼會收到 hello 適當*DateTime*資訊做為參數使用 hello **WindowStart** hello 下列程式碼片段所示的變數。</span><span class="sxs-lookup"><span data-stu-id="cbe36-384">hello hive script receives hello appropriate *DateTime* information as parameters that use hello **WindowStart** variable as shown in hello following snippet.</span></span> <span data-ttu-id="cbe36-385">hello hive 指令碼會使用此變數 tooload hello 資料 hello 正確的資料夾從 hello 日，並執行 hello 彙總 toogenerate hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="cbe36-385">hello hive script uses this variable tooload hello data from hello correct folder for hello day and run hello aggregation toogenerate hello output.</span></span>

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

<span data-ttu-id="cbe36-386">hello 下列圖表顯示 hello 案例從資料相依性的觀點。</span><span class="sxs-lookup"><span data-stu-id="cbe36-386">hello following diagram shows hello scenario from a data-dependency point of view.</span></span>

![資料相依性](./media/data-factory-scheduling-and-execution/data-dependency.png)

<span data-ttu-id="cbe36-388">每一天的 hello 輸出配量取決於輸入資料集從 24 小時的配量。</span><span class="sxs-lookup"><span data-stu-id="cbe36-388">hello output slice for every day depends on 24 hourly slices from an input dataset.</span></span> <span data-ttu-id="cbe36-389">這些相依性，以找出自動 hello 落在 hello 的輸入的資料配量的資料處理站計算相同的時間週期 hello 產生輸出配量 toobe。</span><span class="sxs-lookup"><span data-stu-id="cbe36-389">Data Factory computes these dependencies automatically by figuring out hello input data slices that fall in hello same time period as hello output slice toobe produced.</span></span> <span data-ttu-id="cbe36-390">如果任何 hello 24 輸入配量無法使用，則 Data Factory 會等候 hello 輸入配量 toobe 之後，再啟動 hello 每日執行的活動。</span><span class="sxs-lookup"><span data-stu-id="cbe36-390">If any of hello 24 input slices is not available, Data Factory waits for hello input slice toobe ready before starting hello daily activity run.</span></span>

### <a name="sample-2-specify-dependency-with-expressions-and-data-factory-functions"></a><span data-ttu-id="cbe36-391">範例 2：使用運算式和 Data Factory 函數指定相依性</span><span class="sxs-lookup"><span data-stu-id="cbe36-391">Sample 2: Specify dependency with expressions and Data Factory functions</span></span>
<span data-ttu-id="cbe36-392">我們來看一下另一種案例。</span><span class="sxs-lookup"><span data-stu-id="cbe36-392">Let’s consider another scenario.</span></span> <span data-ttu-id="cbe36-393">假設您有處理兩個輸入資料集的 Hive 活動。</span><span class="sxs-lookup"><span data-stu-id="cbe36-393">Suppose you have a hive activity that processes two input datasets.</span></span> <span data-ttu-id="cbe36-394">其中一個每日有新資料，但是另一個會每週取得新資料。</span><span class="sxs-lookup"><span data-stu-id="cbe36-394">One of them has new data daily, but one of them gets new data every week.</span></span> <span data-ttu-id="cbe36-395">假設您想 toodo 聯結 hello 兩個輸入之間，每日產生的輸出。</span><span class="sxs-lookup"><span data-stu-id="cbe36-395">Suppose you wanted toodo a join across hello two inputs and produce an output every day.</span></span>

<span data-ttu-id="cbe36-396">hello 簡單的方法，在其中 Data Factory 自動找出 hello 右邊輸入分割 tooprocess 對齊 toohello 輸出資料配量的時間週期內無法運作。</span><span class="sxs-lookup"><span data-stu-id="cbe36-396">hello simple approach in which Data Factory automatically figures out hello right input slices tooprocess by aligning toohello output data slice’s time period does not work.</span></span>

<span data-ttu-id="cbe36-397">您必須指定執行每個活動，如 hello Data Factory 應該使用上週的資料配量的 hello 每週的輸入資料集。</span><span class="sxs-lookup"><span data-stu-id="cbe36-397">You must specify that for every activity run, hello Data Factory should use last week’s data slice for hello weekly input dataset.</span></span> <span data-ttu-id="cbe36-398">您使用 Azure Data Factory 函數中所示 hello 下列程式碼片段 tooimplement 這種行為。</span><span class="sxs-lookup"><span data-stu-id="cbe36-398">You use Azure Data Factory functions as shown in hello following snippet tooimplement this behavior.</span></span>

<span data-ttu-id="cbe36-399">**Input1：Azure Blob**</span><span class="sxs-lookup"><span data-stu-id="cbe36-399">**Input1: Azure blob**</span></span>

<span data-ttu-id="cbe36-400">hello 的第一個輸入 hello Azure blob 的每日更新。</span><span class="sxs-lookup"><span data-stu-id="cbe36-400">hello first input is hello Azure blob being updated daily.</span></span>

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

<span data-ttu-id="cbe36-401">**Input2：Azure Blob**</span><span class="sxs-lookup"><span data-stu-id="cbe36-401">**Input2: Azure blob**</span></span>

<span data-ttu-id="cbe36-402">Input2 為 hello Azure blob，每週更新。</span><span class="sxs-lookup"><span data-stu-id="cbe36-402">Input2 is hello Azure blob being updated weekly.</span></span>

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

<span data-ttu-id="cbe36-403">**輸出：Azure Blob**</span><span class="sxs-lookup"><span data-stu-id="cbe36-403">**Output: Azure blob**</span></span>

<span data-ttu-id="cbe36-404">一個輸出檔每天資料夾中建立 hello hello 一天。</span><span class="sxs-lookup"><span data-stu-id="cbe36-404">One output file is created every day in hello folder for hello day.</span></span> <span data-ttu-id="cbe36-405">輸出的可用性設定得**天**(頻率： Day、 interval: 1)。</span><span class="sxs-lookup"><span data-stu-id="cbe36-405">Availability of output is set too**day** (frequency: Day, interval: 1).</span></span>

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

<span data-ttu-id="cbe36-406">**活動：管線中的 Hive 活動**</span><span class="sxs-lookup"><span data-stu-id="cbe36-406">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="cbe36-407">hello hive 活動會採用 hello 兩個輸入，並產生輸出配量每一天。</span><span class="sxs-lookup"><span data-stu-id="cbe36-407">hello hive activity takes hello two inputs and produces an output slice every day.</span></span> <span data-ttu-id="cbe36-408">您可以指定每日輸出配量 toodepend 上的 hello 前一週每週輸入配量，如下所示。</span><span class="sxs-lookup"><span data-stu-id="cbe36-408">You can specify every day’s output slice toodepend on hello previous week’s input slice for weekly input as follows.</span></span>

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

<span data-ttu-id="cbe36-409">如需 Data Factory 所支援的函數與系統變數清單，請參閱 [Data Factory 函式與系統變數](data-factory-functions-variables.md) 。</span><span class="sxs-lookup"><span data-stu-id="cbe36-409">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of functions and system variables that Data Factory supports.</span></span>

## <a name="appendix"></a><span data-ttu-id="cbe36-410">附錄</span><span class="sxs-lookup"><span data-stu-id="cbe36-410">Appendix</span></span>

### <a name="example-copy-sequentially"></a><span data-ttu-id="cbe36-411">範例：循序複製</span><span class="sxs-lookup"><span data-stu-id="cbe36-411">Example: copy sequentially</span></span>
<span data-ttu-id="cbe36-412">它是可能 toorun 多項複製作業逐一循序/排序的方式。</span><span class="sxs-lookup"><span data-stu-id="cbe36-412">It is possible toorun multiple copy operations one after another in a sequential/ordered manner.</span></span> <span data-ttu-id="cbe36-413">例如，您可能有兩個複本活動與 hello 遵循管線 （CopyActivity1 和 CopyActivity2） 中的輸入的資料輸出資料集：</span><span class="sxs-lookup"><span data-stu-id="cbe36-413">For example, you might have two copy activities in a pipeline (CopyActivity1 and CopyActivity2) with hello following input data output datasets:</span></span>   

<span data-ttu-id="cbe36-414">CopyActivity1</span><span class="sxs-lookup"><span data-stu-id="cbe36-414">CopyActivity1</span></span>

<span data-ttu-id="cbe36-415">輸入：Dataset1。</span><span class="sxs-lookup"><span data-stu-id="cbe36-415">Input: Dataset.</span></span> <span data-ttu-id="cbe36-416">輸出：Dataset2。</span><span class="sxs-lookup"><span data-stu-id="cbe36-416">Output: Dataset2.</span></span>

<span data-ttu-id="cbe36-417">CopyActivity2</span><span class="sxs-lookup"><span data-stu-id="cbe36-417">CopyActivity2</span></span>

<span data-ttu-id="cbe36-418">輸入：Dataset2。</span><span class="sxs-lookup"><span data-stu-id="cbe36-418">Input: Dataset2.</span></span>  <span data-ttu-id="cbe36-419">輸出：Dataset3。</span><span class="sxs-lookup"><span data-stu-id="cbe36-419">Output: Dataset3.</span></span>

<span data-ttu-id="cbe36-420">只有 hello CopyActivity1 曾順利執行，且 Dataset2 為可用，就會執行 CopyActivity2。</span><span class="sxs-lookup"><span data-stu-id="cbe36-420">CopyActivity2 would run only if hello CopyActivity1 has run successfully and Dataset2 is available.</span></span>

<span data-ttu-id="cbe36-421">以下是 hello 範例管線 JSON:</span><span class="sxs-lookup"><span data-stu-id="cbe36-421">Here is hello sample pipeline JSON:</span></span>

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

<span data-ttu-id="cbe36-422">請注意在 hello 範例中，指定 hello 輸出資料集的 hello 第一個複製活動 (Dataset2) 是做為輸入 hello 第二個活動。</span><span class="sxs-lookup"><span data-stu-id="cbe36-422">Notice that in hello example, hello output dataset of hello first copy activity (Dataset2) is specified as input for hello second activity.</span></span> <span data-ttu-id="cbe36-423">因此，只有準備 hello 從 hello 第一個活動的輸出資料集時，才會執行 hello 第二個活動。</span><span class="sxs-lookup"><span data-stu-id="cbe36-423">Therefore, hello second activity runs only when hello output dataset from hello first activity is ready.</span></span>  

<span data-ttu-id="cbe36-424">在 hello 範例 CopyActivity2 可以有不同的輸入，例如 Dataset3，但您指定 Dataset2 為輸入的 tooCopyActivity2，因此直到完成 CopyActivity1 hello 活動不會執行。</span><span class="sxs-lookup"><span data-stu-id="cbe36-424">In hello example, CopyActivity2 can have a different input, such as Dataset3, but you specify Dataset2 as an input tooCopyActivity2, so hello activity does not run until CopyActivity1 finishes.</span></span> <span data-ttu-id="cbe36-425">例如：</span><span class="sxs-lookup"><span data-stu-id="cbe36-425">For example:</span></span>

<span data-ttu-id="cbe36-426">CopyActivity1</span><span class="sxs-lookup"><span data-stu-id="cbe36-426">CopyActivity1</span></span>

<span data-ttu-id="cbe36-427">輸入︰Dataset1。</span><span class="sxs-lookup"><span data-stu-id="cbe36-427">Input: Dataset1.</span></span> <span data-ttu-id="cbe36-428">輸出：Dataset2。</span><span class="sxs-lookup"><span data-stu-id="cbe36-428">Output: Dataset2.</span></span>

<span data-ttu-id="cbe36-429">CopyActivity2</span><span class="sxs-lookup"><span data-stu-id="cbe36-429">CopyActivity2</span></span>

<span data-ttu-id="cbe36-430">輸入︰Dataset3、Dataset2。</span><span class="sxs-lookup"><span data-stu-id="cbe36-430">Inputs: Dataset3, Dataset2.</span></span> <span data-ttu-id="cbe36-431">輸出︰Dataset4。</span><span class="sxs-lookup"><span data-stu-id="cbe36-431">Output: Dataset4.</span></span>

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

<span data-ttu-id="cbe36-432">請注意在 hello 範例中，指定兩個輸入資料集是 hello 第二個複製活動。</span><span class="sxs-lookup"><span data-stu-id="cbe36-432">Notice that in hello example, two input datasets are specified for hello second copy activity.</span></span> <span data-ttu-id="cbe36-433">當指定多個輸入時，只有 hello 第一個輸入資料集用來複製資料，但是其他資料集做為相依性。</span><span class="sxs-lookup"><span data-stu-id="cbe36-433">When multiple inputs are specified, only hello first input dataset is used for copying data, but other datasets are used as dependencies.</span></span> <span data-ttu-id="cbe36-434">CopyActivity2 會啟動才 hello 必須符合下列條件：</span><span class="sxs-lookup"><span data-stu-id="cbe36-434">CopyActivity2 would start only after hello following conditions are met:</span></span>

* <span data-ttu-id="cbe36-435">CopyActivity1 已順利完成且 Dataset2 可供使用。</span><span class="sxs-lookup"><span data-stu-id="cbe36-435">CopyActivity1 has successfully completed and Dataset2 is available.</span></span> <span data-ttu-id="cbe36-436">複製資料 tooDataset4 時，不會使用此資料集。</span><span class="sxs-lookup"><span data-stu-id="cbe36-436">This dataset is not used when copying data tooDataset4.</span></span> <span data-ttu-id="cbe36-437">它只會用來做為 CopyActivity2 的排程相依性。</span><span class="sxs-lookup"><span data-stu-id="cbe36-437">It only acts as a scheduling dependency for CopyActivity2.</span></span>   
* <span data-ttu-id="cbe36-438">Dataset3 可供使用。</span><span class="sxs-lookup"><span data-stu-id="cbe36-438">Dataset3 is available.</span></span> <span data-ttu-id="cbe36-439">此資料集代表 hello 資料複製的 toohello 目的地。</span><span class="sxs-lookup"><span data-stu-id="cbe36-439">This dataset represents hello data that is copied toohello destination.</span></span> 
