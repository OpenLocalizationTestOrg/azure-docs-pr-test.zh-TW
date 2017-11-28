---
title: "aaaImport Azure Application Insights 中的您資料 tooAnalytics |Microsoft 文件"
description: "匯入的應用程式遙測的靜態資料 toojoin 或匯入個別的資料流 tooquery 進行分析。"
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
ms.openlocfilehash: 7a3a3c9155adc1885dd366ddb13dda80bb894adb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-into-analytics"></a><span data-ttu-id="87ee9-104">將資料匯入分析</span><span class="sxs-lookup"><span data-stu-id="87ee9-104">Import data into Analytics</span></span>

<span data-ttu-id="87ee9-105">任何表格式資料匯入[分析](app-insights-analytics.md)，任一 toojoin 它與[Application Insights](app-insights-overview.md)從您的應用程式的遙測，或是讓您可以為不同的資料流分析。</span><span class="sxs-lookup"><span data-stu-id="87ee9-105">Import any tabular data into [Analytics](app-insights-analytics.md), either toojoin it with [Application Insights](app-insights-overview.md) telemetry from your app, or so that you can analyze it as a separate stream.</span></span> <span data-ttu-id="87ee9-106">分析是功能強大的查詢語言適合的 tooanalyzing 高容量加上資料流的遙測資料。</span><span class="sxs-lookup"><span data-stu-id="87ee9-106">Analytics is a powerful query language well-suited tooanalyzing high-volume timestamped streams of telemetry.</span></span>

<span data-ttu-id="87ee9-107">您可以使用自己的結構描述將資料匯入分析。</span><span class="sxs-lookup"><span data-stu-id="87ee9-107">You can import data into Analytics using your own schema.</span></span> <span data-ttu-id="87ee9-108">它沒有 toouse hello 標準 Application Insights 結構描述要求或追蹤等。</span><span class="sxs-lookup"><span data-stu-id="87ee9-108">It doesn't have toouse hello standard Application Insights schemas such as request or trace.</span></span>

<span data-ttu-id="87ee9-109">您可以匯入 JSON 或 DSV (以分隔符號分隔值 - 逗號、分號或定位字元) 檔案。</span><span class="sxs-lookup"><span data-stu-id="87ee9-109">You can import JSON or DSV (delimiter-separated values - comma, semicolon or tab) files.</span></span>

<span data-ttu-id="87ee9-110">有三種情況下匯入 tooAnalytics 很有用：</span><span class="sxs-lookup"><span data-stu-id="87ee9-110">There are three situations where importing tooAnalytics is useful:</span></span>

* <span data-ttu-id="87ee9-111">**加入應用程式遙測。**</span><span class="sxs-lookup"><span data-stu-id="87ee9-111">**Join with app telemetry.**</span></span> <span data-ttu-id="87ee9-112">例如，您可以匯入對應 Url 從您的網站 toomore 可讀取的頁面標題的資料表。</span><span class="sxs-lookup"><span data-stu-id="87ee9-112">For example, you could import a table that maps URLs from your website toomore readable page titles.</span></span> <span data-ttu-id="87ee9-113">在分析，您可以建立儀表板圖表報表會顯示 hello 十個最受歡迎頁面中您的網站。</span><span class="sxs-lookup"><span data-stu-id="87ee9-113">In Analytics, you can create a dashboard chart report that shows hello ten most popular pages in your website.</span></span> <span data-ttu-id="87ee9-114">現在可以顯示 hello 而不是 hello Url 的頁面標題。</span><span class="sxs-lookup"><span data-stu-id="87ee9-114">Now it can show hello page titles instead of hello URLs.</span></span>
* <span data-ttu-id="87ee9-115">**相互關聯應用程式遙測**與其他來源，例如網路流量、伺服器資料或 CDN 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="87ee9-115">**Correlate your application telemetry** with other sources such as network traffic, server data, or CDN log files.</span></span>
* <span data-ttu-id="87ee9-116">**適用於分析 tooa 不同的資料流。**</span><span class="sxs-lookup"><span data-stu-id="87ee9-116">**Apply Analytics tooa separate data stream.**</span></span> <span data-ttu-id="87ee9-117">Application Insights 分析是強大的工具，可搭配疏鬆、時間戳記資料流 - 在許多情況下遠優於 SQL。</span><span class="sxs-lookup"><span data-stu-id="87ee9-117">Application Insights Analytics is a powerful tool, that works well with sparse, timestamped streams - much better than SQL in many cases.</span></span> <span data-ttu-id="87ee9-118">如果您有來自其他來源的資料流，您可以使用分析進行分析。</span><span class="sxs-lookup"><span data-stu-id="87ee9-118">If you have such a stream from some other source, you can analyze it with Analytics.</span></span>

<span data-ttu-id="87ee9-119">傳送 tooyour 資料來源的資料很容易。</span><span class="sxs-lookup"><span data-stu-id="87ee9-119">Sending data tooyour data source is easy.</span></span> 

1. <span data-ttu-id="87ee9-120">（一次）定義 hello 結構描述，'data source' 中的資料。</span><span class="sxs-lookup"><span data-stu-id="87ee9-120">(One time) Define hello schema of your data in a 'data source'.</span></span>
2. <span data-ttu-id="87ee9-121">（定期）上傳資料 tooAzure 儲存體，並呼叫 hello REST API toonotify 我們正在等待擷取新的資料。</span><span class="sxs-lookup"><span data-stu-id="87ee9-121">(Periodically) Upload your data tooAzure storage, and call hello REST API toonotify us that new data is waiting for ingestion.</span></span> <span data-ttu-id="87ee9-122">在幾分鐘的時間內 hello 資料可在分析中的查詢。</span><span class="sxs-lookup"><span data-stu-id="87ee9-122">Within a few minutes, hello data is available for query in Analytics.</span></span>

<span data-ttu-id="87ee9-123">hello 的 hello 上傳頻率由您定義和速度您希望您的資料 toobe 可供查詢。</span><span class="sxs-lookup"><span data-stu-id="87ee9-123">hello frequency of hello upload is defined by you and how fast would you like your data toobe available for queries.</span></span> <span data-ttu-id="87ee9-124">它會更有效率的 tooupload 資料在較大的區塊，但不是會超過 1 GB。</span><span class="sxs-lookup"><span data-stu-id="87ee9-124">It is more efficient tooupload data in larger chunks, but not larger than 1GB.</span></span>

> [!NOTE]
> <span data-ttu-id="87ee9-125">*有許多資料來源 tooanalyze 嗎？*</span><span class="sxs-lookup"><span data-stu-id="87ee9-125">*Got lots of data sources tooanalyze?*</span></span> [<span data-ttu-id="87ee9-126">*請考慮使用*logstash *tooship Application Insights 資料。*</span><span class="sxs-lookup"><span data-stu-id="87ee9-126">*Consider using* logstash *tooship your data into Application Insights.*</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
> 

## <a name="before-you-start"></a><span data-ttu-id="87ee9-127">開始之前</span><span class="sxs-lookup"><span data-stu-id="87ee9-127">Before you start</span></span>

<span data-ttu-id="87ee9-128">您需要：</span><span class="sxs-lookup"><span data-stu-id="87ee9-128">You need:</span></span>

1. <span data-ttu-id="87ee9-129">Microsoft Azure 中的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="87ee9-129">An Application Insights resource in Microsoft Azure.</span></span>

 * <span data-ttu-id="87ee9-130">如果您希望 tooanalyze 分開其他遙測資料[建立新的 Application Insights 資源](app-insights-create-new-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="87ee9-130">If you want tooanalyze your data separately from any other telemetry, [create a new Application Insights resource](app-insights-create-new-resource.md).</span></span>
 * <span data-ttu-id="87ee9-131">如果您是聯結或比較與已設定使用 Application Insights 的應用程式的遙測資料，您可以針對該應用程式使用 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="87ee9-131">If you're joining or comparing your data with telemetry from an app that is already set up with Application Insights, then you can use hello resource for that app.</span></span>
 * <span data-ttu-id="87ee9-132">參與者或擁有者存取 toothat 資源。</span><span class="sxs-lookup"><span data-stu-id="87ee9-132">Contributor or owner access toothat resource.</span></span>
 
2. <span data-ttu-id="87ee9-133">Azure 儲存體中的 Blob。</span><span class="sxs-lookup"><span data-stu-id="87ee9-133">Azure storage.</span></span> <span data-ttu-id="87ee9-134">您上傳 tooAzure 存放裝置，並分析從該處取得您的資料。</span><span class="sxs-lookup"><span data-stu-id="87ee9-134">You upload tooAzure storage, and Analytics gets your data from there.</span></span> 

 * <span data-ttu-id="87ee9-135">我們建議您針對 blob 建立專用的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="87ee9-135">We recommend you create a dedicated storage account for your blobs.</span></span> <span data-ttu-id="87ee9-136">如果您的 blob 會共用與其他處理序，會在我們的處理程序 tooread 較長時間您的 blob。</span><span class="sxs-lookup"><span data-stu-id="87ee9-136">If your blobs are shared with other processes, it takes longer for our processes tooread your blobs.</span></span>


## <a name="define-your-schema"></a><span data-ttu-id="87ee9-137">定義結構描述</span><span class="sxs-lookup"><span data-stu-id="87ee9-137">Define your schema</span></span>

<span data-ttu-id="87ee9-138">您可以匯入資料之前，您必須定義*資料來源，*指定 hello 結構描述的資料。</span><span class="sxs-lookup"><span data-stu-id="87ee9-138">Before you can import data, you must define a *data source,* which specifies hello schema of your data.</span></span>
<span data-ttu-id="87ee9-139">您可以在單一的 Application Insights 資源 too50 資料來源</span><span class="sxs-lookup"><span data-stu-id="87ee9-139">You can have up too50 data sources in a single Application Insights resource</span></span>

1. <span data-ttu-id="87ee9-140">啟動 hello 資料來源精靈。</span><span class="sxs-lookup"><span data-stu-id="87ee9-140">Start hello data source wizard.</span></span> <span data-ttu-id="87ee9-141">使用 [新增資料來源] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="87ee9-141">Use "Add new data source" button.</span></span> <span data-ttu-id="87ee9-142">或者 - 按一下右上角的 [設定] 按鈕，然後在下拉式功能表中選擇 [資料來源]。</span><span class="sxs-lookup"><span data-stu-id="87ee9-142">Alternatively - click on settings button in right upper corner and choose "Data Sources" in dropdown menu.</span></span>

    ![新增資料來源](./media/app-insights-analytics-import/add-new-data-source.png)

    <span data-ttu-id="87ee9-144">提供新資料來源的名稱。</span><span class="sxs-lookup"><span data-stu-id="87ee9-144">Provide a name for your new data source.</span></span>

2. <span data-ttu-id="87ee9-145">定義您要上傳的 hello 檔案格式。</span><span class="sxs-lookup"><span data-stu-id="87ee9-145">Define format of hello files that you will upload.</span></span>

    <span data-ttu-id="87ee9-146">您可以手動定義 hello 格式，或上傳範例檔。</span><span class="sxs-lookup"><span data-stu-id="87ee9-146">You can either define hello format manually, or upload a sample file.</span></span>

    <span data-ttu-id="87ee9-147">如果 hello 資料是以 CSV 格式，hello hello 範例的第一個資料列可以是資料行標頭。</span><span class="sxs-lookup"><span data-stu-id="87ee9-147">If hello data is in CSV format, hello first row of hello sample can be column headers.</span></span> <span data-ttu-id="87ee9-148">您可以變更 hello hello 下一個步驟中的欄位名稱。</span><span class="sxs-lookup"><span data-stu-id="87ee9-148">You can change hello field names in hello next step.</span></span>

    <span data-ttu-id="87ee9-149">hello 範例應該包含至少 10 個資料列或資料的記錄。</span><span class="sxs-lookup"><span data-stu-id="87ee9-149">hello sample should include at least 10 rows or records of data.</span></span>

    <span data-ttu-id="87ee9-150">資料行或欄位名稱應包含英數字元名稱 (不含空格或標點符號)。</span><span class="sxs-lookup"><span data-stu-id="87ee9-150">Column or field names should have alphanumeric names (without spaces or punctuation).</span></span>

    ![上傳範例檔案](./media/app-insights-analytics-import/sample-data-file.png)


3. <span data-ttu-id="87ee9-152">有 hello 精靈的檢閱 hello 結構描述。</span><span class="sxs-lookup"><span data-stu-id="87ee9-152">Review hello schema that hello wizard has got.</span></span> <span data-ttu-id="87ee9-153">如果範例中的 hello 類型推斷，您可能需要 hello 資料行 tooadjust hello 推斷型別。</span><span class="sxs-lookup"><span data-stu-id="87ee9-153">If it inferred hello types from a sample, you might need tooadjust hello inferred types of hello columns.</span></span>

    ![檢閱 hello 推斷結構描述](./media/app-insights-analytics-import/data-source-review-schema.png)

 * <span data-ttu-id="87ee9-155">(選擇性。)上傳結構描述定義。</span><span class="sxs-lookup"><span data-stu-id="87ee9-155">(Optional.) Upload a schema definition.</span></span> <span data-ttu-id="87ee9-156">請參閱下面的 hello 格式。</span><span class="sxs-lookup"><span data-stu-id="87ee9-156">See hello format below.</span></span>

 * <span data-ttu-id="87ee9-157">選取時間戳記。</span><span class="sxs-lookup"><span data-stu-id="87ee9-157">Select a Timestamp.</span></span> <span data-ttu-id="87ee9-158">分析中的所有資料都必須都有時間戳記欄位。</span><span class="sxs-lookup"><span data-stu-id="87ee9-158">All data in Analytics must have a timestamp field.</span></span> <span data-ttu-id="87ee9-159">型別必須`datetime`，但不含 toobe 名為 'timestamp'。</span><span class="sxs-lookup"><span data-stu-id="87ee9-159">It must have type `datetime`, but it doesn't have toobe named 'timestamp'.</span></span> <span data-ttu-id="87ee9-160">如果您的資料包含的日期和時間以 ISO 格式的資料行，請選擇此選項為 hello 時間戳記資料行。</span><span class="sxs-lookup"><span data-stu-id="87ee9-160">If your data has a column containing a date and time in ISO format, choose this as hello timestamp column.</span></span> <span data-ttu-id="87ee9-161">否則，請選擇 "做為資料抵達 」，並 hello 匯入程序，將時間戳記欄位。</span><span class="sxs-lookup"><span data-stu-id="87ee9-161">Otherwise, choose "as data arrived", and hello import process will add a timestamp field.</span></span>

5. <span data-ttu-id="87ee9-162">建立 hello 資料來源。</span><span class="sxs-lookup"><span data-stu-id="87ee9-162">Create hello data source.</span></span>

### <a name="schema-definition-file-format"></a><span data-ttu-id="87ee9-163">結構描述定義檔案格式</span><span class="sxs-lookup"><span data-stu-id="87ee9-163">Schema definition file format</span></span>

<span data-ttu-id="87ee9-164">而不是編輯 UI 中的 hello 結構描述，您可以從檔案載入 hello 結構描述定義。</span><span class="sxs-lookup"><span data-stu-id="87ee9-164">Instead of editing hello schema in UI, you can load hello schema definition from a file.</span></span> <span data-ttu-id="87ee9-165">hello 結構描述定義格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="87ee9-165">hello schema definition format is as follows:</span></span> 

<span data-ttu-id="87ee9-166">以符號分隔的格式</span><span class="sxs-lookup"><span data-stu-id="87ee9-166">Delimited format</span></span> 
```
[ 
    {"location": "0", "name": "RequestName", "type": "string"}, 
    {"location": "1", "name": "timestamp", "type": "datetime"}, 
    {"location": "2", "name": "IPAddress", "type": "string"} 
] 
```

<span data-ttu-id="87ee9-167">JSON 格式</span><span class="sxs-lookup"><span data-stu-id="87ee9-167">JSON format</span></span> 
```
[ 
    {"location": "$.name", "name": "name", "type": "string"}, 
    {"location": "$.alias", "name": "alias", "type": "string"}, 
    {"location": "$.room", "name": "room", "type": "long"} 
]
```
 
<span data-ttu-id="87ee9-168">每個資料行被識別 hello 位置、 名稱和類型。</span><span class="sxs-lookup"><span data-stu-id="87ee9-168">Each column is identified by hello location, name and type.</span></span> 

* <span data-ttu-id="87ee9-169">位置 – 分隔的檔案格式，它是 hello 對應值的 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="87ee9-169">Location – For delimited file format it is hello position of hello mapped value.</span></span> <span data-ttu-id="87ee9-170">JSON 格式，則是 hello jpath hello 對應索引鍵。</span><span class="sxs-lookup"><span data-stu-id="87ee9-170">For JSON format, it is hello jpath of hello mapped key.</span></span>
* <span data-ttu-id="87ee9-171">名稱 – hello 顯示 hello 資料行的名稱。</span><span class="sxs-lookup"><span data-stu-id="87ee9-171">Name – hello displayed name of hello column.</span></span>
* <span data-ttu-id="87ee9-172">類型 – hello 該資料行資料類型。</span><span class="sxs-lookup"><span data-stu-id="87ee9-172">Type – hello data type of that column.</span></span>
 
<span data-ttu-id="87ee9-173">如果使用範例資料分隔的檔案格式，必須將所有資料行對應 hello 結構描述定義，然後 hello 結尾處新增新的資料行。</span><span class="sxs-lookup"><span data-stu-id="87ee9-173">In case a sample data was used and file format is delimited, hello schema definition must map all columns and add new columns at hello end.</span></span> 

<span data-ttu-id="87ee9-174">JSON 可讓 hello 資料的部分對應，因此 hello 的 JSON 格式的結構描述定義不具有 toomap 範例資料中找到的每個金鑰。</span><span class="sxs-lookup"><span data-stu-id="87ee9-174">JSON allows partial mapping of hello data, therefore hello schema definition of JSON format doesn’t have toomap every key which is found in a sample data.</span></span> <span data-ttu-id="87ee9-175">它也可以將對應資料行不是 hello 範例資料的一部分。</span><span class="sxs-lookup"><span data-stu-id="87ee9-175">It can also map columns which are not part of hello sample data.</span></span> 

## <a name="import-data"></a><span data-ttu-id="87ee9-176">匯入資料</span><span class="sxs-lookup"><span data-stu-id="87ee9-176">Import data</span></span>

<span data-ttu-id="87ee9-177">tooimport 資料，您將它上傳 tooAzure 儲存體、 建立便捷鍵，以及然後進行 REST API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="87ee9-177">tooimport data, you upload it tooAzure storage, create an access key for it, and then make a REST API call.</span></span>

![新增資料來源](./media/app-insights-analytics-import/analytics-upload-process.png)

<span data-ttu-id="87ee9-179">您可以執行 hello 程序之後，手動或自動化的系統 toodo 它固定間隔。</span><span class="sxs-lookup"><span data-stu-id="87ee9-179">You can perform hello following process manually, or set up an automated system toodo it at regular intervals.</span></span> <span data-ttu-id="87ee9-180">您需要 toofollow 依照您想要的 tooimport 每個資料區塊。</span><span class="sxs-lookup"><span data-stu-id="87ee9-180">You need toofollow these steps for each block of data you want tooimport.</span></span>

1. <span data-ttu-id="87ee9-181">Hello 資料上傳太[Azure blob 儲存體](../storage/blobs/storage-dotnet-how-to-use-blobs.md)。</span><span class="sxs-lookup"><span data-stu-id="87ee9-181">Upload hello data too[Azure blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> 

 * <span data-ttu-id="87ee9-182">Blob 可以是任何向上 too1GB 未壓縮大小。</span><span class="sxs-lookup"><span data-stu-id="87ee9-182">Blobs can be any size up too1GB uncompressed.</span></span> <span data-ttu-id="87ee9-183">從效能觀點來看，數百 MB 的大型 blob 很適合。</span><span class="sxs-lookup"><span data-stu-id="87ee9-183">Large blobs of hundreds of MB are ideal from a performance perspective.</span></span>
 * <span data-ttu-id="87ee9-184">您可以將它壓縮 Gzip tooimprove 上傳時間與 hello 資料 toobe 可用於查詢的延遲。</span><span class="sxs-lookup"><span data-stu-id="87ee9-184">You can compress it with Gzip tooimprove upload time and latency for hello data toobe available for query.</span></span> <span data-ttu-id="87ee9-185">使用 hello`.gz`檔案的副檔名。</span><span class="sxs-lookup"><span data-stu-id="87ee9-185">Use hello `.gz` filename extension.</span></span>
 * <span data-ttu-id="87ee9-186">基於此目的，從不同的服務會讓效能變 tooavoid 呼叫是最佳 toouse 個別儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="87ee9-186">It's best toouse a separate storage account for this purpose, tooavoid calls from different services slowing performance.</span></span>
 * <span data-ttu-id="87ee9-187">傳送資料時在高頻率，每隔幾秒，建議您使用 toouse 多超過一個儲存體帳戶，基於效能的考量。</span><span class="sxs-lookup"><span data-stu-id="87ee9-187">When sending data in high frequency, every few seconds, it is recommended toouse more than one storage account, for performance reasons.</span></span>

 
2. <span data-ttu-id="87ee9-188">[建立 hello blob 的共用存取簽章金鑰](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md)。</span><span class="sxs-lookup"><span data-stu-id="87ee9-188">[Create a Shared Access Signature key for hello blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span></span> <span data-ttu-id="87ee9-189">hello 金鑰應該具有一天的到期時間，並提供讀取權限。</span><span class="sxs-lookup"><span data-stu-id="87ee9-189">hello key should have an expiration period of one day and provide read access.</span></span>
3. <span data-ttu-id="87ee9-190">請等候資料的 Application Insights REST 呼叫 toonotify。</span><span class="sxs-lookup"><span data-stu-id="87ee9-190">Make a REST call toonotify Application Insights that data is waiting.</span></span>

 * <span data-ttu-id="87ee9-191">端點：`https://dc.services.visualstudio.com/v2/track`</span><span class="sxs-lookup"><span data-stu-id="87ee9-191">Endpoint: `https://dc.services.visualstudio.com/v2/track`</span></span>
 * <span data-ttu-id="87ee9-192">HTTP 方法：POST</span><span class="sxs-lookup"><span data-stu-id="87ee9-192">HTTP method: POST</span></span>
 * <span data-ttu-id="87ee9-193">承載：</span><span class="sxs-lookup"><span data-stu-id="87ee9-193">Payload:</span></span>

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

<span data-ttu-id="87ee9-194">hello 預留位置是：</span><span class="sxs-lookup"><span data-stu-id="87ee9-194">hello placeholders are:</span></span>

* <span data-ttu-id="87ee9-195">`Blob URI with Shared Access Key`： 取得此從 hello 程序建立金鑰。</span><span class="sxs-lookup"><span data-stu-id="87ee9-195">`Blob URI with Shared Access Key`: You get this from hello procedure for creating a key.</span></span> <span data-ttu-id="87ee9-196">它是特定 toohello blob。</span><span class="sxs-lookup"><span data-stu-id="87ee9-196">It is specific toohello blob.</span></span>
* <span data-ttu-id="87ee9-197">`Schema ID`: hello 您定義的結構描述產生的結構描述識別碼。</span><span class="sxs-lookup"><span data-stu-id="87ee9-197">`Schema ID`: hello schema ID generated for your defined schema.</span></span> <span data-ttu-id="87ee9-198">此 blob 中的 hello 資料應該符合 toohello 結構描述。</span><span class="sxs-lookup"><span data-stu-id="87ee9-198">hello data in this blob should conform toohello schema.</span></span>
* <span data-ttu-id="87ee9-199">`DateTime`: hello 時間在哪一個 hello 提交要求，UTC。</span><span class="sxs-lookup"><span data-stu-id="87ee9-199">`DateTime`: hello time at which hello request is submitted, UTC.</span></span> <span data-ttu-id="87ee9-200">我們接受這些格式︰ISO8601 (例如 "2016-01-01 13:45:01")；RFC822 ("Wed, 14 Dec 16 14:57:01 +0000")；RFC850 ("Wednesday, 14-Dec-16 14:57:00 UTC")；RFC1123 ("Wed, 14 Dec 2016 14:57:00 +0000")。</span><span class="sxs-lookup"><span data-stu-id="87ee9-200">We accept these formats: ISO8601 (like "2016-01-01 13:45:01"); RFC822 ("Wed, 14 Dec 16 14:57:01 +0000"); RFC850 ("Wednesday, 14-Dec-16 14:57:00 UTC"); RFC1123 ("Wed, 14 Dec 2016 14:57:00 +0000").</span></span>
* <span data-ttu-id="87ee9-201">您 `Instrumentation key` 的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="87ee9-201">`Instrumentation key` of your Application Insights resource.</span></span>

<span data-ttu-id="87ee9-202">hello 資料可在分析後幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="87ee9-202">hello data is available in Analytics after a few minutes.</span></span>

## <a name="error-responses"></a><span data-ttu-id="87ee9-203">錯誤回應</span><span class="sxs-lookup"><span data-stu-id="87ee9-203">Error responses</span></span>

* <span data-ttu-id="87ee9-204">**400 要求錯誤**： 指出該 hello 要求裝載無效。</span><span class="sxs-lookup"><span data-stu-id="87ee9-204">**400 bad request**: indicates that hello request payload is invalid.</span></span> <span data-ttu-id="87ee9-205">勾選：</span><span class="sxs-lookup"><span data-stu-id="87ee9-205">Check:</span></span>
 * <span data-ttu-id="87ee9-206">修正動態檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="87ee9-206">Correct instrumentation key.</span></span>
 * <span data-ttu-id="87ee9-207">有效的時間值。</span><span class="sxs-lookup"><span data-stu-id="87ee9-207">Valid time value.</span></span> <span data-ttu-id="87ee9-208">它應該是 hello 現在時間-UTC 時間。</span><span class="sxs-lookup"><span data-stu-id="87ee9-208">It should be hello time now in UTC.</span></span>
 * <span data-ttu-id="87ee9-209">JSON 的 hello 事件符合 toohello 結構描述。</span><span class="sxs-lookup"><span data-stu-id="87ee9-209">JSON of hello event conforms toohello schema.</span></span>
* <span data-ttu-id="87ee9-210">**403 禁止**： 不能存取您先前曾傳送嗨 blob。</span><span class="sxs-lookup"><span data-stu-id="87ee9-210">**403 Forbidden**: hello blob you've sent is not accessible.</span></span> <span data-ttu-id="87ee9-211">請確定該 hello 共用的存取金鑰無效，而且尚未過期。</span><span class="sxs-lookup"><span data-stu-id="87ee9-211">Make sure that hello shared access key is valid and has not expired.</span></span>
* <span data-ttu-id="87ee9-212">**404 找不到**：</span><span class="sxs-lookup"><span data-stu-id="87ee9-212">**404 Not Found**:</span></span>
 * <span data-ttu-id="87ee9-213">hello blob 不存在。</span><span class="sxs-lookup"><span data-stu-id="87ee9-213">hello blob doesn't exist.</span></span>
 * <span data-ttu-id="87ee9-214">hello sourceId 是錯誤。</span><span class="sxs-lookup"><span data-stu-id="87ee9-214">hello sourceId is wrong.</span></span>

<span data-ttu-id="87ee9-215">Hello 回應錯誤訊息中使用更詳細的資訊。</span><span class="sxs-lookup"><span data-stu-id="87ee9-215">More detailed information is available in hello response error message.</span></span>


## <a name="sample-code"></a><span data-ttu-id="87ee9-216">範例程式碼</span><span class="sxs-lookup"><span data-stu-id="87ee9-216">Sample code</span></span>

<span data-ttu-id="87ee9-217">此程式碼使用 hello [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="87ee9-217">This code uses hello [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) NuGet package.</span></span>

### <a name="classes"></a><span data-ttu-id="87ee9-218">類別</span><span class="sxs-lookup"><span data-stu-id="87ee9-218">Classes</span></span>

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

### <a name="ingest-data"></a><span data-ttu-id="87ee9-219">擷取資料</span><span class="sxs-lookup"><span data-stu-id="87ee9-219">Ingest data</span></span>

<span data-ttu-id="87ee9-220">針對每個 blob 使用此程式碼。</span><span class="sxs-lookup"><span data-stu-id="87ee9-220">Use this code for each blob.</span></span> 

```C#
   AnalyticsDataSourceClient client = new AnalyticsDataSourceClient(); 

   var ingestionRequest = new AnalyticsDataSourceIngestionRequest("iKey", "sourceId", "blobUrlWithSas"); 

   bool success = await client.RequestBlobIngestion(ingestionRequest);
```

## <a name="next-steps"></a><span data-ttu-id="87ee9-221">後續步驟</span><span class="sxs-lookup"><span data-stu-id="87ee9-221">Next steps</span></span>

* [<span data-ttu-id="87ee9-222">教學課程的 hello 記錄分析查詢語言</span><span class="sxs-lookup"><span data-stu-id="87ee9-222">Tour of hello Log Analytics query language</span></span>](app-insights-analytics-tour.md)
* [<span data-ttu-id="87ee9-223">使用*Logstash* toosend 資料 tooApplication Insights</span><span class="sxs-lookup"><span data-stu-id="87ee9-223">Use *Logstash* toosend data tooApplication Insights</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
