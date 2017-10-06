---
<span data-ttu-id="78674-101">標題： aaa"Azure Analysis Services 教學課程第 12 課： 在 Excel 中分析 |Microsoft 文件"描述： 描述如何在 hello toouse 在 Excel 中進行分析 Azure Analysis Services 教學課程專案。</span><span class="sxs-lookup"><span data-stu-id="78674-101">title: aaa"Azure Analysis Services tutorial lesson 12: Analyze in Excel | Microsoft Docs" description: Describes how toouse Analyze in Excel in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="78674-102">服務： analysis services documentationcenter: '作者： minewiskan 管理員： erikre 編輯器:' 標記: '</span><span class="sxs-lookup"><span data-stu-id="78674-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="78674-103">ms.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get 啟動文章 ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="78674-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-12-analyze-in-excel"></a><span data-ttu-id="78674-104">第 12 課：在 Excel 中進行分析</span><span class="sxs-lookup"><span data-stu-id="78674-104">Lesson 12: Analyze in Excel</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="78674-105">在這一課，您可以使用 Excel 功能 tooopen Microsoft Excel 中的 hello 分析、 自動建立連線 toohello 模型工作空間，並自動將樞紐分析表 toohello 工作表。</span><span class="sxs-lookup"><span data-stu-id="78674-105">In this lesson, you use hello Analyze in Excel feature tooopen Microsoft Excel, automatically create a connection toohello model workspace, and automatically add a PivotTable toohello worksheet.</span></span> <span data-ttu-id="78674-106">在 excel 中的 hello 分析的目的在於 tooprovide 模型的快速簡便方式 tootest hello 效率設計先前 toodeploying 模型。</span><span class="sxs-lookup"><span data-stu-id="78674-106">hello Analyze in Excel feature is meant tooprovide a quick and easy way tootest hello efficacy of your model design prior toodeploying your model.</span></span> <span data-ttu-id="78674-107">在這堂課中，您不會執行任何資料分析。</span><span class="sxs-lookup"><span data-stu-id="78674-107">You do not perform any data analysis in this lesson.</span></span> <span data-ttu-id="78674-108">hello 本課程的目的是 toofamiliarize，hello 模型所撰寫，與 hello 工具您可以使用 tootest 模型設計。</span><span class="sxs-lookup"><span data-stu-id="78674-108">hello purpose of this lesson is toofamiliarize you, hello model author, with hello tools you can use tootest your model design.</span></span>   
  
<span data-ttu-id="78674-109">這一課，Excel 必須安裝在 hello toocomplete 與 SSDT 相同的電腦。</span><span class="sxs-lookup"><span data-stu-id="78674-109">toocomplete this lesson, Excel must be installed on hello same computer as SSDT.</span></span>
  
<span data-ttu-id="78674-110">本課程的估計時間 toocomplete:**五分鐘**</span><span class="sxs-lookup"><span data-stu-id="78674-110">Estimated time toocomplete this lesson: **Five minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="78674-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="78674-111">Prerequisites</span></span>  
<span data-ttu-id="78674-112">本主題是表格式模型教學課程的一部分，請依序完成。</span><span class="sxs-lookup"><span data-stu-id="78674-112">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="78674-113">在執行之前 hello 工作在這一課，您應已完成上一課 hello:[第 11 課： 建立角色](../tutorials/aas-lesson-11-create-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="78674-113">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 11: Create roles](../tutorials/aas-lesson-11-create-roles.md).</span></span>  
  
## <a name="browse-using-hello-default-and-internet-sales-perspectives"></a><span data-ttu-id="78674-114">瀏覽使用 hello 預設和網際網路銷售檢視方塊</span><span class="sxs-lookup"><span data-stu-id="78674-114">Browse using hello Default and Internet Sales perspectives</span></span>  
<span data-ttu-id="78674-115">在這些首要工作中，您瀏覽您的模型使用這兩個 hello 預設檢視方塊，包含所有模型物件，並使用 hello 網際網路銷售檢視方塊您稍早。</span><span class="sxs-lookup"><span data-stu-id="78674-115">In these first tasks, you browse your model by using both hello default perspective, which includes all model objects, and also by using hello Internet Sales perspective you earlier.</span></span> <span data-ttu-id="78674-116">hello 網際網路銷售檢視方塊排除 hello Customer 資料表物件。</span><span class="sxs-lookup"><span data-stu-id="78674-116">hello Internet Sales perspective excludes hello Customer table object.</span></span>  
  
#### <a name="toobrowse-by-using-hello-default-perspective"></a><span data-ttu-id="78674-117">toobrowse 使用 hello 預設檢視方塊</span><span class="sxs-lookup"><span data-stu-id="78674-117">toobrowse by using hello Default perspective</span></span>  
  
1.  <span data-ttu-id="78674-118">按一下 hello**模型**功能表 >**在 Excel 中的進行分析**。</span><span class="sxs-lookup"><span data-stu-id="78674-118">Click hello **Model** menu > **Analyze in Excel**.</span></span>  
  
2.  <span data-ttu-id="78674-119">在 hello**在 Excel 中的進行分析**對話方塊中，按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="78674-119">In hello **Analyze in Excel** dialog box, click **OK**.</span></span>  
  
    <span data-ttu-id="78674-120">Excel 會開啟新的活頁簿。</span><span class="sxs-lookup"><span data-stu-id="78674-120">Excel opens with a new workbook.</span></span> <span data-ttu-id="78674-121">會使用 hello 目前的使用者帳戶建立資料來源連接和 hello 預設檢視方塊是使用的 toodefine 可檢視的欄位。</span><span class="sxs-lookup"><span data-stu-id="78674-121">A data source connection is created using hello current user account and hello Default perspective is used toodefine viewable fields.</span></span> <span data-ttu-id="78674-122">樞紐分析表會自動加入 toohello 工作表。</span><span class="sxs-lookup"><span data-stu-id="78674-122">A PivotTable is automatically added toohello worksheet.</span></span>  
  
3.  <span data-ttu-id="78674-123">在 Excel 中，在 hello**樞紐分析表欄位清單**，請注意 hello **DimDate**和**FactInternetSales**量值群組會出現。</span><span class="sxs-lookup"><span data-stu-id="78674-123">In Excel, in hello **PivotTable Field List**, notice hello **DimDate** and **FactInternetSales** measure groups appear.</span></span> <span data-ttu-id="78674-124">hello **DimCustomer**， **DimDate**， **DimGeography**， **DimProduct**， **DimProductCategory**，**DimProductSubcategory**，和**FactInternetSales**具有其各自的資料行的資料表也會出現。</span><span class="sxs-lookup"><span data-stu-id="78674-124">hello **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, and **FactInternetSales** tables with their respective columns also appear.</span></span>  
  
4.  <span data-ttu-id="78674-125">關閉 Excel 而不儲存 hello 活頁簿。</span><span class="sxs-lookup"><span data-stu-id="78674-125">Close Excel without saving hello workbook.</span></span>  
  
#### <a name="toobrowse-by-using-hello-internet-sales-perspective"></a><span data-ttu-id="78674-126">toobrowse 使用 hello 網際網路銷售檢視方塊</span><span class="sxs-lookup"><span data-stu-id="78674-126">toobrowse by using hello Internet Sales perspective</span></span>  
  
1.  <span data-ttu-id="78674-127">按一下 hello**模型**功能表，然後再按一下**在 Excel 中的進行分析**。</span><span class="sxs-lookup"><span data-stu-id="78674-127">Click hello **Model** menu, and then click **Analyze in Excel**.</span></span>  
  
2.  <span data-ttu-id="78674-128">在 hello**在 Excel 中的進行分析**對話方塊中，保留**目前 Windows 使用者**選取，然後在 hello**觀點來看**下拉式清單方塊中，選取**網際網路銷售額**，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="78674-128">In hello **Analyze in Excel** dialog box, leave **Current Windows User** selected, then in hello **Perspective** drop-down listbox, select **Internet Sales**, and then click **OK**.</span></span> 
    
    ![aas 第 12 課檢視方塊](../tutorials/media/aas-lesson12-perspective.png)
    
3.  <span data-ttu-id="78674-130">在 Excel 中，在**樞紐分析表欄位**，請注意 hello DimCustomer 資料表排除 hello 欄位清單。</span><span class="sxs-lookup"><span data-stu-id="78674-130">In Excel, in **PivotTable Fields**, notice hello DimCustomer table is excluded from hello field list.</span></span>  
    
    ![aas 第 12 課欄位](../tutorials/media/aas-lesson12-fields.png)
    
4.  <span data-ttu-id="78674-132">關閉 Excel 而不儲存 hello 活頁簿。</span><span class="sxs-lookup"><span data-stu-id="78674-132">Close Excel without saving hello workbook.</span></span>  
  
## <a name="browse-by-using-roles"></a><span data-ttu-id="78674-133">使用角色來瀏覽</span><span class="sxs-lookup"><span data-stu-id="78674-133">Browse by using roles</span></span>  
<span data-ttu-id="78674-134">角色是任何表格式模型的重要部分。</span><span class="sxs-lookup"><span data-stu-id="78674-134">Roles are an important part of any tabular model.</span></span> <span data-ttu-id="78674-135">若沒有至少一個角色 toowhich 使用者會新增為成員，使用者無法存取並分析資料，使用您的模型。</span><span class="sxs-lookup"><span data-stu-id="78674-135">Without at least one role toowhich users are added as members, users cannot access and analyze data using your model.</span></span> <span data-ttu-id="78674-136">在 excel 中的 hello 分析方式為您提供定義 tootest hello 角色。</span><span class="sxs-lookup"><span data-stu-id="78674-136">hello Analyze in Excel feature provides a way for you tootest hello roles you have defined.</span></span>  
  
#### <a name="toobrowse-by-using-hello-sales-manager-user-role"></a><span data-ttu-id="78674-137">toobrowse 使用 hello Sales Manager 使用者角色</span><span class="sxs-lookup"><span data-stu-id="78674-137">toobrowse by using hello Sales Manager user role</span></span>  
  
1.  <span data-ttu-id="78674-138">在 SSDT 中，按一下 hello**模型**功能表，然後再按一下**在 Excel 中的進行分析**。</span><span class="sxs-lookup"><span data-stu-id="78674-138">In SSDT, click hello **Model** menu, and then click **Analyze in Excel**.</span></span>  
  
2.  <span data-ttu-id="78674-139">在**指定 hello 使用者名稱或角色 toouse tooconnect toohello 模型**，選取**角色**，然後在 hello 下拉式清單方塊中，選取**銷售經理**，然後按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="78674-139">In **Specify hello user name or role toouse tooconnect toohello model**, select **Role**, and then in hello drop-down listbox, select **Sales Manager**, and then click **OK**.</span></span>  
  
    <span data-ttu-id="78674-140">Excel 會開啟新的活頁簿。</span><span class="sxs-lookup"><span data-stu-id="78674-140">Excel opens with a new workbook.</span></span> <span data-ttu-id="78674-141">將會自動建立樞紐分析表。</span><span class="sxs-lookup"><span data-stu-id="78674-141">A PivotTable is automatically created.</span></span> <span data-ttu-id="78674-142">hello 樞紐分析表欄位清單包含所有 hello 可用資料欄位在新的模型。</span><span class="sxs-lookup"><span data-stu-id="78674-142">hello Pivot Table Field List includes all hello data fields available in your new model.</span></span>  
      
3.  <span data-ttu-id="78674-143">關閉 Excel 而不儲存 hello 活頁簿。</span><span class="sxs-lookup"><span data-stu-id="78674-143">Close Excel without saving hello workbook.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="78674-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="78674-144">What's next?</span></span>
<span data-ttu-id="78674-145">下一課中移 toohello: [13 課： 部署](../tutorials/aas-lesson-13-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="78674-145">Go toohello next lesson: [Lesson 13: Deploy](../tutorials/aas-lesson-13-deploy.md).</span></span>

  
  
  
