---
<span data-ttu-id="598c6-101">標題： aaa"Azure Analysis Services 教學課程第 13 課： 部署 |Microsoft 文件"描述： 描述如何 toodeploy hello 教學課程專案 tooAzure Analysis Services。</span><span class="sxs-lookup"><span data-stu-id="598c6-101">title: aaa"Azure Analysis Services tutorial lesson 13: Deploy | Microsoft Docs" description:  Describes how toodeploy hello tutorial project tooAzure Analysis Services.</span></span>
<span data-ttu-id="598c6-102">服務： analysis services documentationcenter: '作者： minewiskan 管理員： erikre 編輯器:' 標記: '</span><span class="sxs-lookup"><span data-stu-id="598c6-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="598c6-103">ms.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get 啟動文章 ms.tgt_pltfrm: NA ms.workload: na ms.date: 07/17/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="598c6-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 07/17/2017 ms.author: owend</span></span>
---
# <a name="lesson-13-deploy"></a><span data-ttu-id="598c6-104">第 13 課：部署</span><span class="sxs-lookup"><span data-stu-id="598c6-104">Lesson 13: Deploy</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="598c6-105">在這一課，您可以設定部署屬性;指定 Azure Analysis Services 伺服器 toodeploy tooand hello 模型的名稱。</span><span class="sxs-lookup"><span data-stu-id="598c6-105">In this lesson, you configure deployment properties; specifying an Azure Analysis Services server toodeploy tooand a name for hello model.</span></span> <span data-ttu-id="598c6-106">然後，您可以部署在 hello 模型 toothat 執行個體。</span><span class="sxs-lookup"><span data-stu-id="598c6-106">You then deploy hello model toothat instance.</span></span> <span data-ttu-id="598c6-107">部署模型之後，使用者可以使用報表用戶端應用程式連線 tooit。</span><span class="sxs-lookup"><span data-stu-id="598c6-107">After your model is deployed, users can connect tooit by using a reporting client application.</span></span> <span data-ttu-id="598c6-108">詳細資訊，請參閱 toolearn[部署 tooAzure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy)。</span><span class="sxs-lookup"><span data-stu-id="598c6-108">toolearn more, see [Deploy tooAzure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).</span></span>  
  
<span data-ttu-id="598c6-109">本課程的估計時間 toocomplete: **5 分鐘**</span><span class="sxs-lookup"><span data-stu-id="598c6-109">Estimated time toocomplete this lesson: **5 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="598c6-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="598c6-110">Prerequisites</span></span>  
<span data-ttu-id="598c6-111">本主題是表格式模型教學課程的一部分，請依序完成。</span><span class="sxs-lookup"><span data-stu-id="598c6-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="598c6-112">在執行之前 hello 工作在這一課，您應已完成上一課 hello:[第 12 課： 在 Excel 中分析](../tutorials/aas-lesson-12-analyze-in-excel.md)。</span><span class="sxs-lookup"><span data-stu-id="598c6-112">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span></span>  

> [!IMPORTANT]  
> <span data-ttu-id="598c6-113">您必須擁有[系統管理員權限](../analysis-services-server-admins.md)在 hello 遠端 Analysis Services 伺服器之 in-order toodeploy tooit。</span><span class="sxs-lookup"><span data-stu-id="598c6-113">You must have [Administrator permissions](../analysis-services-server-admins.md) on hello remote Analysis Services server in-order toodeploy tooit.</span></span>  

> [!IMPORTANT]  
> <span data-ttu-id="598c6-114">如果您在內部部署 SQL Server 上安裝 hello AdventureWorksDW2014 範例資料庫，而且您要部署模型 tooan Azure Analysis Services 伺服器，[在內部部署資料閘道](../analysis-services-gateway.md)需要。</span><span class="sxs-lookup"><span data-stu-id="598c6-114">If you installed hello AdventureWorksDW2014 sample database on an on-premises SQL Server, and you're deploying your model tooan Azure Analysis Services server, an [On-premises data gateway](../analysis-services-gateway.md) is required.</span></span>
  
## <a name="deploy-hello-model"></a><span data-ttu-id="598c6-115">部署 hello 模型</span><span class="sxs-lookup"><span data-stu-id="598c6-115">Deploy hello model</span></span>  
  
#### <a name="tooconfigure-deployment-properties"></a><span data-ttu-id="598c6-116">tooconfigure 部署屬性</span><span class="sxs-lookup"><span data-stu-id="598c6-116">tooconfigure deployment properties</span></span>  

  
1.  <span data-ttu-id="598c6-117">在**方案總管 中**，以滑鼠右鍵按一下 hello **AW Internet Sales**專案，然後再按一下**屬性**。</span><span class="sxs-lookup"><span data-stu-id="598c6-117">In **Solution Explorer**, right-click hello **AW Internet Sales** project, and then click **Properties**.</span></span>  
  
2.  <span data-ttu-id="598c6-118">在 hello **AW Internet Sales 屬性頁**對話方塊的 **部署伺服器**，在 hello**伺服器**屬性，輸入 hello 完整伺服器。</span><span class="sxs-lookup"><span data-stu-id="598c6-118">In hello **AW Internet Sales Property Pages** dialog box, under **Deployment Server**, in hello **Server** property, enter hello full server.</span></span>  

    ![aas 第 13 課部署屬性](../tutorials/media/aas-lesson13-deploy-property.png)
  
3.  <span data-ttu-id="598c6-120">在 hello**資料庫**屬性中，輸入**Adventure Works Internet Sales**。</span><span class="sxs-lookup"><span data-stu-id="598c6-120">In hello **Database** property, type **Adventure Works Internet Sales**.</span></span>  
  
4.  <span data-ttu-id="598c6-121">在 hello**模型名稱**屬性中，輸入**Adventure Works Internet Sales Model**。</span><span class="sxs-lookup"><span data-stu-id="598c6-121">In hello **Model Name** property, type **Adventure Works Internet Sales Model**.</span></span>  
  
5.  <span data-ttu-id="598c6-122">驗證您的選取項目，然後按一下確定。</span><span class="sxs-lookup"><span data-stu-id="598c6-122">Verify your selections and then click **OK**.</span></span>  
  
#### <a name="toodeploy-hello-adventure-works-internet-sales"></a><span data-ttu-id="598c6-123">toodeploy hello Adventure Works Internet Sales</span><span class="sxs-lookup"><span data-stu-id="598c6-123">toodeploy hello Adventure Works Internet Sales</span></span>
  
1.  <span data-ttu-id="598c6-124">在**方案總管 中**，以滑鼠右鍵按一下 hello **AW Internet Sales**專案 >**建置**。</span><span class="sxs-lookup"><span data-stu-id="598c6-124">In **Solution Explorer**, right-click hello **AW Internet Sales** project > **Build**.</span></span>  

2.  <span data-ttu-id="598c6-125">以滑鼠右鍵按一下 hello **AW Internet Sales**專案 >**部署**。</span><span class="sxs-lookup"><span data-stu-id="598c6-125">Right-click hello **AW Internet Sales** project > **Deploy**.</span></span>

    <span data-ttu-id="598c6-126">當部署 tooAzure Analysis Services，您可能會提示的 tooenter 您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="598c6-126">When deploying tooAzure Analysis Services, you may be prompted tooenter your account.</span></span> <span data-ttu-id="598c6-127">請輸入您的組織帳戶和密碼，例如 nancy@adventureworks.com。此帳戶必須在系統管理員在 hello 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="598c6-127">Enter your organizational account and password, for example nancy@adventureworks.com. This account must be in Admins on hello server.</span></span>
  
    <span data-ttu-id="598c6-128">hello [部署] 對話方塊隨即出現，並顯示 hello hello 中繼資料的部署狀態和 hello 模型中每個資料表。</span><span class="sxs-lookup"><span data-stu-id="598c6-128">hello Deploy dialog box appears and displays hello deployment status of hello metadata and each table included in hello model.</span></span>  
    
    ![aas 第 13 課部署狀態](../tutorials/media/aas-lesson13-deploy-status.png)
  
3. <span data-ttu-id="598c6-130">當部署順利完成時，請繼續並按一下 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="598c6-130">When deployment successfully completes, go ahead and click **Close**.</span></span>  
  
## <a name="conclusion"></a><span data-ttu-id="598c6-131">結論</span><span class="sxs-lookup"><span data-stu-id="598c6-131">Conclusion</span></span>  
<span data-ttu-id="598c6-132">恭喜！</span><span class="sxs-lookup"><span data-stu-id="598c6-132">Congratulations!</span></span> <span data-ttu-id="598c6-133">您已完成製作和部署第一個 Analysis Services 表格式模型。</span><span class="sxs-lookup"><span data-stu-id="598c6-133">You're finished authoring and deploying your first Analysis Services Tabular model.</span></span> <span data-ttu-id="598c6-134">此教學課程已幫引導您完成建立表格式模型中的 hello 最常見工作。</span><span class="sxs-lookup"><span data-stu-id="598c6-134">This tutorial has helped guide you through completing hello most common tasks in creating a tabular model.</span></span> <span data-ttu-id="598c6-135">既然部署 Adventure Works Internet Sales 模型之後，您可以使用 SQL Server Management Studio toomanage hello 模型;建立處理程序的指令碼和備份計劃。</span><span class="sxs-lookup"><span data-stu-id="598c6-135">Now that your Adventure Works Internet Sales model is deployed, you can use SQL Server Management Studio toomanage hello model; create process scripts and a backup plan.</span></span> <span data-ttu-id="598c6-136">使用者現在也可以連線 toohello 模型使用報表用戶端應用程式，例如 Microsoft Excel 或 Power BI。</span><span class="sxs-lookup"><span data-stu-id="598c6-136">Users can also now connect toohello model using a reporting client application such as Microsoft Excel or Power BI.</span></span>  

![aas 第 13 課 ssms](../tutorials/media/aas-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a><span data-ttu-id="598c6-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="598c6-138">What's next?</span></span>
<span data-ttu-id="598c6-139">[使用 Power BI Desktop 進行連線](../analysis-services-connect-pbi.md) </span><span class="sxs-lookup"><span data-stu-id="598c6-139">[Connect with Power BI Desktop](../analysis-services-connect-pbi.md) </span></span>  
<span data-ttu-id="598c6-140">[補充課程 - 動態安全性](../tutorials/aas-supplemental-lesson-dynamic-security.md) </span><span class="sxs-lookup"><span data-stu-id="598c6-140">[Supplemental Lesson - Dynamic security](../tutorials/aas-supplemental-lesson-dynamic-security.md) </span></span>  
<span data-ttu-id="598c6-141">[補充課程 - 詳細資料列](../tutorials/aas-supplemental-lesson-detail-rows.md) </span><span class="sxs-lookup"><span data-stu-id="598c6-141">[Supplemental Lesson - Detail rows](../tutorials/aas-supplemental-lesson-detail-rows.md) </span></span>  
[<span data-ttu-id="598c6-142">補充課程 - 不完全階層</span><span class="sxs-lookup"><span data-stu-id="598c6-142">Supplemental Lesson - Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)   
