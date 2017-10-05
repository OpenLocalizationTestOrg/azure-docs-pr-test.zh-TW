---
title: "以視覺化方式呈現串流分析工作並進行疑難排解 | Microsoft Docs"
description: "了解如何使用診斷圖表功能以視覺化方式呈現「串流分析」工作管線，來進行自助疑難排解。"
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
ms.openlocfilehash: 18c39a025f750cf5a17c535ab40923b7cafe413d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="visualize-and-troubleshoot-stream-analytics-jobs"></a><span data-ttu-id="11947-103">以視覺化方式呈現串流分析工作並進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="11947-103">Visualize and troubleshoot Stream Analytics jobs</span></span>
<span data-ttu-id="11947-104">在「串流分析」中，與其他雲端型技術一樣，有時需要進行疑難排解來仔細研究為何某個工作沒有產生預期的輸出 (或就此而言，產生任何輸出)。</span><span class="sxs-lookup"><span data-stu-id="11947-104">In Stream Analytics, as with other cloud-based technologies, troubleshooting is sometimes needed to look into why a job does not produce the expected output (or any output for that matter).</span></span> <span data-ttu-id="11947-105">考量到這一點，「串流分析」提供了以視覺化方式呈現串流工作的功能。</span><span class="sxs-lookup"><span data-stu-id="11947-105">With this in mind, Stream Analytics provides the capability for visualizing a streaming job.</span></span> <span data-ttu-id="11947-106">此功能可作為便利的模型工具，並且對於需要為其工作提供佐證文件的使用者而言，也有附帶的好處。</span><span class="sxs-lookup"><span data-stu-id="11947-106">This is also handy as a modeling tool and has the side benefit for those requiring documentation of their work.</span></span>

<span data-ttu-id="11947-107">在視覺化面板中，可以看到輸入項以及所執行的查詢，還有所有已設定的輸出項。</span><span class="sxs-lookup"><span data-stu-id="11947-107">In the visualization panel the inputs are visible as well as the query being executed and then all the outputs configured.</span></span> <span data-ttu-id="11947-108">連線或設定問題會變得更清楚，此外，以視覺方式呈現您的組態也可能會有幫助。</span><span class="sxs-lookup"><span data-stu-id="11947-108">Connectivity or configuration issues can become more apparent and it can also be helpful to see a visual representation of your configuration.</span></span>

## <a name="using-the-diagnosis-diagram-tool"></a><span data-ttu-id="11947-109">使用診斷圖表工具</span><span class="sxs-lookup"><span data-stu-id="11947-109">Using the diagnosis diagram tool</span></span>
<span data-ttu-id="11947-110">若要存取這個視覺化檢視，只要按一下「串流分析」工作之 [設定] 刀鋒視窗中的 [診斷圖表] 按鈕即可。</span><span class="sxs-lookup"><span data-stu-id="11947-110">To access this visualizer, simply click on the “Diagnosis diagram” button in the “Settings” blade of the of the Stream Analytics job.</span></span>

![stream-analytics-troubleshoot-visualization-diagnosis-diagram](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-diagnosis-diagram1.png)

<span data-ttu-id="11947-112">每個輸入項和輸出項都會以色彩標示，以指出該元件目前的狀態，如以下所示。</span><span class="sxs-lookup"><span data-stu-id="11947-112">Every input and output is color coded to indicate the current state of that component, as shown below.</span></span>

![stream-analytics-troubleshoot-visualization-input-map](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-input-map.png)

<span data-ttu-id="11947-114">當使用者想要查看中繼查詢步驟以了解工作內的資料流模式時，視覺化工具可提供將查詢細分成組成步驟及流程順序的檢視。</span><span class="sxs-lookup"><span data-stu-id="11947-114">When the user wants to look at intermediate query steps to understand the data flow patterns inside a job, the visualization tool provides a view of the breakdown of the query into its component steps and the flow sequence.</span></span> <span data-ttu-id="11947-115">按一下每個查詢步驟，即會在查詢編輯窗格中顯示對應的區段，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="11947-115">Clicking on each query step will show the corresponding section in a query editing pane as illustrated.</span></span> 

![stream-analytics-troubleshoot-visualization-intermediate-steps](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-intermediate-steps.png)

## <a name="next-steps"></a><span data-ttu-id="11947-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="11947-117">Next steps</span></span>
* [<span data-ttu-id="11947-118">Azure Stream Analytics 介紹</span><span class="sxs-lookup"><span data-stu-id="11947-118">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="11947-119">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="11947-119">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="11947-120">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="11947-120">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="11947-121">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="11947-121">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="11947-122">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="11947-122">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

