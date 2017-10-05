---
title: "Azure Analysis Services Adventure Works 教學課程 | Microsoft Docs"
description: "Azure Analysis Services 的 Adventure Works 教學課程簡介"
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
ms.openlocfilehash: 257e0bc442f29bfe6683fb0511deac50d92c1720
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-analysis-services---adventure-works-tutorial"></a><span data-ttu-id="04084-103">Azure Analysis Services - Adventure Works 教學課程</span><span class="sxs-lookup"><span data-stu-id="04084-103">Azure Analysis Services - Adventure Works tutorial</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="04084-104">本教學課程示範如何使用 [SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt) 建立及部署 1400 相容性等級的表格式模型。</span><span class="sxs-lookup"><span data-stu-id="04084-104">This tutorial provides lessons on how to create and deploy a tabular model at the 1400 compatibility level by using [SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).</span></span>  

<span data-ttu-id="04084-105">如果您熟悉 Analysis Services 和表格式模型化，則本教學課程可讓您以最快速度了解如何建立及部署基本表格式模型。</span><span class="sxs-lookup"><span data-stu-id="04084-105">If you're new to Analysis Services and tabular modeling, completing this tutorial is the quickest way to learn how to create and deploy a basic tabular model.</span></span> <span data-ttu-id="04084-106">備齊必要條件後，完成本教學課程需要二至三小時的時間。</span><span class="sxs-lookup"><span data-stu-id="04084-106">Once you have the prerequisites in-place, it should take between two to three hours to complete.</span></span>  
  
## <a name="what-you-learn"></a><span data-ttu-id="04084-107">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="04084-107">What you learn</span></span>   
  
-   <span data-ttu-id="04084-108">如何在 SSDT 中建立 **1400 相容性等級**的新表格式模型專案。</span><span class="sxs-lookup"><span data-stu-id="04084-108">How to create a new tabular model project at the **1400 compatibility level** in SSDT.</span></span>
  
-   <span data-ttu-id="04084-109">如何將關聯式資料庫的資料匯入表格式模型專案。</span><span class="sxs-lookup"><span data-stu-id="04084-109">How to import data from a relational database into a tabular model project.</span></span>  
  
-   <span data-ttu-id="04084-110">如何在模型中建立及管理資料表之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="04084-110">How to create and manage relationships between tables in the model.</span></span>  
  
-   <span data-ttu-id="04084-111">如何建立計算結果欄、量值和關鍵效能指標，幫助使用者分析重要商務計量。</span><span class="sxs-lookup"><span data-stu-id="04084-111">How to create calculated columns, measures, and Key Performance Indicators that help users analyze critical business metrics.</span></span>  
  
-   <span data-ttu-id="04084-112">如何建立及管理檢視方塊和階層，藉由提供商務和應用程式專屬視點，以協助使用者更輕鬆地瀏覽模型資料。</span><span class="sxs-lookup"><span data-stu-id="04084-112">How to create and manage perspectives and hierarchies that help users more easily browse model data by providing business and application-specific viewpoints.</span></span>  
  
-   <span data-ttu-id="04084-113">如何建立分割區將資料表資料分割成較小的邏輯部分，以獨立於其他分割區來處理。</span><span class="sxs-lookup"><span data-stu-id="04084-113">How to create partitions that divide table data into smaller logical parts that can be processed independent from other partitions.</span></span>  
  
-   <span data-ttu-id="04084-114">如何建立具有使用者成員的角色以保護模型物件和資料。</span><span class="sxs-lookup"><span data-stu-id="04084-114">How to secure model objects and data by creating roles with user members.</span></span>  
  
-   <span data-ttu-id="04084-115">如何將表格式模型部署到 **Azure Analysis Services** 伺服器或內部部署 SQL Server 2017 Analysis Services 伺服器。</span><span class="sxs-lookup"><span data-stu-id="04084-115">How to deploy a tabular model to an **Azure Analysis Services** server or an on-premises SQL Server 2017 Analysis Services server.</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="04084-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="04084-116">Prerequisites</span></span>  
<span data-ttu-id="04084-117">若要完成本教學課程，您需要：</span><span class="sxs-lookup"><span data-stu-id="04084-117">To complete this tutorial, you need:</span></span>  
  
-   <span data-ttu-id="04084-118">Azure Analysis Services 或 SQL Server 2017 Analysis Services 執行個體，供部署您的模型。</span><span class="sxs-lookup"><span data-stu-id="04084-118">An Azure Analysis Services or SQL Server 2017 Analysis Services instance to deploy your model to.</span></span> <span data-ttu-id="04084-119">註冊免費的 [Azure Analysis Services 試用版](https://azure.microsoft.com/services/analysis-services/)和[建立伺服器](../analysis-services-create-server.md)。</span><span class="sxs-lookup"><span data-stu-id="04084-119">Sign up for a free [Azure Analysis Services trial](https://azure.microsoft.com/services/analysis-services/) and [create a server](../analysis-services-create-server.md).</span></span> <span data-ttu-id="04084-120">或者，註冊並下載 [SQL Server 2017 Community Technology Preview](https://www.microsoft.com/evalcenter/evaluate-sql-server-vnext-ctp)。</span><span class="sxs-lookup"><span data-stu-id="04084-120">Or, sign up and download [SQL Server 2017 Community Technology Preview](https://www.microsoft.com/evalcenter/evaluate-sql-server-vnext-ctp).</span></span> 

-   <span data-ttu-id="04084-121">SQL Server 資料倉儲或 Azure SQL 資料倉儲，隨附 [AdventureWorksDW2014 範例資料庫](http://go.microsoft.com/fwlink/?LinkID=335807)。</span><span class="sxs-lookup"><span data-stu-id="04084-121">A SQL Server Data Warehouse or Azure SQL Data Warehouse with the [AdventureWorksDW2014 sample database](http://go.microsoft.com/fwlink/?LinkID=335807).</span></span> <span data-ttu-id="04084-122">這個範例資料庫包括完成本教學課程所需的資料。</span><span class="sxs-lookup"><span data-stu-id="04084-122">This sample database includes the data necessary to complete this tutorial.</span></span> <span data-ttu-id="04084-123">下載 [SQL Server 免費版本](https://www.microsoft.com/sql-server/sql-server-downloads)。</span><span class="sxs-lookup"><span data-stu-id="04084-123">Download [SQL Server free editions](https://www.microsoft.com/sql-server/sql-server-downloads).</span></span> <span data-ttu-id="04084-124">或者，註冊免費的 [Azure SQL Database 試用版](https://azure.microsoft.com/services/sql-database/)。</span><span class="sxs-lookup"><span data-stu-id="04084-124">Or, sign up for a free [Azure SQL Database trial](https://azure.microsoft.com/services/sql-database/).</span></span> 

    <span data-ttu-id="04084-125">**重要事項︰**如果您將範例資料庫安裝在內部部署 SQL Server，且將模型部署到 Azure Analysis Services 伺服器，則需要[內部部署資料閘道](../analysis-services-gateway.md)。</span><span class="sxs-lookup"><span data-stu-id="04084-125">**Important:** If you install the sample database on an on-premises SQL Server, and you deploy your model to an Azure Analysis Services server, an [On-premises data gateway](../analysis-services-gateway.md) is required.</span></span>

-   <span data-ttu-id="04084-126">最新版本的 [SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx)。</span><span class="sxs-lookup"><span data-stu-id="04084-126">The latest version of [SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).</span></span>

-   <span data-ttu-id="04084-127">最新版本的 [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。</span><span class="sxs-lookup"><span data-stu-id="04084-127">The latest version of [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>    

-   <span data-ttu-id="04084-128">用戶端應用程式，例如 [Power BI Desktop](https://powerbi.microsoft.com/desktop/) 或 Excel。</span><span class="sxs-lookup"><span data-stu-id="04084-128">A client application such as [Power BI Desktop](https://powerbi.microsoft.com/desktop/) or Excel.</span></span> 

## <a name="scenario"></a><span data-ttu-id="04084-129">案例</span><span class="sxs-lookup"><span data-stu-id="04084-129">Scenario</span></span>  
<span data-ttu-id="04084-130">本教學課程以虛構公司 Adventure Works Cycles 做為基礎。</span><span class="sxs-lookup"><span data-stu-id="04084-130">This tutorial is based on Adventure Works Cycles, a fictitious company.</span></span> <span data-ttu-id="04084-131">Adventure Works 是一家大型的跨國製造公司，主要生產自行車、零件和配件，產品銷售到北美洲、歐洲和亞洲的商業市場。</span><span class="sxs-lookup"><span data-stu-id="04084-131">Adventure Works is a large, multinational manufacturing company that produces and distributes bicycles, parts, and accessories to commercial markets in North America, Europe, and Asia.</span></span> <span data-ttu-id="04084-132">該公司雇用 500 名員工。</span><span class="sxs-lookup"><span data-stu-id="04084-132">The company employs 500 workers.</span></span> <span data-ttu-id="04084-133">此外，Adventure Works 僱用數個區域銷售團隊，遍布其市場規模。</span><span class="sxs-lookup"><span data-stu-id="04084-133">Additionally, Adventure Works employs several regional sales teams throughout its market base.</span></span> <span data-ttu-id="04084-134">您的專案是建立一個表格式模型，讓銷售和行銷使用者分析 AdventureWorksDW 資料庫中的網際網路銷售資料。</span><span class="sxs-lookup"><span data-stu-id="04084-134">Your project is to create a tabular model for sales and marketing users to analyze Internet sales data in the AdventureWorksDW database.</span></span>  
  
<span data-ttu-id="04084-135">若要完成本教學課程，您必須完成各個課程。</span><span class="sxs-lookup"><span data-stu-id="04084-135">To complete the tutorial, you must complete various lessons.</span></span> <span data-ttu-id="04084-136">每個課程有一些工作。</span><span class="sxs-lookup"><span data-stu-id="04084-136">In each lesson, there are tasks.</span></span> <span data-ttu-id="04084-137">必須依序完成每個工作，才能完成本課程。</span><span class="sxs-lookup"><span data-stu-id="04084-137">Completing each task in order is necessary for completing the lesson.</span></span> <span data-ttu-id="04084-138">特定的課程中可能有幾項工作會達成類似的結果，但您完成每項工作的方式會稍有不同。</span><span class="sxs-lookup"><span data-stu-id="04084-138">While in a particular lesson there may be several tasks that accomplish a similar outcome, but how you complete each task is slightly different.</span></span> <span data-ttu-id="04084-139">此方法顯示完成工作通常有一種以上的方法，並激發您運用先前的課程和工作中所學到的技術。</span><span class="sxs-lookup"><span data-stu-id="04084-139">This method shows there is often more than one way to complete a task, and to challenge you by using skills you've learned in previous lessons and tasks.</span></span>  
  
<span data-ttu-id="04084-140">這些課程的目的是引導您使用 SSDT 內含的許多功能來製作基本表格式模型。</span><span class="sxs-lookup"><span data-stu-id="04084-140">The purpose of the lessons is to guide you through authoring a basic tabular model by using many of the features included in SSDT.</span></span> <span data-ttu-id="04084-141">因為每個課程都是根據上一課，您應該依序完成課程。</span><span class="sxs-lookup"><span data-stu-id="04084-141">Because each lesson builds upon the previous lesson, you should complete the lessons in order.</span></span>
  
<span data-ttu-id="04084-142">本教學課程提供的課題不包括：在 Azure 入口網站中管理伺服器、使用 SSMS 管理伺服器或資料庫，或使用用戶端應用程式來瀏覽模型資料。</span><span class="sxs-lookup"><span data-stu-id="04084-142">This tutorial does not provide lessons about managing a server in Azure portal, managing a server or database by using SSMS, or using a client application to browse model data.</span></span> 


## <a name="lessons"></a><span data-ttu-id="04084-143">課程</span><span class="sxs-lookup"><span data-stu-id="04084-143">Lessons</span></span>  
<span data-ttu-id="04084-144">本教學課程包括下列課程︰</span><span class="sxs-lookup"><span data-stu-id="04084-144">This tutorial includes the following lessons:</span></span>  
  
|<span data-ttu-id="04084-145">課程</span><span class="sxs-lookup"><span data-stu-id="04084-145">Lesson</span></span>|<span data-ttu-id="04084-146">預估完成時間</span><span class="sxs-lookup"><span data-stu-id="04084-146">Estimated time to complete</span></span>|  
|----------|------------------------------|  
|[<span data-ttu-id="04084-147">1 - 建立新的表格式模型專案</span><span class="sxs-lookup"><span data-stu-id="04084-147">1 - Create a new tabular model project</span></span>](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md)|<span data-ttu-id="04084-148">10 分鐘</span><span class="sxs-lookup"><span data-stu-id="04084-148">10 minutes</span></span>|  
|[<span data-ttu-id="04084-149">2 - 取得資料</span><span class="sxs-lookup"><span data-stu-id="04084-149">2 - Get data</span></span>](../tutorials/aas-lesson-2-get-data.md)|<span data-ttu-id="04084-150">10 分鐘</span><span class="sxs-lookup"><span data-stu-id="04084-150">10 minutes</span></span>|  
|[<span data-ttu-id="04084-151">3 - 標記為日期資料表</span><span class="sxs-lookup"><span data-stu-id="04084-151">3 - Mark as Date Table</span></span>](../tutorials/aas-lesson-3-mark-as-date-table.md)|<span data-ttu-id="04084-152">3 分鐘</span><span class="sxs-lookup"><span data-stu-id="04084-152">3 minutes</span></span>|  
|[<span data-ttu-id="04084-153">4 - 建立關聯性</span><span class="sxs-lookup"><span data-stu-id="04084-153">4 - Create relationships</span></span>](../tutorials/aas-lesson-4-create-relationships.md)|<span data-ttu-id="04084-154">10 分鐘</span><span class="sxs-lookup"><span data-stu-id="04084-154">10 minutes</span></span>|  
|[<span data-ttu-id="04084-155">5 - 建立計算結果欄</span><span class="sxs-lookup"><span data-stu-id="04084-155">5 - Create calculated columns</span></span>](../tutorials/aas-lesson-5-create-calculated-columns.md)|<span data-ttu-id="04084-156">15 Minuten</span><span class="sxs-lookup"><span data-stu-id="04084-156">15 minutes</span></span>|
|[<span data-ttu-id="04084-157">6 - 建立量值</span><span class="sxs-lookup"><span data-stu-id="04084-157">6 - Create measures</span></span>](../tutorials/aas-lesson-6-create-measures.md)|<span data-ttu-id="04084-158">30 分鐘</span><span class="sxs-lookup"><span data-stu-id="04084-158">30 minutes</span></span>|  
|[<span data-ttu-id="04084-159">7 - 建立關鍵效能指標 (KPI)</span><span class="sxs-lookup"><span data-stu-id="04084-159">7 - Create Key Performance Indicators (KPI)</span></span>](../tutorials/aas-lesson-7-create-key-performance-indicators.md)|<span data-ttu-id="04084-160">15 Minuten</span><span class="sxs-lookup"><span data-stu-id="04084-160">15 minutes</span></span>|  
|[<span data-ttu-id="04084-161">8 - 建立檢視方塊</span><span class="sxs-lookup"><span data-stu-id="04084-161">8 - Create perspectives</span></span>](../tutorials/aas-lesson-8-create-perspectives.md)|<span data-ttu-id="04084-162">5 分鐘</span><span class="sxs-lookup"><span data-stu-id="04084-162">5 minutes</span></span>|  
|[<span data-ttu-id="04084-163">9 - 建立階層</span><span class="sxs-lookup"><span data-stu-id="04084-163">9 - Create hierarchies</span></span>](../tutorials/aas-lesson-9-create-hierarchies.md)|<span data-ttu-id="04084-164">20 分鐘</span><span class="sxs-lookup"><span data-stu-id="04084-164">20 minutes</span></span>|  
|[<span data-ttu-id="04084-165">10 - 建立分割區</span><span class="sxs-lookup"><span data-stu-id="04084-165">10 - Create partitions</span></span>](../tutorials/aas-lesson-10-create-partitions.md)|<span data-ttu-id="04084-166">15 Minuten</span><span class="sxs-lookup"><span data-stu-id="04084-166">15 minutes</span></span>|  
|[<span data-ttu-id="04084-167">11 - 建立角色</span><span class="sxs-lookup"><span data-stu-id="04084-167">11 - Create roles</span></span>](../tutorials/aas-lesson-11-create-roles.md)|<span data-ttu-id="04084-168">15 Minuten</span><span class="sxs-lookup"><span data-stu-id="04084-168">15 minutes</span></span>|  
|[<span data-ttu-id="04084-169">12 - 在 Excel 中分析</span><span class="sxs-lookup"><span data-stu-id="04084-169">12 - Analyze in Excel</span></span>](../tutorials/aas-lesson-12-analyze-in-excel.md)|<span data-ttu-id="04084-170">5 分鐘</span><span class="sxs-lookup"><span data-stu-id="04084-170">5 minutes</span></span>| 
|[<span data-ttu-id="04084-171">13 - 部署</span><span class="sxs-lookup"><span data-stu-id="04084-171">13 - Deploy</span></span>](../tutorials/aas-lesson-13-deploy.md)|<span data-ttu-id="04084-172">5 分鐘</span><span class="sxs-lookup"><span data-stu-id="04084-172">5 minutes</span></span>|  
  
## <a name="supplemental-lessons"></a><span data-ttu-id="04084-173">補充課程</span><span class="sxs-lookup"><span data-stu-id="04084-173">Supplemental lessons</span></span>  
<span data-ttu-id="04084-174">完成這個教學課程並不需要這些課程，但是能幫助您更了解表格式模型的進階製作功能。</span><span class="sxs-lookup"><span data-stu-id="04084-174">These lessons are not required to complete the tutorial, but can be helpful in better understanding advanced tabular model authoring features.</span></span>  
  
|<span data-ttu-id="04084-175">課程</span><span class="sxs-lookup"><span data-stu-id="04084-175">Lesson</span></span>|<span data-ttu-id="04084-176">預估完成時間</span><span class="sxs-lookup"><span data-stu-id="04084-176">Estimated time to complete</span></span>|  
|----------|------------------------------|  
|[<span data-ttu-id="04084-177">詳細資料列</span><span class="sxs-lookup"><span data-stu-id="04084-177">Detail Rows</span></span>](../tutorials/aas-supplemental-lesson-detail-rows.md)|<span data-ttu-id="04084-178">10 分鐘</span><span class="sxs-lookup"><span data-stu-id="04084-178">10 minutes</span></span>|
|[<span data-ttu-id="04084-179">動態安全性</span><span class="sxs-lookup"><span data-stu-id="04084-179">Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)|<span data-ttu-id="04084-180">30 分鐘</span><span class="sxs-lookup"><span data-stu-id="04084-180">30 minutes</span></span>|
|[<span data-ttu-id="04084-181">不完全階層</span><span class="sxs-lookup"><span data-stu-id="04084-181">Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)|<span data-ttu-id="04084-182">20 分鐘</span><span class="sxs-lookup"><span data-stu-id="04084-182">20 minutes</span></span>| 

  
## <a name="next-steps"></a><span data-ttu-id="04084-183">後續步驟</span><span class="sxs-lookup"><span data-stu-id="04084-183">Next steps</span></span>  
<span data-ttu-id="04084-184">若要開始，請參閱[第 1 課：建立新的表格式模型專案](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md)。</span><span class="sxs-lookup"><span data-stu-id="04084-184">To get started, see [Lesson 1: Create a New Tabular Model Project](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span></span>  
  
  
  

