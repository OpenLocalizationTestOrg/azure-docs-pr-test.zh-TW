---
title: "在串流分析中使用參考資料和查閱資料表 | Microsoft Docs"
description: "在串流分析查詢中使用參考資料"
keywords: "查閱資料表, 參考資料"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 06103be5-553a-4da1-8a8d-3be9ca2aff54
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 3fd9c869be68d624a59ffb09ee53e31cd5a2f71b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="using-reference-data-or-lookup-tables-in-a-stream-analytics-input-stream"></a><span data-ttu-id="824d4-104">在串流分析的輸入串流中使用參考資料或查詢資料表</span><span class="sxs-lookup"><span data-stu-id="824d4-104">Using reference data or lookup tables in a Stream Analytics input stream</span></span>
<span data-ttu-id="824d4-105">參考資料 (也稱為查詢資料表) 基本上是靜態或不常變更的有限資料集，可用來執行查閱或與資料流相互關聯。</span><span class="sxs-lookup"><span data-stu-id="824d4-105">Reference data (also known as a lookup table) is a finite data set that is static or slowing changing in nature, used to perform a lookup or to correlate with your data stream.</span></span> <span data-ttu-id="824d4-106">若要使用 Azure 串流分析作業中的參考資料，您通常會在查詢中使用[參考資料聯結](https://msdn.microsoft.com/library/azure/dn949258.aspx)。</span><span class="sxs-lookup"><span data-stu-id="824d4-106">To make use of reference data in your Azure Stream Analytics job, you will generally use a [Reference Data Join](https://msdn.microsoft.com/library/azure/dn949258.aspx) in your Query.</span></span> <span data-ttu-id="824d4-107">串流分析會使用 Azure Blob 儲存體做為參考資料的儲存層，且可和 Azure Data Factory 參考資料一起轉換和/或複製到來自 [任意數目的雲端架構和內部部署資料存放區](../data-factory/data-factory-data-movement-activities.md)的 Azure Blob 儲存體，做為參考資料。</span><span class="sxs-lookup"><span data-stu-id="824d4-107">Stream Analytics uses Azure Blob storage as the storage layer for Reference Data, and with Azure Data Factory reference data can be transformed and/or copied to Azure Blob storage, for use as Reference Data, from [any number of cloud-based and on-premises data stores](../data-factory/data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="824d4-108">參考資料會依 Blob 名稱中指定之日期/時間的遞增順序，以 Blob 序列的形式建立模型 (在輸入組態中定義)。</span><span class="sxs-lookup"><span data-stu-id="824d4-108">Reference data is modeled as a sequence of blobs (defined in the input configuration) in ascending order of the date/time specified in the blob name.</span></span> <span data-ttu-id="824d4-109">它「只」支援使用比序列中最後一個 Blob 指定之日期/時間「大」的日期/時間來新增到序列的結尾。</span><span class="sxs-lookup"><span data-stu-id="824d4-109">It **only** supports adding to the end of the sequence by using a date/time **greater** than the one specified by the last blob in the sequence.</span></span>

<span data-ttu-id="824d4-110">串流分析具有**每個 Bolb 100 MB 的限制**，但作業可以使用**路徑模式**屬性來存取多個參考 Blob。</span><span class="sxs-lookup"><span data-stu-id="824d4-110">Stream Analytics has a **limit of 100 MB per blob** but jobs can process multiple reference blobs by using the **path pattern** property.</span></span>


## <a name="configuring-reference-data"></a><span data-ttu-id="824d4-111">設定參考資料</span><span class="sxs-lookup"><span data-stu-id="824d4-111">Configuring reference data</span></span>
<span data-ttu-id="824d4-112">若要設定參考資料，您必須先建立屬於「 **參考資料**」類型的輸入。</span><span class="sxs-lookup"><span data-stu-id="824d4-112">To configure your reference data, you first need to create an input that is of type **Reference Data**.</span></span> <span data-ttu-id="824d4-113">下表說明您在建立參考資料輸入及其描述時必須提供的每個屬性：</span><span class="sxs-lookup"><span data-stu-id="824d4-113">The table below explains each property that you will need to provide while creating the reference data input with its description:</span></span>


<table>
<tbody>
<tr>
<td><span data-ttu-id="824d4-114">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="824d4-114">Property Name</span></span></td>
<td><span data-ttu-id="824d4-115">說明</span><span class="sxs-lookup"><span data-stu-id="824d4-115">Description</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="824d4-116">輸入別名</span><span class="sxs-lookup"><span data-stu-id="824d4-116">Input Alias</span></span></td>
<td><span data-ttu-id="824d4-117">在工作查詢中將用來參考這個輸入的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="824d4-117">A friendly name that will be used in the job query to reference this input.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="824d4-118">儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="824d4-118">Storage Account</span></span></td>
<td><span data-ttu-id="824d4-119">您 blob 所在的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="824d4-119">The name of the storage account where your blobs are located.</span></span> <span data-ttu-id="824d4-120">如果它與您的串流分析工作位於相同的訂用帳戶，您就可以從下拉式清單中選取它。</span><span class="sxs-lookup"><span data-stu-id="824d4-120">If it’s in the same subscription as your Stream Analytics Job, you can select it from the drop-down.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="824d4-121">儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="824d4-121">Storage Account Key</span></span></td>
<td><span data-ttu-id="824d4-122">與儲存體帳戶相關聯的密碼金鑰。</span><span class="sxs-lookup"><span data-stu-id="824d4-122">The secret key associated with the storage account.</span></span> <span data-ttu-id="824d4-123">如果儲存體帳戶與您的「串流分析」工作位於相同的訂用帳戶，就會自動填入此資訊。</span><span class="sxs-lookup"><span data-stu-id="824d4-123">This gets automatically populated if the storage account is in the same subscription as your Stream Analytics job.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="824d4-124">儲存體容器</span><span class="sxs-lookup"><span data-stu-id="824d4-124">Storage Container</span></span></td>
<td><span data-ttu-id="824d4-125">容器提供邏輯分組給儲存在 Microsoft Azure Blob 服務中的 blob。</span><span class="sxs-lookup"><span data-stu-id="824d4-125">Containers provide a logical grouping for blobs stored in the Microsoft Azure Blob service.</span></span> <span data-ttu-id="824d4-126">當您將 blob 上傳至 Blob 服務時，您必須指定該 blob 的容器。</span><span class="sxs-lookup"><span data-stu-id="824d4-126">When you upload a blob to the Blob service, you must specify a container for that blob.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="824d4-127">路徑格式</span><span class="sxs-lookup"><span data-stu-id="824d4-127">Path Pattern</span></span></td>
<td><span data-ttu-id="824d4-128">用來在指定容器中找出 blob 的路徑。</span><span class="sxs-lookup"><span data-stu-id="824d4-128">The path used to locate your blobs within the specified container.</span></span> <span data-ttu-id="824d4-129">在該路徑內，您也可以指定下列 2 個變數的一個或多個執行個體：</span><span class="sxs-lookup"><span data-stu-id="824d4-129">Within the path, you may choose to specify one or more instances of the following 2 variables:</span></span><BR><span data-ttu-id="824d4-130">{date}、{time}</span><span class="sxs-lookup"><span data-stu-id="824d4-130">{date}, {time}</span></span><BR><span data-ttu-id="824d4-131">範例 1：products/{date}/{time}/product-list.csv</span><span class="sxs-lookup"><span data-stu-id="824d4-131">Example 1: products/{date}/{time}/product-list.csv</span></span><BR><span data-ttu-id="824d4-132">範例 2：products/{date}/product-list.csv</span><span class="sxs-lookup"><span data-stu-id="824d4-132">Example 2: products/{date}/product-list.csv</span></span>
</tr>
<tr>
<td><span data-ttu-id="824d4-133">日期格式 [選用]</span><span class="sxs-lookup"><span data-stu-id="824d4-133">Date Format [optional]</span></span></td>
<td><span data-ttu-id="824d4-134">如果您已在指定的路徑模式內使用 {date}，則您可以從支援格式的下拉式清單中選取組織 Blob 所使用的日期格式。</span><span class="sxs-lookup"><span data-stu-id="824d4-134">If you have used {date} within the Path Pattern that you specified, then you can select the date format in which your blobs are organized from the drop-down of supported formats.</span></span><BR><span data-ttu-id="824d4-135">範例︰YYYY/MM/DD、MM/DD/YYYY 等。</span><span class="sxs-lookup"><span data-stu-id="824d4-135">Example: YYYY/MM/DD, MM/DD/YYYY, etc.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="824d4-136">時間格式 [選用]</span><span class="sxs-lookup"><span data-stu-id="824d4-136">Time Format [optional]</span></span></td>
<td><span data-ttu-id="824d4-137">如果您已在指定的路徑模式內使用 {time}，則您可以從支援格式的下拉式清單中選取組織 Blob 所使用的時間格式。</span><span class="sxs-lookup"><span data-stu-id="824d4-137">If you have used {time} within the Path Pattern that you specified, then you can select the time format in which your blobs are organized from the drop-down of supported formats.</span></span><BR><span data-ttu-id="824d4-138">範例︰HH、HH/mm 或 HH-mm</span><span class="sxs-lookup"><span data-stu-id="824d4-138">Example: HH, HH/mm, or HH-mm</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="824d4-139">事件序列化格式</span><span class="sxs-lookup"><span data-stu-id="824d4-139">Event Serialization Format</span></span></td>
<td><span data-ttu-id="824d4-140">為了確定您的查詢運作如預期，串流分析需要知道您的內送資料流使用哪一種序列化格式。</span><span class="sxs-lookup"><span data-stu-id="824d4-140">To make sure your queries work the way you expect, Stream Analytics needs to know which serialization format you're using for incoming data streams.</span></span> <span data-ttu-id="824d4-141">參考資料的支援格式為 CSV 和 JSON。</span><span class="sxs-lookup"><span data-stu-id="824d4-141">For Reference Data, the supported formats are CSV and JSON.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="824d4-142">編碼</span><span class="sxs-lookup"><span data-stu-id="824d4-142">Encoding</span></span></td>
<td><span data-ttu-id="824d4-143">UTF-8 是目前唯一支援的編碼格式</span><span class="sxs-lookup"><span data-stu-id="824d4-143">UTF-8 is the only supported encoding format at this time</span></span></td>
</tr>
</tbody>
</table>

## <a name="generating-reference-data-on-a-schedule"></a><span data-ttu-id="824d4-144">產生排程上的參考資料</span><span class="sxs-lookup"><span data-stu-id="824d4-144">Generating reference data on a schedule</span></span>
<span data-ttu-id="824d4-145">如果您的參考資料是不常變更的資料集，可以啟用重新整理參考資料的支援，方法是使用 {date} 與 {time} 替代權杖指定輸入設定內的路徑模式。</span><span class="sxs-lookup"><span data-stu-id="824d4-145">If your reference data is a slowly changing data set, then support for refreshing reference data is enabled by specifying a path pattern in the input configuration using the {date} and {time} substitution tokens.</span></span> <span data-ttu-id="824d4-146">串流分析會根據此路徑模式採用更新的參考資料定義。</span><span class="sxs-lookup"><span data-stu-id="824d4-146">Stream Analytics picks up the updated reference data definitions based on this path pattern.</span></span> <span data-ttu-id="824d4-147">例如，日期格式為 **“YYYY-MM-DD”** 且時間格式為 **“HH:mm”** 的模式 `sample/{date}/{time}/products.csv`，會指示串流分析在 UTC 時區 2015 年 4 月 16 日的下午 5:30 採用更新的 Blob `sample/2015-04-16/17-30/products.csv`。</span><span class="sxs-lookup"><span data-stu-id="824d4-147">For example, a pattern of `sample/{date}/{time}/products.csv` with a date format of **“YYYY-MM-DD”** and a time format of **“HH-mm”** instructs Stream Analytics to pick up the updated blob `sample/2015-04-16/17-30/products.csv` at 5:30 PM on April 16th, 2015 UTC time zone.</span></span>

> [!NOTE]
> <span data-ttu-id="824d4-148">目前串流分析作業只有在機器時間朝向 Blob 名稱中編碼的時間時，才會尋求 Blob 重新整理。</span><span class="sxs-lookup"><span data-stu-id="824d4-148">Currently Stream Analytics jobs look for the blob refresh only when the machine time advances to the time encoded in the blob name.</span></span> <span data-ttu-id="824d4-149">例如，作業會儘速尋找 `sample/2015-04-16/17-30/products.csv` ，但不早於 UTC 時區 2015 年 4 月 16 日的下午 5:30。</span><span class="sxs-lookup"><span data-stu-id="824d4-149">For example, the job will look for `sample/2015-04-16/17-30/products.csv` as soon as possible but no earlier than 5:30 PM on April 16th, 2015 UTC time zone.</span></span> <span data-ttu-id="824d4-150">它「決不會」尋找編碼時間早於最後一個探索到的 blob。</span><span class="sxs-lookup"><span data-stu-id="824d4-150">It will *never* look for a blob with an encoded time earlier than the last one that is discovered.</span></span>
> 
> <span data-ttu-id="824d4-151">例如</span><span class="sxs-lookup"><span data-stu-id="824d4-151">E.g.</span></span> <span data-ttu-id="824d4-152">一旦作業找到 Blob `sample/2015-04-16/17-30/products.csv`，就會忽略任何編碼日期早於 2015 年 4 月 16 日下午 5:30 的檔案，所以如果在相同的容器中建立晚到的 `sample/2015-04-16/17-25/products.csv` Blob，作業便不會使用它。</span><span class="sxs-lookup"><span data-stu-id="824d4-152">once the job finds the blob `sample/2015-04-16/17-30/products.csv` it will ignore any files with an encoded date earlier than 5:30 PM April 16th, 2015 so if a late arriving `sample/2015-04-16/17-25/products.csv` blob gets created in the same container the job will not use it.</span></span>
> 
> <span data-ttu-id="824d4-153">同樣地，如果 `sample/2015-04-16/17-30/products.csv` 只會在 2015 年 4 月 16 日下午 10:03 產生，但容器中沒有日期較早的 Blob，則作業會從 2015 年 4 月 16 日下午 10:03 開始使用這個檔案，並在那之前使用先前的參考資料。</span><span class="sxs-lookup"><span data-stu-id="824d4-153">Likewise if `sample/2015-04-16/17-30/products.csv` is only produced at 10:03 PM April 16th, 2015 but no blob with an earlier date is present in the container, the job will use this file starting at 10:03 PM April 16th, 2015 and use the previous reference data until then.</span></span>
> 
> <span data-ttu-id="824d4-154">此情況有例外，就是當工作需要回到之前來重新處理資料，或當工作第一次啟動的時候。</span><span class="sxs-lookup"><span data-stu-id="824d4-154">An exception to this is when the job needs to re-process data back in time or when the job is first started.</span></span> <span data-ttu-id="824d4-155">啟動時，作業會尋找在指定作業啟動時間之前產生的最新 Blob。</span><span class="sxs-lookup"><span data-stu-id="824d4-155">At start time the job is looking for the most recent blob produced before the job start time specified.</span></span> <span data-ttu-id="824d4-156">這是為了確保在作業啟動時，會有 **非空白** 的參考資料集。</span><span class="sxs-lookup"><span data-stu-id="824d4-156">This is done to ensure that there is a **non-empty** reference data set when the job starts.</span></span> <span data-ttu-id="824d4-157">如果無法找到，作業會顯示下列診斷： `Initializing input without a valid reference data blob for UTC time <start time>`。</span><span class="sxs-lookup"><span data-stu-id="824d4-157">If one cannot be found, the job displays the following diagnostic: `Initializing input without a valid reference data blob for UTC time <start time>`.</span></span>
> 
> 

<span data-ttu-id="824d4-158">[Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) 可用來針對串流分析更新參考資料定義時所需的已更新 Blob，協調建立這些 Blob 的工作。</span><span class="sxs-lookup"><span data-stu-id="824d4-158">[Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) can be used to orchestrate the task of creating the updated blobs required by Stream Analytics to update reference data definitions.</span></span> <span data-ttu-id="824d4-159">Data Factory 是雲端架構資料整合服務，用來協調以及自動移動和轉換資料。</span><span class="sxs-lookup"><span data-stu-id="824d4-159">Data Factory is a cloud-based data integration service that orchestrates and automates the movement and transformation of data.</span></span> <span data-ttu-id="824d4-160">Data Factory 可 [連線到大量雲端式和內部部署的資料存放區](../data-factory/data-factory-data-movement-activities.md) ，也可根據您指定的定期排程輕鬆移動資料。</span><span class="sxs-lookup"><span data-stu-id="824d4-160">Data Factory supports [connecting to a large number of cloud based and on-premises data stores](../data-factory/data-factory-data-movement-activities.md) and moving data easily on a regular schedule that you specify.</span></span> <span data-ttu-id="824d4-161">如需詳細資訊及逐步解說指南，瞭解該如何設定 Data Factory 管線才能產生依預先定義排程重新整理的「串流分析」參考資料，請查看此 [GitHub 範例](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ReferenceDataRefreshForASAJobs)。</span><span class="sxs-lookup"><span data-stu-id="824d4-161">For more information and step by step guidance on how to set up a Data Factory pipeline to generate reference data for Stream Analytics which refreshes on a pre-defined schedule, check out this [GitHub sample](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ReferenceDataRefreshForASAJobs).</span></span>

## <a name="tips-on-refreshing-your-reference-data"></a><span data-ttu-id="824d4-162">重新整理參考資料的秘訣</span><span class="sxs-lookup"><span data-stu-id="824d4-162">Tips on refreshing your reference data</span></span>
1. <span data-ttu-id="824d4-163">覆寫參考資料 Blob 並不會造成「串流分析」重新載入 Blob，並且在某些情況下，它可能會造成工作失敗。</span><span class="sxs-lookup"><span data-stu-id="824d4-163">Overwriting reference data blobs will not cause Stream Analytics to reload the blob and in some cases it can cause the job to fail.</span></span> <span data-ttu-id="824d4-164">若要變更參考資料，建議的方式是藉由使用工作輸入中定義的相同容器和路徑格式，並使用比序列中最後一個 Blob 指定之日期/時間「大」  的日期/時間，加入新的 Blob。</span><span class="sxs-lookup"><span data-stu-id="824d4-164">The recommended way to change reference data is to add a new blob using the same container and path pattern defined in the job input and use a date/time **greater** than the one specified by the last blob in the sequence.</span></span>
2. <span data-ttu-id="824d4-165">參考資料 Blob **不是**依 Blob 的「上次修改日期」時間排序，而是只依 Blob 名稱中使用 {date} 和 {time} 替代來指定的時間和日期排序。</span><span class="sxs-lookup"><span data-stu-id="824d4-165">Reference data blobs are **not** ordered by the blob’s “Last Modified” time but only by the time and date specified in the blob name using the {date} and {time} substitutions.</span></span>
3. <span data-ttu-id="824d4-166">在一些情況下，作業必須回到之前的時間，因此參照資料不得被更改或刪除。</span><span class="sxs-lookup"><span data-stu-id="824d4-166">On a few occasions, a job must go back in time, therefore reference data blobs must not be altered or deleted.</span></span>

## <a name="get-help"></a><span data-ttu-id="824d4-167">取得說明</span><span class="sxs-lookup"><span data-stu-id="824d4-167">Get help</span></span>
<span data-ttu-id="824d4-168">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="824d4-168">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="824d4-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="824d4-169">Next steps</span></span>
<span data-ttu-id="824d4-170">以上就是串流分析 (物聯網資料串流分析專用的受管理服務) 的簡介。</span><span class="sxs-lookup"><span data-stu-id="824d4-170">You've been introduced to Stream Analytics, a managed service for streaming analytics on data from the Internet of Things.</span></span> <span data-ttu-id="824d4-171">若要深入了解此服務，請參閱：</span><span class="sxs-lookup"><span data-stu-id="824d4-171">To learn more about this service, see:</span></span>

* [<span data-ttu-id="824d4-172">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="824d4-172">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="824d4-173">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="824d4-173">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="824d4-174">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="824d4-174">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="824d4-175">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="824d4-175">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Link references-->
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.introduction]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.get.started]: stream-analytics-get-started.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
