---
title: "aaaUse 參考資料與查閱資料表中資料流分析 |Microsoft 文件"
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
ms.openlocfilehash: fb1d18fba920db5e097d0c95d333e8e8390d1589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-reference-data-or-lookup-tables-in-a-stream-analytics-input-stream"></a><span data-ttu-id="5ea14-104">在串流分析的輸入串流中使用參考資料或查詢資料表</span><span class="sxs-lookup"><span data-stu-id="5ea14-104">Using reference data or lookup tables in a Stream Analytics input stream</span></span>
<span data-ttu-id="5ea14-105">參考資料 （也稱為查閱資料表） 是有限的資料集是靜態，或降低的本質，變更使用 tooperform 查閱或 toocorrelate 與資料流。</span><span class="sxs-lookup"><span data-stu-id="5ea14-105">Reference data (also known as a lookup table) is a finite data set that is static or slowing changing in nature, used tooperform a lookup or toocorrelate with your data stream.</span></span> <span data-ttu-id="5ea14-106">toomake 使用參考資料在 Azure Stream Analytics 工作中，您通常會使用[參考資料 Join](https://msdn.microsoft.com/library/azure/dn949258.aspx)在查詢中。</span><span class="sxs-lookup"><span data-stu-id="5ea14-106">toomake use of reference data in your Azure Stream Analytics job, you will generally use a [Reference Data Join](https://msdn.microsoft.com/library/azure/dn949258.aspx) in your Query.</span></span> <span data-ttu-id="5ea14-107">串流分析會為 hello 參考資料的儲存層的 Azure Blob 儲存體和 Azure Data Factory 參考資料可以是轉換後及/或複製 tooAzure Blob 儲存體，用來參考資料做[任意數目的雲端和在內部部署資料存放區](../data-factory/data-factory-data-movement-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="5ea14-107">Stream Analytics uses Azure Blob storage as hello storage layer for Reference Data, and with Azure Data Factory reference data can be transformed and/or copied tooAzure Blob storage, for use as Reference Data, from [any number of cloud-based and on-premises data stores](../data-factory/data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="5ea14-108">參考資料會以一連串 blob （hello 輸入組態中定義），以遞增的 hello 日期/時間 hello blob 名稱中指定的模型化。</span><span class="sxs-lookup"><span data-stu-id="5ea14-108">Reference data is modeled as a sequence of blobs (defined in hello input configuration) in ascending order of hello date/time specified in hello blob name.</span></span> <span data-ttu-id="5ea14-109">它**只**支援 toohello hello 序列的結尾加入使用日期/時間**大於**比 hello hello 最後一個 blob 中所指定 hello 序列中。</span><span class="sxs-lookup"><span data-stu-id="5ea14-109">It **only** supports adding toohello end of hello sequence by using a date/time **greater** than hello one specified by hello last blob in hello sequence.</span></span>

<span data-ttu-id="5ea14-110">資料流分析**100 mb 的限制每個 blob**但作業可以處理多個參考 blob 使用 hello**路徑模式**屬性。</span><span class="sxs-lookup"><span data-stu-id="5ea14-110">Stream Analytics has a **limit of 100 MB per blob** but jobs can process multiple reference blobs by using hello **path pattern** property.</span></span>


## <a name="configuring-reference-data"></a><span data-ttu-id="5ea14-111">設定參考資料</span><span class="sxs-lookup"><span data-stu-id="5ea14-111">Configuring reference data</span></span>
<span data-ttu-id="5ea14-112">tooconfigure 您參考的資料，您必須先 toocreate 的型別輸入**參考資料**。</span><span class="sxs-lookup"><span data-stu-id="5ea14-112">tooconfigure your reference data, you first need toocreate an input that is of type **Reference Data**.</span></span> <span data-ttu-id="5ea14-113">hello 下表說明每個屬性，您將需要 tooprovide 時使用其描述建立 hello 參考資料輸入：</span><span class="sxs-lookup"><span data-stu-id="5ea14-113">hello table below explains each property that you will need tooprovide while creating hello reference data input with its description:</span></span>


<table>
<tbody>
<tr>
<td><span data-ttu-id="5ea14-114">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="5ea14-114">Property Name</span></span></td>
<td><span data-ttu-id="5ea14-115">說明</span><span class="sxs-lookup"><span data-stu-id="5ea14-115">Description</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5ea14-116">輸入別名</span><span class="sxs-lookup"><span data-stu-id="5ea14-116">Input Alias</span></span></td>
<td><span data-ttu-id="5ea14-117">這個輸入將用於 hello 工作查詢 tooreference 中的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="5ea14-117">A friendly name that will be used in hello job query tooreference this input.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5ea14-118">儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="5ea14-118">Storage Account</span></span></td>
<td><span data-ttu-id="5ea14-119">hello hello blob 的所在位置的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="5ea14-119">hello name of hello storage account where your blobs are located.</span></span> <span data-ttu-id="5ea14-120">如果是在 hello 做為資料流分析工作的相同訂用帳戶，您也可以從選取 hello 下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="5ea14-120">If it’s in hello same subscription as your Stream Analytics Job, you can select it from hello drop-down.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5ea14-121">儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="5ea14-121">Storage Account Key</span></span></td>
<td><span data-ttu-id="5ea14-122">hello 秘密金鑰與 hello 儲存體帳戶相關聯。</span><span class="sxs-lookup"><span data-stu-id="5ea14-122">hello secret key associated with hello storage account.</span></span> <span data-ttu-id="5ea14-123">這會自動填入 hello hello 儲存體帳戶是否相同的訂用帳戶與串流分析工作。</span><span class="sxs-lookup"><span data-stu-id="5ea14-123">This gets automatically populated if hello storage account is in hello same subscription as your Stream Analytics job.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5ea14-124">儲存體容器</span><span class="sxs-lookup"><span data-stu-id="5ea14-124">Storage Container</span></span></td>
<td><span data-ttu-id="5ea14-125">容器提供 blob 儲存在 hello Microsoft Azure Blob 服務中的邏輯分組。</span><span class="sxs-lookup"><span data-stu-id="5ea14-125">Containers provide a logical grouping for blobs stored in hello Microsoft Azure Blob service.</span></span> <span data-ttu-id="5ea14-126">當您上傳 blob toohello Blob 服務時，您必須指定該 blob 的容器。</span><span class="sxs-lookup"><span data-stu-id="5ea14-126">When you upload a blob toohello Blob service, you must specify a container for that blob.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5ea14-127">路徑格式</span><span class="sxs-lookup"><span data-stu-id="5ea14-127">Path Pattern</span></span></td>
<td><span data-ttu-id="5ea14-128">使用 toolocate hello 指定容器中的 blob hello 路徑。</span><span class="sxs-lookup"><span data-stu-id="5ea14-128">hello path used toolocate your blobs within hello specified container.</span></span> <span data-ttu-id="5ea14-129">Hello 路徑內，您可以選擇 toospecify hello 下列 2 個變數的一或多個執行個體：</span><span class="sxs-lookup"><span data-stu-id="5ea14-129">Within hello path, you may choose toospecify one or more instances of hello following 2 variables:</span></span><BR><span data-ttu-id="5ea14-130">{date}、{time}</span><span class="sxs-lookup"><span data-stu-id="5ea14-130">{date}, {time}</span></span><BR><span data-ttu-id="5ea14-131">範例 1：products/{date}/{time}/product-list.csv</span><span class="sxs-lookup"><span data-stu-id="5ea14-131">Example 1: products/{date}/{time}/product-list.csv</span></span><BR><span data-ttu-id="5ea14-132">範例 2：products/{date}/product-list.csv</span><span class="sxs-lookup"><span data-stu-id="5ea14-132">Example 2: products/{date}/product-list.csv</span></span>
</tr>
<tr>
<td><span data-ttu-id="5ea14-133">日期格式 [選用]</span><span class="sxs-lookup"><span data-stu-id="5ea14-133">Date Format [optional]</span></span></td>
<td><span data-ttu-id="5ea14-134">如果您已經使用 {date} hello 您指定的路徑模式中，您可以從支援的格式 hello 下拉式清單選取 hello 編排您的 blob 的日期格式。</span><span class="sxs-lookup"><span data-stu-id="5ea14-134">If you have used {date} within hello Path Pattern that you specified, then you can select hello date format in which your blobs are organized from hello drop-down of supported formats.</span></span><BR><span data-ttu-id="5ea14-135">範例︰YYYY/MM/DD、MM/DD/YYYY 等。</span><span class="sxs-lookup"><span data-stu-id="5ea14-135">Example: YYYY/MM/DD, MM/DD/YYYY, etc.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5ea14-136">時間格式 [選用]</span><span class="sxs-lookup"><span data-stu-id="5ea14-136">Time Format [optional]</span></span></td>
<td><span data-ttu-id="5ea14-137">如果您已經使用 {time} hello 您指定的路徑模式中，您可以從支援的格式 hello 下拉式清單選取 hello 編排您的 blob 的時間格式。</span><span class="sxs-lookup"><span data-stu-id="5ea14-137">If you have used {time} within hello Path Pattern that you specified, then you can select hello time format in which your blobs are organized from hello drop-down of supported formats.</span></span><BR><span data-ttu-id="5ea14-138">範例︰HH、HH/mm 或 HH-mm</span><span class="sxs-lookup"><span data-stu-id="5ea14-138">Example: HH, HH/mm, or HH-mm</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5ea14-139">事件序列化格式</span><span class="sxs-lookup"><span data-stu-id="5ea14-139">Event Serialization Format</span></span></td>
<td><span data-ttu-id="5ea14-140">確定您的查詢工作 hello 您預期的方式，串流分析 toomake 需要的 tooknow 為傳入的資料流正在使用哪一種序列化格式。</span><span class="sxs-lookup"><span data-stu-id="5ea14-140">toomake sure your queries work hello way you expect, Stream Analytics needs tooknow which serialization format you're using for incoming data streams.</span></span> <span data-ttu-id="5ea14-141">參考資料 hello 支援的格式為 CSV 和 JSON。</span><span class="sxs-lookup"><span data-stu-id="5ea14-141">For Reference Data, hello supported formats are CSV and JSON.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5ea14-142">編碼</span><span class="sxs-lookup"><span data-stu-id="5ea14-142">Encoding</span></span></td>
<td><span data-ttu-id="5ea14-143">Utf-8 是 hello 此時只支援編碼格式</span><span class="sxs-lookup"><span data-stu-id="5ea14-143">UTF-8 is hello only supported encoding format at this time</span></span></td>
</tr>
</tbody>
</table>

## <a name="generating-reference-data-on-a-schedule"></a><span data-ttu-id="5ea14-144">產生排程上的參考資料</span><span class="sxs-lookup"><span data-stu-id="5ea14-144">Generating reference data on a schedule</span></span>
<span data-ttu-id="5ea14-145">如果參考資料是緩時變更的資料集，藉由在使用 hello {date} 及 {time} 替代語彙基元的 hello 輸入組態中指定路徑模式已啟用支援重新整理參考資料。</span><span class="sxs-lookup"><span data-stu-id="5ea14-145">If your reference data is a slowly changing data set, then support for refreshing reference data is enabled by specifying a path pattern in hello input configuration using hello {date} and {time} substitution tokens.</span></span> <span data-ttu-id="5ea14-146">資料流分析會拾取 hello 更新參考資料定義依據這個路徑模式。</span><span class="sxs-lookup"><span data-stu-id="5ea14-146">Stream Analytics picks up hello updated reference data definitions based on this path pattern.</span></span> <span data-ttu-id="5ea14-147">例如，模式的`sample/{date}/{time}/products.csv`使用的日期格式**"YYYY-MM-DD"**和時間格式的**"HH mm"**指示 hello 更新 blob 上的資料流分析 toopick`sample/2015-04-16/17-30/products.csv`年 4 月下午 5:3016，2015 UTC 時區為準。</span><span class="sxs-lookup"><span data-stu-id="5ea14-147">For example, a pattern of `sample/{date}/{time}/products.csv` with a date format of **“YYYY-MM-DD”** and a time format of **“HH-mm”** instructs Stream Analytics toopick up hello updated blob `sample/2015-04-16/17-30/products.csv` at 5:30 PM on April 16th, 2015 UTC time zone.</span></span>

> [!NOTE]
> <span data-ttu-id="5ea14-148">目前資料流分析工作時看起來 hello blob 重新整理只 hello 機器時間往前推進 toohello 時間，並在 hello blob 名稱編碼。</span><span class="sxs-lookup"><span data-stu-id="5ea14-148">Currently Stream Analytics jobs look for hello blob refresh only when hello machine time advances toohello time encoded in hello blob name.</span></span> <span data-ttu-id="5ea14-149">例如，將會尋找 hello 作業`sample/2015-04-16/17-30/products.csv`儘速但前面沒有比下午 5:30 於 2015 年 4 月 16 日 UTC 時區。</span><span class="sxs-lookup"><span data-stu-id="5ea14-149">For example, hello job will look for `sample/2015-04-16/17-30/products.csv` as soon as possible but no earlier than 5:30 PM on April 16th, 2015 UTC time zone.</span></span> <span data-ttu-id="5ea14-150">它會*從未*尋找編碼時間早於 hello 探索到的最後一個 blob。</span><span class="sxs-lookup"><span data-stu-id="5ea14-150">It will *never* look for a blob with an encoded time earlier than hello last one that is discovered.</span></span>
> 
> <span data-ttu-id="5ea14-151">例如</span><span class="sxs-lookup"><span data-stu-id="5ea14-151">E.g.</span></span> <span data-ttu-id="5ea14-152">一旦 hello 作業尋找 hello blob`sample/2015-04-16/17-30/products.csv`就會忽略所有的檔案編碼的日期早於 2015 年 4 月 16 日下午 5:30，如果晚期抵達`sample/2015-04-16/17-25/products.csv`blob 取得中建立 hello 相同容器 hello 作業不會使用它。</span><span class="sxs-lookup"><span data-stu-id="5ea14-152">once hello job finds hello blob `sample/2015-04-16/17-30/products.csv` it will ignore any files with an encoded date earlier than 5:30 PM April 16th, 2015 so if a late arriving `sample/2015-04-16/17-25/products.csv` blob gets created in hello same container hello job will not use it.</span></span>
> 
> <span data-ttu-id="5ea14-153">同樣地如果`sample/2015-04-16/17-30/products.csv`，才會產生在 2015 年 4 月 16 日下午 10:03，但沒有與較早日期的 blob 存在 hello 容器中，hello 作業將會使用在 2015 年 4 月 16 日下午 10:03 啟動這個檔案，並使用之前的 hello 先前的參考資料。</span><span class="sxs-lookup"><span data-stu-id="5ea14-153">Likewise if `sample/2015-04-16/17-30/products.csv` is only produced at 10:03 PM April 16th, 2015 but no blob with an earlier date is present in hello container, hello job will use this file starting at 10:03 PM April 16th, 2015 and use hello previous reference data until then.</span></span>
> 
> <span data-ttu-id="5ea14-154">例外狀況 toothis 是在 hello 作業必須回到過去 toore 同處理序資料，或者 hello 作業初次啟動時。</span><span class="sxs-lookup"><span data-stu-id="5ea14-154">An exception toothis is when hello job needs toore-process data back in time or when hello job is first started.</span></span> <span data-ttu-id="5ea14-155">在開始時間 hello 作業正在尋找 hello 產生 hello 作業指定的開始時間之前的最新 blob。</span><span class="sxs-lookup"><span data-stu-id="5ea14-155">At start time hello job is looking for hello most recent blob produced before hello job start time specified.</span></span> <span data-ttu-id="5ea14-156">這是沒有的 tooensure**非空白**hello 作業啟動時，參考資料集。</span><span class="sxs-lookup"><span data-stu-id="5ea14-156">This is done tooensure that there is a **non-empty** reference data set when hello job starts.</span></span> <span data-ttu-id="5ea14-157">如果無法找到一個，hello 作業就會顯示下列診斷 hello: `Initializing input without a valid reference data blob for UTC time <start time>`。</span><span class="sxs-lookup"><span data-stu-id="5ea14-157">If one cannot be found, hello job displays hello following diagnostic: `Initializing input without a valid reference data blob for UTC time <start time>`.</span></span>
> 
> 

<span data-ttu-id="5ea14-158">[Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/)可以建立 hello 更新 blob 所需的資料流分析 tooupdate 參考資料定義使用的 tooorchestrate hello 工作。</span><span class="sxs-lookup"><span data-stu-id="5ea14-158">[Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) can be used tooorchestrate hello task of creating hello updated blobs required by Stream Analytics tooupdate reference data definitions.</span></span> <span data-ttu-id="5ea14-159">Data Factory 是以雲端為基礎的資料整合服務會協調及自動 hello 移動和轉換資料。</span><span class="sxs-lookup"><span data-stu-id="5ea14-159">Data Factory is a cloud-based data integration service that orchestrates and automates hello movement and transformation of data.</span></span> <span data-ttu-id="5ea14-160">Data Factory 支援[連接 tooa 大量的雲端和內部部署資料存放區](../data-factory/data-factory-data-movement-activities.md)和您指定的定期輕鬆地移動資料。</span><span class="sxs-lookup"><span data-stu-id="5ea14-160">Data Factory supports [connecting tooa large number of cloud based and on-premises data stores](../data-factory/data-factory-data-movement-activities.md) and moving data easily on a regular schedule that you specify.</span></span> <span data-ttu-id="5ea14-161">如需詳細資訊和逐步指引 tooset 向上 Data Factory 的預先定義的排程重新整理的資料流分析管線 toogenerate 參考資料的方式，請參閱這[GitHub 範例](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ReferenceDataRefreshForASAJobs)。</span><span class="sxs-lookup"><span data-stu-id="5ea14-161">For more information and step by step guidance on how tooset up a Data Factory pipeline toogenerate reference data for Stream Analytics which refreshes on a pre-defined schedule, check out this [GitHub sample](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ReferenceDataRefreshForASAJobs).</span></span>

## <a name="tips-on-refreshing-your-reference-data"></a><span data-ttu-id="5ea14-162">重新整理參考資料的秘訣</span><span class="sxs-lookup"><span data-stu-id="5ea14-162">Tips on refreshing your reference data</span></span>
1. <span data-ttu-id="5ea14-163">覆寫參考資料 blob 不會造成資料流分析 tooreload hello blob，而且在某些情況下它可能會導致 hello 作業 toofail。</span><span class="sxs-lookup"><span data-stu-id="5ea14-163">Overwriting reference data blobs will not cause Stream Analytics tooreload hello blob and in some cases it can cause hello job toofail.</span></span> <span data-ttu-id="5ea14-164">hello 的建議方式 toochange 參考資料是 tooadd 新 blob 使用相同的容器和路徑模式定義 hello 作業輸入中的 hello 和使用日期/時間**大於**比 hello hello 最後一個 blob 中所指定 hello 序列中。</span><span class="sxs-lookup"><span data-stu-id="5ea14-164">hello recommended way toochange reference data is tooadd a new blob using hello same container and path pattern defined in hello job input and use a date/time **greater** than hello one specified by hello last blob in hello sequence.</span></span>
2. <span data-ttu-id="5ea14-165">參考資料 blob**不**排序 hello blob 的 「 上次修改 」 的時間，但只能由 hello 時間與 hello blob 名稱使用 hello {date} 及 {time} 替代項目中指定的日期。</span><span class="sxs-lookup"><span data-stu-id="5ea14-165">Reference data blobs are **not** ordered by hello blob’s “Last Modified” time but only by hello time and date specified in hello blob name using hello {date} and {time} substitutions.</span></span>
3. <span data-ttu-id="5ea14-166">在一些情況下，作業必須回到之前的時間，因此參照資料不得被更改或刪除。</span><span class="sxs-lookup"><span data-stu-id="5ea14-166">On a few occasions, a job must go back in time, therefore reference data blobs must not be altered or deleted.</span></span>

## <a name="get-help"></a><span data-ttu-id="5ea14-167">取得說明</span><span class="sxs-lookup"><span data-stu-id="5ea14-167">Get help</span></span>
<span data-ttu-id="5ea14-168">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="5ea14-168">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ea14-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5ea14-169">Next steps</span></span>
<span data-ttu-id="5ea14-170">您已經導入了的 tooStream 分析，資料流分析的資料是來自 hello 物聯網的受管理的服務。</span><span class="sxs-lookup"><span data-stu-id="5ea14-170">You've been introduced tooStream Analytics, a managed service for streaming analytics on data from hello Internet of Things.</span></span> <span data-ttu-id="5ea14-171">toolearn 進一步了解這項服務，請參閱：</span><span class="sxs-lookup"><span data-stu-id="5ea14-171">toolearn more about this service, see:</span></span>

* [<span data-ttu-id="5ea14-172">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5ea14-172">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="5ea14-173">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="5ea14-173">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="5ea14-174">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="5ea14-174">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="5ea14-175">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="5ea14-175">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Link references-->
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.introduction]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.get.started]: stream-analytics-get-started.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
