---
title: "從 Application Insights 連續匯出遙測 | Microsoft Docs"
description: "匯出診斷和使用量資料至 Microsoft Azure 中的儲存體，並從那裡下載。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 5b859200-b484-4c98-9d9f-929713f1030c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: bwren
ms.openlocfilehash: 6ac3bda5101593b5ca66b4c9035e2fdac9d1e833
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="export-telemetry-from-application-insights"></a><span data-ttu-id="661fa-103">從 Application Insights 匯出遙測</span><span class="sxs-lookup"><span data-stu-id="661fa-103">Export telemetry from Application Insights</span></span>
<span data-ttu-id="661fa-104">想要讓遙測保留比標準保留期限還久的時間？</span><span class="sxs-lookup"><span data-stu-id="661fa-104">Want to keep your telemetry for longer than the standard retention period?</span></span> <span data-ttu-id="661fa-105">或以某些特殊方式處理它？</span><span class="sxs-lookup"><span data-stu-id="661fa-105">Or process it in some specialized way?</span></span> <span data-ttu-id="661fa-106">連續匯出很適合此用途。</span><span class="sxs-lookup"><span data-stu-id="661fa-106">Continuous Export is ideal for this.</span></span> <span data-ttu-id="661fa-107">在 Application Insights 入口網站中看見的事件，可以使用 JSON 格式匯出到 Microsoft Azure 中的儲存體。</span><span class="sxs-lookup"><span data-stu-id="661fa-107">The events you see in the Application Insights portal can be exported to storage in Microsoft Azure in JSON format.</span></span> <span data-ttu-id="661fa-108">從那裡，您可以下載資料並編寫處理所需的任何程式碼。</span><span class="sxs-lookup"><span data-stu-id="661fa-108">From there you can download your data and write whatever code you need to process it.</span></span>  

<span data-ttu-id="661fa-109">使用連續匯出，可能會產生額外的費用。</span><span class="sxs-lookup"><span data-stu-id="661fa-109">Using Continuous Export may incur an additional charge.</span></span> <span data-ttu-id="661fa-110">請檢查您的[定價模式](http://azure.microsoft.com/pricing/details/application-insights/)。</span><span class="sxs-lookup"><span data-stu-id="661fa-110">Check your [pricing model](http://azure.microsoft.com/pricing/details/application-insights/).</span></span>

<span data-ttu-id="661fa-111">在設定連續匯出之前，您可能要考慮某些替代作法︰</span><span class="sxs-lookup"><span data-stu-id="661fa-111">Before you set up continuous export, there are some alternatives you might want to consider:</span></span>

* <span data-ttu-id="661fa-112">計量或搜尋刀鋒視窗頂端的 [匯出] 按鈕，可讓您傳送資料表和圖表到 Excel 試算表。</span><span class="sxs-lookup"><span data-stu-id="661fa-112">The Export button at the top of a metrics or search blade lets you transfer tables and charts to an Excel spreadsheet.</span></span>

* <span data-ttu-id="661fa-113">[分析](app-insights-analytics.md) 可提供功能強大的遙測查詢語言。</span><span class="sxs-lookup"><span data-stu-id="661fa-113">[Analytics](app-insights-analytics.md) provides a powerful query language for telemetry.</span></span> <span data-ttu-id="661fa-114">它也可以匯出結果。</span><span class="sxs-lookup"><span data-stu-id="661fa-114">It can also export results.</span></span>
* <span data-ttu-id="661fa-115">如果您想要 [在 Power BI 中探索資料](app-insights-export-power-bi.md)，不需要用到「連續匯出」也可以這麼做。</span><span class="sxs-lookup"><span data-stu-id="661fa-115">If you're looking to [explore your data in Power BI](app-insights-export-power-bi.md), you can do that without using Continuous Export.</span></span>
* <span data-ttu-id="661fa-116">[資料存取 REST API](https://dev.applicationinsights.io/) 可讓您以程式設計方式存取您的遙測。</span><span class="sxs-lookup"><span data-stu-id="661fa-116">The [Data access REST API](https://dev.applicationinsights.io/) lets you access your telemetry programmatically.</span></span>

<span data-ttu-id="661fa-117">在「連續匯出」將您的資料複製到儲存體 (資料可在此依您喜好的時間長短存放) 之後，資料仍然會在 Application Insights 中依一般的[保留期間](app-insights-data-retention-privacy.md)可供使用。</span><span class="sxs-lookup"><span data-stu-id="661fa-117">After Continuous Export copies your data to storage (where it can stay for as long as you like), it's still available in Application Insights for the usual [retention period](app-insights-data-retention-privacy.md).</span></span>

## <span data-ttu-id="661fa-118"><a name="setup"></a> 建立連續匯出</span><span class="sxs-lookup"><span data-stu-id="661fa-118"><a name="setup"></a> Create a Continuous Export</span></span>
1. <span data-ttu-id="661fa-119">在您應用程式的 Application Insights 資源中，開啟 [連續匯出]，然後選擇 [新增]：</span><span class="sxs-lookup"><span data-stu-id="661fa-119">In the Application Insights resource for your app, open Continuous Export and choose **Add**:</span></span>

    ![向下捲動並按一下 [連續匯出]](./media/app-insights-export-telemetry/01-export.png)

2. <span data-ttu-id="661fa-121">選擇您想要匯出的遙測資料類型。</span><span class="sxs-lookup"><span data-stu-id="661fa-121">Choose the telemetry data types you want to export.</span></span>

3. <span data-ttu-id="661fa-122">建立或選取要用來儲存資料的 [Azure 儲存體帳戶](../storage/common/storage-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="661fa-122">Create or select an [Azure storage account](../storage/common/storage-introduction.md) where you want to store the data.</span></span>

    > [!Warning]
    > <span data-ttu-id="661fa-123">根據預設，儲存體位置將設為與您 Application Insights 資源相同的地理區域。</span><span class="sxs-lookup"><span data-stu-id="661fa-123">By default, the storage location will be set to the same geographical region as your Application Insights resource.</span></span> <span data-ttu-id="661fa-124">如果您儲存在不同的區域中，可能會產生傳輸費用。</span><span class="sxs-lookup"><span data-stu-id="661fa-124">If you store in a different region, you may incur transfer charges.</span></span>

    ![按一下 [加入]、[匯出目的地]、[儲存體帳戶]，然後建立新儲存區或選擇現有儲存區](./media/app-insights-export-telemetry/02-add.png)

4. <span data-ttu-id="661fa-126">建立或選取儲存體中的容器︰</span><span class="sxs-lookup"><span data-stu-id="661fa-126">Create or select a container in the storage:</span></span>

    ![按一下 [選擇事件類型]](./media/app-insights-export-telemetry/create-container.png)

<span data-ttu-id="661fa-128">建立匯出之後，就會開始進行。</span><span class="sxs-lookup"><span data-stu-id="661fa-128">Once you've created your export, it starts going.</span></span> <span data-ttu-id="661fa-129">您只會取得建立匯出之後送抵的資料。</span><span class="sxs-lookup"><span data-stu-id="661fa-129">You only get data that arrives after you create the export.</span></span>

<span data-ttu-id="661fa-130">資料出現在儲存體中之前可能有大約一小時的延遲。</span><span class="sxs-lookup"><span data-stu-id="661fa-130">There can be a delay of about an hour before data appears in the storage.</span></span>

### <a name="to-edit-continuous-export"></a><span data-ttu-id="661fa-131">若要編輯連續匯出</span><span class="sxs-lookup"><span data-stu-id="661fa-131">To edit continuous export</span></span>

<span data-ttu-id="661fa-132">如果稍後想要變更事件類型，只需要編輯匯出：</span><span class="sxs-lookup"><span data-stu-id="661fa-132">If you want to change the event types later, just edit the export:</span></span>

![按一下 [選擇事件類型]](./media/app-insights-export-telemetry/05-edit.png)

### <a name="to-stop-continuous-export"></a><span data-ttu-id="661fa-134">若要停止連續匯出</span><span class="sxs-lookup"><span data-stu-id="661fa-134">To stop continuous export</span></span>

<span data-ttu-id="661fa-135">若要停止匯出，請按一下 [停用]。</span><span class="sxs-lookup"><span data-stu-id="661fa-135">To stop the export, click Disable.</span></span> <span data-ttu-id="661fa-136">再次按一下 [啟用] 時，匯出將會以新資料重新啟動。</span><span class="sxs-lookup"><span data-stu-id="661fa-136">When you click Enable again, the export will restart with new data.</span></span> <span data-ttu-id="661fa-137">您無法取得在停用匯出時送抵入口網站的資料。</span><span class="sxs-lookup"><span data-stu-id="661fa-137">You won't get the data that arrived in the portal while export was disabled.</span></span>

<span data-ttu-id="661fa-138">若要永久停止匯出，請刪除它。</span><span class="sxs-lookup"><span data-stu-id="661fa-138">To stop the export permanently, delete it.</span></span> <span data-ttu-id="661fa-139">這麼做不會將您的資料從儲存體刪除。</span><span class="sxs-lookup"><span data-stu-id="661fa-139">Doing so doesn't delete your data from storage.</span></span>

### <a name="cant-add-or-change-an-export"></a><span data-ttu-id="661fa-140">無法加入或變更匯出？</span><span class="sxs-lookup"><span data-stu-id="661fa-140">Can't add or change an export?</span></span>
* <span data-ttu-id="661fa-141">若要加入或變更匯出，您需要擁有者、參與者或 Application Insights 參與者存取權。</span><span class="sxs-lookup"><span data-stu-id="661fa-141">To add or change exports, you need Owner, Contributor or Application Insights Contributor access rights.</span></span> <span data-ttu-id="661fa-142">[了解角色][roles]。</span><span class="sxs-lookup"><span data-stu-id="661fa-142">[Learn about roles][roles].</span></span>

## <span data-ttu-id="661fa-143"><a name="analyze"></a> 您取得什麼事件？</span><span class="sxs-lookup"><span data-stu-id="661fa-143"><a name="analyze"></a> What events do you get?</span></span>
<span data-ttu-id="661fa-144">匯出的資料是我們從您的應用程式接收的原始遙測，只不過我們加入了從用戶端 IP 位址計算的位置資料。</span><span class="sxs-lookup"><span data-stu-id="661fa-144">The exported data is the raw telemetry we receive from your application, except that we add location data which we calculate from the client IP address.</span></span>

<span data-ttu-id="661fa-145">[取樣](app-insights-sampling.md) 已捨棄的資料不會包含在匯出的資料中。</span><span class="sxs-lookup"><span data-stu-id="661fa-145">Data that has been discarded by [sampling](app-insights-sampling.md) is not included in the exported data.</span></span>

<span data-ttu-id="661fa-146">未包含其他計算的度量。</span><span class="sxs-lookup"><span data-stu-id="661fa-146">Other calculated metrics are not included.</span></span> <span data-ttu-id="661fa-147">例如，我們不會匯出平均 CPU 使用率，但我們會匯出用以計算平均的原始遙測。</span><span class="sxs-lookup"><span data-stu-id="661fa-147">For example, we don't export average CPU utilisation, but we do export the raw telemetry from which the average is computed.</span></span>

<span data-ttu-id="661fa-148">該資料也包含您曾設定之 [可用性 Web 測試](app-insights-monitor-web-app-availability.md) 的任何結果。</span><span class="sxs-lookup"><span data-stu-id="661fa-148">The data also includes the results of any [availability web tests](app-insights-monitor-web-app-availability.md) that you have set up.</span></span>

> [!NOTE]
> <span data-ttu-id="661fa-149">**取樣**</span><span class="sxs-lookup"><span data-stu-id="661fa-149">**Sampling.**</span></span> <span data-ttu-id="661fa-150">如果應用程式會傳送大量資料，取樣功能或許會運作，並只傳送一小部分產生的遙測。</span><span class="sxs-lookup"><span data-stu-id="661fa-150">If your application sends a lot of data, the sampling feature may operate and send only a fraction of the generated telemetry.</span></span> [<span data-ttu-id="661fa-151">深入了解取樣。</span><span class="sxs-lookup"><span data-stu-id="661fa-151">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <span data-ttu-id="661fa-152"><a name="get"></a> 檢查資料</span><span class="sxs-lookup"><span data-stu-id="661fa-152"><a name="get"></a> Inspect the data</span></span>
<span data-ttu-id="661fa-153">您可以直接在入口網站中檢查儲存體。</span><span class="sxs-lookup"><span data-stu-id="661fa-153">You can inspect the storage directly in the portal.</span></span> <span data-ttu-id="661fa-154">按一下 [瀏覽]、選取您的儲存體帳戶，然後開啟 [容器]。</span><span class="sxs-lookup"><span data-stu-id="661fa-154">Click **Browse**, select your storage account, and then open **Containers**.</span></span>

<span data-ttu-id="661fa-155">若要在 Visual Studio 中檢查 Azure 儲存體，請依序開啟 [檢視]、[Cloud Explorer]。</span><span class="sxs-lookup"><span data-stu-id="661fa-155">To inspect Azure storage in Visual Studio, open **View**, **Cloud Explorer**.</span></span> <span data-ttu-id="661fa-156">(如果您沒有該功能表命令，則必須安裝 Azure SDK：開啟 [新增專案] 對話方塊，展開 [Visual C#]/[Cloud]，然後選擇 [取得 Microsoft Azure SDK for .NET]。)</span><span class="sxs-lookup"><span data-stu-id="661fa-156">(If you don't have that menu command, you need to install the Azure SDK: Open the **New Project** dialog, expand Visual C#/Cloud and choose **Get Microsoft Azure SDK for .NET**.)</span></span>

<span data-ttu-id="661fa-157">當您開啟 Blob 存放區時，您會看到含有一組 Blob 檔案的容器。</span><span class="sxs-lookup"><span data-stu-id="661fa-157">When you open your blob store, you'll see a container with a set of blob files.</span></span> <span data-ttu-id="661fa-158">衍生自您 Application Insights 的資源名稱、其檢測金鑰、遙測-類型/日期/時間之每個檔案的 URI。</span><span class="sxs-lookup"><span data-stu-id="661fa-158">The URI of each file derived from your Application Insights resource name, its instrumentation key, telemetry-type/date/time.</span></span> <span data-ttu-id="661fa-159">(資源名稱全部小寫，而檢測金鑰會省略連字號。)</span><span class="sxs-lookup"><span data-stu-id="661fa-159">(The resource name is all lowercase, and the instrumentation key omits dashes.)</span></span>

![使用適合的工具檢查 Blob 儲存區](./media/app-insights-export-telemetry/04-data.png)

<span data-ttu-id="661fa-161">日期和時間為 UTC，並且是遙測存放在儲存區的時間 - 而不是產生的時間。</span><span class="sxs-lookup"><span data-stu-id="661fa-161">The date and time are UTC and are when the telemetry was deposited in the store - not the time it was generated.</span></span> <span data-ttu-id="661fa-162">因此，如果您編寫程式碼來下載資料，它可以透過資料線性地移動。</span><span class="sxs-lookup"><span data-stu-id="661fa-162">So if you write code to download the data, it can move linearly through the data.</span></span>

<span data-ttu-id="661fa-163">以下是路徑的格式︰</span><span class="sxs-lookup"><span data-stu-id="661fa-163">Here's the form of the path:</span></span>

    $"{applicationName}_{instrumentationKey}/{type}/{blobDeliveryTimeUtc:yyyy-MM-dd}/{ blobDeliveryTimeUtc:HH}/{blobId}_{blobCreationTimeUtc:yyyyMMdd_HHmmss}.blob"

<span data-ttu-id="661fa-164">Where</span><span class="sxs-lookup"><span data-stu-id="661fa-164">Where</span></span>

* <span data-ttu-id="661fa-165">`blobCreationTimeUtc` 是在內部暫存儲存體中建立 Blob 的時間</span><span class="sxs-lookup"><span data-stu-id="661fa-165">`blobCreationTimeUtc` is time when blob was created in the internal staging storage</span></span>
* <span data-ttu-id="661fa-166">`blobDeliveryTimeUtc` 是將 Blob 複製到匯出目的地儲存體的時間</span><span class="sxs-lookup"><span data-stu-id="661fa-166">`blobDeliveryTimeUtc` is the time when blob is copied to the export destination storage</span></span>

## <span data-ttu-id="661fa-167"><a name="format"></a> 資料格式</span><span class="sxs-lookup"><span data-stu-id="661fa-167"><a name="format"></a> Data format</span></span>
* <span data-ttu-id="661fa-168">每個 Blob 是包含多個以 '\n' 分隔的列的文字檔案。</span><span class="sxs-lookup"><span data-stu-id="661fa-168">Each blob is a text file that contains multiple '\n'-separated rows.</span></span> <span data-ttu-id="661fa-169">它包含大約半分鐘的時間內所處理的遙測。</span><span class="sxs-lookup"><span data-stu-id="661fa-169">It contains the telemetry processed over a time period of roughly half a minute.</span></span>
* <span data-ttu-id="661fa-170">每個資料列都代表遙測資料點，例如要求或頁面檢視。</span><span class="sxs-lookup"><span data-stu-id="661fa-170">Each row represents a telemetry data point such as a request or page view.</span></span>
* <span data-ttu-id="661fa-171">每列是未格式化的 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="661fa-171">Each row is an unformatted JSON document.</span></span> <span data-ttu-id="661fa-172">如果您想要靜靜地仔細觀看，請在 Visual Studio 中開啟，並依序選擇 [編輯]、[進階]、[格式檔案]：</span><span class="sxs-lookup"><span data-stu-id="661fa-172">If you want to sit and stare at it, open it in Visual Studio and choose Edit, Advanced, Format File:</span></span>

![使用合適的工具檢視遙測](./media/app-insights-export-telemetry/06-json.png)

<span data-ttu-id="661fa-174">時間期間依刻度為單位，10000 刻度 = 1 毫秒。</span><span class="sxs-lookup"><span data-stu-id="661fa-174">Time durations are in ticks, where 10 000 ticks = 1ms.</span></span> <span data-ttu-id="661fa-175">例如，這些值顯示從瀏覽器傳送要求用了 1 毫秒的時間，接收它用了 3 毫秒，以及在瀏覽器中處理頁面用了 1.8 秒：</span><span class="sxs-lookup"><span data-stu-id="661fa-175">For example, these values show a time of 1ms to send a request from the browser, 3ms to receive it, and 1.8s to process the page in the browser:</span></span>

    "sendRequest": {"value": 10000.0},
    "receiveRequest": {"value": 30000.0},
    "clientProcess": {"value": 17970000.0}

[<span data-ttu-id="661fa-176">屬性類型和值的詳細資料模型參考。</span><span class="sxs-lookup"><span data-stu-id="661fa-176">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)

## <a name="processing-the-data"></a><span data-ttu-id="661fa-177">處理資料</span><span class="sxs-lookup"><span data-stu-id="661fa-177">Processing the data</span></span>
<span data-ttu-id="661fa-178">就小型規模而言，您可以編寫一些程式碼來取出您的資料，將它讀取為試算表等等。</span><span class="sxs-lookup"><span data-stu-id="661fa-178">On a small scale, you can write some code to pull apart your data, read it into a spreadsheet, and so on.</span></span> <span data-ttu-id="661fa-179">例如：</span><span class="sxs-lookup"><span data-stu-id="661fa-179">For example:</span></span>

    private IEnumerable<T> DeserializeMany<T>(string folderName)
    {
      var files = Directory.EnumerateFiles(folderName, "*.blob", SearchOption.AllDirectories);
      foreach (var file in files)
      {
         using (var fileReader = File.OpenText(file))
         {
            string fileContent = fileReader.ReadToEnd();
            IEnumerable<string> entities = fileContent.Split('\n').Where(s => !string.IsNullOrWhiteSpace(s));
            foreach (var entity in entities)
            {
                yield return JsonConvert.DeserializeObject<T>(entity);
            }
         }
      }
    }

<span data-ttu-id="661fa-180">如需較大型的程式碼範例，請參閱[使用背景工作角色][exportasa]。</span><span class="sxs-lookup"><span data-stu-id="661fa-180">For a larger code sample, see [using a worker role][exportasa].</span></span>

## <span data-ttu-id="661fa-181"><a name="delete"></a>刪除舊資料</span><span class="sxs-lookup"><span data-stu-id="661fa-181"><a name="delete"></a>Delete your old data</span></span>
<span data-ttu-id="661fa-182">請注意，您負責管理儲存容量，以及在必要時刪除舊資料。</span><span class="sxs-lookup"><span data-stu-id="661fa-182">Please note that you are responsible for managing your storage capacity and deleting the old data if necessary.</span></span>

## <a name="if-you-regenerate-your-storage-key"></a><span data-ttu-id="661fa-183">如果您重新產生儲存體金鑰...</span><span class="sxs-lookup"><span data-stu-id="661fa-183">If you regenerate your storage key...</span></span>
<span data-ttu-id="661fa-184">如果您變更儲存體的金鑰，連續匯出將停止運作。</span><span class="sxs-lookup"><span data-stu-id="661fa-184">If you change the key to your storage, continuous export will stop working.</span></span> <span data-ttu-id="661fa-185">您將在 Azure 帳戶中看到通知。</span><span class="sxs-lookup"><span data-stu-id="661fa-185">You'll see a notification in your Azure account.</span></span>

<span data-ttu-id="661fa-186">開啟 [連續匯出] 分頁，並編輯您的匯出。</span><span class="sxs-lookup"><span data-stu-id="661fa-186">Open the Continuous Export blade and edit your export.</span></span> <span data-ttu-id="661fa-187">編輯 [匯出目的地]，但只保留選取相同的儲存體。</span><span class="sxs-lookup"><span data-stu-id="661fa-187">Edit the Export Destination, but just leave the same storage selected.</span></span> <span data-ttu-id="661fa-188">按一下 [確定] 以確認。</span><span class="sxs-lookup"><span data-stu-id="661fa-188">Click OK to confirm.</span></span>

![編輯連續匯出，開啟並關閉匯出目的地。](./media/app-insights-export-telemetry/07-resetstore.png)

<span data-ttu-id="661fa-190">連續匯出將重新開始。</span><span class="sxs-lookup"><span data-stu-id="661fa-190">The continuous export will restart.</span></span>

## <a name="export-samples"></a><span data-ttu-id="661fa-191">匯出範例</span><span class="sxs-lookup"><span data-stu-id="661fa-191">Export samples</span></span>

* <span data-ttu-id="661fa-192">[使用串流分析匯出至 SQL][exportasa]</span><span class="sxs-lookup"><span data-stu-id="661fa-192">[Export to SQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="661fa-193">串流分析範例 2</span><span class="sxs-lookup"><span data-stu-id="661fa-193">Stream Analytics sample 2</span></span>](app-insights-export-stream-analytics.md)

<span data-ttu-id="661fa-194">就更大型規模而言，請考慮 [HDInsight](https://azure.microsoft.com/services/hdinsight/) - 雲端中的 Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="661fa-194">On larger scales, consider [HDInsight](https://azure.microsoft.com/services/hdinsight/) - Hadoop clusters in the cloud.</span></span> <span data-ttu-id="661fa-195">HDInsight 提供各種管理和分析巨量資料的技術，您可以使用它來處理已從 Application Insights 匯出的資料。</span><span class="sxs-lookup"><span data-stu-id="661fa-195">HDInsight provides a variety of technologies for managing and analyzing big data, and you could use it to process data that has been exported from Application Insights.</span></span>

## <a name="q--a"></a><span data-ttu-id="661fa-196">問答集</span><span class="sxs-lookup"><span data-stu-id="661fa-196">Q & A</span></span>
* <span data-ttu-id="661fa-197">*但我想要的只是一次性下載圖表。*</span><span class="sxs-lookup"><span data-stu-id="661fa-197">*But all I want is a one-time download of a chart.*</span></span>  

    <span data-ttu-id="661fa-198">是的，您可以這麼做。</span><span class="sxs-lookup"><span data-stu-id="661fa-198">Yes, you can do that.</span></span> <span data-ttu-id="661fa-199">在刀鋒視窗頂端，按一下 [ **匯出資料**]。</span><span class="sxs-lookup"><span data-stu-id="661fa-199">At the top of the blade, click **Export Data**.</span></span>
* <span data-ttu-id="661fa-200">*我設定匯出，但我的儲存區中沒有資料。*</span><span class="sxs-lookup"><span data-stu-id="661fa-200">*I set up an export, but there's no data in my store.*</span></span>

    <span data-ttu-id="661fa-201">自從設定匯出之後，Application Insights 是否從您的應用程式收到任何遙測？</span><span class="sxs-lookup"><span data-stu-id="661fa-201">Did Application Insights receive any telemetry from your app since you set up the export?</span></span> <span data-ttu-id="661fa-202">您將只會收到新資料。</span><span class="sxs-lookup"><span data-stu-id="661fa-202">You'll only receive new data.</span></span>
* <span data-ttu-id="661fa-203">*我嘗試設定匯出，但被拒絕存取*</span><span class="sxs-lookup"><span data-stu-id="661fa-203">*I tried to set up an export, but was denied access*</span></span>

    <span data-ttu-id="661fa-204">如果帳戶是組織所擁有，您必須是擁有者或參與者群組的成員。</span><span class="sxs-lookup"><span data-stu-id="661fa-204">If the account is owned by your organization, you have to be a member of the owners or contributors groups.</span></span>
* <span data-ttu-id="661fa-205">*我是否能直接匯出到我自己的內部部署儲存區？*</span><span class="sxs-lookup"><span data-stu-id="661fa-205">*Can I export straight to my own on-premises store?*</span></span>

    <span data-ttu-id="661fa-206">否，抱歉。</span><span class="sxs-lookup"><span data-stu-id="661fa-206">No, sorry.</span></span> <span data-ttu-id="661fa-207">我們的匯出引擎目前僅適用於 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="661fa-207">Our export engine currently only works with Azure storage at this time.</span></span>  
* <span data-ttu-id="661fa-208">*放置在我的儲存區中的資料量有任何限制？*</span><span class="sxs-lookup"><span data-stu-id="661fa-208">*Is there any limit to the amount of data you put in my store?*</span></span>

    <span data-ttu-id="661fa-209">沒有。</span><span class="sxs-lookup"><span data-stu-id="661fa-209">No.</span></span> <span data-ttu-id="661fa-210">我們將持續送入資料，直到刪除匯出為止。</span><span class="sxs-lookup"><span data-stu-id="661fa-210">We'll keep pushing data in until you delete the export.</span></span> <span data-ttu-id="661fa-211">如果我們到達 Blob 儲存體的外部限制，將會停止，但那個限制很大。</span><span class="sxs-lookup"><span data-stu-id="661fa-211">We'll stop if we hit the outer limits for blob storage, but that's pretty huge.</span></span> <span data-ttu-id="661fa-212">您可以自行控制使用的儲存體數量。</span><span class="sxs-lookup"><span data-stu-id="661fa-212">It's up to you to control how much storage you use.</span></span>  
* <span data-ttu-id="661fa-213">*應該在儲存體中看到多少 Blob？*</span><span class="sxs-lookup"><span data-stu-id="661fa-213">*How many blobs should I see in the storage?*</span></span>

  * <span data-ttu-id="661fa-214">針對您選取要匯出的每個資料類型，會每分鐘建立一個新的 Blob (如果有可用的資料)。</span><span class="sxs-lookup"><span data-stu-id="661fa-214">For every data type you selected to export, a new blob is created every minute (if data is available).</span></span>
  * <span data-ttu-id="661fa-215">此外，針對具有高流量的應用程式，則會配置額外的分割單位。</span><span class="sxs-lookup"><span data-stu-id="661fa-215">In addition, for applications with high traffic, additional partition units are allocated.</span></span> <span data-ttu-id="661fa-216">在此情況下，每個單位會每分鐘建立一個 Blob。</span><span class="sxs-lookup"><span data-stu-id="661fa-216">In this case each unit creates a blob every minute.</span></span>
* <span data-ttu-id="661fa-217">*我對我的儲存體重新產生了金鑰，或變更了容器的名稱，現在匯出沒有作用。*</span><span class="sxs-lookup"><span data-stu-id="661fa-217">*I regenerated the key to my storage or changed the name of the container, and now the export doesn't work.*</span></span>

    <span data-ttu-id="661fa-218">編輯匯出並開啟匯出目的地分頁。</span><span class="sxs-lookup"><span data-stu-id="661fa-218">Edit the export and open the export destination blade.</span></span> <span data-ttu-id="661fa-219">照舊保留選取相關的儲存體，並按一下 [確定] 來確認。</span><span class="sxs-lookup"><span data-stu-id="661fa-219">Leave the same storage selected as before, and click OK to confirm.</span></span> <span data-ttu-id="661fa-220">匯出將重新開始。</span><span class="sxs-lookup"><span data-stu-id="661fa-220">Export will restart.</span></span> <span data-ttu-id="661fa-221">如果變更是在最近幾天內，您不會遺失資料。</span><span class="sxs-lookup"><span data-stu-id="661fa-221">If the change was within the past few days, you won't lose data.</span></span>
* <span data-ttu-id="661fa-222">*我可以暫停匯出嗎？*</span><span class="sxs-lookup"><span data-stu-id="661fa-222">*Can I pause the export?*</span></span>

    <span data-ttu-id="661fa-223">是。</span><span class="sxs-lookup"><span data-stu-id="661fa-223">Yes.</span></span> <span data-ttu-id="661fa-224">按一下 [停用]。</span><span class="sxs-lookup"><span data-stu-id="661fa-224">Click Disable.</span></span>

## <a name="code-samples"></a><span data-ttu-id="661fa-225">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="661fa-225">Code samples</span></span>

* [<span data-ttu-id="661fa-226">串流分析範例</span><span class="sxs-lookup"><span data-stu-id="661fa-226">Stream Analytics sample</span></span>](app-insights-export-stream-analytics.md)
* <span data-ttu-id="661fa-227">[使用串流分析匯出至 SQL][exportasa]</span><span class="sxs-lookup"><span data-stu-id="661fa-227">[Export to SQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="661fa-228">屬性類型和值的詳細資料模型參考。</span><span class="sxs-lookup"><span data-stu-id="661fa-228">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)

<!--Link references-->

[exportasa]: app-insights-code-sample-export-sql-stream-analytics.md
[roles]: app-insights-resources-roles-access-control.md
