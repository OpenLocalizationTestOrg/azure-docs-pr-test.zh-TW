---
<span data-ttu-id="226e8-101">標題： aaa"Azure Analysis Services 教學課程的補充課程： 不完全階層 |Microsoft 文件"描述： 描述如何 toofix 不完全階層 hello Azure Analysis Services 教學課程中。</span><span class="sxs-lookup"><span data-stu-id="226e8-101">title: aaa"Azure Analysis Services tutorial supplemental lesson: Ragged hierarchies | Microsoft Docs" description: Describes how toofix ragged hierarchies in hello Azure Analysis Services tutorial.</span></span>
<span data-ttu-id="226e8-102">服務： analysis services documentationcenter: '作者： minewiskan 管理員： erikre 編輯器:' 標記: '</span><span class="sxs-lookup"><span data-stu-id="226e8-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="226e8-103">ms.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get 啟動文章 ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="226e8-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="supplemental-lesson---ragged-hierarchies"></a><span data-ttu-id="226e8-104">補充課程 - 不完全階層</span><span class="sxs-lookup"><span data-stu-id="226e8-104">Supplemental lesson - Ragged hierarchies</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="226e8-105">在這堂補充課程中，您可解決對不同層級包含空白值 (成員) 的階層進行樞紐分析時的常見問題。</span><span class="sxs-lookup"><span data-stu-id="226e8-105">In this supplemental lesson, you resolve a common problem when pivoting on hierarchies that contain blank values (members) at different levels.</span></span> <span data-ttu-id="226e8-106">例如，組織中部門經理和非部門經理同時為高階經理的直屬主管。</span><span class="sxs-lookup"><span data-stu-id="226e8-106">For example, an organization where a high-level manager has both departmental managers and non-managers as direct reports.</span></span> <span data-ttu-id="226e8-107">或者，由國家/地區-區域-城市組成的地理階層，其中有些城市缺少上層的州或省，例如華盛頓特區、梵蒂岡。</span><span class="sxs-lookup"><span data-stu-id="226e8-107">Or, geographic hierarchies composed of Country-Region-City, where some cities lack a parent State or Province, such as Washington D.C., Vatican City.</span></span> <span data-ttu-id="226e8-108">當階層具有空白的成員時，它通常會向下延伸 toodifferent，或不完全的層級。</span><span class="sxs-lookup"><span data-stu-id="226e8-108">When a hierarchy has blank members, it often descends toodifferent, or ragged, levels.</span></span>

![aas-lesson-detail-ragged-hierarchies-table](../tutorials/media/aas-lesson-detail-ragged-hierarchies-table.png)

<span data-ttu-id="226e8-110">Hello 1400 相容性層級的表格式模型具有其他**隱藏成員**屬性階層。</span><span class="sxs-lookup"><span data-stu-id="226e8-110">Tabular models at hello 1400 compatibility level have an additional **Hide Members** property for hierarchies.</span></span> <span data-ttu-id="226e8-111">hello**預設**設定假設任何層級沒有空白的成員。</span><span class="sxs-lookup"><span data-stu-id="226e8-111">hello **Default** setting assumes there are no blank members at any level.</span></span> <span data-ttu-id="226e8-112">hello**隱藏空白成員**設定排除 hello 階層時加入的空白成員 tooa 樞紐分析表或報表。</span><span class="sxs-lookup"><span data-stu-id="226e8-112">hello **Hide blank members** setting excludes blank members from hello hierarchy when added tooa PivotTable or report.</span></span>  
  
<span data-ttu-id="226e8-113">本課程的估計時間 toocomplete: **20 分鐘**</span><span class="sxs-lookup"><span data-stu-id="226e8-113">Estimated time toocomplete this lesson: **20 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="226e8-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="226e8-114">Prerequisites</span></span>  
<span data-ttu-id="226e8-115">此補充課程主題是表格式模型教學課程的一部分。</span><span class="sxs-lookup"><span data-stu-id="226e8-115">This supplemental lesson topic is part of a tabular modeling tutorial.</span></span> <span data-ttu-id="226e8-116">在執行前 hello 工作這個補充課程，您應已完成所有先前的課程或已完成的 Adventure Works Internet Sales 範例模型專案。</span><span class="sxs-lookup"><span data-stu-id="226e8-116">Before performing hello tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span></span> 

<span data-ttu-id="226e8-117">如果您已建立 hello AW Internet Sales 專案 hello 教學課程的一部分，您的模型尚未包含任何資料或不完全階層。</span><span class="sxs-lookup"><span data-stu-id="226e8-117">If you've created hello AW Internet Sales project as part of hello tutorial, your model does not yet contain any data or hierarchies that are ragged.</span></span> <span data-ttu-id="226e8-118">toocomplete 這個補充課程中，您必須先 toocreate hello 藉由新增某些其他資料表的問題，請建立關聯性、 導出資料行、 量值和新的組織階層。</span><span class="sxs-lookup"><span data-stu-id="226e8-118">toocomplete this supplemental lesson, you first have toocreate hello problem by adding some additional tables, create relationships, calculated columns, a measure, and a new Organization hierarchy.</span></span> <span data-ttu-id="226e8-119">該部分大約需要 15 分鐘。</span><span class="sxs-lookup"><span data-stu-id="226e8-119">That part takes about 15 minutes.</span></span> <span data-ttu-id="226e8-120">然後，您可以取得 toosolve 在短短幾分鐘內。</span><span class="sxs-lookup"><span data-stu-id="226e8-120">Then, you get toosolve it in just a few minutes.</span></span>  

## <a name="add-tables-and-objects"></a><span data-ttu-id="226e8-121">新增資料表和物件</span><span class="sxs-lookup"><span data-stu-id="226e8-121">Add tables and objects</span></span>
  
### <a name="tooadd-new-tables-tooyour-model"></a><span data-ttu-id="226e8-122">tooadd 新資料表 tooyour 模型</span><span class="sxs-lookup"><span data-stu-id="226e8-122">tooadd new tables tooyour model</span></span>
  
1.  <span data-ttu-id="226e8-123">在 [表格式模型總管] 中，依序展開 [資料來源]，然後以滑鼠右鍵按一下您的連線 > [匯入新資料表]。</span><span class="sxs-lookup"><span data-stu-id="226e8-123">In Tabular Model Explorer, expand **Data Sources**, then right-click your connection > **Import New Tables**.</span></span>
  
2.  <span data-ttu-id="226e8-124">在 導覽器 中，選取 DimEmployee 和 FactResellerSales，然後按一下確定。</span><span class="sxs-lookup"><span data-stu-id="226e8-124">In Navigator, select **DimEmployee** and **FactResellerSales**, and then click **OK**.</span></span>

3.  <span data-ttu-id="226e8-125">在 [查詢編輯器] 中，按一下 [匯入]</span><span class="sxs-lookup"><span data-stu-id="226e8-125">In Query Editor, click **Import**</span></span>

4.  <span data-ttu-id="226e8-126">建立 hello 遵循[關聯性](../tutorials/aas-lesson-4-create-relationships.md):</span><span class="sxs-lookup"><span data-stu-id="226e8-126">Create hello following [relationships](../tutorials/aas-lesson-4-create-relationships.md):</span></span>

    | <span data-ttu-id="226e8-127">表 1</span><span class="sxs-lookup"><span data-stu-id="226e8-127">Table 1</span></span>           | <span data-ttu-id="226e8-128">資料欄</span><span class="sxs-lookup"><span data-stu-id="226e8-128">Column</span></span>       | <span data-ttu-id="226e8-129">篩選方向</span><span class="sxs-lookup"><span data-stu-id="226e8-129">Filter Direction</span></span>   | <span data-ttu-id="226e8-130">表 2</span><span class="sxs-lookup"><span data-stu-id="226e8-130">Table 2</span></span>     | <span data-ttu-id="226e8-131">資料欄</span><span class="sxs-lookup"><span data-stu-id="226e8-131">Column</span></span>      | <span data-ttu-id="226e8-132">作用中</span><span class="sxs-lookup"><span data-stu-id="226e8-132">Active</span></span> |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | <span data-ttu-id="226e8-133">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="226e8-133">FactResellerSales</span></span> | <span data-ttu-id="226e8-134">OrderDateKey</span><span class="sxs-lookup"><span data-stu-id="226e8-134">OrderDateKey</span></span> | <span data-ttu-id="226e8-135">預設值</span><span class="sxs-lookup"><span data-stu-id="226e8-135">Default</span></span>            | <span data-ttu-id="226e8-136">DimDate</span><span class="sxs-lookup"><span data-stu-id="226e8-136">DimDate</span></span>     | <span data-ttu-id="226e8-137">日期</span><span class="sxs-lookup"><span data-stu-id="226e8-137">Date</span></span>        | <span data-ttu-id="226e8-138">是</span><span class="sxs-lookup"><span data-stu-id="226e8-138">Yes</span></span>    |
    | <span data-ttu-id="226e8-139">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="226e8-139">FactResellerSales</span></span> | <span data-ttu-id="226e8-140">DueDate</span><span class="sxs-lookup"><span data-stu-id="226e8-140">DueDate</span></span>      | <span data-ttu-id="226e8-141">預設值</span><span class="sxs-lookup"><span data-stu-id="226e8-141">Default</span></span>            | <span data-ttu-id="226e8-142">DimDate</span><span class="sxs-lookup"><span data-stu-id="226e8-142">DimDate</span></span>     | <span data-ttu-id="226e8-143">日期</span><span class="sxs-lookup"><span data-stu-id="226e8-143">Date</span></span>        | <span data-ttu-id="226e8-144">否</span><span class="sxs-lookup"><span data-stu-id="226e8-144">No</span></span>     |
    | <span data-ttu-id="226e8-145">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="226e8-145">FactResellerSales</span></span> | <span data-ttu-id="226e8-146">ShipDateKey</span><span class="sxs-lookup"><span data-stu-id="226e8-146">ShipDateKey</span></span>  | <span data-ttu-id="226e8-147">預設值</span><span class="sxs-lookup"><span data-stu-id="226e8-147">Default</span></span>            | <span data-ttu-id="226e8-148">DimDate</span><span class="sxs-lookup"><span data-stu-id="226e8-148">DimDate</span></span>     | <span data-ttu-id="226e8-149">日期</span><span class="sxs-lookup"><span data-stu-id="226e8-149">Date</span></span>        | <span data-ttu-id="226e8-150">否</span><span class="sxs-lookup"><span data-stu-id="226e8-150">No</span></span>     |
    | <span data-ttu-id="226e8-151">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="226e8-151">FactResellerSales</span></span> | <span data-ttu-id="226e8-152">ProductKey</span><span class="sxs-lookup"><span data-stu-id="226e8-152">ProductKey</span></span>   | <span data-ttu-id="226e8-153">預設值</span><span class="sxs-lookup"><span data-stu-id="226e8-153">Default</span></span>            | <span data-ttu-id="226e8-154">DimProduct</span><span class="sxs-lookup"><span data-stu-id="226e8-154">DimProduct</span></span>  | <span data-ttu-id="226e8-155">ProductKey</span><span class="sxs-lookup"><span data-stu-id="226e8-155">ProductKey</span></span>  | <span data-ttu-id="226e8-156">是</span><span class="sxs-lookup"><span data-stu-id="226e8-156">Yes</span></span>    |
    | <span data-ttu-id="226e8-157">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="226e8-157">FactResellerSales</span></span> | <span data-ttu-id="226e8-158">EmployeeKey</span><span class="sxs-lookup"><span data-stu-id="226e8-158">EmployeeKey</span></span>  | <span data-ttu-id="226e8-159">tooBoth 資料表</span><span class="sxs-lookup"><span data-stu-id="226e8-159">tooBoth Tables</span></span> | <span data-ttu-id="226e8-160">DimEmployee</span><span class="sxs-lookup"><span data-stu-id="226e8-160">DimEmployee</span></span> | <span data-ttu-id="226e8-161">EmployeeKey</span><span class="sxs-lookup"><span data-stu-id="226e8-161">EmployeeKey</span></span> | <span data-ttu-id="226e8-162">是</span><span class="sxs-lookup"><span data-stu-id="226e8-162">Yes</span></span>    |

5. <span data-ttu-id="226e8-163">在 hello **DimEmployee**資料表中，建立 hello 遵循[導出資料行](../tutorials/aas-lesson-5-create-calculated-columns.md):</span><span class="sxs-lookup"><span data-stu-id="226e8-163">In hello **DimEmployee** table, create hello following [calculated columns](../tutorials/aas-lesson-5-create-calculated-columns.md):</span></span> 

    <span data-ttu-id="226e8-164">**路徑**</span><span class="sxs-lookup"><span data-stu-id="226e8-164">**Path**</span></span> 
    ```
    =PATH([EmployeeKey],[ParentEmployeeKey])
    ```

    <span data-ttu-id="226e8-165">**FullName**</span><span class="sxs-lookup"><span data-stu-id="226e8-165">**FullName**</span></span> 
    ```
    =[FirstName] & " " & [MiddleName] & " " & [LastName]
    ```

    <span data-ttu-id="226e8-166">**Level1**</span><span class="sxs-lookup"><span data-stu-id="226e8-166">**Level1**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,1)) 
    ```

    <span data-ttu-id="226e8-167">**Level2**</span><span class="sxs-lookup"><span data-stu-id="226e8-167">**Level2**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,2)) 
    ```

    <span data-ttu-id="226e8-168">**Level3**</span><span class="sxs-lookup"><span data-stu-id="226e8-168">**Level3**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,3)) 
    ```

    <span data-ttu-id="226e8-169">**Level4**</span><span class="sxs-lookup"><span data-stu-id="226e8-169">**Level4**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,4)) 
    ```

    <span data-ttu-id="226e8-170">**Level5**</span><span class="sxs-lookup"><span data-stu-id="226e8-170">**Level5**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,5)) 
    ```

6.  <span data-ttu-id="226e8-171">在 hello **DimEmployee**資料表中，建立[階層](../tutorials/aas-lesson-9-create-hierarchies.md)名為**組織**。</span><span class="sxs-lookup"><span data-stu-id="226e8-171">In hello **DimEmployee** table, create a [hierarchy](../tutorials/aas-lesson-9-create-hierarchies.md) named **Organization**.</span></span> <span data-ttu-id="226e8-172">新增資料行中的順序 hello: **Level1**， **Level2**， **Level3**， **Level4**， **Level5**。</span><span class="sxs-lookup"><span data-stu-id="226e8-172">Add hello following columns in-order: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.</span></span>

7.  <span data-ttu-id="226e8-173">在 hello **FactResellerSales**資料表中，建立 hello 遵循[量值](../tutorials/aas-lesson-6-create-measures.md):</span><span class="sxs-lookup"><span data-stu-id="226e8-173">In hello **FactResellerSales** table, create hello following [measure](../tutorials/aas-lesson-6-create-measures.md):</span></span>

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  <span data-ttu-id="226e8-174">使用[在 Excel 中的進行分析](../tutorials/aas-lesson-12-analyze-in-excel.md)tooopen Excel，並自動建立樞紐分析表。</span><span class="sxs-lookup"><span data-stu-id="226e8-174">Use [Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md) tooopen Excel and automatically create a PivotTable.</span></span>

9.  <span data-ttu-id="226e8-175">在**樞紐分析表欄位**，新增 hello**組織**hello 階層**DimEmployee**太資料表**列**，和 hello **ResellerTotalSales**量值從 hello **FactResellerSales**太資料表**值**。</span><span class="sxs-lookup"><span data-stu-id="226e8-175">In **PivotTable Fields**, add hello **Organization** hierarchy from hello **DimEmployee** table too**Rows**, and hello **ResellerTotalSales** measure from hello **FactResellerSales**  table too**Values**.</span></span>

    ![aas-lesson-detail-ragged-hierarchies-pivottable](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable.png)

    <span data-ttu-id="226e8-177">您可以看到 hello 樞紐分析表中，是不完全的資料列顯示 hello 階層。</span><span class="sxs-lookup"><span data-stu-id="226e8-177">As you can see in hello PivotTable, hello hierarchy displays rows that are ragged.</span></span> <span data-ttu-id="226e8-178">有許多資料列中顯示空白的成員。</span><span class="sxs-lookup"><span data-stu-id="226e8-178">There are many rows where blank members are shown.</span></span>

## <a name="toofix-hello-ragged-hierarchy-by-setting-hello-hide-members-property"></a><span data-ttu-id="226e8-179">toofix hello 藉由設定 hello 隱藏成員屬性不完全階層</span><span class="sxs-lookup"><span data-stu-id="226e8-179">toofix hello ragged hierarchy by setting hello Hide members property</span></span>

1.  <span data-ttu-id="226e8-180">在 [表格式模型總管] 中，依序展開 [資料表] > [DimEmployee] > [階層] > [組織]。</span><span class="sxs-lookup"><span data-stu-id="226e8-180">In **Tabular Model Explorer**, expand **Tables** > **DimEmployee** > **Hierarchies** > **Organization**.</span></span>

2.  <span data-ttu-id="226e8-181">在 [屬性] > [隱藏成員] 中，選取 [隱藏空白成員]。</span><span class="sxs-lookup"><span data-stu-id="226e8-181">In **Properties** > **Hide Members**, select **Hide blank members**.</span></span> 

    ![aas-lesson-detail-ragged-hierarchies-hidemembers](../tutorials/media/aas-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  <span data-ttu-id="226e8-183">上一步是在 Excel 中重新整理 hello 樞紐分析表。</span><span class="sxs-lookup"><span data-stu-id="226e8-183">Back in Excel, refresh hello PivotTable.</span></span> 

    ![aas-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    <span data-ttu-id="226e8-185">現在看起來好多了！</span><span class="sxs-lookup"><span data-stu-id="226e8-185">Now that looks a whole lot better!</span></span>

## <a name="see-also"></a><span data-ttu-id="226e8-186">另請參閱</span><span class="sxs-lookup"><span data-stu-id="226e8-186">See Also</span></span>   
[<span data-ttu-id="226e8-187">第 9 課：建立階層</span><span class="sxs-lookup"><span data-stu-id="226e8-187">Lesson 9: Create hierarchies</span></span>](../tutorials/aas-lesson-9-create-hierarchies.md)  
[<span data-ttu-id="226e8-188">補充課程 - 動態安全性</span><span class="sxs-lookup"><span data-stu-id="226e8-188">Supplemental Lesson - Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[<span data-ttu-id="226e8-189">補充課程 - 詳細資料列</span><span class="sxs-lookup"><span data-stu-id="226e8-189">Supplemental Lesson - Detail rows</span></span>](../tutorials/aas-supplemental-lesson-detail-rows.md)  