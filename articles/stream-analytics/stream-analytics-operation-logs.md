---
title: "使用中資料流分析作業及服務記錄檔的 aaaDebug |Microsoft 文件"
description: "如何 toouse 資料流分析作業記錄檔"
keywords: "服務記錄檔"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: a2ed9676-f0bd-4398-87c8-a592779ac728
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: d3dd27706ccc879a724e1894b33d47021d972f31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="debug-stream-analytics-jobs-using-service-and-operation-logs"></a><span data-ttu-id="fff91-104">使用服務和作業記錄檔對串流分析工作進行偵錯</span><span class="sxs-lookup"><span data-stu-id="fff91-104">Debug Stream Analytics jobs using service and operation logs</span></span>
<span data-ttu-id="fff91-105">所有 Azure 服務供應器的操作記錄訊息 toousers toorecord 詳細資料相關的 toomanagement 作業。</span><span class="sxs-lookup"><span data-stu-id="fff91-105">All Azure services supply operational logging messages toousers toorecord details related toomanagement operations.</span></span> <span data-ttu-id="fff91-106">在 Azure Stream Analytics 中，這項資訊可用以進行偵錯，例如一段時間，從開始 tooprocessing toooutput 檢視工作狀態、 工作進度和失敗作業的訊息 tootrack hello 進度。</span><span class="sxs-lookup"><span data-stu-id="fff91-106">In Azure Stream Analytics, this information can be used for debugging purposes such as viewing job status, job progress, and failure messages tootrack hello progress of a job over time, from start tooprocessing toooutput.</span></span>

## <a name="find-operation-logs-in-hello-azure-management-portal"></a><span data-ttu-id="fff91-107">尋找 hello Azure 管理入口網站中的作業記錄檔</span><span class="sxs-lookup"><span data-stu-id="fff91-107">Find operation logs in hello Azure Management portal</span></span>
<span data-ttu-id="fff91-108">作業記錄檔可用兩種方式來存取：</span><span class="sxs-lookup"><span data-stu-id="fff91-108">Operation Logs can be accessed in two ways:</span></span>  

* <span data-ttu-id="fff91-109">Hello 資料流分析工作的儀表板</span><span class="sxs-lookup"><span data-stu-id="fff91-109">Dashboard of hello Stream Analytics job</span></span>  
* <span data-ttu-id="fff91-110">Hello Azure 傳統入口網站中管理服務</span><span class="sxs-lookup"><span data-stu-id="fff91-110">Management Services in hello Azure Classic portal</span></span>  

## <a name="dashboard-of-hello-stream-analytics-job"></a><span data-ttu-id="fff91-111">Hello 資料流分析工作的儀表板</span><span class="sxs-lookup"><span data-stu-id="fff91-111">Dashboard of hello Stream Analytics job</span></span>
<span data-ttu-id="fff91-112">連結 toohello 對應的資料流分析工作的記錄檔會顯示 hello 作業儀表板 索引標籤上。如果您按一下該連結時，它會設定 hello 篩選，它會顯示該特定工作的最新記錄檔的方式。</span><span class="sxs-lookup"><span data-stu-id="fff91-112">A link toohello corresponding logs of a Stream Analytics job is displayed on hello job’s Dashboard tab. If you click on that link, it will set hello filters in a way that it shows latest logs for that specific job.</span></span>

  ![選取管理服務記錄檔](./media/stream-analytics-operation-logs/01-stream-analytics-operation-logs.png)  

## <a name="management-services"></a><span data-ttu-id="fff91-114">管理服務</span><span class="sxs-lookup"><span data-stu-id="fff91-114">Management Services</span></span>
<span data-ttu-id="fff91-115">toomanually 巡覽 toohello 作業記錄檔資料流分析和 hello Azure 傳統入口網站中的其他服務：</span><span class="sxs-lookup"><span data-stu-id="fff91-115">toomanually navigate toohello Operation Logs for Stream Analytics and other services in hello Azure Classic portal:</span></span>

1. <span data-ttu-id="fff91-116">按一下**管理服務**在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="fff91-116">Click on **Management Services** in hello [Azure Classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="fff91-117">選取**Stream Analytics**如**類型**和 hello hello 作業名稱**服務名稱**。</span><span class="sxs-lookup"><span data-stu-id="fff91-117">Select **Stream Analytics** for **Type** and hello name of hello job for **Service Name**.</span></span>  
   
   ![選取串流分析](./media/stream-analytics-operation-logs/02-stream-analytics-operation-logs.png)  

## <a name="find-audit-logs-in-hello-azure-portal"></a><span data-ttu-id="fff91-119">找到 hello Azure 入口網站的稽核記錄</span><span class="sxs-lookup"><span data-stu-id="fff91-119">Find audit logs in hello Azure portal</span></span>
<span data-ttu-id="fff91-120">按一下 toofind hello Azure 入口網站中的資料流分析工作的操作記錄檔**瀏覽**，然後選取 **稽核記錄檔**。</span><span class="sxs-lookup"><span data-stu-id="fff91-120">toofind operational logs for your Stream Analytics job in hello Azure portal, Click **Browse** and then select **Audit logs**.</span></span>

  ![Azure 入口網站選取串流分析](./media/stream-analytics-operation-logs/06-stream-analytics-operation-logs.png)  

<span data-ttu-id="fff91-122">這會開啟刀鋒視窗中顯示來自 hello 事件的所有資源的過去 7 天您訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="fff91-122">This will open a blade showing events from hello last 7 days for all resources in your subscription.</span></span>  <span data-ttu-id="fff91-123">您可以篩選指定類型或時間範圍內的 toosee 事件即可 hello**篩選**命令。</span><span class="sxs-lookup"><span data-stu-id="fff91-123">You can filter toosee events of a specify type or time frame by clicking hello **Filter** command.</span></span>

  ![Azure 入口網站選取串流分析](./media/stream-analytics-operation-logs/07-stream-analytics-operation-logs.png)  

## <a name="get-log-details"></a><span data-ttu-id="fff91-125">取得記錄檔詳細資料</span><span class="sxs-lookup"><span data-stu-id="fff91-125">Get log details</span></span>
<span data-ttu-id="fff91-126">您可以篩選由時間範圍和狀態 tooview hello 記錄您的工作。</span><span class="sxs-lookup"><span data-stu-id="fff91-126">You can filter by Time Range and Status tooview hello logs for your job.</span></span>

<span data-ttu-id="fff91-127">在 hello Azure 管理入口網站中，按一下 hello**詳細資料**底部 hello hello 視窗 tooview 按鈕所選事件的詳細。</span><span class="sxs-lookup"><span data-stu-id="fff91-127">In hello Azure Management portal, click on hello **Details** button at hello bottom of hello window tooview more details about a selected event.</span></span> 

  ![選取詳細資料](./media/stream-analytics-operation-logs/03-stream-analytics-operation-logs.png)  

<span data-ttu-id="fff91-129">在 hello Azure 入口網站中，按一下 記錄檔項目 toosee hello 詳細內文中的事件。</span><span class="sxs-lookup"><span data-stu-id="fff91-129">In hello Azure portal, click on a log entry toosee hello detailed events inside it.</span></span>

  ![Azure 入口網站選取詳細資料](./media/stream-analytics-operation-logs/08-stream-analytics-operation-logs.png)  

<span data-ttu-id="fff91-131">您可以從該處，開啟 hello**詳細**刀鋒視窗上 hello 事件即可。</span><span class="sxs-lookup"><span data-stu-id="fff91-131">From there, you can open hello **Detail** blade by clicking on hello event.</span></span>

  ![Azure 入口網站選取詳細資料](./media/stream-analytics-operation-logs/09-stream-analytics-operation-logs.png)  

## <a name="debug-a-failed-job"></a><span data-ttu-id="fff91-133">偵錯失敗的工作</span><span class="sxs-lookup"><span data-stu-id="fff91-133">Debug a failed job</span></span>
<span data-ttu-id="fff91-134">在 hello Azure 管理入口網站中，按一下 hello 搜尋圖示並輸入 '失敗'。</span><span class="sxs-lookup"><span data-stu-id="fff91-134">In hello Azure Management portal, click on hello Search icon and type ‘failed’.</span></span> <span data-ttu-id="fff91-135">這樣可以找出所有包含失敗項目的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="fff91-135">This gives a result of all logs with failures.</span></span> 

  ![針對失敗的工作進行偵錯](./media/stream-analytics-operation-logs/04-stream-analytics-operation-logs.png)  

<span data-ttu-id="fff91-137">在 hello Azure 入口網站，您可以篩選層級的訊息 tooview**重大**事件。</span><span class="sxs-lookup"><span data-stu-id="fff91-137">In hello Azure portal, you can filter by level of message tooview **Critical** events.</span></span>

  ![Azure 入口網站偵錯](./media/stream-analytics-operation-logs/10-stream-analytics-operation-logs.png)  

<span data-ttu-id="fff91-139">您可以選取任何一種 hello 失敗，並按一下 hello**詳細資料**hello 錯誤更多資訊。</span><span class="sxs-lookup"><span data-stu-id="fff91-139">You can select any one of hello failures, and click on hello **Details** for more information on hello error.</span></span>  <span data-ttu-id="fff91-140">某些錯誤訊息也會提供有關如何 toomitigate hello 問題的資訊。</span><span class="sxs-lookup"><span data-stu-id="fff91-140">Some error messages also provide information about how toomitigate hello issue.</span></span> 

  ![Operation Details](./media/stream-analytics-operation-logs/05-stream-analytics-operation-logs.png)  

<span data-ttu-id="fff91-142">萬一您需要 toocontact[支援](https://azure.microsoft.com/support/options/)或提供資訊 toohello 小組透過 hello [MSDN 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)，請注意 hello 作業的詳細資訊，特別是 hello**相互關聯識別碼**.</span><span class="sxs-lookup"><span data-stu-id="fff91-142">In case you need toocontact [Support](https://azure.microsoft.com/support/options/) or provide information toohello team via hello [MSDN forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), please note hello Operation Details, specifically hello **Correlation ID**.</span></span> 

## <a name="get-help"></a><span data-ttu-id="fff91-143">取得說明</span><span class="sxs-lookup"><span data-stu-id="fff91-143">Get help</span></span>
<span data-ttu-id="fff91-144">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="fff91-144">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="fff91-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fff91-145">Next steps</span></span>
* [<span data-ttu-id="fff91-146">簡介 tooAzure 資料流分析</span><span class="sxs-lookup"><span data-stu-id="fff91-146">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="fff91-147">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="fff91-147">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="fff91-148">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="fff91-148">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="fff91-149">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="fff91-149">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="fff91-150">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="fff91-150">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

