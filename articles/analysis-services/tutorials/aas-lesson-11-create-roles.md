---
title: "Azure Analysis Services 教學課程第 11 課：建立角色 | Microsoft Docs"
description: "說明如何在 Azure Analysis Services 教學課程專案中建立角色。"
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
ms.openlocfilehash: 085a36edd2a0e80123ac8754b438bceadfa6c0e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-11-create-roles"></a><span data-ttu-id="cfc64-103">第 11 課：建立角色</span><span class="sxs-lookup"><span data-stu-id="cfc64-103">Lesson 11: Create roles</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="cfc64-104">在這堂課中，您會建立角色。</span><span class="sxs-lookup"><span data-stu-id="cfc64-104">In this lesson, you create roles.</span></span> <span data-ttu-id="cfc64-105">角色可以限制只有身為角色成員的使用者才能存取，提供模型資料庫物件和資料的安全性。</span><span class="sxs-lookup"><span data-stu-id="cfc64-105">Roles provide model database object and data security by limiting access to only those users that are role members.</span></span> <span data-ttu-id="cfc64-106">每個角色都定義有單一權限︰「無」、「讀取」、「讀取和處理」、「處理」或「系統管理員」。</span><span class="sxs-lookup"><span data-stu-id="cfc64-106">Each role is defined with a single permission: None, Read, Read and Process, Process, or Administrator.</span></span> <span data-ttu-id="cfc64-107">在製作模型期間可以使用 [角色管理員] 來定義角色。</span><span class="sxs-lookup"><span data-stu-id="cfc64-107">Roles can be defined during model authoring by using Role Manager.</span></span> <span data-ttu-id="cfc64-108">在部署模型之後，您可以使用 SQL Server Management Studio (SSMS) 來管理角色。</span><span class="sxs-lookup"><span data-stu-id="cfc64-108">After a model has been deployed, you can manage roles by using SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="cfc64-109">若要深入了解，請參閱[角色](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular)。</span><span class="sxs-lookup"><span data-stu-id="cfc64-109">To learn more, see [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).</span></span>
  
> [!NOTE]  
> <span data-ttu-id="cfc64-110">完成本教學課程並不需要建立角色。</span><span class="sxs-lookup"><span data-stu-id="cfc64-110">Creating roles is not necessary to complete this tutorial.</span></span> <span data-ttu-id="cfc64-111">根據預設，您目前登入的帳戶具有模型的「系統管理員」權限。</span><span class="sxs-lookup"><span data-stu-id="cfc64-111">By default, the account you are currently logged in with has Administrator privileges on the model.</span></span> <span data-ttu-id="cfc64-112">不過，若要讓組織中的其他使用者利用報告用戶端瀏覽模型，您必須建立至少一個具有「讀取」權限的角色，並將這些使用者新增為成員。</span><span class="sxs-lookup"><span data-stu-id="cfc64-112">However, for other users in your organization to browse by using a reporting client, you must create at least one role with Read permissions and add those users as members.</span></span>  
  
<span data-ttu-id="cfc64-113">您可建立三個角色︰</span><span class="sxs-lookup"><span data-stu-id="cfc64-113">You create three roles:</span></span>  
  
-   <span data-ttu-id="cfc64-114">**銷售經理** – 此角色可包含組織中對所有模型物件和資料應該具有「讀取」權限的使用者。</span><span class="sxs-lookup"><span data-stu-id="cfc64-114">**Sales Manager** – This role can include users in your organization for which you want to have Read permission to all model objects and data.</span></span>  
  
-   <span data-ttu-id="cfc64-115">**美國銷售分析師** – 此角色可包含組織中只能夠瀏覽美國地區相關銷售資料的使用者。</span><span class="sxs-lookup"><span data-stu-id="cfc64-115">**Sales Analyst US** – This role can include users in your organization for which you want only to be able to browse data related to sales in the United States.</span></span> <span data-ttu-id="cfc64-116">對於此角色，您可使用 DAX 公式來定義「資料列篩選條件」，以限制成員只能瀏覽美國方面的資料。</span><span class="sxs-lookup"><span data-stu-id="cfc64-116">For this role, you use a DAX formula to define a *Row Filter*, which restricts members to browse data only for the United States.</span></span>  
  
-   <span data-ttu-id="cfc64-117">**系統管理員** – 此角色可包含應該擁有「系統管理員」權限的使用者，以授與無限制的存取和權限，而能夠在模型資料庫上執行管理工作。</span><span class="sxs-lookup"><span data-stu-id="cfc64-117">**Administrator** – This role can include users for which you want to have Administrator permission, which allows unlimited access and permissions to perform administrative tasks on the model database.</span></span>  
  
<span data-ttu-id="cfc64-118">因為組織中的 Windows 使用者和群組帳戶都是獨一無二，您可以將特定組織中的帳戶新增至成員。</span><span class="sxs-lookup"><span data-stu-id="cfc64-118">Because Windows user and group accounts in your organization are unique, you can add accounts from your particular organization to members.</span></span> <span data-ttu-id="cfc64-119">不過，在本教學課程中，您也可以將成員留白。</span><span class="sxs-lookup"><span data-stu-id="cfc64-119">However, for this tutorial, you can also leave the members blank.</span></span> <span data-ttu-id="cfc64-120">稍後在「第 12 課︰在 Excel 中進行分析」中，您會測試每個角色的效果。</span><span class="sxs-lookup"><span data-stu-id="cfc64-120">You test the effect of each role later in Lesson 12: Analyze in Excel.</span></span>  
  
<span data-ttu-id="cfc64-121">這堂課的預估完成時間：**15 分鐘**</span><span class="sxs-lookup"><span data-stu-id="cfc64-121">Estimated time to complete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="cfc64-122">必要條件</span><span class="sxs-lookup"><span data-stu-id="cfc64-122">Prerequisites</span></span>  
<span data-ttu-id="cfc64-123">本主題是表格式模型教學課程的一部分，請依序完成。</span><span class="sxs-lookup"><span data-stu-id="cfc64-123">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="cfc64-124">在這堂課中執行工作之前，您必須已完成上一堂課︰[第 10 課︰建立分割區](../tutorials/aas-lesson-10-create-partitions.md)。</span><span class="sxs-lookup"><span data-stu-id="cfc64-124">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span></span>  
  
## <a name="create-roles"></a><span data-ttu-id="cfc64-125">建立角色</span><span class="sxs-lookup"><span data-stu-id="cfc64-125">Create roles</span></span>  
  
#### <a name="to-create-a-sales-manager-user-role"></a><span data-ttu-id="cfc64-126">建立「銷售經理」使用者角色</span><span class="sxs-lookup"><span data-stu-id="cfc64-126">To create a Sales Manager user role</span></span>  
  
1.  <span data-ttu-id="cfc64-127">在 [表格式模型總管] 中，以滑鼠右鍵按一下 [角色] > [角色]。</span><span class="sxs-lookup"><span data-stu-id="cfc64-127">In Tabular Model Explorer, right-click **Roles** > **Roles**.</span></span>  
  
2.  <span data-ttu-id="cfc64-128">在 [角色管理員] 中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="cfc64-128">In Role Manager, click **New**.</span></span>  
  
3.  <span data-ttu-id="cfc64-129">按一下新角色，然後在 [名稱] 資料行中，將角色重新命名為**銷售經理**。</span><span class="sxs-lookup"><span data-stu-id="cfc64-129">Click the new role, and then in the **Name** column, rename the role to **Sales Manager**.</span></span>  
  
4.  <span data-ttu-id="cfc64-130">在 [權限] 資料行中，按一下下拉式清單，然後選取 [讀取] 權限。</span><span class="sxs-lookup"><span data-stu-id="cfc64-130">In the **Permissions** column, click the dropdown list, and then select the **Read** permission.</span></span> 

    ![aas 第 11 課新的角色](../tutorials/media/aas-lesson11-new-role.png) 
  
5.  <span data-ttu-id="cfc64-132">選擇性：按一下 [成員] 索引標籤，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="cfc64-132">Optional: Click the **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="cfc64-133">在 [選取使用者或群組] 對話方塊中，輸入您想從組織中加入此角色的 Windows 使用者或群組。</span><span class="sxs-lookup"><span data-stu-id="cfc64-133">In the **Select Users or Groups** dialog box, enter the Windows users or groups from your organization you want to include in the role.</span></span>  
  
#### <a name="to-create-a-sales-analyst-us-user-role"></a><span data-ttu-id="cfc64-134">建立「美國銷售分析師」使用者角色</span><span class="sxs-lookup"><span data-stu-id="cfc64-134">To create a Sales Analyst US user role</span></span>  
  
1.  <span data-ttu-id="cfc64-135">在 [角色管理員] 中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="cfc64-135">In Role Manager, click **New**.</span></span>    
  
2.  <span data-ttu-id="cfc64-136">將角色重新命名為**美國銷售分析師**。</span><span class="sxs-lookup"><span data-stu-id="cfc64-136">Rename the role to **Sales Analyst US**.</span></span>  
  
3.  <span data-ttu-id="cfc64-137">將 [讀取] 權限授與此角色。</span><span class="sxs-lookup"><span data-stu-id="cfc64-137">Give this role **Read** permission.</span></span>  
  
4.  <span data-ttu-id="cfc64-138">按一下 [資料列篩選條件] 索引標籤，然後只針對 **DimGeography** 資料表，在 [DAX 篩選] 資料行中輸入下列公式︰</span><span class="sxs-lookup"><span data-stu-id="cfc64-138">Click the Row Filters tab, and then for the **DimGeography** table only, in the DAX Filter column, type the following formula:</span></span>  
  
    ```Administrator
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    <span data-ttu-id="cfc64-139">「資料列篩選條件」公式必須解析成布林值 (TRUE/FALSE)。</span><span class="sxs-lookup"><span data-stu-id="cfc64-139">A Row Filter formula must resolve to a Boolean (TRUE/FALSE) value.</span></span> <span data-ttu-id="cfc64-140">在這個公式中，您指定只有 [國家區域碼] 值為 "US" 的資料列才能被使用者看到。</span><span class="sxs-lookup"><span data-stu-id="cfc64-140">With this formula, you are specifying that only rows with the Country Region Code value of “US” are visible to the user.</span></span>  
    ![aas 第 11 課角色篩選](../tutorials/media/aas-lesson11-role-filter.png) 
  
6.  <span data-ttu-id="cfc64-142">選擇性：按一下 [成員] 索引標籤，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="cfc64-142">Optional: Click the **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="cfc64-143">在 [選取使用者或群組] 對話方塊中，輸入您想從組織中加入此角色的 Windows 使用者或群組。</span><span class="sxs-lookup"><span data-stu-id="cfc64-143">In the **Select Users or Groups** dialog box, enter the Windows users or groups from your organization you want to include in the role.</span></span>  
  
#### <a name="to-create-an-administrator-user-role"></a><span data-ttu-id="cfc64-144">建立「系統管理員」使用者角色</span><span class="sxs-lookup"><span data-stu-id="cfc64-144">To create an Administrator user role</span></span>  
  
1.  <span data-ttu-id="cfc64-145">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="cfc64-145">Click **New**.</span></span>  
  
2.  <span data-ttu-id="cfc64-146">將角色重新命名為「系統管理員」。</span><span class="sxs-lookup"><span data-stu-id="cfc64-146">Rename the role to **Administrator**.</span></span>  
  
3.  <span data-ttu-id="cfc64-147">將 [系統管理員] 權限授與此角色。</span><span class="sxs-lookup"><span data-stu-id="cfc64-147">Give this role **Administrator** permission.</span></span>  
  
4.  <span data-ttu-id="cfc64-148">選擇性：按一下 [成員] 索引標籤，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="cfc64-148">Optional: Click the **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="cfc64-149">在 [選取使用者或群組] 對話方塊中，輸入您想從組織中加入此角色的 Windows 使用者或群組。</span><span class="sxs-lookup"><span data-stu-id="cfc64-149">In the **Select Users or Groups** dialog box, enter the Windows users or groups from your organization you want to include in the role.</span></span> 
  
  
## <a name="whats-next"></a><span data-ttu-id="cfc64-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cfc64-150">What's next?</span></span>
<span data-ttu-id="cfc64-151">[第 12 課：在 Excel 中進行分析](../tutorials/aas-lesson-12-analyze-in-excel.md)</span><span class="sxs-lookup"><span data-stu-id="cfc64-151">[Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span></span>

  
  
