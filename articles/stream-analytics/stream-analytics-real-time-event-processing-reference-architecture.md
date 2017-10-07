---
title: "處理資料流分析的事件處理 aaaReal 時間事件 |Microsoft 文件"
description: "了解一組 Azure 服務可如何交互操作以啟用即時事件處理與分析。"
keywords: "即時處理, 事件處理, 參考架構"
services: stream-analytics,event-hubs,storage,sql-database
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: 
ms.assetid: 11af48bc-313c-4527-8c80-91088dc9f3c6
ms.service: stream-analytics
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: jeffstok
ms.openlocfilehash: a43c503d709609ba61e9932822d30bc2208906ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="reference-architecture-real-time-event-processing-with-microsoft-azure-stream-analytics"></a><span data-ttu-id="10047-104">參考架構：使用 Microsoft Azure 串流分析的即時事件處理</span><span class="sxs-lookup"><span data-stu-id="10047-104">Reference architecture: Real-time event processing with Microsoft Azure Stream Analytics</span></span>
<span data-ttu-id="10047-105">使用 Azure Stream Analytics 處理即時事件的 hello 參考架構是預定的 tooprovide 部署即時平台即服務 (PaaS) 資料流處理解決方案使用 Microsoft Azure 的泛型藍圖。</span><span class="sxs-lookup"><span data-stu-id="10047-105">hello reference architecture for real-time event processing with Azure Stream Analytics is intended tooprovide a generic blueprint for deploying a real-time platform as a service (PaaS) stream-processing solution with Microsoft Azure.</span></span>

## <a name="summary"></a><span data-ttu-id="10047-106">摘要</span><span class="sxs-lookup"><span data-stu-id="10047-106">Summary</span></span>
<span data-ttu-id="10047-107">傳統上，分析解決方案已根據擁有功能，例如 ETL （擷取、 轉換、 載入） 和資料倉儲資料的預存的先前 tooanalysis 所在。</span><span class="sxs-lookup"><span data-stu-id="10047-107">Traditionally, analytics solutions have been based on capabilities such as ETL (extract, transform, load) and data warehousing, where data is stored prior tooanalysis.</span></span> <span data-ttu-id="10047-108">多變的需求，包括更多快速抵達的資料，會將此現有的模型 toohello 限制推送。</span><span class="sxs-lookup"><span data-stu-id="10047-108">Changing requirements, including more rapidly arriving data, are pushing this existing model toohello limit.</span></span> <span data-ttu-id="10047-109">hello 能力 tooanalyze 資料內移動資料流之前 toostorage 是一種解決方案，而且不是一項新功能，而 hello 方法已不被廣泛採用跨所有產業有關。</span><span class="sxs-lookup"><span data-stu-id="10047-109">hello ability tooanalyze data within moving streams prior toostorage is one solution, and while it is not a new capability, hello approach has not been widely adopted across all industry verticals.</span></span> 

<span data-ttu-id="10047-110">Microsoft Azure 提供分析技術的全面目錄，可以支援一系列不同的解決方案案例和要求。</span><span class="sxs-lookup"><span data-stu-id="10047-110">Microsoft Azure provides an extensive catalog of analytics technologies that are capable of supporting an array of different solution scenarios and requirements.</span></span> <span data-ttu-id="10047-111">選取的端對端方案的 Azure 服務 toodeploy 可以 hello 廣度的供應項目是項挑戰。</span><span class="sxs-lookup"><span data-stu-id="10047-111">Selecting which Azure services toodeploy for an end-to-end solution can be a challenge given hello breadth of offerings.</span></span> <span data-ttu-id="10047-112">這份文件設計的 toodescribe hello 功能並不互通的 hello 支援事件資料流的解決方案的各種 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="10047-112">This paper is designed toodescribe hello capabilities and interoperation of hello various Azure services that support an event-streaming solution.</span></span> <span data-ttu-id="10047-113">它也會說明一些 hello 案例，客戶可以受益此類型的方法。</span><span class="sxs-lookup"><span data-stu-id="10047-113">It also explains some of hello scenarios in which customers can benefit from this type of approach.</span></span>

## <a name="contents"></a><span data-ttu-id="10047-114">內容</span><span class="sxs-lookup"><span data-stu-id="10047-114">Contents</span></span>
* <span data-ttu-id="10047-115">執行摘要</span><span class="sxs-lookup"><span data-stu-id="10047-115">Executive Summary</span></span>
* <span data-ttu-id="10047-116">簡介 tooReal 時間分析</span><span class="sxs-lookup"><span data-stu-id="10047-116">Introduction tooReal-Time Analytics</span></span>
* <span data-ttu-id="10047-117">在 Azure 中的即時資料價值定位</span><span class="sxs-lookup"><span data-stu-id="10047-117">Value Proposition of Real-Time Data in Azure</span></span>
* <span data-ttu-id="10047-118">即時分析的常見案例</span><span class="sxs-lookup"><span data-stu-id="10047-118">Common Scenarios for Real-Time Analytics</span></span>
* <span data-ttu-id="10047-119">架構與元件</span><span class="sxs-lookup"><span data-stu-id="10047-119">Architecture and Components</span></span>
  * <span data-ttu-id="10047-120">資料來源</span><span class="sxs-lookup"><span data-stu-id="10047-120">Data Sources</span></span>
  * <span data-ttu-id="10047-121">資料整合層</span><span class="sxs-lookup"><span data-stu-id="10047-121">Data-Integration Layer</span></span>
  * <span data-ttu-id="10047-122">即時分析層</span><span class="sxs-lookup"><span data-stu-id="10047-122">Real-time Analytics Layer</span></span>
  * <span data-ttu-id="10047-123">資料儲存層</span><span class="sxs-lookup"><span data-stu-id="10047-123">Data Storage Layer</span></span>
  * <span data-ttu-id="10047-124">展示/使用層</span><span class="sxs-lookup"><span data-stu-id="10047-124">Presentation / Consumption Layer</span></span>
* <span data-ttu-id="10047-125">結論</span><span class="sxs-lookup"><span data-stu-id="10047-125">Conclusion</span></span>

<span data-ttu-id="10047-126">**作者：** Charles Feddersen, Solution Architect, Data Insights Center of Excellence, Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="10047-126">**Author:** Charles Feddersen, Solution Architect, Data Insights Center of Excellence, Microsoft Corporation</span></span>

<span data-ttu-id="10047-127">**發行日期：** 2015 年 1 月</span><span class="sxs-lookup"><span data-stu-id="10047-127">**Published:** January 2015</span></span>

<span data-ttu-id="10047-128">**修訂版本：** 1.0</span><span class="sxs-lookup"><span data-stu-id="10047-128">**Revision:** 1.0</span></span>

<span data-ttu-id="10047-129">**下載：** [使用 Microsoft Azure 串流分析的即時事件處理](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)</span><span class="sxs-lookup"><span data-stu-id="10047-129">**Download:** [Real-Time Event Processing with Microsoft Azure Stream Analytics](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)</span></span>

## <a name="get-help"></a><span data-ttu-id="10047-130">取得說明</span><span class="sxs-lookup"><span data-stu-id="10047-130">Get help</span></span>
<span data-ttu-id="10047-131">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="10047-131">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="10047-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="10047-132">Next steps</span></span>
* [<span data-ttu-id="10047-133">簡介 tooAzure 資料流分析</span><span class="sxs-lookup"><span data-stu-id="10047-133">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="10047-134">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="10047-134">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="10047-135">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="10047-135">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="10047-136">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="10047-136">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="10047-137">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="10047-137">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

