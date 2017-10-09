---
title: "aaaAdd 資料輸入 tooyour 串流分析工作 |Microsoft 文件"
description: "了解如何設定串流分析資料來源 tooyour toohook 作業為資料流的資料輸入從事件中心或參考的資料，從 Blob 儲存體。"
keywords: "資料輸入, 串流資料"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: 
ms.assetid: 9e59bd24-2a80-4ecb-b6b2-309a07c70bcd
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 674000268fcdf9bc000af3e2f166cb66f1366922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-streaming-data-input-or-reference-data-tooa-stream-analytics-job"></a><span data-ttu-id="22cc5-104">新增資料流資料輸入或參考資料 tooa 資料流分析工作</span><span class="sxs-lookup"><span data-stu-id="22cc5-104">Add a streaming data input or reference data tooa Stream Analytics job</span></span>
<span data-ttu-id="22cc5-105">了解如何設定串流分析資料來源 tooyour toohook 作業為資料流的資料輸入從事件中心或參考的資料，從 Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="22cc5-105">Learn how toohook up a data source tooyour Stream Analytics job as streaming data input from Event Hubs or reference data from Blob storage.</span></span>

<span data-ttu-id="22cc5-106">Azure 串流分析工作可以是連線的 tooone 資料輸入或更多，其中每個定義連線 tooan 現有資料來源。</span><span class="sxs-lookup"><span data-stu-id="22cc5-106">Azure Stream Analytics jobs can be connected tooone data input or more, each of which define a connection tooan existing data source.</span></span> <span data-ttu-id="22cc5-107">當資料傳送 toothat 資料來源時，它是 hello 資料流分析工作所耗用，而且處理即時串流資料。</span><span class="sxs-lookup"><span data-stu-id="22cc5-107">As data is sent toothat data source, it is consumed by hello Stream Analytics job and processed in real time as streaming data.</span></span> <span data-ttu-id="22cc5-108">資料流分析第一個類別與已經整合[Azure 事件中心](https://azure.microsoft.com/services/event-hubs/)和[Azure Blob 儲存體](../storage/blobs/storage-dotnet-how-to-use-blobs.md)內部和外部 hello 作業的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="22cc5-108">Stream Analytics has first class integration with [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) and [Azure Blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) both within and outside of hello job's subscription.</span></span>

<span data-ttu-id="22cc5-109">這篇文章是 hello 的步驟[Stream Analytics 學習路徑](/documentation/learning-paths/stream-analytics/)。</span><span class="sxs-lookup"><span data-stu-id="22cc5-109">This article is a step in hello [Stream Analytics learning path](/documentation/learning-paths/stream-analytics/).</span></span>

## <a name="data-input-streaming-data-and-reference-data"></a><span data-ttu-id="22cc5-110">資料輸入：資料流處理資料及參考資料</span><span class="sxs-lookup"><span data-stu-id="22cc5-110">Data input: Streaming data and reference data</span></span>
<span data-ttu-id="22cc5-111">串流分析有兩種不同的輸入類型：資料流和參考資料。</span><span class="sxs-lookup"><span data-stu-id="22cc5-111">There are two distinct types of inputs in Stream Analytics: data streams and reference data.</span></span>

* <span data-ttu-id="22cc5-112">**資料流**： 串流分析工作必須包含至少一個資料資料流輸入的 toobe hello 工作所耗用及轉換。</span><span class="sxs-lookup"><span data-stu-id="22cc5-112">**Data Streams**: Stream Analytics jobs must include at least one data stream input toobe consumed and transformed by hello job.</span></span> <span data-ttu-id="22cc5-113">支援將 Azure Blob 儲存體和 Azure 事件中樞當成資料流輸入來源。</span><span class="sxs-lookup"><span data-stu-id="22cc5-113">Azure Blob storage and Azure Event Hubs are supported as data stream input sources.</span></span> <span data-ttu-id="22cc5-114">Azure 事件中心是使用的 toocollect 事件資料流，從連接的裝置、 服務和應用程式。</span><span class="sxs-lookup"><span data-stu-id="22cc5-114">Azure Event Hubs are used toocollect event streams from connected devices, services and applications.</span></span> <span data-ttu-id="22cc5-115">Azure Blob 儲存體可用於擷取大量資料作為資料流的輸入來源。</span><span class="sxs-lookup"><span data-stu-id="22cc5-115">Azure Blob storage can be used as an input source for ingesting bulk data as a stream.</span></span>  
* <span data-ttu-id="22cc5-116">**參考資料**：串流分析會支援稱為參考資料的第二類型輔助輸入。</span><span class="sxs-lookup"><span data-stu-id="22cc5-116">**Reference data**: Stream Analytics supports a second type of auxiliary input called reference data.</span></span>  <span data-ttu-id="22cc5-117">為移動中的相對於 toodata，此資料是靜態或慢性變更。</span><span class="sxs-lookup"><span data-stu-id="22cc5-117">As opposed toodata in motion, this data is static or slowing changing.</span></span>  <span data-ttu-id="22cc5-118">它通常用來執行查閱和相互關聯資料流 toocreate 更豐富的資料集。</span><span class="sxs-lookup"><span data-stu-id="22cc5-118">It is typically used for performing look-ups and correlations with data streams toocreate a richer data set.</span></span>  <span data-ttu-id="22cc5-119">Azure Blob 儲存體正在 hello 只支援輸入的參考資料來源。</span><span class="sxs-lookup"><span data-stu-id="22cc5-119">Azure Blob storage is currently hello only supported input source for reference data.</span></span>  

<span data-ttu-id="22cc5-120">tooadd tooyour 輸入資料流分析工作：</span><span class="sxs-lookup"><span data-stu-id="22cc5-120">tooadd an input tooyour Stream Analytics job:</span></span>

1. <span data-ttu-id="22cc5-121">Hello Azure 入口網站中按一下**輸入**，然後按一下**將輸入**Stream Analytics 工作。</span><span class="sxs-lookup"><span data-stu-id="22cc5-121">In hello Azure portal click **Inputs** and then click **Add an Input** in your Stream Analytics job.</span></span>
   
    ![Azure 傳統入口網站 - 新增輸入。](./media/stream-analytics-add-inputs/1-stream-analytics-add-inputs.png)  
   
    <span data-ttu-id="22cc5-123">在 hello Azure 入口網站按一下 hello**輸入**磚中的資料流分析工作。</span><span class="sxs-lookup"><span data-stu-id="22cc5-123">In hello Azure portal click hello **Inputs** tile in your Stream Analytics job.</span></span>  
   
    ![Azure 入口網站 - 新增資料輸入。](./media/stream-analytics-add-inputs/7-stream-analytics-add-inputs.png)  
2. <span data-ttu-id="22cc5-125">指定 hello hello 輸入型別： 任一**資料流**或**參考資料**。</span><span class="sxs-lookup"><span data-stu-id="22cc5-125">Specify hello type of hello input: either **Data stream** or **Reference data**.</span></span>
   
    ![新增 hello 正確的資料輸入、 資料流或參考](./media/stream-analytics-add-inputs/2-stream-analytics-add-inputs.png)  
   
    ![新增 hello 正確的資料輸入、 資料流或參考](./media/stream-analytics-add-inputs/8-stream-analytics-add-inputs.png)  
3. <span data-ttu-id="22cc5-128">如果建立資料流輸入，指定 hello hello 輸入的來源類型。</span><span class="sxs-lookup"><span data-stu-id="22cc5-128">If creating a Data Stream input, specify hello source type for hello input.</span></span>  <span data-ttu-id="22cc5-129">由於目前僅支援 Blob 儲存體，因此在參考資料建立期間可以省略此步驟。</span><span class="sxs-lookup"><span data-stu-id="22cc5-129">This step can be skipped during Reference Data creation as only Blob storage is supported at this time.</span></span>
   
    ![加入資料流資料輸入](./media/stream-analytics-add-inputs/3-stream-analytics-add-inputs.png)  
   
    ![加入資料流資料輸入](./media/stream-analytics-add-inputs/9-stream-analytics-add-inputs.png)  
4. <span data-ttu-id="22cc5-132">提供此輸入中的 hello 輸入別名 方塊中的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="22cc5-132">Provide a friendly name for this input in hello Input Alias box.</span></span>  <span data-ttu-id="22cc5-133">此名稱將用於作業的之後會在 toorefer toohello 輸入的查詢。</span><span class="sxs-lookup"><span data-stu-id="22cc5-133">This name will be used in your job's query later on toorefer toohello input.</span></span>
   
    <span data-ttu-id="22cc5-134">填寫 hello rest hello 所需的連接屬性 tooconnect tooyour 資料來源。</span><span class="sxs-lookup"><span data-stu-id="22cc5-134">Fill in hello rest of hello required connection properties tooconnect tooyour data source.</span></span> <span data-ttu-id="22cc5-135">這些欄位會因輸入類型和來源類型而有所不同，詳細定義請見 [此處](stream-analytics-create-a-job.md)。</span><span class="sxs-lookup"><span data-stu-id="22cc5-135">These fields vary by type of input and source type and are defined in detail [here](stream-analytics-create-a-job.md).</span></span>  
   
    ![新增事件中樞資料輸入](./media/stream-analytics-add-inputs/4-stream-analytics-add-inputs.png)  
5. <span data-ttu-id="22cc5-137">指定 hello hello 輸入資料的序列化設定：</span><span class="sxs-lookup"><span data-stu-id="22cc5-137">Specify hello serialization settings for hello input data:</span></span>
   
   * <span data-ttu-id="22cc5-138">確定您的查詢運作 hello 方式您預期，toomake 指定 hello**事件序列化格式**的內送資料。</span><span class="sxs-lookup"><span data-stu-id="22cc5-138">toomake sure your queries work hello way you expect, specify hello **Event Serialization Format** of incoming data.</span></span>  <span data-ttu-id="22cc5-139">支援的序列化格式為 JSON、CSV 及 Avro。</span><span class="sxs-lookup"><span data-stu-id="22cc5-139">Supported serialization formats are JSON, CSV, and Avro.</span></span>
   * <span data-ttu-id="22cc5-140">確認 hello**編碼**hello 資料。</span><span class="sxs-lookup"><span data-stu-id="22cc5-140">Verify hello **Encoding** for hello data.</span></span>  <span data-ttu-id="22cc5-141">Utf-8 是 hello 此時只支援編碼格式。</span><span class="sxs-lookup"><span data-stu-id="22cc5-141">UTF-8 is hello only supported encoding format at this time.</span></span>
     
     ![Hello 資料輸入的資料序列化設定](./media/stream-analytics-add-inputs/5-stream-analytics-add-inputs.png)  
     
     ![Hello 資料輸入的資料序列化設定](./media/stream-analytics-add-inputs/10-stream-analytics-add-inputs.png)  
6. <span data-ttu-id="22cc5-144">完成之後 hello 輸入的建立，資料流分析會確認可連線 toohello 輸入的來源。</span><span class="sxs-lookup"><span data-stu-id="22cc5-144">After completing hello input creation, Stream Analytics will verify that it can connect toohello input source.</span></span>  <span data-ttu-id="22cc5-145">您可以在 hello 通知中樞的檢視 hello hello 測試連接作業狀態。</span><span class="sxs-lookup"><span data-stu-id="22cc5-145">You can view hello status of hello Test Connection operation in hello Notification hub.</span></span>
   
    ![測試連接的資料流資料輸入 hello](./media/stream-analytics-add-inputs/6-stream-analytics-add-inputs.png)  
   
    ![測試連接的資料流資料輸入 hello](./media/stream-analytics-add-inputs/11-stream-analytics-add-inputs.png)  

## <a name="get-help-with-streaming-data-inputs"></a><span data-ttu-id="22cc5-148">取得資料流處理資料輸入的協助</span><span class="sxs-lookup"><span data-stu-id="22cc5-148">Get help with streaming data inputs</span></span>
<span data-ttu-id="22cc5-149">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="22cc5-149">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="22cc5-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="22cc5-150">Next steps</span></span>
* [<span data-ttu-id="22cc5-151">簡介 tooAzure 資料流分析</span><span class="sxs-lookup"><span data-stu-id="22cc5-151">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="22cc5-152">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="22cc5-152">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="22cc5-153">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="22cc5-153">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="22cc5-154">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="22cc5-154">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="22cc5-155">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="22cc5-155">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

