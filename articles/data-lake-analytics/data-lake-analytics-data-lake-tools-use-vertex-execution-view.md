---
title: "aaaUse hello 頂點資料湖 Tools for Visual Studio 中的執行檢視 |Microsoft 文件"
description: "了解如何 toouse hello 頂點執行檢視 tooexam Data Lake Analytics 工作。"
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
ms.openlocfilehash: fb54d2af8a32aa27a54ff50a73c1b4903677a21e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-vertex-execution-view-in-data-lake-tools-for-visual-studio"></a><span data-ttu-id="e7624-103">在資料湖 Tools for Visual Studio 使用 hello 頂點執行檢視</span><span class="sxs-lookup"><span data-stu-id="e7624-103">Use hello Vertex Execution View in Data Lake Tools for Visual Studio</span></span>
<span data-ttu-id="e7624-104">了解如何 toouse hello 頂點執行檢視 tooexam Data Lake Analytics 工作。</span><span class="sxs-lookup"><span data-stu-id="e7624-104">Learn how toouse hello Vertex Execution View tooexam Data Lake Analytics jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e7624-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="e7624-105">Prerequisites</span></span>

<span data-ttu-id="e7624-106">您必須使用 Data Lake Tools for Visual Studio toodevelop U-SQL 指令碼的基本知識。</span><span class="sxs-lookup"><span data-stu-id="e7624-106">You need basic knowledge of using Data Lake Tools for Visual Studio toodevelop U-SQL script.</span></span>  <span data-ttu-id="e7624-107">請參閱[教學課程：使用適用於 Visual Studio 的 Data Lake 工具開發 U-SQL 指令碼](data-lake-analytics-data-lake-tools-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="e7624-107">See [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>

## <a name="open-hello-vertex-execution-view"></a><span data-ttu-id="e7624-108">開啟 hello 頂點執行檢視</span><span class="sxs-lookup"><span data-stu-id="e7624-108">Open hello Vertex Execution View</span></span>
<span data-ttu-id="e7624-109">在 Data Lake Tools for Visual Studio 中開啟 U-SQL 作業。</span><span class="sxs-lookup"><span data-stu-id="e7624-109">Open a U-SQL job in Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="e7624-110">按一下**頂點執行檢視**hello 左下角中。</span><span class="sxs-lookup"><span data-stu-id="e7624-110">Click **Vertex Execution View** in hello bottom left corner.</span></span> <span data-ttu-id="e7624-111">您可能會先提示的 tooload 設定檔，它可能需要一些時間，視您的網路連線。</span><span class="sxs-lookup"><span data-stu-id="e7624-111">You may be prompted tooload profiles first and it can take some time depending on your network connectivity.</span></span>

![Data Lake Analytics 工具頂點執行檢視](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-open-vertex-execution-view.png)

## <a name="understand-vertex-execution-view"></a><span data-ttu-id="e7624-113">了解頂點執行檢視</span><span class="sxs-lookup"><span data-stu-id="e7624-113">Understand Vertex Execution View</span></span>
<span data-ttu-id="e7624-114">hello 頂點執行檢視有三個部分：</span><span class="sxs-lookup"><span data-stu-id="e7624-114">hello Vertex Execution View has three parts:</span></span>

![Data Lake Analytics 工具頂點執行檢視](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view.png)

<span data-ttu-id="e7624-116">hello**頂點選取器**在 hello 左可讓您可以選取頂點功能 （例如前 10 個資料讀取，或選擇由階段）。</span><span class="sxs-lookup"><span data-stu-id="e7624-116">hello **Vertex selector** on hello left lets you select vertices by features (such as top 10 data read, or choose by stage).</span></span> <span data-ttu-id="e7624-117">其中一個 hello 最常用的篩選器為 toosee hello**關鍵路徑的頂點**。</span><span class="sxs-lookup"><span data-stu-id="e7624-117">One of hello most commonly-used filters is toosee hello **vertices on critical path**.</span></span> <span data-ttu-id="e7624-118">hello**徑**hello U SQL 作業的頂點的最長的鏈結。</span><span class="sxs-lookup"><span data-stu-id="e7624-118">hello **Critical path** is hello longest chain of vertices of a U-SQL job.</span></span> <span data-ttu-id="e7624-119">了解 hello 關鍵路徑可用於最佳化您的工作，藉由檢查哪些頂點採用 hello 最長時間。</span><span class="sxs-lookup"><span data-stu-id="e7624-119">Understanding hello critical path is useful for optimizing your jobs by checking which vertex takes hello longest time.</span></span>
  
![Data Lake Analytics 工具頂點執行檢視](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane2.png)

<span data-ttu-id="e7624-121">hello 正上方窗格會顯示 hello**執行中 狀態的所有 hello 頂點**。</span><span class="sxs-lookup"><span data-stu-id="e7624-121">hello top center pane shows hello **running status of all hello vertices**.</span></span>
  
![Data Lake Analytics 工具頂點執行檢視](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane3.png)

<span data-ttu-id="e7624-123">hello 底端中央窗格會顯示每個頂點的相關資訊：</span><span class="sxs-lookup"><span data-stu-id="e7624-123">hello bottom center pane shows information about each vertex:</span></span>
* <span data-ttu-id="e7624-124">處理序名稱： hello hello 頂點的執行個體名稱。</span><span class="sxs-lookup"><span data-stu-id="e7624-124">Process Name: hello name of hello vertex instance.</span></span> <span data-ttu-id="e7624-125">由 StageName|VertexName|VertexRunInstance 中的不同部分組成。</span><span class="sxs-lookup"><span data-stu-id="e7624-125">It is composed of different parts in StageName|VertexName|VertexRunInstance.</span></span> <span data-ttu-id="e7624-126">比方說，hello SV7_Split [62].v1 頂點代表 hello 第二個執行個體 （.v1，從 0 開始的索引） 的頂點數目 62 階段 SV7_Split 中。</span><span class="sxs-lookup"><span data-stu-id="e7624-126">For example, hello SV7_Split[62].v1 vertex stands for hello second running instance (.v1, index starting from 0) of Vertex number 62 in Stage SV7_Split.</span></span>
* <span data-ttu-id="e7624-127">總資料讀取/寫入： hello 資料為讀取/寫入此頂點。</span><span class="sxs-lookup"><span data-stu-id="e7624-127">Total Data Read/Written: hello data was read/written by this vertex.</span></span>
* <span data-ttu-id="e7624-128">狀態/結束： hello 最終狀態 hello 頂點結束時。</span><span class="sxs-lookup"><span data-stu-id="e7624-128">State/Exit Status: hello final status when hello vertex is ended.</span></span>
* <span data-ttu-id="e7624-129">Hello 頂點失敗時，結束碼/失敗類型： hello 時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="e7624-129">Exit Code/Failure Type: hello error when hello vertex failed.</span></span>
* <span data-ttu-id="e7624-130">建立的原因： 為何 hello 頂點已建立。</span><span class="sxs-lookup"><span data-stu-id="e7624-130">Creation Reason: Why hello vertex was created.</span></span>
* <span data-ttu-id="e7624-131">資源延遲處理/延遲/PN 佇列延遲： hello 的時間 hello 頂點 toowait 資源、 tooprocess 資料和 toostay hello 佇列中。</span><span class="sxs-lookup"><span data-stu-id="e7624-131">Resource Latency/Process Latency/PN Queue Latency: hello time taken for hello vertex toowait for resources, tooprocess data, and toostay in hello queue.</span></span>
* <span data-ttu-id="e7624-132">處理序/建立者 GUID: Hello 的目前執行頂點或其建立者的 GUID。</span><span class="sxs-lookup"><span data-stu-id="e7624-132">Process/Creator GUID: GUID for hello current running vertex or its creator.</span></span>
* <span data-ttu-id="e7624-133">版本： 執行頂點的 hello hello 第 N 個執行個體 （hello 系統可能會針對的排程頂點的新執行個體有許多原因，例如容錯移轉時，計算備援等。）</span><span class="sxs-lookup"><span data-stu-id="e7624-133">Version: hello N-th instance of hello running vertex (hello system might schedule new instances of a vertex for many reasons, for example failover, compute redundancy, etc.)</span></span>
* <span data-ttu-id="e7624-134">版本建立時間。</span><span class="sxs-lookup"><span data-stu-id="e7624-134">Version Created Time.</span></span>
* <span data-ttu-id="e7624-135">處理建立開始時間/處理序已排入佇列時間/處理序開始時間/處理序完成時間： hello 頂點處理序啟動建立; 時hello 頂點處理序啟動時執行 tooqueue;當 hello 特定頂點的程序會啟動。hello 特定頂點完成時。</span><span class="sxs-lookup"><span data-stu-id="e7624-135">Process Create Start Time/Process Queued Time/Process Start Time/Process Complete Time: when hello vertex process starts creation; when hello vertex process starts tooqueue; when hello certain vertex process starts; when hello certain vertex is completed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e7624-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e7624-136">Next steps</span></span>
* <span data-ttu-id="e7624-137">toolog 診斷資訊，請參閱[存取 Azure 資料湖分析診斷記錄檔](data-lake-analytics-diagnostic-logs.md)</span><span class="sxs-lookup"><span data-stu-id="e7624-137">toolog diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)</span></span>
* <span data-ttu-id="e7624-138">toosee 更複雜的查詢，請參閱[使用 Azure Data Lake Analytics 分析網站記錄檔](data-lake-analytics-analyze-weblogs.md)。</span><span class="sxs-lookup"><span data-stu-id="e7624-138">toosee a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="e7624-139">tooview 作業的詳細資訊，請參閱[使用作業瀏覽器和 Azure Data lake Analytics 工作的工作檢視](data-lake-analytics-data-lake-tools-view-jobs.md)</span><span class="sxs-lookup"><span data-stu-id="e7624-139">tooview job details, see [Use Job Browser and Job View for Azure Data lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md)</span></span>
