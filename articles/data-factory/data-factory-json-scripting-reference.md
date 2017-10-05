---
title: "Azure Data Factory - JSON 指令碼參考 | Microsoft Docs"
description: "提供 Data Factory 實體的 JSON 結構描述。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 805106c0a5cdbff1f143f22a2ae59f6d2a0bf126
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-data-factory---json-scripting-reference"></a><span data-ttu-id="6dbb4-103">Azure Data Factory - JSON 指令碼參考</span><span class="sxs-lookup"><span data-stu-id="6dbb4-103">Azure Data Factory - JSON Scripting Reference</span></span>
<span data-ttu-id="6dbb4-104">本文提供 JSON 結構描述和範例來定義 Azure Data Factory 實體 (管線、活動、資料集和連結服務)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-104">This article provides JSON schemas and examples for defining Azure Data Factory entities (pipeline, activity, dataset, and linked service).</span></span>  

## <a name="pipeline"></a><span data-ttu-id="6dbb4-105">管線</span><span class="sxs-lookup"><span data-stu-id="6dbb4-105">Pipeline</span></span> 
<span data-ttu-id="6dbb4-106">管線定義的高階結構如下所示︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-106">The high-level structure for a pipeline definition is as follows:</span></span> 

```json
{
  "name": "SamplePipeline",
  "properties": {
    "description": "Describe what pipeline does",
    "activities": [
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

<span data-ttu-id="6dbb4-107">下表說明管線 JSON 定義內的屬性：</span><span class="sxs-lookup"><span data-stu-id="6dbb4-107">Following table describes the properties within the pipeline JSON definition:</span></span>

| <span data-ttu-id="6dbb4-108">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-108">Property</span></span> | <span data-ttu-id="6dbb4-109">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-109">Description</span></span> | <span data-ttu-id="6dbb4-110">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-110">Required</span></span>
-------- | ----------- | --------
| <span data-ttu-id="6dbb4-111">名稱</span><span class="sxs-lookup"><span data-stu-id="6dbb4-111">name</span></span> | <span data-ttu-id="6dbb4-112">管線的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-112">Name of the pipeline.</span></span> <span data-ttu-id="6dbb4-113">指定一個名稱，以表示活動或管線設定要進行的動作</span><span class="sxs-lookup"><span data-stu-id="6dbb4-113">Specify a name that represents the action that the activity or pipeline is configured to do</span></span><br/><ul><li><span data-ttu-id="6dbb4-114">字元數目上限︰260</span><span class="sxs-lookup"><span data-stu-id="6dbb4-114">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="6dbb4-115">開頭必須為字母、數字或底線 (_)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-115">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="6dbb4-116">不允許使用下列字元：“.”、“+”、“?”、“/”、“<”、”>”、”*”、”%”、”&”、”:”、”\\”</span><span class="sxs-lookup"><span data-stu-id="6dbb4-116">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="6dbb4-117">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-117">Yes</span></span> |
| <span data-ttu-id="6dbb4-118">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-118">description</span></span> |<span data-ttu-id="6dbb4-119">說明活動或管線用途的文字</span><span class="sxs-lookup"><span data-stu-id="6dbb4-119">Text describing what the activity or pipeline is used for</span></span> | <span data-ttu-id="6dbb4-120">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-120">No</span></span> |
| <span data-ttu-id="6dbb4-121">活動</span><span class="sxs-lookup"><span data-stu-id="6dbb4-121">activities</span></span> | <span data-ttu-id="6dbb4-122">包含活動清單。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-122">Contains a list of activities.</span></span> | <span data-ttu-id="6dbb4-123">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-123">Yes</span></span> |
| <span data-ttu-id="6dbb4-124">start</span><span class="sxs-lookup"><span data-stu-id="6dbb4-124">start</span></span> |<span data-ttu-id="6dbb4-125">管線的開始日期時間。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-125">Start date-time for the pipeline.</span></span> <span data-ttu-id="6dbb4-126">必須使用 [ISO 格式](http://en.wikipedia.org/wiki/ISO_8601)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-126">Must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="6dbb4-127">例如︰2014-10-14T16:32:41。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-127">For example: 2014-10-14T16:32:41.</span></span> <br/><br/><span data-ttu-id="6dbb4-128">您可以指定本地時間，如 EST 時間。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-128">It is possible to specify a local time, for example an EST time.</span></span> <span data-ttu-id="6dbb4-129">範例如下︰`2016-02-27T06:00:00**-05:00`，這是 6 AM EST。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-129">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="6dbb4-130">管線的 start 和 end 屬性共同指定管線的作用中期間。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-130">The start and end properties together specify active period for the pipeline.</span></span> <span data-ttu-id="6dbb4-131">輸出配量只會在作用中期間內產生。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-131">Output slices are only produced with in this active period.</span></span> |<span data-ttu-id="6dbb4-132">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-132">No</span></span><br/><br/><span data-ttu-id="6dbb4-133">如果您指定 end 屬性的值，也必須指定 start 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-133">If you specify a value for the end property, you must specify value for the start property.</span></span><br/><br/><span data-ttu-id="6dbb4-134">開始和結束時間都可以是空白來建立管線。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-134">The start and end times can both be empty to create a pipeline.</span></span> <span data-ttu-id="6dbb4-135">必須指定兩個值，才能設定執行管線的作用中時間。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-135">You must specify both values to set an active period for the pipeline to run.</span></span> <span data-ttu-id="6dbb4-136">如果您建立管線時未指定開始和結束時間，您可以在稍後使用 Set-AzureRmDataFactoryPipelineActivePeriod Cmdlet 進行設定。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-136">If you do not specify start and end times when creating a pipeline, you can set them using the Set-AzureRmDataFactoryPipelineActivePeriod cmdlet later.</span></span> |
| <span data-ttu-id="6dbb4-137">end</span><span class="sxs-lookup"><span data-stu-id="6dbb4-137">end</span></span> |<span data-ttu-id="6dbb4-138">管線的結束日期時間。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-138">End date-time for the pipeline.</span></span> <span data-ttu-id="6dbb4-139">如果已指定，則必須使用 ISO 格式。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-139">If specified must be in ISO format.</span></span> <span data-ttu-id="6dbb4-140">例如：2014-10-14T17:32:41</span><span class="sxs-lookup"><span data-stu-id="6dbb4-140">For example: 2014-10-14T17:32:41</span></span> <br/><br/><span data-ttu-id="6dbb4-141">您可以指定本地時間，如 EST 時間。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-141">It is possible to specify a local time, for example an EST time.</span></span> <span data-ttu-id="6dbb4-142">範例如下︰`2016-02-27T06:00:00**-05:00`，這是美加東部標準時間上午 6 點。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-142">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="6dbb4-143">若要無限期地執行管線，請指定 9999-09-09 做為 end 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-143">To run the pipeline indefinitely, specify 9999-09-09 as the value for the end property.</span></span> |<span data-ttu-id="6dbb4-144">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-144">No</span></span> <br/><br/><span data-ttu-id="6dbb4-145">如果您指定 start 屬性的值，也必須指定 end 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-145">If you specify a value for the start property, you must specify value for the end property.</span></span><br/><br/><span data-ttu-id="6dbb4-146">請參閱 **start** 屬性的註釋。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-146">See notes for the **start** property.</span></span> |
| <span data-ttu-id="6dbb4-147">isPaused</span><span class="sxs-lookup"><span data-stu-id="6dbb4-147">isPaused</span></span> |<span data-ttu-id="6dbb4-148">如果設為 true，管線不會執行。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-148">If set to true the pipeline does not run.</span></span> <span data-ttu-id="6dbb4-149">預設值 = false。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-149">Default value = false.</span></span> <span data-ttu-id="6dbb4-150">您可以使用此屬性來啟用或停用。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-150">You can use this property to enable or disable.</span></span> |<span data-ttu-id="6dbb4-151">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-151">No</span></span> |
| <span data-ttu-id="6dbb4-152">pipelineMode</span><span class="sxs-lookup"><span data-stu-id="6dbb4-152">pipelineMode</span></span> |<span data-ttu-id="6dbb4-153">排程管線執行的方法。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-153">The method for scheduling runs for the pipeline.</span></span> <span data-ttu-id="6dbb4-154">允許的值包括：scheduled (預設值)、onetime。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-154">Allowed values are: scheduled (default), onetime.</span></span><br/><br/><span data-ttu-id="6dbb4-155">‘Scheduled’ 表示管線會根據其作用中期間 (開始和結束時間) 依指定的時間間隔執行。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-155">‘Scheduled’ indicates that the pipeline runs at a specified time interval according to its active period (start and end time).</span></span> <span data-ttu-id="6dbb4-156">‘Onetime’ 表示管線只會執行一次。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-156">‘Onetime’ indicates that the pipeline runs only once.</span></span> <span data-ttu-id="6dbb4-157">目前，Onetime 管線在建立之後即無法進行修改/更新。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-157">Onetime pipelines once created cannot be modified/updated currently.</span></span> <span data-ttu-id="6dbb4-158">如需 onetime 設定的詳細資料，請參閱 [Onetime 管線](data-factory-create-pipelines.md#onetime-pipeline)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-158">See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details about onetime setting.</span></span> |<span data-ttu-id="6dbb4-159">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-159">No</span></span> |
| <span data-ttu-id="6dbb4-160">expirationTime</span><span class="sxs-lookup"><span data-stu-id="6dbb4-160">expirationTime</span></span> |<span data-ttu-id="6dbb4-161">建立之後，管線有效且應該保持佈建的期間。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-161">Duration of time after creation for which the pipeline is valid and should remain provisioned.</span></span> <span data-ttu-id="6dbb4-162">如果管線沒有任何作用中、失敗或擱置執行，則會在到達到期時間之後自動予以刪除。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-162">If it does not have any active, failed, or pending runs, the pipeline is deleted automatically once it reaches the expiration time.</span></span> |<span data-ttu-id="6dbb4-163">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-163">No</span></span> |


## <a name="activity"></a><span data-ttu-id="6dbb4-164">活動</span><span class="sxs-lookup"><span data-stu-id="6dbb4-164">Activity</span></span> 
<span data-ttu-id="6dbb4-165">管線定義 (activities 元素) 內活動的高階結構如下所示︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-165">The high-level structure for an activity within a pipeline definition (activities element) is as follows:</span></span>

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
    }
    "scheduler":
    {
    }
}
```

<span data-ttu-id="6dbb4-166">下表說明活動 JSON 定義內的屬性：</span><span class="sxs-lookup"><span data-stu-id="6dbb4-166">Following table describe the properties within the activity JSON definition:</span></span>

| <span data-ttu-id="6dbb4-167">Tag</span><span class="sxs-lookup"><span data-stu-id="6dbb4-167">Tag</span></span> | <span data-ttu-id="6dbb4-168">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-168">Description</span></span> | <span data-ttu-id="6dbb4-169">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-170">名稱</span><span class="sxs-lookup"><span data-stu-id="6dbb4-170">name</span></span> |<span data-ttu-id="6dbb4-171">活動的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-171">Name of the activity.</span></span> <span data-ttu-id="6dbb4-172">指定名稱，代表活動設定要進行的動作</span><span class="sxs-lookup"><span data-stu-id="6dbb4-172">Specify a name that represents the action that the activity is configured to do</span></span><br/><ul><li><span data-ttu-id="6dbb4-173">字元數目上限︰260</span><span class="sxs-lookup"><span data-stu-id="6dbb4-173">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="6dbb4-174">開頭必須為字母、數字或底線 (_)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-174">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="6dbb4-175">不允許使用下列字元：“.”、“+”、“?”、“/”、“<”、”>”、”*”、”%”、”&”、”:”、”\\”</span><span class="sxs-lookup"><span data-stu-id="6dbb4-175">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="6dbb4-176">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-176">Yes</span></span> |
| <span data-ttu-id="6dbb4-177">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-177">description</span></span> |<span data-ttu-id="6dbb4-178">說明活動用途的文字。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-178">Text describing what the activity is used for.</span></span> |<span data-ttu-id="6dbb4-179">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-179">Yes</span></span> |
| <span data-ttu-id="6dbb4-180">類型</span><span class="sxs-lookup"><span data-stu-id="6dbb4-180">type</span></span> |<span data-ttu-id="6dbb4-181">指定活動的類型。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-181">Specifies the type of the activity.</span></span> <span data-ttu-id="6dbb4-182">如需了解不同類型的活動，請參閱[資料存放區](#data-stores)和[資料轉換活動](#data-transformation-activities)小節。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-182">See the [DATA STORES](#data-stores) and [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) sections for different types of activities.</span></span> |<span data-ttu-id="6dbb4-183">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-183">Yes</span></span> |
| <span data-ttu-id="6dbb4-184">輸入</span><span class="sxs-lookup"><span data-stu-id="6dbb4-184">inputs</span></span> |<span data-ttu-id="6dbb4-185">活動所使用的輸入資料表</span><span class="sxs-lookup"><span data-stu-id="6dbb4-185">Input tables used by the activity</span></span><br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |<span data-ttu-id="6dbb4-186">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-186">Yes</span></span> |
| <span data-ttu-id="6dbb4-187">輸出</span><span class="sxs-lookup"><span data-stu-id="6dbb4-187">outputs</span></span> |<span data-ttu-id="6dbb4-188">活動所使用的輸出資料表。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-188">Output tables used by the activity.</span></span><br/><br/>`// one output table`<br/>`"outputs":  [ { "name": “outputtable1” } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": “outputtable1” }, { "name": “outputtable2” }  ],` |<span data-ttu-id="6dbb4-189">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-189">Yes</span></span> |
| <span data-ttu-id="6dbb4-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-190">linkedServiceName</span></span> |<span data-ttu-id="6dbb4-191">活動所使用的連結服務名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-191">Name of the linked service used by the activity.</span></span> <br/><br/><span data-ttu-id="6dbb4-192">活動可能會要求您指定可連結至所需計算環境的連結服務。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-192">An activity may require that you specify the linked service that links to the required compute environment.</span></span> |<span data-ttu-id="6dbb4-193">對於 HDInsight 活動、Azure Machine Learning 活動和預存程序活動而言為必要。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-193">Yes for HDInsight activities, Azure Machine Learning activities, and Stored Procedure Activity.</span></span> <br/><br/><span data-ttu-id="6dbb4-194">否：所有其他</span><span class="sxs-lookup"><span data-stu-id="6dbb4-194">No for all others</span></span> |
| <span data-ttu-id="6dbb4-195">typeProperties</span><span class="sxs-lookup"><span data-stu-id="6dbb4-195">typeProperties</span></span> |<span data-ttu-id="6dbb4-196">typeProperties 區段中的屬性會視活動的類型而定。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-196">Properties in the typeProperties section depend on type of the activity.</span></span> |<span data-ttu-id="6dbb4-197">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-197">No</span></span> |
| <span data-ttu-id="6dbb4-198">原則</span><span class="sxs-lookup"><span data-stu-id="6dbb4-198">policy</span></span> |<span data-ttu-id="6dbb4-199">會影響活動之執行階段行為的原則。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-199">Policies that affect the run-time behavior of the activity.</span></span> <span data-ttu-id="6dbb4-200">如果未指定，則會使用預設原則。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-200">If it is not specified, default policies are used.</span></span> |<span data-ttu-id="6dbb4-201">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-201">No</span></span> |
| <span data-ttu-id="6dbb4-202">scheduler</span><span class="sxs-lookup"><span data-stu-id="6dbb4-202">scheduler</span></span> |<span data-ttu-id="6dbb4-203">“scheduler” 屬性用來定義所要的活動排程。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-203">“scheduler” property is used to define desired scheduling for the activity.</span></span> <span data-ttu-id="6dbb4-204">其子屬性與 [資料集中的可用性屬性](data-factory-create-datasets.md#dataset-availability)中的屬性相同。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-204">Its subproperties are the same as the ones in the [availability property in a dataset](data-factory-create-datasets.md#dataset-availability).</span></span> |<span data-ttu-id="6dbb4-205">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-205">No</span></span> |

### <a name="policies"></a><span data-ttu-id="6dbb4-206">原則</span><span class="sxs-lookup"><span data-stu-id="6dbb4-206">Policies</span></span>
<span data-ttu-id="6dbb4-207">原則會影響活動的執行階段行為，特別是在處理資料表配量的時候。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-207">Policies affect the run-time behavior of an activity, specifically when the slice of a table is processed.</span></span> <span data-ttu-id="6dbb4-208">下表提供詳細資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-208">The following table provides the details.</span></span>

| <span data-ttu-id="6dbb4-209">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-209">Property</span></span> | <span data-ttu-id="6dbb4-210">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-210">Permitted values</span></span> | <span data-ttu-id="6dbb4-211">預設值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-211">Default Value</span></span> | <span data-ttu-id="6dbb4-212">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-212">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-213">並行</span><span class="sxs-lookup"><span data-stu-id="6dbb4-213">concurrency</span></span> |<span data-ttu-id="6dbb4-214">整數 </span><span class="sxs-lookup"><span data-stu-id="6dbb4-214">Integer</span></span> <br/><br/><span data-ttu-id="6dbb4-215">最大值：10</span><span class="sxs-lookup"><span data-stu-id="6dbb4-215">Max value: 10</span></span> |<span data-ttu-id="6dbb4-216">1</span><span class="sxs-lookup"><span data-stu-id="6dbb4-216">1</span></span> |<span data-ttu-id="6dbb4-217">活動的並行執行數目。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-217">Number of concurrent executions of the activity.</span></span><br/><br/><span data-ttu-id="6dbb4-218">它可決定不同配量上可以發生的平行活動執行數目。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-218">It determines the number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="6dbb4-219">例如，如果活動需要處理大量可用的資料，具有較大的並行值會加快資料處理。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-219">For example, if an activity needs to go through a large set of available data, having a larger concurrency value speeds up the data processing.</span></span> |
| <span data-ttu-id="6dbb4-220">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="6dbb4-220">executionPriorityOrder</span></span> |<span data-ttu-id="6dbb4-221">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="6dbb4-221">NewestFirst</span></span><br/><br/><span data-ttu-id="6dbb4-222">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="6dbb4-222">OldestFirst</span></span> |<span data-ttu-id="6dbb4-223">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="6dbb4-223">OldestFirst</span></span> |<span data-ttu-id="6dbb4-224">決定正在處理之資料配量的順序。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-224">Determines the ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="6dbb4-225">例如，如果您有 2 個配量 (一個發生在下午 4 點，另一個發生在下午 5 點)，而兩者都暫停執行。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-225">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="6dbb4-226">如果您將 executionPriorityOrder 設為 NewestFirst，則會先處理下午 5 點的配量。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-226">If you set the executionPriorityOrder to be NewestFirst, the slice at 5 PM is processed first.</span></span> <span data-ttu-id="6dbb4-227">同樣地，如果您將 executionPriorityOrder 設為 OldestFIrst，則會處理下午 4 點的配量。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-227">Similarly if you set the executionPriorityORder to be OldestFIrst, then the slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="6dbb4-228">retry</span><span class="sxs-lookup"><span data-stu-id="6dbb4-228">retry</span></span> |<span data-ttu-id="6dbb4-229">整數 </span><span class="sxs-lookup"><span data-stu-id="6dbb4-229">Integer</span></span><br/><br/><span data-ttu-id="6dbb4-230">最大值可以是 10</span><span class="sxs-lookup"><span data-stu-id="6dbb4-230">Max value can be 10</span></span> |<span data-ttu-id="6dbb4-231">0</span><span class="sxs-lookup"><span data-stu-id="6dbb4-231">0</span></span> |<span data-ttu-id="6dbb4-232">在配量的資料處理標示為 [失敗] 前的重試次數。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-232">Number of retries before the data processing for the slice is marked as Failure.</span></span> <span data-ttu-id="6dbb4-233">資料配量的活動執行會一直重試，直到指定的重試計數為止。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-233">Activity execution for a data slice is retried up to the specified retry count.</span></span> <span data-ttu-id="6dbb4-234">在失敗後會儘速完成重試。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-234">The retry is done as soon as possible after the failure.</span></span> |
| <span data-ttu-id="6dbb4-235">timeout</span><span class="sxs-lookup"><span data-stu-id="6dbb4-235">timeout</span></span> |<span data-ttu-id="6dbb4-236">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="6dbb4-236">TimeSpan</span></span> |<span data-ttu-id="6dbb4-237">00:00:00</span><span class="sxs-lookup"><span data-stu-id="6dbb4-237">00:00:00</span></span> |<span data-ttu-id="6dbb4-238">活動的逾時。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-238">Timeout for the activity.</span></span> <span data-ttu-id="6dbb4-239">範例︰00:10:00 (意指逾時 10 分鐘)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-239">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="6dbb4-240">如果您未指定值 (或值為 0)，代表無限逾時。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-240">If a value is not specified or is 0, the timeout is infinite.</span></span><br/><br/><span data-ttu-id="6dbb4-241">如果配量的資料處理時間超過逾時值，該活動會遭到取消，且系統會嘗試重試處理。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-241">If the data processing time on a slice exceeds the timeout value, it is canceled, and the system attempts to retry the processing.</span></span> <span data-ttu-id="6dbb4-242">重試次數取決於 retry 屬性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-242">The number of retries depends on the retry property.</span></span> <span data-ttu-id="6dbb4-243">若發生逾時，狀態會設為 TimedOut。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-243">When timeout occurs, the status is set to TimedOut.</span></span> |
| <span data-ttu-id="6dbb4-244">delay</span><span class="sxs-lookup"><span data-stu-id="6dbb4-244">delay</span></span> |<span data-ttu-id="6dbb4-245">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="6dbb4-245">TimeSpan</span></span> |<span data-ttu-id="6dbb4-246">00:00:00</span><span class="sxs-lookup"><span data-stu-id="6dbb4-246">00:00:00</span></span> |<span data-ttu-id="6dbb4-247">指定配量之資料處理開始之前的延遲。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-247">Specify the delay before data processing of the slice starts.</span></span><br/><br/><span data-ttu-id="6dbb4-248">資料配量的活動執行會在 Delay 超出預期執行時間後開始。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-248">The execution of activity for a data slice is started after the Delay is past the expected execution time.</span></span><br/><br/><span data-ttu-id="6dbb4-249">範例︰00:10:00 (意指延遲 10 分鐘)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-249">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="6dbb4-250">longRetry</span><span class="sxs-lookup"><span data-stu-id="6dbb4-250">longRetry</span></span> |<span data-ttu-id="6dbb4-251">整數 </span><span class="sxs-lookup"><span data-stu-id="6dbb4-251">Integer</span></span><br/><br/><span data-ttu-id="6dbb4-252">最大值：10</span><span class="sxs-lookup"><span data-stu-id="6dbb4-252">Max value: 10</span></span> |<span data-ttu-id="6dbb4-253">1</span><span class="sxs-lookup"><span data-stu-id="6dbb4-253">1</span></span> |<span data-ttu-id="6dbb4-254">配量執行失敗之前的長時間重試嘗試次數。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-254">The number of long retry attempts before the slice execution is failed.</span></span><br/><br/><span data-ttu-id="6dbb4-255">多個 longRetry 嘗試之間以 longRetryInterval 隔開。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-255">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="6dbb4-256">所以如果您需要指定重試嘗試之間的時間，請使用 longRetry。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-256">So if you need to specify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="6dbb4-257">如果您指定 Retry 和 longRetry 兩者，每個 longRetry 嘗試都包含 Retry 嘗試，且最大嘗試次數是 Retry * longRetry。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-257">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and the max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="6dbb4-258">例如，如果活動原則的設定如下︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-258">For example, if we have the following settings in the activity policy:</span></span><br/><span data-ttu-id="6dbb4-259">Retry：3</span><span class="sxs-lookup"><span data-stu-id="6dbb4-259">Retry: 3</span></span><br/><span data-ttu-id="6dbb4-260">longRetry：2</span><span class="sxs-lookup"><span data-stu-id="6dbb4-260">longRetry: 2</span></span><br/><span data-ttu-id="6dbb4-261">longRetryInterval：01:00:00</span><span class="sxs-lookup"><span data-stu-id="6dbb4-261">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="6dbb4-262">假設只有一個要執行的配量 (狀態是 Waiting)，且活動執行每次都失敗。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-262">Assume there is only one slice to execute (status is Waiting) and the activity execution fails every time.</span></span> <span data-ttu-id="6dbb4-263">一開始會有 3 次連續執行嘗試。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-263">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="6dbb4-264">在每次嘗試之後，配量狀態會是 Retry。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-264">After each attempt, the slice status would be Retry.</span></span> <span data-ttu-id="6dbb4-265">在前 3 次嘗試結束之後，配量狀態會是 LongRetry。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-265">After first 3 attempts are over, the slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="6dbb4-266">一個小時 (也就是 longRetryInteval 的值) 之後，會有另一組 3 次連續執行嘗試。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-266">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="6dbb4-267">在那之後，配量狀態會是 Failed，不會再嘗試重試。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-267">After that, the slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="6dbb4-268">因此全部已進行 6 次嘗試。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-268">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="6dbb4-269">如果任何執行成功，配量狀態會是 Ready 且不會再嘗試重試。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-269">If any execution succeeds, the slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="6dbb4-270">longRetry 可能用於下列情況：相依資料達到不具決定性的次數，或進行資料處理的整體環境很脆弱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-270">longRetry may be used in situations where dependent data arrives at non-deterministic times or the overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="6dbb4-271">在這類情況下逐一進行重試並沒有幫助，而在一段時間後進行重試則會導致所要的結果。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-271">In such cases, doing retries one after another may not help and doing so after an interval of time results in the desired output.</span></span><br/><br/><span data-ttu-id="6dbb4-272">提醒：請勿設定較大的 longRetry 或 longRetryInterval 值。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-272">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="6dbb4-273">較大的值通常表示其他系統問題。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-273">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="6dbb4-274">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="6dbb4-274">longRetryInterval</span></span> |<span data-ttu-id="6dbb4-275">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="6dbb4-275">TimeSpan</span></span> |<span data-ttu-id="6dbb4-276">00:00:00</span><span class="sxs-lookup"><span data-stu-id="6dbb4-276">00:00:00</span></span> |<span data-ttu-id="6dbb4-277">長時間重試嘗試之間的延遲</span><span class="sxs-lookup"><span data-stu-id="6dbb4-277">The delay between long retry attempts</span></span> |

### <a name="typeproperties-section"></a><span data-ttu-id="6dbb4-278">typeProperties 區段</span><span class="sxs-lookup"><span data-stu-id="6dbb4-278">typeProperties section</span></span>
<span data-ttu-id="6dbb4-279">每個活動的 typeProperties 區段不同。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-279">The typeProperties section is different for each activity.</span></span> <span data-ttu-id="6dbb4-280">轉換活動只有 type 屬性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-280">Transformation activities have just the type properties.</span></span> <span data-ttu-id="6dbb4-281">如需在管線中定義轉換活動的 JSON 範例，請參閱本文中的[資料轉換活動](#data-transformation-activities)一節。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-281">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span> 

<span data-ttu-id="6dbb4-282">**複製活動**的 typeProperties 區段中有兩個子區段︰**source** 和 **sink**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-282">**Copy activity** has two subsections in the typeProperties section: **source** and **sink**.</span></span> <span data-ttu-id="6dbb4-283">如需示範如何使用資料存放區作為來源和/或接收的 JSON 範例，請參閱本文中的[資料存放區](#data-stores)一節。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-283">See [DATA STORES](#data-stores) section in this article for JSON samples that show how to use a data store as a source and/or sink.</span></span> 

### <a name="sample-copy-pipeline"></a><span data-ttu-id="6dbb4-284">範例複製管線</span><span class="sxs-lookup"><span data-stu-id="6dbb4-284">Sample copy pipeline</span></span>
<span data-ttu-id="6dbb4-285">在以下的範例管線中， **Copy** in the **活動** 類型的活動。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-285">In the following sample pipeline, there is one activity of type **Copy** in the **activities** section.</span></span> <span data-ttu-id="6dbb4-286">在此範例中， [Copy 活動](data-factory-data-movement-activities.md) 會將資料從 Azure Blob 儲存體複製到 Azure SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-286">In this sample, the [Copy activity](data-factory-data-movement-activities.md) copies data from an Azure Blob storage to an Azure SQL database.</span></span> 

```json
{
  "name": "CopyPipeline",
  "properties": {
    "description": "Copy data from a blob to Azure SQL table",
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
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

<span data-ttu-id="6dbb4-287">請注意下列幾點：</span><span class="sxs-lookup"><span data-stu-id="6dbb4-287">Note the following points:</span></span>

* <span data-ttu-id="6dbb4-288">在活動區段中，只會有一個 **type** 設為 **Copy** 的活動。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-288">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span>
* <span data-ttu-id="6dbb4-289">活動的輸入設定為 **InputDataset**，活動的輸出則設定為 **OutputDataset**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-289">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span>
* <span data-ttu-id="6dbb4-290">在 **typeProperties** 區段中，來源類型指定為 **BlobSource**，接收類型指定為 **SqlSink**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-290">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span>

<span data-ttu-id="6dbb4-291">如需示範如何使用資料存放區作為來源和/或接收的 JSON 範例，請參閱本文中的[資料存放區](#data-stores)一節。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-291">See [DATA STORES](#data-stores) section in this article for JSON samples that show how to use a data store as a source and/or sink.</span></span>    

<span data-ttu-id="6dbb4-292">如需建立此管線的完整逐步解說，請參閱 [教學課程：將資料從 Blob 儲存體複製到 SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-292">For a complete walkthrough of creating this pipeline, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

### <a name="sample-transformation-pipeline"></a><span data-ttu-id="6dbb4-293">範例轉換管線</span><span class="sxs-lookup"><span data-stu-id="6dbb4-293">Sample transformation pipeline</span></span>
<span data-ttu-id="6dbb4-294">在以下的範例管線中， **CopyActivity** in the **活動** 類型的活動。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-294">In the following sample pipeline, there is one activity of type **HDInsightHive** in the **activities** section.</span></span> <span data-ttu-id="6dbb4-295">在此範例中， [HDInsight Hive 活動](data-factory-hive-activity.md) 會執行 Azure HDInsight Hadoop 叢集上的 Hive 指令碼檔案，來轉換 Azure Blob 儲存體的資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-295">In this sample, the [HDInsight Hive activity](data-factory-hive-activity.md) transforms data from an Azure Blob storage by running a Hive script file on an Azure HDInsight Hadoop cluster.</span></span> 

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
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="6dbb4-296">請注意下列幾點：</span><span class="sxs-lookup"><span data-stu-id="6dbb4-296">Note the following points:</span></span> 

* <span data-ttu-id="6dbb4-297">在活動區段中，只會有一個 **type** 設為 **HDInsightHive** 的活動。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-297">In the activities section, there is only one activity whose **type** is set to **HDInsightHive**.</span></span>
* <span data-ttu-id="6dbb4-298">Hive 指令碼檔案 **partitionweblogs.hql** 儲存於 Azure 儲存體帳戶 (透過名為 **AzureStorageLinkedService** 的 scriptLinkedService 指定)，且位於 **adfgetstarted** 容器的 **script** 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-298">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span></span>
* <span data-ttu-id="6dbb4-299">**defines** 區段用來指定執行階段設定，該設定將傳遞到 Hive 指令碼作為 Hive 設定值 (例如，`${hiveconf:inputtable}`、`${hiveconf:partitionedtable}`)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-299">The **defines** section is used to specify the runtime settings that are passed to the hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span></span>

<span data-ttu-id="6dbb4-300">如需在管線中定義轉換活動的 JSON 範例，請參閱本文中的[資料轉換活動](#data-transformation-activities)一節。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-300">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span>

<span data-ttu-id="6dbb4-301">如需建立此管線的完整逐步解說，請參閱 [教學課程：使用 Hadoop 叢集建置您的第一個管線來處理資料](data-factory-build-your-first-pipeline.md)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-301">For a complete walkthrough of creating this pipeline, see [Tutorial: Build your first pipeline to process data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="linked-service"></a><span data-ttu-id="6dbb4-302">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-302">Linked service</span></span>
<span data-ttu-id="6dbb4-303">連結服務定義的高階結構如下所示︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-303">The high-level structure for a linked service definition is as follows:</span></span>

```json
{
    "name": "<name of the linked service>",
    "properties": {
        "type": "<type of the linked service>",
        "typeProperties": {
        }
    }
}
```

<span data-ttu-id="6dbb4-304">下表說明活動 JSON 定義內的屬性：</span><span class="sxs-lookup"><span data-stu-id="6dbb4-304">Following table describe the properties within the activity JSON definition:</span></span>

| <span data-ttu-id="6dbb4-305">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-305">Property</span></span> | <span data-ttu-id="6dbb4-306">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-306">Description</span></span> | <span data-ttu-id="6dbb4-307">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-307">Required</span></span> |
| -------- | ----------- | -------- | 
| <span data-ttu-id="6dbb4-308">名稱</span><span class="sxs-lookup"><span data-stu-id="6dbb4-308">name</span></span> | <span data-ttu-id="6dbb4-309">連結服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-309">Name of the linked service.</span></span> | <span data-ttu-id="6dbb4-310">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-310">Yes</span></span> | 
| <span data-ttu-id="6dbb4-311">properties - type</span><span class="sxs-lookup"><span data-stu-id="6dbb4-311">properties - type</span></span> | <span data-ttu-id="6dbb4-312">連結服務的類型。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-312">Type of the linked service.</span></span> <span data-ttu-id="6dbb4-313">例如︰Azure 儲存體、Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-313">For example: Azure Storage, Azure SQL Database.</span></span> |
| <span data-ttu-id="6dbb4-314">typeProperties</span><span class="sxs-lookup"><span data-stu-id="6dbb4-314">typeProperties</span></span> | <span data-ttu-id="6dbb4-315">TypeProperties 區段中的元素隨著每個資料存放區或計算環境而不同。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-315">The typeProperties section has elements that are different for each data store or compute environment.</span></span> <span data-ttu-id="6dbb4-316">關於所有資料存放區連結服務，請參閱[資料存放區](#datastores)一節，關於所有計算連結服務，請參閱[計算環境](#compute-environments)一節</span><span class="sxs-lookup"><span data-stu-id="6dbb4-316">See [data stores](#datastores) section for all the data store linked services and [compute environments](#compute-environments) for all the compute linked services</span></span> |   

## <a name="dataset"></a><span data-ttu-id="6dbb4-317">Dataset</span><span class="sxs-lookup"><span data-stu-id="6dbb4-317">Dataset</span></span> 
<span data-ttu-id="6dbb4-318">Azure Data Factory 中的資料集定義如下：</span><span class="sxs-lookup"><span data-stu-id="6dbb4-318">A dataset in Azure Data Factory is defined as follows:</span></span>

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

<span data-ttu-id="6dbb4-319">下表描述上述 JSON 的屬性：</span><span class="sxs-lookup"><span data-stu-id="6dbb4-319">The following table describes properties in the above JSON:</span></span>   

| <span data-ttu-id="6dbb4-320">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-320">Property</span></span> | <span data-ttu-id="6dbb4-321">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-321">Description</span></span> | <span data-ttu-id="6dbb4-322">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-322">Required</span></span> | <span data-ttu-id="6dbb4-323">預設值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-323">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-324">名稱</span><span class="sxs-lookup"><span data-stu-id="6dbb4-324">name</span></span> | <span data-ttu-id="6dbb4-325">資料集的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-325">Name of the dataset.</span></span> <span data-ttu-id="6dbb4-326">請參閱 [Azure Data Factory - 命名規則](data-factory-naming-rules.md) ，以了解命名規則。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-326">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="6dbb4-327">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-327">Yes</span></span> |<span data-ttu-id="6dbb4-328">NA</span><span class="sxs-lookup"><span data-stu-id="6dbb4-328">NA</span></span> |
| <span data-ttu-id="6dbb4-329">類型</span><span class="sxs-lookup"><span data-stu-id="6dbb4-329">type</span></span> | <span data-ttu-id="6dbb4-330">資料集的類型。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-330">Type of the dataset.</span></span> <span data-ttu-id="6dbb4-331">指定 Azure Data Factory 支援的其中一個類型 (例如︰AzureBlob、AzureSqlTable)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-331">Specify one of the types supported by Azure Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <span data-ttu-id="6dbb4-332">關於 Data Factory 支援的所有資料存放區和資料集類型，請參閱[資料存放區](#data-stores)一節。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-332">See [DATA STORES](#data-stores) section for all the data stores and dataset types supported by Data Factory.</span></span> | 
| <span data-ttu-id="6dbb4-333">structure</span><span class="sxs-lookup"><span data-stu-id="6dbb4-333">structure</span></span> | <span data-ttu-id="6dbb4-334">資料集的結構描述。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-334">Schema of the dataset.</span></span> <span data-ttu-id="6dbb4-335">它包含資料行、其類型等。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-335">It contains columns, their types, etc.</span></span> | <span data-ttu-id="6dbb4-336">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-336">No</span></span> |<span data-ttu-id="6dbb4-337">NA</span><span class="sxs-lookup"><span data-stu-id="6dbb4-337">NA</span></span> |
| <span data-ttu-id="6dbb4-338">typeProperties</span><span class="sxs-lookup"><span data-stu-id="6dbb4-338">typeProperties</span></span> | <span data-ttu-id="6dbb4-339">對應至所選類型的屬性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-339">Properties corresponding to the selected type.</span></span> <span data-ttu-id="6dbb4-340">關於支援的類型和其屬性，請參閱[資料存放區](#data-stores)一節。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-340">See [DATA STORES](#data-stores) section for supported types and their properties.</span></span> |<span data-ttu-id="6dbb4-341">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-341">Yes</span></span> |<span data-ttu-id="6dbb4-342">NA</span><span class="sxs-lookup"><span data-stu-id="6dbb4-342">NA</span></span> |
| <span data-ttu-id="6dbb4-343">external</span><span class="sxs-lookup"><span data-stu-id="6dbb4-343">external</span></span> | <span data-ttu-id="6dbb4-344">用來指定資料集是否由 Data Factory 管線明確產生的布林值旗標。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-344">Boolean flag to specify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> |<span data-ttu-id="6dbb4-345">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-345">No</span></span> |<span data-ttu-id="6dbb4-346">false</span><span class="sxs-lookup"><span data-stu-id="6dbb4-346">false</span></span> |
| <span data-ttu-id="6dbb4-347">availability</span><span class="sxs-lookup"><span data-stu-id="6dbb4-347">availability</span></span> | <span data-ttu-id="6dbb4-348">定義處理時間範圍或資料集生產的切割模型。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-348">Defines the processing window or the slicing model for the dataset production.</span></span> <span data-ttu-id="6dbb4-349">如需資料集切割模型的詳細資訊，請參閱 [排程和執行](data-factory-scheduling-and-execution.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-349">For details on the dataset slicing model, see [Scheduling and Execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="6dbb4-350">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-350">Yes</span></span> |<span data-ttu-id="6dbb4-351">NA</span><span class="sxs-lookup"><span data-stu-id="6dbb4-351">NA</span></span> |
| <span data-ttu-id="6dbb4-352">原則</span><span class="sxs-lookup"><span data-stu-id="6dbb4-352">policy</span></span> |<span data-ttu-id="6dbb4-353">定義資料集配量必須符合的準則或條件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-353">Defines the criteria or the condition that the dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="6dbb4-354">如需詳細資訊，請參閱 [資料集原則](#Policy) 一節。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-354">For details, see [Dataset Policy](#Policy) section.</span></span> |<span data-ttu-id="6dbb4-355">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-355">No</span></span> |<span data-ttu-id="6dbb4-356">NA</span><span class="sxs-lookup"><span data-stu-id="6dbb4-356">NA</span></span> |

<span data-ttu-id="6dbb4-357">**structure** 區段中的每個資料行包含下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-357">Each column in the **structure** section contains the following properties:</span></span>

| <span data-ttu-id="6dbb4-358">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-358">Property</span></span> | <span data-ttu-id="6dbb4-359">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-359">Description</span></span> | <span data-ttu-id="6dbb4-360">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-360">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-361">名稱</span><span class="sxs-lookup"><span data-stu-id="6dbb4-361">name</span></span> |<span data-ttu-id="6dbb4-362">資料行的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-362">Name of the column.</span></span> |<span data-ttu-id="6dbb4-363">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-363">Yes</span></span> |
| <span data-ttu-id="6dbb4-364">類型</span><span class="sxs-lookup"><span data-stu-id="6dbb4-364">type</span></span> |<span data-ttu-id="6dbb4-365">資料行的資料類型。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-365">Data type of the column.</span></span>  |<span data-ttu-id="6dbb4-366">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-366">No</span></span> |
| <span data-ttu-id="6dbb4-367">culture</span><span class="sxs-lookup"><span data-stu-id="6dbb4-367">culture</span></span> |<span data-ttu-id="6dbb4-368">.NET 型文化特性是在已指定類型 (type) 且是 .NET 類型 `Datetime` 或 `Datetimeoffset` 時使用。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-368">.NET based culture to be used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="6dbb4-369">預設值為 `en-us`。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-369">Default is `en-us`.</span></span> |<span data-ttu-id="6dbb4-370">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-370">No</span></span> |
| <span data-ttu-id="6dbb4-371">format</span><span class="sxs-lookup"><span data-stu-id="6dbb4-371">format</span></span> |<span data-ttu-id="6dbb4-372">格式字串是在已指定類型且是 .NET 類型 `Datetime` 或 `Datetimeoffset` 時使用。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-372">Format string to be used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="6dbb4-373">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-373">No</span></span> |

<span data-ttu-id="6dbb4-374">在下列範例中，資料集有三個資料行 `slicetimestamp`、`projectname` 及 `pageviews`，類型分別為：String、String 及 Decimal。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-374">In the following example, the dataset has three columns `slicetimestamp`, `projectname`, and `pageviews` and they are of type: String, String, and Decimal respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="6dbb4-375">下表描述您在 **availability** 區段中可使用的屬性：</span><span class="sxs-lookup"><span data-stu-id="6dbb4-375">The following table describes properties you can use in the **availability** section:</span></span>

| <span data-ttu-id="6dbb4-376">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-376">Property</span></span> | <span data-ttu-id="6dbb4-377">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-377">Description</span></span> | <span data-ttu-id="6dbb4-378">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-378">Required</span></span> | <span data-ttu-id="6dbb4-379">預設值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-379">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-380">frequency</span><span class="sxs-lookup"><span data-stu-id="6dbb4-380">frequency</span></span> |<span data-ttu-id="6dbb4-381">指定資料集配量生產的時間單位。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-381">Specifies the time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="6dbb4-382"><b>支援的頻率</b>：Minute、Hour、Day、Week、Month</span><span class="sxs-lookup"><span data-stu-id="6dbb4-382"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="6dbb4-383">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-383">Yes</span></span> |<span data-ttu-id="6dbb4-384">NA</span><span class="sxs-lookup"><span data-stu-id="6dbb4-384">NA</span></span> |
| <span data-ttu-id="6dbb4-385">interval</span><span class="sxs-lookup"><span data-stu-id="6dbb4-385">interval</span></span> |<span data-ttu-id="6dbb4-386">指定頻率的倍數</span><span class="sxs-lookup"><span data-stu-id="6dbb4-386">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="6dbb4-387">「頻率 x 間隔」會決定產生配量的頻率。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-387">”Frequency x interval” determines how often the slice is produced.</span></span><br/><br/><span data-ttu-id="6dbb4-388">如果您需要將資料集以每小時為單位來切割，請將 <b>Frequency</b> 設定為 <b>Hour</b>，將 <b>interval</b> 設定為 <b>1</b>。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-388">If you need the dataset to be sliced on an hourly basis, you set <b>Frequency</b> to <b>Hour</b>, and <b>interval</b> to <b>1</b>.</span></span><br/><br/><span data-ttu-id="6dbb4-389"><b>注意</b>：如果您將 Frequency 指定為 Minute，建議您將 interval 設定為不小於 15</span><span class="sxs-lookup"><span data-stu-id="6dbb4-389"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set the interval to no less than 15</span></span> |<span data-ttu-id="6dbb4-390">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-390">Yes</span></span> |<span data-ttu-id="6dbb4-391">NA</span><span class="sxs-lookup"><span data-stu-id="6dbb4-391">NA</span></span> |
| <span data-ttu-id="6dbb4-392">style</span><span class="sxs-lookup"><span data-stu-id="6dbb4-392">style</span></span> |<span data-ttu-id="6dbb4-393">指定是否應該在間隔開始/結束時產生配量。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-393">Specifies whether the slice should be produced at the start/end of the interval.</span></span><ul><li><span data-ttu-id="6dbb4-394">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="6dbb4-394">StartOfInterval</span></span></li><li><span data-ttu-id="6dbb4-395">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="6dbb4-395">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="6dbb4-396">如果 Frequency 設為 Month，style 設為 EndOfInterval，則會在當月最後一天產生配量。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-396">If Frequency is set to Month and style is set to EndOfInterval, the slice is produced on the last day of month.</span></span> <span data-ttu-id="6dbb4-397">如果 style 設為 StartOfInterval，則會在每月的第一天產生配量。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-397">If the style is set to StartOfInterval, the slice is produced on the first day of month.</span></span><br/><br/><span data-ttu-id="6dbb4-398">如果 Frequency 設為 Day，style 設為 EndOfInterval，則會在當天最後一個小時產生配量。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-398">If Frequency is set to Day and style is set to EndOfInterval, the slice is produced in the last hour of the day.</span></span><br/><br/><span data-ttu-id="6dbb4-399">如果 Frequency 設為 Hour，style 設為 EndOfInterval，則會在每小時結束時產生配量。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-399">If Frequency is set to Hour and style is set to EndOfInterval, the slice is produced at the end of the hour.</span></span> <span data-ttu-id="6dbb4-400">例如，若為下午 1 – 2 點期間的配量，此配量會在下午 2 點產生。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-400">For example, for a slice for 1 PM – 2 PM period, the slice is produced at 2 PM.</span></span> |<span data-ttu-id="6dbb4-401">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-401">No</span></span> |<span data-ttu-id="6dbb4-402">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="6dbb4-402">EndOfInterval</span></span> |
| <span data-ttu-id="6dbb4-403">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="6dbb4-403">anchorDateTime</span></span> |<span data-ttu-id="6dbb4-404">定義排程器用來計算資料集配量界限的時間絕對位置。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-404">Defines the absolute position in time used by scheduler to compute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="6dbb4-405"><b>注意</b>：如果 AnchorDateTime 有比頻率更細微的日期部分，則系統會忽略那些更細微的部分。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-405"><b>Note</b>: If the AnchorDateTime has date parts that are more granular than the frequency then the more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="6dbb4-406">例如，如果 <b>interval</b> 為 <b>hourly</b> (frequency: hour 且 interval: 1)，而且 <b>AnchorDateTime</b> 包含<b>分鐘和秒鐘</b>，則會忽略 AnchorDateTime 的<b>分鐘和秒鐘</b>部分。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-406">For example, if the <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and the <b>AnchorDateTime</b> contains <b>minutes and seconds</b> then the <b>minutes and seconds</b> parts of the AnchorDateTime are ignored.</span></span> |<span data-ttu-id="6dbb4-407">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-407">No</span></span> |<span data-ttu-id="6dbb4-408">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="6dbb4-408">01/01/0001</span></span> |
| <span data-ttu-id="6dbb4-409">Offset</span><span class="sxs-lookup"><span data-stu-id="6dbb4-409">offset</span></span> |<span data-ttu-id="6dbb4-410">所有資料集配量的開始和結束移位所依據的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-410">Timespan by which the start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="6dbb4-411"><b>注意</b>︰如果同時指定 anchorDateTime 和 offset，結果會是合併的位移。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-411"><b>Note</b>: If both anchorDateTime and offset are specified, the result is the combined shift.</span></span> |<span data-ttu-id="6dbb4-412">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-412">No</span></span> |<span data-ttu-id="6dbb4-413">NA</span><span class="sxs-lookup"><span data-stu-id="6dbb4-413">NA</span></span> |

<span data-ttu-id="6dbb4-414">下列 availability 區段指定輸出資料集是每小時產生 (或) 輸入資料集是每小時可用：</span><span class="sxs-lookup"><span data-stu-id="6dbb4-414">The following availability section specifies that the output dataset is either produced hourly (or) input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="6dbb4-415">資料集中的 **policy** 區段定義資料集配量必須符合的準則或條件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-415">The **policy** section in dataset definition defines the criteria or the condition that the dataset slices must fulfill.</span></span>

| <span data-ttu-id="6dbb4-416">原則名稱</span><span class="sxs-lookup"><span data-stu-id="6dbb4-416">Policy Name</span></span> | <span data-ttu-id="6dbb4-417">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-417">Description</span></span> | <span data-ttu-id="6dbb4-418">適用於</span><span class="sxs-lookup"><span data-stu-id="6dbb4-418">Applied To</span></span> | <span data-ttu-id="6dbb4-419">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-419">Required</span></span> | <span data-ttu-id="6dbb4-420">預設值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-420">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-421">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="6dbb4-421">minimumSizeMB</span></span> |<span data-ttu-id="6dbb4-422">驗證 **Azure Blob** 中的資料是否符合最小的大小需求 (以 MB 為單位)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-422">Validates that the data in an **Azure blob** meets the minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="6dbb4-423">Azure Blob</span><span class="sxs-lookup"><span data-stu-id="6dbb4-423">Azure Blob</span></span> |<span data-ttu-id="6dbb4-424">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-424">No</span></span> |<span data-ttu-id="6dbb4-425">NA</span><span class="sxs-lookup"><span data-stu-id="6dbb4-425">NA</span></span> |
| <span data-ttu-id="6dbb4-426">minimumRows</span><span class="sxs-lookup"><span data-stu-id="6dbb4-426">minimumRows</span></span> |<span data-ttu-id="6dbb4-427">驗證 **Azure SQL Database** 或 **Azure 資料表**中的資料是否包含最小的資料列數。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-427">Validates that the data in an **Azure SQL database** or an **Azure table** contains the minimum number of rows.</span></span> |<ul><li><span data-ttu-id="6dbb4-428">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="6dbb4-428">Azure SQL Database</span></span></li><li><span data-ttu-id="6dbb4-429">Azure 資料表</span><span class="sxs-lookup"><span data-stu-id="6dbb4-429">Azure Table</span></span></li></ul> |<span data-ttu-id="6dbb4-430">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-430">No</span></span> |<span data-ttu-id="6dbb4-431">NA</span><span class="sxs-lookup"><span data-stu-id="6dbb4-431">NA</span></span> |

<span data-ttu-id="6dbb4-432">**範例：**</span><span class="sxs-lookup"><span data-stu-id="6dbb4-432">**Example:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="6dbb4-433">除非資料集是由 Azure Data Factory 產生，否則應該標示為 **外部**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-433">Unless a dataset is being produced by Azure Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="6dbb4-434">除非會使用活動或管線鏈結，否則此設定通常會套用到管線中第一個活動的輸入。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-434">This setting generally applies to the inputs of first activity in a pipeline unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="6dbb4-435">名稱</span><span class="sxs-lookup"><span data-stu-id="6dbb4-435">Name</span></span> | <span data-ttu-id="6dbb4-436">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-436">Description</span></span> | <span data-ttu-id="6dbb4-437">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-437">Required</span></span> | <span data-ttu-id="6dbb4-438">預設值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-438">Default Value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-439">dataDelay</span><span class="sxs-lookup"><span data-stu-id="6dbb4-439">dataDelay</span></span> |<span data-ttu-id="6dbb4-440">延遲指定配量之外部資料可用性檢查的時間。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-440">Time to delay the check on the availability of the external data for the given slice.</span></span> <span data-ttu-id="6dbb4-441">例如，如果是每小時有資料可用，則可以使用 dataDelay 來延遲查看「外部資料是否可用，且對應的配量是否已就緒」的檢查。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-441">For example, if the data is available hourly, the check to see the external data is available and the corresponding slice is Ready can be delayed by using dataDelay.</span></span><br/><br/><span data-ttu-id="6dbb4-442">僅適用於目前的時間。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-442">Only applies to the present time.</span></span>  <span data-ttu-id="6dbb4-443">例如，如果現在時間是下午 1:00，且此值是 10 分鐘，驗證就會在下午 1:10 開始。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-443">For example, if it is 1:00 PM right now and this value is 10 minutes, the validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="6dbb4-444">此設定不會影響過去配量 (配量結束時間 + dataDelay < 現在的配量) 的處理方式而不產生任何延遲。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-444">This setting does not affect slices in the past (slices with Slice End Time + dataDelay < Now) are processed without any delay.</span></span><br/><br/><span data-ttu-id="6dbb4-445">時間若大於 23:59 小時，則必須使用 `day.hours:minutes:seconds` 格式指定。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-445">Time greater than 23:59 hours need to specified using the `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="6dbb4-446">例如，若要指定 24 小時，請不要使用 24:00:00；請改用 1.00:00:00。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-446">For example, to specify 24 hours, don't use 24:00:00; instead, use 1.00:00:00.</span></span> <span data-ttu-id="6dbb4-447">如果您使用 24:00:00，這會視同 24 天 (24.00:00:00)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-447">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="6dbb4-448">如為 1 天又 4 小時，請指定 1:04:00:00。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-448">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="6dbb4-449">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-449">No</span></span> |<span data-ttu-id="6dbb4-450">0</span><span class="sxs-lookup"><span data-stu-id="6dbb4-450">0</span></span> |
| <span data-ttu-id="6dbb4-451">retryInterval</span><span class="sxs-lookup"><span data-stu-id="6dbb4-451">retryInterval</span></span> |<span data-ttu-id="6dbb4-452">失敗與下一步重試嘗試之間的等待時間。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-452">The wait time between a failure and the next retry attempt.</span></span> <span data-ttu-id="6dbb4-453">如果嘗試失敗，則下一次嘗試是在 retryInterval 之後。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-453">If a try fails, the next try is after retryInterval.</span></span> <br/><br/><span data-ttu-id="6dbb4-454">如果現在是下午 1:00，我們會開始第一次嘗試。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-454">If it is 1:00 PM right now, we begin the first try.</span></span> <span data-ttu-id="6dbb4-455">如果完成第一次驗證檢查的持續時間是 1 分鐘且作業失敗，則下一次重試會在 1:00 + 1 分鐘 (持續時間) + 1 分鐘 (重試間隔) = 1:02 PM。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-455">If the duration to complete the first validation check is 1 minute and the operation failed, the next retry is at 1:00 + 1 min (duration) + 1 min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="6dbb4-456">若是過去的配量，則不會有任何延遲。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-456">For slices in the past, there is no delay.</span></span> <span data-ttu-id="6dbb4-457">重試會立即發生。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-457">The retry happens immediately.</span></span> |<span data-ttu-id="6dbb4-458">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-458">No</span></span> |<span data-ttu-id="6dbb4-459">00:01:00 (1 分鐘)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-459">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="6dbb4-460">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="6dbb4-460">retryTimeout</span></span> |<span data-ttu-id="6dbb4-461">每次重試嘗試的逾時。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-461">The timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="6dbb4-462">如果此屬性設為 10 分鐘，則必須在 10 分鐘內完成驗證。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-462">If this property is set to 10 minutes, the validation needs to be completed within 10 minutes.</span></span> <span data-ttu-id="6dbb4-463">如果花超過 10 分鐘來執行驗證，則重試會逾時。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-463">If it takes longer than 10 minutes to perform the validation, the retry times out.</span></span><br/><br/><span data-ttu-id="6dbb4-464">如果驗證的所有嘗試都逾時，配量會標示為 TimedOut。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-464">If all attempts for the validation times out, the slice is marked as TimedOut.</span></span> |<span data-ttu-id="6dbb4-465">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-465">No</span></span> |<span data-ttu-id="6dbb4-466">00:10:00 (10 分鐘)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-466">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="6dbb4-467">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="6dbb4-467">maximumRetry</span></span> |<span data-ttu-id="6dbb4-468">檢查外部資料可用性的次數。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-468">Number of times to check for the availability of the external data.</span></span> <span data-ttu-id="6dbb4-469">允許的最大值為 10。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-469">The allowed maximum value is 10.</span></span> |<span data-ttu-id="6dbb4-470">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-470">No</span></span> |<span data-ttu-id="6dbb4-471">3</span><span class="sxs-lookup"><span data-stu-id="6dbb4-471">3</span></span> |


## <a name="data-stores"></a><span data-ttu-id="6dbb4-472">資料存放區</span><span class="sxs-lookup"><span data-stu-id="6dbb4-472">DATA STORES</span></span>
<span data-ttu-id="6dbb4-473">[連結服務](#linked-service)一節描述所有連結服務類型通用的 JSON 元素。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-473">The [Linked service](#linked-service) section provided descriptions for JSON elements that are common to all types of linked services.</span></span> <span data-ttu-id="6dbb4-474">本節提供每個資料存放區特有的 JSON 元素的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-474">This section provides details about JSON elements that are specific to each data store.</span></span>

<span data-ttu-id="6dbb4-475">[資料集](#dataset)一節描述所有資料集類型通用的 JSON 元素。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-475">The [Dataset](#dataset) section provided descriptions for JSON elements that are common to all types of datasets.</span></span> <span data-ttu-id="6dbb4-476">本節提供每個資料存放區特有的 JSON 元素的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-476">This section provides details about JSON elements that are specific to each data store.</span></span>

<span data-ttu-id="6dbb4-477">[活動](#activity)一節描述所有活動類型通用的 JSON 元素。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-477">The [Activity](#activity) section provided descriptions for JSON elements that are common to all types of activities.</span></span> <span data-ttu-id="6dbb4-478">本節詳細說明複製活動中作為來源/接收之每個資料存放區特有的 JSON 元素。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-478">This section provides details about JSON elements that are specific to each data store when it is used as a source/sink in a copy activity.</span></span>  

<span data-ttu-id="6dbb4-479">按一下您感興趣之存放區的連結，以查看連結服務的 JSON 結構描述、資料集，以及複製活動的來源/接收。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-479">Click the link for the store you are interested in to see the JSON schemas for linked service, dataset, and the source/sink for the copy activity.</span></span>

| <span data-ttu-id="6dbb4-480">類別</span><span class="sxs-lookup"><span data-stu-id="6dbb4-480">Category</span></span> | <span data-ttu-id="6dbb4-481">資料存放區</span><span class="sxs-lookup"><span data-stu-id="6dbb4-481">Data store</span></span> 
|:--- |:--- |
| <span data-ttu-id="6dbb4-482">**Azure**</span><span class="sxs-lookup"><span data-stu-id="6dbb4-482">**Azure**</span></span> |[<span data-ttu-id="6dbb4-483">Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="6dbb4-483">Azure Blob storage</span></span>](#azure-blob-storage) |
| &nbsp; |[<span data-ttu-id="6dbb4-484">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="6dbb4-484">Azure Data Lake Store</span></span>](#azure-datalake-store) |
| &nbsp; |[<span data-ttu-id="6dbb4-485">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6dbb4-485">Azure Cosmos DB</span></span>](#azure-cosmos-db) |
| &nbsp; |[<span data-ttu-id="6dbb4-486">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="6dbb4-486">Azure SQL Database</span></span>](#azure-sql-database) |
| &nbsp; |[<span data-ttu-id="6dbb4-487">Azure SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="6dbb4-487">Azure SQL Data Warehouse</span></span>](#azure-sql-data-warehouse) |
| &nbsp; |[<span data-ttu-id="6dbb4-488">Azure 搜尋服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-488">Azure Search</span></span>](#azure-search) |
| &nbsp; |[<span data-ttu-id="6dbb4-489">Azure 表格儲存體</span><span class="sxs-lookup"><span data-stu-id="6dbb4-489">Azure Table storage</span></span>](#azure-table-storage) |
| <span data-ttu-id="6dbb4-490">**資料庫**</span><span class="sxs-lookup"><span data-stu-id="6dbb4-490">**Databases**</span></span> |[<span data-ttu-id="6dbb4-491">Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="6dbb4-491">Amazon Redshift</span></span>](#amazon-redshift) |
| &nbsp; |[<span data-ttu-id="6dbb4-492">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="6dbb4-492">IBM DB2</span></span>](#ibm-db2) |
| &nbsp; |[<span data-ttu-id="6dbb4-493">MySQL</span><span class="sxs-lookup"><span data-stu-id="6dbb4-493">MySQL</span></span>](#mysql) |
| &nbsp; |[<span data-ttu-id="6dbb4-494">Oracle</span><span class="sxs-lookup"><span data-stu-id="6dbb4-494">Oracle</span></span>](#oracle) |
| &nbsp; |[<span data-ttu-id="6dbb4-495">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="6dbb4-495">PostgreSQL</span></span>](#postgresql) |
| &nbsp; |[<span data-ttu-id="6dbb4-496">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="6dbb4-496">SAP Business Warehouse</span></span>](#sap-business-warehouse) |
| &nbsp; |[<span data-ttu-id="6dbb4-497">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="6dbb4-497">SAP HANA</span></span>](#sap-hana) |
| &nbsp; |[<span data-ttu-id="6dbb4-498">SQL Server</span><span class="sxs-lookup"><span data-stu-id="6dbb4-498">SQL Server</span></span>](#sql-server) |
| &nbsp; |[<span data-ttu-id="6dbb4-499">Sybase</span><span class="sxs-lookup"><span data-stu-id="6dbb4-499">Sybase</span></span>](#sybase) |
| &nbsp; |[<span data-ttu-id="6dbb4-500">Teradata</span><span class="sxs-lookup"><span data-stu-id="6dbb4-500">Teradata</span></span>](#teradata) |
| <span data-ttu-id="6dbb4-501">**NoSQL**</span><span class="sxs-lookup"><span data-stu-id="6dbb4-501">**NoSQL**</span></span> |[<span data-ttu-id="6dbb4-502">Cassandra</span><span class="sxs-lookup"><span data-stu-id="6dbb4-502">Cassandra</span></span>](#cassandra) |
| &nbsp; |[<span data-ttu-id="6dbb4-503">MongoDB</span><span class="sxs-lookup"><span data-stu-id="6dbb4-503">MongoDB</span></span>](#mongodb) |
| <span data-ttu-id="6dbb4-504">**檔案**</span><span class="sxs-lookup"><span data-stu-id="6dbb4-504">**File**</span></span> |[<span data-ttu-id="6dbb4-505">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="6dbb4-505">Amazon S3</span></span>](#amazon-s3) |
| &nbsp; |[<span data-ttu-id="6dbb4-506">檔案系統</span><span class="sxs-lookup"><span data-stu-id="6dbb4-506">File System</span></span>](#file-system) |
| &nbsp; |[<span data-ttu-id="6dbb4-507">FTP</span><span class="sxs-lookup"><span data-stu-id="6dbb4-507">FTP</span></span>](#ftp) |
| &nbsp; |[<span data-ttu-id="6dbb4-508">HDFS</span><span class="sxs-lookup"><span data-stu-id="6dbb4-508">HDFS</span></span>](#hdfs) |
| &nbsp; |[<span data-ttu-id="6dbb4-509">SFTP</span><span class="sxs-lookup"><span data-stu-id="6dbb4-509">SFTP</span></span>](#sftp) |
| <span data-ttu-id="6dbb4-510">**其他**</span><span class="sxs-lookup"><span data-stu-id="6dbb4-510">**Others**</span></span> |[<span data-ttu-id="6dbb4-511">HTTP</span><span class="sxs-lookup"><span data-stu-id="6dbb4-511">HTTP</span></span>](#http) |
| &nbsp; |[<span data-ttu-id="6dbb4-512">OData</span><span class="sxs-lookup"><span data-stu-id="6dbb4-512">OData</span></span>](#odata) |
| &nbsp; |[<span data-ttu-id="6dbb4-513">ODBC</span><span class="sxs-lookup"><span data-stu-id="6dbb4-513">ODBC</span></span>](#odbc) |
| &nbsp; |[<span data-ttu-id="6dbb4-514">Salesforce</span><span class="sxs-lookup"><span data-stu-id="6dbb4-514">Salesforce</span></span>](#salesforce) |
| &nbsp; |[<span data-ttu-id="6dbb4-515">Web 資料表</span><span class="sxs-lookup"><span data-stu-id="6dbb4-515">Web Table</span></span>](#web-table) |

## <a name="azure-blob-storage"></a><span data-ttu-id="6dbb4-516">Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="6dbb4-516">Azure Blob Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="6dbb4-517">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-517">Linked service</span></span>
<span data-ttu-id="6dbb4-518">有兩種連結服務類型︰Azure 儲存體連結服務和 Azure 儲存體 SAS 連結服務。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-518">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="6dbb4-519">Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-519">Azure Storage Linked Service</span></span>
<span data-ttu-id="6dbb4-520">若要使用**帳戶金鑰**將 Azure 儲存體帳戶連結至資料處理站，請建立 Azure 儲存體連結服務。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-520">To link your Azure storage account to a data factory by using the **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="6dbb4-521">若要定義 Azure 儲存體連結服務，請將連結服務的**類型**設為 **AzureStorage**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-521">To define an Azure Storage linked service, set the **type** of the linked service to **AzureStorage**.</span></span> <span data-ttu-id="6dbb4-522">然後，您可以在 **typeProperties** 區段中指定下列屬性：</span><span class="sxs-lookup"><span data-stu-id="6dbb4-522">Then, you can specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="6dbb4-523">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-523">Property</span></span> | <span data-ttu-id="6dbb4-524">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-524">Description</span></span> | <span data-ttu-id="6dbb4-525">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-525">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="6dbb4-526">connectionString</span><span class="sxs-lookup"><span data-stu-id="6dbb4-526">connectionString</span></span> |<span data-ttu-id="6dbb4-527">針對 connectionString 屬性指定連接到 Azure 儲存體所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-527">Specify information needed to connect to Azure storage for the connectionString property.</span></span> |<span data-ttu-id="6dbb4-528">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-528">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="6dbb4-529">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-529">Example</span></span>  

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="6dbb4-530">Azure 儲存體 SAS 連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-530">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="6dbb4-531">Azure 儲存體 SAS 連結服務可讓您使用共用存取簽章 (SAS)，將 Azure 儲存體帳戶連結到 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-531">The Azure Storage SAS linked service allows you to link an Azure Storage Account to an Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="6dbb4-532">它提供受限制/時間界限存取權，讓資料處理站存取儲存體中的所有/特定資源 (blob/容器)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-532">It provides the data factory with restricted/time-bound access to all/specific resources (blob/container) in the storage.</span></span> <span data-ttu-id="6dbb4-533">若要使用共用存取簽章將 Azure 儲存體帳戶連結至資料處理站，請建立 Azure 儲存體 SAS 連結服務。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-533">To link your Azure storage account to a data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="6dbb4-534">若要定義 Azure 儲存體 SAS 連結服務，請將連結服務的**類型**設為 **AzureStorageSas**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-534">To define an Azure Storage SAS linked service, set the **type** of the linked service to **AzureStorageSas**.</span></span> <span data-ttu-id="6dbb4-535">然後，您可以在 **typeProperties** 區段中指定下列屬性：</span><span class="sxs-lookup"><span data-stu-id="6dbb4-535">Then, you can specify following properties in the **typeProperties** section:</span></span>   

| <span data-ttu-id="6dbb4-536">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-536">Property</span></span> | <span data-ttu-id="6dbb4-537">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-537">Description</span></span> | <span data-ttu-id="6dbb4-538">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-538">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="6dbb4-539">sasUri</span><span class="sxs-lookup"><span data-stu-id="6dbb4-539">sasUri</span></span> |<span data-ttu-id="6dbb4-540">指定 Azure 儲存體資源 (例如 Blob、容器或資料表) 的共用存取簽章 URI。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-540">Specify Shared Access Signature URI to the Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="6dbb4-541">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-541">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="6dbb4-542">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-542">Example</span></span>

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

<span data-ttu-id="6dbb4-543">如需這些連結服務的詳細資訊，請參閱 [Azure Blob 儲存體連接器](data-factory-azure-blob-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-543">For more information about these linked services, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="6dbb4-544">Dataset</span><span class="sxs-lookup"><span data-stu-id="6dbb4-544">Dataset</span></span>
<span data-ttu-id="6dbb4-545">若要定義 Azure Blob 資料集，請將資料集的 **type** 設為 **AzureBlob**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-545">To define an Azure Blob dataset, set the **type** of the dataset to **AzureBlob**.</span></span> <span data-ttu-id="6dbb4-546">然後，在 **typeProperties** 區段中指定下列 Azure Blob 特定屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-546">Then, specify the following Azure Blob specific properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="6dbb4-547">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-547">Property</span></span> | <span data-ttu-id="6dbb4-548">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-548">Description</span></span> | <span data-ttu-id="6dbb4-549">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-549">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-550">folderPath</span><span class="sxs-lookup"><span data-stu-id="6dbb4-550">folderPath</span></span> |<span data-ttu-id="6dbb4-551">Blob 儲存體中容器和資料夾的路徑。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-551">Path to the container and folder in the blob storage.</span></span> <span data-ttu-id="6dbb4-552">範例：myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="6dbb4-552">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="6dbb4-553">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-553">Yes</span></span> |
| <span data-ttu-id="6dbb4-554">fileName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-554">fileName</span></span> |<span data-ttu-id="6dbb4-555">Blob 的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-555">Name of the blob.</span></span> <span data-ttu-id="6dbb4-556">fileName 是選擇性的，而且區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-556">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="6dbb4-557">如果您指定檔案名稱，活動 (包括複製) 適用於特定的 Blob。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-557">If you specify a filename, the activity (including Copy) works on the specific Blob.</span></span><br/><br/><span data-ttu-id="6dbb4-558">如果您未指定 fileName，複製會包含 folderPath 中的所有 Blob 以做為輸入資料集。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-558">When fileName is not specified, Copy includes all Blobs in the folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="6dbb4-559">沒有為輸出資料集指定 fileName 時，所產生的檔案名稱會是下列格式：Data.<Guid>.txt (例如：Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="6dbb4-559">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="6dbb4-560">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-560">No</span></span> |
| <span data-ttu-id="6dbb4-561">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="6dbb4-561">partitionedBy</span></span> |<span data-ttu-id="6dbb4-562">partitionedBy 是選擇性的屬性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-562">partitionedBy is an optional property.</span></span> <span data-ttu-id="6dbb4-563">您可以用來指定時間序列資料的動態 folderPath 和 filename。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-563">You can use it to specify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="6dbb4-564">例如，folderPath 可針對每小時的資料進行參數化。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-564">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="6dbb4-565">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-565">No</span></span> |
| <span data-ttu-id="6dbb4-566">format</span><span class="sxs-lookup"><span data-stu-id="6dbb4-566">format</span></span> | <span data-ttu-id="6dbb4-567">支援下列格式類型：**TextFormat**、**JsonFormat**、**AvroFormat**、**OrcFormat**、**ParquetFormat**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-567">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="6dbb4-568">將格式下的 **type** 屬性設定為這些值其中之一。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-568">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="6dbb4-569">如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-569">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="6dbb4-570">如果您想要在以檔案為基礎的存放區之間**依原樣複製檔案** (二進位複本)，請在輸入和輸出資料集定義中略過格式區段。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-570">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="6dbb4-571">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-571">No</span></span> |
| <span data-ttu-id="6dbb4-572">compression</span><span class="sxs-lookup"><span data-stu-id="6dbb4-572">compression</span></span> | <span data-ttu-id="6dbb4-573">指定此資料的壓縮類型和層級。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-573">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="6dbb4-574">支援的類型為：**GZip**、**Deflate**、**BZip2** 及 **ZipDeflate**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-574">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="6dbb4-575">支援的層級為：**Optimal** 和 **Fastest**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-575">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="6dbb4-576">如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-576">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="6dbb4-577">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-577">No</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-578">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-578">Example</span></span>

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


<span data-ttu-id="6dbb4-579">如需詳細資訊，請參閱 [Azure Blob 連接器](data-factory-azure-blob-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-579">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#dataset-properties) article.</span></span>

### <a name="blobsource-in-copy-activity"></a><span data-ttu-id="6dbb4-580">複製活動中的 BlobSource</span><span class="sxs-lookup"><span data-stu-id="6dbb4-580">BlobSource in Copy Activity</span></span>
<span data-ttu-id="6dbb4-581">如果您從 Azure Blob 儲存體複製資料，請將複製活動的 **source type** 設為 **BlobSource**，並在 **source** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-581">If you are copying data from an Azure Blob Storage, set the **source type** of the copy activity to **BlobSource**, and specify following properties in the **source **section:</span></span>

| <span data-ttu-id="6dbb4-582">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-582">Property</span></span> | <span data-ttu-id="6dbb4-583">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-583">Description</span></span> | <span data-ttu-id="6dbb4-584">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-584">Allowed values</span></span> | <span data-ttu-id="6dbb4-585">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-585">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-586">遞迴</span><span class="sxs-lookup"><span data-stu-id="6dbb4-586">recursive</span></span> |<span data-ttu-id="6dbb4-587">表示是否從子資料夾，或只有從指定的資料夾，以遞迴方式讀取資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-587">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="6dbb4-588">True (預設值)、False</span><span class="sxs-lookup"><span data-stu-id="6dbb4-588">True (default value), False</span></span> |<span data-ttu-id="6dbb4-589">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-589">No</span></span> |

#### <a name="example-blobsource"></a><span data-ttu-id="6dbb4-590">範例︰BlobSource**</span><span class="sxs-lookup"><span data-stu-id="6dbb4-590">Example: BlobSource**</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
### <a name="blobsink-in-copy-activity"></a><span data-ttu-id="6dbb4-591">複製活動中的 BlobSink</span><span class="sxs-lookup"><span data-stu-id="6dbb4-591">BlobSink in Copy Activity</span></span>
<span data-ttu-id="6dbb4-592">如果您將資料複製到 Azure Blob 儲存體，請將複製活動的 **sink type** 設為 **BlobSink**，並在 **sink** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-592">If you are copying data to an Azure Blob Storage, set the **sink type** of the copy activity to **BlobSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="6dbb4-593">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-593">Property</span></span> | <span data-ttu-id="6dbb4-594">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-594">Description</span></span> | <span data-ttu-id="6dbb4-595">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-595">Allowed values</span></span> | <span data-ttu-id="6dbb4-596">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-596">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-597">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="6dbb4-597">copyBehavior</span></span> |<span data-ttu-id="6dbb4-598">當來源為 BlobSource 或 FileSystem 時，定義複製行為。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-598">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="6dbb4-599"><b>PreserveHierarchy</b>：保留目標資料夾中的檔案階層。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-599"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="6dbb4-600">來源檔案到來源資料夾的相對路徑，與目標檔案到目標資料夾的相對路徑相同。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-600">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="6dbb4-601"><b>FlattenHierarchy</b>：來自來源資料夾的所有檔案都在目標資料夾的第一層中。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-601"><b>FlattenHierarchy</b>: all files from the source folder are in the first level of target folder.</span></span> <span data-ttu-id="6dbb4-602">目標檔案會有自動產生的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-602">The target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="6dbb4-603"><b>MergeFiles (預設值)</b>：將來自來源資料夾的所有檔案合併成一個檔案。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-603"><b>MergeFiles (default):</b> merges all files from the source folder to one file.</span></span> <span data-ttu-id="6dbb4-604">如果已指定檔案/Blob 名稱，合併檔案名稱會是指定的名稱；否則，就會是自動產生的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-604">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="6dbb4-605">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-605">No</span></span> |

#### <a name="example-blobsink"></a><span data-ttu-id="6dbb4-606">範例︰BlobSink</span><span class="sxs-lookup"><span data-stu-id="6dbb4-606">Example: BlobSink</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="6dbb4-607">如需詳細資訊，請參閱 [Azure Blob 連接器](data-factory-azure-blob-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-607">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-data-lake-store"></a><span data-ttu-id="6dbb4-608">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="6dbb4-608">Azure Data Lake Store</span></span>

### <a name="linked-service"></a><span data-ttu-id="6dbb4-609">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-609">Linked service</span></span>
<span data-ttu-id="6dbb4-610">若要定義 Azure Data Lake Store 連結服務，請將連結服務的 type 設為 **AzureDataLakeStore**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-610">To define an Azure Data Lake Store linked service, set the type of the linked service to **AzureDataLakeStore**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="6dbb4-611">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-611">Property</span></span> | <span data-ttu-id="6dbb4-612">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-612">Description</span></span> | <span data-ttu-id="6dbb4-613">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-613">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="6dbb4-614">類型</span><span class="sxs-lookup"><span data-stu-id="6dbb4-614">type</span></span> | <span data-ttu-id="6dbb4-615">type 屬性必須設為： **AzureDataLakeStore**</span><span class="sxs-lookup"><span data-stu-id="6dbb4-615">The type property must be set to: **AzureDataLakeStore**</span></span> | <span data-ttu-id="6dbb4-616">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-616">Yes</span></span> |
| <span data-ttu-id="6dbb4-617">dataLakeStoreUri</span><span class="sxs-lookup"><span data-stu-id="6dbb4-617">dataLakeStoreUri</span></span> | <span data-ttu-id="6dbb4-618">指定有關 Azure Data Lake Store 帳戶的資訊。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-618">Specify information about the Azure Data Lake Store account.</span></span> <span data-ttu-id="6dbb4-619">它的格式如下：`https://[accountname].azuredatalakestore.net/webhdfs/v1` 或 `adl://[accountname].azuredatalakestore.net/`。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-619">It is in the following format: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="6dbb4-620">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-620">Yes</span></span> |
| <span data-ttu-id="6dbb4-621">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="6dbb4-621">subscriptionId</span></span> | <span data-ttu-id="6dbb4-622">Data Lake Store 所屬的 Azure 訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-622">Azure subscription Id to which Data Lake Store belongs.</span></span> | <span data-ttu-id="6dbb4-623">接收 (Sink) 的必要項目</span><span class="sxs-lookup"><span data-stu-id="6dbb4-623">Required for sink</span></span> |
| <span data-ttu-id="6dbb4-624">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-624">resourceGroupName</span></span> | <span data-ttu-id="6dbb4-625">Data Lake Store 所屬的 Azure 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-625">Azure resource group name to which Data Lake Store belongs.</span></span> | <span data-ttu-id="6dbb4-626">接收 (Sink) 的必要項目</span><span class="sxs-lookup"><span data-stu-id="6dbb4-626">Required for sink</span></span> |
| <span data-ttu-id="6dbb4-627">servicePrincipalId</span><span class="sxs-lookup"><span data-stu-id="6dbb4-627">servicePrincipalId</span></span> | <span data-ttu-id="6dbb4-628">指定應用程式的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-628">Specify the application's client ID.</span></span> | <span data-ttu-id="6dbb4-629">是 (適用於服務主體驗證)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-629">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="6dbb4-630">servicePrincipalKey</span><span class="sxs-lookup"><span data-stu-id="6dbb4-630">servicePrincipalKey</span></span> | <span data-ttu-id="6dbb4-631">指定應用程式的金鑰。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-631">Specify the application's key.</span></span> | <span data-ttu-id="6dbb4-632">是 (適用於服務主體驗證)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-632">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="6dbb4-633">tenant</span><span class="sxs-lookup"><span data-stu-id="6dbb4-633">tenant</span></span> | <span data-ttu-id="6dbb4-634">指定您的應用程式所在租用戶的資訊 (網域名稱或租用戶識別碼)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-634">Specify the tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="6dbb4-635">將滑鼠游標暫留在 Azure 入口網站右上角，即可擷取它。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-635">You can retrieve it by hovering the mouse in the top-right corner of the Azure portal.</span></span> | <span data-ttu-id="6dbb4-636">是 (適用於服務主體驗證)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-636">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="6dbb4-637">授權</span><span class="sxs-lookup"><span data-stu-id="6dbb4-637">authorization</span></span> | <span data-ttu-id="6dbb4-638">按一下 [Data Factory 編輯器] 中的 [授權] 按鈕，然後輸入您的認證，此動作會將自動產生的授權 URL 指派給此屬性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-638">Click **Authorize** button in the **Data Factory Editor** and enter your credential that assigns the auto-generated authorization URL to this property.</span></span> | <span data-ttu-id="6dbb4-639">是 (適用於使用者認證驗證)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-639">Yes (for user credential authentication)</span></span>|
| <span data-ttu-id="6dbb4-640">sessionId</span><span class="sxs-lookup"><span data-stu-id="6dbb4-640">sessionId</span></span> | <span data-ttu-id="6dbb4-641">OAuth 授權工作階段的 OAuth 工作階段識別碼。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-641">OAuth session id from the OAuth authorization session.</span></span> <span data-ttu-id="6dbb4-642">每個工作階段識別碼都是唯一的，只能使用一次。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-642">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="6dbb4-643">當您使用 Data Factory 編輯器時便會自動產生此設定。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-643">This setting is automatically generated when you use Data Factory Editor.</span></span> | <span data-ttu-id="6dbb4-644">是 (適用於使用者認證驗證)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-644">Yes (for user credential authentication)</span></span> |

#### <a name="example-using-service-principal-authentication"></a><span data-ttu-id="6dbb4-645">範例：使用服務主體驗證</span><span class="sxs-lookup"><span data-stu-id="6dbb4-645">Example: using service principal authentication</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info. Example: microsoft.onmicrosoft.com>"
        }
    }
}
```

#### <a name="example-using-user-credential-authentication"></a><span data-ttu-id="6dbb4-646">範例︰使用使用者認證驗證</span><span class="sxs-lookup"><span data-stu-id="6dbb4-646">Example: using user credential authentication</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

<span data-ttu-id="6dbb4-647">如需詳細資訊，請參閱 [Azure Data Lake Store 連接器](data-factory-azure-datalake-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-647">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="6dbb4-648">Dataset</span><span class="sxs-lookup"><span data-stu-id="6dbb4-648">Dataset</span></span>
<span data-ttu-id="6dbb4-649">若要定義 Azure Data Lake Store 資料集，請將資料集的 **type** 設為 **AzureDataLakeStore**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-649">To define an Azure Data Lake Store dataset, set the **type** of the dataset to **AzureDataLakeStore**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="6dbb4-650">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-650">Property</span></span> | <span data-ttu-id="6dbb4-651">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-651">Description</span></span> | <span data-ttu-id="6dbb4-652">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-652">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="6dbb4-653">folderPath</span><span class="sxs-lookup"><span data-stu-id="6dbb4-653">folderPath</span></span> |<span data-ttu-id="6dbb4-654">Azure Data Lake Store 中容器與資料夾的路徑。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-654">Path to the container and folder in the Azure Data Lake store.</span></span> |<span data-ttu-id="6dbb4-655">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-655">Yes</span></span> |
| <span data-ttu-id="6dbb4-656">fileName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-656">fileName</span></span> |<span data-ttu-id="6dbb4-657">Azure Data Lake Store 中的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-657">Name of the file in the Azure Data Lake store.</span></span> <span data-ttu-id="6dbb4-658">fileName 是選擇性的，而且區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-658">fileName is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="6dbb4-659">如果您指定檔案名稱，活動 (包括複製) 適用於特定的檔案。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-659">If you specify a filename, the activity (including Copy) works on the specific file.</span></span><br/><br/><span data-ttu-id="6dbb4-660">如果您未指定 fileName，複製會包含 folderPath 中的所有檔案以做為輸入資料集。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-660">When fileName is not specified, Copy includes all files in the folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="6dbb4-661">沒有為輸出資料集指定 fileName 時，所產生的檔案名稱會是下列格式：Data<Guid>.txt (例如：Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="6dbb4-661">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="6dbb4-662">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-662">No</span></span> |
| <span data-ttu-id="6dbb4-663">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="6dbb4-663">partitionedBy</span></span> |<span data-ttu-id="6dbb4-664">partitionedBy 是選擇性的屬性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-664">partitionedBy is an optional property.</span></span> <span data-ttu-id="6dbb4-665">您可以用來指定時間序列資料的動態 folderPath 和 filename。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-665">You can use it to specify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="6dbb4-666">例如，folderPath 可針對每小時的資料進行參數化。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-666">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="6dbb4-667">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-667">No</span></span> |
| <span data-ttu-id="6dbb4-668">format</span><span class="sxs-lookup"><span data-stu-id="6dbb4-668">format</span></span> | <span data-ttu-id="6dbb4-669">支援下列格式類型：**TextFormat**、**JsonFormat**、**AvroFormat**、**OrcFormat**、**ParquetFormat**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-669">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="6dbb4-670">將格式下的 **type** 屬性設定為這些值其中之一。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-670">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="6dbb4-671">如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-671">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="6dbb4-672">如果您想要在以檔案為基礎的存放區之間**依原樣複製檔案** (二進位複本)，請在輸入和輸出資料集定義中略過格式區段。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-672">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="6dbb4-673">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-673">No</span></span> |
| <span data-ttu-id="6dbb4-674">compression</span><span class="sxs-lookup"><span data-stu-id="6dbb4-674">compression</span></span> | <span data-ttu-id="6dbb4-675">指定此資料的壓縮類型和層級。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-675">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="6dbb4-676">支援的類型為：**GZip**、**Deflate**、**BZip2** 及 **ZipDeflate**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-676">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="6dbb4-677">支援的層級為：**Optimal** 和 **Fastest**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-677">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="6dbb4-678">如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-678">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="6dbb4-679">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-679">No</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-680">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-680">Example</span></span>
```json
{
    "name": "AzureDataLakeStoreInput",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="6dbb4-681">如需詳細資訊，請參閱 [Azure Data Lake Store 連接器](data-factory-azure-datalake-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-681">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-data-lake-store-source-in-copy-activity"></a><span data-ttu-id="6dbb4-682">複製活動中的 Azure Data Lake Store 來源</span><span class="sxs-lookup"><span data-stu-id="6dbb4-682">Azure Data Lake Store Source in Copy Activity</span></span>
<span data-ttu-id="6dbb4-683">如果您從 Azure Data Lake Store 複製資料，請將複製活動的 **source type** 設為 **AzureDataLakeStoreSource**，並在 **source** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-683">If you are copying data from an Azure Data Lake Store, set the **source type** of the copy activity to **AzureDataLakeStoreSource**, and specify following properties in the **source** section:</span></span>

<span data-ttu-id="6dbb4-684">**AzureDataLakeStoreSource** 支援下列屬性 **typeProperties** 區段：</span><span class="sxs-lookup"><span data-stu-id="6dbb4-684">**AzureDataLakeStoreSource** supports the following properties **typeProperties** section:</span></span>

| <span data-ttu-id="6dbb4-685">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-685">Property</span></span> | <span data-ttu-id="6dbb4-686">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-686">Description</span></span> | <span data-ttu-id="6dbb4-687">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-687">Allowed values</span></span> | <span data-ttu-id="6dbb4-688">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-688">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-689">遞迴</span><span class="sxs-lookup"><span data-stu-id="6dbb4-689">recursive</span></span> |<span data-ttu-id="6dbb4-690">表示是否從子資料夾，或只有從指定的資料夾，以遞迴方式讀取資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-690">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="6dbb4-691">True (預設值)、False</span><span class="sxs-lookup"><span data-stu-id="6dbb4-691">True (default value), False</span></span> |<span data-ttu-id="6dbb4-692">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-692">No</span></span> |

#### <a name="example-azuredatalakestoresource"></a><span data-ttu-id="6dbb4-693">範例：AzureDataLakeStoreSource</span><span class="sxs-lookup"><span data-stu-id="6dbb4-693">Example: AzureDataLakeStoreSource</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureDakeLaketoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureDataLakeStoreInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureDataLakeStoreSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="6dbb4-694">如需詳細資訊，請參閱 [Azure Data Lake Store 連接器](data-factory-azure-datalake-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-694">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span>

### <a name="azure-data-lake-store-sink-in-copy-activity"></a><span data-ttu-id="6dbb4-695">複製活動中的 Azure Data Lake Store 接收</span><span class="sxs-lookup"><span data-stu-id="6dbb4-695">Azure Data Lake Store Sink in Copy Activity</span></span>
<span data-ttu-id="6dbb4-696">如果您將資料複製到 Azure Data Lake Store，請將複製活動的 **sink type** 設為 **AzureDataLakeStoreSink**，並在 **sink** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-696">If you are copying data to an Azure Data Lake Store, set the **sink type** of the copy activity to **AzureDataLakeStoreSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="6dbb4-697">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-697">Property</span></span> | <span data-ttu-id="6dbb4-698">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-698">Description</span></span> | <span data-ttu-id="6dbb4-699">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-699">Allowed values</span></span> | <span data-ttu-id="6dbb4-700">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-700">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-701">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="6dbb4-701">copyBehavior</span></span> |<span data-ttu-id="6dbb4-702">指定複製行為。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-702">Specifies the copy behavior.</span></span> |<span data-ttu-id="6dbb4-703"><b>PreserveHierarchy</b>：保留目標資料夾中的檔案階層。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-703"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="6dbb4-704">來源檔案到來源資料夾的相對路徑，與目標檔案到目標資料夾的相對路徑相同。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-704">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="6dbb4-705"><b>FlattenHierarchy</b>：來源資料夾的中所有檔案都會建立在目標資料夾的第一個層級中。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-705"><b>FlattenHierarchy</b>: all files from the source folder are created in the first level of target folder.</span></span> <span data-ttu-id="6dbb4-706">建立的目標檔案會具有自動產生的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-706">The target files are created with auto generated name.</span></span><br/><br/><span data-ttu-id="6dbb4-707"><b>MergeFiles</b>：將來源資料夾的所有檔案合併為一個檔案。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-707"><b>MergeFiles</b>: merges all files from the source folder to one file.</span></span> <span data-ttu-id="6dbb4-708">如果已指定檔案/Blob 名稱，合併檔案名稱會是指定的名稱；否則，就會是自動產生的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-708">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="6dbb4-709">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-709">No</span></span> |

#### <a name="example-azuredatalakestoresink"></a><span data-ttu-id="6dbb4-710">範例：AzureDataLakeStoreSink</span><span class="sxs-lookup"><span data-stu-id="6dbb4-710">Example: AzureDataLakeStoreSink</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoDataLake",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureDataLakeStoreOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureDataLakeStoreSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="6dbb4-711">如需詳細資訊，請參閱 [Azure Data Lake Store 連接器](data-factory-azure-datalake-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-711">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-cosmos-db"></a><span data-ttu-id="6dbb4-712">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6dbb4-712">Azure Cosmos DB</span></span>  

### <a name="linked-service"></a><span data-ttu-id="6dbb4-713">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-713">Linked service</span></span>
<span data-ttu-id="6dbb4-714">若要定義 Azure Cosmos DB 連結服務，請將連結服務的 **type** 設定為 **DocumentDb**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-714">To define an Azure Cosmos DB linked service, set the **type** of the linked service to **DocumentDb**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="6dbb4-715">**屬性**</span><span class="sxs-lookup"><span data-stu-id="6dbb4-715">**Property**</span></span> | <span data-ttu-id="6dbb4-716">**說明**</span><span class="sxs-lookup"><span data-stu-id="6dbb4-716">**Description**</span></span> | <span data-ttu-id="6dbb4-717">**必要**</span><span class="sxs-lookup"><span data-stu-id="6dbb4-717">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-718">connectionString</span><span class="sxs-lookup"><span data-stu-id="6dbb4-718">connectionString</span></span> |<span data-ttu-id="6dbb4-719">指定連接到 Azure Cosmos DB 資料庫所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-719">Specify information needed to connect to Azure Cosmos DB database.</span></span> |<span data-ttu-id="6dbb4-720">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-720">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-721">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-721">Example</span></span>

```json
{
    "name": "CosmosDBLinkedService",
    "properties": {
        "type": "DocumentDb",
        "typeProperties": {
            "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
        }
    }
}
```
<span data-ttu-id="6dbb4-722">如需詳細資訊，請參閱 [Azure Cosmos DB 連接器](data-factory-azure-documentdb-connector.md#linked-service-properties)一文。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-722">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="6dbb4-723">Dataset</span><span class="sxs-lookup"><span data-stu-id="6dbb4-723">Dataset</span></span>
<span data-ttu-id="6dbb4-724">若要定義 Azure Cosmos DB 資料集，請將資料集的 **type** 設定為 **DocumentDbCollection**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-724">To define an Azure Cosmos DB dataset, set the **type** of the dataset to **DocumentDbCollection**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="6dbb4-725">**屬性**</span><span class="sxs-lookup"><span data-stu-id="6dbb4-725">**Property**</span></span> | <span data-ttu-id="6dbb4-726">**說明**</span><span class="sxs-lookup"><span data-stu-id="6dbb4-726">**Description**</span></span> | <span data-ttu-id="6dbb4-727">**必要**</span><span class="sxs-lookup"><span data-stu-id="6dbb4-727">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-728">collectionName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-728">collectionName</span></span> |<span data-ttu-id="6dbb4-729">Azure Cosmos DB 集合的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-729">Name of the Azure Cosmos DB collection.</span></span> |<span data-ttu-id="6dbb4-730">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-730">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-731">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-731">Example</span></span>

```json
{
    "name": "PersonCosmosDBTable",
    "properties": {
        "type": "DocumentDbCollection",
        "linkedServiceName": "CosmosDBLinkedService",
        "typeProperties": {
            "collectionName": "Person"
        },
        "external": true,
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```
<span data-ttu-id="6dbb4-732">如需詳細資訊，請參閱 [Azure Cosmos DB 連接器](data-factory-azure-documentdb-connector.md#dataset-properties)一文。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-732">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#dataset-properties) article.</span></span>

### <a name="azure-cosmos-db-collection-source-in-copy-activity"></a><span data-ttu-id="6dbb4-733">複製活動中的 Azure Cosmos DB 集合來源</span><span class="sxs-lookup"><span data-stu-id="6dbb4-733">Azure Cosmos DB Collection Source in Copy Activity</span></span>
<span data-ttu-id="6dbb4-734">如果您要從 Azure Cosmos DB 複製資料，請將複製活動的 **source type** 設定為 **DocumentDbCollectionSource**，並在 **source** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-734">If you are copying data from an Azure Cosmos DB, set the **source type** of the copy activity to **DocumentDbCollectionSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="6dbb4-735">**屬性**</span><span class="sxs-lookup"><span data-stu-id="6dbb4-735">**Property**</span></span> | <span data-ttu-id="6dbb4-736">**說明**</span><span class="sxs-lookup"><span data-stu-id="6dbb4-736">**Description**</span></span> | <span data-ttu-id="6dbb4-737">**允許的值**</span><span class="sxs-lookup"><span data-stu-id="6dbb4-737">**Allowed values**</span></span> | <span data-ttu-id="6dbb4-738">**必要**</span><span class="sxs-lookup"><span data-stu-id="6dbb4-738">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-739">query</span><span class="sxs-lookup"><span data-stu-id="6dbb4-739">query</span></span> |<span data-ttu-id="6dbb4-740">指定查詢來讀取資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-740">Specify the query to read data.</span></span> |<span data-ttu-id="6dbb4-741">Azure Cosmos DB 所支援的查詢字串。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-741">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="6dbb4-742">範例： `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="6dbb4-742">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="6dbb4-743">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-743">No</span></span> <br/><br/><span data-ttu-id="6dbb4-744">如果未指定，執行的 SQL 陳述式：`select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="6dbb4-744">If not specified, the SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="6dbb4-745">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="6dbb4-745">nestingSeparator</span></span> |<span data-ttu-id="6dbb4-746">用來表示文件為巢狀文件的特殊字元</span><span class="sxs-lookup"><span data-stu-id="6dbb4-746">Special character to indicate that the document is nested</span></span> |<span data-ttu-id="6dbb4-747">任何字元。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-747">Any character.</span></span> <br/><br/><span data-ttu-id="6dbb4-748">Azure Cosmos DB 是 JSON 文件的 NoSQL 存放區 (允許巢狀結構)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-748">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="6dbb4-749">Azure Data Factory 可讓使用者透過 nestingSeparator (也就是上述範例中的 “.”) 表示階層</span><span class="sxs-lookup"><span data-stu-id="6dbb4-749">Azure Data Factory enables user to denote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="6dbb4-750">。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-750">in the above examples.</span></span> <span data-ttu-id="6dbb4-751">使用分隔符號，複製活動將會根據資料表定義中的 “Name.First”、“Name.Middle” 和 “Name.Last”，產生含有三個子元素 (First、Middle 和 Last) 的 "Name" 物件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-751">With the separator, the copy activity will generate the “Name” object with three children elements First, Middle and Last, according to “Name.First”, “Name.Middle” and “Name.Last” in the table definition.</span></span> |<span data-ttu-id="6dbb4-752">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-752">No</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-753">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-753">Example</span></span>

```json
{
    "name": "DocDbToBlobPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "DocumentDbCollectionSource",
                    "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
                    "nestingSeparator": "."
                },
                "sink": {
                    "type": "BlobSink",
                    "blobWriterAddHeader": true,
                    "writeBatchSize": 1000,
                    "writeBatchTimeout": "00:00:59"
                }
            },
            "inputs": [{
                "name": "PersonCosmosDBTable"
            }],
            "outputs": [{
                "name": "PersonBlobTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromCosmosDbToBlob"
        }],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00"
    }
}
```

### <a name="azure-cosmos-db-collection-sink-in-copy-activity"></a><span data-ttu-id="6dbb4-754">複製活動中的 Azure Cosmos DB 集合接收器</span><span class="sxs-lookup"><span data-stu-id="6dbb4-754">Azure Cosmos DB Collection Sink in Copy Activity</span></span>
<span data-ttu-id="6dbb4-755">如果您要將資料複製到 Azure Cosmos DB，請將複製活動的 **sink type** 設定為 **DocumentDbCollectionSink**，並在 **sink** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-755">If you are copying data to Azure Cosmos DB, set the **sink type** of the copy activity to **DocumentDbCollectionSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="6dbb4-756">**屬性**</span><span class="sxs-lookup"><span data-stu-id="6dbb4-756">**Property**</span></span> | <span data-ttu-id="6dbb4-757">**說明**</span><span class="sxs-lookup"><span data-stu-id="6dbb4-757">**Description**</span></span> | <span data-ttu-id="6dbb4-758">**允許的值**</span><span class="sxs-lookup"><span data-stu-id="6dbb4-758">**Allowed values**</span></span> | <span data-ttu-id="6dbb4-759">**必要**</span><span class="sxs-lookup"><span data-stu-id="6dbb4-759">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-760">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="6dbb4-760">nestingSeparator</span></span> |<span data-ttu-id="6dbb4-761">來源資料行名稱中用來表示需要巢狀文件的特殊字元。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-761">A special character in the source column name to indicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="6dbb4-762">就上述範例而言：輸出資料表中的 `Name.First` 會在 Cosmos DB 文件中產生下列 JSON 結構：</span><span class="sxs-lookup"><span data-stu-id="6dbb4-762">For example above: `Name.First` in the output table produces the following JSON structure in the Cosmos DB document:</span></span><br/><br/><span data-ttu-id="6dbb4-763">"Name": {</span><span class="sxs-lookup"><span data-stu-id="6dbb4-763">"Name": {</span></span><br/>    <span data-ttu-id="6dbb4-764">"First": "John"</span><span class="sxs-lookup"><span data-stu-id="6dbb4-764">"First": "John"</span></span><br/><span data-ttu-id="6dbb4-765">},</span><span class="sxs-lookup"><span data-stu-id="6dbb4-765">},</span></span> |<span data-ttu-id="6dbb4-766">用來分隔巢狀層級的字元。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-766">Character that is used to separate nesting levels.</span></span><br/><br/><span data-ttu-id="6dbb4-767">預設值為 `.` (點)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-767">Default value is `.` (dot).</span></span> |<span data-ttu-id="6dbb4-768">用來分隔巢狀層級的字元。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-768">Character that is used to separate nesting levels.</span></span> <br/><br/><span data-ttu-id="6dbb4-769">預設值為 `.` (點)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-769">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="6dbb4-770">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="6dbb4-770">writeBatchSize</span></span> |<span data-ttu-id="6dbb4-771">為了建立文件而傳送到 Azure Cosmos DB 服務的平行要求數目。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-771">Number of parallel requests to Azure Cosmos DB service to create documents.</span></span><br/><br/><span data-ttu-id="6dbb4-772">您可以在將資料複製到 Azure Cosmos DB 或從該處複製資料時，使用這個屬性來微調效能。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-772">You can fine-tune the performance when copying data to/from Azure Cosmos DB by using this property.</span></span> <span data-ttu-id="6dbb4-773">增大 writeBatchSize 的值時，預期可以提升效能，因為會對 Azure Cosmos DB 傳送更多平行要求。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-773">You can expect a better performance when you increase writeBatchSize because more parallel requests to Azure Cosmos DB are sent.</span></span> <span data-ttu-id="6dbb4-774">不過，您必須避免可能擲回錯誤訊息的節流：「要求速率很高」。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-774">However you’ll need to avoid throttling that can throw the error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="6dbb4-775">節流是由許多因素所決定，包括文件大小、文件中的詞彙數目、目標集合的檢索原則等。對於複製作業，您可以使用更好的集合 (例如 S3) 以取得最多可用輸送量 (2,500 要求單位/秒)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-775">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (for example, S3) to have the most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="6dbb4-776">Integer</span><span class="sxs-lookup"><span data-stu-id="6dbb4-776">Integer</span></span> |<span data-ttu-id="6dbb4-777">否 (預設值：5)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-777">No (default: 5)</span></span> |
| <span data-ttu-id="6dbb4-778">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="6dbb4-778">writeBatchTimeout</span></span> |<span data-ttu-id="6dbb4-779">在逾時前等待作業完成的時間。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-779">Wait time for the operation to complete before it times out.</span></span> |<span data-ttu-id="6dbb4-780">時間範圍</span><span class="sxs-lookup"><span data-stu-id="6dbb4-780">timespan</span></span><br/><br/> <span data-ttu-id="6dbb4-781">範例：“00:30:00” (30 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-781">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="6dbb4-782">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-782">No</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-783">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-783">Example</span></span>

```json
{
    "name": "BlobToDocDbPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "DocumentDbCollectionSink",
                    "nestingSeparator": ".",
                    "writeBatchSize": 2,
                    "writeBatchTimeout": "00:00:00"
                },
                "translator": {
                    "type": "TabularTranslator",
                    "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, Title: Title, Suffix: Suffix"
                }
            },
            "inputs": [{
                "name": "PersonBlobTableIn"
            }],
            "outputs": [{
                "name": "PersonCosmosDbTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromBlobToCosmosDb"
        }],
        "start": "2016-04-14T00:00:00",
        "end": "2016-04-15T00:00:00"
    }
}
```

<span data-ttu-id="6dbb4-784">如需詳細資訊，請參閱 [Azure Cosmos DB 連接器](data-factory-azure-documentdb-connector.md#copy-activity-properties)一文。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-784">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="6dbb4-785">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="6dbb4-785">Azure SQL Database</span></span>

### <a name="linked-service"></a><span data-ttu-id="6dbb4-786">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-786">Linked service</span></span>
<span data-ttu-id="6dbb4-787">若要定義 Azure SQL Database 連結服務，請將連結服務的 **type** 設為 **AzureSqlDatabase**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-787">To define an Azure SQL Database linked service, set the **type** of the linked service to **AzureSqlDatabase**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="6dbb4-788">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-788">Property</span></span> | <span data-ttu-id="6dbb4-789">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-789">Description</span></span> | <span data-ttu-id="6dbb4-790">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-790">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-791">connectionString</span><span class="sxs-lookup"><span data-stu-id="6dbb4-791">connectionString</span></span> |<span data-ttu-id="6dbb4-792">針對 connectionString 屬性指定連接到 Azure SQL Database 執行個體所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-792">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span></span> |<span data-ttu-id="6dbb4-793">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-793">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-794">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-794">Example</span></span>
```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="6dbb4-795">如需詳細資訊，請參閱 [Azure SQL 連接器](data-factory-azure-sql-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-795">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="6dbb4-796">Dataset</span><span class="sxs-lookup"><span data-stu-id="6dbb4-796">Dataset</span></span>
<span data-ttu-id="6dbb4-797">若要定義 Azure SQL Database 資料集，請將資料集的 **type** 設為 **AzureSqlTable**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-797">To define an Azure SQL Database dataset, set the **type** of the dataset to **AzureSqlTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="6dbb4-798">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-798">Property</span></span> | <span data-ttu-id="6dbb4-799">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-799">Description</span></span> | <span data-ttu-id="6dbb4-800">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-800">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-801">tableName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-801">tableName</span></span> |<span data-ttu-id="6dbb4-802">Azure SQL Database 執行個體中連結服務所參考的資料表或檢視的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-802">Name of the table or view in the Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="6dbb4-803">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-803">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-804">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-804">Example</span></span>

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="6dbb4-805">如需詳細資訊，請參閱 [Azure SQL 連接器](data-factory-azure-sql-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-805">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="6dbb4-806">複製活動中的 SQL 來源</span><span class="sxs-lookup"><span data-stu-id="6dbb4-806">SQL Source in Copy Activity</span></span>
<span data-ttu-id="6dbb4-807">如果您從 Azure SQL Database 複製資料，請將複製活動的 **source type** 設為 **SqlSource**，並在 **source** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-807">If you are copying data from an Azure SQL Database, set the **source type** of the copy activity to **SqlSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="6dbb4-808">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-808">Property</span></span> | <span data-ttu-id="6dbb4-809">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-809">Description</span></span> | <span data-ttu-id="6dbb4-810">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-810">Allowed values</span></span> | <span data-ttu-id="6dbb4-811">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-811">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-812">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="6dbb4-812">sqlReaderQuery</span></span> |<span data-ttu-id="6dbb4-813">使用自訂查詢來讀取資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-813">Use the custom query to read data.</span></span> |<span data-ttu-id="6dbb4-814">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-814">SQL query string.</span></span> <span data-ttu-id="6dbb4-815">範例： `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="6dbb4-815">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="6dbb4-816">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-816">No</span></span> |
| <span data-ttu-id="6dbb4-817">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-817">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="6dbb4-818">從來源資料表讀取資料的預存程序名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-818">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="6dbb4-819">預存程序的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-819">Name of the stored procedure.</span></span> |<span data-ttu-id="6dbb4-820">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-820">No</span></span> |
| <span data-ttu-id="6dbb4-821">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="6dbb4-821">storedProcedureParameters</span></span> |<span data-ttu-id="6dbb4-822">預存程序的參數。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-822">Parameters for the stored procedure.</span></span> |<span data-ttu-id="6dbb4-823">名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-823">Name/value pairs.</span></span> <span data-ttu-id="6dbb4-824">參數的名稱和大小寫必須符合預存程序參數的名稱和大小寫。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-824">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="6dbb4-825">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-825">No</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-826">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-826">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="6dbb4-827">如需詳細資訊，請參閱 [Azure SQL 連接器](data-factory-azure-sql-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-827">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="6dbb4-828">複製活動中的 SQL 接收</span><span class="sxs-lookup"><span data-stu-id="6dbb4-828">SQL Sink in Copy Activity</span></span>
<span data-ttu-id="6dbb4-829">如果您將資料複製到 Azure SQL Database，請將複製活動的 **sink type** 設為 **SqlSink**，並在 **sink** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-829">If you are copying data to Azure SQL Database, set the **sink type** of the copy activity to **SqlSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="6dbb4-830">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-830">Property</span></span> | <span data-ttu-id="6dbb4-831">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-831">Description</span></span> | <span data-ttu-id="6dbb4-832">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-832">Allowed values</span></span> | <span data-ttu-id="6dbb4-833">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-833">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-834">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="6dbb4-834">writeBatchTimeout</span></span> |<span data-ttu-id="6dbb4-835">在逾時前等待批次插入作業完成的時間。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-835">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="6dbb4-836">時間範圍</span><span class="sxs-lookup"><span data-stu-id="6dbb4-836">timespan</span></span><br/><br/> <span data-ttu-id="6dbb4-837">範例：“00:30:00” (30 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-837">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="6dbb4-838">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-838">No</span></span> |
| <span data-ttu-id="6dbb4-839">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="6dbb4-839">writeBatchSize</span></span> |<span data-ttu-id="6dbb4-840">當緩衝區大小達到 writeBatchSize 時，將資料插入 SQL 資料表中</span><span class="sxs-lookup"><span data-stu-id="6dbb4-840">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="6dbb4-841">整數 (資料列數目)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-841">Integer (number of rows)</span></span> |<span data-ttu-id="6dbb4-842">否 (預設值：10000)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-842">No (default: 10000)</span></span> |
| <span data-ttu-id="6dbb4-843">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="6dbb4-843">sqlWriterCleanupScript</span></span> |<span data-ttu-id="6dbb4-844">指定要讓「複製活動」執行的查詢，以便清除特定分割的資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-844">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="6dbb4-845">查詢陳述式。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-845">A query statement.</span></span> |<span data-ttu-id="6dbb4-846">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-846">No</span></span> |
| <span data-ttu-id="6dbb4-847">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-847">sliceIdentifierColumnName</span></span> |<span data-ttu-id="6dbb4-848">指定要讓「複製活動」以自動產生的分割識別碼填入的資料行名稱，這可在重新執行時用來清除特定分割的資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-848">Specify a column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="6dbb4-849">資料類型為 binary(32) 之資料行的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-849">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="6dbb4-850">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-850">No</span></span> |
| <span data-ttu-id="6dbb4-851">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-851">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="6dbb4-852">將資料更新插入 (更新/插入) 目標資料表中的預存程序名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-852">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="6dbb4-853">預存程序的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-853">Name of the stored procedure.</span></span> |<span data-ttu-id="6dbb4-854">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-854">No</span></span> |
| <span data-ttu-id="6dbb4-855">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="6dbb4-855">storedProcedureParameters</span></span> |<span data-ttu-id="6dbb4-856">預存程序的參數。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-856">Parameters for the stored procedure.</span></span> |<span data-ttu-id="6dbb4-857">名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-857">Name/value pairs.</span></span> <span data-ttu-id="6dbb4-858">參數的名稱和大小寫必須符合預存程序參數的名稱和大小寫。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-858">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="6dbb4-859">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-859">No</span></span> |
| <span data-ttu-id="6dbb4-860">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="6dbb4-860">sqlWriterTableType</span></span> |<span data-ttu-id="6dbb4-861">指定要在預存程序中使用的資料表類型名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-861">Specify a table type name to be used in the stored procedure.</span></span> <span data-ttu-id="6dbb4-862">複製活動可讓正在移動的資料可用於此資料表類型的暫存資料表。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-862">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="6dbb4-863">然後，預存程序程式碼可以合併正在複製的資料與現有的資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-863">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="6dbb4-864">資料表類型名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-864">A table type name.</span></span> |<span data-ttu-id="6dbb4-865">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-865">No</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-866">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-866">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="6dbb4-867">如需詳細資訊，請參閱 [Azure SQL 連接器](data-factory-azure-sql-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-867">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="6dbb4-868">Azure SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="6dbb4-868">Azure SQL Data Warehouse</span></span>

### <a name="linked-service"></a><span data-ttu-id="6dbb4-869">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-869">Linked service</span></span>
<span data-ttu-id="6dbb4-870">若要定義 Azure SQL 資料倉儲連結服務，請將連結服務的 **type** 設為 **AzureSqlDW**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-870">To define an Azure SQL Data Warehouse linked service, set the **type** of the linked service to **AzureSqlDW**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="6dbb4-871">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-871">Property</span></span> | <span data-ttu-id="6dbb4-872">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-872">Description</span></span> | <span data-ttu-id="6dbb4-873">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-873">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-874">connectionString</span><span class="sxs-lookup"><span data-stu-id="6dbb4-874">connectionString</span></span> |<span data-ttu-id="6dbb4-875">針對 connectionString 屬性指定連線到 Azure SQL 資料倉儲執行個體所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-875">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span></span> |<span data-ttu-id="6dbb4-876">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-876">Yes</span></span> |



#### <a name="example"></a><span data-ttu-id="6dbb4-877">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-877">Example</span></span>

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="6dbb4-878">如需詳細資訊，請參閱 [Azure SQL 資料倉儲連接器](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-878">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="6dbb4-879">Dataset</span><span class="sxs-lookup"><span data-stu-id="6dbb4-879">Dataset</span></span>
<span data-ttu-id="6dbb4-880">若要定義 Azure SQL 資料倉儲資料集，請將資料集的 **type** 設為 **AzureSqlDWTable**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-880">To define an Azure SQL Data Warehouse dataset, set the **type** of the dataset to **AzureSqlDWTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="6dbb4-881">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-881">Property</span></span> | <span data-ttu-id="6dbb4-882">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-882">Description</span></span> | <span data-ttu-id="6dbb4-883">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-883">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-884">tableName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-884">tableName</span></span> |<span data-ttu-id="6dbb4-885">Azure SQL 資料倉儲資料庫中連結服務所參照的資料表名稱或檢視名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-885">Name of the table or view in the Azure SQL Data Warehouse database that the linked service refers to.</span></span> |<span data-ttu-id="6dbb4-886">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-886">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-887">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-887">Example</span></span>

```json
{
    "name": "AzureSqlDWInput",
    "properties": {
    "type": "AzureSqlDWTable",
        "linkedServiceName": "AzureSqlDWLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="6dbb4-888">如需詳細資訊，請參閱 [Azure SQL 資料倉儲連接器](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-888">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-dw-source-in-copy-activity"></a><span data-ttu-id="6dbb4-889">複製活動中的 SQL DW 來源</span><span class="sxs-lookup"><span data-stu-id="6dbb4-889">SQL DW Source in Copy Activity</span></span>
<span data-ttu-id="6dbb4-890">如果您從 Azure SQL 資料倉儲複製資料，請將複製活動的 **source type** 設為 **SqlDWSource**，並在 **source** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-890">If you are copying data from Azure SQL Data Warehouse, set the **source type** of the copy activity to **SqlDWSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="6dbb4-891">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-891">Property</span></span> | <span data-ttu-id="6dbb4-892">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-892">Description</span></span> | <span data-ttu-id="6dbb4-893">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-893">Allowed values</span></span> | <span data-ttu-id="6dbb4-894">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-894">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-895">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="6dbb4-895">sqlReaderQuery</span></span> |<span data-ttu-id="6dbb4-896">使用自訂查詢來讀取資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-896">Use the custom query to read data.</span></span> |<span data-ttu-id="6dbb4-897">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-897">SQL query string.</span></span> <span data-ttu-id="6dbb4-898">例如： `select * from MyTable`。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-898">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="6dbb4-899">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-899">No</span></span> |
| <span data-ttu-id="6dbb4-900">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-900">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="6dbb4-901">從來源資料表讀取資料的預存程序名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-901">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="6dbb4-902">預存程序的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-902">Name of the stored procedure.</span></span> |<span data-ttu-id="6dbb4-903">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-903">No</span></span> |
| <span data-ttu-id="6dbb4-904">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="6dbb4-904">storedProcedureParameters</span></span> |<span data-ttu-id="6dbb4-905">預存程序的參數。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-905">Parameters for the stored procedure.</span></span> |<span data-ttu-id="6dbb4-906">名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-906">Name/value pairs.</span></span> <span data-ttu-id="6dbb4-907">參數的名稱和大小寫必須符合預存程序參數的名稱和大小寫。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-907">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="6dbb4-908">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-908">No</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-909">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-909">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLDWtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSqlDWInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlDWSource",
                    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="6dbb4-910">如需詳細資訊，請參閱 [Azure SQL 資料倉儲連接器](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-910">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-dw-sink-in-copy-activity"></a><span data-ttu-id="6dbb4-911">複製活動中的 SQL DW 接收</span><span class="sxs-lookup"><span data-stu-id="6dbb4-911">SQL DW Sink in Copy Activity</span></span>
<span data-ttu-id="6dbb4-912">如果您將資料複製到 Azure SQL 資料倉儲，請將複製活動的 **sink type** 設為 **SqlDWSink**，並在 **sink** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-912">If you are copying data to Azure SQL Data Warehouse, set the **sink type** of the copy activity to **SqlDWSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="6dbb4-913">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-913">Property</span></span> | <span data-ttu-id="6dbb4-914">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-914">Description</span></span> | <span data-ttu-id="6dbb4-915">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-915">Allowed values</span></span> | <span data-ttu-id="6dbb4-916">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-916">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-917">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="6dbb4-917">sqlWriterCleanupScript</span></span> |<span data-ttu-id="6dbb4-918">指定要讓「複製活動」執行的查詢，以便清除特定分割的資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-918">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="6dbb4-919">查詢陳述式。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-919">A query statement.</span></span> |<span data-ttu-id="6dbb4-920">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-920">No</span></span> |
| <span data-ttu-id="6dbb4-921">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="6dbb4-921">allowPolyBase</span></span> |<span data-ttu-id="6dbb4-922">指出是否使用 PolyBase (適用的話) 而不是使用 BULKINSERT 機制。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-922">Indicates whether to use PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="6dbb4-923">**建議使用 PolyBase 將資料載入 SQL 資料倉儲。**</span><span class="sxs-lookup"><span data-stu-id="6dbb4-923">**Using PolyBase is the recommended way to load data into SQL Data Warehouse.**</span></span> |<span data-ttu-id="6dbb4-924">True</span><span class="sxs-lookup"><span data-stu-id="6dbb4-924">True</span></span> <br/><span data-ttu-id="6dbb4-925">FALSE (預設值)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-925">False (default)</span></span> |<span data-ttu-id="6dbb4-926">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-926">No</span></span> |
| <span data-ttu-id="6dbb4-927">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="6dbb4-927">polyBaseSettings</span></span> |<span data-ttu-id="6dbb4-928">可以在 **allowPolybase** 屬性設定為 **true** 時指定的一組屬性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-928">A group of properties that can be specified when the **allowPolybase** property is set to **true**.</span></span> |&nbsp; |<span data-ttu-id="6dbb4-929">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-929">No</span></span> |
| <span data-ttu-id="6dbb4-930">rejectValue</span><span class="sxs-lookup"><span data-stu-id="6dbb4-930">rejectValue</span></span> |<span data-ttu-id="6dbb4-931">指定在查詢失敗前可以拒絕的資料列數目或百分比。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-931">Specifies the number or percentage of rows that can be rejected before the query fails.</span></span> <br/><br/><span data-ttu-id="6dbb4-932">在 **CREATE EXTERNAL TABLE (Transact-SQL)** 主題的 [引數](https://msdn.microsoft.com/library/dn935021.aspx) 一節中，深入了解 PolyBase 的拒絕選項。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-932">Learn more about the PolyBase’s reject options in the **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="6dbb4-933">0 (預設值)、1、2、…</span><span class="sxs-lookup"><span data-stu-id="6dbb4-933">0 (default), 1, 2, …</span></span> |<span data-ttu-id="6dbb4-934">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-934">No</span></span> |
| <span data-ttu-id="6dbb4-935">rejectType</span><span class="sxs-lookup"><span data-stu-id="6dbb4-935">rejectType</span></span> |<span data-ttu-id="6dbb4-936">指定要將 rejectValue 選項指定為常值或百分比。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-936">Specifies whether the rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="6dbb4-937">值 (預設值)、百分比</span><span class="sxs-lookup"><span data-stu-id="6dbb4-937">Value (default), Percentage</span></span> |<span data-ttu-id="6dbb4-938">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-938">No</span></span> |
| <span data-ttu-id="6dbb4-939">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="6dbb4-939">rejectSampleValue</span></span> |<span data-ttu-id="6dbb4-940">決定在 PolyBase 重新計算已拒絕的資料列百分比之前，所要擷取的資料列數目。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-940">Determines the number of rows to retrieve before the PolyBase recalculates the percentage of rejected rows.</span></span> |<span data-ttu-id="6dbb4-941">1、2、…</span><span class="sxs-lookup"><span data-stu-id="6dbb4-941">1, 2, …</span></span> |<span data-ttu-id="6dbb4-942">是，如果 **rejectType** 是 **percentage**</span><span class="sxs-lookup"><span data-stu-id="6dbb4-942">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="6dbb4-943">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="6dbb4-943">useTypeDefault</span></span> |<span data-ttu-id="6dbb4-944">指定當 PolyBase 從文字檔擷取資料時，如何處理分隔符號文字檔中的遺漏值。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-944">Specifies how to handle missing values in delimited text files when PolyBase retrieves data from the text file.</span></span><br/><br/><span data-ttu-id="6dbb4-945">從 [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx) 的＜引數＞一節深入了解這個屬性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-945">Learn more about this property from the Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="6dbb4-946">True/False (預設值為 False)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-946">True, False (default)</span></span> |<span data-ttu-id="6dbb4-947">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-947">No</span></span> |
| <span data-ttu-id="6dbb4-948">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="6dbb4-948">writeBatchSize</span></span> |<span data-ttu-id="6dbb4-949">當緩衝區大小達到 writeBatchSize 時，將資料插入 SQL 資料表中</span><span class="sxs-lookup"><span data-stu-id="6dbb4-949">Inserts data into the SQL table when the buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="6dbb4-950">整數 (資料列數目)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-950">Integer (number of rows)</span></span> |<span data-ttu-id="6dbb4-951">否 (預設值：10000)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-951">No (default: 10000)</span></span> |
| <span data-ttu-id="6dbb4-952">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="6dbb4-952">writeBatchTimeout</span></span> |<span data-ttu-id="6dbb4-953">在逾時前等待批次插入作業完成的時間。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-953">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="6dbb4-954">時間範圍</span><span class="sxs-lookup"><span data-stu-id="6dbb4-954">timespan</span></span><br/><br/> <span data-ttu-id="6dbb4-955">範例：“00:30:00” (30 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-955">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="6dbb4-956">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-956">No</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-957">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-957">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQLDW",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlDWOutput"
            }],
            "typeProperties": {
                "source": {
                "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlDWSink",
                    "allowPolyBase": true
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="6dbb4-958">如需詳細資訊，請參閱 [Azure SQL 資料倉儲連接器](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-958">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-search"></a><span data-ttu-id="6dbb4-959">Azure 搜尋服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-959">Azure Search</span></span>

### <a name="linked-service"></a><span data-ttu-id="6dbb4-960">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-960">Linked service</span></span>
<span data-ttu-id="6dbb4-961">若要定義 Azure 搜尋服務連結服務，請將連結服務的 **type** 設為 **AzureSearch**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-961">To define an Azure Search linked service, set the **type** of the linked service to **AzureSearch**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="6dbb4-962">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-962">Property</span></span> | <span data-ttu-id="6dbb4-963">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-963">Description</span></span> | <span data-ttu-id="6dbb4-964">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-964">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="6dbb4-965">url</span><span class="sxs-lookup"><span data-stu-id="6dbb4-965">url</span></span> | <span data-ttu-id="6dbb4-966">Azure 搜尋服務的 URL。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-966">URL for the Azure Search service.</span></span> | <span data-ttu-id="6dbb4-967">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-967">Yes</span></span> |
| <span data-ttu-id="6dbb4-968">key</span><span class="sxs-lookup"><span data-stu-id="6dbb4-968">key</span></span> | <span data-ttu-id="6dbb4-969">Azure 搜尋服務的系統管理金鑰。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-969">Admin key for the Azure Search service.</span></span> | <span data-ttu-id="6dbb4-970">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-970">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-971">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-971">Example</span></span>

```json
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

<span data-ttu-id="6dbb4-972">如需詳細資訊，請參閱 [Azure 搜尋服務連接器](data-factory-azure-search-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-972">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="6dbb4-973">Dataset</span><span class="sxs-lookup"><span data-stu-id="6dbb4-973">Dataset</span></span>
<span data-ttu-id="6dbb4-974">若要定義 Azure 搜尋服務資料集，請將資料集的 **type** 設為 **AzureSearchIndex**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-974">To define an Azure Search dataset, set the **type** of the dataset to **AzureSearchIndex**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="6dbb4-975">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-975">Property</span></span> | <span data-ttu-id="6dbb4-976">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-976">Description</span></span> | <span data-ttu-id="6dbb4-977">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-977">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="6dbb4-978">類型</span><span class="sxs-lookup"><span data-stu-id="6dbb4-978">type</span></span> | <span data-ttu-id="6dbb4-979">type 屬性必須設為 **AzureSearchIndex**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-979">The type property must be set to **AzureSearchIndex**.</span></span>| <span data-ttu-id="6dbb4-980">yes</span><span class="sxs-lookup"><span data-stu-id="6dbb4-980">Yes</span></span> |
| <span data-ttu-id="6dbb4-981">IndexName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-981">indexName</span></span> | <span data-ttu-id="6dbb4-982">Azure 搜尋服務索引的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-982">Name of the Azure Search index.</span></span> <span data-ttu-id="6dbb4-983">Data Factory 不會建立索引。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-983">Data Factory does not create the index.</span></span> <span data-ttu-id="6dbb4-984">索引必須存在於 Azure 搜尋服務中。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-984">The index must exist in Azure Search.</span></span> | <span data-ttu-id="6dbb4-985">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-985">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-986">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-986">Example</span></span>

```json
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties": {
            "indexName": "products"
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
    }
}
```

<span data-ttu-id="6dbb4-987">如需詳細資訊，請參閱 [Azure 搜尋服務連接器](data-factory-azure-search-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-987">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#dataset-properties) article.</span></span>

### <a name="azure-search-index-sink-in-copy-activity"></a><span data-ttu-id="6dbb4-988">複製活動中的 Azure 搜尋服務索引接收</span><span class="sxs-lookup"><span data-stu-id="6dbb4-988">Azure Search Index Sink in Copy Activity</span></span>
<span data-ttu-id="6dbb4-989">如果您將資料複製到 Azure 搜尋服務索引，請將複製活動的 **sink type** 設為 **AzureSearchIndexSink**，並在 **sink** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-989">If you are copying data to an Azure Search index, set the **sink type** of the copy activity to **AzureSearchIndexSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="6dbb4-990">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-990">Property</span></span> | <span data-ttu-id="6dbb4-991">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-991">Description</span></span> | <span data-ttu-id="6dbb4-992">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-992">Allowed values</span></span> | <span data-ttu-id="6dbb4-993">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-993">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="6dbb4-994">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="6dbb4-994">WriteBehavior</span></span> | <span data-ttu-id="6dbb4-995">指定若文件已經存在於索引中，是否要合併或取代。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-995">Specifies whether to merge or replace when a document already exists in the index.</span></span> | <span data-ttu-id="6dbb4-996">合併 (預設值)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-996">Merge (default)</span></span><br/><span data-ttu-id="6dbb4-997">上傳</span><span class="sxs-lookup"><span data-stu-id="6dbb4-997">Upload</span></span>| <span data-ttu-id="6dbb4-998">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-998">No</span></span> |
| <span data-ttu-id="6dbb4-999">WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="6dbb4-999">WriteBatchSize</span></span> | <span data-ttu-id="6dbb4-1000">當緩衝區大小達到 writeBatchSize 時，將資料上傳至 Azure 搜尋服務中。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1000">Uploads data into the Azure Search index when the buffer size reaches writeBatchSize.</span></span> | <span data-ttu-id="6dbb4-1001">1 到 1000。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1001">1 to 1,000.</span></span> <span data-ttu-id="6dbb4-1002">預設值為 1000。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1002">Default value is 1000.</span></span> | <span data-ttu-id="6dbb4-1003">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1003">No</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-1004">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1004">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoAzureSearchIndex",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureSearchIndexDataset"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "AzureSearchIndexSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="6dbb4-1005">如需詳細資訊，請參閱 [Azure 搜尋服務連接器](data-factory-azure-search-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1005">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-table-storage"></a><span data-ttu-id="6dbb4-1006">Azure 表格儲存體</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1006">Azure Table Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="6dbb4-1007">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1007">Linked service</span></span>
<span data-ttu-id="6dbb4-1008">有兩種連結服務類型︰Azure 儲存體連結服務和 Azure 儲存體 SAS 連結服務。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1008">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="6dbb4-1009">Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1009">Azure Storage Linked Service</span></span>
<span data-ttu-id="6dbb4-1010">若要使用**帳戶金鑰**將 Azure 儲存體帳戶連結至資料處理站，請建立 Azure 儲存體連結服務。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1010">To link your Azure storage account to a data factory by using the **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="6dbb4-1011">若要定義 Azure 儲存體連結服務，請將連結服務的**類型**設為 **AzureStorage**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1011">To define an Azure Storage linked service, set the **type** of the linked service to **AzureStorage**.</span></span> <span data-ttu-id="6dbb4-1012">然後，您可以在 **typeProperties** 區段中指定下列屬性：</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1012">Then, you can specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="6dbb4-1013">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1013">Property</span></span> | <span data-ttu-id="6dbb4-1014">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1014">Description</span></span> | <span data-ttu-id="6dbb4-1015">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1015">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="6dbb4-1016">類型</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1016">type</span></span> |<span data-ttu-id="6dbb4-1017">類型屬性必須設為： **AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1017">The type property must be set to: **AzureStorage**</span></span> |<span data-ttu-id="6dbb4-1018">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1018">Yes</span></span> |
| <span data-ttu-id="6dbb4-1019">connectionString</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1019">connectionString</span></span> |<span data-ttu-id="6dbb4-1020">針對 connectionString 屬性指定連接到 Azure 儲存體所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1020">Specify information needed to connect to Azure storage for the connectionString property.</span></span> |<span data-ttu-id="6dbb4-1021">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1021">Yes</span></span> |

<span data-ttu-id="6dbb4-1022">**範例：**</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1022">**Example:**</span></span>  

```json
{  
    "name": "StorageLinkedService",  
    "properties": {  
        "type": "AzureStorage",  
        "typeProperties": {  
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"  
        }  
    }  
}  
```

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="6dbb4-1023">Azure 儲存體 SAS 連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1023">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="6dbb4-1024">Azure 儲存體 SAS 連結服務可讓您使用共用存取簽章 (SAS)，將 Azure 儲存體帳戶連結到 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1024">The Azure Storage SAS linked service allows you to link an Azure Storage Account to an Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="6dbb4-1025">它提供受限制/時間界限存取權，讓資料處理站存取儲存體中的所有/特定資源 (blob/容器)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1025">It provides the data factory with restricted/time-bound access to all/specific resources (blob/container) in the storage.</span></span> <span data-ttu-id="6dbb4-1026">若要使用共用存取簽章將 Azure 儲存體帳戶連結至資料處理站，請建立 Azure 儲存體 SAS 連結服務。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1026">To link your Azure storage account to a data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="6dbb4-1027">若要定義 Azure 儲存體 SAS 連結服務，請將連結服務的**類型**設為 **AzureStorageSas**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1027">To define an Azure Storage SAS linked service, set the **type** of the linked service to **AzureStorageSas**.</span></span> <span data-ttu-id="6dbb4-1028">然後，您可以在 **typeProperties** 區段中指定下列屬性：</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1028">Then, you can specify following properties in the **typeProperties** section:</span></span>   

| <span data-ttu-id="6dbb4-1029">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1029">Property</span></span> | <span data-ttu-id="6dbb4-1030">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1030">Description</span></span> | <span data-ttu-id="6dbb4-1031">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1031">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="6dbb4-1032">類型</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1032">type</span></span> |<span data-ttu-id="6dbb4-1033">類型屬性必須設為： **AzureStorageSas**</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1033">The type property must be set to: **AzureStorageSas**</span></span> |<span data-ttu-id="6dbb4-1034">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1034">Yes</span></span> |
| <span data-ttu-id="6dbb4-1035">sasUri</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1035">sasUri</span></span> |<span data-ttu-id="6dbb4-1036">指定 Azure 儲存體資源 (例如 Blob、容器或資料表) 的共用存取簽章 URI。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1036">Specify Shared Access Signature URI to the Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="6dbb4-1037">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1037">Yes</span></span> |

<span data-ttu-id="6dbb4-1038">**範例：**</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1038">**Example:**</span></span>

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

<span data-ttu-id="6dbb4-1039">如需這些連結服務的詳細資訊，請參閱 [Azure 表格儲存體連接器](data-factory-azure-table-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1039">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="6dbb4-1040">Dataset</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1040">Dataset</span></span>
<span data-ttu-id="6dbb4-1041">若要定義 Azure 資料表資料集，請將資料集的 **type** 設為 **AzureTable**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1041">To define an Azure Table dataset, set the **type** of the dataset to **AzureTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="6dbb4-1042">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1042">Property</span></span> | <span data-ttu-id="6dbb4-1043">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1043">Description</span></span> | <span data-ttu-id="6dbb4-1044">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1044">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-1045">tableName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1045">tableName</span></span> |<span data-ttu-id="6dbb4-1046">Azure 資料表資料庫執行個體中連結服務所參照的資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1046">Name of the table in the Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="6dbb4-1047">是。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1047">Yes.</span></span> <span data-ttu-id="6dbb4-1048">指定 tableName 時若沒有指定 azureTableSourceQuery，資料表中的所有記錄都會複製到目的地。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1048">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="6dbb4-1049">如果同時指定了 azureTableSourceQuery，則資料表中符合查詢的記錄會複製到目的地。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1049">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-1050">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1050">Example</span></span>

```json
{
    "name": "AzureTableInput",
    "properties": {
        "type": "AzureTable",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="6dbb4-1051">如需這些連結服務的詳細資訊，請參閱 [Azure 表格儲存體連接器](data-factory-azure-table-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1051">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-table-source-in-copy-activity"></a><span data-ttu-id="6dbb4-1052">複製活動中的 Azure 資料表來源</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1052">Azure Table Source in Copy Activity</span></span>
<span data-ttu-id="6dbb4-1053">如果您從 Azure 表格儲存體複製資料，請將複製活動的 **source type** 設為 **AzureTableSource**，並在 **source** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1053">If you are copying data from Azure Table Storage, set the **source type** of the copy activity to **AzureTableSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="6dbb4-1054">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1054">Property</span></span> | <span data-ttu-id="6dbb4-1055">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1055">Description</span></span> | <span data-ttu-id="6dbb4-1056">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1056">Allowed values</span></span> | <span data-ttu-id="6dbb4-1057">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1057">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-1058">AzureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1058">azureTableSourceQuery</span></span> |<span data-ttu-id="6dbb4-1059">使用自訂查詢來讀取資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1059">Use the custom query to read data.</span></span> |<span data-ttu-id="6dbb4-1060">Azure 資料表查詢字串。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1060">Azure table query string.</span></span> <span data-ttu-id="6dbb4-1061">請參閱下一節中的範例。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1061">See examples in the next section.</span></span> |<span data-ttu-id="6dbb4-1062">否。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1062">No.</span></span> <span data-ttu-id="6dbb4-1063">指定 tableName 時若沒有指定 azureTableSourceQuery，資料表中的所有記錄都會複製到目的地。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1063">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="6dbb4-1064">如果同時指定了 azureTableSourceQuery，則資料表中符合查詢的記錄會複製到目的地。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1064">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |
| <span data-ttu-id="6dbb4-1065">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1065">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="6dbb4-1066">指出是否忍受資料表不存在的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1066">Indicate whether swallow the exception of table not exist.</span></span> |<span data-ttu-id="6dbb4-1067">TRUE</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1067">TRUE</span></span><br/><span data-ttu-id="6dbb4-1068">FALSE</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1068">FALSE</span></span> |<span data-ttu-id="6dbb4-1069">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1069">No</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-1070">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1070">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureTabletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureTableSource",
                    "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="6dbb4-1071">如需這些連結服務的詳細資訊，請參閱 [Azure 表格儲存體連接器](data-factory-azure-table-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1071">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

### <a name="azure-table-sink-in-copy-activity"></a><span data-ttu-id="6dbb4-1072">複製活動中的 Azure 資料表接收</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1072">Azure Table Sink in Copy Activity</span></span>
<span data-ttu-id="6dbb4-1073">如果您將資料複製到 Azure 表格儲存體，請將複製活動的 **sink type** 設為 **AzureTableSink**，並在 **sink** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1073">If you are copying data to Azure Table Storage, set the **sink type** of the copy activity to **AzureTableSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="6dbb4-1074">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1074">Property</span></span> | <span data-ttu-id="6dbb4-1075">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1075">Description</span></span> | <span data-ttu-id="6dbb4-1076">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1076">Allowed values</span></span> | <span data-ttu-id="6dbb4-1077">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1077">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-1078">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1078">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="6dbb4-1079">可供接收器使用的預設資料分割索引鍵值。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1079">Default partition key value that can be used by the sink.</span></span> |<span data-ttu-id="6dbb4-1080">字串值。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1080">A string value.</span></span> |<span data-ttu-id="6dbb4-1081">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1081">No</span></span> |
| <span data-ttu-id="6dbb4-1082">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1082">azureTablePartitionKeyName</span></span> |<span data-ttu-id="6dbb4-1083">指定其值用來作為分割區索引鍵的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1083">Specify name of the column whose values are used as partition keys.</span></span> <span data-ttu-id="6dbb4-1084">如果未指定，則會使用 AzureTableDefaultPartitionKeyValue 做為資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1084">If not specified, AzureTableDefaultPartitionKeyValue is used as the partition key.</span></span> |<span data-ttu-id="6dbb4-1085">資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1085">A column name.</span></span> |<span data-ttu-id="6dbb4-1086">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1086">No</span></span> |
| <span data-ttu-id="6dbb4-1087">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1087">azureTableRowKeyName</span></span> |<span data-ttu-id="6dbb4-1088">指定其值用來作為資料列索引鍵的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1088">Specify name of the column whose column values are used as row key.</span></span> <span data-ttu-id="6dbb4-1089">如果未指定，則會針對每個資料列使用 GUID。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1089">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="6dbb4-1090">資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1090">A column name.</span></span> |<span data-ttu-id="6dbb4-1091">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1091">No</span></span> |
| <span data-ttu-id="6dbb4-1092">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1092">azureTableInsertType</span></span> |<span data-ttu-id="6dbb4-1093">將資料插入 Azure 資料表的模式。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1093">The mode to insert data into Azure table.</span></span><br/><br/><span data-ttu-id="6dbb4-1094">此屬性可控制針對輸出資料表中具有相符分割區和資料列索引鍵的現有資料列，是要取代還是合併其值。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1094">This property controls whether existing rows in the output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="6dbb4-1095">若要了解這些設定 (合併和取代) 的運作方式，請參閱[插入或合併實體](https://msdn.microsoft.com/library/azure/hh452241.aspx)和[插入或取代實體](https://msdn.microsoft.com/library/azure/hh452242.aspx)主題。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1095">To learn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="6dbb4-1096">此設定是在資料列層級套用，而不是在資料表層級套用，而且兩個選項都不會刪除存在於輸出資料表中但不存在於輸入中的資料列。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1096">This setting applies at the row level, not the table level, and neither option deletes rows in the output table that do not exist in the input.</span></span> |<span data-ttu-id="6dbb4-1097">合併 (預設值)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1097">merge (default)</span></span><br/><span data-ttu-id="6dbb4-1098">取代</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1098">replace</span></span> |<span data-ttu-id="6dbb4-1099">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1099">No</span></span> |
| <span data-ttu-id="6dbb4-1100">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1100">writeBatchSize</span></span> |<span data-ttu-id="6dbb4-1101">在達到 WriteBatchSize 或 writeBatchTimeout 時將資料插入 Azure 資料表中。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1101">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="6dbb4-1102">整數 (資料列數目)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1102">Integer (number of rows)</span></span> |<span data-ttu-id="6dbb4-1103">否 (預設值：10000)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1103">No (default: 10000)</span></span> |
| <span data-ttu-id="6dbb4-1104">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1104">writeBatchTimeout</span></span> |<span data-ttu-id="6dbb4-1105">在達到 WriteBatchSize 或 writeBatchTimeout 時將資料插入 Azure 資料表中</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1105">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="6dbb4-1106">時間範圍</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1106">timespan</span></span><br/><br/><span data-ttu-id="6dbb4-1107">範例：“00:20:00” (20 分鐘)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1107">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="6dbb4-1108">否 (預設為儲存體用戶端預設逾時值 90 秒)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1108">No (Default to storage client default timeout value 90 sec)</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-1109">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1109">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoTable",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureTableOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureTableSink",
                    "writeBatchSize": 100,
                    "writeBatchTimeout": "01:00:00"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="6dbb4-1110">如需這些連結服務的詳細資訊，請參閱 [Azure 表格儲存體連接器](data-factory-azure-table-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1110">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="amazon-redshift"></a><span data-ttu-id="6dbb4-1111">Amazon RedShift</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1111">Amazon RedShift</span></span>

### <a name="linked-service"></a><span data-ttu-id="6dbb4-1112">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1112">Linked service</span></span>
<span data-ttu-id="6dbb4-1113">若要定義 Amazon Redshift 連結服務，請將連結服務的 **type** 設為 **AmazonRedshift**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1113">To define an Amazon Redshift linked service, set the **type** of the linked service to **AmazonRedshift**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="6dbb4-1114">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1114">Property</span></span> | <span data-ttu-id="6dbb4-1115">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1115">Description</span></span> | <span data-ttu-id="6dbb4-1116">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1116">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-1117">伺服器</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1117">server</span></span> |<span data-ttu-id="6dbb4-1118">Amazon Redshift 伺服器的 IP 位址或主機名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1118">IP address or host name of the Amazon Redshift server.</span></span> |<span data-ttu-id="6dbb4-1119">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1119">Yes</span></span> |
| <span data-ttu-id="6dbb4-1120">連接埠</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1120">port</span></span> |<span data-ttu-id="6dbb4-1121">Amazon Redshift 伺服器用來接聽用戶端連線的 TCP 連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1121">The number of the TCP port that the Amazon Redshift server uses to listen for client connections.</span></span> |<span data-ttu-id="6dbb4-1122">否，預設值︰5439</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1122">No, default value: 5439</span></span> |
| <span data-ttu-id="6dbb4-1123">資料庫</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1123">database</span></span> |<span data-ttu-id="6dbb4-1124">Amazon Redshift 資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1124">Name of the Amazon Redshift database.</span></span> |<span data-ttu-id="6dbb4-1125">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1125">Yes</span></span> |
| <span data-ttu-id="6dbb4-1126">username</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1126">username</span></span> |<span data-ttu-id="6dbb4-1127">可存取資料庫之使用者的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1127">Name of user who has access to the database.</span></span> |<span data-ttu-id="6dbb4-1128">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1128">Yes</span></span> |
| <span data-ttu-id="6dbb4-1129">password</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1129">password</span></span> |<span data-ttu-id="6dbb4-1130">使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1130">Password for the user account.</span></span> |<span data-ttu-id="6dbb4-1131">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1131">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-1132">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1132">Example</span></span>

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties": {
        "type": "AmazonRedshift",
        "typeProperties": {
            "server": "<Amazon Redshift host name or IP address>",
            "port": 5439,
            "database": "<database name>",
            "username": "user",
            "password": "password"
        }
    }
}
```

<span data-ttu-id="6dbb4-1133">如需詳細資訊，請參閱 [Amazon Redshift 連接器](#data-factory-amazon-redshift-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1133">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="6dbb4-1134">Dataset</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1134">Dataset</span></span>
<span data-ttu-id="6dbb4-1135">若要定義 Amazon Redshift 資料集，請將資料集的 **type** 設為 **RelationalTable**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1135">To define an Amazon Redshift dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="6dbb4-1136">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1136">Property</span></span> | <span data-ttu-id="6dbb4-1137">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1137">Description</span></span> | <span data-ttu-id="6dbb4-1138">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1138">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-1139">tableName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1139">tableName</span></span> |<span data-ttu-id="6dbb4-1140">Amazon Redshift 資料庫中連結服務所參照的資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1140">Name of the table in the Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="6dbb4-1141">否 (如果已指定 **RelationalSource** 的 **query**)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1141">No (if **query** of **RelationalSource** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="6dbb4-1142">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1142">Example</span></span>

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="6dbb4-1143">如需詳細資訊，請參閱 [Amazon Redshift 連接器](#data-factory-amazon-redshift-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1143">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="6dbb4-1144">複製活動中的關聯式來源</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1144">Relational Source in Copy Activity</span></span> 
<span data-ttu-id="6dbb4-1145">如果您從 Amazon Redshift 複製資料，請將複製活動的 **source type** 設為 **RelationalSource**，並在 **source** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1145">If you are copying data from Amazon Redshift, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="6dbb4-1146">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1146">Property</span></span> | <span data-ttu-id="6dbb4-1147">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1147">Description</span></span> | <span data-ttu-id="6dbb4-1148">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1148">Allowed values</span></span> | <span data-ttu-id="6dbb4-1149">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1149">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-1150">query</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1150">query</span></span> |<span data-ttu-id="6dbb4-1151">使用自訂查詢來讀取資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1151">Use the custom query to read data.</span></span> |<span data-ttu-id="6dbb4-1152">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1152">SQL query string.</span></span> <span data-ttu-id="6dbb4-1153">例如： `select * from MyTable`。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1153">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="6dbb4-1154">否 (如果已指定 **dataset** 的 **tableName**)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1154">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-1155">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1155">Example</span></span>

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonRedshiftInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonRedshiftToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
<span data-ttu-id="6dbb4-1156">如需詳細資訊，請參閱 [Amazon Redshift 連接器](#data-factory-amazon-redshift-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1156">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#copy-activity-properties) article.</span></span>

## <a name="ibm-db2"></a><span data-ttu-id="6dbb4-1157">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1157">IBM DB2</span></span>

### <a name="linked-service"></a><span data-ttu-id="6dbb4-1158">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1158">Linked service</span></span>
<span data-ttu-id="6dbb4-1159">若要定義 IBM DB2 連結服務，請將連結服務的 **type** 設為 **OnPremisesDB2**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1159">To define an IBM DB2 linked service, set the **type** of the linked service to **OnPremisesDB2**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="6dbb4-1160">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1160">Property</span></span> | <span data-ttu-id="6dbb4-1161">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1161">Description</span></span> | <span data-ttu-id="6dbb4-1162">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-1163">伺服器</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1163">server</span></span> |<span data-ttu-id="6dbb4-1164">DB2 伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1164">Name of the DB2 server.</span></span> |<span data-ttu-id="6dbb4-1165">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1165">Yes</span></span> |
| <span data-ttu-id="6dbb4-1166">資料庫</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1166">database</span></span> |<span data-ttu-id="6dbb4-1167">DB2 資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1167">Name of the DB2 database.</span></span> |<span data-ttu-id="6dbb4-1168">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1168">Yes</span></span> |
| <span data-ttu-id="6dbb4-1169">結構描述</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1169">schema</span></span> |<span data-ttu-id="6dbb4-1170">在資料庫中的結構描述名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1170">Name of the schema in the database.</span></span> <span data-ttu-id="6dbb4-1171">結構描述名稱會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1171">The schema name is case-sensitive.</span></span> |<span data-ttu-id="6dbb4-1172">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1172">No</span></span> |
| <span data-ttu-id="6dbb4-1173">authenticationType</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1173">authenticationType</span></span> |<span data-ttu-id="6dbb4-1174">用來連接到 DB2 資料庫的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1174">Type of authentication used to connect to the DB2 database.</span></span> <span data-ttu-id="6dbb4-1175">可能的值為：匿名、基本和 Windows。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1175">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="6dbb4-1176">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1176">Yes</span></span> |
| <span data-ttu-id="6dbb4-1177">username</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1177">username</span></span> |<span data-ttu-id="6dbb4-1178">如果您使用基本或 Windows 驗證，請指定使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1178">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="6dbb4-1179">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1179">No</span></span> |
| <span data-ttu-id="6dbb4-1180">password</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1180">password</span></span> |<span data-ttu-id="6dbb4-1181">指定您為使用者名稱所指定之使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1181">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="6dbb4-1182">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1182">No</span></span> |
| <span data-ttu-id="6dbb4-1183">gatewayName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1183">gatewayName</span></span> |<span data-ttu-id="6dbb4-1184">Data Factory 服務應該用來連接到內部部署 DB2 資料庫的閘道器名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1184">Name of the gateway that the Data Factory service should use to connect to the on-premises DB2 database.</span></span> |<span data-ttu-id="6dbb4-1185">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1185">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-1186">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1186">Example</span></span>
```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
<span data-ttu-id="6dbb4-1187">如需詳細資訊，請參閱 [IBM DB2 連接器](#data-factory-onprem-db2-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1187">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="6dbb4-1188">Dataset</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1188">Dataset</span></span>
<span data-ttu-id="6dbb4-1189">若要定義 DB2 資料集，請將資料集的 **type** 設為 **RelationalTable**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1189">To define a DB2 dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span>

| <span data-ttu-id="6dbb4-1190">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1190">Property</span></span> | <span data-ttu-id="6dbb4-1191">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1191">Description</span></span> | <span data-ttu-id="6dbb4-1192">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1192">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-1193">tableName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1193">tableName</span></span> |<span data-ttu-id="6dbb4-1194">DB2 資料庫執行個體中連結服務所參照的資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1194">Name of the table in the DB2 Database instance that linked service refers to.</span></span> <span data-ttu-id="6dbb4-1195">tableName 會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1195">The tableName is case-sensitive.</span></span> |<span data-ttu-id="6dbb4-1196">否 (如果已指定 **RelationalSource** 的 **query**)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1196">No (if **query** of **RelationalSource** is specified)</span></span> 

#### <a name="example"></a><span data-ttu-id="6dbb4-1197">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1197">Example</span></span>
```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="6dbb4-1198">如需詳細資訊，請參閱 [IBM DB2 連接器](#data-factory-onprem-db2-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1198">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="6dbb4-1199">複製活動中的關聯式來源</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1199">Relational Source in Copy Activity</span></span>
<span data-ttu-id="6dbb4-1200">如果您從 IBM DB2 複製資料，請將複製活動的 **source type** 設為 **RelationalSource**，並在 **source** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1200">If you are copying data from IBM DB2, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="6dbb4-1201">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1201">Property</span></span> | <span data-ttu-id="6dbb4-1202">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1202">Description</span></span> | <span data-ttu-id="6dbb4-1203">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1203">Allowed values</span></span> | <span data-ttu-id="6dbb4-1204">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1204">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-1205">query</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1205">query</span></span> |<span data-ttu-id="6dbb4-1206">使用自訂查詢來讀取資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1206">Use the custom query to read data.</span></span> |<span data-ttu-id="6dbb4-1207">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1207">SQL query string.</span></span> <span data-ttu-id="6dbb4-1208">例如： `"query": "select * from "MySchema"."MyTable""`。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1208">For example: `"query": "select * from "MySchema"."MyTable""`.</span></span> |<span data-ttu-id="6dbb4-1209">否 (如果已指定 **dataset** 的 **tableName**)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1209">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-1210">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1210">Example</span></span>
```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"Orders\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "Db2DataSet"
            }],
            "outputs": [{
                "name": "AzureBlobDb2DataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "Db2ToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
<span data-ttu-id="6dbb4-1211">如需詳細資訊，請參閱 [IBM DB2 連接器](#data-factory-onprem-db2-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1211">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#copy-activity-properties) article.</span></span>

## <a name="mysql"></a><span data-ttu-id="6dbb4-1212">MySQL</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1212">MySQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="6dbb4-1213">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1213">Linked service</span></span>
<span data-ttu-id="6dbb4-1214">若要定義 MySQL 連結服務，請將連結服務的 **type** 設為 **OnPremisesMySql**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1214">To define a MySQL linked service, set the **type** of the linked service to **OnPremisesMySql**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="6dbb4-1215">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1215">Property</span></span> | <span data-ttu-id="6dbb4-1216">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1216">Description</span></span> | <span data-ttu-id="6dbb4-1217">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1217">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-1218">伺服器</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1218">server</span></span> |<span data-ttu-id="6dbb4-1219">MySQL 伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1219">Name of the MySQL server.</span></span> |<span data-ttu-id="6dbb4-1220">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1220">Yes</span></span> |
| <span data-ttu-id="6dbb4-1221">資料庫</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1221">database</span></span> |<span data-ttu-id="6dbb4-1222">MySQL 資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1222">Name of the MySQL database.</span></span> |<span data-ttu-id="6dbb4-1223">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1223">Yes</span></span> |
| <span data-ttu-id="6dbb4-1224">結構描述</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1224">schema</span></span> |<span data-ttu-id="6dbb4-1225">在資料庫中的結構描述名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1225">Name of the schema in the database.</span></span> |<span data-ttu-id="6dbb4-1226">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1226">No</span></span> |
| <span data-ttu-id="6dbb4-1227">authenticationType</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1227">authenticationType</span></span> |<span data-ttu-id="6dbb4-1228">用來連接到 MySQL 資料庫的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1228">Type of authentication used to connect to the MySQL database.</span></span> <span data-ttu-id="6dbb4-1229">可能的值為：`Basic`。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1229">Possible values are: `Basic`.</span></span> |<span data-ttu-id="6dbb4-1230">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1230">Yes</span></span> |
| <span data-ttu-id="6dbb4-1231">username</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1231">username</span></span> |<span data-ttu-id="6dbb4-1232">指定要連線到 MySQL 資料庫的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1232">Specify user name to connect to the MySQL database.</span></span> |<span data-ttu-id="6dbb4-1233">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1233">Yes</span></span> |
| <span data-ttu-id="6dbb4-1234">password</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1234">password</span></span> |<span data-ttu-id="6dbb4-1235">指定您所指定使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1235">Specify password for the user account you specified.</span></span> |<span data-ttu-id="6dbb4-1236">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1236">Yes</span></span> |
| <span data-ttu-id="6dbb4-1237">gatewayName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1237">gatewayName</span></span> |<span data-ttu-id="6dbb4-1238">Data Factory 服務應該用來連接到內部部署 MySQL 資料庫的閘道器名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1238">Name of the gateway that the Data Factory service should use to connect to the on-premises MySQL database.</span></span> |<span data-ttu-id="6dbb4-1239">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1239">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-1240">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1240">Example</span></span>

```json
{
    "name": "OnPremMySqlLinkedService",
    "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
            "server": "<server name>",
            "database": "<database name>",
            "schema": "<schema name>",
            "authenticationType": "<authentication type>",
            "userName": "<user name>",
            "password": "<password>",
            "gatewayName": "<gateway>"
        }
    }
}
```

<span data-ttu-id="6dbb4-1241">如需詳細資訊，請參閱 [MySQL 連接器](data-factory-onprem-mysql-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1241">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="6dbb4-1242">Dataset</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1242">Dataset</span></span>
<span data-ttu-id="6dbb4-1243">若要定義 MySQL 資料集，請將資料集的 **type** 設為 **RelationalTable**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1243">To define a MySQL dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="6dbb4-1244">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1244">Property</span></span> | <span data-ttu-id="6dbb4-1245">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1245">Description</span></span> | <span data-ttu-id="6dbb4-1246">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-1247">tableName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1247">tableName</span></span> |<span data-ttu-id="6dbb4-1248">MySQL 資料庫執行個體中連結服務所參照的資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1248">Name of the table in the MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="6dbb4-1249">否 (如果已指定 **RelationalSource** 的 **query**)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1249">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-1250">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1250">Example</span></span>

```json
{
    "name": "MySqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremMySqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="6dbb4-1251">如需詳細資訊，請參閱 [MySQL 連接器](data-factory-onprem-mysql-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1251">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="6dbb4-1252">複製活動中的關聯式來源</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1252">Relational Source in Copy Activity</span></span>
<span data-ttu-id="6dbb4-1253">如果您從 MySQL 資料庫複製資料，請將複製活動的 **source type** 設為 **RelationalSource**，並在 **source** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1253">If you are copying data from a MySQL database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="6dbb4-1254">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1254">Property</span></span> | <span data-ttu-id="6dbb4-1255">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1255">Description</span></span> | <span data-ttu-id="6dbb4-1256">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1256">Allowed values</span></span> | <span data-ttu-id="6dbb4-1257">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1257">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-1258">query</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1258">query</span></span> |<span data-ttu-id="6dbb4-1259">使用自訂查詢來讀取資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1259">Use the custom query to read data.</span></span> |<span data-ttu-id="6dbb4-1260">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1260">SQL query string.</span></span> <span data-ttu-id="6dbb4-1261">例如： `select * from MyTable`。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1261">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="6dbb4-1262">否 (如果已指定 **dataset** 的 **tableName**)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1262">No (if **tableName** of **dataset** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="6dbb4-1263">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1263">Example</span></span>
```json
{
    "name": "CopyMySqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MySqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobMySqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MySqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="6dbb4-1264">如需詳細資訊，請參閱 [MySQL 連接器](data-factory-onprem-mysql-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1264">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="oracle"></a><span data-ttu-id="6dbb4-1265">Oracle</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1265">Oracle</span></span> 

### <a name="linked-service"></a><span data-ttu-id="6dbb4-1266">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1266">Linked service</span></span>
<span data-ttu-id="6dbb4-1267">若要定義 Oracle 連結服務，請將連結服務的 **type** 設為 **OnPremisesOracle**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1267">To define an Oracle linked service, set the **type** of the linked service to **OnPremisesOracle**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="6dbb4-1268">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1268">Property</span></span> | <span data-ttu-id="6dbb4-1269">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1269">Description</span></span> | <span data-ttu-id="6dbb4-1270">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1270">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-1271">driverType</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1271">driverType</span></span> | <span data-ttu-id="6dbb4-1272">指定要用來從 Oracle 複製資料/將資料複製到 Oracle 資料庫的驅動程式。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1272">Specify which driver to use to copy data from/to Oracle Database.</span></span> <span data-ttu-id="6dbb4-1273">允許的值為 **Microsoft** 或 **ODP** (預設值)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1273">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="6dbb4-1274">如需驅動程式詳細資料，請參閱[支援的版本和安裝](#supported-versions-and-installation)一節。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1274">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="6dbb4-1275">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1275">No</span></span> |
| <span data-ttu-id="6dbb4-1276">connectionString</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1276">connectionString</span></span> | <span data-ttu-id="6dbb4-1277">針對 connectionString 屬性指定連接到 Oracle 資料庫執行個體所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1277">Specify information needed to connect to the Oracle Database instance for the connectionString property.</span></span> | <span data-ttu-id="6dbb4-1278">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1278">Yes</span></span> |
| <span data-ttu-id="6dbb4-1279">gatewayName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1279">gatewayName</span></span> | <span data-ttu-id="6dbb4-1280">用來連接到內部部署 Oracle 伺服器的閘道器名稱</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1280">Name of the gateway that that is used to connect to the on-premises Oracle server</span></span> |<span data-ttu-id="6dbb4-1281">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1281">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-1282">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1282">Example</span></span>
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString": "Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="6dbb4-1283">如需詳細資訊，請參閱 [Oracle 連接器](data-factory-onprem-oracle-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1283">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="6dbb4-1284">Dataset</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1284">Dataset</span></span>
<span data-ttu-id="6dbb4-1285">若要定義 Oracle 資料集，請將資料集的 **type** 設為 **OracleTable**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1285">To define an Oracle dataset, set the **type** of the dataset to **OracleTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="6dbb4-1286">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1286">Property</span></span> | <span data-ttu-id="6dbb4-1287">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1287">Description</span></span> | <span data-ttu-id="6dbb4-1288">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1288">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-1289">tableName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1289">tableName</span></span> |<span data-ttu-id="6dbb4-1290">Oracle 資料庫中連結服務所參照的資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1290">Name of the table in the Oracle Database that the linked service refers to.</span></span> |<span data-ttu-id="6dbb4-1291">否 (如果已指定 **OracleSource** 的 **oracleReaderQuery**)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1291">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-1292">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1292">Example</span></span>

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2016-02-27T12:00:00",
            "frequency": "Hour"
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="6dbb4-1293">如需詳細資訊，請參閱 [Oracle 連接器](data-factory-onprem-oracle-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1293">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#dataset-properties) article.</span></span>

### <a name="oracle-source-in-copy-activity"></a><span data-ttu-id="6dbb4-1294">複製活動中的 Oracle 來源</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1294">Oracle Source in Copy Activity</span></span>
<span data-ttu-id="6dbb4-1295">如果您從 Oracle 資料庫複製資料，請將複製活動的 **source type** 設為 **OracleSource**，並在 **source** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1295">If you are copying data from an Oracle database, set the **source type** of the copy activity to **OracleSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="6dbb4-1296">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1296">Property</span></span> | <span data-ttu-id="6dbb4-1297">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1297">Description</span></span> | <span data-ttu-id="6dbb4-1298">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1298">Allowed values</span></span> | <span data-ttu-id="6dbb4-1299">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1299">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-1300">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1300">oracleReaderQuery</span></span> |<span data-ttu-id="6dbb4-1301">使用自訂查詢來讀取資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1301">Use the custom query to read data.</span></span> |<span data-ttu-id="6dbb4-1302">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1302">SQL query string.</span></span> <span data-ttu-id="6dbb4-1303">例如：`select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1303">For example: `select * from MyTable`</span></span> <br/><br/><span data-ttu-id="6dbb4-1304">如果未指定，執行的 SQL 陳述式：`select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1304">If not specified, the SQL statement that is executed: `select * from MyTable`</span></span> |<span data-ttu-id="6dbb4-1305">否 (如果已指定 **dataset** 的 **tableName**)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1305">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-1306">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1306">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "OracletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " OracleInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "OracleSource",
                    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
            "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="6dbb4-1307">如需詳細資訊，請參閱 [Oracle 連接器](data-factory-onprem-oracle-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1307">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

### <a name="oracle-sink-in-copy-activity"></a><span data-ttu-id="6dbb4-1308">複製活動中的 Oracle 接收</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1308">Oracle Sink in Copy Activity</span></span>
<span data-ttu-id="6dbb4-1309">如果您將資料複製到 Oracle 資料庫，請將複製活動的 **sink type** 設為 **OracleSink**，並在 **sink** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1309">If you are copying data to am Oracle database, set the **sink type** of the copy activity to **OracleSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="6dbb4-1310">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1310">Property</span></span> | <span data-ttu-id="6dbb4-1311">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1311">Description</span></span> | <span data-ttu-id="6dbb4-1312">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1312">Allowed values</span></span> | <span data-ttu-id="6dbb4-1313">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1313">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-1314">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1314">writeBatchTimeout</span></span> |<span data-ttu-id="6dbb4-1315">在逾時前等待批次插入作業完成的時間。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1315">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="6dbb4-1316">時間範圍</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1316">timespan</span></span><br/><br/> <span data-ttu-id="6dbb4-1317">範例：00:30:00 (30 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1317">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="6dbb4-1318">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1318">No</span></span> |
| <span data-ttu-id="6dbb4-1319">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1319">writeBatchSize</span></span> |<span data-ttu-id="6dbb4-1320">當緩衝區大小達到 writeBatchSize 時，將資料插入 SQL 資料表中</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1320">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="6dbb4-1321">整數 (資料列數目)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1321">Integer (number of rows)</span></span> |<span data-ttu-id="6dbb4-1322">否 (預設值：100)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1322">No (default: 100)</span></span> |
| <span data-ttu-id="6dbb4-1323">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1323">sqlWriterCleanupScript</span></span> |<span data-ttu-id="6dbb4-1324">指定要讓「複製活動」執行的查詢，以便清除特定分割的資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1324">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="6dbb4-1325">查詢陳述式。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1325">A query statement.</span></span> |<span data-ttu-id="6dbb4-1326">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1326">No</span></span> |
| <span data-ttu-id="6dbb4-1327">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1327">sliceIdentifierColumnName</span></span> |<span data-ttu-id="6dbb4-1328">指定要讓「複製活動」以自動產生的分割識別碼填入的資料行名稱，這可在重新執行時用來清除特定分割的資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1328">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="6dbb4-1329">資料類型為 binary(32) 之資料行的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1329">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="6dbb4-1330">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1330">No</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-1331">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1331">Example</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-05T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoOracle",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "OracleOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "OracleSink"
                }
            },
            "scheduler": {
                "frequency": "Day",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="6dbb4-1332">如需詳細資訊，請參閱 [Oracle 連接器](data-factory-onprem-oracle-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1332">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

## <a name="postgresql"></a><span data-ttu-id="6dbb4-1333">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1333">PostgreSQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="6dbb4-1334">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1334">Linked service</span></span>
<span data-ttu-id="6dbb4-1335">若要定義 PostgreSQL 連結服務，請將連結服務的 **type** 設為 **OnPremisesPostgreSql**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1335">To define a PostgreSQL linked service, set the **type** of the linked service to **OnPremisesPostgreSql**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="6dbb4-1336">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1336">Property</span></span> | <span data-ttu-id="6dbb4-1337">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1337">Description</span></span> | <span data-ttu-id="6dbb4-1338">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1338">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-1339">伺服器</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1339">server</span></span> |<span data-ttu-id="6dbb4-1340">PostgreSQL 伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1340">Name of the PostgreSQL server.</span></span> |<span data-ttu-id="6dbb4-1341">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1341">Yes</span></span> |
| <span data-ttu-id="6dbb4-1342">資料庫</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1342">database</span></span> |<span data-ttu-id="6dbb4-1343">PostgreSQL 資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1343">Name of the PostgreSQL database.</span></span> |<span data-ttu-id="6dbb4-1344">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1344">Yes</span></span> |
| <span data-ttu-id="6dbb4-1345">結構描述</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1345">schema</span></span> |<span data-ttu-id="6dbb4-1346">在資料庫中的結構描述名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1346">Name of the schema in the database.</span></span> <span data-ttu-id="6dbb4-1347">結構描述名稱會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1347">The schema name is case-sensitive.</span></span> |<span data-ttu-id="6dbb4-1348">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1348">No</span></span> |
| <span data-ttu-id="6dbb4-1349">authenticationType</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1349">authenticationType</span></span> |<span data-ttu-id="6dbb4-1350">用來連接到 PostgreSQL 資料庫的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1350">Type of authentication used to connect to the PostgreSQL database.</span></span> <span data-ttu-id="6dbb4-1351">可能的值為：匿名、基本和 Windows。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1351">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="6dbb4-1352">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1352">Yes</span></span> |
| <span data-ttu-id="6dbb4-1353">username</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1353">username</span></span> |<span data-ttu-id="6dbb4-1354">如果您使用基本或 Windows 驗證，請指定使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1354">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="6dbb4-1355">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1355">No</span></span> |
| <span data-ttu-id="6dbb4-1356">password</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1356">password</span></span> |<span data-ttu-id="6dbb4-1357">指定您為使用者名稱所指定之使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1357">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="6dbb4-1358">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1358">No</span></span> |
| <span data-ttu-id="6dbb4-1359">gatewayName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1359">gatewayName</span></span> |<span data-ttu-id="6dbb4-1360">Data Factory 服務應該用來連接到內部部署 PostgreSQL 資料庫的閘道器名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1360">Name of the gateway that the Data Factory service should use to connect to the on-premises PostgreSQL database.</span></span> |<span data-ttu-id="6dbb4-1361">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1361">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-1362">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1362">Example</span></span>

```json
{
    "name": "OnPremPostgreSqlLinkedService",
    "properties": {
        "type": "OnPremisesPostgreSql",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
<span data-ttu-id="6dbb4-1363">如需詳細資訊，請參閱 [PostgreSQL 連接器](data-factory-onprem-postgresql-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1363">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="6dbb4-1364">Dataset</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1364">Dataset</span></span>
<span data-ttu-id="6dbb4-1365">若要定義 PostgreSQL 資料集，請將資料集的 **type** 設為 **RelationalTable**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1365">To define a PostgreSQL dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="6dbb4-1366">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1366">Property</span></span> | <span data-ttu-id="6dbb4-1367">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1367">Description</span></span> | <span data-ttu-id="6dbb4-1368">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1368">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-1369">tableName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1369">tableName</span></span> |<span data-ttu-id="6dbb4-1370">PostgreSQL 資料庫執行個體中連結服務所參照的資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1370">Name of the table in the PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="6dbb4-1371">tableName 會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1371">The tableName is case-sensitive.</span></span> |<span data-ttu-id="6dbb4-1372">否 (如果已指定 **RelationalSource** 的 **query**)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1372">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-1373">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1373">Example</span></span>
```json
{
    "name": "PostgreSqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremPostgreSqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="6dbb4-1374">如需詳細資訊，請參閱 [PostgreSQL 連接器](data-factory-onprem-postgresql-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1374">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="6dbb4-1375">複製活動中的關聯式來源</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1375">Relational Source in Copy Activity</span></span>
<span data-ttu-id="6dbb4-1376">如果您從 PostgreSQL 資料庫複製資料，請將複製活動的 **source type** 設為 **RelationalSource**，並在 **source** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1376">If you are copying data from a PostgreSQL database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="6dbb4-1377">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1377">Property</span></span> | <span data-ttu-id="6dbb4-1378">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1378">Description</span></span> | <span data-ttu-id="6dbb4-1379">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1379">Allowed values</span></span> | <span data-ttu-id="6dbb4-1380">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1380">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-1381">query</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1381">query</span></span> |<span data-ttu-id="6dbb4-1382">使用自訂查詢來讀取資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1382">Use the custom query to read data.</span></span> |<span data-ttu-id="6dbb4-1383">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1383">SQL query string.</span></span> <span data-ttu-id="6dbb4-1384">例如："query": "select * from \"MySchema\".\"MyTable\""。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1384">For example: "query": "select * from \"MySchema\".\"MyTable\"".</span></span> |<span data-ttu-id="6dbb4-1385">否 (如果已指定 **dataset** 的 **tableName**)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1385">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-1386">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1386">Example</span></span>

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"public\".\"usstates\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "PostgreSqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobPostgreSqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "PostgreSqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="6dbb4-1387">如需詳細資訊，請參閱 [PostgreSQL 連接器](data-factory-onprem-postgresql-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1387">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#copy-activity-properties) article.</span></span>

## <a name="sap-business-warehouse"></a><span data-ttu-id="6dbb4-1388">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1388">SAP Business Warehouse</span></span>


### <a name="linked-service"></a><span data-ttu-id="6dbb4-1389">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1389">Linked service</span></span>
<span data-ttu-id="6dbb4-1390">若要定義 SAP Business Warehouse (BW) 連結服務，請將連結服務的 **type** 設為 **SapBw**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1390">To define a SAP Business Warehouse (BW) linked service, set the **type** of the linked service to **SapBw**, and specify following properties in the **typeProperties** section:</span></span>  

<span data-ttu-id="6dbb4-1391">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1391">Property</span></span> | <span data-ttu-id="6dbb4-1392">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1392">Description</span></span> | <span data-ttu-id="6dbb4-1393">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1393">Allowed values</span></span> | <span data-ttu-id="6dbb4-1394">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1394">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="6dbb4-1395">伺服器</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1395">server</span></span> | <span data-ttu-id="6dbb4-1396">SAP BW 執行個體所在之伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1396">Name of the server on which the SAP BW instance resides.</span></span> | <span data-ttu-id="6dbb4-1397">字串</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1397">string</span></span> | <span data-ttu-id="6dbb4-1398">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1398">Yes</span></span>
<span data-ttu-id="6dbb4-1399">systemNumber</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1399">systemNumber</span></span> | <span data-ttu-id="6dbb4-1400">SAP BW 系統的系統編號。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1400">System number of the SAP BW system.</span></span> | <span data-ttu-id="6dbb4-1401">以字串表示的二位數十進位數字。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1401">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="6dbb4-1402">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1402">Yes</span></span>
<span data-ttu-id="6dbb4-1403">clientId</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1403">clientId</span></span> | <span data-ttu-id="6dbb4-1404">SAP W 系統中用戶端的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1404">Client ID of the client in the SAP W system.</span></span> | <span data-ttu-id="6dbb4-1405">以字串表示的三位數十進位數字。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1405">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="6dbb4-1406">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1406">Yes</span></span>
<span data-ttu-id="6dbb4-1407">username</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1407">username</span></span> | <span data-ttu-id="6dbb4-1408">具有 SAP 伺服器存取權之使用者的名稱</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1408">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="6dbb4-1409">字串</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1409">string</span></span> | <span data-ttu-id="6dbb4-1410">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1410">Yes</span></span>
<span data-ttu-id="6dbb4-1411">password</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1411">password</span></span> | <span data-ttu-id="6dbb4-1412">使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1412">Password for the user.</span></span> | <span data-ttu-id="6dbb4-1413">字串</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1413">string</span></span> | <span data-ttu-id="6dbb4-1414">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1414">Yes</span></span>
<span data-ttu-id="6dbb4-1415">gatewayName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1415">gatewayName</span></span> | <span data-ttu-id="6dbb4-1416">資料處理站服務應該用來連線至內部部署 SAP BW 執行個體的閘道器名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1416">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP BW instance.</span></span> | <span data-ttu-id="6dbb4-1417">字串</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1417">string</span></span> | <span data-ttu-id="6dbb4-1418">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1418">Yes</span></span>
<span data-ttu-id="6dbb4-1419">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1419">encryptedCredential</span></span> | <span data-ttu-id="6dbb4-1420">加密的認證字串。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1420">The encrypted credential string.</span></span> | <span data-ttu-id="6dbb4-1421">string</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1421">string</span></span> | <span data-ttu-id="6dbb4-1422">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1422">No</span></span>

#### <a name="example"></a><span data-ttu-id="6dbb4-1423">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1423">Example</span></span>

```json
{
    "name": "SapBwLinkedService",
    "properties": {
        "type": "SapBw",
        "typeProperties": {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="6dbb4-1424">如需詳細資訊，請參閱 [SAP Business Warehouse 連接器](data-factory-sap-business-warehouse-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1424">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="6dbb4-1425">Dataset</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1425">Dataset</span></span>
<span data-ttu-id="6dbb4-1426">若要定義 SAP BW 資料集，請將資料集的 **type** 設為 **RelationalTable**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1426">To define a SAP BW dataset, set the **type** of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="6dbb4-1427">**RelationalTable** 類型的 SAP BW 資料集不支援類型專用的屬性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1427">There are no type-specific properties supported for the SAP BW dataset of type **RelationalTable**.</span></span>  

#### <a name="example"></a><span data-ttu-id="6dbb4-1428">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1428">Example</span></span>

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="6dbb4-1429">如需詳細資訊，請參閱 [SAP Business Warehouse 連接器](data-factory-sap-business-warehouse-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1429">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="6dbb4-1430">複製活動中的關聯式來源</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1430">Relational Source in Copy Activity</span></span>
<span data-ttu-id="6dbb4-1431">如果您從 SAP Business Warehouse 複製資料，請將複製活動的 **source type** 設為 **RelationalSource**，並在 **source** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1431">If you are copying data from SAP Business Warehouse, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="6dbb4-1432">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1432">Property</span></span> | <span data-ttu-id="6dbb4-1433">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1433">Description</span></span> | <span data-ttu-id="6dbb4-1434">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1434">Allowed values</span></span> | <span data-ttu-id="6dbb4-1435">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1435">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-1436">query</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1436">query</span></span> | <span data-ttu-id="6dbb4-1437">指定 MDX 查詢從 SAP BW 執行個體讀取資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1437">Specifies the MDX query to read data from the SAP BW instance.</span></span> | <span data-ttu-id="6dbb4-1438">MDX 查詢。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1438">MDX query.</span></span> | <span data-ttu-id="6dbb4-1439">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1439">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-1440">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1440">Example</span></span>

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<MDX query for SAP BW>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapBwDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapBwToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

<span data-ttu-id="6dbb4-1441">如需詳細資訊，請參閱 [SAP Business Warehouse 連接器](data-factory-sap-business-warehouse-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1441">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sap-hana"></a><span data-ttu-id="6dbb4-1442">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1442">SAP HANA</span></span>

### <a name="linked-service"></a><span data-ttu-id="6dbb4-1443">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1443">Linked service</span></span>
<span data-ttu-id="6dbb4-1444">若要定義 SAP HANA 連結服務，請將連結服務的 **type** 設為 **SapHana**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1444">To define a SAP HANA linked service, set the **type** of the linked service to **SapHana**, and specify following properties in the **typeProperties** section:</span></span>  

<span data-ttu-id="6dbb4-1445">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1445">Property</span></span> | <span data-ttu-id="6dbb4-1446">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1446">Description</span></span> | <span data-ttu-id="6dbb4-1447">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1447">Allowed values</span></span> | <span data-ttu-id="6dbb4-1448">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1448">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="6dbb4-1449">伺服器</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1449">server</span></span> | <span data-ttu-id="6dbb4-1450">SAP Hana 執行個體所在之伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1450">Name of the server on which the SAP HANA instance resides.</span></span> <span data-ttu-id="6dbb4-1451">如果您的伺服器使用自訂連接埠，指定 `server:port`。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1451">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="6dbb4-1452">字串</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1452">string</span></span> | <span data-ttu-id="6dbb4-1453">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1453">Yes</span></span>
<span data-ttu-id="6dbb4-1454">authenticationType</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1454">authenticationType</span></span> | <span data-ttu-id="6dbb4-1455">驗證類型。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1455">Type of authentication.</span></span> | <span data-ttu-id="6dbb4-1456">字串。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1456">string.</span></span> <span data-ttu-id="6dbb4-1457">"Basic" 或 "Windows"</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1457">"Basic" or "Windows"</span></span> | <span data-ttu-id="6dbb4-1458">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1458">Yes</span></span> 
<span data-ttu-id="6dbb4-1459">username</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1459">username</span></span> | <span data-ttu-id="6dbb4-1460">具有 SAP 伺服器存取權之使用者的名稱</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1460">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="6dbb4-1461">字串</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1461">string</span></span> | <span data-ttu-id="6dbb4-1462">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1462">Yes</span></span>
<span data-ttu-id="6dbb4-1463">password</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1463">password</span></span> | <span data-ttu-id="6dbb4-1464">使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1464">Password for the user.</span></span> | <span data-ttu-id="6dbb4-1465">字串</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1465">string</span></span> | <span data-ttu-id="6dbb4-1466">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1466">Yes</span></span>
<span data-ttu-id="6dbb4-1467">gatewayName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1467">gatewayName</span></span> | <span data-ttu-id="6dbb4-1468">Data Factory 服務應該用來連接到內部部署 SAP Hana 執行個體的閘道器名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1468">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP HANA instance.</span></span> | <span data-ttu-id="6dbb4-1469">字串</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1469">string</span></span> | <span data-ttu-id="6dbb4-1470">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1470">Yes</span></span>
<span data-ttu-id="6dbb4-1471">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1471">encryptedCredential</span></span> | <span data-ttu-id="6dbb4-1472">加密的認證字串。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1472">The encrypted credential string.</span></span> | <span data-ttu-id="6dbb4-1473">string</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1473">string</span></span> | <span data-ttu-id="6dbb4-1474">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1474">No</span></span>

#### <a name="example"></a><span data-ttu-id="6dbb4-1475">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1475">Example</span></span>

```json
{
    "name": "SapHanaLinkedService",
    "properties": {
        "type": "SapHana",
        "typeProperties": {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```
<span data-ttu-id="6dbb4-1476">如需詳細資訊，請參閱 [SAP HANA 連接器](data-factory-sap-hana-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1476">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#linked-service-properties) article.</span></span>
 
### <a name="dataset"></a><span data-ttu-id="6dbb4-1477">Dataset</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1477">Dataset</span></span>
<span data-ttu-id="6dbb4-1478">若要定義 SAP HANA 資料集，請將資料集的 **type** 設為 **RelationalTable**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1478">To define a SAP HANA dataset, set the **type** of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="6dbb4-1479">沒有類型特定的屬性支援 **RelationalTable** 的 SAP HANA 資料集類型。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1479">There are no type-specific properties supported for the SAP HANA dataset of type **RelationalTable**.</span></span> 

#### <a name="example"></a><span data-ttu-id="6dbb4-1480">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1480">Example</span></span>

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="6dbb4-1481">如需詳細資訊，請參閱 [SAP HANA 連接器](data-factory-sap-hana-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1481">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="6dbb4-1482">複製活動中的關聯式來源</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1482">Relational Source in Copy Activity</span></span>
<span data-ttu-id="6dbb4-1483">如果您從 SAP HANA 資料存放區複製資料，請將複製活動的 **source type** 設為 **RelationalSource**，並在 **source** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1483">If you are copying data from a SAP HANA data store, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="6dbb4-1484">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1484">Property</span></span> | <span data-ttu-id="6dbb4-1485">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1485">Description</span></span> | <span data-ttu-id="6dbb4-1486">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1486">Allowed values</span></span> | <span data-ttu-id="6dbb4-1487">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1487">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-1488">query</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1488">query</span></span> | <span data-ttu-id="6dbb4-1489">指定 SQL 查詢從 SAP HANA 執行個體讀取資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1489">Specifies the SQL query to read data from the SAP HANA instance.</span></span> | <span data-ttu-id="6dbb4-1490">SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1490">SQL query.</span></span> | <span data-ttu-id="6dbb4-1491">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1491">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="6dbb4-1492">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1492">Example</span></span>


```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<SQL Query for HANA>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapHanaDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapHanaToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

<span data-ttu-id="6dbb4-1493">如需詳細資訊，請參閱 [SAP HANA 連接器](data-factory-sap-hana-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1493">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#copy-activity-properties) article.</span></span>


## <a name="sql-server"></a><span data-ttu-id="6dbb4-1494">SQL Server</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1494">SQL Server</span></span>

### <a name="linked-service"></a><span data-ttu-id="6dbb4-1495">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1495">Linked service</span></span>
<span data-ttu-id="6dbb4-1496">您可以建立 **OnPremisesSqlServer** 類型的連結服務，以將內部部署 SQL Server 資料庫連結至資料處理站。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1496">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span></span> <span data-ttu-id="6dbb4-1497">下表提供內部部署 SQL Server 連結服務專屬 JSON 元素的描述。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1497">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span></span>

<span data-ttu-id="6dbb4-1498">下表提供 SQL Server 連結服務專屬 JSON 元素的描述。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1498">The following table provides description for JSON elements specific to SQL Server linked service.</span></span>

| <span data-ttu-id="6dbb4-1499">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1499">Property</span></span> | <span data-ttu-id="6dbb4-1500">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1500">Description</span></span> | <span data-ttu-id="6dbb4-1501">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1501">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-1502">類型</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1502">type</span></span> |<span data-ttu-id="6dbb4-1503">類型屬性應設為： **OnPremisesSqlServer**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1503">The type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="6dbb4-1504">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1504">Yes</span></span> |
| <span data-ttu-id="6dbb4-1505">connectionString</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1505">connectionString</span></span> |<span data-ttu-id="6dbb4-1506">指定使用 SQL 驗證或 Windows 驗證連接至內部部署 SQL Server 資料庫所需的 connectionString 資訊。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1506">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="6dbb4-1507">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1507">Yes</span></span> |
| <span data-ttu-id="6dbb4-1508">gatewayName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1508">gatewayName</span></span> |<span data-ttu-id="6dbb4-1509">Data Factory 服務應該用來連接到內部部署 SQL Server 資料庫的閘道器名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1509">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span></span> |<span data-ttu-id="6dbb4-1510">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1510">Yes</span></span> |
| <span data-ttu-id="6dbb4-1511">username</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1511">username</span></span> |<span data-ttu-id="6dbb4-1512">如果您使用「Windows 驗證」，請指定使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1512">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="6dbb4-1513">範例︰**domainname\\username**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1513">Example: **domainname\\username**.</span></span> |<span data-ttu-id="6dbb4-1514">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1514">No</span></span> |
| <span data-ttu-id="6dbb4-1515">password</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1515">password</span></span> |<span data-ttu-id="6dbb4-1516">指定您為使用者名稱所指定之使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1516">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="6dbb4-1517">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1517">No</span></span> |

<span data-ttu-id="6dbb4-1518">您可以使用 **New-AzureRmDataFactoryEncryptValue** Cmdlet 加密認證，並在連接字串中使用這些認證，如下列範例所示 (**EncryptedCredential** 屬性)：</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1518">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span></span>  

```json
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="6dbb4-1519">範例：用於 SQL 驗證的 JSON</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1519">Example: JSON for using SQL Authentication</span></span>

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="6dbb4-1520">範例：用於 Windows 驗證的 JSON</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1520">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="6dbb4-1521">如果已指定使用者名稱和密碼，閘道就會使用它們來模擬指定的使用者帳戶，以連線到內部部署 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1521">If username and password are specified, gateway uses them to impersonate the specified user account to connect to the on-premises SQL Server database.</span></span> <span data-ttu-id="6dbb4-1522">否則，閘道會使用閘道的安全性內容 (其啟動帳戶) 直接連線到 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1522">Otherwise, gateway connects to the SQL Server directly with the security context of Gateway (its startup account).</span></span>

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="6dbb4-1523">如需詳細資訊，請參閱 [SQL Server 連接器](data-factory-sqlserver-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1523">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="6dbb4-1524">Dataset</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1524">Dataset</span></span>
<span data-ttu-id="6dbb4-1525">若要定義 SQL Server 資料集，請將資料集的 **type** 設為 **SqlServerTable**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1525">To define a SQL Server dataset, set the **type** of the dataset to **SqlServerTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="6dbb4-1526">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1526">Property</span></span> | <span data-ttu-id="6dbb4-1527">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1527">Description</span></span> | <span data-ttu-id="6dbb4-1528">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1528">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-1529">tableName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1529">tableName</span></span> |<span data-ttu-id="6dbb4-1530">SQL Server Database 執行個體中連結服務所參照的資料表或檢視名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1530">Name of the table or view in the SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="6dbb4-1531">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1531">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-1532">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1532">Example</span></span>
```json
{
    "name": "SqlServerInput",
    "properties": {
        "type": "SqlServerTable",
        "linkedServiceName": "SqlServerLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="6dbb4-1533">如需詳細資訊，請參閱 [SQL Server 連接器](data-factory-sqlserver-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1533">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="6dbb4-1534">複製活動中的 Sql 來源</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1534">Sql Source in Copy Activity</span></span>
<span data-ttu-id="6dbb4-1535">如果您從 SQL Server 資料庫複製資料，請將複製活動的 **source type** 設為 **SqlSource**，並在 **source** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1535">If you are copying data from a SQL Server database, set the **source type** of the copy activity to **SqlSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="6dbb4-1536">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1536">Property</span></span> | <span data-ttu-id="6dbb4-1537">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1537">Description</span></span> | <span data-ttu-id="6dbb4-1538">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1538">Allowed values</span></span> | <span data-ttu-id="6dbb4-1539">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1539">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-1540">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1540">sqlReaderQuery</span></span> |<span data-ttu-id="6dbb4-1541">使用自訂查詢來讀取資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1541">Use the custom query to read data.</span></span> |<span data-ttu-id="6dbb4-1542">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1542">SQL query string.</span></span> <span data-ttu-id="6dbb4-1543">例如： `select * from MyTable`。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1543">For example: `select * from MyTable`.</span></span> <span data-ttu-id="6dbb4-1544">可以參考輸入資料集所參考資料庫中的多個資料表。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1544">May reference multiple tables from the database referenced by the input dataset.</span></span> <span data-ttu-id="6dbb4-1545">如果未指定，執行的 SQL 陳述式：select from MyTable。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1545">If not specified, the SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="6dbb4-1546">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1546">No</span></span> |
| <span data-ttu-id="6dbb4-1547">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1547">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="6dbb4-1548">從來源資料表讀取資料的預存程序名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1548">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="6dbb4-1549">預存程序的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1549">Name of the stored procedure.</span></span> |<span data-ttu-id="6dbb4-1550">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1550">No</span></span> |
| <span data-ttu-id="6dbb4-1551">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1551">storedProcedureParameters</span></span> |<span data-ttu-id="6dbb4-1552">預存程序的參數。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1552">Parameters for the stored procedure.</span></span> |<span data-ttu-id="6dbb4-1553">名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1553">Name/value pairs.</span></span> <span data-ttu-id="6dbb4-1554">參數的名稱和大小寫必須符合預存程序參數的名稱和大小寫。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1554">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="6dbb4-1555">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1555">No</span></span> |

<span data-ttu-id="6dbb4-1556">如果已為 SqlSource 指定 **sqlReaderQuery** ，複製活動會針對 SQL Server 資料庫來源執行這項查詢以取得資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1556">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the SQL Server Database source to get the data.</span></span>

<span data-ttu-id="6dbb4-1557">或者，您可以藉由指定 **sqlReaderStoredProcedureName** 和 **storedProcedureParameters** (如果預存程序接受參數) 來指定預存程序。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1557">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="6dbb4-1558">如果您未指定 sqlReaderQuery 或 sqlReaderStoredProcedureName，系統就會使用 structure 區段中定義的資料行來建立一個要對「SQL Server 資料庫」執行的 select 查詢。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1558">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="6dbb4-1559">如果資料集定義沒有結構，則會從資料表中選取所有資料行。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1559">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

> [!NOTE]
> <span data-ttu-id="6dbb4-1560">當您使用 **sqlReaderStoredProcedureName** 時，仍必須為資料集 JSON 中的 **tableName** 屬性指定值。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1560">When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON.</span></span> <span data-ttu-id="6dbb4-1561">雖然目前尚未針對此資料表來進行驗證。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1561">There are no validations performed against this table though.</span></span>


#### <a name="example"></a><span data-ttu-id="6dbb4-1562">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1562">Example</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="6dbb4-1563">在此範例中，已為 SqlSource 指定 **sqlReaderQuery** 。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1563">In this example, **sqlReaderQuery** is specified for the SqlSource.</span></span> <span data-ttu-id="6dbb4-1564">複製活動會針對 SQL Server 資料庫來源執行這項查詢以取得資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1564">The Copy Activity runs this query against the SQL Server Database source to get the data.</span></span> <span data-ttu-id="6dbb4-1565">或者，您可以藉由指定 **sqlReaderStoredProcedureName** 和 **storedProcedureParameters** (如果預存程序接受參數) 來指定預存程序。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1565">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span> <span data-ttu-id="6dbb4-1566">sqlReaderQuery 可以參考輸入資料集所參考之資料庫內的多個資料表。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1566">The sqlReaderQuery can reference multiple tables within the database referenced by the input dataset.</span></span> <span data-ttu-id="6dbb4-1567">這不限於只有設定為資料集之 tableName typeProperty 的資料表。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1567">It is not limited to only the table set as the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="6dbb4-1568">如果您未指定 sqlReaderQuery 或 sqlReaderStoredProcedureName，系統就會使用 structure 區段中定義的資料行來建立一個要對「SQL Server 資料庫」執行的 select 查詢。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1568">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="6dbb4-1569">如果資料集定義沒有結構，則會從資料表中選取所有資料行。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1569">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

<span data-ttu-id="6dbb4-1570">如需詳細資訊，請參閱 [SQL Server 連接器](data-factory-sqlserver-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1570">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="6dbb4-1571">複製活動中的 Sql 接收</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1571">Sql Sink in Copy Activity</span></span>
<span data-ttu-id="6dbb4-1572">如果您將資料複製到 SQL Server 資料庫，請將複製活動的 **sink type** 設為 **SqlSink**，並在 **sink** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1572">If you are copying data to a SQL Server database, set the **sink type** of the copy activity to **SqlSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="6dbb4-1573">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1573">Property</span></span> | <span data-ttu-id="6dbb4-1574">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1574">Description</span></span> | <span data-ttu-id="6dbb4-1575">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1575">Allowed values</span></span> | <span data-ttu-id="6dbb4-1576">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1576">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-1577">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1577">writeBatchTimeout</span></span> |<span data-ttu-id="6dbb4-1578">在逾時前等待批次插入作業完成的時間。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1578">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="6dbb4-1579">時間範圍</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1579">timespan</span></span><br/><br/> <span data-ttu-id="6dbb4-1580">範例：“00:30:00” (30 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1580">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="6dbb4-1581">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1581">No</span></span> |
| <span data-ttu-id="6dbb4-1582">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1582">writeBatchSize</span></span> |<span data-ttu-id="6dbb4-1583">當緩衝區大小達到 writeBatchSize 時，將資料插入 SQL 資料表中</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1583">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="6dbb4-1584">整數 (資料列數目)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1584">Integer (number of rows)</span></span> |<span data-ttu-id="6dbb4-1585">否 (預設值：10000)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1585">No (default: 10000)</span></span> |
| <span data-ttu-id="6dbb4-1586">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1586">sqlWriterCleanupScript</span></span> |<span data-ttu-id="6dbb4-1587">指定要讓「複製活動」執行的查詢，以便清除特定分割的資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1587">Specify query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="6dbb4-1588">如需詳細資訊，請參閱 [可重複性](#repeatability-during-copy) 一節。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1588">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="6dbb4-1589">查詢陳述式。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1589">A query statement.</span></span> |<span data-ttu-id="6dbb4-1590">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1590">No</span></span> |
| <span data-ttu-id="6dbb4-1591">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1591">sliceIdentifierColumnName</span></span> |<span data-ttu-id="6dbb4-1592">指定要讓「複製活動」以自動產生的分割識別碼填入的資料行名稱，這可在重新執行時用來清除特定分割的資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1592">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> <span data-ttu-id="6dbb4-1593">如需詳細資訊，請參閱 [可重複性](#repeatability-during-copy) 一節。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1593">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="6dbb4-1594">資料類型為 binary(32) 之資料行的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1594">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="6dbb4-1595">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1595">No</span></span> |
| <span data-ttu-id="6dbb4-1596">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1596">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="6dbb4-1597">將資料更新插入 (更新/插入) 目標資料表中的預存程序名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1597">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="6dbb4-1598">預存程序的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1598">Name of the stored procedure.</span></span> |<span data-ttu-id="6dbb4-1599">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1599">No</span></span> |
| <span data-ttu-id="6dbb4-1600">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1600">storedProcedureParameters</span></span> |<span data-ttu-id="6dbb4-1601">預存程序的參數。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1601">Parameters for the stored procedure.</span></span> |<span data-ttu-id="6dbb4-1602">名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1602">Name/value pairs.</span></span> <span data-ttu-id="6dbb4-1603">參數的名稱和大小寫必須符合預存程序參數的名稱和大小寫。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1603">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="6dbb4-1604">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1604">No</span></span> |
| <span data-ttu-id="6dbb4-1605">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1605">sqlWriterTableType</span></span> |<span data-ttu-id="6dbb4-1606">指定要在預存程序中使用的資料表類型名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1606">Specify table type name to be used in the stored procedure.</span></span> <span data-ttu-id="6dbb4-1607">複製活動可讓正在移動的資料可用於此資料表類型的暫存資料表。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1607">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="6dbb4-1608">然後，預存程序程式碼可以合併正在複製的資料與現有的資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1608">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="6dbb4-1609">資料表類型名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1609">A table type name.</span></span> |<span data-ttu-id="6dbb4-1610">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1610">No</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-1611">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1611">Example</span></span>
<span data-ttu-id="6dbb4-1612">此管線包含「複製活動」，該活動已設定為使用這些輸入和輸出資料集，並且排定為每小時執行。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1612">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="6dbb4-1613">在管線 JSON 定義中，**source** 類型設為 **BlobSource**，而 **sink** 類型設為 **SqlSink**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1613">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": " SqlServerOutput "
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="6dbb4-1614">如需詳細資訊，請參閱 [SQL Server 連接器](data-factory-sqlserver-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1614">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sybase"></a><span data-ttu-id="6dbb4-1615">Sybase</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1615">Sybase</span></span>

### <a name="linked-service"></a><span data-ttu-id="6dbb4-1616">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1616">Linked service</span></span>
<span data-ttu-id="6dbb4-1617">若要定義 Sybase 連結服務，請將連結服務的 **type** 設為 **OnPremisesSybase**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1617">To define a Sybase linked service, set the **type** of the linked service to **OnPremisesSybase**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="6dbb4-1618">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1618">Property</span></span> | <span data-ttu-id="6dbb4-1619">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1619">Description</span></span> | <span data-ttu-id="6dbb4-1620">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1620">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-1621">伺服器</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1621">server</span></span> |<span data-ttu-id="6dbb4-1622">Sybase 伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1622">Name of the Sybase server.</span></span> |<span data-ttu-id="6dbb4-1623">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1623">Yes</span></span> |
| <span data-ttu-id="6dbb4-1624">資料庫</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1624">database</span></span> |<span data-ttu-id="6dbb4-1625">Sybase 資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1625">Name of the Sybase database.</span></span> |<span data-ttu-id="6dbb4-1626">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1626">Yes</span></span> |
| <span data-ttu-id="6dbb4-1627">結構描述</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1627">schema</span></span> |<span data-ttu-id="6dbb4-1628">在資料庫中的結構描述名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1628">Name of the schema in the database.</span></span> |<span data-ttu-id="6dbb4-1629">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1629">No</span></span> |
| <span data-ttu-id="6dbb4-1630">authenticationType</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1630">authenticationType</span></span> |<span data-ttu-id="6dbb4-1631">用來連接到 Sybase 資料庫的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1631">Type of authentication used to connect to the Sybase database.</span></span> <span data-ttu-id="6dbb4-1632">可能的值為：匿名、基本和 Windows。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1632">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="6dbb4-1633">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1633">Yes</span></span> |
| <span data-ttu-id="6dbb4-1634">username</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1634">username</span></span> |<span data-ttu-id="6dbb4-1635">如果您使用基本或 Windows 驗證，請指定使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1635">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="6dbb4-1636">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1636">No</span></span> |
| <span data-ttu-id="6dbb4-1637">password</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1637">password</span></span> |<span data-ttu-id="6dbb4-1638">指定您為使用者名稱所指定之使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1638">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="6dbb4-1639">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1639">No</span></span> |
| <span data-ttu-id="6dbb4-1640">gatewayName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1640">gatewayName</span></span> |<span data-ttu-id="6dbb4-1641">Data Factory 服務應該用來連接到內部部署 Sybase 資料庫的閘道器名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1641">Name of the gateway that the Data Factory service should use to connect to the on-premises Sybase database.</span></span> |<span data-ttu-id="6dbb4-1642">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1642">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-1643">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1643">Example</span></span>
```json
{
    "name": "OnPremSybaseLinkedService",
    "properties": {
        "type": "OnPremisesSybase",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="6dbb4-1644">如需詳細資訊，請參閱 [Sybase 連接器](data-factory-onprem-sybase-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1644">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="6dbb4-1645">Dataset</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1645">Dataset</span></span>
<span data-ttu-id="6dbb4-1646">若要定義 Sybase 資料集，請將資料集的 **type** 設為 **RelationalTable**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1646">To define a Sybase dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="6dbb4-1647">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1647">Property</span></span> | <span data-ttu-id="6dbb4-1648">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1648">Description</span></span> | <span data-ttu-id="6dbb4-1649">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1649">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-1650">tableName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1650">tableName</span></span> |<span data-ttu-id="6dbb4-1651">Sybase 資料庫執行個體中連結服務所參照的資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1651">Name of the table in the Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="6dbb4-1652">否 (如果已指定 **RelationalSource** 的 **query**)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1652">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-1653">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1653">Example</span></span>

```json
{
    "name": "SybaseDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremSybaseLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="6dbb4-1654">如需詳細資訊，請參閱 [Sybase 連接器](data-factory-onprem-sybase-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1654">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="6dbb4-1655">複製活動中的關聯式來源</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1655">Relational Source in Copy Activity</span></span>
<span data-ttu-id="6dbb4-1656">如果您從 Sybase 資料庫複製資料，請將複製活動的 **source type** 設為 **RelationalSource**，並在 **source** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1656">If you are copying data from a Sybase database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="6dbb4-1657">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1657">Property</span></span> | <span data-ttu-id="6dbb4-1658">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1658">Description</span></span> | <span data-ttu-id="6dbb4-1659">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1659">Allowed values</span></span> | <span data-ttu-id="6dbb4-1660">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1660">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-1661">query</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1661">query</span></span> |<span data-ttu-id="6dbb4-1662">使用自訂查詢來讀取資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1662">Use the custom query to read data.</span></span> |<span data-ttu-id="6dbb4-1663">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1663">SQL query string.</span></span> <span data-ttu-id="6dbb4-1664">例如： `select * from MyTable`。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1664">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="6dbb4-1665">否 (如果已指定 **dataset** 的 **tableName**)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1665">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-1666">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1666">Example</span></span>

```json
{
    "name": "CopySybaseToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from DBA.Orders"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "SybaseDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobSybaseDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SybaseToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="6dbb4-1667">如需詳細資訊，請參閱 [Sybase 連接器](data-factory-onprem-sybase-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1667">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#copy-activity-properties) article.</span></span>

## <a name="teradata"></a><span data-ttu-id="6dbb4-1668">Teradata</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1668">Teradata</span></span>

### <a name="linked-service"></a><span data-ttu-id="6dbb4-1669">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1669">Linked service</span></span>
<span data-ttu-id="6dbb4-1670">若要定義 Teradata 連結服務，請將連結服務的 **type** 設為 **OnPremisesTeradata**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1670">To define a Teradata linked service, set the **type** of the linked service to **OnPremisesTeradata**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="6dbb4-1671">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1671">Property</span></span> | <span data-ttu-id="6dbb4-1672">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1672">Description</span></span> | <span data-ttu-id="6dbb4-1673">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1673">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-1674">伺服器</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1674">server</span></span> |<span data-ttu-id="6dbb4-1675">Teradata 伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1675">Name of the Teradata server.</span></span> |<span data-ttu-id="6dbb4-1676">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1676">Yes</span></span> |
| <span data-ttu-id="6dbb4-1677">authenticationType</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1677">authenticationType</span></span> |<span data-ttu-id="6dbb4-1678">用來連接到 Teradata 資料庫的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1678">Type of authentication used to connect to the Teradata database.</span></span> <span data-ttu-id="6dbb4-1679">可能的值為：匿名、基本和 Windows。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1679">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="6dbb4-1680">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1680">Yes</span></span> |
| <span data-ttu-id="6dbb4-1681">username</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1681">username</span></span> |<span data-ttu-id="6dbb4-1682">如果您使用基本或 Windows 驗證，請指定使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1682">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="6dbb4-1683">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1683">No</span></span> |
| <span data-ttu-id="6dbb4-1684">password</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1684">password</span></span> |<span data-ttu-id="6dbb4-1685">指定您為使用者名稱所指定之使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1685">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="6dbb4-1686">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1686">No</span></span> |
| <span data-ttu-id="6dbb4-1687">gatewayName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1687">gatewayName</span></span> |<span data-ttu-id="6dbb4-1688">Data Factory 服務應該用來連接到內部部署 Teradata 資料庫的閘道器名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1688">Name of the gateway that the Data Factory service should use to connect to the on-premises Teradata database.</span></span> |<span data-ttu-id="6dbb4-1689">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1689">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-1690">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1690">Example</span></span>
```json
{
    "name": "OnPremTeradataLinkedService",
    "properties": {
        "type": "OnPremisesTeradata",
        "typeProperties": {
            "server": "<server>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="6dbb4-1691">如需詳細資訊，請參閱 [Teradata 連接器](data-factory-onprem-teradata-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1691">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="6dbb4-1692">Dataset</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1692">Dataset</span></span>
<span data-ttu-id="6dbb4-1693">若要定義 Teradata Blob 資料集，請將資料集的 **type** 設為 **RelationalTable**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1693">To define a Teradata Blob dataset, set the **type** of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="6dbb4-1694">目前沒有支援 Teradata 資料集的類型屬性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1694">Currently, there are no type properties supported for the Teradata dataset.</span></span> 

#### <a name="example"></a><span data-ttu-id="6dbb4-1695">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1695">Example</span></span>
```json
{
    "name": "TeradataDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremTeradataLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="6dbb4-1696">如需詳細資訊，請參閱 [Teradata 連接器](data-factory-onprem-teradata-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1696">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="6dbb4-1697">複製活動中的關聯式來源</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1697">Relational Source in Copy Activity</span></span>
<span data-ttu-id="6dbb4-1698">如果您從 Teradata 資料庫複製資料，請將複製活動的 **source type** 設為 **RelationalSource**，並在 **source** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1698">If you are copying data from a Teradata database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="6dbb4-1699">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1699">Property</span></span> | <span data-ttu-id="6dbb4-1700">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1700">Description</span></span> | <span data-ttu-id="6dbb4-1701">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1701">Allowed values</span></span> | <span data-ttu-id="6dbb4-1702">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1702">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-1703">query</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1703">query</span></span> |<span data-ttu-id="6dbb4-1704">使用自訂查詢來讀取資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1704">Use the custom query to read data.</span></span> |<span data-ttu-id="6dbb4-1705">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1705">SQL query string.</span></span> <span data-ttu-id="6dbb4-1706">例如： `select * from MyTable`。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1706">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="6dbb4-1707">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1707">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-1708">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1708">Example</span></span>

```json
{
    "name": "CopyTeradataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', SliceStart, SliceEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "TeradataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobTeradataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "TeradataToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="6dbb4-1709">如需詳細資訊，請參閱 [Teradata 連接器](data-factory-onprem-teradata-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1709">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#copy-activity-properties) article.</span></span>

## <a name="cassandra"></a><span data-ttu-id="6dbb4-1710">Cassandra</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1710">Cassandra</span></span>


### <a name="linked-service"></a><span data-ttu-id="6dbb4-1711">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1711">Linked service</span></span>
<span data-ttu-id="6dbb4-1712">若要定義 Cassandra 連結服務，請將連結服務的 **type** 設為 **OnPremisesCassandra**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1712">To define a Cassandra linked service, set the **type** of the linked service to **OnPremisesCassandra**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="6dbb4-1713">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1713">Property</span></span> | <span data-ttu-id="6dbb4-1714">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1714">Description</span></span> | <span data-ttu-id="6dbb4-1715">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1715">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-1716">主機</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1716">host</span></span> |<span data-ttu-id="6dbb4-1717">一或多個 Cassandra 伺服器 IP 位址或主機名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1717">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="6dbb4-1718">指定以逗號分隔的 IP 位址或主機名稱清單，以同時連線到所有伺服器。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1718">Specify a comma-separated list of IP addresses or host names to connect to all servers concurrently.</span></span> |<span data-ttu-id="6dbb4-1719">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1719">Yes</span></span> |
| <span data-ttu-id="6dbb4-1720">連接埠</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1720">port</span></span> |<span data-ttu-id="6dbb4-1721">Cassandra 伺服器用來接聽用戶端連線的 TCP 連接埠。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1721">The TCP port that the Cassandra server uses to listen for client connections.</span></span> |<span data-ttu-id="6dbb4-1722">否，預設值：9042</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1722">No, default value: 9042</span></span> |
| <span data-ttu-id="6dbb4-1723">authenticationType</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1723">authenticationType</span></span> |<span data-ttu-id="6dbb4-1724">基本或匿名</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1724">Basic, or Anonymous</span></span> |<span data-ttu-id="6dbb4-1725">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1725">Yes</span></span> |
| <span data-ttu-id="6dbb4-1726">username</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1726">username</span></span> |<span data-ttu-id="6dbb4-1727">指定使用者帳戶的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1727">Specify user name for the user account.</span></span> |<span data-ttu-id="6dbb4-1728">是，如果 authenticationType 設定為 [基本]。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1728">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="6dbb4-1729">password</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1729">password</span></span> |<span data-ttu-id="6dbb4-1730">指定使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1730">Specify password for the user account.</span></span> |<span data-ttu-id="6dbb4-1731">是，如果 authenticationType 設定為 [基本]。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1731">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="6dbb4-1732">gatewayName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1732">gatewayName</span></span> |<span data-ttu-id="6dbb4-1733">用來連線到內部部署 Cassandra 資料庫的閘道器名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1733">The name of the gateway that is used to connect to the on-premises Cassandra database.</span></span> |<span data-ttu-id="6dbb4-1734">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1734">Yes</span></span> |
| <span data-ttu-id="6dbb4-1735">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1735">encryptedCredential</span></span> |<span data-ttu-id="6dbb4-1736">由閘道加密認證。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1736">Credential encrypted by the gateway.</span></span> |<span data-ttu-id="6dbb4-1737">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1737">No</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-1738">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1738">Example</span></span>

```json
{
    "name": "CassandraLinkedService",
    "properties": {
        "type": "OnPremisesCassandra",
        "typeProperties": {
            "authenticationType": "Basic",
            "host": "<cassandra server name or IP address>",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="6dbb4-1739">如需詳細資訊，請參閱 [Cassandra 連接器](data-factory-onprem-cassandra-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1739">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="6dbb4-1740">Dataset</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1740">Dataset</span></span>
<span data-ttu-id="6dbb4-1741">若要定義 Cassandra 資料集，請將資料集的 **type** 設為 **CassandraTable**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1741">To define a Cassandra dataset, set the **type** of the dataset to **CassandraTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="6dbb4-1742">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1742">Property</span></span> | <span data-ttu-id="6dbb4-1743">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1743">Description</span></span> | <span data-ttu-id="6dbb4-1744">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1744">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-1745">keyspace</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1745">keyspace</span></span> |<span data-ttu-id="6dbb4-1746">Cassandra 資料庫中的 Keyspace 或結構描述名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1746">Name of the keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="6dbb4-1747">是 (如果未定義 **CassandraSource** 的**查詢**)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1747">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="6dbb4-1748">tableName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1748">tableName</span></span> |<span data-ttu-id="6dbb4-1749">Cassandra 資料庫中資料表的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1749">Name of the table in Cassandra database.</span></span> |<span data-ttu-id="6dbb4-1750">是 (如果未定義 **CassandraSource** 的**查詢**)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1750">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-1751">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1751">Example</span></span>

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "<key space>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="6dbb4-1752">如需詳細資訊，請參閱 [Cassandra 連接器](data-factory-onprem-cassandra-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1752">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#dataset-properties) article.</span></span> 

### <a name="cassandra-source-in-copy-activity"></a><span data-ttu-id="6dbb4-1753">複製活動中的 SCassandra 來源</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1753">Cassandra Source in Copy Activity</span></span>
<span data-ttu-id="6dbb4-1754">如果您從 Cassandra 複製資料，請將複製活動的 **source type** 設為 **CassandraSource**，並在 **source** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1754">If you are copying data from Cassandra, set the **source type** of the copy activity to **CassandraSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="6dbb4-1755">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1755">Property</span></span> | <span data-ttu-id="6dbb4-1756">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1756">Description</span></span> | <span data-ttu-id="6dbb4-1757">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1757">Allowed values</span></span> | <span data-ttu-id="6dbb4-1758">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1758">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-1759">query</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1759">query</span></span> |<span data-ttu-id="6dbb4-1760">使用自訂查詢來讀取資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1760">Use the custom query to read data.</span></span> |<span data-ttu-id="6dbb4-1761">SQL-92 查詢或 CQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1761">SQL-92 query or CQL query.</span></span> <span data-ttu-id="6dbb4-1762">請參閱 [CQL 參考資料](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1762">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="6dbb4-1763">在使用 SQL 查詢時，指定 **keyspace name.table 名稱** 來代表您想要查詢的資料表。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1763">When using SQL query, specify **keyspace name.table name** to represent the table you want to query.</span></span> |<span data-ttu-id="6dbb4-1764">否 (如果已定義資料集上的 tableName 和 keyspace)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1764">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="6dbb4-1765">consistencyLevel</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1765">consistencyLevel</span></span> |<span data-ttu-id="6dbb4-1766">一致性層級可指定必須先有多少複本回應讀取要求，才會將資料傳回用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1766">The consistency level specifies how many replicas must respond to a read request before returning data to the client application.</span></span> <span data-ttu-id="6dbb4-1767">Cassandra 會檢查要讓資料滿足讀取要求的指定複本數目。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1767">Cassandra checks the specified number of replicas for data to satisfy the read request.</span></span> |<span data-ttu-id="6dbb4-1768">ONE、TWO、THREE、QUORUM、ALL、LOCAL_QUORUM、EACH_QUORUM、LOCAL_ONE。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1768">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="6dbb4-1769">如需詳細資訊，請參閱 [設定資料一致性](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) 。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1769">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="6dbb4-1770">否。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1770">No.</span></span> <span data-ttu-id="6dbb4-1771">預設值為 ONE。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1771">Default value is ONE.</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-1772">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1772">Example</span></span>
  
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra to an Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "CassandraInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="6dbb4-1773">如需詳細資訊，請參閱 [Cassandra 連接器](data-factory-onprem-cassandra-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1773">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#copy-activity-properties) article.</span></span>

## <a name="mongodb"></a><span data-ttu-id="6dbb4-1774">MongoDB</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1774">MongoDB</span></span>

### <a name="linked-service"></a><span data-ttu-id="6dbb4-1775">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1775">Linked service</span></span>
<span data-ttu-id="6dbb4-1776">若要定義 MongoDB 連結服務，請將連結服務的 **type** 設為 **OnPremisesMongoDB**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1776">To define a MongoDB linked service, set the **type** of the linked service to **OnPremisesMongoDB**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="6dbb4-1777">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1777">Property</span></span> | <span data-ttu-id="6dbb4-1778">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1778">Description</span></span> | <span data-ttu-id="6dbb4-1779">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1779">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-1780">伺服器</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1780">server</span></span> |<span data-ttu-id="6dbb4-1781">MongoDB 伺服器的 IP 位址或主機名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1781">IP address or host name of the MongoDB server.</span></span> |<span data-ttu-id="6dbb4-1782">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1782">Yes</span></span> |
| <span data-ttu-id="6dbb4-1783">連接埠</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1783">port</span></span> |<span data-ttu-id="6dbb4-1784">MongoDB 伺服器用來接聽用戶端連線的 TCP 連接埠。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1784">TCP port that the MongoDB server uses to listen for client connections.</span></span> |<span data-ttu-id="6dbb4-1785">選用，預設值︰27017</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1785">Optional, default value: 27017</span></span> |
| <span data-ttu-id="6dbb4-1786">authenticationType</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1786">authenticationType</span></span> |<span data-ttu-id="6dbb4-1787">基本或匿名。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1787">Basic, or Anonymous.</span></span> |<span data-ttu-id="6dbb4-1788">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1788">Yes</span></span> |
| <span data-ttu-id="6dbb4-1789">username</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1789">username</span></span> |<span data-ttu-id="6dbb4-1790">用來存取 MongoDB 的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1790">User account to access MongoDB.</span></span> |<span data-ttu-id="6dbb4-1791">是 (如果使用基本驗證)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1791">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="6dbb4-1792">password</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1792">password</span></span> |<span data-ttu-id="6dbb4-1793">使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1793">Password for the user.</span></span> |<span data-ttu-id="6dbb4-1794">是 (如果使用基本驗證)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1794">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="6dbb4-1795">authSource</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1795">authSource</span></span> |<span data-ttu-id="6dbb4-1796">您想要用來檢查驗證所用之認證的 MongoDB 資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1796">Name of the MongoDB database that you want to use to check your credentials for authentication.</span></span> |<span data-ttu-id="6dbb4-1797">選用 (如果使用基本驗證)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1797">Optional (if basic authentication is used).</span></span> <span data-ttu-id="6dbb4-1798">預設值︰使用以 databaseName 屬性指定的系統管理員帳戶和資料庫。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1798">default: uses the admin account and the database specified using databaseName property.</span></span> |
| <span data-ttu-id="6dbb4-1799">databaseName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1799">databaseName</span></span> |<span data-ttu-id="6dbb4-1800">您想要存取之 MongoDB 資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1800">Name of the MongoDB database that you want to access.</span></span> |<span data-ttu-id="6dbb4-1801">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1801">Yes</span></span> |
| <span data-ttu-id="6dbb4-1802">gatewayName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1802">gatewayName</span></span> |<span data-ttu-id="6dbb4-1803">存取資料存放區之閘道的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1803">Name of the gateway that accesses the data store.</span></span> |<span data-ttu-id="6dbb4-1804">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1804">Yes</span></span> |
| <span data-ttu-id="6dbb4-1805">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1805">encryptedCredential</span></span> |<span data-ttu-id="6dbb4-1806">由閘道加密的認證。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1806">Credential encrypted by gateway.</span></span> |<span data-ttu-id="6dbb4-1807">選用</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1807">Optional</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-1808">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1808">Example</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties": {
        "type": "OnPremisesMongoDb",
        "typeProperties": {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< The IP address or host name of the MongoDB server >",
            "port": "<The number of the TCP port that the MongoDB server uses to listen for client connections.>",
            "username": "<username>",
            "password": "<password>",
            "authSource": "< The database that you want to use to check your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="6dbb4-1809">如需詳細資訊，請參閱 [MongoDB 連接器文件](data-factory-on-premises-mongodb-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1809">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#linked-service-properties)</span></span>

### <a name="dataset"></a><span data-ttu-id="6dbb4-1810">Dataset</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1810">Dataset</span></span>
<span data-ttu-id="6dbb4-1811">若要定義 MongoDB 資料集，請將資料集的 **type** 設為 **MongoDbCollection**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1811">To define a MongoDB dataset, set the **type** of the dataset to **MongoDbCollection**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="6dbb4-1812">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1812">Property</span></span> | <span data-ttu-id="6dbb4-1813">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1813">Description</span></span> | <span data-ttu-id="6dbb4-1814">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1814">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-1815">collectionName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1815">collectionName</span></span> |<span data-ttu-id="6dbb4-1816">MongoDB 資料庫中集合的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1816">Name of the collection in MongoDB database.</span></span> |<span data-ttu-id="6dbb4-1817">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1817">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-1818">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1818">Example</span></span>

```json
{
    "name": "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

<span data-ttu-id="6dbb4-1819">如需詳細資訊，請參閱 [MongoDB 連接器文件](data-factory-on-premises-mongodb-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1819">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#dataset-properties)</span></span>

#### <a name="mongodb-source-in-copy-activity"></a><span data-ttu-id="6dbb4-1820">複製活動中的 MongoDB 來源</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1820">MongoDB Source in Copy Activity</span></span>
<span data-ttu-id="6dbb4-1821">如果您從 MongoDB 複製資料，請將複製活動的 **source type** 設為 **MongoDbSource**，並在 **source** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1821">If you are copying data from MongoDB, set the **source type** of the copy activity to **MongoDbSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="6dbb4-1822">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1822">Property</span></span> | <span data-ttu-id="6dbb4-1823">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1823">Description</span></span> | <span data-ttu-id="6dbb4-1824">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1824">Allowed values</span></span> | <span data-ttu-id="6dbb4-1825">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1825">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-1826">query</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1826">query</span></span> |<span data-ttu-id="6dbb4-1827">使用自訂查詢來讀取資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1827">Use the custom query to read data.</span></span> |<span data-ttu-id="6dbb4-1828">SQL-92 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1828">SQL-92 query string.</span></span> <span data-ttu-id="6dbb4-1829">例如： `select * from MyTable`。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1829">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="6dbb4-1830">否 (如果已指定 **dataset** 的 **collectionName**)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1830">No (if **collectionName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-1831">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1831">Example</span></span>

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "MongoDbSource",
                    "query": "select * from MyTable"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MongoDbInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MongoDBToAzureBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="6dbb4-1832">如需詳細資訊，請參閱 [MongoDB 連接器文件](data-factory-on-premises-mongodb-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1832">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#copy-activity-properties)</span></span>

## <a name="amazon-s3"></a><span data-ttu-id="6dbb4-1833">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1833">Amazon S3</span></span>


### <a name="linked-service"></a><span data-ttu-id="6dbb4-1834">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1834">Linked service</span></span>
<span data-ttu-id="6dbb4-1835">若要定義 Amazon S3 連結服務，請將連結服務的 **type** 設為 **AwsAccessKey**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1835">To define an Amazon S3 linked service, set the **type** of the linked service to **AwsAccessKey**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="6dbb4-1836">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1836">Property</span></span> | <span data-ttu-id="6dbb4-1837">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1837">Description</span></span> | <span data-ttu-id="6dbb4-1838">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1838">Allowed values</span></span> | <span data-ttu-id="6dbb4-1839">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1839">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-1840">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1840">accessKeyID</span></span> |<span data-ttu-id="6dbb4-1841">密碼存取金鑰的識別碼。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1841">ID of the secret access key.</span></span> |<span data-ttu-id="6dbb4-1842">string</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1842">string</span></span> |<span data-ttu-id="6dbb4-1843">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1843">Yes</span></span> |
| <span data-ttu-id="6dbb4-1844">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1844">secretAccessKey</span></span> |<span data-ttu-id="6dbb4-1845">密碼存取金鑰本身。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1845">The secret access key itself.</span></span> |<span data-ttu-id="6dbb4-1846">加密的密碼字串</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1846">Encrypted secret string</span></span> |<span data-ttu-id="6dbb4-1847">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1847">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-1848">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1848">Example</span></span>
```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

<span data-ttu-id="6dbb4-1849">如需詳細資訊，請參閱 [Amazon S3 連接器文件](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1849">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="6dbb4-1850">Dataset</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1850">Dataset</span></span>
<span data-ttu-id="6dbb4-1851">若要定義 Amazon S3 資料集，請將資料集的 **type** 設為 **AmazonS3**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1851">To define an Amazon S3 dataset, set the **type** of the dataset to **AmazonS3**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="6dbb4-1852">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1852">Property</span></span> | <span data-ttu-id="6dbb4-1853">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1853">Description</span></span> | <span data-ttu-id="6dbb4-1854">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1854">Allowed values</span></span> | <span data-ttu-id="6dbb4-1855">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1855">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-1856">bucketName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1856">bucketName</span></span> |<span data-ttu-id="6dbb4-1857">S3 貯體名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1857">The S3 bucket name.</span></span> |<span data-ttu-id="6dbb4-1858">string</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1858">String</span></span> |<span data-ttu-id="6dbb4-1859">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1859">Yes</span></span> |
| <span data-ttu-id="6dbb4-1860">key</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1860">key</span></span> |<span data-ttu-id="6dbb4-1861">S3 物件索引鍵。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1861">The S3 object key.</span></span> |<span data-ttu-id="6dbb4-1862">string</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1862">String</span></span> |<span data-ttu-id="6dbb4-1863">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1863">No</span></span> |
| <span data-ttu-id="6dbb4-1864">prefix</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1864">prefix</span></span> |<span data-ttu-id="6dbb4-1865">S3 物件索引鍵的前置詞。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1865">Prefix for the S3 object key.</span></span> <span data-ttu-id="6dbb4-1866">系統會選取索引鍵以此前置詞開頭的物件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1866">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="6dbb4-1867">只有當索引鍵空白時才適用。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1867">Applies only when key is empty.</span></span> |<span data-ttu-id="6dbb4-1868">string</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1868">String</span></span> |<span data-ttu-id="6dbb4-1869">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1869">No</span></span> |
| <span data-ttu-id="6dbb4-1870">version</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1870">version</span></span> |<span data-ttu-id="6dbb4-1871">如果已啟用 S3 版本設定功能，則為 S3 物件的版本。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1871">The version of S3 object if S3 versioning is enabled.</span></span> |<span data-ttu-id="6dbb4-1872">string</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1872">String</span></span> |<span data-ttu-id="6dbb4-1873">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1873">No</span></span> |
| <span data-ttu-id="6dbb4-1874">format</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1874">format</span></span> | <span data-ttu-id="6dbb4-1875">支援下列格式類型：**TextFormat**、**JsonFormat**、**AvroFormat**、**OrcFormat**、**ParquetFormat**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1875">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="6dbb4-1876">將格式下的 **type** 屬性設定為這些值其中之一。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1876">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="6dbb4-1877">如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1877">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="6dbb4-1878">如果您想要在以檔案為基礎的存放區之間**依原樣複製檔案** (二進位複本)，請在輸入和輸出資料集定義中略過格式區段。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1878">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="6dbb4-1879">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1879">No</span></span> | |
| <span data-ttu-id="6dbb4-1880">compression</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1880">compression</span></span> | <span data-ttu-id="6dbb4-1881">指定此資料的壓縮類型和層級。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1881">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="6dbb4-1882">支援的類型為：**GZip**、**Deflate**、**BZip2** 及 **ZipDeflate**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1882">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="6dbb4-1883">支援的層級為：**Optimal** 和 **Fastest**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1883">The supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="6dbb4-1884">如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1884">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="6dbb4-1885">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1885">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="6dbb4-1886">bucketName + key 可指定 S3 物件的位置，其中貯體是 S3 物件的根容器，而索引鍵是 S3 物件的完整路徑。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1886">bucketName + key specifies the location of the S3 object where bucket is the root container for S3 objects and key is the full path to S3 object.</span></span>

#### <a name="example-sample-dataset-with-prefix"></a><span data-ttu-id="6dbb4-1887">範例：範例資料集 (含 prefix)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1887">Example: Sample dataset with prefix</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "<S3 bucket name>",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
#### <a name="example-sample-data-set-with-version"></a><span data-ttu-id="6dbb4-1888">範例︰範例資料集 (含 version)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1888">Example: Sample data set (with version)</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "<S3 bucket name>",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

#### <a name="example-dynamic-paths-for-s3"></a><span data-ttu-id="6dbb4-1889">範例：S3 的動態路徑</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1889">Example: Dynamic paths for S3</span></span>
<span data-ttu-id="6dbb4-1890">在此範例中，我們針對 Amazon S3 資料集內的 key 和 bucketName 屬性使用固定的值。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1890">In the sample, we use fixed values for key and bucketName properties in the Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "<S3 bucket name>",
```

<span data-ttu-id="6dbb4-1891">您可以藉由使用系統變數 (例如 SliceStart)，讓 Data Factory 在執行階段動態地計算 key 和 bucketName 的值。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1891">You can have Data Factory calculate the key and bucketName dynamically at runtime by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="6dbb4-1892">您也可以對 Amazon S3 資料集的 prefix 屬性執行相同的操作。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1892">You can do the same for the prefix property of an Amazon S3 dataset.</span></span> <span data-ttu-id="6dbb4-1893">如需支援的函式和變數清單，請參閱 [Data Factory 函式與系統變數](data-factory-functions-variables.md) 。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1893">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of supported functions and variables.</span></span>

<span data-ttu-id="6dbb4-1894">如需詳細資訊，請參閱 [Amazon S3 連接器文件](data-factory-amazon-simple-storage-service-connector.md#dataset-properties)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1894">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="6dbb4-1895">複製活動中的檔案系統來源</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1895">File System Source in Copy Activity</span></span>
<span data-ttu-id="6dbb4-1896">如果您從 Amazon S3 複製資料，請將複製活動的 **source type** 設為 **FileSystemSource**，並在 **source** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1896">If you are copying data from Amazon S3, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="6dbb4-1897">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1897">Property</span></span> | <span data-ttu-id="6dbb4-1898">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1898">Description</span></span> | <span data-ttu-id="6dbb4-1899">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1899">Allowed values</span></span> | <span data-ttu-id="6dbb4-1900">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1900">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-1901">遞迴</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1901">recursive</span></span> |<span data-ttu-id="6dbb4-1902">指定是否要以遞迴方式列出目錄下的 S3 物件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1902">Specifies whether to recursively list S3 objects under the directory.</span></span> |<span data-ttu-id="6dbb4-1903">true/false</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1903">true/false</span></span> |<span data-ttu-id="6dbb4-1904">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1904">No</span></span> |


#### <a name="example"></a><span data-ttu-id="6dbb4-1905">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1905">Example</span></span>


```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource",
                    "recursive": true
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonS3InputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonS3ToBlob"
        }],
        "start": "2016-08-08T18:00:00",
        "end": "2016-08-08T19:00:00"
    }
}
```

<span data-ttu-id="6dbb4-1906">如需詳細資訊，請參閱 [Amazon S3 連接器文件](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1906">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span></span>

## <a name="file-system"></a><span data-ttu-id="6dbb4-1907">檔案系統</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1907">File System</span></span>


### <a name="linked-service"></a><span data-ttu-id="6dbb4-1908">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1908">Linked service</span></span>
<span data-ttu-id="6dbb4-1909">您可以利用「內部部署檔案伺服器」已連結服務，將內部部署的檔案系統連結到 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1909">You can link an on-premises file system to an Azure data factory with the **On-Premises File Server** linked service.</span></span> <span data-ttu-id="6dbb4-1910">下表說明內部部署檔案伺服器連結服務專屬的 JSON 元素。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1910">The following table provides descriptions for JSON elements that are specific to the On-Premises File Server linked service.</span></span>

| <span data-ttu-id="6dbb4-1911">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1911">Property</span></span> | <span data-ttu-id="6dbb4-1912">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1912">Description</span></span> | <span data-ttu-id="6dbb4-1913">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1913">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-1914">類型</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1914">type</span></span> |<span data-ttu-id="6dbb4-1915">確保 type 屬性設為 **OnPremisesFileServer**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1915">Ensure that the type property is set to **OnPremisesFileServer**.</span></span> |<span data-ttu-id="6dbb4-1916">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1916">Yes</span></span> |
| <span data-ttu-id="6dbb4-1917">主機</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1917">host</span></span> |<span data-ttu-id="6dbb4-1918">指定想要複製之資料夾的根路徑。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1918">Specifies the root path of the folder that you want to copy.</span></span> <span data-ttu-id="6dbb4-1919">字串中的特殊字元需使用逸出字元 ‘ \ ’。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1919">Use the escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="6dbb4-1920">如需範例，請參閱 [範例連結服務和資料集定義](#sample-linked-service-and-dataset-definitions) 。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1920">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="6dbb4-1921">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1921">Yes</span></span> |
| <span data-ttu-id="6dbb4-1922">userid</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1922">userid</span></span> |<span data-ttu-id="6dbb4-1923">指定具有伺服器存取權之使用者的識別碼。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1923">Specify the ID of the user who has access to the server.</span></span> |<span data-ttu-id="6dbb4-1924">否 (如果您選擇 encryptedCredential)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1924">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="6dbb4-1925">password</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1925">password</span></span> |<span data-ttu-id="6dbb4-1926">指定使用者 (userid) 的密碼。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1926">Specify the password for the user (userid).</span></span> |<span data-ttu-id="6dbb4-1927">否 (如果您選擇 encryptedCredential)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1927">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="6dbb4-1928">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1928">encryptedCredential</span></span> |<span data-ttu-id="6dbb4-1929">指定可以透過執行 New-AzureRmDataFactoryEncryptValue Cmdlet 來取得的加密認證。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1929">Specify the encrypted credentials that you can get by running the New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="6dbb4-1930">否 (如果您選擇以純文字指定使用者識別碼和密碼)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1930">No (if you choose to specify userid and password in plain text)</span></span> |
| <span data-ttu-id="6dbb4-1931">gatewayName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1931">gatewayName</span></span> |<span data-ttu-id="6dbb4-1932">指定 Data Factory 應該用來連接到內部部署檔案伺服器的閘道器名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1932">Specifies the name of the gateway that Data Factory should use to connect to the on-premises file server.</span></span> |<span data-ttu-id="6dbb4-1933">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1933">Yes</span></span> |

#### <a name="sample-folder-path-definitions"></a><span data-ttu-id="6dbb4-1934">範例資料夾路徑定義</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1934">Sample folder path definitions</span></span> 
| <span data-ttu-id="6dbb4-1935">案例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1935">Scenario</span></span> | <span data-ttu-id="6dbb4-1936">連結服務定義中的主機</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1936">Host in linked service definition</span></span> | <span data-ttu-id="6dbb4-1937">資料集定義中的 folderPath</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1937">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-1938">資料管理閘道電腦上的本機資料夾︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1938">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="6dbb4-1939">範例：D:\\\* 或 D:\folder\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1939">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="6dbb4-1940">D:\\\\ (適用於資料管理閘道 2.0 和更新版本)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1940">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="6dbb4-1941">localhost (適用於比資料管理閘道 2.0 更早的版本)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1941">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="6dbb4-1942">.\\\\ 或 folder\\\\subfolder (適用於資料管理閘道 2.0 和更新版本)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1942">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="6dbb4-1943">D:\\\\ 或 D:\\\\folder\\\\subfolder (適用低於閘道 2.0 的版本)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1943">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="6dbb4-1944">遠端共用資料夾︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1944">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="6dbb4-1945">範例︰\\\\myserver\\share\\\* 或 \\\\myserver\\share\\folder\\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1945">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="6dbb4-1946">\\\\\\\\myserver\\\\share</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1946">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="6dbb4-1947">.\\\\ 或 folder\\\\subfolder</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1947">.\\\\ or folder\\\\subfolder</span></span> |


#### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="6dbb4-1948">範例：使用純文字的使用者名稱和密碼</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1948">Example: Using username and password in plain text</span></span>

```json
{
    "Name": "OnPremisesFileServerLinkedService",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "\\\\Contosogame-Asia",
            "userid": "Admin",
            "password": "123456",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-encryptedcredential"></a><span data-ttu-id="6dbb4-1949">範例：使用 encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1949">Example: Using encryptedcredential</span></span>

```json
{
    "Name": " OnPremisesFileServerLinkedService ",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "D:\\",
            "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="6dbb4-1950">如需詳細資訊，請參閱[檔案系統連接器文件](data-factory-onprem-file-system-connector.md#linked-service-properties)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1950">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="6dbb4-1951">Dataset</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1951">Dataset</span></span>
<span data-ttu-id="6dbb4-1952">若要定義檔案系統資料集，請將資料集的 **type** 設為 **FileShare**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1952">To define a File System dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="6dbb4-1953">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1953">Property</span></span> | <span data-ttu-id="6dbb4-1954">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1954">Description</span></span> | <span data-ttu-id="6dbb4-1955">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1955">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-1956">folderPath</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1956">folderPath</span></span> |<span data-ttu-id="6dbb4-1957">指定資料夾的子路徑。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1957">Specifies the subpath to the folder.</span></span> <span data-ttu-id="6dbb4-1958">字串中的特殊字元需使用逸出字元 ‘ \ ’。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1958">Use the escape character ‘\’ for special characters in the string.</span></span> <span data-ttu-id="6dbb4-1959">如需範例，請參閱 [範例連結服務和資料集定義](#sample-linked-service-and-dataset-definitions) 。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1959">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="6dbb4-1960">您可以結合此屬性與 **partitionBy**，讓資料夾路徑以配量開始/結束日期時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1960">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="6dbb4-1961">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1961">Yes</span></span> |
| <span data-ttu-id="6dbb4-1962">fileName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1962">fileName</span></span> |<span data-ttu-id="6dbb4-1963">如果您想要資料表參考資料夾中的特定檔案，請指定 **folderPath** 中的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1963">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="6dbb4-1964">如果沒有為此屬性指定任何值，資料表會指向資料夾中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1964">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="6dbb4-1965">若未指定輸出資料集的 fileName，所產生檔案的名稱是下列格式︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1965">When fileName is not specified for an output dataset, the name of the generated file is in the following format:</span></span> <br/><br/><span data-ttu-id="6dbb4-1966">`Data.<Guid>.txt` (例如： Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1966">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="6dbb4-1967">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1967">No</span></span> |
| <span data-ttu-id="6dbb4-1968">fileFilter</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1968">fileFilter</span></span> |<span data-ttu-id="6dbb4-1969">指定要用來在 folderPath (而不是所有檔案) 中選取檔案子集的篩選器。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1969">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="6dbb4-1970">允許的值為︰`*` (多個字元) 和 `?` (單一字元)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1970">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="6dbb4-1971">範例 1："fileFilter": "*.log"</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1971">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="6dbb4-1972">範例 2："fileFilter": 2016-1-?.txt"</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1972">Example 2: "fileFilter": 2016-1-?.txt"</span></span><br/><br/><span data-ttu-id="6dbb4-1973">請注意，fileFilter 適用於輸入 FileShare 資料集。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1973">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="6dbb4-1974">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1974">No</span></span> |
| <span data-ttu-id="6dbb4-1975">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1975">partitionedBy</span></span> |<span data-ttu-id="6dbb4-1976">您可以使用 partitionedBy 來指定時間序列資料的動態 folderPath/fileName。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1976">You can use partitionedBy to specify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="6dbb4-1977">例如，folderPath 可針對每小時的資料進行參數化。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1977">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="6dbb4-1978">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1978">No</span></span> |
| <span data-ttu-id="6dbb4-1979">format</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1979">format</span></span> | <span data-ttu-id="6dbb4-1980">支援下列格式類型：**TextFormat**、**JsonFormat**、**AvroFormat**、**OrcFormat**、**ParquetFormat**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1980">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="6dbb4-1981">將格式下的 **type** 屬性設定為這些值其中之一。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1981">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="6dbb4-1982">如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1982">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="6dbb4-1983">如果您想要在以檔案為基礎的存放區之間**依原樣複製檔案** (二進位複本)，請在輸入和輸出資料集定義中略過格式區段。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1983">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="6dbb4-1984">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1984">No</span></span> |
| <span data-ttu-id="6dbb4-1985">compression</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1985">compression</span></span> | <span data-ttu-id="6dbb4-1986">指定此資料的壓縮類型和層級。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1986">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="6dbb4-1987">支援的類型為：**GZip**、**Deflate**、**BZip2** 和 **ZipDeflate**，而支援的層級為：**最佳**和**最快**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1987">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="6dbb4-1988">請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1988">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="6dbb4-1989">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1989">No</span></span> |

> [!NOTE]
> <span data-ttu-id="6dbb4-1990">無法同時使用 fileName 和 fileFilter。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1990">You cannot use fileName and fileFilter simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="6dbb4-1991">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1991">Example</span></span>

```json
{
    "name": "OnpremisesFileSystemInput",
    "properties": {
        "type": " FileShare",
        "linkedServiceName": " OnPremisesFileServerLinkedService ",
        "typeProperties": {
            "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
            "fileName": "{Hour}.csv",
            "partitionedBy": [{
                "name": "Year",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                        "format": "yyyy"
                }
            }, {
                "name": "Month",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "MM"
                }
            }, {
                "name": "Day",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "dd"
                }
            }, {
                "name": "Hour",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "HH"
                }
            }]
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="6dbb4-1992">如需詳細資訊，請參閱[檔案系統連接器文件](data-factory-onprem-file-system-connector.md#dataset-properties)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1992">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="6dbb4-1993">複製活動中的檔案系統來源</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1993">File System Source in Copy Activity</span></span>
<span data-ttu-id="6dbb4-1994">如果您從檔案系統複製資料，請將複製活動的 **source type** 設為 **FileSystemSource**，並在 **source** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1994">If you are copying data from File System, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="6dbb4-1995">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1995">Property</span></span> | <span data-ttu-id="6dbb4-1996">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1996">Description</span></span> | <span data-ttu-id="6dbb4-1997">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1997">Allowed values</span></span> | <span data-ttu-id="6dbb4-1998">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1998">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-1999">遞迴</span><span class="sxs-lookup"><span data-stu-id="6dbb4-1999">recursive</span></span> |<span data-ttu-id="6dbb4-2000">指出是否從子資料夾、或只有從指定的資料夾，以遞迴方式讀取資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2000">Indicates whether the data is read recursively from the subfolders or only from the specified folder.</span></span> |<span data-ttu-id="6dbb4-2001">True/False (預設值為 False)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2001">True, False (default)</span></span> |<span data-ttu-id="6dbb4-2002">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2002">No</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-2003">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2003">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T19:00:00",
        "description": "Pipeline for copy activity",
        "activities": [{
            "name": "OnpremisesFileSystemtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "OnpremisesFileSystemInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
            "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="6dbb4-2004">如需詳細資訊，請參閱[檔案系統連接器文件](data-factory-onprem-file-system-connector.md#copy-activity-properties)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2004">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

### <a name="file-system-sink-in-copy-activity"></a><span data-ttu-id="6dbb4-2005">複製活動中的檔案系統接收</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2005">File System Sink in Copy Activity</span></span>
<span data-ttu-id="6dbb4-2006">如果您將資料複製到檔案系統，請將複製活動的 **sink type** 設為 **FileSystemSink**，並在 **sink** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2006">If you are copying data to File System, set the **sink type** of the copy activity to **FileSystemSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="6dbb4-2007">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2007">Property</span></span> | <span data-ttu-id="6dbb4-2008">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2008">Description</span></span> | <span data-ttu-id="6dbb4-2009">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2009">Allowed values</span></span> | <span data-ttu-id="6dbb4-2010">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2010">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-2011">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2011">copyBehavior</span></span> |<span data-ttu-id="6dbb4-2012">當來源為 BlobSource 或 FileSystem 時，定義複製行為。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2012">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="6dbb4-2013">**PreserveHierarchy：**保留目標資料夾中的檔案階層。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2013">**PreserveHierarchy:** Preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="6dbb4-2014">亦即，來源檔案到來源資料夾的相對路徑，與目標檔案到目標資料夾的相對路徑相同。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2014">That is, the relative path of the source file to the source folder is the same as the relative path of the target file to the target folder.</span></span><br/><br/><span data-ttu-id="6dbb4-2015">**FlattenHierarchy：**來源資料夾的中所有檔案都會建立在目標資料夾的第一層中。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2015">**FlattenHierarchy:** All files from the source folder are created in the first level of target folder.</span></span> <span data-ttu-id="6dbb4-2016">建立的目標檔案會具有自動產生的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2016">The target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="6dbb4-2017">**MergeFiles：**將來源資料夾的所有檔案合併為一個檔案。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2017">**MergeFiles:** Merges all files from the source folder to one file.</span></span> <span data-ttu-id="6dbb4-2018">如果有指定檔案/Blob 名稱，合併檔案的名稱會是指定的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2018">If the file name/blob name is specified, the merged file name is the specified name.</span></span> <span data-ttu-id="6dbb4-2019">否則，就會是自動產生的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2019">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="6dbb4-2020">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2020">No</span></span> |
<span data-ttu-id="6dbb4-2021">auto-</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2021">auto-</span></span>

#### <a name="example"></a><span data-ttu-id="6dbb4-2022">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2022">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T20:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoOnPremisesFile",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "OnpremisesFileSystemOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "FileSystemSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 3,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="6dbb4-2023">如需詳細資訊，請參閱[檔案系統連接器文件](data-factory-onprem-file-system-connector.md#copy-activity-properties)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2023">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

## <a name="ftp"></a><span data-ttu-id="6dbb4-2024">FTP</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2024">FTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="6dbb4-2025">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2025">Linked service</span></span>
<span data-ttu-id="6dbb4-2026">若要定義 FTP 連結服務，請將連結服務的 **type** 設為 **FtpServer**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2026">To define an FTP linked service, set the **type** of the linked service to **FtpServer**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="6dbb4-2027">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2027">Property</span></span> | <span data-ttu-id="6dbb4-2028">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2028">Description</span></span> | <span data-ttu-id="6dbb4-2029">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2029">Required</span></span> | <span data-ttu-id="6dbb4-2030">預設值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2030">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-2031">主機</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2031">host</span></span> |<span data-ttu-id="6dbb4-2032">FTP 伺服器的名稱或 IP 位址</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2032">Name or IP address of the FTP Server</span></span> |<span data-ttu-id="6dbb4-2033">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2033">Yes</span></span> |&nbsp; |
| <span data-ttu-id="6dbb4-2034">authenticationType</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2034">authenticationType</span></span> |<span data-ttu-id="6dbb4-2035">指定驗證類型</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2035">Specify authentication type</span></span> |<span data-ttu-id="6dbb4-2036">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2036">Yes</span></span> |<span data-ttu-id="6dbb4-2037">基本或匿名</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2037">Basic, Anonymous</span></span> |
| <span data-ttu-id="6dbb4-2038">username</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2038">username</span></span> |<span data-ttu-id="6dbb4-2039">可存取 FTP 伺服器的使用者</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2039">User who has access to the FTP server</span></span> |<span data-ttu-id="6dbb4-2040">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2040">No</span></span> |&nbsp; |
| <span data-ttu-id="6dbb4-2041">password</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2041">password</span></span> |<span data-ttu-id="6dbb4-2042">使用者 (使用者名稱) 的密碼</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2042">Password for the user (username)</span></span> |<span data-ttu-id="6dbb4-2043">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2043">No</span></span> |&nbsp; |
| <span data-ttu-id="6dbb4-2044">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2044">encryptedCredential</span></span> |<span data-ttu-id="6dbb4-2045">用來存取 FTP 伺服器的加密認證</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2045">Encrypted credential to access the FTP server</span></span> |<span data-ttu-id="6dbb4-2046">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2046">No</span></span> |&nbsp; |
| <span data-ttu-id="6dbb4-2047">gatewayName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2047">gatewayName</span></span> |<span data-ttu-id="6dbb4-2048">連接至內部部署 FTP 伺服器的「資料管理閘道」閘道</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2048">Name of the Data Management Gateway gateway to connect to an on-premises FTP server</span></span> |<span data-ttu-id="6dbb4-2049">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2049">No</span></span> |&nbsp; |
| <span data-ttu-id="6dbb4-2050">連接埠</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2050">port</span></span> |<span data-ttu-id="6dbb4-2051">FTP 伺服器所接聽的連接埠</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2051">Port on which the FTP server is listening</span></span> |<span data-ttu-id="6dbb4-2052">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2052">No</span></span> |<span data-ttu-id="6dbb4-2053">21</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2053">21</span></span> |
| <span data-ttu-id="6dbb4-2054">enableSsl</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2054">enableSsl</span></span> |<span data-ttu-id="6dbb4-2055">指定是否使用透過 SSL/TLS 的 FTP 通道</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2055">Specify whether to use FTP over SSL/TLS channel</span></span> |<span data-ttu-id="6dbb4-2056">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2056">No</span></span> |<span data-ttu-id="6dbb4-2057">true</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2057">true</span></span> |
| <span data-ttu-id="6dbb4-2058">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2058">enableServerCertificateValidation</span></span> |<span data-ttu-id="6dbb4-2059">指定是否在使用透過 SSL/TLS 的 FTP 通道時啟用伺服器 SSL 憑證驗證</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2059">Specify whether to enable server SSL certificate validation when using FTP over SSL/TLS channel</span></span> |<span data-ttu-id="6dbb4-2060">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2060">No</span></span> |<span data-ttu-id="6dbb4-2061">true</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2061">true</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="6dbb4-2062">範例：使用匿名驗證</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2062">Example: Using Anonymous authentication</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
            "typeProperties": {
            "authenticationType": "Anonymous",
            "host": "myftpserver.com"
        }
    }
}
```

#### <a name="example-using-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="6dbb4-2063">範例：使用純文字的使用者名稱和密碼進行基本驗證</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2063">Example: Using username and password in plain text for basic authentication</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
    }
}
```

#### <a name="example-using-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="6dbb4-2064">範例：使用 port、enableSsl、enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2064">Example: Using port, enableSsl, enableServerCertificateValidation</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

#### <a name="example-using-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="6dbb4-2065">範例：針對驗證和閘道使用 encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2065">Example: Using encryptedCredential for authentication and gateway</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
      }
}
```

<span data-ttu-id="6dbb4-2066">如需詳細資訊，請參閱 [FTP 連接器](data-factory-ftp-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2066">For more information, see [FTP connector](data-factory-ftp-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="6dbb4-2067">Dataset</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2067">Dataset</span></span>
<span data-ttu-id="6dbb4-2068">若要定義 FTP 資料集，請將資料集的 **type** 設為 **FileShare**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2068">To define an FTP dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="6dbb4-2069">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2069">Property</span></span> | <span data-ttu-id="6dbb4-2070">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2070">Description</span></span> | <span data-ttu-id="6dbb4-2071">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2071">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-2072">folderPath</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2072">folderPath</span></span> |<span data-ttu-id="6dbb4-2073">資料夾的子路徑。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2073">Sub path to the folder.</span></span> <span data-ttu-id="6dbb4-2074">使用逸出字元 ‘ \ ’ 當做字串中的特殊字元。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2074">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="6dbb4-2075">如需範例，請參閱 [範例連結服務和資料集定義](#sample-linked-service-and-dataset-definitions) 。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2075">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="6dbb4-2076">您可以結合此屬性與 **partitionBy**，讓資料夾路徑以配量開始/結束日期時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2076">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="6dbb4-2077">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2077">Yes</span></span> 
| <span data-ttu-id="6dbb4-2078">fileName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2078">fileName</span></span> |<span data-ttu-id="6dbb4-2079">如果您想要資料表參考資料夾中的特定檔案，請指定 **folderPath** 中的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2079">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="6dbb4-2080">如果沒有為此屬性指定任何值，資料表會指向資料夾中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2080">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="6dbb4-2081">若未指定輸出資料集的 fileName，所產生檔案的名稱是下列格式︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2081">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="6dbb4-2082">Data.<Guid>.txt (範例：Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2082">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="6dbb4-2083">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2083">No</span></span> |
| <span data-ttu-id="6dbb4-2084">fileFilter</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2084">fileFilter</span></span> |<span data-ttu-id="6dbb4-2085">指定要用來在 folderPath (而不是所有檔案) 中選取檔案子集的篩選器。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2085">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="6dbb4-2086">允許的值為︰`*` (多個字元) 和 `?` (單一字元)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2086">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="6dbb4-2087">範例 1：`"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2087">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="6dbb4-2088">範例 2：`"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2088">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="6dbb4-2089">fileFilter 適用於輸入 FileShare 資料集。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2089">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="6dbb4-2090">這個屬性不支援使用 HDFS。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2090">This property is not supported with HDFS.</span></span> |<span data-ttu-id="6dbb4-2091">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2091">No</span></span> |
| <span data-ttu-id="6dbb4-2092">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2092">partitionedBy</span></span> |<span data-ttu-id="6dbb4-2093">partitionedBy 可以用來指定時間序列資料的動態 folderPath 和 filename。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2093">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="6dbb4-2094">例如，folderPath 可針對每小時的資料進行參數化。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2094">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="6dbb4-2095">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2095">No</span></span> |
| <span data-ttu-id="6dbb4-2096">format</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2096">format</span></span> | <span data-ttu-id="6dbb4-2097">支援下列格式類型：**TextFormat**、**JsonFormat**、**AvroFormat**、**OrcFormat**、**ParquetFormat**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2097">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="6dbb4-2098">將格式下的 **type** 屬性設定為這些值其中之一。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2098">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="6dbb4-2099">如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2099">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="6dbb4-2100">如果您想要在以檔案為基礎的存放區之間**依原樣複製檔案** (二進位複本)，請在輸入和輸出資料集定義中略過格式區段。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2100">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="6dbb4-2101">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2101">No</span></span> |
| <span data-ttu-id="6dbb4-2102">compression</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2102">compression</span></span> | <span data-ttu-id="6dbb4-2103">指定此資料的壓縮類型和層級。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2103">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="6dbb4-2104">支援的類型為：**GZip**、**Deflate**、**BZip2** 和 **ZipDeflate**，而支援的層級為：**最佳**和**最快**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2104">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="6dbb4-2105">如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2105">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="6dbb4-2106">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2106">No</span></span> |
| <span data-ttu-id="6dbb4-2107">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2107">useBinaryTransfer</span></span> |<span data-ttu-id="6dbb4-2108">指定是否使用二進位傳輸模式。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2108">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="6dbb4-2109">二進位模式為 true，ASCII 則為 false。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2109">True for binary mode and false ASCII.</span></span> <span data-ttu-id="6dbb4-2110">預設值：True。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2110">Default value: True.</span></span> <span data-ttu-id="6dbb4-2111">只有在相關聯的連結服務類型的類型為 FtpServer 時，才可以使用這個屬性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2111">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="6dbb4-2112">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2112">No</span></span> |

> [!NOTE]
> <span data-ttu-id="6dbb4-2113">無法同時使用檔名和 fileFilter。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2113">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="6dbb4-2114">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2114">Example</span></span>

```json
{
    "name": "FTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "FTPLinkedService",
        "typeProperties": {
            "folderPath": "<path to shared folder>",
            "fileName": "test.csv",
            "useBinaryTransfer": true
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="6dbb4-2115">如需詳細資訊，請參閱 [FTP 連接器](data-factory-ftp-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2115">For more information, see [FTP connector](data-factory-ftp-connector.md#dataset-properties) article.</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="6dbb4-2116">複製活動中的檔案系統來源</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2116">File System Source in Copy Activity</span></span>
<span data-ttu-id="6dbb4-2117">如果您從 FTP 伺服器複製資料，請將複製活動的 **source type** 設為 **FileSystemSource**，並在 **source** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2117">If you are copying data from an FTP server, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="6dbb4-2118">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2118">Property</span></span> | <span data-ttu-id="6dbb4-2119">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2119">Description</span></span> | <span data-ttu-id="6dbb4-2120">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2120">Allowed values</span></span> | <span data-ttu-id="6dbb4-2121">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2121">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-2122">遞迴</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2122">recursive</span></span> |<span data-ttu-id="6dbb4-2123">表示是否從子資料夾，或只有從指定的資料夾，以遞迴方式讀取資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2123">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="6dbb4-2124">True/False (預設值為 False)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2124">True, False (default)</span></span> |<span data-ttu-id="6dbb4-2125">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2125">No</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-2126">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2126">Example</span></span>

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00",
        "end": "2016-08-24T19:00:00"
    }
}
```

<span data-ttu-id="6dbb4-2127">如需詳細資訊，請參閱 [FTP 連接器](data-factory-ftp-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2127">For more information, see [FTP connector](data-factory-ftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="hdfs"></a><span data-ttu-id="6dbb4-2128">HDFS</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2128">HDFS</span></span>

### <a name="linked-service"></a><span data-ttu-id="6dbb4-2129">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2129">Linked service</span></span>
<span data-ttu-id="6dbb4-2130">若要定義 HDFS 連結服務，請將連結服務的 **type** 設為 **Hdfs**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2130">To define a HDFS linked service, set the **type** of the linked service to **Hdfs**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="6dbb4-2131">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2131">Property</span></span> | <span data-ttu-id="6dbb4-2132">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2132">Description</span></span> | <span data-ttu-id="6dbb4-2133">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2133">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-2134">類型</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2134">type</span></span> |<span data-ttu-id="6dbb4-2135">類型屬性必須設為： **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2135">The type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="6dbb4-2136">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2136">Yes</span></span> |
| <span data-ttu-id="6dbb4-2137">Url</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2137">Url</span></span> |<span data-ttu-id="6dbb4-2138">到 HDFS 的 URL</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2138">URL to the HDFS</span></span> |<span data-ttu-id="6dbb4-2139">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2139">Yes</span></span> |
| <span data-ttu-id="6dbb4-2140">authenticationType</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2140">authenticationType</span></span> |<span data-ttu-id="6dbb4-2141">匿名或 Windows。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2141">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="6dbb4-2142">若要對 HDFS 連接器使用 **Kerberos 驗證**，請參閱[此章節](#use-kerberos-authentication-for-hdfs-connector)來據以設定您的內部部署環境。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2142">To use **Kerberos authentication** for HDFS connector, refer to [this section](#use-kerberos-authentication-for-hdfs-connector) to set up your on-premises environment accordingly.</span></span> |<span data-ttu-id="6dbb4-2143">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2143">Yes</span></span> |
| <span data-ttu-id="6dbb4-2144">userName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2144">userName</span></span> |<span data-ttu-id="6dbb4-2145">Windows 驗證的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2145">Username for Windows authentication.</span></span> |<span data-ttu-id="6dbb4-2146">是 (適用於 Windows 驗證)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2146">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="6dbb4-2147">password</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2147">password</span></span> |<span data-ttu-id="6dbb4-2148">Windows 驗證的密碼。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2148">Password for Windows authentication.</span></span> |<span data-ttu-id="6dbb4-2149">是 (適用於 Windows 驗證)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2149">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="6dbb4-2150">gatewayName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2150">gatewayName</span></span> |<span data-ttu-id="6dbb4-2151">Data Factory 服務應該用來連接到 HDFS 的閘道器名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2151">Name of the gateway that the Data Factory service should use to connect to the HDFS.</span></span> |<span data-ttu-id="6dbb4-2152">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2152">Yes</span></span> |
| <span data-ttu-id="6dbb4-2153">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2153">encryptedCredential</span></span> |<span data-ttu-id="6dbb4-2154">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) 輸出。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2154">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output of the access credential.</span></span> |<span data-ttu-id="6dbb4-2155">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2155">No</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="6dbb4-2156">範例：使用匿名驗證</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2156">Example: Using Anonymous authentication</span></span>

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-windows-authentication"></a><span data-ttu-id="6dbb4-2157">範例：使用 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2157">Example: Using Windows authentication</span></span>

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="6dbb4-2158">如需詳細資訊，請參閱 [HDFS 連接器](#data-factory-hdfs-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2158">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="6dbb4-2159">Dataset</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2159">Dataset</span></span>
<span data-ttu-id="6dbb4-2160">若要定義 HDFS 資料集，請將資料集的 **type** 設為 **FileShare**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2160">To define a HDFS dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="6dbb4-2161">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2161">Property</span></span> | <span data-ttu-id="6dbb4-2162">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2162">Description</span></span> | <span data-ttu-id="6dbb4-2163">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2163">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-2164">folderPath</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2164">folderPath</span></span> |<span data-ttu-id="6dbb4-2165">資料夾的路徑。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2165">Path to the folder.</span></span> <span data-ttu-id="6dbb4-2166">範例：`myfolder`</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2166">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="6dbb4-2167">使用逸出字元 ‘ \ ’ 當做字串中的特殊字元。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2167">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="6dbb4-2168">例如︰若為 folder\subfolder，請指定 folder\\\\subfolder；若為 d:\samplefolder，請指定 d:\\\\samplefolder。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2168">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="6dbb4-2169">您可以結合此屬性與 **partitionBy**，讓資料夾路徑以配量開始/結束日期時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2169">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="6dbb4-2170">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2170">Yes</span></span> |
| <span data-ttu-id="6dbb4-2171">fileName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2171">fileName</span></span> |<span data-ttu-id="6dbb4-2172">如果您想要資料表參考資料夾中的特定檔案，請指定 **folderPath** 中的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2172">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="6dbb4-2173">如果沒有為此屬性指定任何值，資料表會指向資料夾中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2173">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="6dbb4-2174">若未指定輸出資料集的 fileName，所產生檔案的名稱是下列格式︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2174">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="6dbb4-2175">Data<Guid>.txt (例如：Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2175">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="6dbb4-2176">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2176">No</span></span> |
| <span data-ttu-id="6dbb4-2177">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2177">partitionedBy</span></span> |<span data-ttu-id="6dbb4-2178">partitionedBy 可以用來指定時間序列資料的動態 folderPath 和 filename。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2178">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="6dbb4-2179">範例：folderPath 可針對每小時的資料進行參數化。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2179">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="6dbb4-2180">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2180">No</span></span> |
| <span data-ttu-id="6dbb4-2181">format</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2181">format</span></span> | <span data-ttu-id="6dbb4-2182">支援下列格式類型：**TextFormat**、**JsonFormat**、**AvroFormat**、**OrcFormat**、**ParquetFormat**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2182">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="6dbb4-2183">將格式下的 **type** 屬性設定為這些值其中之一。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2183">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="6dbb4-2184">如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2184">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="6dbb4-2185">如果您想要在以檔案為基礎的存放區之間**依原樣複製檔案** (二進位複本)，請在輸入和輸出資料集定義中略過格式區段。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2185">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="6dbb4-2186">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2186">No</span></span> |
| <span data-ttu-id="6dbb4-2187">compression</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2187">compression</span></span> | <span data-ttu-id="6dbb4-2188">指定此資料的壓縮類型和層級。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2188">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="6dbb4-2189">支援的類型為：**GZip**、**Deflate**、**BZip2** 及 **ZipDeflate**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2189">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="6dbb4-2190">支援的層級為：**Optimal** 和 **Fastest**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2190">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="6dbb4-2191">如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2191">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="6dbb4-2192">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2192">No</span></span> |

> [!NOTE]
> <span data-ttu-id="6dbb4-2193">無法同時使用檔名和 fileFilter。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2193">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="6dbb4-2194">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2194">Example</span></span>

```json
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="6dbb4-2195">如需詳細資訊，請參閱 [HDFS 連接器](#data-factory-hdfs-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2195">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="6dbb4-2196">複製活動中的檔案系統來源</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2196">File System Source in Copy Activity</span></span>
<span data-ttu-id="6dbb4-2197">如果您從 HDFS 複製資料，請將複製活動的 **source type** 設為 **FileSystemSource**，並在 **source** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2197">If you are copying data from HDFS, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

<span data-ttu-id="6dbb4-2198">**FileSystemSource** 支援下列屬性：</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2198">**FileSystemSource** supports the following properties:</span></span>

| <span data-ttu-id="6dbb4-2199">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2199">Property</span></span> | <span data-ttu-id="6dbb4-2200">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2200">Description</span></span> | <span data-ttu-id="6dbb4-2201">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2201">Allowed values</span></span> | <span data-ttu-id="6dbb4-2202">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2202">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-2203">遞迴</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2203">recursive</span></span> |<span data-ttu-id="6dbb4-2204">表示是否從子資料夾，或只有從指定的資料夾，以遞迴方式讀取資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2204">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="6dbb4-2205">True/False (預設值為 False)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2205">True, False (default)</span></span> |<span data-ttu-id="6dbb4-2206">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2206">No</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-2207">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2207">Example</span></span>

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "HdfsToBlobCopy",
            "inputs": [{
                "name": "InputDataset"
            }],
            "outputs": [{
                "name": "OutputDataset"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="6dbb4-2208">如需詳細資訊，請參閱 [HDFS 連接器](#data-factory-hdfs-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2208">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#copy-activity-properties) article.</span></span>

## <a name="sftp"></a><span data-ttu-id="6dbb4-2209">SFTP</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2209">SFTP</span></span>


### <a name="linked-service"></a><span data-ttu-id="6dbb4-2210">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2210">Linked service</span></span>
<span data-ttu-id="6dbb4-2211">若要定義 SFTP 連結服務，請將連結服務的 **type** 設為 **Sftp**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2211">To define an SFTP linked service, set the **type** of the linked service to **Sftp**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="6dbb4-2212">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2212">Property</span></span> | <span data-ttu-id="6dbb4-2213">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2213">Description</span></span> | <span data-ttu-id="6dbb4-2214">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2214">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-2215">主機</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2215">host</span></span> | <span data-ttu-id="6dbb4-2216">SFTP 伺服器的名稱或 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2216">Name or IP address of the SFTP server.</span></span> |<span data-ttu-id="6dbb4-2217">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2217">Yes</span></span> |
| <span data-ttu-id="6dbb4-2218">連接埠</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2218">port</span></span> |<span data-ttu-id="6dbb4-2219">SFTP 伺服器所接聽的連接埠。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2219">Port on which the SFTP server is listening.</span></span> <span data-ttu-id="6dbb4-2220">預設值：21</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2220">The default value is: 21</span></span> |<span data-ttu-id="6dbb4-2221">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2221">No</span></span> |
| <span data-ttu-id="6dbb4-2222">authenticationType</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2222">authenticationType</span></span> |<span data-ttu-id="6dbb4-2223">指定驗證類型。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2223">Specify authentication type.</span></span> <span data-ttu-id="6dbb4-2224">允許的值︰**Basic**、**SshPublicKey**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2224">Allowed values: **Basic**, **SshPublicKey**.</span></span> <br><br> <span data-ttu-id="6dbb4-2225">請參閱[使用基本驗證](#using-basic-authentication)和[使用 SSH 公開金鑰驗證](#using-ssh-public-key-authentication)章節，分別取得更多屬性和 JSON 範例。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2225">Refer to [Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span></span> |<span data-ttu-id="6dbb4-2226">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2226">Yes</span></span> |
| <span data-ttu-id="6dbb4-2227">skipHostKeyValidation</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2227">skipHostKeyValidation</span></span> | <span data-ttu-id="6dbb4-2228">指定是否略過主機金鑰驗證。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2228">Specify whether to skip host key validation.</span></span> | <span data-ttu-id="6dbb4-2229">否。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2229">No.</span></span> <span data-ttu-id="6dbb4-2230">預設值：false</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2230">The default value: false</span></span> |
| <span data-ttu-id="6dbb4-2231">hostKeyFingerprint</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2231">hostKeyFingerprint</span></span> | <span data-ttu-id="6dbb4-2232">指定主機金鑰的指紋。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2232">Specify the finger print of the host key.</span></span> | <span data-ttu-id="6dbb4-2233">如果 `skipHostKeyValidation` 設為 false，則為 [是]。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2233">Yes if the `skipHostKeyValidation` is set to false.</span></span>  |
| <span data-ttu-id="6dbb4-2234">gatewayName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2234">gatewayName</span></span> |<span data-ttu-id="6dbb4-2235">要連線至內部部署 SFTP 伺服器的資料管理閘道名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2235">Name of the Data Management Gateway to connect to an on-premises SFTP server.</span></span> | <span data-ttu-id="6dbb4-2236">如果從內部部署 SFTP 伺服器複製資料，則為 [是]。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2236">Yes if copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="6dbb4-2237">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2237">encryptedCredential</span></span> | <span data-ttu-id="6dbb4-2238">用來存取 SFTP 伺服器的加密認證。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2238">Encrypted credential to access the SFTP server.</span></span> <span data-ttu-id="6dbb4-2239">當您在複製精靈或 ClickOnce 快顯對話方塊中指定基本驗證 (使用者名稱 + 密碼) 或 SshPublicKey 驗證 (使用者名稱 + 私密金鑰路徑或內容) 時自動產生。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2239">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or the ClickOnce popup dialog.</span></span> | <span data-ttu-id="6dbb4-2240">否。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2240">No.</span></span> <span data-ttu-id="6dbb4-2241">僅當從內部部署 SFTP 伺服器複製資料時才套用。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2241">Apply only when copying data from an on-premises SFTP server.</span></span> |

#### <a name="example-using-basic-authentication"></a><span data-ttu-id="6dbb4-2242">範例：使用基本驗證</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2242">Example: Using basic authentication</span></span>

<span data-ttu-id="6dbb4-2243">若要使用基本驗證，將 `authenticationType` 設定為 `Basic`，然後指定上一節中介紹的 SFTP 連接器泛用以外的下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2243">To use basic authentication, set `authenticationType` as `Basic`, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span></span>

| <span data-ttu-id="6dbb4-2244">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2244">Property</span></span> | <span data-ttu-id="6dbb4-2245">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2245">Description</span></span> | <span data-ttu-id="6dbb4-2246">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2246">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-2247">username</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2247">username</span></span> | <span data-ttu-id="6dbb4-2248">可存取 SFTP 伺服器的使用者。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2248">User who has access to the SFTP server.</span></span> |<span data-ttu-id="6dbb4-2249">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2249">Yes</span></span> |
| <span data-ttu-id="6dbb4-2250">password</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2250">password</span></span> | <span data-ttu-id="6dbb4-2251">使用者 (使用者名稱) 的密碼。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2251">Password for the user (username).</span></span> | <span data-ttu-id="6dbb4-2252">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2252">Yes</span></span> |

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<SFTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a><span data-ttu-id="6dbb4-2253">範例：採用加密認證的基本驗證**</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2253">Example: Basic authentication with encrypted credential**</span></span>

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="using-ssh-public-key-authentication"></a><span data-ttu-id="6dbb4-2254">使用 SSH 公用金鑰驗證：**</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2254">Using SSH public key authentication:**</span></span>

<span data-ttu-id="6dbb4-2255">若要使用基本驗證，將 `authenticationType` 設定為 `SshPublicKey`，然後指定上一節中介紹的 SFTP 連接器泛用以外的下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2255">To use basic authentication, set `authenticationType` as `SshPublicKey`, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span></span>

| <span data-ttu-id="6dbb4-2256">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2256">Property</span></span> | <span data-ttu-id="6dbb4-2257">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2257">Description</span></span> | <span data-ttu-id="6dbb4-2258">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2258">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-2259">username</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2259">username</span></span> |<span data-ttu-id="6dbb4-2260">可存取 SFTP 伺服器的使用者</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2260">User who has access to the SFTP server</span></span> |<span data-ttu-id="6dbb4-2261">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2261">Yes</span></span> |
| <span data-ttu-id="6dbb4-2262">privateKeyPath</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2262">privateKeyPath</span></span> | <span data-ttu-id="6dbb4-2263">指定閘道可以存取之私密金鑰檔案的絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2263">Specify absolute path to the private key file that gateway can access.</span></span> | <span data-ttu-id="6dbb4-2264">指定 `privateKeyPath` 或 `privateKeyContent`。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2264">Specify either the `privateKeyPath` or `privateKeyContent`.</span></span> <br><br> <span data-ttu-id="6dbb4-2265">僅當從內部部署 SFTP 伺服器複製資料時才套用。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2265">Apply only when copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="6dbb4-2266">privateKeyContent</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2266">privateKeyContent</span></span> | <span data-ttu-id="6dbb4-2267">私密金鑰內容的序列化字串。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2267">A serialized string of the private key content.</span></span> <span data-ttu-id="6dbb4-2268">複製精靈可以讀取私密金鑰檔案，並自動解壓縮私密金鑰內容。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2268">The Copy Wizard can read the private key file and extract the private key content automatically.</span></span> <span data-ttu-id="6dbb4-2269">如果您使用任何其他工具/SDK，請改為使用 privateKeyPath 屬性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2269">If you are using any other tool/SDK, use the privateKeyPath property instead.</span></span> | <span data-ttu-id="6dbb4-2270">指定 `privateKeyPath` 或 `privateKeyContent`。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2270">Specify either the `privateKeyPath` or `privateKeyContent`.</span></span> |
| <span data-ttu-id="6dbb4-2271">passPhrase</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2271">passPhrase</span></span> | <span data-ttu-id="6dbb4-2272">如果金鑰檔案受到複雜密碼保護，請指定複雜密碼/密碼以將私密金鑰解密。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2272">Specify the pass phrase/password to decrypt the private key if the key file is protected by a pass phrase.</span></span> | <span data-ttu-id="6dbb4-2273">如果私密金鑰檔案受到複雜密碼保護，則為 [是]。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2273">Yes if the private key file is protected by a pass phrase.</span></span> |

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a><span data-ttu-id="6dbb4-2274">範例︰使用私密金鑰內容的 SshPublicKey 驗證**</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2274">Example: SshPublicKey authentication using private key content**</span></span>

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of the private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

<span data-ttu-id="6dbb4-2275">如需詳細資訊，請參閱 [SFTP 連接器](data-factory-sftp-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2275">For more information, see [SFTP connector](data-factory-sftp-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="6dbb4-2276">Dataset</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2276">Dataset</span></span>
<span data-ttu-id="6dbb4-2277">若要定義 SFTP 資料集，請將資料集的 **type** 設為 **FileShare**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2277">To define an SFTP dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="6dbb4-2278">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2278">Property</span></span> | <span data-ttu-id="6dbb4-2279">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2279">Description</span></span> | <span data-ttu-id="6dbb4-2280">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2280">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-2281">folderPath</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2281">folderPath</span></span> |<span data-ttu-id="6dbb4-2282">資料夾的子路徑。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2282">Sub path to the folder.</span></span> <span data-ttu-id="6dbb4-2283">使用逸出字元 ‘ \ ’ 當做字串中的特殊字元。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2283">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="6dbb4-2284">如需範例，請參閱 [範例連結服務和資料集定義](#sample-linked-service-and-dataset-definitions) 。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2284">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="6dbb4-2285">您可以結合此屬性與 **partitionBy**，讓資料夾路徑以配量開始/結束日期時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2285">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="6dbb4-2286">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2286">Yes</span></span> |
| <span data-ttu-id="6dbb4-2287">fileName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2287">fileName</span></span> |<span data-ttu-id="6dbb4-2288">如果您想要資料表參考資料夾中的特定檔案，請指定 **folderPath** 中的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2288">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="6dbb4-2289">如果沒有為此屬性指定任何值，資料表會指向資料夾中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2289">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="6dbb4-2290">若未指定輸出資料集的 fileName，所產生檔案的名稱是下列格式︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2290">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="6dbb4-2291">Data.<Guid>.txt (範例：Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2291">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="6dbb4-2292">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2292">No</span></span> |
| <span data-ttu-id="6dbb4-2293">fileFilter</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2293">fileFilter</span></span> |<span data-ttu-id="6dbb4-2294">指定要用來在 folderPath (而不是所有檔案) 中選取檔案子集的篩選器。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2294">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="6dbb4-2295">允許的值為︰`*` (多個字元) 和 `?` (單一字元)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2295">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="6dbb4-2296">範例 1：`"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2296">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="6dbb4-2297">範例 2：`"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2297">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="6dbb4-2298">fileFilter 適用於輸入 FileShare 資料集。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2298">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="6dbb4-2299">這個屬性不支援使用 HDFS。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2299">This property is not supported with HDFS.</span></span> |<span data-ttu-id="6dbb4-2300">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2300">No</span></span> |
| <span data-ttu-id="6dbb4-2301">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2301">partitionedBy</span></span> |<span data-ttu-id="6dbb4-2302">partitionedBy 可以用來指定時間序列資料的動態 folderPath 和 filename。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2302">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="6dbb4-2303">例如，folderPath 可針對每小時的資料進行參數化。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2303">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="6dbb4-2304">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2304">No</span></span> |
| <span data-ttu-id="6dbb4-2305">format</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2305">format</span></span> | <span data-ttu-id="6dbb4-2306">支援下列格式類型：**TextFormat**、**JsonFormat**、**AvroFormat**、**OrcFormat**、**ParquetFormat**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2306">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="6dbb4-2307">將格式下的 **type** 屬性設定為這些值其中之一。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2307">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="6dbb4-2308">如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2308">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="6dbb4-2309">如果您想要在以檔案為基礎的存放區之間**依原樣複製檔案** (二進位複本)，請在輸入和輸出資料集定義中略過格式區段。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2309">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="6dbb4-2310">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2310">No</span></span> |
| <span data-ttu-id="6dbb4-2311">compression</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2311">compression</span></span> | <span data-ttu-id="6dbb4-2312">指定此資料的壓縮類型和層級。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2312">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="6dbb4-2313">支援的類型為：**GZip**、**Deflate**、**BZip2** 及 **ZipDeflate**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2313">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="6dbb4-2314">支援的層級為：**Optimal** 和 **Fastest**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2314">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="6dbb4-2315">如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2315">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="6dbb4-2316">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2316">No</span></span> |
| <span data-ttu-id="6dbb4-2317">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2317">useBinaryTransfer</span></span> |<span data-ttu-id="6dbb4-2318">指定是否使用二進位傳輸模式。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2318">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="6dbb4-2319">二進位模式為 true，ASCII 則為 false。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2319">True for binary mode and false ASCII.</span></span> <span data-ttu-id="6dbb4-2320">預設值：True。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2320">Default value: True.</span></span> <span data-ttu-id="6dbb4-2321">只有在相關聯的連結服務類型的類型為 FtpServer 時，才可以使用這個屬性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2321">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="6dbb4-2322">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2322">No</span></span> |

> [!NOTE]
> <span data-ttu-id="6dbb4-2323">無法同時使用檔名和 fileFilter。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2323">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="6dbb4-2324">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2324">Example</span></span>

```json
{
    "name": "SFTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "SftpLinkedService",
        "typeProperties": {
            "folderPath": "<path to shared folder>",
            "fileName": "test.csv"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="6dbb4-2325">如需詳細資訊，請參閱 [SFTP 連接器](data-factory-sftp-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2325">For more information, see [SFTP connector](data-factory-sftp-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="6dbb4-2326">複製活動中的檔案系統來源</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2326">File System Source in Copy Activity</span></span>
<span data-ttu-id="6dbb4-2327">如果您從 SFTP 來源複製資料，請將複製活動的 **source type** 設為 **FileSystemSource**，並在 **source** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2327">If you are copying data from an SFTP source, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="6dbb4-2328">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2328">Property</span></span> | <span data-ttu-id="6dbb4-2329">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2329">Description</span></span> | <span data-ttu-id="6dbb4-2330">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2330">Allowed values</span></span> | <span data-ttu-id="6dbb4-2331">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2331">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-2332">遞迴</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2332">recursive</span></span> |<span data-ttu-id="6dbb4-2333">表示是否從子資料夾，或只有從指定的資料夾，以遞迴方式讀取資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2333">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="6dbb4-2334">True/False (預設值為 False)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2334">True, False (default)</span></span> |<span data-ttu-id="6dbb4-2335">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2335">No</span></span> |



#### <a name="example"></a><span data-ttu-id="6dbb4-2336">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2336">Example</span></span>

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2017-02-20T18:00:00",
        "end": "2017-02-20T19:00:00"
    }
}
```

<span data-ttu-id="6dbb4-2337">如需詳細資訊，請參閱 [SFTP 連接器](data-factory-sftp-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2337">For more information, see [SFTP connector](data-factory-sftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="http"></a><span data-ttu-id="6dbb4-2338">HTTP</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2338">HTTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="6dbb4-2339">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2339">Linked service</span></span>
<span data-ttu-id="6dbb4-2340">若要定義 HTTP 連結服務，請將連結服務的 **type** 設為 **Http**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2340">To define a HTTP linked service, set the **type** of the linked service to **Http**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="6dbb4-2341">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2341">Property</span></span> | <span data-ttu-id="6dbb4-2342">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2342">Description</span></span> | <span data-ttu-id="6dbb4-2343">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2343">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-2344">url</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2344">url</span></span> | <span data-ttu-id="6dbb4-2345">Web 伺服器的基本 URL</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2345">Base URL to the Web Server</span></span> | <span data-ttu-id="6dbb4-2346">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2346">Yes</span></span> |
| <span data-ttu-id="6dbb4-2347">authenticationType</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2347">authenticationType</span></span> | <span data-ttu-id="6dbb4-2348">指定驗證類型。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2348">Specifies the authentication type.</span></span> <span data-ttu-id="6dbb4-2349">允許的值為︰**匿名**、**基本**、**摘要**、**Windows**、**ClientCertificate**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2349">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="6dbb4-2350">請分別參閱此關於更多屬性的下列資料表各節以及這些驗證類型的 JSON 範例。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2350">Refer to sections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="6dbb4-2351">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2351">Yes</span></span> |
| <span data-ttu-id="6dbb4-2352">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2352">enableServerCertificateValidation</span></span> | <span data-ttu-id="6dbb4-2353">如果來源是 HTTPS Web 伺服器，指定是否啟用伺服器 SSL 憑證驗證</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2353">Specify whether to enable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="6dbb4-2354">否，預設值是 True</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2354">No, default is true</span></span> |
| <span data-ttu-id="6dbb4-2355">gatewayName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2355">gatewayName</span></span> | <span data-ttu-id="6dbb4-2356">連接至內部部署 HTTP 來源的「資料管理閘道」閘道。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2356">Name of the Data Management Gateway to connect to an on-premises HTTP source.</span></span> | <span data-ttu-id="6dbb4-2357">如果從內部部署 HTTP 來源複製資料，則為是。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2357">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="6dbb4-2358">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2358">encryptedCredential</span></span> | <span data-ttu-id="6dbb4-2359">用來存取 HTTP 端點的加密認證。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2359">Encrypted credential to access the HTTP endpoint.</span></span> <span data-ttu-id="6dbb4-2360">當您在複製精靈或 ClickOnce 快顯對話方塊中設定驗證資訊時會自動產生。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2360">Auto-generated when you configure the authentication information in copy wizard or the ClickOnce popup dialog.</span></span> | <span data-ttu-id="6dbb4-2361">否。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2361">No.</span></span> <span data-ttu-id="6dbb4-2362">僅當從內部部署 HTTP 伺服器複製資料時才套用。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2362">Apply only when copying data from an on-premises HTTP server.</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="6dbb4-2363">範例︰使用基本、摘要或 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2363">Example: Using Basic, Digest, or Windows authentication</span></span>
<span data-ttu-id="6dbb4-2364">將 `authenticationType` 設定為 `Basic`、`Digest`或 `Windows`，並指定除了上面介紹的 HTTP 連接器泛用的下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2364">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="6dbb4-2365">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2365">Property</span></span> | <span data-ttu-id="6dbb4-2366">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2366">Description</span></span> | <span data-ttu-id="6dbb4-2367">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2367">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-2368">username</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2368">username</span></span> | <span data-ttu-id="6dbb4-2369">存取 HTTP 端點的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2369">Username to access the HTTP endpoint.</span></span> | <span data-ttu-id="6dbb4-2370">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2370">Yes</span></span> |
| <span data-ttu-id="6dbb4-2371">password</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2371">password</span></span> | <span data-ttu-id="6dbb4-2372">使用者 (使用者名稱) 的密碼。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2372">Password for the user (username).</span></span> | <span data-ttu-id="6dbb4-2373">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2373">Yes</span></span> |

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "basic",
            "url": "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

#### <a name="example-using-clientcertificate-authentication"></a><span data-ttu-id="6dbb4-2374">範例：使用 ClientCertificate 驗證</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2374">Example: Using ClientCertificate authentication</span></span>

<span data-ttu-id="6dbb4-2375">若要使用基本驗證，將 `authenticationType` 設定為 `ClientCertificate`，並指定除了上面介紹的 HTTP 連接器泛用的下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2375">To use basic authentication, set `authenticationType` as `ClientCertificate`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="6dbb4-2376">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2376">Property</span></span> | <span data-ttu-id="6dbb4-2377">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2377">Description</span></span> | <span data-ttu-id="6dbb4-2378">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2378">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-2379">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2379">embeddedCertData</span></span> | <span data-ttu-id="6dbb4-2380">Base 64 編碼的個人資訊交換 (PFX) 檔案之二進位資料內容。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2380">The Base64-encoded contents of binary data of the Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="6dbb4-2381">指定 `embeddedCertData` 或 `certThumbprint`。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2381">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="6dbb4-2382">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2382">certThumbprint</span></span> | <span data-ttu-id="6dbb4-2383">憑證指紋已安裝在您閘道器電腦的憑證存放區上。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2383">The thumbprint of the certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="6dbb4-2384">僅當從內部部署 HTTP 來源複製資料時才套用。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2384">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="6dbb4-2385">指定 `embeddedCertData` 或 `certThumbprint`。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2385">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="6dbb4-2386">password</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2386">password</span></span> | <span data-ttu-id="6dbb4-2387">與憑證相關聯的密碼。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2387">Password associated with the certificate.</span></span> | <span data-ttu-id="6dbb4-2388">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2388">No</span></span> |

<span data-ttu-id="6dbb4-2389">如果您使用 `certThumbprint` 進行驗證且憑證已安裝在本機電腦的個人存放區中，您必須授與讀取權限給閘道器服務︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2389">If you use `certThumbprint` for authentication and the certificate is installed in the personal store of the local computer, you need to grant the read permission to the gateway service:</span></span>

1. <span data-ttu-id="6dbb4-2390">啟動 Microsoft Management Console (MMC)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2390">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="6dbb4-2391">新增目標為 [本機電腦] 的 [憑證] 嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2391">Add the **Certificates** snap-in that targets the **Local Computer**.</span></span>
2. <span data-ttu-id="6dbb4-2392">展開 [憑證]，[個人]，然後按一下 [憑證]。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2392">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="6dbb4-2393">以滑鼠右鍵按一下個人存放區中的 [憑證]，然後選取 [所有工作]->[管理私用金鑰...]</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2393">Right-click the certificate from the personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="6dbb4-2394">在 [安全性] 索引標籤上，新增資料管理閘道主機服務使用憑證讀取存取執行所在的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2394">On the **Security** tab, add the user account under which Data Management Gateway Host Service is running with the read access to the certificate.</span></span>  

<span data-ttu-id="6dbb4-2395">**範例：使用用戶端憑證：**此連結服務會將您的資料處理站連結至內部部署 HTTP Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2395">**Example: using client certificate:** This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="6dbb4-2396">它會使用已安裝資料管理閘道的電腦上所安裝的用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2396">It uses a client certificate that is installed on the machine with Data Management Gateway installed.</span></span>

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"
        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="6dbb4-2397">範例︰在檔案中使用用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2397">Example: using client certificate in a file</span></span>
<span data-ttu-id="6dbb4-2398">此連結服務會將您的資料處理站與內部部署 HTTP web 伺服器連結。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2398">This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="6dbb4-2399">它會使用已安裝資料管理閘道的電腦上的用戶端憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2399">It uses a client certificate file on the machine with Data Management Gateway installed.</span></span>

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

<span data-ttu-id="6dbb4-2400">如需詳細資訊，請參閱 [HTTP 連接器](data-factory-http-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2400">For more information, see [HTTP connector](data-factory-http-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="6dbb4-2401">Dataset</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2401">Dataset</span></span>
<span data-ttu-id="6dbb4-2402">若要定義 HTTP 資料集，請將資料集的 **type** 設為 **Http**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2402">To define a HTTP dataset, set the **type** of the dataset to **Http**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="6dbb4-2403">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2403">Property</span></span> | <span data-ttu-id="6dbb4-2404">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2404">Description</span></span> | <span data-ttu-id="6dbb4-2405">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2405">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="6dbb4-2406">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2406">relativeUrl</span></span> | <span data-ttu-id="6dbb4-2407">包含資料之資源的相對 URL。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2407">A relative URL to the resource that contains the data.</span></span> <span data-ttu-id="6dbb4-2408">當路徑未指定時，則只會使用在連結服務定義中指定的 URL。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2408">When path is not specified, only the URL specified in the linked service definition is used.</span></span> <br><br> <span data-ttu-id="6dbb4-2409">若要建構動態 URL，您可以使用 [Data Factory 函式和系統變數](data-factory-functions-variables.md)，範例︰`"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2409">To construct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), Example: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span></span> | <span data-ttu-id="6dbb4-2410">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2410">No</span></span> |
| <span data-ttu-id="6dbb4-2411">requestMethod</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2411">requestMethod</span></span> | <span data-ttu-id="6dbb4-2412">HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2412">Http method.</span></span> <span data-ttu-id="6dbb4-2413">允許的值為 **GET** 或 **POST**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2413">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="6dbb4-2414">否。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2414">No.</span></span> <span data-ttu-id="6dbb4-2415">預設值為 `GET`。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2415">Default is `GET`.</span></span> |
| <span data-ttu-id="6dbb4-2416">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2416">additionalHeaders</span></span> | <span data-ttu-id="6dbb4-2417">其他 HTTP 要求標頭。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2417">Additional HTTP request headers.</span></span> | <span data-ttu-id="6dbb4-2418">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2418">No</span></span> |
| <span data-ttu-id="6dbb4-2419">requestBody</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2419">requestBody</span></span> | <span data-ttu-id="6dbb4-2420">HTTP 要求的內文。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2420">Body for HTTP request.</span></span> | <span data-ttu-id="6dbb4-2421">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2421">No</span></span> |
| <span data-ttu-id="6dbb4-2422">format</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2422">format</span></span> | <span data-ttu-id="6dbb4-2423">如果您只想要**從 HTTP 端點依現狀擷取資料**而不剖析它，請略過此格式設定。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2423">If you want to simply **retrieve the data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="6dbb4-2424">如果您想要在複製期間剖析 HTTP 回應內容，支援下列格式類型：**TextFormat**、**JsonFormat**、**AvroFormat**、**OrcFormat**、**ParquetFormat**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2424">If you want to parse the HTTP response content during copy, the following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="6dbb4-2425">如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2425">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="6dbb4-2426">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2426">No</span></span> |
| <span data-ttu-id="6dbb4-2427">compression</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2427">compression</span></span> | <span data-ttu-id="6dbb4-2428">指定此資料的壓縮類型和層級。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2428">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="6dbb4-2429">支援的類型為：**GZip**、**Deflate**、**BZip2** 及 **ZipDeflate**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2429">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="6dbb4-2430">支援的層級為：**Optimal** 和 **Fastest**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2430">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="6dbb4-2431">如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2431">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="6dbb4-2432">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2432">No</span></span> |

#### <a name="example-using-the-get-default-method"></a><span data-ttu-id="6dbb4-2433">範例︰使用 GET (預設值) 方法</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2433">Example: using the GET (default) method</span></span>

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

#### <a name="example-using-the-post-method"></a><span data-ttu-id="6dbb4-2434">範例︰使用 POST 方法</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2434">Example: using the POST method</span></span>

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
            "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
<span data-ttu-id="6dbb4-2435">如需詳細資訊，請參閱 [HTTP 連接器](data-factory-http-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2435">For more information, see [HTTP connector](data-factory-http-connector.md#dataset-properties) article.</span></span>

### <a name="http-source-in-copy-activity"></a><span data-ttu-id="6dbb4-2436">複製活動中的 HTTP 來源</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2436">HTTP Source in Copy Activity</span></span>
<span data-ttu-id="6dbb4-2437">如果您從 HTTP 來源複製資料，請將複製活動的 **source type** 設為 **HttpSource**，並在 **source** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2437">If you are copying data from a HTTP source, set the **source type** of the copy activity to **HttpSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="6dbb4-2438">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2438">Property</span></span> | <span data-ttu-id="6dbb4-2439">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2439">Description</span></span> | <span data-ttu-id="6dbb4-2440">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2440">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="6dbb4-2441">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2441">httpRequestTimeout</span></span> | <span data-ttu-id="6dbb4-2442">HTTP 的逾時 (TimeSpan) 要求取得回應。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2442">The timeout (TimeSpan) for the HTTP request to get a response.</span></span> <span data-ttu-id="6dbb4-2443">逾時會取得回應，而非逾時讀取回應資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2443">It is the timeout to get a response, not the timeout to read response data.</span></span> | <span data-ttu-id="6dbb4-2444">否。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2444">No.</span></span> <span data-ttu-id="6dbb4-2445">預設值：00:01:40</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2445">Default value: 00:01:40</span></span> |


#### <a name="example"></a><span data-ttu-id="6dbb4-2446">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2446">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "HttpSourceToAzureBlob",
            "description": "Copy from an HTTP source to an Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "HttpSourceDataInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "HttpSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="6dbb4-2447">如需詳細資訊，請參閱 [HTTP 連接器](data-factory-http-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2447">For more information, see [HTTP connector](data-factory-http-connector.md#copy-activity-properties) article.</span></span>

## <a name="odata"></a><span data-ttu-id="6dbb4-2448">OData</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2448">OData</span></span>

### <a name="linked-service"></a><span data-ttu-id="6dbb4-2449">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2449">Linked service</span></span>
<span data-ttu-id="6dbb4-2450">若要定義 OData 連結服務，請將連結服務的 **type** 設為 **OData**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2450">To define an OData linked service, set the **type** of the linked service to **OData**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="6dbb4-2451">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2451">Property</span></span> | <span data-ttu-id="6dbb4-2452">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2452">Description</span></span> | <span data-ttu-id="6dbb4-2453">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2453">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-2454">url</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2454">url</span></span> |<span data-ttu-id="6dbb4-2455">OData 服務的 URL。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2455">Url of the OData service.</span></span> |<span data-ttu-id="6dbb4-2456">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2456">Yes</span></span> |
| <span data-ttu-id="6dbb4-2457">authenticationType</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2457">authenticationType</span></span> |<span data-ttu-id="6dbb4-2458">用來連線到 OData 來源的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2458">Type of authentication used to connect to the OData source.</span></span> <br/><br/> <span data-ttu-id="6dbb4-2459">若為雲端 OData，可能的值為 Anonymous、Basic 和 OAuth (請注意，Azure Data Factory 目前僅支援 Azure Active Directory 架構的 OAuth)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2459">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="6dbb4-2460">若為內部部署 OData，可能的值為 Anonymous、Basic 和 Windows。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2460">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="6dbb4-2461">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2461">Yes</span></span> |
| <span data-ttu-id="6dbb4-2462">username</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2462">username</span></span> |<span data-ttu-id="6dbb4-2463">如果您要使用 Basic 驗證，請指定使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2463">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="6dbb4-2464">是 (只在您使用基本驗證時)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2464">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="6dbb4-2465">password</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2465">password</span></span> |<span data-ttu-id="6dbb4-2466">指定您為使用者名稱所指定之使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2466">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="6dbb4-2467">是 (只在您使用基本驗證時)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2467">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="6dbb4-2468">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2468">authorizedCredential</span></span> |<span data-ttu-id="6dbb4-2469">如果您使用 OAuth，按一下 Data Factory 複製精靈或編輯器中的 [授權] 按鈕，然後輸入您的認證，接著將會自動產生這個屬性的值。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2469">If you are using OAuth, click **Authorize** button in the Data Factory Copy Wizard or Editor and enter your credential, then the value of this property will be auto-generated.</span></span> |<span data-ttu-id="6dbb4-2470">是 (只有在您使用 OAuth 驗證時)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2470">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="6dbb4-2471">gatewayName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2471">gatewayName</span></span> |<span data-ttu-id="6dbb4-2472">Data Factory 服務應該用來連接到內部部署 OData 服務的閘道器名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2472">Name of the gateway that the Data Factory service should use to connect to the on-premises OData service.</span></span> <span data-ttu-id="6dbb4-2473">只在要從內部部署 OData 來源複製資料時才指定。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2473">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="6dbb4-2474">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2474">No</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="6dbb4-2475">範例 - 使用基本驗證</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2475">Example - Using Basic authentication</span></span>
```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Basic",
            "username": "username",
            "password": "password"
        }
    }
}
```

#### <a name="example---using-anonymous-authentication"></a><span data-ttu-id="6dbb4-2476">範例 - 使用匿名驗證</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2476">Example - Using Anonymous authentication</span></span>

```json
{
    "name": "ODataLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        }
    }
}
```

#### <a name="example---using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="6dbb4-2477">範例 - 使用 Windows 驗證存取內部部署 OData 來源</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2477">Example - Using Windows authentication accessing on-premises OData source</span></span>

```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "<endpoint of on-premises OData source, for example, Dynamics CRM>",
            "authenticationType": "Windows",
            "username": "domain\\user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example---using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="6dbb4-2478">範例 - 使用 OAuth 驗證存取雲端 OData 來源</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2478">Example - Using OAuth authentication accessing cloud OData source</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of cloud OData source, for example, https://<tenant>.crm.dynamics.com/XRMServices/2011/OrganizationData.svc>",
            "authenticationType": "OAuth",
            "authorizedCredential": "<auto generated by clicking the Authorize button on UI>"
        }
    }
}
```

<span data-ttu-id="6dbb4-2479">如需詳細資訊，請參閱 [OData 連接器](data-factory-odata-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2479">For more information, see [OData connector](data-factory-odata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="6dbb4-2480">Dataset</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2480">Dataset</span></span>
<span data-ttu-id="6dbb4-2481">若要定義 OData 資料集，請將資料集的 **type** 設為 **ODataResource**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2481">To define an OData dataset, set the **type** of the dataset to **ODataResource**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="6dbb4-2482">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2482">Property</span></span> | <span data-ttu-id="6dbb4-2483">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2483">Description</span></span> | <span data-ttu-id="6dbb4-2484">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2484">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-2485">path</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2485">path</span></span> |<span data-ttu-id="6dbb4-2486">OData 資源的路徑</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2486">Path to the OData resource</span></span> |<span data-ttu-id="6dbb4-2487">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2487">No</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-2488">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2488">Example</span></span>

```json
{
    "name": "ODataDataset",
    "properties": {
        "type": "ODataResource",
        "typeProperties": {
            "path": "Products"
        },
        "linkedServiceName": "ODataLinkedService",
        "structure": [],
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3
        }
    }
}
```

<span data-ttu-id="6dbb4-2489">如需詳細資訊，請參閱 [OData 連接器](data-factory-odata-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2489">For more information, see [OData connector](data-factory-odata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="6dbb4-2490">複製活動中的關聯式來源</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2490">Relational Source in Copy Activity</span></span>
<span data-ttu-id="6dbb4-2491">如果您從 OData 來源複製資料，請將複製活動的 **source type** 設為 **RelationalSource**，並在 **source** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2491">If you are copying data from an OData source, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="6dbb4-2492">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2492">Property</span></span> | <span data-ttu-id="6dbb4-2493">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2493">Description</span></span> | <span data-ttu-id="6dbb4-2494">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2494">Example</span></span> | <span data-ttu-id="6dbb4-2495">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2495">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-2496">query</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2496">query</span></span> |<span data-ttu-id="6dbb4-2497">使用自訂查詢來讀取資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2497">Use the custom query to read data.</span></span> |<span data-ttu-id="6dbb4-2498">「?$select=Name, Description&$top=5」</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2498">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="6dbb4-2499">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2499">No</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-2500">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2500">Example</span></span>

```json
{
    "name": "CopyODataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "?$select=Name, Description&$top=5"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "ODataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobODataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "ODataToBlob"
        }],
        "start": "2017-02-01T18:00:00",
        "end": "2017-02-03T19:00:00"
    }
}
```

<span data-ttu-id="6dbb4-2501">如需詳細資訊，請參閱 [OData 連接器](data-factory-odata-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2501">For more information, see [OData connector](data-factory-odata-connector.md#copy-activity-properties) article.</span></span>


## <a name="odbc"></a><span data-ttu-id="6dbb4-2502">ODBC</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2502">ODBC</span></span>


### <a name="linked-service"></a><span data-ttu-id="6dbb4-2503">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2503">Linked service</span></span>
<span data-ttu-id="6dbb4-2504">若要定義 ODBC 連結服務，請將連結服務的 **type** 設為 **OnPremisesOdbc**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2504">To define an ODBC linked service, set the **type** of the linked service to **OnPremisesOdbc**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="6dbb4-2505">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2505">Property</span></span> | <span data-ttu-id="6dbb4-2506">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2506">Description</span></span> | <span data-ttu-id="6dbb4-2507">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2507">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-2508">connectionString</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2508">connectionString</span></span> |<span data-ttu-id="6dbb4-2509">連接字串的非存取認證部分和選擇性的加密認證。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2509">The non-access credential portion of the connection string and an optional encrypted credential.</span></span> <span data-ttu-id="6dbb4-2510">請參閱下列幾節中的範例。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2510">See examples in the following sections.</span></span> |<span data-ttu-id="6dbb4-2511">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2511">Yes</span></span> |
| <span data-ttu-id="6dbb4-2512">認證</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2512">credential</span></span> |<span data-ttu-id="6dbb4-2513">以驅動程式特定「屬性-值」格式指定之連接字串的存取認證部分。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2513">The access credential portion of the connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="6dbb4-2514">範例：“Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2514">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="6dbb4-2515">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2515">No</span></span> |
| <span data-ttu-id="6dbb4-2516">authenticationType</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2516">authenticationType</span></span> |<span data-ttu-id="6dbb4-2517">用來連接到 ODBC 資料存放區的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2517">Type of authentication used to connect to the ODBC data store.</span></span> <span data-ttu-id="6dbb4-2518">可能的值為：Anonymous 和 Basic。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2518">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="6dbb4-2519">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2519">Yes</span></span> |
| <span data-ttu-id="6dbb4-2520">username</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2520">username</span></span> |<span data-ttu-id="6dbb4-2521">如果您要使用 Basic 驗證，請指定使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2521">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="6dbb4-2522">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2522">No</span></span> |
| <span data-ttu-id="6dbb4-2523">password</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2523">password</span></span> |<span data-ttu-id="6dbb4-2524">指定您為使用者名稱所指定之使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2524">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="6dbb4-2525">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2525">No</span></span> |
| <span data-ttu-id="6dbb4-2526">gatewayName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2526">gatewayName</span></span> |<span data-ttu-id="6dbb4-2527">Data Factory 服務應該用來連接到 ODBC 資料存放區的閘道器名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2527">Name of the gateway that the Data Factory service should use to connect to the ODBC data store.</span></span> |<span data-ttu-id="6dbb4-2528">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2528">Yes</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="6dbb4-2529">範例 - 使用基本驗證</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2529">Example - Using Basic authentication</span></span>

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```
#### <a name="example---using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="6dbb4-2530">範例 - 使用基本驗證搭配加密認證</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2530">Example - Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="6dbb4-2531">您可以使用 [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 版的 Azure PowerShell) Cmdlet 或 [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 或更舊版的 Azure PowerShell) 來加密認證。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2531">You can encrypt the credentials using the [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of the Azure PowerShell).</span></span>  

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="6dbb4-2532">範例：使用匿名驗證</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2532">Example: Using Anonymous authentication</span></span>

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="6dbb4-2533">如需詳細資訊，請參閱 [ODBC 連接器](data-factory-odbc-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2533">For more information, see [ODBC connector](data-factory-odbc-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="6dbb4-2534">Dataset</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2534">Dataset</span></span>
<span data-ttu-id="6dbb4-2535">若要定義 ODBC 資料集，請將資料集的 **type** 設為 **RelationalTable**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2535">To define an ODBC dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="6dbb4-2536">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2536">Property</span></span> | <span data-ttu-id="6dbb4-2537">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2537">Description</span></span> | <span data-ttu-id="6dbb4-2538">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2538">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-2539">tableName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2539">tableName</span></span> |<span data-ttu-id="6dbb4-2540">ODBC 資料存放區中資料表的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2540">Name of the table in the ODBC data store.</span></span> |<span data-ttu-id="6dbb4-2541">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2541">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="6dbb4-2542">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2542">Example</span></span>

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "ODBCLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="6dbb4-2543">如需詳細資訊，請參閱 [ODBC 連接器](data-factory-odbc-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2543">For more information, see [ODBC connector](data-factory-odbc-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="6dbb4-2544">複製活動中的關聯式來源</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2544">Relational Source in Copy Activity</span></span>
<span data-ttu-id="6dbb4-2545">如果您從 ODBC 資料存放區複製資料，請將複製活動的 **source type** 設為 **RelationalSource**，並在 **source** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2545">If you are copying data from an ODBC data store, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="6dbb4-2546">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2546">Property</span></span> | <span data-ttu-id="6dbb4-2547">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2547">Description</span></span> | <span data-ttu-id="6dbb4-2548">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2548">Allowed values</span></span> | <span data-ttu-id="6dbb4-2549">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2549">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-2550">query</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2550">query</span></span> |<span data-ttu-id="6dbb4-2551">使用自訂查詢來讀取資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2551">Use the custom query to read data.</span></span> |<span data-ttu-id="6dbb4-2552">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2552">SQL query string.</span></span> <span data-ttu-id="6dbb4-2553">例如： `select * from MyTable`。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2553">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="6dbb4-2554">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2554">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-2555">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2555">Example</span></span>

```json
{
    "name": "CopyODBCToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "OdbcDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobOdbcDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "OdbcToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
``` 

<span data-ttu-id="6dbb4-2556">如需詳細資訊，請參閱 [ODBC 連接器](data-factory-odbc-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2556">For more information, see [ODBC connector](data-factory-odbc-connector.md#copy-activity-properties) article.</span></span>

## <a name="salesforce"></a><span data-ttu-id="6dbb4-2557">Salesforce</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2557">Salesforce</span></span>


### <a name="linked-service"></a><span data-ttu-id="6dbb4-2558">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2558">Linked service</span></span>
<span data-ttu-id="6dbb4-2559">若要定義 Salesforce 連結服務，請將連結服務的 **type** 設為 **Salesforce**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2559">To define a Salesforce linked service, set the **type** of the linked service to **Salesforce**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="6dbb4-2560">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2560">Property</span></span> | <span data-ttu-id="6dbb4-2561">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2561">Description</span></span> | <span data-ttu-id="6dbb4-2562">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2562">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-2563">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2563">environmentUrl</span></span> | <span data-ttu-id="6dbb4-2564">指定 Salesforce 執行個體的 URL。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2564">Specify the URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="6dbb4-2565">- 預設值為 "https://login.salesforce.com"。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2565">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="6dbb4-2566">- 若要從沙箱複製資料，請指定 "https://test.salesforce.com"。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2566">- To copy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="6dbb4-2567">- 若要從自訂網域複製資料，舉例來說，請指定 "https://[網域].my.salesforce.com"。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2567">- To copy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="6dbb4-2568">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2568">No</span></span> |
| <span data-ttu-id="6dbb4-2569">username</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2569">username</span></span> |<span data-ttu-id="6dbb4-2570">指定使用者帳戶的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2570">Specify a user name for the user account.</span></span> |<span data-ttu-id="6dbb4-2571">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2571">Yes</span></span> |
| <span data-ttu-id="6dbb4-2572">password</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2572">password</span></span> |<span data-ttu-id="6dbb4-2573">指定使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2573">Specify a password for the user account.</span></span> |<span data-ttu-id="6dbb4-2574">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2574">Yes</span></span> |
| <span data-ttu-id="6dbb4-2575">securityToken</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2575">securityToken</span></span> |<span data-ttu-id="6dbb4-2576">指定使用者帳戶的安全性權杖。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2576">Specify a security token for the user account.</span></span> <span data-ttu-id="6dbb4-2577">如需如何重設/取得安全性權杖的指示，請參閱 [取得安全性權杖](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) 。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2577">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how to reset/get a security token.</span></span> <span data-ttu-id="6dbb4-2578">若要整體了解安全性權杖，請參閱[安全性和 API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2578">To learn about security tokens in general, see [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="6dbb4-2579">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2579">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-2580">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2580">Example</span></span>

```json
{
    "name": "SalesforceLinkedService",
    "properties": {
        "type": "Salesforce",
        "typeProperties": {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```

<span data-ttu-id="6dbb4-2581">如需詳細資訊，請參閱 [Salesforce 連接器](data-factory-salesforce-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2581">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="6dbb4-2582">Dataset</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2582">Dataset</span></span>
<span data-ttu-id="6dbb4-2583">若要定義 Salesforce 資料集，請將資料集的 **type** 設為 **RelationalTable**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2583">To define a Salesforce dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="6dbb4-2584">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2584">Property</span></span> | <span data-ttu-id="6dbb4-2585">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2585">Description</span></span> | <span data-ttu-id="6dbb4-2586">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2586">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-2587">tableName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2587">tableName</span></span> |<span data-ttu-id="6dbb4-2588">Salesforce 中資料表的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2588">Name of the table in Salesforce.</span></span> |<span data-ttu-id="6dbb4-2589">否 (如果已指定 **RelationalSource** 的 **query**)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2589">No (if a **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-2590">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2590">Example</span></span>

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="6dbb4-2591">如需詳細資訊，請參閱 [Salesforce 連接器](data-factory-salesforce-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2591">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="6dbb4-2592">複製活動中的關聯式來源</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2592">Relational Source in Copy Activity</span></span>
<span data-ttu-id="6dbb4-2593">如果您從 Salesforce 複製資料，請將複製活動的 **source type** 設為 **RelationalSource**，並在 **source** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2593">If you are copying data from Salesforce, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="6dbb4-2594">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2594">Property</span></span> | <span data-ttu-id="6dbb4-2595">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2595">Description</span></span> | <span data-ttu-id="6dbb4-2596">允許的值</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2596">Allowed values</span></span> | <span data-ttu-id="6dbb4-2597">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2597">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dbb4-2598">query</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2598">query</span></span> |<span data-ttu-id="6dbb4-2599">使用自訂查詢來讀取資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2599">Use the custom query to read data.</span></span> |<span data-ttu-id="6dbb4-2600">SQL-92 查詢或 [Salesforce 物件查詢語言 (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) 查詢。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2600">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="6dbb4-2601">例如：`select * from MyTable__c`。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2601">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="6dbb4-2602">否 (如果已指定 **dataset** 的 **tableName**)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2602">No (if the **tableName** of the **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-2603">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2603">Example</span></span>  



```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce to an Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "SalesforceInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="6dbb4-2604">任何自訂物件都需要 API 名稱的「__c」部分。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2604">The "__c" part of the API Name is needed for any custom object.</span></span>

<span data-ttu-id="6dbb4-2605">如需詳細資訊，請參閱 [Salesforce 連接器](data-factory-salesforce-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2605">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#copy-activity-properties) article.</span></span> 

## <a name="web-data"></a><span data-ttu-id="6dbb4-2606">Web 資料</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2606">Web Data</span></span> 

### <a name="linked-service"></a><span data-ttu-id="6dbb4-2607">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2607">Linked service</span></span>
<span data-ttu-id="6dbb4-2608">若要定義 Web 連結服務，請將連結服務的 **type** 設為 **Web**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2608">To define a Web linked service, set the **type** of the linked service to **Web**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="6dbb4-2609">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2609">Property</span></span> | <span data-ttu-id="6dbb4-2610">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2610">Description</span></span> | <span data-ttu-id="6dbb4-2611">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2611">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-2612">Url</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2612">Url</span></span> |<span data-ttu-id="6dbb4-2613">Web 來源的 URL</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2613">URL to the Web source</span></span> |<span data-ttu-id="6dbb4-2614">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2614">Yes</span></span> |
| <span data-ttu-id="6dbb4-2615">authenticationType</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2615">authenticationType</span></span> |<span data-ttu-id="6dbb4-2616">匿名。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2616">Anonymous.</span></span> |<span data-ttu-id="6dbb4-2617">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2617">Yes</span></span> |
 

#### <a name="example"></a><span data-ttu-id="6dbb4-2618">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2618">Example</span></span>


```json
{
    "name": "web",
    "properties": {
        "type": "Web",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "url": "https://en.wikipedia.org/wiki/"
        }
    }
}
```

<span data-ttu-id="6dbb4-2619">如需詳細資訊，請參閱 [Web 資料表連接器](data-factory-web-table-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2619">For more information, see [Web Table connector](data-factory-web-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="6dbb4-2620">Dataset</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2620">Dataset</span></span>
<span data-ttu-id="6dbb4-2621">若要定義 Web 資料集，請將資料集的 **type** 設為 **WebTable**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2621">To define a Web dataset, set the **type** of the dataset to **WebTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="6dbb4-2622">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2622">Property</span></span> | <span data-ttu-id="6dbb4-2623">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2623">Description</span></span> | <span data-ttu-id="6dbb4-2624">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2624">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="6dbb4-2625">類型</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2625">type</span></span> |<span data-ttu-id="6dbb4-2626">資料集的類型。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2626">type of the dataset.</span></span> <span data-ttu-id="6dbb4-2627">必須設定為 **WebTable**</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2627">must be set to **WebTable**</span></span> |<span data-ttu-id="6dbb4-2628">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2628">Yes</span></span> |
| <span data-ttu-id="6dbb4-2629">路徑</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2629">path</span></span> |<span data-ttu-id="6dbb4-2630">包含資料表之資源的相對 URL。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2630">A relative URL to the resource that contains the table.</span></span> |<span data-ttu-id="6dbb4-2631">否。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2631">No.</span></span> <span data-ttu-id="6dbb4-2632">當路徑未指定時，則只會使用在連結服務定義中指定的 URL。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2632">When path is not specified, only the URL specified in the linked service definition is used.</span></span> |
| <span data-ttu-id="6dbb4-2633">index</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2633">index</span></span> |<span data-ttu-id="6dbb4-2634">資源中資料表的索引。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2634">The index of the table in the resource.</span></span> <span data-ttu-id="6dbb4-2635">如需如何取得 HTML 網頁中資料表索引的步驟，請參閱 [取得 HTML 網頁中資料表的索引](#get-index-of-a-table-in-an-html-page) 一節。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2635">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps to getting index of a table in an HTML page.</span></span> |<span data-ttu-id="6dbb4-2636">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2636">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="6dbb4-2637">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2637">Example</span></span>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="6dbb4-2638">如需詳細資訊，請參閱 [Web 資料表連接器](data-factory-web-table-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2638">For more information, see [Web Table connector](data-factory-web-table-connector.md#dataset-properties) article.</span></span> 

### <a name="web-source-in-copy-activity"></a><span data-ttu-id="6dbb4-2639">複製活動中的 Web 來源</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2639">Web Source in Copy Activity</span></span>
<span data-ttu-id="6dbb4-2640">如果您從 Web 資料表複製資料，請將複製活動的 **source type** 設為 **WebSource**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2640">If you are copying data from a web table, set the **source type** of the copy activity to **WebSource**.</span></span> <span data-ttu-id="6dbb4-2641">當複製活動中的來源類型為 **WebSource**，目前並未支援任何其他屬性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2641">Currently, when the source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>

#### <a name="example"></a><span data-ttu-id="6dbb4-2642">範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2642">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "WebTableToAzureBlob",
            "description": "Copy from a Web table to an Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "WebTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "WebSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="6dbb4-2643">如需詳細資訊，請參閱 [Web 資料表連接器](data-factory-web-table-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2643">For more information, see [Web Table connector](data-factory-web-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="compute-environments"></a><span data-ttu-id="6dbb4-2644">計算環境</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2644">COMPUTE ENVIRONMENTS</span></span>
<span data-ttu-id="6dbb4-2645">下表列出 Data Factory 支援的計算環境和可在這些環境上執行的轉換活動。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2645">The following table lists the compute environments supported by Data Factory and the transformation activities that can run on them.</span></span> <span data-ttu-id="6dbb4-2646">按一下您感興趣的計算連結，查看連結服務的 JSON 結構描述，以將它連結至資料處理站。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2646">Click the link for the compute you are interested in to see the JSON schemas for linked service to link it to a data factory.</span></span> 

| <span data-ttu-id="6dbb4-2647">計算環境</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2647">Compute environment</span></span> | <span data-ttu-id="6dbb4-2648">活動</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2648">Activities</span></span> |
| --- | --- |
| <span data-ttu-id="6dbb4-2649">[隨選 HDInsight 叢集](#on-demand-azure-hdinsight-cluster)或[您自己的 HDInsight 叢集](#existing-azure-hdinsight-cluster)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2649">[On-demand HDInsight cluster](#on-demand-azure-hdinsight-cluster) or [your own HDInsight cluster](#existing-azure-hdinsight-cluster)</span></span> |<span data-ttu-id="6dbb4-2650">[.NET 自訂活動](#net-custom-activity)、[Hive 活動](#hdinsight-hive-activity)、[Pig 活動](#hdinsight-pig-acitivity、[MapReduce 活動](#hdinsight-mapreduce-activity)、[Hadoop 串流活動](#hdinsight-streaming-activityd)、[Spark 活動](#hdinsight-spark-activity)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2650">[.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity)</span></span> |
| [<span data-ttu-id="6dbb4-2651">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2651">Azure Batch</span></span>](#azure-batch) |[<span data-ttu-id="6dbb4-2652">.NET 自訂活動</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2652">.NET custom activity</span></span>](#net-custom-activity) |
| [<span data-ttu-id="6dbb4-2653">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2653">Azure Machine Learning</span></span>](#azure-machine-learning) | <span data-ttu-id="6dbb4-2654">[Machine Learning 批次執行活動](#machine-learning-batch-execution-activity)、[Machine Learning 更新資源活動](#machine-learning-update-resource-activity)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2654">[Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity)</span></span> |
| [<span data-ttu-id="6dbb4-2655">Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2655">Azure Data Lake Analytics</span></span>](#azure-data-lake-analytics) |[<span data-ttu-id="6dbb4-2656">Data Lake Analytics U-SQL</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2656">Data Lake Analytics U-SQL</span></span>](#data-lake-analytics-u-sql-activity) |
| <span data-ttu-id="6dbb4-2657">[Azure SQL Database](#azure-sql-database-1)、[Azure SQL 資料倉儲](#azure-sql-data-warehouse-1)、[SQL Server](#sql-server-1)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2657">[Azure SQL Database](#azure-sql-database-1), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1)</span></span> |[<span data-ttu-id="6dbb4-2658">預存程序</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2658">Stored Procedure</span></span>](#stored-procedure-activity) |

## <a name="on-demand-azure-hdinsight-cluster"></a><span data-ttu-id="6dbb4-2659">隨選 Azure HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2659">On-demand Azure HDInsight cluster</span></span>
<span data-ttu-id="6dbb4-2660">Azure Data Factory 服務可自動建立以 Windows/Linux 為基礎的隨選 HDInsight 叢集來處理資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2660">The Azure Data Factory service can automatically create a Windows/Linux-based on-demand HDInsight cluster to process data.</span></span> <span data-ttu-id="6dbb4-2661">此叢集會建立在與叢集相關聯的儲存體帳戶 (JSON 中的 linkedServiceName 屬性) 相同的區域中。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2661">The cluster is created in the same region as the storage account (linkedServiceName property in the JSON) associated with the cluster.</span></span> <span data-ttu-id="6dbb4-2662">您可以在此連結服務上執行下列轉換活動：[.NET 自訂活動](#net-custom-activity)、[Hive 活動](#hdinsight-hive-activity)、[Pig 活動](#hdinsight-pig-acitivity、[MapReduce 活動](#hdinsight-mapreduce-activity)、[Hadoop 串流活動](#hdinsight-streaming-activityd)、[Spark 活動](#hdinsight-spark-activity)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2662">You can run the following transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="6dbb4-2663">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2663">Linked service</span></span> 
<span data-ttu-id="6dbb4-2664">下表描述隨選 HDInsight 連結服務的 Azure JSON 定義中所使用的屬性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2664">The following table provides descriptions for the properties used in the Azure JSON definition of an on-demand HDInsight linked service.</span></span>

| <span data-ttu-id="6dbb4-2665">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2665">Property</span></span> | <span data-ttu-id="6dbb4-2666">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2666">Description</span></span> | <span data-ttu-id="6dbb4-2667">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2667">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-2668">類型</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2668">type</span></span> |<span data-ttu-id="6dbb4-2669">type 屬性應設為 **HDInsightOnDemand**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2669">The type property should be set to **HDInsightOnDemand**.</span></span> |<span data-ttu-id="6dbb4-2670">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2670">Yes</span></span> |
| <span data-ttu-id="6dbb4-2671">clusterSize</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2671">clusterSize</span></span> |<span data-ttu-id="6dbb4-2672">叢集中的背景工作/資料節點數。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2672">Number of worker/data nodes in the cluster.</span></span> <span data-ttu-id="6dbb4-2673">HDInsight 叢集會利用您為此屬性指定的 2 個前端節點以及背景工作節點數目來建立。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2673">The HDInsight cluster is created with 2 head nodes along with the number of worker nodes you specify for this property.</span></span> <span data-ttu-id="6dbb4-2674">節點大小為具有 4 個核心的 Standard_D3，因此 4 個背景工作節點的叢集需要 24 個核心 (4\*4 = 16 個核心用於背景工作節點，加上 2\*4 = 8 個核心用於前端節點)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2674">The nodes are of size Standard_D3 that has 4 cores, so a 4 worker node cluster takes 24 cores (4\*4 = 16 cores for worker nodes, plus 2\*4 = 8 cores for head nodes).</span></span> <span data-ttu-id="6dbb4-2675">如需 Standard_D3 層的詳細資料，請參閱[在 HDInsight 中建立 Linux 型 Hadoop 叢集](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2675">See [Create Linux-based Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) for details about the Standard_D3 tier.</span></span> |<span data-ttu-id="6dbb4-2676">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2676">Yes</span></span> |
| <span data-ttu-id="6dbb4-2677">timetolive</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2677">timetolive</span></span> |<span data-ttu-id="6dbb4-2678">隨選 HDInsight 叢集允許的閒置時間。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2678">The allowed idle time for the on-demand HDInsight cluster.</span></span> <span data-ttu-id="6dbb4-2679">指定在活動執行完成後，如果叢集中沒有其他作用中的作業，隨選 HDInsight 叢集要保持運作多久。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2679">Specifies how long the on-demand HDInsight cluster stays alive after completion of an activity run if there are no other active jobs in the cluster.</span></span><br/><br/><span data-ttu-id="6dbb4-2680">例如，如果活動執行花費 6 分鐘，而 timetolive 設為 5 分鐘，叢集會在處理活動執行的 6 分鐘期間之後保持運作 5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2680">For example, if an activity run takes 6 minutes and timetolive is set to 5 minutes, the cluster stays alive for 5 minutes after the 6 minutes of processing the activity run.</span></span> <span data-ttu-id="6dbb4-2681">如果 6 分鐘期間內執行了另一個活動執行，它便會由相同叢集來處理。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2681">If another activity run is executed with the 6 minutes window, it is processed by the same cluster.</span></span><br/><br/><span data-ttu-id="6dbb4-2682">建立隨選 HDInsight 叢集是昂貴的作業 (可能需要一段時間)，因此請視需要使用這項設定，重複使用隨選 HDInsight 叢集以改善 Data Factory 的效能。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2682">Creating an on-demand HDInsight cluster is an expensive operation (could take a while), so use this setting as needed to improve performance of a data factory by reusing an on-demand HDInsight cluster.</span></span><br/><br/><span data-ttu-id="6dbb4-2683">如果您將 timetolive 值設為 0，叢集會在處理活動執行後立即刪除。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2683">If you set timetolive value to 0, the cluster is deleted as soon as the activity run in processed.</span></span> <span data-ttu-id="6dbb4-2684">另一方面，如果您設定較高的值，叢集可能會有不必要的閒置而導致高成本。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2684">On the other hand, if you set a high value, the cluster may stay idle unnecessarily resulting in high costs.</span></span> <span data-ttu-id="6dbb4-2685">因此，請務必根據您的需求設定適當的值。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2685">Therefore, it is important that you set the appropriate value based on your needs.</span></span><br/><br/><span data-ttu-id="6dbb4-2686">如果適當地設定 timetolive 屬性值，則多個管線可以共用相同的隨選 HDInsight 叢集執行個體</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2686">Multiple pipelines can share the same instance of the on-demand HDInsight cluster if the timetolive property value is appropriately set</span></span> |<span data-ttu-id="6dbb4-2687">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2687">Yes</span></span> |
| <span data-ttu-id="6dbb4-2688">版本</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2688">version</span></span> |<span data-ttu-id="6dbb4-2689">HDInsight 叢集的版本。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2689">Version of the HDInsight cluster.</span></span> <span data-ttu-id="6dbb4-2690">如需詳細資訊，請參閱 [Azure Data Factory 中支援的 HDInsight 版本](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2690">For details, see [supported HDInsight versions in Azure Data Factory](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> |<span data-ttu-id="6dbb4-2691">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2691">No</span></span> |
| <span data-ttu-id="6dbb4-2692">預設容器</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2692">linkedServiceName</span></span> |<span data-ttu-id="6dbb4-2693">隨選叢集用於儲存及處理資料的 Azure 儲存體連結服務。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2693">Azure Storage linked service to be used by the on-demand cluster for storing and processing data.</span></span> <p><span data-ttu-id="6dbb4-2694">目前，您無法建立使用 Azure Data Lake Store 做為儲存體的隨選 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2694">Currently, you cannot create an on-demand HDInsight cluster that uses an Azure Data Lake Store as the storage.</span></span> <span data-ttu-id="6dbb4-2695">如果您想要在 Azure Data Lake Store 中儲存 HDInsight 處理的結果資料，可使用複製活動將 Azure Blob 儲存體的資料複製到 Azure Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2695">If you want to store the result data from HDInsight processing in an Azure Data Lake Store, use a Copy Activity to copy the data from the Azure Blob Storage to the Azure Data Lake Store.</span></span></p>  | <span data-ttu-id="6dbb4-2696">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2696">Yes</span></span> |
| <span data-ttu-id="6dbb4-2697">additionalLinkedServiceNames</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2697">additionalLinkedServiceNames</span></span> |<span data-ttu-id="6dbb4-2698">指定 HDInsight 連結服務的其他儲存體帳戶，讓 Data Factory 服務代表您註冊它們。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2698">Specifies additional storage accounts for the HDInsight linked service so that the Data Factory service can register them on your behalf.</span></span> |<span data-ttu-id="6dbb4-2699">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2699">No</span></span> |
| <span data-ttu-id="6dbb4-2700">osType</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2700">osType</span></span> |<span data-ttu-id="6dbb4-2701">作業系統的類型。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2701">Type of operating system.</span></span> <span data-ttu-id="6dbb4-2702">允許的值為：Windows (預設值) 和 linux</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2702">Allowed values are: Windows (default) and Linux</span></span> |<span data-ttu-id="6dbb4-2703">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2703">No</span></span> |
| <span data-ttu-id="6dbb4-2704">hcatalogLinkedServiceName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2704">hcatalogLinkedServiceName</span></span> |<span data-ttu-id="6dbb4-2705">指向 HCatalog 資料庫的 Azure SQL 連結服務名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2705">The name of Azure SQL linked service that point to the HCatalog database.</span></span> <span data-ttu-id="6dbb4-2706">會使用 Azure SQL 資料庫作為中繼存放區，建立隨選 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2706">The on-demand HDInsight cluster is created by using the Azure SQL database as the metastore.</span></span> |<span data-ttu-id="6dbb4-2707">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2707">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="6dbb4-2708">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2708">JSON example</span></span>
<span data-ttu-id="6dbb4-2709">下列 JSON 會定義以 Linux 為基礎的隨選 HDInsight 連結服務。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2709">The following JSON defines a Linux-based on-demand HDInsight linked service.</span></span> <span data-ttu-id="6dbb4-2710">Data Factory 服務會在處理資料配量時自動建立 **以 Linux 為基礎的** HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2710">The Data Factory service automatically creates a **Linux-based** HDInsight cluster when processing a data slice.</span></span> 

```json
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "StorageLinkedService"
        }
    }
}
```

<span data-ttu-id="6dbb4-2711">如需詳細資訊，請參閱[計算連結服務](data-factory-compute-linked-services.md)一文。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2711">For more information, see [Compute linked services](data-factory-compute-linked-services.md) article.</span></span> 

## <a name="existing-azure-hdinsight-cluster"></a><span data-ttu-id="6dbb4-2712">現有的 Azure HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2712">Existing Azure HDInsight cluster</span></span>
<span data-ttu-id="6dbb4-2713">您可以建立 Azure HDInsight 連結服務，以向 Data Factory 註冊自己的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2713">You can create an Azure HDInsight linked service to register your own HDInsight cluster with Data Factory.</span></span> <span data-ttu-id="6dbb4-2714">您可以在此連結服務上執行下列資料轉換活動︰[.NET 自訂活動](#net-custom-activity)、[Hive 活動](#hdinsight-hive-activity)、[Pig 活動](#hdinsight-pig-activity、[MapReduce 活動](#hdinsight-mapreduce-activity)、[Hadoop 串流活動](#hdinsight-streaming-activityd)、[Spark 活動](#hdinsight-spark-activity)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2714">You can run the following data transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="6dbb4-2715">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2715">Linked service</span></span>
<span data-ttu-id="6dbb4-2716">下表描述 Azure HDInsight 連結服務的 Azure JSON 定義中所使用的屬性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2716">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure HDInsight linked service.</span></span>

| <span data-ttu-id="6dbb4-2717">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2717">Property</span></span> | <span data-ttu-id="6dbb4-2718">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2718">Description</span></span> | <span data-ttu-id="6dbb4-2719">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2719">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-2720">類型</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2720">type</span></span> |<span data-ttu-id="6dbb4-2721">type 屬性應設為 **HDInsight**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2721">The type property should be set to **HDInsight**.</span></span> |<span data-ttu-id="6dbb4-2722">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2722">Yes</span></span> |
| <span data-ttu-id="6dbb4-2723">clusterUri</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2723">clusterUri</span></span> |<span data-ttu-id="6dbb4-2724">HDInsight 叢集的 URI。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2724">The URI of the HDInsight cluster.</span></span> |<span data-ttu-id="6dbb4-2725">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2725">Yes</span></span> |
| <span data-ttu-id="6dbb4-2726">username</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2726">username</span></span> |<span data-ttu-id="6dbb4-2727">指定要用來連接到現有 HDInsight 叢集的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2727">Specify the name of the user to be used to connect to an existing HDInsight cluster.</span></span> |<span data-ttu-id="6dbb4-2728">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2728">Yes</span></span> |
| <span data-ttu-id="6dbb4-2729">password</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2729">password</span></span> |<span data-ttu-id="6dbb4-2730">指定使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2730">Specify password for the user account.</span></span> |<span data-ttu-id="6dbb4-2731">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2731">Yes</span></span> |
| <span data-ttu-id="6dbb4-2732">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2732">linkedServiceName</span></span> | <span data-ttu-id="6dbb4-2733">參照 HDInsight 叢集所使用 Azure Blob 儲存體的 Azure 儲存體連結服務名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2733">Name of the Azure Storage linked service that refers to the Azure blob storage used by the HDInsight cluster.</span></span> <p><span data-ttu-id="6dbb4-2734">目前，您無法針對此屬性指定 Azure Data Lake Store 連結服務。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2734">Currently, you cannot specify an Azure Data Lake Store linked service for this property.</span></span> <span data-ttu-id="6dbb4-2735">如果 HDInsight 叢集可存取 Data Lake Store，您可以透過 Hive/Pig 指令碼存取 Azure Data Lake Store 中的資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2735">You may access data in the Azure Data Lake Store from Hive/Pig scripts if the HDInsight cluster has access to the Data Lake Store.</span></span> </p>  |<span data-ttu-id="6dbb4-2736">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2736">Yes</span></span> |

<span data-ttu-id="6dbb4-2737">如需支援的 HDInsight 叢集版本，請參閱[支援的 HDInsight 版本](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2737">For versions of HDInsight clusters supported, see [supported HDInsight versions](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> 

#### <a name="json-example"></a><span data-ttu-id="6dbb4-2738">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2738">JSON example</span></span>

```json
{
    "name": "HDInsightLinkedService",
    "properties": {
        "type": "HDInsight",
        "typeProperties": {
            "clusterUri": " https://<hdinsightclustername>.azurehdinsight.net/",
            "userName": "admin",
            "password": "<password>",
            "linkedServiceName": "MyHDInsightStoragelinkedService"
        }
    }
}
```

## <a name="azure-batch"></a><span data-ttu-id="6dbb4-2739">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2739">Azure Batch</span></span>
<span data-ttu-id="6dbb4-2740">您可以建立 Azure Batch 連結服務，以向資料處理站註冊虛擬機器 (VM) 的 Batch 集區。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2740">You can create an Azure Batch linked service to register a Batch pool of virtual machines (VMs) with a data factory.</span></span> <span data-ttu-id="6dbb4-2741">您可以使用 Azure Batch 或 Azure HDInsight 執行 .NET 自訂活動。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2741">You can run .NET custom activities using either Azure Batch or Azure HDInsight.</span></span> <span data-ttu-id="6dbb4-2742">您可以在此連結服務上執行 [.NET 自訂活動](#net-custom-activity)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2742">You can run a [.NET custom activity](#net-custom-activity) on this linked service.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="6dbb4-2743">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2743">Linked service</span></span>
<span data-ttu-id="6dbb4-2744">下表描述 Azure Batch 連結服務的 Azure JSON 定義中所使用的屬性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2744">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure Batch linked service.</span></span>

| <span data-ttu-id="6dbb4-2745">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2745">Property</span></span> | <span data-ttu-id="6dbb4-2746">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2746">Description</span></span> | <span data-ttu-id="6dbb4-2747">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2747">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-2748">類型</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2748">type</span></span> |<span data-ttu-id="6dbb4-2749">type 屬性應設為 **AzureBatch**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2749">The type property should be set to **AzureBatch**.</span></span> |<span data-ttu-id="6dbb4-2750">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2750">Yes</span></span> |
| <span data-ttu-id="6dbb4-2751">accountName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2751">accountName</span></span> |<span data-ttu-id="6dbb4-2752">建立 Azure Batch 帳戶。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2752">Name of the Azure Batch account.</span></span> |<span data-ttu-id="6dbb4-2753">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2753">Yes</span></span> |
| <span data-ttu-id="6dbb4-2754">accessKey</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2754">accessKey</span></span> |<span data-ttu-id="6dbb4-2755">Azure Batch 帳戶的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2755">Access key for the Azure Batch account.</span></span> |<span data-ttu-id="6dbb4-2756">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2756">Yes</span></span> |
| <span data-ttu-id="6dbb4-2757">poolName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2757">poolName</span></span> |<span data-ttu-id="6dbb4-2758">虛擬機器的集區名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2758">Name of the pool of virtual machines.</span></span> |<span data-ttu-id="6dbb4-2759">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2759">Yes</span></span> |
| <span data-ttu-id="6dbb4-2760">預設容器</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2760">linkedServiceName</span></span> |<span data-ttu-id="6dbb4-2761">與此 Azure Batch 連結服務相關聯的 Azure 儲存體服務連結名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2761">Name of the Azure Storage linked service associated with this Azure Batch linked service.</span></span> <span data-ttu-id="6dbb4-2762">此連結服務用於執行活動及儲存活動執行記錄檔所需的暫存檔案。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2762">This linked service is used for staging files required to run the activity and storing the activity execution logs.</span></span> |<span data-ttu-id="6dbb4-2763">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2763">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="6dbb4-2764">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2764">JSON example</span></span>

```json
{
    "name": "AzureBatchLinkedService",
    "properties": {
        "type": "AzureBatch",
        "typeProperties": {
            "accountName": "<Azure Batch account name>",
            "accessKey": "<Azure Batch account key>",
            "poolName": "<Azure Batch pool name>",
            "linkedServiceName": "<Specify associated storage linked service reference here>"
        }
    }
}
```

## <a name="azure-machine-learning"></a><span data-ttu-id="6dbb4-2765">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2765">Azure Machine Learning</span></span>
<span data-ttu-id="6dbb4-2766">您可建立 Azure Machine Learning 連結服務，以向資料處理站註冊 Machine Learning 批次評分端點。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2766">You create an Azure Machine Learning linked service to register a Machine Learning batch scoring endpoint with a data factory.</span></span> <span data-ttu-id="6dbb4-2767">您可以在此連結服務上執行兩個資料轉換活動︰[Machine Learning 批次執行活動](#machine-learning-batch-execution-activity)、[Machine Learning 更新資源活動](#machine-learning-update-resource-activity)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2767">Two data transformation activities that can run on this linked service: [Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="6dbb4-2768">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2768">Linked service</span></span>
<span data-ttu-id="6dbb4-2769">下表描述 Azure Machine Learning 連結服務的 Azure JSON 定義中所使用的屬性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2769">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure Machine Learning linked service.</span></span>

| <span data-ttu-id="6dbb4-2770">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2770">Property</span></span> | <span data-ttu-id="6dbb4-2771">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2771">Description</span></span> | <span data-ttu-id="6dbb4-2772">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2772">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-2773">類型</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2773">Type</span></span> |<span data-ttu-id="6dbb4-2774">type 屬性應設為： **AzureML**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2774">The type property should be set to: **AzureML**.</span></span> |<span data-ttu-id="6dbb4-2775">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2775">Yes</span></span> |
| <span data-ttu-id="6dbb4-2776">mlEndpoint</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2776">mlEndpoint</span></span> |<span data-ttu-id="6dbb4-2777">批次評分 URL。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2777">The batch scoring URL.</span></span> |<span data-ttu-id="6dbb4-2778">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2778">Yes</span></span> |
| <span data-ttu-id="6dbb4-2779">apiKey</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2779">apiKey</span></span> |<span data-ttu-id="6dbb4-2780">已發佈的工作區模型的 API。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2780">The published workspace model’s API.</span></span> |<span data-ttu-id="6dbb4-2781">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2781">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="6dbb4-2782">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2782">JSON example</span></span>

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://[batch scoring endpoint]/jobs",
            "apiKey": "<apikey>"
        }
    }
}
```

## <a name="azure-data-lake-analytics"></a><span data-ttu-id="6dbb4-2783">Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2783">Azure Data Lake Analytics</span></span>
<span data-ttu-id="6dbb4-2784">您應建立 **Azure Data Lake Analytics** 連結服務，將 Azure Data Lake Analytics 計算服務連結至 Azure Data Factory，然後再使用管線中的 [Data Lake Analytics U-SQL 活動](data-factory-usql-activity.md) 。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2784">You create an **Azure Data Lake Analytics** linked service to link an Azure Data Lake Analytics compute service to an Azure data factory before using the [Data Lake Analytics U-SQL activity](data-factory-usql-activity.md) in a pipeline.</span></span>

### <a name="linked-service"></a><span data-ttu-id="6dbb4-2785">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2785">Linked service</span></span>

<span data-ttu-id="6dbb4-2786">下表描述 Azure Data Lake Analytics 連結服務的 JSON 定義中所使用的屬性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2786">The following table provides descriptions for the properties used in the JSON definition of an Azure Data Lake Analytics linked service.</span></span> 

| <span data-ttu-id="6dbb4-2787">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2787">Property</span></span> | <span data-ttu-id="6dbb4-2788">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2788">Description</span></span> | <span data-ttu-id="6dbb4-2789">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2789">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-2790">類型</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2790">Type</span></span> |<span data-ttu-id="6dbb4-2791">type 屬性應設為： **AzureDataLakeAnalytics**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2791">The type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="6dbb4-2792">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2792">Yes</span></span> |
| <span data-ttu-id="6dbb4-2793">accountName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2793">accountName</span></span> |<span data-ttu-id="6dbb4-2794">Azure Data Lake Analytics 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2794">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="6dbb4-2795">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2795">Yes</span></span> |
| <span data-ttu-id="6dbb4-2796">dataLakeAnalyticsUri</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2796">dataLakeAnalyticsUri</span></span> |<span data-ttu-id="6dbb4-2797">Azure Data Lake Analytics URI。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2797">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="6dbb4-2798">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2798">No</span></span> |
| <span data-ttu-id="6dbb4-2799">授權</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2799">authorization</span></span> |<span data-ttu-id="6dbb4-2800">按一下 Data Factory 編輯器中的 [授權]  按鈕並完成 OAuth 登入後，即會自動擷取授權碼。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2800">Authorization code is automatically retrieved after clicking **Authorize** button in the Data Factory Editor and completing the OAuth login.</span></span> |<span data-ttu-id="6dbb4-2801">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2801">Yes</span></span> |
| <span data-ttu-id="6dbb4-2802">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2802">subscriptionId</span></span> |<span data-ttu-id="6dbb4-2803">Azure 訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2803">Azure subscription id</span></span> |<span data-ttu-id="6dbb4-2804">否 (如果未指定，便會使用 Data Factory 的訂用帳戶)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2804">No (If not specified, subscription of the data factory is used).</span></span> |
| <span data-ttu-id="6dbb4-2805">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2805">resourceGroupName</span></span> |<span data-ttu-id="6dbb4-2806">Azure 資源群組名稱</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2806">Azure resource group name</span></span> |<span data-ttu-id="6dbb4-2807">否 (若未指定，便會使用 Data Factory 的資源群組)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2807">No (If not specified, resource group of the data factory is used).</span></span> |
| <span data-ttu-id="6dbb4-2808">sessionId</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2808">sessionId</span></span> |<span data-ttu-id="6dbb4-2809">OAuth 授權工作階段的工作階段識別碼。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2809">session id from the OAuth authorization session.</span></span> <span data-ttu-id="6dbb4-2810">每個工作階段識別碼都是唯一的，只能使用一次。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2810">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="6dbb4-2811">使用 Data Factory 編輯器時會自動產生此識別碼。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2811">When you use the Data Factory Editor, this ID is auto-generated.</span></span> |<span data-ttu-id="6dbb4-2812">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2812">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="6dbb4-2813">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2813">JSON example</span></span>
<span data-ttu-id="6dbb4-2814">下列範例提供 Azure Data Lake Analytics 連結服務的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2814">The following example provides JSON definition for an Azure Data Lake Analytics linked service.</span></span>

```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "<account name>",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>",
            "subscriptionId": "<subscription id>",
            "resourceGroupName": "<resource group name>"
        }
    }
}
```

## <a name="azure-sql-database"></a><span data-ttu-id="6dbb4-2815">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2815">Azure SQL Database</span></span>
<span data-ttu-id="6dbb4-2816">您可建立 Azure SQL 連結服務，並將其與 [預存程序活動](#stored-procedure-activity) 搭配使用，以叫用 Data Factory 管線中的預存程序。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2816">You create an Azure SQL linked service and use it with the [Stored Procedure Activity](#stored-procedure-activity) to invoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="6dbb4-2817">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2817">Linked service</span></span>
<span data-ttu-id="6dbb4-2818">若要定義 Azure SQL Database 連結服務，請將連結服務的 **type** 設為 **AzureSqlDatabase**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2818">To define an Azure SQL Database linked service, set the **type** of the linked service to **AzureSqlDatabase**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="6dbb4-2819">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2819">Property</span></span> | <span data-ttu-id="6dbb4-2820">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2820">Description</span></span> | <span data-ttu-id="6dbb4-2821">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2821">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-2822">connectionString</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2822">connectionString</span></span> |<span data-ttu-id="6dbb4-2823">針對 connectionString 屬性指定連接到 Azure SQL Database 執行個體所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2823">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span></span> |<span data-ttu-id="6dbb4-2824">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2824">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="6dbb4-2825">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2825">JSON example</span></span>

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="6dbb4-2826">如需此連結服務的詳細資料，請參閱 [Azure SQL 連接器](data-factory-azure-sql-connector.md#linked-service-properties) 一文。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2826">See [Azure SQL Connector](data-factory-azure-sql-connector.md#linked-service-properties) article for details about this linked service.</span></span>

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="6dbb4-2827">Azure SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2827">Azure SQL Data Warehouse</span></span>
<span data-ttu-id="6dbb4-2828">您可以建立 Azure SQL 資料倉儲連結服務，並將其與 [預存程序活動](data-factory-stored-proc-activity.md) 搭配使用，以叫用 Data Factory 管線中的預存程序。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2828">You create an Azure SQL Data Warehouse linked service and use it with the [Stored Procedure Activity](data-factory-stored-proc-activity.md) to invoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="6dbb4-2829">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2829">Linked service</span></span>
<span data-ttu-id="6dbb4-2830">若要定義 Azure SQL 資料倉儲連結服務，請將連結服務的 **type** 設為 **AzureSqlDW**，並在 **typeProperties** 區段中指定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2830">To define an Azure SQL Data Warehouse linked service, set the **type** of the linked service to **AzureSqlDW**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="6dbb4-2831">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2831">Property</span></span> | <span data-ttu-id="6dbb4-2832">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2832">Description</span></span> | <span data-ttu-id="6dbb4-2833">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2833">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-2834">connectionString</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2834">connectionString</span></span> |<span data-ttu-id="6dbb4-2835">針對 connectionString 屬性指定連線到 Azure SQL 資料倉儲執行個體所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2835">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span></span> |<span data-ttu-id="6dbb4-2836">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2836">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="6dbb4-2837">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2837">JSON example</span></span>

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="6dbb4-2838">如需詳細資訊，請參閱 [Azure SQL 資料倉儲連接器](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2838">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

## <a name="sql-server"></a><span data-ttu-id="6dbb4-2839">SQL Server</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2839">SQL Server</span></span> 
<span data-ttu-id="6dbb4-2840">您可以建立 SQL Server 連結服務，並將其與 [預存程序活動](data-factory-stored-proc-activity.md) 搭配使用，以叫用 Data Factory 管線中的預存程序。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2840">You create a SQL Server linked service and use it with the [Stored Procedure Activity](data-factory-stored-proc-activity.md) to invoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="6dbb4-2841">連結服務</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2841">Linked service</span></span>
<span data-ttu-id="6dbb4-2842">您可以建立 **OnPremisesSqlServer** 類型的連結服務，以將內部部署 SQL Server 資料庫連結至資料處理站。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2842">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span></span> <span data-ttu-id="6dbb4-2843">下表提供內部部署 SQL Server 連結服務專屬 JSON 元素的描述。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2843">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span></span>

<span data-ttu-id="6dbb4-2844">下表提供 SQL Server 連結服務專屬 JSON 元素的描述。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2844">The following table provides description for JSON elements specific to SQL Server linked service.</span></span>

| <span data-ttu-id="6dbb4-2845">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2845">Property</span></span> | <span data-ttu-id="6dbb4-2846">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2846">Description</span></span> | <span data-ttu-id="6dbb4-2847">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2847">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-2848">類型</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2848">type</span></span> |<span data-ttu-id="6dbb4-2849">類型屬性應設為： **OnPremisesSqlServer**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2849">The type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="6dbb4-2850">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2850">Yes</span></span> |
| <span data-ttu-id="6dbb4-2851">connectionString</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2851">connectionString</span></span> |<span data-ttu-id="6dbb4-2852">指定使用 SQL 驗證或 Windows 驗證連接至內部部署 SQL Server 資料庫所需的 connectionString 資訊。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2852">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="6dbb4-2853">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2853">Yes</span></span> |
| <span data-ttu-id="6dbb4-2854">gatewayName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2854">gatewayName</span></span> |<span data-ttu-id="6dbb4-2855">Data Factory 服務應該用來連接到內部部署 SQL Server 資料庫的閘道器名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2855">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span></span> |<span data-ttu-id="6dbb4-2856">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2856">Yes</span></span> |
| <span data-ttu-id="6dbb4-2857">username</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2857">username</span></span> |<span data-ttu-id="6dbb4-2858">如果您使用「Windows 驗證」，請指定使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2858">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="6dbb4-2859">範例︰**domainname\\username**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2859">Example: **domainname\\username**.</span></span> |<span data-ttu-id="6dbb4-2860">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2860">No</span></span> |
| <span data-ttu-id="6dbb4-2861">password</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2861">password</span></span> |<span data-ttu-id="6dbb4-2862">指定您為使用者名稱所指定之使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2862">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="6dbb4-2863">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2863">No</span></span> |

<span data-ttu-id="6dbb4-2864">您可以使用 **New-AzureRmDataFactoryEncryptValue** Cmdlet 加密認證，並在連接字串中使用這些認證，如下列範例所示 (**EncryptedCredential** 屬性)：</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2864">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="6dbb4-2865">範例：用於 SQL 驗證的 JSON</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2865">Example: JSON for using SQL Authentication</span></span>

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="6dbb4-2866">範例：用於 Windows 驗證的 JSON</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2866">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="6dbb4-2867">如果已指定使用者名稱和密碼，閘道就會使用它們來模擬指定的使用者帳戶，以連線到內部部署 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2867">If username and password are specified, gateway uses them to impersonate the specified user account to connect to the on-premises SQL Server database.</span></span> <span data-ttu-id="6dbb4-2868">否則，閘道會使用閘道的安全性內容 (其啟動帳戶) 直接連線到 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2868">Otherwise, gateway connects to the SQL Server directly with the security context of Gateway (its startup account).</span></span>

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="6dbb4-2869">如需詳細資訊，請參閱 [SQL Server 連接器](data-factory-sqlserver-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2869">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span>

## <a name="data-transformation-activities"></a><span data-ttu-id="6dbb4-2870">資料轉換活動</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2870">DATA TRANSFORMATION ACTIVITIES</span></span>

<span data-ttu-id="6dbb4-2871">活動</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2871">Activity</span></span> | <span data-ttu-id="6dbb4-2872">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2872">Description</span></span>
-------- | -----------
[<span data-ttu-id="6dbb4-2873">HDInsight Hive 活動</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2873">HDInsight Hive activity</span></span>](#hdinsight-hive-activity) | <span data-ttu-id="6dbb4-2874">Data Factory 管線中的 HDInsight Hive 活動會在您自己或隨選的 Windows/Linux 架構 HDInsight 叢集上執行 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2874">The HDInsight Hive activity in a Data Factory pipeline executes Hive queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span> 
[<span data-ttu-id="6dbb4-2875">HDInsight Pig 活動</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2875">HDInsight Pig activity</span></span>](#hdinsight-pig-activity) | <span data-ttu-id="6dbb4-2876">Data Factory 管線中的 HDInsight Pig 活動會在您自己或隨選的 Windows/Linux 架構 HDInsight 叢集上執行 Pig 查詢。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2876">The HDInsight Pig activity in a Data Factory pipeline executes Pig queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="6dbb4-2877">HDInsight MapReduce 活動</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2877">HDInsight MapReduce Activity</span></span>](#hdinsight-mapreduce-activity) | <span data-ttu-id="6dbb4-2878">Data Factory 管線中的 HDInsight MapReduce 活動會在您自己或隨選的 Windows/Linux 架構 HDInsight 叢集上執行 MapReduce 程式。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2878">The HDInsight MapReduce activity in a Data Factory pipeline executes MapReduce programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="6dbb4-2879">HDInsight 串流活動</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2879">HDInsight Streaming Activity</span></span>](#hdinsight-streaming-activity) | <span data-ttu-id="6dbb4-2880">Data Factory 管線中的 HDInsight 串流活動會在您自己或隨選的 Windows/Linux 架構 HDInsight 叢集上執行 Hadoop 串流程式。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2880">The HDInsight Streaming Activity in a Data Factory pipeline executes Hadoop Streaming programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="6dbb4-2881">HDInsight Spark 活動</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2881">HDInsight Spark Activity</span></span>](#hdinsight-spark-activity) | <span data-ttu-id="6dbb4-2882">Data Factory 管線中的 HDInsight Spark 活動會在您自己的 HDInsight 叢集上執行 Spark 程式。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2882">The HDInsight Spark activity in a Data Factory pipeline executes Spark programs on your own HDInsight cluster.</span></span> 
[<span data-ttu-id="6dbb4-2883">Machine Learning Batch 執行活動</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2883">Machine Learning Batch Execution Activity</span></span>](#machine-learning-batch-execution-activity) | <span data-ttu-id="6dbb4-2884">Azure Data Factory 可讓您輕鬆地建立管線，使用已發佈的 Azure Machine Learning Web 服務進行預測性分析。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2884">Azure Data Factory enables you to easily create pipelines that use a published Azure Machine Learning web service for predictive analytics.</span></span> <span data-ttu-id="6dbb4-2885">在 Azure Data Factory 管線中使用批次執行活動，您可以叫用 Machine Learning Web 服務來對批次中的資料進行預測。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2885">Using the Batch Execution Activity in an Azure Data Factory pipeline, you can invoke a Machine Learning web service to make predictions on the data in batch.</span></span> 
[<span data-ttu-id="6dbb4-2886">Machine Learning 更新資源活動</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2886">Machine Learning Update Resource Activity</span></span>](#machine-learning-update-resource-activity) | <span data-ttu-id="6dbb4-2887">經過一段時間，必須使用新的輸入資料集重新訓練 Machine Learning 評分實驗中的預測模型。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2887">Over time, the predictive models in the Machine Learning scoring experiments need to be retrained using new input datasets.</span></span> <span data-ttu-id="6dbb4-2888">完成重新訓練之後，您想要使用已重新訓練的 Machine Learning 模型來更新評分 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2888">After you are done with retraining, you want to update the scoring web service with the retrained Machine Learning model.</span></span> <span data-ttu-id="6dbb4-2889">您可以使用更新資源活動，以新訓練的模型更新 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2889">You can use the Update Resource Activity to update the web service with the newly trained model.</span></span>
[<span data-ttu-id="6dbb4-2890">預存程序活動</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2890">Stored Procedure Activity</span></span>](#stored-procedure-activity) | <span data-ttu-id="6dbb4-2891">您可以在 Data Factory 管線中使用預存程序活動，以叫用下列其中一個資料存放區中的預存程序：您的企業或 Azure VM 中的 Azure SQL Database、Azure SQL 資料倉儲、SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2891">You can use the Stored Procedure activity in a Data Factory pipeline to invoke a stored procedure in one of the following data stores: Azure SQL Database, Azure SQL Data Warehouse, SQL Server Database in your enterprise or an Azure VM.</span></span> 
[<span data-ttu-id="6dbb4-2892">Data Lake Analytics U-SQL 活動</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2892">Data Lake Analytics U-SQL activity</span></span>](#data-lake-analytics-u-sql-activity) | <span data-ttu-id="6dbb4-2893">Data Lake Analytics U-SQL 活動會在 Azure Data Lake Analytics 叢集上執行 U-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2893">Data Lake Analytics U-SQL Activity runs a U-SQL script on an Azure Data Lake Analytics cluster.</span></span>  
[<span data-ttu-id="6dbb4-2894">.NET 自訂活動</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2894">.NET custom activity</span></span>](#net-custom-activity) | <span data-ttu-id="6dbb4-2895">如果您需要以 Data Factory 不支援的方法轉換資料，可以利用自己的資料處理邏輯建立自訂活動，然後在管線中使用活動。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2895">If you need to transform data in a way that is not supported by Data Factory, you can create a custom activity with your own data processing logic and use the activity in the pipeline.</span></span> <span data-ttu-id="6dbb4-2896">您可以將自訂 .NET 活動設定為使用 Azure Batch 服務或 Azure HDInsight 叢集來執行。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2896">You can configure the custom .NET activity to run using either an Azure Batch service or an Azure HDInsight cluster.</span></span> 

     
## <a name="hdinsight-hive-activity"></a><span data-ttu-id="6dbb4-2897">HDInsight Hive 活動</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2897">HDInsight Hive Activity</span></span>
<span data-ttu-id="6dbb4-2898">您可以在 Hive 活動 JSON 定義中指定下列屬性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2898">You can specify the following properties in a Hive Activity JSON definition.</span></span> <span data-ttu-id="6dbb4-2899">活動的 type 屬性必須是︰**HDInsightHive**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2899">The type property for the activity must be: **HDInsightHive**.</span></span> <span data-ttu-id="6dbb4-2900">您必須先建立 HDInsight 連結服務，再指定它的名稱作為 **linkedServiceName** 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2900">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="6dbb4-2901">當您將活動類型設為 HDInsightHive 時，**typeProperties** 區段中支援下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2901">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightHive:</span></span>

| <span data-ttu-id="6dbb4-2902">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2902">Property</span></span> | <span data-ttu-id="6dbb4-2903">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2903">Description</span></span> | <span data-ttu-id="6dbb4-2904">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2904">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-2905">script</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2905">script</span></span> |<span data-ttu-id="6dbb4-2906">指定 Hive 指令碼內嵌</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2906">Specify the Hive script inline</span></span> |<span data-ttu-id="6dbb4-2907">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2907">No</span></span> |
| <span data-ttu-id="6dbb4-2908">指令碼路徑</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2908">script path</span></span> |<span data-ttu-id="6dbb4-2909">在 Azure Blob 儲存體中儲存 Hive 指令碼，並提供檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2909">Store the Hive script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="6dbb4-2910">使用 'script' 或 'scriptPath' 屬性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2910">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="6dbb4-2911">兩者無法同時使用。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2911">Both cannot be used together.</span></span> <span data-ttu-id="6dbb4-2912">檔案名稱有區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2912">The file name is case-sensitive.</span></span> |<span data-ttu-id="6dbb4-2913">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2913">No</span></span> |
| <span data-ttu-id="6dbb4-2914">定義</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2914">defines</span></span> |<span data-ttu-id="6dbb4-2915">在使用 'hiveconf' 的 Hive 指令碼內指定參數做為參考的金鑰/值組</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2915">Specify parameters as key/value pairs for referencing within the Hive script using 'hiveconf'</span></span> |<span data-ttu-id="6dbb4-2916">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2916">No</span></span> |

<span data-ttu-id="6dbb4-2917">只有 Hive 活動才有這些類型屬性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2917">These type properties are specific to the Hive Activity.</span></span> <span data-ttu-id="6dbb4-2918">其他屬性 (在 typeProperties 區段外) 在所有活動中都支援。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2918">Other properties (outside the typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="6dbb4-2919">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2919">JSON example</span></span>
<span data-ttu-id="6dbb4-2920">下列 JSON 定義管線中的 HDInsight Hive 活動。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2920">The following JSON defines a HDInsight Hive activity in a pipeline.</span></span>  

```json
{
    "name": "Hive Activity",
    "description": "description",
    "type": "HDInsightHive",
    "inputs": [
      {
        "name": "input tables"
      }
    ],
    "outputs": [
      {
        "name": "output tables"
      }
    ],
    "linkedServiceName": "MyHDInsightLinkedService",
    "typeProperties": {
      "script": "Hive script",
      "scriptPath": "<pathtotheHivescriptfileinAzureblobstorage>",
      "defines": {
        "param1": "param1Value"
      }
    },
   "scheduler": {
      "frequency": "Day",
      "interval": 1
    }
}
```

<span data-ttu-id="6dbb4-2921">如需詳細資訊，請參閱 [Hive 活動](data-factory-hive-activity.md)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2921">For more information, see [Hive Activity](data-factory-hive-activity.md) article.</span></span> 

## <a name="hdinsight-pig-activity"></a><span data-ttu-id="6dbb4-2922">HDInsight Pig 活動</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2922">HDInsight Pig Activity</span></span>
<span data-ttu-id="6dbb4-2923">您可以在 Pig 活動 JSON 定義中指定下列屬性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2923">You can specify the following properties in a Pig Activity JSON definition.</span></span> <span data-ttu-id="6dbb4-2924">活動的 type 屬性必須是︰**HDInsightPig**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2924">The type property for the activity must be: **HDInsightPig**.</span></span> <span data-ttu-id="6dbb4-2925">您必須先建立 HDInsight 連結服務，再指定它的名稱作為 **linkedServiceName** 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2925">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="6dbb4-2926">當您將活動類型設為 HDInsightPig 時，**typeProperties** 區段中支援下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2926">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightPig:</span></span> 

| <span data-ttu-id="6dbb4-2927">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2927">Property</span></span> | <span data-ttu-id="6dbb4-2928">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2928">Description</span></span> | <span data-ttu-id="6dbb4-2929">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2929">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-2930">script</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2930">script</span></span> |<span data-ttu-id="6dbb4-2931">指定 Pig 指令碼內嵌</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2931">Specify the Pig script inline</span></span> |<span data-ttu-id="6dbb4-2932">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2932">No</span></span> |
| <span data-ttu-id="6dbb4-2933">指令碼路徑</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2933">script path</span></span> |<span data-ttu-id="6dbb4-2934">在 Azure blob 儲存體中儲存 Pig 指令碼，並提供檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2934">Store the Pig script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="6dbb4-2935">使用 'script' 或 'scriptPath' 屬性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2935">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="6dbb4-2936">兩者無法同時使用。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2936">Both cannot be used together.</span></span> <span data-ttu-id="6dbb4-2937">檔案名稱有區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2937">The file name is case-sensitive.</span></span> |<span data-ttu-id="6dbb4-2938">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2938">No</span></span> |
| <span data-ttu-id="6dbb4-2939">定義</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2939">defines</span></span> |<span data-ttu-id="6dbb4-2940">在使用 Pig 指令碼內指定參數做為參考的機碼/值組</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2940">Specify parameters as key/value pairs for referencing within the Pig script</span></span> |<span data-ttu-id="6dbb4-2941">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2941">No</span></span> |

<span data-ttu-id="6dbb4-2942">只有 Pig 活動才有這些類型屬性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2942">These type properties are specific to the Pig Activity.</span></span> <span data-ttu-id="6dbb4-2943">其他屬性 (在 typeProperties 區段外) 在所有活動中都支援。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2943">Other properties (outside the typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="6dbb4-2944">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2944">JSON example</span></span>

```json
{
    "name": "HiveActivitySamplePipeline",
      "properties": {
    "activities": [
        {
            "name": "Pig Activity",
            "description": "description",
            "type": "HDInsightPig",
            "inputs": [
                  {
                    "name": "input tables"
                  }
            ],
            "outputs": [
                  {
                    "name": "output tables"
                  }
            ],
            "linkedServiceName": "MyHDInsightLinkedService",
            "typeProperties": {
                  "script": "Pig script",
                  "scriptPath": "<pathtothePigscriptfileinAzureblobstorage>",
                  "defines": {
                    "param1": "param1Value"
                  }
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
    ]
  }
}
```

<span data-ttu-id="6dbb4-2945">如需詳細資訊，請參閱 [Pig 活動](#data-factory-pig-activity.md)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2945">For more information, see [Pig Activity](#data-factory-pig-activity.md) article.</span></span> 

## <a name="hdinsight-mapreduce-activity"></a><span data-ttu-id="6dbb4-2946">HDInsight MapReduce 活動</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2946">HDInsight MapReduce Activity</span></span>
<span data-ttu-id="6dbb4-2947">您可以在 MapReduce 活動 JSON 定義中指定下列屬性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2947">You can specify the following properties in a MapReduce Activity JSON definition.</span></span> <span data-ttu-id="6dbb4-2948">活動的 type 屬性必須是︰**HDInsightMapReduce**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2948">The type property for the activity must be: **HDInsightMapReduce**.</span></span> <span data-ttu-id="6dbb4-2949">您必須先建立 HDInsight 連結服務，再指定它的名稱作為 **linkedServiceName** 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2949">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="6dbb4-2950">當您將活動類型設為 HDInsightMapReduce 時，**typeProperties** 區段中支援下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2950">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightMapReduce:</span></span> 

| <span data-ttu-id="6dbb4-2951">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2951">Property</span></span> | <span data-ttu-id="6dbb4-2952">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2952">Description</span></span> | <span data-ttu-id="6dbb4-2953">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2953">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-2954">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2954">jarLinkedService</span></span> | <span data-ttu-id="6dbb4-2955">含有 JAR 檔案之 Azure 儲存體的連結服務名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2955">Name of the linked service for the Azure Storage that contains the JAR file.</span></span> | <span data-ttu-id="6dbb4-2956">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2956">Yes</span></span> |
| <span data-ttu-id="6dbb4-2957">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2957">jarFilePath</span></span> | <span data-ttu-id="6dbb4-2958">Azure 儲存體中的 JAR 檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2958">Path to the JAR file in the Azure Storage.</span></span> | <span data-ttu-id="6dbb4-2959">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2959">Yes</span></span> | 
| <span data-ttu-id="6dbb4-2960">className</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2960">className</span></span> | <span data-ttu-id="6dbb4-2961">JAR 檔案中的主要類別名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2961">Name of the main class in the JAR file.</span></span> | <span data-ttu-id="6dbb4-2962">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2962">Yes</span></span> | 
| <span data-ttu-id="6dbb4-2963">arguments</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2963">arguments</span></span> | <span data-ttu-id="6dbb4-2964">MapReduce 程式以逗號分隔的引數清單。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2964">A list of comma-separated arguments for the MapReduce program.</span></span> <span data-ttu-id="6dbb4-2965">在執行階段，您會看到幾個來自 MapReduce 架構的額外引數 (例如：mapreduce.job.tags)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2965">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span></span> <span data-ttu-id="6dbb4-2966">若要區分您的引數與 MapReduce 引數，請考慮同時使用選項和值作為引數，如下列範例所示 (-s、--input、--output 等等是後面接著其值的選項)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2966">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | <span data-ttu-id="6dbb4-2967">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2967">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="6dbb4-2968">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2968">JSON example</span></span>

```json
{
    "name": "MahoutMapReduceSamplePipeline",
    "properties": {
        "description": "Sample Pipeline to Run a Mahout Custom Map Reduce Jar. This job calculates an Item Similarity Matrix to determine the similarity between two items",
        "activities": [
            {
                "type": "HDInsightMapReduce",
                "typeProperties": {
                    "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
                    "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
                    "jarLinkedService": "StorageLinkedService",
                    "arguments": ["-s", "SIMILARITY_LOGLIKELIHOOD", "--input", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/input", "--output", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/output/", "--maxSimilaritiesPerItem", "500", "--tempDir", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/temp/mahout"]
                },
                "inputs": [
                    {
                        "name": "MahoutInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "MahoutOutput"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "MahoutActivity",
                "description": "Custom Map Reduce to generate Mahout result",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00",
        "end": "2017-01-04T00:00:00"
    }
}
```

<span data-ttu-id="6dbb4-2969">如需詳細資訊，請參閱 [MapReduce 活動](data-factory-map-reduce.md)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2969">For more information, see [MapReduce Activity](data-factory-map-reduce.md) article.</span></span> 

## <a name="hdinsight-streaming-activity"></a><span data-ttu-id="6dbb4-2970">HDInsight 串流活動</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2970">HDInsight Streaming Activity</span></span>
<span data-ttu-id="6dbb4-2971">您可以在 Hadoop 串流活動 JSON 定義中指定下列屬性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2971">You can specify the following properties in a Hadoop Streaming Activity JSON definition.</span></span> <span data-ttu-id="6dbb4-2972">活動的 type 屬性必須是︰**HDInsightStreaming**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2972">The type property for the activity must be: **HDInsightStreaming**.</span></span> <span data-ttu-id="6dbb4-2973">您必須先建立 HDInsight 連結服務，再指定它的名稱作為 **linkedServiceName** 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2973">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="6dbb4-2974">當您將活動類型設為 HDInsightStreaming 時，**typeProperties** 區段中支援下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2974">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightStreaming:</span></span> 

| <span data-ttu-id="6dbb4-2975">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2975">Property</span></span> | <span data-ttu-id="6dbb4-2976">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2976">Description</span></span> | 
| --- | --- |
| <span data-ttu-id="6dbb4-2977">mapper</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2977">mapper</span></span> | <span data-ttu-id="6dbb4-2978">對應程式可執行檔的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2978">Name of the mapper executable.</span></span> <span data-ttu-id="6dbb4-2979">在範例中，cat.exe 是對應程式可執行檔。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2979">In the example, cat.exe is the mapper executable.</span></span>| 
| <span data-ttu-id="6dbb4-2980">reducer</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2980">reducer</span></span> | <span data-ttu-id="6dbb4-2981">歸納器可執行檔的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2981">Name of the reducer executable.</span></span> <span data-ttu-id="6dbb4-2982">在範例中，cat.exe 是減壓器可執行檔。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2982">In the example, wc.exe is the reducer executable.</span></span> | 
| <span data-ttu-id="6dbb4-2983">input</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2983">input</span></span> | <span data-ttu-id="6dbb4-2984">對應工具的輸入檔 (包括位置)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2984">Input file (including location) for the mapper.</span></span> <span data-ttu-id="6dbb4-2985">在 "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt" 範例中：adfsample 是 blob 容器，example/data/Gutenberg 是資料夾，而 davinci.txt 是 blob。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2985">In the example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is the blob container, example/data/Gutenberg is the folder, and davinci.txt is the blob.</span></span> |
| <span data-ttu-id="6dbb4-2986">output</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2986">output</span></span> | <span data-ttu-id="6dbb4-2987">歸納器的輸出檔 (包括位置)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2987">Output file (including location) for the reducer.</span></span> <span data-ttu-id="6dbb4-2988">Hadoop 串流作業的輸出會寫入針對這個屬性指定的位置。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2988">The output of the Hadoop Streaming job is written to the location specified for this property.</span></span> |
| <span data-ttu-id="6dbb4-2989">filePaths</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2989">filePaths</span></span> | <span data-ttu-id="6dbb4-2990">對應器和歸納器可執行檔的路徑。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2990">Paths for the mapper and reducer executables.</span></span> <span data-ttu-id="6dbb4-2991">在 "adfsample/example/apps/wc.exe" 範例中，adfsample 是 blob 容器，example/apps 是資料夾，而 wc.exe 是可執行檔。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2991">In the example: "adfsample/example/apps/wc.exe", adfsample is the blob container, example/apps is the folder, and wc.exe is the executable.</span></span> | 
| <span data-ttu-id="6dbb4-2992">fileLinkedService</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2992">fileLinkedService</span></span> | <span data-ttu-id="6dbb4-2993">Azure 儲存體連結服務，代表含有 filePaths 區段中指定之檔案的 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2993">Azure Storage linked service that represents the Azure storage that contains the files specified in the filePaths section.</span></span> | 
| <span data-ttu-id="6dbb4-2994">arguments</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2994">arguments</span></span> | <span data-ttu-id="6dbb4-2995">MapReduce 程式以逗號分隔的引數清單。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2995">A list of comma-separated arguments for the MapReduce program.</span></span> <span data-ttu-id="6dbb4-2996">在執行階段，您會看到幾個來自 MapReduce 架構的額外引數 (例如：mapreduce.job.tags)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2996">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span></span> <span data-ttu-id="6dbb4-2997">若要區分您的引數與 MapReduce 引數，請考慮同時使用選項和值作為引數，如下列範例所示 (-s、--input、--output 等等是後面接著其值的選項)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2997">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | 
| <span data-ttu-id="6dbb4-2998">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2998">getDebugInfo</span></span> | <span data-ttu-id="6dbb4-2999">選擇性元素。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-2999">An optional element.</span></span> <span data-ttu-id="6dbb4-3000">該屬性設定為 [失敗] 時，只能在執行失敗時下載記錄檔。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3000">When it is set to Failure, the logs are downloaded only on failure.</span></span> <span data-ttu-id="6dbb4-3001">當其設定為「所有」時，無論執行狀態為何，一律下載記錄檔。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3001">When it is set to All, logs are always downloaded irrespective of the execution status.</span></span> | 

> [!NOTE]
> <span data-ttu-id="6dbb4-3002">您必須在 **outputs** 屬性中指定 Hadoop 串流活動的輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3002">You must specify an output dataset for the Hadoop Streaming Activity for the **outputs** property.</span></span> <span data-ttu-id="6dbb4-3003">這個資料集可能只是驅動管線排程 (每小時、每天等) 所需的虛設資料集。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3003">This dataset can be just a dummy dataset that is required to drive the pipeline schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="6dbb4-3004">如果活動不需要有輸入，您可以略過不用在 **inputs** 屬性中指定活動的輸入資料集。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3004">If the activity doesn't take an input, you can skip specifying an input dataset for the activity for the **inputs** property.</span></span>  

## <a name="json-example"></a><span data-ttu-id="6dbb4-3005">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3005">JSON example</span></span>

```json
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": ["<nameofthecluster>/example/apps/wc.exe","<nameofthecluster>/example/apps/cat.exe"],
                    "fileLinkedService": "StorageLinkedService",
                    "getDebugInfo": "Failure"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-04T00:00:00",
        "end": "2014-01-05T00:00:00"
    }
}
```

<span data-ttu-id="6dbb4-3006">如需詳細資訊，請參閱 [Hadoop 串流活動](data-factory-hadoop-streaming-activity.md)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3006">For more information, see [Hadoop Streaming Activity](data-factory-hadoop-streaming-activity.md) article.</span></span> 

## <a name="hdinsight-spark-activity"></a><span data-ttu-id="6dbb4-3007">HDInsight Spark 活動</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3007">HDInsight Spark Activity</span></span>
<span data-ttu-id="6dbb4-3008">您可以在 Spark 活動 JSON 定義中指定下列屬性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3008">You can specify the following properties in a Spark Activity JSON definition.</span></span> <span data-ttu-id="6dbb4-3009">活動的 type 屬性必須是︰**HDInsightSpark**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3009">The type property for the activity must be: **HDInsightSpark**.</span></span> <span data-ttu-id="6dbb4-3010">您必須先建立 HDInsight 連結服務，再指定它的名稱作為 **linkedServiceName** 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3010">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="6dbb4-3011">當您將活動類型設為 HDInsightSpark 時，**typeProperties** 區段中支援下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3011">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightSpark:</span></span> 

| <span data-ttu-id="6dbb4-3012">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3012">Property</span></span> | <span data-ttu-id="6dbb4-3013">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3013">Description</span></span> | <span data-ttu-id="6dbb4-3014">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3014">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="6dbb4-3015">rootPath</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3015">rootPath</span></span> | <span data-ttu-id="6dbb4-3016">Spark 檔案所在的 Azure Blob 容器和資料夾。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3016">The Azure Blob container and folder that contains the Spark file.</span></span> <span data-ttu-id="6dbb4-3017">檔案名稱有區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3017">The file name is case-sensitive.</span></span> | <span data-ttu-id="6dbb4-3018">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3018">Yes</span></span> |
| <span data-ttu-id="6dbb4-3019">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3019">entryFilePath</span></span> | <span data-ttu-id="6dbb4-3020">Spark 程式碼/套件之根資料夾的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3020">Relative path to the root folder of the Spark code/package.</span></span> | <span data-ttu-id="6dbb4-3021">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3021">Yes</span></span> |
| <span data-ttu-id="6dbb4-3022">className</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3022">className</span></span> | <span data-ttu-id="6dbb4-3023">應用程式的 Java/Spark 主要類別</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3023">Application's Java/Spark main class</span></span> | <span data-ttu-id="6dbb4-3024">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3024">No</span></span> | 
| <span data-ttu-id="6dbb4-3025">arguments</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3025">arguments</span></span> | <span data-ttu-id="6dbb4-3026">Spark 程式的命令列引數清單。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3026">A list of command-line arguments to the Spark program.</span></span> | <span data-ttu-id="6dbb4-3027">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3027">No</span></span> | 
| <span data-ttu-id="6dbb4-3028">proxyUser</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3028">proxyUser</span></span> | <span data-ttu-id="6dbb4-3029">模擬來執行 Spark 程式的使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3029">The user account to impersonate to execute the Spark program</span></span> | <span data-ttu-id="6dbb4-3030">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3030">No</span></span> | 
| <span data-ttu-id="6dbb4-3031">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3031">sparkConfig</span></span> | <span data-ttu-id="6dbb4-3032">Spark 組態屬性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3032">Spark configuration properties.</span></span> | <span data-ttu-id="6dbb4-3033">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3033">No</span></span> | 
| <span data-ttu-id="6dbb4-3034">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3034">getDebugInfo</span></span> | <span data-ttu-id="6dbb4-3035">指定何時將 Spark 記錄檔複製到 HDInsight 叢集所使用 (或) sparkJobLinkedService 所指定的 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3035">Specifies when the Spark log files are copied to the Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="6dbb4-3036">允許的值︰None、Always 或 Failure。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3036">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="6dbb4-3037">預設值：None。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3037">Default value: None.</span></span> | <span data-ttu-id="6dbb4-3038">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3038">No</span></span> | 
| <span data-ttu-id="6dbb4-3039">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3039">sparkJobLinkedService</span></span> | <span data-ttu-id="6dbb4-3040">存放 Spark 作業檔案、相依性和記錄的 Azure 儲存體連結服務。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3040">The Azure Storage linked service that holds the Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="6dbb4-3041">如果您未指定此屬性的值，則會使用與 HDInsight 叢集相關聯的儲存體。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3041">If you do not specify a value for this property, the storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="6dbb4-3042">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3042">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="6dbb4-3043">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3043">JSON example</span></span>

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-05T00:00:00",
        "end": "2017-02-06T00:00:00"
    }
}
```
<span data-ttu-id="6dbb4-3044">請注意下列幾點：</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3044">Note the following points:</span></span> 

- <span data-ttu-id="6dbb4-3045">**type** 屬性會設為 **HDInsightSpark**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3045">The **type** property is set to **HDInsightSpark**.</span></span>
- <span data-ttu-id="6dbb4-3046">**rootPath** 會設為 **adfspark\\pyFiles**，其中 adfspark 是 Azure Blob 容器，而 pyFiles 是該容器中的正常資料夾。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3046">The **rootPath** is set to **adfspark\\pyFiles** where adfspark is the Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="6dbb4-3047">在此範例中，Azure Blob 儲存體是與 Spark 叢集相關聯的儲存體。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3047">In this example, the Azure Blob Storage is the one that is associated with the Spark cluster.</span></span> <span data-ttu-id="6dbb4-3048">您可以將檔案上傳至不同的 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3048">You can upload the file to a different Azure Storage.</span></span> <span data-ttu-id="6dbb4-3049">如果您這麼做，請建立 Azure 儲存體連結服務，以將該儲存體帳戶連結至資料處理站。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3049">If you do so, create an Azure Storage linked service to link that storage account to the data factory.</span></span> <span data-ttu-id="6dbb4-3050">然後，將連結服務的名稱指定為 **sparkJobLinkedService** 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3050">Then, specify the name of the linked service as a value for the **sparkJobLinkedService** property.</span></span> <span data-ttu-id="6dbb4-3051">如需此屬性和 Spark 活動所支援的其他屬性詳細資訊，請參閱 [Spark 活動屬性](#spark-activity-properties)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3051">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by the Spark Activity.</span></span>
- <span data-ttu-id="6dbb4-3052">**entryFilePath** 會設為 **test.py**，這就是 python 檔案。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3052">The **entryFilePath** is set to the **test.py**, which is the python file.</span></span> 
- <span data-ttu-id="6dbb4-3053">**getDebugInfo** 屬性會設為 **Always**，表示永遠產生記錄檔 (不論成功或失敗)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3053">The **getDebugInfo** property is set to **Always**, which means the log files are always generated (success or failure).</span></span>  

    > [!IMPORTANT]
    > <span data-ttu-id="6dbb4-3054">我們建議您不要在生產環境中將這個屬性設定為 Always，除非您要針對問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3054">We recommend that you do not set this property to Always in a production environment unless you are troubleshooting an issue.</span></span> 
- <span data-ttu-id="6dbb4-3055">**outputs** 區段有一個輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3055">The **outputs** section has one output dataset.</span></span> <span data-ttu-id="6dbb4-3056">您必須指定輸出資料集，即使 Spark 程式不會產生任何輸出。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3056">You must specify an output dataset even if the spark program does not produce any output.</span></span> <span data-ttu-id="6dbb4-3057">輸出資料集可以驅動管線的排程 (每小時、每天等)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3057">The output dataset drives the schedule for the pipeline (hourly, daily, etc.).</span></span>

<span data-ttu-id="6dbb4-3058">如需活動的詳細資訊，請參閱 [Spark 活動](data-factory-spark.md)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3058">For more information about the activity, see [Spark Activity](data-factory-spark.md) article.</span></span>  

## <a name="machine-learning-batch-execution-activity"></a><span data-ttu-id="6dbb4-3059">Machine Learning 批次執行活動</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3059">Machine Learning Batch Execution Activity</span></span>
<span data-ttu-id="6dbb4-3060">您可以在 Azure ML 批次執行活動 JSON 定義中指定下列屬性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3060">You can specify the following properties in a Azure ML Batch Execution Activity JSON definition.</span></span> <span data-ttu-id="6dbb4-3061">活動的 type 屬性必須是︰**AzureMLBatchExecution**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3061">The type property for the activity must be: **AzureMLBatchExecution**.</span></span> <span data-ttu-id="6dbb4-3062">您必須先建立 Azure Machine Learning 連結服務，再指定它的名稱作為 **linkedServiceName** 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3062">You must create a Azure Machine Learning linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="6dbb4-3063">當您將活動類型設為 AzureMLBatchExecution 時，**typeProperties** 區段中支援下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3063">The following properties are supported in the **typeProperties** section when you set the type of activity to AzureMLBatchExecution:</span></span>

<span data-ttu-id="6dbb4-3064">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3064">Property</span></span> | <span data-ttu-id="6dbb4-3065">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3065">Description</span></span> | <span data-ttu-id="6dbb4-3066">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3066">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="6dbb4-3067">webServiceInput</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3067">webServiceInput</span></span> | <span data-ttu-id="6dbb4-3068">傳遞作為 Azure ML Web 服務之輸入的資料集。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3068">The dataset to be passed as an input for the Azure ML web service.</span></span> <span data-ttu-id="6dbb4-3069">此資料集也必須包含在活動的輸入中。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3069">This dataset must also be included in the inputs for the activity.</span></span> |<span data-ttu-id="6dbb4-3070">使用 webServiceInput 或 webServiceInputs。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3070">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="6dbb4-3071">webServiceInputs</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3071">webServiceInputs</span></span> | <span data-ttu-id="6dbb4-3072">指定要傳遞作為 Azure ML Web 服務之輸入的資料集。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3072">Specify datasets to be passed as inputs for the Azure ML web service.</span></span> <span data-ttu-id="6dbb4-3073">如果 Web 服務接受多個輸入，請使用 webServiceInputs 屬性，而不要使用 webServiceInput 屬性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3073">If the web service takes multiple inputs, use the webServiceInputs property instead of using the webServiceInput property.</span></span> <span data-ttu-id="6dbb4-3074">**webServiceInputs** 所參考的資料集也必須包含在活動的 **inputs** 中。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3074">Datasets that are referenced by the **webServiceInputs** must also be included in the Activity **inputs**.</span></span> | <span data-ttu-id="6dbb4-3075">使用 webServiceInput 或 webServiceInputs。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3075">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="6dbb4-3076">webServiceOutputs</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3076">webServiceOutputs</span></span> | <span data-ttu-id="6dbb4-3077">指派作為 Azure ML Web 服務之輸出的資料集。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3077">The datasets that are assigned as outputs for the Azure ML web service.</span></span> <span data-ttu-id="6dbb4-3078">Web 服務會在此資料集中傳回輸出資料。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3078">The web service returns output data in this dataset.</span></span> | <span data-ttu-id="6dbb4-3079">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3079">Yes</span></span> | 
<span data-ttu-id="6dbb4-3080">globalParameters</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3080">globalParameters</span></span> | <span data-ttu-id="6dbb4-3081">在此區段中指定 Web 服務參數的值。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3081">Specify values for the web service parameters in this section.</span></span> | <span data-ttu-id="6dbb4-3082">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3082">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="6dbb4-3083">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3083">JSON example</span></span>
<span data-ttu-id="6dbb4-3084">在這個範例中，活動有資料集 **MLSqlInput** 作為輸入，也有 **MLSqlOutput** 作為輸出。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3084">In this example, the activity has the dataset **MLSqlInput** as input and **MLSqlOutput** as the output.</span></span> <span data-ttu-id="6dbb4-3085">**MLSqlInput** 透過 **webServiceInput** JSON 屬性，傳遞至 Web 服務作為輸入。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3085">The **MLSqlInput** is passed as an input to the web service by using the **webServiceInput** JSON property.</span></span> <span data-ttu-id="6dbb4-3086">**MLSqlOutput** 透過 **webServiceOutputs** JSON 屬性，傳遞至 Web 服務作為輸出。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3086">The **MLSqlOutput** is passed as an output to the Web service by using the **webServiceOutputs** JSON property.</span></span> 

```json
{
   "name": "MLWithSqlReaderSqlWriter",
   "properties": {
      "description": "Azure ML model with sql azure reader/writer",
      "activities": [{
         "name": "MLSqlReaderSqlWriterActivity",
         "type": "AzureMLBatchExecution",
         "description": "test",
         "inputs": [ { "name": "MLSqlInput" }],
         "outputs": [ { "name": "MLSqlOutput" } ],
         "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
         "typeProperties":
         {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
               "output1": "MLSqlOutput"
            },
            "globalParameters": {
               "Database server name": "<myserver>.database.windows.net",
               "Database name": "<database>",
               "Server user account name": "<user name>",
               "Server user account password": "<password>"
            }              
         },
         "policy": {
            "concurrency": 1,
            "executionPriorityOrder": "NewestFirst",
            "retry": 1,
            "timeout": "02:00:00"
         }
      }],
      "start": "2016-02-13T00:00:00",
       "end": "2016-02-14T00:00:00"
   }
}
```

<span data-ttu-id="6dbb4-3087">在 JSON 範例中，已部署的 Azure Machine Learning Web 服務使用讀取器和寫入器模組，讀取 Azure SQL Database 的資料，或將資料寫入其中。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3087">In the JSON example, the deployed Azure Machine Learning Web service uses a reader and a writer module to read/write data from/to an Azure SQL Database.</span></span> <span data-ttu-id="6dbb4-3088">此 Web 服務會公開下列 4 個參數：資料庫伺服器名稱、資料庫名稱、伺服器使用者帳戶名稱和伺服器使用者帳戶密碼。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3088">This Web service exposes the following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>

> [!NOTE]
> <span data-ttu-id="6dbb4-3089">只有當輸入及輸出屬於 AzureMLBatchExecution 活動時，才可以當做參數傳遞至 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3089">Only inputs and outputs of the AzureMLBatchExecution activity can be passed as parameters to the Web service.</span></span> <span data-ttu-id="6dbb4-3090">例如，在上面的 JSON 片段中，MLSqlInput 是 AzureMLBatchExecution 活動的輸入，其透過 webServiceInput 參數傳遞至 Web 服務作為輸入。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3090">For example, in the above JSON snippet, MLSqlInput is an input to the AzureMLBatchExecution activity, which is passed as an input to the Web service via webServiceInput parameter.</span></span>

## <a name="machine-learning-update-resource-activity"></a><span data-ttu-id="6dbb4-3091">Machine Learning 更新資源活動</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3091">Machine Learning Update Resource Activity</span></span>
<span data-ttu-id="6dbb4-3092">您可以在 Azure ML 更新資源活動 JSON 定義中指定下列屬性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3092">You can specify the following properties in a Azure ML Update Resource Activity JSON definition.</span></span> <span data-ttu-id="6dbb4-3093">活動的 type 屬性必須是︰**AzureMLUpdateResource**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3093">The type property for the activity must be: **AzureMLUpdateResource**.</span></span> <span data-ttu-id="6dbb4-3094">您必須先建立 Azure Machine Learning 連結服務，再指定它的名稱作為 **linkedServiceName** 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3094">You must create a Azure Machine Learning linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="6dbb4-3095">當您將活動類型設為 AzureMLUpdateResource 時，**typeProperties** 區段中支援下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3095">The following properties are supported in the **typeProperties** section when you set the type of activity to AzureMLUpdateResource:</span></span>

<span data-ttu-id="6dbb4-3096">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3096">Property</span></span> | <span data-ttu-id="6dbb4-3097">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3097">Description</span></span> | <span data-ttu-id="6dbb4-3098">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3098">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="6dbb4-3099">trainedModelName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3099">trainedModelName</span></span> | <span data-ttu-id="6dbb4-3100">重新定型之模型的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3100">Name of the retrained model.</span></span> | <span data-ttu-id="6dbb4-3101">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3101">Yes</span></span> |  
<span data-ttu-id="6dbb4-3102">trainedModelDatasetName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3102">trainedModelDatasetName</span></span> | <span data-ttu-id="6dbb4-3103">此資料集指向重新訓練作業所傳回的 iLearner 檔案。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3103">Dataset pointing to the iLearner file returned by the retraining operation.</span></span> | <span data-ttu-id="6dbb4-3104">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3104">Yes</span></span> | 

### <a name="json-example"></a><span data-ttu-id="6dbb4-3105">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3105">JSON example</span></span>
<span data-ttu-id="6dbb4-3106">管線有兩個活動：**AzureMLBatchExecution** 和 **AzureMLUpdateResource**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3106">The pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="6dbb4-3107">Azure ML 批次執行活動會以訓練資料做為輸入並產生 iLearner 檔案做為輸出。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3107">The Azure ML Batch Execution activity takes the training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="6dbb4-3108">此活動會使用輸入訓練資料叫用訓練 Web 服務 (公開為 Web 服務的訓練實驗)，並從 Web 服務接收 iLearner 檔案。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3108">The activity invokes the training web service (training experiment exposed as a web service) with the input training data and receives the ilearner file from the webservice.</span></span> <span data-ttu-id="6dbb4-3109">PlaceholderBlob 只是 Azure Data Factory 服務執行管線所需的虛擬輸出資料集而已。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3109">The placeholderBlob is just a dummy output dataset that is required by the Azure Data Factory service to run the pipeline.</span></span>


```json
{
    "name": "pipeline",
    "properties": {
        "activities": [
            {
                "name": "retraining",
                "type": "AzureMLBatchExecution",
                "inputs": [
                    {
                        "name": "trainingData"
                    }
                ],
                "outputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "typeProperties": {
                    "webServiceInput": "trainingData",
                    "webServiceOutputs": {
                        "output1": "trainedModelBlob"
                    }              
                 },
                "linkedServiceName": "trainingEndpoint",
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            },
            {
                "type": "AzureMLUpdateResource",
                "typeProperties": {
                    "trainedModelName": "trained model",
                    "trainedModelDatasetName" :  "trainedModelBlob"
                },
                "inputs": [{ "name": "trainedModelBlob" }],
                "outputs": [{ "name": "placeholderBlob" }],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "AzureML Update Resource",
                "linkedServiceName": "updatableScoringEndpoint2"
            }
        ],
        "start": "2016-02-13T00:00:00",
        "end": "2016-02-14T00:00:00"
    }
}
```

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="6dbb4-3110">Data Lake Analytics U-SQL 活動</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3110">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="6dbb4-3111">您可以在 U-SQL 活動 JSON 定義中指定下列屬性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3111">You can specify the following properties in a U-SQL Activity JSON definition.</span></span> <span data-ttu-id="6dbb4-3112">活動的 type 屬性必須是︰**DataLakeAnalyticsU-SQL**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3112">The type property for the activity must be: **DataLakeAnalyticsU-SQL**.</span></span> <span data-ttu-id="6dbb4-3113">您必須建立 Azure Data Lake Analytics 連結服務，並指定它的名稱作為 **linkedServiceName** 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3113">You must create an Azure Data Lake Analytics linked service and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="6dbb4-3114">當您將活動類型設為 DataLakeAnalyticsU-SQL 時，**typeProperties** 區段中支援下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3114">The following properties are supported in the **typeProperties** section when you set the type of activity to DataLakeAnalyticsU-SQL:</span></span> 

| <span data-ttu-id="6dbb4-3115">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3115">Property</span></span> | <span data-ttu-id="6dbb4-3116">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3116">Description</span></span> | <span data-ttu-id="6dbb4-3117">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3117">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="6dbb4-3118">scriptPath</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3118">scriptPath</span></span> |<span data-ttu-id="6dbb4-3119">包含 U-SQL 指令碼的資料夾的路徑。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3119">Path to folder that contains the U-SQL script.</span></span> <span data-ttu-id="6dbb4-3120">檔案的名稱有區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3120">Name of the file is case-sensitive.</span></span> |<span data-ttu-id="6dbb4-3121">否 (如果您使用指令碼)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3121">No (if you use script)</span></span> |
| <span data-ttu-id="6dbb4-3122">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3122">scriptLinkedService</span></span> |<span data-ttu-id="6dbb4-3123">連結服務會連結包含 Data Factory 的指令碼的儲存體</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3123">Linked service that links the storage that contains the script to the data factory</span></span> |<span data-ttu-id="6dbb4-3124">否 (如果您使用指令碼)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3124">No (if you use script)</span></span> |
| <span data-ttu-id="6dbb4-3125">script</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3125">script</span></span> |<span data-ttu-id="6dbb4-3126">指定內嵌指令碼而不是指定 scriptPath 和 scriptLinkedService。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3126">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="6dbb4-3127">例如："script": "CREATE DATABASE test"。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3127">For example: "script": "CREATE DATABASE test".</span></span> |<span data-ttu-id="6dbb4-3128">否 (如果您使用 scriptPath 和 scriptLinkedService)</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3128">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="6dbb4-3129">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3129">degreeOfParallelism</span></span> |<span data-ttu-id="6dbb4-3130">同時用來執行作業的節點數目上限。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3130">The maximum number of nodes simultaneously used to run the job.</span></span> |<span data-ttu-id="6dbb4-3131">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3131">No</span></span> |
| <span data-ttu-id="6dbb4-3132">優先順序</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3132">priority</span></span> |<span data-ttu-id="6dbb4-3133">判斷應該選取排入佇列的哪些工作首先執行。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3133">Determines which jobs out of all that are queued should be selected to run first.</span></span> <span data-ttu-id="6dbb4-3134">編號愈低，優先順序愈高。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3134">The lower the number, the higher the priority.</span></span> |<span data-ttu-id="6dbb4-3135">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3135">No</span></span> |
| <span data-ttu-id="6dbb4-3136">參數</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3136">parameters</span></span> |<span data-ttu-id="6dbb4-3137">U-SQL 指令碼的參數</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3137">Parameters for the U-SQL script</span></span> |<span data-ttu-id="6dbb4-3138">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3138">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="6dbb4-3139">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3139">JSON example</span></span>

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This pipeline computes events for en-gb locale and date less than Feb 19, 2012.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00",
        "end": "2015-08-08T01:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="6dbb4-3140">如需詳細資訊，請參閱 [Data Lake Analytics U-SQL 活動](data-factory-usql-activity.md)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3140">For more information, see [Data Lake Analytics U-SQL Activity](data-factory-usql-activity.md).</span></span> 

## <a name="stored-procedure-activity"></a><span data-ttu-id="6dbb4-3141">預存程序活動</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3141">Stored Procedure Activity</span></span>
<span data-ttu-id="6dbb4-3142">您可以在預存程序活動 JSON 定義中指定下列屬性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3142">You can specify the following properties in a Stored Procedure Activity JSON definition.</span></span> <span data-ttu-id="6dbb4-3143">活動的 type 屬性必須是︰**SqlServerStoredProcedure**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3143">The type property for the activity must be: **SqlServerStoredProcedure**.</span></span> <span data-ttu-id="6dbb4-3144">您必須建立下列其中一個連結服務，並指定連結服務的名稱作為 **linkedServiceName** 屬性的值：</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3144">You must create an one of the following linked services and specify the name of the linked service as a value for the **linkedServiceName** property:</span></span>

- <span data-ttu-id="6dbb4-3145">SQL Server</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3145">SQL Server</span></span> 
- <span data-ttu-id="6dbb4-3146">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3146">Azure SQL Database</span></span>
- <span data-ttu-id="6dbb4-3147">Azure SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3147">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="6dbb4-3148">當您將活動類型設為 SqlServerStoredProcedure 時，**typeProperties** 區段中支援下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3148">The following properties are supported in the **typeProperties** section when you set the type of activity to SqlServerStoredProcedure:</span></span>

| <span data-ttu-id="6dbb4-3149">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3149">Property</span></span> | <span data-ttu-id="6dbb4-3150">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3150">Description</span></span> | <span data-ttu-id="6dbb4-3151">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3151">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dbb4-3152">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3152">storedProcedureName</span></span> |<span data-ttu-id="6dbb4-3153">指定 Azure SQL Database 或 Azure SQL 資料倉儲中預存程序的名稱，由輸出資料表使用的連結的服務代表。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3153">Specify the name of the stored procedure in the Azure SQL database or Azure SQL Data Warehouse that is represented by the linked service that the output table uses.</span></span> |<span data-ttu-id="6dbb4-3154">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3154">Yes</span></span> |
| <span data-ttu-id="6dbb4-3155">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3155">storedProcedureParameters</span></span> |<span data-ttu-id="6dbb4-3156">指定預存程序參數的值。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3156">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="6dbb4-3157">如果您要為參數傳遞 null，請使用語法："param1": null (全部小寫)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3157">If you need to pass null for a parameter, use the syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="6dbb4-3158">請參閱下列範例以了解如何使用這個屬性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3158">See the following sample to learn about using this property.</span></span> |<span data-ttu-id="6dbb4-3159">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3159">No</span></span> |

<span data-ttu-id="6dbb4-3160">如果您有指定輸入資料集，它必須可供使用 (「就緒」狀態)，預存程序活動才能執行。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3160">If you do specify an input dataset, it must be available (in ‘Ready’ status) for the stored procedure activity to run.</span></span> <span data-ttu-id="6dbb4-3161">在預存程序中輸入資料集無法做為參數取用。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3161">The input dataset cannot be consumed in the stored procedure as a parameter.</span></span> <span data-ttu-id="6dbb4-3162">它只會用來在啟動預存程序活動之前檢查相依性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3162">It is only used to check the dependency before starting the stored procedure activity.</span></span> <span data-ttu-id="6dbb4-3163">您必須指定預存程序活動的輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3163">You must specify an output dataset for a stored procedure activity.</span></span> 

<span data-ttu-id="6dbb4-3164">輸出資料集會指定預存程序活動的 **排程** (每小時、每週、每月等)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3164">Output dataset specifies the **schedule** for the stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <span data-ttu-id="6dbb4-3165">輸出資料集必須使用參考了想在其中執行預存程序之 Azure SQL Database、Azure SQL 資料倉儲或 SQL Server Database 的 **連結服務** 。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3165">The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run.</span></span> <span data-ttu-id="6dbb4-3166">輸出資料集可以做為傳遞預存程序結果，以供管線中的另一個活動 ([鏈結活動](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) 進行後續處理的方式。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3166">The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) in the pipeline.</span></span> <span data-ttu-id="6dbb4-3167">不過，Data Factory 不會自動將預存程序的輸出寫入至此資料集。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3167">However, Data Factory does not automatically write the output of a stored procedure to this dataset.</span></span> <span data-ttu-id="6dbb4-3168">它是會寫入至輸出資料集所指向之 SQL 資料表的預存程序。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3168">It is the stored procedure that writes to a SQL table that the output dataset points to.</span></span> <span data-ttu-id="6dbb4-3169">在某些情況下，輸出資料集可以是 **虛擬資料集**，只會用來指定用於執行預存程序活動的排程。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3169">In some cases, the output dataset can be a **dummy dataset**, which is used only to specify the schedule for running the stored procedure activity.</span></span>  

### <a name="json-example"></a><span data-ttu-id="6dbb4-3170">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3170">JSON example</span></span>

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
                "outputs": [{ "name": "sprocsampleout" }],
                "name": "SprocActivitySample"
            }
        ],
         "start": "2016-08-02T00:00:00",
         "end": "2016-08-02T05:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="6dbb4-3171">如需詳細資訊，請參閱[預存程序活動](data-factory-stored-proc-activity.md)。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3171">For more information, see [Stored Procedure Activity](data-factory-stored-proc-activity.md) article.</span></span> 

## <a name="net-custom-activity"></a><span data-ttu-id="6dbb4-3172">.NET 自訂活動</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3172">.NET custom activity</span></span>
<span data-ttu-id="6dbb4-3173">您可以在 .NET 自訂活動 JSON 定義中指定下列屬性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3173">You can specify the following properties in a .NET custom activity JSON definition.</span></span> <span data-ttu-id="6dbb4-3174">活動的 type 屬性必須是︰**DotNetActivity**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3174">The type property for the activity must be: **DotNetActivity**.</span></span> <span data-ttu-id="6dbb4-3175">您必須建立 Azure HDInsight 連結服務，或 Azure Batch 連結服務，然後指定連結服務的名稱作為 **linkedServiceName** 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3175">You must create an Azure HDInsight linked service or an Azure Batch linked service, and specify the name of the linked service as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="6dbb4-3176">當您將活動類型設為 DotNetActivity 時，**typeProperties** 區段中支援下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3176">The following properties are supported in the **typeProperties** section when you set the type of activity to DotNetActivity:</span></span>
 
| <span data-ttu-id="6dbb4-3177">屬性</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3177">Property</span></span> | <span data-ttu-id="6dbb4-3178">說明</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3178">Description</span></span> | <span data-ttu-id="6dbb4-3179">必要</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3179">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="6dbb4-3180">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3180">AssemblyName</span></span> | <span data-ttu-id="6dbb4-3181">組件的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3181">Name of the assembly.</span></span> <span data-ttu-id="6dbb4-3182">在此範例中，它是︰**MyDotnetActivity.dll**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3182">In the example, it is: **MyDotnetActivity.dll**.</span></span> | <span data-ttu-id="6dbb4-3183">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3183">Yes</span></span> |
| <span data-ttu-id="6dbb4-3184">EntryPoint</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3184">EntryPoint</span></span> |<span data-ttu-id="6dbb4-3185">實作 IDotNetActivity 介面的類別名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3185">Name of the class that implements the IDotNetActivity interface.</span></span> <span data-ttu-id="6dbb4-3186">在此範例中，它是︰**MyDotNetActivityNS.MyDotNetActivity**，其中 MyDotNetActivityNS 是命名空間，而 MyDotNetActivity 是類別。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3186">In the example, it is: **MyDotNetActivityNS.MyDotNetActivity** where MyDotNetActivityNS is the namespace and MyDotNetActivity is the class.</span></span>  | <span data-ttu-id="6dbb4-3187">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3187">Yes</span></span> | 
| <span data-ttu-id="6dbb4-3188">PackageLinkedService</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3188">PackageLinkedService</span></span> | <span data-ttu-id="6dbb4-3189">Azure 儲存體連結服務的名稱，指向包含自訂活動 zip 檔案的 Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3189">Name of the Azure Storage linked service that points to the blob storage that contains the custom activity zip file.</span></span> <span data-ttu-id="6dbb4-3190">在此範例中，它是：**AzureStorageLinkedService**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3190">In the example, it is: **AzureStorageLinkedService**.</span></span>| <span data-ttu-id="6dbb4-3191">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3191">Yes</span></span> |
| <span data-ttu-id="6dbb4-3192">PackageFile</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3192">PackageFile</span></span> | <span data-ttu-id="6dbb4-3193">zip 檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3193">Name of the zip file.</span></span> <span data-ttu-id="6dbb4-3194">在此範例中，它是：**customactivitycontainer/MyDotNetActivity.zip**。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3194">In the example, it is: **customactivitycontainer/MyDotNetActivity.zip**.</span></span> | <span data-ttu-id="6dbb4-3195">是</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3195">Yes</span></span> |
| <span data-ttu-id="6dbb4-3196">extendedProperties</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3196">extendedProperties</span></span> | <span data-ttu-id="6dbb4-3197">可定義並傳遞至 .NET 程式碼的擴充屬性。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3197">Extended properties that you can define and pass on to the .NET code.</span></span> <span data-ttu-id="6dbb4-3198">在此範例中，**SliceStart** 變數的值是根據 SliceStart 系統變數來設定。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3198">In this example, the **SliceStart** variable is set to a value based on the SliceStart system variable.</span></span> | <span data-ttu-id="6dbb4-3199">否</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3199">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="6dbb4-3200">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3200">JSON example</span></span>

```json
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "AzureBatchLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00",
    "end": "2016-11-16T05:00:00",
    "isPaused": false
  }
}
```

<span data-ttu-id="6dbb4-3201">如需詳細資訊，請參閱[在 Data Factory 中使用自訂活動](data-factory-use-custom-activities.md)文件。</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3201">For detailed information, see [Use custom activities in Data Factory](data-factory-use-custom-activities.md) article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6dbb4-3202">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3202">Next Steps</span></span>
<span data-ttu-id="6dbb4-3203">請參閱下列教學課程：</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3203">See the following tutorials:</span></span> 

- [<span data-ttu-id="6dbb4-3204">教學課程：建立具有複製活動的管線</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3204">Tutorial: create a pipeline with a copy activity</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
- [<span data-ttu-id="6dbb4-3205">教學課程：建立具有 Hive 活動的管線</span><span class="sxs-lookup"><span data-stu-id="6dbb4-3205">Tutorial: create a pipeline with a hive activity</span></span>](data-factory-build-your-first-pipeline-using-editor.md)