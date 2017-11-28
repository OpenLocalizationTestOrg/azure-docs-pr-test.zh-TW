---
title: "aaa\"Azure Analysis Services 的 Adventure Works 教學課程 |Microsoft 文件 」"
description: "Hello Adventure Works 教學課程介紹 Azure Analysis services"
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
ms.openlocfilehash: 2df8b3ab4e8c4ffbe0086418d60fd2e2abd35e7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-analysis-services---adventure-works-tutorial"></a><span data-ttu-id="5ab6d-103">Azure Analysis Services - Adventure Works 教學課程</span><span class="sxs-lookup"><span data-stu-id="5ab6d-103">Azure Analysis Services - Adventure Works tutorial</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="5ab6d-104">本教學課程提供如何課程 toocreate 和部署的 hello 1400 相容性層級的表格式模型使用[SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)。</span><span class="sxs-lookup"><span data-stu-id="5ab6d-104">This tutorial provides lessons on how toocreate and deploy a tabular model at hello 1400 compatibility level by using [SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).</span></span>  

<span data-ttu-id="5ab6d-105">如果您是新 tooAnalysis 服務和表格式模型，完成本教學課程會最快速方式 toolearn hello 是如何 toocreate 和部署的基本表格式模型。</span><span class="sxs-lookup"><span data-stu-id="5ab6d-105">If you're new tooAnalysis Services and tabular modeling, completing this tutorial is hello quickest way toolearn how toocreate and deploy a basic tabular model.</span></span> <span data-ttu-id="5ab6d-106">一旦您擁有 hello 必要條件就地，所應使用兩個 toothree 小時 toocomplete 之間。</span><span class="sxs-lookup"><span data-stu-id="5ab6d-106">Once you have hello prerequisites in-place, it should take between two toothree hours toocomplete.</span></span>  
  
## <a name="what-you-learn"></a><span data-ttu-id="5ab6d-107">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="5ab6d-107">What you learn</span></span>   
  
-   <span data-ttu-id="5ab6d-108">在 hello toocreate 新的表格式模型專案的方式**1400年相容性層級**在 SSDT 中。</span><span class="sxs-lookup"><span data-stu-id="5ab6d-108">How toocreate a new tabular model project at hello **1400 compatibility level** in SSDT.</span></span>
  
-   <span data-ttu-id="5ab6d-109">如何從關聯式資料庫到表格式模型專案 tooimport 資料。</span><span class="sxs-lookup"><span data-stu-id="5ab6d-109">How tooimport data from a relational database into a tabular model project.</span></span>  
  
-   <span data-ttu-id="5ab6d-110">如何 toocreate 和管理 hello 模型中的資料表之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="5ab6d-110">How toocreate and manage relationships between tables in hello model.</span></span>  
  
-   <span data-ttu-id="5ab6d-111">如何 toocreate 導出資料行、 量值和關鍵效能指標，幫助使用者分析重要商務標準。</span><span class="sxs-lookup"><span data-stu-id="5ab6d-111">How toocreate calculated columns, measures, and Key Performance Indicators that help users analyze critical business metrics.</span></span>  
  
-   <span data-ttu-id="5ab6d-112">如何 toocreate 和管理檢視方塊和階層，幫助使用者更輕鬆地瀏覽模型資料提供業務和應用程式特有視點。</span><span class="sxs-lookup"><span data-stu-id="5ab6d-112">How toocreate and manage perspectives and hierarchies that help users more easily browse model data by providing business and application-specific viewpoints.</span></span>  
  
-   <span data-ttu-id="5ab6d-113">如何 toocreate 資料分割的資料表資料分成較小的邏輯部分可獨立於其他資料分割處理。</span><span class="sxs-lookup"><span data-stu-id="5ab6d-113">How toocreate partitions that divide table data into smaller logical parts that can be processed independent from other partitions.</span></span>  
  
-   <span data-ttu-id="5ab6d-114">如何 toosecure 藉由建立角色的使用者成員模型物件和資料。</span><span class="sxs-lookup"><span data-stu-id="5ab6d-114">How toosecure model objects and data by creating roles with user members.</span></span>  
  
-   <span data-ttu-id="5ab6d-115">如何 toodeploy 表格式模型 tooan **Azure Analysis Services**伺服器或內部部署 SQL Server 2017 Analysis Services 伺服器。</span><span class="sxs-lookup"><span data-stu-id="5ab6d-115">How toodeploy a tabular model tooan **Azure Analysis Services** server or an on-premises SQL Server 2017 Analysis Services server.</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="5ab6d-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="5ab6d-116">Prerequisites</span></span>  
<span data-ttu-id="5ab6d-117">toocomplete 本教學課程中，您需要：</span><span class="sxs-lookup"><span data-stu-id="5ab6d-117">toocomplete this tutorial, you need:</span></span>  
  
-   <span data-ttu-id="5ab6d-118">Azure Analysis Services 或 SQL Server 2017 Analysis Services 執行個體 toodeploy 至模型。</span><span class="sxs-lookup"><span data-stu-id="5ab6d-118">An Azure Analysis Services or SQL Server 2017 Analysis Services instance toodeploy your model to.</span></span> <span data-ttu-id="5ab6d-119">註冊免費的 [Azure Analysis Services 試用版](https://azure.microsoft.com/services/analysis-services/)和[建立伺服器](../analysis-services-create-server.md)。</span><span class="sxs-lookup"><span data-stu-id="5ab6d-119">Sign up for a free [Azure Analysis Services trial](https://azure.microsoft.com/services/analysis-services/) and [create a server](../analysis-services-create-server.md).</span></span> <span data-ttu-id="5ab6d-120">或者，註冊並下載 [SQL Server 2017 Community Technology Preview](https://www.microsoft.com/evalcenter/evaluate-sql-server-vnext-ctp)。</span><span class="sxs-lookup"><span data-stu-id="5ab6d-120">Or, sign up and download [SQL Server 2017 Community Technology Preview](https://www.microsoft.com/evalcenter/evaluate-sql-server-vnext-ctp).</span></span> 

-   <span data-ttu-id="5ab6d-121">SQL Server 資料倉儲或 Azure SQL 資料倉儲以 hello [AdventureWorksDW2014 範例資料庫](http://go.microsoft.com/fwlink/?LinkID=335807)。</span><span class="sxs-lookup"><span data-stu-id="5ab6d-121">A SQL Server Data Warehouse or Azure SQL Data Warehouse with hello [AdventureWorksDW2014 sample database](http://go.microsoft.com/fwlink/?LinkID=335807).</span></span> <span data-ttu-id="5ab6d-122">這個範例資料庫包括 hello 資料所需 toocomplete 本教學課程。</span><span class="sxs-lookup"><span data-stu-id="5ab6d-122">This sample database includes hello data necessary toocomplete this tutorial.</span></span> <span data-ttu-id="5ab6d-123">下載 [SQL Server 免費版本](https://www.microsoft.com/sql-server/sql-server-downloads)。</span><span class="sxs-lookup"><span data-stu-id="5ab6d-123">Download [SQL Server free editions](https://www.microsoft.com/sql-server/sql-server-downloads).</span></span> <span data-ttu-id="5ab6d-124">或者，註冊免費的 [Azure SQL Database 試用版](https://azure.microsoft.com/services/sql-database/)。</span><span class="sxs-lookup"><span data-stu-id="5ab6d-124">Or, sign up for a free [Azure SQL Database trial](https://azure.microsoft.com/services/sql-database/).</span></span> 

    <span data-ttu-id="5ab6d-125">**重要事項：**如果您在內部部署 SQL Server 上安裝 hello 範例資料庫，而且您部署模型 tooan Azure Analysis Services 伺服器時，[在內部部署資料閘道](../analysis-services-gateway.md)需要。</span><span class="sxs-lookup"><span data-stu-id="5ab6d-125">**Important:** If you install hello sample database on an on-premises SQL Server, and you deploy your model tooan Azure Analysis Services server, an [On-premises data gateway](../analysis-services-gateway.md) is required.</span></span>

-   <span data-ttu-id="5ab6d-126">hello 最新版本的[SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5ab6d-126">hello latest version of [SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).</span></span>

-   <span data-ttu-id="5ab6d-127">hello 最新版本的[SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。</span><span class="sxs-lookup"><span data-stu-id="5ab6d-127">hello latest version of [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>    

-   <span data-ttu-id="5ab6d-128">用戶端應用程式，例如 [Power BI Desktop](https://powerbi.microsoft.com/desktop/) 或 Excel。</span><span class="sxs-lookup"><span data-stu-id="5ab6d-128">A client application such as [Power BI Desktop](https://powerbi.microsoft.com/desktop/) or Excel.</span></span> 

## <a name="scenario"></a><span data-ttu-id="5ab6d-129">案例</span><span class="sxs-lookup"><span data-stu-id="5ab6d-129">Scenario</span></span>  
<span data-ttu-id="5ab6d-130">本教學課程以虛構公司 Adventure Works Cycles 做為基礎。</span><span class="sxs-lookup"><span data-stu-id="5ab6d-130">This tutorial is based on Adventure Works Cycles, a fictitious company.</span></span> <span data-ttu-id="5ab6d-131">Adventure Works 則是大型的跨國製造公司，製造及批發自行車、 組件] 和 [附屬應用程式 toocommercial 市場中北美、 歐洲和亞洲。</span><span class="sxs-lookup"><span data-stu-id="5ab6d-131">Adventure Works is a large, multinational manufacturing company that produces and distributes bicycles, parts, and accessories toocommercial markets in North America, Europe, and Asia.</span></span> <span data-ttu-id="5ab6d-132">hello 公司雇用 500 位員工。</span><span class="sxs-lookup"><span data-stu-id="5ab6d-132">hello company employs 500 workers.</span></span> <span data-ttu-id="5ab6d-133">此外，Adventure Works 僱用數個區域銷售團隊，遍布其市場規模。</span><span class="sxs-lookup"><span data-stu-id="5ab6d-133">Additionally, Adventure Works employs several regional sales teams throughout its market base.</span></span> <span data-ttu-id="5ab6d-134">您的專案是 toocreate 表格式模型，讓銷售及行銷使用者 tooanalyze hello AdventureWorksDW 資料庫中的網際網路銷售資料。</span><span class="sxs-lookup"><span data-stu-id="5ab6d-134">Your project is toocreate a tabular model for sales and marketing users tooanalyze Internet sales data in hello AdventureWorksDW database.</span></span>  
  
<span data-ttu-id="5ab6d-135">toocomplete hello 教學課程中，您必須完成各種課程。</span><span class="sxs-lookup"><span data-stu-id="5ab6d-135">toocomplete hello tutorial, you must complete various lessons.</span></span> <span data-ttu-id="5ab6d-136">每個課程有一些工作。</span><span class="sxs-lookup"><span data-stu-id="5ab6d-136">In each lesson, there are tasks.</span></span> <span data-ttu-id="5ab6d-137">必須完成 hello 課程完成每項工作順序。</span><span class="sxs-lookup"><span data-stu-id="5ab6d-137">Completing each task in order is necessary for completing hello lesson.</span></span> <span data-ttu-id="5ab6d-138">特定的課程中可能有幾項工作會達成類似的結果，但您完成每項工作的方式會稍有不同。</span><span class="sxs-lookup"><span data-stu-id="5ab6d-138">While in a particular lesson there may be several tasks that accomplish a similar outcome, but how you complete each task is slightly different.</span></span> <span data-ttu-id="5ab6d-139">這個方法顯示，通常會有多個方法之一 toocomplete 工作和 toochallenge 您使用技術學中先前的課程和工作。</span><span class="sxs-lookup"><span data-stu-id="5ab6d-139">This method shows there is often more than one way toocomplete a task, and toochallenge you by using skills you've learned in previous lessons and tasks.</span></span>  
  
<span data-ttu-id="5ab6d-140">hello hello 課程的目的是的 tooguide 您透過撰寫的基本表格式模型使用的許多 hello 功能包含在 SSDT 中。</span><span class="sxs-lookup"><span data-stu-id="5ab6d-140">hello purpose of hello lessons is tooguide you through authoring a basic tabular model by using many of hello features included in SSDT.</span></span> <span data-ttu-id="5ab6d-141">因為每個課程根據 hello 上一課，您應該完成 hello 課程中的順序。</span><span class="sxs-lookup"><span data-stu-id="5ab6d-141">Because each lesson builds upon hello previous lesson, you should complete hello lessons in order.</span></span>
  
<span data-ttu-id="5ab6d-142">本教學課程不提供有關管理伺服器，以在 Azure 入口網站，管理伺服器或資料庫使用 SSMS，或使用用戶端應用程式 toobrowse 模型資料。</span><span class="sxs-lookup"><span data-stu-id="5ab6d-142">This tutorial does not provide lessons about managing a server in Azure portal, managing a server or database by using SSMS, or using a client application toobrowse model data.</span></span> 


## <a name="lessons"></a><span data-ttu-id="5ab6d-143">課程</span><span class="sxs-lookup"><span data-stu-id="5ab6d-143">Lessons</span></span>  
<span data-ttu-id="5ab6d-144">這個教學課程包括下列課程中的 hello:</span><span class="sxs-lookup"><span data-stu-id="5ab6d-144">This tutorial includes hello following lessons:</span></span>  
  
|<span data-ttu-id="5ab6d-145">課程</span><span class="sxs-lookup"><span data-stu-id="5ab6d-145">Lesson</span></span>|<span data-ttu-id="5ab6d-146">預估的時間 toocomplete</span><span class="sxs-lookup"><span data-stu-id="5ab6d-146">Estimated time toocomplete</span></span>|  
|----------|------------------------------|  
|[<span data-ttu-id="5ab6d-147">1 - 建立新的表格式模型專案</span><span class="sxs-lookup"><span data-stu-id="5ab6d-147">1 - Create a new tabular model project</span></span>](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md)|<span data-ttu-id="5ab6d-148">10 分鐘</span><span class="sxs-lookup"><span data-stu-id="5ab6d-148">10 minutes</span></span>|  
|[<span data-ttu-id="5ab6d-149">2 - 取得資料</span><span class="sxs-lookup"><span data-stu-id="5ab6d-149">2 - Get data</span></span>](../tutorials/aas-lesson-2-get-data.md)|<span data-ttu-id="5ab6d-150">10 分鐘</span><span class="sxs-lookup"><span data-stu-id="5ab6d-150">10 minutes</span></span>|  
|[<span data-ttu-id="5ab6d-151">3 - 標記為日期資料表</span><span class="sxs-lookup"><span data-stu-id="5ab6d-151">3 - Mark as Date Table</span></span>](../tutorials/aas-lesson-3-mark-as-date-table.md)|<span data-ttu-id="5ab6d-152">3 分鐘</span><span class="sxs-lookup"><span data-stu-id="5ab6d-152">3 minutes</span></span>|  
|[<span data-ttu-id="5ab6d-153">4 - 建立關聯性</span><span class="sxs-lookup"><span data-stu-id="5ab6d-153">4 - Create relationships</span></span>](../tutorials/aas-lesson-4-create-relationships.md)|<span data-ttu-id="5ab6d-154">10 分鐘</span><span class="sxs-lookup"><span data-stu-id="5ab6d-154">10 minutes</span></span>|  
|[<span data-ttu-id="5ab6d-155">5 - 建立計算結果欄</span><span class="sxs-lookup"><span data-stu-id="5ab6d-155">5 - Create calculated columns</span></span>](../tutorials/aas-lesson-5-create-calculated-columns.md)|<span data-ttu-id="5ab6d-156">15 Minuten</span><span class="sxs-lookup"><span data-stu-id="5ab6d-156">15 minutes</span></span>|
|[<span data-ttu-id="5ab6d-157">6 - 建立量值</span><span class="sxs-lookup"><span data-stu-id="5ab6d-157">6 - Create measures</span></span>](../tutorials/aas-lesson-6-create-measures.md)|<span data-ttu-id="5ab6d-158">30 分鐘</span><span class="sxs-lookup"><span data-stu-id="5ab6d-158">30 minutes</span></span>|  
|[<span data-ttu-id="5ab6d-159">7 - 建立關鍵效能指標 (KPI)</span><span class="sxs-lookup"><span data-stu-id="5ab6d-159">7 - Create Key Performance Indicators (KPI)</span></span>](../tutorials/aas-lesson-7-create-key-performance-indicators.md)|<span data-ttu-id="5ab6d-160">15 Minuten</span><span class="sxs-lookup"><span data-stu-id="5ab6d-160">15 minutes</span></span>|  
|[<span data-ttu-id="5ab6d-161">8 - 建立檢視方塊</span><span class="sxs-lookup"><span data-stu-id="5ab6d-161">8 - Create perspectives</span></span>](../tutorials/aas-lesson-8-create-perspectives.md)|<span data-ttu-id="5ab6d-162">5 分鐘</span><span class="sxs-lookup"><span data-stu-id="5ab6d-162">5 minutes</span></span>|  
|[<span data-ttu-id="5ab6d-163">9 - 建立階層</span><span class="sxs-lookup"><span data-stu-id="5ab6d-163">9 - Create hierarchies</span></span>](../tutorials/aas-lesson-9-create-hierarchies.md)|<span data-ttu-id="5ab6d-164">20 分鐘</span><span class="sxs-lookup"><span data-stu-id="5ab6d-164">20 minutes</span></span>|  
|[<span data-ttu-id="5ab6d-165">10 - 建立分割區</span><span class="sxs-lookup"><span data-stu-id="5ab6d-165">10 - Create partitions</span></span>](../tutorials/aas-lesson-10-create-partitions.md)|<span data-ttu-id="5ab6d-166">15 Minuten</span><span class="sxs-lookup"><span data-stu-id="5ab6d-166">15 minutes</span></span>|  
|[<span data-ttu-id="5ab6d-167">11 - 建立角色</span><span class="sxs-lookup"><span data-stu-id="5ab6d-167">11 - Create roles</span></span>](../tutorials/aas-lesson-11-create-roles.md)|<span data-ttu-id="5ab6d-168">15 Minuten</span><span class="sxs-lookup"><span data-stu-id="5ab6d-168">15 minutes</span></span>|  
|[<span data-ttu-id="5ab6d-169">12 - 在 Excel 中分析</span><span class="sxs-lookup"><span data-stu-id="5ab6d-169">12 - Analyze in Excel</span></span>](../tutorials/aas-lesson-12-analyze-in-excel.md)|<span data-ttu-id="5ab6d-170">5 分鐘</span><span class="sxs-lookup"><span data-stu-id="5ab6d-170">5 minutes</span></span>| 
|[<span data-ttu-id="5ab6d-171">13 - 部署</span><span class="sxs-lookup"><span data-stu-id="5ab6d-171">13 - Deploy</span></span>](../tutorials/aas-lesson-13-deploy.md)|<span data-ttu-id="5ab6d-172">5 分鐘</span><span class="sxs-lookup"><span data-stu-id="5ab6d-172">5 minutes</span></span>|  
  
## <a name="supplemental-lessons"></a><span data-ttu-id="5ab6d-173">補充課程</span><span class="sxs-lookup"><span data-stu-id="5ab6d-173">Supplemental lessons</span></span>  
<span data-ttu-id="5ab6d-174">這些課程不需要的 toocomplete hello 教學課程中，但可能有助於更佳了解進階表格式模型撰寫功能。</span><span class="sxs-lookup"><span data-stu-id="5ab6d-174">These lessons are not required toocomplete hello tutorial, but can be helpful in better understanding advanced tabular model authoring features.</span></span>  
  
|<span data-ttu-id="5ab6d-175">課程</span><span class="sxs-lookup"><span data-stu-id="5ab6d-175">Lesson</span></span>|<span data-ttu-id="5ab6d-176">預估的時間 toocomplete</span><span class="sxs-lookup"><span data-stu-id="5ab6d-176">Estimated time toocomplete</span></span>|  
|----------|------------------------------|  
|[<span data-ttu-id="5ab6d-177">詳細資料列</span><span class="sxs-lookup"><span data-stu-id="5ab6d-177">Detail Rows</span></span>](../tutorials/aas-supplemental-lesson-detail-rows.md)|<span data-ttu-id="5ab6d-178">10 分鐘</span><span class="sxs-lookup"><span data-stu-id="5ab6d-178">10 minutes</span></span>|
|[<span data-ttu-id="5ab6d-179">動態安全性</span><span class="sxs-lookup"><span data-stu-id="5ab6d-179">Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)|<span data-ttu-id="5ab6d-180">30 分鐘</span><span class="sxs-lookup"><span data-stu-id="5ab6d-180">30 minutes</span></span>|
|[<span data-ttu-id="5ab6d-181">不完全階層</span><span class="sxs-lookup"><span data-stu-id="5ab6d-181">Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)|<span data-ttu-id="5ab6d-182">20 分鐘</span><span class="sxs-lookup"><span data-stu-id="5ab6d-182">20 minutes</span></span>| 

  
## <a name="next-steps"></a><span data-ttu-id="5ab6d-183">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5ab6d-183">Next steps</span></span>  
<span data-ttu-id="5ab6d-184">tooget 啟動，請參閱[第 1 課： 建立新的表格式模型專案](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md)。</span><span class="sxs-lookup"><span data-stu-id="5ab6d-184">tooget started, see [Lesson 1: Create a New Tabular Model Project](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span></span>  
  
  
  

