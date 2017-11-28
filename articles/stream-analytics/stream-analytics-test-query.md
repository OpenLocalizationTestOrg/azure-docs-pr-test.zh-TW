---
title: "Azure 串流分析查詢測試 |M icrosoft Docs"
description: "如何在串流分析作業中測試查詢。"
keywords: "測試查詢、對查詢進行移難排解"
documentation center: 
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
ms.openlocfilehash: 16bb3f26ec3a69e5204162db9e54a186cf1ec6a6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="test-azure-stream-analytics-queries-in-the-azure-portal"></a><span data-ttu-id="325f4-104">在 Azure 入口網站測試串流分析查詢</span><span class="sxs-lookup"><span data-stu-id="325f4-104">Test Azure Stream Analytics queries in the Azure portal</span></span>

<span data-ttu-id="325f4-105">透過 Azure 串流分析，您可以在 Azure 入口網站中測試查詢，且無須啟動或停止作業。</span><span class="sxs-lookup"><span data-stu-id="325f4-105">With Azure Stream Analytics, you can test queries in the Azure portal without needing to start or stop a job.</span></span>

## <a name="test-the-input"></a><span data-ttu-id="325f4-106">測試輸入</span><span class="sxs-lookup"><span data-stu-id="325f4-106">Test the input</span></span>

1. <span data-ttu-id="325f4-107">若要測試樣本輸入資料，以滑鼠右鍵按一下任何輸入，然後選取 [從檔案上傳樣本資料]。</span><span class="sxs-lookup"><span data-stu-id="325f4-107">To test with sample input data, right-click any of your inputs, and then select **Upload sample data from file**.</span></span>

    ![串流分析查詢編輯器的測試查詢](media/stream-analytics-test-query/stream-analytics-test-query-editor-upload.png)

2. <span data-ttu-id="325f4-109">上傳完成後，按一下 [測試] 以根據您提供的樣本資料測試此查詢。</span><span class="sxs-lookup"><span data-stu-id="325f4-109">After the upload is complete, click **Test** to test this query against the sample data you have provided.</span></span>

    ![串流分析查詢編輯器的樣本資料](media/stream-analytics-test-query/stream-analytics-test-query-editor-test.png)

<span data-ttu-id="325f4-111">查詢的輸出會顯示在瀏覽器中，還有 [下載結果] 連結可讓您儲存測試輸出以供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="325f4-111">The output of your query is displayed in the browser, with Download results link should you want to save the test output for later use.</span></span> <span data-ttu-id="325f4-112">您現在可以輕鬆地反覆修改查詢並反覆測試查詢來查看輸出的變更狀況。</span><span class="sxs-lookup"><span data-stu-id="325f4-112">You can now easily and iteratively modify your query and test it repeatedly to see how the output changes.</span></span>

![串流分析查詢編輯器樣本輸出](media/stream-analytics-test-query/stream-analytics-test-query-editor-samples-output.png)

<span data-ttu-id="325f4-114">透過在查詢中使用多個輸出，您可以分別查看兩個輸出的結果，並輕鬆地在兩者之間切換。</span><span class="sxs-lookup"><span data-stu-id="325f4-114">With multiple outputs used in a query, you can see the results for both outputs separately and easily toggle between them.</span></span>

<span data-ttu-id="325f4-115">當您滿意顯示在瀏覽器中的結果後，您可以儲存查詢、啟動作業，以及讓其在沒有錯誤的情況下處理事件。</span><span class="sxs-lookup"><span data-stu-id="325f4-115">After you are satisfied with the results shown in the browser, you can save your query, start your job, and let it process events without error.</span></span>

## <a name="get-help"></a><span data-ttu-id="325f4-116">取得說明</span><span class="sxs-lookup"><span data-stu-id="325f4-116">Get help</span></span>

<span data-ttu-id="325f4-117">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。</span><span class="sxs-lookup"><span data-stu-id="325f4-117">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="325f4-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="325f4-118">Next steps</span></span>

* [<span data-ttu-id="325f4-119">Azure Stream Analytics 介紹</span><span class="sxs-lookup"><span data-stu-id="325f4-119">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="325f4-120">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="325f4-120">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="325f4-121">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="325f4-121">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="325f4-122">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="325f4-122">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="325f4-123">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="325f4-123">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
