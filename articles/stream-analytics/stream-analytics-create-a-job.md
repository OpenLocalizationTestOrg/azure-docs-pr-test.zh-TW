---
title: "如何為串流分析建立資料分析處理工作 | Microsoft Docs"
description: "為串流分析建立資料分析處理工作 | 學習路徑區段。"
keywords: "資料分析處理"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: e825fbcf-69e9-443f-b402-3b7a4568f415
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 05fdf1e20efd129cdfc27e1d37bc9e124edf5dcd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-create-a-data-analytics-processing-job-for-stream-analytics"></a><span data-ttu-id="8b953-104">如何為串流分析建立資料分析處理工作</span><span class="sxs-lookup"><span data-stu-id="8b953-104">How to create a data analytics processing job for Stream Analytics</span></span>
<span data-ttu-id="8b953-105">Azure 串流分析中的最上層資源就是串流分析工作。</span><span class="sxs-lookup"><span data-stu-id="8b953-105">The top-level resource in Azure Stream Analytics is a Stream Analytics Job.</span></span>  <span data-ttu-id="8b953-106">其包含一或多個輸入資料來源、一個表示資料轉換的查詢，以及一或多個用來寫入結果的輸出目標。</span><span class="sxs-lookup"><span data-stu-id="8b953-106">It consists of one or more input data sources, a query expressing the data transformation, and one or more output targets that results are written to.</span></span> <span data-ttu-id="8b953-107">這些功能結合的結果，讓使用者能夠執行串流資料案例的資料分析處理工作。</span><span class="sxs-lookup"><span data-stu-id="8b953-107">Together these enable the user to perform data analytics processing for streaming data scenarios.</span></span>

<span data-ttu-id="8b953-108">若要開始使用串流分析，您必須先建立新的串流分析工作。</span><span class="sxs-lookup"><span data-stu-id="8b953-108">To start using Stream Analytics, begin by creating a new Stream Analytics job.</span></span>  <span data-ttu-id="8b953-109">請注意，直到作業開始之前，這個動作不會以任何方式計費。</span><span class="sxs-lookup"><span data-stu-id="8b953-109">Note this action has no billing implications until the job is started.</span></span>

1. <span data-ttu-id="8b953-110">登入線上 [Azure 傳統入口網站](http://manage.windowsazure.com)或 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="8b953-110">Sign in on the online [Azure classic portal](http://manage.windowsazure.com) or the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="8b953-111">在入口網站中︰按一下 [新增]，根據您的入口網站按一下 [資料服務] 或 [資料分析]，然後按一下 [Azure 串流分析] 或 [串流分析]，再按一下 [快速建立]。</span><span class="sxs-lookup"><span data-stu-id="8b953-111">In the portal: **Click New**, then click **Data Services** or **Data Analytics** depending on your portal and then click **Azure Stream Analytics** or **Stream Analytics** and then **Quick Create**.</span></span>
   
   ![資料分析處理工作精靈](./media/stream-analytics-create-a-job/1-stream-analytics-create-a-job.png)  
   
   ![建立資料分析處理工作](./media/stream-analytics-create-a-job/4-stream-analytics-create-a-job.png)  
3. <span data-ttu-id="8b953-114">為串流分析工作指定所需的組態。</span><span class="sxs-lookup"><span data-stu-id="8b953-114">Specify the desired configuration for the Stream Analytics job.</span></span>
   
   * <span data-ttu-id="8b953-115">請在 [工作名稱]  方塊輸入名稱，以識別串流分析工作。</span><span class="sxs-lookup"><span data-stu-id="8b953-115">In the **Job Name** box, enter a name to identify the Stream Analytics job.</span></span> <span data-ttu-id="8b953-116">[工作名稱]  經驗證後，[工作名稱] 方塊中便會出現綠色的核取記號。</span><span class="sxs-lookup"><span data-stu-id="8b953-116">When the **Job Name** is validated, a green check mark appears in the Job Name box.</span></span> <span data-ttu-id="8b953-117">此 [工作名稱]  只能包含英數及 '-' 字元，且長度必須介於 3 到 63 個字元。</span><span class="sxs-lookup"><span data-stu-id="8b953-117">The **Job Name** may contain only alphanumeric characters and the '-' character, and must be between 3 and 63 characters.</span></span>
   * <span data-ttu-id="8b953-118">請使用 Azure 入口網站的 [區域] 或 Azure 入口網站的 [位置]，來指定您要用來執行工作的地理位置。</span><span class="sxs-lookup"><span data-stu-id="8b953-118">Use **Region** in the Azure portal or **Location** in the Azure portal to specify the geographic location where you want to run the job.</span></span>
   * <span data-ttu-id="8b953-119">如果您使用的是 Azure 入口網站，請選取或建立儲存體帳戶來做為「區域監視儲存體帳戶」 。</span><span class="sxs-lookup"><span data-stu-id="8b953-119">If using the Azure portal, select or create a storage account to use as the **Regional Monitoring Storage Account**.</span></span> <span data-ttu-id="8b953-120">此儲存體帳戶會用來儲存在此區域內執行之所有串流分析工作的監視資料。</span><span class="sxs-lookup"><span data-stu-id="8b953-120">This storage account is used to store monitoring data for all Stream Analytics jobs running in this region.</span></span>
   * <span data-ttu-id="8b953-121">如果使用 Azure 入口網站，請指定新的或現有的 **資源群組** 來保存應用程式的相關資源。</span><span class="sxs-lookup"><span data-stu-id="8b953-121">If using the Azure portal, specify a new or existing **Resource Group** to hold related resources for your application.</span></span>
4. <span data-ttu-id="8b953-122">當新的串流分析工作選項設定完畢之後，請按一下 [建立串流分析工作] 。</span><span class="sxs-lookup"><span data-stu-id="8b953-122">Once the new Stream Analytics job options are configured, click **Create Stream Analytics Job**.</span></span> <span data-ttu-id="8b953-123">建立串流分析工作可能需要數分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="8b953-123">It can take a few minutes for the Stream Analytics job to be created.</span></span> <span data-ttu-id="8b953-124">若要檢查狀態，您可以監視 [通知中樞] 中的進度。</span><span class="sxs-lookup"><span data-stu-id="8b953-124">To check the status, you can monitor the progress in the Notifications hub.</span></span>
   
   ![資料分析處理作業通知中樞](./media/stream-analytics-create-a-job/2-stream-analytics-create-a-job.png)  
   
   ![Azure 入口網站中資料分析處理作業的建立作業](./media/stream-analytics-create-a-job/5-stream-analytics-create-a-job.png)  
5. <span data-ttu-id="8b953-127">新作業會顯示 [已建立] 的狀態。</span><span class="sxs-lookup"><span data-stu-id="8b953-127">The new job will show a status of **Created**.</span></span> <span data-ttu-id="8b953-128">請注意，此時 [開始]  按鈕已停用。</span><span class="sxs-lookup"><span data-stu-id="8b953-128">Notice that the **Start** button is disabled.</span></span> <span data-ttu-id="8b953-129">請先設定作業輸入、查詢和輸出，才能開始作業。</span><span class="sxs-lookup"><span data-stu-id="8b953-129">Configure the job input, query, and output before you start the job.</span></span>
   
   ![資料分析處理的作業狀態](./media/stream-analytics-create-a-job/3-stream-analytics-create-a-job.png)  
   
   ![Azure 入口網站中資料分析處理的作業狀態](./media/stream-analytics-create-a-job/6-stream-analytics-create-a-job.png)  

## <a name="get-help"></a><span data-ttu-id="8b953-132">取得說明</span><span class="sxs-lookup"><span data-stu-id="8b953-132">Get help</span></span>
<span data-ttu-id="8b953-133">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="8b953-133">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b953-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8b953-134">Next steps</span></span>
* [<span data-ttu-id="8b953-135">Azure Stream Analytics 介紹</span><span class="sxs-lookup"><span data-stu-id="8b953-135">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="8b953-136">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8b953-136">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="8b953-137">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="8b953-137">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="8b953-138">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="8b953-138">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="8b953-139">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="8b953-139">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

