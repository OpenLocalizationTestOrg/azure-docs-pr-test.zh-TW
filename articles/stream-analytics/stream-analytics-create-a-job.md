---
title: "aaaHow toocreate 資料流分析的資料分析處理作業 |Microsoft 文件"
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
ms.openlocfilehash: d4a3c89d8862d59688d06a1719b063efa2ab1c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-data-analytics-processing-job-for-stream-analytics"></a><span data-ttu-id="6e34b-104">如何 toocreate 處理資料分析工作的資料流分析</span><span class="sxs-lookup"><span data-stu-id="6e34b-104">How toocreate a data analytics processing job for Stream Analytics</span></span>
<span data-ttu-id="6e34b-105">在 Azure Stream Analytics hello 最上層資源是串流分析工作。</span><span class="sxs-lookup"><span data-stu-id="6e34b-105">hello top-level resource in Azure Stream Analytics is a Stream Analytics Job.</span></span>  <span data-ttu-id="6e34b-106">它包含一或多個輸入資料來源、 表達 hello 資料轉換、 查詢和結果會寫入一或多個輸出為目標。</span><span class="sxs-lookup"><span data-stu-id="6e34b-106">It consists of one or more input data sources, a query expressing hello data transformation, and one or more output targets that results are written to.</span></span> <span data-ttu-id="6e34b-107">這些一起可讓 hello 使用者 tooperform 資料分析的資料流資料處理實例。</span><span class="sxs-lookup"><span data-stu-id="6e34b-107">Together these enable hello user tooperform data analytics processing for streaming data scenarios.</span></span>

<span data-ttu-id="6e34b-108">toostart 使用 Stream Analytics 中，開始建立新的資料流分析工作。</span><span class="sxs-lookup"><span data-stu-id="6e34b-108">toostart using Stream Analytics, begin by creating a new Stream Analytics job.</span></span>  <span data-ttu-id="6e34b-109">請注意這個動作沒有任何的計費方式，直到 hello 工作已啟動。</span><span class="sxs-lookup"><span data-stu-id="6e34b-109">Note this action has no billing implications until hello job is started.</span></span>

1. <span data-ttu-id="6e34b-110">登入線上 hello [Azure 傳統入口網站](http://manage.windowsazure.com)或 hello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="6e34b-110">Sign in on hello online [Azure classic portal](http://manage.windowsazure.com) or hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="6e34b-111">Hello 入口網站中：**按一下 新增**，然後按一下 **Data Services**或**資料分析**根據您的入口網站，然後按一下**Azure Stream Analytics**或**串流分析**然後**快速建立**。</span><span class="sxs-lookup"><span data-stu-id="6e34b-111">In hello portal: **Click New**, then click **Data Services** or **Data Analytics** depending on your portal and then click **Azure Stream Analytics** or **Stream Analytics** and then **Quick Create**.</span></span>
   
   ![資料分析處理工作精靈](./media/stream-analytics-create-a-job/1-stream-analytics-create-a-job.png)  
   
   ![建立資料分析處理工作](./media/stream-analytics-create-a-job/4-stream-analytics-create-a-job.png)  
3. <span data-ttu-id="6e34b-114">指定 hello hello 資料流分析工作所需的組態。</span><span class="sxs-lookup"><span data-stu-id="6e34b-114">Specify hello desired configuration for hello Stream Analytics job.</span></span>
   
   * <span data-ttu-id="6e34b-115">在 hello**工作名稱**方塊中，輸入名稱 tooidentify hello 資料流分析工作。</span><span class="sxs-lookup"><span data-stu-id="6e34b-115">In hello **Job Name** box, enter a name tooidentify hello Stream Analytics job.</span></span> <span data-ttu-id="6e34b-116">當 hello**工作名稱**驗證時，綠色的核取記號會出現在 hello 工作名稱 方塊。</span><span class="sxs-lookup"><span data-stu-id="6e34b-116">When hello **Job Name** is validated, a green check mark appears in hello Job Name box.</span></span> <span data-ttu-id="6e34b-117">hello**工作名稱**可能只包含英數字元和 hello '-' 字元，而且必須介於 3 到 63 個字元之間。</span><span class="sxs-lookup"><span data-stu-id="6e34b-117">hello **Job Name** may contain only alphanumeric characters and hello '-' character, and must be between 3 and 63 characters.</span></span>
   * <span data-ttu-id="6e34b-118">使用**區域**hello Azure 入口網站中或**位置**在 hello Azure 入口網站 toospecify hello toorun hello 作業所在的地理位置。</span><span class="sxs-lookup"><span data-stu-id="6e34b-118">Use **Region** in hello Azure portal or **Location** in hello Azure portal toospecify hello geographic location where you want toorun hello job.</span></span>
   * <span data-ttu-id="6e34b-119">如果使用 hello Azure 入口網站，請選取或建立 hello 為儲存體帳戶 toouse**區域監視儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="6e34b-119">If using hello Azure portal, select or create a storage account toouse as hello **Regional Monitoring Storage Account**.</span></span> <span data-ttu-id="6e34b-120">這個儲存體帳戶是使用的 toostore 監視在此區域中執行的所有串流分析工作的資料。</span><span class="sxs-lookup"><span data-stu-id="6e34b-120">This storage account is used toostore monitoring data for all Stream Analytics jobs running in this region.</span></span>
   * <span data-ttu-id="6e34b-121">如果使用 hello Azure 入口網站，指定新的或現有的**資源群組**toohold 相關聯的應用程式的資源。</span><span class="sxs-lookup"><span data-stu-id="6e34b-121">If using hello Azure portal, specify a new or existing **Resource Group** toohold related resources for your application.</span></span>
4. <span data-ttu-id="6e34b-122">一旦設定 hello 新的資料流分析工作選項，按一下**建立串流分析工作**。</span><span class="sxs-lookup"><span data-stu-id="6e34b-122">Once hello new Stream Analytics job options are configured, click **Create Stream Analytics Job**.</span></span> <span data-ttu-id="6e34b-123">可能需要幾分鐘，讓建立 hello 資料流分析工作 toobe。</span><span class="sxs-lookup"><span data-stu-id="6e34b-123">It can take a few minutes for hello Stream Analytics job toobe created.</span></span> <span data-ttu-id="6e34b-124">toocheck hello 狀態，您可以監視 hello 通知中樞中的 hello 進度。</span><span class="sxs-lookup"><span data-stu-id="6e34b-124">toocheck hello status, you can monitor hello progress in hello Notifications hub.</span></span>
   
   ![資料分析處理作業通知中樞](./media/stream-analytics-create-a-job/2-stream-analytics-create-a-job.png)  
   
   ![Azure 入口網站中資料分析處理作業的建立作業](./media/stream-analytics-create-a-job/5-stream-analytics-create-a-job.png)  
5. <span data-ttu-id="6e34b-127">hello 新作業將會顯示狀態為**Created**。</span><span class="sxs-lookup"><span data-stu-id="6e34b-127">hello new job will show a status of **Created**.</span></span> <span data-ttu-id="6e34b-128">請注意該 hello**啟動**按鈕已停用。</span><span class="sxs-lookup"><span data-stu-id="6e34b-128">Notice that hello **Start** button is disabled.</span></span> <span data-ttu-id="6e34b-129">Hello 作業開始之前，請設定 hello 作業輸入、 查詢和輸出。</span><span class="sxs-lookup"><span data-stu-id="6e34b-129">Configure hello job input, query, and output before you start hello job.</span></span>
   
   ![資料分析處理的作業狀態](./media/stream-analytics-create-a-job/3-stream-analytics-create-a-job.png)  
   
   ![Azure 入口網站中資料分析處理的作業狀態](./media/stream-analytics-create-a-job/6-stream-analytics-create-a-job.png)  

## <a name="get-help"></a><span data-ttu-id="6e34b-132">取得說明</span><span class="sxs-lookup"><span data-stu-id="6e34b-132">Get help</span></span>
<span data-ttu-id="6e34b-133">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="6e34b-133">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e34b-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6e34b-134">Next steps</span></span>
* [<span data-ttu-id="6e34b-135">簡介 tooAzure 資料流分析</span><span class="sxs-lookup"><span data-stu-id="6e34b-135">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="6e34b-136">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6e34b-136">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="6e34b-137">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="6e34b-137">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="6e34b-138">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="6e34b-138">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="6e34b-139">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="6e34b-139">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

