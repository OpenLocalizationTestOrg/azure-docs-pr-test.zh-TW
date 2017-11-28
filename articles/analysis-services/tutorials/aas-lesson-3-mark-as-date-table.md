---
<span data-ttu-id="4c076-101">標題： aaa"Azure Analysis Services 教學課程第 3 課： 標記為日期資料表 |Microsoft 文件"描述： 描述如何 toomark 日期資料表 hello Azure Analysis Services 教學課程專案中。</span><span class="sxs-lookup"><span data-stu-id="4c076-101">title: aaa"Azure Analysis Services tutorial lesson 3: Mark as Date Table | Microsoft Docs" description: Describes how toomark a date table in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="4c076-102">服務： analysis services documentationcenter: '作者： minewiskan 管理員： erikre 編輯器:' 標記: '</span><span class="sxs-lookup"><span data-stu-id="4c076-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="4c076-103">ms.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get 啟動文章 ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="4c076-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span></span>
---
# <a name="lesson-3-mark-as-date-table"></a><span data-ttu-id="4c076-104">第 3 課：標記為日期資料表</span><span class="sxs-lookup"><span data-stu-id="4c076-104">Lesson 3: Mark as Date Table</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="4c076-105">在「第 2 課：取得資料」中，您已匯入名為 DimDate 的維度資料表。</span><span class="sxs-lookup"><span data-stu-id="4c076-105">In Lesson 2: Get data, you imported a dimension table named DimDate.</span></span> <span data-ttu-id="4c076-106">雖然此資料表在您的模型中名為 DimDate，但可以也稱為「日期資料表」，因為它包含日期和時間資料。</span><span class="sxs-lookup"><span data-stu-id="4c076-106">While in your model this table is named DimDate, it can also be known as a *Date table*, in that it contains date and time data.</span></span>  
  
<span data-ttu-id="4c076-107">每當您使用 DAX 時間智慧函式時 (像是稍後您建立量值時)，您必須指定一些屬性，其中包括「日期資料表」和該資料表中的唯一識別碼「日期資料行」。</span><span class="sxs-lookup"><span data-stu-id="4c076-107">Whenever you use DAX time-intelligence functions, like when you create measures later, you must specify properties which include a *Date table* and a unique identifier *Date column* in that table.</span></span>
  
<span data-ttu-id="4c076-108">在這一課，您將標示為 hello hello DimDate 資料表*日期資料表*和 hello 日期資料行 （在 hello Date 資料表） 做為 hello*日期資料行*（唯一識別碼）。</span><span class="sxs-lookup"><span data-stu-id="4c076-108">In this lesson, you mark hello DimDate table as hello *Date table* and hello Date column (in hello Date table) as hello *Date column* (unique identifier).</span></span>  

<span data-ttu-id="4c076-109">Hello 日期資料表和日期資料行標示之前，它會是您的模型更容易 toounderstand 有點例行性 toomake 恰好 toodo。</span><span class="sxs-lookup"><span data-stu-id="4c076-109">Before you mark hello date table and date column, it's a good time toodo a little housekeeping toomake your model easier toounderstand.</span></span> <span data-ttu-id="4c076-110">請注意，在 hello DimDate 資料表的資料行**FullDateAlternateKey**。</span><span class="sxs-lookup"><span data-stu-id="4c076-110">Notice in hello DimDate table a column named **FullDateAlternateKey**.</span></span> <span data-ttu-id="4c076-111">此資料行包含一個資料列包含 hello 資料表中每個日曆年度中每一天。</span><span class="sxs-lookup"><span data-stu-id="4c076-111">This column contains one row for every day in each calendar year included in hello table.</span></span> <span data-ttu-id="4c076-112">您在量值公式和報告中常會用到此資料行。</span><span class="sxs-lookup"><span data-stu-id="4c076-112">You use this column a lot in measure formulas and in reports.</span></span> <span data-ttu-id="4c076-113">但是，FullDateAlternateKey 並不是此資料行的理想識別項。</span><span class="sxs-lookup"><span data-stu-id="4c076-113">But, FullDateAlternateKey isn't really a good identifier for this column.</span></span> <span data-ttu-id="4c076-114">您將它重新命名過**日期**，讓它更容易 tooidentify，並在公式中包含。</span><span class="sxs-lookup"><span data-stu-id="4c076-114">You rename it too**Date**, making it easier tooidentify and include in formulas.</span></span> <span data-ttu-id="4c076-115">可能的話，它是個不錯的主意 toorename 物件如資料表和資料行 toomake 它們更容易 tooidentify SSDT 和用戶端報表應用程式，例如 Power BI 與 Excel 中的。</span><span class="sxs-lookup"><span data-stu-id="4c076-115">Whenever possible, it's a good idea toorename objects like tables and columns toomake them easier tooidentify in SSDT and client reporting applications like Power BI and Excel.</span></span> 
  
<span data-ttu-id="4c076-116">本課程的估計時間 toocomplete:**三分鐘**</span><span class="sxs-lookup"><span data-stu-id="4c076-116">Estimated time toocomplete this lesson: **Three minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="4c076-117">必要條件</span><span class="sxs-lookup"><span data-stu-id="4c076-117">Prerequisites</span></span>  
<span data-ttu-id="4c076-118">本主題是表格式模型教學課程的一部分，請依序完成。</span><span class="sxs-lookup"><span data-stu-id="4c076-118">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="4c076-119">在執行之前 hello 工作在這一課，您應已完成上一課 hello:[第 2 課： 取得資料](../tutorials/aas-lesson-2-get-data.md)。</span><span class="sxs-lookup"><span data-stu-id="4c076-119">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 2: Get data](../tutorials/aas-lesson-2-get-data.md).</span></span> 

### <a name="toorename-hello-fulldatealternatekey-column"></a><span data-ttu-id="4c076-120">toorename hello FullDateAlternateKey 資料行</span><span class="sxs-lookup"><span data-stu-id="4c076-120">toorename hello FullDateAlternateKey column</span></span>

1.  <span data-ttu-id="4c076-121">在 hello 模型設計師中，按一下 hello **DimDate**資料表。</span><span class="sxs-lookup"><span data-stu-id="4c076-121">In hello model designer, click hello **DimDate** table.</span></span>

2.  <span data-ttu-id="4c076-122">按兩下 hello hello 標頭**FullDateAlternateKey**資料行，然後重新命名過**日期**。</span><span class="sxs-lookup"><span data-stu-id="4c076-122">Double-click hello header for hello **FullDateAlternateKey** column, and then rename it too**Date**.</span></span>

  
### <a name="tooset-mark-as-date-table"></a><span data-ttu-id="4c076-123">tooset 標記為日期資料表</span><span class="sxs-lookup"><span data-stu-id="4c076-123">tooset Mark as Date Table</span></span>  
  
1.  <span data-ttu-id="4c076-124">選取 hello**日期**資料行，然後在 hello**屬性**視窗底下**資料型別**，請確定**日期**已選取。</span><span class="sxs-lookup"><span data-stu-id="4c076-124">Select hello **Date** column, and then in hello **Properties** window, under **Data Type**, make sure  **Date** is selected.</span></span>  
  
2.  <span data-ttu-id="4c076-125">按一下 hello**資料表**功能表，然後按一下**日期**，然後按一下**標記為日期資料表**。</span><span class="sxs-lookup"><span data-stu-id="4c076-125">Click hello **Table** menu, then click **Date**, and then click **Mark as Date Table**.</span></span>  
  
3.  <span data-ttu-id="4c076-126">在 hello**標記為日期資料表**對話方塊中的，在 hello**日期**清單方塊中，選取 hello**日期**hello 唯一識別碼資料行。</span><span class="sxs-lookup"><span data-stu-id="4c076-126">In hello **Mark as Date Table** dialog box, in hello **Date** listbox, select hello **Date** column as hello unique identifier.</span></span> <span data-ttu-id="4c076-127">依預設通常會選取它。</span><span class="sxs-lookup"><span data-stu-id="4c076-127">It's usually selected by default.</span></span> <span data-ttu-id="4c076-128">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="4c076-128">Click **OK**.</span></span> 

    ![aas-lesson3-date-table](../tutorials/media/aas-lesson3-date-table.png)
  

## <a name="whats-next"></a><span data-ttu-id="4c076-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4c076-130">What's next?</span></span>
<span data-ttu-id="4c076-131">[第 4 課：建立關聯性](../tutorials/aas-lesson-4-create-relationships.md)。</span><span class="sxs-lookup"><span data-stu-id="4c076-131">[Lesson 4: Create relationships](../tutorials/aas-lesson-4-create-relationships.md).</span></span>
  
