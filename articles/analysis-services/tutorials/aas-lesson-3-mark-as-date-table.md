---
title: "Azure Analysis Services 教學課程第 3 課：標記為日期資料表 | Microsoft Docs"
description: "說明如何在 Azure Analysis Services 教學課程專案中標記日期資料表。"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 06/01/2017
ms.author: owend
ms.openlocfilehash: c62f2726fef5219155a08b70c61162c914600d1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-3-mark-as-date-table"></a><span data-ttu-id="0a464-103">第 3 課：標記為日期資料表</span><span class="sxs-lookup"><span data-stu-id="0a464-103">Lesson 3: Mark as Date Table</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="0a464-104">在「第 2 課：取得資料」中，您已匯入名為 DimDate 的維度資料表。</span><span class="sxs-lookup"><span data-stu-id="0a464-104">In Lesson 2: Get data, you imported a dimension table named DimDate.</span></span> <span data-ttu-id="0a464-105">雖然此資料表在您的模型中名為 DimDate，但可以也稱為「日期資料表」，因為它包含日期和時間資料。</span><span class="sxs-lookup"><span data-stu-id="0a464-105">While in your model this table is named DimDate, it can also be known as a *Date table*, in that it contains date and time data.</span></span>  
  
<span data-ttu-id="0a464-106">每當您使用 DAX 時間智慧函式時 (像是稍後您建立量值時)，您必須指定一些屬性，其中包括「日期資料表」和該資料表中的唯一識別碼「日期資料行」。</span><span class="sxs-lookup"><span data-stu-id="0a464-106">Whenever you use DAX time-intelligence functions, like when you create measures later, you must specify properties which include a *Date table* and a unique identifier *Date column* in that table.</span></span>
  
<span data-ttu-id="0a464-107">在這堂課中，您會將 DimDate 資料表標記為「日期資料表」，並將 Date 資料行 (在 Date 資料表中) 標記為「日期資料行」 (唯一識別碼)。</span><span class="sxs-lookup"><span data-stu-id="0a464-107">In this lesson, you mark the DimDate table as the *Date table* and the Date column (in the Date table) as the *Date column* (unique identifier).</span></span>  

<span data-ttu-id="0a464-108">在標記日期資料表和日期資料行之前，最好稍微整理一下，讓您的模型更容易懂。</span><span class="sxs-lookup"><span data-stu-id="0a464-108">Before you mark the date table and date column, it's a good time to do a little housekeeping to make your model easier to understand.</span></span> <span data-ttu-id="0a464-109">請注意 DimDate 資料表中名為 **FullDateAlternateKey** 的資料行。</span><span class="sxs-lookup"><span data-stu-id="0a464-109">Notice in the DimDate table a column named **FullDateAlternateKey**.</span></span> <span data-ttu-id="0a464-110">對於資料表內含的每個日曆年度中的每一天，此資料行都包含一個資料列。</span><span class="sxs-lookup"><span data-stu-id="0a464-110">This column contains one row for every day in each calendar year included in the table.</span></span> <span data-ttu-id="0a464-111">您在量值公式和報告中常會用到此資料行。</span><span class="sxs-lookup"><span data-stu-id="0a464-111">You use this column a lot in measure formulas and in reports.</span></span> <span data-ttu-id="0a464-112">但是，FullDateAlternateKey 並不是此資料行的理想識別項。</span><span class="sxs-lookup"><span data-stu-id="0a464-112">But, FullDateAlternateKey isn't really a good identifier for this column.</span></span> <span data-ttu-id="0a464-113">您會將它重新命名為 **Date**，使其更容易識別和納入公式中。</span><span class="sxs-lookup"><span data-stu-id="0a464-113">You rename it to **Date**, making it easier to identify and include in formulas.</span></span> <span data-ttu-id="0a464-114">可能的話，最好重新命名物件，例如資料表和資料行，以更容易在 SSDT 和用戶端報告應用程式 (例如 Power BI 和 Excel) 中識別。</span><span class="sxs-lookup"><span data-stu-id="0a464-114">Whenever possible, it's a good idea to rename objects like tables and columns to make them easier to identify in SSDT and client reporting applications like Power BI and Excel.</span></span> 
  
<span data-ttu-id="0a464-115">這堂課的預估完成時間：**3 分鐘**</span><span class="sxs-lookup"><span data-stu-id="0a464-115">Estimated time to complete this lesson: **Three minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="0a464-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="0a464-116">Prerequisites</span></span>  
<span data-ttu-id="0a464-117">本主題是表格式模型教學課程的一部分，請依序完成。</span><span class="sxs-lookup"><span data-stu-id="0a464-117">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="0a464-118">在這堂課中執行工作之前，您必須已完成上一堂課︰[第 2 課︰取得資料](../tutorials/aas-lesson-2-get-data.md)。</span><span class="sxs-lookup"><span data-stu-id="0a464-118">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 2: Get data](../tutorials/aas-lesson-2-get-data.md).</span></span> 

### <a name="to-rename-the-fulldatealternatekey-column"></a><span data-ttu-id="0a464-119">重新命名 FullDateAlternateKey 資料行</span><span class="sxs-lookup"><span data-stu-id="0a464-119">To rename the FullDateAlternateKey column</span></span>

1.  <span data-ttu-id="0a464-120">在模型設計師中，按一下 [DimDate] 資料表。</span><span class="sxs-lookup"><span data-stu-id="0a464-120">In the model designer, click the **DimDate** table.</span></span>

2.  <span data-ttu-id="0a464-121">按兩下 [FullDateAlternateKey] 資料行的標頭，然後將它重新命名為 **Date**。</span><span class="sxs-lookup"><span data-stu-id="0a464-121">Double-click the header for the **FullDateAlternateKey** column, and then rename it to **Date**.</span></span>

  
### <a name="to-set-mark-as-date-table"></a><span data-ttu-id="0a464-122">設定標記為日期資料表</span><span class="sxs-lookup"><span data-stu-id="0a464-122">To set Mark as Date Table</span></span>  
  
1.  <span data-ttu-id="0a464-123">選取 [Date] 資料行，然後在 [屬性] 視窗的 [資料類型] 下方，確定已選取 [日期]。</span><span class="sxs-lookup"><span data-stu-id="0a464-123">Select the **Date** column, and then in the **Properties** window, under **Data Type**, make sure  **Date** is selected.</span></span>  
  
2.  <span data-ttu-id="0a464-124">依序按一下 [資料表] 功能表、[日期]和 [標記為日期資料表]。</span><span class="sxs-lookup"><span data-stu-id="0a464-124">Click the **Table** menu, then click **Date**, and then click **Mark as Date Table**.</span></span>  
  
3.  <span data-ttu-id="0a464-125">在 [標記為日期資料表] 對話方塊中，在 [日期] 清單方塊中選取 [Date] 資料行當作唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="0a464-125">In the **Mark as Date Table** dialog box, in the **Date** listbox, select the **Date** column as the unique identifier.</span></span> <span data-ttu-id="0a464-126">依預設通常會選取它。</span><span class="sxs-lookup"><span data-stu-id="0a464-126">It's usually selected by default.</span></span> <span data-ttu-id="0a464-127">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="0a464-127">Click **OK**.</span></span> 

    ![aas-lesson3-date-table](../tutorials/media/aas-lesson3-date-table.png)
  

## <a name="whats-next"></a><span data-ttu-id="0a464-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0a464-129">What's next?</span></span>
<span data-ttu-id="0a464-130">[第 4 課：建立關聯性](../tutorials/aas-lesson-4-create-relationships.md)。</span><span class="sxs-lookup"><span data-stu-id="0a464-130">[Lesson 4: Create relationships](../tutorials/aas-lesson-4-create-relationships.md).</span></span>
  
