---
title: "將資料匯入 Azure Application Insights 中的分析 | Microsoft Docs"
description: "匯入靜態資料以加入應用程式遙測，或匯入個別的資料流以分析查詢。"
services: application-insights
keywords: "開啟結構描述、匯入資料"
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: bwren
ms.openlocfilehash: aa855a9050ec4e5e7c5db88b7209b8bb48bdba51
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="import-data-into-analytics"></a><span data-ttu-id="bcc1e-104">將資料匯入分析</span><span class="sxs-lookup"><span data-stu-id="bcc1e-104">Import data into Analytics</span></span>

<span data-ttu-id="bcc1e-105">將任何表格式資料匯入[分析](app-insights-analytics.md)，將它從應用程式加入 [Application Insights](app-insights-overview.md) 遙測，或是讓您可以為個別的資料流進行分析。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-105">Import any tabular data into [Analytics](app-insights-analytics.md), either to join it with [Application Insights](app-insights-overview.md) telemetry from your app, or so that you can analyze it as a separate stream.</span></span> <span data-ttu-id="bcc1e-106">分析是適用於分析大量遙測時間戳記資料流的強大查詢語言。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-106">Analytics is a powerful query language well-suited to analyzing high-volume timestamped streams of telemetry.</span></span>

<span data-ttu-id="bcc1e-107">您可以使用自己的結構描述將資料匯入分析。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-107">You can import data into Analytics using your own schema.</span></span> <span data-ttu-id="bcc1e-108">它不需要使用標準 Application Insights 結構描述，例如要求或追蹤。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-108">It doesn't have to use the standard Application Insights schemas such as request or trace.</span></span>

<span data-ttu-id="bcc1e-109">您可以匯入 JSON 或 DSV (以分隔符號分隔值 - 逗號、分號或定位字元) 檔案。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-109">You can import JSON or DSV (delimiter-separated values - comma, semicolon or tab) files.</span></span>

<span data-ttu-id="bcc1e-110">有三種情況下，匯入至分析會很實用︰</span><span class="sxs-lookup"><span data-stu-id="bcc1e-110">There are three situations where importing to Analytics is useful:</span></span>

* <span data-ttu-id="bcc1e-111">**加入應用程式遙測。**</span><span class="sxs-lookup"><span data-stu-id="bcc1e-111">**Join with app telemetry.**</span></span> <span data-ttu-id="bcc1e-112">例如，您可以匯入將來自您網站的 URL 對應至更容易閱讀之頁面標題的資料表。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-112">For example, you could import a table that maps URLs from your website to more readable page titles.</span></span> <span data-ttu-id="bcc1e-113">在分析中，您可以建立儀表板圖表報表，其會顯示您的網站中十個最常用的頁面。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-113">In Analytics, you can create a dashboard chart report that shows the ten most popular pages in your website.</span></span> <span data-ttu-id="bcc1e-114">現在其可以顯示頁面標題，而非 URL。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-114">Now it can show the page titles instead of the URLs.</span></span>
* <span data-ttu-id="bcc1e-115">**相互關聯應用程式遙測**與其他來源，例如網路流量、伺服器資料或 CDN 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-115">**Correlate your application telemetry** with other sources such as network traffic, server data, or CDN log files.</span></span>
* <span data-ttu-id="bcc1e-116">**將個別的資料流套用至分析。**</span><span class="sxs-lookup"><span data-stu-id="bcc1e-116">**Apply Analytics to a separate data stream.**</span></span> <span data-ttu-id="bcc1e-117">Application Insights 分析是強大的工具，可搭配疏鬆、時間戳記資料流 - 在許多情況下遠優於 SQL。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-117">Application Insights Analytics is a powerful tool, that works well with sparse, timestamped streams - much better than SQL in many cases.</span></span> <span data-ttu-id="bcc1e-118">如果您有來自其他來源的資料流，您可以使用分析進行分析。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-118">If you have such a stream from some other source, you can analyze it with Analytics.</span></span>

<span data-ttu-id="bcc1e-119">將資料傳送至您的資料來源很簡單。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-119">Sending data to your data source is easy.</span></span> 

1. <span data-ttu-id="bcc1e-120">(一次性) 在資料來源中定義資料結構描述。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-120">(One time) Define the schema of your data in a 'data source'.</span></span>
2. <span data-ttu-id="bcc1e-121">(定期) 將您的資料上傳至 Azure 儲存體並呼叫 REST API，以通知我們新的資料正在等候擷取。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-121">(Periodically) Upload your data to Azure storage, and call the REST API to notify us that new data is waiting for ingestion.</span></span> <span data-ttu-id="bcc1e-122">在幾分鐘內，資料可在分析中供查詢。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-122">Within a few minutes, the data is available for query in Analytics.</span></span>

<span data-ttu-id="bcc1e-123">上傳的頻率是由您以及您希望您的資料多快可供查詢來定義。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-123">The frequency of the upload is defined by you and how fast would you like your data to be available for queries.</span></span> <span data-ttu-id="bcc1e-124">以較大的區塊上傳是更有效率的方式，但不超過 1 GB。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-124">It is more efficient to upload data in larger chunks, but not larger than 1GB.</span></span>

> [!NOTE]
> <span data-ttu-id="bcc1e-125">*有許多資料來源要分析嗎？*</span><span class="sxs-lookup"><span data-stu-id="bcc1e-125">*Got lots of data sources to analyze?*</span></span> [<span data-ttu-id="bcc1e-126">*請考慮使用 logstash* *以將您的資料傳送至 Application Insights。*</span><span class="sxs-lookup"><span data-stu-id="bcc1e-126">*Consider using* logstash *to ship your data into Application Insights.*</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
> 

## <a name="before-you-start"></a><span data-ttu-id="bcc1e-127">開始之前</span><span class="sxs-lookup"><span data-stu-id="bcc1e-127">Before you start</span></span>

<span data-ttu-id="bcc1e-128">您需要：</span><span class="sxs-lookup"><span data-stu-id="bcc1e-128">You need:</span></span>

1. <span data-ttu-id="bcc1e-129">Microsoft Azure 中的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-129">An Application Insights resource in Microsoft Azure.</span></span>

 * <span data-ttu-id="bcc1e-130">如果您想要與其他遙測分開分析您的資料，[建立新的 Application Insights 資源](app-insights-create-new-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-130">If you want to analyze your data separately from any other telemetry, [create a new Application Insights resource](app-insights-create-new-resource.md).</span></span>
 * <span data-ttu-id="bcc1e-131">如果您要加入或比較從已使用 Application Insights 設定的應用程式遙測之資料，您可以使用該應用程式的資源。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-131">If you're joining or comparing your data with telemetry from an app that is already set up with Application Insights, then you can use the resource for that app.</span></span>
 * <span data-ttu-id="bcc1e-132">參與者或擁有者存取該資源。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-132">Contributor or owner access to that resource.</span></span>
 
2. <span data-ttu-id="bcc1e-133">Azure 儲存體中的 Blob。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-133">Azure storage.</span></span> <span data-ttu-id="bcc1e-134">您上傳至 Azure 儲存體，分析會從該處取得您的資料。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-134">You upload to Azure storage, and Analytics gets your data from there.</span></span> 

 * <span data-ttu-id="bcc1e-135">我們建議您針對 blob 建立專用的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-135">We recommend you create a dedicated storage account for your blobs.</span></span> <span data-ttu-id="bcc1e-136">如果與其他處理序共用您的 blob，我們的程序會花較長時間來讀取 blob。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-136">If your blobs are shared with other processes, it takes longer for our processes to read your blobs.</span></span>


## <a name="define-your-schema"></a><span data-ttu-id="bcc1e-137">定義結構描述</span><span class="sxs-lookup"><span data-stu-id="bcc1e-137">Define your schema</span></span>

<span data-ttu-id="bcc1e-138">在您匯入資料之前，您必須定義資料來源，以指定您資料的結構描述。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-138">Before you can import data, you must define a *data source,* which specifies the schema of your data.</span></span>
<span data-ttu-id="bcc1e-139">在單一 Application Insights 資源中，最多可包含 50 個資料來源</span><span class="sxs-lookup"><span data-stu-id="bcc1e-139">You can have up to 50 data sources in a single Application Insights resource</span></span>

1. <span data-ttu-id="bcc1e-140">啟動資料來源精靈。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-140">Start the data source wizard.</span></span> <span data-ttu-id="bcc1e-141">使用 [新增資料來源] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-141">Use "Add new data source" button.</span></span> <span data-ttu-id="bcc1e-142">或者 - 按一下右上角的 [設定] 按鈕，然後在下拉式功能表中選擇 [資料來源]。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-142">Alternatively - click on settings button in right upper corner and choose "Data Sources" in dropdown menu.</span></span>

    ![新增資料來源](./media/app-insights-analytics-import/add-new-data-source.png)

    <span data-ttu-id="bcc1e-144">提供新資料來源的名稱。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-144">Provide a name for your new data source.</span></span>

2. <span data-ttu-id="bcc1e-145">定義您要上傳的檔案格式。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-145">Define format of the files that you will upload.</span></span>

    <span data-ttu-id="bcc1e-146">您可以手動定義格式，或上傳範例檔案。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-146">You can either define the format manually, or upload a sample file.</span></span>

    <span data-ttu-id="bcc1e-147">如果資料是 CSV 格式，此範例的第一列可以是資料行標頭。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-147">If the data is in CSV format, the first row of the sample can be column headers.</span></span> <span data-ttu-id="bcc1e-148">您可以在下一個步驟中變更欄位名稱。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-148">You can change the field names in the next step.</span></span>

    <span data-ttu-id="bcc1e-149">範例應該包含至少 10 個資料列或資料記錄。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-149">The sample should include at least 10 rows or records of data.</span></span>

    <span data-ttu-id="bcc1e-150">資料行或欄位名稱應包含英數字元名稱 (不含空格或標點符號)。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-150">Column or field names should have alphanumeric names (without spaces or punctuation).</span></span>

    ![上傳範例檔案](./media/app-insights-analytics-import/sample-data-file.png)


3. <span data-ttu-id="bcc1e-152">檢閱精靈已經得到的結構描述。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-152">Review the schema that the wizard has got.</span></span> <span data-ttu-id="bcc1e-153">如果它是從範例推斷出類型，您可能需要調整推斷的資料行類型。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-153">If it inferred the types from a sample, you might need to adjust the inferred types of the columns.</span></span>

    ![檢閱推斷的結構描述](./media/app-insights-analytics-import/data-source-review-schema.png)

 * <span data-ttu-id="bcc1e-155">(選擇性。)上傳結構描述定義。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-155">(Optional.) Upload a schema definition.</span></span> <span data-ttu-id="bcc1e-156">請看以下的格式。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-156">See the format below.</span></span>

 * <span data-ttu-id="bcc1e-157">選取時間戳記。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-157">Select a Timestamp.</span></span> <span data-ttu-id="bcc1e-158">分析中的所有資料都必須都有時間戳記欄位。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-158">All data in Analytics must have a timestamp field.</span></span> <span data-ttu-id="bcc1e-159">必須有 `datetime` 類型，但不必命名為 'timestamp'。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-159">It must have type `datetime`, but it doesn't have to be named 'timestamp'.</span></span> <span data-ttu-id="bcc1e-160">如果您的資料具有包含以 ISO 格式表示之日期和時間的資料行，選擇此選項為時間戳記資料行。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-160">If your data has a column containing a date and time in ISO format, choose this as the timestamp column.</span></span> <span data-ttu-id="bcc1e-161">否則，請選擇「資料抵達時」，匯入程序將會新增時間戳記欄位。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-161">Otherwise, choose "as data arrived", and the import process will add a timestamp field.</span></span>

5. <span data-ttu-id="bcc1e-162">建立資料來源。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-162">Create the data source.</span></span>

### <a name="schema-definition-file-format"></a><span data-ttu-id="bcc1e-163">結構描述定義檔案格式</span><span class="sxs-lookup"><span data-stu-id="bcc1e-163">Schema definition file format</span></span>

<span data-ttu-id="bcc1e-164">不要在 UI 中編輯結構描述，而是從檔案載入結構描述定義。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-164">Instead of editing the schema in UI, you can load the schema definition from a file.</span></span> <span data-ttu-id="bcc1e-165">結構描述定義格式如下︰</span><span class="sxs-lookup"><span data-stu-id="bcc1e-165">The schema definition format is as follows:</span></span> 

<span data-ttu-id="bcc1e-166">以符號分隔的格式</span><span class="sxs-lookup"><span data-stu-id="bcc1e-166">Delimited format</span></span> 
```
[ 
    {"location": "0", "name": "RequestName", "type": "string"}, 
    {"location": "1", "name": "timestamp", "type": "datetime"}, 
    {"location": "2", "name": "IPAddress", "type": "string"} 
] 
```

<span data-ttu-id="bcc1e-167">JSON 格式</span><span class="sxs-lookup"><span data-stu-id="bcc1e-167">JSON format</span></span> 
```
[ 
    {"location": "$.name", "name": "name", "type": "string"}, 
    {"location": "$.alias", "name": "alias", "type": "string"}, 
    {"location": "$.room", "name": "room", "type": "long"} 
]
```
 
<span data-ttu-id="bcc1e-168">以每個資料行的位置、名稱、類型識別它。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-168">Each column is identified by the location, name and type.</span></span> 

* <span data-ttu-id="bcc1e-169">位置 - 若為以符號分隔的檔案格式，則是對應值的位置。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-169">Location – For delimited file format it is the position of the mapped value.</span></span> <span data-ttu-id="bcc1e-170">若為 JSON 格式，則是對應索引鍵的 jpath。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-170">For JSON format, it is the jpath of the mapped key.</span></span>
* <span data-ttu-id="bcc1e-171">名稱 - 資料行的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-171">Name – the displayed name of the column.</span></span>
* <span data-ttu-id="bcc1e-172">類型 - 資料行的類型。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-172">Type – the data type of that column.</span></span>
 
<span data-ttu-id="bcc1e-173">在使用範例資料、而且檔案格式是符號分隔的情況下，結構描述定義必須對應所有資料行，並在結尾加入新的資料行。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-173">In case a sample data was used and file format is delimited, the schema definition must map all columns and add new columns at the end.</span></span> 

<span data-ttu-id="bcc1e-174">JSON 允許資料部分對應，因此 JSON 格式的結構描述定義不需要對應範例資料中找到的每個索引鍵。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-174">JSON allows partial mapping of the data, therefore the schema definition of JSON format doesn’t have to map every key which is found in a sample data.</span></span> <span data-ttu-id="bcc1e-175">它也可以對應不屬於範例資料的資料行。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-175">It can also map columns which are not part of the sample data.</span></span> 

## <a name="import-data"></a><span data-ttu-id="bcc1e-176">匯入資料</span><span class="sxs-lookup"><span data-stu-id="bcc1e-176">Import data</span></span>

<span data-ttu-id="bcc1e-177">若要匯入資料，請將它上傳至 Azure 儲存體、建立便捷鍵，然後建立 REST API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-177">To import data, you upload it to Azure storage, create an access key for it, and then make a REST API call.</span></span>

![新增資料來源](./media/app-insights-analytics-import/analytics-upload-process.png)

<span data-ttu-id="bcc1e-179">您可以手動執行下列程序，或設定自動系統定期執行。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-179">You can perform the following process manually, or set up an automated system to do it at regular intervals.</span></span> <span data-ttu-id="bcc1e-180">您必須依照下列步驟進行每個您要匯入的資料區塊。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-180">You need to follow these steps for each block of data you want to import.</span></span>

1. <span data-ttu-id="bcc1e-181">將資料上傳至 [Azure Blob 儲存體](../storage/blobs/storage-dotnet-how-to-use-blobs.md)。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-181">Upload the data to [Azure blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> 

 * <span data-ttu-id="bcc1e-182">Blob 未壓縮大小可以達 1 GB 。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-182">Blobs can be any size up to 1GB uncompressed.</span></span> <span data-ttu-id="bcc1e-183">從效能觀點來看，數百 MB 的大型 blob 很適合。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-183">Large blobs of hundreds of MB are ideal from a performance perspective.</span></span>
 * <span data-ttu-id="bcc1e-184">可以使用 Gzip 進行壓縮，以改善上傳時間和延遲時間，以便資料可用於查詢。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-184">You can compress it with Gzip to improve upload time and latency for the data to be available for query.</span></span> <span data-ttu-id="bcc1e-185">使用 `.gz` 副檔名。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-185">Use the `.gz` filename extension.</span></span>
 * <span data-ttu-id="bcc1e-186">針對此目的，最好使用個別的儲存體帳戶，以避免來自不同服務的呼叫拖慢效能。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-186">It's best to use a separate storage account for this purpose, to avoid calls from different services slowing performance.</span></span>
 * <span data-ttu-id="bcc1e-187">以高頻率 (每幾秒一次) 傳送資料時，基於效能考量，建議使用多個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-187">When sending data in high frequency, every few seconds, it is recommended to use more than one storage account, for performance reasons.</span></span>

 
2. <span data-ttu-id="bcc1e-188">[建立 blob 的共用存取簽章](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span><span class="sxs-lookup"><span data-stu-id="bcc1e-188">[Create a Shared Access Signature key for the blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span></span> <span data-ttu-id="bcc1e-189">金鑰應該有一天的到期時間，並提供讀取權限。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-189">The key should have an expiration period of one day and provide read access.</span></span>
3. <span data-ttu-id="bcc1e-190">進行 REST 呼叫，以通知 Application Insights 資料正在等候。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-190">Make a REST call to notify Application Insights that data is waiting.</span></span>

 * <span data-ttu-id="bcc1e-191">端點：`https://dc.services.visualstudio.com/v2/track`</span><span class="sxs-lookup"><span data-stu-id="bcc1e-191">Endpoint: `https://dc.services.visualstudio.com/v2/track`</span></span>
 * <span data-ttu-id="bcc1e-192">HTTP 方法：POST</span><span class="sxs-lookup"><span data-stu-id="bcc1e-192">HTTP method: POST</span></span>
 * <span data-ttu-id="bcc1e-193">承載：</span><span class="sxs-lookup"><span data-stu-id="bcc1e-193">Payload:</span></span>

```JSON

    {
       "data": {
            "baseType":"OpenSchemaData",
            "baseData":{
               "ver":"2",
               "blobSasUri":"<Blob URI with Shared Access Key>",
               "sourceName":"<Schema ID>",
               "sourceVersion":"1.0"
             }
       },
       "ver":1,
       "name":"Microsoft.ApplicationInsights.OpenSchema",
       "time":"<DateTime>",
       "iKey":"<instrumentation key>"
    }
```

<span data-ttu-id="bcc1e-194">預留位置是︰</span><span class="sxs-lookup"><span data-stu-id="bcc1e-194">The placeholders are:</span></span>

* <span data-ttu-id="bcc1e-195">`Blob URI with Shared Access Key`︰從建立機碼程序取得。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-195">`Blob URI with Shared Access Key`: You get this from the procedure for creating a key.</span></span> <span data-ttu-id="bcc1e-196">它是 blob 特定。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-196">It is specific to the blob.</span></span>
* <span data-ttu-id="bcc1e-197">`Schema ID`：為已定義的結構描述產生的結構描述識別碼。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-197">`Schema ID`: The schema ID generated for your defined schema.</span></span> <span data-ttu-id="bcc1e-198">此 Blob 中的資料應該與結構描述相符。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-198">The data in this blob should conform to the schema.</span></span>
* <span data-ttu-id="bcc1e-199">`DateTime`：送出要求的時間 (UTC)。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-199">`DateTime`: The time at which the request is submitted, UTC.</span></span> <span data-ttu-id="bcc1e-200">我們接受這些格式︰ISO8601 (例如 "2016-01-01 13:45:01")；RFC822 ("Wed, 14 Dec 16 14:57:01 +0000")；RFC850 ("Wednesday, 14-Dec-16 14:57:00 UTC")；RFC1123 ("Wed, 14 Dec 2016 14:57:00 +0000")。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-200">We accept these formats: ISO8601 (like "2016-01-01 13:45:01"); RFC822 ("Wed, 14 Dec 16 14:57:01 +0000"); RFC850 ("Wednesday, 14-Dec-16 14:57:00 UTC"); RFC1123 ("Wed, 14 Dec 2016 14:57:00 +0000").</span></span>
* <span data-ttu-id="bcc1e-201">您 `Instrumentation key` 的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-201">`Instrumentation key` of your Application Insights resource.</span></span>

<span data-ttu-id="bcc1e-202">後幾分鐘可在分析中使用資料。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-202">The data is available in Analytics after a few minutes.</span></span>

## <a name="error-responses"></a><span data-ttu-id="bcc1e-203">錯誤回應</span><span class="sxs-lookup"><span data-stu-id="bcc1e-203">Error responses</span></span>

* <span data-ttu-id="bcc1e-204">**400 不正確的要求**︰表示要求承載無效。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-204">**400 bad request**: indicates that the request payload is invalid.</span></span> <span data-ttu-id="bcc1e-205">勾選：</span><span class="sxs-lookup"><span data-stu-id="bcc1e-205">Check:</span></span>
 * <span data-ttu-id="bcc1e-206">修正動態檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-206">Correct instrumentation key.</span></span>
 * <span data-ttu-id="bcc1e-207">有效的時間值。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-207">Valid time value.</span></span> <span data-ttu-id="bcc1e-208">它應該是現在的 UTC 時間。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-208">It should be the time now in UTC.</span></span>
 * <span data-ttu-id="bcc1e-209">事件的 JSON 符合結構描述。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-209">JSON of the event conforms to the schema.</span></span>
* <span data-ttu-id="bcc1e-210">**403 禁止**︰您所傳送的 blob 不能存取。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-210">**403 Forbidden**: The blob you've sent is not accessible.</span></span> <span data-ttu-id="bcc1e-211">請確定共用的存取金鑰有效且尚未過期。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-211">Make sure that the shared access key is valid and has not expired.</span></span>
* <span data-ttu-id="bcc1e-212">**404 找不到**：</span><span class="sxs-lookup"><span data-stu-id="bcc1e-212">**404 Not Found**:</span></span>
 * <span data-ttu-id="bcc1e-213">Blob 不存在。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-213">The blob doesn't exist.</span></span>
 * <span data-ttu-id="bcc1e-214">來源識別碼是錯誤的。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-214">The sourceId is wrong.</span></span>

<span data-ttu-id="bcc1e-215">回應錯誤訊息中有更詳細的資訊。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-215">More detailed information is available in the response error message.</span></span>


## <a name="sample-code"></a><span data-ttu-id="bcc1e-216">範例程式碼</span><span class="sxs-lookup"><span data-stu-id="bcc1e-216">Sample code</span></span>

<span data-ttu-id="bcc1e-217">此程式碼使用 [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-217">This code uses the [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) NuGet package.</span></span>

### <a name="classes"></a><span data-ttu-id="bcc1e-218">類別</span><span class="sxs-lookup"><span data-stu-id="bcc1e-218">Classes</span></span>

```C#
namespace IngestionClient 
{ 
    using System; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceIngestionRequest 
    { 
        #region Members 
        private const string BaseDataRequiredVersion = "2"; 
        private const string RequestName = "Microsoft.ApplicationInsights.OpenSchema"; 
        #endregion Members 

        public AnalyticsDataSourceIngestionRequest(string ikey, string schemaId, string blobSasUri, int version = 1) 
        { 
            Ver = version; 
            IKey = ikey; 
            Data = new Data 
            { 
                BaseData = new BaseData 
                { 
                    Ver = BaseDataRequiredVersion, 
                    BlobSasUri = blobSasUri, 
                    SourceName = schemaId, 
                    SourceVersion = version.ToString() 
                } 
            }; 
        } 


        [JsonProperty("data")] 
        public Data Data { get; set; } 

        [JsonProperty("ver")] 
        public int Ver { get; set; } 

        [JsonProperty("name")] 
        public string Name { get { return RequestName; } } 

        [JsonProperty("time")] 
        public DateTime Time { get { return DateTime.UtcNow; } } 

        [JsonProperty("iKey")] 
        public string IKey { get; set; } 
    } 

    #region Internal Classes 

    public class Data 
    { 
        private const string DataBaseType = "OpenSchemaData"; 

        [JsonProperty("baseType")] 
        public string BaseType 
        { 
            get { return DataBaseType; } 
        } 

        [JsonProperty("baseData")] 
        public BaseData BaseData { get; set; } 
    } 


    public class BaseData 
    { 
        [JsonProperty("ver")] 
        public string Ver { get; set; } 

        [JsonProperty("blobSasUri")] 
        public string BlobSasUri { get; set; } 

        [JsonProperty("sourceName")] 
        public string SourceName { get; set; } 

        [JsonProperty("sourceVersion")] 
        public string SourceVersion { get; set; } 
    } 

    #endregion Internal Classes 
} 


namespace IngestionClient 
{ 
    using System; 
    using System.IO; 
    using System.Net; 
    using System.Text; 
    using System.Threading.Tasks; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceClient 
    { 
        #region Members 
        private readonly Uri endpoint = new Uri("https://dc.services.visualstudio.com/v2/track"); 
        private const string RequestContentType = "application/json; charset=UTF-8"; 
        private const string RequestAccess = "application/json"; 
        #endregion Members 

        #region Public 

        public async Task<bool> RequestBlobIngestion(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            HttpWebRequest request = WebRequest.CreateHttp(endpoint); 
            request.Method = WebRequestMethods.Http.Post; 
            request.ContentType = RequestContentType; 
            request.Accept = RequestAccess; 

            string notificationJson = Serialize(ingestionRequest); 
            byte[] notificationBytes = GetContentBytes(notificationJson); 
            request.ContentLength = notificationBytes.Length; 

            Stream requestStream = request.GetRequestStream(); 
            requestStream.Write(notificationBytes, 0, notificationBytes.Length); 
            requestStream.Close(); 

            try 
            { 
                using (var response = (HttpWebResponse)await request.GetResponseAsync())
                {
                    return response.StatusCode == HttpStatusCode.OK;
                }
            } 
            catch (WebException e) 
            { 
                HttpWebResponse httpResponse = e.Response as HttpWebResponse; 
                if (httpResponse != null) 
                { 
                    Console.WriteLine( 
                        "Ingestion request failed with status code: {0}. Error: {1}", 
                        httpResponse.StatusCode, 
                        httpResponse.StatusDescription); 
                    return false; 
                }
                throw; 
            } 
        } 
        #endregion Public 

        #region Private 
        private byte[] GetContentBytes(string content) 
        { 
            return Encoding.UTF8.GetBytes(content);
        } 


        private string Serialize(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            return JsonConvert.SerializeObject(ingestionRequest); 
        } 
        #endregion Private 
    } 
} 
```

### <a name="ingest-data"></a><span data-ttu-id="bcc1e-219">擷取資料</span><span class="sxs-lookup"><span data-stu-id="bcc1e-219">Ingest data</span></span>

<span data-ttu-id="bcc1e-220">針對每個 blob 使用此程式碼。</span><span class="sxs-lookup"><span data-stu-id="bcc1e-220">Use this code for each blob.</span></span> 

```C#
   AnalyticsDataSourceClient client = new AnalyticsDataSourceClient(); 

   var ingestionRequest = new AnalyticsDataSourceIngestionRequest("iKey", "sourceId", "blobUrlWithSas"); 

   bool success = await client.RequestBlobIngestion(ingestionRequest);
```

## <a name="next-steps"></a><span data-ttu-id="bcc1e-221">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bcc1e-221">Next steps</span></span>

* [<span data-ttu-id="bcc1e-222">Log Analytics 查詢語言導覽</span><span class="sxs-lookup"><span data-stu-id="bcc1e-222">Tour of the Log Analytics query language</span></span>](app-insights-analytics-tour.md)
* [<span data-ttu-id="bcc1e-223">使用 Logstash 將資料傳送至 Application Insights</span><span class="sxs-lookup"><span data-stu-id="bcc1e-223">Use *Logstash* to send data to Application Insights</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
