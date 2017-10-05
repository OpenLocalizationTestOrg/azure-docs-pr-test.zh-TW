---
title: "將資料輸入新增至串流分析工作中 | Microsoft Docs"
description: "了解如何從事件中樞或 Blog 儲存體的參考資料，將資料來源連接至串流分析工作，以做為資料流處理資料輸入。"
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
ms.openlocfilehash: 8bdbcf78f2892cbd1e1cc09cef220dff08dd9490
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="add-a-streaming-data-input-or-reference-data-to-a-stream-analytics-job"></a><span data-ttu-id="c703d-104">將資料流處理資料輸入或參考資料新增至串流分析工作</span><span class="sxs-lookup"><span data-stu-id="c703d-104">Add a streaming data input or reference data to a Stream Analytics job</span></span>
<span data-ttu-id="c703d-105">了解如何從事件中樞或 Blob 儲存體的參考資料，將資料來源連接至串流分析工作，以做為資料流處理資料輸入。</span><span class="sxs-lookup"><span data-stu-id="c703d-105">Learn how to hook up a data source to your Stream Analytics job as streaming data input from Event Hubs or reference data from Blob storage.</span></span>

<span data-ttu-id="c703d-106">Azure 串流分析工作可以連線至一或多個資料輸入，且每個資料輸入都定義了一個與現有資料來源之間的連線。</span><span class="sxs-lookup"><span data-stu-id="c703d-106">Azure Stream Analytics jobs can be connected to one data input or more, each of which define a connection to an existing data source.</span></span> <span data-ttu-id="c703d-107">當資料傳送到該資料來源時，串流分析工作會即時取用該資料，並把它當做串流資料來處理。</span><span class="sxs-lookup"><span data-stu-id="c703d-107">As data is sent to that data source, it is consumed by the Stream Analytics job and processed in real time as streaming data.</span></span> <span data-ttu-id="c703d-108">「串流分析」與 [Azure 事件中樞](https://azure.microsoft.com/services/event-hubs/)及 [Azure Blob 儲存體](../storage/blobs/storage-dotnet-how-to-use-blobs.md)整合性極佳，不論它們是在工作訂用帳戶內還是工作訂用帳戶外。</span><span class="sxs-lookup"><span data-stu-id="c703d-108">Stream Analytics has first class integration with [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) and [Azure Blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) both within and outside of the job's subscription.</span></span>

<span data-ttu-id="c703d-109">本文章是 [串流分析學習路徑](/documentation/learning-paths/stream-analytics/)中的一個步驟。</span><span class="sxs-lookup"><span data-stu-id="c703d-109">This article is a step in the [Stream Analytics learning path](/documentation/learning-paths/stream-analytics/).</span></span>

## <a name="data-input-streaming-data-and-reference-data"></a><span data-ttu-id="c703d-110">資料輸入：資料流處理資料及參考資料</span><span class="sxs-lookup"><span data-stu-id="c703d-110">Data input: Streaming data and reference data</span></span>
<span data-ttu-id="c703d-111">串流分析有兩種不同的輸入類型：資料流和參考資料。</span><span class="sxs-lookup"><span data-stu-id="c703d-111">There are two distinct types of inputs in Stream Analytics: data streams and reference data.</span></span>

* <span data-ttu-id="c703d-112">**資料流**：串流分析工作必須至少包含一個由工作取用和轉換的資料流輸入。</span><span class="sxs-lookup"><span data-stu-id="c703d-112">**Data Streams**: Stream Analytics jobs must include at least one data stream input to be consumed and transformed by the job.</span></span> <span data-ttu-id="c703d-113">支援將 Azure Blob 儲存體和 Azure 事件中樞當成資料流輸入來源。</span><span class="sxs-lookup"><span data-stu-id="c703d-113">Azure Blob storage and Azure Event Hubs are supported as data stream input sources.</span></span> <span data-ttu-id="c703d-114">Azure 事件中樞是用於從多個連接的裝置和服務收集事件資料流。</span><span class="sxs-lookup"><span data-stu-id="c703d-114">Azure Event Hubs are used to collect event streams from connected devices, services and applications.</span></span> <span data-ttu-id="c703d-115">Azure Blob 儲存體可用於擷取大量資料作為資料流的輸入來源。</span><span class="sxs-lookup"><span data-stu-id="c703d-115">Azure Blob storage can be used as an input source for ingesting bulk data as a stream.</span></span>  
* <span data-ttu-id="c703d-116">**參考資料**：串流分析會支援稱為參考資料的第二類型輔助輸入。</span><span class="sxs-lookup"><span data-stu-id="c703d-116">**Reference data**: Stream Analytics supports a second type of auxiliary input called reference data.</span></span>  <span data-ttu-id="c703d-117">與動態資料相反，這種資料是靜態或變化緩慢的。</span><span class="sxs-lookup"><span data-stu-id="c703d-117">As opposed to data in motion, this data is static or slowing changing.</span></span>  <span data-ttu-id="c703d-118">其通常與資料流搭配使用來執行查閱和關聯，以建立更豐富的資料集。</span><span class="sxs-lookup"><span data-stu-id="c703d-118">It is typically used for performing look-ups and correlations with data streams to create a richer data set.</span></span>  <span data-ttu-id="c703d-119">在預覽版本中，Azure Blob 儲存體是目前唯一支援當成參考資料的輸入來源。</span><span class="sxs-lookup"><span data-stu-id="c703d-119">Azure Blob storage is currently the only supported input source for reference data.</span></span>  

<span data-ttu-id="c703d-120">若要將輸入加入串流分析工作中：</span><span class="sxs-lookup"><span data-stu-id="c703d-120">To add an input to your Stream Analytics job:</span></span>

1. <span data-ttu-id="c703d-121">在 Azure 入口網站中按一下 [輸入]，然後按一下串流分析工作的 [新增輸入]。</span><span class="sxs-lookup"><span data-stu-id="c703d-121">In the Azure portal click **Inputs** and then click **Add an Input** in your Stream Analytics job.</span></span>
   
    ![Azure 傳統入口網站 - 新增輸入。](./media/stream-analytics-add-inputs/1-stream-analytics-add-inputs.png)  
   
    <span data-ttu-id="c703d-123">在 Azure 入口網站中，按一下串流分析工作的 [輸入]  磚。</span><span class="sxs-lookup"><span data-stu-id="c703d-123">In the Azure portal click the **Inputs** tile in your Stream Analytics job.</span></span>  
   
    ![Azure 入口網站 - 新增資料輸入。](./media/stream-analytics-add-inputs/7-stream-analytics-add-inputs.png)  
2. <span data-ttu-id="c703d-125">指定輸入類型：**資料流**或**參考資料**。</span><span class="sxs-lookup"><span data-stu-id="c703d-125">Specify the type of the input: either **Data stream** or **Reference data**.</span></span>
   
    ![新增正確的資料輸入, 串流或參考](./media/stream-analytics-add-inputs/2-stream-analytics-add-inputs.png)  
   
    ![新增正確的資料輸入, 串流或參考](./media/stream-analytics-add-inputs/8-stream-analytics-add-inputs.png)  
3. <span data-ttu-id="c703d-128">如果要建立資料流輸入，請指定輸入的來源類型。</span><span class="sxs-lookup"><span data-stu-id="c703d-128">If creating a Data Stream input, specify the source type for the input.</span></span>  <span data-ttu-id="c703d-129">由於目前僅支援 Blob 儲存體，因此在參考資料建立期間可以省略此步驟。</span><span class="sxs-lookup"><span data-stu-id="c703d-129">This step can be skipped during Reference Data creation as only Blob storage is supported at this time.</span></span>
   
    ![加入資料流資料輸入](./media/stream-analytics-add-inputs/3-stream-analytics-add-inputs.png)  
   
    ![加入資料流資料輸入](./media/stream-analytics-add-inputs/9-stream-analytics-add-inputs.png)  
4. <span data-ttu-id="c703d-132">在 [輸入別名] 方塊中，替這個輸出取一個易記的名稱。</span><span class="sxs-lookup"><span data-stu-id="c703d-132">Provide a friendly name for this input in the Input Alias box.</span></span>  <span data-ttu-id="c703d-133">此名稱稍後將在作業查詢中用作指稱輸入。</span><span class="sxs-lookup"><span data-stu-id="c703d-133">This name will be used in your job's query later on to refer to the input.</span></span>
   
    <span data-ttu-id="c703d-134">填寫其餘必要的連接屬性，以連接到資料來源。</span><span class="sxs-lookup"><span data-stu-id="c703d-134">Fill in the rest of the required connection properties to connect to your data source.</span></span> <span data-ttu-id="c703d-135">這些欄位會因輸入類型和來源類型而有所不同，詳細定義請見 [此處](stream-analytics-create-a-job.md)。</span><span class="sxs-lookup"><span data-stu-id="c703d-135">These fields vary by type of input and source type and are defined in detail [here](stream-analytics-create-a-job.md).</span></span>  
   
    ![新增事件中樞資料輸入](./media/stream-analytics-add-inputs/4-stream-analytics-add-inputs.png)  
5. <span data-ttu-id="c703d-137">指定輸入資料的序列化設定：</span><span class="sxs-lookup"><span data-stu-id="c703d-137">Specify the serialization settings for the input data:</span></span>
   
   * <span data-ttu-id="c703d-138">若要確定查詢會依照您所預期的方式處理，請指定傳入資料的 **事件序列化格式** 。</span><span class="sxs-lookup"><span data-stu-id="c703d-138">To make sure your queries work the way you expect, specify the **Event Serialization Format** of incoming data.</span></span>  <span data-ttu-id="c703d-139">支援的序列化格式為 JSON、CSV 及 Avro。</span><span class="sxs-lookup"><span data-stu-id="c703d-139">Supported serialization formats are JSON, CSV, and Avro.</span></span>
   * <span data-ttu-id="c703d-140">確認資料的 **編碼** 。</span><span class="sxs-lookup"><span data-stu-id="c703d-140">Verify the **Encoding** for the data.</span></span>  <span data-ttu-id="c703d-141">UTF-8 是目前唯一支援的編碼格式。</span><span class="sxs-lookup"><span data-stu-id="c703d-141">UTF-8 is the only supported encoding format at this time.</span></span>
     
     ![資料輸入的資料序列化設定](./media/stream-analytics-add-inputs/5-stream-analytics-add-inputs.png)  
     
     ![資料輸入的資料序列化設定](./media/stream-analytics-add-inputs/10-stream-analytics-add-inputs.png)  
6. <span data-ttu-id="c703d-144">完成建立輸入之後，串流分析會確認其是否可以連接到輸入來源。</span><span class="sxs-lookup"><span data-stu-id="c703d-144">After completing the input creation, Stream Analytics will verify that it can connect to the input source.</span></span>  <span data-ttu-id="c703d-145">您可以在 [通知中樞] 中檢視測試連接作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="c703d-145">You can view the status of the Test Connection operation in the Notification hub.</span></span>
   
    ![測試串流資料輸入的連線](./media/stream-analytics-add-inputs/6-stream-analytics-add-inputs.png)  
   
    ![測試串流資料輸入的連線](./media/stream-analytics-add-inputs/11-stream-analytics-add-inputs.png)  

## <a name="get-help-with-streaming-data-inputs"></a><span data-ttu-id="c703d-148">取得資料流處理資料輸入的協助</span><span class="sxs-lookup"><span data-stu-id="c703d-148">Get help with streaming data inputs</span></span>
<span data-ttu-id="c703d-149">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="c703d-149">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="c703d-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c703d-150">Next steps</span></span>
* [<span data-ttu-id="c703d-151">Azure Stream Analytics 介紹</span><span class="sxs-lookup"><span data-stu-id="c703d-151">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="c703d-152">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="c703d-152">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="c703d-153">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="c703d-153">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="c703d-154">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="c703d-154">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="c703d-155">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="c703d-155">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

