---
title: "如何設定串流分析工作的資料輸出 | Microsoft Docs"
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
ms.openlocfilehash: 1ffa517469da1a8d79917b9747abc97ca3bef463
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-data-outputs-for-stream-analytics-jobs"></a><span data-ttu-id="4bcc4-104">如何設定串流分析工作的資料輸出</span><span class="sxs-lookup"><span data-stu-id="4bcc4-104">How to configure data outputs for Stream Analytics jobs</span></span>

<span data-ttu-id="4bcc4-105">Azure 串流分析工作可以連線至一或多個輸出，且每個輸出都定義了一個與現有資料接收器之間的連線。</span><span class="sxs-lookup"><span data-stu-id="4bcc4-105">Azure Stream Analytics jobs can be connected to one or more data outputs, which define a connection to an existing data sink.</span></span> <span data-ttu-id="4bcc4-106">當您的串流分析工作處理並轉換傳入的資料時，系統會將資料輸出事件串流寫入工作的輸出中。</span><span class="sxs-lookup"><span data-stu-id="4bcc4-106">As your Stream Analytics job processes and transforms incoming data, a stream of data output events is written to your job's output.</span></span>

<span data-ttu-id="4bcc4-107">串流分析資料輸出可用來獲得即時的儀表板或警示資訊、觸發資料移動流程，或是單純保存資料以供稍後進行批次處理。</span><span class="sxs-lookup"><span data-stu-id="4bcc4-107">Stream Analytics data outputs can be used to source real-time dashboards or alerts, trigger data movement workflows, or simply archive data for batch processing later on.</span></span> <span data-ttu-id="4bcc4-108">串流分析與數個 Azure 服務具有第一級的整合，將在此詳述。</span><span class="sxs-lookup"><span data-stu-id="4bcc4-108">Stream Analytics has first class integration with several Azure services, which are documented in detail here.</span></span>

<span data-ttu-id="4bcc4-109">若要將輸入加入至串流分析工作：</span><span class="sxs-lookup"><span data-stu-id="4bcc4-109">To add an output to your Stream Analytics job:</span></span>

1. <span data-ttu-id="4bcc4-110">在 [Azure 入口網站](https://portal.azure.com)中開啟您的作業並按一下 [輸出]，然後在隨即顯示的輸出刀鋒視窗中按一下[新增]。</span><span class="sxs-lookup"><span data-stu-id="4bcc4-110">In the [Azure portal](https://portal.azure.com), open your job and click **Outputs** and then click **Add** in the Outputs blade that appears.</span></span>
   
    ![加入輸出](./media/stream-analytics-add-outputs/1-stream-analytics-add-outputs.png)  
   
2. <span data-ttu-id="4bcc4-112">在 [ **輸出別名** ] 方塊中，替此輸出取一個好記的名稱。</span><span class="sxs-lookup"><span data-stu-id="4bcc4-112">Provide a friendly name for this output in the **Output Alias** box.</span></span> <span data-ttu-id="4bcc4-113">此名稱稍後可在作業查詢中用作指稱輸出。</span><span class="sxs-lookup"><span data-stu-id="4bcc4-113">This name can be used in your job's query later on to refer to the output.</span></span>  
   
    <span data-ttu-id="4bcc4-114">填寫其餘必要的連接屬性，以連接到輸出。</span><span class="sxs-lookup"><span data-stu-id="4bcc4-114">Fill in the rest of the required connection properties to connect to your output.</span></span>  <span data-ttu-id="4bcc4-115">這些欄位會因輸出類型而有所不同，其詳細定義在這裡。</span><span class="sxs-lookup"><span data-stu-id="4bcc4-115">These fields vary by output type and are defined in detail here.</span></span>  
   
    ![選擇資料移動類型](./media/stream-analytics-add-outputs/2-stream-analytics-add-outputs.png)  
   
3. <span data-ttu-id="4bcc4-117">取決於輸出類型，您可能需要指定資料序列化或格式化的方式。</span><span class="sxs-lookup"><span data-stu-id="4bcc4-117">Depending on the output type, you may need to specify how the data is serialized or formatted.</span></span> <span data-ttu-id="4bcc4-118">每個輸出類型的特定序列化設定值記載於此。</span><span class="sxs-lookup"><span data-stu-id="4bcc4-118">The specific serialization settings for each output type are documented here.</span></span>
   
    <span data-ttu-id="4bcc4-119">填寫其餘必要的連接屬性，以連接到資料來源。</span><span class="sxs-lookup"><span data-stu-id="4bcc4-119">Fill in the rest of the required connection properties to connect to your data source.</span></span> <span data-ttu-id="4bcc4-120">這些欄位會因輸入類型和來源類型而有所不同，詳細定義請見[建立作業文章](stream-analytics-create-a-job.md)。</span><span class="sxs-lookup"><span data-stu-id="4bcc4-120">These fields vary by type of input and source type and are defined in detail in the [Create Job article](stream-analytics-create-a-job.md).</span></span>  

> [!Note]
>
> <span data-ttu-id="4bcc4-121">任何新增至工作的輸出元素，都必須在工作開始之前，以及在事件開始運作之前就已經存在。</span><span class="sxs-lookup"><span data-stu-id="4bcc4-121">Any output element added to the job, must exist before the job is started and events start flowing.</span></span> <span data-ttu-id="4bcc4-122">例如，如果您把 Blob 儲存體當做輸出來使用，工作就不會自動建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="4bcc4-122">For example, if you use Blob storage as an output, the job will not create a storage account automatically.</span></span> <span data-ttu-id="4bcc4-123">使用者必須在 Azure 串流分析工作開始之前建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="4bcc4-123">It needs to be created by the user before the ASA job is started.</span></span>
> 
 

## <a name="get-help"></a><span data-ttu-id="4bcc4-124">取得說明</span><span class="sxs-lookup"><span data-stu-id="4bcc4-124">Get help</span></span>
<span data-ttu-id="4bcc4-125">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="4bcc4-125">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="4bcc4-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4bcc4-126">Next steps</span></span>
* [<span data-ttu-id="4bcc4-127">Azure Stream Analytics 介紹</span><span class="sxs-lookup"><span data-stu-id="4bcc4-127">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="4bcc4-128">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="4bcc4-128">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="4bcc4-129">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="4bcc4-129">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="4bcc4-130">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="4bcc4-130">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="4bcc4-131">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="4bcc4-131">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

