---
title: "aaaAzure Data Factory-JSON 指令碼參考 |Microsoft 文件"
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
ms.openlocfilehash: 813fd752bb0ecb1b513d022b9f302325105dac31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---json-scripting-reference"></a><span data-ttu-id="566d6-103">Azure Data Factory - JSON 指令碼參考</span><span class="sxs-lookup"><span data-stu-id="566d6-103">Azure Data Factory - JSON Scripting Reference</span></span>
<span data-ttu-id="566d6-104">本文提供 JSON 結構描述和範例來定義 Azure Data Factory 實體 (管線、活動、資料集和連結服務)。</span><span class="sxs-lookup"><span data-stu-id="566d6-104">This article provides JSON schemas and examples for defining Azure Data Factory entities (pipeline, activity, dataset, and linked service).</span></span>  

## <a name="pipeline"></a><span data-ttu-id="566d6-105">管線</span><span class="sxs-lookup"><span data-stu-id="566d6-105">Pipeline</span></span> 
<span data-ttu-id="566d6-106">如需管線定義 hello 高階結構如下所示：</span><span class="sxs-lookup"><span data-stu-id="566d6-106">hello high-level structure for a pipeline definition is as follows:</span></span> 

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

<span data-ttu-id="566d6-107">下表描述 hello 管線 JSON 定義中的 hello 屬性：</span><span class="sxs-lookup"><span data-stu-id="566d6-107">Following table describes hello properties within hello pipeline JSON definition:</span></span>

| <span data-ttu-id="566d6-108">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-108">Property</span></span> | <span data-ttu-id="566d6-109">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-109">Description</span></span> | <span data-ttu-id="566d6-110">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-110">Required</span></span>
-------- | ----------- | --------
| <span data-ttu-id="566d6-111">名稱</span><span class="sxs-lookup"><span data-stu-id="566d6-111">name</span></span> | <span data-ttu-id="566d6-112">Hello 管線的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-112">Name of hello pipeline.</span></span> <span data-ttu-id="566d6-113">指定代表 hello 活動的 hello 動作的名稱或管線是設定的 toodo</span><span class="sxs-lookup"><span data-stu-id="566d6-113">Specify a name that represents hello action that hello activity or pipeline is configured toodo</span></span><br/><ul><li><span data-ttu-id="566d6-114">字元數目上限︰260</span><span class="sxs-lookup"><span data-stu-id="566d6-114">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="566d6-115">開頭必須為字母、數字或底線 (_)</span><span class="sxs-lookup"><span data-stu-id="566d6-115">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="566d6-116">不允許使用下列字元：“.”、“+”、“?”、“/”、“<”、”>”、”*”、”%”、”&”、”:”、”\\”</span><span class="sxs-lookup"><span data-stu-id="566d6-116">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="566d6-117">是</span><span class="sxs-lookup"><span data-stu-id="566d6-117">Yes</span></span> |
| <span data-ttu-id="566d6-118">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-118">description</span></span> |<span data-ttu-id="566d6-119">描述使用何種 hello 活動或管線做為文字</span><span class="sxs-lookup"><span data-stu-id="566d6-119">Text describing what hello activity or pipeline is used for</span></span> | <span data-ttu-id="566d6-120">否</span><span class="sxs-lookup"><span data-stu-id="566d6-120">No</span></span> |
| <span data-ttu-id="566d6-121">活動</span><span class="sxs-lookup"><span data-stu-id="566d6-121">activities</span></span> | <span data-ttu-id="566d6-122">包含活動清單。</span><span class="sxs-lookup"><span data-stu-id="566d6-122">Contains a list of activities.</span></span> | <span data-ttu-id="566d6-123">是</span><span class="sxs-lookup"><span data-stu-id="566d6-123">Yes</span></span> |
| <span data-ttu-id="566d6-124">start</span><span class="sxs-lookup"><span data-stu-id="566d6-124">start</span></span> |<span data-ttu-id="566d6-125">開始日期-時間 hello 管線。</span><span class="sxs-lookup"><span data-stu-id="566d6-125">Start date-time for hello pipeline.</span></span> <span data-ttu-id="566d6-126">必須使用 [ISO 格式](http://en.wikipedia.org/wiki/ISO_8601)。</span><span class="sxs-lookup"><span data-stu-id="566d6-126">Must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="566d6-127">例如︰2014-10-14T16:32:41。</span><span class="sxs-lookup"><span data-stu-id="566d6-127">For example: 2014-10-14T16:32:41.</span></span> <br/><br/><span data-ttu-id="566d6-128">很可能 toospecify 本地時間，例如預估時間。</span><span class="sxs-lookup"><span data-stu-id="566d6-128">It is possible toospecify a local time, for example an EST time.</span></span> <span data-ttu-id="566d6-129">範例如下︰`2016-02-27T06:00:00**-05:00`，這是 6 AM EST。</span><span class="sxs-lookup"><span data-stu-id="566d6-129">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="566d6-130">hello 開始和結束屬性一起指定 hello 管線的作用期間。</span><span class="sxs-lookup"><span data-stu-id="566d6-130">hello start and end properties together specify active period for hello pipeline.</span></span> <span data-ttu-id="566d6-131">輸出配量只會在作用中期間內產生。</span><span class="sxs-lookup"><span data-stu-id="566d6-131">Output slices are only produced with in this active period.</span></span> |<span data-ttu-id="566d6-132">否</span><span class="sxs-lookup"><span data-stu-id="566d6-132">No</span></span><br/><br/><span data-ttu-id="566d6-133">如果您指定 hello 結束屬性的值，您必須指定 hello 開始屬性值。</span><span class="sxs-lookup"><span data-stu-id="566d6-133">If you specify a value for hello end property, you must specify value for hello start property.</span></span><br/><br/><span data-ttu-id="566d6-134">hello 開始和結束時間可以是空的 toocreate 管線。</span><span class="sxs-lookup"><span data-stu-id="566d6-134">hello start and end times can both be empty toocreate a pipeline.</span></span> <span data-ttu-id="566d6-135">您必須指定這兩個值的作用中期間 hello 管線 toorun tooset。</span><span class="sxs-lookup"><span data-stu-id="566d6-135">You must specify both values tooset an active period for hello pipeline toorun.</span></span> <span data-ttu-id="566d6-136">如果您未指定開始和結束時間時建立管線，您可以設定它們使用 hello 組 AzureRmDataFactoryPipelineActivePeriod 指令程式更新版本。</span><span class="sxs-lookup"><span data-stu-id="566d6-136">If you do not specify start and end times when creating a pipeline, you can set them using hello Set-AzureRmDataFactoryPipelineActivePeriod cmdlet later.</span></span> |
| <span data-ttu-id="566d6-137">end</span><span class="sxs-lookup"><span data-stu-id="566d6-137">end</span></span> |<span data-ttu-id="566d6-138">結束日期與時間 hello 管線。</span><span class="sxs-lookup"><span data-stu-id="566d6-138">End date-time for hello pipeline.</span></span> <span data-ttu-id="566d6-139">如果已指定，則必須使用 ISO 格式。</span><span class="sxs-lookup"><span data-stu-id="566d6-139">If specified must be in ISO format.</span></span> <span data-ttu-id="566d6-140">例如：2014-10-14T17:32:41</span><span class="sxs-lookup"><span data-stu-id="566d6-140">For example: 2014-10-14T17:32:41</span></span> <br/><br/><span data-ttu-id="566d6-141">很可能 toospecify 本地時間，例如預估時間。</span><span class="sxs-lookup"><span data-stu-id="566d6-141">It is possible toospecify a local time, for example an EST time.</span></span> <span data-ttu-id="566d6-142">範例如下︰`2016-02-27T06:00:00**-05:00`，這是 6 AM EST。</span><span class="sxs-lookup"><span data-stu-id="566d6-142">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="566d6-143">toorun hello 管線無限期地指定 9999-09-09 hello hello end 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="566d6-143">toorun hello pipeline indefinitely, specify 9999-09-09 as hello value for hello end property.</span></span> |<span data-ttu-id="566d6-144">否</span><span class="sxs-lookup"><span data-stu-id="566d6-144">No</span></span> <br/><br/><span data-ttu-id="566d6-145">如果您指定 hello 開始屬性的值，您必須指定 hello end 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="566d6-145">If you specify a value for hello start property, you must specify value for hello end property.</span></span><br/><br/><span data-ttu-id="566d6-146">請參閱備註 hello**啟動**屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-146">See notes for hello **start** property.</span></span> |
| <span data-ttu-id="566d6-147">isPaused</span><span class="sxs-lookup"><span data-stu-id="566d6-147">isPaused</span></span> |<span data-ttu-id="566d6-148">如果組 tootrue hello 管線不會執行。</span><span class="sxs-lookup"><span data-stu-id="566d6-148">If set tootrue hello pipeline does not run.</span></span> <span data-ttu-id="566d6-149">預設值 = false。</span><span class="sxs-lookup"><span data-stu-id="566d6-149">Default value = false.</span></span> <span data-ttu-id="566d6-150">您可以使用這個屬性 tooenable 或停用。</span><span class="sxs-lookup"><span data-stu-id="566d6-150">You can use this property tooenable or disable.</span></span> |<span data-ttu-id="566d6-151">否</span><span class="sxs-lookup"><span data-stu-id="566d6-151">No</span></span> |
| <span data-ttu-id="566d6-152">pipelineMode</span><span class="sxs-lookup"><span data-stu-id="566d6-152">pipelineMode</span></span> |<span data-ttu-id="566d6-153">hello 管線的可執行的排程 hello 方法。</span><span class="sxs-lookup"><span data-stu-id="566d6-153">hello method for scheduling runs for hello pipeline.</span></span> <span data-ttu-id="566d6-154">允許的值包括：scheduled (預設值)、onetime。</span><span class="sxs-lookup"><span data-stu-id="566d6-154">Allowed values are: scheduled (default), onetime.</span></span><br/><br/><span data-ttu-id="566d6-155">排程' 表示該 hello 管線 tooits 作用期間 （開始和結束時間），根據指定的時間間隔執行。</span><span class="sxs-lookup"><span data-stu-id="566d6-155">‘Scheduled’ indicates that hello pipeline runs at a specified time interval according tooits active period (start and end time).</span></span> <span data-ttu-id="566d6-156">'一次' 表示該 hello 管線只執行一次。</span><span class="sxs-lookup"><span data-stu-id="566d6-156">‘Onetime’ indicates that hello pipeline runs only once.</span></span> <span data-ttu-id="566d6-157">目前，Onetime 管線在建立之後即無法進行修改/更新。</span><span class="sxs-lookup"><span data-stu-id="566d6-157">Onetime pipelines once created cannot be modified/updated currently.</span></span> <span data-ttu-id="566d6-158">如需 onetime 設定的詳細資料，請參閱 [Onetime 管線](data-factory-create-pipelines.md#onetime-pipeline)。</span><span class="sxs-lookup"><span data-stu-id="566d6-158">See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details about onetime setting.</span></span> |<span data-ttu-id="566d6-159">否</span><span class="sxs-lookup"><span data-stu-id="566d6-159">No</span></span> |
| <span data-ttu-id="566d6-160">expirationTime</span><span class="sxs-lookup"><span data-stu-id="566d6-160">expirationTime</span></span> |<span data-ttu-id="566d6-161">長時間後建立的 hello 管線有效，且應保持已佈建。</span><span class="sxs-lookup"><span data-stu-id="566d6-161">Duration of time after creation for which hello pipeline is valid and should remain provisioned.</span></span> <span data-ttu-id="566d6-162">如果它沒有任何作用中、 失敗，或暫止執行，hello 管線則會自動刪除到達 hello 到期時間。</span><span class="sxs-lookup"><span data-stu-id="566d6-162">If it does not have any active, failed, or pending runs, hello pipeline is deleted automatically once it reaches hello expiration time.</span></span> |<span data-ttu-id="566d6-163">否</span><span class="sxs-lookup"><span data-stu-id="566d6-163">No</span></span> |


## <a name="activity"></a><span data-ttu-id="566d6-164">活動</span><span class="sxs-lookup"><span data-stu-id="566d6-164">Activity</span></span> 
<span data-ttu-id="566d6-165">hello 管線定義 （活動項目） 中活動的高階結構如下所示：</span><span class="sxs-lookup"><span data-stu-id="566d6-165">hello high-level structure for an activity within a pipeline definition (activities element) is as follows:</span></span>

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

<span data-ttu-id="566d6-166">下列表格說明 hello 活動 JSON 定義中的 hello 屬性：</span><span class="sxs-lookup"><span data-stu-id="566d6-166">Following table describe hello properties within hello activity JSON definition:</span></span>

| <span data-ttu-id="566d6-167">Tag</span><span class="sxs-lookup"><span data-stu-id="566d6-167">Tag</span></span> | <span data-ttu-id="566d6-168">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-168">Description</span></span> | <span data-ttu-id="566d6-169">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-170">名稱</span><span class="sxs-lookup"><span data-stu-id="566d6-170">name</span></span> |<span data-ttu-id="566d6-171">Hello 活動名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-171">Name of hello activity.</span></span> <span data-ttu-id="566d6-172">指定代表 hello 動作 hello 活動的名稱設定 toodo</span><span class="sxs-lookup"><span data-stu-id="566d6-172">Specify a name that represents hello action that hello activity is configured toodo</span></span><br/><ul><li><span data-ttu-id="566d6-173">字元數目上限︰260</span><span class="sxs-lookup"><span data-stu-id="566d6-173">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="566d6-174">開頭必須為字母、數字或底線 (_)</span><span class="sxs-lookup"><span data-stu-id="566d6-174">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="566d6-175">不允許使用下列字元：“.”、“+”、“?”、“/”、“<”、”>”、”*”、”%”、”&”、”:”、”\\”</span><span class="sxs-lookup"><span data-stu-id="566d6-175">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="566d6-176">是</span><span class="sxs-lookup"><span data-stu-id="566d6-176">Yes</span></span> |
| <span data-ttu-id="566d6-177">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-177">description</span></span> |<span data-ttu-id="566d6-178">描述用於 hello 活動的文字。</span><span class="sxs-lookup"><span data-stu-id="566d6-178">Text describing what hello activity is used for.</span></span> |<span data-ttu-id="566d6-179">是</span><span class="sxs-lookup"><span data-stu-id="566d6-179">Yes</span></span> |
| <span data-ttu-id="566d6-180">類型</span><span class="sxs-lookup"><span data-stu-id="566d6-180">type</span></span> |<span data-ttu-id="566d6-181">指定 hello hello 活動型別。</span><span class="sxs-lookup"><span data-stu-id="566d6-181">Specifies hello type of hello activity.</span></span> <span data-ttu-id="566d6-182">請參閱 hello[資料存放區](#data-stores)和[資料轉換活動](#data-transformation-activities)區段的不同類型的活動。</span><span class="sxs-lookup"><span data-stu-id="566d6-182">See hello [DATA STORES](#data-stores) and [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) sections for different types of activities.</span></span> |<span data-ttu-id="566d6-183">是</span><span class="sxs-lookup"><span data-stu-id="566d6-183">Yes</span></span> |
| <span data-ttu-id="566d6-184">輸入</span><span class="sxs-lookup"><span data-stu-id="566d6-184">inputs</span></span> |<span data-ttu-id="566d6-185">Hello 活動所使用的輸入的資料表</span><span class="sxs-lookup"><span data-stu-id="566d6-185">Input tables used by hello activity</span></span><br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |<span data-ttu-id="566d6-186">是</span><span class="sxs-lookup"><span data-stu-id="566d6-186">Yes</span></span> |
| <span data-ttu-id="566d6-187">輸出</span><span class="sxs-lookup"><span data-stu-id="566d6-187">outputs</span></span> |<span data-ttu-id="566d6-188">使用的 hello 活動的輸出的資料表。</span><span class="sxs-lookup"><span data-stu-id="566d6-188">Output tables used by hello activity.</span></span><br/><br/>`// one output table`<br/>`"outputs":  [ { "name": “outputtable1” } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": “outputtable1” }, { "name": “outputtable2” }  ],` |<span data-ttu-id="566d6-189">是</span><span class="sxs-lookup"><span data-stu-id="566d6-189">Yes</span></span> |
| <span data-ttu-id="566d6-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="566d6-190">linkedServiceName</span></span> |<span data-ttu-id="566d6-191">Hello 活動所使用的 hello 連結服務名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-191">Name of hello linked service used by hello activity.</span></span> <br/><br/><span data-ttu-id="566d6-192">活動可能會要求您指定連結 toohello 必要的運算環境的 hello 連結服務。</span><span class="sxs-lookup"><span data-stu-id="566d6-192">An activity may require that you specify hello linked service that links toohello required compute environment.</span></span> |<span data-ttu-id="566d6-193">對於 HDInsight 活動、Azure Machine Learning 活動和預存程序活動而言為必要。</span><span class="sxs-lookup"><span data-stu-id="566d6-193">Yes for HDInsight activities, Azure Machine Learning activities, and Stored Procedure Activity.</span></span> <br/><br/><span data-ttu-id="566d6-194">否：所有其他</span><span class="sxs-lookup"><span data-stu-id="566d6-194">No for all others</span></span> |
| <span data-ttu-id="566d6-195">typeProperties</span><span class="sxs-lookup"><span data-stu-id="566d6-195">typeProperties</span></span> |<span data-ttu-id="566d6-196">Hello typeProperties > 一節中的屬性取決於 hello 活動的類型。</span><span class="sxs-lookup"><span data-stu-id="566d6-196">Properties in hello typeProperties section depend on type of hello activity.</span></span> |<span data-ttu-id="566d6-197">否</span><span class="sxs-lookup"><span data-stu-id="566d6-197">No</span></span> |
| <span data-ttu-id="566d6-198">原則</span><span class="sxs-lookup"><span data-stu-id="566d6-198">policy</span></span> |<span data-ttu-id="566d6-199">影響 hello hello 活動執行階段行為的原則。</span><span class="sxs-lookup"><span data-stu-id="566d6-199">Policies that affect hello run-time behavior of hello activity.</span></span> <span data-ttu-id="566d6-200">如果未指定，則會使用預設原則。</span><span class="sxs-lookup"><span data-stu-id="566d6-200">If it is not specified, default policies are used.</span></span> |<span data-ttu-id="566d6-201">否</span><span class="sxs-lookup"><span data-stu-id="566d6-201">No</span></span> |
| <span data-ttu-id="566d6-202">scheduler</span><span class="sxs-lookup"><span data-stu-id="566d6-202">scheduler</span></span> |<span data-ttu-id="566d6-203">「 排程器 」 屬性是使用的 toodefine 預期 hello 活動的排程。</span><span class="sxs-lookup"><span data-stu-id="566d6-203">“scheduler” property is used toodefine desired scheduling for hello activity.</span></span> <span data-ttu-id="566d6-204">及其子屬性會 hello 與 hello hello 於相同[可用性屬性集中](data-factory-create-datasets.md#dataset-availability)。</span><span class="sxs-lookup"><span data-stu-id="566d6-204">Its subproperties are hello same as hello ones in hello [availability property in a dataset](data-factory-create-datasets.md#dataset-availability).</span></span> |<span data-ttu-id="566d6-205">否</span><span class="sxs-lookup"><span data-stu-id="566d6-205">No</span></span> |

### <a name="policies"></a><span data-ttu-id="566d6-206">原則</span><span class="sxs-lookup"><span data-stu-id="566d6-206">Policies</span></span>
<span data-ttu-id="566d6-207">特別是當處理資料表的 hello 配量時，原則會影響 hello 執行階段行為的活動。</span><span class="sxs-lookup"><span data-stu-id="566d6-207">Policies affect hello run-time behavior of an activity, specifically when hello slice of a table is processed.</span></span> <span data-ttu-id="566d6-208">下表中的 hello 提供 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-208">hello following table provides hello details.</span></span>

| <span data-ttu-id="566d6-209">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-209">Property</span></span> | <span data-ttu-id="566d6-210">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-210">Permitted values</span></span> | <span data-ttu-id="566d6-211">預設值</span><span class="sxs-lookup"><span data-stu-id="566d6-211">Default Value</span></span> | <span data-ttu-id="566d6-212">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-212">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-213">並行</span><span class="sxs-lookup"><span data-stu-id="566d6-213">concurrency</span></span> |<span data-ttu-id="566d6-214">整數 </span><span class="sxs-lookup"><span data-stu-id="566d6-214">Integer</span></span> <br/><br/><span data-ttu-id="566d6-215">最大值：10</span><span class="sxs-lookup"><span data-stu-id="566d6-215">Max value: 10</span></span> |<span data-ttu-id="566d6-216">1</span><span class="sxs-lookup"><span data-stu-id="566d6-216">1</span></span> |<span data-ttu-id="566d6-217">並行執行的 hello 活動的數目。</span><span class="sxs-lookup"><span data-stu-id="566d6-217">Number of concurrent executions of hello activity.</span></span><br/><br/><span data-ttu-id="566d6-218">它決定不同配量上可能發生的平行活動執行的 hello 次數。</span><span class="sxs-lookup"><span data-stu-id="566d6-218">It determines hello number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="566d6-219">例如，如果活動需要透過 toogo 大量可用的資料，具有較大的並行值就會加快 hello 資料處理。</span><span class="sxs-lookup"><span data-stu-id="566d6-219">For example, if an activity needs toogo through a large set of available data, having a larger concurrency value speeds up hello data processing.</span></span> |
| <span data-ttu-id="566d6-220">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="566d6-220">executionPriorityOrder</span></span> |<span data-ttu-id="566d6-221">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="566d6-221">NewestFirst</span></span><br/><br/><span data-ttu-id="566d6-222">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="566d6-222">OldestFirst</span></span> |<span data-ttu-id="566d6-223">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="566d6-223">OldestFirst</span></span> |<span data-ttu-id="566d6-224">判斷正在處理的資料配量順序 hello。</span><span class="sxs-lookup"><span data-stu-id="566d6-224">Determines hello ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="566d6-225">例如，如果您有 2 個配量 (一個發生在下午 4 點，另一個發生在下午 5 點)，而兩者都暫停執行。</span><span class="sxs-lookup"><span data-stu-id="566d6-225">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="566d6-226">如果您設定 hello executionpriorityorder 設 toobe NewestFirst，會先處理下午 5 點的 hello 配量。</span><span class="sxs-lookup"><span data-stu-id="566d6-226">If you set hello executionPriorityOrder toobe NewestFirst, hello slice at 5 PM is processed first.</span></span> <span data-ttu-id="566d6-227">同樣地如果您設定 hello executionpriorityorder 設 toobe OldestFIrst，然後在下午 4 點 hello 配量會處理。</span><span class="sxs-lookup"><span data-stu-id="566d6-227">Similarly if you set hello executionPriorityORder toobe OldestFIrst, then hello slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="566d6-228">retry</span><span class="sxs-lookup"><span data-stu-id="566d6-228">retry</span></span> |<span data-ttu-id="566d6-229">整數 </span><span class="sxs-lookup"><span data-stu-id="566d6-229">Integer</span></span><br/><br/><span data-ttu-id="566d6-230">最大值可以是 10</span><span class="sxs-lookup"><span data-stu-id="566d6-230">Max value can be 10</span></span> |<span data-ttu-id="566d6-231">0</span><span class="sxs-lookup"><span data-stu-id="566d6-231">0</span></span> |<span data-ttu-id="566d6-232">Hello hello 配量的資料處理之前的重試的數目會標示為失敗。</span><span class="sxs-lookup"><span data-stu-id="566d6-232">Number of retries before hello data processing for hello slice is marked as Failure.</span></span> <span data-ttu-id="566d6-233">資料配量的活動執行會重試總 toohello 指定重試計數。</span><span class="sxs-lookup"><span data-stu-id="566d6-233">Activity execution for a data slice is retried up toohello specified retry count.</span></span> <span data-ttu-id="566d6-234">hello 重試會儘速 hello 失敗後進行。</span><span class="sxs-lookup"><span data-stu-id="566d6-234">hello retry is done as soon as possible after hello failure.</span></span> |
| <span data-ttu-id="566d6-235">timeout</span><span class="sxs-lookup"><span data-stu-id="566d6-235">timeout</span></span> |<span data-ttu-id="566d6-236">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="566d6-236">TimeSpan</span></span> |<span data-ttu-id="566d6-237">00:00:00</span><span class="sxs-lookup"><span data-stu-id="566d6-237">00:00:00</span></span> |<span data-ttu-id="566d6-238">Hello 活動的逾時。</span><span class="sxs-lookup"><span data-stu-id="566d6-238">Timeout for hello activity.</span></span> <span data-ttu-id="566d6-239">範例︰00:10:00 (意指逾時 10 分鐘)</span><span class="sxs-lookup"><span data-stu-id="566d6-239">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="566d6-240">如果未指定值，或為 0，hello 逾時是無限的。</span><span class="sxs-lookup"><span data-stu-id="566d6-240">If a value is not specified or is 0, hello timeout is infinite.</span></span><br/><br/><span data-ttu-id="566d6-241">如果配量的 hello 資料處理時間超過 hello 逾時值，則會取消，並 hello 系統會嘗試 tooretry hello 處理。</span><span class="sxs-lookup"><span data-stu-id="566d6-241">If hello data processing time on a slice exceeds hello timeout value, it is canceled, and hello system attempts tooretry hello processing.</span></span> <span data-ttu-id="566d6-242">hello 重試次數取決於 hello 重試屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-242">hello number of retries depends on hello retry property.</span></span> <span data-ttu-id="566d6-243">發生逾時，hello 狀態會設定 tooTimedOut。</span><span class="sxs-lookup"><span data-stu-id="566d6-243">When timeout occurs, hello status is set tooTimedOut.</span></span> |
| <span data-ttu-id="566d6-244">delay</span><span class="sxs-lookup"><span data-stu-id="566d6-244">delay</span></span> |<span data-ttu-id="566d6-245">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="566d6-245">TimeSpan</span></span> |<span data-ttu-id="566d6-246">00:00:00</span><span class="sxs-lookup"><span data-stu-id="566d6-246">00:00:00</span></span> |<span data-ttu-id="566d6-247">指定 hello hello 配量開始的資料處理之前的延遲。</span><span class="sxs-lookup"><span data-stu-id="566d6-247">Specify hello delay before data processing of hello slice starts.</span></span><br/><br/><span data-ttu-id="566d6-248">hello 延遲 hello 預期執行時間過去後，會啟動 hello 執行之活動的資料配量。</span><span class="sxs-lookup"><span data-stu-id="566d6-248">hello execution of activity for a data slice is started after hello Delay is past hello expected execution time.</span></span><br/><br/><span data-ttu-id="566d6-249">範例︰00:10:00 (意指延遲 10 分鐘)</span><span class="sxs-lookup"><span data-stu-id="566d6-249">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="566d6-250">longRetry</span><span class="sxs-lookup"><span data-stu-id="566d6-250">longRetry</span></span> |<span data-ttu-id="566d6-251">整數 </span><span class="sxs-lookup"><span data-stu-id="566d6-251">Integer</span></span><br/><br/><span data-ttu-id="566d6-252">最大值：10</span><span class="sxs-lookup"><span data-stu-id="566d6-252">Max value: 10</span></span> |<span data-ttu-id="566d6-253">1</span><span class="sxs-lookup"><span data-stu-id="566d6-253">1</span></span> |<span data-ttu-id="566d6-254">hello 的長時間重試次數 hello 配量執行失敗。</span><span class="sxs-lookup"><span data-stu-id="566d6-254">hello number of long retry attempts before hello slice execution is failed.</span></span><br/><br/><span data-ttu-id="566d6-255">多個 longRetry 嘗試之間以 longRetryInterval 隔開。</span><span class="sxs-lookup"><span data-stu-id="566d6-255">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="566d6-256">因此，如果您需要 toospecify 重試嘗試之間的時間，請使用 longRetry。</span><span class="sxs-lookup"><span data-stu-id="566d6-256">So if you need toospecify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="566d6-257">如果指定 Retry 和 longRetry，每個 longRetry 嘗試包含重試次數和 hello 最大嘗試次數為重試 * longRetry。</span><span class="sxs-lookup"><span data-stu-id="566d6-257">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and hello max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="566d6-258">例如，如果我們有下列 hello 活動原則中的設定的 hello:</span><span class="sxs-lookup"><span data-stu-id="566d6-258">For example, if we have hello following settings in hello activity policy:</span></span><br/><span data-ttu-id="566d6-259">Retry：3</span><span class="sxs-lookup"><span data-stu-id="566d6-259">Retry: 3</span></span><br/><span data-ttu-id="566d6-260">longRetry：2</span><span class="sxs-lookup"><span data-stu-id="566d6-260">longRetry: 2</span></span><br/><span data-ttu-id="566d6-261">longRetryInterval：01:00:00</span><span class="sxs-lookup"><span data-stu-id="566d6-261">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="566d6-262">假設有一個配量 tooexecute （等待狀態），就會失敗的每次 hello 活動執行。</span><span class="sxs-lookup"><span data-stu-id="566d6-262">Assume there is only one slice tooexecute (status is Waiting) and hello activity execution fails every time.</span></span> <span data-ttu-id="566d6-263">一開始會有 3 次連續執行嘗試。</span><span class="sxs-lookup"><span data-stu-id="566d6-263">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="566d6-264">每次嘗試之後, hello 配量狀態會是 Retry。</span><span class="sxs-lookup"><span data-stu-id="566d6-264">After each attempt, hello slice status would be Retry.</span></span> <span data-ttu-id="566d6-265">前 3 的嘗試次數已超過之後，hello 配量狀態就會是 LongRetry。</span><span class="sxs-lookup"><span data-stu-id="566d6-265">After first 3 attempts are over, hello slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="566d6-266">一個小時 (也就是 longRetryInteval 的值) 之後，會有另一組 3 次連續執行嘗試。</span><span class="sxs-lookup"><span data-stu-id="566d6-266">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="566d6-267">之後，hello 配量狀態會變成 Failed，而且會嘗試重試。</span><span class="sxs-lookup"><span data-stu-id="566d6-267">After that, hello slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="566d6-268">因此全部已進行 6 次嘗試。</span><span class="sxs-lookup"><span data-stu-id="566d6-268">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="566d6-269">如果執行成功，hello 配量狀態就會是 Ready，無需重試嘗試。</span><span class="sxs-lookup"><span data-stu-id="566d6-269">If any execution succeeds, hello slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="566d6-270">在位置相依的資料到達在不具決定性的時間或 hello 整體環境穩定底下的資料處理發生的情況下可用 longRetry。</span><span class="sxs-lookup"><span data-stu-id="566d6-270">longRetry may be used in situations where dependent data arrives at non-deterministic times or hello overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="566d6-271">在這種情況下，逐一進行重試可能無法幫助，這樣導致 hello 的時間間隔之後想要的輸出。</span><span class="sxs-lookup"><span data-stu-id="566d6-271">In such cases, doing retries one after another may not help and doing so after an interval of time results in hello desired output.</span></span><br/><br/><span data-ttu-id="566d6-272">提醒：請勿設定較大的 longRetry 或 longRetryInterval 值。</span><span class="sxs-lookup"><span data-stu-id="566d6-272">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="566d6-273">較大的值通常表示其他系統問題。</span><span class="sxs-lookup"><span data-stu-id="566d6-273">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="566d6-274">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="566d6-274">longRetryInterval</span></span> |<span data-ttu-id="566d6-275">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="566d6-275">TimeSpan</span></span> |<span data-ttu-id="566d6-276">00:00:00</span><span class="sxs-lookup"><span data-stu-id="566d6-276">00:00:00</span></span> |<span data-ttu-id="566d6-277">hello 長時間重試嘗試之間的延遲</span><span class="sxs-lookup"><span data-stu-id="566d6-277">hello delay between long retry attempts</span></span> |

### <a name="typeproperties-section"></a><span data-ttu-id="566d6-278">typeProperties 區段</span><span class="sxs-lookup"><span data-stu-id="566d6-278">typeProperties section</span></span>
<span data-ttu-id="566d6-279">hello typeProperties 區段是不同的每個活動。</span><span class="sxs-lookup"><span data-stu-id="566d6-279">hello typeProperties section is different for each activity.</span></span> <span data-ttu-id="566d6-280">轉換活動都只是 hello 類型屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-280">Transformation activities have just hello type properties.</span></span> <span data-ttu-id="566d6-281">如需在管線中定義轉換活動的 JSON 範例，請參閱本文中的[資料轉換活動](#data-transformation-activities)一節。</span><span class="sxs-lookup"><span data-stu-id="566d6-281">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span> 

<span data-ttu-id="566d6-282">**複製活動**hello typeProperties > 一節中有兩個子區段：**來源**和**接收**。</span><span class="sxs-lookup"><span data-stu-id="566d6-282">**Copy activity** has two subsections in hello typeProperties section: **source** and **sink**.</span></span> <span data-ttu-id="566d6-283">請參閱[資料存放區](#data-stores)區段在本文中針對 JSON 範例 toouse 資料將儲存為來源及/或接收的方式，顯示。</span><span class="sxs-lookup"><span data-stu-id="566d6-283">See [DATA STORES](#data-stores) section in this article for JSON samples that show how toouse a data store as a source and/or sink.</span></span> 

### <a name="sample-copy-pipeline"></a><span data-ttu-id="566d6-284">範例複製管線</span><span class="sxs-lookup"><span data-stu-id="566d6-284">Sample copy pipeline</span></span>
<span data-ttu-id="566d6-285">在下列範例管線 hello，沒有一個活動的型別**複製**在 hello**活動**> 一節。</span><span class="sxs-lookup"><span data-stu-id="566d6-285">In hello following sample pipeline, there is one activity of type **Copy** in hello **activities** section.</span></span> <span data-ttu-id="566d6-286">在此範例中，hello[複製活動](data-factory-data-movement-activities.md)將資料從 Azure Blob 儲存體 tooan Azure SQL database 複製。</span><span class="sxs-lookup"><span data-stu-id="566d6-286">In this sample, hello [Copy activity](data-factory-data-movement-activities.md) copies data from an Azure Blob storage tooan Azure SQL database.</span></span> 

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
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

<span data-ttu-id="566d6-287">請注意下列點 hello:</span><span class="sxs-lookup"><span data-stu-id="566d6-287">Note hello following points:</span></span>

* <span data-ttu-id="566d6-288">在 [hello 活動] 區段中，沒有一個活動其**類型**設定得**複製**。</span><span class="sxs-lookup"><span data-stu-id="566d6-288">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span>
* <span data-ttu-id="566d6-289">輸入 hello 活動設定太**InputDataset**和輸出 hello 活動設定太**OutputDataset**。</span><span class="sxs-lookup"><span data-stu-id="566d6-289">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span>
* <span data-ttu-id="566d6-290">在 [hello **typeProperties** ] 區段中， **BlobSource**指定 hello 來源類型為和**SqlSink**指定為 hello 接收器類型。</span><span class="sxs-lookup"><span data-stu-id="566d6-290">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span>

<span data-ttu-id="566d6-291">請參閱[資料存放區](#data-stores)區段在本文中針對 JSON 範例 toouse 資料將儲存為來源及/或接收的方式，顯示。</span><span class="sxs-lookup"><span data-stu-id="566d6-291">See [DATA STORES](#data-stores) section in this article for JSON samples that show how toouse a data store as a source and/or sink.</span></span>    

<span data-ttu-id="566d6-292">建立此管線的完整逐步解說，請參閱[教學課程： 將資料從 Blob 儲存體 tooSQL 資料庫複製](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="566d6-292">For a complete walkthrough of creating this pipeline, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

### <a name="sample-transformation-pipeline"></a><span data-ttu-id="566d6-293">範例轉換管線</span><span class="sxs-lookup"><span data-stu-id="566d6-293">Sample transformation pipeline</span></span>
<span data-ttu-id="566d6-294">在下列範例管線 hello，沒有一個活動的型別**HDInsightHive**在 hello**活動**> 一節。</span><span class="sxs-lookup"><span data-stu-id="566d6-294">In hello following sample pipeline, there is one activity of type **HDInsightHive** in hello **activities** section.</span></span> <span data-ttu-id="566d6-295">在此範例中，hello [HDInsight Hive 活動](data-factory-hive-activity.md)執行 Azure HDInsight Hadoop 叢集上的 Hive 指令碼檔案來轉換資料從 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="566d6-295">In this sample, hello [HDInsight Hive activity](data-factory-hive-activity.md) transforms data from an Azure Blob storage by running a Hive script file on an Azure HDInsight Hadoop cluster.</span></span> 

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

<span data-ttu-id="566d6-296">請注意下列點 hello:</span><span class="sxs-lookup"><span data-stu-id="566d6-296">Note hello following points:</span></span> 

* <span data-ttu-id="566d6-297">在 [hello 活動] 區段中，沒有一個活動其**類型**設定得**HDInsightHive**。</span><span class="sxs-lookup"><span data-stu-id="566d6-297">In hello activities section, there is only one activity whose **type** is set too**HDInsightHive**.</span></span>
* <span data-ttu-id="566d6-298">hello Hive 指令碼檔案， **partitionweblogs.hql**，儲存在 hello Azure 儲存體帳戶 (由 hello scriptLinkedService，稱為**AzureStorageLinkedService**)，然後在**指令碼**hello 容器中的資料夾**adfgetstarted**。</span><span class="sxs-lookup"><span data-stu-id="566d6-298">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>
* <span data-ttu-id="566d6-299">hello**定義**區段是做為 Hive 組態值傳遞 toohello hive 指令碼使用的 toospecify hello 執行階段設定 (例如`${hiveconf:inputtable}`， `${hiveconf:partitionedtable}`)。</span><span class="sxs-lookup"><span data-stu-id="566d6-299">hello **defines** section is used toospecify hello runtime settings that are passed toohello hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span></span>

<span data-ttu-id="566d6-300">如需在管線中定義轉換活動的 JSON 範例，請參閱本文中的[資料轉換活動](#data-transformation-activities)一節。</span><span class="sxs-lookup"><span data-stu-id="566d6-300">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span>

<span data-ttu-id="566d6-301">建立此管線的完整逐步解說，請參閱[教學課程： 建立第一個管線 tooprocess 資料使用 Hadoop 叢集](data-factory-build-your-first-pipeline.md)。</span><span class="sxs-lookup"><span data-stu-id="566d6-301">For a complete walkthrough of creating this pipeline, see [Tutorial: Build your first pipeline tooprocess data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="linked-service"></a><span data-ttu-id="566d6-302">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-302">Linked service</span></span>
<span data-ttu-id="566d6-303">如需連結的服務定義 hello 高階結構如下所示：</span><span class="sxs-lookup"><span data-stu-id="566d6-303">hello high-level structure for a linked service definition is as follows:</span></span>

```json
{
    "name": "<name of hello linked service>",
    "properties": {
        "type": "<type of hello linked service>",
        "typeProperties": {
        }
    }
}
```

<span data-ttu-id="566d6-304">下列表格說明 hello 活動 JSON 定義中的 hello 屬性：</span><span class="sxs-lookup"><span data-stu-id="566d6-304">Following table describe hello properties within hello activity JSON definition:</span></span>

| <span data-ttu-id="566d6-305">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-305">Property</span></span> | <span data-ttu-id="566d6-306">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-306">Description</span></span> | <span data-ttu-id="566d6-307">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-307">Required</span></span> |
| -------- | ----------- | -------- | 
| <span data-ttu-id="566d6-308">名稱</span><span class="sxs-lookup"><span data-stu-id="566d6-308">name</span></span> | <span data-ttu-id="566d6-309">Hello 連結服務名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-309">Name of hello linked service.</span></span> | <span data-ttu-id="566d6-310">是</span><span class="sxs-lookup"><span data-stu-id="566d6-310">Yes</span></span> | 
| <span data-ttu-id="566d6-311">properties - type</span><span class="sxs-lookup"><span data-stu-id="566d6-311">properties - type</span></span> | <span data-ttu-id="566d6-312">Hello 連結服務類型。</span><span class="sxs-lookup"><span data-stu-id="566d6-312">Type of hello linked service.</span></span> <span data-ttu-id="566d6-313">例如︰Azure 儲存體、Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="566d6-313">For example: Azure Storage, Azure SQL Database.</span></span> |
| <span data-ttu-id="566d6-314">typeProperties</span><span class="sxs-lookup"><span data-stu-id="566d6-314">typeProperties</span></span> | <span data-ttu-id="566d6-315">hello typeProperties 區段具有不同的每個資料存放區或計算環境的項目。</span><span class="sxs-lookup"><span data-stu-id="566d6-315">hello typeProperties section has elements that are different for each data store or compute environment.</span></span> <span data-ttu-id="566d6-316">請參閱[資料存放區](#datastores)區段中針對所有的 hello 資料存放區連結的服務和[計算環境](#compute-environments)所有 hello 計算連結的服務</span><span class="sxs-lookup"><span data-stu-id="566d6-316">See [data stores](#datastores) section for all hello data store linked services and [compute environments](#compute-environments) for all hello compute linked services</span></span> |   

## <a name="dataset"></a><span data-ttu-id="566d6-317">Dataset</span><span class="sxs-lookup"><span data-stu-id="566d6-317">Dataset</span></span> 
<span data-ttu-id="566d6-318">Azure Data Factory 中的資料集定義如下：</span><span class="sxs-lookup"><span data-stu-id="566d6-318">A dataset in Azure Data Factory is defined as follows:</span></span>

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

<span data-ttu-id="566d6-319">hello 下表描述上方 JSON hello 中的屬性：</span><span class="sxs-lookup"><span data-stu-id="566d6-319">hello following table describes properties in hello above JSON:</span></span>   

| <span data-ttu-id="566d6-320">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-320">Property</span></span> | <span data-ttu-id="566d6-321">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-321">Description</span></span> | <span data-ttu-id="566d6-322">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-322">Required</span></span> | <span data-ttu-id="566d6-323">預設值</span><span class="sxs-lookup"><span data-stu-id="566d6-323">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-324">名稱</span><span class="sxs-lookup"><span data-stu-id="566d6-324">name</span></span> | <span data-ttu-id="566d6-325">Hello 資料集的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-325">Name of hello dataset.</span></span> <span data-ttu-id="566d6-326">請參閱 [Azure Data Factory - 命名規則](data-factory-naming-rules.md) ，以了解命名規則。</span><span class="sxs-lookup"><span data-stu-id="566d6-326">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="566d6-327">是</span><span class="sxs-lookup"><span data-stu-id="566d6-327">Yes</span></span> |<span data-ttu-id="566d6-328">NA</span><span class="sxs-lookup"><span data-stu-id="566d6-328">NA</span></span> |
| <span data-ttu-id="566d6-329">類型</span><span class="sxs-lookup"><span data-stu-id="566d6-329">type</span></span> | <span data-ttu-id="566d6-330">hello 資料集的類型。</span><span class="sxs-lookup"><span data-stu-id="566d6-330">Type of hello dataset.</span></span> <span data-ttu-id="566d6-331">指定一個支援的 Azure Data Factory 的 hello 類型 (例如： AzureBlob、 AzureSqlTable)。</span><span class="sxs-lookup"><span data-stu-id="566d6-331">Specify one of hello types supported by Azure Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <span data-ttu-id="566d6-332">請參閱[資料存放區](#data-stores)區段中針對所有 hello 資料存放區和資料處理站所支援的資料集類型。</span><span class="sxs-lookup"><span data-stu-id="566d6-332">See [DATA STORES](#data-stores) section for all hello data stores and dataset types supported by Data Factory.</span></span> | 
| <span data-ttu-id="566d6-333">structure</span><span class="sxs-lookup"><span data-stu-id="566d6-333">structure</span></span> | <span data-ttu-id="566d6-334">Hello 資料集的結構描述。</span><span class="sxs-lookup"><span data-stu-id="566d6-334">Schema of hello dataset.</span></span> <span data-ttu-id="566d6-335">它包含資料行、其類型等。</span><span class="sxs-lookup"><span data-stu-id="566d6-335">It contains columns, their types, etc.</span></span> | <span data-ttu-id="566d6-336">否</span><span class="sxs-lookup"><span data-stu-id="566d6-336">No</span></span> |<span data-ttu-id="566d6-337">NA</span><span class="sxs-lookup"><span data-stu-id="566d6-337">NA</span></span> |
| <span data-ttu-id="566d6-338">typeProperties</span><span class="sxs-lookup"><span data-stu-id="566d6-338">typeProperties</span></span> | <span data-ttu-id="566d6-339">屬性對應 toohello 選取型別。</span><span class="sxs-lookup"><span data-stu-id="566d6-339">Properties corresponding toohello selected type.</span></span> <span data-ttu-id="566d6-340">關於支援的類型和其屬性，請參閱[資料存放區](#data-stores)一節。</span><span class="sxs-lookup"><span data-stu-id="566d6-340">See [DATA STORES](#data-stores) section for supported types and their properties.</span></span> |<span data-ttu-id="566d6-341">是</span><span class="sxs-lookup"><span data-stu-id="566d6-341">Yes</span></span> |<span data-ttu-id="566d6-342">NA</span><span class="sxs-lookup"><span data-stu-id="566d6-342">NA</span></span> |
| <span data-ttu-id="566d6-343">external</span><span class="sxs-lookup"><span data-stu-id="566d6-343">external</span></span> | <span data-ttu-id="566d6-344">布林值旗標 toospecify，是否與否，資料 factory 管線所明確產生資料集。</span><span class="sxs-lookup"><span data-stu-id="566d6-344">Boolean flag toospecify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> |<span data-ttu-id="566d6-345">否</span><span class="sxs-lookup"><span data-stu-id="566d6-345">No</span></span> |<span data-ttu-id="566d6-346">false</span><span class="sxs-lookup"><span data-stu-id="566d6-346">false</span></span> |
| <span data-ttu-id="566d6-347">Availability</span><span class="sxs-lookup"><span data-stu-id="566d6-347">availability</span></span> | <span data-ttu-id="566d6-348">定義處理期間，或者 hello 配量模型 hello 資料集的生產環境的 hello。</span><span class="sxs-lookup"><span data-stu-id="566d6-348">Defines hello processing window or hello slicing model for hello dataset production.</span></span> <span data-ttu-id="566d6-349">Hello 資料集配量模型的詳細資訊，請參閱[排程與執行](data-factory-scheduling-and-execution.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="566d6-349">For details on hello dataset slicing model, see [Scheduling and Execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="566d6-350">是</span><span class="sxs-lookup"><span data-stu-id="566d6-350">Yes</span></span> |<span data-ttu-id="566d6-351">NA</span><span class="sxs-lookup"><span data-stu-id="566d6-351">NA</span></span> |
| <span data-ttu-id="566d6-352">原則</span><span class="sxs-lookup"><span data-stu-id="566d6-352">policy</span></span> |<span data-ttu-id="566d6-353">定義 hello 準則或 hello hello 資料集配量，都必須符合的條件。</span><span class="sxs-lookup"><span data-stu-id="566d6-353">Defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="566d6-354">如需詳細資訊，請參閱 [資料集原則](#Policy) 一節。</span><span class="sxs-lookup"><span data-stu-id="566d6-354">For details, see [Dataset Policy](#Policy) section.</span></span> |<span data-ttu-id="566d6-355">否</span><span class="sxs-lookup"><span data-stu-id="566d6-355">No</span></span> |<span data-ttu-id="566d6-356">NA</span><span class="sxs-lookup"><span data-stu-id="566d6-356">NA</span></span> |

<span data-ttu-id="566d6-357">每個資料行中 hello**結構**區段包含下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="566d6-357">Each column in hello **structure** section contains hello following properties:</span></span>

| <span data-ttu-id="566d6-358">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-358">Property</span></span> | <span data-ttu-id="566d6-359">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-359">Description</span></span> | <span data-ttu-id="566d6-360">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-360">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-361">名稱</span><span class="sxs-lookup"><span data-stu-id="566d6-361">name</span></span> |<span data-ttu-id="566d6-362">Hello 資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-362">Name of hello column.</span></span> |<span data-ttu-id="566d6-363">是</span><span class="sxs-lookup"><span data-stu-id="566d6-363">Yes</span></span> |
| <span data-ttu-id="566d6-364">類型</span><span class="sxs-lookup"><span data-stu-id="566d6-364">type</span></span> |<span data-ttu-id="566d6-365">Hello 資料行資料類型。</span><span class="sxs-lookup"><span data-stu-id="566d6-365">Data type of hello column.</span></span>  |<span data-ttu-id="566d6-366">否</span><span class="sxs-lookup"><span data-stu-id="566d6-366">No</span></span> |
| <span data-ttu-id="566d6-367">culture</span><span class="sxs-lookup"><span data-stu-id="566d6-367">culture</span></span> |<span data-ttu-id="566d6-368">.NET 基礎類型指定且為.NET 型別時使用的文化特性 toobe`Datetime`或`Datetimeoffset`。</span><span class="sxs-lookup"><span data-stu-id="566d6-368">.NET based culture toobe used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="566d6-369">預設值為 `en-us`。</span><span class="sxs-lookup"><span data-stu-id="566d6-369">Default is `en-us`.</span></span> |<span data-ttu-id="566d6-370">否</span><span class="sxs-lookup"><span data-stu-id="566d6-370">No</span></span> |
| <span data-ttu-id="566d6-371">format</span><span class="sxs-lookup"><span data-stu-id="566d6-371">format</span></span> |<span data-ttu-id="566d6-372">格式化指定類型，並為.NET 型別時所使用的字串 toobe`Datetime`或`Datetimeoffset`。</span><span class="sxs-lookup"><span data-stu-id="566d6-372">Format string toobe used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="566d6-373">否</span><span class="sxs-lookup"><span data-stu-id="566d6-373">No</span></span> |

<span data-ttu-id="566d6-374">在下列範例的 hello，hello 資料集有三個資料行`slicetimestamp`， `projectname`，和`pageviews`，而且它們的型別： 字串、 字串和小數點分別。</span><span class="sxs-lookup"><span data-stu-id="566d6-374">In hello following example, hello dataset has three columns `slicetimestamp`, `projectname`, and `pageviews` and they are of type: String, String, and Decimal respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="566d6-375">hello 下表描述您可以使用在 hello 屬性**可用性**> 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-375">hello following table describes properties you can use in hello **availability** section:</span></span>

| <span data-ttu-id="566d6-376">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-376">Property</span></span> | <span data-ttu-id="566d6-377">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-377">Description</span></span> | <span data-ttu-id="566d6-378">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-378">Required</span></span> | <span data-ttu-id="566d6-379">預設值</span><span class="sxs-lookup"><span data-stu-id="566d6-379">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-380">frequency</span><span class="sxs-lookup"><span data-stu-id="566d6-380">frequency</span></span> |<span data-ttu-id="566d6-381">指定資料集配量實際執行環境的 hello 時間單位。</span><span class="sxs-lookup"><span data-stu-id="566d6-381">Specifies hello time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="566d6-382"><b>支援的頻率</b>：Minute、Hour、Day、Week、Month</span><span class="sxs-lookup"><span data-stu-id="566d6-382"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="566d6-383">是</span><span class="sxs-lookup"><span data-stu-id="566d6-383">Yes</span></span> |<span data-ttu-id="566d6-384">NA</span><span class="sxs-lookup"><span data-stu-id="566d6-384">NA</span></span> |
| <span data-ttu-id="566d6-385">interval</span><span class="sxs-lookup"><span data-stu-id="566d6-385">interval</span></span> |<span data-ttu-id="566d6-386">指定頻率的倍數</span><span class="sxs-lookup"><span data-stu-id="566d6-386">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="566d6-387">[頻率 x 間隔] 判斷頻率 hello 產生配量。</span><span class="sxs-lookup"><span data-stu-id="566d6-387">”Frequency x interval” determines how often hello slice is produced.</span></span><br/><br/><span data-ttu-id="566d6-388">如果您需要 hello 配量每小時的資料集 toobe，設定<b>頻率</b>太<b>小時</b>，和<b>間隔</b>太<b>1</b>。</span><span class="sxs-lookup"><span data-stu-id="566d6-388">If you need hello dataset toobe sliced on an hourly basis, you set <b>Frequency</b> too<b>Hour</b>, and <b>interval</b> too<b>1</b>.</span></span><br/><br/><span data-ttu-id="566d6-389"><b>請注意</b>： 如果您將 Frequency 指定為 Minute，我們建議您設定小於 15 的 hello 間隔 toono</span><span class="sxs-lookup"><span data-stu-id="566d6-389"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set hello interval toono less than 15</span></span> |<span data-ttu-id="566d6-390">是</span><span class="sxs-lookup"><span data-stu-id="566d6-390">Yes</span></span> |<span data-ttu-id="566d6-391">NA</span><span class="sxs-lookup"><span data-stu-id="566d6-391">NA</span></span> |
| <span data-ttu-id="566d6-392">style</span><span class="sxs-lookup"><span data-stu-id="566d6-392">style</span></span> |<span data-ttu-id="566d6-393">指定是否應該在 hello 開始/結束 hello 間隔產生 hello 配量。</span><span class="sxs-lookup"><span data-stu-id="566d6-393">Specifies whether hello slice should be produced at hello start/end of hello interval.</span></span><ul><li><span data-ttu-id="566d6-394">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="566d6-394">StartOfInterval</span></span></li><li><span data-ttu-id="566d6-395">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="566d6-395">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="566d6-396">如果頻率設定 tooMonth 樣式設定 tooEndOfInterval，hello 當月最後一天產生 hello 配量。</span><span class="sxs-lookup"><span data-stu-id="566d6-396">If Frequency is set tooMonth and style is set tooEndOfInterval, hello slice is produced on hello last day of month.</span></span> <span data-ttu-id="566d6-397">如果 hello 樣式設定 tooStartOfInterval，hello 點產生配量 hello 當月第一日。</span><span class="sxs-lookup"><span data-stu-id="566d6-397">If hello style is set tooStartOfInterval, hello slice is produced on hello first day of month.</span></span><br/><br/><span data-ttu-id="566d6-398">如果頻率設定 tooDay tooEndOfInterval 設定樣式時，會產生 hello 的 hello 當日的前一個小時 hello 配量。</span><span class="sxs-lookup"><span data-stu-id="566d6-398">If Frequency is set tooDay and style is set tooEndOfInterval, hello slice is produced in hello last hour of hello day.</span></span><br/><br/><span data-ttu-id="566d6-399">如果頻率設定 tooHour 樣式設定 tooEndOfInterval，hello 配量會產生在 hello hello 小時結尾。</span><span class="sxs-lookup"><span data-stu-id="566d6-399">If Frequency is set tooHour and style is set tooEndOfInterval, hello slice is produced at hello end of hello hour.</span></span> <span data-ttu-id="566d6-400">例如，1 PM – 2 PM 期間的配量，hello 配量會在 2 PM 產生。</span><span class="sxs-lookup"><span data-stu-id="566d6-400">For example, for a slice for 1 PM – 2 PM period, hello slice is produced at 2 PM.</span></span> |<span data-ttu-id="566d6-401">否</span><span class="sxs-lookup"><span data-stu-id="566d6-401">No</span></span> |<span data-ttu-id="566d6-402">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="566d6-402">EndOfInterval</span></span> |
| <span data-ttu-id="566d6-403">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="566d6-403">anchorDateTime</span></span> |<span data-ttu-id="566d6-404">定義中使用的排程器 toocompute 資料集配量界限時間 hello 絕對位置。</span><span class="sxs-lookup"><span data-stu-id="566d6-404">Defines hello absolute position in time used by scheduler toocompute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="566d6-405"><b>請注意</b>： 如果 hello AnchorDateTime 具有比 hello 頻率較精細的日期部分，則 hello 更精細的部分會被忽略。</span><span class="sxs-lookup"><span data-stu-id="566d6-405"><b>Note</b>: If hello AnchorDateTime has date parts that are more granular than hello frequency then hello more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="566d6-406">例如，如果 hello<b>間隔</b>是<b>每小時</b>(頻率： hour，interval: 1) 和 hello <b>AnchorDateTime</b>包含<b>分鐘和秒鐘</b>然後 hello<b>分鐘和秒鐘</b>hello AnchorDateTime 的部分會被忽略。</span><span class="sxs-lookup"><span data-stu-id="566d6-406">For example, if hello <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and hello <b>AnchorDateTime</b> contains <b>minutes and seconds</b> then hello <b>minutes and seconds</b> parts of hello AnchorDateTime are ignored.</span></span> |<span data-ttu-id="566d6-407">否</span><span class="sxs-lookup"><span data-stu-id="566d6-407">No</span></span> |<span data-ttu-id="566d6-408">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="566d6-408">01/01/0001</span></span> |
| <span data-ttu-id="566d6-409">Offset</span><span class="sxs-lookup"><span data-stu-id="566d6-409">offset</span></span> |<span data-ttu-id="566d6-410">哪些 hello 的所有資料集配量的開始與結束移位的 Timespan。</span><span class="sxs-lookup"><span data-stu-id="566d6-410">Timespan by which hello start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="566d6-411"><b>請注意</b>: hello 結果指定 anchorDateTime 和 offset，如果是合併的 hello 移位。</span><span class="sxs-lookup"><span data-stu-id="566d6-411"><b>Note</b>: If both anchorDateTime and offset are specified, hello result is hello combined shift.</span></span> |<span data-ttu-id="566d6-412">否</span><span class="sxs-lookup"><span data-stu-id="566d6-412">No</span></span> |<span data-ttu-id="566d6-413">NA</span><span class="sxs-lookup"><span data-stu-id="566d6-413">NA</span></span> |

<span data-ttu-id="566d6-414">下列可用性一節的 hello 指定該 hello 輸出資料集則為產生每小時 （或） 的輸入資料集是每小時可用：</span><span class="sxs-lookup"><span data-stu-id="566d6-414">hello following availability section specifies that hello output dataset is either produced hourly (or) input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="566d6-415">hello**原則**資料集定義中的區段會定義 hello 準則或 hello 資料集配量的 hello 條件必須滿足。</span><span class="sxs-lookup"><span data-stu-id="566d6-415">hello **policy** section in dataset definition defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span>

| <span data-ttu-id="566d6-416">原則名稱</span><span class="sxs-lookup"><span data-stu-id="566d6-416">Policy Name</span></span> | <span data-ttu-id="566d6-417">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-417">Description</span></span> | <span data-ttu-id="566d6-418">套用太</span><span class="sxs-lookup"><span data-stu-id="566d6-418">Applied too</span></span>| <span data-ttu-id="566d6-419">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-419">Required</span></span> | <span data-ttu-id="566d6-420">預設值</span><span class="sxs-lookup"><span data-stu-id="566d6-420">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="566d6-421">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="566d6-421">minimumSizeMB</span></span> |<span data-ttu-id="566d6-422">驗證中的 hello 資料**Azure blob**符合 hello 最小大小需求 （以 mb 為單位）。</span><span class="sxs-lookup"><span data-stu-id="566d6-422">Validates that hello data in an **Azure blob** meets hello minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="566d6-423">Azure Blob</span><span class="sxs-lookup"><span data-stu-id="566d6-423">Azure Blob</span></span> |<span data-ttu-id="566d6-424">否</span><span class="sxs-lookup"><span data-stu-id="566d6-424">No</span></span> |<span data-ttu-id="566d6-425">NA</span><span class="sxs-lookup"><span data-stu-id="566d6-425">NA</span></span> |
| <span data-ttu-id="566d6-426">minimumRows</span><span class="sxs-lookup"><span data-stu-id="566d6-426">minimumRows</span></span> |<span data-ttu-id="566d6-427">驗證中的 hello 資料**Azure SQL database**或**Azure 資料表**包含 hello 最小數目的資料列。</span><span class="sxs-lookup"><span data-stu-id="566d6-427">Validates that hello data in an **Azure SQL database** or an **Azure table** contains hello minimum number of rows.</span></span> |<ul><li><span data-ttu-id="566d6-428">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="566d6-428">Azure SQL Database</span></span></li><li><span data-ttu-id="566d6-429">Azure 資料表</span><span class="sxs-lookup"><span data-stu-id="566d6-429">Azure Table</span></span></li></ul> |<span data-ttu-id="566d6-430">否</span><span class="sxs-lookup"><span data-stu-id="566d6-430">No</span></span> |<span data-ttu-id="566d6-431">NA</span><span class="sxs-lookup"><span data-stu-id="566d6-431">NA</span></span> |

<span data-ttu-id="566d6-432">**範例：**</span><span class="sxs-lookup"><span data-stu-id="566d6-432">**Example:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="566d6-433">除非資料集是由 Azure Data Factory 產生，否則應該標示為 **外部**。</span><span class="sxs-lookup"><span data-stu-id="566d6-433">Unless a dataset is being produced by Azure Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="566d6-434">除非正在使用活動或管線鏈結，這項設定通常適用於 toohello 輸入管線中的第一個活動。</span><span class="sxs-lookup"><span data-stu-id="566d6-434">This setting generally applies toohello inputs of first activity in a pipeline unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="566d6-435">名稱</span><span class="sxs-lookup"><span data-stu-id="566d6-435">Name</span></span> | <span data-ttu-id="566d6-436">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-436">Description</span></span> | <span data-ttu-id="566d6-437">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-437">Required</span></span> | <span data-ttu-id="566d6-438">預設值</span><span class="sxs-lookup"><span data-stu-id="566d6-438">Default Value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-439">dataDelay</span><span class="sxs-lookup"><span data-stu-id="566d6-439">dataDelay</span></span> |<span data-ttu-id="566d6-440">時間 toodelay hello hello 可用性檢查的 hello hello 指定配量的外部資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-440">Time toodelay hello check on hello availability of hello external data for hello given slice.</span></span> <span data-ttu-id="566d6-441">例如，如果 hello 資料可每小時、 hello 檢查 toosee hello 外部資料而且 hello 對應配量已備妥可以延遲使用 dataDelay。</span><span class="sxs-lookup"><span data-stu-id="566d6-441">For example, if hello data is available hourly, hello check toosee hello external data is available and hello corresponding slice is Ready can be delayed by using dataDelay.</span></span><br/><br/><span data-ttu-id="566d6-442">僅適用於 toohello 目前的時間。</span><span class="sxs-lookup"><span data-stu-id="566d6-442">Only applies toohello present time.</span></span>  <span data-ttu-id="566d6-443">例如，如果它是 1:00 PM 現在，這個值為 10 分鐘 hello 驗證就會開始 1:10 PM。</span><span class="sxs-lookup"><span data-stu-id="566d6-443">For example, if it is 1:00 PM right now and this value is 10 minutes, hello validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="566d6-444">此設定不會影響在 hello 過去的配量 (以配量結束的時間 + dataDelay 的配量 < 現在) 會處理沒有任何延遲。</span><span class="sxs-lookup"><span data-stu-id="566d6-444">This setting does not affect slices in hello past (slices with Slice End Time + dataDelay < Now) are processed without any delay.</span></span><br/><br/><span data-ttu-id="566d6-445">時間大於 23:59 小時需要使用 hello toospecified`day.hours:minutes:seconds`格式。</span><span class="sxs-lookup"><span data-stu-id="566d6-445">Time greater than 23:59 hours need toospecified using hello `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="566d6-446">例如，toospecify 24 小時，請勿使用 24:00:00。請改用 1.00:00:00。</span><span class="sxs-lookup"><span data-stu-id="566d6-446">For example, toospecify 24 hours, don't use 24:00:00; instead, use 1.00:00:00.</span></span> <span data-ttu-id="566d6-447">如果您使用 24:00:00，這會視同 24 天 (24.00:00:00)。</span><span class="sxs-lookup"><span data-stu-id="566d6-447">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="566d6-448">如為 1 天又 4 小時，請指定 1:04:00:00。</span><span class="sxs-lookup"><span data-stu-id="566d6-448">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="566d6-449">否</span><span class="sxs-lookup"><span data-stu-id="566d6-449">No</span></span> |<span data-ttu-id="566d6-450">0</span><span class="sxs-lookup"><span data-stu-id="566d6-450">0</span></span> |
| <span data-ttu-id="566d6-451">retryInterval</span><span class="sxs-lookup"><span data-stu-id="566d6-451">retryInterval</span></span> |<span data-ttu-id="566d6-452">hello 失敗與 hello 下一次的重試嘗試之間的等待時間。</span><span class="sxs-lookup"><span data-stu-id="566d6-452">hello wait time between a failure and hello next retry attempt.</span></span> <span data-ttu-id="566d6-453">如果嘗試會失敗，retryInterval 之後便為 hello 下一步 再試一次。</span><span class="sxs-lookup"><span data-stu-id="566d6-453">If a try fails, hello next try is after retryInterval.</span></span> <br/><br/><span data-ttu-id="566d6-454">如果是 1:00 PM 現在，我們會開始 hello 第一次嘗試。</span><span class="sxs-lookup"><span data-stu-id="566d6-454">If it is 1:00 PM right now, we begin hello first try.</span></span> <span data-ttu-id="566d6-455">Hello 下次重試 hello 持續時間 toocomplete hello 第一次驗證檢查是 1 分鐘而且 hello 作業失敗，如果是在 1:00 + 1 分鐘 （持續時間） + 1 分鐘 （重試間隔） = 1: 02PM。</span><span class="sxs-lookup"><span data-stu-id="566d6-455">If hello duration toocomplete hello first validation check is 1 minute and hello operation failed, hello next retry is at 1:00 + 1 min (duration) + 1 min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="566d6-456">在 hello 過去的配量，沒有任何延遲。</span><span class="sxs-lookup"><span data-stu-id="566d6-456">For slices in hello past, there is no delay.</span></span> <span data-ttu-id="566d6-457">hello 重試會立即發生。</span><span class="sxs-lookup"><span data-stu-id="566d6-457">hello retry happens immediately.</span></span> |<span data-ttu-id="566d6-458">否</span><span class="sxs-lookup"><span data-stu-id="566d6-458">No</span></span> |<span data-ttu-id="566d6-459">00:01:00 (1 分鐘)</span><span class="sxs-lookup"><span data-stu-id="566d6-459">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="566d6-460">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="566d6-460">retryTimeout</span></span> |<span data-ttu-id="566d6-461">每次重試的 hello 逾時。</span><span class="sxs-lookup"><span data-stu-id="566d6-461">hello timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="566d6-462">如果這個屬性設定 too10 分鐘 hello 驗證需求 toobe 10 分鐘內完成。</span><span class="sxs-lookup"><span data-stu-id="566d6-462">If this property is set too10 minutes, hello validation needs toobe completed within 10 minutes.</span></span> <span data-ttu-id="566d6-463">如果需花時間超過 10 分鐘 tooperform hello 驗證，hello 重試逾時。</span><span class="sxs-lookup"><span data-stu-id="566d6-463">If it takes longer than 10 minutes tooperform hello validation, hello retry times out.</span></span><br/><br/><span data-ttu-id="566d6-464">如果所有嘗試都 hello 驗證都逾時，hello 配量會標示為已逾時。</span><span class="sxs-lookup"><span data-stu-id="566d6-464">If all attempts for hello validation times out, hello slice is marked as TimedOut.</span></span> |<span data-ttu-id="566d6-465">否</span><span class="sxs-lookup"><span data-stu-id="566d6-465">No</span></span> |<span data-ttu-id="566d6-466">00:10:00 (10 分鐘)</span><span class="sxs-lookup"><span data-stu-id="566d6-466">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="566d6-467">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="566d6-467">maximumRetry</span></span> |<span data-ttu-id="566d6-468">次數 toocheck hello hello 外部資料可用性。</span><span class="sxs-lookup"><span data-stu-id="566d6-468">Number of times toocheck for hello availability of hello external data.</span></span> <span data-ttu-id="566d6-469">hello 允許最大值為 10。</span><span class="sxs-lookup"><span data-stu-id="566d6-469">hello allowed maximum value is 10.</span></span> |<span data-ttu-id="566d6-470">否</span><span class="sxs-lookup"><span data-stu-id="566d6-470">No</span></span> |<span data-ttu-id="566d6-471">3</span><span class="sxs-lookup"><span data-stu-id="566d6-471">3</span></span> |


## <a name="data-stores"></a><span data-ttu-id="566d6-472">資料存放區</span><span class="sxs-lookup"><span data-stu-id="566d6-472">DATA STORES</span></span>
<span data-ttu-id="566d6-473">hello[連結服務](#linked-service)> 一節提供描述常見的 tooall 類型的連結服務的 JSON 元素。</span><span class="sxs-lookup"><span data-stu-id="566d6-473">hello [Linked service](#linked-service) section provided descriptions for JSON elements that are common tooall types of linked services.</span></span> <span data-ttu-id="566d6-474">本節提供有關屬於特定 tooeach 資料存放區的 JSON 元素的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-474">This section provides details about JSON elements that are specific tooeach data store.</span></span>

<span data-ttu-id="566d6-475">hello[資料集](#dataset)是常見的資料集的 tooall 類型的 JSON 元素 > 一節提供描述。</span><span class="sxs-lookup"><span data-stu-id="566d6-475">hello [Dataset](#dataset) section provided descriptions for JSON elements that are common tooall types of datasets.</span></span> <span data-ttu-id="566d6-476">本節提供有關屬於特定 tooeach 資料存放區的 JSON 元素的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-476">This section provides details about JSON elements that are specific tooeach data store.</span></span>

<span data-ttu-id="566d6-477">hello[活動](#activity)是常見的活動 tooall 類型的 JSON 元素 > 一節提供描述。</span><span class="sxs-lookup"><span data-stu-id="566d6-477">hello [Activity](#activity) section provided descriptions for JSON elements that are common tooall types of activities.</span></span> <span data-ttu-id="566d6-478">本節提供有關特定 tooeach 資料存放區時，它會當做來源/接收器複製活動中使用的 JSON 元素的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-478">This section provides details about JSON elements that are specific tooeach data store when it is used as a source/sink in a copy activity.</span></span>  

<span data-ttu-id="566d6-479">按一下 hello hello 存放區中，使用您感興趣 toosee hello JSON 結構描述連結的服務，資料集，以及 hello 來源/接收器 hello 複製活動的連結。</span><span class="sxs-lookup"><span data-stu-id="566d6-479">Click hello link for hello store you are interested in toosee hello JSON schemas for linked service, dataset, and hello source/sink for hello copy activity.</span></span>

| <span data-ttu-id="566d6-480">類別</span><span class="sxs-lookup"><span data-stu-id="566d6-480">Category</span></span> | <span data-ttu-id="566d6-481">資料存放區</span><span class="sxs-lookup"><span data-stu-id="566d6-481">Data store</span></span> 
|:--- |:--- |
| <span data-ttu-id="566d6-482">**Azure**</span><span class="sxs-lookup"><span data-stu-id="566d6-482">**Azure**</span></span> |[<span data-ttu-id="566d6-483">Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="566d6-483">Azure Blob storage</span></span>](#azure-blob-storage) |
| &nbsp; |[<span data-ttu-id="566d6-484">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="566d6-484">Azure Data Lake Store</span></span>](#azure-datalake-store) |
| &nbsp; |[<span data-ttu-id="566d6-485">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="566d6-485">Azure Cosmos DB</span></span>](#azure-cosmos-db) |
| &nbsp; |[<span data-ttu-id="566d6-486">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="566d6-486">Azure SQL Database</span></span>](#azure-sql-database) |
| &nbsp; |[<span data-ttu-id="566d6-487">Azure SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="566d6-487">Azure SQL Data Warehouse</span></span>](#azure-sql-data-warehouse) |
| &nbsp; |[<span data-ttu-id="566d6-488">Azure 搜尋服務</span><span class="sxs-lookup"><span data-stu-id="566d6-488">Azure Search</span></span>](#azure-search) |
| &nbsp; |[<span data-ttu-id="566d6-489">Azure 表格儲存體</span><span class="sxs-lookup"><span data-stu-id="566d6-489">Azure Table storage</span></span>](#azure-table-storage) |
| <span data-ttu-id="566d6-490">**資料庫**</span><span class="sxs-lookup"><span data-stu-id="566d6-490">**Databases**</span></span> |[<span data-ttu-id="566d6-491">Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="566d6-491">Amazon Redshift</span></span>](#amazon-redshift) |
| &nbsp; |[<span data-ttu-id="566d6-492">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="566d6-492">IBM DB2</span></span>](#ibm-db2) |
| &nbsp; |[<span data-ttu-id="566d6-493">MySQL</span><span class="sxs-lookup"><span data-stu-id="566d6-493">MySQL</span></span>](#mysql) |
| &nbsp; |[<span data-ttu-id="566d6-494">Oracle</span><span class="sxs-lookup"><span data-stu-id="566d6-494">Oracle</span></span>](#oracle) |
| &nbsp; |[<span data-ttu-id="566d6-495">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="566d6-495">PostgreSQL</span></span>](#postgresql) |
| &nbsp; |[<span data-ttu-id="566d6-496">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="566d6-496">SAP Business Warehouse</span></span>](#sap-business-warehouse) |
| &nbsp; |[<span data-ttu-id="566d6-497">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="566d6-497">SAP HANA</span></span>](#sap-hana) |
| &nbsp; |[<span data-ttu-id="566d6-498">SQL Server</span><span class="sxs-lookup"><span data-stu-id="566d6-498">SQL Server</span></span>](#sql-server) |
| &nbsp; |[<span data-ttu-id="566d6-499">Sybase</span><span class="sxs-lookup"><span data-stu-id="566d6-499">Sybase</span></span>](#sybase) |
| &nbsp; |[<span data-ttu-id="566d6-500">Teradata</span><span class="sxs-lookup"><span data-stu-id="566d6-500">Teradata</span></span>](#teradata) |
| <span data-ttu-id="566d6-501">**NoSQL**</span><span class="sxs-lookup"><span data-stu-id="566d6-501">**NoSQL**</span></span> |[<span data-ttu-id="566d6-502">Cassandra</span><span class="sxs-lookup"><span data-stu-id="566d6-502">Cassandra</span></span>](#cassandra) |
| &nbsp; |[<span data-ttu-id="566d6-503">MongoDB</span><span class="sxs-lookup"><span data-stu-id="566d6-503">MongoDB</span></span>](#mongodb) |
| <span data-ttu-id="566d6-504">**檔案**</span><span class="sxs-lookup"><span data-stu-id="566d6-504">**File**</span></span> |[<span data-ttu-id="566d6-505">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="566d6-505">Amazon S3</span></span>](#amazon-s3) |
| &nbsp; |[<span data-ttu-id="566d6-506">檔案系統</span><span class="sxs-lookup"><span data-stu-id="566d6-506">File System</span></span>](#file-system) |
| &nbsp; |[<span data-ttu-id="566d6-507">FTP</span><span class="sxs-lookup"><span data-stu-id="566d6-507">FTP</span></span>](#ftp) |
| &nbsp; |[<span data-ttu-id="566d6-508">HDFS</span><span class="sxs-lookup"><span data-stu-id="566d6-508">HDFS</span></span>](#hdfs) |
| &nbsp; |[<span data-ttu-id="566d6-509">SFTP</span><span class="sxs-lookup"><span data-stu-id="566d6-509">SFTP</span></span>](#sftp) |
| <span data-ttu-id="566d6-510">**其他**</span><span class="sxs-lookup"><span data-stu-id="566d6-510">**Others**</span></span> |[<span data-ttu-id="566d6-511">HTTP</span><span class="sxs-lookup"><span data-stu-id="566d6-511">HTTP</span></span>](#http) |
| &nbsp; |[<span data-ttu-id="566d6-512">OData</span><span class="sxs-lookup"><span data-stu-id="566d6-512">OData</span></span>](#odata) |
| &nbsp; |[<span data-ttu-id="566d6-513">ODBC</span><span class="sxs-lookup"><span data-stu-id="566d6-513">ODBC</span></span>](#odbc) |
| &nbsp; |[<span data-ttu-id="566d6-514">Salesforce</span><span class="sxs-lookup"><span data-stu-id="566d6-514">Salesforce</span></span>](#salesforce) |
| &nbsp; |[<span data-ttu-id="566d6-515">Web 資料表</span><span class="sxs-lookup"><span data-stu-id="566d6-515">Web Table</span></span>](#web-table) |

## <a name="azure-blob-storage"></a><span data-ttu-id="566d6-516">Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="566d6-516">Azure Blob Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="566d6-517">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-517">Linked service</span></span>
<span data-ttu-id="566d6-518">有兩種連結服務類型︰Azure 儲存體連結服務和 Azure 儲存體 SAS 連結服務。</span><span class="sxs-lookup"><span data-stu-id="566d6-518">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="566d6-519">Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-519">Azure Storage Linked Service</span></span>
<span data-ttu-id="566d6-520">toolink 您 Azure 儲存體帳戶 tooa 的 data factory 使用 hello**帳戶金鑰**，建立 Azure 儲存體連結服務。</span><span class="sxs-lookup"><span data-stu-id="566d6-520">toolink your Azure storage account tooa data factory by using hello **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="566d6-521">toodefine Azure 儲存體連結服務，設定 hello**類型**hello 的連結服務太**AzureStorage**。</span><span class="sxs-lookup"><span data-stu-id="566d6-521">toodefine an Azure Storage linked service, set hello **type** of hello linked service too**AzureStorage**.</span></span> <span data-ttu-id="566d6-522">然後，您可以指定下列屬性在 hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-522">Then, you can specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="566d6-523">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-523">Property</span></span> | <span data-ttu-id="566d6-524">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-524">Description</span></span> | <span data-ttu-id="566d6-525">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-525">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="566d6-526">connectionString</span><span class="sxs-lookup"><span data-stu-id="566d6-526">connectionString</span></span> |<span data-ttu-id="566d6-527">指定所需的資訊 tooconnect tooAzure 儲存體 hello connectionString 屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-527">Specify information needed tooconnect tooAzure storage for hello connectionString property.</span></span> |<span data-ttu-id="566d6-528">是</span><span class="sxs-lookup"><span data-stu-id="566d6-528">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="566d6-529">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-529">Example</span></span>  

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

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="566d6-530">Azure 儲存體 SAS 連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-530">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="566d6-531">hello Azure 儲存體 SAS 連結服務可讓您 Azure 儲存體帳戶 tooan Azure data factory toolink 使用共用存取簽章 (SAS)。</span><span class="sxs-lookup"><span data-stu-id="566d6-531">hello Azure Storage SAS linked service allows you toolink an Azure Storage Account tooan Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="566d6-532">它提供 hello 資料 factory 限制/時間繫結存取 tooall/特定資源 （blob/容器） hello 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="566d6-532">It provides hello data factory with restricted/time-bound access tooall/specific resources (blob/container) in hello storage.</span></span> <span data-ttu-id="566d6-533">toolink 使用共用存取簽章、 您 Azure 儲存體帳戶 tooa data factory 建立 Azure 儲存體 SAS 連結服務。</span><span class="sxs-lookup"><span data-stu-id="566d6-533">toolink your Azure storage account tooa data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="566d6-534">Azure 儲存體 SAS toodefine 連結服務，設定 hello**類型**hello 的連結服務太**AzureStorageSas**。</span><span class="sxs-lookup"><span data-stu-id="566d6-534">toodefine an Azure Storage SAS linked service, set hello **type** of hello linked service too**AzureStorageSas**.</span></span> <span data-ttu-id="566d6-535">然後，您可以指定下列屬性在 hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-535">Then, you can specify following properties in hello **typeProperties** section:</span></span>   

| <span data-ttu-id="566d6-536">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-536">Property</span></span> | <span data-ttu-id="566d6-537">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-537">Description</span></span> | <span data-ttu-id="566d6-538">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-538">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="566d6-539">sasUri</span><span class="sxs-lookup"><span data-stu-id="566d6-539">sasUri</span></span> |<span data-ttu-id="566d6-540">指定共用存取簽章 URI toohello Azure 儲存體資源，例如 blob、 容器或資料表。</span><span class="sxs-lookup"><span data-stu-id="566d6-540">Specify Shared Access Signature URI toohello Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="566d6-541">是</span><span class="sxs-lookup"><span data-stu-id="566d6-541">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="566d6-542">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-542">Example</span></span>

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

<span data-ttu-id="566d6-543">如需這些連結服務的詳細資訊，請參閱 [Azure Blob 儲存體連接器](data-factory-azure-blob-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-543">For more information about these linked services, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="566d6-544">Dataset</span><span class="sxs-lookup"><span data-stu-id="566d6-544">Dataset</span></span>
<span data-ttu-id="566d6-545">toodefine Azure Blob 資料集設定 hello**類型**hello 資料集太**AzureBlob**。</span><span class="sxs-lookup"><span data-stu-id="566d6-545">toodefine an Azure Blob dataset, set hello **type** of hello dataset too**AzureBlob**.</span></span> <span data-ttu-id="566d6-546">然後，指定下列 Azure Blob 中 hello 的特定屬性的 hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-546">Then, specify hello following Azure Blob specific properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="566d6-547">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-547">Property</span></span> | <span data-ttu-id="566d6-548">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-548">Description</span></span> | <span data-ttu-id="566d6-549">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-549">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-550">folderPath</span><span class="sxs-lookup"><span data-stu-id="566d6-550">folderPath</span></span> |<span data-ttu-id="566d6-551">路徑 toohello 容器，並且在 hello blob 儲存體中的資料夾。</span><span class="sxs-lookup"><span data-stu-id="566d6-551">Path toohello container and folder in hello blob storage.</span></span> <span data-ttu-id="566d6-552">範例：myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="566d6-552">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="566d6-553">是</span><span class="sxs-lookup"><span data-stu-id="566d6-553">Yes</span></span> |
| <span data-ttu-id="566d6-554">fileName</span><span class="sxs-lookup"><span data-stu-id="566d6-554">fileName</span></span> |<span data-ttu-id="566d6-555">Hello blob 名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-555">Name of hello blob.</span></span> <span data-ttu-id="566d6-556">fileName 是選擇性的，而且區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="566d6-556">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="566d6-557">如果您在上指定的檔名、 hello 活動 （包括複製） 運作 hello 特定 Blob。</span><span class="sxs-lookup"><span data-stu-id="566d6-557">If you specify a filename, hello activity (including Copy) works on hello specific Blob.</span></span><br/><br/><span data-ttu-id="566d6-558">若未指定檔名，複本會輸入資料集的 hello folderPath 中包含所有 Blob。</span><span class="sxs-lookup"><span data-stu-id="566d6-558">When fileName is not specified, Copy includes all Blobs in hello folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="566d6-559">當檔案名稱未指定輸出資料集時，會在遵循此格式的 hello hello hello 產生檔案名稱： 資料。<Guid>.txt (例如:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="566d6-559">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="566d6-560">否</span><span class="sxs-lookup"><span data-stu-id="566d6-560">No</span></span> |
| <span data-ttu-id="566d6-561">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="566d6-561">partitionedBy</span></span> |<span data-ttu-id="566d6-562">partitionedBy 是選擇性的屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-562">partitionedBy is an optional property.</span></span> <span data-ttu-id="566d6-563">您可以使用它 toospecify 動態 folderPath 和 filename 時間序列資料的。</span><span class="sxs-lookup"><span data-stu-id="566d6-563">You can use it toospecify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="566d6-564">例如，folderPath 可針對每小時的資料進行參數化。</span><span class="sxs-lookup"><span data-stu-id="566d6-564">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="566d6-565">否</span><span class="sxs-lookup"><span data-stu-id="566d6-565">No</span></span> |
| <span data-ttu-id="566d6-566">format</span><span class="sxs-lookup"><span data-stu-id="566d6-566">format</span></span> | <span data-ttu-id="566d6-567">支援下列格式類型的 hello: **TextFormat**， **JsonFormat**， **AvroFormat**， **OrcFormat**， **ParquetFormat**。</span><span class="sxs-lookup"><span data-stu-id="566d6-567">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="566d6-568">設定 hello**類型**下格式 tooone 這些值的屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-568">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="566d6-569">如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。</span><span class="sxs-lookup"><span data-stu-id="566d6-569">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="566d6-570">如果您想太**複製檔做為-是**之間以檔案為基礎存放區 （二進位複製），略過這兩個輸入和輸出資料集定義中的 hello 格式 > 一節。</span><span class="sxs-lookup"><span data-stu-id="566d6-570">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="566d6-571">否</span><span class="sxs-lookup"><span data-stu-id="566d6-571">No</span></span> |
| <span data-ttu-id="566d6-572">compression</span><span class="sxs-lookup"><span data-stu-id="566d6-572">compression</span></span> | <span data-ttu-id="566d6-573">指定 hello 類型和層級的 hello 資料壓縮。</span><span class="sxs-lookup"><span data-stu-id="566d6-573">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="566d6-574">支援的類型為：**GZip**、**Deflate**、**BZip2** 及 **ZipDeflate**。</span><span class="sxs-lookup"><span data-stu-id="566d6-574">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="566d6-575">支援的層級為：**Optimal** 和 **Fastest**。</span><span class="sxs-lookup"><span data-stu-id="566d6-575">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="566d6-576">如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。</span><span class="sxs-lookup"><span data-stu-id="566d6-576">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="566d6-577">否</span><span class="sxs-lookup"><span data-stu-id="566d6-577">No</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-578">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-578">Example</span></span>

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


<span data-ttu-id="566d6-579">如需詳細資訊，請參閱 [Azure Blob 連接器](data-factory-azure-blob-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-579">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#dataset-properties) article.</span></span>

### <a name="blobsource-in-copy-activity"></a><span data-ttu-id="566d6-580">複製活動中的 BlobSource</span><span class="sxs-lookup"><span data-stu-id="566d6-580">BlobSource in Copy Activity</span></span>
<span data-ttu-id="566d6-581">如果您從 Azure Blob 儲存體複製資料，設定 hello**來源類型**的 hello 複製活動太**BlobSource**，並指定下列屬性在 hello * * 來源 * * 區段：</span><span class="sxs-lookup"><span data-stu-id="566d6-581">If you are copying data from an Azure Blob Storage, set hello **source type** of hello copy activity too**BlobSource**, and specify following properties in hello **source **section:</span></span>

| <span data-ttu-id="566d6-582">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-582">Property</span></span> | <span data-ttu-id="566d6-583">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-583">Description</span></span> | <span data-ttu-id="566d6-584">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-584">Allowed values</span></span> | <span data-ttu-id="566d6-585">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-585">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-586">遞迴</span><span class="sxs-lookup"><span data-stu-id="566d6-586">recursive</span></span> |<span data-ttu-id="566d6-587">指出是否 hello 讀取資料以遞迴方式從 hello 子資料夾，或只能從 hello 指定的資料夾。</span><span class="sxs-lookup"><span data-stu-id="566d6-587">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="566d6-588">True (預設值)、False</span><span class="sxs-lookup"><span data-stu-id="566d6-588">True (default value), False</span></span> |<span data-ttu-id="566d6-589">否</span><span class="sxs-lookup"><span data-stu-id="566d6-589">No</span></span> |

#### <a name="example-blobsource"></a><span data-ttu-id="566d6-590">範例︰BlobSource**</span><span class="sxs-lookup"><span data-stu-id="566d6-590">Example: BlobSource**</span></span>
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
### <a name="blobsink-in-copy-activity"></a><span data-ttu-id="566d6-591">複製活動中的 BlobSink</span><span class="sxs-lookup"><span data-stu-id="566d6-591">BlobSink in Copy Activity</span></span>
<span data-ttu-id="566d6-592">如果您要複製資料 tooan Azure Blob 儲存體，請設定 hello**接收器類型**的 hello 複製活動太**BlobSink**，並指定下列屬性在 hello**接收**> 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-592">If you are copying data tooan Azure Blob Storage, set hello **sink type** of hello copy activity too**BlobSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="566d6-593">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-593">Property</span></span> | <span data-ttu-id="566d6-594">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-594">Description</span></span> | <span data-ttu-id="566d6-595">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-595">Allowed values</span></span> | <span data-ttu-id="566d6-596">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-596">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-597">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="566d6-597">copyBehavior</span></span> |<span data-ttu-id="566d6-598">Hello 來源 BlobSource 或檔案系統時，請定義 hello 複製行為。</span><span class="sxs-lookup"><span data-stu-id="566d6-598">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="566d6-599"><b>PreserveHierarchy</b>： 保留 hello hello 目標資料夾中的檔案階層。</span><span class="sxs-lookup"><span data-stu-id="566d6-599"><b>PreserveHierarchy</b>: preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="566d6-600">hello 的來源檔案 toosource 資料夾的相對路徑會是相同 toohello 的目標檔案 tootarget 資料夾的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="566d6-600">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="566d6-601"><b>FlattenHierarchy</b>: hello 來源資料夾中的所有檔案都位於 hello 第一次層級的目標資料夾。</span><span class="sxs-lookup"><span data-stu-id="566d6-601"><b>FlattenHierarchy</b>: all files from hello source folder are in hello first level of target folder.</span></span> <span data-ttu-id="566d6-602">hello 目標檔案已自動產生的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-602">hello target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="566d6-603"><b>MergeFiles （預設值）：</b>合併 hello 來源資料夾 tooone 檔案中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="566d6-603"><b>MergeFiles (default):</b> merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="566d6-604">如果指定 hello/Blob 檔案的名稱，則 hello 合併的檔案名稱就是指定之名稱; hello否則，將會自動產生的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-604">If hello File/Blob Name is specified, hello merged file name would be hello specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="566d6-605">否</span><span class="sxs-lookup"><span data-stu-id="566d6-605">No</span></span> |

#### <a name="example-blobsink"></a><span data-ttu-id="566d6-606">範例︰BlobSink</span><span class="sxs-lookup"><span data-stu-id="566d6-606">Example: BlobSink</span></span>

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

<span data-ttu-id="566d6-607">如需詳細資訊，請參閱 [Azure Blob 連接器](data-factory-azure-blob-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-607">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-data-lake-store"></a><span data-ttu-id="566d6-608">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="566d6-608">Azure Data Lake Store</span></span>

### <a name="linked-service"></a><span data-ttu-id="566d6-609">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-609">Linked service</span></span>
<span data-ttu-id="566d6-610">toodefine 連結 Azure Data Lake Store 服務，hello 集 hello 類型的連結服務太**AzureDataLakeStore**，並指定下列屬性在 hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-610">toodefine an Azure Data Lake Store linked service, set hello type of hello linked service too**AzureDataLakeStore**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="566d6-611">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-611">Property</span></span> | <span data-ttu-id="566d6-612">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-612">Description</span></span> | <span data-ttu-id="566d6-613">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-613">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="566d6-614">類型</span><span class="sxs-lookup"><span data-stu-id="566d6-614">type</span></span> | <span data-ttu-id="566d6-615">hello 類型屬性必須設定為： **AzureDataLakeStore**</span><span class="sxs-lookup"><span data-stu-id="566d6-615">hello type property must be set to: **AzureDataLakeStore**</span></span> | <span data-ttu-id="566d6-616">是</span><span class="sxs-lookup"><span data-stu-id="566d6-616">Yes</span></span> |
| <span data-ttu-id="566d6-617">dataLakeStoreUri</span><span class="sxs-lookup"><span data-stu-id="566d6-617">dataLakeStoreUri</span></span> | <span data-ttu-id="566d6-618">指定 hello Azure Data Lake Store 帳戶的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="566d6-618">Specify information about hello Azure Data Lake Store account.</span></span> <span data-ttu-id="566d6-619">在下列格式的 hello:`https://[accountname].azuredatalakestore.net/webhdfs/v1`或`adl://[accountname].azuredatalakestore.net/`。</span><span class="sxs-lookup"><span data-stu-id="566d6-619">It is in hello following format: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="566d6-620">是</span><span class="sxs-lookup"><span data-stu-id="566d6-620">Yes</span></span> |
| <span data-ttu-id="566d6-621">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="566d6-621">subscriptionId</span></span> | <span data-ttu-id="566d6-622">所屬的 azure 訂用帳戶 Id toowhich 資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="566d6-622">Azure subscription Id toowhich Data Lake Store belongs.</span></span> | <span data-ttu-id="566d6-623">接收 (Sink) 的必要項目</span><span class="sxs-lookup"><span data-stu-id="566d6-623">Required for sink</span></span> |
| <span data-ttu-id="566d6-624">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="566d6-624">resourceGroupName</span></span> | <span data-ttu-id="566d6-625">所屬的 azure 資源群組名稱 toowhich 資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="566d6-625">Azure resource group name toowhich Data Lake Store belongs.</span></span> | <span data-ttu-id="566d6-626">接收 (Sink) 的必要項目</span><span class="sxs-lookup"><span data-stu-id="566d6-626">Required for sink</span></span> |
| <span data-ttu-id="566d6-627">servicePrincipalId</span><span class="sxs-lookup"><span data-stu-id="566d6-627">servicePrincipalId</span></span> | <span data-ttu-id="566d6-628">指定 hello 應用程式的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="566d6-628">Specify hello application's client ID.</span></span> | <span data-ttu-id="566d6-629">是 (適用於服務主體驗證)</span><span class="sxs-lookup"><span data-stu-id="566d6-629">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="566d6-630">servicePrincipalKey</span><span class="sxs-lookup"><span data-stu-id="566d6-630">servicePrincipalKey</span></span> | <span data-ttu-id="566d6-631">指定 hello 應用程式的金鑰。</span><span class="sxs-lookup"><span data-stu-id="566d6-631">Specify hello application's key.</span></span> | <span data-ttu-id="566d6-632">是 (適用於服務主體驗證)</span><span class="sxs-lookup"><span data-stu-id="566d6-632">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="566d6-633">tenant</span><span class="sxs-lookup"><span data-stu-id="566d6-633">tenant</span></span> | <span data-ttu-id="566d6-634">指定在您的應用程式所在的 hello 租用戶資訊 (網域名稱或租用戶 ID)。</span><span class="sxs-lookup"><span data-stu-id="566d6-634">Specify hello tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="566d6-635">您可以透過暫留在 hello 右上角的 hello Azure 入口網站中的 hello 滑鼠擷取它。</span><span class="sxs-lookup"><span data-stu-id="566d6-635">You can retrieve it by hovering hello mouse in hello top-right corner of hello Azure portal.</span></span> | <span data-ttu-id="566d6-636">是 (適用於服務主體驗證)</span><span class="sxs-lookup"><span data-stu-id="566d6-636">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="566d6-637">授權</span><span class="sxs-lookup"><span data-stu-id="566d6-637">authorization</span></span> | <span data-ttu-id="566d6-638">按一下**授權**按鈕在 hello **Data Factory 編輯器**並輸入您 hello 自動產生的授權 URL toothis 屬性指派的認證。</span><span class="sxs-lookup"><span data-stu-id="566d6-638">Click **Authorize** button in hello **Data Factory Editor** and enter your credential that assigns hello auto-generated authorization URL toothis property.</span></span> | <span data-ttu-id="566d6-639">是 (適用於使用者認證驗證)</span><span class="sxs-lookup"><span data-stu-id="566d6-639">Yes (for user credential authentication)</span></span>|
| <span data-ttu-id="566d6-640">sessionId</span><span class="sxs-lookup"><span data-stu-id="566d6-640">sessionId</span></span> | <span data-ttu-id="566d6-641">從 hello OAuth 授權工作階段的 OAuth 工作階段識別碼。</span><span class="sxs-lookup"><span data-stu-id="566d6-641">OAuth session id from hello OAuth authorization session.</span></span> <span data-ttu-id="566d6-642">每個工作階段識別碼都是唯一的，只能使用一次。</span><span class="sxs-lookup"><span data-stu-id="566d6-642">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="566d6-643">當您使用 Data Factory 編輯器時便會自動產生此設定。</span><span class="sxs-lookup"><span data-stu-id="566d6-643">This setting is automatically generated when you use Data Factory Editor.</span></span> | <span data-ttu-id="566d6-644">是 (適用於使用者認證驗證)</span><span class="sxs-lookup"><span data-stu-id="566d6-644">Yes (for user credential authentication)</span></span> |

#### <a name="example-using-service-principal-authentication"></a><span data-ttu-id="566d6-645">範例：使用服務主體驗證</span><span class="sxs-lookup"><span data-stu-id="566d6-645">Example: using service principal authentication</span></span>
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

#### <a name="example-using-user-credential-authentication"></a><span data-ttu-id="566d6-646">範例︰使用使用者認證驗證</span><span class="sxs-lookup"><span data-stu-id="566d6-646">Example: using user credential authentication</span></span>
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

<span data-ttu-id="566d6-647">如需詳細資訊，請參閱 [Azure Data Lake Store 連接器](data-factory-azure-datalake-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-647">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="566d6-648">Dataset</span><span class="sxs-lookup"><span data-stu-id="566d6-648">Dataset</span></span>
<span data-ttu-id="566d6-649">toodefine Azure 資料湖存放區資料集設定 hello**類型**hello 資料集太**AzureDataLakeStore**，並指定下列屬性在 hello hello **typeProperties**> 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-649">toodefine an Azure Data Lake Store dataset, set hello **type** of hello dataset too**AzureDataLakeStore**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="566d6-650">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-650">Property</span></span> | <span data-ttu-id="566d6-651">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-651">Description</span></span> | <span data-ttu-id="566d6-652">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-652">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="566d6-653">folderPath</span><span class="sxs-lookup"><span data-stu-id="566d6-653">folderPath</span></span> |<span data-ttu-id="566d6-654">路徑 toohello 容器和資料夾在 hello Azure 資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="566d6-654">Path toohello container and folder in hello Azure Data Lake store.</span></span> |<span data-ttu-id="566d6-655">是</span><span class="sxs-lookup"><span data-stu-id="566d6-655">Yes</span></span> |
| <span data-ttu-id="566d6-656">fileName</span><span class="sxs-lookup"><span data-stu-id="566d6-656">fileName</span></span> |<span data-ttu-id="566d6-657">Hello Azure 資料湖存放區中的 hello 檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-657">Name of hello file in hello Azure Data Lake store.</span></span> <span data-ttu-id="566d6-658">fileName 是選擇性的，而且區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="566d6-658">fileName is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="566d6-659">如果您指定的檔名，hello 活動 （包括複製） 適用於 hello 特定檔案。</span><span class="sxs-lookup"><span data-stu-id="566d6-659">If you specify a filename, hello activity (including Copy) works on hello specific file.</span></span><br/><br/><span data-ttu-id="566d6-660">若未指定檔名，複本會輸入資料集的 hello folderPath 中包含所有檔案。</span><span class="sxs-lookup"><span data-stu-id="566d6-660">When fileName is not specified, Copy includes all files in hello folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="566d6-661">當檔案名稱未指定輸出資料集時，會在遵循此格式的 hello hello hello 產生檔案名稱： 資料。<Guid>.txt (例如:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="566d6-661">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="566d6-662">否</span><span class="sxs-lookup"><span data-stu-id="566d6-662">No</span></span> |
| <span data-ttu-id="566d6-663">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="566d6-663">partitionedBy</span></span> |<span data-ttu-id="566d6-664">partitionedBy 是選擇性的屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-664">partitionedBy is an optional property.</span></span> <span data-ttu-id="566d6-665">您可以使用它 toospecify 動態 folderPath 和 filename 時間序列資料的。</span><span class="sxs-lookup"><span data-stu-id="566d6-665">You can use it toospecify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="566d6-666">例如，folderPath 可針對每小時的資料進行參數化。</span><span class="sxs-lookup"><span data-stu-id="566d6-666">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="566d6-667">否</span><span class="sxs-lookup"><span data-stu-id="566d6-667">No</span></span> |
| <span data-ttu-id="566d6-668">format</span><span class="sxs-lookup"><span data-stu-id="566d6-668">format</span></span> | <span data-ttu-id="566d6-669">支援下列格式類型的 hello: **TextFormat**， **JsonFormat**， **AvroFormat**， **OrcFormat**， **ParquetFormat**。</span><span class="sxs-lookup"><span data-stu-id="566d6-669">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="566d6-670">設定 hello**類型**下格式 tooone 這些值的屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-670">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="566d6-671">如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。</span><span class="sxs-lookup"><span data-stu-id="566d6-671">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="566d6-672">如果您想太**複製檔做為-是**之間以檔案為基礎存放區 （二進位複製），略過這兩個輸入和輸出資料集定義中的 hello 格式 > 一節。</span><span class="sxs-lookup"><span data-stu-id="566d6-672">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="566d6-673">否</span><span class="sxs-lookup"><span data-stu-id="566d6-673">No</span></span> |
| <span data-ttu-id="566d6-674">compression</span><span class="sxs-lookup"><span data-stu-id="566d6-674">compression</span></span> | <span data-ttu-id="566d6-675">指定 hello 類型和層級的 hello 資料壓縮。</span><span class="sxs-lookup"><span data-stu-id="566d6-675">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="566d6-676">支援的類型為：**GZip**、**Deflate**、**BZip2** 及 **ZipDeflate**。</span><span class="sxs-lookup"><span data-stu-id="566d6-676">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="566d6-677">支援的層級為：**Optimal** 和 **Fastest**。</span><span class="sxs-lookup"><span data-stu-id="566d6-677">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="566d6-678">如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。</span><span class="sxs-lookup"><span data-stu-id="566d6-678">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="566d6-679">否</span><span class="sxs-lookup"><span data-stu-id="566d6-679">No</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-680">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-680">Example</span></span>
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

<span data-ttu-id="566d6-681">如需詳細資訊，請參閱 [Azure Data Lake Store 連接器](data-factory-azure-datalake-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-681">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-data-lake-store-source-in-copy-activity"></a><span data-ttu-id="566d6-682">複製活動中的 Azure Data Lake Store 來源</span><span class="sxs-lookup"><span data-stu-id="566d6-682">Azure Data Lake Store Source in Copy Activity</span></span>
<span data-ttu-id="566d6-683">如果您從 Azure 資料湖存放區複製資料，設定 hello**來源類型**的 hello 複製活動太**AzureDataLakeStoreSource**，並指定下列屬性在 hello**來源** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-683">If you are copying data from an Azure Data Lake Store, set hello **source type** of hello copy activity too**AzureDataLakeStoreSource**, and specify following properties in hello **source** section:</span></span>

<span data-ttu-id="566d6-684">**AzureDataLakeStoreSource**支援下列屬性的 hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-684">**AzureDataLakeStoreSource** supports hello following properties **typeProperties** section:</span></span>

| <span data-ttu-id="566d6-685">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-685">Property</span></span> | <span data-ttu-id="566d6-686">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-686">Description</span></span> | <span data-ttu-id="566d6-687">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-687">Allowed values</span></span> | <span data-ttu-id="566d6-688">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-688">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-689">遞迴</span><span class="sxs-lookup"><span data-stu-id="566d6-689">recursive</span></span> |<span data-ttu-id="566d6-690">指出是否 hello 讀取資料以遞迴方式從 hello 子資料夾，或只能從 hello 指定的資料夾。</span><span class="sxs-lookup"><span data-stu-id="566d6-690">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="566d6-691">True (預設值)、False</span><span class="sxs-lookup"><span data-stu-id="566d6-691">True (default value), False</span></span> |<span data-ttu-id="566d6-692">否</span><span class="sxs-lookup"><span data-stu-id="566d6-692">No</span></span> |

#### <a name="example-azuredatalakestoresource"></a><span data-ttu-id="566d6-693">範例：AzureDataLakeStoreSource</span><span class="sxs-lookup"><span data-stu-id="566d6-693">Example: AzureDataLakeStoreSource</span></span>

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

<span data-ttu-id="566d6-694">如需詳細資訊，請參閱 [Azure Data Lake Store 連接器](data-factory-azure-datalake-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-694">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span>

### <a name="azure-data-lake-store-sink-in-copy-activity"></a><span data-ttu-id="566d6-695">複製活動中的 Azure Data Lake Store 接收</span><span class="sxs-lookup"><span data-stu-id="566d6-695">Azure Data Lake Store Sink in Copy Activity</span></span>
<span data-ttu-id="566d6-696">如果您要複製資料 tooan Azure 資料湖存放區，請設定 hello**接收器類型**的 hello 複製活動太**AzureDataLakeStoreSink**，並指定下列屬性在 hello**接收**> 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-696">If you are copying data tooan Azure Data Lake Store, set hello **sink type** of hello copy activity too**AzureDataLakeStoreSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="566d6-697">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-697">Property</span></span> | <span data-ttu-id="566d6-698">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-698">Description</span></span> | <span data-ttu-id="566d6-699">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-699">Allowed values</span></span> | <span data-ttu-id="566d6-700">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-700">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-701">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="566d6-701">copyBehavior</span></span> |<span data-ttu-id="566d6-702">指定 hello 複製行為。</span><span class="sxs-lookup"><span data-stu-id="566d6-702">Specifies hello copy behavior.</span></span> |<span data-ttu-id="566d6-703"><b>PreserveHierarchy</b>： 保留 hello hello 目標資料夾中的檔案階層。</span><span class="sxs-lookup"><span data-stu-id="566d6-703"><b>PreserveHierarchy</b>: preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="566d6-704">hello 的來源檔案 toosource 資料夾的相對路徑會是相同 toohello 的目標檔案 tootarget 資料夾的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="566d6-704">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="566d6-705"><b>FlattenHierarchy</b>: hello 第一個層級的目標資料夾中建立 hello 來源資料夾中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="566d6-705"><b>FlattenHierarchy</b>: all files from hello source folder are created in hello first level of target folder.</span></span> <span data-ttu-id="566d6-706">會使用自動產生的名稱建立 hello 目標檔案。</span><span class="sxs-lookup"><span data-stu-id="566d6-706">hello target files are created with auto generated name.</span></span><br/><br/><span data-ttu-id="566d6-707"><b>MergeFiles</b>： 合併 hello 來源資料夾 tooone 檔案中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="566d6-707"><b>MergeFiles</b>: merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="566d6-708">如果指定 hello/Blob 檔案的名稱，則 hello 合併的檔案名稱就是指定之名稱; hello否則，將會自動產生的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-708">If hello File/Blob Name is specified, hello merged file name would be hello specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="566d6-709">否</span><span class="sxs-lookup"><span data-stu-id="566d6-709">No</span></span> |

#### <a name="example-azuredatalakestoresink"></a><span data-ttu-id="566d6-710">範例：AzureDataLakeStoreSink</span><span class="sxs-lookup"><span data-stu-id="566d6-710">Example: AzureDataLakeStoreSink</span></span>
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

<span data-ttu-id="566d6-711">如需詳細資訊，請參閱 [Azure Data Lake Store 連接器](data-factory-azure-datalake-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-711">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-cosmos-db"></a><span data-ttu-id="566d6-712">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="566d6-712">Azure Cosmos DB</span></span>  

### <a name="linked-service"></a><span data-ttu-id="566d6-713">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-713">Linked service</span></span>
<span data-ttu-id="566d6-714">toodefine Azure Cosmos DB 的連結服務，設定 hello**類型**hello 的連結服務太**DocumentDb**，並指定下列屬性在 hello **typeProperties**區段：</span><span class="sxs-lookup"><span data-stu-id="566d6-714">toodefine an Azure Cosmos DB linked service, set hello **type** of hello linked service too**DocumentDb**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="566d6-715">**屬性**</span><span class="sxs-lookup"><span data-stu-id="566d6-715">**Property**</span></span> | <span data-ttu-id="566d6-716">**說明**</span><span class="sxs-lookup"><span data-stu-id="566d6-716">**Description**</span></span> | <span data-ttu-id="566d6-717">**必要**</span><span class="sxs-lookup"><span data-stu-id="566d6-717">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-718">connectionString</span><span class="sxs-lookup"><span data-stu-id="566d6-718">connectionString</span></span> |<span data-ttu-id="566d6-719">指定所需 tooconnect tooAzure Cosmos DB 資料庫的資訊。</span><span class="sxs-lookup"><span data-stu-id="566d6-719">Specify information needed tooconnect tooAzure Cosmos DB database.</span></span> |<span data-ttu-id="566d6-720">是</span><span class="sxs-lookup"><span data-stu-id="566d6-720">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-721">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-721">Example</span></span>

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
<span data-ttu-id="566d6-722">如需詳細資訊，請參閱 [Azure Cosmos DB 連接器](data-factory-azure-documentdb-connector.md#linked-service-properties)一文。</span><span class="sxs-lookup"><span data-stu-id="566d6-722">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="566d6-723">Dataset</span><span class="sxs-lookup"><span data-stu-id="566d6-723">Dataset</span></span>
<span data-ttu-id="566d6-724">toodefine Azure Cosmos DB 資料集設定 hello**類型**hello 資料集太**DocumentDbCollection**，並指定下列屬性在 hello hello **typeProperties**區段：</span><span class="sxs-lookup"><span data-stu-id="566d6-724">toodefine an Azure Cosmos DB dataset, set hello **type** of hello dataset too**DocumentDbCollection**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="566d6-725">**屬性**</span><span class="sxs-lookup"><span data-stu-id="566d6-725">**Property**</span></span> | <span data-ttu-id="566d6-726">**說明**</span><span class="sxs-lookup"><span data-stu-id="566d6-726">**Description**</span></span> | <span data-ttu-id="566d6-727">**必要**</span><span class="sxs-lookup"><span data-stu-id="566d6-727">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-728">collectionName</span><span class="sxs-lookup"><span data-stu-id="566d6-728">collectionName</span></span> |<span data-ttu-id="566d6-729">Hello Azure Cosmos DB 集合的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-729">Name of hello Azure Cosmos DB collection.</span></span> |<span data-ttu-id="566d6-730">是</span><span class="sxs-lookup"><span data-stu-id="566d6-730">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-731">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-731">Example</span></span>

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
<span data-ttu-id="566d6-732">如需詳細資訊，請參閱 [Azure Cosmos DB 連接器](data-factory-azure-documentdb-connector.md#dataset-properties)一文。</span><span class="sxs-lookup"><span data-stu-id="566d6-732">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#dataset-properties) article.</span></span>

### <a name="azure-cosmos-db-collection-source-in-copy-activity"></a><span data-ttu-id="566d6-733">複製活動中的 Azure Cosmos DB 集合來源</span><span class="sxs-lookup"><span data-stu-id="566d6-733">Azure Cosmos DB Collection Source in Copy Activity</span></span>
<span data-ttu-id="566d6-734">如果您從 Azure Cosmos DB 複製資料，設定 hello**來源類型**的 hello 複製活動太**DocumentDbCollectionSource**，並指定下列屬性在 hello**來源** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-734">If you are copying data from an Azure Cosmos DB, set hello **source type** of hello copy activity too**DocumentDbCollectionSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="566d6-735">**屬性**</span><span class="sxs-lookup"><span data-stu-id="566d6-735">**Property**</span></span> | <span data-ttu-id="566d6-736">**說明**</span><span class="sxs-lookup"><span data-stu-id="566d6-736">**Description**</span></span> | <span data-ttu-id="566d6-737">**允許的值**</span><span class="sxs-lookup"><span data-stu-id="566d6-737">**Allowed values**</span></span> | <span data-ttu-id="566d6-738">**必要**</span><span class="sxs-lookup"><span data-stu-id="566d6-738">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-739">query</span><span class="sxs-lookup"><span data-stu-id="566d6-739">query</span></span> |<span data-ttu-id="566d6-740">指定 hello 查詢 tooread 資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-740">Specify hello query tooread data.</span></span> |<span data-ttu-id="566d6-741">Azure Cosmos DB 所支援的查詢字串。</span><span class="sxs-lookup"><span data-stu-id="566d6-741">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="566d6-742">範例： `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="566d6-742">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="566d6-743">否</span><span class="sxs-lookup"><span data-stu-id="566d6-743">No</span></span> <br/><br/><span data-ttu-id="566d6-744">如果未指定，hello 執行的 SQL 陳述式：`select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="566d6-744">If not specified, hello SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="566d6-745">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="566d6-745">nestingSeparator</span></span> |<span data-ttu-id="566d6-746">巢狀 hello 文件的特殊字元 tooindicate</span><span class="sxs-lookup"><span data-stu-id="566d6-746">Special character tooindicate that hello document is nested</span></span> |<span data-ttu-id="566d6-747">任何字元。</span><span class="sxs-lookup"><span data-stu-id="566d6-747">Any character.</span></span> <br/><br/><span data-ttu-id="566d6-748">Azure Cosmos DB 是 JSON 文件的 NoSQL 存放區 (允許巢狀結構)。</span><span class="sxs-lookup"><span data-stu-id="566d6-748">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="566d6-749">Azure Data Factory 可讓使用者 toodenote 階層 nestingSeparator，也就是透過 「。 」</span><span class="sxs-lookup"><span data-stu-id="566d6-749">Azure Data Factory enables user toodenote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="566d6-750">在上述範例 hello。</span><span class="sxs-lookup"><span data-stu-id="566d6-750">in hello above examples.</span></span> <span data-ttu-id="566d6-751">Hello 分隔符號 hello 複製活動會產生三個子系的元素與 hello"Name"物件第一個中間和最後一個、 相應 too"Name.First"，"Name.Middle"和"Name.Last"hello 在資料表定義。</span><span class="sxs-lookup"><span data-stu-id="566d6-751">With hello separator, hello copy activity will generate hello “Name” object with three children elements First, Middle and Last, according too“Name.First”, “Name.Middle” and “Name.Last” in hello table definition.</span></span> |<span data-ttu-id="566d6-752">否</span><span class="sxs-lookup"><span data-stu-id="566d6-752">No</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-753">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-753">Example</span></span>

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

### <a name="azure-cosmos-db-collection-sink-in-copy-activity"></a><span data-ttu-id="566d6-754">複製活動中的 Azure Cosmos DB 集合接收器</span><span class="sxs-lookup"><span data-stu-id="566d6-754">Azure Cosmos DB Collection Sink in Copy Activity</span></span>
<span data-ttu-id="566d6-755">如果您要複製資料 tooAzure Cosmos DB，請設定 hello**接收器類型**的 hello 複製活動太**DocumentDbCollectionSink**，並指定下列屬性在 hello**接收**> 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-755">If you are copying data tooAzure Cosmos DB, set hello **sink type** of hello copy activity too**DocumentDbCollectionSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="566d6-756">**屬性**</span><span class="sxs-lookup"><span data-stu-id="566d6-756">**Property**</span></span> | <span data-ttu-id="566d6-757">**說明**</span><span class="sxs-lookup"><span data-stu-id="566d6-757">**Description**</span></span> | <span data-ttu-id="566d6-758">**允許的值**</span><span class="sxs-lookup"><span data-stu-id="566d6-758">**Allowed values**</span></span> | <span data-ttu-id="566d6-759">**必要**</span><span class="sxs-lookup"><span data-stu-id="566d6-759">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-760">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="566d6-760">nestingSeparator</span></span> |<span data-ttu-id="566d6-761">需要 hello 來源資料行名稱 tooindicate 巢狀文件中的特殊字元。</span><span class="sxs-lookup"><span data-stu-id="566d6-761">A special character in hello source column name tooindicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="566d6-762">例如上述： `Name.First` hello 輸出資料表會產生下列 JSON 結構 hello Cosmos DB 文件中的 hello:</span><span class="sxs-lookup"><span data-stu-id="566d6-762">For example above: `Name.First` in hello output table produces hello following JSON structure in hello Cosmos DB document:</span></span><br/><br/><span data-ttu-id="566d6-763">"Name": {</span><span class="sxs-lookup"><span data-stu-id="566d6-763">"Name": {</span></span><br/>    <span data-ttu-id="566d6-764">"First": "John"</span><span class="sxs-lookup"><span data-stu-id="566d6-764">"First": "John"</span></span><br/><span data-ttu-id="566d6-765">},</span><span class="sxs-lookup"><span data-stu-id="566d6-765">},</span></span> |<span data-ttu-id="566d6-766">為使用的 tooseparate 巢狀層級的字元。</span><span class="sxs-lookup"><span data-stu-id="566d6-766">Character that is used tooseparate nesting levels.</span></span><br/><br/><span data-ttu-id="566d6-767">預設值為 `.` (點)。</span><span class="sxs-lookup"><span data-stu-id="566d6-767">Default value is `.` (dot).</span></span> |<span data-ttu-id="566d6-768">為使用的 tooseparate 巢狀層級的字元。</span><span class="sxs-lookup"><span data-stu-id="566d6-768">Character that is used tooseparate nesting levels.</span></span> <br/><br/><span data-ttu-id="566d6-769">預設值為 `.` (點)。</span><span class="sxs-lookup"><span data-stu-id="566d6-769">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="566d6-770">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="566d6-770">writeBatchSize</span></span> |<span data-ttu-id="566d6-771">並行要求數目 tooAzure Cosmos DB 服務 toocreate 文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-771">Number of parallel requests tooAzure Cosmos DB service toocreate documents.</span></span><br/><br/><span data-ttu-id="566d6-772">使用這個屬性來複製資料從 Azure Cosmos DB 時，您可以微調 hello 效能。</span><span class="sxs-lookup"><span data-stu-id="566d6-772">You can fine-tune hello performance when copying data to/from Azure Cosmos DB by using this property.</span></span> <span data-ttu-id="566d6-773">當您增加叫用 writeBatchSize，因為會傳送多個平行要求 tooAzure Cosmos DB 時，您可以預期更佳的效能。</span><span class="sxs-lookup"><span data-stu-id="566d6-773">You can expect a better performance when you increase writeBatchSize because more parallel requests tooAzure Cosmos DB are sent.</span></span> <span data-ttu-id="566d6-774">不過，您必須先 tooavoid 節流，可擲回 hello 錯誤訊息: 「 要求率非常大 」。</span><span class="sxs-lookup"><span data-stu-id="566d6-774">However you’ll need tooavoid throttling that can throw hello error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="566d6-775">節流是由許多因素所決定，包括文件大小、文件中的詞彙數目、目標集合的檢索原則等。複製作業，您可以使用較佳的集合 (例如，S3) toohave hello 大部分可用的輸送量 （2500 的要求單位/秒）。</span><span class="sxs-lookup"><span data-stu-id="566d6-775">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (for example, S3) toohave hello most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="566d6-776">Integer</span><span class="sxs-lookup"><span data-stu-id="566d6-776">Integer</span></span> |<span data-ttu-id="566d6-777">否 (預設值：5)</span><span class="sxs-lookup"><span data-stu-id="566d6-777">No (default: 5)</span></span> |
| <span data-ttu-id="566d6-778">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="566d6-778">writeBatchTimeout</span></span> |<span data-ttu-id="566d6-779">在逾時之前，請等待 hello 作業 toocomplete 時間。</span><span class="sxs-lookup"><span data-stu-id="566d6-779">Wait time for hello operation toocomplete before it times out.</span></span> |<span data-ttu-id="566d6-780">時間範圍</span><span class="sxs-lookup"><span data-stu-id="566d6-780">timespan</span></span><br/><br/> <span data-ttu-id="566d6-781">範例：“00:30:00” (30 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="566d6-781">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="566d6-782">否</span><span class="sxs-lookup"><span data-stu-id="566d6-782">No</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-783">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-783">Example</span></span>

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
                    "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix"
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

<span data-ttu-id="566d6-784">如需詳細資訊，請參閱 [Azure Cosmos DB 連接器](data-factory-azure-documentdb-connector.md#copy-activity-properties)一文。</span><span class="sxs-lookup"><span data-stu-id="566d6-784">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="566d6-785">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="566d6-785">Azure SQL Database</span></span>

### <a name="linked-service"></a><span data-ttu-id="566d6-786">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-786">Linked service</span></span>
<span data-ttu-id="566d6-787">Azure SQL Database toodefine 連結服務，設定 hello**類型**hello 的連結服務太**AzureSqlDatabase**，並指定下列屬性在 hello **typeProperties**> 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-787">toodefine an Azure SQL Database linked service, set hello **type** of hello linked service too**AzureSqlDatabase**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="566d6-788">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-788">Property</span></span> | <span data-ttu-id="566d6-789">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-789">Description</span></span> | <span data-ttu-id="566d6-790">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-790">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-791">connectionString</span><span class="sxs-lookup"><span data-stu-id="566d6-791">connectionString</span></span> |<span data-ttu-id="566d6-792">指定所需的資訊 tooconnect toohello Azure SQL Database 執行個體 hello connectionString 屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-792">Specify information needed tooconnect toohello Azure SQL Database instance for hello connectionString property.</span></span> |<span data-ttu-id="566d6-793">是</span><span class="sxs-lookup"><span data-stu-id="566d6-793">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-794">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-794">Example</span></span>
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

<span data-ttu-id="566d6-795">如需詳細資訊，請參閱 [Azure SQL 連接器](data-factory-azure-sql-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-795">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="566d6-796">Dataset</span><span class="sxs-lookup"><span data-stu-id="566d6-796">Dataset</span></span>
<span data-ttu-id="566d6-797">toodefine 是 Azure SQL Database 資料集，設定 hello**類型**hello 資料集太**AzureSqlTable**，並指定下列屬性在 hello hello **typeProperties**區段：</span><span class="sxs-lookup"><span data-stu-id="566d6-797">toodefine an Azure SQL Database dataset, set hello **type** of hello dataset too**AzureSqlTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="566d6-798">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-798">Property</span></span> | <span data-ttu-id="566d6-799">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-799">Description</span></span> | <span data-ttu-id="566d6-800">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-800">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-801">tableName</span><span class="sxs-lookup"><span data-stu-id="566d6-801">tableName</span></span> |<span data-ttu-id="566d6-802">參照 hello 資料表或檢視中的連結服務的 hello Azure SQL Database 執行個體的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-802">Name of hello table or view in hello Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="566d6-803">是</span><span class="sxs-lookup"><span data-stu-id="566d6-803">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-804">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-804">Example</span></span>

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
<span data-ttu-id="566d6-805">如需詳細資訊，請參閱 [Azure SQL 連接器](data-factory-azure-sql-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-805">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="566d6-806">複製活動中的 SQL 來源</span><span class="sxs-lookup"><span data-stu-id="566d6-806">SQL Source in Copy Activity</span></span>
<span data-ttu-id="566d6-807">如果您從 Azure SQL Database 中複製資料，設定 hello**來源類型**的 hello 複製活動太**SqlSource**，並指定下列屬性在 hello**來源**區段：</span><span class="sxs-lookup"><span data-stu-id="566d6-807">If you are copying data from an Azure SQL Database, set hello **source type** of hello copy activity too**SqlSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="566d6-808">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-808">Property</span></span> | <span data-ttu-id="566d6-809">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-809">Description</span></span> | <span data-ttu-id="566d6-810">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-810">Allowed values</span></span> | <span data-ttu-id="566d6-811">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-811">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-812">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="566d6-812">sqlReaderQuery</span></span> |<span data-ttu-id="566d6-813">使用自訂查詢 tooread hello 的資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-813">Use hello custom query tooread data.</span></span> |<span data-ttu-id="566d6-814">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="566d6-814">SQL query string.</span></span> <span data-ttu-id="566d6-815">範例： `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="566d6-815">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="566d6-816">否</span><span class="sxs-lookup"><span data-stu-id="566d6-816">No</span></span> |
| <span data-ttu-id="566d6-817">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="566d6-817">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="566d6-818">名稱的 hello 預存程序會從 hello 來源資料表讀取資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-818">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="566d6-819">名稱的 hello 預存程序。</span><span class="sxs-lookup"><span data-stu-id="566d6-819">Name of hello stored procedure.</span></span> |<span data-ttu-id="566d6-820">否</span><span class="sxs-lookup"><span data-stu-id="566d6-820">No</span></span> |
| <span data-ttu-id="566d6-821">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="566d6-821">storedProcedureParameters</span></span> |<span data-ttu-id="566d6-822">Hello 參數，預存程序。</span><span class="sxs-lookup"><span data-stu-id="566d6-822">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="566d6-823">名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="566d6-823">Name/value pairs.</span></span> <span data-ttu-id="566d6-824">名稱和大小寫的參數必須符合 hello 名稱和大小寫的 hello 預存程序參數。</span><span class="sxs-lookup"><span data-stu-id="566d6-824">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="566d6-825">否</span><span class="sxs-lookup"><span data-stu-id="566d6-825">No</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-826">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-826">Example</span></span>

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
<span data-ttu-id="566d6-827">如需詳細資訊，請參閱 [Azure SQL 連接器](data-factory-azure-sql-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-827">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="566d6-828">複製活動中的 SQL 接收</span><span class="sxs-lookup"><span data-stu-id="566d6-828">SQL Sink in Copy Activity</span></span>
<span data-ttu-id="566d6-829">如果您要複製資料 tooAzure SQL 資料庫，請設定 hello**接收器類型**的 hello 複製活動太**SqlSink**，並指定下列屬性在 hello**接收**> 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-829">If you are copying data tooAzure SQL Database, set hello **sink type** of hello copy activity too**SqlSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="566d6-830">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-830">Property</span></span> | <span data-ttu-id="566d6-831">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-831">Description</span></span> | <span data-ttu-id="566d6-832">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-832">Allowed values</span></span> | <span data-ttu-id="566d6-833">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-833">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-834">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="566d6-834">writeBatchTimeout</span></span> |<span data-ttu-id="566d6-835">在逾時之前，請等待 hello 批次插入作業 toocomplete 時間。</span><span class="sxs-lookup"><span data-stu-id="566d6-835">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="566d6-836">時間範圍</span><span class="sxs-lookup"><span data-stu-id="566d6-836">timespan</span></span><br/><br/> <span data-ttu-id="566d6-837">範例：“00:30:00” (30 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="566d6-837">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="566d6-838">否</span><span class="sxs-lookup"><span data-stu-id="566d6-838">No</span></span> |
| <span data-ttu-id="566d6-839">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="566d6-839">writeBatchSize</span></span> |<span data-ttu-id="566d6-840">當 hello 緩衝區大小到達叫用 writeBatchSize 時，請將資料插入 hello SQL 資料表。</span><span class="sxs-lookup"><span data-stu-id="566d6-840">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="566d6-841">整數 (資料列數目)</span><span class="sxs-lookup"><span data-stu-id="566d6-841">Integer (number of rows)</span></span> |<span data-ttu-id="566d6-842">否 (預設值：10000)</span><span class="sxs-lookup"><span data-stu-id="566d6-842">No (default: 10000)</span></span> |
| <span data-ttu-id="566d6-843">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="566d6-843">sqlWriterCleanupScript</span></span> |<span data-ttu-id="566d6-844">複製活動 tooexecute 查詢指定的特定配量的資料清除。</span><span class="sxs-lookup"><span data-stu-id="566d6-844">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="566d6-845">查詢陳述式。</span><span class="sxs-lookup"><span data-stu-id="566d6-845">A query statement.</span></span> |<span data-ttu-id="566d6-846">否</span><span class="sxs-lookup"><span data-stu-id="566d6-846">No</span></span> |
| <span data-ttu-id="566d6-847">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="566d6-847">sliceIdentifierColumnName</span></span> |<span data-ttu-id="566d6-848">指定複製活動 toofill 的資料行名稱與自動產生配量識別項，也就是使用的 tooclean 何時重新執行的特定配量的資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-848">Specify a column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="566d6-849">資料類型為 binary(32) 之資料行的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-849">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="566d6-850">否</span><span class="sxs-lookup"><span data-stu-id="566d6-850">No</span></span> |
| <span data-ttu-id="566d6-851">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="566d6-851">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="566d6-852">名稱的 hello 預存程序 upserts （更新/插入） 資料到 hello 目標資料表。</span><span class="sxs-lookup"><span data-stu-id="566d6-852">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="566d6-853">名稱的 hello 預存程序。</span><span class="sxs-lookup"><span data-stu-id="566d6-853">Name of hello stored procedure.</span></span> |<span data-ttu-id="566d6-854">否</span><span class="sxs-lookup"><span data-stu-id="566d6-854">No</span></span> |
| <span data-ttu-id="566d6-855">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="566d6-855">storedProcedureParameters</span></span> |<span data-ttu-id="566d6-856">Hello 參數，預存程序。</span><span class="sxs-lookup"><span data-stu-id="566d6-856">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="566d6-857">名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="566d6-857">Name/value pairs.</span></span> <span data-ttu-id="566d6-858">名稱和大小寫的參數必須符合 hello 名稱和大小寫的 hello 預存程序參數。</span><span class="sxs-lookup"><span data-stu-id="566d6-858">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="566d6-859">否</span><span class="sxs-lookup"><span data-stu-id="566d6-859">No</span></span> |
| <span data-ttu-id="566d6-860">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="566d6-860">sqlWriterTableType</span></span> |<span data-ttu-id="566d6-861">指定用於 hello 預存程序中的資料表類型名稱 toobe。</span><span class="sxs-lookup"><span data-stu-id="566d6-861">Specify a table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="566d6-862">複製活動移動 hello 資料可讓在暫存資料表與此資料表類型。</span><span class="sxs-lookup"><span data-stu-id="566d6-862">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="566d6-863">預存程序程式碼可以再合併 hello 資料會被複製現有的資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-863">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="566d6-864">資料表類型名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-864">A table type name.</span></span> |<span data-ttu-id="566d6-865">否</span><span class="sxs-lookup"><span data-stu-id="566d6-865">No</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-866">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-866">Example</span></span>

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

<span data-ttu-id="566d6-867">如需詳細資訊，請參閱 [Azure SQL 連接器](data-factory-azure-sql-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-867">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="566d6-868">Azure SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="566d6-868">Azure SQL Data Warehouse</span></span>

### <a name="linked-service"></a><span data-ttu-id="566d6-869">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-869">Linked service</span></span>
<span data-ttu-id="566d6-870">Azure SQL 資料倉儲 toodefine 連結服務，設定 hello**類型**hello 的連結服務太**AzureSqlDW**，並指定下列屬性在 hello **typeProperties**> 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-870">toodefine an Azure SQL Data Warehouse linked service, set hello **type** of hello linked service too**AzureSqlDW**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="566d6-871">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-871">Property</span></span> | <span data-ttu-id="566d6-872">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-872">Description</span></span> | <span data-ttu-id="566d6-873">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-873">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-874">connectionString</span><span class="sxs-lookup"><span data-stu-id="566d6-874">connectionString</span></span> |<span data-ttu-id="566d6-875">指定所需的資訊 tooconnect toohello Azure SQL 資料倉儲執行個體 hello connectionString 屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-875">Specify information needed tooconnect toohello Azure SQL Data Warehouse instance for hello connectionString property.</span></span> |<span data-ttu-id="566d6-876">是</span><span class="sxs-lookup"><span data-stu-id="566d6-876">Yes</span></span> |



#### <a name="example"></a><span data-ttu-id="566d6-877">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-877">Example</span></span>

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

<span data-ttu-id="566d6-878">如需詳細資訊，請參閱 [Azure SQL 資料倉儲連接器](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-878">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="566d6-879">Dataset</span><span class="sxs-lookup"><span data-stu-id="566d6-879">Dataset</span></span>
<span data-ttu-id="566d6-880">toodefine 是 Azure SQL 資料倉儲資料集，設定 hello**類型**hello 資料集太**AzureSqlDWTable**，並指定下列屬性在 hello hello **typeProperties**> 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-880">toodefine an Azure SQL Data Warehouse dataset, set hello **type** of hello dataset too**AzureSqlDWTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="566d6-881">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-881">Property</span></span> | <span data-ttu-id="566d6-882">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-882">Description</span></span> | <span data-ttu-id="566d6-883">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-883">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-884">tableName</span><span class="sxs-lookup"><span data-stu-id="566d6-884">tableName</span></span> |<span data-ttu-id="566d6-885">參照 hello 資料表或檢視 hello 連結的服務的 hello Azure SQL 資料倉儲資料庫中的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-885">Name of hello table or view in hello Azure SQL Data Warehouse database that hello linked service refers to.</span></span> |<span data-ttu-id="566d6-886">是</span><span class="sxs-lookup"><span data-stu-id="566d6-886">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-887">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-887">Example</span></span>

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

<span data-ttu-id="566d6-888">如需詳細資訊，請參閱 [Azure SQL 資料倉儲連接器](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-888">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-dw-source-in-copy-activity"></a><span data-ttu-id="566d6-889">複製活動中的 SQL DW 來源</span><span class="sxs-lookup"><span data-stu-id="566d6-889">SQL DW Source in Copy Activity</span></span>
<span data-ttu-id="566d6-890">如果您要從 Azure SQL 資料倉儲來複製資料，設定 hello**來源類型**的 hello 複製活動太**SqlDWSource**，並指定下列屬性在 hello**來源**> 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-890">If you are copying data from Azure SQL Data Warehouse, set hello **source type** of hello copy activity too**SqlDWSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="566d6-891">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-891">Property</span></span> | <span data-ttu-id="566d6-892">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-892">Description</span></span> | <span data-ttu-id="566d6-893">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-893">Allowed values</span></span> | <span data-ttu-id="566d6-894">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-894">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-895">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="566d6-895">sqlReaderQuery</span></span> |<span data-ttu-id="566d6-896">使用自訂查詢 tooread hello 的資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-896">Use hello custom query tooread data.</span></span> |<span data-ttu-id="566d6-897">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="566d6-897">SQL query string.</span></span> <span data-ttu-id="566d6-898">例如： `select * from MyTable`。</span><span class="sxs-lookup"><span data-stu-id="566d6-898">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="566d6-899">否</span><span class="sxs-lookup"><span data-stu-id="566d6-899">No</span></span> |
| <span data-ttu-id="566d6-900">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="566d6-900">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="566d6-901">名稱的 hello 預存程序會從 hello 來源資料表讀取資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-901">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="566d6-902">名稱的 hello 預存程序。</span><span class="sxs-lookup"><span data-stu-id="566d6-902">Name of hello stored procedure.</span></span> |<span data-ttu-id="566d6-903">否</span><span class="sxs-lookup"><span data-stu-id="566d6-903">No</span></span> |
| <span data-ttu-id="566d6-904">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="566d6-904">storedProcedureParameters</span></span> |<span data-ttu-id="566d6-905">Hello 參數，預存程序。</span><span class="sxs-lookup"><span data-stu-id="566d6-905">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="566d6-906">名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="566d6-906">Name/value pairs.</span></span> <span data-ttu-id="566d6-907">名稱和大小寫的參數必須符合 hello 名稱和大小寫的 hello 預存程序參數。</span><span class="sxs-lookup"><span data-stu-id="566d6-907">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="566d6-908">否</span><span class="sxs-lookup"><span data-stu-id="566d6-908">No</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-909">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-909">Example</span></span>

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

<span data-ttu-id="566d6-910">如需詳細資訊，請參閱 [Azure SQL 資料倉儲連接器](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-910">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-dw-sink-in-copy-activity"></a><span data-ttu-id="566d6-911">複製活動中的 SQL DW 接收</span><span class="sxs-lookup"><span data-stu-id="566d6-911">SQL DW Sink in Copy Activity</span></span>
<span data-ttu-id="566d6-912">如果您複製資料 tooAzure SQL 資料倉儲，設定 hello**接收器類型**的 hello 複製活動太**SqlDWSink**，並指定下列屬性在 hello**接收**區段：</span><span class="sxs-lookup"><span data-stu-id="566d6-912">If you are copying data tooAzure SQL Data Warehouse, set hello **sink type** of hello copy activity too**SqlDWSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="566d6-913">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-913">Property</span></span> | <span data-ttu-id="566d6-914">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-914">Description</span></span> | <span data-ttu-id="566d6-915">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-915">Allowed values</span></span> | <span data-ttu-id="566d6-916">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-916">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-917">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="566d6-917">sqlWriterCleanupScript</span></span> |<span data-ttu-id="566d6-918">複製活動 tooexecute 查詢指定的特定配量的資料清除。</span><span class="sxs-lookup"><span data-stu-id="566d6-918">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="566d6-919">查詢陳述式。</span><span class="sxs-lookup"><span data-stu-id="566d6-919">A query statement.</span></span> |<span data-ttu-id="566d6-920">否</span><span class="sxs-lookup"><span data-stu-id="566d6-920">No</span></span> |
| <span data-ttu-id="566d6-921">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="566d6-921">allowPolyBase</span></span> |<span data-ttu-id="566d6-922">指出是否 toouse PolyBase （如果適用的話），而不是 BULKINSERT 機制。</span><span class="sxs-lookup"><span data-stu-id="566d6-922">Indicates whether toouse PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="566d6-923">**使用 PolyBase 是建議的方式 tooload 資料到 SQL 資料倉儲的 hello。**</span><span class="sxs-lookup"><span data-stu-id="566d6-923">**Using PolyBase is hello recommended way tooload data into SQL Data Warehouse.**</span></span> |<span data-ttu-id="566d6-924">True</span><span class="sxs-lookup"><span data-stu-id="566d6-924">True</span></span> <br/><span data-ttu-id="566d6-925">FALSE (預設值)</span><span class="sxs-lookup"><span data-stu-id="566d6-925">False (default)</span></span> |<span data-ttu-id="566d6-926">否</span><span class="sxs-lookup"><span data-stu-id="566d6-926">No</span></span> |
| <span data-ttu-id="566d6-927">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="566d6-927">polyBaseSettings</span></span> |<span data-ttu-id="566d6-928">一組屬性，可指定當 hello **allowPolybase**屬性設定太**true**。</span><span class="sxs-lookup"><span data-stu-id="566d6-928">A group of properties that can be specified when hello **allowPolybase** property is set too**true**.</span></span> |&nbsp; |<span data-ttu-id="566d6-929">否</span><span class="sxs-lookup"><span data-stu-id="566d6-929">No</span></span> |
| <span data-ttu-id="566d6-930">rejectValue</span><span class="sxs-lookup"><span data-stu-id="566d6-930">rejectValue</span></span> |<span data-ttu-id="566d6-931">指定 hello 數目或百分比的 hello 查詢失敗前，可能會拒絕的資料列。</span><span class="sxs-lookup"><span data-stu-id="566d6-931">Specifies hello number or percentage of rows that can be rejected before hello query fails.</span></span> <br/><br/><span data-ttu-id="566d6-932">深入了解 hello PolyBase 拒絕之選項的 hello**引數**區段[CREATE EXTERNAL TABLE (TRANSACT-SQL)](https://msdn.microsoft.com/library/dn935021.aspx)主題。</span><span class="sxs-lookup"><span data-stu-id="566d6-932">Learn more about hello PolyBase’s reject options in hello **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="566d6-933">0 (預設值)、1、2、…</span><span class="sxs-lookup"><span data-stu-id="566d6-933">0 (default), 1, 2, …</span></span> |<span data-ttu-id="566d6-934">否</span><span class="sxs-lookup"><span data-stu-id="566d6-934">No</span></span> |
| <span data-ttu-id="566d6-935">rejectType</span><span class="sxs-lookup"><span data-stu-id="566d6-935">rejectType</span></span> |<span data-ttu-id="566d6-936">指定是否要將 hello rejectValue 選項指定為常值或百分比。</span><span class="sxs-lookup"><span data-stu-id="566d6-936">Specifies whether hello rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="566d6-937">值 (預設值)、百分比</span><span class="sxs-lookup"><span data-stu-id="566d6-937">Value (default), Percentage</span></span> |<span data-ttu-id="566d6-938">否</span><span class="sxs-lookup"><span data-stu-id="566d6-938">No</span></span> |
| <span data-ttu-id="566d6-939">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="566d6-939">rejectSampleValue</span></span> |<span data-ttu-id="566d6-940">決定 hello 數量的資料列 tooretrieve hello PolyBase 重新計算 hello 百分比的已拒絕的資料列之前。</span><span class="sxs-lookup"><span data-stu-id="566d6-940">Determines hello number of rows tooretrieve before hello PolyBase recalculates hello percentage of rejected rows.</span></span> |<span data-ttu-id="566d6-941">1、2、…</span><span class="sxs-lookup"><span data-stu-id="566d6-941">1, 2, …</span></span> |<span data-ttu-id="566d6-942">是，如果 **rejectType** 是 **percentage**</span><span class="sxs-lookup"><span data-stu-id="566d6-942">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="566d6-943">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="566d6-943">useTypeDefault</span></span> |<span data-ttu-id="566d6-944">指定如何 toohandle 遺漏值中的分隔的文字檔案 PolyBase hello 文字檔案中擷取的資料時。</span><span class="sxs-lookup"><span data-stu-id="566d6-944">Specifies how toohandle missing values in delimited text files when PolyBase retrieves data from hello text file.</span></span><br/><br/><span data-ttu-id="566d6-945">深入了解來自 hello 引數 > 一節中的這個屬性[CREATE EXTERNAL FILE FORMAT (TRANSACT-SQL)](https://msdn.microsoft.com/library/dn935026.aspx)。</span><span class="sxs-lookup"><span data-stu-id="566d6-945">Learn more about this property from hello Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="566d6-946">True/False (預設值為 False)</span><span class="sxs-lookup"><span data-stu-id="566d6-946">True, False (default)</span></span> |<span data-ttu-id="566d6-947">否</span><span class="sxs-lookup"><span data-stu-id="566d6-947">No</span></span> |
| <span data-ttu-id="566d6-948">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="566d6-948">writeBatchSize</span></span> |<span data-ttu-id="566d6-949">用戶端 hello 緩衝區的大小達到叫用 writeBatchSize 時，將資料插入 hello SQL 資料表</span><span class="sxs-lookup"><span data-stu-id="566d6-949">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="566d6-950">整數 (資料列數目)</span><span class="sxs-lookup"><span data-stu-id="566d6-950">Integer (number of rows)</span></span> |<span data-ttu-id="566d6-951">否 (預設值：10000)</span><span class="sxs-lookup"><span data-stu-id="566d6-951">No (default: 10000)</span></span> |
| <span data-ttu-id="566d6-952">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="566d6-952">writeBatchTimeout</span></span> |<span data-ttu-id="566d6-953">在逾時之前，請等待 hello 批次插入作業 toocomplete 時間。</span><span class="sxs-lookup"><span data-stu-id="566d6-953">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="566d6-954">時間範圍</span><span class="sxs-lookup"><span data-stu-id="566d6-954">timespan</span></span><br/><br/> <span data-ttu-id="566d6-955">範例：“00:30:00” (30 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="566d6-955">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="566d6-956">否</span><span class="sxs-lookup"><span data-stu-id="566d6-956">No</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-957">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-957">Example</span></span>

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

<span data-ttu-id="566d6-958">如需詳細資訊，請參閱 [Azure SQL 資料倉儲連接器](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-958">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-search"></a><span data-ttu-id="566d6-959">Azure 搜尋服務</span><span class="sxs-lookup"><span data-stu-id="566d6-959">Azure Search</span></span>

### <a name="linked-service"></a><span data-ttu-id="566d6-960">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-960">Linked service</span></span>
<span data-ttu-id="566d6-961">Azure 搜尋 toodefine 連結服務，設定 hello**類型**hello 的連結服務太**AzureSearch**，並指定下列屬性在 hello **typeProperties**區段：</span><span class="sxs-lookup"><span data-stu-id="566d6-961">toodefine an Azure Search linked service, set hello **type** of hello linked service too**AzureSearch**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="566d6-962">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-962">Property</span></span> | <span data-ttu-id="566d6-963">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-963">Description</span></span> | <span data-ttu-id="566d6-964">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-964">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="566d6-965">url</span><span class="sxs-lookup"><span data-stu-id="566d6-965">url</span></span> | <span data-ttu-id="566d6-966">Hello Azure 搜尋服務的 URL。</span><span class="sxs-lookup"><span data-stu-id="566d6-966">URL for hello Azure Search service.</span></span> | <span data-ttu-id="566d6-967">是</span><span class="sxs-lookup"><span data-stu-id="566d6-967">Yes</span></span> |
| <span data-ttu-id="566d6-968">key</span><span class="sxs-lookup"><span data-stu-id="566d6-968">key</span></span> | <span data-ttu-id="566d6-969">Hello Azure 搜尋服務的管理金鑰。</span><span class="sxs-lookup"><span data-stu-id="566d6-969">Admin key for hello Azure Search service.</span></span> | <span data-ttu-id="566d6-970">是</span><span class="sxs-lookup"><span data-stu-id="566d6-970">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-971">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-971">Example</span></span>

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

<span data-ttu-id="566d6-972">如需詳細資訊，請參閱 [Azure 搜尋服務連接器](data-factory-azure-search-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-972">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="566d6-973">Dataset</span><span class="sxs-lookup"><span data-stu-id="566d6-973">Dataset</span></span>
<span data-ttu-id="566d6-974">toodefine Azure 搜尋資料集設定 hello**類型**hello 資料集太**AzureSearchIndex**，並指定下列屬性在 hello hello **typeProperties**區段:</span><span class="sxs-lookup"><span data-stu-id="566d6-974">toodefine an Azure Search dataset, set hello **type** of hello dataset too**AzureSearchIndex**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="566d6-975">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-975">Property</span></span> | <span data-ttu-id="566d6-976">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-976">Description</span></span> | <span data-ttu-id="566d6-977">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-977">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="566d6-978">類型</span><span class="sxs-lookup"><span data-stu-id="566d6-978">type</span></span> | <span data-ttu-id="566d6-979">hello type 屬性必須設定得**AzureSearchIndex**。</span><span class="sxs-lookup"><span data-stu-id="566d6-979">hello type property must be set too**AzureSearchIndex**.</span></span>| <span data-ttu-id="566d6-980">是</span><span class="sxs-lookup"><span data-stu-id="566d6-980">Yes</span></span> |
| <span data-ttu-id="566d6-981">IndexName</span><span class="sxs-lookup"><span data-stu-id="566d6-981">indexName</span></span> | <span data-ttu-id="566d6-982">Hello Azure 搜尋索引的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-982">Name of hello Azure Search index.</span></span> <span data-ttu-id="566d6-983">Data Factory 不會建立 hello 索引。</span><span class="sxs-lookup"><span data-stu-id="566d6-983">Data Factory does not create hello index.</span></span> <span data-ttu-id="566d6-984">hello 索引必須存在於 Azure 搜尋中。</span><span class="sxs-lookup"><span data-stu-id="566d6-984">hello index must exist in Azure Search.</span></span> | <span data-ttu-id="566d6-985">是</span><span class="sxs-lookup"><span data-stu-id="566d6-985">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-986">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-986">Example</span></span>

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

<span data-ttu-id="566d6-987">如需詳細資訊，請參閱 [Azure 搜尋服務連接器](data-factory-azure-search-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-987">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#dataset-properties) article.</span></span>

### <a name="azure-search-index-sink-in-copy-activity"></a><span data-ttu-id="566d6-988">複製活動中的 Azure 搜尋服務索引接收</span><span class="sxs-lookup"><span data-stu-id="566d6-988">Azure Search Index Sink in Copy Activity</span></span>
<span data-ttu-id="566d6-989">如果您要複製資料 tooan Azure 搜尋索引，請設定 hello**接收器類型**的 hello 複製活動太**AzureSearchIndexSink**，並指定下列屬性在 hello**接收**> 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-989">If you are copying data tooan Azure Search index, set hello **sink type** of hello copy activity too**AzureSearchIndexSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="566d6-990">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-990">Property</span></span> | <span data-ttu-id="566d6-991">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-991">Description</span></span> | <span data-ttu-id="566d6-992">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-992">Allowed values</span></span> | <span data-ttu-id="566d6-993">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-993">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="566d6-994">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="566d6-994">WriteBehavior</span></span> | <span data-ttu-id="566d6-995">指定是否 toomerge 或取代文件時已存在於 hello 索引。</span><span class="sxs-lookup"><span data-stu-id="566d6-995">Specifies whether toomerge or replace when a document already exists in hello index.</span></span> | <span data-ttu-id="566d6-996">合併 (預設值)</span><span class="sxs-lookup"><span data-stu-id="566d6-996">Merge (default)</span></span><br/><span data-ttu-id="566d6-997">上傳</span><span class="sxs-lookup"><span data-stu-id="566d6-997">Upload</span></span>| <span data-ttu-id="566d6-998">否</span><span class="sxs-lookup"><span data-stu-id="566d6-998">No</span></span> |
| <span data-ttu-id="566d6-999">WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="566d6-999">WriteBatchSize</span></span> | <span data-ttu-id="566d6-1000">將資料上傳至 hello Azure 搜尋索引，當 hello 緩衝區大小到達叫用 writeBatchSize 時。</span><span class="sxs-lookup"><span data-stu-id="566d6-1000">Uploads data into hello Azure Search index when hello buffer size reaches writeBatchSize.</span></span> | <span data-ttu-id="566d6-1001">1 too1，000。</span><span class="sxs-lookup"><span data-stu-id="566d6-1001">1 too1,000.</span></span> <span data-ttu-id="566d6-1002">預設值為 1000。</span><span class="sxs-lookup"><span data-stu-id="566d6-1002">Default value is 1000.</span></span> | <span data-ttu-id="566d6-1003">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1003">No</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-1004">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1004">Example</span></span>

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

<span data-ttu-id="566d6-1005">如需詳細資訊，請參閱 [Azure 搜尋服務連接器](data-factory-azure-search-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1005">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-table-storage"></a><span data-ttu-id="566d6-1006">Azure 表格儲存體</span><span class="sxs-lookup"><span data-stu-id="566d6-1006">Azure Table Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="566d6-1007">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-1007">Linked service</span></span>
<span data-ttu-id="566d6-1008">有兩種連結服務類型︰Azure 儲存體連結服務和 Azure 儲存體 SAS 連結服務。</span><span class="sxs-lookup"><span data-stu-id="566d6-1008">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="566d6-1009">Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-1009">Azure Storage Linked Service</span></span>
<span data-ttu-id="566d6-1010">toolink 您 Azure 儲存體帳戶 tooa 的 data factory 使用 hello**帳戶金鑰**，建立 Azure 儲存體連結服務。</span><span class="sxs-lookup"><span data-stu-id="566d6-1010">toolink your Azure storage account tooa data factory by using hello **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="566d6-1011">toodefine Azure 儲存體連結服務，設定 hello**類型**hello 的連結服務太**AzureStorage**。</span><span class="sxs-lookup"><span data-stu-id="566d6-1011">toodefine an Azure Storage linked service, set hello **type** of hello linked service too**AzureStorage**.</span></span> <span data-ttu-id="566d6-1012">然後，您可以指定下列屬性在 hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-1012">Then, you can specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="566d6-1013">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1013">Property</span></span> | <span data-ttu-id="566d6-1014">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1014">Description</span></span> | <span data-ttu-id="566d6-1015">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1015">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="566d6-1016">類型</span><span class="sxs-lookup"><span data-stu-id="566d6-1016">type</span></span> |<span data-ttu-id="566d6-1017">hello 類型屬性必須設定為： **AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="566d6-1017">hello type property must be set to: **AzureStorage**</span></span> |<span data-ttu-id="566d6-1018">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1018">Yes</span></span> |
| <span data-ttu-id="566d6-1019">connectionString</span><span class="sxs-lookup"><span data-stu-id="566d6-1019">connectionString</span></span> |<span data-ttu-id="566d6-1020">指定所需的資訊 tooconnect tooAzure 儲存體 hello connectionString 屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-1020">Specify information needed tooconnect tooAzure storage for hello connectionString property.</span></span> |<span data-ttu-id="566d6-1021">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1021">Yes</span></span> |

<span data-ttu-id="566d6-1022">**範例：**</span><span class="sxs-lookup"><span data-stu-id="566d6-1022">**Example:**</span></span>  

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

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="566d6-1023">Azure 儲存體 SAS 連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-1023">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="566d6-1024">hello Azure 儲存體 SAS 連結服務可讓您 Azure 儲存體帳戶 tooan Azure data factory toolink 使用共用存取簽章 (SAS)。</span><span class="sxs-lookup"><span data-stu-id="566d6-1024">hello Azure Storage SAS linked service allows you toolink an Azure Storage Account tooan Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="566d6-1025">它提供 hello 資料 factory 限制/時間繫結存取 tooall/特定資源 （blob/容器） hello 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="566d6-1025">It provides hello data factory with restricted/time-bound access tooall/specific resources (blob/container) in hello storage.</span></span> <span data-ttu-id="566d6-1026">toolink 使用共用存取簽章、 您 Azure 儲存體帳戶 tooa data factory 建立 Azure 儲存體 SAS 連結服務。</span><span class="sxs-lookup"><span data-stu-id="566d6-1026">toolink your Azure storage account tooa data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="566d6-1027">Azure 儲存體 SAS toodefine 連結服務，設定 hello**類型**hello 的連結服務太**AzureStorageSas**。</span><span class="sxs-lookup"><span data-stu-id="566d6-1027">toodefine an Azure Storage SAS linked service, set hello **type** of hello linked service too**AzureStorageSas**.</span></span> <span data-ttu-id="566d6-1028">然後，您可以指定下列屬性在 hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-1028">Then, you can specify following properties in hello **typeProperties** section:</span></span>   

| <span data-ttu-id="566d6-1029">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1029">Property</span></span> | <span data-ttu-id="566d6-1030">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1030">Description</span></span> | <span data-ttu-id="566d6-1031">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1031">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="566d6-1032">類型</span><span class="sxs-lookup"><span data-stu-id="566d6-1032">type</span></span> |<span data-ttu-id="566d6-1033">hello 類型屬性必須設定為： **AzureStorageSas**</span><span class="sxs-lookup"><span data-stu-id="566d6-1033">hello type property must be set to: **AzureStorageSas**</span></span> |<span data-ttu-id="566d6-1034">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1034">Yes</span></span> |
| <span data-ttu-id="566d6-1035">sasUri</span><span class="sxs-lookup"><span data-stu-id="566d6-1035">sasUri</span></span> |<span data-ttu-id="566d6-1036">指定共用存取簽章 URI toohello Azure 儲存體資源，例如 blob、 容器或資料表。</span><span class="sxs-lookup"><span data-stu-id="566d6-1036">Specify Shared Access Signature URI toohello Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="566d6-1037">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1037">Yes</span></span> |

<span data-ttu-id="566d6-1038">**範例：**</span><span class="sxs-lookup"><span data-stu-id="566d6-1038">**Example:**</span></span>

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

<span data-ttu-id="566d6-1039">如需這些連結服務的詳細資訊，請參閱 [Azure 表格儲存體連接器](data-factory-azure-table-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1039">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="566d6-1040">Dataset</span><span class="sxs-lookup"><span data-stu-id="566d6-1040">Dataset</span></span>
<span data-ttu-id="566d6-1041">toodefine 是 Azure 資料表的資料集，設定 hello**類型**hello 資料集太**AzureTable**，並指定下列屬性在 hello hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-1041">toodefine an Azure Table dataset, set hello **type** of hello dataset too**AzureTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="566d6-1042">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1042">Property</span></span> | <span data-ttu-id="566d6-1043">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1043">Description</span></span> | <span data-ttu-id="566d6-1044">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1044">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-1045">tableName</span><span class="sxs-lookup"><span data-stu-id="566d6-1045">tableName</span></span> |<span data-ttu-id="566d6-1046">參照的連結服務的 hello Azure 資料表的資料庫執行個體中的 hello 資料表的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1046">Name of hello table in hello Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="566d6-1047">是。</span><span class="sxs-lookup"><span data-stu-id="566d6-1047">Yes.</span></span> <span data-ttu-id="566d6-1048">當 tableName azureTableSourceQuery 沒有指定時，hello 資料表內的所有記錄都會複製的 toohello 目的地。</span><span class="sxs-lookup"><span data-stu-id="566d6-1048">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="566d6-1049">如果同時指定 azureTableSourceQuery，滿足 hello 查詢的 hello 資料表內的記錄將會複製的 toohello 目的地。</span><span class="sxs-lookup"><span data-stu-id="566d6-1049">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-1050">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1050">Example</span></span>

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

<span data-ttu-id="566d6-1051">如需這些連結服務的詳細資訊，請參閱 [Azure 表格儲存體連接器](data-factory-azure-table-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1051">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-table-source-in-copy-activity"></a><span data-ttu-id="566d6-1052">複製活動中的 Azure 資料表來源</span><span class="sxs-lookup"><span data-stu-id="566d6-1052">Azure Table Source in Copy Activity</span></span>
<span data-ttu-id="566d6-1053">如果您從 Azure 資料表儲存體複製資料，設定 hello**來源類型**的 hello 複製活動太**AzureTableSource**，並指定下列屬性在 hello**來源**> 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-1053">If you are copying data from Azure Table Storage, set hello **source type** of hello copy activity too**AzureTableSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="566d6-1054">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1054">Property</span></span> | <span data-ttu-id="566d6-1055">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1055">Description</span></span> | <span data-ttu-id="566d6-1056">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-1056">Allowed values</span></span> | <span data-ttu-id="566d6-1057">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1057">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-1058">AzureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="566d6-1058">azureTableSourceQuery</span></span> |<span data-ttu-id="566d6-1059">使用自訂查詢 tooread hello 的資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-1059">Use hello custom query tooread data.</span></span> |<span data-ttu-id="566d6-1060">Azure 資料表查詢字串。</span><span class="sxs-lookup"><span data-stu-id="566d6-1060">Azure table query string.</span></span> <span data-ttu-id="566d6-1061">請參閱 hello 下一節中的範例。</span><span class="sxs-lookup"><span data-stu-id="566d6-1061">See examples in hello next section.</span></span> |<span data-ttu-id="566d6-1062">否。</span><span class="sxs-lookup"><span data-stu-id="566d6-1062">No.</span></span> <span data-ttu-id="566d6-1063">當 tableName azureTableSourceQuery 沒有指定時，hello 資料表內的所有記錄都會複製的 toohello 目的地。</span><span class="sxs-lookup"><span data-stu-id="566d6-1063">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="566d6-1064">如果同時指定 azureTableSourceQuery，滿足 hello 查詢的 hello 資料表內的記錄將會複製的 toohello 目的地。</span><span class="sxs-lookup"><span data-stu-id="566d6-1064">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |
| <span data-ttu-id="566d6-1065">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="566d6-1065">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="566d6-1066">指出是否壓抑 hello 的資料表不存在例外狀況。</span><span class="sxs-lookup"><span data-stu-id="566d6-1066">Indicate whether swallow hello exception of table not exist.</span></span> |<span data-ttu-id="566d6-1067">TRUE</span><span class="sxs-lookup"><span data-stu-id="566d6-1067">TRUE</span></span><br/><span data-ttu-id="566d6-1068">FALSE</span><span class="sxs-lookup"><span data-stu-id="566d6-1068">FALSE</span></span> |<span data-ttu-id="566d6-1069">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1069">No</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-1070">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1070">Example</span></span>

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

<span data-ttu-id="566d6-1071">如需這些連結服務的詳細資訊，請參閱 [Azure 表格儲存體連接器](data-factory-azure-table-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1071">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

### <a name="azure-table-sink-in-copy-activity"></a><span data-ttu-id="566d6-1072">複製活動中的 Azure 資料表接收</span><span class="sxs-lookup"><span data-stu-id="566d6-1072">Azure Table Sink in Copy Activity</span></span>
<span data-ttu-id="566d6-1073">如果您要複製資料 tooAzure 資料表儲存體，請設定 hello**接收器類型**的 hello 複製活動太**AzureTableSink**，並指定下列屬性在 hello**接收**區段：</span><span class="sxs-lookup"><span data-stu-id="566d6-1073">If you are copying data tooAzure Table Storage, set hello **sink type** of hello copy activity too**AzureTableSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="566d6-1074">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1074">Property</span></span> | <span data-ttu-id="566d6-1075">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1075">Description</span></span> | <span data-ttu-id="566d6-1076">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-1076">Allowed values</span></span> | <span data-ttu-id="566d6-1077">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1077">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-1078">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="566d6-1078">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="566d6-1079">預設資料分割索引鍵值，可供 hello 接收。</span><span class="sxs-lookup"><span data-stu-id="566d6-1079">Default partition key value that can be used by hello sink.</span></span> |<span data-ttu-id="566d6-1080">字串值。</span><span class="sxs-lookup"><span data-stu-id="566d6-1080">A string value.</span></span> |<span data-ttu-id="566d6-1081">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1081">No</span></span> |
| <span data-ttu-id="566d6-1082">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="566d6-1082">azureTablePartitionKeyName</span></span> |<span data-ttu-id="566d6-1083">指定的值用做為資料分割索引鍵的 hello 資料行的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1083">Specify name of hello column whose values are used as partition keys.</span></span> <span data-ttu-id="566d6-1084">如果未指定，azuretabledefaultpartitionkeyvalue 會做為 hello 資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="566d6-1084">If not specified, AzureTableDefaultPartitionKeyValue is used as hello partition key.</span></span> |<span data-ttu-id="566d6-1085">資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1085">A column name.</span></span> |<span data-ttu-id="566d6-1086">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1086">No</span></span> |
| <span data-ttu-id="566d6-1087">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="566d6-1087">azureTableRowKeyName</span></span> |<span data-ttu-id="566d6-1088">指定的資料行值用做為資料列索引鍵的 hello 資料行的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1088">Specify name of hello column whose column values are used as row key.</span></span> <span data-ttu-id="566d6-1089">如果未指定，則會針對每個資料列使用 GUID。</span><span class="sxs-lookup"><span data-stu-id="566d6-1089">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="566d6-1090">資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1090">A column name.</span></span> |<span data-ttu-id="566d6-1091">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1091">No</span></span> |
| <span data-ttu-id="566d6-1092">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="566d6-1092">azureTableInsertType</span></span> |<span data-ttu-id="566d6-1093">hello 模式 tooinsert 資料插入 Azure 資料表。</span><span class="sxs-lookup"><span data-stu-id="566d6-1093">hello mode tooinsert data into Azure table.</span></span><br/><br/><span data-ttu-id="566d6-1094">這個屬性控制與相符的資料分割和資料列的索引鍵的 hello 輸出資料表中的現有資料列是否具有取代或合併其值。</span><span class="sxs-lookup"><span data-stu-id="566d6-1094">This property controls whether existing rows in hello output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="566d6-1095">toolearn 有關這些設定 （「 合併 」 和 「 取代 」） 的運作方式，請參閱[插入或合併實體](https://msdn.microsoft.com/library/azure/hh452241.aspx)和[插入或取代實體](https://msdn.microsoft.com/library/azure/hh452242.aspx)主題。</span><span class="sxs-lookup"><span data-stu-id="566d6-1095">toolearn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="566d6-1096">此設定適用於在 hello 資料列層級，不 hello 資料表層級，和這兩個選項會刪除 hello 輸出資料表不存在於 hello 輸入的資料列。</span><span class="sxs-lookup"><span data-stu-id="566d6-1096">This setting applies at hello row level, not hello table level, and neither option deletes rows in hello output table that do not exist in hello input.</span></span> |<span data-ttu-id="566d6-1097">合併 (預設值)</span><span class="sxs-lookup"><span data-stu-id="566d6-1097">merge (default)</span></span><br/><span data-ttu-id="566d6-1098">取代</span><span class="sxs-lookup"><span data-stu-id="566d6-1098">replace</span></span> |<span data-ttu-id="566d6-1099">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1099">No</span></span> |
| <span data-ttu-id="566d6-1100">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="566d6-1100">writeBatchSize</span></span> |<span data-ttu-id="566d6-1101">Hello 叫用 writeBatchSize 或 writeBatchTimeout 時，請將資料插入至 hello Azure 資料表中。</span><span class="sxs-lookup"><span data-stu-id="566d6-1101">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="566d6-1102">整數 (資料列數目)</span><span class="sxs-lookup"><span data-stu-id="566d6-1102">Integer (number of rows)</span></span> |<span data-ttu-id="566d6-1103">否 (預設值：10000)</span><span class="sxs-lookup"><span data-stu-id="566d6-1103">No (default: 10000)</span></span> |
| <span data-ttu-id="566d6-1104">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="566d6-1104">writeBatchTimeout</span></span> |<span data-ttu-id="566d6-1105">用戶端 hello 叫用 writeBatchSize 或 writeBatchTimeout 時，將資料插入 hello Azure 資料表</span><span class="sxs-lookup"><span data-stu-id="566d6-1105">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="566d6-1106">時間範圍</span><span class="sxs-lookup"><span data-stu-id="566d6-1106">timespan</span></span><br/><br/><span data-ttu-id="566d6-1107">範例：“00:20:00” (20 分鐘)</span><span class="sxs-lookup"><span data-stu-id="566d6-1107">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="566d6-1108">否 （預設 toostorage 用戶端預設逾時值 90 秒）</span><span class="sxs-lookup"><span data-stu-id="566d6-1108">No (Default toostorage client default timeout value 90 sec)</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-1109">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1109">Example</span></span>

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
<span data-ttu-id="566d6-1110">如需這些連結服務的詳細資訊，請參閱 [Azure 表格儲存體連接器](data-factory-azure-table-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1110">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="amazon-redshift"></a><span data-ttu-id="566d6-1111">Amazon RedShift</span><span class="sxs-lookup"><span data-stu-id="566d6-1111">Amazon RedShift</span></span>

### <a name="linked-service"></a><span data-ttu-id="566d6-1112">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-1112">Linked service</span></span>
<span data-ttu-id="566d6-1113">toodefine Amazon Redshift 連結服務，設定 hello**類型**hello 的連結服務太**AmazonRedshift**，並指定下列屬性在 hello **typeProperties**> 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-1113">toodefine an Amazon Redshift linked service, set hello **type** of hello linked service too**AmazonRedshift**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="566d6-1114">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1114">Property</span></span> | <span data-ttu-id="566d6-1115">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1115">Description</span></span> | <span data-ttu-id="566d6-1116">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1116">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-1117">伺服器</span><span class="sxs-lookup"><span data-stu-id="566d6-1117">server</span></span> |<span data-ttu-id="566d6-1118">IP 位址或主機名稱的 hello Amazon Redshift 伺服器。</span><span class="sxs-lookup"><span data-stu-id="566d6-1118">IP address or host name of hello Amazon Redshift server.</span></span> |<span data-ttu-id="566d6-1119">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1119">Yes</span></span> |
| <span data-ttu-id="566d6-1120">連接埠</span><span class="sxs-lookup"><span data-stu-id="566d6-1120">port</span></span> |<span data-ttu-id="566d6-1121">hello hello Amazon Redshift 伺服器 hello TCP 連接埠號碼使用 toolisten 用於用戶端連線。</span><span class="sxs-lookup"><span data-stu-id="566d6-1121">hello number of hello TCP port that hello Amazon Redshift server uses toolisten for client connections.</span></span> |<span data-ttu-id="566d6-1122">否，預設值︰5439</span><span class="sxs-lookup"><span data-stu-id="566d6-1122">No, default value: 5439</span></span> |
| <span data-ttu-id="566d6-1123">資料庫</span><span class="sxs-lookup"><span data-stu-id="566d6-1123">database</span></span> |<span data-ttu-id="566d6-1124">Hello Amazon Redshift 資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1124">Name of hello Amazon Redshift database.</span></span> |<span data-ttu-id="566d6-1125">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1125">Yes</span></span> |
| <span data-ttu-id="566d6-1126">username</span><span class="sxs-lookup"><span data-stu-id="566d6-1126">username</span></span> |<span data-ttu-id="566d6-1127">具有存取 toohello 資料庫使用者的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1127">Name of user who has access toohello database.</span></span> |<span data-ttu-id="566d6-1128">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1128">Yes</span></span> |
| <span data-ttu-id="566d6-1129">password</span><span class="sxs-lookup"><span data-stu-id="566d6-1129">password</span></span> |<span data-ttu-id="566d6-1130">Hello 使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="566d6-1130">Password for hello user account.</span></span> |<span data-ttu-id="566d6-1131">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1131">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-1132">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1132">Example</span></span>

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

<span data-ttu-id="566d6-1133">如需詳細資訊，請參閱 [Amazon Redshift 連接器](#data-factory-amazon-redshift-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1133">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="566d6-1134">Dataset</span><span class="sxs-lookup"><span data-stu-id="566d6-1134">Dataset</span></span>
<span data-ttu-id="566d6-1135">toodefine Amazon Redshift 資料集設定 hello**類型**hello 資料集太**RelationalTable**，並指定下列屬性在 hello hello **typeProperties**區段：</span><span class="sxs-lookup"><span data-stu-id="566d6-1135">toodefine an Amazon Redshift dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="566d6-1136">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1136">Property</span></span> | <span data-ttu-id="566d6-1137">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1137">Description</span></span> | <span data-ttu-id="566d6-1138">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1138">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-1139">tableName</span><span class="sxs-lookup"><span data-stu-id="566d6-1139">tableName</span></span> |<span data-ttu-id="566d6-1140">連結服務的 hello Amazon Redshift 資料庫中的 hello 資料表名稱參考。</span><span class="sxs-lookup"><span data-stu-id="566d6-1140">Name of hello table in hello Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="566d6-1141">否 (如果已指定 **RelationalSource** 的 **query**)</span><span class="sxs-lookup"><span data-stu-id="566d6-1141">No (if **query** of **RelationalSource** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="566d6-1142">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1142">Example</span></span>

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
<span data-ttu-id="566d6-1143">如需詳細資訊，請參閱 [Amazon Redshift 連接器](#data-factory-amazon-redshift-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1143">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="566d6-1144">複製活動中的關聯式來源</span><span class="sxs-lookup"><span data-stu-id="566d6-1144">Relational Source in Copy Activity</span></span> 
<span data-ttu-id="566d6-1145">如果您從 Amazon Redshift 複製資料，設定 hello**來源類型**的 hello 複製活動太**RelationalSource**，並指定下列屬性在 hello**來源**區段：</span><span class="sxs-lookup"><span data-stu-id="566d6-1145">If you are copying data from Amazon Redshift, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="566d6-1146">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1146">Property</span></span> | <span data-ttu-id="566d6-1147">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1147">Description</span></span> | <span data-ttu-id="566d6-1148">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-1148">Allowed values</span></span> | <span data-ttu-id="566d6-1149">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1149">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-1150">query</span><span class="sxs-lookup"><span data-stu-id="566d6-1150">query</span></span> |<span data-ttu-id="566d6-1151">使用自訂查詢 tooread hello 的資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-1151">Use hello custom query tooread data.</span></span> |<span data-ttu-id="566d6-1152">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="566d6-1152">SQL query string.</span></span> <span data-ttu-id="566d6-1153">例如： `select * from MyTable`。</span><span class="sxs-lookup"><span data-stu-id="566d6-1153">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="566d6-1154">否 (如果已指定 **dataset** 的 **tableName**)</span><span class="sxs-lookup"><span data-stu-id="566d6-1154">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-1155">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1155">Example</span></span>

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
<span data-ttu-id="566d6-1156">如需詳細資訊，請參閱 [Amazon Redshift 連接器](#data-factory-amazon-redshift-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1156">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#copy-activity-properties) article.</span></span>

## <a name="ibm-db2"></a><span data-ttu-id="566d6-1157">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="566d6-1157">IBM DB2</span></span>

### <a name="linked-service"></a><span data-ttu-id="566d6-1158">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-1158">Linked service</span></span>
<span data-ttu-id="566d6-1159">toodefine IBM DB2 連結服務，設定 hello**類型**hello 的連結服務太**OnPremisesDB2**，並指定下列屬性在 hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-1159">toodefine an IBM DB2 linked service, set hello **type** of hello linked service too**OnPremisesDB2**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="566d6-1160">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1160">Property</span></span> | <span data-ttu-id="566d6-1161">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1161">Description</span></span> | <span data-ttu-id="566d6-1162">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-1163">伺服器</span><span class="sxs-lookup"><span data-stu-id="566d6-1163">server</span></span> |<span data-ttu-id="566d6-1164">Hello DB2 伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1164">Name of hello DB2 server.</span></span> |<span data-ttu-id="566d6-1165">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1165">Yes</span></span> |
| <span data-ttu-id="566d6-1166">資料庫</span><span class="sxs-lookup"><span data-stu-id="566d6-1166">database</span></span> |<span data-ttu-id="566d6-1167">Hello DB2 資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1167">Name of hello DB2 database.</span></span> |<span data-ttu-id="566d6-1168">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1168">Yes</span></span> |
| <span data-ttu-id="566d6-1169">結構描述</span><span class="sxs-lookup"><span data-stu-id="566d6-1169">schema</span></span> |<span data-ttu-id="566d6-1170">Hello hello 資料庫中的結構描述名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1170">Name of hello schema in hello database.</span></span> <span data-ttu-id="566d6-1171">hello 結構描述名稱會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="566d6-1171">hello schema name is case-sensitive.</span></span> |<span data-ttu-id="566d6-1172">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1172">No</span></span> |
| <span data-ttu-id="566d6-1173">authenticationType</span><span class="sxs-lookup"><span data-stu-id="566d6-1173">authenticationType</span></span> |<span data-ttu-id="566d6-1174">Tooconnect toohello DB2 資料庫使用的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="566d6-1174">Type of authentication used tooconnect toohello DB2 database.</span></span> <span data-ttu-id="566d6-1175">可能的值為：匿名、基本和 Windows。</span><span class="sxs-lookup"><span data-stu-id="566d6-1175">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="566d6-1176">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1176">Yes</span></span> |
| <span data-ttu-id="566d6-1177">username</span><span class="sxs-lookup"><span data-stu-id="566d6-1177">username</span></span> |<span data-ttu-id="566d6-1178">如果您使用基本或 Windows 驗證，請指定使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1178">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="566d6-1179">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1179">No</span></span> |
| <span data-ttu-id="566d6-1180">password</span><span class="sxs-lookup"><span data-stu-id="566d6-1180">password</span></span> |<span data-ttu-id="566d6-1181">指定 hello hello 使用者名稱所指定的使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="566d6-1181">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="566d6-1182">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1182">No</span></span> |
| <span data-ttu-id="566d6-1183">gatewayName</span><span class="sxs-lookup"><span data-stu-id="566d6-1183">gatewayName</span></span> |<span data-ttu-id="566d6-1184">Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello 在內部部署 DB2 資料庫。</span><span class="sxs-lookup"><span data-stu-id="566d6-1184">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises DB2 database.</span></span> |<span data-ttu-id="566d6-1185">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1185">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-1186">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1186">Example</span></span>
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
<span data-ttu-id="566d6-1187">如需詳細資訊，請參閱 [IBM DB2 連接器](#data-factory-onprem-db2-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1187">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="566d6-1188">Dataset</span><span class="sxs-lookup"><span data-stu-id="566d6-1188">Dataset</span></span>
<span data-ttu-id="566d6-1189">toodefine DB2 資料集，設定 hello**類型**hello 資料集太**RelationalTable**，並指定下列屬性在 hello hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-1189">toodefine a DB2 dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span>

| <span data-ttu-id="566d6-1190">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1190">Property</span></span> | <span data-ttu-id="566d6-1191">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1191">Description</span></span> | <span data-ttu-id="566d6-1192">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1192">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-1193">tableName</span><span class="sxs-lookup"><span data-stu-id="566d6-1193">tableName</span></span> |<span data-ttu-id="566d6-1194">參照的連結服務的 hello DB2 資料庫執行個體中的 hello 資料表的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1194">Name of hello table in hello DB2 Database instance that linked service refers to.</span></span> <span data-ttu-id="566d6-1195">hello tableName 是區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="566d6-1195">hello tableName is case-sensitive.</span></span> |<span data-ttu-id="566d6-1196">否 (如果已指定 **RelationalSource** 的 **query**)</span><span class="sxs-lookup"><span data-stu-id="566d6-1196">No (if **query** of **RelationalSource** is specified)</span></span> 

#### <a name="example"></a><span data-ttu-id="566d6-1197">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1197">Example</span></span>
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

<span data-ttu-id="566d6-1198">如需詳細資訊，請參閱 [IBM DB2 連接器](#data-factory-onprem-db2-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1198">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="566d6-1199">複製活動中的關聯式來源</span><span class="sxs-lookup"><span data-stu-id="566d6-1199">Relational Source in Copy Activity</span></span>
<span data-ttu-id="566d6-1200">如果您從 IBM DB2 複製資料，設定 hello**來源類型**的 hello 複製活動太**RelationalSource**，並指定下列屬性在 hello**來源**> 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-1200">If you are copying data from IBM DB2, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="566d6-1201">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1201">Property</span></span> | <span data-ttu-id="566d6-1202">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1202">Description</span></span> | <span data-ttu-id="566d6-1203">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-1203">Allowed values</span></span> | <span data-ttu-id="566d6-1204">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1204">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-1205">query</span><span class="sxs-lookup"><span data-stu-id="566d6-1205">query</span></span> |<span data-ttu-id="566d6-1206">使用自訂查詢 tooread hello 的資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-1206">Use hello custom query tooread data.</span></span> |<span data-ttu-id="566d6-1207">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="566d6-1207">SQL query string.</span></span> <span data-ttu-id="566d6-1208">例如： `"query": "select * from "MySchema"."MyTable""`。</span><span class="sxs-lookup"><span data-stu-id="566d6-1208">For example: `"query": "select * from "MySchema"."MyTable""`.</span></span> |<span data-ttu-id="566d6-1209">否 (如果已指定 **dataset** 的 **tableName**)</span><span class="sxs-lookup"><span data-stu-id="566d6-1209">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-1210">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1210">Example</span></span>
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
<span data-ttu-id="566d6-1211">如需詳細資訊，請參閱 [IBM DB2 連接器](#data-factory-onprem-db2-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1211">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#copy-activity-properties) article.</span></span>

## <a name="mysql"></a><span data-ttu-id="566d6-1212">MySQL</span><span class="sxs-lookup"><span data-stu-id="566d6-1212">MySQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="566d6-1213">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-1213">Linked service</span></span>
<span data-ttu-id="566d6-1214">toodefine MySQL 連結服務，設定 hello**類型**hello 的連結服務太**OnPremisesMySql**，並指定下列屬性在 hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-1214">toodefine a MySQL linked service, set hello **type** of hello linked service too**OnPremisesMySql**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="566d6-1215">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1215">Property</span></span> | <span data-ttu-id="566d6-1216">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1216">Description</span></span> | <span data-ttu-id="566d6-1217">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1217">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-1218">伺服器</span><span class="sxs-lookup"><span data-stu-id="566d6-1218">server</span></span> |<span data-ttu-id="566d6-1219">Hello MySQL 伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1219">Name of hello MySQL server.</span></span> |<span data-ttu-id="566d6-1220">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1220">Yes</span></span> |
| <span data-ttu-id="566d6-1221">資料庫</span><span class="sxs-lookup"><span data-stu-id="566d6-1221">database</span></span> |<span data-ttu-id="566d6-1222">Hello MySQL 資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1222">Name of hello MySQL database.</span></span> |<span data-ttu-id="566d6-1223">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1223">Yes</span></span> |
| <span data-ttu-id="566d6-1224">結構描述</span><span class="sxs-lookup"><span data-stu-id="566d6-1224">schema</span></span> |<span data-ttu-id="566d6-1225">Hello hello 資料庫中的結構描述名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1225">Name of hello schema in hello database.</span></span> |<span data-ttu-id="566d6-1226">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1226">No</span></span> |
| <span data-ttu-id="566d6-1227">authenticationType</span><span class="sxs-lookup"><span data-stu-id="566d6-1227">authenticationType</span></span> |<span data-ttu-id="566d6-1228">Tooconnect toohello MySQL 資料庫使用的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="566d6-1228">Type of authentication used tooconnect toohello MySQL database.</span></span> <span data-ttu-id="566d6-1229">可能的值為：`Basic`。</span><span class="sxs-lookup"><span data-stu-id="566d6-1229">Possible values are: `Basic`.</span></span> |<span data-ttu-id="566d6-1230">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1230">Yes</span></span> |
| <span data-ttu-id="566d6-1231">username</span><span class="sxs-lookup"><span data-stu-id="566d6-1231">username</span></span> |<span data-ttu-id="566d6-1232">指定使用者名稱 tooconnect toohello MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="566d6-1232">Specify user name tooconnect toohello MySQL database.</span></span> |<span data-ttu-id="566d6-1233">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1233">Yes</span></span> |
| <span data-ttu-id="566d6-1234">password</span><span class="sxs-lookup"><span data-stu-id="566d6-1234">password</span></span> |<span data-ttu-id="566d6-1235">指定您所指定的 hello 使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="566d6-1235">Specify password for hello user account you specified.</span></span> |<span data-ttu-id="566d6-1236">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1236">Yes</span></span> |
| <span data-ttu-id="566d6-1237">gatewayName</span><span class="sxs-lookup"><span data-stu-id="566d6-1237">gatewayName</span></span> |<span data-ttu-id="566d6-1238">Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello 在內部部署 MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="566d6-1238">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises MySQL database.</span></span> |<span data-ttu-id="566d6-1239">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1239">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-1240">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1240">Example</span></span>

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

<span data-ttu-id="566d6-1241">如需詳細資訊，請參閱 [MySQL 連接器](data-factory-onprem-mysql-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1241">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="566d6-1242">Dataset</span><span class="sxs-lookup"><span data-stu-id="566d6-1242">Dataset</span></span>
<span data-ttu-id="566d6-1243">toodefine MySQL 資料集設定 hello**類型**hello 資料集太**RelationalTable**，並指定下列屬性在 hello hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-1243">toodefine a MySQL dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="566d6-1244">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1244">Property</span></span> | <span data-ttu-id="566d6-1245">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1245">Description</span></span> | <span data-ttu-id="566d6-1246">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-1247">tableName</span><span class="sxs-lookup"><span data-stu-id="566d6-1247">tableName</span></span> |<span data-ttu-id="566d6-1248">在 hello MySQL 資料庫連結的服務參考的執行個體中的 hello 資料表的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1248">Name of hello table in hello MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="566d6-1249">否 (如果已指定 **RelationalSource** 的 **query**)</span><span class="sxs-lookup"><span data-stu-id="566d6-1249">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-1250">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1250">Example</span></span>

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
<span data-ttu-id="566d6-1251">如需詳細資訊，請參閱 [MySQL 連接器](data-factory-onprem-mysql-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1251">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="566d6-1252">複製活動中的關聯式來源</span><span class="sxs-lookup"><span data-stu-id="566d6-1252">Relational Source in Copy Activity</span></span>
<span data-ttu-id="566d6-1253">如果您從 MySQL 資料庫複製資料，設定 hello**來源類型**的 hello 複製活動太**RelationalSource**，並指定下列屬性在 hello**來源**區段：</span><span class="sxs-lookup"><span data-stu-id="566d6-1253">If you are copying data from a MySQL database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="566d6-1254">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1254">Property</span></span> | <span data-ttu-id="566d6-1255">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1255">Description</span></span> | <span data-ttu-id="566d6-1256">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-1256">Allowed values</span></span> | <span data-ttu-id="566d6-1257">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1257">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-1258">query</span><span class="sxs-lookup"><span data-stu-id="566d6-1258">query</span></span> |<span data-ttu-id="566d6-1259">使用自訂查詢 tooread hello 的資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-1259">Use hello custom query tooread data.</span></span> |<span data-ttu-id="566d6-1260">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="566d6-1260">SQL query string.</span></span> <span data-ttu-id="566d6-1261">例如： `select * from MyTable`。</span><span class="sxs-lookup"><span data-stu-id="566d6-1261">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="566d6-1262">否 (如果已指定 **dataset** 的 **tableName**)</span><span class="sxs-lookup"><span data-stu-id="566d6-1262">No (if **tableName** of **dataset** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="566d6-1263">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1263">Example</span></span>
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

<span data-ttu-id="566d6-1264">如需詳細資訊，請參閱 [MySQL 連接器](data-factory-onprem-mysql-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1264">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="oracle"></a><span data-ttu-id="566d6-1265">Oracle</span><span class="sxs-lookup"><span data-stu-id="566d6-1265">Oracle</span></span> 

### <a name="linked-service"></a><span data-ttu-id="566d6-1266">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-1266">Linked service</span></span>
<span data-ttu-id="566d6-1267">toodefine Oracle 連結服務，設定 hello**類型**hello 的連結服務太**OnPremisesOracle**，並指定下列屬性在 hello **typeProperties**區段：</span><span class="sxs-lookup"><span data-stu-id="566d6-1267">toodefine an Oracle linked service, set hello **type** of hello linked service too**OnPremisesOracle**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="566d6-1268">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1268">Property</span></span> | <span data-ttu-id="566d6-1269">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1269">Description</span></span> | <span data-ttu-id="566d6-1270">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1270">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-1271">driverType</span><span class="sxs-lookup"><span data-stu-id="566d6-1271">driverType</span></span> | <span data-ttu-id="566d6-1272">指定從哪一個驅動程式 toouse toocopy 資料 / tooOracle 資料庫。</span><span class="sxs-lookup"><span data-stu-id="566d6-1272">Specify which driver toouse toocopy data from/tooOracle Database.</span></span> <span data-ttu-id="566d6-1273">允許的值為 **Microsoft** 或 **ODP** (預設值)。</span><span class="sxs-lookup"><span data-stu-id="566d6-1273">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="566d6-1274">如需驅動程式詳細資料，請參閱[支援的版本和安裝](#supported-versions-and-installation)一節。</span><span class="sxs-lookup"><span data-stu-id="566d6-1274">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="566d6-1275">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1275">No</span></span> |
| <span data-ttu-id="566d6-1276">connectionString</span><span class="sxs-lookup"><span data-stu-id="566d6-1276">connectionString</span></span> | <span data-ttu-id="566d6-1277">指定所需的資訊 tooconnect toohello Oracle 資料庫執行個體 hello connectionString 屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-1277">Specify information needed tooconnect toohello Oracle Database instance for hello connectionString property.</span></span> | <span data-ttu-id="566d6-1278">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1278">Yes</span></span> |
| <span data-ttu-id="566d6-1279">gatewayName</span><span class="sxs-lookup"><span data-stu-id="566d6-1279">gatewayName</span></span> | <span data-ttu-id="566d6-1280">Hello 閘道名稱，是使用的 tooconnect toohello 在內部部署 Oracle 伺服器</span><span class="sxs-lookup"><span data-stu-id="566d6-1280">Name of hello gateway that that is used tooconnect toohello on-premises Oracle server</span></span> |<span data-ttu-id="566d6-1281">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1281">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-1282">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1282">Example</span></span>
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

<span data-ttu-id="566d6-1283">如需詳細資訊，請參閱 [Oracle 連接器](data-factory-onprem-oracle-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1283">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="566d6-1284">Dataset</span><span class="sxs-lookup"><span data-stu-id="566d6-1284">Dataset</span></span>
<span data-ttu-id="566d6-1285">toodefine Oracle 資料集設定 hello**類型**hello 資料集太**OracleTable**，並指定下列屬性在 hello hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-1285">toodefine an Oracle dataset, set hello **type** of hello dataset too**OracleTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="566d6-1286">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1286">Property</span></span> | <span data-ttu-id="566d6-1287">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1287">Description</span></span> | <span data-ttu-id="566d6-1288">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1288">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-1289">tableName</span><span class="sxs-lookup"><span data-stu-id="566d6-1289">tableName</span></span> |<span data-ttu-id="566d6-1290">Hello hello 連結的服務的 Oracle 資料庫中的 hello 資料表名稱參考。</span><span class="sxs-lookup"><span data-stu-id="566d6-1290">Name of hello table in hello Oracle Database that hello linked service refers to.</span></span> |<span data-ttu-id="566d6-1291">否 (如果已指定 **OracleSource** 的 **oracleReaderQuery**)</span><span class="sxs-lookup"><span data-stu-id="566d6-1291">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-1292">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1292">Example</span></span>

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
<span data-ttu-id="566d6-1293">如需詳細資訊，請參閱 [Oracle 連接器](data-factory-onprem-oracle-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1293">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#dataset-properties) article.</span></span>

### <a name="oracle-source-in-copy-activity"></a><span data-ttu-id="566d6-1294">複製活動中的 Oracle 來源</span><span class="sxs-lookup"><span data-stu-id="566d6-1294">Oracle Source in Copy Activity</span></span>
<span data-ttu-id="566d6-1295">如果您從 Oracle 資料庫複製資料，設定 hello**來源類型**的 hello 複製活動太**OracleSource**，並指定下列屬性在 hello**來源**區段：</span><span class="sxs-lookup"><span data-stu-id="566d6-1295">If you are copying data from an Oracle database, set hello **source type** of hello copy activity too**OracleSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="566d6-1296">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1296">Property</span></span> | <span data-ttu-id="566d6-1297">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1297">Description</span></span> | <span data-ttu-id="566d6-1298">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-1298">Allowed values</span></span> | <span data-ttu-id="566d6-1299">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1299">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-1300">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="566d6-1300">oracleReaderQuery</span></span> |<span data-ttu-id="566d6-1301">使用自訂查詢 tooread hello 的資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-1301">Use hello custom query tooread data.</span></span> |<span data-ttu-id="566d6-1302">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="566d6-1302">SQL query string.</span></span> <span data-ttu-id="566d6-1303">例如：`select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="566d6-1303">For example: `select * from MyTable`</span></span> <br/><br/><span data-ttu-id="566d6-1304">如果未指定，hello 執行的 SQL 陳述式：`select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="566d6-1304">If not specified, hello SQL statement that is executed: `select * from MyTable`</span></span> |<span data-ttu-id="566d6-1305">否 (如果已指定 **dataset** 的 **tableName**)</span><span class="sxs-lookup"><span data-stu-id="566d6-1305">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-1306">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1306">Example</span></span>

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

<span data-ttu-id="566d6-1307">如需詳細資訊，請參閱 [Oracle 連接器](data-factory-onprem-oracle-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1307">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

### <a name="oracle-sink-in-copy-activity"></a><span data-ttu-id="566d6-1308">複製活動中的 Oracle 接收</span><span class="sxs-lookup"><span data-stu-id="566d6-1308">Oracle Sink in Copy Activity</span></span>
<span data-ttu-id="566d6-1309">如果您要複製資料 tooam Oracle 資料庫，請設定 hello**接收器類型**的 hello 複製活動太**OracleSink**，並指定下列屬性在 hello**接收**> 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-1309">If you are copying data tooam Oracle database, set hello **sink type** of hello copy activity too**OracleSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="566d6-1310">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1310">Property</span></span> | <span data-ttu-id="566d6-1311">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1311">Description</span></span> | <span data-ttu-id="566d6-1312">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-1312">Allowed values</span></span> | <span data-ttu-id="566d6-1313">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1313">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-1314">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="566d6-1314">writeBatchTimeout</span></span> |<span data-ttu-id="566d6-1315">在逾時之前，請等待 hello 批次插入作業 toocomplete 時間。</span><span class="sxs-lookup"><span data-stu-id="566d6-1315">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="566d6-1316">時間範圍</span><span class="sxs-lookup"><span data-stu-id="566d6-1316">timespan</span></span><br/><br/> <span data-ttu-id="566d6-1317">範例：00:30:00 (30 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="566d6-1317">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="566d6-1318">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1318">No</span></span> |
| <span data-ttu-id="566d6-1319">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="566d6-1319">writeBatchSize</span></span> |<span data-ttu-id="566d6-1320">當 hello 緩衝區大小到達叫用 writeBatchSize 時，請將資料插入 hello SQL 資料表。</span><span class="sxs-lookup"><span data-stu-id="566d6-1320">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="566d6-1321">整數 (資料列數目)</span><span class="sxs-lookup"><span data-stu-id="566d6-1321">Integer (number of rows)</span></span> |<span data-ttu-id="566d6-1322">否 (預設值：100)</span><span class="sxs-lookup"><span data-stu-id="566d6-1322">No (default: 100)</span></span> |
| <span data-ttu-id="566d6-1323">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="566d6-1323">sqlWriterCleanupScript</span></span> |<span data-ttu-id="566d6-1324">複製活動 tooexecute 查詢指定的特定配量的資料清除。</span><span class="sxs-lookup"><span data-stu-id="566d6-1324">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="566d6-1325">查詢陳述式。</span><span class="sxs-lookup"><span data-stu-id="566d6-1325">A query statement.</span></span> |<span data-ttu-id="566d6-1326">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1326">No</span></span> |
| <span data-ttu-id="566d6-1327">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="566d6-1327">sliceIdentifierColumnName</span></span> |<span data-ttu-id="566d6-1328">指定資料行名稱複製活動 toofill 與自動產生配量識別項，也就是使用的 tooclean 何時重新執行的特定配量的資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-1328">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="566d6-1329">資料類型為 binary(32) 之資料行的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1329">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="566d6-1330">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1330">No</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-1331">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1331">Example</span></span>
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
<span data-ttu-id="566d6-1332">如需詳細資訊，請參閱 [Oracle 連接器](data-factory-onprem-oracle-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1332">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

## <a name="postgresql"></a><span data-ttu-id="566d6-1333">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="566d6-1333">PostgreSQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="566d6-1334">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-1334">Linked service</span></span>
<span data-ttu-id="566d6-1335">toodefine PostgreSQL 連結服務，設定 hello**類型**hello 的連結服務太**OnPremisesPostgreSql**，並指定下列屬性在 hello **typeProperties**> 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-1335">toodefine a PostgreSQL linked service, set hello **type** of hello linked service too**OnPremisesPostgreSql**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="566d6-1336">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1336">Property</span></span> | <span data-ttu-id="566d6-1337">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1337">Description</span></span> | <span data-ttu-id="566d6-1338">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1338">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-1339">伺服器</span><span class="sxs-lookup"><span data-stu-id="566d6-1339">server</span></span> |<span data-ttu-id="566d6-1340">Hello PostgreSQL 伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1340">Name of hello PostgreSQL server.</span></span> |<span data-ttu-id="566d6-1341">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1341">Yes</span></span> |
| <span data-ttu-id="566d6-1342">資料庫</span><span class="sxs-lookup"><span data-stu-id="566d6-1342">database</span></span> |<span data-ttu-id="566d6-1343">Hello PostgreSQL 資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1343">Name of hello PostgreSQL database.</span></span> |<span data-ttu-id="566d6-1344">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1344">Yes</span></span> |
| <span data-ttu-id="566d6-1345">結構描述</span><span class="sxs-lookup"><span data-stu-id="566d6-1345">schema</span></span> |<span data-ttu-id="566d6-1346">Hello hello 資料庫中的結構描述名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1346">Name of hello schema in hello database.</span></span> <span data-ttu-id="566d6-1347">hello 結構描述名稱會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="566d6-1347">hello schema name is case-sensitive.</span></span> |<span data-ttu-id="566d6-1348">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1348">No</span></span> |
| <span data-ttu-id="566d6-1349">authenticationType</span><span class="sxs-lookup"><span data-stu-id="566d6-1349">authenticationType</span></span> |<span data-ttu-id="566d6-1350">Tooconnect toohello PostgreSQL 資料庫使用的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="566d6-1350">Type of authentication used tooconnect toohello PostgreSQL database.</span></span> <span data-ttu-id="566d6-1351">可能的值為：匿名、基本和 Windows。</span><span class="sxs-lookup"><span data-stu-id="566d6-1351">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="566d6-1352">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1352">Yes</span></span> |
| <span data-ttu-id="566d6-1353">username</span><span class="sxs-lookup"><span data-stu-id="566d6-1353">username</span></span> |<span data-ttu-id="566d6-1354">如果您使用基本或 Windows 驗證，請指定使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1354">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="566d6-1355">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1355">No</span></span> |
| <span data-ttu-id="566d6-1356">password</span><span class="sxs-lookup"><span data-stu-id="566d6-1356">password</span></span> |<span data-ttu-id="566d6-1357">指定 hello hello 使用者名稱所指定的使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="566d6-1357">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="566d6-1358">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1358">No</span></span> |
| <span data-ttu-id="566d6-1359">gatewayName</span><span class="sxs-lookup"><span data-stu-id="566d6-1359">gatewayName</span></span> |<span data-ttu-id="566d6-1360">Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello 在內部部署 PostgreSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="566d6-1360">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises PostgreSQL database.</span></span> |<span data-ttu-id="566d6-1361">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1361">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-1362">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1362">Example</span></span>

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
<span data-ttu-id="566d6-1363">如需詳細資訊，請參閱 [PostgreSQL 連接器](data-factory-onprem-postgresql-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1363">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="566d6-1364">Dataset</span><span class="sxs-lookup"><span data-stu-id="566d6-1364">Dataset</span></span>
<span data-ttu-id="566d6-1365">toodefine PostgreSQL 資料集設定 hello**類型**hello 資料集太**RelationalTable**，並指定下列屬性在 hello hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-1365">toodefine a PostgreSQL dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="566d6-1366">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1366">Property</span></span> | <span data-ttu-id="566d6-1367">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1367">Description</span></span> | <span data-ttu-id="566d6-1368">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1368">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-1369">tableName</span><span class="sxs-lookup"><span data-stu-id="566d6-1369">tableName</span></span> |<span data-ttu-id="566d6-1370">Hello PostgreSQL 資料庫連結的服務參考的執行個體中的 hello 資料表的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1370">Name of hello table in hello PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="566d6-1371">hello tableName 是區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="566d6-1371">hello tableName is case-sensitive.</span></span> |<span data-ttu-id="566d6-1372">否 (如果已指定 **RelationalSource** 的 **query**)</span><span class="sxs-lookup"><span data-stu-id="566d6-1372">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-1373">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1373">Example</span></span>
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
<span data-ttu-id="566d6-1374">如需詳細資訊，請參閱 [PostgreSQL 連接器](data-factory-onprem-postgresql-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1374">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="566d6-1375">複製活動中的關聯式來源</span><span class="sxs-lookup"><span data-stu-id="566d6-1375">Relational Source in Copy Activity</span></span>
<span data-ttu-id="566d6-1376">如果您從 PostgreSQL 資料庫複製資料，設定 hello**來源類型**的 hello 複製活動太**RelationalSource**，並指定下列屬性在 hello**來源**> 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-1376">If you are copying data from a PostgreSQL database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="566d6-1377">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1377">Property</span></span> | <span data-ttu-id="566d6-1378">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1378">Description</span></span> | <span data-ttu-id="566d6-1379">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-1379">Allowed values</span></span> | <span data-ttu-id="566d6-1380">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1380">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-1381">query</span><span class="sxs-lookup"><span data-stu-id="566d6-1381">query</span></span> |<span data-ttu-id="566d6-1382">使用自訂查詢 tooread hello 的資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-1382">Use hello custom query tooread data.</span></span> |<span data-ttu-id="566d6-1383">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="566d6-1383">SQL query string.</span></span> <span data-ttu-id="566d6-1384">例如："query": "select * from \"MySchema\".\"MyTable\""。</span><span class="sxs-lookup"><span data-stu-id="566d6-1384">For example: "query": "select * from \"MySchema\".\"MyTable\"".</span></span> |<span data-ttu-id="566d6-1385">否 (如果已指定 **dataset** 的 **tableName**)</span><span class="sxs-lookup"><span data-stu-id="566d6-1385">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-1386">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1386">Example</span></span>

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

<span data-ttu-id="566d6-1387">如需詳細資訊，請參閱 [PostgreSQL 連接器](data-factory-onprem-postgresql-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1387">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#copy-activity-properties) article.</span></span>

## <a name="sap-business-warehouse"></a><span data-ttu-id="566d6-1388">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="566d6-1388">SAP Business Warehouse</span></span>


### <a name="linked-service"></a><span data-ttu-id="566d6-1389">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-1389">Linked service</span></span>
<span data-ttu-id="566d6-1390">toodefine SAP Business 倉儲 (BW) 連結服務，設定 hello**類型**hello 的連結服務太**SapBw**，並指定下列屬性在 hello **typeProperties**> 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-1390">toodefine a SAP Business Warehouse (BW) linked service, set hello **type** of hello linked service too**SapBw**, and specify following properties in hello **typeProperties** section:</span></span>  

<span data-ttu-id="566d6-1391">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1391">Property</span></span> | <span data-ttu-id="566d6-1392">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1392">Description</span></span> | <span data-ttu-id="566d6-1393">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-1393">Allowed values</span></span> | <span data-ttu-id="566d6-1394">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1394">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="566d6-1395">伺服器</span><span class="sxs-lookup"><span data-stu-id="566d6-1395">server</span></span> | <span data-ttu-id="566d6-1396">執行個體所在的 hello SAP BW 的 hello 伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1396">Name of hello server on which hello SAP BW instance resides.</span></span> | <span data-ttu-id="566d6-1397">字串</span><span class="sxs-lookup"><span data-stu-id="566d6-1397">string</span></span> | <span data-ttu-id="566d6-1398">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1398">Yes</span></span>
<span data-ttu-id="566d6-1399">systemNumber</span><span class="sxs-lookup"><span data-stu-id="566d6-1399">systemNumber</span></span> | <span data-ttu-id="566d6-1400">Hello SAP BW 系統的系統編號。</span><span class="sxs-lookup"><span data-stu-id="566d6-1400">System number of hello SAP BW system.</span></span> | <span data-ttu-id="566d6-1401">以字串表示的二位數十進位數字。</span><span class="sxs-lookup"><span data-stu-id="566d6-1401">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="566d6-1402">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1402">Yes</span></span>
<span data-ttu-id="566d6-1403">clientId</span><span class="sxs-lookup"><span data-stu-id="566d6-1403">clientId</span></span> | <span data-ttu-id="566d6-1404">Hello W SAP 系統中的 hello 用戶端的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="566d6-1404">Client ID of hello client in hello SAP W system.</span></span> | <span data-ttu-id="566d6-1405">以字串表示的三位數十進位數字。</span><span class="sxs-lookup"><span data-stu-id="566d6-1405">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="566d6-1406">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1406">Yes</span></span>
<span data-ttu-id="566d6-1407">username</span><span class="sxs-lookup"><span data-stu-id="566d6-1407">username</span></span> | <span data-ttu-id="566d6-1408">Hello 使用者具有存取 toohello SAP 伺服器的名稱</span><span class="sxs-lookup"><span data-stu-id="566d6-1408">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="566d6-1409">字串</span><span class="sxs-lookup"><span data-stu-id="566d6-1409">string</span></span> | <span data-ttu-id="566d6-1410">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1410">Yes</span></span>
<span data-ttu-id="566d6-1411">password</span><span class="sxs-lookup"><span data-stu-id="566d6-1411">password</span></span> | <span data-ttu-id="566d6-1412">Hello 使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="566d6-1412">Password for hello user.</span></span> | <span data-ttu-id="566d6-1413">字串</span><span class="sxs-lookup"><span data-stu-id="566d6-1413">string</span></span> | <span data-ttu-id="566d6-1414">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1414">Yes</span></span>
<span data-ttu-id="566d6-1415">gatewayName</span><span class="sxs-lookup"><span data-stu-id="566d6-1415">gatewayName</span></span> | <span data-ttu-id="566d6-1416">Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello 在內部部署 SAP BW 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="566d6-1416">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP BW instance.</span></span> | <span data-ttu-id="566d6-1417">字串</span><span class="sxs-lookup"><span data-stu-id="566d6-1417">string</span></span> | <span data-ttu-id="566d6-1418">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1418">Yes</span></span>
<span data-ttu-id="566d6-1419">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="566d6-1419">encryptedCredential</span></span> | <span data-ttu-id="566d6-1420">hello 加密認證的字串。</span><span class="sxs-lookup"><span data-stu-id="566d6-1420">hello encrypted credential string.</span></span> | <span data-ttu-id="566d6-1421">字串</span><span class="sxs-lookup"><span data-stu-id="566d6-1421">string</span></span> | <span data-ttu-id="566d6-1422">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1422">No</span></span>

#### <a name="example"></a><span data-ttu-id="566d6-1423">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1423">Example</span></span>

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

<span data-ttu-id="566d6-1424">如需詳細資訊，請參閱 [SAP Business Warehouse 連接器](data-factory-sap-business-warehouse-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1424">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="566d6-1425">Dataset</span><span class="sxs-lookup"><span data-stu-id="566d6-1425">Dataset</span></span>
<span data-ttu-id="566d6-1426">toodefine SAP BW 資料集設定 hello**類型**hello 資料集太**RelationalTable**。</span><span class="sxs-lookup"><span data-stu-id="566d6-1426">toodefine a SAP BW dataset, set hello **type** of hello dataset too**RelationalTable**.</span></span> <span data-ttu-id="566d6-1427">支援的型別 hello SAP BW 資料集沒有特定型別的屬性**RelationalTable**。</span><span class="sxs-lookup"><span data-stu-id="566d6-1427">There are no type-specific properties supported for hello SAP BW dataset of type **RelationalTable**.</span></span>  

#### <a name="example"></a><span data-ttu-id="566d6-1428">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1428">Example</span></span>

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
<span data-ttu-id="566d6-1429">如需詳細資訊，請參閱 [SAP Business Warehouse 連接器](data-factory-sap-business-warehouse-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1429">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="566d6-1430">複製活動中的關聯式來源</span><span class="sxs-lookup"><span data-stu-id="566d6-1430">Relational Source in Copy Activity</span></span>
<span data-ttu-id="566d6-1431">如果您要從 SAP Business Warehouse 來複製資料，設定 hello**來源類型**的 hello 複製活動太**RelationalSource**，並指定下列屬性在 hello**來源**> 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-1431">If you are copying data from SAP Business Warehouse, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="566d6-1432">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1432">Property</span></span> | <span data-ttu-id="566d6-1433">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1433">Description</span></span> | <span data-ttu-id="566d6-1434">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-1434">Allowed values</span></span> | <span data-ttu-id="566d6-1435">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1435">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-1436">query</span><span class="sxs-lookup"><span data-stu-id="566d6-1436">query</span></span> | <span data-ttu-id="566d6-1437">指定 hello MDX 查詢 tooread 資料從 hello SAP BW 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="566d6-1437">Specifies hello MDX query tooread data from hello SAP BW instance.</span></span> | <span data-ttu-id="566d6-1438">MDX 查詢。</span><span class="sxs-lookup"><span data-stu-id="566d6-1438">MDX query.</span></span> | <span data-ttu-id="566d6-1439">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1439">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-1440">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1440">Example</span></span>

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

<span data-ttu-id="566d6-1441">如需詳細資訊，請參閱 [SAP Business Warehouse 連接器](data-factory-sap-business-warehouse-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1441">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sap-hana"></a><span data-ttu-id="566d6-1442">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="566d6-1442">SAP HANA</span></span>

### <a name="linked-service"></a><span data-ttu-id="566d6-1443">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-1443">Linked service</span></span>
<span data-ttu-id="566d6-1444">SAP HANA toodefine 連結服務，設定 hello**類型**hello 的連結服務太**SapHana**，並指定下列屬性在 hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-1444">toodefine a SAP HANA linked service, set hello **type** of hello linked service too**SapHana**, and specify following properties in hello **typeProperties** section:</span></span>  

<span data-ttu-id="566d6-1445">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1445">Property</span></span> | <span data-ttu-id="566d6-1446">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1446">Description</span></span> | <span data-ttu-id="566d6-1447">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-1447">Allowed values</span></span> | <span data-ttu-id="566d6-1448">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1448">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="566d6-1449">伺服器</span><span class="sxs-lookup"><span data-stu-id="566d6-1449">server</span></span> | <span data-ttu-id="566d6-1450">執行個體所在的 hello SAP HANA hello 伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1450">Name of hello server on which hello SAP HANA instance resides.</span></span> <span data-ttu-id="566d6-1451">如果您的伺服器使用自訂連接埠，指定 `server:port`。</span><span class="sxs-lookup"><span data-stu-id="566d6-1451">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="566d6-1452">字串</span><span class="sxs-lookup"><span data-stu-id="566d6-1452">string</span></span> | <span data-ttu-id="566d6-1453">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1453">Yes</span></span>
<span data-ttu-id="566d6-1454">authenticationType</span><span class="sxs-lookup"><span data-stu-id="566d6-1454">authenticationType</span></span> | <span data-ttu-id="566d6-1455">驗證類型。</span><span class="sxs-lookup"><span data-stu-id="566d6-1455">Type of authentication.</span></span> | <span data-ttu-id="566d6-1456">字串。</span><span class="sxs-lookup"><span data-stu-id="566d6-1456">string.</span></span> <span data-ttu-id="566d6-1457">"Basic" 或 "Windows"</span><span class="sxs-lookup"><span data-stu-id="566d6-1457">"Basic" or "Windows"</span></span> | <span data-ttu-id="566d6-1458">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1458">Yes</span></span> 
<span data-ttu-id="566d6-1459">username</span><span class="sxs-lookup"><span data-stu-id="566d6-1459">username</span></span> | <span data-ttu-id="566d6-1460">Hello 使用者具有存取 toohello SAP 伺服器的名稱</span><span class="sxs-lookup"><span data-stu-id="566d6-1460">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="566d6-1461">字串</span><span class="sxs-lookup"><span data-stu-id="566d6-1461">string</span></span> | <span data-ttu-id="566d6-1462">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1462">Yes</span></span>
<span data-ttu-id="566d6-1463">password</span><span class="sxs-lookup"><span data-stu-id="566d6-1463">password</span></span> | <span data-ttu-id="566d6-1464">Hello 使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="566d6-1464">Password for hello user.</span></span> | <span data-ttu-id="566d6-1465">字串</span><span class="sxs-lookup"><span data-stu-id="566d6-1465">string</span></span> | <span data-ttu-id="566d6-1466">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1466">Yes</span></span>
<span data-ttu-id="566d6-1467">gatewayName</span><span class="sxs-lookup"><span data-stu-id="566d6-1467">gatewayName</span></span> | <span data-ttu-id="566d6-1468">Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello 在內部部署 SAP HANA 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="566d6-1468">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP HANA instance.</span></span> | <span data-ttu-id="566d6-1469">字串</span><span class="sxs-lookup"><span data-stu-id="566d6-1469">string</span></span> | <span data-ttu-id="566d6-1470">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1470">Yes</span></span>
<span data-ttu-id="566d6-1471">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="566d6-1471">encryptedCredential</span></span> | <span data-ttu-id="566d6-1472">hello 加密認證的字串。</span><span class="sxs-lookup"><span data-stu-id="566d6-1472">hello encrypted credential string.</span></span> | <span data-ttu-id="566d6-1473">字串</span><span class="sxs-lookup"><span data-stu-id="566d6-1473">string</span></span> | <span data-ttu-id="566d6-1474">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1474">No</span></span>

#### <a name="example"></a><span data-ttu-id="566d6-1475">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1475">Example</span></span>

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
<span data-ttu-id="566d6-1476">如需詳細資訊，請參閱 [SAP HANA 連接器](data-factory-sap-hana-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1476">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#linked-service-properties) article.</span></span>
 
### <a name="dataset"></a><span data-ttu-id="566d6-1477">Dataset</span><span class="sxs-lookup"><span data-stu-id="566d6-1477">Dataset</span></span>
<span data-ttu-id="566d6-1478">toodefine SAP HANA 資料集設定 hello**類型**hello 資料集太**RelationalTable**。</span><span class="sxs-lookup"><span data-stu-id="566d6-1478">toodefine a SAP HANA dataset, set hello **type** of hello dataset too**RelationalTable**.</span></span> <span data-ttu-id="566d6-1479">支援的型別 hello SAP HANA 資料集沒有特定型別的屬性**RelationalTable**。</span><span class="sxs-lookup"><span data-stu-id="566d6-1479">There are no type-specific properties supported for hello SAP HANA dataset of type **RelationalTable**.</span></span> 

#### <a name="example"></a><span data-ttu-id="566d6-1480">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1480">Example</span></span>

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
<span data-ttu-id="566d6-1481">如需詳細資訊，請參閱 [SAP HANA 連接器](data-factory-sap-hana-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1481">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="566d6-1482">複製活動中的關聯式來源</span><span class="sxs-lookup"><span data-stu-id="566d6-1482">Relational Source in Copy Activity</span></span>
<span data-ttu-id="566d6-1483">如果您從 SAP HANA 資料存放區複製資料，設定 hello**來源類型**的 hello 複製活動太**RelationalSource**，並指定下列屬性在 hello**來源**> 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-1483">If you are copying data from a SAP HANA data store, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="566d6-1484">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1484">Property</span></span> | <span data-ttu-id="566d6-1485">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1485">Description</span></span> | <span data-ttu-id="566d6-1486">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-1486">Allowed values</span></span> | <span data-ttu-id="566d6-1487">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1487">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-1488">query</span><span class="sxs-lookup"><span data-stu-id="566d6-1488">query</span></span> | <span data-ttu-id="566d6-1489">指定 hello SQL 查詢 tooread 資料從 hello SAP HANA 執行個體。</span><span class="sxs-lookup"><span data-stu-id="566d6-1489">Specifies hello SQL query tooread data from hello SAP HANA instance.</span></span> | <span data-ttu-id="566d6-1490">SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="566d6-1490">SQL query.</span></span> | <span data-ttu-id="566d6-1491">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1491">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="566d6-1492">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1492">Example</span></span>


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

<span data-ttu-id="566d6-1493">如需詳細資訊，請參閱 [SAP HANA 連接器](data-factory-sap-hana-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1493">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#copy-activity-properties) article.</span></span>


## <a name="sql-server"></a><span data-ttu-id="566d6-1494">SQL Server</span><span class="sxs-lookup"><span data-stu-id="566d6-1494">SQL Server</span></span>

### <a name="linked-service"></a><span data-ttu-id="566d6-1495">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-1495">Linked service</span></span>
<span data-ttu-id="566d6-1496">您建立連結的服務型別的**OnPremisesSqlServer** toolink 在內部部署 SQL Server 資料庫 tooa 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="566d6-1496">You create a linked service of type **OnPremisesSqlServer** toolink an on-premises SQL Server database tooa data factory.</span></span> <span data-ttu-id="566d6-1497">下表中的 hello 提供 JSON 項目特定 tooon 內部部署 SQL Server 連結服務的描述。</span><span class="sxs-lookup"><span data-stu-id="566d6-1497">hello following table provides description for JSON elements specific tooon-premises SQL Server linked service.</span></span>

<span data-ttu-id="566d6-1498">下表中的 hello 提供 JSON 項目特定 tooSQL 連結的伺服器服務的描述。</span><span class="sxs-lookup"><span data-stu-id="566d6-1498">hello following table provides description for JSON elements specific tooSQL Server linked service.</span></span>

| <span data-ttu-id="566d6-1499">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1499">Property</span></span> | <span data-ttu-id="566d6-1500">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1500">Description</span></span> | <span data-ttu-id="566d6-1501">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1501">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-1502">類型</span><span class="sxs-lookup"><span data-stu-id="566d6-1502">type</span></span> |<span data-ttu-id="566d6-1503">hello 類型屬性應該設定為： **OnPremisesSqlServer**。</span><span class="sxs-lookup"><span data-stu-id="566d6-1503">hello type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="566d6-1504">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1504">Yes</span></span> |
| <span data-ttu-id="566d6-1505">connectionString</span><span class="sxs-lookup"><span data-stu-id="566d6-1505">connectionString</span></span> |<span data-ttu-id="566d6-1506">指定所需的 connectionString 資訊 tooconnect toohello 在內部部署 SQL Server 資料庫使用 SQL 驗證或 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="566d6-1506">Specify connectionString information needed tooconnect toohello on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="566d6-1507">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1507">Yes</span></span> |
| <span data-ttu-id="566d6-1508">gatewayName</span><span class="sxs-lookup"><span data-stu-id="566d6-1508">gatewayName</span></span> |<span data-ttu-id="566d6-1509">Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello 在內部部署 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="566d6-1509">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SQL Server database.</span></span> |<span data-ttu-id="566d6-1510">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1510">Yes</span></span> |
| <span data-ttu-id="566d6-1511">username</span><span class="sxs-lookup"><span data-stu-id="566d6-1511">username</span></span> |<span data-ttu-id="566d6-1512">如果您使用「Windows 驗證」，請指定使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1512">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="566d6-1513">範例︰**domainname\\username**。</span><span class="sxs-lookup"><span data-stu-id="566d6-1513">Example: **domainname\\username**.</span></span> |<span data-ttu-id="566d6-1514">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1514">No</span></span> |
| <span data-ttu-id="566d6-1515">password</span><span class="sxs-lookup"><span data-stu-id="566d6-1515">password</span></span> |<span data-ttu-id="566d6-1516">指定 hello hello 使用者名稱所指定的使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="566d6-1516">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="566d6-1517">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1517">No</span></span> |

<span data-ttu-id="566d6-1518">您可以加密認證使用 hello**新增 AzureRmDataFactoryEncryptValue** cmdlet 並將其用於 hello 連接字串 hello 下列範例所示 (**EncryptedCredential**屬性):</span><span class="sxs-lookup"><span data-stu-id="566d6-1518">You can encrypt credentials using hello **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in hello connection string as shown in hello following example (**EncryptedCredential** property):</span></span>  

```json
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="566d6-1519">範例：用於 SQL 驗證的 JSON</span><span class="sxs-lookup"><span data-stu-id="566d6-1519">Example: JSON for using SQL Authentication</span></span>

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
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="566d6-1520">範例：用於 Windows 驗證的 JSON</span><span class="sxs-lookup"><span data-stu-id="566d6-1520">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="566d6-1521">如果未指定使用者名稱和密碼，閘道會使用這些 tooimpersonate hello 指定的使用者帳戶 tooconnect toohello 在內部部署 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="566d6-1521">If username and password are specified, gateway uses them tooimpersonate hello specified user account tooconnect toohello on-premises SQL Server database.</span></span> <span data-ttu-id="566d6-1522">否則，閘道會直接與 hello 的閘道 （其啟動帳戶） 的安全性內容連線 toohello SQL Server。</span><span class="sxs-lookup"><span data-stu-id="566d6-1522">Otherwise, gateway connects toohello SQL Server directly with hello security context of Gateway (its startup account).</span></span>

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

<span data-ttu-id="566d6-1523">如需詳細資訊，請參閱 [SQL Server 連接器](data-factory-sqlserver-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1523">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="566d6-1524">Dataset</span><span class="sxs-lookup"><span data-stu-id="566d6-1524">Dataset</span></span>
<span data-ttu-id="566d6-1525">toodefine SQL Server 資料集設定 hello**類型**hello 資料集太**SqlServerTable**，並指定下列屬性在 hello hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-1525">toodefine a SQL Server dataset, set hello **type** of hello dataset too**SqlServerTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="566d6-1526">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1526">Property</span></span> | <span data-ttu-id="566d6-1527">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1527">Description</span></span> | <span data-ttu-id="566d6-1528">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1528">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-1529">tableName</span><span class="sxs-lookup"><span data-stu-id="566d6-1529">tableName</span></span> |<span data-ttu-id="566d6-1530">參照 hello 資料表或檢視中的連結服務的 hello 的 SQL Server 資料庫執行個體的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1530">Name of hello table or view in hello SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="566d6-1531">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1531">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-1532">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1532">Example</span></span>
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

<span data-ttu-id="566d6-1533">如需詳細資訊，請參閱 [SQL Server 連接器](data-factory-sqlserver-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1533">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="566d6-1534">複製活動中的 Sql 來源</span><span class="sxs-lookup"><span data-stu-id="566d6-1534">Sql Source in Copy Activity</span></span>
<span data-ttu-id="566d6-1535">如果您從 SQL Server 資料庫複製資料，設定 hello**來源類型**的 hello 複製活動太**SqlSource**，並指定下列屬性在 hello**來源**區段：</span><span class="sxs-lookup"><span data-stu-id="566d6-1535">If you are copying data from a SQL Server database, set hello **source type** of hello copy activity too**SqlSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="566d6-1536">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1536">Property</span></span> | <span data-ttu-id="566d6-1537">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1537">Description</span></span> | <span data-ttu-id="566d6-1538">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-1538">Allowed values</span></span> | <span data-ttu-id="566d6-1539">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1539">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-1540">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="566d6-1540">sqlReaderQuery</span></span> |<span data-ttu-id="566d6-1541">使用自訂查詢 tooread hello 的資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-1541">Use hello custom query tooread data.</span></span> |<span data-ttu-id="566d6-1542">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="566d6-1542">SQL query string.</span></span> <span data-ttu-id="566d6-1543">例如： `select * from MyTable`。</span><span class="sxs-lookup"><span data-stu-id="566d6-1543">For example: `select * from MyTable`.</span></span> <span data-ttu-id="566d6-1544">從 hello hello 輸入資料集所參考的資料庫，可以參考多個資料表。</span><span class="sxs-lookup"><span data-stu-id="566d6-1544">May reference multiple tables from hello database referenced by hello input dataset.</span></span> <span data-ttu-id="566d6-1545">如果未指定，hello 執行的 SQL 陳述式： select from MyTable。</span><span class="sxs-lookup"><span data-stu-id="566d6-1545">If not specified, hello SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="566d6-1546">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1546">No</span></span> |
| <span data-ttu-id="566d6-1547">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="566d6-1547">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="566d6-1548">名稱的 hello 預存程序會從 hello 來源資料表讀取資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-1548">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="566d6-1549">名稱的 hello 預存程序。</span><span class="sxs-lookup"><span data-stu-id="566d6-1549">Name of hello stored procedure.</span></span> |<span data-ttu-id="566d6-1550">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1550">No</span></span> |
| <span data-ttu-id="566d6-1551">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="566d6-1551">storedProcedureParameters</span></span> |<span data-ttu-id="566d6-1552">Hello 參數，預存程序。</span><span class="sxs-lookup"><span data-stu-id="566d6-1552">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="566d6-1553">名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="566d6-1553">Name/value pairs.</span></span> <span data-ttu-id="566d6-1554">名稱和大小寫的參數必須符合 hello 名稱和大小寫的 hello 預存程序參數。</span><span class="sxs-lookup"><span data-stu-id="566d6-1554">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="566d6-1555">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1555">No</span></span> |

<span data-ttu-id="566d6-1556">如果 hello **sqlReaderQuery**指定 hello SqlSource，hello 複製活動會針對 hello 的 SQL Server 資料庫來源 tooget hello 資料執行此查詢。</span><span class="sxs-lookup"><span data-stu-id="566d6-1556">If hello **sqlReaderQuery** is specified for hello SqlSource, hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span>

<span data-ttu-id="566d6-1557">或者，您可以指定預存程序，藉由指定 hello **sqlReaderStoredProcedureName**和**storedProcedureParameters** （如果 hello 預存程序會採用參數）。</span><span class="sxs-lookup"><span data-stu-id="566d6-1557">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="566d6-1558">如果您未指定 sqlReaderQuery 或 sqlReaderStoredProcedureName，hello hello 結構區段中定義的資料行是使用的 toobuild select 查詢 toorun 針對 hello 的 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="566d6-1558">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="566d6-1559">如果您不需要 hello 資料集定義 hello 結構，所有資料行選取的 hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="566d6-1559">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="566d6-1560">當您使用**sqlReaderStoredProcedureName**，您仍然需要 toospecify 值 hello **tableName** hello 資料集 JSON 中的屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-1560">When you use **sqlReaderStoredProcedureName**, you still need toospecify a value for hello **tableName** property in hello dataset JSON.</span></span> <span data-ttu-id="566d6-1561">雖然目前尚未針對此資料表來進行驗證。</span><span class="sxs-lookup"><span data-stu-id="566d6-1561">There are no validations performed against this table though.</span></span>


#### <a name="example"></a><span data-ttu-id="566d6-1562">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1562">Example</span></span>
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

<span data-ttu-id="566d6-1563">在此範例中， **sqlReaderQuery** hello SqlSource 指定。</span><span class="sxs-lookup"><span data-stu-id="566d6-1563">In this example, **sqlReaderQuery** is specified for hello SqlSource.</span></span> <span data-ttu-id="566d6-1564">hello 複製活動會針對 hello 的 SQL Server 資料庫來源 tooget hello 資料執行此查詢。</span><span class="sxs-lookup"><span data-stu-id="566d6-1564">hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span> <span data-ttu-id="566d6-1565">或者，您可以指定預存程序，藉由指定 hello **sqlReaderStoredProcedureName**和**storedProcedureParameters** （如果 hello 預存程序會採用參數）。</span><span class="sxs-lookup"><span data-stu-id="566d6-1565">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span> <span data-ttu-id="566d6-1566">hello sqlReaderQuery 參考 hello hello 輸入資料集所參考的資料庫內的多個資料表。</span><span class="sxs-lookup"><span data-stu-id="566d6-1566">hello sqlReaderQuery can reference multiple tables within hello database referenced by hello input dataset.</span></span> <span data-ttu-id="566d6-1567">它不是設定為 hello 資料集的 tableName typeProperty 有限的 tooonly hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="566d6-1567">It is not limited tooonly hello table set as hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="566d6-1568">如果您未指定 sqlReaderQuery 或 sqlReaderStoredProcedureName，hello hello 結構區段中定義的資料行是使用的 toobuild select 查詢 toorun 針對 hello 的 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="566d6-1568">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="566d6-1569">如果您不需要 hello 資料集定義 hello 結構，所有資料行選取的 hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="566d6-1569">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

<span data-ttu-id="566d6-1570">如需詳細資訊，請參閱 [SQL Server 連接器](data-factory-sqlserver-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1570">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="566d6-1571">複製活動中的 Sql 接收</span><span class="sxs-lookup"><span data-stu-id="566d6-1571">Sql Sink in Copy Activity</span></span>
<span data-ttu-id="566d6-1572">如果您要複製資料 tooa SQL Server 資料庫，請設定 hello**接收器類型**的 hello 複製活動太**SqlSink**，並指定下列屬性在 hello**接收**> 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-1572">If you are copying data tooa SQL Server database, set hello **sink type** of hello copy activity too**SqlSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="566d6-1573">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1573">Property</span></span> | <span data-ttu-id="566d6-1574">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1574">Description</span></span> | <span data-ttu-id="566d6-1575">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-1575">Allowed values</span></span> | <span data-ttu-id="566d6-1576">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1576">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-1577">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="566d6-1577">writeBatchTimeout</span></span> |<span data-ttu-id="566d6-1578">在逾時之前，請等待 hello 批次插入作業 toocomplete 時間。</span><span class="sxs-lookup"><span data-stu-id="566d6-1578">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="566d6-1579">時間範圍</span><span class="sxs-lookup"><span data-stu-id="566d6-1579">timespan</span></span><br/><br/> <span data-ttu-id="566d6-1580">範例：“00:30:00” (30 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="566d6-1580">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="566d6-1581">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1581">No</span></span> |
| <span data-ttu-id="566d6-1582">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="566d6-1582">writeBatchSize</span></span> |<span data-ttu-id="566d6-1583">當 hello 緩衝區大小到達叫用 writeBatchSize 時，請將資料插入 hello SQL 資料表。</span><span class="sxs-lookup"><span data-stu-id="566d6-1583">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="566d6-1584">整數 (資料列數目)</span><span class="sxs-lookup"><span data-stu-id="566d6-1584">Integer (number of rows)</span></span> |<span data-ttu-id="566d6-1585">否 (預設值：10000)</span><span class="sxs-lookup"><span data-stu-id="566d6-1585">No (default: 10000)</span></span> |
| <span data-ttu-id="566d6-1586">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="566d6-1586">sqlWriterCleanupScript</span></span> |<span data-ttu-id="566d6-1587">複製活動 tooexecute 查詢指定的特定配量的資料清除。</span><span class="sxs-lookup"><span data-stu-id="566d6-1587">Specify query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="566d6-1588">如需詳細資訊，請參閱 [可重複性](#repeatability-during-copy) 一節。</span><span class="sxs-lookup"><span data-stu-id="566d6-1588">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="566d6-1589">查詢陳述式。</span><span class="sxs-lookup"><span data-stu-id="566d6-1589">A query statement.</span></span> |<span data-ttu-id="566d6-1590">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1590">No</span></span> |
| <span data-ttu-id="566d6-1591">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="566d6-1591">sliceIdentifierColumnName</span></span> |<span data-ttu-id="566d6-1592">指定資料行名稱複製活動 toofill 與自動產生配量識別項，也就是使用的 tooclean 何時重新執行的特定配量的資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-1592">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> <span data-ttu-id="566d6-1593">如需詳細資訊，請參閱 [可重複性](#repeatability-during-copy) 一節。</span><span class="sxs-lookup"><span data-stu-id="566d6-1593">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="566d6-1594">資料類型為 binary(32) 之資料行的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1594">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="566d6-1595">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1595">No</span></span> |
| <span data-ttu-id="566d6-1596">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="566d6-1596">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="566d6-1597">名稱的 hello 預存程序 upserts （更新/插入） 資料到 hello 目標資料表。</span><span class="sxs-lookup"><span data-stu-id="566d6-1597">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="566d6-1598">名稱的 hello 預存程序。</span><span class="sxs-lookup"><span data-stu-id="566d6-1598">Name of hello stored procedure.</span></span> |<span data-ttu-id="566d6-1599">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1599">No</span></span> |
| <span data-ttu-id="566d6-1600">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="566d6-1600">storedProcedureParameters</span></span> |<span data-ttu-id="566d6-1601">Hello 參數，預存程序。</span><span class="sxs-lookup"><span data-stu-id="566d6-1601">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="566d6-1602">名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="566d6-1602">Name/value pairs.</span></span> <span data-ttu-id="566d6-1603">名稱和大小寫的參數必須符合 hello 名稱和大小寫的 hello 預存程序參數。</span><span class="sxs-lookup"><span data-stu-id="566d6-1603">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="566d6-1604">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1604">No</span></span> |
| <span data-ttu-id="566d6-1605">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="566d6-1605">sqlWriterTableType</span></span> |<span data-ttu-id="566d6-1606">指定資料表類型名稱 toobe hello 預存程序中使用。</span><span class="sxs-lookup"><span data-stu-id="566d6-1606">Specify table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="566d6-1607">複製活動移動 hello 資料可讓在暫存資料表與此資料表類型。</span><span class="sxs-lookup"><span data-stu-id="566d6-1607">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="566d6-1608">預存程序程式碼可以再合併 hello 資料會被複製現有的資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-1608">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="566d6-1609">資料表類型名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1609">A table type name.</span></span> |<span data-ttu-id="566d6-1610">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1610">No</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-1611">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1611">Example</span></span>
<span data-ttu-id="566d6-1612">hello 管線包含複製活動的設定的 toouse 這些輸入和輸出資料集，而排程的 toorun 每小時。</span><span class="sxs-lookup"><span data-stu-id="566d6-1612">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="566d6-1613">在 hello 管線 JSON 定義中，hello**來源**類型設定得**BlobSource**和**接收**類型設定得**SqlSink**。</span><span class="sxs-lookup"><span data-stu-id="566d6-1613">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

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

<span data-ttu-id="566d6-1614">如需詳細資訊，請參閱 [SQL Server 連接器](data-factory-sqlserver-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1614">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sybase"></a><span data-ttu-id="566d6-1615">Sybase</span><span class="sxs-lookup"><span data-stu-id="566d6-1615">Sybase</span></span>

### <a name="linked-service"></a><span data-ttu-id="566d6-1616">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-1616">Linked service</span></span>
<span data-ttu-id="566d6-1617">toodefine Sybase 連結服務，設定 hello**類型**hello 的連結服務太**OnPremisesSybase**，並指定下列屬性在 hello **typeProperties**區段：</span><span class="sxs-lookup"><span data-stu-id="566d6-1617">toodefine a Sybase linked service, set hello **type** of hello linked service too**OnPremisesSybase**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="566d6-1618">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1618">Property</span></span> | <span data-ttu-id="566d6-1619">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1619">Description</span></span> | <span data-ttu-id="566d6-1620">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1620">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-1621">伺服器</span><span class="sxs-lookup"><span data-stu-id="566d6-1621">server</span></span> |<span data-ttu-id="566d6-1622">Hello Sybase 伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1622">Name of hello Sybase server.</span></span> |<span data-ttu-id="566d6-1623">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1623">Yes</span></span> |
| <span data-ttu-id="566d6-1624">資料庫</span><span class="sxs-lookup"><span data-stu-id="566d6-1624">database</span></span> |<span data-ttu-id="566d6-1625">Hello Sybase 資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1625">Name of hello Sybase database.</span></span> |<span data-ttu-id="566d6-1626">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1626">Yes</span></span> |
| <span data-ttu-id="566d6-1627">結構描述</span><span class="sxs-lookup"><span data-stu-id="566d6-1627">schema</span></span> |<span data-ttu-id="566d6-1628">Hello hello 資料庫中的結構描述名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1628">Name of hello schema in hello database.</span></span> |<span data-ttu-id="566d6-1629">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1629">No</span></span> |
| <span data-ttu-id="566d6-1630">authenticationType</span><span class="sxs-lookup"><span data-stu-id="566d6-1630">authenticationType</span></span> |<span data-ttu-id="566d6-1631">Tooconnect toohello Sybase 資料庫使用的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="566d6-1631">Type of authentication used tooconnect toohello Sybase database.</span></span> <span data-ttu-id="566d6-1632">可能的值為：匿名、基本和 Windows。</span><span class="sxs-lookup"><span data-stu-id="566d6-1632">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="566d6-1633">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1633">Yes</span></span> |
| <span data-ttu-id="566d6-1634">username</span><span class="sxs-lookup"><span data-stu-id="566d6-1634">username</span></span> |<span data-ttu-id="566d6-1635">如果您使用基本或 Windows 驗證，請指定使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1635">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="566d6-1636">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1636">No</span></span> |
| <span data-ttu-id="566d6-1637">password</span><span class="sxs-lookup"><span data-stu-id="566d6-1637">password</span></span> |<span data-ttu-id="566d6-1638">指定 hello hello 使用者名稱所指定的使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="566d6-1638">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="566d6-1639">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1639">No</span></span> |
| <span data-ttu-id="566d6-1640">gatewayName</span><span class="sxs-lookup"><span data-stu-id="566d6-1640">gatewayName</span></span> |<span data-ttu-id="566d6-1641">Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello 在內部部署 Sybase 資料庫。</span><span class="sxs-lookup"><span data-stu-id="566d6-1641">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Sybase database.</span></span> |<span data-ttu-id="566d6-1642">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1642">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-1643">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1643">Example</span></span>
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

<span data-ttu-id="566d6-1644">如需詳細資訊，請參閱 [Sybase 連接器](data-factory-onprem-sybase-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1644">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="566d6-1645">Dataset</span><span class="sxs-lookup"><span data-stu-id="566d6-1645">Dataset</span></span>
<span data-ttu-id="566d6-1646">toodefine Sybase 資料集設定 hello**類型**hello 資料集太**RelationalTable**，並指定下列屬性在 hello hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-1646">toodefine a Sybase dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="566d6-1647">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1647">Property</span></span> | <span data-ttu-id="566d6-1648">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1648">Description</span></span> | <span data-ttu-id="566d6-1649">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1649">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-1650">tableName</span><span class="sxs-lookup"><span data-stu-id="566d6-1650">tableName</span></span> |<span data-ttu-id="566d6-1651">Hello Sybase 資料庫連結的服務參考的執行個體中的 hello 資料表的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1651">Name of hello table in hello Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="566d6-1652">否 (如果已指定 **RelationalSource** 的 **query**)</span><span class="sxs-lookup"><span data-stu-id="566d6-1652">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-1653">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1653">Example</span></span>

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

<span data-ttu-id="566d6-1654">如需詳細資訊，請參閱 [Sybase 連接器](data-factory-onprem-sybase-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1654">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="566d6-1655">複製活動中的關聯式來源</span><span class="sxs-lookup"><span data-stu-id="566d6-1655">Relational Source in Copy Activity</span></span>
<span data-ttu-id="566d6-1656">如果您從 Sybase 資料庫複製資料，設定 hello**來源類型**的 hello 複製活動太**RelationalSource**，並指定下列屬性在 hello**來源**區段：</span><span class="sxs-lookup"><span data-stu-id="566d6-1656">If you are copying data from a Sybase database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="566d6-1657">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1657">Property</span></span> | <span data-ttu-id="566d6-1658">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1658">Description</span></span> | <span data-ttu-id="566d6-1659">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-1659">Allowed values</span></span> | <span data-ttu-id="566d6-1660">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1660">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-1661">query</span><span class="sxs-lookup"><span data-stu-id="566d6-1661">query</span></span> |<span data-ttu-id="566d6-1662">使用自訂查詢 tooread hello 的資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-1662">Use hello custom query tooread data.</span></span> |<span data-ttu-id="566d6-1663">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="566d6-1663">SQL query string.</span></span> <span data-ttu-id="566d6-1664">例如： `select * from MyTable`。</span><span class="sxs-lookup"><span data-stu-id="566d6-1664">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="566d6-1665">否 (如果已指定 **dataset** 的 **tableName**)</span><span class="sxs-lookup"><span data-stu-id="566d6-1665">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-1666">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1666">Example</span></span>

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

<span data-ttu-id="566d6-1667">如需詳細資訊，請參閱 [Sybase 連接器](data-factory-onprem-sybase-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1667">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#copy-activity-properties) article.</span></span>

## <a name="teradata"></a><span data-ttu-id="566d6-1668">Teradata</span><span class="sxs-lookup"><span data-stu-id="566d6-1668">Teradata</span></span>

### <a name="linked-service"></a><span data-ttu-id="566d6-1669">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-1669">Linked service</span></span>
<span data-ttu-id="566d6-1670">toodefine Teradata 連結服務，設定 hello**類型**hello 的連結服務太**OnPremisesTeradata**，並指定下列屬性在 hello **typeProperties**區段：</span><span class="sxs-lookup"><span data-stu-id="566d6-1670">toodefine a Teradata linked service, set hello **type** of hello linked service too**OnPremisesTeradata**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="566d6-1671">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1671">Property</span></span> | <span data-ttu-id="566d6-1672">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1672">Description</span></span> | <span data-ttu-id="566d6-1673">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1673">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-1674">伺服器</span><span class="sxs-lookup"><span data-stu-id="566d6-1674">server</span></span> |<span data-ttu-id="566d6-1675">Hello Teradata 伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1675">Name of hello Teradata server.</span></span> |<span data-ttu-id="566d6-1676">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1676">Yes</span></span> |
| <span data-ttu-id="566d6-1677">authenticationType</span><span class="sxs-lookup"><span data-stu-id="566d6-1677">authenticationType</span></span> |<span data-ttu-id="566d6-1678">Tooconnect toohello Teradata 資料庫使用的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="566d6-1678">Type of authentication used tooconnect toohello Teradata database.</span></span> <span data-ttu-id="566d6-1679">可能的值為：匿名、基本和 Windows。</span><span class="sxs-lookup"><span data-stu-id="566d6-1679">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="566d6-1680">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1680">Yes</span></span> |
| <span data-ttu-id="566d6-1681">username</span><span class="sxs-lookup"><span data-stu-id="566d6-1681">username</span></span> |<span data-ttu-id="566d6-1682">如果您使用基本或 Windows 驗證，請指定使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1682">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="566d6-1683">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1683">No</span></span> |
| <span data-ttu-id="566d6-1684">password</span><span class="sxs-lookup"><span data-stu-id="566d6-1684">password</span></span> |<span data-ttu-id="566d6-1685">指定 hello hello 使用者名稱所指定的使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="566d6-1685">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="566d6-1686">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1686">No</span></span> |
| <span data-ttu-id="566d6-1687">gatewayName</span><span class="sxs-lookup"><span data-stu-id="566d6-1687">gatewayName</span></span> |<span data-ttu-id="566d6-1688">Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello 在內部部署 Teradata 資料庫。</span><span class="sxs-lookup"><span data-stu-id="566d6-1688">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Teradata database.</span></span> |<span data-ttu-id="566d6-1689">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1689">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-1690">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1690">Example</span></span>
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

<span data-ttu-id="566d6-1691">如需詳細資訊，請參閱 [Teradata 連接器](data-factory-onprem-teradata-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1691">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="566d6-1692">Dataset</span><span class="sxs-lookup"><span data-stu-id="566d6-1692">Dataset</span></span>
<span data-ttu-id="566d6-1693">toodefine Teradata Blob 資料集設定 hello**類型**hello 資料集太**RelationalTable**。</span><span class="sxs-lookup"><span data-stu-id="566d6-1693">toodefine a Teradata Blob dataset, set hello **type** of hello dataset too**RelationalTable**.</span></span> <span data-ttu-id="566d6-1694">目前沒有任何支援 hello Teradata 資料集的類型屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-1694">Currently, there are no type properties supported for hello Teradata dataset.</span></span> 

#### <a name="example"></a><span data-ttu-id="566d6-1695">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1695">Example</span></span>
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

<span data-ttu-id="566d6-1696">如需詳細資訊，請參閱 [Teradata 連接器](data-factory-onprem-teradata-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1696">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="566d6-1697">複製活動中的關聯式來源</span><span class="sxs-lookup"><span data-stu-id="566d6-1697">Relational Source in Copy Activity</span></span>
<span data-ttu-id="566d6-1698">如果您要從 Teradata 資料庫來複製資料，設定 hello**來源類型**的 hello 複製活動太**RelationalSource**，並指定下列屬性在 hello**來源**> 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-1698">If you are copying data from a Teradata database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="566d6-1699">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1699">Property</span></span> | <span data-ttu-id="566d6-1700">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1700">Description</span></span> | <span data-ttu-id="566d6-1701">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-1701">Allowed values</span></span> | <span data-ttu-id="566d6-1702">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1702">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-1703">query</span><span class="sxs-lookup"><span data-stu-id="566d6-1703">query</span></span> |<span data-ttu-id="566d6-1704">使用自訂查詢 tooread hello 的資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-1704">Use hello custom query tooread data.</span></span> |<span data-ttu-id="566d6-1705">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="566d6-1705">SQL query string.</span></span> <span data-ttu-id="566d6-1706">例如： `select * from MyTable`。</span><span class="sxs-lookup"><span data-stu-id="566d6-1706">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="566d6-1707">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1707">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-1708">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1708">Example</span></span>

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

<span data-ttu-id="566d6-1709">如需詳細資訊，請參閱 [Teradata 連接器](data-factory-onprem-teradata-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1709">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#copy-activity-properties) article.</span></span>

## <a name="cassandra"></a><span data-ttu-id="566d6-1710">Cassandra</span><span class="sxs-lookup"><span data-stu-id="566d6-1710">Cassandra</span></span>


### <a name="linked-service"></a><span data-ttu-id="566d6-1711">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-1711">Linked service</span></span>
<span data-ttu-id="566d6-1712">toodefine Cassandra 連結服務，設定 hello**類型**hello 的連結服務太**OnPremisesCassandra**，並指定下列屬性在 hello **typeProperties**區段：</span><span class="sxs-lookup"><span data-stu-id="566d6-1712">toodefine a Cassandra linked service, set hello **type** of hello linked service too**OnPremisesCassandra**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="566d6-1713">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1713">Property</span></span> | <span data-ttu-id="566d6-1714">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1714">Description</span></span> | <span data-ttu-id="566d6-1715">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1715">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-1716">主機</span><span class="sxs-lookup"><span data-stu-id="566d6-1716">host</span></span> |<span data-ttu-id="566d6-1717">一或多個 Cassandra 伺服器 IP 位址或主機名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1717">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="566d6-1718">同時指定以逗號分隔的 IP 位址或主機名稱 tooconnect tooall 伺服器清單。</span><span class="sxs-lookup"><span data-stu-id="566d6-1718">Specify a comma-separated list of IP addresses or host names tooconnect tooall servers concurrently.</span></span> |<span data-ttu-id="566d6-1719">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1719">Yes</span></span> |
| <span data-ttu-id="566d6-1720">連接埠</span><span class="sxs-lookup"><span data-stu-id="566d6-1720">port</span></span> |<span data-ttu-id="566d6-1721">hello hello Cassandra 伺服器的 TCP 連接埠會使用用戶端連線 toolisten。</span><span class="sxs-lookup"><span data-stu-id="566d6-1721">hello TCP port that hello Cassandra server uses toolisten for client connections.</span></span> |<span data-ttu-id="566d6-1722">否，預設值：9042</span><span class="sxs-lookup"><span data-stu-id="566d6-1722">No, default value: 9042</span></span> |
| <span data-ttu-id="566d6-1723">authenticationType</span><span class="sxs-lookup"><span data-stu-id="566d6-1723">authenticationType</span></span> |<span data-ttu-id="566d6-1724">基本或匿名</span><span class="sxs-lookup"><span data-stu-id="566d6-1724">Basic, or Anonymous</span></span> |<span data-ttu-id="566d6-1725">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1725">Yes</span></span> |
| <span data-ttu-id="566d6-1726">username</span><span class="sxs-lookup"><span data-stu-id="566d6-1726">username</span></span> |<span data-ttu-id="566d6-1727">指定 hello 使用者帳戶的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1727">Specify user name for hello user account.</span></span> |<span data-ttu-id="566d6-1728">是，如果設定 tooBasic authenticationType。</span><span class="sxs-lookup"><span data-stu-id="566d6-1728">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="566d6-1729">password</span><span class="sxs-lookup"><span data-stu-id="566d6-1729">password</span></span> |<span data-ttu-id="566d6-1730">指定 hello 使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="566d6-1730">Specify password for hello user account.</span></span> |<span data-ttu-id="566d6-1731">是，如果設定 tooBasic authenticationType。</span><span class="sxs-lookup"><span data-stu-id="566d6-1731">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="566d6-1732">gatewayName</span><span class="sxs-lookup"><span data-stu-id="566d6-1732">gatewayName</span></span> |<span data-ttu-id="566d6-1733">hello hello 閘道所使用的 tooconnect toohello 內部 Cassandra 資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1733">hello name of hello gateway that is used tooconnect toohello on-premises Cassandra database.</span></span> |<span data-ttu-id="566d6-1734">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1734">Yes</span></span> |
| <span data-ttu-id="566d6-1735">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="566d6-1735">encryptedCredential</span></span> |<span data-ttu-id="566d6-1736">加密的 hello 閘道的認證。</span><span class="sxs-lookup"><span data-stu-id="566d6-1736">Credential encrypted by hello gateway.</span></span> |<span data-ttu-id="566d6-1737">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1737">No</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-1738">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1738">Example</span></span>

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

<span data-ttu-id="566d6-1739">如需詳細資訊，請參閱 [Cassandra 連接器](data-factory-onprem-cassandra-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1739">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="566d6-1740">Dataset</span><span class="sxs-lookup"><span data-stu-id="566d6-1740">Dataset</span></span>
<span data-ttu-id="566d6-1741">toodefine Cassandra 資料集設定 hello**類型**hello 資料集太**CassandraTable**，並指定下列屬性在 hello hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-1741">toodefine a Cassandra dataset, set hello **type** of hello dataset too**CassandraTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="566d6-1742">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1742">Property</span></span> | <span data-ttu-id="566d6-1743">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1743">Description</span></span> | <span data-ttu-id="566d6-1744">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1744">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-1745">keyspace</span><span class="sxs-lookup"><span data-stu-id="566d6-1745">keyspace</span></span> |<span data-ttu-id="566d6-1746">Hello keyspace 或 Cassandra 資料庫中的結構描述的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1746">Name of hello keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="566d6-1747">是 (如果未定義 **CassandraSource** 的**查詢**)。</span><span class="sxs-lookup"><span data-stu-id="566d6-1747">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="566d6-1748">tableName</span><span class="sxs-lookup"><span data-stu-id="566d6-1748">tableName</span></span> |<span data-ttu-id="566d6-1749">Cassandra 資料庫中的 hello 資料表的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1749">Name of hello table in Cassandra database.</span></span> |<span data-ttu-id="566d6-1750">是 (如果未定義 **CassandraSource** 的**查詢**)。</span><span class="sxs-lookup"><span data-stu-id="566d6-1750">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-1751">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1751">Example</span></span>

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

<span data-ttu-id="566d6-1752">如需詳細資訊，請參閱 [Cassandra 連接器](data-factory-onprem-cassandra-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1752">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#dataset-properties) article.</span></span> 

### <a name="cassandra-source-in-copy-activity"></a><span data-ttu-id="566d6-1753">複製活動中的 SCassandra 來源</span><span class="sxs-lookup"><span data-stu-id="566d6-1753">Cassandra Source in Copy Activity</span></span>
<span data-ttu-id="566d6-1754">如果您從 Cassandra 複製資料，設定 hello**來源類型**的 hello 複製活動太**CassandraSource**，並指定下列屬性在 hello**來源**區段:</span><span class="sxs-lookup"><span data-stu-id="566d6-1754">If you are copying data from Cassandra, set hello **source type** of hello copy activity too**CassandraSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="566d6-1755">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1755">Property</span></span> | <span data-ttu-id="566d6-1756">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1756">Description</span></span> | <span data-ttu-id="566d6-1757">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-1757">Allowed values</span></span> | <span data-ttu-id="566d6-1758">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1758">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-1759">query</span><span class="sxs-lookup"><span data-stu-id="566d6-1759">query</span></span> |<span data-ttu-id="566d6-1760">使用自訂查詢 tooread hello 的資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-1760">Use hello custom query tooread data.</span></span> |<span data-ttu-id="566d6-1761">SQL-92 查詢或 CQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="566d6-1761">SQL-92 query or CQL query.</span></span> <span data-ttu-id="566d6-1762">請參閱 [CQL 參考資料](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html)。</span><span class="sxs-lookup"><span data-stu-id="566d6-1762">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="566d6-1763">當使用 SQL 查詢，指定**keyspace name.table 名稱**想 tooquery toorepresent hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="566d6-1763">When using SQL query, specify **keyspace name.table name** toorepresent hello table you want tooquery.</span></span> |<span data-ttu-id="566d6-1764">否 (如果已定義資料集上的 tableName 和 keyspace)。</span><span class="sxs-lookup"><span data-stu-id="566d6-1764">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="566d6-1765">consistencyLevel</span><span class="sxs-lookup"><span data-stu-id="566d6-1765">consistencyLevel</span></span> |<span data-ttu-id="566d6-1766">hello 一致性層級指定幾個複本必須回應 tooa 讀取的要求傳回資料 toohello 用戶端應用程式之前。</span><span class="sxs-lookup"><span data-stu-id="566d6-1766">hello consistency level specifies how many replicas must respond tooa read request before returning data toohello client application.</span></span> <span data-ttu-id="566d6-1767">Cassandra 檢查 hello 複本的指定的數目的資料 toosatisfy hello 讀取的要求。</span><span class="sxs-lookup"><span data-stu-id="566d6-1767">Cassandra checks hello specified number of replicas for data toosatisfy hello read request.</span></span> |<span data-ttu-id="566d6-1768">ONE、TWO、THREE、QUORUM、ALL、LOCAL_QUORUM、EACH_QUORUM、LOCAL_ONE。</span><span class="sxs-lookup"><span data-stu-id="566d6-1768">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="566d6-1769">如需詳細資訊，請參閱 [設定資料一致性](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) 。</span><span class="sxs-lookup"><span data-stu-id="566d6-1769">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="566d6-1770">否。</span><span class="sxs-lookup"><span data-stu-id="566d6-1770">No.</span></span> <span data-ttu-id="566d6-1771">預設值為 ONE。</span><span class="sxs-lookup"><span data-stu-id="566d6-1771">Default value is ONE.</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-1772">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1772">Example</span></span>
  
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra tooan Azure blob",
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

<span data-ttu-id="566d6-1773">如需詳細資訊，請參閱 [Cassandra 連接器](data-factory-onprem-cassandra-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1773">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#copy-activity-properties) article.</span></span>

## <a name="mongodb"></a><span data-ttu-id="566d6-1774">MongoDB</span><span class="sxs-lookup"><span data-stu-id="566d6-1774">MongoDB</span></span>

### <a name="linked-service"></a><span data-ttu-id="566d6-1775">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-1775">Linked service</span></span>
<span data-ttu-id="566d6-1776">toodefine MongoDB 連結服務，設定 hello**類型**hello 的連結服務太**OnPremisesMongoDB**，並指定下列屬性在 hello **typeProperties**區段：</span><span class="sxs-lookup"><span data-stu-id="566d6-1776">toodefine a MongoDB linked service, set hello **type** of hello linked service too**OnPremisesMongoDB**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="566d6-1777">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1777">Property</span></span> | <span data-ttu-id="566d6-1778">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1778">Description</span></span> | <span data-ttu-id="566d6-1779">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1779">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-1780">伺服器</span><span class="sxs-lookup"><span data-stu-id="566d6-1780">server</span></span> |<span data-ttu-id="566d6-1781">IP 位址或主機名稱的 hello MongoDB 伺服器。</span><span class="sxs-lookup"><span data-stu-id="566d6-1781">IP address or host name of hello MongoDB server.</span></span> |<span data-ttu-id="566d6-1782">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1782">Yes</span></span> |
| <span data-ttu-id="566d6-1783">連接埠</span><span class="sxs-lookup"><span data-stu-id="566d6-1783">port</span></span> |<span data-ttu-id="566d6-1784">Hello MongoDB 伺服器的 TCP 連接埠會使用用戶端連線 toolisten。</span><span class="sxs-lookup"><span data-stu-id="566d6-1784">TCP port that hello MongoDB server uses toolisten for client connections.</span></span> |<span data-ttu-id="566d6-1785">選用，預設值︰27017</span><span class="sxs-lookup"><span data-stu-id="566d6-1785">Optional, default value: 27017</span></span> |
| <span data-ttu-id="566d6-1786">authenticationType</span><span class="sxs-lookup"><span data-stu-id="566d6-1786">authenticationType</span></span> |<span data-ttu-id="566d6-1787">基本或匿名。</span><span class="sxs-lookup"><span data-stu-id="566d6-1787">Basic, or Anonymous.</span></span> |<span data-ttu-id="566d6-1788">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1788">Yes</span></span> |
| <span data-ttu-id="566d6-1789">username</span><span class="sxs-lookup"><span data-stu-id="566d6-1789">username</span></span> |<span data-ttu-id="566d6-1790">使用者帳戶 tooaccess MongoDB。</span><span class="sxs-lookup"><span data-stu-id="566d6-1790">User account tooaccess MongoDB.</span></span> |<span data-ttu-id="566d6-1791">是 (如果使用基本驗證)。</span><span class="sxs-lookup"><span data-stu-id="566d6-1791">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="566d6-1792">password</span><span class="sxs-lookup"><span data-stu-id="566d6-1792">password</span></span> |<span data-ttu-id="566d6-1793">Hello 使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="566d6-1793">Password for hello user.</span></span> |<span data-ttu-id="566d6-1794">是 (如果使用基本驗證)。</span><span class="sxs-lookup"><span data-stu-id="566d6-1794">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="566d6-1795">authSource</span><span class="sxs-lookup"><span data-stu-id="566d6-1795">authSource</span></span> |<span data-ttu-id="566d6-1796">您想 toouse toocheck 您的認證進行驗證的 hello MongoDB 資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1796">Name of hello MongoDB database that you want toouse toocheck your credentials for authentication.</span></span> |<span data-ttu-id="566d6-1797">選用 (如果使用基本驗證)。</span><span class="sxs-lookup"><span data-stu-id="566d6-1797">Optional (if basic authentication is used).</span></span> <span data-ttu-id="566d6-1798">預設值： 使用 hello 系統管理員帳戶和 hello 使用 databaseName 屬性所指定的資料庫。</span><span class="sxs-lookup"><span data-stu-id="566d6-1798">default: uses hello admin account and hello database specified using databaseName property.</span></span> |
| <span data-ttu-id="566d6-1799">databaseName</span><span class="sxs-lookup"><span data-stu-id="566d6-1799">databaseName</span></span> |<span data-ttu-id="566d6-1800">您想 tooaccess hello MongoDB 資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1800">Name of hello MongoDB database that you want tooaccess.</span></span> |<span data-ttu-id="566d6-1801">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1801">Yes</span></span> |
| <span data-ttu-id="566d6-1802">gatewayName</span><span class="sxs-lookup"><span data-stu-id="566d6-1802">gatewayName</span></span> |<span data-ttu-id="566d6-1803">Hello 閘道存取 hello 資料存放區的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1803">Name of hello gateway that accesses hello data store.</span></span> |<span data-ttu-id="566d6-1804">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1804">Yes</span></span> |
| <span data-ttu-id="566d6-1805">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="566d6-1805">encryptedCredential</span></span> |<span data-ttu-id="566d6-1806">由閘道加密的認證。</span><span class="sxs-lookup"><span data-stu-id="566d6-1806">Credential encrypted by gateway.</span></span> |<span data-ttu-id="566d6-1807">選用</span><span class="sxs-lookup"><span data-stu-id="566d6-1807">Optional</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-1808">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1808">Example</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties": {
        "type": "OnPremisesMongoDb",
        "typeProperties": {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
            "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="566d6-1809">如需詳細資訊，請參閱 [MongoDB 連接器文件](data-factory-on-premises-mongodb-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="566d6-1809">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#linked-service-properties)</span></span>

### <a name="dataset"></a><span data-ttu-id="566d6-1810">Dataset</span><span class="sxs-lookup"><span data-stu-id="566d6-1810">Dataset</span></span>
<span data-ttu-id="566d6-1811">toodefine MongoDB 資料集設定 hello**類型**hello 資料集太**MongoDbCollection**，並指定下列屬性在 hello hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-1811">toodefine a MongoDB dataset, set hello **type** of hello dataset too**MongoDbCollection**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="566d6-1812">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1812">Property</span></span> | <span data-ttu-id="566d6-1813">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1813">Description</span></span> | <span data-ttu-id="566d6-1814">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1814">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-1815">collectionName</span><span class="sxs-lookup"><span data-stu-id="566d6-1815">collectionName</span></span> |<span data-ttu-id="566d6-1816">MongoDB 資料庫中的 hello 集合的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1816">Name of hello collection in MongoDB database.</span></span> |<span data-ttu-id="566d6-1817">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1817">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-1818">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1818">Example</span></span>

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

<span data-ttu-id="566d6-1819">如需詳細資訊，請參閱 [MongoDB 連接器文件](data-factory-on-premises-mongodb-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="566d6-1819">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#dataset-properties)</span></span>

#### <a name="mongodb-source-in-copy-activity"></a><span data-ttu-id="566d6-1820">複製活動中的 MongoDB 來源</span><span class="sxs-lookup"><span data-stu-id="566d6-1820">MongoDB Source in Copy Activity</span></span>
<span data-ttu-id="566d6-1821">如果您從 MongoDB 複製資料，設定 hello**來源類型**的 hello 複製活動太**MongoDbSource**，並指定下列屬性在 hello**來源**> 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-1821">If you are copying data from MongoDB, set hello **source type** of hello copy activity too**MongoDbSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="566d6-1822">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1822">Property</span></span> | <span data-ttu-id="566d6-1823">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1823">Description</span></span> | <span data-ttu-id="566d6-1824">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-1824">Allowed values</span></span> | <span data-ttu-id="566d6-1825">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1825">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-1826">query</span><span class="sxs-lookup"><span data-stu-id="566d6-1826">query</span></span> |<span data-ttu-id="566d6-1827">使用自訂查詢 tooread hello 的資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-1827">Use hello custom query tooread data.</span></span> |<span data-ttu-id="566d6-1828">SQL-92 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="566d6-1828">SQL-92 query string.</span></span> <span data-ttu-id="566d6-1829">例如： `select * from MyTable`。</span><span class="sxs-lookup"><span data-stu-id="566d6-1829">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="566d6-1830">否 (如果已指定 **dataset** 的 **collectionName**)</span><span class="sxs-lookup"><span data-stu-id="566d6-1830">No (if **collectionName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-1831">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1831">Example</span></span>

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

<span data-ttu-id="566d6-1832">如需詳細資訊，請參閱 [MongoDB 連接器文件](data-factory-on-premises-mongodb-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="566d6-1832">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#copy-activity-properties)</span></span>

## <a name="amazon-s3"></a><span data-ttu-id="566d6-1833">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="566d6-1833">Amazon S3</span></span>


### <a name="linked-service"></a><span data-ttu-id="566d6-1834">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-1834">Linked service</span></span>
<span data-ttu-id="566d6-1835">toodefine Amazon S3 連結服務，設定 hello**類型**hello 的連結服務太**AwsAccessKey**，並指定下列屬性在 hello **typeProperties**區段:</span><span class="sxs-lookup"><span data-stu-id="566d6-1835">toodefine an Amazon S3 linked service, set hello **type** of hello linked service too**AwsAccessKey**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="566d6-1836">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1836">Property</span></span> | <span data-ttu-id="566d6-1837">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1837">Description</span></span> | <span data-ttu-id="566d6-1838">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-1838">Allowed values</span></span> | <span data-ttu-id="566d6-1839">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1839">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-1840">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="566d6-1840">accessKeyID</span></span> |<span data-ttu-id="566d6-1841">Hello 密碼的存取金鑰的識別碼。</span><span class="sxs-lookup"><span data-stu-id="566d6-1841">ID of hello secret access key.</span></span> |<span data-ttu-id="566d6-1842">字串</span><span class="sxs-lookup"><span data-stu-id="566d6-1842">string</span></span> |<span data-ttu-id="566d6-1843">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1843">Yes</span></span> |
| <span data-ttu-id="566d6-1844">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="566d6-1844">secretAccessKey</span></span> |<span data-ttu-id="566d6-1845">hello 密碼存取金鑰本身。</span><span class="sxs-lookup"><span data-stu-id="566d6-1845">hello secret access key itself.</span></span> |<span data-ttu-id="566d6-1846">加密的密碼字串</span><span class="sxs-lookup"><span data-stu-id="566d6-1846">Encrypted secret string</span></span> |<span data-ttu-id="566d6-1847">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1847">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-1848">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1848">Example</span></span>
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

<span data-ttu-id="566d6-1849">如需詳細資訊，請參閱 [Amazon S3 連接器文件](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties)。</span><span class="sxs-lookup"><span data-stu-id="566d6-1849">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="566d6-1850">Dataset</span><span class="sxs-lookup"><span data-stu-id="566d6-1850">Dataset</span></span>
<span data-ttu-id="566d6-1851">toodefine Amazon S3 資料集，設定 hello**類型**hello 資料集太**AmazonS3**，並指定下列屬性在 hello hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-1851">toodefine an Amazon S3 dataset, set hello **type** of hello dataset too**AmazonS3**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="566d6-1852">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1852">Property</span></span> | <span data-ttu-id="566d6-1853">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1853">Description</span></span> | <span data-ttu-id="566d6-1854">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-1854">Allowed values</span></span> | <span data-ttu-id="566d6-1855">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1855">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-1856">bucketName</span><span class="sxs-lookup"><span data-stu-id="566d6-1856">bucketName</span></span> |<span data-ttu-id="566d6-1857">hello S3 值區的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1857">hello S3 bucket name.</span></span> |<span data-ttu-id="566d6-1858">String</span><span class="sxs-lookup"><span data-stu-id="566d6-1858">String</span></span> |<span data-ttu-id="566d6-1859">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1859">Yes</span></span> |
| <span data-ttu-id="566d6-1860">key</span><span class="sxs-lookup"><span data-stu-id="566d6-1860">key</span></span> |<span data-ttu-id="566d6-1861">hello S3 物件索引鍵。</span><span class="sxs-lookup"><span data-stu-id="566d6-1861">hello S3 object key.</span></span> |<span data-ttu-id="566d6-1862">String</span><span class="sxs-lookup"><span data-stu-id="566d6-1862">String</span></span> |<span data-ttu-id="566d6-1863">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1863">No</span></span> |
| <span data-ttu-id="566d6-1864">prefix</span><span class="sxs-lookup"><span data-stu-id="566d6-1864">prefix</span></span> |<span data-ttu-id="566d6-1865">Hello S3 物件索引鍵的前置詞。</span><span class="sxs-lookup"><span data-stu-id="566d6-1865">Prefix for hello S3 object key.</span></span> <span data-ttu-id="566d6-1866">系統會選取索引鍵以此前置詞開頭的物件。</span><span class="sxs-lookup"><span data-stu-id="566d6-1866">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="566d6-1867">只有當索引鍵空白時才適用。</span><span class="sxs-lookup"><span data-stu-id="566d6-1867">Applies only when key is empty.</span></span> |<span data-ttu-id="566d6-1868">string</span><span class="sxs-lookup"><span data-stu-id="566d6-1868">String</span></span> |<span data-ttu-id="566d6-1869">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1869">No</span></span> |
| <span data-ttu-id="566d6-1870">版本</span><span class="sxs-lookup"><span data-stu-id="566d6-1870">version</span></span> |<span data-ttu-id="566d6-1871">如果已啟用 S3 版本控制的 S3 物件 hello 版本。</span><span class="sxs-lookup"><span data-stu-id="566d6-1871">hello version of S3 object if S3 versioning is enabled.</span></span> |<span data-ttu-id="566d6-1872">String</span><span class="sxs-lookup"><span data-stu-id="566d6-1872">String</span></span> |<span data-ttu-id="566d6-1873">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1873">No</span></span> |
| <span data-ttu-id="566d6-1874">format</span><span class="sxs-lookup"><span data-stu-id="566d6-1874">format</span></span> | <span data-ttu-id="566d6-1875">支援下列格式類型的 hello: **TextFormat**， **JsonFormat**， **AvroFormat**， **OrcFormat**， **ParquetFormat**。</span><span class="sxs-lookup"><span data-stu-id="566d6-1875">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="566d6-1876">設定 hello**類型**下格式 tooone 這些值的屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-1876">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="566d6-1877">如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。</span><span class="sxs-lookup"><span data-stu-id="566d6-1877">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="566d6-1878">如果您想太**複製檔做為-是**之間以檔案為基礎存放區 （二進位複製），略過這兩個輸入和輸出資料集定義中的 hello 格式 > 一節。</span><span class="sxs-lookup"><span data-stu-id="566d6-1878">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="566d6-1879">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1879">No</span></span> | |
| <span data-ttu-id="566d6-1880">compression</span><span class="sxs-lookup"><span data-stu-id="566d6-1880">compression</span></span> | <span data-ttu-id="566d6-1881">指定 hello 類型和層級的 hello 資料壓縮。</span><span class="sxs-lookup"><span data-stu-id="566d6-1881">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="566d6-1882">支援的類型為：**GZip**、**Deflate**、**BZip2** 及 **ZipDeflate**。</span><span class="sxs-lookup"><span data-stu-id="566d6-1882">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="566d6-1883">hello 支援層級為：**最佳**和**最快**。</span><span class="sxs-lookup"><span data-stu-id="566d6-1883">hello supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="566d6-1884">如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。</span><span class="sxs-lookup"><span data-stu-id="566d6-1884">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="566d6-1885">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1885">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="566d6-1886">bucketName + 鍵指定 hello hello S3 物件其中貯體是 S3 物件 hello 根容器，而索引鍵是 hello 完整路徑 tooS3 物件位置。</span><span class="sxs-lookup"><span data-stu-id="566d6-1886">bucketName + key specifies hello location of hello S3 object where bucket is hello root container for S3 objects and key is hello full path tooS3 object.</span></span>

#### <a name="example-sample-dataset-with-prefix"></a><span data-ttu-id="566d6-1887">範例：範例資料集 (含 prefix)</span><span class="sxs-lookup"><span data-stu-id="566d6-1887">Example: Sample dataset with prefix</span></span>

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
#### <a name="example-sample-data-set-with-version"></a><span data-ttu-id="566d6-1888">範例︰範例資料集 (含 version)</span><span class="sxs-lookup"><span data-stu-id="566d6-1888">Example: Sample data set (with version)</span></span>

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

#### <a name="example-dynamic-paths-for-s3"></a><span data-ttu-id="566d6-1889">範例：S3 的動態路徑</span><span class="sxs-lookup"><span data-stu-id="566d6-1889">Example: Dynamic paths for S3</span></span>
<span data-ttu-id="566d6-1890">在 hello 範例中，我們會使用固定的值為 hello Amazon S3 資料集中的索引鍵和 bucketName 屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-1890">In hello sample, we use fixed values for key and bucketName properties in hello Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "<S3 bucket name>",
```

<span data-ttu-id="566d6-1891">您可以使用系統變數 SliceStart 如 hello 索引鍵和 bucketName 在執行階段動態計算的 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="566d6-1891">You can have Data Factory calculate hello key and bucketName dynamically at runtime by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="566d6-1892">您可以相同 hello hello 前置詞屬性的 Amazon S3 資料集。</span><span class="sxs-lookup"><span data-stu-id="566d6-1892">You can do hello same for hello prefix property of an Amazon S3 dataset.</span></span> <span data-ttu-id="566d6-1893">如需支援的函式和變數清單，請參閱 [Data Factory 函式與系統變數](data-factory-functions-variables.md) 。</span><span class="sxs-lookup"><span data-stu-id="566d6-1893">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of supported functions and variables.</span></span>

<span data-ttu-id="566d6-1894">如需詳細資訊，請參閱 [Amazon S3 連接器文件](data-factory-amazon-simple-storage-service-connector.md#dataset-properties)。</span><span class="sxs-lookup"><span data-stu-id="566d6-1894">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="566d6-1895">複製活動中的檔案系統來源</span><span class="sxs-lookup"><span data-stu-id="566d6-1895">File System Source in Copy Activity</span></span>
<span data-ttu-id="566d6-1896">如果您從 Amazon S3 複製資料，設定 hello**來源類型**的 hello 複製活動太**FileSystemSource**，並指定下列屬性在 hello**來源**區段:</span><span class="sxs-lookup"><span data-stu-id="566d6-1896">If you are copying data from Amazon S3, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="566d6-1897">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1897">Property</span></span> | <span data-ttu-id="566d6-1898">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1898">Description</span></span> | <span data-ttu-id="566d6-1899">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-1899">Allowed values</span></span> | <span data-ttu-id="566d6-1900">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1900">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-1901">遞迴</span><span class="sxs-lookup"><span data-stu-id="566d6-1901">recursive</span></span> |<span data-ttu-id="566d6-1902">指定是否 toorecursively 清單 S3 物件 hello 目錄下。</span><span class="sxs-lookup"><span data-stu-id="566d6-1902">Specifies whether toorecursively list S3 objects under hello directory.</span></span> |<span data-ttu-id="566d6-1903">true/false</span><span class="sxs-lookup"><span data-stu-id="566d6-1903">true/false</span></span> |<span data-ttu-id="566d6-1904">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1904">No</span></span> |


#### <a name="example"></a><span data-ttu-id="566d6-1905">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1905">Example</span></span>


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

<span data-ttu-id="566d6-1906">如需詳細資訊，請參閱 [Amazon S3 連接器文件](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties)。</span><span class="sxs-lookup"><span data-stu-id="566d6-1906">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span></span>

## <a name="file-system"></a><span data-ttu-id="566d6-1907">檔案系統</span><span class="sxs-lookup"><span data-stu-id="566d6-1907">File System</span></span>


### <a name="linked-service"></a><span data-ttu-id="566d6-1908">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-1908">Linked service</span></span>
<span data-ttu-id="566d6-1909">您可以連結在內部部署檔案系統 tooan Azure data factory 以 hello**在內部部署檔案伺服器**連結服務。</span><span class="sxs-lookup"><span data-stu-id="566d6-1909">You can link an on-premises file system tooan Azure data factory with hello **On-Premises File Server** linked service.</span></span> <span data-ttu-id="566d6-1910">hello 下表提供說明屬於特定 toohello 連結在內部部署檔案伺服器服務的 JSON 元素。</span><span class="sxs-lookup"><span data-stu-id="566d6-1910">hello following table provides descriptions for JSON elements that are specific toohello On-Premises File Server linked service.</span></span>

| <span data-ttu-id="566d6-1911">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1911">Property</span></span> | <span data-ttu-id="566d6-1912">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1912">Description</span></span> | <span data-ttu-id="566d6-1913">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1913">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-1914">類型</span><span class="sxs-lookup"><span data-stu-id="566d6-1914">type</span></span> |<span data-ttu-id="566d6-1915">請確定 hello type 屬性設定太**OnPremisesFileServer**。</span><span class="sxs-lookup"><span data-stu-id="566d6-1915">Ensure that hello type property is set too**OnPremisesFileServer**.</span></span> |<span data-ttu-id="566d6-1916">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1916">Yes</span></span> |
| <span data-ttu-id="566d6-1917">主機</span><span class="sxs-lookup"><span data-stu-id="566d6-1917">host</span></span> |<span data-ttu-id="566d6-1918">指定您想 toocopy hello 資料夾 hello 根路徑。</span><span class="sxs-lookup"><span data-stu-id="566d6-1918">Specifies hello root path of hello folder that you want toocopy.</span></span> <span data-ttu-id="566d6-1919">使用 hello 逸出字元 '\' hello 字串中的特殊字元。</span><span class="sxs-lookup"><span data-stu-id="566d6-1919">Use hello escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="566d6-1920">如需範例，請參閱 [範例連結服務和資料集定義](#sample-linked-service-and-dataset-definitions) 。</span><span class="sxs-lookup"><span data-stu-id="566d6-1920">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="566d6-1921">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1921">Yes</span></span> |
| <span data-ttu-id="566d6-1922">userid</span><span class="sxs-lookup"><span data-stu-id="566d6-1922">userid</span></span> |<span data-ttu-id="566d6-1923">指定具有存取 toohello 伺服器 hello 使用者識別碼 hello。</span><span class="sxs-lookup"><span data-stu-id="566d6-1923">Specify hello ID of hello user who has access toohello server.</span></span> |<span data-ttu-id="566d6-1924">否 (如果您選擇 encryptedCredential)</span><span class="sxs-lookup"><span data-stu-id="566d6-1924">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="566d6-1925">password</span><span class="sxs-lookup"><span data-stu-id="566d6-1925">password</span></span> |<span data-ttu-id="566d6-1926">指定 hello hello 使用者 (userid) 的密碼。</span><span class="sxs-lookup"><span data-stu-id="566d6-1926">Specify hello password for hello user (userid).</span></span> |<span data-ttu-id="566d6-1927">否 (如果您選擇 encryptedCredential)</span><span class="sxs-lookup"><span data-stu-id="566d6-1927">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="566d6-1928">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="566d6-1928">encryptedCredential</span></span> |<span data-ttu-id="566d6-1929">指定您可以藉由執行 hello 新增 AzureRmDataFactoryEncryptValue cmdlet 取得的 hello 加密認證。</span><span class="sxs-lookup"><span data-stu-id="566d6-1929">Specify hello encrypted credentials that you can get by running hello New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="566d6-1930">否 （如果您選擇 toospecify 使用者識別碼和密碼以純文字）</span><span class="sxs-lookup"><span data-stu-id="566d6-1930">No (if you choose toospecify userid and password in plain text)</span></span> |
| <span data-ttu-id="566d6-1931">gatewayName</span><span class="sxs-lookup"><span data-stu-id="566d6-1931">gatewayName</span></span> |<span data-ttu-id="566d6-1932">指定 hello hello 閘道的 Data Factory 應該使用 tooconnect toohello 在內部部署檔案伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-1932">Specifies hello name of hello gateway that Data Factory should use tooconnect toohello on-premises file server.</span></span> |<span data-ttu-id="566d6-1933">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1933">Yes</span></span> |

#### <a name="sample-folder-path-definitions"></a><span data-ttu-id="566d6-1934">範例資料夾路徑定義</span><span class="sxs-lookup"><span data-stu-id="566d6-1934">Sample folder path definitions</span></span> 
| <span data-ttu-id="566d6-1935">案例</span><span class="sxs-lookup"><span data-stu-id="566d6-1935">Scenario</span></span> | <span data-ttu-id="566d6-1936">連結服務定義中的主機</span><span class="sxs-lookup"><span data-stu-id="566d6-1936">Host in linked service definition</span></span> | <span data-ttu-id="566d6-1937">資料集定義中的 folderPath</span><span class="sxs-lookup"><span data-stu-id="566d6-1937">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-1938">資料管理閘道電腦上的本機資料夾︰</span><span class="sxs-lookup"><span data-stu-id="566d6-1938">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="566d6-1939">範例：D:\\\* 或 D:\folder\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="566d6-1939">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="566d6-1940">D:\\\\ (適用於資料管理閘道 2.0 和更新版本)</span><span class="sxs-lookup"><span data-stu-id="566d6-1940">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="566d6-1941">localhost (適用於比資料管理閘道 2.0 更早的版本)</span><span class="sxs-lookup"><span data-stu-id="566d6-1941">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="566d6-1942">.\\\\ 或 folder\\\\subfolder (適用於資料管理閘道 2.0 和更新版本)</span><span class="sxs-lookup"><span data-stu-id="566d6-1942">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="566d6-1943">D:\\\\ 或 D:\\\\folder\\\\subfolder (適用低於閘道 2.0 的版本)</span><span class="sxs-lookup"><span data-stu-id="566d6-1943">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="566d6-1944">遠端共用資料夾︰</span><span class="sxs-lookup"><span data-stu-id="566d6-1944">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="566d6-1945">範例︰\\\\myserver\\share\\\* 或 \\\\myserver\\share\\folder\\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="566d6-1945">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="566d6-1946">\\\\\\\\myserver\\\\share</span><span class="sxs-lookup"><span data-stu-id="566d6-1946">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="566d6-1947">.\\\\ 或 folder\\\\subfolder</span><span class="sxs-lookup"><span data-stu-id="566d6-1947">.\\\\ or folder\\\\subfolder</span></span> |


#### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="566d6-1948">範例：使用純文字的使用者名稱和密碼</span><span class="sxs-lookup"><span data-stu-id="566d6-1948">Example: Using username and password in plain text</span></span>

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

#### <a name="example-using-encryptedcredential"></a><span data-ttu-id="566d6-1949">範例：使用 encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="566d6-1949">Example: Using encryptedcredential</span></span>

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

<span data-ttu-id="566d6-1950">如需詳細資訊，請參閱[檔案系統連接器文件](data-factory-onprem-file-system-connector.md#linked-service-properties)。</span><span class="sxs-lookup"><span data-stu-id="566d6-1950">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="566d6-1951">Dataset</span><span class="sxs-lookup"><span data-stu-id="566d6-1951">Dataset</span></span>
<span data-ttu-id="566d6-1952">toodefine 檔案系統資料集設定 hello**類型**hello 資料集太**FileShare**，並指定下列屬性在 hello hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-1952">toodefine a File System dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="566d6-1953">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1953">Property</span></span> | <span data-ttu-id="566d6-1954">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1954">Description</span></span> | <span data-ttu-id="566d6-1955">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1955">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-1956">folderPath</span><span class="sxs-lookup"><span data-stu-id="566d6-1956">folderPath</span></span> |<span data-ttu-id="566d6-1957">指定 hello 子路徑 toohello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="566d6-1957">Specifies hello subpath toohello folder.</span></span> <span data-ttu-id="566d6-1958">使用 hello 逸出字元 ' \' hello 字串中的特殊字元。</span><span class="sxs-lookup"><span data-stu-id="566d6-1958">Use hello escape character ‘\’ for special characters in hello string.</span></span> <span data-ttu-id="566d6-1959">如需範例，請參閱 [範例連結服務和資料集定義](#sample-linked-service-and-dataset-definitions) 。</span><span class="sxs-lookup"><span data-stu-id="566d6-1959">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="566d6-1960">您可以結合此屬性與**partitionBy** toohave 資料夾路徑根據配量開始/結束日期時間。</span><span class="sxs-lookup"><span data-stu-id="566d6-1960">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="566d6-1961">是</span><span class="sxs-lookup"><span data-stu-id="566d6-1961">Yes</span></span> |
| <span data-ttu-id="566d6-1962">fileName</span><span class="sxs-lookup"><span data-stu-id="566d6-1962">fileName</span></span> |<span data-ttu-id="566d6-1963">在 hello 指定 hello hello 檔案名稱**folderPath**如果您想 hello 資料表 toorefer tooa 特定檔案 hello 資料夾中的。</span><span class="sxs-lookup"><span data-stu-id="566d6-1963">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="566d6-1964">如果您未指定任何值，這個屬性，hello 資料表會指向 tooall hello 資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="566d6-1964">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="566d6-1965">檔案名稱未指定輸出資料集，hello hello 產生檔案名稱時在 hello 下列格式：</span><span class="sxs-lookup"><span data-stu-id="566d6-1965">When fileName is not specified for an output dataset, hello name of hello generated file is in hello following format:</span></span> <br/><br/><span data-ttu-id="566d6-1966">`Data.<Guid>.txt` (例如： Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="566d6-1966">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="566d6-1967">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1967">No</span></span> |
| <span data-ttu-id="566d6-1968">fileFilter</span><span class="sxs-lookup"><span data-stu-id="566d6-1968">fileFilter</span></span> |<span data-ttu-id="566d6-1969">指定篩選 toobe 使用 tooselect hello folderPath 中檔案的子集，而不是所有的檔案。</span><span class="sxs-lookup"><span data-stu-id="566d6-1969">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="566d6-1970">允許的值為︰`*` (多個字元) 和 `?` (單一字元)。</span><span class="sxs-lookup"><span data-stu-id="566d6-1970">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="566d6-1971">範例 1："fileFilter": "*.log"</span><span class="sxs-lookup"><span data-stu-id="566d6-1971">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="566d6-1972">範例 2："fileFilter": 2016-1-?.txt"</span><span class="sxs-lookup"><span data-stu-id="566d6-1972">Example 2: "fileFilter": 2016-1-?.txt"</span></span><br/><br/><span data-ttu-id="566d6-1973">請注意，fileFilter 適用於輸入 FileShare 資料集。</span><span class="sxs-lookup"><span data-stu-id="566d6-1973">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="566d6-1974">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1974">No</span></span> |
| <span data-ttu-id="566d6-1975">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="566d6-1975">partitionedBy</span></span> |<span data-ttu-id="566d6-1976">您可以使用 partitionedBy toospecify 動態 folderPath/檔名，時間序列資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-1976">You can use partitionedBy toospecify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="566d6-1977">例如，folderPath 可針對每小時的資料進行參數化。</span><span class="sxs-lookup"><span data-stu-id="566d6-1977">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="566d6-1978">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1978">No</span></span> |
| <span data-ttu-id="566d6-1979">format</span><span class="sxs-lookup"><span data-stu-id="566d6-1979">format</span></span> | <span data-ttu-id="566d6-1980">支援下列格式類型的 hello: **TextFormat**， **JsonFormat**， **AvroFormat**， **OrcFormat**， **ParquetFormat**。</span><span class="sxs-lookup"><span data-stu-id="566d6-1980">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="566d6-1981">設定 hello**類型**下格式 tooone 這些值的屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-1981">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="566d6-1982">如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。</span><span class="sxs-lookup"><span data-stu-id="566d6-1982">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="566d6-1983">如果您想太**複製檔做為-是**之間以檔案為基礎存放區 （二進位複製），略過這兩個輸入和輸出資料集定義中的 hello 格式 > 一節。</span><span class="sxs-lookup"><span data-stu-id="566d6-1983">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="566d6-1984">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1984">No</span></span> |
| <span data-ttu-id="566d6-1985">compression</span><span class="sxs-lookup"><span data-stu-id="566d6-1985">compression</span></span> | <span data-ttu-id="566d6-1986">指定 hello 類型和層級的 hello 資料壓縮。</span><span class="sxs-lookup"><span data-stu-id="566d6-1986">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="566d6-1987">支援的類型為：**GZip**、**Deflate**、**BZip2** 和 **ZipDeflate**，而支援的層級為：**最佳**和**最快**。</span><span class="sxs-lookup"><span data-stu-id="566d6-1987">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="566d6-1988">請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。</span><span class="sxs-lookup"><span data-stu-id="566d6-1988">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="566d6-1989">否</span><span class="sxs-lookup"><span data-stu-id="566d6-1989">No</span></span> |

> [!NOTE]
> <span data-ttu-id="566d6-1990">無法同時使用 fileName 和 fileFilter。</span><span class="sxs-lookup"><span data-stu-id="566d6-1990">You cannot use fileName and fileFilter simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="566d6-1991">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-1991">Example</span></span>

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

<span data-ttu-id="566d6-1992">如需詳細資訊，請參閱[檔案系統連接器文件](data-factory-onprem-file-system-connector.md#dataset-properties)。</span><span class="sxs-lookup"><span data-stu-id="566d6-1992">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="566d6-1993">複製活動中的檔案系統來源</span><span class="sxs-lookup"><span data-stu-id="566d6-1993">File System Source in Copy Activity</span></span>
<span data-ttu-id="566d6-1994">如果您從檔案系統複製資料，設定 hello**來源類型**的 hello 複製活動太**FileSystemSource**，並指定下列屬性在 hello**來源**區段：</span><span class="sxs-lookup"><span data-stu-id="566d6-1994">If you are copying data from File System, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="566d6-1995">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-1995">Property</span></span> | <span data-ttu-id="566d6-1996">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-1996">Description</span></span> | <span data-ttu-id="566d6-1997">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-1997">Allowed values</span></span> | <span data-ttu-id="566d6-1998">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-1998">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-1999">遞迴</span><span class="sxs-lookup"><span data-stu-id="566d6-1999">recursive</span></span> |<span data-ttu-id="566d6-2000">指出是否 hello 讀取資料以遞迴方式從 hello 子資料夾，或只能從 hello 指定的資料夾。</span><span class="sxs-lookup"><span data-stu-id="566d6-2000">Indicates whether hello data is read recursively from hello subfolders or only from hello specified folder.</span></span> |<span data-ttu-id="566d6-2001">True/False (預設值為 False)</span><span class="sxs-lookup"><span data-stu-id="566d6-2001">True, False (default)</span></span> |<span data-ttu-id="566d6-2002">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2002">No</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-2003">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-2003">Example</span></span>

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
<span data-ttu-id="566d6-2004">如需詳細資訊，請參閱[檔案系統連接器文件](data-factory-onprem-file-system-connector.md#copy-activity-properties)。</span><span class="sxs-lookup"><span data-stu-id="566d6-2004">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

### <a name="file-system-sink-in-copy-activity"></a><span data-ttu-id="566d6-2005">複製活動中的檔案系統接收</span><span class="sxs-lookup"><span data-stu-id="566d6-2005">File System Sink in Copy Activity</span></span>
<span data-ttu-id="566d6-2006">如果您要複製資料 tooFile 系統，請設定 hello**接收器類型**的 hello 複製活動太**使用 FileSystemSink**，並指定下列屬性在 hello**接收**> 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-2006">If you are copying data tooFile System, set hello **sink type** of hello copy activity too**FileSystemSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="566d6-2007">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2007">Property</span></span> | <span data-ttu-id="566d6-2008">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2008">Description</span></span> | <span data-ttu-id="566d6-2009">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-2009">Allowed values</span></span> | <span data-ttu-id="566d6-2010">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2010">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-2011">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="566d6-2011">copyBehavior</span></span> |<span data-ttu-id="566d6-2012">Hello 來源 BlobSource 或檔案系統時，請定義 hello 複製行為。</span><span class="sxs-lookup"><span data-stu-id="566d6-2012">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="566d6-2013">**PreserveHierarchy:**保留 hello hello 目標資料夾中的檔案階層。</span><span class="sxs-lookup"><span data-stu-id="566d6-2013">**PreserveHierarchy:** Preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="566d6-2014">也就是說，hello hello 來源檔案 toohello 來源資料夾的相對路徑是 hello 與 hello 相對路徑的 hello 目標檔案 toohello 目標資料夾相同。</span><span class="sxs-lookup"><span data-stu-id="566d6-2014">That is, hello relative path of hello source file toohello source folder is hello same as hello relative path of hello target file toohello target folder.</span></span><br/><br/><span data-ttu-id="566d6-2015">**FlattenHierarchy:** hello 第一個層級的目標資料夾中建立 hello 來源資料夾中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="566d6-2015">**FlattenHierarchy:** All files from hello source folder are created in hello first level of target folder.</span></span> <span data-ttu-id="566d6-2016">會使用自動產生名稱建立 hello 目標檔案。</span><span class="sxs-lookup"><span data-stu-id="566d6-2016">hello target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="566d6-2017">**MergeFiles:**合併 hello 來源資料夾 tooone 檔案中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="566d6-2017">**MergeFiles:** Merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="566d6-2018">如果指定 hello 檔案名稱/blob 名稱，則 hello 合併的檔案名稱是 hello 指定的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-2018">If hello file name/blob name is specified, hello merged file name is hello specified name.</span></span> <span data-ttu-id="566d6-2019">否則，就會是自動產生的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-2019">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="566d6-2020">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2020">No</span></span> |
<span data-ttu-id="566d6-2021">auto-</span><span class="sxs-lookup"><span data-stu-id="566d6-2021">auto-</span></span>

#### <a name="example"></a><span data-ttu-id="566d6-2022">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-2022">Example</span></span>

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

<span data-ttu-id="566d6-2023">如需詳細資訊，請參閱[檔案系統連接器文件](data-factory-onprem-file-system-connector.md#copy-activity-properties)。</span><span class="sxs-lookup"><span data-stu-id="566d6-2023">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

## <a name="ftp"></a><span data-ttu-id="566d6-2024">FTP</span><span class="sxs-lookup"><span data-stu-id="566d6-2024">FTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="566d6-2025">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-2025">Linked service</span></span>
<span data-ttu-id="566d6-2026">toodefine FTP 連結服務，設定 hello**類型**hello 的連結服務太**FtpServer**，並指定下列屬性在 hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-2026">toodefine an FTP linked service, set hello **type** of hello linked service too**FtpServer**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="566d6-2027">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2027">Property</span></span> | <span data-ttu-id="566d6-2028">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2028">Description</span></span> | <span data-ttu-id="566d6-2029">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2029">Required</span></span> | <span data-ttu-id="566d6-2030">預設值</span><span class="sxs-lookup"><span data-stu-id="566d6-2030">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-2031">主機</span><span class="sxs-lookup"><span data-stu-id="566d6-2031">host</span></span> |<span data-ttu-id="566d6-2032">Hello FTP 伺服器的名稱或 IP 位址</span><span class="sxs-lookup"><span data-stu-id="566d6-2032">Name or IP address of hello FTP Server</span></span> |<span data-ttu-id="566d6-2033">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2033">Yes</span></span> |&nbsp; |
| <span data-ttu-id="566d6-2034">authenticationType</span><span class="sxs-lookup"><span data-stu-id="566d6-2034">authenticationType</span></span> |<span data-ttu-id="566d6-2035">指定驗證類型</span><span class="sxs-lookup"><span data-stu-id="566d6-2035">Specify authentication type</span></span> |<span data-ttu-id="566d6-2036">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2036">Yes</span></span> |<span data-ttu-id="566d6-2037">基本或匿名</span><span class="sxs-lookup"><span data-stu-id="566d6-2037">Basic, Anonymous</span></span> |
| <span data-ttu-id="566d6-2038">username</span><span class="sxs-lookup"><span data-stu-id="566d6-2038">username</span></span> |<span data-ttu-id="566d6-2039">使用者具有存取 toohello FTP 伺服器</span><span class="sxs-lookup"><span data-stu-id="566d6-2039">User who has access toohello FTP server</span></span> |<span data-ttu-id="566d6-2040">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2040">No</span></span> |&nbsp; |
| <span data-ttu-id="566d6-2041">password</span><span class="sxs-lookup"><span data-stu-id="566d6-2041">password</span></span> |<span data-ttu-id="566d6-2042">Hello 使用者 （使用者名稱） 的密碼</span><span class="sxs-lookup"><span data-stu-id="566d6-2042">Password for hello user (username)</span></span> |<span data-ttu-id="566d6-2043">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2043">No</span></span> |&nbsp; |
| <span data-ttu-id="566d6-2044">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="566d6-2044">encryptedCredential</span></span> |<span data-ttu-id="566d6-2045">加密的認證 tooaccess hello FTP 伺服器</span><span class="sxs-lookup"><span data-stu-id="566d6-2045">Encrypted credential tooaccess hello FTP server</span></span> |<span data-ttu-id="566d6-2046">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2046">No</span></span> |&nbsp; |
| <span data-ttu-id="566d6-2047">gatewayName</span><span class="sxs-lookup"><span data-stu-id="566d6-2047">gatewayName</span></span> |<span data-ttu-id="566d6-2048">Hello 資料管理閘道器閘道 tooconnect tooan 名稱在內部 FTP 伺服器</span><span class="sxs-lookup"><span data-stu-id="566d6-2048">Name of hello Data Management Gateway gateway tooconnect tooan on-premises FTP server</span></span> |<span data-ttu-id="566d6-2049">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2049">No</span></span> |&nbsp; |
| <span data-ttu-id="566d6-2050">連接埠</span><span class="sxs-lookup"><span data-stu-id="566d6-2050">port</span></span> |<span data-ttu-id="566d6-2051">哪些 hello FTP 伺服器正在接聽的連接埠</span><span class="sxs-lookup"><span data-stu-id="566d6-2051">Port on which hello FTP server is listening</span></span> |<span data-ttu-id="566d6-2052">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2052">No</span></span> |<span data-ttu-id="566d6-2053">21</span><span class="sxs-lookup"><span data-stu-id="566d6-2053">21</span></span> |
| <span data-ttu-id="566d6-2054">enableSsl</span><span class="sxs-lookup"><span data-stu-id="566d6-2054">enableSsl</span></span> |<span data-ttu-id="566d6-2055">指定是否 toouse FTP over SSL/TLS 通道</span><span class="sxs-lookup"><span data-stu-id="566d6-2055">Specify whether toouse FTP over SSL/TLS channel</span></span> |<span data-ttu-id="566d6-2056">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2056">No</span></span> |<span data-ttu-id="566d6-2057">true</span><span class="sxs-lookup"><span data-stu-id="566d6-2057">true</span></span> |
| <span data-ttu-id="566d6-2058">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="566d6-2058">enableServerCertificateValidation</span></span> |<span data-ttu-id="566d6-2059">指定是否 tooenable 伺服器 SSL 憑證驗證時使用 FTP over SSL/TLS 通道</span><span class="sxs-lookup"><span data-stu-id="566d6-2059">Specify whether tooenable server SSL certificate validation when using FTP over SSL/TLS channel</span></span> |<span data-ttu-id="566d6-2060">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2060">No</span></span> |<span data-ttu-id="566d6-2061">true</span><span class="sxs-lookup"><span data-stu-id="566d6-2061">true</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="566d6-2062">範例：使用匿名驗證</span><span class="sxs-lookup"><span data-stu-id="566d6-2062">Example: Using Anonymous authentication</span></span>

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

#### <a name="example-using-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="566d6-2063">範例：使用純文字的使用者名稱和密碼進行基本驗證</span><span class="sxs-lookup"><span data-stu-id="566d6-2063">Example: Using username and password in plain text for basic authentication</span></span>

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

#### <a name="example-using-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="566d6-2064">範例：使用 port、enableSsl、enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="566d6-2064">Example: Using port, enableSsl, enableServerCertificateValidation</span></span>

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

#### <a name="example-using-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="566d6-2065">範例：針對驗證和閘道使用 encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="566d6-2065">Example: Using encryptedCredential for authentication and gateway</span></span>

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

<span data-ttu-id="566d6-2066">如需詳細資訊，請參閱 [FTP 連接器](data-factory-ftp-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-2066">For more information, see [FTP connector](data-factory-ftp-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="566d6-2067">Dataset</span><span class="sxs-lookup"><span data-stu-id="566d6-2067">Dataset</span></span>
<span data-ttu-id="566d6-2068">toodefine FTP 資料集，設定 hello**類型**hello 資料集太**FileShare**，並指定下列屬性在 hello hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-2068">toodefine an FTP dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="566d6-2069">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2069">Property</span></span> | <span data-ttu-id="566d6-2070">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2070">Description</span></span> | <span data-ttu-id="566d6-2071">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2071">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-2072">folderPath</span><span class="sxs-lookup"><span data-stu-id="566d6-2072">folderPath</span></span> |<span data-ttu-id="566d6-2073">子路徑 toohello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="566d6-2073">Sub path toohello folder.</span></span> <span data-ttu-id="566d6-2074">使用逸出字元 '\' hello 字串中的特殊字元。</span><span class="sxs-lookup"><span data-stu-id="566d6-2074">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="566d6-2075">如需範例，請參閱 [範例連結服務和資料集定義](#sample-linked-service-and-dataset-definitions) 。</span><span class="sxs-lookup"><span data-stu-id="566d6-2075">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="566d6-2076">您可以結合此屬性與**partitionBy** toohave 資料夾路徑根據配量開始/結束日期時間。</span><span class="sxs-lookup"><span data-stu-id="566d6-2076">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="566d6-2077">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2077">Yes</span></span> 
| <span data-ttu-id="566d6-2078">fileName</span><span class="sxs-lookup"><span data-stu-id="566d6-2078">fileName</span></span> |<span data-ttu-id="566d6-2079">在 hello 指定 hello hello 檔案名稱**folderPath**如果您想 hello 資料表 toorefer tooa 特定檔案 hello 資料夾中的。</span><span class="sxs-lookup"><span data-stu-id="566d6-2079">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="566d6-2080">如果您未指定任何值，這個屬性，hello 資料表會指向 tooall hello 資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="566d6-2080">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="566d6-2081">檔案名稱未指定輸出資料集，hello hello 產生檔案名稱會在 hello 遵循此格式：</span><span class="sxs-lookup"><span data-stu-id="566d6-2081">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="566d6-2082">Data.<Guid>.txt (範例：Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="566d6-2082">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="566d6-2083">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2083">No</span></span> |
| <span data-ttu-id="566d6-2084">fileFilter</span><span class="sxs-lookup"><span data-stu-id="566d6-2084">fileFilter</span></span> |<span data-ttu-id="566d6-2085">指定篩選 toobe 使用 tooselect hello folderPath 中檔案的子集，而不是所有的檔案。</span><span class="sxs-lookup"><span data-stu-id="566d6-2085">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="566d6-2086">允許的值為︰`*` (多個字元) 和 `?` (單一字元)。</span><span class="sxs-lookup"><span data-stu-id="566d6-2086">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="566d6-2087">範例 1：`"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="566d6-2087">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="566d6-2088">範例 2：`"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="566d6-2088">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="566d6-2089">fileFilter 適用於輸入 FileShare 資料集。</span><span class="sxs-lookup"><span data-stu-id="566d6-2089">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="566d6-2090">這個屬性不支援使用 HDFS。</span><span class="sxs-lookup"><span data-stu-id="566d6-2090">This property is not supported with HDFS.</span></span> |<span data-ttu-id="566d6-2091">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2091">No</span></span> |
| <span data-ttu-id="566d6-2092">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="566d6-2092">partitionedBy</span></span> |<span data-ttu-id="566d6-2093">partitionedBy 可以是使用的 toospecify 動態 folderPath，時間序列資料的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-2093">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="566d6-2094">例如，folderPath 可針對每小時的資料進行參數化。</span><span class="sxs-lookup"><span data-stu-id="566d6-2094">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="566d6-2095">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2095">No</span></span> |
| <span data-ttu-id="566d6-2096">format</span><span class="sxs-lookup"><span data-stu-id="566d6-2096">format</span></span> | <span data-ttu-id="566d6-2097">支援下列格式類型的 hello: **TextFormat**， **JsonFormat**， **AvroFormat**， **OrcFormat**， **ParquetFormat**。</span><span class="sxs-lookup"><span data-stu-id="566d6-2097">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="566d6-2098">設定 hello**類型**下格式 tooone 這些值的屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-2098">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="566d6-2099">如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。</span><span class="sxs-lookup"><span data-stu-id="566d6-2099">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="566d6-2100">如果您想太**複製檔做為-是**之間以檔案為基礎存放區 （二進位複製），略過這兩個輸入和輸出資料集定義中的 hello 格式 > 一節。</span><span class="sxs-lookup"><span data-stu-id="566d6-2100">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="566d6-2101">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2101">No</span></span> |
| <span data-ttu-id="566d6-2102">compression</span><span class="sxs-lookup"><span data-stu-id="566d6-2102">compression</span></span> | <span data-ttu-id="566d6-2103">指定 hello 類型和層級的 hello 資料壓縮。</span><span class="sxs-lookup"><span data-stu-id="566d6-2103">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="566d6-2104">支援的類型為：**GZip**、**Deflate**、**BZip2** 和 **ZipDeflate**，而支援的層級為：**最佳**和**最快**。</span><span class="sxs-lookup"><span data-stu-id="566d6-2104">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="566d6-2105">如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。</span><span class="sxs-lookup"><span data-stu-id="566d6-2105">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="566d6-2106">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2106">No</span></span> |
| <span data-ttu-id="566d6-2107">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="566d6-2107">useBinaryTransfer</span></span> |<span data-ttu-id="566d6-2108">指定是否使用二進位傳輸模式。</span><span class="sxs-lookup"><span data-stu-id="566d6-2108">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="566d6-2109">二進位模式為 true，ASCII 則為 false。</span><span class="sxs-lookup"><span data-stu-id="566d6-2109">True for binary mode and false ASCII.</span></span> <span data-ttu-id="566d6-2110">預設值：True。</span><span class="sxs-lookup"><span data-stu-id="566d6-2110">Default value: True.</span></span> <span data-ttu-id="566d6-2111">只有在相關聯的連結服務類型的類型為 FtpServer 時，才可以使用這個屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-2111">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="566d6-2112">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2112">No</span></span> |

> [!NOTE]
> <span data-ttu-id="566d6-2113">無法同時使用檔名和 fileFilter。</span><span class="sxs-lookup"><span data-stu-id="566d6-2113">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="566d6-2114">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-2114">Example</span></span>

```json
{
    "name": "FTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "FTPLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
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

<span data-ttu-id="566d6-2115">如需詳細資訊，請參閱 [FTP 連接器](data-factory-ftp-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-2115">For more information, see [FTP connector](data-factory-ftp-connector.md#dataset-properties) article.</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="566d6-2116">複製活動中的檔案系統來源</span><span class="sxs-lookup"><span data-stu-id="566d6-2116">File System Source in Copy Activity</span></span>
<span data-ttu-id="566d6-2117">如果您從 FTP 伺服器複製資料，設定 hello**來源類型**的 hello 複製活動太**FileSystemSource**，並指定下列屬性在 hello**來源**區段：</span><span class="sxs-lookup"><span data-stu-id="566d6-2117">If you are copying data from an FTP server, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="566d6-2118">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2118">Property</span></span> | <span data-ttu-id="566d6-2119">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2119">Description</span></span> | <span data-ttu-id="566d6-2120">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-2120">Allowed values</span></span> | <span data-ttu-id="566d6-2121">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2121">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-2122">遞迴</span><span class="sxs-lookup"><span data-stu-id="566d6-2122">recursive</span></span> |<span data-ttu-id="566d6-2123">指出是否 hello 讀取資料以遞迴方式從 hello 子資料夾，或只能從 hello 指定的資料夾。</span><span class="sxs-lookup"><span data-stu-id="566d6-2123">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="566d6-2124">True/False (預設值為 False)</span><span class="sxs-lookup"><span data-stu-id="566d6-2124">True, False (default)</span></span> |<span data-ttu-id="566d6-2125">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2125">No</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-2126">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-2126">Example</span></span>

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

<span data-ttu-id="566d6-2127">如需詳細資訊，請參閱 [FTP 連接器](data-factory-ftp-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-2127">For more information, see [FTP connector](data-factory-ftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="hdfs"></a><span data-ttu-id="566d6-2128">HDFS</span><span class="sxs-lookup"><span data-stu-id="566d6-2128">HDFS</span></span>

### <a name="linked-service"></a><span data-ttu-id="566d6-2129">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-2129">Linked service</span></span>
<span data-ttu-id="566d6-2130">toodefine HDFS 連結服務，設定 hello**類型**hello 的連結服務太**Hdfs**，並指定下列屬性在 hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-2130">toodefine a HDFS linked service, set hello **type** of hello linked service too**Hdfs**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="566d6-2131">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2131">Property</span></span> | <span data-ttu-id="566d6-2132">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2132">Description</span></span> | <span data-ttu-id="566d6-2133">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2133">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-2134">類型</span><span class="sxs-lookup"><span data-stu-id="566d6-2134">type</span></span> |<span data-ttu-id="566d6-2135">hello 類型屬性必須設定為： **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="566d6-2135">hello type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="566d6-2136">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2136">Yes</span></span> |
| <span data-ttu-id="566d6-2137">Url</span><span class="sxs-lookup"><span data-stu-id="566d6-2137">Url</span></span> |<span data-ttu-id="566d6-2138">URL toohello HDFS</span><span class="sxs-lookup"><span data-stu-id="566d6-2138">URL toohello HDFS</span></span> |<span data-ttu-id="566d6-2139">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2139">Yes</span></span> |
| <span data-ttu-id="566d6-2140">authenticationType</span><span class="sxs-lookup"><span data-stu-id="566d6-2140">authenticationType</span></span> |<span data-ttu-id="566d6-2141">匿名或 Windows。</span><span class="sxs-lookup"><span data-stu-id="566d6-2141">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="566d6-2142">toouse **Kerberos 驗證**HDFS 連接器，請參閱太[本節](#use-kerberos-authentication-for-hdfs-connector)在內部部署環境 tooset 據此。</span><span class="sxs-lookup"><span data-stu-id="566d6-2142">toouse **Kerberos authentication** for HDFS connector, refer too[this section](#use-kerberos-authentication-for-hdfs-connector) tooset up your on-premises environment accordingly.</span></span> |<span data-ttu-id="566d6-2143">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2143">Yes</span></span> |
| <span data-ttu-id="566d6-2144">userName</span><span class="sxs-lookup"><span data-stu-id="566d6-2144">userName</span></span> |<span data-ttu-id="566d6-2145">Windows 驗證的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-2145">Username for Windows authentication.</span></span> |<span data-ttu-id="566d6-2146">是 (適用於 Windows 驗證)</span><span class="sxs-lookup"><span data-stu-id="566d6-2146">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="566d6-2147">password</span><span class="sxs-lookup"><span data-stu-id="566d6-2147">password</span></span> |<span data-ttu-id="566d6-2148">Windows 驗證的密碼。</span><span class="sxs-lookup"><span data-stu-id="566d6-2148">Password for Windows authentication.</span></span> |<span data-ttu-id="566d6-2149">是 (適用於 Windows 驗證)</span><span class="sxs-lookup"><span data-stu-id="566d6-2149">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="566d6-2150">gatewayName</span><span class="sxs-lookup"><span data-stu-id="566d6-2150">gatewayName</span></span> |<span data-ttu-id="566d6-2151">Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello HDFS。</span><span class="sxs-lookup"><span data-stu-id="566d6-2151">Name of hello gateway that hello Data Factory service should use tooconnect toohello HDFS.</span></span> |<span data-ttu-id="566d6-2152">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2152">Yes</span></span> |
| <span data-ttu-id="566d6-2153">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="566d6-2153">encryptedCredential</span></span> |<span data-ttu-id="566d6-2154">[新 AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) hello 存取認證的輸出。</span><span class="sxs-lookup"><span data-stu-id="566d6-2154">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output of hello access credential.</span></span> |<span data-ttu-id="566d6-2155">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2155">No</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="566d6-2156">範例：使用匿名驗證</span><span class="sxs-lookup"><span data-stu-id="566d6-2156">Example: Using Anonymous authentication</span></span>

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

#### <a name="example-using-windows-authentication"></a><span data-ttu-id="566d6-2157">範例：使用 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="566d6-2157">Example: Using Windows authentication</span></span>

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

<span data-ttu-id="566d6-2158">如需詳細資訊，請參閱 [HDFS 連接器](#data-factory-hdfs-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-2158">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="566d6-2159">Dataset</span><span class="sxs-lookup"><span data-stu-id="566d6-2159">Dataset</span></span>
<span data-ttu-id="566d6-2160">toodefine HDFS 資料集設定 hello**類型**hello 資料集太**FileShare**，並指定下列屬性在 hello hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-2160">toodefine a HDFS dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="566d6-2161">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2161">Property</span></span> | <span data-ttu-id="566d6-2162">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2162">Description</span></span> | <span data-ttu-id="566d6-2163">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2163">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-2164">folderPath</span><span class="sxs-lookup"><span data-stu-id="566d6-2164">folderPath</span></span> |<span data-ttu-id="566d6-2165">路徑 toohello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="566d6-2165">Path toohello folder.</span></span> <span data-ttu-id="566d6-2166">範例： `myfolder`</span><span class="sxs-lookup"><span data-stu-id="566d6-2166">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="566d6-2167">使用逸出字元 '\' hello 字串中的特殊字元。</span><span class="sxs-lookup"><span data-stu-id="566d6-2167">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="566d6-2168">例如︰若為 folder\subfolder，請指定 folder\\\\subfolder；若為 d:\samplefolder，請指定 d:\\\\samplefolder。</span><span class="sxs-lookup"><span data-stu-id="566d6-2168">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="566d6-2169">您可以結合此屬性與**partitionBy** toohave 資料夾路徑根據配量開始/結束日期時間。</span><span class="sxs-lookup"><span data-stu-id="566d6-2169">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="566d6-2170">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2170">Yes</span></span> |
| <span data-ttu-id="566d6-2171">fileName</span><span class="sxs-lookup"><span data-stu-id="566d6-2171">fileName</span></span> |<span data-ttu-id="566d6-2172">在 hello 指定 hello hello 檔案名稱**folderPath**如果您想 hello 資料表 toorefer tooa 特定檔案 hello 資料夾中的。</span><span class="sxs-lookup"><span data-stu-id="566d6-2172">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="566d6-2173">如果您未指定任何值，這個屬性，hello 資料表會指向 tooall hello 資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="566d6-2173">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="566d6-2174">檔案名稱未指定輸出資料集，hello hello 產生檔案名稱會在 hello 遵循此格式：</span><span class="sxs-lookup"><span data-stu-id="566d6-2174">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="566d6-2175">Data<Guid>.txt (例如：Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="566d6-2175">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="566d6-2176">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2176">No</span></span> |
| <span data-ttu-id="566d6-2177">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="566d6-2177">partitionedBy</span></span> |<span data-ttu-id="566d6-2178">partitionedBy 可以是使用的 toospecify 動態 folderPath，時間序列資料的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-2178">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="566d6-2179">範例：folderPath 可針對每小時的資料進行參數化。</span><span class="sxs-lookup"><span data-stu-id="566d6-2179">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="566d6-2180">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2180">No</span></span> |
| <span data-ttu-id="566d6-2181">format</span><span class="sxs-lookup"><span data-stu-id="566d6-2181">format</span></span> | <span data-ttu-id="566d6-2182">支援下列格式類型的 hello: **TextFormat**， **JsonFormat**， **AvroFormat**， **OrcFormat**， **ParquetFormat**。</span><span class="sxs-lookup"><span data-stu-id="566d6-2182">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="566d6-2183">設定 hello**類型**下格式 tooone 這些值的屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-2183">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="566d6-2184">如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。</span><span class="sxs-lookup"><span data-stu-id="566d6-2184">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="566d6-2185">如果您想太**複製檔做為-是**之間以檔案為基礎存放區 （二進位複製），略過這兩個輸入和輸出資料集定義中的 hello 格式 > 一節。</span><span class="sxs-lookup"><span data-stu-id="566d6-2185">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="566d6-2186">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2186">No</span></span> |
| <span data-ttu-id="566d6-2187">compression</span><span class="sxs-lookup"><span data-stu-id="566d6-2187">compression</span></span> | <span data-ttu-id="566d6-2188">指定 hello 類型和層級的 hello 資料壓縮。</span><span class="sxs-lookup"><span data-stu-id="566d6-2188">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="566d6-2189">支援的類型為：**GZip**、**Deflate**、**BZip2** 及 **ZipDeflate**。</span><span class="sxs-lookup"><span data-stu-id="566d6-2189">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="566d6-2190">支援的層級為：**Optimal** 和 **Fastest**。</span><span class="sxs-lookup"><span data-stu-id="566d6-2190">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="566d6-2191">如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。</span><span class="sxs-lookup"><span data-stu-id="566d6-2191">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="566d6-2192">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2192">No</span></span> |

> [!NOTE]
> <span data-ttu-id="566d6-2193">無法同時使用檔名和 fileFilter。</span><span class="sxs-lookup"><span data-stu-id="566d6-2193">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="566d6-2194">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-2194">Example</span></span>

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

<span data-ttu-id="566d6-2195">如需詳細資訊，請參閱 [HDFS 連接器](#data-factory-hdfs-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-2195">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="566d6-2196">複製活動中的檔案系統來源</span><span class="sxs-lookup"><span data-stu-id="566d6-2196">File System Source in Copy Activity</span></span>
<span data-ttu-id="566d6-2197">如果您從 HDFS 中複製資料，設定 hello**來源類型**的 hello 複製活動太**FileSystemSource**，並指定下列屬性在 hello**來源**> 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-2197">If you are copying data from HDFS, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

<span data-ttu-id="566d6-2198">**FileSystemSource**支援 hello 下列屬性：</span><span class="sxs-lookup"><span data-stu-id="566d6-2198">**FileSystemSource** supports hello following properties:</span></span>

| <span data-ttu-id="566d6-2199">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2199">Property</span></span> | <span data-ttu-id="566d6-2200">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2200">Description</span></span> | <span data-ttu-id="566d6-2201">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-2201">Allowed values</span></span> | <span data-ttu-id="566d6-2202">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2202">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-2203">遞迴</span><span class="sxs-lookup"><span data-stu-id="566d6-2203">recursive</span></span> |<span data-ttu-id="566d6-2204">指出是否 hello 讀取資料以遞迴方式從 hello 子資料夾，或只能從 hello 指定的資料夾。</span><span class="sxs-lookup"><span data-stu-id="566d6-2204">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="566d6-2205">True/False (預設值為 False)</span><span class="sxs-lookup"><span data-stu-id="566d6-2205">True, False (default)</span></span> |<span data-ttu-id="566d6-2206">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2206">No</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-2207">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-2207">Example</span></span>

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

<span data-ttu-id="566d6-2208">如需詳細資訊，請參閱 [HDFS 連接器](#data-factory-hdfs-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-2208">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#copy-activity-properties) article.</span></span>

## <a name="sftp"></a><span data-ttu-id="566d6-2209">SFTP</span><span class="sxs-lookup"><span data-stu-id="566d6-2209">SFTP</span></span>


### <a name="linked-service"></a><span data-ttu-id="566d6-2210">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-2210">Linked service</span></span>
<span data-ttu-id="566d6-2211">toodefine SFTP 連結服務，設定 hello**類型**hello 的連結服務太**Sftp**，並指定下列屬性在 hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-2211">toodefine an SFTP linked service, set hello **type** of hello linked service too**Sftp**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="566d6-2212">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2212">Property</span></span> | <span data-ttu-id="566d6-2213">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2213">Description</span></span> | <span data-ttu-id="566d6-2214">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2214">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-2215">主機</span><span class="sxs-lookup"><span data-stu-id="566d6-2215">host</span></span> | <span data-ttu-id="566d6-2216">Hello SFTP 伺服器的名稱或 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="566d6-2216">Name or IP address of hello SFTP server.</span></span> |<span data-ttu-id="566d6-2217">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2217">Yes</span></span> |
| <span data-ttu-id="566d6-2218">連接埠</span><span class="sxs-lookup"><span data-stu-id="566d6-2218">port</span></span> |<span data-ttu-id="566d6-2219">哪些 hello SFTP 伺服器正在接聽連接埠。</span><span class="sxs-lookup"><span data-stu-id="566d6-2219">Port on which hello SFTP server is listening.</span></span> <span data-ttu-id="566d6-2220">hello 預設值是： 21</span><span class="sxs-lookup"><span data-stu-id="566d6-2220">hello default value is: 21</span></span> |<span data-ttu-id="566d6-2221">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2221">No</span></span> |
| <span data-ttu-id="566d6-2222">authenticationType</span><span class="sxs-lookup"><span data-stu-id="566d6-2222">authenticationType</span></span> |<span data-ttu-id="566d6-2223">指定驗證類型。</span><span class="sxs-lookup"><span data-stu-id="566d6-2223">Specify authentication type.</span></span> <span data-ttu-id="566d6-2224">允許的值︰**Basic**、**SshPublicKey**。</span><span class="sxs-lookup"><span data-stu-id="566d6-2224">Allowed values: **Basic**, **SshPublicKey**.</span></span> <br><br> <span data-ttu-id="566d6-2225">請參閱太[使用基本驗證](#using-basic-authentication)和[使用 SSH 公開金鑰驗證](#using-ssh-public-key-authentication)分別區段上多個屬性和 JSON 範例。</span><span class="sxs-lookup"><span data-stu-id="566d6-2225">Refer too[Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span></span> |<span data-ttu-id="566d6-2226">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2226">Yes</span></span> |
| <span data-ttu-id="566d6-2227">skipHostKeyValidation</span><span class="sxs-lookup"><span data-stu-id="566d6-2227">skipHostKeyValidation</span></span> | <span data-ttu-id="566d6-2228">指定是否 tooskip 主機金鑰的驗證。</span><span class="sxs-lookup"><span data-stu-id="566d6-2228">Specify whether tooskip host key validation.</span></span> | <span data-ttu-id="566d6-2229">否。</span><span class="sxs-lookup"><span data-stu-id="566d6-2229">No.</span></span> <span data-ttu-id="566d6-2230">hello 預設值： false</span><span class="sxs-lookup"><span data-stu-id="566d6-2230">hello default value: false</span></span> |
| <span data-ttu-id="566d6-2231">hostKeyFingerprint</span><span class="sxs-lookup"><span data-stu-id="566d6-2231">hostKeyFingerprint</span></span> | <span data-ttu-id="566d6-2232">指定 hello 指紋 hello 主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="566d6-2232">Specify hello finger print of hello host key.</span></span> | <span data-ttu-id="566d6-2233">是如果 hello `skipHostKeyValidation` toofalse 設定。</span><span class="sxs-lookup"><span data-stu-id="566d6-2233">Yes if hello `skipHostKeyValidation` is set toofalse.</span></span>  |
| <span data-ttu-id="566d6-2234">gatewayName</span><span class="sxs-lookup"><span data-stu-id="566d6-2234">gatewayName</span></span> |<span data-ttu-id="566d6-2235">名稱的 hello 資料管理閘道器 tooconnect tooan 內部 SFTP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="566d6-2235">Name of hello Data Management Gateway tooconnect tooan on-premises SFTP server.</span></span> | <span data-ttu-id="566d6-2236">如果從內部部署 SFTP 伺服器複製資料，則為 [是]。</span><span class="sxs-lookup"><span data-stu-id="566d6-2236">Yes if copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="566d6-2237">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="566d6-2237">encryptedCredential</span></span> | <span data-ttu-id="566d6-2238">加密的認證 tooaccess hello SFTP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="566d6-2238">Encrypted credential tooaccess hello SFTP server.</span></span> <span data-ttu-id="566d6-2239">自動產生複製精靈] 或 [hello ClickOnce 快顯對話方塊中指定基本驗證 （使用者名稱 + 密碼） 或 SshPublicKey 驗證 （使用者名稱 + 私用金鑰的路徑或內容） 時。</span><span class="sxs-lookup"><span data-stu-id="566d6-2239">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="566d6-2240">否。</span><span class="sxs-lookup"><span data-stu-id="566d6-2240">No.</span></span> <span data-ttu-id="566d6-2241">僅當從內部部署 SFTP 伺服器複製資料時才套用。</span><span class="sxs-lookup"><span data-stu-id="566d6-2241">Apply only when copying data from an on-premises SFTP server.</span></span> |

#### <a name="example-using-basic-authentication"></a><span data-ttu-id="566d6-2242">範例：使用基本驗證</span><span class="sxs-lookup"><span data-stu-id="566d6-2242">Example: Using basic authentication</span></span>

<span data-ttu-id="566d6-2243">toouse 基本驗證時，設定`authenticationType`為`Basic`，並指定下列屬性，除了 hello SFTP 連接器 hello 最後一節中導入的泛型的 hello:</span><span class="sxs-lookup"><span data-stu-id="566d6-2243">toouse basic authentication, set `authenticationType` as `Basic`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="566d6-2244">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2244">Property</span></span> | <span data-ttu-id="566d6-2245">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2245">Description</span></span> | <span data-ttu-id="566d6-2246">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2246">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-2247">username</span><span class="sxs-lookup"><span data-stu-id="566d6-2247">username</span></span> | <span data-ttu-id="566d6-2248">具有存取 toohello SFTP 伺服器的使用者。</span><span class="sxs-lookup"><span data-stu-id="566d6-2248">User who has access toohello SFTP server.</span></span> |<span data-ttu-id="566d6-2249">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2249">Yes</span></span> |
| <span data-ttu-id="566d6-2250">password</span><span class="sxs-lookup"><span data-stu-id="566d6-2250">password</span></span> | <span data-ttu-id="566d6-2251">Hello 使用者 （使用者名稱） 的密碼。</span><span class="sxs-lookup"><span data-stu-id="566d6-2251">Password for hello user (username).</span></span> | <span data-ttu-id="566d6-2252">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2252">Yes</span></span> |

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

#### <a name="example-basic-authentication-with-encrypted-credential"></a><span data-ttu-id="566d6-2253">範例：採用加密認證的基本驗證**</span><span class="sxs-lookup"><span data-stu-id="566d6-2253">Example: Basic authentication with encrypted credential**</span></span>

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

#### <a name="using-ssh-public-key-authentication"></a><span data-ttu-id="566d6-2254">使用 SSH 公用金鑰驗證：**</span><span class="sxs-lookup"><span data-stu-id="566d6-2254">Using SSH public key authentication:**</span></span>

<span data-ttu-id="566d6-2255">toouse 基本驗證時，設定`authenticationType`為`SshPublicKey`，並指定下列屬性，除了 hello SFTP 連接器 hello 最後一節中導入的泛型的 hello:</span><span class="sxs-lookup"><span data-stu-id="566d6-2255">toouse basic authentication, set `authenticationType` as `SshPublicKey`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="566d6-2256">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2256">Property</span></span> | <span data-ttu-id="566d6-2257">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2257">Description</span></span> | <span data-ttu-id="566d6-2258">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2258">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-2259">username</span><span class="sxs-lookup"><span data-stu-id="566d6-2259">username</span></span> |<span data-ttu-id="566d6-2260">使用者具有存取 toohello SFTP 伺服器</span><span class="sxs-lookup"><span data-stu-id="566d6-2260">User who has access toohello SFTP server</span></span> |<span data-ttu-id="566d6-2261">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2261">Yes</span></span> |
| <span data-ttu-id="566d6-2262">privateKeyPath</span><span class="sxs-lookup"><span data-stu-id="566d6-2262">privateKeyPath</span></span> | <span data-ttu-id="566d6-2263">指定絕對路徑 toohello 私密金鑰檔案可以存取該閘道。</span><span class="sxs-lookup"><span data-stu-id="566d6-2263">Specify absolute path toohello private key file that gateway can access.</span></span> | <span data-ttu-id="566d6-2264">指定任一個 hello`privateKeyPath`或`privateKeyContent`。</span><span class="sxs-lookup"><span data-stu-id="566d6-2264">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> <br><br> <span data-ttu-id="566d6-2265">僅當從內部部署 SFTP 伺服器複製資料時才套用。</span><span class="sxs-lookup"><span data-stu-id="566d6-2265">Apply only when copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="566d6-2266">privateKeyContent</span><span class="sxs-lookup"><span data-stu-id="566d6-2266">privateKeyContent</span></span> | <span data-ttu-id="566d6-2267">Hello 私用的索引鍵內容的序列化的字串。</span><span class="sxs-lookup"><span data-stu-id="566d6-2267">A serialized string of hello private key content.</span></span> <span data-ttu-id="566d6-2268">hello 複製精靈可以讀取 hello 私密金鑰檔案，並自動擷取 hello 私用的索引鍵內容。</span><span class="sxs-lookup"><span data-stu-id="566d6-2268">hello Copy Wizard can read hello private key file and extract hello private key content automatically.</span></span> <span data-ttu-id="566d6-2269">如果您使用任何其他工具/SDK，請改為使用 hello privateKeyPath 屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-2269">If you are using any other tool/SDK, use hello privateKeyPath property instead.</span></span> | <span data-ttu-id="566d6-2270">指定任一個 hello`privateKeyPath`或`privateKeyContent`。</span><span class="sxs-lookup"><span data-stu-id="566d6-2270">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> |
| <span data-ttu-id="566d6-2271">passPhrase</span><span class="sxs-lookup"><span data-stu-id="566d6-2271">passPhrase</span></span> | <span data-ttu-id="566d6-2272">指定 hello 傳遞片語/密碼 toodecrypt hello 私密金鑰如果 hello 金鑰檔受複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="566d6-2272">Specify hello pass phrase/password toodecrypt hello private key if hello key file is protected by a pass phrase.</span></span> | <span data-ttu-id="566d6-2273">[是] 如果 hello 私密金鑰檔案受複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="566d6-2273">Yes if hello private key file is protected by a pass phrase.</span></span> |

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

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a><span data-ttu-id="566d6-2274">範例︰使用私密金鑰內容的 SshPublicKey 驗證**</span><span class="sxs-lookup"><span data-stu-id="566d6-2274">Example: SshPublicKey authentication using private key content**</span></span>

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
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

<span data-ttu-id="566d6-2275">如需詳細資訊，請參閱 [SFTP 連接器](data-factory-sftp-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-2275">For more information, see [SFTP connector](data-factory-sftp-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="566d6-2276">Dataset</span><span class="sxs-lookup"><span data-stu-id="566d6-2276">Dataset</span></span>
<span data-ttu-id="566d6-2277">toodefine SFTP 資料集設定 hello**類型**hello 資料集太**FileShare**，並指定下列屬性在 hello hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-2277">toodefine an SFTP dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="566d6-2278">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2278">Property</span></span> | <span data-ttu-id="566d6-2279">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2279">Description</span></span> | <span data-ttu-id="566d6-2280">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2280">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-2281">folderPath</span><span class="sxs-lookup"><span data-stu-id="566d6-2281">folderPath</span></span> |<span data-ttu-id="566d6-2282">子路徑 toohello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="566d6-2282">Sub path toohello folder.</span></span> <span data-ttu-id="566d6-2283">使用逸出字元 '\' hello 字串中的特殊字元。</span><span class="sxs-lookup"><span data-stu-id="566d6-2283">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="566d6-2284">如需範例，請參閱 [範例連結服務和資料集定義](#sample-linked-service-and-dataset-definitions) 。</span><span class="sxs-lookup"><span data-stu-id="566d6-2284">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="566d6-2285">您可以結合此屬性與**partitionBy** toohave 資料夾路徑根據配量開始/結束日期時間。</span><span class="sxs-lookup"><span data-stu-id="566d6-2285">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="566d6-2286">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2286">Yes</span></span> |
| <span data-ttu-id="566d6-2287">fileName</span><span class="sxs-lookup"><span data-stu-id="566d6-2287">fileName</span></span> |<span data-ttu-id="566d6-2288">在 hello 指定 hello hello 檔案名稱**folderPath**如果您想 hello 資料表 toorefer tooa 特定檔案 hello 資料夾中的。</span><span class="sxs-lookup"><span data-stu-id="566d6-2288">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="566d6-2289">如果您未指定任何值，這個屬性，hello 資料表會指向 tooall hello 資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="566d6-2289">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="566d6-2290">檔案名稱未指定輸出資料集，hello hello 產生檔案名稱會在 hello 遵循此格式：</span><span class="sxs-lookup"><span data-stu-id="566d6-2290">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="566d6-2291">Data.<Guid>.txt (範例：Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="566d6-2291">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="566d6-2292">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2292">No</span></span> |
| <span data-ttu-id="566d6-2293">fileFilter</span><span class="sxs-lookup"><span data-stu-id="566d6-2293">fileFilter</span></span> |<span data-ttu-id="566d6-2294">指定篩選 toobe 使用 tooselect hello folderPath 中檔案的子集，而不是所有的檔案。</span><span class="sxs-lookup"><span data-stu-id="566d6-2294">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="566d6-2295">允許的值為︰`*` (多個字元) 和 `?` (單一字元)。</span><span class="sxs-lookup"><span data-stu-id="566d6-2295">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="566d6-2296">範例 1：`"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="566d6-2296">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="566d6-2297">範例 2：`"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="566d6-2297">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="566d6-2298">fileFilter 適用於輸入 FileShare 資料集。</span><span class="sxs-lookup"><span data-stu-id="566d6-2298">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="566d6-2299">這個屬性不支援使用 HDFS。</span><span class="sxs-lookup"><span data-stu-id="566d6-2299">This property is not supported with HDFS.</span></span> |<span data-ttu-id="566d6-2300">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2300">No</span></span> |
| <span data-ttu-id="566d6-2301">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="566d6-2301">partitionedBy</span></span> |<span data-ttu-id="566d6-2302">partitionedBy 可以是使用的 toospecify 動態 folderPath，時間序列資料的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-2302">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="566d6-2303">例如，folderPath 可針對每小時的資料進行參數化。</span><span class="sxs-lookup"><span data-stu-id="566d6-2303">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="566d6-2304">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2304">No</span></span> |
| <span data-ttu-id="566d6-2305">format</span><span class="sxs-lookup"><span data-stu-id="566d6-2305">format</span></span> | <span data-ttu-id="566d6-2306">支援下列格式類型的 hello: **TextFormat**， **JsonFormat**， **AvroFormat**， **OrcFormat**， **ParquetFormat**。</span><span class="sxs-lookup"><span data-stu-id="566d6-2306">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="566d6-2307">設定 hello**類型**下格式 tooone 這些值的屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-2307">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="566d6-2308">如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。</span><span class="sxs-lookup"><span data-stu-id="566d6-2308">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="566d6-2309">如果您想太**複製檔做為-是**之間以檔案為基礎存放區 （二進位複製），略過這兩個輸入和輸出資料集定義中的 hello 格式 > 一節。</span><span class="sxs-lookup"><span data-stu-id="566d6-2309">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="566d6-2310">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2310">No</span></span> |
| <span data-ttu-id="566d6-2311">compression</span><span class="sxs-lookup"><span data-stu-id="566d6-2311">compression</span></span> | <span data-ttu-id="566d6-2312">指定 hello 類型和層級的 hello 資料壓縮。</span><span class="sxs-lookup"><span data-stu-id="566d6-2312">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="566d6-2313">支援的類型為：**GZip**、**Deflate**、**BZip2** 及 **ZipDeflate**。</span><span class="sxs-lookup"><span data-stu-id="566d6-2313">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="566d6-2314">支援的層級為：**Optimal** 和 **Fastest**。</span><span class="sxs-lookup"><span data-stu-id="566d6-2314">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="566d6-2315">如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。</span><span class="sxs-lookup"><span data-stu-id="566d6-2315">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="566d6-2316">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2316">No</span></span> |
| <span data-ttu-id="566d6-2317">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="566d6-2317">useBinaryTransfer</span></span> |<span data-ttu-id="566d6-2318">指定是否使用二進位傳輸模式。</span><span class="sxs-lookup"><span data-stu-id="566d6-2318">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="566d6-2319">二進位模式為 true，ASCII 則為 false。</span><span class="sxs-lookup"><span data-stu-id="566d6-2319">True for binary mode and false ASCII.</span></span> <span data-ttu-id="566d6-2320">預設值：True。</span><span class="sxs-lookup"><span data-stu-id="566d6-2320">Default value: True.</span></span> <span data-ttu-id="566d6-2321">只有在相關聯的連結服務類型的類型為 FtpServer 時，才可以使用這個屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-2321">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="566d6-2322">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2322">No</span></span> |

> [!NOTE]
> <span data-ttu-id="566d6-2323">無法同時使用檔名和 fileFilter。</span><span class="sxs-lookup"><span data-stu-id="566d6-2323">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="566d6-2324">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-2324">Example</span></span>

```json
{
    "name": "SFTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "SftpLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
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

<span data-ttu-id="566d6-2325">如需詳細資訊，請參閱 [SFTP 連接器](data-factory-sftp-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-2325">For more information, see [SFTP connector](data-factory-sftp-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="566d6-2326">複製活動中的檔案系統來源</span><span class="sxs-lookup"><span data-stu-id="566d6-2326">File System Source in Copy Activity</span></span>
<span data-ttu-id="566d6-2327">如果您從 SFTP 來源複製資料，設定 hello**來源類型**的 hello 複製活動太**FileSystemSource**，並指定下列屬性在 hello**來源**區段：</span><span class="sxs-lookup"><span data-stu-id="566d6-2327">If you are copying data from an SFTP source, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="566d6-2328">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2328">Property</span></span> | <span data-ttu-id="566d6-2329">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2329">Description</span></span> | <span data-ttu-id="566d6-2330">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-2330">Allowed values</span></span> | <span data-ttu-id="566d6-2331">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2331">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-2332">遞迴</span><span class="sxs-lookup"><span data-stu-id="566d6-2332">recursive</span></span> |<span data-ttu-id="566d6-2333">指出是否 hello 讀取資料以遞迴方式從 hello 子資料夾，或只能從 hello 指定的資料夾。</span><span class="sxs-lookup"><span data-stu-id="566d6-2333">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="566d6-2334">True/False (預設值為 False)</span><span class="sxs-lookup"><span data-stu-id="566d6-2334">True, False (default)</span></span> |<span data-ttu-id="566d6-2335">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2335">No</span></span> |



#### <a name="example"></a><span data-ttu-id="566d6-2336">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-2336">Example</span></span>

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

<span data-ttu-id="566d6-2337">如需詳細資訊，請參閱 [SFTP 連接器](data-factory-sftp-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-2337">For more information, see [SFTP connector](data-factory-sftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="http"></a><span data-ttu-id="566d6-2338">HTTP</span><span class="sxs-lookup"><span data-stu-id="566d6-2338">HTTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="566d6-2339">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-2339">Linked service</span></span>
<span data-ttu-id="566d6-2340">toodefine HTTP 連結服務，設定 hello**類型**hello 的連結服務太**Http**，並指定下列屬性在 hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-2340">toodefine a HTTP linked service, set hello **type** of hello linked service too**Http**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="566d6-2341">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2341">Property</span></span> | <span data-ttu-id="566d6-2342">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2342">Description</span></span> | <span data-ttu-id="566d6-2343">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2343">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-2344">url</span><span class="sxs-lookup"><span data-stu-id="566d6-2344">url</span></span> | <span data-ttu-id="566d6-2345">基底 URL toohello Web 伺服器</span><span class="sxs-lookup"><span data-stu-id="566d6-2345">Base URL toohello Web Server</span></span> | <span data-ttu-id="566d6-2346">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2346">Yes</span></span> |
| <span data-ttu-id="566d6-2347">authenticationType</span><span class="sxs-lookup"><span data-stu-id="566d6-2347">authenticationType</span></span> | <span data-ttu-id="566d6-2348">指定 hello 驗證類型。</span><span class="sxs-lookup"><span data-stu-id="566d6-2348">Specifies hello authentication type.</span></span> <span data-ttu-id="566d6-2349">允許的值為︰**匿名**、**基本**、**摘要**、**Windows**、**ClientCertificate**。</span><span class="sxs-lookup"><span data-stu-id="566d6-2349">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="566d6-2350">請參閱 「 toosections 上多個屬性和 JSON 範例此表格下方的驗證類型分別。</span><span class="sxs-lookup"><span data-stu-id="566d6-2350">Refer toosections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="566d6-2351">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2351">Yes</span></span> |
| <span data-ttu-id="566d6-2352">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="566d6-2352">enableServerCertificateValidation</span></span> | <span data-ttu-id="566d6-2353">指定是否 tooenable 伺服器 SSL 憑證驗證，是否來源是 HTTPS 的網頁伺服器</span><span class="sxs-lookup"><span data-stu-id="566d6-2353">Specify whether tooenable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="566d6-2354">否，預設值是 True</span><span class="sxs-lookup"><span data-stu-id="566d6-2354">No, default is true</span></span> |
| <span data-ttu-id="566d6-2355">gatewayName</span><span class="sxs-lookup"><span data-stu-id="566d6-2355">gatewayName</span></span> | <span data-ttu-id="566d6-2356">名稱的 hello 資料管理閘道器 tooconnect tooan 內部 HTTP 的來源。</span><span class="sxs-lookup"><span data-stu-id="566d6-2356">Name of hello Data Management Gateway tooconnect tooan on-premises HTTP source.</span></span> | <span data-ttu-id="566d6-2357">如果從內部部署 HTTP 來源複製資料，則為是。</span><span class="sxs-lookup"><span data-stu-id="566d6-2357">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="566d6-2358">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="566d6-2358">encryptedCredential</span></span> | <span data-ttu-id="566d6-2359">加密的認證 tooaccess hello HTTP 端點。</span><span class="sxs-lookup"><span data-stu-id="566d6-2359">Encrypted credential tooaccess hello HTTP endpoint.</span></span> <span data-ttu-id="566d6-2360">自動產生複製精靈] 或 [hello ClickOnce 快顯對話方塊以設定 hello 驗證資訊。</span><span class="sxs-lookup"><span data-stu-id="566d6-2360">Auto-generated when you configure hello authentication information in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="566d6-2361">否。</span><span class="sxs-lookup"><span data-stu-id="566d6-2361">No.</span></span> <span data-ttu-id="566d6-2362">僅當從內部部署 HTTP 伺服器複製資料時才套用。</span><span class="sxs-lookup"><span data-stu-id="566d6-2362">Apply only when copying data from an on-premises HTTP server.</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="566d6-2363">範例︰使用基本、摘要或 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="566d6-2363">Example: Using Basic, Digest, or Windows authentication</span></span>
<span data-ttu-id="566d6-2364">設定`authenticationType`為`Basic`， `Digest`，或`Windows`，並指定 hello 除了 hello HTTP 連接器泛型的上方導入了下列屬性：</span><span class="sxs-lookup"><span data-stu-id="566d6-2364">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="566d6-2365">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2365">Property</span></span> | <span data-ttu-id="566d6-2366">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2366">Description</span></span> | <span data-ttu-id="566d6-2367">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2367">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-2368">username</span><span class="sxs-lookup"><span data-stu-id="566d6-2368">username</span></span> | <span data-ttu-id="566d6-2369">使用者名稱 tooaccess hello HTTP 端點。</span><span class="sxs-lookup"><span data-stu-id="566d6-2369">Username tooaccess hello HTTP endpoint.</span></span> | <span data-ttu-id="566d6-2370">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2370">Yes</span></span> |
| <span data-ttu-id="566d6-2371">password</span><span class="sxs-lookup"><span data-stu-id="566d6-2371">password</span></span> | <span data-ttu-id="566d6-2372">Hello 使用者 （使用者名稱） 的密碼。</span><span class="sxs-lookup"><span data-stu-id="566d6-2372">Password for hello user (username).</span></span> | <span data-ttu-id="566d6-2373">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2373">Yes</span></span> |

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

#### <a name="example-using-clientcertificate-authentication"></a><span data-ttu-id="566d6-2374">範例：使用 ClientCertificate 驗證</span><span class="sxs-lookup"><span data-stu-id="566d6-2374">Example: Using ClientCertificate authentication</span></span>

<span data-ttu-id="566d6-2375">toouse 基本驗證時，設定`authenticationType`為`ClientCertificate`，並指定 hello 除了 hello HTTP 連接器泛型的上方導入了下列屬性：</span><span class="sxs-lookup"><span data-stu-id="566d6-2375">toouse basic authentication, set `authenticationType` as `ClientCertificate`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="566d6-2376">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2376">Property</span></span> | <span data-ttu-id="566d6-2377">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2377">Description</span></span> | <span data-ttu-id="566d6-2378">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2378">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-2379">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="566d6-2379">embeddedCertData</span></span> | <span data-ttu-id="566d6-2380">hello Base64 編碼內容的 hello 個人資訊交換 (PFX) 檔案的二進位資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-2380">hello Base64-encoded contents of binary data of hello Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="566d6-2381">指定任一個 hello`embeddedCertData`或`certThumbprint`。</span><span class="sxs-lookup"><span data-stu-id="566d6-2381">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="566d6-2382">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="566d6-2382">certThumbprint</span></span> | <span data-ttu-id="566d6-2383">hello hello 憑證已安裝在閘道機器的憑證存放區上的憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="566d6-2383">hello thumbprint of hello certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="566d6-2384">僅當從內部部署 HTTP 來源複製資料時才套用。</span><span class="sxs-lookup"><span data-stu-id="566d6-2384">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="566d6-2385">指定任一個 hello`embeddedCertData`或`certThumbprint`。</span><span class="sxs-lookup"><span data-stu-id="566d6-2385">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="566d6-2386">password</span><span class="sxs-lookup"><span data-stu-id="566d6-2386">password</span></span> | <span data-ttu-id="566d6-2387">Hello 憑證相關聯的密碼。</span><span class="sxs-lookup"><span data-stu-id="566d6-2387">Password associated with hello certificate.</span></span> | <span data-ttu-id="566d6-2388">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2388">No</span></span> |

<span data-ttu-id="566d6-2389">如果您使用`certThumbprint`安裝適用於驗證和 hello 憑證的 hello hello 本機電腦的個人存放區中，您需要 toogrant hello 的讀取權限 toohello 閘道服務：</span><span class="sxs-lookup"><span data-stu-id="566d6-2389">If you use `certThumbprint` for authentication and hello certificate is installed in hello personal store of hello local computer, you need toogrant hello read permission toohello gateway service:</span></span>

1. <span data-ttu-id="566d6-2390">啟動 Microsoft Management Console (MMC)。</span><span class="sxs-lookup"><span data-stu-id="566d6-2390">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="566d6-2391">新增 hello**憑證**嵌入式管理單元的目標 hello**本機電腦**。</span><span class="sxs-lookup"><span data-stu-id="566d6-2391">Add hello **Certificates** snap-in that targets hello **Local Computer**.</span></span>
2. <span data-ttu-id="566d6-2392">展開 [憑證]，[個人]，然後按一下 [憑證]。</span><span class="sxs-lookup"><span data-stu-id="566d6-2392">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="566d6-2393">Hello 個人存放區中的 hello 憑證上按一下滑鼠右鍵，然後選取**所有工作**->**管理私用金鑰...**</span><span class="sxs-lookup"><span data-stu-id="566d6-2393">Right-click hello certificate from hello personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="566d6-2394">在 hello**安全性**索引標籤上，新增 hello 資料管理閘道主機服務執行使用 hello 讀取權限 toohello 憑證的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="566d6-2394">On hello **Security** tab, add hello user account under which Data Management Gateway Host Service is running with hello read access toohello certificate.</span></span>  

<span data-ttu-id="566d6-2395">**範例： 使用用戶端憑證：**此連結服務連結資料 factory tooan 內部 HTTP web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="566d6-2395">**Example: using client certificate:** This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="566d6-2396">它會使用與資料管理閘道器安裝 hello 機器已安裝的用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="566d6-2396">It uses a client certificate that is installed on hello machine with Data Management Gateway installed.</span></span>

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

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="566d6-2397">範例︰在檔案中使用用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="566d6-2397">Example: using client certificate in a file</span></span>
<span data-ttu-id="566d6-2398">此連結服務連結資料 factory tooan 內部 HTTP web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="566d6-2398">This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="566d6-2399">它會使用資料管理閘道器安裝 hello 機器上的用戶端憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="566d6-2399">It uses a client certificate file on hello machine with Data Management Gateway installed.</span></span>

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

<span data-ttu-id="566d6-2400">如需詳細資訊，請參閱 [HTTP 連接器](data-factory-http-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-2400">For more information, see [HTTP connector](data-factory-http-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="566d6-2401">Dataset</span><span class="sxs-lookup"><span data-stu-id="566d6-2401">Dataset</span></span>
<span data-ttu-id="566d6-2402">toodefine HTTP 資料集，設定 hello**類型**hello 資料集太**Http**，並指定下列屬性在 hello hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-2402">toodefine a HTTP dataset, set hello **type** of hello dataset too**Http**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="566d6-2403">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2403">Property</span></span> | <span data-ttu-id="566d6-2404">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2404">Description</span></span> | <span data-ttu-id="566d6-2405">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2405">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="566d6-2406">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="566d6-2406">relativeUrl</span></span> | <span data-ttu-id="566d6-2407">包含 hello 資料的相對 URL toohello 資源。</span><span class="sxs-lookup"><span data-stu-id="566d6-2407">A relative URL toohello resource that contains hello data.</span></span> <span data-ttu-id="566d6-2408">若未指定路徑，則會使用連結的 hello 服務定義中指定的唯一 hello URL。</span><span class="sxs-lookup"><span data-stu-id="566d6-2408">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> <br><br> <span data-ttu-id="566d6-2409">tooconstruct 動態 URL，您可以使用[Data Factory 函數和系統變數](data-factory-functions-variables.md)，範例： `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`。</span><span class="sxs-lookup"><span data-stu-id="566d6-2409">tooconstruct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), Example: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span></span> | <span data-ttu-id="566d6-2410">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2410">No</span></span> |
| <span data-ttu-id="566d6-2411">requestMethod</span><span class="sxs-lookup"><span data-stu-id="566d6-2411">requestMethod</span></span> | <span data-ttu-id="566d6-2412">HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="566d6-2412">Http method.</span></span> <span data-ttu-id="566d6-2413">允許的值為 **GET** 或 **POST**。</span><span class="sxs-lookup"><span data-stu-id="566d6-2413">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="566d6-2414">否。</span><span class="sxs-lookup"><span data-stu-id="566d6-2414">No.</span></span> <span data-ttu-id="566d6-2415">預設值為 `GET`。</span><span class="sxs-lookup"><span data-stu-id="566d6-2415">Default is `GET`.</span></span> |
| <span data-ttu-id="566d6-2416">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="566d6-2416">additionalHeaders</span></span> | <span data-ttu-id="566d6-2417">其他 HTTP 要求標頭。</span><span class="sxs-lookup"><span data-stu-id="566d6-2417">Additional HTTP request headers.</span></span> | <span data-ttu-id="566d6-2418">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2418">No</span></span> |
| <span data-ttu-id="566d6-2419">requestBody</span><span class="sxs-lookup"><span data-stu-id="566d6-2419">requestBody</span></span> | <span data-ttu-id="566d6-2420">HTTP 要求的內文。</span><span class="sxs-lookup"><span data-stu-id="566d6-2420">Body for HTTP request.</span></span> | <span data-ttu-id="566d6-2421">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2421">No</span></span> |
| <span data-ttu-id="566d6-2422">format</span><span class="sxs-lookup"><span data-stu-id="566d6-2422">format</span></span> | <span data-ttu-id="566d6-2423">如果您想 toosimply **hello 資料擷取 HTTP 端點以-為**而不剖析它，請略過此格式設定。</span><span class="sxs-lookup"><span data-stu-id="566d6-2423">If you want toosimply **retrieve hello data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="566d6-2424">如果您希望 tooparse hello HTTP 回應內容進行複製時，支援下列格式類型的 hello: **TextFormat**， **JsonFormat**， **AvroFormat**， **OrcFormat**， **ParquetFormat**。</span><span class="sxs-lookup"><span data-stu-id="566d6-2424">If you want tooparse hello HTTP response content during copy, hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="566d6-2425">如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。</span><span class="sxs-lookup"><span data-stu-id="566d6-2425">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="566d6-2426">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2426">No</span></span> |
| <span data-ttu-id="566d6-2427">compression</span><span class="sxs-lookup"><span data-stu-id="566d6-2427">compression</span></span> | <span data-ttu-id="566d6-2428">指定 hello 類型和層級的 hello 資料壓縮。</span><span class="sxs-lookup"><span data-stu-id="566d6-2428">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="566d6-2429">支援的類型為：**GZip**、**Deflate**、**BZip2** 及 **ZipDeflate**。</span><span class="sxs-lookup"><span data-stu-id="566d6-2429">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="566d6-2430">支援的層級為：**Optimal** 和 **Fastest**。</span><span class="sxs-lookup"><span data-stu-id="566d6-2430">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="566d6-2431">如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。</span><span class="sxs-lookup"><span data-stu-id="566d6-2431">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="566d6-2432">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2432">No</span></span> |

#### <a name="example-using-hello-get-default-method"></a><span data-ttu-id="566d6-2433">範例： 使用 hello GET （預設值） 方法</span><span class="sxs-lookup"><span data-stu-id="566d6-2433">Example: using hello GET (default) method</span></span>

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

#### <a name="example-using-hello-post-method"></a><span data-ttu-id="566d6-2434">範例： 使用 hello POST 方法</span><span class="sxs-lookup"><span data-stu-id="566d6-2434">Example: using hello POST method</span></span>

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
<span data-ttu-id="566d6-2435">如需詳細資訊，請參閱 [HTTP 連接器](data-factory-http-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-2435">For more information, see [HTTP connector](data-factory-http-connector.md#dataset-properties) article.</span></span>

### <a name="http-source-in-copy-activity"></a><span data-ttu-id="566d6-2436">複製活動中的 HTTP 來源</span><span class="sxs-lookup"><span data-stu-id="566d6-2436">HTTP Source in Copy Activity</span></span>
<span data-ttu-id="566d6-2437">如果您從 HTTP 來源複製資料，設定 hello**來源類型**的 hello 複製活動太**HttpSource**，並指定下列屬性在 hello**來源**> 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-2437">If you are copying data from a HTTP source, set hello **source type** of hello copy activity too**HttpSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="566d6-2438">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2438">Property</span></span> | <span data-ttu-id="566d6-2439">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2439">Description</span></span> | <span data-ttu-id="566d6-2440">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2440">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="566d6-2441">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="566d6-2441">httpRequestTimeout</span></span> | <span data-ttu-id="566d6-2442">hello 回應 hello HTTP 要求 tooget 的逾時 (TimeSpan)。</span><span class="sxs-lookup"><span data-stu-id="566d6-2442">hello timeout (TimeSpan) for hello HTTP request tooget a response.</span></span> <span data-ttu-id="566d6-2443">它是 hello 逾時 tooget 回應時，不 hello 逾時 tooread 回應資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-2443">It is hello timeout tooget a response, not hello timeout tooread response data.</span></span> | <span data-ttu-id="566d6-2444">否。</span><span class="sxs-lookup"><span data-stu-id="566d6-2444">No.</span></span> <span data-ttu-id="566d6-2445">預設值：00:01:40</span><span class="sxs-lookup"><span data-stu-id="566d6-2445">Default value: 00:01:40</span></span> |


#### <a name="example"></a><span data-ttu-id="566d6-2446">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-2446">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "HttpSourceToAzureBlob",
            "description": "Copy from an HTTP source tooan Azure blob",
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

<span data-ttu-id="566d6-2447">如需詳細資訊，請參閱 [HTTP 連接器](data-factory-http-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-2447">For more information, see [HTTP connector](data-factory-http-connector.md#copy-activity-properties) article.</span></span>

## <a name="odata"></a><span data-ttu-id="566d6-2448">OData</span><span class="sxs-lookup"><span data-stu-id="566d6-2448">OData</span></span>

### <a name="linked-service"></a><span data-ttu-id="566d6-2449">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-2449">Linked service</span></span>
<span data-ttu-id="566d6-2450">toodefine OData 連結的服務，設定 hello**類型**hello 的連結服務太**OData**，並指定下列屬性在 hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-2450">toodefine an OData linked service, set hello **type** of hello linked service too**OData**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="566d6-2451">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2451">Property</span></span> | <span data-ttu-id="566d6-2452">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2452">Description</span></span> | <span data-ttu-id="566d6-2453">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2453">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-2454">url</span><span class="sxs-lookup"><span data-stu-id="566d6-2454">url</span></span> |<span data-ttu-id="566d6-2455">Hello OData 服務的 Url。</span><span class="sxs-lookup"><span data-stu-id="566d6-2455">Url of hello OData service.</span></span> |<span data-ttu-id="566d6-2456">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2456">Yes</span></span> |
| <span data-ttu-id="566d6-2457">authenticationType</span><span class="sxs-lookup"><span data-stu-id="566d6-2457">authenticationType</span></span> |<span data-ttu-id="566d6-2458">Tooconnect toohello OData 來源使用的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="566d6-2458">Type of authentication used tooconnect toohello OData source.</span></span> <br/><br/> <span data-ttu-id="566d6-2459">若為雲端 OData，可能的值為 Anonymous、Basic 和 OAuth (請注意，Azure Data Factory 目前僅支援 Azure Active Directory 架構的 OAuth)。</span><span class="sxs-lookup"><span data-stu-id="566d6-2459">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="566d6-2460">若為內部部署 OData，可能的值為 Anonymous、Basic 和 Windows。</span><span class="sxs-lookup"><span data-stu-id="566d6-2460">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="566d6-2461">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2461">Yes</span></span> |
| <span data-ttu-id="566d6-2462">username</span><span class="sxs-lookup"><span data-stu-id="566d6-2462">username</span></span> |<span data-ttu-id="566d6-2463">如果您要使用 Basic 驗證，請指定使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-2463">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="566d6-2464">是 (只在您使用基本驗證時)</span><span class="sxs-lookup"><span data-stu-id="566d6-2464">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="566d6-2465">password</span><span class="sxs-lookup"><span data-stu-id="566d6-2465">password</span></span> |<span data-ttu-id="566d6-2466">指定 hello hello 使用者名稱所指定的使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="566d6-2466">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="566d6-2467">是 (只在您使用基本驗證時)</span><span class="sxs-lookup"><span data-stu-id="566d6-2467">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="566d6-2468">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="566d6-2468">authorizedCredential</span></span> |<span data-ttu-id="566d6-2469">如果您使用 OAuth 時，按一下**授權**按鈕 hello 資料 Factory 複製精靈或編輯器中，輸入您的認證，然後 hello 這個屬性的值將會自動產生。</span><span class="sxs-lookup"><span data-stu-id="566d6-2469">If you are using OAuth, click **Authorize** button in hello Data Factory Copy Wizard or Editor and enter your credential, then hello value of this property will be auto-generated.</span></span> |<span data-ttu-id="566d6-2470">是 (只有在您使用 OAuth 驗證時)</span><span class="sxs-lookup"><span data-stu-id="566d6-2470">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="566d6-2471">gatewayName</span><span class="sxs-lookup"><span data-stu-id="566d6-2471">gatewayName</span></span> |<span data-ttu-id="566d6-2472">Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello 在內部部署 OData 服務。</span><span class="sxs-lookup"><span data-stu-id="566d6-2472">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises OData service.</span></span> <span data-ttu-id="566d6-2473">只在要從內部部署 OData 來源複製資料時才指定。</span><span class="sxs-lookup"><span data-stu-id="566d6-2473">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="566d6-2474">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2474">No</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="566d6-2475">範例 - 使用基本驗證</span><span class="sxs-lookup"><span data-stu-id="566d6-2475">Example - Using Basic authentication</span></span>
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

#### <a name="example---using-anonymous-authentication"></a><span data-ttu-id="566d6-2476">範例 - 使用匿名驗證</span><span class="sxs-lookup"><span data-stu-id="566d6-2476">Example - Using Anonymous authentication</span></span>

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

#### <a name="example---using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="566d6-2477">範例 - 使用 Windows 驗證存取內部部署 OData 來源</span><span class="sxs-lookup"><span data-stu-id="566d6-2477">Example - Using Windows authentication accessing on-premises OData source</span></span>

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

#### <a name="example---using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="566d6-2478">範例 - 使用 OAuth 驗證存取雲端 OData 來源</span><span class="sxs-lookup"><span data-stu-id="566d6-2478">Example - Using OAuth authentication accessing cloud OData source</span></span>
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
            "authorizedCredential": "<auto generated by clicking hello Authorize button on UI>"
        }
    }
}
```

<span data-ttu-id="566d6-2479">如需詳細資訊，請參閱 [OData 連接器](data-factory-odata-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-2479">For more information, see [OData connector](data-factory-odata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="566d6-2480">Dataset</span><span class="sxs-lookup"><span data-stu-id="566d6-2480">Dataset</span></span>
<span data-ttu-id="566d6-2481">toodefine OData 資料集設定 hello**類型**hello 資料集太**ODataResource**，並指定下列屬性在 hello hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-2481">toodefine an OData dataset, set hello **type** of hello dataset too**ODataResource**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="566d6-2482">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2482">Property</span></span> | <span data-ttu-id="566d6-2483">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2483">Description</span></span> | <span data-ttu-id="566d6-2484">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2484">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-2485">路徑</span><span class="sxs-lookup"><span data-stu-id="566d6-2485">path</span></span> |<span data-ttu-id="566d6-2486">路徑 toohello OData 資源</span><span class="sxs-lookup"><span data-stu-id="566d6-2486">Path toohello OData resource</span></span> |<span data-ttu-id="566d6-2487">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2487">No</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-2488">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-2488">Example</span></span>

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

<span data-ttu-id="566d6-2489">如需詳細資訊，請參閱 [OData 連接器](data-factory-odata-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-2489">For more information, see [OData connector](data-factory-odata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="566d6-2490">複製活動中的關聯式來源</span><span class="sxs-lookup"><span data-stu-id="566d6-2490">Relational Source in Copy Activity</span></span>
<span data-ttu-id="566d6-2491">如果您從 OData 來源複製資料，設定 hello**來源類型**的 hello 複製活動太**RelationalSource**，並指定下列屬性在 hello**來源**區段：</span><span class="sxs-lookup"><span data-stu-id="566d6-2491">If you are copying data from an OData source, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="566d6-2492">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2492">Property</span></span> | <span data-ttu-id="566d6-2493">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2493">Description</span></span> | <span data-ttu-id="566d6-2494">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-2494">Example</span></span> | <span data-ttu-id="566d6-2495">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2495">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-2496">query</span><span class="sxs-lookup"><span data-stu-id="566d6-2496">query</span></span> |<span data-ttu-id="566d6-2497">使用自訂查詢 tooread hello 的資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-2497">Use hello custom query tooread data.</span></span> |<span data-ttu-id="566d6-2498">「?$select=Name, Description&$top=5」</span><span class="sxs-lookup"><span data-stu-id="566d6-2498">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="566d6-2499">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2499">No</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-2500">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-2500">Example</span></span>

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

<span data-ttu-id="566d6-2501">如需詳細資訊，請參閱 [OData 連接器](data-factory-odata-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-2501">For more information, see [OData connector](data-factory-odata-connector.md#copy-activity-properties) article.</span></span>


## <a name="odbc"></a><span data-ttu-id="566d6-2502">ODBC</span><span class="sxs-lookup"><span data-stu-id="566d6-2502">ODBC</span></span>


### <a name="linked-service"></a><span data-ttu-id="566d6-2503">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-2503">Linked service</span></span>
<span data-ttu-id="566d6-2504">toodefine ODBC 連結服務，設定 hello**類型**hello 的連結服務太**OnPremisesOdbc**，並指定下列屬性在 hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-2504">toodefine an ODBC linked service, set hello **type** of hello linked service too**OnPremisesOdbc**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="566d6-2505">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2505">Property</span></span> | <span data-ttu-id="566d6-2506">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2506">Description</span></span> | <span data-ttu-id="566d6-2507">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2507">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-2508">connectionString</span><span class="sxs-lookup"><span data-stu-id="566d6-2508">connectionString</span></span> |<span data-ttu-id="566d6-2509">hello 非存取認證部分 hello 連接字串和選擇性的加密認證。</span><span class="sxs-lookup"><span data-stu-id="566d6-2509">hello non-access credential portion of hello connection string and an optional encrypted credential.</span></span> <span data-ttu-id="566d6-2510">請參閱下列各節的 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="566d6-2510">See examples in hello following sections.</span></span> |<span data-ttu-id="566d6-2511">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2511">Yes</span></span> |
| <span data-ttu-id="566d6-2512">認證</span><span class="sxs-lookup"><span data-stu-id="566d6-2512">credential</span></span> |<span data-ttu-id="566d6-2513">hello 存取認證的 hello 驅動程式特有的屬性值的格式指定的連接字串部分。</span><span class="sxs-lookup"><span data-stu-id="566d6-2513">hello access credential portion of hello connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="566d6-2514">範例：“Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”。</span><span class="sxs-lookup"><span data-stu-id="566d6-2514">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="566d6-2515">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2515">No</span></span> |
| <span data-ttu-id="566d6-2516">authenticationType</span><span class="sxs-lookup"><span data-stu-id="566d6-2516">authenticationType</span></span> |<span data-ttu-id="566d6-2517">Tooconnect toohello ODBC 資料存放區使用的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="566d6-2517">Type of authentication used tooconnect toohello ODBC data store.</span></span> <span data-ttu-id="566d6-2518">可能的值為：Anonymous 和 Basic。</span><span class="sxs-lookup"><span data-stu-id="566d6-2518">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="566d6-2519">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2519">Yes</span></span> |
| <span data-ttu-id="566d6-2520">username</span><span class="sxs-lookup"><span data-stu-id="566d6-2520">username</span></span> |<span data-ttu-id="566d6-2521">如果您要使用 Basic 驗證，請指定使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-2521">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="566d6-2522">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2522">No</span></span> |
| <span data-ttu-id="566d6-2523">password</span><span class="sxs-lookup"><span data-stu-id="566d6-2523">password</span></span> |<span data-ttu-id="566d6-2524">指定 hello hello 使用者名稱所指定的使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="566d6-2524">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="566d6-2525">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2525">No</span></span> |
| <span data-ttu-id="566d6-2526">gatewayName</span><span class="sxs-lookup"><span data-stu-id="566d6-2526">gatewayName</span></span> |<span data-ttu-id="566d6-2527">Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello ODBC 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="566d6-2527">Name of hello gateway that hello Data Factory service should use tooconnect toohello ODBC data store.</span></span> |<span data-ttu-id="566d6-2528">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2528">Yes</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="566d6-2529">範例 - 使用基本驗證</span><span class="sxs-lookup"><span data-stu-id="566d6-2529">Example - Using Basic authentication</span></span>

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
#### <a name="example---using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="566d6-2530">範例 - 使用基本驗證搭配加密認證</span><span class="sxs-lookup"><span data-stu-id="566d6-2530">Example - Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="566d6-2531">您可以加密使用 hello hello 認證[新增 AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) （1.0 版本的 Azure PowerShell） 指令程式或[New-azuredatafactoryencryptvalue](https://msdn.microsoft.com/library/dn834940.aspx) （0.9 或更早版本的 helloAzure PowerShell)。</span><span class="sxs-lookup"><span data-stu-id="566d6-2531">You can encrypt hello credentials using hello [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of hello Azure PowerShell).</span></span>  

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

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="566d6-2532">範例：使用匿名驗證</span><span class="sxs-lookup"><span data-stu-id="566d6-2532">Example: Using Anonymous authentication</span></span>

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

<span data-ttu-id="566d6-2533">如需詳細資訊，請參閱 [ODBC 連接器](data-factory-odbc-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-2533">For more information, see [ODBC connector](data-factory-odbc-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="566d6-2534">Dataset</span><span class="sxs-lookup"><span data-stu-id="566d6-2534">Dataset</span></span>
<span data-ttu-id="566d6-2535">toodefine ODBC 資料集設定 hello**類型**hello 資料集太**RelationalTable**，並指定下列屬性在 hello hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-2535">toodefine an ODBC dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="566d6-2536">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2536">Property</span></span> | <span data-ttu-id="566d6-2537">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2537">Description</span></span> | <span data-ttu-id="566d6-2538">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2538">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-2539">tableName</span><span class="sxs-lookup"><span data-stu-id="566d6-2539">tableName</span></span> |<span data-ttu-id="566d6-2540">Hello ODBC 資料存放區中的 hello 資料表的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-2540">Name of hello table in hello ODBC data store.</span></span> |<span data-ttu-id="566d6-2541">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2541">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="566d6-2542">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-2542">Example</span></span>

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

<span data-ttu-id="566d6-2543">如需詳細資訊，請參閱 [ODBC 連接器](data-factory-odbc-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-2543">For more information, see [ODBC connector](data-factory-odbc-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="566d6-2544">複製活動中的關聯式來源</span><span class="sxs-lookup"><span data-stu-id="566d6-2544">Relational Source in Copy Activity</span></span>
<span data-ttu-id="566d6-2545">如果您從 ODBC 資料存放區複製資料，設定 hello**來源類型**的 hello 複製活動太**RelationalSource**，並指定下列屬性在 hello**來源**區段：</span><span class="sxs-lookup"><span data-stu-id="566d6-2545">If you are copying data from an ODBC data store, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="566d6-2546">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2546">Property</span></span> | <span data-ttu-id="566d6-2547">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2547">Description</span></span> | <span data-ttu-id="566d6-2548">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-2548">Allowed values</span></span> | <span data-ttu-id="566d6-2549">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2549">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-2550">query</span><span class="sxs-lookup"><span data-stu-id="566d6-2550">query</span></span> |<span data-ttu-id="566d6-2551">使用自訂查詢 tooread hello 的資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-2551">Use hello custom query tooread data.</span></span> |<span data-ttu-id="566d6-2552">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="566d6-2552">SQL query string.</span></span> <span data-ttu-id="566d6-2553">例如： `select * from MyTable`。</span><span class="sxs-lookup"><span data-stu-id="566d6-2553">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="566d6-2554">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2554">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-2555">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-2555">Example</span></span>

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

<span data-ttu-id="566d6-2556">如需詳細資訊，請參閱 [ODBC 連接器](data-factory-odbc-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-2556">For more information, see [ODBC connector](data-factory-odbc-connector.md#copy-activity-properties) article.</span></span>

## <a name="salesforce"></a><span data-ttu-id="566d6-2557">Salesforce</span><span class="sxs-lookup"><span data-stu-id="566d6-2557">Salesforce</span></span>


### <a name="linked-service"></a><span data-ttu-id="566d6-2558">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-2558">Linked service</span></span>
<span data-ttu-id="566d6-2559">toodefine Salesforce 連結服務，設定 hello**類型**hello 的連結服務太**Salesforce**，並指定下列屬性在 hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-2559">toodefine a Salesforce linked service, set hello **type** of hello linked service too**Salesforce**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="566d6-2560">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2560">Property</span></span> | <span data-ttu-id="566d6-2561">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2561">Description</span></span> | <span data-ttu-id="566d6-2562">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2562">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-2563">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="566d6-2563">environmentUrl</span></span> | <span data-ttu-id="566d6-2564">指定 hello URL 的 Salesforce 執行個體。</span><span class="sxs-lookup"><span data-stu-id="566d6-2564">Specify hello URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="566d6-2565">- 預設值為 " https://login.salesforce.com "。</span><span class="sxs-lookup"><span data-stu-id="566d6-2565">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="566d6-2566">-從沙箱，toocopy 資料指定"https://test.salesforce.com"。</span><span class="sxs-lookup"><span data-stu-id="566d6-2566">- toocopy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="566d6-2567">-toocopy 資料從自訂網域，指定，例如，"https://[domain].my.salesforce.com"。</span><span class="sxs-lookup"><span data-stu-id="566d6-2567">- toocopy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="566d6-2568">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2568">No</span></span> |
| <span data-ttu-id="566d6-2569">username</span><span class="sxs-lookup"><span data-stu-id="566d6-2569">username</span></span> |<span data-ttu-id="566d6-2570">指定 hello 使用者帳戶的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-2570">Specify a user name for hello user account.</span></span> |<span data-ttu-id="566d6-2571">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2571">Yes</span></span> |
| <span data-ttu-id="566d6-2572">password</span><span class="sxs-lookup"><span data-stu-id="566d6-2572">password</span></span> |<span data-ttu-id="566d6-2573">指定 hello 使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="566d6-2573">Specify a password for hello user account.</span></span> |<span data-ttu-id="566d6-2574">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2574">Yes</span></span> |
| <span data-ttu-id="566d6-2575">securityToken</span><span class="sxs-lookup"><span data-stu-id="566d6-2575">securityToken</span></span> |<span data-ttu-id="566d6-2576">指定 hello 使用者帳戶的安全性權杖。</span><span class="sxs-lookup"><span data-stu-id="566d6-2576">Specify a security token for hello user account.</span></span> <span data-ttu-id="566d6-2577">請參閱[取得安全性權杖](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm)如需有關指示 tooreset 取得安全性權杖。</span><span class="sxs-lookup"><span data-stu-id="566d6-2577">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how tooreset/get a security token.</span></span> <span data-ttu-id="566d6-2578">一般情況下，請參閱關於安全性權杖的 toolearn[安全性和 hello API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm)。</span><span class="sxs-lookup"><span data-stu-id="566d6-2578">toolearn about security tokens in general, see [Security and hello API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="566d6-2579">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2579">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-2580">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-2580">Example</span></span>

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

<span data-ttu-id="566d6-2581">如需詳細資訊，請參閱 [Salesforce 連接器](data-factory-salesforce-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-2581">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="566d6-2582">Dataset</span><span class="sxs-lookup"><span data-stu-id="566d6-2582">Dataset</span></span>
<span data-ttu-id="566d6-2583">toodefine Salesforce 資料集設定 hello**類型**hello 資料集太**RelationalTable**，並指定下列屬性在 hello hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-2583">toodefine a Salesforce dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="566d6-2584">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2584">Property</span></span> | <span data-ttu-id="566d6-2585">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2585">Description</span></span> | <span data-ttu-id="566d6-2586">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2586">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-2587">tableName</span><span class="sxs-lookup"><span data-stu-id="566d6-2587">tableName</span></span> |<span data-ttu-id="566d6-2588">在 Salesforce 中的 hello 資料表的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-2588">Name of hello table in Salesforce.</span></span> |<span data-ttu-id="566d6-2589">否 (如果已指定 **RelationalSource** 的 **query**)</span><span class="sxs-lookup"><span data-stu-id="566d6-2589">No (if a **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-2590">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-2590">Example</span></span>

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

<span data-ttu-id="566d6-2591">如需詳細資訊，請參閱 [Salesforce 連接器](data-factory-salesforce-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-2591">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="566d6-2592">複製活動中的關聯式來源</span><span class="sxs-lookup"><span data-stu-id="566d6-2592">Relational Source in Copy Activity</span></span>
<span data-ttu-id="566d6-2593">如果您從 Salesforce 複製資料，設定 hello**來源類型**的 hello 複製活動太**RelationalSource**，並指定下列屬性在 hello**來源**區段：</span><span class="sxs-lookup"><span data-stu-id="566d6-2593">If you are copying data from Salesforce, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="566d6-2594">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2594">Property</span></span> | <span data-ttu-id="566d6-2595">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2595">Description</span></span> | <span data-ttu-id="566d6-2596">允許的值</span><span class="sxs-lookup"><span data-stu-id="566d6-2596">Allowed values</span></span> | <span data-ttu-id="566d6-2597">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2597">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="566d6-2598">query</span><span class="sxs-lookup"><span data-stu-id="566d6-2598">query</span></span> |<span data-ttu-id="566d6-2599">使用自訂查詢 tooread hello 的資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-2599">Use hello custom query tooread data.</span></span> |<span data-ttu-id="566d6-2600">SQL-92 查詢或 [Salesforce 物件查詢語言 (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) 查詢。</span><span class="sxs-lookup"><span data-stu-id="566d6-2600">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="566d6-2601">例如：`select * from MyTable__c`。</span><span class="sxs-lookup"><span data-stu-id="566d6-2601">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="566d6-2602">否 (如果 hello **tableName**的 hello**資料集**指定)</span><span class="sxs-lookup"><span data-stu-id="566d6-2602">No (if hello **tableName** of hello **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-2603">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-2603">Example</span></span>  



```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce tooan Azure blob",
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
> <span data-ttu-id="566d6-2604">hello"__c"hello API 名稱部分所需的任何自訂的物件。</span><span class="sxs-lookup"><span data-stu-id="566d6-2604">hello "__c" part of hello API Name is needed for any custom object.</span></span>

<span data-ttu-id="566d6-2605">如需詳細資訊，請參閱 [Salesforce 連接器](data-factory-salesforce-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-2605">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#copy-activity-properties) article.</span></span> 

## <a name="web-data"></a><span data-ttu-id="566d6-2606">Web 資料</span><span class="sxs-lookup"><span data-stu-id="566d6-2606">Web Data</span></span> 

### <a name="linked-service"></a><span data-ttu-id="566d6-2607">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-2607">Linked service</span></span>
<span data-ttu-id="566d6-2608">toodefine Web 連結服務，設定 hello**類型**hello 的連結服務太**Web**，並指定下列屬性在 hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-2608">toodefine a Web linked service, set hello **type** of hello linked service too**Web**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="566d6-2609">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2609">Property</span></span> | <span data-ttu-id="566d6-2610">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2610">Description</span></span> | <span data-ttu-id="566d6-2611">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2611">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-2612">Url</span><span class="sxs-lookup"><span data-stu-id="566d6-2612">Url</span></span> |<span data-ttu-id="566d6-2613">URL toohello Web 來源</span><span class="sxs-lookup"><span data-stu-id="566d6-2613">URL toohello Web source</span></span> |<span data-ttu-id="566d6-2614">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2614">Yes</span></span> |
| <span data-ttu-id="566d6-2615">authenticationType</span><span class="sxs-lookup"><span data-stu-id="566d6-2615">authenticationType</span></span> |<span data-ttu-id="566d6-2616">匿名。</span><span class="sxs-lookup"><span data-stu-id="566d6-2616">Anonymous.</span></span> |<span data-ttu-id="566d6-2617">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2617">Yes</span></span> |
 

#### <a name="example"></a><span data-ttu-id="566d6-2618">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-2618">Example</span></span>


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

<span data-ttu-id="566d6-2619">如需詳細資訊，請參閱 [Web 資料表連接器](data-factory-web-table-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-2619">For more information, see [Web Table connector](data-factory-web-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="566d6-2620">Dataset</span><span class="sxs-lookup"><span data-stu-id="566d6-2620">Dataset</span></span>
<span data-ttu-id="566d6-2621">toodefine Web 資料集設定 hello**類型**hello 資料集太**WebTable**，並指定下列屬性在 hello hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-2621">toodefine a Web dataset, set hello **type** of hello dataset too**WebTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="566d6-2622">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2622">Property</span></span> | <span data-ttu-id="566d6-2623">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2623">Description</span></span> | <span data-ttu-id="566d6-2624">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2624">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="566d6-2625">類型</span><span class="sxs-lookup"><span data-stu-id="566d6-2625">type</span></span> |<span data-ttu-id="566d6-2626">hello 資料集的類型。</span><span class="sxs-lookup"><span data-stu-id="566d6-2626">type of hello dataset.</span></span> <span data-ttu-id="566d6-2627">必須設定得**WebTable**</span><span class="sxs-lookup"><span data-stu-id="566d6-2627">must be set too**WebTable**</span></span> |<span data-ttu-id="566d6-2628">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2628">Yes</span></span> |
| <span data-ttu-id="566d6-2629">路徑</span><span class="sxs-lookup"><span data-stu-id="566d6-2629">path</span></span> |<span data-ttu-id="566d6-2630">相對 URL toohello 資源包含 hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="566d6-2630">A relative URL toohello resource that contains hello table.</span></span> |<span data-ttu-id="566d6-2631">否。</span><span class="sxs-lookup"><span data-stu-id="566d6-2631">No.</span></span> <span data-ttu-id="566d6-2632">若未指定路徑，則會使用連結的 hello 服務定義中指定的唯一 hello URL。</span><span class="sxs-lookup"><span data-stu-id="566d6-2632">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> |
| <span data-ttu-id="566d6-2633">index</span><span class="sxs-lookup"><span data-stu-id="566d6-2633">index</span></span> |<span data-ttu-id="566d6-2634">hello hello 資源中的 hello 資料表的索引。</span><span class="sxs-lookup"><span data-stu-id="566d6-2634">hello index of hello table in hello resource.</span></span> <span data-ttu-id="566d6-2635">請參閱[Get 索引的資料表中的 HTML 網頁的](#get-index-of-a-table-in-an-html-page)> 一節步驟 toogetting 索引的 HTML 網頁中的資料表。</span><span class="sxs-lookup"><span data-stu-id="566d6-2635">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps toogetting index of a table in an HTML page.</span></span> |<span data-ttu-id="566d6-2636">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2636">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="566d6-2637">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-2637">Example</span></span>

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

<span data-ttu-id="566d6-2638">如需詳細資訊，請參閱 [Web 資料表連接器](data-factory-web-table-connector.md#dataset-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-2638">For more information, see [Web Table connector](data-factory-web-table-connector.md#dataset-properties) article.</span></span> 

### <a name="web-source-in-copy-activity"></a><span data-ttu-id="566d6-2639">複製活動中的 Web 來源</span><span class="sxs-lookup"><span data-stu-id="566d6-2639">Web Source in Copy Activity</span></span>
<span data-ttu-id="566d6-2640">如果您從 web 資料表複製資料，設定 hello**來源類型**的 hello 複製活動太**WebSource**。</span><span class="sxs-lookup"><span data-stu-id="566d6-2640">If you are copying data from a web table, set hello **source type** of hello copy activity too**WebSource**.</span></span> <span data-ttu-id="566d6-2641">目前，當複製活動中的 hello 來源屬於型別**WebSource**，支援任何其他屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-2641">Currently, when hello source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>

#### <a name="example"></a><span data-ttu-id="566d6-2642">範例</span><span class="sxs-lookup"><span data-stu-id="566d6-2642">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "WebTableToAzureBlob",
            "description": "Copy from a Web table tooan Azure blob",
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

<span data-ttu-id="566d6-2643">如需詳細資訊，請參閱 [Web 資料表連接器](data-factory-web-table-connector.md#copy-activity-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-2643">For more information, see [Web Table connector](data-factory-web-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="compute-environments"></a><span data-ttu-id="566d6-2644">計算環境</span><span class="sxs-lookup"><span data-stu-id="566d6-2644">COMPUTE ENVIRONMENTS</span></span>
<span data-ttu-id="566d6-2645">hello 下表列出支援的 Data Factory 和 hello 轉換活動可以在其上執行的 hello 運算環境。</span><span class="sxs-lookup"><span data-stu-id="566d6-2645">hello following table lists hello compute environments supported by Data Factory and hello transformation activities that can run on them.</span></span> <span data-ttu-id="566d6-2646">按一下 hello 連結 hello 計算您所感興趣 toosee hello JSON 結構描述的連結的服務 toolink 它 tooa 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="566d6-2646">Click hello link for hello compute you are interested in toosee hello JSON schemas for linked service toolink it tooa data factory.</span></span> 

| <span data-ttu-id="566d6-2647">計算環境</span><span class="sxs-lookup"><span data-stu-id="566d6-2647">Compute environment</span></span> | <span data-ttu-id="566d6-2648">活動</span><span class="sxs-lookup"><span data-stu-id="566d6-2648">Activities</span></span> |
| --- | --- |
| <span data-ttu-id="566d6-2649">[隨選 HDInsight 叢集](#on-demand-azure-hdinsight-cluster)或[您自己的 HDInsight 叢集](#existing-azure-hdinsight-cluster)</span><span class="sxs-lookup"><span data-stu-id="566d6-2649">[On-demand HDInsight cluster](#on-demand-azure-hdinsight-cluster) or [your own HDInsight cluster](#existing-azure-hdinsight-cluster)</span></span> |<span data-ttu-id="566d6-2650">[.NET 自訂活動](#net-custom-activity)、[Hive 活動](#hdinsight-hive-activity)、[Pig 活動](#hdinsight-pig-acitivity、[MapReduce 活動](#hdinsight-mapreduce-activity)、[Hadoop 串流活動](#hdinsight-streaming-activityd)、[Spark 活動](#hdinsight-spark-activity)</span><span class="sxs-lookup"><span data-stu-id="566d6-2650">[.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity)</span></span> |
| [<span data-ttu-id="566d6-2651">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="566d6-2651">Azure Batch</span></span>](#azure-batch) |[<span data-ttu-id="566d6-2652">.NET 自訂活動</span><span class="sxs-lookup"><span data-stu-id="566d6-2652">.NET custom activity</span></span>](#net-custom-activity) |
| [<span data-ttu-id="566d6-2653">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="566d6-2653">Azure Machine Learning</span></span>](#azure-machine-learning) | <span data-ttu-id="566d6-2654">[Machine Learning 批次執行活動](#machine-learning-batch-execution-activity)、[Machine Learning 更新資源活動](#machine-learning-update-resource-activity)</span><span class="sxs-lookup"><span data-stu-id="566d6-2654">[Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity)</span></span> |
| [<span data-ttu-id="566d6-2655">Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="566d6-2655">Azure Data Lake Analytics</span></span>](#azure-data-lake-analytics) |[<span data-ttu-id="566d6-2656">Data Lake Analytics U-SQL</span><span class="sxs-lookup"><span data-stu-id="566d6-2656">Data Lake Analytics U-SQL</span></span>](#data-lake-analytics-u-sql-activity) |
| <span data-ttu-id="566d6-2657">[Azure SQL Database](#azure-sql-database-1)、[Azure SQL 資料倉儲](#azure-sql-data-warehouse-1)、[SQL Server](#sql-server-1)</span><span class="sxs-lookup"><span data-stu-id="566d6-2657">[Azure SQL Database](#azure-sql-database-1), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1)</span></span> |[<span data-ttu-id="566d6-2658">預存程序</span><span class="sxs-lookup"><span data-stu-id="566d6-2658">Stored Procedure</span></span>](#stored-procedure-activity) |

## <a name="on-demand-azure-hdinsight-cluster"></a><span data-ttu-id="566d6-2659">隨選 Azure HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="566d6-2659">On-demand Azure HDInsight cluster</span></span>
<span data-ttu-id="566d6-2660">hello Azure Data Factory 服務會自動建立 Windows/Linux 為基礎-隨選 HDInsight 叢集 tooprocess 資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-2660">hello Azure Data Factory service can automatically create a Windows/Linux-based on-demand HDInsight cluster tooprocess data.</span></span> <span data-ttu-id="566d6-2661">hello 叢集建立在 hello 與 hello 叢集與 hello 儲存體帳戶 （hello JSON 中的 linkedServiceName 屬性） 相同的區域相關聯。</span><span class="sxs-lookup"><span data-stu-id="566d6-2661">hello cluster is created in hello same region as hello storage account (linkedServiceName property in hello JSON) associated with hello cluster.</span></span> <span data-ttu-id="566d6-2662">您可以執行下列轉換活動上這項連結服務的 hello: [.NET 自訂活動](#net-custom-activity)， [Hive 活動](#hdinsight-hive-activity)，[Pig 活動] (#hdinsight pig-活動， [MapReduce 活動](#hdinsight-mapreduce-activity)， [Hadoop 串流活動](#hdinsight-streaming-activityd)，[二手活動](#hdinsight-spark-activity)。</span><span class="sxs-lookup"><span data-stu-id="566d6-2662">You can run hello following transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="566d6-2663">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-2663">Linked service</span></span> 
<span data-ttu-id="566d6-2664">下表中的 hello 提供 hello 屬性視 HDInsight 連結服務的 hello Azure JSON 定義中所使用的說明。</span><span class="sxs-lookup"><span data-stu-id="566d6-2664">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an on-demand HDInsight linked service.</span></span>

| <span data-ttu-id="566d6-2665">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2665">Property</span></span> | <span data-ttu-id="566d6-2666">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2666">Description</span></span> | <span data-ttu-id="566d6-2667">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2667">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-2668">類型</span><span class="sxs-lookup"><span data-stu-id="566d6-2668">type</span></span> |<span data-ttu-id="566d6-2669">hello 類型屬性應該設定太**HDInsightOnDemand**。</span><span class="sxs-lookup"><span data-stu-id="566d6-2669">hello type property should be set too**HDInsightOnDemand**.</span></span> |<span data-ttu-id="566d6-2670">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2670">Yes</span></span> |
| <span data-ttu-id="566d6-2671">clusterSize</span><span class="sxs-lookup"><span data-stu-id="566d6-2671">clusterSize</span></span> |<span data-ttu-id="566d6-2672">背景工作/資料 hello 叢集中的節點數目。</span><span class="sxs-lookup"><span data-stu-id="566d6-2672">Number of worker/data nodes in hello cluster.</span></span> <span data-ttu-id="566d6-2673">以及您為此屬性指定的背景工作角色節點的 hello 數目的 2 個前端節點建立 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="566d6-2673">hello HDInsight cluster is created with 2 head nodes along with hello number of worker nodes you specify for this property.</span></span> <span data-ttu-id="566d6-2674">hello 節點有大小有 4 個核心，因此 4 的背景工作節點叢集會採用 24 個核心的 Standard_D3 (4\*4 = 16 個核心的背景工作節點，再加上 2\*4 = 8 個核心的前端節點)。</span><span class="sxs-lookup"><span data-stu-id="566d6-2674">hello nodes are of size Standard_D3 that has 4 cores, so a 4 worker node cluster takes 24 cores (4\*4 = 16 cores for worker nodes, plus 2\*4 = 8 cores for head nodes).</span></span> <span data-ttu-id="566d6-2675">請參閱[HDInsight 叢集建立 Linux Hadoop](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) hello Standard_D3 層的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-2675">See [Create Linux-based Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) for details about hello Standard_D3 tier.</span></span> |<span data-ttu-id="566d6-2676">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2676">Yes</span></span> |
| <span data-ttu-id="566d6-2677">timetolive</span><span class="sxs-lookup"><span data-stu-id="566d6-2677">timetolive</span></span> |<span data-ttu-id="566d6-2678">hello 允許 hello 隨選 HDInsight 叢集的閒置時間。</span><span class="sxs-lookup"><span data-stu-id="566d6-2678">hello allowed idle time for hello on-demand HDInsight cluster.</span></span> <span data-ttu-id="566d6-2679">指定多久 hello 隨選 HDInsight 叢集會保持運作如果 hello 叢集中沒有其他作用中的工作執行的活動完成後。</span><span class="sxs-lookup"><span data-stu-id="566d6-2679">Specifies how long hello on-demand HDInsight cluster stays alive after completion of an activity run if there are no other active jobs in hello cluster.</span></span><br/><br/><span data-ttu-id="566d6-2680">例如，如果在 6 分鐘和 timetolive 執行的活動是設定 too5 分鐘，hello 叢集會保持運作 5 分鐘之後 hello 6 分鐘處理 hello 活動執行。</span><span class="sxs-lookup"><span data-stu-id="566d6-2680">For example, if an activity run takes 6 minutes and timetolive is set too5 minutes, hello cluster stays alive for 5 minutes after hello 6 minutes of processing hello activity run.</span></span> <span data-ttu-id="566d6-2681">如果另一個執行的活動與 hello 6 分鐘視窗執行時，處理 hello 相同叢集中。</span><span class="sxs-lookup"><span data-stu-id="566d6-2681">If another activity run is executed with hello 6 minutes window, it is processed by hello same cluster.</span></span><br/><br/><span data-ttu-id="566d6-2682">建立隨選 HDInsight 叢集是昂貴的作業 （可能需要一些時間），因此使用這項設定的 data factory 所需的 tooimprove 效能重複使用隨選 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="566d6-2682">Creating an on-demand HDInsight cluster is an expensive operation (could take a while), so use this setting as needed tooimprove performance of a data factory by reusing an on-demand HDInsight cluster.</span></span><br/><br/><span data-ttu-id="566d6-2683">如果您設定 timetolive 值 too0，只要執行的 hello 活動處理，會刪除 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="566d6-2683">If you set timetolive value too0, hello cluster is deleted as soon as hello activity run in processed.</span></span> <span data-ttu-id="566d6-2684">在 hello 相反地，如果您設定較高的值，hello 叢集可能保持閒置不必要地產生高成本。</span><span class="sxs-lookup"><span data-stu-id="566d6-2684">On hello other hand, if you set a high value, hello cluster may stay idle unnecessarily resulting in high costs.</span></span> <span data-ttu-id="566d6-2685">因此，很重要，您會設定 hello 適當的值，根據您的需求。</span><span class="sxs-lookup"><span data-stu-id="566d6-2685">Therefore, it is important that you set hello appropriate value based on your needs.</span></span><br/><br/><span data-ttu-id="566d6-2686">多個管線可以共用 hello hello 隨選 HDInsight 叢集的同一個執行個體，如果適當地設定 hello timetolive 屬性值</span><span class="sxs-lookup"><span data-stu-id="566d6-2686">Multiple pipelines can share hello same instance of hello on-demand HDInsight cluster if hello timetolive property value is appropriately set</span></span> |<span data-ttu-id="566d6-2687">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2687">Yes</span></span> |
| <span data-ttu-id="566d6-2688">版本</span><span class="sxs-lookup"><span data-stu-id="566d6-2688">version</span></span> |<span data-ttu-id="566d6-2689">Hello HDInsight 叢集的版本。</span><span class="sxs-lookup"><span data-stu-id="566d6-2689">Version of hello HDInsight cluster.</span></span> <span data-ttu-id="566d6-2690">如需詳細資訊，請參閱 [Azure Data Factory 中支援的 HDInsight 版本](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory)。</span><span class="sxs-lookup"><span data-stu-id="566d6-2690">For details, see [supported HDInsight versions in Azure Data Factory](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> |<span data-ttu-id="566d6-2691">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2691">No</span></span> |
| <span data-ttu-id="566d6-2692">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="566d6-2692">linkedServiceName</span></span> |<span data-ttu-id="566d6-2693">Azure 儲存體連結服務 toobe hello 視叢集使用的儲存及處理資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-2693">Azure Storage linked service toobe used by hello on-demand cluster for storing and processing data.</span></span> <p><span data-ttu-id="566d6-2694">目前，您無法建立使用 Azure 資料湖存放區為 hello 存放裝置的隨 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="566d6-2694">Currently, you cannot create an on-demand HDInsight cluster that uses an Azure Data Lake Store as hello storage.</span></span> <span data-ttu-id="566d6-2695">如果您想要從 HDInsight 處理 Azure 資料湖存放區中的 toostore hello 結果資料，請使用 hello Azure Blob 儲存體 toohello Azure Data Lake Store 複製活動 toocopy hello 資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-2695">If you want toostore hello result data from HDInsight processing in an Azure Data Lake Store, use a Copy Activity toocopy hello data from hello Azure Blob Storage toohello Azure Data Lake Store.</span></span></p>  | <span data-ttu-id="566d6-2696">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2696">Yes</span></span> |
| <span data-ttu-id="566d6-2697">additionalLinkedServiceNames</span><span class="sxs-lookup"><span data-stu-id="566d6-2697">additionalLinkedServiceNames</span></span> |<span data-ttu-id="566d6-2698">指定額外的儲存體帳戶的 hello HDInsight 連結服務，以便 hello Data Factory 服務可以代表您註冊它們。</span><span class="sxs-lookup"><span data-stu-id="566d6-2698">Specifies additional storage accounts for hello HDInsight linked service so that hello Data Factory service can register them on your behalf.</span></span> |<span data-ttu-id="566d6-2699">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2699">No</span></span> |
| <span data-ttu-id="566d6-2700">osType</span><span class="sxs-lookup"><span data-stu-id="566d6-2700">osType</span></span> |<span data-ttu-id="566d6-2701">作業系統的類型。</span><span class="sxs-lookup"><span data-stu-id="566d6-2701">Type of operating system.</span></span> <span data-ttu-id="566d6-2702">允許的值為：Windows (預設值) 和 linux</span><span class="sxs-lookup"><span data-stu-id="566d6-2702">Allowed values are: Windows (default) and Linux</span></span> |<span data-ttu-id="566d6-2703">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2703">No</span></span> |
| <span data-ttu-id="566d6-2704">hcatalogLinkedServiceName</span><span class="sxs-lookup"><span data-stu-id="566d6-2704">hcatalogLinkedServiceName</span></span> |<span data-ttu-id="566d6-2705">該點 toohello HCatalog 資料庫服務的 Azure SQL 連結的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-2705">hello name of Azure SQL linked service that point toohello HCatalog database.</span></span> <span data-ttu-id="566d6-2706">hello 隨選 HDInsight 叢集會建立使用 hello Azure SQL database 當做 hello 中繼存放區。</span><span class="sxs-lookup"><span data-stu-id="566d6-2706">hello on-demand HDInsight cluster is created by using hello Azure SQL database as hello metastore.</span></span> |<span data-ttu-id="566d6-2707">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2707">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="566d6-2708">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="566d6-2708">JSON example</span></span>
<span data-ttu-id="566d6-2709">下列 JSON hello 定義以 Linux 為基礎的隨選 HDInsight 連結服務。</span><span class="sxs-lookup"><span data-stu-id="566d6-2709">hello following JSON defines a Linux-based on-demand HDInsight linked service.</span></span> <span data-ttu-id="566d6-2710">hello Data Factory 服務會自動建立**linux**時處理資料配量的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="566d6-2710">hello Data Factory service automatically creates a **Linux-based** HDInsight cluster when processing a data slice.</span></span> 

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

<span data-ttu-id="566d6-2711">如需詳細資訊，請參閱[計算連結服務](data-factory-compute-linked-services.md)一文。</span><span class="sxs-lookup"><span data-stu-id="566d6-2711">For more information, see [Compute linked services](data-factory-compute-linked-services.md) article.</span></span> 

## <a name="existing-azure-hdinsight-cluster"></a><span data-ttu-id="566d6-2712">現有的 Azure HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="566d6-2712">Existing Azure HDInsight cluster</span></span>
<span data-ttu-id="566d6-2713">您可以使用 Data Factory 建立 Azure HDInsight 連結服務 tooregister HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="566d6-2713">You can create an Azure HDInsight linked service tooregister your own HDInsight cluster with Data Factory.</span></span> <span data-ttu-id="566d6-2714">您可以執行資料轉換活動遵循這項連結服務的 hello: [.NET 自訂活動](#net-custom-activity)， [Hive 活動](#hdinsight-hive-activity)，[Pig 活動] (#hdinsight pig-活動， [MapReduce活動](#hdinsight-mapreduce-activity)， [Hadoop 串流活動](#hdinsight-streaming-activityd)，[二手活動](#hdinsight-spark-activity)。</span><span class="sxs-lookup"><span data-stu-id="566d6-2714">You can run hello following data transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="566d6-2715">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-2715">Linked service</span></span>
<span data-ttu-id="566d6-2716">hello 下表提供使用 Azure HDInsight 連結服務的 hello Azure JSON 定義中的 hello 屬性的說明。</span><span class="sxs-lookup"><span data-stu-id="566d6-2716">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an Azure HDInsight linked service.</span></span>

| <span data-ttu-id="566d6-2717">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2717">Property</span></span> | <span data-ttu-id="566d6-2718">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2718">Description</span></span> | <span data-ttu-id="566d6-2719">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2719">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-2720">類型</span><span class="sxs-lookup"><span data-stu-id="566d6-2720">type</span></span> |<span data-ttu-id="566d6-2721">hello 類型屬性應該設定太**HDInsight**。</span><span class="sxs-lookup"><span data-stu-id="566d6-2721">hello type property should be set too**HDInsight**.</span></span> |<span data-ttu-id="566d6-2722">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2722">Yes</span></span> |
| <span data-ttu-id="566d6-2723">clusterUri</span><span class="sxs-lookup"><span data-stu-id="566d6-2723">clusterUri</span></span> |<span data-ttu-id="566d6-2724">hello hello HDInsight 叢集的 URI。</span><span class="sxs-lookup"><span data-stu-id="566d6-2724">hello URI of hello HDInsight cluster.</span></span> |<span data-ttu-id="566d6-2725">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2725">Yes</span></span> |
| <span data-ttu-id="566d6-2726">username</span><span class="sxs-lookup"><span data-stu-id="566d6-2726">username</span></span> |<span data-ttu-id="566d6-2727">指定的 hello 使用者 toobe hello 名稱使用 tooconnect tooan 現有 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="566d6-2727">Specify hello name of hello user toobe used tooconnect tooan existing HDInsight cluster.</span></span> |<span data-ttu-id="566d6-2728">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2728">Yes</span></span> |
| <span data-ttu-id="566d6-2729">password</span><span class="sxs-lookup"><span data-stu-id="566d6-2729">password</span></span> |<span data-ttu-id="566d6-2730">指定 hello 使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="566d6-2730">Specify password for hello user account.</span></span> |<span data-ttu-id="566d6-2731">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2731">Yes</span></span> |
| <span data-ttu-id="566d6-2732">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="566d6-2732">linkedServiceName</span></span> | <span data-ttu-id="566d6-2733">Hello HDInsight 叢集供 hello 參照 toohello Azure blob 儲存體的 Azure 儲存體連結服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-2733">Name of hello Azure Storage linked service that refers toohello Azure blob storage used by hello HDInsight cluster.</span></span> <p><span data-ttu-id="566d6-2734">目前，您無法針對此屬性指定 Azure Data Lake Store 連結服務。</span><span class="sxs-lookup"><span data-stu-id="566d6-2734">Currently, you cannot specify an Azure Data Lake Store linked service for this property.</span></span> <span data-ttu-id="566d6-2735">如果 hello HDInsight 叢集已存取 toohello 資料湖存放區，您可能會存取 hello Azure 資料湖存放區中的資料從 Hive/Pig 指令碼。</span><span class="sxs-lookup"><span data-stu-id="566d6-2735">You may access data in hello Azure Data Lake Store from Hive/Pig scripts if hello HDInsight cluster has access toohello Data Lake Store.</span></span> </p>  |<span data-ttu-id="566d6-2736">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2736">Yes</span></span> |

<span data-ttu-id="566d6-2737">如需支援的 HDInsight 叢集版本，請參閱[支援的 HDInsight 版本](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory)。</span><span class="sxs-lookup"><span data-stu-id="566d6-2737">For versions of HDInsight clusters supported, see [supported HDInsight versions](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> 

#### <a name="json-example"></a><span data-ttu-id="566d6-2738">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="566d6-2738">JSON example</span></span>

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

## <a name="azure-batch"></a><span data-ttu-id="566d6-2739">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="566d6-2739">Azure Batch</span></span>
<span data-ttu-id="566d6-2740">您可以使用 data factory 建立 Azure 批次連結服務 tooregister 批次集區的虛擬機器 (Vm)。</span><span class="sxs-lookup"><span data-stu-id="566d6-2740">You can create an Azure Batch linked service tooregister a Batch pool of virtual machines (VMs) with a data factory.</span></span> <span data-ttu-id="566d6-2741">您可以使用 Azure Batch 或 Azure HDInsight 執行 .NET 自訂活動。</span><span class="sxs-lookup"><span data-stu-id="566d6-2741">You can run .NET custom activities using either Azure Batch or Azure HDInsight.</span></span> <span data-ttu-id="566d6-2742">您可以在此連結服務上執行 [.NET 自訂活動](#net-custom-activity)。</span><span class="sxs-lookup"><span data-stu-id="566d6-2742">You can run a [.NET custom activity](#net-custom-activity) on this linked service.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="566d6-2743">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-2743">Linked service</span></span>
<span data-ttu-id="566d6-2744">hello 下表提供使用 Azure Batch 連結服務的 hello Azure JSON 定義中的 hello 屬性的說明。</span><span class="sxs-lookup"><span data-stu-id="566d6-2744">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an Azure Batch linked service.</span></span>

| <span data-ttu-id="566d6-2745">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2745">Property</span></span> | <span data-ttu-id="566d6-2746">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2746">Description</span></span> | <span data-ttu-id="566d6-2747">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2747">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-2748">類型</span><span class="sxs-lookup"><span data-stu-id="566d6-2748">type</span></span> |<span data-ttu-id="566d6-2749">hello 類型屬性應該設定太**AzureBatch**。</span><span class="sxs-lookup"><span data-stu-id="566d6-2749">hello type property should be set too**AzureBatch**.</span></span> |<span data-ttu-id="566d6-2750">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2750">Yes</span></span> |
| <span data-ttu-id="566d6-2751">accountName</span><span class="sxs-lookup"><span data-stu-id="566d6-2751">accountName</span></span> |<span data-ttu-id="566d6-2752">Hello Azure Batch 帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-2752">Name of hello Azure Batch account.</span></span> |<span data-ttu-id="566d6-2753">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2753">Yes</span></span> |
| <span data-ttu-id="566d6-2754">accessKey</span><span class="sxs-lookup"><span data-stu-id="566d6-2754">accessKey</span></span> |<span data-ttu-id="566d6-2755">Hello Azure Batch 帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="566d6-2755">Access key for hello Azure Batch account.</span></span> |<span data-ttu-id="566d6-2756">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2756">Yes</span></span> |
| <span data-ttu-id="566d6-2757">poolName</span><span class="sxs-lookup"><span data-stu-id="566d6-2757">poolName</span></span> |<span data-ttu-id="566d6-2758">Hello 集區的虛擬機器名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-2758">Name of hello pool of virtual machines.</span></span> |<span data-ttu-id="566d6-2759">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2759">Yes</span></span> |
| <span data-ttu-id="566d6-2760">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="566d6-2760">linkedServiceName</span></span> |<span data-ttu-id="566d6-2761">Hello 與此 Azure Batch 連結服務相關聯的 Azure 儲存體連結服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-2761">Name of hello Azure Storage linked service associated with this Azure Batch linked service.</span></span> <span data-ttu-id="566d6-2762">這項連結的服務用於暫存檔案需要 toorun hello 活動與 hello 活動執行記錄的儲存。</span><span class="sxs-lookup"><span data-stu-id="566d6-2762">This linked service is used for staging files required toorun hello activity and storing hello activity execution logs.</span></span> |<span data-ttu-id="566d6-2763">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2763">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="566d6-2764">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="566d6-2764">JSON example</span></span>

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

## <a name="azure-machine-learning"></a><span data-ttu-id="566d6-2765">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="566d6-2765">Azure Machine Learning</span></span>
<span data-ttu-id="566d6-2766">建立 Azure Machine Learning 連結服務 tooregister Machine Learning 批次評分端點使用 data factory。</span><span class="sxs-lookup"><span data-stu-id="566d6-2766">You create an Azure Machine Learning linked service tooregister a Machine Learning batch scoring endpoint with a data factory.</span></span> <span data-ttu-id="566d6-2767">您可以在此連結服務上執行兩個資料轉換活動︰[Machine Learning 批次執行活動](#machine-learning-batch-execution-activity)、[Machine Learning 更新資源活動](#machine-learning-update-resource-activity)。</span><span class="sxs-lookup"><span data-stu-id="566d6-2767">Two data transformation activities that can run on this linked service: [Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="566d6-2768">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-2768">Linked service</span></span>
<span data-ttu-id="566d6-2769">hello 下表提供使用 Azure Machine Learning 連結服務的 hello Azure JSON 定義中的 hello 屬性的說明。</span><span class="sxs-lookup"><span data-stu-id="566d6-2769">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an Azure Machine Learning linked service.</span></span>

| <span data-ttu-id="566d6-2770">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2770">Property</span></span> | <span data-ttu-id="566d6-2771">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2771">Description</span></span> | <span data-ttu-id="566d6-2772">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2772">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-2773">類型</span><span class="sxs-lookup"><span data-stu-id="566d6-2773">Type</span></span> |<span data-ttu-id="566d6-2774">hello 類型屬性應該設定為： **AzureML**。</span><span class="sxs-lookup"><span data-stu-id="566d6-2774">hello type property should be set to: **AzureML**.</span></span> |<span data-ttu-id="566d6-2775">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2775">Yes</span></span> |
| <span data-ttu-id="566d6-2776">mlEndpoint</span><span class="sxs-lookup"><span data-stu-id="566d6-2776">mlEndpoint</span></span> |<span data-ttu-id="566d6-2777">hello 批次評分 URL。</span><span class="sxs-lookup"><span data-stu-id="566d6-2777">hello batch scoring URL.</span></span> |<span data-ttu-id="566d6-2778">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2778">Yes</span></span> |
| <span data-ttu-id="566d6-2779">apiKey</span><span class="sxs-lookup"><span data-stu-id="566d6-2779">apiKey</span></span> |<span data-ttu-id="566d6-2780">hello 發行工作區模型的 API。</span><span class="sxs-lookup"><span data-stu-id="566d6-2780">hello published workspace model’s API.</span></span> |<span data-ttu-id="566d6-2781">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2781">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="566d6-2782">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="566d6-2782">JSON example</span></span>

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

## <a name="azure-data-lake-analytics"></a><span data-ttu-id="566d6-2783">Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="566d6-2783">Azure Data Lake Analytics</span></span>
<span data-ttu-id="566d6-2784">您建立**Azure Data Lake Analytics**之前使用 hello 連結服務 toolink Azure Data Lake Analytics 計算服務 tooan Azure data factory[資料 Lake Analytics U-SQL 活動](data-factory-usql-activity.md)管線中.</span><span class="sxs-lookup"><span data-stu-id="566d6-2784">You create an **Azure Data Lake Analytics** linked service toolink an Azure Data Lake Analytics compute service tooan Azure data factory before using hello [Data Lake Analytics U-SQL activity](data-factory-usql-activity.md) in a pipeline.</span></span>

### <a name="linked-service"></a><span data-ttu-id="566d6-2785">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-2785">Linked service</span></span>

<span data-ttu-id="566d6-2786">下表中的 hello 提供 hello 屬性連結 Azure Data Lake Analytics 服務的 hello JSON 定義中所使用的說明。</span><span class="sxs-lookup"><span data-stu-id="566d6-2786">hello following table provides descriptions for hello properties used in hello JSON definition of an Azure Data Lake Analytics linked service.</span></span> 

| <span data-ttu-id="566d6-2787">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2787">Property</span></span> | <span data-ttu-id="566d6-2788">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2788">Description</span></span> | <span data-ttu-id="566d6-2789">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2789">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-2790">類型</span><span class="sxs-lookup"><span data-stu-id="566d6-2790">Type</span></span> |<span data-ttu-id="566d6-2791">hello 類型屬性應該設定為： **AzureDataLakeAnalytics**。</span><span class="sxs-lookup"><span data-stu-id="566d6-2791">hello type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="566d6-2792">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2792">Yes</span></span> |
| <span data-ttu-id="566d6-2793">accountName</span><span class="sxs-lookup"><span data-stu-id="566d6-2793">accountName</span></span> |<span data-ttu-id="566d6-2794">Azure Data Lake Analytics 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-2794">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="566d6-2795">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2795">Yes</span></span> |
| <span data-ttu-id="566d6-2796">dataLakeAnalyticsUri</span><span class="sxs-lookup"><span data-stu-id="566d6-2796">dataLakeAnalyticsUri</span></span> |<span data-ttu-id="566d6-2797">Azure Data Lake Analytics URI。</span><span class="sxs-lookup"><span data-stu-id="566d6-2797">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="566d6-2798">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2798">No</span></span> |
| <span data-ttu-id="566d6-2799">授權</span><span class="sxs-lookup"><span data-stu-id="566d6-2799">authorization</span></span> |<span data-ttu-id="566d6-2800">按一下之後，就會自動擷取授權碼**授權**hello Data Factory 編輯器和完成 hello OAuth 登入 按鈕。</span><span class="sxs-lookup"><span data-stu-id="566d6-2800">Authorization code is automatically retrieved after clicking **Authorize** button in hello Data Factory Editor and completing hello OAuth login.</span></span> |<span data-ttu-id="566d6-2801">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2801">Yes</span></span> |
| <span data-ttu-id="566d6-2802">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="566d6-2802">subscriptionId</span></span> |<span data-ttu-id="566d6-2803">Azure 訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="566d6-2803">Azure subscription id</span></span> |<span data-ttu-id="566d6-2804">否 （如果未指定，訂用帳戶的資料處理站可用的 hello）。</span><span class="sxs-lookup"><span data-stu-id="566d6-2804">No (If not specified, subscription of hello data factory is used).</span></span> |
| <span data-ttu-id="566d6-2805">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="566d6-2805">resourceGroupName</span></span> |<span data-ttu-id="566d6-2806">Azure 資源群組名稱</span><span class="sxs-lookup"><span data-stu-id="566d6-2806">Azure resource group name</span></span> |<span data-ttu-id="566d6-2807">否 （如果未指定，資源群組的資料處理站可用的 hello）。</span><span class="sxs-lookup"><span data-stu-id="566d6-2807">No (If not specified, resource group of hello data factory is used).</span></span> |
| <span data-ttu-id="566d6-2808">sessionId</span><span class="sxs-lookup"><span data-stu-id="566d6-2808">sessionId</span></span> |<span data-ttu-id="566d6-2809">從 hello OAuth 授權工作階段的工作階段識別碼。</span><span class="sxs-lookup"><span data-stu-id="566d6-2809">session id from hello OAuth authorization session.</span></span> <span data-ttu-id="566d6-2810">每個工作階段識別碼都是唯一的，只能使用一次。</span><span class="sxs-lookup"><span data-stu-id="566d6-2810">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="566d6-2811">當您使用 hello Data Factory 編輯器時，這個識別碼是自動產生。</span><span class="sxs-lookup"><span data-stu-id="566d6-2811">When you use hello Data Factory Editor, this ID is auto-generated.</span></span> |<span data-ttu-id="566d6-2812">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2812">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="566d6-2813">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="566d6-2813">JSON example</span></span>
<span data-ttu-id="566d6-2814">下列範例中的 hello 提供 JSON 定義連結的 Azure 資料湖分析服務。</span><span class="sxs-lookup"><span data-stu-id="566d6-2814">hello following example provides JSON definition for an Azure Data Lake Analytics linked service.</span></span>

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

## <a name="azure-sql-database"></a><span data-ttu-id="566d6-2815">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="566d6-2815">Azure SQL Database</span></span>
<span data-ttu-id="566d6-2816">您建立 Azure SQL 連結服務，並使用它搭配 hello[預存程序活動](#stored-procedure-activity)tooinvoke 從 Data Factory 管線的預存程序。</span><span class="sxs-lookup"><span data-stu-id="566d6-2816">You create an Azure SQL linked service and use it with hello [Stored Procedure Activity](#stored-procedure-activity) tooinvoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="566d6-2817">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-2817">Linked service</span></span>
<span data-ttu-id="566d6-2818">Azure SQL Database toodefine 連結服務，設定 hello**類型**hello 的連結服務太**AzureSqlDatabase**，並指定下列屬性在 hello **typeProperties**> 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-2818">toodefine an Azure SQL Database linked service, set hello **type** of hello linked service too**AzureSqlDatabase**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="566d6-2819">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2819">Property</span></span> | <span data-ttu-id="566d6-2820">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2820">Description</span></span> | <span data-ttu-id="566d6-2821">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2821">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-2822">connectionString</span><span class="sxs-lookup"><span data-stu-id="566d6-2822">connectionString</span></span> |<span data-ttu-id="566d6-2823">指定所需的資訊 tooconnect toohello Azure SQL Database 執行個體 hello connectionString 屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-2823">Specify information needed tooconnect toohello Azure SQL Database instance for hello connectionString property.</span></span> |<span data-ttu-id="566d6-2824">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2824">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="566d6-2825">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="566d6-2825">JSON example</span></span>

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

<span data-ttu-id="566d6-2826">如需此連結服務的詳細資料，請參閱 [Azure SQL 連接器](data-factory-azure-sql-connector.md#linked-service-properties) 一文。</span><span class="sxs-lookup"><span data-stu-id="566d6-2826">See [Azure SQL Connector](data-factory-azure-sql-connector.md#linked-service-properties) article for details about this linked service.</span></span>

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="566d6-2827">Azure SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="566d6-2827">Azure SQL Data Warehouse</span></span>
<span data-ttu-id="566d6-2828">您建立連結的 Azure SQL 資料倉儲服務，並使用它搭配 hello[預存程序活動](data-factory-stored-proc-activity.md)tooinvoke 從 Data Factory 管線的預存程序。</span><span class="sxs-lookup"><span data-stu-id="566d6-2828">You create an Azure SQL Data Warehouse linked service and use it with hello [Stored Procedure Activity](data-factory-stored-proc-activity.md) tooinvoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="566d6-2829">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-2829">Linked service</span></span>
<span data-ttu-id="566d6-2830">Azure SQL 資料倉儲 toodefine 連結服務，設定 hello**類型**hello 的連結服務太**AzureSqlDW**，並指定下列屬性在 hello **typeProperties**> 一節：</span><span class="sxs-lookup"><span data-stu-id="566d6-2830">toodefine an Azure SQL Data Warehouse linked service, set hello **type** of hello linked service too**AzureSqlDW**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="566d6-2831">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2831">Property</span></span> | <span data-ttu-id="566d6-2832">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2832">Description</span></span> | <span data-ttu-id="566d6-2833">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2833">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-2834">connectionString</span><span class="sxs-lookup"><span data-stu-id="566d6-2834">connectionString</span></span> |<span data-ttu-id="566d6-2835">指定所需的資訊 tooconnect toohello Azure SQL 資料倉儲執行個體 hello connectionString 屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-2835">Specify information needed tooconnect toohello Azure SQL Data Warehouse instance for hello connectionString property.</span></span> |<span data-ttu-id="566d6-2836">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2836">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="566d6-2837">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="566d6-2837">JSON example</span></span>

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

<span data-ttu-id="566d6-2838">如需詳細資訊，請參閱 [Azure SQL 資料倉儲連接器](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-2838">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

## <a name="sql-server"></a><span data-ttu-id="566d6-2839">SQL Server</span><span class="sxs-lookup"><span data-stu-id="566d6-2839">SQL Server</span></span> 
<span data-ttu-id="566d6-2840">建立連結的 SQL Server 服務，並使用以 hello[預存程序活動](data-factory-stored-proc-activity.md)tooinvoke 從 Data Factory 管線的預存程序。</span><span class="sxs-lookup"><span data-stu-id="566d6-2840">You create a SQL Server linked service and use it with hello [Stored Procedure Activity](data-factory-stored-proc-activity.md) tooinvoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="566d6-2841">連結服務</span><span class="sxs-lookup"><span data-stu-id="566d6-2841">Linked service</span></span>
<span data-ttu-id="566d6-2842">您建立連結的服務型別的**OnPremisesSqlServer** toolink 在內部部署 SQL Server 資料庫 tooa 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="566d6-2842">You create a linked service of type **OnPremisesSqlServer** toolink an on-premises SQL Server database tooa data factory.</span></span> <span data-ttu-id="566d6-2843">下表中的 hello 提供 JSON 項目特定 tooon 內部部署 SQL Server 連結服務的描述。</span><span class="sxs-lookup"><span data-stu-id="566d6-2843">hello following table provides description for JSON elements specific tooon-premises SQL Server linked service.</span></span>

<span data-ttu-id="566d6-2844">下表中的 hello 提供 JSON 項目特定 tooSQL 連結的伺服器服務的描述。</span><span class="sxs-lookup"><span data-stu-id="566d6-2844">hello following table provides description for JSON elements specific tooSQL Server linked service.</span></span>

| <span data-ttu-id="566d6-2845">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2845">Property</span></span> | <span data-ttu-id="566d6-2846">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2846">Description</span></span> | <span data-ttu-id="566d6-2847">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2847">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-2848">類型</span><span class="sxs-lookup"><span data-stu-id="566d6-2848">type</span></span> |<span data-ttu-id="566d6-2849">hello 類型屬性應該設定為： **OnPremisesSqlServer**。</span><span class="sxs-lookup"><span data-stu-id="566d6-2849">hello type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="566d6-2850">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2850">Yes</span></span> |
| <span data-ttu-id="566d6-2851">connectionString</span><span class="sxs-lookup"><span data-stu-id="566d6-2851">connectionString</span></span> |<span data-ttu-id="566d6-2852">指定所需的 connectionString 資訊 tooconnect toohello 在內部部署 SQL Server 資料庫使用 SQL 驗證或 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="566d6-2852">Specify connectionString information needed tooconnect toohello on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="566d6-2853">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2853">Yes</span></span> |
| <span data-ttu-id="566d6-2854">gatewayName</span><span class="sxs-lookup"><span data-stu-id="566d6-2854">gatewayName</span></span> |<span data-ttu-id="566d6-2855">Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello 在內部部署 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="566d6-2855">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SQL Server database.</span></span> |<span data-ttu-id="566d6-2856">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2856">Yes</span></span> |
| <span data-ttu-id="566d6-2857">username</span><span class="sxs-lookup"><span data-stu-id="566d6-2857">username</span></span> |<span data-ttu-id="566d6-2858">如果您使用「Windows 驗證」，請指定使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-2858">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="566d6-2859">範例︰**domainname\\username**。</span><span class="sxs-lookup"><span data-stu-id="566d6-2859">Example: **domainname\\username**.</span></span> |<span data-ttu-id="566d6-2860">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2860">No</span></span> |
| <span data-ttu-id="566d6-2861">password</span><span class="sxs-lookup"><span data-stu-id="566d6-2861">password</span></span> |<span data-ttu-id="566d6-2862">指定 hello hello 使用者名稱所指定的使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="566d6-2862">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="566d6-2863">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2863">No</span></span> |

<span data-ttu-id="566d6-2864">您可以加密認證使用 hello**新增 AzureRmDataFactoryEncryptValue** cmdlet 並將其用於 hello 連接字串 hello 下列範例所示 (**EncryptedCredential**屬性):</span><span class="sxs-lookup"><span data-stu-id="566d6-2864">You can encrypt credentials using hello **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in hello connection string as shown in hello following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="566d6-2865">範例：用於 SQL 驗證的 JSON</span><span class="sxs-lookup"><span data-stu-id="566d6-2865">Example: JSON for using SQL Authentication</span></span>

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
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="566d6-2866">範例：用於 Windows 驗證的 JSON</span><span class="sxs-lookup"><span data-stu-id="566d6-2866">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="566d6-2867">如果未指定使用者名稱和密碼，閘道會使用這些 tooimpersonate hello 指定的使用者帳戶 tooconnect toohello 在內部部署 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="566d6-2867">If username and password are specified, gateway uses them tooimpersonate hello specified user account tooconnect toohello on-premises SQL Server database.</span></span> <span data-ttu-id="566d6-2868">否則，閘道會直接與 hello 的閘道 （其啟動帳戶） 的安全性內容連線 toohello SQL Server。</span><span class="sxs-lookup"><span data-stu-id="566d6-2868">Otherwise, gateway connects toohello SQL Server directly with hello security context of Gateway (its startup account).</span></span>

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

<span data-ttu-id="566d6-2869">如需詳細資訊，請參閱 [SQL Server 連接器](data-factory-sqlserver-connector.md#linked-service-properties)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-2869">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span>

## <a name="data-transformation-activities"></a><span data-ttu-id="566d6-2870">資料轉換活動</span><span class="sxs-lookup"><span data-stu-id="566d6-2870">DATA TRANSFORMATION ACTIVITIES</span></span>

<span data-ttu-id="566d6-2871">活動</span><span class="sxs-lookup"><span data-stu-id="566d6-2871">Activity</span></span> | <span data-ttu-id="566d6-2872">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2872">Description</span></span>
-------- | -----------
[<span data-ttu-id="566d6-2873">HDInsight Hive 活動</span><span class="sxs-lookup"><span data-stu-id="566d6-2873">HDInsight Hive activity</span></span>](#hdinsight-hive-activity) | <span data-ttu-id="566d6-2874">hello HDInsight Hive 活動 Data Factory 管線中執行您自己的 Hive 查詢或隨 Windows/linux 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="566d6-2874">hello HDInsight Hive activity in a Data Factory pipeline executes Hive queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span> 
[<span data-ttu-id="566d6-2875">HDInsight Pig 活動</span><span class="sxs-lookup"><span data-stu-id="566d6-2875">HDInsight Pig activity</span></span>](#hdinsight-pig-activity) | <span data-ttu-id="566d6-2876">hello HDInsight Pig 活動 Data Factory 管線中執行您自己的 Pig 查詢或隨 Windows/linux 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="566d6-2876">hello HDInsight Pig activity in a Data Factory pipeline executes Pig queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="566d6-2877">HDInsight MapReduce 活動</span><span class="sxs-lookup"><span data-stu-id="566d6-2877">HDInsight MapReduce Activity</span></span>](#hdinsight-mapreduce-activity) | <span data-ttu-id="566d6-2878">hello HDInsight MapReduce 活動 Data Factory 管線中執行您自己的 MapReduce 程式或隨 Windows/linux 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="566d6-2878">hello HDInsight MapReduce activity in a Data Factory pipeline executes MapReduce programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="566d6-2879">HDInsight 串流活動</span><span class="sxs-lookup"><span data-stu-id="566d6-2879">HDInsight Streaming Activity</span></span>](#hdinsight-streaming-activity) | <span data-ttu-id="566d6-2880">Data Factory 管線中的 hello HDInsight 串流活動執行您自己的 Hadoop 串流程式或隨 Windows/linux 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="566d6-2880">hello HDInsight Streaming Activity in a Data Factory pipeline executes Hadoop Streaming programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="566d6-2881">HDInsight Spark 活動</span><span class="sxs-lookup"><span data-stu-id="566d6-2881">HDInsight Spark Activity</span></span>](#hdinsight-spark-activity) | <span data-ttu-id="566d6-2882">hello HDInsight Spark Data Factory 管線中的活動執行您自己的 HDInsight 叢集上的 Spark 程式。</span><span class="sxs-lookup"><span data-stu-id="566d6-2882">hello HDInsight Spark activity in a Data Factory pipeline executes Spark programs on your own HDInsight cluster.</span></span> 
[<span data-ttu-id="566d6-2883">Machine Learning Batch 執行活動</span><span class="sxs-lookup"><span data-stu-id="566d6-2883">Machine Learning Batch Execution Activity</span></span>](#machine-learning-batch-execution-activity) | <span data-ttu-id="566d6-2884">Azure Data Factory 可讓您 tooeasily 建立管線，使用已發行的 Azure Machine Learning web 服務的預測分析。</span><span class="sxs-lookup"><span data-stu-id="566d6-2884">Azure Data Factory enables you tooeasily create pipelines that use a published Azure Machine Learning web service for predictive analytics.</span></span> <span data-ttu-id="566d6-2885">使用 Azure Data Factory 管線中的 hello 批次執行活動，您可以叫用批次中的 hello 資料機器學習 web 服務 toomake 的預測。</span><span class="sxs-lookup"><span data-stu-id="566d6-2885">Using hello Batch Execution Activity in an Azure Data Factory pipeline, you can invoke a Machine Learning web service toomake predictions on hello data in batch.</span></span> 
[<span data-ttu-id="566d6-2886">Machine Learning 更新資源活動</span><span class="sxs-lookup"><span data-stu-id="566d6-2886">Machine Learning Update Resource Activity</span></span>](#machine-learning-update-resource-activity) | <span data-ttu-id="566d6-2887">經過一段時間，在 hello 計分實驗需要 toobe 重新定型使用全新的機器學習中的 hello 預測模型的輸入資料集。</span><span class="sxs-lookup"><span data-stu-id="566d6-2887">Over time, hello predictive models in hello Machine Learning scoring experiments need toobe retrained using new input datasets.</span></span> <span data-ttu-id="566d6-2888">您完成定型之後，您會想要計分 web 服務以 hello tooupdate hello 重新定型機器學習模型。</span><span class="sxs-lookup"><span data-stu-id="566d6-2888">After you are done with retraining, you want tooupdate hello scoring web service with hello retrained Machine Learning model.</span></span> <span data-ttu-id="566d6-2889">您可以使用 hello 更新資源活動 tooupdate hello web 服務與 hello 新定型模型。</span><span class="sxs-lookup"><span data-stu-id="566d6-2889">You can use hello Update Resource Activity tooupdate hello web service with hello newly trained model.</span></span>
[<span data-ttu-id="566d6-2890">預存程序活動</span><span class="sxs-lookup"><span data-stu-id="566d6-2890">Stored Procedure Activity</span></span>](#stored-procedure-activity) | <span data-ttu-id="566d6-2891">您可以使用 Data Factory 管線 tooinvoke 其中一種 hello 下列資料存放區預存程序中的 hello 預存程序活動： Azure SQL Database、 Azure SQL 資料倉儲，在您企業中的 SQL Server 資料庫或 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="566d6-2891">You can use hello Stored Procedure activity in a Data Factory pipeline tooinvoke a stored procedure in one of hello following data stores: Azure SQL Database, Azure SQL Data Warehouse, SQL Server Database in your enterprise or an Azure VM.</span></span> 
[<span data-ttu-id="566d6-2892">Data Lake Analytics U-SQL 活動</span><span class="sxs-lookup"><span data-stu-id="566d6-2892">Data Lake Analytics U-SQL activity</span></span>](#data-lake-analytics-u-sql-activity) | <span data-ttu-id="566d6-2893">Data Lake Analytics U-SQL 活動會在 Azure Data Lake Analytics 叢集上執行 U-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="566d6-2893">Data Lake Analytics U-SQL Activity runs a U-SQL script on an Azure Data Lake Analytics cluster.</span></span>  
[<span data-ttu-id="566d6-2894">.NET 自訂活動</span><span class="sxs-lookup"><span data-stu-id="566d6-2894">.NET custom activity</span></span>](#net-custom-activity) | <span data-ttu-id="566d6-2895">如果您需要 tootransform 資料不支援的 Data Factory 的方式，您可以建立您自己的資料處理邏輯的自訂活動，並使用 hello 管線中的 hello 活動。</span><span class="sxs-lookup"><span data-stu-id="566d6-2895">If you need tootransform data in a way that is not supported by Data Factory, you can create a custom activity with your own data processing logic and use hello activity in hello pipeline.</span></span> <span data-ttu-id="566d6-2896">您可以設定 hello 自訂.NET 活動 toorun 使用 Azure Batch 服務或 Azure HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="566d6-2896">You can configure hello custom .NET activity toorun using either an Azure Batch service or an Azure HDInsight cluster.</span></span> 

     
## <a name="hdinsight-hive-activity"></a><span data-ttu-id="566d6-2897">HDInsight Hive 活動</span><span class="sxs-lookup"><span data-stu-id="566d6-2897">HDInsight Hive Activity</span></span>
<span data-ttu-id="566d6-2898">您可以指定下列屬性 Hive 活動 JSON 定義中的 hello。</span><span class="sxs-lookup"><span data-stu-id="566d6-2898">You can specify hello following properties in a Hive Activity JSON definition.</span></span> <span data-ttu-id="566d6-2899">hello hello 活動的型別屬性必須是： **HDInsightHive**。</span><span class="sxs-lookup"><span data-stu-id="566d6-2899">hello type property for hello activity must be: **HDInsightHive**.</span></span> <span data-ttu-id="566d6-2900">您必須先建立 HDInsight 連結服務，並指定它 hello 名稱做為 hello 值**linkedServiceName**屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-2900">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="566d6-2901">hello 支援下列屬性在 hello **typeProperties**區段，當您設定活動 tooHDInsightHive hello 類型：</span><span class="sxs-lookup"><span data-stu-id="566d6-2901">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightHive:</span></span>

| <span data-ttu-id="566d6-2902">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2902">Property</span></span> | <span data-ttu-id="566d6-2903">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2903">Description</span></span> | <span data-ttu-id="566d6-2904">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2904">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-2905">script</span><span class="sxs-lookup"><span data-stu-id="566d6-2905">script</span></span> |<span data-ttu-id="566d6-2906">指定內嵌 hello Hive 指令碼</span><span class="sxs-lookup"><span data-stu-id="566d6-2906">Specify hello Hive script inline</span></span> |<span data-ttu-id="566d6-2907">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2907">No</span></span> |
| <span data-ttu-id="566d6-2908">指令碼路徑</span><span class="sxs-lookup"><span data-stu-id="566d6-2908">script path</span></span> |<span data-ttu-id="566d6-2909">存放區 hello Hive 指令碼在 Azure blob 儲存體，並提供 hello 路徑 toohello 檔案。</span><span class="sxs-lookup"><span data-stu-id="566d6-2909">Store hello Hive script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="566d6-2910">使用 'script' 或 'scriptPath' 屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-2910">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="566d6-2911">兩者無法同時使用。</span><span class="sxs-lookup"><span data-stu-id="566d6-2911">Both cannot be used together.</span></span> <span data-ttu-id="566d6-2912">hello 檔案名稱是區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="566d6-2912">hello file name is case-sensitive.</span></span> |<span data-ttu-id="566d6-2913">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2913">No</span></span> |
| <span data-ttu-id="566d6-2914">定義</span><span class="sxs-lookup"><span data-stu-id="566d6-2914">defines</span></span> |<span data-ttu-id="566d6-2915">指定參數做為索引鍵/值組內使用 'hiveconf' hello Hive 指令碼參考</span><span class="sxs-lookup"><span data-stu-id="566d6-2915">Specify parameters as key/value pairs for referencing within hello Hive script using 'hiveconf'</span></span> |<span data-ttu-id="566d6-2916">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2916">No</span></span> |

<span data-ttu-id="566d6-2917">這些類型的屬性是特定 toohello Hive 活動。</span><span class="sxs-lookup"><span data-stu-id="566d6-2917">These type properties are specific toohello Hive Activity.</span></span> <span data-ttu-id="566d6-2918">（外部 hello typeProperties 區段） 的其他屬性都支援所有活動。</span><span class="sxs-lookup"><span data-stu-id="566d6-2918">Other properties (outside hello typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="566d6-2919">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="566d6-2919">JSON example</span></span>
<span data-ttu-id="566d6-2920">下列 JSON hello 管線中定義 HDInsight Hive 活動。</span><span class="sxs-lookup"><span data-stu-id="566d6-2920">hello following JSON defines a HDInsight Hive activity in a pipeline.</span></span>  

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

<span data-ttu-id="566d6-2921">如需詳細資訊，請參閱 [Hive 活動](data-factory-hive-activity.md)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-2921">For more information, see [Hive Activity](data-factory-hive-activity.md) article.</span></span> 

## <a name="hdinsight-pig-activity"></a><span data-ttu-id="566d6-2922">HDInsight Pig 活動</span><span class="sxs-lookup"><span data-stu-id="566d6-2922">HDInsight Pig Activity</span></span>
<span data-ttu-id="566d6-2923">您可以指定下列屬性 Pig 活動 JSON 定義中的 hello。</span><span class="sxs-lookup"><span data-stu-id="566d6-2923">You can specify hello following properties in a Pig Activity JSON definition.</span></span> <span data-ttu-id="566d6-2924">hello hello 活動的型別屬性必須是： **HDInsightPig**。</span><span class="sxs-lookup"><span data-stu-id="566d6-2924">hello type property for hello activity must be: **HDInsightPig**.</span></span> <span data-ttu-id="566d6-2925">您必須先建立 HDInsight 連結服務，並指定它 hello 名稱做為 hello 值**linkedServiceName**屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-2925">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="566d6-2926">hello 支援下列屬性在 hello **typeProperties**區段，當您設定活動 tooHDInsightPig hello 類型：</span><span class="sxs-lookup"><span data-stu-id="566d6-2926">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightPig:</span></span> 

| <span data-ttu-id="566d6-2927">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2927">Property</span></span> | <span data-ttu-id="566d6-2928">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2928">Description</span></span> | <span data-ttu-id="566d6-2929">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2929">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-2930">script</span><span class="sxs-lookup"><span data-stu-id="566d6-2930">script</span></span> |<span data-ttu-id="566d6-2931">指定 hello Pig 指令碼內嵌</span><span class="sxs-lookup"><span data-stu-id="566d6-2931">Specify hello Pig script inline</span></span> |<span data-ttu-id="566d6-2932">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2932">No</span></span> |
| <span data-ttu-id="566d6-2933">指令碼路徑</span><span class="sxs-lookup"><span data-stu-id="566d6-2933">script path</span></span> |<span data-ttu-id="566d6-2934">在 Azure blob 儲存體中儲存 hello Pig 指令碼，並提供 hello 路徑 toohello 檔案。</span><span class="sxs-lookup"><span data-stu-id="566d6-2934">Store hello Pig script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="566d6-2935">使用 'script' 或 'scriptPath' 屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-2935">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="566d6-2936">兩者無法同時使用。</span><span class="sxs-lookup"><span data-stu-id="566d6-2936">Both cannot be used together.</span></span> <span data-ttu-id="566d6-2937">hello 檔案名稱是區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="566d6-2937">hello file name is case-sensitive.</span></span> |<span data-ttu-id="566d6-2938">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2938">No</span></span> |
| <span data-ttu-id="566d6-2939">定義</span><span class="sxs-lookup"><span data-stu-id="566d6-2939">defines</span></span> |<span data-ttu-id="566d6-2940">指定參數做為索引鍵/值組內 hello Pig 指令碼參考</span><span class="sxs-lookup"><span data-stu-id="566d6-2940">Specify parameters as key/value pairs for referencing within hello Pig script</span></span> |<span data-ttu-id="566d6-2941">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2941">No</span></span> |

<span data-ttu-id="566d6-2942">這些類型的屬性是特定 toohello Pig 活動。</span><span class="sxs-lookup"><span data-stu-id="566d6-2942">These type properties are specific toohello Pig Activity.</span></span> <span data-ttu-id="566d6-2943">（外部 hello typeProperties 區段） 的其他屬性都支援所有活動。</span><span class="sxs-lookup"><span data-stu-id="566d6-2943">Other properties (outside hello typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="566d6-2944">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="566d6-2944">JSON example</span></span>

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

<span data-ttu-id="566d6-2945">如需詳細資訊，請參閱 [Pig 活動](#data-factory-pig-activity.md)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-2945">For more information, see [Pig Activity](#data-factory-pig-activity.md) article.</span></span> 

## <a name="hdinsight-mapreduce-activity"></a><span data-ttu-id="566d6-2946">HDInsight MapReduce 活動</span><span class="sxs-lookup"><span data-stu-id="566d6-2946">HDInsight MapReduce Activity</span></span>
<span data-ttu-id="566d6-2947">您可以指定下列屬性 MapReduce 活動 JSON 定義中的 hello。</span><span class="sxs-lookup"><span data-stu-id="566d6-2947">You can specify hello following properties in a MapReduce Activity JSON definition.</span></span> <span data-ttu-id="566d6-2948">hello hello 活動的型別屬性必須是： **HDInsightMapReduce**。</span><span class="sxs-lookup"><span data-stu-id="566d6-2948">hello type property for hello activity must be: **HDInsightMapReduce**.</span></span> <span data-ttu-id="566d6-2949">您必須先建立 HDInsight 連結服務，並指定它 hello 名稱做為 hello 值**linkedServiceName**屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-2949">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="566d6-2950">hello 支援下列屬性在 hello **typeProperties**區段，當您設定活動 tooHDInsightMapReduce hello 類型：</span><span class="sxs-lookup"><span data-stu-id="566d6-2950">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightMapReduce:</span></span> 

| <span data-ttu-id="566d6-2951">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2951">Property</span></span> | <span data-ttu-id="566d6-2952">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2952">Description</span></span> | <span data-ttu-id="566d6-2953">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-2953">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-2954">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="566d6-2954">jarLinkedService</span></span> | <span data-ttu-id="566d6-2955">連結 hello 包含 hello JAR 檔案的 Azure 儲存體服務的 hello 的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-2955">Name of hello linked service for hello Azure Storage that contains hello JAR file.</span></span> | <span data-ttu-id="566d6-2956">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2956">Yes</span></span> |
| <span data-ttu-id="566d6-2957">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="566d6-2957">jarFilePath</span></span> | <span data-ttu-id="566d6-2958">在 hello Azure 儲存體 toohello JAR 檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="566d6-2958">Path toohello JAR file in hello Azure Storage.</span></span> | <span data-ttu-id="566d6-2959">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2959">Yes</span></span> | 
| <span data-ttu-id="566d6-2960">className</span><span class="sxs-lookup"><span data-stu-id="566d6-2960">className</span></span> | <span data-ttu-id="566d6-2961">Hello hello JAR 檔案中的主要類別的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-2961">Name of hello main class in hello JAR file.</span></span> | <span data-ttu-id="566d6-2962">是</span><span class="sxs-lookup"><span data-stu-id="566d6-2962">Yes</span></span> | 
| <span data-ttu-id="566d6-2963">arguments</span><span class="sxs-lookup"><span data-stu-id="566d6-2963">arguments</span></span> | <span data-ttu-id="566d6-2964">Hello MapReduce 程式以逗號分隔的引數清單。</span><span class="sxs-lookup"><span data-stu-id="566d6-2964">A list of comma-separated arguments for hello MapReduce program.</span></span> <span data-ttu-id="566d6-2965">在執行階段，您會看到幾個額外的引數 (例如： mapreduce.job.tags) 從 hello MapReduce 架構。</span><span class="sxs-lookup"><span data-stu-id="566d6-2965">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from hello MapReduce framework.</span></span> <span data-ttu-id="566d6-2966">toodifferentiate hello MapReduce 引數時，您的引數，請考慮使用選項和值做為引數中 hello 下列範例所示 (-s，-輸入、--輸出等，是後面緊跟著其值的選項)</span><span class="sxs-lookup"><span data-stu-id="566d6-2966">toodifferentiate your arguments with hello MapReduce arguments, consider using both option and value as arguments as shown in hello following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | <span data-ttu-id="566d6-2967">否</span><span class="sxs-lookup"><span data-stu-id="566d6-2967">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="566d6-2968">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="566d6-2968">JSON example</span></span>

```json
{
    "name": "MahoutMapReduceSamplePipeline",
    "properties": {
        "description": "Sample Pipeline tooRun a Mahout Custom Map Reduce Jar. This job calculates an Item Similarity Matrix toodetermine hello similarity between two items",
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
                "description": "Custom Map Reduce toogenerate Mahout result",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00",
        "end": "2017-01-04T00:00:00"
    }
}
```

<span data-ttu-id="566d6-2969">如需詳細資訊，請參閱 [MapReduce 活動](data-factory-map-reduce.md)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-2969">For more information, see [MapReduce Activity](data-factory-map-reduce.md) article.</span></span> 

## <a name="hdinsight-streaming-activity"></a><span data-ttu-id="566d6-2970">HDInsight 串流活動</span><span class="sxs-lookup"><span data-stu-id="566d6-2970">HDInsight Streaming Activity</span></span>
<span data-ttu-id="566d6-2971">您可以指定下列屬性 Hadoop 串流活動 JSON 定義中的 hello。</span><span class="sxs-lookup"><span data-stu-id="566d6-2971">You can specify hello following properties in a Hadoop Streaming Activity JSON definition.</span></span> <span data-ttu-id="566d6-2972">hello hello 活動的型別屬性必須是： **HDInsightStreaming**。</span><span class="sxs-lookup"><span data-stu-id="566d6-2972">hello type property for hello activity must be: **HDInsightStreaming**.</span></span> <span data-ttu-id="566d6-2973">您必須先建立 HDInsight 連結服務，並指定它 hello 名稱做為 hello 值**linkedServiceName**屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-2973">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="566d6-2974">hello 支援下列屬性在 hello **typeProperties**區段，當您設定活動 tooHDInsightStreaming hello 類型：</span><span class="sxs-lookup"><span data-stu-id="566d6-2974">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightStreaming:</span></span> 

| <span data-ttu-id="566d6-2975">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-2975">Property</span></span> | <span data-ttu-id="566d6-2976">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-2976">Description</span></span> | 
| --- | --- |
| <span data-ttu-id="566d6-2977">mapper</span><span class="sxs-lookup"><span data-stu-id="566d6-2977">mapper</span></span> | <span data-ttu-id="566d6-2978">Hello 對應工具可執行檔的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-2978">Name of hello mapper executable.</span></span> <span data-ttu-id="566d6-2979">在 hello 範例 cat.exe 會是 hello 對應工具可執行檔。</span><span class="sxs-lookup"><span data-stu-id="566d6-2979">In hello example, cat.exe is hello mapper executable.</span></span>| 
| <span data-ttu-id="566d6-2980">reducer</span><span class="sxs-lookup"><span data-stu-id="566d6-2980">reducer</span></span> | <span data-ttu-id="566d6-2981">Hello 減壓器可執行檔的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-2981">Name of hello reducer executable.</span></span> <span data-ttu-id="566d6-2982">在 hello 範例 wc.exe 是 hello 減壓器可執行檔。</span><span class="sxs-lookup"><span data-stu-id="566d6-2982">In hello example, wc.exe is hello reducer executable.</span></span> | 
| <span data-ttu-id="566d6-2983">input</span><span class="sxs-lookup"><span data-stu-id="566d6-2983">input</span></span> | <span data-ttu-id="566d6-2984">輸入的檔 （包括位置） hello 對應工具。</span><span class="sxs-lookup"><span data-stu-id="566d6-2984">Input file (including location) for hello mapper.</span></span> <span data-ttu-id="566d6-2985">在 hello 範例: 「 wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample 是 blob 容器，hello 範例/data/Gutenberg 是 hello 資料夾，而 davinci.txt 是 hello blob。</span><span class="sxs-lookup"><span data-stu-id="566d6-2985">In hello example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is hello blob container, example/data/Gutenberg is hello folder, and davinci.txt is hello blob.</span></span> |
| <span data-ttu-id="566d6-2986">output</span><span class="sxs-lookup"><span data-stu-id="566d6-2986">output</span></span> | <span data-ttu-id="566d6-2987">輸出檔 （包括位置） hello 減壓器。</span><span class="sxs-lookup"><span data-stu-id="566d6-2987">Output file (including location) for hello reducer.</span></span> <span data-ttu-id="566d6-2988">hello hello Hadoop 串流工作輸出寫入 toohello 針對此屬性指定的位置。</span><span class="sxs-lookup"><span data-stu-id="566d6-2988">hello output of hello Hadoop Streaming job is written toohello location specified for this property.</span></span> |
| <span data-ttu-id="566d6-2989">filePaths</span><span class="sxs-lookup"><span data-stu-id="566d6-2989">filePaths</span></span> | <span data-ttu-id="566d6-2990">Hello 對應工具和減壓器可執行檔的路徑。</span><span class="sxs-lookup"><span data-stu-id="566d6-2990">Paths for hello mapper and reducer executables.</span></span> <span data-ttu-id="566d6-2991">在 hello 範例:"adfsample/example/apps/wc.exe"，adfsample 是 hello blob 容器，example/apps 是 hello 資料夾和 wc.exe 是可執行檔的 hello。</span><span class="sxs-lookup"><span data-stu-id="566d6-2991">In hello example: "adfsample/example/apps/wc.exe", adfsample is hello blob container, example/apps is hello folder, and wc.exe is hello executable.</span></span> | 
| <span data-ttu-id="566d6-2992">fileLinkedService</span><span class="sxs-lookup"><span data-stu-id="566d6-2992">fileLinkedService</span></span> | <span data-ttu-id="566d6-2993">Azure 儲存體連結代表 hello hello hello filePaths 區段中指定的檔案所在的 Azure 儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="566d6-2993">Azure Storage linked service that represents hello Azure storage that contains hello files specified in hello filePaths section.</span></span> | 
| <span data-ttu-id="566d6-2994">arguments</span><span class="sxs-lookup"><span data-stu-id="566d6-2994">arguments</span></span> | <span data-ttu-id="566d6-2995">Hello MapReduce 程式以逗號分隔的引數清單。</span><span class="sxs-lookup"><span data-stu-id="566d6-2995">A list of comma-separated arguments for hello MapReduce program.</span></span> <span data-ttu-id="566d6-2996">在執行階段，您會看到幾個額外的引數 (例如： mapreduce.job.tags) 從 hello MapReduce 架構。</span><span class="sxs-lookup"><span data-stu-id="566d6-2996">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from hello MapReduce framework.</span></span> <span data-ttu-id="566d6-2997">toodifferentiate hello MapReduce 引數時，您的引數，請考慮使用選項和值做為引數中 hello 下列範例所示 (-s，-輸入、--輸出等，是後面緊跟著其值的選項)</span><span class="sxs-lookup"><span data-stu-id="566d6-2997">toodifferentiate your arguments with hello MapReduce arguments, consider using both option and value as arguments as shown in hello following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | 
| <span data-ttu-id="566d6-2998">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="566d6-2998">getDebugInfo</span></span> | <span data-ttu-id="566d6-2999">選擇性元素。</span><span class="sxs-lookup"><span data-stu-id="566d6-2999">An optional element.</span></span> <span data-ttu-id="566d6-3000">當它設定為 tooFailure 時，只在失敗下載 hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="566d6-3000">When it is set tooFailure, hello logs are downloaded only on failure.</span></span> <span data-ttu-id="566d6-3001">當它設定為 tooAll 時，無論 hello 執行狀態永遠下載記錄檔。</span><span class="sxs-lookup"><span data-stu-id="566d6-3001">When it is set tooAll, logs are always downloaded irrespective of hello execution status.</span></span> | 

> [!NOTE]
> <span data-ttu-id="566d6-3002">您必須指定 hello Hadoop 資料流活動的輸出資料集**輸出**屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-3002">You must specify an output dataset for hello Hadoop Streaming Activity for hello **outputs** property.</span></span> <span data-ttu-id="566d6-3003">此資料集可以是只的空資料集是必要的 toodrive hello 管線排程 （每小時、 每天、 等等）。</span><span class="sxs-lookup"><span data-stu-id="566d6-3003">This dataset can be just a dummy dataset that is required toodrive hello pipeline schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="566d6-3004">如果 hello 活動不接受輸入，您可以略過指定 hello 活動的輸入資料集**輸入**屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-3004">If hello activity doesn't take an input, you can skip specifying an input dataset for hello activity for hello **inputs** property.</span></span>  

## <a name="json-example"></a><span data-ttu-id="566d6-3005">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="566d6-3005">JSON example</span></span>

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

<span data-ttu-id="566d6-3006">如需詳細資訊，請參閱 [Hadoop 串流活動](data-factory-hadoop-streaming-activity.md)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-3006">For more information, see [Hadoop Streaming Activity](data-factory-hadoop-streaming-activity.md) article.</span></span> 

## <a name="hdinsight-spark-activity"></a><span data-ttu-id="566d6-3007">HDInsight Spark 活動</span><span class="sxs-lookup"><span data-stu-id="566d6-3007">HDInsight Spark Activity</span></span>
<span data-ttu-id="566d6-3008">您可以指定下列屬性的 Spark 活動 JSON 定義中的 hello。</span><span class="sxs-lookup"><span data-stu-id="566d6-3008">You can specify hello following properties in a Spark Activity JSON definition.</span></span> <span data-ttu-id="566d6-3009">hello hello 活動的型別屬性必須是： **HDInsightSpark**。</span><span class="sxs-lookup"><span data-stu-id="566d6-3009">hello type property for hello activity must be: **HDInsightSpark**.</span></span> <span data-ttu-id="566d6-3010">您必須先建立 HDInsight 連結服務，並指定它 hello 名稱做為 hello 值**linkedServiceName**屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-3010">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="566d6-3011">hello 支援下列屬性在 hello **typeProperties**區段，當您設定活動 tooHDInsightSpark hello 類型：</span><span class="sxs-lookup"><span data-stu-id="566d6-3011">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightSpark:</span></span> 

| <span data-ttu-id="566d6-3012">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-3012">Property</span></span> | <span data-ttu-id="566d6-3013">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-3013">Description</span></span> | <span data-ttu-id="566d6-3014">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-3014">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="566d6-3015">rootPath</span><span class="sxs-lookup"><span data-stu-id="566d6-3015">rootPath</span></span> | <span data-ttu-id="566d6-3016">hello Azure Blob 容器，並包含 hello Spark 檔案的資料夾。</span><span class="sxs-lookup"><span data-stu-id="566d6-3016">hello Azure Blob container and folder that contains hello Spark file.</span></span> <span data-ttu-id="566d6-3017">hello 檔案名稱是區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="566d6-3017">hello file name is case-sensitive.</span></span> | <span data-ttu-id="566d6-3018">是</span><span class="sxs-lookup"><span data-stu-id="566d6-3018">Yes</span></span> |
| <span data-ttu-id="566d6-3019">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="566d6-3019">entryFilePath</span></span> | <span data-ttu-id="566d6-3020">相對路徑 toohello 的 hello Spark 程式碼/封裝的根資料夾。</span><span class="sxs-lookup"><span data-stu-id="566d6-3020">Relative path toohello root folder of hello Spark code/package.</span></span> | <span data-ttu-id="566d6-3021">是</span><span class="sxs-lookup"><span data-stu-id="566d6-3021">Yes</span></span> |
| <span data-ttu-id="566d6-3022">className</span><span class="sxs-lookup"><span data-stu-id="566d6-3022">className</span></span> | <span data-ttu-id="566d6-3023">應用程式的 Java/Spark 主要類別</span><span class="sxs-lookup"><span data-stu-id="566d6-3023">Application's Java/Spark main class</span></span> | <span data-ttu-id="566d6-3024">否</span><span class="sxs-lookup"><span data-stu-id="566d6-3024">No</span></span> | 
| <span data-ttu-id="566d6-3025">arguments</span><span class="sxs-lookup"><span data-stu-id="566d6-3025">arguments</span></span> | <span data-ttu-id="566d6-3026">命令列引數 toohello Spark 程式的清單。</span><span class="sxs-lookup"><span data-stu-id="566d6-3026">A list of command-line arguments toohello Spark program.</span></span> | <span data-ttu-id="566d6-3027">否</span><span class="sxs-lookup"><span data-stu-id="566d6-3027">No</span></span> | 
| <span data-ttu-id="566d6-3028">proxyUser</span><span class="sxs-lookup"><span data-stu-id="566d6-3028">proxyUser</span></span> | <span data-ttu-id="566d6-3029">hello 使用者帳戶 tooimpersonate tooexecute hello Spark 程式</span><span class="sxs-lookup"><span data-stu-id="566d6-3029">hello user account tooimpersonate tooexecute hello Spark program</span></span> | <span data-ttu-id="566d6-3030">否</span><span class="sxs-lookup"><span data-stu-id="566d6-3030">No</span></span> | 
| <span data-ttu-id="566d6-3031">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="566d6-3031">sparkConfig</span></span> | <span data-ttu-id="566d6-3032">Spark 組態屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-3032">Spark configuration properties.</span></span> | <span data-ttu-id="566d6-3033">否</span><span class="sxs-lookup"><span data-stu-id="566d6-3033">No</span></span> | 
| <span data-ttu-id="566d6-3034">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="566d6-3034">getDebugInfo</span></span> | <span data-ttu-id="566d6-3035">指定當 hello Spark 記錄檔會複製的 toohello HDInsight 叢集所使用的 Azure 儲存體 （或） sparkJobLinkedService 所指定。</span><span class="sxs-lookup"><span data-stu-id="566d6-3035">Specifies when hello Spark log files are copied toohello Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="566d6-3036">允許的值︰None、Always 或 Failure。</span><span class="sxs-lookup"><span data-stu-id="566d6-3036">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="566d6-3037">預設值：None。</span><span class="sxs-lookup"><span data-stu-id="566d6-3037">Default value: None.</span></span> | <span data-ttu-id="566d6-3038">否</span><span class="sxs-lookup"><span data-stu-id="566d6-3038">No</span></span> | 
| <span data-ttu-id="566d6-3039">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="566d6-3039">sparkJobLinkedService</span></span> | <span data-ttu-id="566d6-3040">hello Azure 儲存體連結服務的 hello Spark 工作檔案、 相依性，以及記錄檔。</span><span class="sxs-lookup"><span data-stu-id="566d6-3040">hello Azure Storage linked service that holds hello Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="566d6-3041">如果您未指定此屬性的值，則會使用 hello 與 HDInsight 叢集相關聯的儲存體。</span><span class="sxs-lookup"><span data-stu-id="566d6-3041">If you do not specify a value for this property, hello storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="566d6-3042">否</span><span class="sxs-lookup"><span data-stu-id="566d6-3042">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="566d6-3043">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="566d6-3043">JSON example</span></span>

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
<span data-ttu-id="566d6-3044">請注意下列點 hello:</span><span class="sxs-lookup"><span data-stu-id="566d6-3044">Note hello following points:</span></span> 

- <span data-ttu-id="566d6-3045">hello**類型**屬性設定太**HDInsightSpark**。</span><span class="sxs-lookup"><span data-stu-id="566d6-3045">hello **type** property is set too**HDInsightSpark**.</span></span>
- <span data-ttu-id="566d6-3046">hello **rootPath**設定得**adfspark\\pyFiles** adfspark 所在 hello Azure Blob 容器和 pyFiles 是正常的資料夾，該容器中。</span><span class="sxs-lookup"><span data-stu-id="566d6-3046">hello **rootPath** is set too**adfspark\\pyFiles** where adfspark is hello Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="566d6-3047">在此範例中，hello Azure Blob 儲存體是 hello 與 hello Spark 叢集相關聯的其中一個。</span><span class="sxs-lookup"><span data-stu-id="566d6-3047">In this example, hello Azure Blob Storage is hello one that is associated with hello Spark cluster.</span></span> <span data-ttu-id="566d6-3048">您可以上傳 hello 檔案 tooa 不同的 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="566d6-3048">You can upload hello file tooa different Azure Storage.</span></span> <span data-ttu-id="566d6-3049">如果您這樣做，請建立 Azure 儲存體連結服務 toolink 該儲存體帳戶 toohello 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="566d6-3049">If you do so, create an Azure Storage linked service toolink that storage account toohello data factory.</span></span> <span data-ttu-id="566d6-3050">然後，指定 hello hello 連結服務名稱做為 hello 值**sparkJobLinkedService**屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-3050">Then, specify hello name of hello linked service as a value for hello **sparkJobLinkedService** property.</span></span> <span data-ttu-id="566d6-3051">請參閱[Spark 活動屬性](#spark-activity-properties)如需詳細資訊，這個屬性，而且支援 hello Spark 活動的其他內容。</span><span class="sxs-lookup"><span data-stu-id="566d6-3051">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by hello Spark Activity.</span></span>
- <span data-ttu-id="566d6-3052">hello **entryFilePath**設定 toohello **test.py**，這是 hello python 檔案。</span><span class="sxs-lookup"><span data-stu-id="566d6-3052">hello **entryFilePath** is set toohello **test.py**, which is hello python file.</span></span> 
- <span data-ttu-id="566d6-3053">hello **getDebugInfo**屬性設定太**永遠**，這表示 hello 記錄檔一律會產生 （成功或失敗）。</span><span class="sxs-lookup"><span data-stu-id="566d6-3053">hello **getDebugInfo** property is set too**Always**, which means hello log files are always generated (success or failure).</span></span>  

    > [!IMPORTANT]
    > <span data-ttu-id="566d6-3054">我們建議您沒有設定這個屬性 tooAlways 加在生產環境中，除非您疑難排解問題。</span><span class="sxs-lookup"><span data-stu-id="566d6-3054">We recommend that you do not set this property tooAlways in a production environment unless you are troubleshooting an issue.</span></span> 
- <span data-ttu-id="566d6-3055">hello**輸出**區段具有一個輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="566d6-3055">hello **outputs** section has one output dataset.</span></span> <span data-ttu-id="566d6-3056">您必須指定輸出資料集，即使 hello spark 程式不會產生任何輸出。</span><span class="sxs-lookup"><span data-stu-id="566d6-3056">You must specify an output dataset even if hello spark program does not produce any output.</span></span> <span data-ttu-id="566d6-3057">hello 輸出資料集的磁碟機 hello 排程 hello 管線 （每小時、 每天、 等等）。</span><span class="sxs-lookup"><span data-stu-id="566d6-3057">hello output dataset drives hello schedule for hello pipeline (hourly, daily, etc.).</span></span>

<span data-ttu-id="566d6-3058">如需 hello 活動的詳細資訊，請參閱[Spark 活動](data-factory-spark.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="566d6-3058">For more information about hello activity, see [Spark Activity](data-factory-spark.md) article.</span></span>  

## <a name="machine-learning-batch-execution-activity"></a><span data-ttu-id="566d6-3059">Machine Learning 批次執行活動</span><span class="sxs-lookup"><span data-stu-id="566d6-3059">Machine Learning Batch Execution Activity</span></span>
<span data-ttu-id="566d6-3060">您可以指定下列屬性，Azure ML 批次執行活動 JSON 定義中的 hello。</span><span class="sxs-lookup"><span data-stu-id="566d6-3060">You can specify hello following properties in a Azure ML Batch Execution Activity JSON definition.</span></span> <span data-ttu-id="566d6-3061">hello hello 活動的型別屬性必須是： **AzureMLBatchExecution**。</span><span class="sxs-lookup"><span data-stu-id="566d6-3061">hello type property for hello activity must be: **AzureMLBatchExecution**.</span></span> <span data-ttu-id="566d6-3062">您必須建立 Azure 機器學習連結的服務第一次，並指定做為 hello 值的 hello 目的**linkedServiceName**屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-3062">You must create a Azure Machine Learning linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="566d6-3063">hello 支援下列屬性在 hello **typeProperties**區段，當您設定活動 tooAzureMLBatchExecution hello 類型：</span><span class="sxs-lookup"><span data-stu-id="566d6-3063">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooAzureMLBatchExecution:</span></span>

<span data-ttu-id="566d6-3064">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-3064">Property</span></span> | <span data-ttu-id="566d6-3065">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-3065">Description</span></span> | <span data-ttu-id="566d6-3066">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-3066">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="566d6-3067">webServiceInput</span><span class="sxs-lookup"><span data-stu-id="566d6-3067">webServiceInput</span></span> | <span data-ttu-id="566d6-3068">hello 資料集 toobe 傳遞做為輸入 hello Azure ML web 服務。</span><span class="sxs-lookup"><span data-stu-id="566d6-3068">hello dataset toobe passed as an input for hello Azure ML web service.</span></span> <span data-ttu-id="566d6-3069">此資料集也必須包含 hello 輸入 hello 活動中。</span><span class="sxs-lookup"><span data-stu-id="566d6-3069">This dataset must also be included in hello inputs for hello activity.</span></span> |<span data-ttu-id="566d6-3070">使用 webServiceInput 或 webServiceInputs。</span><span class="sxs-lookup"><span data-stu-id="566d6-3070">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="566d6-3071">webServiceInputs</span><span class="sxs-lookup"><span data-stu-id="566d6-3071">webServiceInputs</span></span> | <span data-ttu-id="566d6-3072">指定資料集 toobe 傳遞做為輸入 hello Azure ML web 服務。</span><span class="sxs-lookup"><span data-stu-id="566d6-3072">Specify datasets toobe passed as inputs for hello Azure ML web service.</span></span> <span data-ttu-id="566d6-3073">如果 hello web 服務接受多個輸入，使用 hello webServiceInputs 屬性而不是使用 hello webServiceInput 屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-3073">If hello web service takes multiple inputs, use hello webServiceInputs property instead of using hello webServiceInput property.</span></span> <span data-ttu-id="566d6-3074">資料集所參考的 hello **webServiceInputs**也必須包含在 hello 活動**輸入**。</span><span class="sxs-lookup"><span data-stu-id="566d6-3074">Datasets that are referenced by hello **webServiceInputs** must also be included in hello Activity **inputs**.</span></span> | <span data-ttu-id="566d6-3075">使用 webServiceInput 或 webServiceInputs。</span><span class="sxs-lookup"><span data-stu-id="566d6-3075">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="566d6-3076">webServiceOutputs</span><span class="sxs-lookup"><span data-stu-id="566d6-3076">webServiceOutputs</span></span> | <span data-ttu-id="566d6-3077">已被指派為輸出 hello Azure ML web 服務的 hello 資料集。</span><span class="sxs-lookup"><span data-stu-id="566d6-3077">hello datasets that are assigned as outputs for hello Azure ML web service.</span></span> <span data-ttu-id="566d6-3078">hello web 服務傳回此資料集的輸出資料。</span><span class="sxs-lookup"><span data-stu-id="566d6-3078">hello web service returns output data in this dataset.</span></span> | <span data-ttu-id="566d6-3079">是</span><span class="sxs-lookup"><span data-stu-id="566d6-3079">Yes</span></span> | 
<span data-ttu-id="566d6-3080">globalParameters</span><span class="sxs-lookup"><span data-stu-id="566d6-3080">globalParameters</span></span> | <span data-ttu-id="566d6-3081">在此區段指定 hello web 服務參數的值。</span><span class="sxs-lookup"><span data-stu-id="566d6-3081">Specify values for hello web service parameters in this section.</span></span> | <span data-ttu-id="566d6-3082">否</span><span class="sxs-lookup"><span data-stu-id="566d6-3082">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="566d6-3083">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="566d6-3083">JSON example</span></span>
<span data-ttu-id="566d6-3084">在此範例中，hello 活動具有 hello 資料集**MLSqlInput**做為輸入和**MLSqlOutput**做為 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="566d6-3084">In this example, hello activity has hello dataset **MLSqlInput** as input and **MLSqlOutput** as hello output.</span></span> <span data-ttu-id="566d6-3085">hello **MLSqlInput**被當做輸入的 toohello web 服務，方法是使用 hello **webServiceInput** JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-3085">hello **MLSqlInput** is passed as an input toohello web service by using hello **webServiceInput** JSON property.</span></span> <span data-ttu-id="566d6-3086">hello **MLSqlOutput**被當做輸出 toohello Web 服務，方法是使用 hello **webServiceOutputs** JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-3086">hello **MLSqlOutput** is passed as an output toohello Web service by using hello **webServiceOutputs** JSON property.</span></span> 

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

<span data-ttu-id="566d6-3087">在 hello JSON 範例中，hello 部署 Azure 機器學習 Web 服務會使用讀取器和寫入器模組 tooread/寫入資料，從 / tooan Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="566d6-3087">In hello JSON example, hello deployed Azure Machine Learning Web service uses a reader and a writer module tooread/write data from/tooan Azure SQL Database.</span></span> <span data-ttu-id="566d6-3088">此 Web 服務會公開下列四個參數的 hello： 資料庫伺服器名稱、 資料庫名稱、 伺服器使用者帳戶名稱，以及伺服器的使用者帳戶密碼。</span><span class="sxs-lookup"><span data-stu-id="566d6-3088">This Web service exposes hello following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>

> [!NOTE]
> <span data-ttu-id="566d6-3089">只有輸入及輸出的 hello AzureMLBatchExecution 活動可以傳遞為參數 toohello Web 服務。</span><span class="sxs-lookup"><span data-stu-id="566d6-3089">Only inputs and outputs of hello AzureMLBatchExecution activity can be passed as parameters toohello Web service.</span></span> <span data-ttu-id="566d6-3090">例如，在 JSON 片段上方 hello，MLSqlInput 是輸入的 toohello AzureMLBatchExecution 活動，以透過 webServiceInput 參數當做輸入的 toohello Web 服務。</span><span class="sxs-lookup"><span data-stu-id="566d6-3090">For example, in hello above JSON snippet, MLSqlInput is an input toohello AzureMLBatchExecution activity, which is passed as an input toohello Web service via webServiceInput parameter.</span></span>

## <a name="machine-learning-update-resource-activity"></a><span data-ttu-id="566d6-3091">Machine Learning 更新資源活動</span><span class="sxs-lookup"><span data-stu-id="566d6-3091">Machine Learning Update Resource Activity</span></span>
<span data-ttu-id="566d6-3092">您可以指定下列屬性，Azure ML 更新資源活動 JSON 定義中的 hello。</span><span class="sxs-lookup"><span data-stu-id="566d6-3092">You can specify hello following properties in a Azure ML Update Resource Activity JSON definition.</span></span> <span data-ttu-id="566d6-3093">hello hello 活動的型別屬性必須是： **AzureMLUpdateResource**。</span><span class="sxs-lookup"><span data-stu-id="566d6-3093">hello type property for hello activity must be: **AzureMLUpdateResource**.</span></span> <span data-ttu-id="566d6-3094">您必須建立 Azure 機器學習連結的服務第一次，並指定做為 hello 值的 hello 目的**linkedServiceName**屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-3094">You must create a Azure Machine Learning linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="566d6-3095">hello 支援下列屬性在 hello **typeProperties**區段，當您設定活動 tooAzureMLUpdateResource hello 類型：</span><span class="sxs-lookup"><span data-stu-id="566d6-3095">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooAzureMLUpdateResource:</span></span>

<span data-ttu-id="566d6-3096">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-3096">Property</span></span> | <span data-ttu-id="566d6-3097">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-3097">Description</span></span> | <span data-ttu-id="566d6-3098">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-3098">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="566d6-3099">trainedModelName</span><span class="sxs-lookup"><span data-stu-id="566d6-3099">trainedModelName</span></span> | <span data-ttu-id="566d6-3100">Hello 的名稱重新定型模型。</span><span class="sxs-lookup"><span data-stu-id="566d6-3100">Name of hello retrained model.</span></span> | <span data-ttu-id="566d6-3101">是</span><span class="sxs-lookup"><span data-stu-id="566d6-3101">Yes</span></span> |  
<span data-ttu-id="566d6-3102">trainedModelDatasetName</span><span class="sxs-lookup"><span data-stu-id="566d6-3102">trainedModelDatasetName</span></span> | <span data-ttu-id="566d6-3103">資料集指標的 toohello ilearner 做為檔案，hello 定型作業所傳回。</span><span class="sxs-lookup"><span data-stu-id="566d6-3103">Dataset pointing toohello iLearner file returned by hello retraining operation.</span></span> | <span data-ttu-id="566d6-3104">是</span><span class="sxs-lookup"><span data-stu-id="566d6-3104">Yes</span></span> | 

### <a name="json-example"></a><span data-ttu-id="566d6-3105">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="566d6-3105">JSON example</span></span>
<span data-ttu-id="566d6-3106">hello 管線有兩個活動： **AzureMLBatchExecution**和**AzureMLUpdateResource**。</span><span class="sxs-lookup"><span data-stu-id="566d6-3106">hello pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="566d6-3107">hello Azure ML 批次執行的活動會接受做為輸入的 hello 定型資料，並產生 ilearner 做為檔案，做為輸出。</span><span class="sxs-lookup"><span data-stu-id="566d6-3107">hello Azure ML Batch Execution activity takes hello training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="566d6-3108">hello 活動與 hello 輸入培訓資料叫用 hello 訓練 web 服務 （定型實驗公開為 web 服務），並從 hello webservice 接收 hello ilearner 做為檔。</span><span class="sxs-lookup"><span data-stu-id="566d6-3108">hello activity invokes hello training web service (training experiment exposed as a web service) with hello input training data and receives hello ilearner file from hello webservice.</span></span> <span data-ttu-id="566d6-3109">hello placeholderBlob 是所需的 hello Azure Data Factory 服務 toorun hello 管線只要 dummy 輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="566d6-3109">hello placeholderBlob is just a dummy output dataset that is required by hello Azure Data Factory service toorun hello pipeline.</span></span>


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

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="566d6-3110">Data Lake Analytics U-SQL 活動</span><span class="sxs-lookup"><span data-stu-id="566d6-3110">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="566d6-3111">您可以指定下列屬性 U-SQL 活動 JSON 定義中的 hello。</span><span class="sxs-lookup"><span data-stu-id="566d6-3111">You can specify hello following properties in a U-SQL Activity JSON definition.</span></span> <span data-ttu-id="566d6-3112">hello hello 活動的型別屬性必須是： **DataLakeAnalyticsU SQL**。</span><span class="sxs-lookup"><span data-stu-id="566d6-3112">hello type property for hello activity must be: **DataLakeAnalyticsU-SQL**.</span></span> <span data-ttu-id="566d6-3113">您必須建立連結的 Azure 資料湖分析服務，並指定它 hello 名稱做為 hello 值**linkedServiceName**屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-3113">You must create an Azure Data Lake Analytics linked service and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="566d6-3114">hello 支援下列屬性在 hello **typeProperties**區段，當您設定活動 tooDataLakeAnalyticsU SQL hello 類型：</span><span class="sxs-lookup"><span data-stu-id="566d6-3114">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooDataLakeAnalyticsU-SQL:</span></span> 

| <span data-ttu-id="566d6-3115">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-3115">Property</span></span> | <span data-ttu-id="566d6-3116">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-3116">Description</span></span> | <span data-ttu-id="566d6-3117">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-3117">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="566d6-3118">scriptPath</span><span class="sxs-lookup"><span data-stu-id="566d6-3118">scriptPath</span></span> |<span data-ttu-id="566d6-3119">路徑 toofolder 包含 hello U-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="566d6-3119">Path toofolder that contains hello U-SQL script.</span></span> <span data-ttu-id="566d6-3120">Hello 檔案的名稱會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="566d6-3120">Name of hello file is case-sensitive.</span></span> |<span data-ttu-id="566d6-3121">否 (如果您使用指令碼)</span><span class="sxs-lookup"><span data-stu-id="566d6-3121">No (if you use script)</span></span> |
| <span data-ttu-id="566d6-3122">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="566d6-3122">scriptLinkedService</span></span> |<span data-ttu-id="566d6-3123">連結包含 hello 指令碼 toohello 資料 factory 的 hello 儲存體連結的服務</span><span class="sxs-lookup"><span data-stu-id="566d6-3123">Linked service that links hello storage that contains hello script toohello data factory</span></span> |<span data-ttu-id="566d6-3124">否 (如果您使用指令碼)</span><span class="sxs-lookup"><span data-stu-id="566d6-3124">No (if you use script)</span></span> |
| <span data-ttu-id="566d6-3125">script</span><span class="sxs-lookup"><span data-stu-id="566d6-3125">script</span></span> |<span data-ttu-id="566d6-3126">指定內嵌指令碼而不是指定 scriptPath 和 scriptLinkedService。</span><span class="sxs-lookup"><span data-stu-id="566d6-3126">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="566d6-3127">例如："script": "CREATE DATABASE test"。</span><span class="sxs-lookup"><span data-stu-id="566d6-3127">For example: "script": "CREATE DATABASE test".</span></span> |<span data-ttu-id="566d6-3128">否 (如果您使用 scriptPath 和 scriptLinkedService)</span><span class="sxs-lookup"><span data-stu-id="566d6-3128">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="566d6-3129">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="566d6-3129">degreeOfParallelism</span></span> |<span data-ttu-id="566d6-3130">hello 的節點數目上限，同時使用 toorun hello 作業。</span><span class="sxs-lookup"><span data-stu-id="566d6-3130">hello maximum number of nodes simultaneously used toorun hello job.</span></span> |<span data-ttu-id="566d6-3131">否</span><span class="sxs-lookup"><span data-stu-id="566d6-3131">No</span></span> |
| <span data-ttu-id="566d6-3132">優先順序</span><span class="sxs-lookup"><span data-stu-id="566d6-3132">priority</span></span> |<span data-ttu-id="566d6-3133">決定從所有已排入佇列的作業應該選取的 toorun 第一次。</span><span class="sxs-lookup"><span data-stu-id="566d6-3133">Determines which jobs out of all that are queued should be selected toorun first.</span></span> <span data-ttu-id="566d6-3134">hello 低 hello 數字，hello hello 優先順序越高。</span><span class="sxs-lookup"><span data-stu-id="566d6-3134">hello lower hello number, hello higher hello priority.</span></span> |<span data-ttu-id="566d6-3135">否</span><span class="sxs-lookup"><span data-stu-id="566d6-3135">No</span></span> |
| <span data-ttu-id="566d6-3136">參數</span><span class="sxs-lookup"><span data-stu-id="566d6-3136">parameters</span></span> |<span data-ttu-id="566d6-3137">Hello U-SQL 指令碼的參數</span><span class="sxs-lookup"><span data-stu-id="566d6-3137">Parameters for hello U-SQL script</span></span> |<span data-ttu-id="566d6-3138">否</span><span class="sxs-lookup"><span data-stu-id="566d6-3138">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="566d6-3139">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="566d6-3139">JSON example</span></span>

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

<span data-ttu-id="566d6-3140">如需詳細資訊，請參閱 [Data Lake Analytics U-SQL 活動](data-factory-usql-activity.md)。</span><span class="sxs-lookup"><span data-stu-id="566d6-3140">For more information, see [Data Lake Analytics U-SQL Activity](data-factory-usql-activity.md).</span></span> 

## <a name="stored-procedure-activity"></a><span data-ttu-id="566d6-3141">預存程序活動</span><span class="sxs-lookup"><span data-stu-id="566d6-3141">Stored Procedure Activity</span></span>
<span data-ttu-id="566d6-3142">您可以指定下列屬性的預存程序活動 JSON 定義中的 hello。</span><span class="sxs-lookup"><span data-stu-id="566d6-3142">You can specify hello following properties in a Stored Procedure Activity JSON definition.</span></span> <span data-ttu-id="566d6-3143">hello hello 活動的型別屬性必須是： **SqlServerStoredProcedure**。</span><span class="sxs-lookup"><span data-stu-id="566d6-3143">hello type property for hello activity must be: **SqlServerStoredProcedure**.</span></span> <span data-ttu-id="566d6-3144">您必須建立一個 hello 遵循連結的服務，並指定 hello hello 連結服務名稱做為 hello 值**linkedServiceName**屬性：</span><span class="sxs-lookup"><span data-stu-id="566d6-3144">You must create an one of hello following linked services and specify hello name of hello linked service as a value for hello **linkedServiceName** property:</span></span>

- <span data-ttu-id="566d6-3145">SQL Server</span><span class="sxs-lookup"><span data-stu-id="566d6-3145">SQL Server</span></span> 
- <span data-ttu-id="566d6-3146">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="566d6-3146">Azure SQL Database</span></span>
- <span data-ttu-id="566d6-3147">Azure SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="566d6-3147">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="566d6-3148">hello 支援下列屬性在 hello **typeProperties**區段，當您設定活動 tooSqlServerStoredProcedure hello 類型：</span><span class="sxs-lookup"><span data-stu-id="566d6-3148">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooSqlServerStoredProcedure:</span></span>

| <span data-ttu-id="566d6-3149">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-3149">Property</span></span> | <span data-ttu-id="566d6-3150">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-3150">Description</span></span> | <span data-ttu-id="566d6-3151">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-3151">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566d6-3152">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="566d6-3152">storedProcedureName</span></span> |<span data-ttu-id="566d6-3153">指定 hello Azure SQL database 或 Azure SQL 資料倉儲由 hello 輸出資料表中使用的 hello 連結服務中的 hello hello 預存程序名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-3153">Specify hello name of hello stored procedure in hello Azure SQL database or Azure SQL Data Warehouse that is represented by hello linked service that hello output table uses.</span></span> |<span data-ttu-id="566d6-3154">是</span><span class="sxs-lookup"><span data-stu-id="566d6-3154">Yes</span></span> |
| <span data-ttu-id="566d6-3155">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="566d6-3155">storedProcedureParameters</span></span> |<span data-ttu-id="566d6-3156">指定預存程序參數的值。</span><span class="sxs-lookup"><span data-stu-id="566d6-3156">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="566d6-3157">如果您需要 toopass null 參數，使用 hello 語法:"param1": null （所有大小寫）。</span><span class="sxs-lookup"><span data-stu-id="566d6-3157">If you need toopass null for a parameter, use hello syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="566d6-3158">請參閱下列有關使用這個屬性的範例 toolearn hello。</span><span class="sxs-lookup"><span data-stu-id="566d6-3158">See hello following sample toolearn about using this property.</span></span> |<span data-ttu-id="566d6-3159">否</span><span class="sxs-lookup"><span data-stu-id="566d6-3159">No</span></span> |

<span data-ttu-id="566d6-3160">如果您指定的輸入資料集，它必須可用 （處於 [就緒]' 的狀態） hello 預存程序活動 toorun。</span><span class="sxs-lookup"><span data-stu-id="566d6-3160">If you do specify an input dataset, it must be available (in ‘Ready’ status) for hello stored procedure activity toorun.</span></span> <span data-ttu-id="566d6-3161">hello 輸入資料集無法取用 hello 預存程序中，做為參數。</span><span class="sxs-lookup"><span data-stu-id="566d6-3161">hello input dataset cannot be consumed in hello stored procedure as a parameter.</span></span> <span data-ttu-id="566d6-3162">起始 hello 預存程序活動之前，它是只使用的 toocheck hello 相依性。</span><span class="sxs-lookup"><span data-stu-id="566d6-3162">It is only used toocheck hello dependency before starting hello stored procedure activity.</span></span> <span data-ttu-id="566d6-3163">您必須指定預存程序活動的輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="566d6-3163">You must specify an output dataset for a stored procedure activity.</span></span> 

<span data-ttu-id="566d6-3164">輸出資料集指定 hello**排程**hello 預存程序活動 （每小時、 每週、 每月等）。</span><span class="sxs-lookup"><span data-stu-id="566d6-3164">Output dataset specifies hello **schedule** for hello stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <span data-ttu-id="566d6-3165">hello 輸出資料集必須使用**連結服務**參考 tooan Azure SQL Database 或 Azure SQL 資料倉儲或您想在其中 hello toorun 預存程序的 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="566d6-3165">hello output dataset must use a **linked service** that refers tooan Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want hello stored procedure toorun.</span></span> <span data-ttu-id="566d6-3166">hello 輸出資料集可以做為方法 toopass hello hello 預存程序的結果進行後續處理另一個活動 ([鏈結活動](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) hello 管線中。</span><span class="sxs-lookup"><span data-stu-id="566d6-3166">hello output dataset can serve as a way toopass hello result of hello stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) in hello pipeline.</span></span> <span data-ttu-id="566d6-3167">不過，Data Factory 不會自動寫入預存程序 toothis 資料集的 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="566d6-3167">However, Data Factory does not automatically write hello output of a stored procedure toothis dataset.</span></span> <span data-ttu-id="566d6-3168">它是 hello 預存程序 hello 輸出資料集指向該寫入 tooa SQL 資料表。</span><span class="sxs-lookup"><span data-stu-id="566d6-3168">It is hello stored procedure that writes tooa SQL table that hello output dataset points to.</span></span> <span data-ttu-id="566d6-3169">在某些情況下，可以是 hello 輸出資料集**空資料集**，用僅執行 hello toospecify hello 排程預存程序活動。</span><span class="sxs-lookup"><span data-stu-id="566d6-3169">In some cases, hello output dataset can be a **dummy dataset**, which is used only toospecify hello schedule for running hello stored procedure activity.</span></span>  

### <a name="json-example"></a><span data-ttu-id="566d6-3170">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="566d6-3170">JSON example</span></span>

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

<span data-ttu-id="566d6-3171">如需詳細資訊，請參閱[預存程序活動](data-factory-stored-proc-activity.md)。</span><span class="sxs-lookup"><span data-stu-id="566d6-3171">For more information, see [Stored Procedure Activity](data-factory-stored-proc-activity.md) article.</span></span> 

## <a name="net-custom-activity"></a><span data-ttu-id="566d6-3172">.NET 自訂活動</span><span class="sxs-lookup"><span data-stu-id="566d6-3172">.NET custom activity</span></span>
<span data-ttu-id="566d6-3173">您可以指定下列屬性.NET 自訂活動 JSON 定義中的 hello。</span><span class="sxs-lookup"><span data-stu-id="566d6-3173">You can specify hello following properties in a .NET custom activity JSON definition.</span></span> <span data-ttu-id="566d6-3174">hello hello 活動的型別屬性必須是： **DotNetActivity**。</span><span class="sxs-lookup"><span data-stu-id="566d6-3174">hello type property for hello activity must be: **DotNetActivity**.</span></span> <span data-ttu-id="566d6-3175">您必須建立 Azure HDInsight 連結服務或 Azure 批次連結服務，並指定 hello hello 連結服務名稱做為 hello 值**linkedServiceName**屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-3175">You must create an Azure HDInsight linked service or an Azure Batch linked service, and specify hello name of hello linked service as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="566d6-3176">hello 支援下列屬性在 hello **typeProperties**區段，當您設定活動 tooDotNetActivity hello 類型：</span><span class="sxs-lookup"><span data-stu-id="566d6-3176">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooDotNetActivity:</span></span>
 
| <span data-ttu-id="566d6-3177">屬性</span><span class="sxs-lookup"><span data-stu-id="566d6-3177">Property</span></span> | <span data-ttu-id="566d6-3178">說明</span><span class="sxs-lookup"><span data-stu-id="566d6-3178">Description</span></span> | <span data-ttu-id="566d6-3179">必要</span><span class="sxs-lookup"><span data-stu-id="566d6-3179">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="566d6-3180">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="566d6-3180">AssemblyName</span></span> | <span data-ttu-id="566d6-3181">Hello 組件名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-3181">Name of hello assembly.</span></span> <span data-ttu-id="566d6-3182">在 hello 範例很： **MyDotnetActivity.dll**。</span><span class="sxs-lookup"><span data-stu-id="566d6-3182">In hello example, it is: **MyDotnetActivity.dll**.</span></span> | <span data-ttu-id="566d6-3183">是</span><span class="sxs-lookup"><span data-stu-id="566d6-3183">Yes</span></span> |
| <span data-ttu-id="566d6-3184">EntryPoint</span><span class="sxs-lookup"><span data-stu-id="566d6-3184">EntryPoint</span></span> |<span data-ttu-id="566d6-3185">Hello 類別可實作 hello IDotNetActivity 介面的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-3185">Name of hello class that implements hello IDotNetActivity interface.</span></span> <span data-ttu-id="566d6-3186">在 hello 範例很： **MyDotNetActivityNS.MyDotNetActivity**其中 MyDotNetActivityNS 是 hello 命名空間且 MyDotNetActivity hello 類別。</span><span class="sxs-lookup"><span data-stu-id="566d6-3186">In hello example, it is: **MyDotNetActivityNS.MyDotNetActivity** where MyDotNetActivityNS is hello namespace and MyDotNetActivity is hello class.</span></span>  | <span data-ttu-id="566d6-3187">是</span><span class="sxs-lookup"><span data-stu-id="566d6-3187">Yes</span></span> | 
| <span data-ttu-id="566d6-3188">PackageLinkedService</span><span class="sxs-lookup"><span data-stu-id="566d6-3188">PackageLinkedService</span></span> | <span data-ttu-id="566d6-3189">Hello 點 toohello blob 儲存體包含 hello 自訂活動的 zip 檔案的 Azure 儲存體連結服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-3189">Name of hello Azure Storage linked service that points toohello blob storage that contains hello custom activity zip file.</span></span> <span data-ttu-id="566d6-3190">在 hello 範例很： **AzureStorageLinkedService**。</span><span class="sxs-lookup"><span data-stu-id="566d6-3190">In hello example, it is: **AzureStorageLinkedService**.</span></span>| <span data-ttu-id="566d6-3191">是</span><span class="sxs-lookup"><span data-stu-id="566d6-3191">Yes</span></span> |
| <span data-ttu-id="566d6-3192">PackageFile</span><span class="sxs-lookup"><span data-stu-id="566d6-3192">PackageFile</span></span> | <span data-ttu-id="566d6-3193">Hello zip 檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="566d6-3193">Name of hello zip file.</span></span> <span data-ttu-id="566d6-3194">在 hello 範例很： **customactivitycontainer/MyDotNetActivity.zip**。</span><span class="sxs-lookup"><span data-stu-id="566d6-3194">In hello example, it is: **customactivitycontainer/MyDotNetActivity.zip**.</span></span> | <span data-ttu-id="566d6-3195">是</span><span class="sxs-lookup"><span data-stu-id="566d6-3195">Yes</span></span> |
| <span data-ttu-id="566d6-3196">extendedProperties</span><span class="sxs-lookup"><span data-stu-id="566d6-3196">extendedProperties</span></span> | <span data-ttu-id="566d6-3197">您可以定義及傳遞 toohello.NET 程式碼的擴充的屬性。</span><span class="sxs-lookup"><span data-stu-id="566d6-3197">Extended properties that you can define and pass on toohello .NET code.</span></span> <span data-ttu-id="566d6-3198">在此範例中，hello **SliceStart**變數設定為 tooa 根據 hello SliceStart 系統變數的值。</span><span class="sxs-lookup"><span data-stu-id="566d6-3198">In this example, hello **SliceStart** variable is set tooa value based on hello SliceStart system variable.</span></span> | <span data-ttu-id="566d6-3199">否</span><span class="sxs-lookup"><span data-stu-id="566d6-3199">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="566d6-3200">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="566d6-3200">JSON example</span></span>

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

<span data-ttu-id="566d6-3201">如需詳細資訊，請參閱[在 Data Factory 中使用自訂活動](data-factory-use-custom-activities.md)文件。</span><span class="sxs-lookup"><span data-stu-id="566d6-3201">For detailed information, see [Use custom activities in Data Factory](data-factory-use-custom-activities.md) article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="566d6-3202">後續步驟</span><span class="sxs-lookup"><span data-stu-id="566d6-3202">Next Steps</span></span>
<span data-ttu-id="566d6-3203">請參閱下列教學課程的 hello:</span><span class="sxs-lookup"><span data-stu-id="566d6-3203">See hello following tutorials:</span></span> 

- [<span data-ttu-id="566d6-3204">教學課程：建立具有複製活動的管線</span><span class="sxs-lookup"><span data-stu-id="566d6-3204">Tutorial: create a pipeline with a copy activity</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
- [<span data-ttu-id="566d6-3205">教學課程：建立具有 Hive 活動的管線</span><span class="sxs-lookup"><span data-stu-id="566d6-3205">Tutorial: create a pipeline with a hive activity</span></span>](data-factory-build-your-first-pipeline-using-editor.md)