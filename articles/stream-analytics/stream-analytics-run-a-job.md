---
title: "如何在串流分析中啟動串流工作 | Microsoft Docs"
description: "如何在 Azure 串流分析中執行串流工作 | 學習路徑區段。"
keywords: "串流工作"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9d46950f-2b69-49ce-a567-df558c5dd820
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 9a3ff37a893b0f29a2ac2eda6cd50687ee779ead
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-run-a-streaming-job-in-azure-stream-analytics"></a><span data-ttu-id="cb9d4-104">如何在 Azure 串流分析中執行串流工作</span><span class="sxs-lookup"><span data-stu-id="cb9d4-104">How to run a streaming job in Azure Stream Analytics</span></span>
<span data-ttu-id="cb9d4-105">當已指定工作輸入、查詢及輸出時，即可開始串流分析工作。</span><span class="sxs-lookup"><span data-stu-id="cb9d4-105">When a job input, query and output have all been specified you can start the Stream Analytics job.</span></span>

<span data-ttu-id="cb9d4-106">開始您的工作：</span><span class="sxs-lookup"><span data-stu-id="cb9d4-106">To start your job:</span></span>

1. <span data-ttu-id="cb9d4-107">在 Azure 傳統入口網站的工作儀表板，按一下頁面底部的 [開始]  。</span><span class="sxs-lookup"><span data-stu-id="cb9d4-107">In the Azure Classic portal, from the job dashboard, click **Start** at the bottom of the page.</span></span>
   
   ![開始工作按鈕](./media/stream-analytics-run-a-job/1-stream-analytics-run-a-job.png)  
   
   <span data-ttu-id="cb9d4-109">在 Azure 入口網站中，按一下工作頁面頂端的 [開始]  。</span><span class="sxs-lookup"><span data-stu-id="cb9d4-109">In the Azure portal, click **Start** at the top of your job page.</span></span>
   
   ![Azure 入口網站開始工作按鈕](./media/stream-analytics-run-a-job/4-stream-analytics-run-a-job.png)  
2. <span data-ttu-id="cb9d4-111">指定 [開始輸出]  值來決定這項工作開始產生輸出的時間。</span><span class="sxs-lookup"><span data-stu-id="cb9d4-111">Specify a **Start Output** value to determine when this job will start producing output.</span></span> <span data-ttu-id="cb9d4-112">先前尚未開始之工作的預設設定為 [工作開始時間] ，這代表該工作會立即開始處理資料。</span><span class="sxs-lookup"><span data-stu-id="cb9d4-112">The default setting for jobs that have not previously been started is **Job Start Time**, which means that the job will immediately start processing data.</span></span> <span data-ttu-id="cb9d4-113">您也可以指定在過去 (適用於取用歷史資料) 或未來 (用來延遲處理到未來某個時間) 的 [自訂]  時間。</span><span class="sxs-lookup"><span data-stu-id="cb9d4-113">You can also specify a **Custom** time in the past (for consuming historical data) or the future (to delay processing until a future time).</span></span> <span data-ttu-id="cb9d4-114">對於先前已經開始並停止的工作，您可選取 [上次停止時間]  ，以便從上次輸出的時間點繼續工作，並避免資料遺失。</span><span class="sxs-lookup"><span data-stu-id="cb9d4-114">For cases when a job has been previously started and stopped, the option **Last Stopped Time** is available in order to resume the job from the last output time and avoid data loss.</span></span>  
   
   ![啟動串流工作的時間](./media/stream-analytics-run-a-job/2-stream-analytics-run-a-job.png)  
   
   ![Azure 入口網站開始串流工作的時間](./media/stream-analytics-run-a-job/5-stream-analytics-run-a-job.png)  
3. <span data-ttu-id="cb9d4-117">確認選擇。</span><span class="sxs-lookup"><span data-stu-id="cb9d4-117">Confirm your selection.</span></span> <span data-ttu-id="cb9d4-118">工作狀態會變更為 [啟動中]，並會在工作開始後的短時間內變為 [執行中]。</span><span class="sxs-lookup"><span data-stu-id="cb9d4-118">The job status will change to *Starting* and will shortly move to *Running* once the job has started.</span></span> <span data-ttu-id="cb9d4-119">您可以在 [通知中樞] 中監視「開始」作業的進度：</span><span class="sxs-lookup"><span data-stu-id="cb9d4-119">You can monitor the progress of the **Start** operation in the **Notification Hub**:</span></span>
   
   ![串流工作進度](./media/stream-analytics-run-a-job/3-stream-analytics-run-a-job.png)  
   
   ![Azure 入口網站串流工作進度](./media/stream-analytics-run-a-job/6-stream-analytics-run-a-job.png)  

## <a name="get-help"></a><span data-ttu-id="cb9d4-122">取得說明</span><span class="sxs-lookup"><span data-stu-id="cb9d4-122">Get help</span></span>
<span data-ttu-id="cb9d4-123">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="cb9d4-123">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb9d4-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cb9d4-124">Next steps</span></span>
* [<span data-ttu-id="cb9d4-125">Azure Stream Analytics 介紹</span><span class="sxs-lookup"><span data-stu-id="cb9d4-125">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="cb9d4-126">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cb9d4-126">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="cb9d4-127">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="cb9d4-127">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="cb9d4-128">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="cb9d4-128">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="cb9d4-129">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="cb9d4-129">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

