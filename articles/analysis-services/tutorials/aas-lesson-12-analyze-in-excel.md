---
title: "Azure Analysis Services 教學課程第 12 課：在 Excel 中進行分析 | Microsoft Docs"
description: "說明如何在 Azure Analysis Services 教學課程專案中使用「在 Excel 中進行分析」。"
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
ms.openlocfilehash: 6f47de43ff8d94de22f8b7c12fa0707a8d7ffbbc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-12-analyze-in-excel"></a><span data-ttu-id="e15ad-103">第 12 課：在 Excel 中進行分析</span><span class="sxs-lookup"><span data-stu-id="e15ad-103">Lesson 12: Analyze in Excel</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="e15ad-104">在這堂課中，您會使用「在 Excel 中進行分析」功能來開啟 Microsoft Excel、自動建立模型工作區的連線，以及自動將樞紐分析表新增至工作表。</span><span class="sxs-lookup"><span data-stu-id="e15ad-104">In this lesson, you use the Analyze in Excel feature to open Microsoft Excel, automatically create a connection to the model workspace, and automatically add a PivotTable to the worksheet.</span></span> <span data-ttu-id="e15ad-105">「在 Excel 中進行分析」功能是為了在部署模型之前，以快速又輕鬆的方式來測試模型設計的功效。</span><span class="sxs-lookup"><span data-stu-id="e15ad-105">The Analyze in Excel feature is meant to provide a quick and easy way to test the efficacy of your model design prior to deploying your model.</span></span> <span data-ttu-id="e15ad-106">在這堂課中，您不會執行任何資料分析。</span><span class="sxs-lookup"><span data-stu-id="e15ad-106">You do not perform any data analysis in this lesson.</span></span> <span data-ttu-id="e15ad-107">這堂課的目的是讓您 (模型作者) 熟悉可用來測試模型設計的工具。</span><span class="sxs-lookup"><span data-stu-id="e15ad-107">The purpose of this lesson is to familiarize you, the model author, with the tools you can use to test your model design.</span></span>   
  
<span data-ttu-id="e15ad-108">若要完成本這堂課，Excel 必須安裝在 SSDT 所在的同一台電腦。</span><span class="sxs-lookup"><span data-stu-id="e15ad-108">To complete this lesson, Excel must be installed on the same computer as SSDT.</span></span>
  
<span data-ttu-id="e15ad-109">這堂課的預估完成時間：**5 分鐘**</span><span class="sxs-lookup"><span data-stu-id="e15ad-109">Estimated time to complete this lesson: **Five minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="e15ad-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="e15ad-110">Prerequisites</span></span>  
<span data-ttu-id="e15ad-111">本主題是表格式模型教學課程的一部分，請依序完成。</span><span class="sxs-lookup"><span data-stu-id="e15ad-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="e15ad-112">在這堂課中執行工作之前，您必須已完成上一堂課︰[第 11 課︰建立角色](../tutorials/aas-lesson-11-create-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="e15ad-112">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 11: Create roles](../tutorials/aas-lesson-11-create-roles.md).</span></span>  
  
## <a name="browse-using-the-default-and-internet-sales-perspectives"></a><span data-ttu-id="e15ad-113">使用 [預設] 和 [網際網路銷售] 檢視方塊來瀏覽</span><span class="sxs-lookup"><span data-stu-id="e15ad-113">Browse using the Default and Internet Sales perspectives</span></span>  
<span data-ttu-id="e15ad-114">在這些首要工作中，您將會使用 [預設] 檢視方塊 (包含所有模型物件) 來瀏覽模型，也會使用您稍早建立的 [網際網路銷售] 檢視方塊來瀏覽模型。</span><span class="sxs-lookup"><span data-stu-id="e15ad-114">In these first tasks, you browse your model by using both the default perspective, which includes all model objects, and also by using the Internet Sales perspective you earlier.</span></span> <span data-ttu-id="e15ad-115">[網際網路銷售] 檢視方塊會排除 Customer 資料表物件。</span><span class="sxs-lookup"><span data-stu-id="e15ad-115">The Internet Sales perspective excludes the Customer table object.</span></span>  
  
#### <a name="to-browse-by-using-the-default-perspective"></a><span data-ttu-id="e15ad-116">使用 [預設] 檢視方塊來瀏覽</span><span class="sxs-lookup"><span data-stu-id="e15ad-116">To browse by using the Default perspective</span></span>  
  
1.  <span data-ttu-id="e15ad-117">按一下 [模型] 功能表 > [在 Excel 中的進行分析]。</span><span class="sxs-lookup"><span data-stu-id="e15ad-117">Click the **Model** menu > **Analyze in Excel**.</span></span>  
  
2.  <span data-ttu-id="e15ad-118">於 [在 Excel 中的進行分析] 對話方塊中，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="e15ad-118">In the **Analyze in Excel** dialog box, click **OK**.</span></span>  
  
    <span data-ttu-id="e15ad-119">Excel 會開啟新的活頁簿。</span><span class="sxs-lookup"><span data-stu-id="e15ad-119">Excel opens with a new workbook.</span></span> <span data-ttu-id="e15ad-120">將會使用目前的使用者帳戶建立資料來源連線，並使用 [預設] 檢視方塊來定義可檢視的欄位。</span><span class="sxs-lookup"><span data-stu-id="e15ad-120">A data source connection is created using the current user account and the Default perspective is used to define viewable fields.</span></span> <span data-ttu-id="e15ad-121">樞紐分析表會自動新增至工作表。</span><span class="sxs-lookup"><span data-stu-id="e15ad-121">A PivotTable is automatically added to the worksheet.</span></span>  
  
3.  <span data-ttu-id="e15ad-122">在 Excel 的 [樞紐分析表欄位清單] 中，注意 **DimDate** 和 **FactInternetSales** 量值群組會出現。</span><span class="sxs-lookup"><span data-stu-id="e15ad-122">In Excel, in the **PivotTable Field List**, notice the **DimDate** and **FactInternetSales** measure groups appear.</span></span> <span data-ttu-id="e15ad-123">**DimCustomer**、**DimDate**、**DimGeography**、**DimProduct**、**DimProductCategory**、**DimProductSubcategory** 和 **FactInternetSales** 資料表與其各自資料行也會出現。</span><span class="sxs-lookup"><span data-stu-id="e15ad-123">The **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, and **FactInternetSales** tables with their respective columns also appear.</span></span>  
  
4.  <span data-ttu-id="e15ad-124">關閉 Excel 而不儲存活頁簿。</span><span class="sxs-lookup"><span data-stu-id="e15ad-124">Close Excel without saving the workbook.</span></span>  
  
#### <a name="to-browse-by-using-the-internet-sales-perspective"></a><span data-ttu-id="e15ad-125">使用 [網際網路銷售] 檢視方塊來瀏覽</span><span class="sxs-lookup"><span data-stu-id="e15ad-125">To browse by using the Internet Sales perspective</span></span>  
  
1.  <span data-ttu-id="e15ad-126">按一下 [模型] 功能表，然後按一下 [使用 Excel 分析]。</span><span class="sxs-lookup"><span data-stu-id="e15ad-126">Click the **Model** menu, and then click **Analyze in Excel**.</span></span>  
  
2.  <span data-ttu-id="e15ad-127">於 [在 Excel 中進行分析] 對話方塊中，保持選取 [目前的 Windows 使用者]，接著在 [檢視方塊] 下拉式清單方塊中，選取 [網際網路銷售]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="e15ad-127">In the **Analyze in Excel** dialog box, leave **Current Windows User** selected, then in the **Perspective** drop-down listbox, select **Internet Sales**, and then click **OK**.</span></span> 
    
    ![aas 第 12 課檢視方塊](../tutorials/media/aas-lesson12-perspective.png)
    
3.  <span data-ttu-id="e15ad-129">在 Excel 的 [樞紐分析表欄位] 中，請注意 DimCustomer 資料表已從欄位清單中排除。</span><span class="sxs-lookup"><span data-stu-id="e15ad-129">In Excel, in **PivotTable Fields**, notice the DimCustomer table is excluded from the field list.</span></span>  
    
    ![aas 第 12 課欄位](../tutorials/media/aas-lesson12-fields.png)
    
4.  <span data-ttu-id="e15ad-131">關閉 Excel 而不儲存活頁簿。</span><span class="sxs-lookup"><span data-stu-id="e15ad-131">Close Excel without saving the workbook.</span></span>  
  
## <a name="browse-by-using-roles"></a><span data-ttu-id="e15ad-132">使用角色來瀏覽</span><span class="sxs-lookup"><span data-stu-id="e15ad-132">Browse by using roles</span></span>  
<span data-ttu-id="e15ad-133">角色是任何表格式模型的重要部分。</span><span class="sxs-lookup"><span data-stu-id="e15ad-133">Roles are an important part of any tabular model.</span></span> <span data-ttu-id="e15ad-134">沒有連一個可將使用者新增為成員的角色也沒有，使用者無法使用您的模型來存取和分析資料。</span><span class="sxs-lookup"><span data-stu-id="e15ad-134">Without at least one role to which users are added as members, users cannot access and analyze data using your model.</span></span> <span data-ttu-id="e15ad-135">「在 Excel 中進行分析」功能可讓您測試您已定義的角色。</span><span class="sxs-lookup"><span data-stu-id="e15ad-135">The Analyze in Excel feature provides a way for you to test the roles you have defined.</span></span>  
  
#### <a name="to-browse-by-using-the-sales-manager-user-role"></a><span data-ttu-id="e15ad-136">使用「銷售經理」使用者角色來瀏覽</span><span class="sxs-lookup"><span data-stu-id="e15ad-136">To browse by using the Sales Manager user role</span></span>  
  
1.  <span data-ttu-id="e15ad-137">在 SSDT 中，按一下 [模型] 功能表，然後按一下 [使用 Excel 分析]。</span><span class="sxs-lookup"><span data-stu-id="e15ad-137">In SSDT, click the **Model** menu, and then click **Analyze in Excel**.</span></span>  
  
2.  <span data-ttu-id="e15ad-138">在 [指定要用來連線至模型的使用者名稱或角色] 中，選取 [角色]，接著在下拉式清單方塊中選取 [銷售經理]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="e15ad-138">In **Specify the user name or role to use to connect to the model**, select **Role**, and then in the drop-down listbox, select **Sales Manager**, and then click **OK**.</span></span>  
  
    <span data-ttu-id="e15ad-139">Excel 會開啟新的活頁簿。</span><span class="sxs-lookup"><span data-stu-id="e15ad-139">Excel opens with a new workbook.</span></span> <span data-ttu-id="e15ad-140">將會自動建立樞紐分析表。</span><span class="sxs-lookup"><span data-stu-id="e15ad-140">A PivotTable is automatically created.</span></span> <span data-ttu-id="e15ad-141">[樞紐分析表欄位清單] 包含您的新模型中可用的所有資料欄位。</span><span class="sxs-lookup"><span data-stu-id="e15ad-141">The Pivot Table Field List includes all the data fields available in your new model.</span></span>  
      
3.  <span data-ttu-id="e15ad-142">關閉 Excel 而不儲存活頁簿。</span><span class="sxs-lookup"><span data-stu-id="e15ad-142">Close Excel without saving the workbook.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="e15ad-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e15ad-143">What's next?</span></span>
<span data-ttu-id="e15ad-144">移至下一個課程︰[第 13 課︰部署](../tutorials/aas-lesson-13-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="e15ad-144">Go to the next lesson: [Lesson 13: Deploy](../tutorials/aas-lesson-13-deploy.md).</span></span>

  
  
  
