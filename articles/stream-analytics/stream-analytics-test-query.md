---
title: "aaaAzure 串流分析查詢測試 |Microsoft 文件"
description: "如何 tootest 您在資料流分析作業中的查詢。"
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
ms.openlocfilehash: 3b141d98332fdc170e696e181c8446796a86f78e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="test-azure-stream-analytics-queries-in-hello-azure-portal"></a><span data-ttu-id="db0d1-104">在 hello Azure 入口網站中測試 Azure 串流分析查詢</span><span class="sxs-lookup"><span data-stu-id="db0d1-104">Test Azure Stream Analytics queries in hello Azure portal</span></span>

<span data-ttu-id="db0d1-105">使用 Azure Stream Analytics 中，您可以測試 hello Azure 入口網站中的查詢，而不需要 toostart 或停止作業。</span><span class="sxs-lookup"><span data-stu-id="db0d1-105">With Azure Stream Analytics, you can test queries in hello Azure portal without needing toostart or stop a job.</span></span>

## <a name="test-hello-input"></a><span data-ttu-id="db0d1-106">測試 hello 輸入</span><span class="sxs-lookup"><span data-stu-id="db0d1-106">Test hello input</span></span>

1. <span data-ttu-id="db0d1-107">tootest 範例輸入資料，與任何輸入，以滑鼠右鍵按一下，然後選取**從檔案的範例資料上傳**。</span><span class="sxs-lookup"><span data-stu-id="db0d1-107">tootest with sample input data, right-click any of your inputs, and then select **Upload sample data from file**.</span></span>

    ![串流分析查詢編輯器的測試查詢](media/stream-analytics-test-query/stream-analytics-test-query-editor-upload.png)

2. <span data-ttu-id="db0d1-109">Hello 上傳完成後，按一下**測試**tootest hello 針對此查詢範例所提供的資料。</span><span class="sxs-lookup"><span data-stu-id="db0d1-109">After hello upload is complete, click **Test** tootest this query against hello sample data you have provided.</span></span>

    ![串流分析查詢編輯器的樣本資料](media/stream-analytics-test-query/stream-analytics-test-query-editor-test.png)

<span data-ttu-id="db0d1-111">hello 查詢的輸出會顯示在 hello 的瀏覽器中，以下載結果連結應該要 toosave hello 測試輸出以供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="db0d1-111">hello output of your query is displayed in hello browser, with Download results link should you want toosave hello test output for later use.</span></span> <span data-ttu-id="db0d1-112">您現在可以輕鬆並反覆地修改查詢並測試它重複 toosee hello 輸出如何變更。</span><span class="sxs-lookup"><span data-stu-id="db0d1-112">You can now easily and iteratively modify your query and test it repeatedly toosee how hello output changes.</span></span>

![串流分析查詢編輯器樣本輸出](media/stream-analytics-test-query/stream-analytics-test-query-editor-samples-output.png)

<span data-ttu-id="db0d1-114">具有多個查詢中使用的輸出，您可以分別查看 hello 結果的兩個輸出，並兩者之間輕鬆切換。</span><span class="sxs-lookup"><span data-stu-id="db0d1-114">With multiple outputs used in a query, you can see hello results for both outputs separately and easily toggle between them.</span></span>

<span data-ttu-id="db0d1-115">其 hello 結果顯示在 hello 瀏覽器中，您可以儲存您的查詢，請啟動您的工作，並讓您感到滿意後，它會處理事件不會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="db0d1-115">After you are satisfied with hello results shown in hello browser, you can save your query, start your job, and let it process events without error.</span></span>

## <a name="get-help"></a><span data-ttu-id="db0d1-116">取得說明</span><span class="sxs-lookup"><span data-stu-id="db0d1-116">Get help</span></span>

<span data-ttu-id="db0d1-117">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。</span><span class="sxs-lookup"><span data-stu-id="db0d1-117">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="db0d1-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="db0d1-118">Next steps</span></span>

* [<span data-ttu-id="db0d1-119">簡介 tooAzure 資料流分析</span><span class="sxs-lookup"><span data-stu-id="db0d1-119">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="db0d1-120">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="db0d1-120">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="db0d1-121">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="db0d1-121">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="db0d1-122">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="db0d1-122">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="db0d1-123">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="db0d1-123">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
