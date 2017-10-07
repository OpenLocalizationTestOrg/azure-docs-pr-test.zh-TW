---
<span data-ttu-id="2068c-101">標題： aaa"Azure Analysis Services 教學課程第 9 課： 建立階層 |Microsoft 文件"描述： 服務： analysis services documentationcenter: '作者： minewiskan 管理員： erikre 編輯器:' 標記: '</span><span class="sxs-lookup"><span data-stu-id="2068c-101">title: aaa"Azure Analysis Services tutorial lesson 9: Create hierarchies | Microsoft Docs" description: services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="2068c-102">ms.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get 啟動文章 ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="2068c-102">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-9-create-hierarchies"></a><span data-ttu-id="2068c-103">第 9 課：建立階層</span><span class="sxs-lookup"><span data-stu-id="2068c-103">Lesson 9: Create hierarchies</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="2068c-104">在這堂課中，您會建立階層。</span><span class="sxs-lookup"><span data-stu-id="2068c-104">In this lesson, you create hierarchies.</span></span> <span data-ttu-id="2068c-105">階層是依層級排列的資料行群組；例如，地理階層可能有國家/地區、州、縣和市的子層級。</span><span class="sxs-lookup"><span data-stu-id="2068c-105">Hierarchies are groups of columns arranged in levels; for example, a Geography hierarchy might have sublevels for Country, State, County, and City.</span></span> <span data-ttu-id="2068c-106">階層可以顯示不同於其他資料行，在報表用戶端應用程式欄位清單，讓用戶端更容易使用者 toonavigate 和包含在報表中。</span><span class="sxs-lookup"><span data-stu-id="2068c-106">Hierarchies can appear separate from other columns in a reporting client application field list, making them easier for client users toonavigate and include in a report.</span></span> <span data-ttu-id="2068c-107">詳細資訊，請參閱 toolearn[階層](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)</span><span class="sxs-lookup"><span data-stu-id="2068c-107">toolearn more, see [Hierarchies](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)</span></span>
  
<span data-ttu-id="2068c-108">toocreate 階層，使用中的 hello 模型設計師*圖表檢視*。</span><span class="sxs-lookup"><span data-stu-id="2068c-108">toocreate hierarchies, use hello model designer in *Diagram View*.</span></span> <span data-ttu-id="2068c-109">不支援在 [資料檢視] 中建立及管理階層。</span><span class="sxs-lookup"><span data-stu-id="2068c-109">Creating and managing hierarchies is not supported in Data View.</span></span>  
  
<span data-ttu-id="2068c-110">本課程的估計時間 toocomplete: **20 分鐘**</span><span class="sxs-lookup"><span data-stu-id="2068c-110">Estimated time toocomplete this lesson: **20 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="2068c-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="2068c-111">Prerequisites</span></span>  
<span data-ttu-id="2068c-112">本主題是表格式模型教學課程的一部分，請依序完成。</span><span class="sxs-lookup"><span data-stu-id="2068c-112">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="2068c-113">在執行之前 hello 工作在這一課，您應已完成上一課 hello:[第 8 課： 建立檢視方塊](../tutorials/aas-lesson-8-create-perspectives.md)。</span><span class="sxs-lookup"><span data-stu-id="2068c-113">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span></span>  
  
## <a name="create-hierarchies"></a><span data-ttu-id="2068c-114">建立階層</span><span class="sxs-lookup"><span data-stu-id="2068c-114">Create hierarchies</span></span>  
  
#### <a name="toocreate-a-category-hierarchy-in-hello-dimproduct-table"></a><span data-ttu-id="2068c-115">toocreate hello DimProduct 資料表內的類別目錄階層</span><span class="sxs-lookup"><span data-stu-id="2068c-115">toocreate a Category hierarchy in hello DimProduct table</span></span>  
  
1.  <span data-ttu-id="2068c-116">在 hello 模型設計工具 （圖表檢視），以滑鼠右鍵按一下 hello **DimProduct**資料表 >**建立階層**。</span><span class="sxs-lookup"><span data-stu-id="2068c-116">In hello model designer (diagram view), right-click hello **DimProduct** table > **Create Hierarchy**.</span></span> <span data-ttu-id="2068c-117">新的階層會出現在 hello hello 資料表視窗底部。</span><span class="sxs-lookup"><span data-stu-id="2068c-117">A new hierarchy appears at hello bottom of hello table window.</span></span> <span data-ttu-id="2068c-118">重新命名階層 hello**類別**。</span><span class="sxs-lookup"><span data-stu-id="2068c-118">Rename hello hierarchy **Category**.</span></span>  
  
2.  <span data-ttu-id="2068c-119">按一下並拖曳 hello **ProductCategoryName**新的資料行 toohello**類別**階層。</span><span class="sxs-lookup"><span data-stu-id="2068c-119">Click and drag hello **ProductCategoryName** column toohello new **Category** hierarchy.</span></span>  
  
3.  <span data-ttu-id="2068c-120">在 hello**類別**階層，以滑鼠右鍵按一下 hello **ProductCategoryName** > **重新命名**，然後輸入**類別**。</span><span class="sxs-lookup"><span data-stu-id="2068c-120">In hello **Category** hierarchy, right-click hello **ProductCategoryName** > **Rename**, and then type **Category**.</span></span>  
  
    > [!NOTE]  
    > <span data-ttu-id="2068c-121">重新命名階層中的資料行，無法重新命名 hello 資料表中的該資料行。</span><span class="sxs-lookup"><span data-stu-id="2068c-121">Renaming a column in a hierarchy does not rename that column in hello table.</span></span> <span data-ttu-id="2068c-122">在階層中的資料行是只 hello hello 資料表中的資料行表示法。</span><span class="sxs-lookup"><span data-stu-id="2068c-122">A column in a hierarchy is just a representation of hello column in hello table.</span></span>  
  
4.  <span data-ttu-id="2068c-123">按一下並拖曳 hello **ProductSubcategoryName**資料行 toohello**類別**階層。</span><span class="sxs-lookup"><span data-stu-id="2068c-123">Click and drag hello **ProductSubcategoryName** column toohello **Category** hierarchy.</span></span> <span data-ttu-id="2068c-124">將它重新命名為 **Subcategory**。</span><span class="sxs-lookup"><span data-stu-id="2068c-124">Rename it **Subcategory**.</span></span> 
  
5.  <span data-ttu-id="2068c-125">以滑鼠右鍵按一下 hello **ModelName**資料行 >**新增 toohierarchy**，然後選取**類別**。</span><span class="sxs-lookup"><span data-stu-id="2068c-125">Right-click hello **ModelName** column > **Add toohierarchy**, and then select **Category**.</span></span> <span data-ttu-id="2068c-126">將它重新命名為 **Model**。</span><span class="sxs-lookup"><span data-stu-id="2068c-126">Rename it **Model**.</span></span>

6.  <span data-ttu-id="2068c-127">最後，會加入**[englishproductname]** toohello 類別目錄階層。</span><span class="sxs-lookup"><span data-stu-id="2068c-127">Finally, add **EnglishProductName** toohello Category hierarchy.</span></span> <span data-ttu-id="2068c-128">將它重新命名 **Product**。</span><span class="sxs-lookup"><span data-stu-id="2068c-128">Rename it **Product**.</span></span>  

    ![aas-lesson9-category](../tutorials/media/aas-lesson9-category.png)
  
#### <a name="toocreate-hierarchies-in-hello-dimdate-table"></a><span data-ttu-id="2068c-130">toocreate hello DimDate 資料表中的階層</span><span class="sxs-lookup"><span data-stu-id="2068c-130">toocreate hierarchies in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="2068c-131">在 hello **DimDate**資料表中，建立名為階層**行事曆**。</span><span class="sxs-lookup"><span data-stu-id="2068c-131">In hello **DimDate** table, create a hierarchy named **Calendar**.</span></span>  
  
3.  <span data-ttu-id="2068c-132">加入下列資料行之 in-order hello:</span><span class="sxs-lookup"><span data-stu-id="2068c-132">Add hello following columns in-order:</span></span>

    *  <span data-ttu-id="2068c-133">CalendarYear</span><span class="sxs-lookup"><span data-stu-id="2068c-133">CalendarYear</span></span>
    *  <span data-ttu-id="2068c-134">CalendarSemester</span><span class="sxs-lookup"><span data-stu-id="2068c-134">CalendarSemester</span></span>
    *  <span data-ttu-id="2068c-135">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="2068c-135">CalendarQuarter</span></span>
    *  <span data-ttu-id="2068c-136">MonthCalendar</span><span class="sxs-lookup"><span data-stu-id="2068c-136">MonthCalendar</span></span>
    *  <span data-ttu-id="2068c-137">DayNumberOfMonth</span><span class="sxs-lookup"><span data-stu-id="2068c-137">DayNumberOfMonth</span></span>
    
4.  <span data-ttu-id="2068c-138">在 hello **DimDate**資料表中，建立**會計**階層。</span><span class="sxs-lookup"><span data-stu-id="2068c-138">In hello **DimDate** table, create a **Fiscal** hierarchy.</span></span> <span data-ttu-id="2068c-139">包括下列資料行之 in-order hello:</span><span class="sxs-lookup"><span data-stu-id="2068c-139">Include hello following columns in-order:</span></span>  
  
    *  <span data-ttu-id="2068c-140">FiscalYear</span><span class="sxs-lookup"><span data-stu-id="2068c-140">FiscalYear</span></span>
    *  <span data-ttu-id="2068c-141">FiscalSemester</span><span class="sxs-lookup"><span data-stu-id="2068c-141">FiscalSemester</span></span>
    *  <span data-ttu-id="2068c-142">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="2068c-142">FiscalQuarter</span></span>
    *  <span data-ttu-id="2068c-143">MonthCalendar</span><span class="sxs-lookup"><span data-stu-id="2068c-143">MonthCalendar</span></span>
    *  <span data-ttu-id="2068c-144">DayNumberOfMonth</span><span class="sxs-lookup"><span data-stu-id="2068c-144">DayNumberOfMonth</span></span>
  
5.  <span data-ttu-id="2068c-145">最後，在 hello **DimDate**資料表中，建立**ProductionCalendar**階層。</span><span class="sxs-lookup"><span data-stu-id="2068c-145">Finally, in hello **DimDate** table, create a **ProductionCalendar** hierarchy.</span></span> <span data-ttu-id="2068c-146">包括下列資料行之 in-order hello:</span><span class="sxs-lookup"><span data-stu-id="2068c-146">Include hello following columns in-order:</span></span>  
    *  <span data-ttu-id="2068c-147">CalendarYear</span><span class="sxs-lookup"><span data-stu-id="2068c-147">CalendarYear</span></span>
    *  <span data-ttu-id="2068c-148">WeekNumberOfYear</span><span class="sxs-lookup"><span data-stu-id="2068c-148">WeekNumberOfYear</span></span>
    *  <span data-ttu-id="2068c-149">DayNumberOfWeek</span><span class="sxs-lookup"><span data-stu-id="2068c-149">DayNumberOfWeek</span></span>
  
 ## <a name="whats-next"></a><span data-ttu-id="2068c-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2068c-150">What's next?</span></span>
<span data-ttu-id="2068c-151">[第 10 課：建立資料分割](../tutorials/aas-lesson-10-create-partitions.md)。</span><span class="sxs-lookup"><span data-stu-id="2068c-151">[Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span></span> 
  
  
