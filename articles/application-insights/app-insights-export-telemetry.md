---
title: "從 Application Insights 遙測 aaaContinuous 匯出 |Microsoft 文件"
description: "匯出 Microsoft Azure 中的診斷和使用方式資料 toostorage，並從該處下載。"
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
ms.openlocfilehash: be9ed7e05922c1c8186df9ca4e642862adaa5fd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="export-telemetry-from-application-insights"></a><span data-ttu-id="f6d8a-103">從 Application Insights 匯出遙測</span><span class="sxs-lookup"><span data-stu-id="f6d8a-103">Export telemetry from Application Insights</span></span>
<span data-ttu-id="f6d8a-104">要使用 tookeep 您遙測超過 hello 標準保留期間？</span><span class="sxs-lookup"><span data-stu-id="f6d8a-104">Want tookeep your telemetry for longer than hello standard retention period?</span></span> <span data-ttu-id="f6d8a-105">或以某些特殊方式處理它？</span><span class="sxs-lookup"><span data-stu-id="f6d8a-105">Or process it in some specialized way?</span></span> <span data-ttu-id="f6d8a-106">連續匯出很適合此用途。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-106">Continuous Export is ideal for this.</span></span> <span data-ttu-id="f6d8a-107">您在 hello Application Insights 入口網站中看到的 hello 事件可能會在 Microsoft Azure 中的匯出的 toostorage JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-107">hello events you see in hello Application Insights portal can be exported toostorage in Microsoft Azure in JSON format.</span></span> <span data-ttu-id="f6d8a-108">您可以從該處下載您的資料，並寫入您指定任何程式碼需要 tooprocess 它。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-108">From there you can download your data and write whatever code you need tooprocess it.</span></span>  

<span data-ttu-id="f6d8a-109">使用連續匯出，可能會產生額外的費用。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-109">Using Continuous Export may incur an additional charge.</span></span> <span data-ttu-id="f6d8a-110">請檢查您的[定價模式](http://azure.microsoft.com/pricing/details/application-insights/)。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-110">Check your [pricing model](http://azure.microsoft.com/pricing/details/application-insights/).</span></span>

<span data-ttu-id="f6d8a-111">連續匯出設定之前，有一些其他替代方案，您可能會想 tooconsider:</span><span class="sxs-lookup"><span data-stu-id="f6d8a-111">Before you set up continuous export, there are some alternatives you might want tooconsider:</span></span>

* <span data-ttu-id="f6d8a-112">在 hello 度量 或 搜尋 刀鋒視窗頂端的 hello 匯出按鈕可讓您傳送資料表和圖表 tooan Excel 試算表。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-112">hello Export button at hello top of a metrics or search blade lets you transfer tables and charts tooan Excel spreadsheet.</span></span>

* <span data-ttu-id="f6d8a-113">[分析](app-insights-analytics.md) 可提供功能強大的遙測查詢語言。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-113">[Analytics](app-insights-analytics.md) provides a powerful query language for telemetry.</span></span> <span data-ttu-id="f6d8a-114">它也可以匯出結果。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-114">It can also export results.</span></span>
* <span data-ttu-id="f6d8a-115">如果您想太[瀏覽 Power BI 中的資料](app-insights-export-power-bi.md)，您可以執行，而不使用連續匯出。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-115">If you're looking too[explore your data in Power BI](app-insights-export-power-bi.md), you can do that without using Continuous Export.</span></span>
* <span data-ttu-id="f6d8a-116">hello[資料存取 REST API](https://dev.applicationinsights.io/)可讓您以程式設計方式存取您的遙測。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-116">hello [Data access REST API](https://dev.applicationinsights.io/) lets you access your telemetry programmatically.</span></span>

<span data-ttu-id="f6d8a-117">連續匯出複製您的資料 toostorage （其中它可以保留的只要您喜歡） 之後，就仍然可以使用 Application Insights 中的 hello 一般[保留期限](app-insights-data-retention-privacy.md)。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-117">After Continuous Export copies your data toostorage (where it can stay for as long as you like), it's still available in Application Insights for hello usual [retention period](app-insights-data-retention-privacy.md).</span></span>

## <span data-ttu-id="f6d8a-118"><a name="setup"></a> 建立連續匯出</span><span class="sxs-lookup"><span data-stu-id="f6d8a-118"><a name="setup"></a> Create a Continuous Export</span></span>
1. <span data-ttu-id="f6d8a-119">在 hello 應用程式的 Application Insights 資源，請在開啟連續匯出，然後選擇 **新增**:</span><span class="sxs-lookup"><span data-stu-id="f6d8a-119">In hello Application Insights resource for your app, open Continuous Export and choose **Add**:</span></span>

    ![向下捲動並按一下 [連續匯出]](./media/app-insights-export-telemetry/01-export.png)

2. <span data-ttu-id="f6d8a-121">選擇 hello 遙測資料型別想 tooexport。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-121">Choose hello telemetry data types you want tooexport.</span></span>

3. <span data-ttu-id="f6d8a-122">建立或選取[Azure 儲存體帳戶](../storage/common/storage-introduction.md)想 toostore hello 資料。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-122">Create or select an [Azure storage account](../storage/common/storage-introduction.md) where you want toostore hello data.</span></span>

    > [!Warning]
    > <span data-ttu-id="f6d8a-123">根據預設，hello 存放位置將會設定 toohello 與 Application Insights 資源的相同地理區域。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-123">By default, hello storage location will be set toohello same geographical region as your Application Insights resource.</span></span> <span data-ttu-id="f6d8a-124">如果您儲存在不同的區域中，可能會產生傳輸費用。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-124">If you store in a different region, you may incur transfer charges.</span></span>

    ![按一下 [加入]、[匯出目的地]、[儲存體帳戶]，然後建立新儲存區或選擇現有儲存區](./media/app-insights-export-telemetry/02-add.png)

4. <span data-ttu-id="f6d8a-126">建立或選取在 hello 儲存體容器：</span><span class="sxs-lookup"><span data-stu-id="f6d8a-126">Create or select a container in hello storage:</span></span>

    ![按一下 [選擇事件類型]](./media/app-insights-export-telemetry/create-container.png)

<span data-ttu-id="f6d8a-128">建立匯出之後，就會開始進行。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-128">Once you've created your export, it starts going.</span></span> <span data-ttu-id="f6d8a-129">您只能取得到達後建立 hello 匯出的資料。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-129">You only get data that arrives after you create hello export.</span></span>

<span data-ttu-id="f6d8a-130">可以有大約一小時才 hello 儲存體中的資料會出現延遲。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-130">There can be a delay of about an hour before data appears in hello storage.</span></span>

### <a name="tooedit-continuous-export"></a><span data-ttu-id="f6d8a-131">tooedit 連續匯出</span><span class="sxs-lookup"><span data-stu-id="f6d8a-131">tooedit continuous export</span></span>

<span data-ttu-id="f6d8a-132">如果您想 toochange hello 事件類型之後，只需編輯 hello 匯出：</span><span class="sxs-lookup"><span data-stu-id="f6d8a-132">If you want toochange hello event types later, just edit hello export:</span></span>

![按一下 [選擇事件類型]](./media/app-insights-export-telemetry/05-edit.png)

### <a name="toostop-continuous-export"></a><span data-ttu-id="f6d8a-134">toostop 連續匯出</span><span class="sxs-lookup"><span data-stu-id="f6d8a-134">toostop continuous export</span></span>

<span data-ttu-id="f6d8a-135">toostop hello 匯出中，按一下 停用。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-135">toostop hello export, click Disable.</span></span> <span data-ttu-id="f6d8a-136">當您按一下 [啟用] 時，hello 匯出會重新啟動以新的資料。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-136">When you click Enable again, hello export will restart with new data.</span></span> <span data-ttu-id="f6d8a-137">您不會取得匯出已停用時，到達 hello 入口網站中的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-137">You won't get hello data that arrived in hello portal while export was disabled.</span></span>

<span data-ttu-id="f6d8a-138">toostop hello 匯出，它永久刪除。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-138">toostop hello export permanently, delete it.</span></span> <span data-ttu-id="f6d8a-139">這麼做不會將您的資料從儲存體刪除。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-139">Doing so doesn't delete your data from storage.</span></span>

### <a name="cant-add-or-change-an-export"></a><span data-ttu-id="f6d8a-140">無法加入或變更匯出？</span><span class="sxs-lookup"><span data-stu-id="f6d8a-140">Can't add or change an export?</span></span>
* <span data-ttu-id="f6d8a-141">tooadd 或變更的匯出，您必須擁有者、 參與者或應用程式 Insights 參與者的存取權限。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-141">tooadd or change exports, you need Owner, Contributor or Application Insights Contributor access rights.</span></span> <span data-ttu-id="f6d8a-142">[了解角色][roles]。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-142">[Learn about roles][roles].</span></span>

## <span data-ttu-id="f6d8a-143"><a name="analyze"></a> 您取得什麼事件？</span><span class="sxs-lookup"><span data-stu-id="f6d8a-143"><a name="analyze"></a> What events do you get?</span></span>
<span data-ttu-id="f6d8a-144">hello 匯出的資料是 hello 未經處理的遙測，我們收到您的應用程式中，不同之處在於我們加入我們計算位置資料來自 hello 用戶端 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-144">hello exported data is hello raw telemetry we receive from your application, except that we add location data which we calculate from hello client IP address.</span></span>

<span data-ttu-id="f6d8a-145">已捨棄的資料[取樣](app-insights-sampling.md)未包含在匯出的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-145">Data that has been discarded by [sampling](app-insights-sampling.md) is not included in hello exported data.</span></span>

<span data-ttu-id="f6d8a-146">未包含其他計算的度量。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-146">Other calculated metrics are not included.</span></span> <span data-ttu-id="f6d8a-147">比方說，我們不要匯出平均 CPU utilisation，但是我們不要匯出 hello 原始遙測從中計算 hello 平均值。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-147">For example, we don't export average CPU utilisation, but we do export hello raw telemetry from which hello average is computed.</span></span>

<span data-ttu-id="f6d8a-148">hello 資料也包含任何 hello 結果[可用性 web 測試](app-insights-monitor-web-app-availability.md)您設定。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-148">hello data also includes hello results of any [availability web tests](app-insights-monitor-web-app-availability.md) that you have set up.</span></span>

> [!NOTE]
> <span data-ttu-id="f6d8a-149">**取樣**</span><span class="sxs-lookup"><span data-stu-id="f6d8a-149">**Sampling.**</span></span> <span data-ttu-id="f6d8a-150">如果您的應用程式傳送大量資料，hello 取樣功能可能會運作，並傳送 hello 產生遙測的分數。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-150">If your application sends a lot of data, hello sampling feature may operate and send only a fraction of hello generated telemetry.</span></span> [<span data-ttu-id="f6d8a-151">深入了解取樣。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-151">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <span data-ttu-id="f6d8a-152"><a name="get"></a>檢查 hello 資料</span><span class="sxs-lookup"><span data-stu-id="f6d8a-152"><a name="get"></a> Inspect hello data</span></span>
<span data-ttu-id="f6d8a-153">您可以檢查 hello 直接在 hello 入口網站中的儲存體。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-153">You can inspect hello storage directly in hello portal.</span></span> <span data-ttu-id="f6d8a-154">按一下 [瀏覽]、選取您的儲存體帳戶，然後開啟 [容器]。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-154">Click **Browse**, select your storage account, and then open **Containers**.</span></span>

<span data-ttu-id="f6d8a-155">在 Visual Studio 中的 Azure 儲存體 tooinspect 開啟**檢視**， **Cloud Explorer**。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-155">tooinspect Azure storage in Visual Studio, open **View**, **Cloud Explorer**.</span></span> <span data-ttu-id="f6d8a-156">(如果您沒有該功能表命令，您需要 tooinstall hello Azure SDK： 開啟 hello**新專案** 對話方塊中，展開 Visual C# / 雲端，然後選擇 **取得 Microsoft Azure SDK for.NET**。)</span><span class="sxs-lookup"><span data-stu-id="f6d8a-156">(If you don't have that menu command, you need tooinstall hello Azure SDK: Open hello **New Project** dialog, expand Visual C#/Cloud and choose **Get Microsoft Azure SDK for .NET**.)</span></span>

<span data-ttu-id="f6d8a-157">當您開啟 Blob 存放區時，您會看到含有一組 Blob 檔案的容器。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-157">When you open your blob store, you'll see a container with a set of blob files.</span></span> <span data-ttu-id="f6d8a-158">hello 衍生自您的 Application Insights 資源名稱、 檢測金鑰、 遙測-/ 日期/時間類型的每個檔案的 URI。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-158">hello URI of each file derived from your Application Insights resource name, its instrumentation key, telemetry-type/date/time.</span></span> <span data-ttu-id="f6d8a-159">（hello 資源名稱會全部小寫，和 hello 檢測金鑰省略連字號）。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-159">(hello resource name is all lowercase, and hello instrumentation key omits dashes.)</span></span>

![檢查 hello blob 存放區具有適當的工具](./media/app-insights-export-telemetry/04-data.png)

<span data-ttu-id="f6d8a-161">hello 日期和時間是 UTC，以及會 hello 遙測已儲放在 hello 存放區中，而不是 hello 時間產生。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-161">hello date and time are UTC and are when hello telemetry was deposited in hello store - not hello time it was generated.</span></span> <span data-ttu-id="f6d8a-162">如果您撰寫程式碼 toodownload hello 資料時，它可以透過 hello 資料以線性方式移動。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-162">So if you write code toodownload hello data, it can move linearly through hello data.</span></span>

<span data-ttu-id="f6d8a-163">以下是 hello hello 路徑形式：</span><span class="sxs-lookup"><span data-stu-id="f6d8a-163">Here's hello form of hello path:</span></span>

    $"{applicationName}_{instrumentationKey}/{type}/{blobDeliveryTimeUtc:yyyy-MM-dd}/{ blobDeliveryTimeUtc:HH}/{blobId}_{blobCreationTimeUtc:yyyyMMdd_HHmmss}.blob"

<span data-ttu-id="f6d8a-164">Where</span><span class="sxs-lookup"><span data-stu-id="f6d8a-164">Where</span></span>

* <span data-ttu-id="f6d8a-165">`blobCreationTimeUtc`blob 建立的時間在 hello 內部暫存儲存體</span><span class="sxs-lookup"><span data-stu-id="f6d8a-165">`blobCreationTimeUtc` is time when blob was created in hello internal staging storage</span></span>
* <span data-ttu-id="f6d8a-166">`blobDeliveryTimeUtc`是 hello 時間 blob 複製的 toohello 匯出目的地儲存體</span><span class="sxs-lookup"><span data-stu-id="f6d8a-166">`blobDeliveryTimeUtc` is hello time when blob is copied toohello export destination storage</span></span>

## <span data-ttu-id="f6d8a-167"><a name="format"></a> 資料格式</span><span class="sxs-lookup"><span data-stu-id="f6d8a-167"><a name="format"></a> Data format</span></span>
* <span data-ttu-id="f6d8a-168">每個 Blob 是包含多個以 '\n' 分隔的列的文字檔案。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-168">Each blob is a text file that contains multiple '\n'-separated rows.</span></span> <span data-ttu-id="f6d8a-169">它包含一段時間約半分鐘處理的 hello 遙測。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-169">It contains hello telemetry processed over a time period of roughly half a minute.</span></span>
* <span data-ttu-id="f6d8a-170">每個資料列都代表遙測資料點，例如要求或頁面檢視。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-170">Each row represents a telemetry data point such as a request or page view.</span></span>
* <span data-ttu-id="f6d8a-171">每列是未格式化的 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-171">Each row is an unformatted JSON document.</span></span> <span data-ttu-id="f6d8a-172">如果您 toosit 和 stare 在它，Visual Studio 中開啟它，然後選擇編輯進階，格式檔案：</span><span class="sxs-lookup"><span data-stu-id="f6d8a-172">If you want toosit and stare at it, open it in Visual Studio and choose Edit, Advanced, Format File:</span></span>

![使用適當工具檢視 hello 遙測](./media/app-insights-export-telemetry/06-json.png)

<span data-ttu-id="f6d8a-174">時間期間依刻度為單位，10000 刻度 = 1 毫秒。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-174">Time durations are in ticks, where 10 000 ticks = 1ms.</span></span> <span data-ttu-id="f6d8a-175">例如，這些值會顯示 1 毫秒的時間 toosend hello 瀏覽器中，3 毫秒的要求 tooreceive hello 瀏覽器頁面，以及 1.8s tooprocess hello:</span><span class="sxs-lookup"><span data-stu-id="f6d8a-175">For example, these values show a time of 1ms toosend a request from hello browser, 3ms tooreceive it, and 1.8s tooprocess hello page in hello browser:</span></span>

    "sendRequest": {"value": 10000.0},
    "receiveRequest": {"value": 30000.0},
    "clientProcess": {"value": 17970000.0}

[<span data-ttu-id="f6d8a-176">詳細的資料的模型 hello 屬性類型和值的參考。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-176">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)

## <a name="processing-hello-data"></a><span data-ttu-id="f6d8a-177">處理 hello 資料</span><span class="sxs-lookup"><span data-stu-id="f6d8a-177">Processing hello data</span></span>
<span data-ttu-id="f6d8a-178">小型標尺時，您可以撰寫一些程式碼 toopull 一樣，不過您的資料、 讀入試算表，並以此類推。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-178">On a small scale, you can write some code toopull apart your data, read it into a spreadsheet, and so on.</span></span> <span data-ttu-id="f6d8a-179">例如：</span><span class="sxs-lookup"><span data-stu-id="f6d8a-179">For example:</span></span>

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

<span data-ttu-id="f6d8a-180">如需較大型的程式碼範例，請參閱[使用背景工作角色][exportasa]。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-180">For a larger code sample, see [using a worker role][exportasa].</span></span>

## <span data-ttu-id="f6d8a-181"><a name="delete"></a>刪除舊資料</span><span class="sxs-lookup"><span data-stu-id="f6d8a-181"><a name="delete"></a>Delete your old data</span></span>
<span data-ttu-id="f6d8a-182">請注意，您負責管理您的儲存體容量，並且刪除 hello 舊資料，如有必要。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-182">Please note that you are responsible for managing your storage capacity and deleting hello old data if necessary.</span></span>

## <a name="if-you-regenerate-your-storage-key"></a><span data-ttu-id="f6d8a-183">如果您重新產生儲存體金鑰...</span><span class="sxs-lookup"><span data-stu-id="f6d8a-183">If you regenerate your storage key...</span></span>
<span data-ttu-id="f6d8a-184">如果您變更 hello 金鑰 tooyour 儲存體，連續匯出，將會停止運作。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-184">If you change hello key tooyour storage, continuous export will stop working.</span></span> <span data-ttu-id="f6d8a-185">您將在 Azure 帳戶中看到通知。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-185">You'll see a notification in your Azure account.</span></span>

<span data-ttu-id="f6d8a-186">開啟 hello 連續匯出刀鋒視窗，並編輯您的匯出。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-186">Open hello Continuous Export blade and edit your export.</span></span> <span data-ttu-id="f6d8a-187">編輯 hello 匯出目的地，但只要維持相同的存放裝置選取的 hello。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-187">Edit hello Export Destination, but just leave hello same storage selected.</span></span> <span data-ttu-id="f6d8a-188">按一下 [確定] tooconfirm。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-188">Click OK tooconfirm.</span></span>

![編輯 hello 連續匯出、 開啟和關閉三個匯出目的地。](./media/app-insights-export-telemetry/07-resetstore.png)

<span data-ttu-id="f6d8a-190">將重新啟動 hello 連續匯出。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-190">hello continuous export will restart.</span></span>

## <a name="export-samples"></a><span data-ttu-id="f6d8a-191">匯出範例</span><span class="sxs-lookup"><span data-stu-id="f6d8a-191">Export samples</span></span>

* <span data-ttu-id="f6d8a-192">[匯出 tooSQL 使用資料流分析][exportasa]</span><span class="sxs-lookup"><span data-stu-id="f6d8a-192">[Export tooSQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="f6d8a-193">串流分析範例 2</span><span class="sxs-lookup"><span data-stu-id="f6d8a-193">Stream Analytics sample 2</span></span>](app-insights-export-stream-analytics.md)

<span data-ttu-id="f6d8a-194">在較大的縮放比例，請考慮[HDInsight](https://azure.microsoft.com/services/hdinsight/) -在 hello 雲端中的 Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-194">On larger scales, consider [HDInsight](https://azure.microsoft.com/services/hdinsight/) - Hadoop clusters in hello cloud.</span></span> <span data-ttu-id="f6d8a-195">HDInsight 提供各種不同的技術，用於管理和分析大型的資料，而且您無法使用它 tooprocess 資料已匯出從 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-195">HDInsight provides a variety of technologies for managing and analyzing big data, and you could use it tooprocess data that has been exported from Application Insights.</span></span>

## <a name="q--a"></a><span data-ttu-id="f6d8a-196">問答集</span><span class="sxs-lookup"><span data-stu-id="f6d8a-196">Q & A</span></span>
* <span data-ttu-id="f6d8a-197">*但我想要的只是一次性下載圖表。*</span><span class="sxs-lookup"><span data-stu-id="f6d8a-197">*But all I want is a one-time download of a chart.*</span></span>  

    <span data-ttu-id="f6d8a-198">是的，您可以這麼做。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-198">Yes, you can do that.</span></span> <span data-ttu-id="f6d8a-199">在 hello hello 刀鋒視窗頂端，按一下**匯出資料**。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-199">At hello top of hello blade, click **Export Data**.</span></span>
* <span data-ttu-id="f6d8a-200">*我設定匯出，但我的儲存區中沒有資料。*</span><span class="sxs-lookup"><span data-stu-id="f6d8a-200">*I set up an export, but there's no data in my store.*</span></span>

    <span data-ttu-id="f6d8a-201">沒有 Application Insights 收到任何遙測從您的應用程式因為設定 hello 匯出？</span><span class="sxs-lookup"><span data-stu-id="f6d8a-201">Did Application Insights receive any telemetry from your app since you set up hello export?</span></span> <span data-ttu-id="f6d8a-202">您將只會收到新資料。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-202">You'll only receive new data.</span></span>
* <span data-ttu-id="f6d8a-203">*我已嘗試 tooset 向上匯出，但是被拒絕存取*</span><span class="sxs-lookup"><span data-stu-id="f6d8a-203">*I tried tooset up an export, but was denied access*</span></span>

    <span data-ttu-id="f6d8a-204">如果 hello 帳戶由您的組織所擁有，您必須 toobe hello 的擁有者或 contributors 群組的成員。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-204">If hello account is owned by your organization, you have toobe a member of hello owners or contributors groups.</span></span>
* <span data-ttu-id="f6d8a-205">*我可以匯出直線 toomy 自己的內部存放區嗎？*</span><span class="sxs-lookup"><span data-stu-id="f6d8a-205">*Can I export straight toomy own on-premises store?*</span></span>

    <span data-ttu-id="f6d8a-206">否，抱歉。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-206">No, sorry.</span></span> <span data-ttu-id="f6d8a-207">我們的匯出引擎目前僅適用於 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-207">Our export engine currently only works with Azure storage at this time.</span></span>  
* <span data-ttu-id="f6d8a-208">*是否有任何限制 toohello 的數量您放在 my 存放區的資料？*</span><span class="sxs-lookup"><span data-stu-id="f6d8a-208">*Is there any limit toohello amount of data you put in my store?*</span></span>

    <span data-ttu-id="f6d8a-209">否。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-209">No.</span></span> <span data-ttu-id="f6d8a-210">我們將會保留將資料推送直到您刪除 hello 匯出。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-210">We'll keep pushing data in until you delete hello export.</span></span> <span data-ttu-id="f6d8a-211">如果我們叫用 hello 外部 blob 儲存體限制，但這很龐大，我們將停止。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-211">We'll stop if we hit hello outer limits for blob storage, but that's pretty huge.</span></span> <span data-ttu-id="f6d8a-212">它是最多 tooyou toocontrol 您使用多少儲存空間。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-212">It's up tooyou toocontrol how much storage you use.</span></span>  
* <span data-ttu-id="f6d8a-213">*Hello 儲存體中應該查看多少 blob？*</span><span class="sxs-lookup"><span data-stu-id="f6d8a-213">*How many blobs should I see in hello storage?*</span></span>

  * <span data-ttu-id="f6d8a-214">每個資料中，輸入您所選的 tooexport，新的 blob （如果有可用的資料） 會建立每隔一分鐘。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-214">For every data type you selected tooexport, a new blob is created every minute (if data is available).</span></span>
  * <span data-ttu-id="f6d8a-215">此外，針對具有高流量的應用程式，則會配置額外的分割單位。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-215">In addition, for applications with high traffic, additional partition units are allocated.</span></span> <span data-ttu-id="f6d8a-216">在此情況下，每個單位會每分鐘建立一個 Blob。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-216">In this case each unit creates a blob every minute.</span></span>
* <span data-ttu-id="f6d8a-217">*我重新產生 hello 金鑰 toomy 儲存體，或者變更 hello hello 容器名稱和 hello 匯出現在無法運作。*</span><span class="sxs-lookup"><span data-stu-id="f6d8a-217">*I regenerated hello key toomy storage or changed hello name of hello container, and now hello export doesn't work.*</span></span>

    <span data-ttu-id="f6d8a-218">編輯 hello 匯出並開啟 hello 匯出目的地刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-218">Edit hello export and open hello export destination blade.</span></span> <span data-ttu-id="f6d8a-219">讓的 hello 相同存放裝置選取如往常一般，並按一下 [確定] tooconfirm。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-219">Leave hello same storage selected as before, and click OK tooconfirm.</span></span> <span data-ttu-id="f6d8a-220">匯出將重新開始。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-220">Export will restart.</span></span> <span data-ttu-id="f6d8a-221">如果 hello 變更是 hello 過去幾天內，您不必擔心會遺失資料。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-221">If hello change was within hello past few days, you won't lose data.</span></span>
* <span data-ttu-id="f6d8a-222">*可以暫停 hello 匯出？*</span><span class="sxs-lookup"><span data-stu-id="f6d8a-222">*Can I pause hello export?*</span></span>

    <span data-ttu-id="f6d8a-223">是。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-223">Yes.</span></span> <span data-ttu-id="f6d8a-224">按一下 [停用]。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-224">Click Disable.</span></span>

## <a name="code-samples"></a><span data-ttu-id="f6d8a-225">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="f6d8a-225">Code samples</span></span>

* [<span data-ttu-id="f6d8a-226">串流分析範例</span><span class="sxs-lookup"><span data-stu-id="f6d8a-226">Stream Analytics sample</span></span>](app-insights-export-stream-analytics.md)
* <span data-ttu-id="f6d8a-227">[匯出 tooSQL 使用資料流分析][exportasa]</span><span class="sxs-lookup"><span data-stu-id="f6d8a-227">[Export tooSQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="f6d8a-228">詳細的資料的模型 hello 屬性類型和值的參考。</span><span class="sxs-lookup"><span data-stu-id="f6d8a-228">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)

<!--Link references-->

[exportasa]: app-insights-code-sample-export-sql-stream-analytics.md
[roles]: app-insights-resources-roles-access-control.md
