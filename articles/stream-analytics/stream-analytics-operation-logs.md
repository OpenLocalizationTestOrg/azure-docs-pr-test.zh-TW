---
title: "使用串流分析中的作業和服務記錄檔偵錯 | Microsoft Docs"
description: "如何使用串流分析作業記錄檔"
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
ms.openlocfilehash: c95d240ebef6a84228eb98db70002792fcfbdea6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="debug-stream-analytics-jobs-using-service-and-operation-logs"></a><span data-ttu-id="f7f7a-104">使用服務和作業記錄檔對串流分析工作進行偵錯</span><span class="sxs-lookup"><span data-stu-id="f7f7a-104">Debug Stream Analytics jobs using service and operation logs</span></span>
<span data-ttu-id="f7f7a-105">所有 Azure 服務都會將作業記錄訊息提供給使用者，以記錄與管理作業有關的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f7f7a-105">All Azure services supply operational logging messages to users to record details related to management operations.</span></span> <span data-ttu-id="f7f7a-106">在 Azure 串流分析中，這項資訊可用於偵錯用途，例如檢視工作狀態、工作進度與失敗訊息，以從一開始處理到輸出都可隨著時間追蹤作業進度。</span><span class="sxs-lookup"><span data-stu-id="f7f7a-106">In Azure Stream Analytics, this information can be used for debugging purposes such as viewing job status, job progress, and failure messages to track the progress of a job over time, from start to processing to output.</span></span>

## <a name="find-operation-logs-in-the-azure-management-portal"></a><span data-ttu-id="f7f7a-107">在 Azure 管理入口網站中尋找作業記錄檔</span><span class="sxs-lookup"><span data-stu-id="f7f7a-107">Find operation logs in the Azure Management portal</span></span>
<span data-ttu-id="f7f7a-108">作業記錄檔可用兩種方式來存取：</span><span class="sxs-lookup"><span data-stu-id="f7f7a-108">Operation Logs can be accessed in two ways:</span></span>  

* <span data-ttu-id="f7f7a-109">串流分析工作的儀表板</span><span class="sxs-lookup"><span data-stu-id="f7f7a-109">Dashboard of the Stream Analytics job</span></span>  
* <span data-ttu-id="f7f7a-110">Azure 傳統入口網站中的管理服務</span><span class="sxs-lookup"><span data-stu-id="f7f7a-110">Management Services in the Azure Classic portal</span></span>  

## <a name="dashboard-of-the-stream-analytics-job"></a><span data-ttu-id="f7f7a-111">串流分析工作的儀表板</span><span class="sxs-lookup"><span data-stu-id="f7f7a-111">Dashboard of the Stream Analytics job</span></span>
<span data-ttu-id="f7f7a-112">串流分析工作相對應的記錄檔連結會顯示在該工作的 [儀表板] 索引標籤上。按一下該連結時，其會以能夠顯示該特定工作最新記錄檔的方式來設定篩選器。</span><span class="sxs-lookup"><span data-stu-id="f7f7a-112">A link to the corresponding logs of a Stream Analytics job is displayed on the job’s Dashboard tab. If you click on that link, it will set the filters in a way that it shows latest logs for that specific job.</span></span>

  ![選取管理服務記錄檔](./media/stream-analytics-operation-logs/01-stream-analytics-operation-logs.png)  

## <a name="management-services"></a><span data-ttu-id="f7f7a-114">管理服務</span><span class="sxs-lookup"><span data-stu-id="f7f7a-114">Management Services</span></span>
<span data-ttu-id="f7f7a-115">若要以手動方式瀏覽至串流分析的作業記錄檔以及 Azure 傳統入口網站中的其他服務：</span><span class="sxs-lookup"><span data-stu-id="f7f7a-115">To manually navigate to the Operation Logs for Stream Analytics and other services in the Azure Classic portal:</span></span>

1. <span data-ttu-id="f7f7a-116">按一下 [Azure 傳統入口網站](https://manage.windowsazure.com) 中的 [管理服務]。</span><span class="sxs-lookup"><span data-stu-id="f7f7a-116">Click on **Management Services** in the [Azure Classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="f7f7a-117">[類型] 選取 [串流分析]，並在 [服務名稱] 選取作業的名稱。</span><span class="sxs-lookup"><span data-stu-id="f7f7a-117">Select **Stream Analytics** for **Type** and the name of the job for **Service Name**.</span></span>  
   
   ![選取串流分析](./media/stream-analytics-operation-logs/02-stream-analytics-operation-logs.png)  

## <a name="find-audit-logs-in-the-azure-portal"></a><span data-ttu-id="f7f7a-119">在 Azure 入口網站中尋找稽核記錄檔</span><span class="sxs-lookup"><span data-stu-id="f7f7a-119">Find audit logs in the Azure portal</span></span>
<span data-ttu-id="f7f7a-120">若要在 Azure 入口網站中尋找串流分析工作的作業記錄檔，請按一下 [瀏覽]，然後選取 [稽核記錄檔]。</span><span class="sxs-lookup"><span data-stu-id="f7f7a-120">To find operational logs for your Stream Analytics job in the Azure portal, Click **Browse** and then select **Audit logs**.</span></span>

  ![Azure 入口網站選取串流分析](./media/stream-analytics-operation-logs/06-stream-analytics-operation-logs.png)  

<span data-ttu-id="f7f7a-122">這會開啟刀鋒視窗，當中會顯示您訂用帳戶中所有資源在過去 7 天的事件。</span><span class="sxs-lookup"><span data-stu-id="f7f7a-122">This will open a blade showing events from the last 7 days for all resources in your subscription.</span></span>  <span data-ttu-id="f7f7a-123">按一下 [篩選]  命令，可以篩選查看指定類型或時間範圍的事件。</span><span class="sxs-lookup"><span data-stu-id="f7f7a-123">You can filter to see events of a specify type or time frame by clicking the **Filter** command.</span></span>

  ![Azure 入口網站選取串流分析](./media/stream-analytics-operation-logs/07-stream-analytics-operation-logs.png)  

## <a name="get-log-details"></a><span data-ttu-id="f7f7a-125">取得記錄檔詳細資料</span><span class="sxs-lookup"><span data-stu-id="f7f7a-125">Get log details</span></span>
<span data-ttu-id="f7f7a-126">您可以依照時間範圍和狀態來篩選，以檢視工作的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f7f7a-126">You can filter by Time Range and Status to view the logs for your job.</span></span>

<span data-ttu-id="f7f7a-127">在 Azure 管理入口網站中，按一下視窗底部的 [詳細資料]  按鈕來檢視所選事件的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f7f7a-127">In the Azure Management portal, click on the **Details** button at the bottom of the window to view more details about a selected event.</span></span> 

  ![選取詳細資料](./media/stream-analytics-operation-logs/03-stream-analytics-operation-logs.png)  

<span data-ttu-id="f7f7a-129">在 Azure 入口網站中，按一下記錄項目即可查看其中的詳細事件。</span><span class="sxs-lookup"><span data-stu-id="f7f7a-129">In the Azure portal, click on a log entry to see the detailed events inside it.</span></span>

  ![Azure 入口網站選取詳細資料](./media/stream-analytics-operation-logs/08-stream-analytics-operation-logs.png)  

<span data-ttu-id="f7f7a-131">從該處，按一下事件即可開啟 [詳細資料]  刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f7f7a-131">From there, you can open the **Detail** blade by clicking on the event.</span></span>

  ![Azure 入口網站選取詳細資料](./media/stream-analytics-operation-logs/09-stream-analytics-operation-logs.png)  

## <a name="debug-a-failed-job"></a><span data-ttu-id="f7f7a-133">偵錯失敗的工作</span><span class="sxs-lookup"><span data-stu-id="f7f7a-133">Debug a failed job</span></span>
<span data-ttu-id="f7f7a-134">在 Azure 管理入口網站中，按一下搜尋圖示並鍵入 ‘failed’。</span><span class="sxs-lookup"><span data-stu-id="f7f7a-134">In the Azure Management portal, click on the Search icon and type ‘failed’.</span></span> <span data-ttu-id="f7f7a-135">這樣可以找出所有包含失敗項目的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f7f7a-135">This gives a result of all logs with failures.</span></span> 

  ![針對失敗的工作進行偵錯](./media/stream-analytics-operation-logs/04-stream-analytics-operation-logs.png)  

<span data-ttu-id="f7f7a-137">在 Azure 入口網站中，您可以按訊息層級篩選，以檢視 **嚴重** 事件。</span><span class="sxs-lookup"><span data-stu-id="f7f7a-137">In the Azure portal, you can filter by level of message to view **Critical** events.</span></span>

  ![Azure 入口網站偵錯](./media/stream-analytics-operation-logs/10-stream-analytics-operation-logs.png)  

<span data-ttu-id="f7f7a-139">您可以選取任何一個失敗項目，並按一下 [詳細資料]  來取得有關此錯誤的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f7f7a-139">You can select any one of the failures, and click on the **Details** for more information on the error.</span></span>  <span data-ttu-id="f7f7a-140">某些錯誤訊息也會提供如何降低此問題之風險的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="f7f7a-140">Some error messages also provide information about how to mitigate the issue.</span></span> 

  ![Operation Details](./media/stream-analytics-operation-logs/05-stream-analytics-operation-logs.png)  

<span data-ttu-id="f7f7a-142">萬一您需要連絡[支援服務](https://azure.microsoft.com/support/options/)或透過 [MSDN 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)將資訊提供給團隊，請注意作業詳細資料，特別是**相互關聯識別碼**。</span><span class="sxs-lookup"><span data-stu-id="f7f7a-142">In case you need to contact [Support](https://azure.microsoft.com/support/options/) or provide information to the team via the [MSDN forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), please note the Operation Details, specifically the **Correlation ID**.</span></span> 

## <a name="get-help"></a><span data-ttu-id="f7f7a-143">取得說明</span><span class="sxs-lookup"><span data-stu-id="f7f7a-143">Get help</span></span>
<span data-ttu-id="f7f7a-144">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="f7f7a-144">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7f7a-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f7f7a-145">Next steps</span></span>
* [<span data-ttu-id="f7f7a-146">Azure Stream Analytics 介紹</span><span class="sxs-lookup"><span data-stu-id="f7f7a-146">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="f7f7a-147">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f7f7a-147">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="f7f7a-148">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="f7f7a-148">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="f7f7a-149">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="f7f7a-149">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="f7f7a-150">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="f7f7a-150">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

