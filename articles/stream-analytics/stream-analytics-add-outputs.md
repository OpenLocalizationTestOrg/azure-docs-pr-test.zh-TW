---
title: "aaaHow tooconfigure 資料輸出資料流分析作業 |Microsoft 文件"
description: "設定串流分析工作的輸出 | 學習路徑區段。"
keywords: "資料輸出, 資料移動"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 3bbea3da-bfce-4af1-a15e-d4b23874034f
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/26/2017
ms.author: samacha
ms.openlocfilehash: c5d89e9e9f9211d3e778580c071dd53d56aed9fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-data-outputs-for-stream-analytics-jobs"></a><span data-ttu-id="2b74c-104">Tooconfigure 資料輸出資料流分析工作的方式</span><span class="sxs-lookup"><span data-stu-id="2b74c-104">How tooconfigure data outputs for Stream Analytics jobs</span></span>

<span data-ttu-id="2b74c-105">Azure 串流分析工作可以是連線的 tooone 或更多的資料輸出，定義連接 tooan 現有資料接收。</span><span class="sxs-lookup"><span data-stu-id="2b74c-105">Azure Stream Analytics jobs can be connected tooone or more data outputs, which define a connection tooan existing data sink.</span></span> <span data-ttu-id="2b74c-106">串流分析工作處理，並將內送資料轉換，因為資料輸出事件資料流寫入 tooyour 工作的輸出。</span><span class="sxs-lookup"><span data-stu-id="2b74c-106">As your Stream Analytics job processes and transforms incoming data, a stream of data output events is written tooyour job's output.</span></span>

<span data-ttu-id="2b74c-107">使用的 toosource 即時儀表板或警示、 觸發程序的資料移動工作流程或只是供稍後處理批次的封存資料，可以是資料流分析資料輸出。</span><span class="sxs-lookup"><span data-stu-id="2b74c-107">Stream Analytics data outputs can be used toosource real-time dashboards or alerts, trigger data movement workflows, or simply archive data for batch processing later on.</span></span> <span data-ttu-id="2b74c-108">串流分析與數個 Azure 服務具有第一級的整合，將在此詳述。</span><span class="sxs-lookup"><span data-stu-id="2b74c-108">Stream Analytics has first class integration with several Azure services, which are documented in detail here.</span></span>

<span data-ttu-id="2b74c-109">tooadd 輸出 tooyour 資料流分析工作：</span><span class="sxs-lookup"><span data-stu-id="2b74c-109">tooadd an output tooyour Stream Analytics job:</span></span>

1. <span data-ttu-id="2b74c-110">在 hello [Azure 入口網站](https://portal.azure.com)，開啟您的工作，然後按一下**輸出**，然後按一下**新增**在 hello 輸出刀鋒視窗中出現。</span><span class="sxs-lookup"><span data-stu-id="2b74c-110">In hello [Azure portal](https://portal.azure.com), open your job and click **Outputs** and then click **Add** in hello Outputs blade that appears.</span></span>
   
    ![加入輸出](./media/stream-analytics-add-outputs/1-stream-analytics-add-outputs.png)  
   
2. <span data-ttu-id="2b74c-112">提供在 hello 此輸出的易記名稱**輸出別名**方塊。</span><span class="sxs-lookup"><span data-stu-id="2b74c-112">Provide a friendly name for this output in hello **Output Alias** box.</span></span> <span data-ttu-id="2b74c-113">這個名稱可以用於作業的查詢，之後會在 toorefer toohello 輸出。</span><span class="sxs-lookup"><span data-stu-id="2b74c-113">This name can be used in your job's query later on toorefer toohello output.</span></span>  
   
    <span data-ttu-id="2b74c-114">在所需的 hello 連接屬性 tooconnect tooyour 輸出 hello 其餘部分填滿。</span><span class="sxs-lookup"><span data-stu-id="2b74c-114">Fill in hello rest of hello required connection properties tooconnect tooyour output.</span></span>  <span data-ttu-id="2b74c-115">這些欄位會因輸出類型而有所不同，其詳細定義在這裡。</span><span class="sxs-lookup"><span data-stu-id="2b74c-115">These fields vary by output type and are defined in detail here.</span></span>  
   
    ![選擇資料移動類型](./media/stream-analytics-add-outputs/2-stream-analytics-add-outputs.png)  
   
3. <span data-ttu-id="2b74c-117">根據 hello 輸出類型，您可能需要的 toospecify hello 資料已序列化或格式化的方式。</span><span class="sxs-lookup"><span data-stu-id="2b74c-117">Depending on hello output type, you may need toospecify how hello data is serialized or formatted.</span></span> <span data-ttu-id="2b74c-118">記載 hello 特定的序列化設定每個輸出類型。</span><span class="sxs-lookup"><span data-stu-id="2b74c-118">hello specific serialization settings for each output type are documented here.</span></span>
   
    <span data-ttu-id="2b74c-119">填寫 hello rest hello 所需的連接屬性 tooconnect tooyour 資料來源。</span><span class="sxs-lookup"><span data-stu-id="2b74c-119">Fill in hello rest of hello required connection properties tooconnect tooyour data source.</span></span> <span data-ttu-id="2b74c-120">這些欄位變更類型的輸入和來源的類型，且已定義在 hello 詳細[建立作業的發行項](stream-analytics-create-a-job.md)。</span><span class="sxs-lookup"><span data-stu-id="2b74c-120">These fields vary by type of input and source type and are defined in detail in hello [Create Job article](stream-analytics-create-a-job.md).</span></span>  

> [!Note]
>
> <span data-ttu-id="2b74c-121">任何輸出項目加入的 toohello 的作業，必須先建立 hello 作業已啟動，而且流動開始事件。</span><span class="sxs-lookup"><span data-stu-id="2b74c-121">Any output element added toohello job, must exist before hello job is started and events start flowing.</span></span> <span data-ttu-id="2b74c-122">比方說，如果您使用 Blob 儲存體做為輸出時，hello 作業將不會自動建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="2b74c-122">For example, if you use Blob storage as an output, hello job will not create a storage account automatically.</span></span> <span data-ttu-id="2b74c-123">它需要 toobe hello ASA 工作啟動之前，由 hello 使用者所建立。</span><span class="sxs-lookup"><span data-stu-id="2b74c-123">It needs toobe created by hello user before hello ASA job is started.</span></span>
> 
 

## <a name="get-help"></a><span data-ttu-id="2b74c-124">取得說明</span><span class="sxs-lookup"><span data-stu-id="2b74c-124">Get help</span></span>
<span data-ttu-id="2b74c-125">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="2b74c-125">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b74c-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2b74c-126">Next steps</span></span>
* [<span data-ttu-id="2b74c-127">簡介 tooAzure 資料流分析</span><span class="sxs-lookup"><span data-stu-id="2b74c-127">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="2b74c-128">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2b74c-128">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="2b74c-129">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="2b74c-129">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="2b74c-130">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="2b74c-130">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="2b74c-131">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="2b74c-131">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

