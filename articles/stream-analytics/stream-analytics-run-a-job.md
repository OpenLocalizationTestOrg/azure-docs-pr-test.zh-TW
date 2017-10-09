---
title: "資料流中資料流分析工作的 aaaHow toostart |Microsoft 文件"
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
ms.openlocfilehash: 67aa14860c38cbd0535d0ec4f23729445d0185c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-streaming-job-in-azure-stream-analytics"></a><span data-ttu-id="74dbf-104">在 Azure Stream Analytics toorun 串流工作的方式</span><span class="sxs-lookup"><span data-stu-id="74dbf-104">How toorun a streaming job in Azure Stream Analytics</span></span>
<span data-ttu-id="74dbf-105">作業輸入，當查詢和輸出都已指定您可以啟動 hello 資料流分析工作。</span><span class="sxs-lookup"><span data-stu-id="74dbf-105">When a job input, query and output have all been specified you can start hello Stream Analytics job.</span></span>

<span data-ttu-id="74dbf-106">toostart 您的工作：</span><span class="sxs-lookup"><span data-stu-id="74dbf-106">toostart your job:</span></span>

1. <span data-ttu-id="74dbf-107">在 hello Azure 傳統入口網站，從 hello 作業儀表板中，按一下 **啟動**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="74dbf-107">In hello Azure Classic portal, from hello job dashboard, click **Start** at hello bottom of hello page.</span></span>
   
   ![開始工作按鈕](./media/stream-analytics-run-a-job/1-stream-analytics-run-a-job.png)  
   
   <span data-ttu-id="74dbf-109">在 hello Azure 入口網站，按一下 **啟動**在 hello 頁面頂端的工作。</span><span class="sxs-lookup"><span data-stu-id="74dbf-109">In hello Azure portal, click **Start** at hello top of your job page.</span></span>
   
   ![Azure 入口網站開始工作按鈕](./media/stream-analytics-run-a-job/4-stream-analytics-run-a-job.png)  
2. <span data-ttu-id="74dbf-111">指定**開始輸出**值 toodetermine 時此工作會開始產生輸出。</span><span class="sxs-lookup"><span data-stu-id="74dbf-111">Specify a **Start Output** value toodetermine when this job will start producing output.</span></span> <span data-ttu-id="74dbf-112">hello 先前尚未啟動的工作的預設值是**工作開始時間**，這表示 hello 作業會立即開始處理資料。</span><span class="sxs-lookup"><span data-stu-id="74dbf-112">hello default setting for jobs that have not previously been started is **Job Start Time**, which means that hello job will immediately start processing data.</span></span> <span data-ttu-id="74dbf-113">您也可以指定**自訂**hello 時間 （適用於使用歷程記錄資料） 的過去或未來 hello (toodelay 處理，直到未來的時間)。</span><span class="sxs-lookup"><span data-stu-id="74dbf-113">You can also specify a **Custom** time in hello past (for consuming historical data) or hello future (toodelay processing until a future time).</span></span> <span data-ttu-id="74dbf-114">情況下，作業已經先前啟動和停止，hello 選項**上次停止時間**隨附於從 hello 上次輸出順序 tooresume hello 作業，避免資料遺失。</span><span class="sxs-lookup"><span data-stu-id="74dbf-114">For cases when a job has been previously started and stopped, hello option **Last Stopped Time** is available in order tooresume hello job from hello last output time and avoid data loss.</span></span>  
   
   ![啟動串流工作的時間](./media/stream-analytics-run-a-job/2-stream-analytics-run-a-job.png)  
   
   ![Azure 入口網站開始串流工作的時間](./media/stream-analytics-run-a-job/5-stream-analytics-run-a-job.png)  
3. <span data-ttu-id="74dbf-117">確認選擇。</span><span class="sxs-lookup"><span data-stu-id="74dbf-117">Confirm your selection.</span></span> <span data-ttu-id="74dbf-118">hello 工作狀態會變更太*起始*和稍後也會跟著移動*執行*hello 工作啟動之後。</span><span class="sxs-lookup"><span data-stu-id="74dbf-118">hello job status will change too*Starting* and will shortly move too*Running* once hello job has started.</span></span> <span data-ttu-id="74dbf-119">您可以監視 hello 進度的 hello**啟動**作業在 hello**通知中樞**:</span><span class="sxs-lookup"><span data-stu-id="74dbf-119">You can monitor hello progress of hello **Start** operation in hello **Notification Hub**:</span></span>
   
   ![串流工作進度](./media/stream-analytics-run-a-job/3-stream-analytics-run-a-job.png)  
   
   ![Azure 入口網站串流工作進度](./media/stream-analytics-run-a-job/6-stream-analytics-run-a-job.png)  

## <a name="get-help"></a><span data-ttu-id="74dbf-122">取得說明</span><span class="sxs-lookup"><span data-stu-id="74dbf-122">Get help</span></span>
<span data-ttu-id="74dbf-123">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="74dbf-123">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="74dbf-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="74dbf-124">Next steps</span></span>
* [<span data-ttu-id="74dbf-125">簡介 tooAzure 資料流分析</span><span class="sxs-lookup"><span data-stu-id="74dbf-125">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="74dbf-126">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="74dbf-126">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="74dbf-127">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="74dbf-127">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="74dbf-128">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="74dbf-128">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="74dbf-129">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="74dbf-129">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

