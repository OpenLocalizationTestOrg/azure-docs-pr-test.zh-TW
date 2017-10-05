---
title: "使用串流分析事件處理的即時事件處理 | Microsoft Docs"
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
ms.openlocfilehash: b3057be995e551aac0761c3ce40a8dbf828a5f29
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="reference-architecture-real-time-event-processing-with-microsoft-azure-stream-analytics"></a><span data-ttu-id="fcd2f-104">參考架構：使用 Microsoft Azure 串流分析的即時事件處理</span><span class="sxs-lookup"><span data-stu-id="fcd2f-104">Reference architecture: Real-time event processing with Microsoft Azure Stream Analytics</span></span>
<span data-ttu-id="fcd2f-105">使用 Microsoft Azure 串流分析的即時事件處理之參考架構主要用來提供一般的藍圖，供使用 Microsoft Azure 部署即時的平台即服務 (PaaS) 串流處理解決方案。</span><span class="sxs-lookup"><span data-stu-id="fcd2f-105">The reference architecture for real-time event processing with Azure Stream Analytics is intended to provide a generic blueprint for deploying a real-time platform as a service (PaaS) stream-processing solution with Microsoft Azure.</span></span>

## <a name="summary"></a><span data-ttu-id="fcd2f-106">摘要</span><span class="sxs-lookup"><span data-stu-id="fcd2f-106">Summary</span></span>
<span data-ttu-id="fcd2f-107">傳統上，分析解決方案為基於例如 ETL (擷取、轉換、載入) 和資料倉儲等功能運作，其中資料在分析前就已儲存。</span><span class="sxs-lookup"><span data-stu-id="fcd2f-107">Traditionally, analytics solutions have been based on capabilities such as ETL (extract, transform, load) and data warehousing, where data is stored prior to analysis.</span></span> <span data-ttu-id="fcd2f-108">不斷變化的要求，包含更快速到達的資料，將此現有的模型推到了極限。</span><span class="sxs-lookup"><span data-stu-id="fcd2f-108">Changing requirements, including more rapidly arriving data, are pushing this existing model to the limit.</span></span> <span data-ttu-id="fcd2f-109">在移動串流到儲存體之前分析資料的能力是一種解決方式，雖然這並非新的功能，但此方式並未廣泛受到所有產業縱向市場採用。</span><span class="sxs-lookup"><span data-stu-id="fcd2f-109">The ability to analyze data within moving streams prior to storage is one solution, and while it is not a new capability, the approach has not been widely adopted across all industry verticals.</span></span> 

<span data-ttu-id="fcd2f-110">Microsoft Azure 提供分析技術的全面目錄，可以支援一系列不同的解決方案案例和要求。</span><span class="sxs-lookup"><span data-stu-id="fcd2f-110">Microsoft Azure provides an extensive catalog of analytics technologies that are capable of supporting an array of different solution scenarios and requirements.</span></span> <span data-ttu-id="fcd2f-111">當產品相當多元時，選取要為端對端解決方案部署哪一個 Azure 服務可說是項挑戰。</span><span class="sxs-lookup"><span data-stu-id="fcd2f-111">Selecting which Azure services to deploy for an end-to-end solution can be a challenge given the breadth of offerings.</span></span> <span data-ttu-id="fcd2f-112">本文件主要用來描述支援事件串流解決方案之各種 Azure 服務的功能和交互操作。</span><span class="sxs-lookup"><span data-stu-id="fcd2f-112">This paper is designed to describe the capabilities and interoperation of the various Azure services that support an event-streaming solution.</span></span> <span data-ttu-id="fcd2f-113">這也說明客戶可從此類方式中獲益的某些案例。</span><span class="sxs-lookup"><span data-stu-id="fcd2f-113">It also explains some of the scenarios in which customers can benefit from this type of approach.</span></span>

## <a name="contents"></a><span data-ttu-id="fcd2f-114">內容</span><span class="sxs-lookup"><span data-stu-id="fcd2f-114">Contents</span></span>
* <span data-ttu-id="fcd2f-115">執行摘要</span><span class="sxs-lookup"><span data-stu-id="fcd2f-115">Executive Summary</span></span>
* <span data-ttu-id="fcd2f-116">即時分析簡介</span><span class="sxs-lookup"><span data-stu-id="fcd2f-116">Introduction to Real-Time Analytics</span></span>
* <span data-ttu-id="fcd2f-117">在 Azure 中的即時資料價值定位</span><span class="sxs-lookup"><span data-stu-id="fcd2f-117">Value Proposition of Real-Time Data in Azure</span></span>
* <span data-ttu-id="fcd2f-118">即時分析的常見案例</span><span class="sxs-lookup"><span data-stu-id="fcd2f-118">Common Scenarios for Real-Time Analytics</span></span>
* <span data-ttu-id="fcd2f-119">架構與元件</span><span class="sxs-lookup"><span data-stu-id="fcd2f-119">Architecture and Components</span></span>
  * <span data-ttu-id="fcd2f-120">資料來源</span><span class="sxs-lookup"><span data-stu-id="fcd2f-120">Data Sources</span></span>
  * <span data-ttu-id="fcd2f-121">資料整合層</span><span class="sxs-lookup"><span data-stu-id="fcd2f-121">Data-Integration Layer</span></span>
  * <span data-ttu-id="fcd2f-122">即時分析層</span><span class="sxs-lookup"><span data-stu-id="fcd2f-122">Real-time Analytics Layer</span></span>
  * <span data-ttu-id="fcd2f-123">資料儲存層</span><span class="sxs-lookup"><span data-stu-id="fcd2f-123">Data Storage Layer</span></span>
  * <span data-ttu-id="fcd2f-124">展示/使用層</span><span class="sxs-lookup"><span data-stu-id="fcd2f-124">Presentation / Consumption Layer</span></span>
* <span data-ttu-id="fcd2f-125">結論</span><span class="sxs-lookup"><span data-stu-id="fcd2f-125">Conclusion</span></span>

<span data-ttu-id="fcd2f-126">**作者：** Charles Feddersen, Solution Architect, Data Insights Center of Excellence, Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="fcd2f-126">**Author:** Charles Feddersen, Solution Architect, Data Insights Center of Excellence, Microsoft Corporation</span></span>

<span data-ttu-id="fcd2f-127">**發行日期：** 2015 年 1 月</span><span class="sxs-lookup"><span data-stu-id="fcd2f-127">**Published:** January 2015</span></span>

<span data-ttu-id="fcd2f-128">**修訂版本：** 1.0</span><span class="sxs-lookup"><span data-stu-id="fcd2f-128">**Revision:** 1.0</span></span>

<span data-ttu-id="fcd2f-129">**下載：** [使用 Microsoft Azure 串流分析的即時事件處理](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)</span><span class="sxs-lookup"><span data-stu-id="fcd2f-129">**Download:** [Real-Time Event Processing with Microsoft Azure Stream Analytics](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)</span></span>

## <a name="get-help"></a><span data-ttu-id="fcd2f-130">取得說明</span><span class="sxs-lookup"><span data-stu-id="fcd2f-130">Get help</span></span>
<span data-ttu-id="fcd2f-131">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="fcd2f-131">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="fcd2f-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fcd2f-132">Next steps</span></span>
* [<span data-ttu-id="fcd2f-133">Azure Stream Analytics 介紹</span><span class="sxs-lookup"><span data-stu-id="fcd2f-133">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="fcd2f-134">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="fcd2f-134">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="fcd2f-135">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="fcd2f-135">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="fcd2f-136">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="fcd2f-136">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="fcd2f-137">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="fcd2f-137">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

