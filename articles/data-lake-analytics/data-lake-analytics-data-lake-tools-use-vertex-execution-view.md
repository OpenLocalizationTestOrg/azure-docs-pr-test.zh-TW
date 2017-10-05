---
title: "在 Data Lake Tools for Visual Studio 中使用頂點執行檢視 | Microsoft Docs"
description: "了解如何使用頂點執行檢視測驗 Data Lake Analytics 作業。"
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 5366d852-e7d6-44cf-a88c-e9f52f15f7df
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/13/2016
ms.author: jgao
ms.openlocfilehash: b788e7bc8ded86ebd49cc0be73e5b4e1bcbeaba3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-vertex-execution-view-in-data-lake-tools-for-visual-studio"></a><span data-ttu-id="994cd-103">在適用於 Visual Studio 的 Data Lake 工具中使用 Vertex 執行檢視</span><span class="sxs-lookup"><span data-stu-id="994cd-103">Use the Vertex Execution View in Data Lake Tools for Visual Studio</span></span>
<span data-ttu-id="994cd-104">了解如何使用頂點執行檢視測驗 Data Lake Analytics 作業。</span><span class="sxs-lookup"><span data-stu-id="994cd-104">Learn how to use the Vertex Execution View to exam Data Lake Analytics jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="994cd-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="994cd-105">Prerequisites</span></span>

<span data-ttu-id="994cd-106">您需要有使用 Data Lake Tools for Visual Studio 的基本知識，才能開發 U-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="994cd-106">You need basic knowledge of using Data Lake Tools for Visual Studio to develop U-SQL script.</span></span>  <span data-ttu-id="994cd-107">請參閱[教學課程：使用適用於 Visual Studio 的 Data Lake 工具開發 U-SQL 指令碼](data-lake-analytics-data-lake-tools-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="994cd-107">See [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>

## <a name="open-the-vertex-execution-view"></a><span data-ttu-id="994cd-108">開啟頂點執行檢視</span><span class="sxs-lookup"><span data-stu-id="994cd-108">Open the Vertex Execution View</span></span>
<span data-ttu-id="994cd-109">在 Data Lake Tools for Visual Studio 中開啟 U-SQL 作業。</span><span class="sxs-lookup"><span data-stu-id="994cd-109">Open a U-SQL job in Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="994cd-110">按一下左下角的 [頂點執行檢視]。</span><span class="sxs-lookup"><span data-stu-id="994cd-110">Click **Vertex Execution View** in the bottom left corner.</span></span> <span data-ttu-id="994cd-111">系統可能會提示您先載入設定檔，這可能需要一些時間，視您的網路連線而定。</span><span class="sxs-lookup"><span data-stu-id="994cd-111">You may be prompted to load profiles first and it can take some time depending on your network connectivity.</span></span>

![Data Lake Analytics 工具頂點執行檢視](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-open-vertex-execution-view.png)

## <a name="understand-vertex-execution-view"></a><span data-ttu-id="994cd-113">了解頂點執行檢視</span><span class="sxs-lookup"><span data-stu-id="994cd-113">Understand Vertex Execution View</span></span>
<span data-ttu-id="994cd-114">[頂點執行檢視] 有三個部分：</span><span class="sxs-lookup"><span data-stu-id="994cd-114">The Vertex Execution View has three parts:</span></span>

![Data Lake Analytics 工具頂點執行檢視](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view.png)

<span data-ttu-id="994cd-116">左邊的**頂點選取器**可讓您根據功能選取頂點 (例如前 10 個讀取的資料，或根據階段選擇)。</span><span class="sxs-lookup"><span data-stu-id="994cd-116">The **Vertex selector** on the left lets you select vertices by features (such as top 10 data read, or choose by stage).</span></span> <span data-ttu-id="994cd-117">其中一個最常使用的篩選條件是查看**關鍵路徑的頂點**。</span><span class="sxs-lookup"><span data-stu-id="994cd-117">One of the most commonly-used filters is to see the **vertices on critical path**.</span></span> <span data-ttu-id="994cd-118">**關鍵路徑** 是 U-SQL 作業頂點的最長鏈結。</span><span class="sxs-lookup"><span data-stu-id="994cd-118">The **Critical path** is the longest chain of vertices of a U-SQL job.</span></span> <span data-ttu-id="994cd-119">了解關鍵路徑有助於最佳化您的作業，方法是檢查哪一個頂點耗用最長時間。</span><span class="sxs-lookup"><span data-stu-id="994cd-119">Understanding the critical path is useful for optimizing your jobs by checking which vertex takes the longest time.</span></span>
  
![Data Lake Analytics 工具頂點執行檢視](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane2.png)

<span data-ttu-id="994cd-121">正上方的窗格顯示**所有頂點的執行狀態**。</span><span class="sxs-lookup"><span data-stu-id="994cd-121">The top center pane shows the **running status of all the vertices**.</span></span>
  
![Data Lake Analytics 工具頂點執行檢視](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane3.png)

<span data-ttu-id="994cd-123">正下方的窗格顯示每個頂點的相關資訊：</span><span class="sxs-lookup"><span data-stu-id="994cd-123">The bottom center pane shows information about each vertex:</span></span>
* <span data-ttu-id="994cd-124">處理序名稱︰頂點執行個體的名稱。</span><span class="sxs-lookup"><span data-stu-id="994cd-124">Process Name: The name of the vertex instance.</span></span> <span data-ttu-id="994cd-125">由 StageName|VertexName|VertexRunInstance 中的不同部分組成。</span><span class="sxs-lookup"><span data-stu-id="994cd-125">It is composed of different parts in StageName|VertexName|VertexRunInstance.</span></span> <span data-ttu-id="994cd-126">例如，SV7_Split[62].v1 頂點表示階段 SV7_Split 中第 62 號頂點的第二個執行中執行個體 (.v1，從 0 開始編制索引)。</span><span class="sxs-lookup"><span data-stu-id="994cd-126">For example, the SV7_Split[62].v1 vertex stands for the second running instance (.v1, index starting from 0) of Vertex number 62 in Stage SV7_Split.</span></span>
* <span data-ttu-id="994cd-127">總資料讀取/寫入︰此頂點讀取/寫入的資料。</span><span class="sxs-lookup"><span data-stu-id="994cd-127">Total Data Read/Written: The data was read/written by this vertex.</span></span>
* <span data-ttu-id="994cd-128">狀態/結束狀態︰頂點結束時的最終狀態。</span><span class="sxs-lookup"><span data-stu-id="994cd-128">State/Exit Status: The final status when the vertex is ended.</span></span>
* <span data-ttu-id="994cd-129">結束代碼/失敗類型︰頂點失敗時的錯誤。</span><span class="sxs-lookup"><span data-stu-id="994cd-129">Exit Code/Failure Type: The error when the vertex failed.</span></span>
* <span data-ttu-id="994cd-130">建立原因︰為什麼建立頂點。</span><span class="sxs-lookup"><span data-stu-id="994cd-130">Creation Reason: Why the vertex was created.</span></span>
* <span data-ttu-id="994cd-131">資源延遲/處理序延遲/PN 佇列延遲︰頂點等待資源、處理資料以及保持在佇列中所花費的時間。</span><span class="sxs-lookup"><span data-stu-id="994cd-131">Resource Latency/Process Latency/PN Queue Latency: the time taken for the vertex to wait for resources, to process data, and to stay in the queue.</span></span>
* <span data-ttu-id="994cd-132">處理序/建立者 GUID：目前執行的頂點或其建立者的 GUID。</span><span class="sxs-lookup"><span data-stu-id="994cd-132">Process/Creator GUID: GUID for the current running vertex or its creator.</span></span>
* <span data-ttu-id="994cd-133">版本︰執行中頂點的第 N 個執行個體 (系統可能會針對許多原因排程頂點的新執行個體，例如容錯移轉、計算備援等等。)</span><span class="sxs-lookup"><span data-stu-id="994cd-133">Version: the N-th instance of the running vertex (the system might schedule new instances of a vertex for many reasons, for example failover, compute redundancy, etc.)</span></span>
* <span data-ttu-id="994cd-134">版本建立時間。</span><span class="sxs-lookup"><span data-stu-id="994cd-134">Version Created Time.</span></span>
* <span data-ttu-id="994cd-135">處理序建立開始時間/處理序佇列時間/處理序開始時間/處理序完成時間：頂點處理序開始建立時；頂點處理序開始佇列時；特定頂點處理序開始時；特定頂點完成時。</span><span class="sxs-lookup"><span data-stu-id="994cd-135">Process Create Start Time/Process Queued Time/Process Start Time/Process Complete Time: when the vertex process starts creation; when the vertex process starts to queue; when the certain vertex process starts; when the certain vertex is completed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="994cd-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="994cd-136">Next steps</span></span>
* <span data-ttu-id="994cd-137">若要記錄診斷資訊，請參閱 [為 Azure Data Lake Analytics 存取診斷記錄檔](data-lake-analytics-diagnostic-logs.md)</span><span class="sxs-lookup"><span data-stu-id="994cd-137">To log diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)</span></span>
* <span data-ttu-id="994cd-138">若要了解更複雜的查詢，請參閱 [使用 Azure 資料湖分析來分析網站記錄檔](data-lake-analytics-analyze-weblogs.md)。</span><span class="sxs-lookup"><span data-stu-id="994cd-138">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="994cd-139">若要檢視作業詳細資料，請參閱[針對 Azure Data Lake Analytics 作業使用作業瀏覽器和作業檢視](data-lake-analytics-data-lake-tools-view-jobs.md)</span><span class="sxs-lookup"><span data-stu-id="994cd-139">To view job details, see [Use Job Browser and Job View for Azure Data lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md)</span></span>
