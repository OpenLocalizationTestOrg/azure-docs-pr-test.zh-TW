---
title: "在 Azure Stream Analytics aaa 取樣輸入 |Microsoft 文件"
description: "針對串流分析作業進行移難排解時精準找出問題。"
keywords: "對輸入進行疑難排解、輸入取樣"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 9637a8664de099eebb8f5654036d2957f4c6b7ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-input-stream-sampling"></a><span data-ttu-id="24f78-104">Azure 資料流分析輸入串流的取樣</span><span class="sxs-lookup"><span data-stu-id="24f78-104">Azure Stream Analytics input-stream sampling</span></span>

<span data-ttu-id="24f78-105">藉由使用 Azure Stream Analytics 中，您可以取樣輸入的事件來自檔案並測試 hello 入口網站中的查詢，而不需要 toostart 或停止的作業。</span><span class="sxs-lookup"><span data-stu-id="24f78-105">By using Azure Stream Analytics, you can sample input events that come from a file and test queries in hello portal without needing toostart or stop a job.</span></span>

## <a name="testing-your-query"></a><span data-ttu-id="24f78-106">測試查詢</span><span class="sxs-lookup"><span data-stu-id="24f78-106">Testing your query</span></span>

<span data-ttu-id="24f78-107">在 hello 資料流分析工作詳細資料窗格中，開啟 hello**查詢編輯器**刀鋒視窗中按一下底下的 hello 查詢名稱**查詢**。</span><span class="sxs-lookup"><span data-stu-id="24f78-107">In hello Stream Analytics job details pane, open hello **Query editor** blade by clicking hello query name under **Query**.</span></span> <span data-ttu-id="24f78-108">(在我們的範例案例，因為尚未建立任何查詢，按一下 hello **< >**預留位置。)</span><span class="sxs-lookup"><span data-stu-id="24f78-108">(In our example scenario, because no query has been created yet, click hello **< >** placeholder.)</span></span>

![hello 資料流分析查詢編輯器](media/stream-analytics-sample-data-input/stream-analytics-query-editor.png)

<span data-ttu-id="24f78-110">hello 先前版本中，會顯示 hello 豐富編輯器刀鋒視窗中建立您的查詢。</span><span class="sxs-lookup"><span data-stu-id="24f78-110">hello rich editor blade for creating your query is displayed as it was in hello previous release.</span></span> <span data-ttu-id="24f78-111">現在已使用新的更新 hello 刀鋒視窗左窗格中，該顯示 hello 輸入和輸出 hello 查詢所使用且定義為此工作。</span><span class="sxs-lookup"><span data-stu-id="24f78-111">Now hello blade has been updated with a new left pane that shows hello inputs and outputs that are used by hello query and defined for this job.</span></span>

![hello 資料流分析查詢編輯器中輸入及輸出 清單](media/stream-analytics-sample-data-input/stream-analytics-query-editor-highlight.png)

<span data-ttu-id="24f78-113">此外也會顯示尚未定義的其他一組輸入與輸出。</span><span class="sxs-lookup"><span data-stu-id="24f78-113">Also shown are an additional input and output, which are not defined.</span></span> <span data-ttu-id="24f78-114">這些是來自 hello 新的查詢範本您開始使用。</span><span class="sxs-lookup"><span data-stu-id="24f78-114">They come from hello new query template that you start with.</span></span> <span data-ttu-id="24f78-115">這些變更，或甚至就會完全消失，當您編輯 hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="24f78-115">They change, or even disappear altogether, as you edit hello query.</span></span> <span data-ttu-id="24f78-116">您目前可以放心地忽略這組輸入與輸出。</span><span class="sxs-lookup"><span data-stu-id="24f78-116">You can safely ignore them for now.</span></span>

<span data-ttu-id="24f78-117">tootest 範例輸入資料，與任何輸入，以滑鼠右鍵按一下，然後選取**從檔案的範例資料上傳**。</span><span class="sxs-lookup"><span data-stu-id="24f78-117">tootest with sample input data, right-click any of your inputs, and then select **Upload sample data from file**.</span></span>

![hello 資料流分析查詢編輯器 上傳的範例資料檔案命令](media/stream-analytics-sample-data-input/stream-analytics-query-editor-upload.png)

<span data-ttu-id="24f78-119">Hello 上傳完成後，按一下**測試**tootest hello 針對此查詢範例您剛才提供的資料。</span><span class="sxs-lookup"><span data-stu-id="24f78-119">After hello upload is complete, click **Test** tootest this query against hello sample data you have just provided.</span></span>

![hello 資料流分析查詢編輯器 [測試] 按鈕](media/stream-analytics-sample-data-input/stream-analytics-query-editor-test.png)

<span data-ttu-id="24f78-121">如果您想要稍後使用 toosave hello 測試輸出，hello 查詢的輸出會顯示在 hello 瀏覽器連結 toohello 下載的結果中。</span><span class="sxs-lookup"><span data-stu-id="24f78-121">If you want toosave hello test output for later use, hello output of your query is displayed in hello browser with a link toohello download results.</span></span> <span data-ttu-id="24f78-122">您現在可以輕鬆並反覆地修改查詢並測試它重複 toosee hello 輸出如何變更。</span><span class="sxs-lookup"><span data-stu-id="24f78-122">You can now easily and iteratively modify your query and test it repeatedly toosee how hello output changes.</span></span>

![串流分析查詢編輯器樣本輸出](media/stream-analytics-sample-data-input/stream-analytics-query-editor-samples-output.png)

<span data-ttu-id="24f78-124">在上述映像的 hello，已加入第二個輸出，稱為**HighAvgTempOutput**。</span><span class="sxs-lookup"><span data-stu-id="24f78-124">In hello preceding image, a second output has been added, called **HighAvgTempOutput**.</span></span>

<span data-ttu-id="24f78-125">當您在查詢中使用多個輸出時，您可以查看每個輸出的 hello 結果分別，且兩者之間輕鬆切換。</span><span class="sxs-lookup"><span data-stu-id="24f78-125">When you use multiple outputs in a query, you can see hello results for each output separately and easily toggle between them.</span></span>

<span data-ttu-id="24f78-126">您滿意 hello 結果之後，您可以儲存您的查詢、 啟動您的工作、 耐心及監看的資料流分析的 hello 魔力。</span><span class="sxs-lookup"><span data-stu-id="24f78-126">After you are satisfied with hello results, you can save your query, start your job, sit back and watch hello magic of Stream Analytics.</span></span>

## <a name="get-help"></a><span data-ttu-id="24f78-127">取得說明</span><span class="sxs-lookup"><span data-stu-id="24f78-127">Get help</span></span>

<span data-ttu-id="24f78-128">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。</span><span class="sxs-lookup"><span data-stu-id="24f78-128">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="24f78-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="24f78-129">Next steps</span></span>
* [<span data-ttu-id="24f78-130">簡介 tooAzure 資料流分析</span><span class="sxs-lookup"><span data-stu-id="24f78-130">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="24f78-131">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="24f78-131">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="24f78-132">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="24f78-132">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="24f78-133">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="24f78-133">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="24f78-134">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="24f78-134">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
