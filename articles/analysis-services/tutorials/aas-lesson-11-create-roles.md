---
<span data-ttu-id="3ed25-101">標題： aaa"Azure Analysis Services 教學課程第 11 課： 建立角色 |Microsoft 文件"描述： 描述如何在 toocreate 角色 hello Azure Analysis Services 教學課程專案。</span><span class="sxs-lookup"><span data-stu-id="3ed25-101">title: aaa"Azure Analysis Services tutorial lesson 11: Create roles | Microsoft Docs" description: Describes how toocreate roles in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="3ed25-102">服務： analysis services documentationcenter: '作者： minewiskan 管理員： erikre 編輯器:' 標記: '</span><span class="sxs-lookup"><span data-stu-id="3ed25-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="3ed25-103">ms.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get 啟動文章 ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="3ed25-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-11-create-roles"></a><span data-ttu-id="3ed25-104">第 11 課：建立角色</span><span class="sxs-lookup"><span data-stu-id="3ed25-104">Lesson 11: Create roles</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="3ed25-105">在這堂課中，您會建立角色。</span><span class="sxs-lookup"><span data-stu-id="3ed25-105">In this lesson, you create roles.</span></span> <span data-ttu-id="3ed25-106">角色提供模型資料庫物件和資料安全性，方法是限制存取 tooonly 這些使用者角色的成員。</span><span class="sxs-lookup"><span data-stu-id="3ed25-106">Roles provide model database object and data security by limiting access tooonly those users that are role members.</span></span> <span data-ttu-id="3ed25-107">每個角色都定義有單一權限︰「無」、「讀取」、「讀取和處理」、「處理」或「系統管理員」。</span><span class="sxs-lookup"><span data-stu-id="3ed25-107">Each role is defined with a single permission: None, Read, Read and Process, Process, or Administrator.</span></span> <span data-ttu-id="3ed25-108">在製作模型期間可以使用 [角色管理員] 來定義角色。</span><span class="sxs-lookup"><span data-stu-id="3ed25-108">Roles can be defined during model authoring by using Role Manager.</span></span> <span data-ttu-id="3ed25-109">在部署模型之後，您可以使用 SQL Server Management Studio (SSMS) 來管理角色。</span><span class="sxs-lookup"><span data-stu-id="3ed25-109">After a model has been deployed, you can manage roles by using SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="3ed25-110">詳細資訊，請參閱 toolearn[角色](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular)。</span><span class="sxs-lookup"><span data-stu-id="3ed25-110">toolearn more, see [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).</span></span>
  
> [!NOTE]  
> <span data-ttu-id="3ed25-111">建立角色時，則不需要 toocomplete 本教學課程。</span><span class="sxs-lookup"><span data-stu-id="3ed25-111">Creating roles is not necessary toocomplete this tutorial.</span></span> <span data-ttu-id="3ed25-112">根據預設，您目前登入的 hello 帳戶具有 hello 模型系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="3ed25-112">By default, hello account you are currently logged in with has Administrator privileges on hello model.</span></span> <span data-ttu-id="3ed25-113">不過，在您的組織 toobrowse 使用報表用戶端中的其他使用者，您必須建立至少一個角色具有讀取權限，並將這些使用者新增為成員。</span><span class="sxs-lookup"><span data-stu-id="3ed25-113">However, for other users in your organization toobrowse by using a reporting client, you must create at least one role with Read permissions and add those users as members.</span></span>  
  
<span data-ttu-id="3ed25-114">您可建立三個角色︰</span><span class="sxs-lookup"><span data-stu-id="3ed25-114">You create three roles:</span></span>  
  
-   <span data-ttu-id="3ed25-115">**銷售經理**– 此角色可包含您要為其 toohave 讀取權限 tooall 模型物件和資料的組織中的使用者。</span><span class="sxs-lookup"><span data-stu-id="3ed25-115">**Sales Manager** – This role can include users in your organization for which you want toohave Read permission tooall model objects and data.</span></span>  
  
-   <span data-ttu-id="3ed25-116">**Sales Analyst US** – 此角色可包含您想 toobe 無法 toobrowse 資料的組織中的使用者相關 toosales hello 美國中的。</span><span class="sxs-lookup"><span data-stu-id="3ed25-116">**Sales Analyst US** – This role can include users in your organization for which you want only toobe able toobrowse data related toosales in hello United States.</span></span> <span data-ttu-id="3ed25-117">此角色中，您可以使用 DAX 公式的 toodefine*資料列篩選器*，以限制僅針對 hello 美國成員 toobrowse 資料。</span><span class="sxs-lookup"><span data-stu-id="3ed25-117">For this role, you use a DAX formula toodefine a *Row Filter*, which restricts members toobrowse data only for hello United States.</span></span>  
  
-   <span data-ttu-id="3ed25-118">**系統管理員**– 此角色可包含您想要的 toohave 系統管理員權限，這允許無限制的存取和權限 tooperform 系統管理工作 hello 模型資料庫上的使用者。</span><span class="sxs-lookup"><span data-stu-id="3ed25-118">**Administrator** – This role can include users for which you want toohave Administrator permission, which allows unlimited access and permissions tooperform administrative tasks on hello model database.</span></span>  
  
<span data-ttu-id="3ed25-119">因為您組織中的 Windows 使用者和群組帳戶是唯一的您可以從特定組織 toomembers 新增帳戶。</span><span class="sxs-lookup"><span data-stu-id="3ed25-119">Because Windows user and group accounts in your organization are unique, you can add accounts from your particular organization toomembers.</span></span> <span data-ttu-id="3ed25-120">不過，本教學課程，您可以也留 hello 成員。</span><span class="sxs-lookup"><span data-stu-id="3ed25-120">However, for this tutorial, you can also leave hello members blank.</span></span> <span data-ttu-id="3ed25-121">您稍後在第 12 課中測試的每個角色的 hello 效果： 在 Excel 中進行分析。</span><span class="sxs-lookup"><span data-stu-id="3ed25-121">You test hello effect of each role later in Lesson 12: Analyze in Excel.</span></span>  
  
<span data-ttu-id="3ed25-122">本課程的估計時間 toocomplete: **15 分鐘**</span><span class="sxs-lookup"><span data-stu-id="3ed25-122">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="3ed25-123">必要條件</span><span class="sxs-lookup"><span data-stu-id="3ed25-123">Prerequisites</span></span>  
<span data-ttu-id="3ed25-124">本主題是表格式模型教學課程的一部分，請依序完成。</span><span class="sxs-lookup"><span data-stu-id="3ed25-124">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="3ed25-125">在執行之前 hello 工作在這一課，您應已完成上一課 hello:[第 10 課： 建立資料分割](../tutorials/aas-lesson-10-create-partitions.md)。</span><span class="sxs-lookup"><span data-stu-id="3ed25-125">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span></span>  
  
## <a name="create-roles"></a><span data-ttu-id="3ed25-126">建立角色</span><span class="sxs-lookup"><span data-stu-id="3ed25-126">Create roles</span></span>  
  
#### <a name="toocreate-a-sales-manager-user-role"></a><span data-ttu-id="3ed25-127">toocreate Sales Manager 使用者角色</span><span class="sxs-lookup"><span data-stu-id="3ed25-127">toocreate a Sales Manager user role</span></span>  
  
1.  <span data-ttu-id="3ed25-128">在 [表格式模型總管] 中，以滑鼠右鍵按一下 [角色] > [角色]。</span><span class="sxs-lookup"><span data-stu-id="3ed25-128">In Tabular Model Explorer, right-click **Roles** > **Roles**.</span></span>  
  
2.  <span data-ttu-id="3ed25-129">在 [角色管理員] 中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="3ed25-129">In Role Manager, click **New**.</span></span>  
  
3.  <span data-ttu-id="3ed25-130">按一下 hello 新角色，然後在 hello**名稱**資料行，hello 角色重新命名過**銷售經理**。</span><span class="sxs-lookup"><span data-stu-id="3ed25-130">Click hello new role, and then in hello **Name** column, rename hello role too**Sales Manager**.</span></span>  
  
4.  <span data-ttu-id="3ed25-131">在 hello**權限**資料行中，按一下 hello 下拉式清單中，然後選取 hello**讀取**權限。</span><span class="sxs-lookup"><span data-stu-id="3ed25-131">In hello **Permissions** column, click hello dropdown list, and then select hello **Read** permission.</span></span> 

    ![aas 第 11 課新的角色](../tutorials/media/aas-lesson11-new-role.png) 
  
5.  <span data-ttu-id="3ed25-133">選擇性： 按一下 hello**成員**索引標籤，然後再按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="3ed25-133">Optional: Click hello **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="3ed25-134">在 hello**選取使用者或群組**對話方塊方塊中，輸入 hello Windows 使用者或群組從您的組織想要 tooinclude hello 角色中的。</span><span class="sxs-lookup"><span data-stu-id="3ed25-134">In hello **Select Users or Groups** dialog box, enter hello Windows users or groups from your organization you want tooinclude in hello role.</span></span>  
  
#### <a name="toocreate-a-sales-analyst-us-user-role"></a><span data-ttu-id="3ed25-135">toocreate Sales Analyst US 使用者角色</span><span class="sxs-lookup"><span data-stu-id="3ed25-135">toocreate a Sales Analyst US user role</span></span>  
  
1.  <span data-ttu-id="3ed25-136">在 [角色管理員] 中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="3ed25-136">In Role Manager, click **New**.</span></span>    
  
2.  <span data-ttu-id="3ed25-137">Hello 角色重新命名過**Sales Analyst US**。</span><span class="sxs-lookup"><span data-stu-id="3ed25-137">Rename hello role too**Sales Analyst US**.</span></span>  
  
3.  <span data-ttu-id="3ed25-138">將 [讀取] 權限授與此角色。</span><span class="sxs-lookup"><span data-stu-id="3ed25-138">Give this role **Read** permission.</span></span>  
  
4.  <span data-ttu-id="3ed25-139">按一下 hello 資料列篩選器 索引標籤，然後 hello **DimGeography**資料表僅 hello DAX 篩選資料行中，下列公式的型別 hello:</span><span class="sxs-lookup"><span data-stu-id="3ed25-139">Click hello Row Filters tab, and then for hello **DimGeography** table only, in hello DAX Filter column, type hello following formula:</span></span>  
  
    ```Administrator
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    <span data-ttu-id="3ed25-140">資料列篩選公式必須解析 tooa 布林 (TRUE/FALSE) 值。</span><span class="sxs-lookup"><span data-stu-id="3ed25-140">A Row Filter formula must resolve tooa Boolean (TRUE/FALSE) value.</span></span> <span data-ttu-id="3ed25-141">使用這個公式，就指定的資料列 hello Country Region Code 值為"US"可見的 toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="3ed25-141">With this formula, you are specifying that only rows with hello Country Region Code value of “US” are visible toohello user.</span></span>  
    ![aas 第 11 課角色篩選](../tutorials/media/aas-lesson11-role-filter.png) 
  
6.  <span data-ttu-id="3ed25-143">選擇性： 按一下 hello**成員**索引標籤，然後再按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="3ed25-143">Optional: Click hello **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="3ed25-144">在 hello**選取使用者或群組**對話方塊方塊中，輸入 hello Windows 使用者或群組從您的組織想要 tooinclude hello 角色中的。</span><span class="sxs-lookup"><span data-stu-id="3ed25-144">In hello **Select Users or Groups** dialog box, enter hello Windows users or groups from your organization you want tooinclude in hello role.</span></span>  
  
#### <a name="toocreate-an-administrator-user-role"></a><span data-ttu-id="3ed25-145">toocreate 系統管理員使用者角色</span><span class="sxs-lookup"><span data-stu-id="3ed25-145">toocreate an Administrator user role</span></span>  
  
1.  <span data-ttu-id="3ed25-146">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="3ed25-146">Click **New**.</span></span>  
  
2.  <span data-ttu-id="3ed25-147">Hello 角色重新命名過**管理員**。</span><span class="sxs-lookup"><span data-stu-id="3ed25-147">Rename hello role too**Administrator**.</span></span>  
  
3.  <span data-ttu-id="3ed25-148">將 [系統管理員] 權限授與此角色。</span><span class="sxs-lookup"><span data-stu-id="3ed25-148">Give this role **Administrator** permission.</span></span>  
  
4.  <span data-ttu-id="3ed25-149">選擇性： 按一下 hello**成員**索引標籤，然後再按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="3ed25-149">Optional: Click hello **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="3ed25-150">在 hello**選取使用者或群組**對話方塊方塊中，輸入 hello Windows 使用者或群組從您的組織想要 tooinclude hello 角色中的。</span><span class="sxs-lookup"><span data-stu-id="3ed25-150">In hello **Select Users or Groups** dialog box, enter hello Windows users or groups from your organization you want tooinclude in hello role.</span></span> 
  
  
## <a name="whats-next"></a><span data-ttu-id="3ed25-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3ed25-151">What's next?</span></span>
<span data-ttu-id="3ed25-152">[第 12 課：在 Excel 中進行分析](../tutorials/aas-lesson-12-analyze-in-excel.md)</span><span class="sxs-lookup"><span data-stu-id="3ed25-152">[Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span></span>

  
  
