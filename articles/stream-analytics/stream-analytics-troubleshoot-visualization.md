---
title: "aaaVisualize 和疑難排解串流分析工作 |Microsoft 文件"
description: "了解 toovisualize 資料流分析工作如何管線使用 hello 診斷圖表功能進行疑難排解自助功能。"
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: d87841cd-c59f-4a46-b46e-8b904fdc12e9
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 8a6715be601fdc47b8d9caf4112da161dad22618
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-and-troubleshoot-stream-analytics-jobs"></a><span data-ttu-id="fee6d-103">以視覺化方式呈現串流分析工作並進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="fee6d-103">Visualize and troubleshoot Stream Analytics jobs</span></span>
<span data-ttu-id="fee6d-104">在 Stream Analytics 中，與其他雲端架構技術一樣，疑難排解是有時候需要的 toolook 到為什麼作業不會產生預期的 hello 輸出 （或任何輸出就此而言）。</span><span class="sxs-lookup"><span data-stu-id="fee6d-104">In Stream Analytics, as with other cloud-based technologies, troubleshooting is sometimes needed toolook into why a job does not produce hello expected output (or any output for that matter).</span></span> <span data-ttu-id="fee6d-105">這一點，串流分析會提供視覺化資料流工作的 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="fee6d-105">With this in mind, Stream Analytics provides hello capability for visualizing a streaming job.</span></span> <span data-ttu-id="fee6d-106">這也是很方便做為模型工具，而且 hello 端權益，適用於需要其工作的文件的部分。</span><span class="sxs-lookup"><span data-stu-id="fee6d-106">This is also handy as a modeling tool and has hello side benefit for those requiring documentation of their work.</span></span>

<span data-ttu-id="fee6d-107">Hello 視覺效果中面板 hello 輸入看到以及 hello 查詢正在執行且然後所有 hello 輸出都設定。</span><span class="sxs-lookup"><span data-stu-id="fee6d-107">In hello visualization panel hello inputs are visible as well as hello query being executed and then all hello outputs configured.</span></span> <span data-ttu-id="fee6d-108">連線或設定問題可能會變得更清楚看到，而且它也可能很有幫助 toosee 您設定的視覺表示法。</span><span class="sxs-lookup"><span data-stu-id="fee6d-108">Connectivity or configuration issues can become more apparent and it can also be helpful toosee a visual representation of your configuration.</span></span>

## <a name="using-hello-diagnosis-diagram-tool"></a><span data-ttu-id="fee6d-109">使用 hello 診斷圖表工具</span><span class="sxs-lookup"><span data-stu-id="fee6d-109">Using hello diagnosis diagram tool</span></span>
<span data-ttu-id="fee6d-110">這個視覺化檢視，只要按一下 hello 中的 「 診斷圖 」 按鈕 tooaccess hello hello hello 資料流分析作業的 [設定] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="fee6d-110">tooaccess this visualizer, simply click on hello “Diagnosis diagram” button in hello “Settings” blade of hello of hello Stream Analytics job.</span></span>

![stream-analytics-troubleshoot-visualization-diagnosis-diagram](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-diagnosis-diagram1.png)

<span data-ttu-id="fee6d-112">每個輸入和輸出是自動程式化的色彩 tooindicate hello 目前狀態該元件，如下所示。</span><span class="sxs-lookup"><span data-stu-id="fee6d-112">Every input and output is color coded tooindicate hello current state of that component, as shown below.</span></span>

![stream-analytics-troubleshoot-visualization-input-map](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-input-map.png)

<span data-ttu-id="fee6d-114">當 hello 使用者想 toolook 中繼查詢步驟 toounderstand hello 資料流模式內工作時，hello 視覺效果工具會提供成它的元件步驟並 hello 流程順序的 hello 分解的 hello 查詢的檢視。</span><span class="sxs-lookup"><span data-stu-id="fee6d-114">When hello user wants toolook at intermediate query steps toounderstand hello data flow patterns inside a job, hello visualization tool provides a view of hello breakdown of hello query into its component steps and hello flow sequence.</span></span> <span data-ttu-id="fee6d-115">按一下每個查詢步驟會在編輯窗格中所示的查詢顯示 hello 對應的章節。</span><span class="sxs-lookup"><span data-stu-id="fee6d-115">Clicking on each query step will show hello corresponding section in a query editing pane as illustrated.</span></span> 

![stream-analytics-troubleshoot-visualization-intermediate-steps](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-intermediate-steps.png)

## <a name="next-steps"></a><span data-ttu-id="fee6d-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fee6d-117">Next steps</span></span>
* [<span data-ttu-id="fee6d-118">簡介 tooAzure 資料流分析</span><span class="sxs-lookup"><span data-stu-id="fee6d-118">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="fee6d-119">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="fee6d-119">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="fee6d-120">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="fee6d-120">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="fee6d-121">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="fee6d-121">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="fee6d-122">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="fee6d-122">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

