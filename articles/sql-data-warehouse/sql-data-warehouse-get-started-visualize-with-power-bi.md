---
title: "aaaVisualize 使用 Power BI 的 Microsoft Azure SQL 資料倉儲資料"
description: "使用 Power BI 視覺化 SQL 資料倉儲資料"
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: d7fb89d1-da1d-4788-a111-68d0e3fda799
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: 0425cf5abe7bc001b2a41df4d09bf5f2e42527e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-data-with-power-bi"></a><span data-ttu-id="44e39-103">使用 Power BI 視覺化資料</span><span class="sxs-lookup"><span data-stu-id="44e39-103">Visualize data with Power BI</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="44e39-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="44e39-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="44e39-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="44e39-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="44e39-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="44e39-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="44e39-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="44e39-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="44e39-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="44e39-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="44e39-109">本教學課程示範如何 toouse Power BI tooconnect tooSQL 資料倉儲，並建立一些基本的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="44e39-109">This tutorial shows you how toouse Power BI tooconnect tooSQL Data Warehouse and create a few basic visualizations.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Data-Warehouse-Sample-Data-and-PowerBI/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="44e39-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="44e39-110">Prerequisites</span></span>
<span data-ttu-id="44e39-111">在本教學課程 toostep，您需要：</span><span class="sxs-lookup"><span data-stu-id="44e39-111">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="44e39-112">SQL 資料倉儲預先載入與 hello AdventureWorksDW 資料庫。</span><span class="sxs-lookup"><span data-stu-id="44e39-112">A SQL Data Warehouse pre-loaded with hello AdventureWorksDW database.</span></span> <span data-ttu-id="44e39-113">tooprovision，請參閱[建立 SQL 資料倉儲][ Create a SQL Data Warehouse]選擇 tooload hello 範例資料。</span><span class="sxs-lookup"><span data-stu-id="44e39-113">tooprovision this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse] and choose tooload hello sample data.</span></span> <span data-ttu-id="44e39-114">如果您已經有資料倉儲但沒有範例資料，您可以[手動載入範例資料][load sample data manually]。</span><span class="sxs-lookup"><span data-stu-id="44e39-114">If you already have a data warehouse but do not have sample data, you can [load sample data manually][load sample data manually].</span></span>

## <a name="1-connect-tooyour-database"></a><span data-ttu-id="44e39-115">1.連接 tooyour 資料庫</span><span class="sxs-lookup"><span data-stu-id="44e39-115">1. Connect tooyour database</span></span>
<span data-ttu-id="44e39-116">tooopen Power BI，並連接 tooyour AdventureWorksDW 資料庫：</span><span class="sxs-lookup"><span data-stu-id="44e39-116">tooopen Power BI and connect tooyour AdventureWorksDW database:</span></span>

1. <span data-ttu-id="44e39-117">登入 hello [Azure 入口網站][Azure portal]。</span><span class="sxs-lookup"><span data-stu-id="44e39-117">Sign into hello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="44e39-118">按一下 [SQL 資料庫]  ，並選擇您的 AdventureWorks SQL 資料倉儲資料庫。</span><span class="sxs-lookup"><span data-stu-id="44e39-118">Click **SQL databases** and choose your AdventureWorks SQL Data Warehouse database.</span></span>
   
    ![尋找您的資料庫][1]
3. <span data-ttu-id="44e39-120">按一下 hello 'Power BI 中開啟 按鈕。</span><span class="sxs-lookup"><span data-stu-id="44e39-120">Click hello 'Open in Power BI' button.</span></span>
   
    ![Power BI 按鈕][2]
4. <span data-ttu-id="44e39-122">您現在應該會看到 hello SQL 資料倉儲連接頁面顯示您資料庫的網址。</span><span class="sxs-lookup"><span data-stu-id="44e39-122">You should now see hello SQL Data Warehouse connection page displaying your database web address.</span></span> <span data-ttu-id="44e39-123">按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="44e39-123">Click next.</span></span>
   
    ![Power BI 連接][3]
5. <span data-ttu-id="44e39-125">輸入您的 Azure SQL server 使用者名稱和密碼，然後您將無法完全連接的 tooyour SQL 資料倉儲資料庫。</span><span class="sxs-lookup"><span data-stu-id="44e39-125">Enter your Azure SQL server username and password and you will be fully connected tooyour SQL Data Warehouse database.</span></span>
   
    ![Power BI 登入][4]
6. <span data-ttu-id="44e39-127">一旦您已登入 Power BI 中，按一下 hello 左刀鋒視窗上的 hello AdventureWorksDW 資料集。</span><span class="sxs-lookup"><span data-stu-id="44e39-127">Once you have signed into Power BI, click hello AdventureWorksDW dataset on hello left blade.</span></span> <span data-ttu-id="44e39-128">這會開啟 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="44e39-128">This will open hello database.</span></span>
   
    ![Power BI 開啟 AdventureWorksDW][5]

## <a name="2-create-a-report"></a><span data-ttu-id="44e39-130">2.建立報表</span><span class="sxs-lookup"><span data-stu-id="44e39-130">2. Create a report</span></span>
<span data-ttu-id="44e39-131">您會立即準備 toouse Power BI tooanalyze AdventureWorksDW 範例資料。</span><span class="sxs-lookup"><span data-stu-id="44e39-131">You are now ready toouse Power BI tooanalyze your AdventureWorksDW sample data.</span></span> <span data-ttu-id="44e39-132">tooperform hello 分析 AdventureWorksDW 有一個稱為 AggregateSales 的檢視。</span><span class="sxs-lookup"><span data-stu-id="44e39-132">tooperform hello analysis, AdventureWorksDW has a view called AggregateSales.</span></span> <span data-ttu-id="44e39-133">這個檢視包含幾個 hello 分析 hello hello 公司銷售的關鍵計量。</span><span class="sxs-lookup"><span data-stu-id="44e39-133">This view contains a few of hello key metrics for analyzing hello sales of hello company.</span></span>

1. <span data-ttu-id="44e39-134">按一下 [hello AggregateSales 檢視 tooexpand toocreate 的銷售量 toopostal 的程式碼中，在 hello 右邊的欄位] 窗格中，根據對應它。</span><span class="sxs-lookup"><span data-stu-id="44e39-134">toocreate a map of sales amount according toopostal code, in hello right-hand fields pane, click hello AggregateSales view tooexpand it.</span></span> <span data-ttu-id="44e39-135">按一下 hello [郵遞區號] 和 [salesamount] 資料行 tooselect 它們。</span><span class="sxs-lookup"><span data-stu-id="44e39-135">Click hello PostalCode and SalesAmount columns tooselect them.</span></span>
   
    ![Power BI 選取 AggregateSales][6]
   
    <span data-ttu-id="44e39-137">Power BI 會自動將此辨識為地理資料，並將它放入地圖中。</span><span class="sxs-lookup"><span data-stu-id="44e39-137">Power BI automatically recognizes this is geographic data and put it in a map for you.</span></span>
   
    ![Power BI 對應圖][7]
2. <span data-ttu-id="44e39-139">這個步驟會建立橫條圖，顯示每個客戶收入的銷售金額。</span><span class="sxs-lookup"><span data-stu-id="44e39-139">This step creates a bar graph that shows amount of sales per customer income.</span></span> <span data-ttu-id="44e39-140">toocreate 此移 toohello 展開 AggregateSales 檢視。</span><span class="sxs-lookup"><span data-stu-id="44e39-140">toocreate this go toohello expanded AggregateSales view.</span></span> <span data-ttu-id="44e39-141">按一下 hello [salesamount] 欄位。</span><span class="sxs-lookup"><span data-stu-id="44e39-141">Click hello SalesAmount field.</span></span> <span data-ttu-id="44e39-142">Hello 客戶收入欄位 toohello 向左拖曳，並將其放置到座標軸。</span><span class="sxs-lookup"><span data-stu-id="44e39-142">Drag hello Customer Income field toohello left and drop it into Axis.</span></span>
   
    ![Power BI 選取軸][8]
   
    <span data-ttu-id="44e39-144">我們透過 hello 左移動 hello 橫條圖。</span><span class="sxs-lookup"><span data-stu-id="44e39-144">We moved hello bar chart over hello left.</span></span>
   
    ![Power BI 長條圖][9]
3. <span data-ttu-id="44e39-146">這個步驟會建立折線圖，顯示每個訂單日期的銷售金額。</span><span class="sxs-lookup"><span data-stu-id="44e39-146">This step creates a line chart that shows sales amount per order date.</span></span> <span data-ttu-id="44e39-147">toocreate 此移 toohello 展開 AggregateSales 檢視。</span><span class="sxs-lookup"><span data-stu-id="44e39-147">toocreate this go toohello expanded AggregateSales view.</span></span> <span data-ttu-id="44e39-148">按一下 [SalesAmount] 和 [OrderDate]。</span><span class="sxs-lookup"><span data-stu-id="44e39-148">Click SalesAmount and OrderDate.</span></span> <span data-ttu-id="44e39-149">Hello 視覺效果的資料行中按一下 hello 折線圖圖示。這是在視覺效果的 hello 第二行 hello 第一個圖示。</span><span class="sxs-lookup"><span data-stu-id="44e39-149">In hello Visualizations column click hello Line Chart icon; this is hello first icon in hello second line under visualizations.</span></span>
   
    ![Power BI 選取折線圖][10]
   
    <span data-ttu-id="44e39-151">您現在有顯示 hello 資料的三個不同的視覺效果的報表。</span><span class="sxs-lookup"><span data-stu-id="44e39-151">You now have a report that shows three different visualizations of hello data.</span></span>
   
    ![Power BI 折線圖][11]

<span data-ttu-id="44e39-153">您也可以隨時按一下 [檔案]，並選取 [儲存] 來儲存您的進度。</span><span class="sxs-lookup"><span data-stu-id="44e39-153">You can save your progress at any time by clicking **File** and selecting **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44e39-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="44e39-154">Next steps</span></span>
<span data-ttu-id="44e39-155">現在，我們提供了一些時間 toowarm hello 範例資料，請參閱如何太[開發][develop]，[載入][load]，或[移轉][migrate]。</span><span class="sxs-lookup"><span data-stu-id="44e39-155">Now that we've given you some time toowarm up with hello sample data, see how too[develop][develop], [load][load], or [migrate][migrate].</span></span> <span data-ttu-id="44e39-156">看看 hello 或者[Power BI 網站][Power BI website]。</span><span class="sxs-lookup"><span data-stu-id="44e39-156">Or take a look at hello [Power BI website][Power BI website].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-find-database.png
[2]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-button.png
[3]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-connect-to-azure.png
[4]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-sign-in.png
[5]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-open-adventureworks.png
[6]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-aggregatesales.png
[7]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-map.png
[8]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-chooseaxis.png
[9]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-bar.png
[10]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-prepare-line.png
[11]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-line.png
[12]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-save.png

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[connecting tooSQL Data Warehouse]: sql-data-warehouse-integrate-power-bi.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md

<!--Other-->
[Azure portal]: https://portal.azure.com/
[Power BI website]: http://www.powerbi.com/
