---
title: "使用 Data Factory 進行排程和執行 | Microsoft Docs"
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
ms.openlocfilehash: e6fd92cde91ae5f171c855c07fa8974a19703b41
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="data-factory-scheduling-and-execution"></a><span data-ttu-id="67292-103">Data Factory 排程和執行</span><span class="sxs-lookup"><span data-stu-id="67292-103">Data Factory scheduling and execution</span></span>
<span data-ttu-id="67292-104">本文說明 Azure Data Factory 應用程式模型的排程和執行層面。</span><span class="sxs-lookup"><span data-stu-id="67292-104">This article explains the scheduling and execution aspects of the Azure Data Factory application model.</span></span> <span data-ttu-id="67292-105">本文假設您已了解 Data Factory 應用程式模型的基本概念，包括活動、管線、連結的服務和資料集。</span><span class="sxs-lookup"><span data-stu-id="67292-105">This article assumes that you understand basics of Data Factory application model concepts, including activity, pipelines, linked services, and datasets.</span></span> <span data-ttu-id="67292-106">請看下列文章，了解 Azure Data Factory 的基本概念：</span><span class="sxs-lookup"><span data-stu-id="67292-106">For basic concepts of Azure Data Factory, see the following articles:</span></span>

* [<span data-ttu-id="67292-107">Data Factory 服務簡介</span><span class="sxs-lookup"><span data-stu-id="67292-107">Introduction to Data Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="67292-108">管線</span><span class="sxs-lookup"><span data-stu-id="67292-108">Pipelines</span></span>](data-factory-create-pipelines.md)
* [<span data-ttu-id="67292-109">資料集</span><span class="sxs-lookup"><span data-stu-id="67292-109">Datasets</span></span>](data-factory-create-datasets.md) 

## <a name="start-and-end-times-of-pipeline"></a><span data-ttu-id="67292-110">管線的開始和結束時間</span><span class="sxs-lookup"><span data-stu-id="67292-110">Start and end times of pipeline</span></span>
<span data-ttu-id="67292-111">管線僅在其「開始」時間與「結束」時間之間有作用。</span><span class="sxs-lookup"><span data-stu-id="67292-111">A pipeline is active only between its **start** time and **end** time.</span></span> <span data-ttu-id="67292-112">在開始時間之前或結束時間之後就不會執行。</span><span class="sxs-lookup"><span data-stu-id="67292-112">It is not executed before the start time or after the end time.</span></span> <span data-ttu-id="67292-113">如果管線已暫停，不論其開始和結束時間為何，都不會執行。</span><span class="sxs-lookup"><span data-stu-id="67292-113">If the pipeline is paused, it is not executed irrespective of its start and end time.</span></span> <span data-ttu-id="67292-114">若要執行管線，則不該將它暫停。</span><span class="sxs-lookup"><span data-stu-id="67292-114">For a pipeline to run, it should not be paused.</span></span> <span data-ttu-id="67292-115">您可以在管線定義中找到這些設定 (start、end、paused)：</span><span class="sxs-lookup"><span data-stu-id="67292-115">You find these settings (start, end, paused) in the pipeline definition:</span></span> 

```json
"start": "2017-04-01T08:00:00Z",
"end": "2017-04-01T11:00:00Z"
"isPaused": false
```

<span data-ttu-id="67292-116">如需有關這些屬性的詳細資訊，請參閱[建立管線](data-factory-create-pipelines.md)一文。</span><span class="sxs-lookup"><span data-stu-id="67292-116">For more information these properties, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> 


## <a name="specify-schedule-for-an-activity"></a><span data-ttu-id="67292-117">為活動指定排程</span><span class="sxs-lookup"><span data-stu-id="67292-117">Specify schedule for an activity</span></span>
<span data-ttu-id="67292-118">執行的不是管線。</span><span class="sxs-lookup"><span data-stu-id="67292-118">It is not the pipeline that is executed.</span></span> <span data-ttu-id="67292-119">在管線的整體內容中，執行的是管線中的活動。</span><span class="sxs-lookup"><span data-stu-id="67292-119">It is the activities in the pipeline that are executed in the overall context of the pipeline.</span></span> <span data-ttu-id="67292-120">您可以使用活動 JSON 的 **scheduler** 區段，來為活動指定週期性排程。</span><span class="sxs-lookup"><span data-stu-id="67292-120">You can specify a recurring schedule for an activity by using the **scheduler** section of activity JSON.</span></span> <span data-ttu-id="67292-121">例如，您可以排定讓活動每小時執行一次，如下：</span><span class="sxs-lookup"><span data-stu-id="67292-121">For example, you can schedule an activity to run hourly as follows:</span></span>  

```json
"scheduler": {
    "frequency": "Hour",
    "interval": 1
},
```

<span data-ttu-id="67292-122">如下圖所示，為活動指定排程會在管線的開始和結束時間內，建立一系列輪轉時段。</span><span class="sxs-lookup"><span data-stu-id="67292-122">As shown in the following diagram, specifying a schedule for an activity creates a series of tumbling windows with in the pipeline start and end times.</span></span> <span data-ttu-id="67292-123">輪轉時段是一系列大小固定、非重疊的連續時間間隔。</span><span class="sxs-lookup"><span data-stu-id="67292-123">Tumbling windows are a series of fixed-size non-overlapping, contiguous time intervals.</span></span> <span data-ttu-id="67292-124">活動的這些邏輯輪轉時段稱為「活動時段」。</span><span class="sxs-lookup"><span data-stu-id="67292-124">These logical tumbling windows for an activity are called **activity windows**.</span></span>

![活動排程器範例](media/data-factory-scheduling-and-execution/scheduler-example.png)

<span data-ttu-id="67292-126">活動的 **scheduler** 屬性是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="67292-126">The **scheduler** property for an activity is optional.</span></span> <span data-ttu-id="67292-127">如果您指定此屬性，它就必須符合您在活動輸出資料集的定義中指定的頻率。</span><span class="sxs-lookup"><span data-stu-id="67292-127">If you do specify this property, it must match the cadence you specify in the definition of output dataset for the activity.</span></span> <span data-ttu-id="67292-128">目前，驅動排程的是輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="67292-128">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="67292-129">因此，即使活動不會產生任何輸出，您也必須指定輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="67292-129">Therefore, you must create an output dataset even if the activity does not produce any output.</span></span> 

## <a name="specify-schedule-for-a-dataset"></a><span data-ttu-id="67292-130">為資料集指定排程</span><span class="sxs-lookup"><span data-stu-id="67292-130">Specify schedule for a dataset</span></span>
<span data-ttu-id="67292-131">Data Factory 管線中的一個活動可以接受零個或多個輸入「資料集」，並且會產生一個或多個輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="67292-131">An activity in a Data Factory pipeline can take zero or more input **datasets** and produce one or more output datasets.</span></span> <span data-ttu-id="67292-132">針對活動，您可以在資料集定義中使用 **availability** 區段，來指定提供輸入資料或產生輸出資料的頻率。</span><span class="sxs-lookup"><span data-stu-id="67292-132">For an activity, you can specify the cadence at which the input data is available or the output data is produced by using the **availability** section in the dataset definitions.</span></span> 

<span data-ttu-id="67292-133">**availability** 區段中的 **frequency** 會指定時間單位。</span><span class="sxs-lookup"><span data-stu-id="67292-133">**Frequency** in the **availability** section specifies the time unit.</span></span> <span data-ttu-id="67292-134">允許的 frequency 值為：Minute、Hour、Day、Week 及 Month。</span><span class="sxs-lookup"><span data-stu-id="67292-134">The allowed values for frequency are: Minute, Hour, Day, Week, and Month.</span></span> <span data-ttu-id="67292-135">availability 區段中的 **interval** 屬性會指定 frequency 的倍數。</span><span class="sxs-lookup"><span data-stu-id="67292-135">The **interval** property in the availability section specifies a multiplier for frequency.</span></span> <span data-ttu-id="67292-136">例如：如果將輸出資料集的 frequency 設定為 Day，並將 interval 是設定為 1，就會每天產生輸出資料。</span><span class="sxs-lookup"><span data-stu-id="67292-136">For example: if the frequency is set to Day and interval is set to 1 for an output dataset, the output data is produced daily.</span></span> <span data-ttu-id="67292-137">如果您將 frequency 指定為 minute，建議您將 interval 設定為不小於 15。</span><span class="sxs-lookup"><span data-stu-id="67292-137">If you specify the frequency as minute, we recommend that you set the interval to no less than 15.</span></span> 

<span data-ttu-id="67292-138">在下列範例中，會每小時提供輸入資料，並每小時產生輸出資料 (`"frequency": "Hour", "interval": 1`)。</span><span class="sxs-lookup"><span data-stu-id="67292-138">In the following example, the input data is available hourly and the output data is produced hourly (`"frequency": "Hour", "interval": 1`).</span></span> 

<span data-ttu-id="67292-139">**輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="67292-139">**Input dataset:**</span></span> 

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


<span data-ttu-id="67292-140">**輸出資料集**</span><span class="sxs-lookup"><span data-stu-id="67292-140">**Output dataset**</span></span>

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

<span data-ttu-id="67292-141">目前，**是由輸出資料集驅動排程**。</span><span class="sxs-lookup"><span data-stu-id="67292-141">Currently, **output dataset drives the schedule**.</span></span> <span data-ttu-id="67292-142">換句話說，會使用為輸出資料集指定的排程在執行階段執行活動。</span><span class="sxs-lookup"><span data-stu-id="67292-142">In other words, the schedule specified for the output dataset is used to run an activity at runtime.</span></span> <span data-ttu-id="67292-143">因此，即使活動不會產生任何輸出，您也必須指定輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="67292-143">Therefore, you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="67292-144">如果活動沒有任何輸入，您可以略過建立輸入資料集。</span><span class="sxs-lookup"><span data-stu-id="67292-144">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> 

<span data-ttu-id="67292-145">在下列管線定義中，會使用 **scheduler** 屬性來為活動指定排程。</span><span class="sxs-lookup"><span data-stu-id="67292-145">In the following pipeline definition, the **scheduler** property is used to specify schedule for the activity.</span></span> <span data-ttu-id="67292-146">這是選用屬性。</span><span class="sxs-lookup"><span data-stu-id="67292-146">This property is optional.</span></span> <span data-ttu-id="67292-147">目前，活動的排程必須與為輸出資料集指定的排程相符。</span><span class="sxs-lookup"><span data-stu-id="67292-147">Currently, the schedule for the activity must match the schedule specified for the output dataset.</span></span>
 
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

<span data-ttu-id="67292-148">在此範例中，活動會在管線的開始與結束時間之間每小時執行一次。</span><span class="sxs-lookup"><span data-stu-id="67292-148">In this example, the activity runs hourly between the start and end times of the pipeline.</span></span> <span data-ttu-id="67292-149">針對三小時的時段 (上午 8 點 - 上午 9 點、上午 9 點 - 上午 10 點，以及上午 10 點 - 上午 11 點) 會每小時產生一次輸出資料。</span><span class="sxs-lookup"><span data-stu-id="67292-149">The output data is produced hourly for three-hour windows (8 AM - 9 AM, 9 AM - 10 AM, and 10 AM - 11 AM).</span></span> 

<span data-ttu-id="67292-150">活動執行所取用或產生的每個資料單位稱為「資料配量」。</span><span class="sxs-lookup"><span data-stu-id="67292-150">Each unit of data consumed or produced by an activity run is called a **data slice**.</span></span> <span data-ttu-id="67292-151">下表顯示具有一個輸入資料集和一個輸出資料集的活動範例：</span><span class="sxs-lookup"><span data-stu-id="67292-151">The following diagram shows an example of an activity with one input dataset and one output dataset:</span></span> 

![可用性排程器](./media/data-factory-scheduling-and-execution/availability-scheduler.png)

<span data-ttu-id="67292-153">上圖顯示輸入和輸出資料集的每小時資料配量。</span><span class="sxs-lookup"><span data-stu-id="67292-153">The diagram shows the hourly data slices for the input and output dataset.</span></span> <span data-ttu-id="67292-154">圖中顯示 3 個已經可供處理的輸入配量。</span><span class="sxs-lookup"><span data-stu-id="67292-154">The diagram shows three input slices that are ready for processing.</span></span> <span data-ttu-id="67292-155">10-11 AM 活動正在進行中，會產生 10-11 AM 輸出配量。</span><span class="sxs-lookup"><span data-stu-id="67292-155">The 10-11 AM activity is in progress, producing the 10-11 AM output slice.</span></span> 

<span data-ttu-id="67292-156">您可以使用 [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) 和 [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables) 變數，來存取與資料集 JSON 中目前配量關聯的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="67292-156">You can access the time interval associated with the current slice in the dataset JSON by using variables: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) and [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables).</span></span> <span data-ttu-id="67292-157">同樣地，您可以使用 WindowStart 和 WindowEnd，來存取與活動時段關聯的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="67292-157">Similarly, you can access the time interval associated with an activity window by using the WindowStart and WindowEnd.</span></span> <span data-ttu-id="67292-158">活動的排程必須與活動之輸出資料集的排程相符。</span><span class="sxs-lookup"><span data-stu-id="67292-158">The schedule of an activity must match the schedule of the output dataset for the activity.</span></span> <span data-ttu-id="67292-159">因此，SliceStart 和 SliceEnd 值會分別與 WindowStart 和 WindowEnd 值相同。</span><span class="sxs-lookup"><span data-stu-id="67292-159">Therefore, the SliceStart and SliceEnd values are the same as WindowStart and WindowEnd values respectively.</span></span> <span data-ttu-id="67292-160">如需有關這些變數的詳細資訊，請參閱 [Data Factory 函式與系統變數](data-factory-functions-variables.md#data-factory-system-variables)文章。</span><span class="sxs-lookup"><span data-stu-id="67292-160">For more information on these variables, see [Data Factory functions and system variables](data-factory-functions-variables.md#data-factory-system-variables) articles.</span></span>  

<span data-ttu-id="67292-161">您可以在活動 JSON 中針對不同用途使用這些變數。</span><span class="sxs-lookup"><span data-stu-id="67292-161">You can use these variables for different purposes in your activity JSON.</span></span> <span data-ttu-id="67292-162">例如，您可以使用它們從代表時間序列資料 (例如：上午 8 點到上午 9 點) 的輸入和輸出資料集選取資料。</span><span class="sxs-lookup"><span data-stu-id="67292-162">For example, you can use them to select data from input and output datasets representing time series data (for example: 8 AM to 9 AM).</span></span> <span data-ttu-id="67292-163">此範例也使用 **WindowStart** 和 **WindowEnd** 來選取活動執行的相關資料，並將它複製到具有適當 **folderPath** 的 Blob。</span><span class="sxs-lookup"><span data-stu-id="67292-163">This example also uses **WindowStart** and **WindowEnd** to select relevant data for an activity run and copy it to a blob with the appropriate **folderPath**.</span></span> <span data-ttu-id="67292-164">**folderPath** 會參數化為讓每小時具有個別的資料夾。</span><span class="sxs-lookup"><span data-stu-id="67292-164">The **folderPath** is parameterized to have a separate folder for every hour.</span></span>  

<span data-ttu-id="67292-165">在上述範例中，為輸入和輸出資料集指定的排程是相同的 (每小時)。</span><span class="sxs-lookup"><span data-stu-id="67292-165">In the preceding example, the schedule specified for input and output datasets is the same (hourly).</span></span> <span data-ttu-id="67292-166">如果活動的輸入資料集會以不同的頻率提供 (假設是每隔 15 分鐘)，產生此輸出資料集的活動仍然會一小時執行一次，因為驅動活動排程的是輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="67292-166">If the input dataset for the activity is available at a different frequency, say every 15 minutes, the activity that produces this output dataset still runs once an hour as the output dataset is what drives the activity schedule.</span></span> <span data-ttu-id="67292-167">如需詳細資訊，請參閱[使用不同的頻率模型化資料集](#model-datasets-with-different-frequencies)。</span><span class="sxs-lookup"><span data-stu-id="67292-167">For more information, see [Model datasets with different frequencies](#model-datasets-with-different-frequencies).</span></span>

## <a name="dataset-availability-and-policies"></a><span data-ttu-id="67292-168">資料集可用性和原則</span><span class="sxs-lookup"><span data-stu-id="67292-168">Dataset availability and policies</span></span>
<span data-ttu-id="67292-169">您已了解資料集定義之 availability 區段中 frequency 和 interval 屬性的使用方式。</span><span class="sxs-lookup"><span data-stu-id="67292-169">You have seen the usage of frequency and interval properties in the availability section of dataset definition.</span></span> <span data-ttu-id="67292-170">還有一些影響活動的排程和執行的其他屬性。</span><span class="sxs-lookup"><span data-stu-id="67292-170">There are a few other properties that affect the scheduling and execution of an activity.</span></span> 

### <a name="dataset-availability"></a><span data-ttu-id="67292-171">資料集可用性</span><span class="sxs-lookup"><span data-stu-id="67292-171">Dataset availability</span></span> 
<span data-ttu-id="67292-172">下表描述您在 **availability** 區段中可使用的屬性：</span><span class="sxs-lookup"><span data-stu-id="67292-172">The following table describes properties you can use in the **availability** section:</span></span>

| <span data-ttu-id="67292-173">屬性</span><span class="sxs-lookup"><span data-stu-id="67292-173">Property</span></span> | <span data-ttu-id="67292-174">說明</span><span class="sxs-lookup"><span data-stu-id="67292-174">Description</span></span> | <span data-ttu-id="67292-175">必要</span><span class="sxs-lookup"><span data-stu-id="67292-175">Required</span></span> | <span data-ttu-id="67292-176">預設值</span><span class="sxs-lookup"><span data-stu-id="67292-176">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="67292-177">frequency</span><span class="sxs-lookup"><span data-stu-id="67292-177">frequency</span></span> |<span data-ttu-id="67292-178">指定資料集配量生產的時間單位。</span><span class="sxs-lookup"><span data-stu-id="67292-178">Specifies the time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="67292-179"><b>支援的頻率</b>：Minute、Hour、Day、Week、Month</span><span class="sxs-lookup"><span data-stu-id="67292-179"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="67292-180">是</span><span class="sxs-lookup"><span data-stu-id="67292-180">Yes</span></span> |<span data-ttu-id="67292-181">NA</span><span class="sxs-lookup"><span data-stu-id="67292-181">NA</span></span> |
| <span data-ttu-id="67292-182">interval</span><span class="sxs-lookup"><span data-stu-id="67292-182">interval</span></span> |<span data-ttu-id="67292-183">指定頻率的倍數</span><span class="sxs-lookup"><span data-stu-id="67292-183">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="67292-184">「頻率 x 間隔」會決定產生配量的頻率。</span><span class="sxs-lookup"><span data-stu-id="67292-184">”Frequency x interval” determines how often the slice is produced.</span></span><br/><br/><span data-ttu-id="67292-185">如果您需要將資料集以每小時為單位來切割，請將 <b>Frequency</b> 設定為 <b>Hour</b>，將 <b>interval</b> 設定為 <b>1</b>。</span><span class="sxs-lookup"><span data-stu-id="67292-185">If you need the dataset to be sliced on an hourly basis, you set <b>Frequency</b> to <b>Hour</b>, and <b>interval</b> to <b>1</b>.</span></span><br/><br/><span data-ttu-id="67292-186"><b>注意</b>：如果您將 Frequency 指定為 Minute，建議您將 interval 設定為不小於 15</span><span class="sxs-lookup"><span data-stu-id="67292-186"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set the interval to no less than 15</span></span> |<span data-ttu-id="67292-187">是</span><span class="sxs-lookup"><span data-stu-id="67292-187">Yes</span></span> |<span data-ttu-id="67292-188">NA</span><span class="sxs-lookup"><span data-stu-id="67292-188">NA</span></span> |
| <span data-ttu-id="67292-189">style</span><span class="sxs-lookup"><span data-stu-id="67292-189">style</span></span> |<span data-ttu-id="67292-190">指定是否應該在間隔開始/結束時產生配量。</span><span class="sxs-lookup"><span data-stu-id="67292-190">Specifies whether the slice should be produced at the start/end of the interval.</span></span><ul><li><span data-ttu-id="67292-191">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="67292-191">StartOfInterval</span></span></li><li><span data-ttu-id="67292-192">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="67292-192">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="67292-193">如果 Frequency 設為 Month，style 設為 EndOfInterval，則會在當月最後一天產生配量。</span><span class="sxs-lookup"><span data-stu-id="67292-193">If Frequency is set to Month and style is set to EndOfInterval, the slice is produced on the last day of month.</span></span> <span data-ttu-id="67292-194">如果 style 設為 StartOfInterval，則會在每月的第一天產生配量。</span><span class="sxs-lookup"><span data-stu-id="67292-194">If the style is set to StartOfInterval, the slice is produced on the first day of month.</span></span><br/><br/><span data-ttu-id="67292-195">如果 Frequency 設為 Day，style 設為 EndOfInterval，則會在當天最後一個小時產生配量。</span><span class="sxs-lookup"><span data-stu-id="67292-195">If Frequency is set to Day and style is set to EndOfInterval, the slice is produced in the last hour of the day.</span></span><br/><br/><span data-ttu-id="67292-196">如果 Frequency 設為 Hour，style 設為 EndOfInterval，則會在每小時結束時產生配量。</span><span class="sxs-lookup"><span data-stu-id="67292-196">If Frequency is set to Hour and style is set to EndOfInterval, the slice is produced at the end of the hour.</span></span> <span data-ttu-id="67292-197">例如，若為下午 1 – 2 點期間的配量，此配量會在下午 2 點產生。</span><span class="sxs-lookup"><span data-stu-id="67292-197">For example, for a slice for 1 PM – 2 PM period, the slice is produced at 2 PM.</span></span> |<span data-ttu-id="67292-198">否</span><span class="sxs-lookup"><span data-stu-id="67292-198">No</span></span> |<span data-ttu-id="67292-199">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="67292-199">EndOfInterval</span></span> |
| <span data-ttu-id="67292-200">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="67292-200">anchorDateTime</span></span> |<span data-ttu-id="67292-201">定義排程器用來計算資料集配量界限的時間絕對位置。</span><span class="sxs-lookup"><span data-stu-id="67292-201">Defines the absolute position in time used by scheduler to compute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="67292-202"><b>注意</b>：如果 AnchorDateTime 有比頻率更細微的日期部分，則系統會忽略那些更細微的部分。</span><span class="sxs-lookup"><span data-stu-id="67292-202"><b>Note</b>: If the AnchorDateTime has date parts that are more granular than the frequency then the more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="67292-203">例如，如果 <b>interval</b> 為 <b>hourly</b> (frequency: hour 且 interval: 1) 而且 <b>AnchorDateTime</b> 包含<b>分鐘和秒鐘</b>，則會忽略 AnchorDateTime 的<b>分鐘和秒鐘</b>部分。</span><span class="sxs-lookup"><span data-stu-id="67292-203">For example, if the <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and the <b>AnchorDateTime</b> contains <b>minutes and seconds</b>, then the <b>minutes and seconds</b> parts of the AnchorDateTime are ignored.</span></span> |<span data-ttu-id="67292-204">否</span><span class="sxs-lookup"><span data-stu-id="67292-204">No</span></span> |<span data-ttu-id="67292-205">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="67292-205">01/01/0001</span></span> |
| <span data-ttu-id="67292-206">Offset</span><span class="sxs-lookup"><span data-stu-id="67292-206">offset</span></span> |<span data-ttu-id="67292-207">所有資料集配量的開始和結束移位所依據的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="67292-207">Timespan by which the start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="67292-208"><b>注意</b>︰如果同時指定 anchorDateTime 和 offset，結果會是合併的位移。</span><span class="sxs-lookup"><span data-stu-id="67292-208"><b>Note</b>: If both anchorDateTime and offset are specified, the result is the combined shift.</span></span> |<span data-ttu-id="67292-209">否</span><span class="sxs-lookup"><span data-stu-id="67292-209">No</span></span> |<span data-ttu-id="67292-210">NA</span><span class="sxs-lookup"><span data-stu-id="67292-210">NA</span></span> |

### <a name="offset-example"></a><span data-ttu-id="67292-211">位移範例</span><span class="sxs-lookup"><span data-stu-id="67292-211">offset example</span></span>
<span data-ttu-id="67292-212">根據預設，每日 (`"frequency": "Day", "interval": 1`) 配量的開始時間是 UTC 時間上午 12 點 (午夜)。</span><span class="sxs-lookup"><span data-stu-id="67292-212">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM UTC time (midnight).</span></span> <span data-ttu-id="67292-213">如果您希望將開始時間改為 UTC 時間上午 6 點，請依照下列程式碼片段所示設定位移：</span><span class="sxs-lookup"><span data-stu-id="67292-213">If you want the start time to be 6 AM UTC time instead, set the offset as shown in the following snippet:</span></span> 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a><span data-ttu-id="67292-214">anchorDateTime 範例</span><span class="sxs-lookup"><span data-stu-id="67292-214">anchorDateTime example</span></span>
<span data-ttu-id="67292-215">在下列範例中，會每隔 23 小時產生一次資料集。</span><span class="sxs-lookup"><span data-stu-id="67292-215">In the following example, the dataset is produced once every 23 hours.</span></span> <span data-ttu-id="67292-216">第一個配量會在 anchorDateTime 所指定的時間開始，這是設定成 `2017-04-19T08:00:00` (UTC 時間)。</span><span class="sxs-lookup"><span data-stu-id="67292-216">The first slice starts at the time specified by the anchorDateTime, which is set to `2017-04-19T08:00:00` (UTC time).</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a><span data-ttu-id="67292-217">位移/樣式範例</span><span class="sxs-lookup"><span data-stu-id="67292-217">offset/style Example</span></span>
<span data-ttu-id="67292-218">下列資料集是每月資料集，會在每月 3 號的上午 8:00 (`3.08:00:00`) 產生：</span><span class="sxs-lookup"><span data-stu-id="67292-218">The following dataset is a monthly dataset and is produced on 3rd of every month at 8:00 AM (`3.08:00:00`):</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

### <a name="dataset-policy"></a><span data-ttu-id="67292-219">資料集原則</span><span class="sxs-lookup"><span data-stu-id="67292-219">Dataset policy</span></span>
<span data-ttu-id="67292-220">資料集可以具有定義的驗證原則，指定配量執行所產生的資料在供取用之前如何驗證。</span><span class="sxs-lookup"><span data-stu-id="67292-220">A dataset can have a validation policy defined that specifies how the data generated by a slice execution can be validated before it is ready for consumption.</span></span> <span data-ttu-id="67292-221">在這種情況下，於配量完成執行後，輸出配量狀態就會變更為**等候**，子狀態為**驗證**。</span><span class="sxs-lookup"><span data-stu-id="67292-221">In such cases, after the slice has finished execution, the output slice status is changed to **Waiting** with a substatus of **Validation**.</span></span> <span data-ttu-id="67292-222">配量通過驗證之後，配量狀態會變更為 **就緒**。</span><span class="sxs-lookup"><span data-stu-id="67292-222">After the slices are validated, the slice status changes to **Ready**.</span></span> <span data-ttu-id="67292-223">如果已產生資料配量但是未通過驗證，將不會處理相依於此配量的下游配量活動執行。</span><span class="sxs-lookup"><span data-stu-id="67292-223">If a data slice has been produced but did not pass the validation, activity runs for downstream slices that depend on this slice are not processed.</span></span> <span data-ttu-id="67292-224">[監視和管理管線](data-factory-monitor-manage-pipelines.md) 涵蓋 Data Factory 中資料配量的各種狀態。</span><span class="sxs-lookup"><span data-stu-id="67292-224">[Monitor and manage pipelines](data-factory-monitor-manage-pipelines.md) covers the various states of data slices in Data Factory.</span></span>

<span data-ttu-id="67292-225">資料集中的 **policy** 區段定義資料集配量必須符合的準則或條件。</span><span class="sxs-lookup"><span data-stu-id="67292-225">The **policy** section in dataset definition defines the criteria or the condition that the dataset slices must fulfill.</span></span> <span data-ttu-id="67292-226">下表說明您可以在 **policy** 區段中使用的屬性：</span><span class="sxs-lookup"><span data-stu-id="67292-226">The following table describes properties you can use in the **policy** section:</span></span>

| <span data-ttu-id="67292-227">原則名稱</span><span class="sxs-lookup"><span data-stu-id="67292-227">Policy Name</span></span> | <span data-ttu-id="67292-228">說明</span><span class="sxs-lookup"><span data-stu-id="67292-228">Description</span></span> | <span data-ttu-id="67292-229">適用於</span><span class="sxs-lookup"><span data-stu-id="67292-229">Applied To</span></span> | <span data-ttu-id="67292-230">必要</span><span class="sxs-lookup"><span data-stu-id="67292-230">Required</span></span> | <span data-ttu-id="67292-231">預設值</span><span class="sxs-lookup"><span data-stu-id="67292-231">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="67292-232">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="67292-232">minimumSizeMB</span></span> | <span data-ttu-id="67292-233">驗證 **Azure Blob** 中的資料是否符合最小的大小需求 (以 MB 為單位)。</span><span class="sxs-lookup"><span data-stu-id="67292-233">Validates that the data in an **Azure blob** meets the minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="67292-234">Azure Blob</span><span class="sxs-lookup"><span data-stu-id="67292-234">Azure Blob</span></span> |<span data-ttu-id="67292-235">否</span><span class="sxs-lookup"><span data-stu-id="67292-235">No</span></span> |<span data-ttu-id="67292-236">NA</span><span class="sxs-lookup"><span data-stu-id="67292-236">NA</span></span> |
| <span data-ttu-id="67292-237">minimumRows</span><span class="sxs-lookup"><span data-stu-id="67292-237">minimumRows</span></span> | <span data-ttu-id="67292-238">驗證 **Azure SQL Database** 或 **Azure 資料表**中的資料是否包含最小的資料列數。</span><span class="sxs-lookup"><span data-stu-id="67292-238">Validates that the data in an **Azure SQL database** or an **Azure table** contains the minimum number of rows.</span></span> |<ul><li><span data-ttu-id="67292-239">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="67292-239">Azure SQL Database</span></span></li><li><span data-ttu-id="67292-240">Azure 資料表</span><span class="sxs-lookup"><span data-stu-id="67292-240">Azure Table</span></span></li></ul> |<span data-ttu-id="67292-241">否</span><span class="sxs-lookup"><span data-stu-id="67292-241">No</span></span> |<span data-ttu-id="67292-242">NA</span><span class="sxs-lookup"><span data-stu-id="67292-242">NA</span></span> |

#### <a name="examples"></a><span data-ttu-id="67292-243">範例</span><span class="sxs-lookup"><span data-stu-id="67292-243">Examples</span></span>
<span data-ttu-id="67292-244">**minimumSizeMB：**</span><span class="sxs-lookup"><span data-stu-id="67292-244">**minimumSizeMB:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="67292-245">**minimumRows**</span><span class="sxs-lookup"><span data-stu-id="67292-245">**minimumRows**</span></span>

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

<span data-ttu-id="67292-246">如需有關這些屬性及範例的詳細資訊，請參閱[建立資料集](data-factory-create-datasets.md)一文。</span><span class="sxs-lookup"><span data-stu-id="67292-246">For more information about these properties and examples, see [Create datasets](data-factory-create-datasets.md) article.</span></span> 

## <a name="activity-policies"></a><span data-ttu-id="67292-247">活動原則</span><span class="sxs-lookup"><span data-stu-id="67292-247">Activity policies</span></span>
<span data-ttu-id="67292-248">原則會影響活動的執行階段行為，特別是在處理資料表配量的時候。</span><span class="sxs-lookup"><span data-stu-id="67292-248">Policies affect the run-time behavior of an activity, specifically when the slice of a table is processed.</span></span> <span data-ttu-id="67292-249">下表提供詳細資料。</span><span class="sxs-lookup"><span data-stu-id="67292-249">The following table provides the details.</span></span>

| <span data-ttu-id="67292-250">屬性</span><span class="sxs-lookup"><span data-stu-id="67292-250">Property</span></span> | <span data-ttu-id="67292-251">允許的值</span><span class="sxs-lookup"><span data-stu-id="67292-251">Permitted values</span></span> | <span data-ttu-id="67292-252">預設值</span><span class="sxs-lookup"><span data-stu-id="67292-252">Default Value</span></span> | <span data-ttu-id="67292-253">說明</span><span class="sxs-lookup"><span data-stu-id="67292-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="67292-254">並行</span><span class="sxs-lookup"><span data-stu-id="67292-254">concurrency</span></span> |<span data-ttu-id="67292-255">整數 </span><span class="sxs-lookup"><span data-stu-id="67292-255">Integer</span></span> <br/><br/><span data-ttu-id="67292-256">最大值：10</span><span class="sxs-lookup"><span data-stu-id="67292-256">Max value: 10</span></span> |<span data-ttu-id="67292-257">1</span><span class="sxs-lookup"><span data-stu-id="67292-257">1</span></span> |<span data-ttu-id="67292-258">活動的並行執行數目。</span><span class="sxs-lookup"><span data-stu-id="67292-258">Number of concurrent executions of the activity.</span></span><br/><br/><span data-ttu-id="67292-259">它可決定不同配量上可以發生的平行活動執行數目。</span><span class="sxs-lookup"><span data-stu-id="67292-259">It determines the number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="67292-260">例如，如果活動需要處理大量可用的資料，具有較大的並行值會加快資料處理。</span><span class="sxs-lookup"><span data-stu-id="67292-260">For example, if an activity needs to go through a large set of available data, having a larger concurrency value speeds up the data processing.</span></span> |
| <span data-ttu-id="67292-261">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="67292-261">executionPriorityOrder</span></span> |<span data-ttu-id="67292-262">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="67292-262">NewestFirst</span></span><br/><br/><span data-ttu-id="67292-263">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="67292-263">OldestFirst</span></span> |<span data-ttu-id="67292-264">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="67292-264">OldestFirst</span></span> |<span data-ttu-id="67292-265">決定正在處理之資料配量的順序。</span><span class="sxs-lookup"><span data-stu-id="67292-265">Determines the ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="67292-266">例如，如果您有 2 個配量 (一個發生在下午 4 點，另一個發生在下午 5 點)，而兩者都暫停執行。</span><span class="sxs-lookup"><span data-stu-id="67292-266">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="67292-267">如果您將 executionPriorityOrder 設為 NewestFirst，則會先處理下午 5 點的配量。</span><span class="sxs-lookup"><span data-stu-id="67292-267">If you set the executionPriorityOrder to be NewestFirst, the slice at 5 PM is processed first.</span></span> <span data-ttu-id="67292-268">同樣地，如果您將 executionPriorityOrder 設為 OldestFIrst，則會處理下午 4 點的配量。</span><span class="sxs-lookup"><span data-stu-id="67292-268">Similarly if you set the executionPriorityORder to be OldestFIrst, then the slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="67292-269">retry</span><span class="sxs-lookup"><span data-stu-id="67292-269">retry</span></span> |<span data-ttu-id="67292-270">整數 </span><span class="sxs-lookup"><span data-stu-id="67292-270">Integer</span></span><br/><br/><span data-ttu-id="67292-271">最大值可以是 10</span><span class="sxs-lookup"><span data-stu-id="67292-271">Max value can be 10</span></span> |<span data-ttu-id="67292-272">0</span><span class="sxs-lookup"><span data-stu-id="67292-272">0</span></span> |<span data-ttu-id="67292-273">在配量的資料處理標示為 [失敗] 前的重試次數。</span><span class="sxs-lookup"><span data-stu-id="67292-273">Number of retries before the data processing for the slice is marked as Failure.</span></span> <span data-ttu-id="67292-274">資料配量的活動執行會一直重試，直到指定的重試計數為止。</span><span class="sxs-lookup"><span data-stu-id="67292-274">Activity execution for a data slice is retried up to the specified retry count.</span></span> <span data-ttu-id="67292-275">在失敗後會儘速完成重試。</span><span class="sxs-lookup"><span data-stu-id="67292-275">The retry is done as soon as possible after the failure.</span></span> |
| <span data-ttu-id="67292-276">timeout</span><span class="sxs-lookup"><span data-stu-id="67292-276">timeout</span></span> |<span data-ttu-id="67292-277">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="67292-277">TimeSpan</span></span> |<span data-ttu-id="67292-278">00:00:00</span><span class="sxs-lookup"><span data-stu-id="67292-278">00:00:00</span></span> |<span data-ttu-id="67292-279">活動的逾時。</span><span class="sxs-lookup"><span data-stu-id="67292-279">Timeout for the activity.</span></span> <span data-ttu-id="67292-280">範例︰00:10:00 (意指逾時 10 分鐘)</span><span class="sxs-lookup"><span data-stu-id="67292-280">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="67292-281">如果您未指定值 (或值為 0)，代表無限逾時。</span><span class="sxs-lookup"><span data-stu-id="67292-281">If a value is not specified or is 0, the timeout is infinite.</span></span><br/><br/><span data-ttu-id="67292-282">如果配量的資料處理時間超過逾時值，該活動會遭到取消，且系統會嘗試重試處理。</span><span class="sxs-lookup"><span data-stu-id="67292-282">If the data processing time on a slice exceeds the timeout value, it is canceled, and the system attempts to retry the processing.</span></span> <span data-ttu-id="67292-283">重試次數取決於 retry 屬性。</span><span class="sxs-lookup"><span data-stu-id="67292-283">The number of retries depends on the retry property.</span></span> <span data-ttu-id="67292-284">若發生逾時，狀態會設為 TimedOut。</span><span class="sxs-lookup"><span data-stu-id="67292-284">When timeout occurs, the status is set to TimedOut.</span></span> |
| <span data-ttu-id="67292-285">delay</span><span class="sxs-lookup"><span data-stu-id="67292-285">delay</span></span> |<span data-ttu-id="67292-286">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="67292-286">TimeSpan</span></span> |<span data-ttu-id="67292-287">00:00:00</span><span class="sxs-lookup"><span data-stu-id="67292-287">00:00:00</span></span> |<span data-ttu-id="67292-288">指定配量之資料處理開始之前的延遲。</span><span class="sxs-lookup"><span data-stu-id="67292-288">Specify the delay before data processing of the slice starts.</span></span><br/><br/><span data-ttu-id="67292-289">資料配量的活動執行會在 Delay 超出預期執行時間後開始。</span><span class="sxs-lookup"><span data-stu-id="67292-289">The execution of activity for a data slice is started after the Delay is past the expected execution time.</span></span><br/><br/><span data-ttu-id="67292-290">範例︰00:10:00 (意指延遲 10 分鐘)</span><span class="sxs-lookup"><span data-stu-id="67292-290">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="67292-291">longRetry</span><span class="sxs-lookup"><span data-stu-id="67292-291">longRetry</span></span> |<span data-ttu-id="67292-292">整數 </span><span class="sxs-lookup"><span data-stu-id="67292-292">Integer</span></span><br/><br/><span data-ttu-id="67292-293">最大值：10</span><span class="sxs-lookup"><span data-stu-id="67292-293">Max value: 10</span></span> |<span data-ttu-id="67292-294">1</span><span class="sxs-lookup"><span data-stu-id="67292-294">1</span></span> |<span data-ttu-id="67292-295">配量執行失敗之前的長時間重試嘗試次數。</span><span class="sxs-lookup"><span data-stu-id="67292-295">The number of long retry attempts before the slice execution is failed.</span></span><br/><br/><span data-ttu-id="67292-296">多個 longRetry 嘗試之間以 longRetryInterval 隔開。</span><span class="sxs-lookup"><span data-stu-id="67292-296">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="67292-297">所以如果您需要指定重試嘗試之間的時間，請使用 longRetry。</span><span class="sxs-lookup"><span data-stu-id="67292-297">So if you need to specify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="67292-298">如果您指定 Retry 和 longRetry 兩者，每個 longRetry 嘗試都包含 Retry 嘗試，且最大嘗試次數是 Retry * longRetry。</span><span class="sxs-lookup"><span data-stu-id="67292-298">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and the max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="67292-299">例如，如果活動原則的設定如下︰</span><span class="sxs-lookup"><span data-stu-id="67292-299">For example, if we have the following settings in the activity policy:</span></span><br/><span data-ttu-id="67292-300">Retry：3</span><span class="sxs-lookup"><span data-stu-id="67292-300">Retry: 3</span></span><br/><span data-ttu-id="67292-301">longRetry：2</span><span class="sxs-lookup"><span data-stu-id="67292-301">longRetry: 2</span></span><br/><span data-ttu-id="67292-302">longRetryInterval：01:00:00</span><span class="sxs-lookup"><span data-stu-id="67292-302">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="67292-303">假設只有一個要執行的配量 (狀態是 Waiting)，且活動執行每次都失敗。</span><span class="sxs-lookup"><span data-stu-id="67292-303">Assume there is only one slice to execute (status is Waiting) and the activity execution fails every time.</span></span> <span data-ttu-id="67292-304">一開始會有 3 次連續執行嘗試。</span><span class="sxs-lookup"><span data-stu-id="67292-304">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="67292-305">在每次嘗試之後，配量狀態會是 Retry。</span><span class="sxs-lookup"><span data-stu-id="67292-305">After each attempt, the slice status would be Retry.</span></span> <span data-ttu-id="67292-306">在前 3 次嘗試結束之後，配量狀態會是 LongRetry。</span><span class="sxs-lookup"><span data-stu-id="67292-306">After first 3 attempts are over, the slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="67292-307">一個小時 (也就是 longRetryInteval 的值) 之後，會有另一組 3 次連續執行嘗試。</span><span class="sxs-lookup"><span data-stu-id="67292-307">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="67292-308">在那之後，配量狀態會是 Failed，不會再嘗試重試。</span><span class="sxs-lookup"><span data-stu-id="67292-308">After that, the slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="67292-309">因此全部已進行 6 次嘗試。</span><span class="sxs-lookup"><span data-stu-id="67292-309">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="67292-310">如果任何執行成功，配量狀態會是 Ready 且不會再嘗試重試。</span><span class="sxs-lookup"><span data-stu-id="67292-310">If any execution succeeds, the slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="67292-311">longRetry 可能用於下列情況：相依資料達到不具決定性的次數，或進行資料處理的整體環境很脆弱。</span><span class="sxs-lookup"><span data-stu-id="67292-311">longRetry may be used in situations where dependent data arrives at non-deterministic times or the overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="67292-312">在這類情況下逐一進行重試並沒有幫助，而在一段時間後進行重試則會導致所要的結果。</span><span class="sxs-lookup"><span data-stu-id="67292-312">In such cases, doing retries one after another may not help and doing so after an interval of time results in the desired output.</span></span><br/><br/><span data-ttu-id="67292-313">提醒：請勿設定較大的 longRetry 或 longRetryInterval 值。</span><span class="sxs-lookup"><span data-stu-id="67292-313">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="67292-314">較大的值通常表示其他系統問題。</span><span class="sxs-lookup"><span data-stu-id="67292-314">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="67292-315">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="67292-315">longRetryInterval</span></span> |<span data-ttu-id="67292-316">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="67292-316">TimeSpan</span></span> |<span data-ttu-id="67292-317">00:00:00</span><span class="sxs-lookup"><span data-stu-id="67292-317">00:00:00</span></span> |<span data-ttu-id="67292-318">長時間重試嘗試之間的延遲</span><span class="sxs-lookup"><span data-stu-id="67292-318">The delay between long retry attempts</span></span> |

<span data-ttu-id="67292-319">如需詳細資訊，請參閱[管線](data-factory-create-pipelines.md)一文。</span><span class="sxs-lookup"><span data-stu-id="67292-319">For more information, see [Pipelines](data-factory-create-pipelines.md) article.</span></span> 

## <a name="parallel-processing-of-data-slices"></a><span data-ttu-id="67292-320">資料配量的平行處理</span><span class="sxs-lookup"><span data-stu-id="67292-320">Parallel processing of data slices</span></span>
<span data-ttu-id="67292-321">您可以將管線的開始日期設定為過去的日期。</span><span class="sxs-lookup"><span data-stu-id="67292-321">You can set the start date for the pipeline in the past.</span></span> <span data-ttu-id="67292-322">當您這麼做時，Data Factory 會自動計算 (回補) 過去的所有資料配量，並開始處理它們。</span><span class="sxs-lookup"><span data-stu-id="67292-322">When you do so, Data Factory automatically calculates (back fills) all data slices in the past and begins processing them.</span></span> <span data-ttu-id="67292-323">例如：如果您建立一個開始日期為 2017-04-01 的管線，而目前的日期是 2017-04-10。</span><span class="sxs-lookup"><span data-stu-id="67292-323">For example: if you create a pipeline with start date 2017-04-01 and the current date is 2017-04-10.</span></span> <span data-ttu-id="67292-324">當輸出資料集的頻率是每天時，Data Factory 會立即開始處理從 2017-04-01 到 2017-04-09 的所有配量，因為開始日期是過去的日期。</span><span class="sxs-lookup"><span data-stu-id="67292-324">If the cadence of the output dataset is daily, then Data Factory starts processing all the slices from 2017-04-01 to 2017-04-09 immediately because the start date is in the past.</span></span> <span data-ttu-id="67292-325">從 2017-04-10 起的配量尚未處理，因為 availability 區段中 style 屬性的值預設為 EndOfInterval。</span><span class="sxs-lookup"><span data-stu-id="67292-325">The slice from 2017-04-10 is not processed yet because the value of style property in the availability section is EndOfInterval by default.</span></span> <span data-ttu-id="67292-326">最舊的配量會最先處理，因為 executionPriorityOrder 的預設值為 OldestFirst。</span><span class="sxs-lookup"><span data-stu-id="67292-326">The oldest slice is processed first as the default value of executionPriorityOrder is OldestFirst.</span></span> <span data-ttu-id="67292-327">如需 style 屬性的相關描述，請參閱[資料集可用性](#dataset-availability)一節。</span><span class="sxs-lookup"><span data-stu-id="67292-327">For a description of the style property, see [dataset availability](#dataset-availability) section.</span></span> <span data-ttu-id="67292-328">如需 executionPriorityOrder 區段的相關描述，請參閱[活動原則](#activity-policies)一節。</span><span class="sxs-lookup"><span data-stu-id="67292-328">For a description of the executionPriorityOrder section, see the [activity policies](#activity-policies) section.</span></span> 

<span data-ttu-id="67292-329">您可以透過設定活動 JSON 之 **policy** 區段中的 **concurrency** 屬性，設定以平行方式處理回補的資料配量。</span><span class="sxs-lookup"><span data-stu-id="67292-329">You can configure back-filled data slices to be processed in parallel by setting the **concurrency** property in the **policy** section of the activity JSON.</span></span> <span data-ttu-id="67292-330">此屬性可決定不同配量上可以發生的平行活動執行數目。</span><span class="sxs-lookup"><span data-stu-id="67292-330">This property determines the number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="67292-331">concurrency 屬性的預設值是 1。</span><span class="sxs-lookup"><span data-stu-id="67292-331">The default value for the concurrency property is 1.</span></span> <span data-ttu-id="67292-332">因此，預設會一次處理一個配量。</span><span class="sxs-lookup"><span data-stu-id="67292-332">Therefore, one slice is processed at a time by default.</span></span> <span data-ttu-id="67292-333">最大值為 10。</span><span class="sxs-lookup"><span data-stu-id="67292-333">The maximum value is 10.</span></span> <span data-ttu-id="67292-334">當管線需要處理一組大量的可用資料時，concurrency 的值越大，資料處理的速度就越快。</span><span class="sxs-lookup"><span data-stu-id="67292-334">When a pipeline needs to go through a large set of available data, having a larger concurrency value speeds up the data processing.</span></span> 

## <a name="rerun-a-failed-data-slice"></a><span data-ttu-id="67292-335">重新執行失敗的資料配量</span><span class="sxs-lookup"><span data-stu-id="67292-335">Rerun a failed data slice</span></span>
<span data-ttu-id="67292-336">處理資料配量時，如果發生錯誤，您可以使用 Azure 入口網站刀鋒視窗或「監視與管理」應用程式來找出配量處理失敗的原因。</span><span class="sxs-lookup"><span data-stu-id="67292-336">When an error occurs while processing a data slice, you can find out why the processing of a slice failed by using Azure portal blades or Monitor and Manage App.</span></span> <span data-ttu-id="67292-337">如需詳細資訊，請參閱[使用 Azure 入口網站刀鋒視窗監視和管理管線](data-factory-monitor-manage-pipelines.md)或[監視和管理應用程式](data-factory-monitor-manage-app.md)。</span><span class="sxs-lookup"><span data-stu-id="67292-337">See [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md) for details.</span></span>

<span data-ttu-id="67292-338">請思考一下會顯示兩個活動的下列範例。</span><span class="sxs-lookup"><span data-stu-id="67292-338">Consider the following example, which shows two activities.</span></span> <span data-ttu-id="67292-339">Activity1 和 Activity 2。</span><span class="sxs-lookup"><span data-stu-id="67292-339">Activity1 and Activity 2.</span></span> <span data-ttu-id="67292-340">Activity1 會取用 Dataset1 配量並產生 Dataset2 配量，而此配量會由 Activity2 取用來作為輸入以產生 Final Dataset (最終資料集)。</span><span class="sxs-lookup"><span data-stu-id="67292-340">Activity1 consumes a slice of Dataset1 and produces a slice of Dataset2, which is consumed as an input by Activity2 to produce a slice of the Final Dataset.</span></span>

![失敗的配量](./media/data-factory-scheduling-and-execution/failed-slice.png)

<span data-ttu-id="67292-342">圖中顯示 3 個最近的配量當中有失敗，針對 Dataset2 產生 9-10 AM 配量。</span><span class="sxs-lookup"><span data-stu-id="67292-342">The diagram shows that out of three recent slices, there was a failure producing the 9-10 AM slice for Dataset2.</span></span> <span data-ttu-id="67292-343">Data Factory 會自動追蹤時間序列資料集的相依性。</span><span class="sxs-lookup"><span data-stu-id="67292-343">Data Factory automatically tracks dependency for the time series dataset.</span></span> <span data-ttu-id="67292-344">因此，它不會開始 9-10 AM 下游配量的活動執行。</span><span class="sxs-lookup"><span data-stu-id="67292-344">As a result, it does not start the activity run for the 9-10 AM downstream slice.</span></span>

<span data-ttu-id="67292-345">Data Factory 監視和管理工具可讓您深入診斷記錄以了解失敗的配量，輕鬆地找出問題的根本原因並加以修正。</span><span class="sxs-lookup"><span data-stu-id="67292-345">Data Factory monitoring and management tools allow you to drill into the diagnostic logs for the failed slice to easily find the root cause for the issue and fix it.</span></span> <span data-ttu-id="67292-346">在您修正問題之後，即可輕易地開始活動執行以產生失敗的配量。</span><span class="sxs-lookup"><span data-stu-id="67292-346">After you have fixed the issue, you can easily start the activity run to produce the failed slice.</span></span> <span data-ttu-id="67292-347">如需有關如何重新執行和了解資料配量的狀態轉換的詳細資訊，請參閱[使用 Azure 入口網站刀鋒視窗監視和管理管線](data-factory-monitor-manage-pipelines.md)或[監視和管理應用程式](data-factory-monitor-manage-app.md)。</span><span class="sxs-lookup"><span data-stu-id="67292-347">For more information on how to rerun and understand state transitions for data slices, see [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span>

<span data-ttu-id="67292-348">在您重新執行 **Dataset2**的 9-10 AM 配量之後，Data Factory 會開始執行最終資料集上 9-10 AM 相依的配量。</span><span class="sxs-lookup"><span data-stu-id="67292-348">After you rerun the 9-10 AM slice for **Dataset2**, Data Factory starts the run for the 9-10 AM dependent slice on the final dataset.</span></span>

![重新執行失敗的配量](./media/data-factory-scheduling-and-execution/rerun-failed-slice.png)

## <a name="multiple-activities-in-a-pipeline"></a><span data-ttu-id="67292-350">管線中的多個活動</span><span class="sxs-lookup"><span data-stu-id="67292-350">Multiple activities in a pipeline</span></span>
<span data-ttu-id="67292-351">您可以在一個管線中包含多個活動。</span><span class="sxs-lookup"><span data-stu-id="67292-351">You can have more than one activity in a pipeline.</span></span> <span data-ttu-id="67292-352">如果您的管線中有多個活動，而且活動的輸出不是另一個活動的輸入，則當活動的輸入資料配量已備妥時，活動可能會平行執行。</span><span class="sxs-lookup"><span data-stu-id="67292-352">If you have multiple activities in a pipeline and the output of an activity is not an input of another activity, the activities may run in parallel if input data slices for the activities are ready.</span></span>

<span data-ttu-id="67292-353">您可以將一個活動的輸出資料集設為另一個活動的輸入資料集，藉此鏈結兩個活動 (讓一個活動接著另一個活動執行)。</span><span class="sxs-lookup"><span data-stu-id="67292-353">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="67292-354">活動可以在相同的管線中或在不同的管線中。</span><span class="sxs-lookup"><span data-stu-id="67292-354">The activities can be in the same pipeline or in different pipelines.</span></span> <span data-ttu-id="67292-355">只有當第一個活動執行成功完成時，第二個活動才會執行。</span><span class="sxs-lookup"><span data-stu-id="67292-355">The second activity executes only when the first one finishes successfully.</span></span>

<span data-ttu-id="67292-356">例如，請思考一下以下情況，其中管線包含兩個活動：</span><span class="sxs-lookup"><span data-stu-id="67292-356">For example, consider the following case where a pipeline has two activities:</span></span>

1. <span data-ttu-id="67292-357">需要外部輸入資料集 D1 並且會產生輸出資料集 D2 的活動 A1。</span><span class="sxs-lookup"><span data-stu-id="67292-357">Activity A1 that requires external input dataset D1, and produces output dataset D2.</span></span>
2. <span data-ttu-id="67292-358">需要來自資料集 D2 之輸入並且會產生輸出資料集 D3 的活動 A2。</span><span class="sxs-lookup"><span data-stu-id="67292-358">Activity A2 that requires input from dataset D2, and produces output dataset D3.</span></span>

<span data-ttu-id="67292-359">在此案例中，活動 A1 和 A2 是在相同的管線中。</span><span class="sxs-lookup"><span data-stu-id="67292-359">In this scenario, activities A1 and A2 are in the same pipeline.</span></span> <span data-ttu-id="67292-360">活動 A1 會在有外部資料可供使用且達到排定的可用性頻率時執行。</span><span class="sxs-lookup"><span data-stu-id="67292-360">The activity A1 runs when the external data is available and the scheduled availability frequency is reached.</span></span> <span data-ttu-id="67292-361">活動 A2 會在來自 D2 的排定分割可供使用且達到排定的可用性頻率時執行。</span><span class="sxs-lookup"><span data-stu-id="67292-361">The activity A2 runs when the scheduled slices from D2 become available and the scheduled availability frequency is reached.</span></span> <span data-ttu-id="67292-362">如果資料集 D2 中的其中一個分割發生錯誤，則不會針對該分割執行 A2，直到該分割可供使用為止。</span><span class="sxs-lookup"><span data-stu-id="67292-362">If there is an error in one of the slices in dataset D2, A2 does not run for that slice until it becomes available.</span></span>

<span data-ttu-id="67292-363">兩個活動同時在相同管線中的 [圖表] 檢視看起來如下圖：</span><span class="sxs-lookup"><span data-stu-id="67292-363">The Diagram view with both activities in the same pipeline would look like the following diagram:</span></span>

![相同管線中的鏈結活動](./media/data-factory-scheduling-and-execution/chaining-one-pipeline.png)

<span data-ttu-id="67292-365">如先前所述，活動可以在不同的管線中。</span><span class="sxs-lookup"><span data-stu-id="67292-365">As mentioned earlier, the activities could be in different pipelines.</span></span> <span data-ttu-id="67292-366">在這類案例中，圖表檢視看起來會如下圖：</span><span class="sxs-lookup"><span data-stu-id="67292-366">In such a scenario, the diagram view would look like the following diagram:</span></span>

![兩個管線中的鏈結活動](./media/data-factory-scheduling-and-execution/chaining-two-pipelines.png)

<span data-ttu-id="67292-368">如需範例，請參閱附錄中的[循序複製](#copy-sequentially)一節。</span><span class="sxs-lookup"><span data-stu-id="67292-368">See the [copy sequentially](#copy-sequentially) section in the appendix for an example.</span></span>

## <a name="model-datasets-with-different-frequencies"></a><span data-ttu-id="67292-369">使用不同的頻率模型化資料集</span><span class="sxs-lookup"><span data-stu-id="67292-369">Model datasets with different frequencies</span></span>
<span data-ttu-id="67292-370">在範例中，輸入和輸出資料集和活動排程時段的頻率是相同的。</span><span class="sxs-lookup"><span data-stu-id="67292-370">In the samples, the frequencies for input and output datasets and the activity schedule window were the same.</span></span> <span data-ttu-id="67292-371">某些案例需要能夠以不同於一或多個輸入的頻率產生輸出。</span><span class="sxs-lookup"><span data-stu-id="67292-371">Some scenarios require the ability to produce output at a frequency different than the frequencies of one or more inputs.</span></span> <span data-ttu-id="67292-372">Data Factory 支援模型化這些案例。</span><span class="sxs-lookup"><span data-stu-id="67292-372">Data Factory supports modeling these scenarios.</span></span>

### <a name="sample-1-produce-a-daily-output-report-for-input-data-that-is-available-every-hour"></a><span data-ttu-id="67292-373">範例 1：對每小時可用的輸入資料產生每日輸出報告</span><span class="sxs-lookup"><span data-stu-id="67292-373">Sample 1: Produce a daily output report for input data that is available every hour</span></span>
<span data-ttu-id="67292-374">請設想 Azure Blob 儲存體中每小時會有來自感應器的輸入測量資料的案例。</span><span class="sxs-lookup"><span data-stu-id="67292-374">Consider a scenario in which you have input measurement data from sensors available every hour in Azure Blob storage.</span></span> <span data-ttu-id="67292-375">您想要為具有 [Data Factory Hive 活動](data-factory-hive-activity.md)的日子，產生具有統計資料 (例如平均值、最大值及最小值) 的每日彙總報告。</span><span class="sxs-lookup"><span data-stu-id="67292-375">You want to produce a daily aggregate report with statistics such as mean, maximum, and minimum for the day with [Data Factory hive activity](data-factory-hive-activity.md).</span></span>

<span data-ttu-id="67292-376">以下是使用 Data Factory 模型化此案例的方式：</span><span class="sxs-lookup"><span data-stu-id="67292-376">Here is how you can model this scenario with Data Factory:</span></span>

<span data-ttu-id="67292-377">**輸入資料集**</span><span class="sxs-lookup"><span data-stu-id="67292-377">**Input dataset**</span></span>

<span data-ttu-id="67292-378">每小時輸入檔案會針對指定日期在資料夾中卸除。</span><span class="sxs-lookup"><span data-stu-id="67292-378">The hourly input files are dropped in the folder for the given day.</span></span> <span data-ttu-id="67292-379">輸入的可用性設定為 **小時** (頻率：小時、間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="67292-379">Availability for input is set at **Hour** (frequency: Hour, interval: 1).</span></span>

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
<span data-ttu-id="67292-380">**輸出資料集**</span><span class="sxs-lookup"><span data-stu-id="67292-380">**Output dataset**</span></span>

<span data-ttu-id="67292-381">每天會在當天的資料夾中建立一個輸出檔。</span><span class="sxs-lookup"><span data-stu-id="67292-381">One output file is created every day in the day's folder.</span></span> <span data-ttu-id="67292-382">輸出的可用性設定為 **日** (頻率：日、間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="67292-382">Availability of output is set at **Day** (frequency: Day and interval: 1).</span></span>

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

<span data-ttu-id="67292-383">**活動：管線中的 Hive 活動**</span><span class="sxs-lookup"><span data-stu-id="67292-383">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="67292-384">Hive 指令碼會收到適當的「日期時間」  資訊，做為使用 **WindowStart** 變數的參數，如下列程式碼片段所示。</span><span class="sxs-lookup"><span data-stu-id="67292-384">The hive script receives the appropriate *DateTime* information as parameters that use the **WindowStart** variable as shown in the following snippet.</span></span> <span data-ttu-id="67292-385">Hive 指令碼會使用此變數將資料從正確的資料夾載入，並執行彙總來產生輸出。</span><span class="sxs-lookup"><span data-stu-id="67292-385">The hive script uses this variable to load the data from the correct folder for the day and run the aggregation to generate the output.</span></span>

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

<span data-ttu-id="67292-386">下圖顯示從資料相依性觀點來看的案例。</span><span class="sxs-lookup"><span data-stu-id="67292-386">The following diagram shows the scenario from a data-dependency point of view.</span></span>

![資料相依性](./media/data-factory-scheduling-and-execution/data-dependency.png)

<span data-ttu-id="67292-388">每一天的輸出配量取決於輸入資料集之 24 小時每小時的配量。</span><span class="sxs-lookup"><span data-stu-id="67292-388">The output slice for every day depends on 24 hourly slices from an input dataset.</span></span> <span data-ttu-id="67292-389">Data Factory 會自動計算這些相依性，方法是釐清落在與要產生之輸出配量相同時間期間的輸入資料配量。</span><span class="sxs-lookup"><span data-stu-id="67292-389">Data Factory computes these dependencies automatically by figuring out the input data slices that fall in the same time period as the output slice to be produced.</span></span> <span data-ttu-id="67292-390">如果這 24 個輸入配量中有任何一個無法使用，Data Factory 會先等待輸入配量就緒，再開始每日活動執行。</span><span class="sxs-lookup"><span data-stu-id="67292-390">If any of the 24 input slices is not available, Data Factory waits for the input slice to be ready before starting the daily activity run.</span></span>

### <a name="sample-2-specify-dependency-with-expressions-and-data-factory-functions"></a><span data-ttu-id="67292-391">範例 2：使用運算式和 Data Factory 函數指定相依性</span><span class="sxs-lookup"><span data-stu-id="67292-391">Sample 2: Specify dependency with expressions and Data Factory functions</span></span>
<span data-ttu-id="67292-392">我們來看一下另一種案例。</span><span class="sxs-lookup"><span data-stu-id="67292-392">Let’s consider another scenario.</span></span> <span data-ttu-id="67292-393">假設您有處理兩個輸入資料集的 Hive 活動。</span><span class="sxs-lookup"><span data-stu-id="67292-393">Suppose you have a hive activity that processes two input datasets.</span></span> <span data-ttu-id="67292-394">其中一個每日有新資料，但是另一個會每週取得新資料。</span><span class="sxs-lookup"><span data-stu-id="67292-394">One of them has new data daily, but one of them gets new data every week.</span></span> <span data-ttu-id="67292-395">假設您想要跨兩個輸入進行聯結作業，並且每日產生輸出。</span><span class="sxs-lookup"><span data-stu-id="67292-395">Suppose you wanted to do a join across the two inputs and produce an output every day.</span></span>

<span data-ttu-id="67292-396">Data Factory 會藉由對齊輸出資料配量的時間期間來自動找出要處理的正確輸入配量的簡單方法不會奏效。</span><span class="sxs-lookup"><span data-stu-id="67292-396">The simple approach in which Data Factory automatically figures out the right input slices to process by aligning to the output data slice’s time period does not work.</span></span>

<span data-ttu-id="67292-397">您必須指定對於每個活動執行，Data Factory 應該針對每週輸入資料集使用上一週的資料配量。</span><span class="sxs-lookup"><span data-stu-id="67292-397">You must specify that for every activity run, the Data Factory should use last week’s data slice for the weekly input dataset.</span></span> <span data-ttu-id="67292-398">使用 Azure Data Factory 的函式來實作此行為，如下列程式碼片段所示。</span><span class="sxs-lookup"><span data-stu-id="67292-398">You use Azure Data Factory functions as shown in the following snippet to implement this behavior.</span></span>

<span data-ttu-id="67292-399">**Input1：Azure Blob**</span><span class="sxs-lookup"><span data-stu-id="67292-399">**Input1: Azure blob**</span></span>

<span data-ttu-id="67292-400">第一個輸入是將會每日更新的 Azure Blob。</span><span class="sxs-lookup"><span data-stu-id="67292-400">The first input is the Azure blob being updated daily.</span></span>

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

<span data-ttu-id="67292-401">**Input2：Azure Blob**</span><span class="sxs-lookup"><span data-stu-id="67292-401">**Input2: Azure blob**</span></span>

<span data-ttu-id="67292-402">Input2 是將會每週更新的 Azure Blob。</span><span class="sxs-lookup"><span data-stu-id="67292-402">Input2 is the Azure blob being updated weekly.</span></span>

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

<span data-ttu-id="67292-403">**輸出：Azure Blob**</span><span class="sxs-lookup"><span data-stu-id="67292-403">**Output: Azure blob**</span></span>

<span data-ttu-id="67292-404">每天會在資料夾中建立一個當天的輸出檔。</span><span class="sxs-lookup"><span data-stu-id="67292-404">One output file is created every day in the folder for the day.</span></span> <span data-ttu-id="67292-405">輸出的可用性設定為 **日** (頻率：日、間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="67292-405">Availability of output is set to **day** (frequency: Day, interval: 1).</span></span>

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

<span data-ttu-id="67292-406">**活動：管線中的 Hive 活動**</span><span class="sxs-lookup"><span data-stu-id="67292-406">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="67292-407">Hive 活動接受 2 個輸入，並且每日產生輸出配量。</span><span class="sxs-lookup"><span data-stu-id="67292-407">The hive activity takes the two inputs and produces an output slice every day.</span></span> <span data-ttu-id="67292-408">您可以針對每週輸入指定每日的輸出配量是根據上一週的輸入配量，如下所示。</span><span class="sxs-lookup"><span data-stu-id="67292-408">You can specify every day’s output slice to depend on the previous week’s input slice for weekly input as follows.</span></span>

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

<span data-ttu-id="67292-409">如需 Data Factory 所支援的函數與系統變數清單，請參閱 [Data Factory 函式與系統變數](data-factory-functions-variables.md) 。</span><span class="sxs-lookup"><span data-stu-id="67292-409">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of functions and system variables that Data Factory supports.</span></span>

## <a name="appendix"></a><span data-ttu-id="67292-410">附錄</span><span class="sxs-lookup"><span data-stu-id="67292-410">Appendix</span></span>

### <a name="example-copy-sequentially"></a><span data-ttu-id="67292-411">範例：循序複製</span><span class="sxs-lookup"><span data-stu-id="67292-411">Example: copy sequentially</span></span>
<span data-ttu-id="67292-412">您可以利用循序/排序的方式，逐一執行多個複製作業。</span><span class="sxs-lookup"><span data-stu-id="67292-412">It is possible to run multiple copy operations one after another in a sequential/ordered manner.</span></span> <span data-ttu-id="67292-413">例如，您在管線中可能有兩個具有下列輸入資料輸出資料集的複製活動 (CopyActivity1 和 CopyActivity2)：</span><span class="sxs-lookup"><span data-stu-id="67292-413">For example, you might have two copy activities in a pipeline (CopyActivity1 and CopyActivity2) with the following input data output datasets:</span></span>   

<span data-ttu-id="67292-414">CopyActivity1</span><span class="sxs-lookup"><span data-stu-id="67292-414">CopyActivity1</span></span>

<span data-ttu-id="67292-415">輸入：Dataset1。</span><span class="sxs-lookup"><span data-stu-id="67292-415">Input: Dataset.</span></span> <span data-ttu-id="67292-416">輸出：Dataset2。</span><span class="sxs-lookup"><span data-stu-id="67292-416">Output: Dataset2.</span></span>

<span data-ttu-id="67292-417">CopyActivity2</span><span class="sxs-lookup"><span data-stu-id="67292-417">CopyActivity2</span></span>

<span data-ttu-id="67292-418">輸入：Dataset2。</span><span class="sxs-lookup"><span data-stu-id="67292-418">Input: Dataset2.</span></span>  <span data-ttu-id="67292-419">輸出：Dataset3。</span><span class="sxs-lookup"><span data-stu-id="67292-419">Output: Dataset3.</span></span>

<span data-ttu-id="67292-420">唯有當 CopyActivity1 成功執行且 Dataset2 可供使用時，CopyActivity2 才會執行。</span><span class="sxs-lookup"><span data-stu-id="67292-420">CopyActivity2 would run only if the CopyActivity1 has run successfully and Dataset2 is available.</span></span>

<span data-ttu-id="67292-421">以下是範例管線 JSON：</span><span class="sxs-lookup"><span data-stu-id="67292-421">Here is the sample pipeline JSON:</span></span>

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
                "description": "Copy data from a blob to another"
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
                "description": "Copy data from a blob to another"
            }
        ],
        "start": "2016-08-25T01:00:00Z",
        "end": "2016-08-25T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="67292-422">請注意，在此範例中，是將第一個複製活動的輸出資料集 (Dataset2) 指定為第二個活動的輸入。</span><span class="sxs-lookup"><span data-stu-id="67292-422">Notice that in the example, the output dataset of the first copy activity (Dataset2) is specified as input for the second activity.</span></span> <span data-ttu-id="67292-423">因此，只有當來自第一個活動的輸出資料集準備就緒時，第二個活動才會執行。</span><span class="sxs-lookup"><span data-stu-id="67292-423">Therefore, the second activity runs only when the output dataset from the first activity is ready.</span></span>  

<span data-ttu-id="67292-424">在範例中，CopyActivity2 可以有不同的輸入 (例如 Dataset3)，但是您必須指定 Dataset2 做為 CopyActivity2 的輸入，因此在 CopyActivity1 完成之前，活動不會執行。</span><span class="sxs-lookup"><span data-stu-id="67292-424">In the example, CopyActivity2 can have a different input, such as Dataset3, but you specify Dataset2 as an input to CopyActivity2, so the activity does not run until CopyActivity1 finishes.</span></span> <span data-ttu-id="67292-425">例如：</span><span class="sxs-lookup"><span data-stu-id="67292-425">For example:</span></span>

<span data-ttu-id="67292-426">CopyActivity1</span><span class="sxs-lookup"><span data-stu-id="67292-426">CopyActivity1</span></span>

<span data-ttu-id="67292-427">輸入︰Dataset1。</span><span class="sxs-lookup"><span data-stu-id="67292-427">Input: Dataset1.</span></span> <span data-ttu-id="67292-428">輸出：Dataset2。</span><span class="sxs-lookup"><span data-stu-id="67292-428">Output: Dataset2.</span></span>

<span data-ttu-id="67292-429">CopyActivity2</span><span class="sxs-lookup"><span data-stu-id="67292-429">CopyActivity2</span></span>

<span data-ttu-id="67292-430">輸入︰Dataset3、Dataset2。</span><span class="sxs-lookup"><span data-stu-id="67292-430">Inputs: Dataset3, Dataset2.</span></span> <span data-ttu-id="67292-431">輸出︰Dataset4。</span><span class="sxs-lookup"><span data-stu-id="67292-431">Output: Dataset4.</span></span>

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
                "description": "Copy data from a blob to another"
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
                "description": "Copy data from a blob to another"
            }
        ],
        "start": "2017-04-25T01:00:00Z",
        "end": "2017-04-25T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="67292-432">請注意，在此範例中，為第二個複製活動指定了兩個輸入資料集。</span><span class="sxs-lookup"><span data-stu-id="67292-432">Notice that in the example, two input datasets are specified for the second copy activity.</span></span> <span data-ttu-id="67292-433">指定多個輸入時，只有第一個輸入資料集會用來複製資料，但是其他資料集會用來做為相依性。</span><span class="sxs-lookup"><span data-stu-id="67292-433">When multiple inputs are specified, only the first input dataset is used for copying data, but other datasets are used as dependencies.</span></span> <span data-ttu-id="67292-434">CopyActivity2 只會在符合下列條件後才開始︰</span><span class="sxs-lookup"><span data-stu-id="67292-434">CopyActivity2 would start only after the following conditions are met:</span></span>

* <span data-ttu-id="67292-435">CopyActivity1 已順利完成且 Dataset2 可供使用。</span><span class="sxs-lookup"><span data-stu-id="67292-435">CopyActivity1 has successfully completed and Dataset2 is available.</span></span> <span data-ttu-id="67292-436">將資料複製到 Dataset4 時，不會使用此資料集。</span><span class="sxs-lookup"><span data-stu-id="67292-436">This dataset is not used when copying data to Dataset4.</span></span> <span data-ttu-id="67292-437">它只會用來做為 CopyActivity2 的排程相依性。</span><span class="sxs-lookup"><span data-stu-id="67292-437">It only acts as a scheduling dependency for CopyActivity2.</span></span>   
* <span data-ttu-id="67292-438">Dataset3 可供使用。</span><span class="sxs-lookup"><span data-stu-id="67292-438">Dataset3 is available.</span></span> <span data-ttu-id="67292-439">此資料集代表已複製到目的地的資料。</span><span class="sxs-lookup"><span data-stu-id="67292-439">This dataset represents the data that is copied to the destination.</span></span> 