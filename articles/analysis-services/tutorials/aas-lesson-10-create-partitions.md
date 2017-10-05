---
title: "Azure Analysis Services 教學課程第 10 課：建立分割區 | Microsoft Docs"
description: "說明如何在 Azure Analysis Services 教學課程專案中建立分割區。"
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
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: df74d9cbdcf4916c24955e491767589e72389155
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-10-create-partitions"></a><span data-ttu-id="e8909-103">第 10 課：建立分割區</span><span class="sxs-lookup"><span data-stu-id="e8909-103">Lesson 10: Create partitions</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="e8909-104">在這堂課中，您會建立分割區，將 FactInternetSales 資料表分割成較小的邏輯部分，以獨立於其他分割區來處理 (重新整理)。</span><span class="sxs-lookup"><span data-stu-id="e8909-104">In this lesson, you create partitions to divide the FactInternetSales table into smaller logical parts that can be processed (refreshed) independent of other partitions.</span></span> <span data-ttu-id="e8909-105">根據預設，您在模型中包含的每個資料表會有一個分割區，其中包括資料表的所有資料行和資料列。</span><span class="sxs-lookup"><span data-stu-id="e8909-105">By default, every table you include in your model has one partition, which includes all the table’s columns and rows.</span></span> <span data-ttu-id="e8909-106">對於 FactInternetSales 資料表，我們準備依年份來分割資料，將資料表的五個年份各建立一個分割區。</span><span class="sxs-lookup"><span data-stu-id="e8909-106">For the FactInternetSales table, we want to divide the data by year; one partition for each of the table’s five years.</span></span> <span data-ttu-id="e8909-107">然後就可以獨立處理每個分割區。</span><span class="sxs-lookup"><span data-stu-id="e8909-107">Each partition can then be processed independently.</span></span> <span data-ttu-id="e8909-108">若要深入了解，請參閱[分割區](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular)。</span><span class="sxs-lookup"><span data-stu-id="e8909-108">To learn more, see [Partitions](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular).</span></span> 
  
<span data-ttu-id="e8909-109">這堂課的預估完成時間：**15 分鐘**</span><span class="sxs-lookup"><span data-stu-id="e8909-109">Estimated time to complete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="e8909-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="e8909-110">Prerequisites</span></span>  
<span data-ttu-id="e8909-111">本主題是表格式模型教學課程的一部分，請依序完成。</span><span class="sxs-lookup"><span data-stu-id="e8909-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="e8909-112">在這堂課中執行工作之前，您必須已完成上一堂課︰[第 9 課：建立階層](../tutorials/aas-lesson-9-create-hierarchies.md)。</span><span class="sxs-lookup"><span data-stu-id="e8909-112">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 9: Create Hierarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span></span>  
  
## <a name="create-partitions"></a><span data-ttu-id="e8909-113">建立分割區</span><span class="sxs-lookup"><span data-stu-id="e8909-113">Create partitions</span></span>  
  
#### <a name="to-create-partitions-in-the-factinternetsales-table"></a><span data-ttu-id="e8909-114">在 FactInternetSales 資料表中建立分割區</span><span class="sxs-lookup"><span data-stu-id="e8909-114">To create partitions in the FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="e8909-115">在 [表格式模型總管] 中，展開 [資料表]，然後以滑鼠右鍵按一下 [FactInternetSales] > [分割區]。</span><span class="sxs-lookup"><span data-stu-id="e8909-115">In Tabular Model Explorer, expand **Tables**, and then right-click **FactInternetSales** > **Partitions**.</span></span>  
  
2.  <span data-ttu-id="e8909-116">在 [分割區管理員] 中，按一下 [複製]，然後將名稱變更為 **FactInternetSales2010**。</span><span class="sxs-lookup"><span data-stu-id="e8909-116">In Partition Manager, click **Copy**, and then change the name to **FactInternetSales2010**.</span></span>
  
    <span data-ttu-id="e8909-117">因為您只希望分割區包含 2010 年某段期間的資料列，所以必須修改查詢運算式。</span><span class="sxs-lookup"><span data-stu-id="e8909-117">Because you want the partition to include only those rows within a certain period, for the year 2010, you must modify the query expression.</span></span>
  
4.  <span data-ttu-id="e8909-118">按一下 [設計] 以開啟查詢編輯器，然後按一下 [FactInternetSales2010] 查詢。</span><span class="sxs-lookup"><span data-stu-id="e8909-118">Click **Design** to open Query Editor, and then click the **FactInternetSales2010** query.</span></span>

5.  <span data-ttu-id="e8909-119">在預覽中，按一下 **OrderDate**資料行標題的向下箭號，然後按一下 [日期/時間篩選] > [介於]。</span><span class="sxs-lookup"><span data-stu-id="e8909-119">In preview, click the down arrow in the **OrderDate** column heading, and then click **Date/Time Filters** > **Between**.</span></span>

    ![aas 第 10 課查詢編輯器](../tutorials/media/aas-lesson10-query-editor.png)

6.  <span data-ttu-id="e8909-121">在 [篩選資料列] 對話方塊中，保留 [顯示符合條件的列: OrderDate] 中的 [之後或等於]，然後在日期欄位中輸入 **2010/1/1**。</span><span class="sxs-lookup"><span data-stu-id="e8909-121">In the Filter Rows dialog box, in **Show rows where: OrderDate**, leave **is after or equal to**, and then in the date field, enter **1/1/2010**.</span></span> <span data-ttu-id="e8909-122">保持選取 [且] 運算子，並選取 [之前]，在日期欄位中輸入 **2011/1/1**，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="e8909-122">Leave the **And** operator selected, then select **is before**, then in the date field, enter **1/1/2011**, and then click **OK**.</span></span>

    ![aas-lesson10-filter-rows](../tutorials/media/aas-lesson10-filter-rows.png)
    
    <span data-ttu-id="e8909-124">請注意，在查詢編輯器的 APPLIED STEPS 中，您會看到另一個名為 Filtered Rows 步驟。</span><span class="sxs-lookup"><span data-stu-id="e8909-124">Notice in Query Editor, in APPLIED STEPS, you see another step named Filtered Rows.</span></span> <span data-ttu-id="e8909-125">此篩選條件只會選取 2010 年中的訂單日期。</span><span class="sxs-lookup"><span data-stu-id="e8909-125">This filter is to select only order dates from 2010.</span></span>

8.  <span data-ttu-id="e8909-126">按一下 [匯入] 。</span><span class="sxs-lookup"><span data-stu-id="e8909-126">Click **Import**.</span></span>

    <span data-ttu-id="e8909-127">在 [分割區管理員] 中，您可以看到查詢運算式現在有額外的 Filtered Rows 子句。</span><span class="sxs-lookup"><span data-stu-id="e8909-127">In Partition Manager, notice the query expression now has an additional Filtered Rows clause.</span></span>

    ![aas 第 10 課查詢](../tutorials/media/aas-lesson10-query.png)
  
    <span data-ttu-id="e8909-129">此陳述式指定此分割區所包含的資料，僅限於 Filtered Rows 子句中指定 OrderDate 必須是 2010 日曆年度的那些資料列。</span><span class="sxs-lookup"><span data-stu-id="e8909-129">This statement specifies this partition should include only the data in those rows where the OrderDate is in the 2010 calendar year as specified in the filtered rows clause.</span></span>  
  
  
#### <a name="to-create-a-partition-for-the-2011-year"></a><span data-ttu-id="e8909-130">建立 2011 年的分割區</span><span class="sxs-lookup"><span data-stu-id="e8909-130">To create a partition for the 2011 year</span></span>  
  
1.  <span data-ttu-id="e8909-131">在分割區清單中，按一下您建立的 [FactInternetSales2010]分割區，然後按一下 [複製]。</span><span class="sxs-lookup"><span data-stu-id="e8909-131">In the partitions list, click the **FactInternetSales2010** partition you created, and then click **Copy**.</span></span>  <span data-ttu-id="e8909-132">將分割區名稱變更為 **FactInternetSales2011**。</span><span class="sxs-lookup"><span data-stu-id="e8909-132">Change the partition name to **FactInternetSales2011**.</span></span> 

    <span data-ttu-id="e8909-133">您不需要使用查詢編輯器來建立新的 Filtered Rows 子句。</span><span class="sxs-lookup"><span data-stu-id="e8909-133">You do not need to use Query Editor to create a new filtered rows clause.</span></span> <span data-ttu-id="e8909-134">因為是從 2010 年的查詢建立複本，2011 年的查詢只需要稍微變更即可。</span><span class="sxs-lookup"><span data-stu-id="e8909-134">Because you created a copy of the query for 2010, all you need to do is make a slight change in the query for 2011.</span></span>
  
2.  <span data-ttu-id="e8909-135">在 [查詢運算式] 中，為了讓此分割區只包含 2011 年的資料列，請將 Filtered Rows 子句中的年份各改為 **2011** 和 **2012**，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="e8909-135">In **Query Expression**, in-order for this partition to include only those rows for the 2011 year, replace the years in the Filtered Rows clause with **2011** and **2012**, respectively, like:</span></span>  
  
    ```  
    let
        Source = #"SQL/localhost;AdventureWorksDW2014",
        dbo_FactInternetSales = Source{[Schema="dbo",Item="FactInternetSales"]}[Data],
        #"Removed Columns" = Table.RemoveColumns(dbo_FactInternetSales,{"OrderDateKey", "DueDateKey", "ShipDateKey"}),
        #"Filtered Rows" = Table.SelectRows(#"Removed Columns", each [OrderDate] >= #datetime(2011, 1, 1, 0, 0, 0) and [OrderDate] < #datetime(2012, 1, 1, 0, 0, 0))
    in
        #"Filtered Rows"
   
    ```  
  
#### <a name="to-create-partitions-for-2012-2013-and-2014"></a><span data-ttu-id="e8909-136">建立 2012、2013 和 2014 年的分割區。</span><span class="sxs-lookup"><span data-stu-id="e8909-136">To create partitions for 2012, 2013, and 2014.</span></span>  
  
- <span data-ttu-id="e8909-137">請遵循先前的步驟，建立 2012、2013 和 2014 年的分割區，並變更 Filtered Rows 中的年份，以便只包含該年份的資料列。</span><span class="sxs-lookup"><span data-stu-id="e8909-137">Follow the previous steps, creating partitions for 2012, 2013, and 2014, changing the years in the Filtered Rows clause to include only rows for that year.</span></span> 
  

## <a name="delete-the-factinternetsales-partition"></a><span data-ttu-id="e8909-138">刪除 FactInternetSales 分割區</span><span class="sxs-lookup"><span data-stu-id="e8909-138">Delete the FactInternetSales partition</span></span>
<span data-ttu-id="e8909-139">現在每一年都有分割區，您可以刪除 FactInternetSales 分割區。處理分割區時，如果選擇 [處理全部]，請避免重疊。</span><span class="sxs-lookup"><span data-stu-id="e8909-139">Now that you have partitions for each year, you can delete the FactInternetSales partition; preventing overlap when choosing Process all when processing partitions.</span></span>

#### <a name="to-delete-the-factinternetsales-partition"></a><span data-ttu-id="e8909-140">刪除 FactInternetSales 分割區</span><span class="sxs-lookup"><span data-stu-id="e8909-140">To delete the FactInternetSales partition</span></span>
-  <span data-ttu-id="e8909-141">按一下 [FactInternetSales] 分割區，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="e8909-141">Click the FactInternetSales partition, and then click **Delete**.</span></span>



## <a name="process-partitions"></a><span data-ttu-id="e8909-142">處理分割區</span><span class="sxs-lookup"><span data-stu-id="e8909-142">Process partitions</span></span>  
<span data-ttu-id="e8909-143">在 [分割區管理員] 中，請注意，您建立的每個分割區的 [上次處理] 資料行會顯示尚未處理這些分割區。</span><span class="sxs-lookup"><span data-stu-id="e8909-143">In Partition Manager, notice the **Last Processed** column for each of the new partitions you created shows these partitions have never been processed.</span></span> <span data-ttu-id="e8909-144">建立分割區時，請執行 [處理分割區] 或 [處理資料表] 作業，以重新整理這些分割區中的資料。</span><span class="sxs-lookup"><span data-stu-id="e8909-144">When you create partitions, you should run a Process Partitions or Process Table operation to refresh the data in those partitions.</span></span>  
  
#### <a name="to-process-the-factinternetsales-partitions"></a><span data-ttu-id="e8909-145">處理 FactInternetSales 分割區</span><span class="sxs-lookup"><span data-stu-id="e8909-145">To process the FactInternetSales partitions</span></span>  
  
1.  <span data-ttu-id="e8909-146">按一下 [確定] 來關閉 [分割區管理員]。</span><span class="sxs-lookup"><span data-stu-id="e8909-146">Click **OK** to close Partition Manager.</span></span>  
  
2.  <span data-ttu-id="e8909-147">按一下 [FactInternetSales] 資料表，然後按一下 [模型] 功能表 > [處理] > [處理分割區]。</span><span class="sxs-lookup"><span data-stu-id="e8909-147">Click the **FactInternetSales** table, then click the **Model** menu > **Process** > **Process Partitions**.</span></span>  
  
3.  <span data-ttu-id="e8909-148">在 [處理分割區] 對話方塊中，確認 [模式] 設為 [處理預設]。</span><span class="sxs-lookup"><span data-stu-id="e8909-148">In the Process Partitions dialog box, verify **Mode** is set to **Process Default**.</span></span>  
  
4.  <span data-ttu-id="e8909-149">對於您建立的五個分割區，將 [處理]資料行的核取方塊全部選取，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="e8909-149">Select the checkbox in the **Process** column for each of the five partitions you created, and then click **OK**.</span></span>  

    ![aas 第 10 課處理分割區](../tutorials/media/aas-lesson10-process-partitions.png)
  
    <span data-ttu-id="e8909-151">如果系統提示您輸入模擬認證，請輸入您在第 2 課指定的 Windows 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="e8909-151">If you're prompted for Impersonation credentials, enter the Windows user name and password you specified in Lesson 2.</span></span>  
  
    <span data-ttu-id="e8909-152">[資料處理] 對話方塊隨即出現，顯示每個分割區的處理詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e8909-152">The **Data Processing** dialog box appears and displays process details for each partition.</span></span> <span data-ttu-id="e8909-153">請注意，傳送給每個分割區的資料列數目都不同。</span><span class="sxs-lookup"><span data-stu-id="e8909-153">Notice that a different number of rows for each partition are transferred.</span></span> <span data-ttu-id="e8909-154">每個分割區只會包含 SQL 陳述式的 WHERE 子句已指定之年份的資料列。</span><span class="sxs-lookup"><span data-stu-id="e8909-154">Each partition includes only those rows for the year specified in the WHERE clause in the SQL Statement.</span></span> <span data-ttu-id="e8909-155">處理完成時，請繼續並關閉 [資料處理] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="e8909-155">When processing is finished, go ahead and close the Data Processing dialog box.</span></span>  
  
    ![aas 第 10 課處理完成](../tutorials/media/aas-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a><span data-ttu-id="e8909-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e8909-157">What's next?</span></span>
<span data-ttu-id="e8909-158">移至下一個課程︰[第 11 課︰建立角色](../tutorials/aas-lesson-11-create-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="e8909-158">Go to the next lesson: [Lesson 11: Create Roles](../tutorials/aas-lesson-11-create-roles.md).</span></span> 
