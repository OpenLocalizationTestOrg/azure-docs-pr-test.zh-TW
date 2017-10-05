---
title: "使用 Power BI 來將 SQL 資料倉儲資料視覺化 | Microsoft Azure"
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
ms.openlocfilehash: a41393730143b14e91318a61858d989fff3786c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="visualize-data-with-power-bi"></a><span data-ttu-id="f9b27-103">使用 Power BI 視覺化資料</span><span class="sxs-lookup"><span data-stu-id="f9b27-103">Visualize data with Power BI</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f9b27-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="f9b27-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="f9b27-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f9b27-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="f9b27-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f9b27-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="f9b27-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="f9b27-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="f9b27-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="f9b27-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="f9b27-109">本教學課程會示範如何使用 Power BI 來連接到 SQL 資料倉儲，並建立一些基本的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="f9b27-109">This tutorial shows you how to use Power BI to connect to SQL Data Warehouse and create a few basic visualizations.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Data-Warehouse-Sample-Data-and-PowerBI/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="f9b27-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="f9b27-110">Prerequisites</span></span>
<span data-ttu-id="f9b27-111">若要逐步執行本教學課程，您需要：</span><span class="sxs-lookup"><span data-stu-id="f9b27-111">To step through this tutorial, you need:</span></span>

* <span data-ttu-id="f9b27-112">預先載入 AdventureWorksDW 資料庫的 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="f9b27-112">A SQL Data Warehouse pre-loaded with the AdventureWorksDW database.</span></span> <span data-ttu-id="f9b27-113">若要進行佈建，請參閱[建立 SQL 資料倉儲][Create a SQL Data Warehouse]並選擇載入範例資料。</span><span class="sxs-lookup"><span data-stu-id="f9b27-113">To provision this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse] and choose to load the sample data.</span></span> <span data-ttu-id="f9b27-114">如果您已經有資料倉儲但沒有範例資料，您可以[手動載入範例資料][load sample data manually]。</span><span class="sxs-lookup"><span data-stu-id="f9b27-114">If you already have a data warehouse but do not have sample data, you can [load sample data manually][load sample data manually].</span></span>

## <a name="1-connect-to-your-database"></a><span data-ttu-id="f9b27-115">1.連接到您的資料庫</span><span class="sxs-lookup"><span data-stu-id="f9b27-115">1. Connect to your database</span></span>
<span data-ttu-id="f9b27-116">若要開啟 Power BI 並連接到您的 AdventureWorksDW 資料庫：</span><span class="sxs-lookup"><span data-stu-id="f9b27-116">To open Power BI and connect to your AdventureWorksDW database:</span></span>

1. <span data-ttu-id="f9b27-117">登入 [Azure 入口網站][Azure portal]。</span><span class="sxs-lookup"><span data-stu-id="f9b27-117">Sign into the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="f9b27-118">按一下 [SQL 資料庫]  ，並選擇您的 AdventureWorks SQL 資料倉儲資料庫。</span><span class="sxs-lookup"><span data-stu-id="f9b27-118">Click **SQL databases** and choose your AdventureWorks SQL Data Warehouse database.</span></span>
   
    ![尋找您的資料庫][1]
3. <span data-ttu-id="f9b27-120">按一下 [在 Power BI 中開啟] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f9b27-120">Click the 'Open in Power BI' button.</span></span>
   
    ![Power BI 按鈕][2]
4. <span data-ttu-id="f9b27-122">您現在應該會看到 SQL 資料倉儲連接頁面顯示您的資料庫網址。</span><span class="sxs-lookup"><span data-stu-id="f9b27-122">You should now see the SQL Data Warehouse connection page displaying your database web address.</span></span> <span data-ttu-id="f9b27-123">按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="f9b27-123">Click next.</span></span>
   
    ![Power BI 連接][3]
5. <span data-ttu-id="f9b27-125">輸入您的 Azure SQL Server 使用者名稱和密碼，隨後會將您完全連接到 SQL 資料倉儲資料庫。</span><span class="sxs-lookup"><span data-stu-id="f9b27-125">Enter your Azure SQL server username and password and you will be fully connected to your SQL Data Warehouse database.</span></span>
   
    ![Power BI 登入][4]
6. <span data-ttu-id="f9b27-127">一旦登入了 Power BI，請在左刀鋒視窗上按一下  AdventureWorksDW 資料集。</span><span class="sxs-lookup"><span data-stu-id="f9b27-127">Once you have signed into Power BI, click the AdventureWorksDW dataset on the left blade.</span></span> <span data-ttu-id="f9b27-128">這會開啟資料庫。</span><span class="sxs-lookup"><span data-stu-id="f9b27-128">This will open the database.</span></span>
   
    ![Power BI 開啟 AdventureWorksDW][5]

## <a name="2-create-a-report"></a><span data-ttu-id="f9b27-130">2.建立報表</span><span class="sxs-lookup"><span data-stu-id="f9b27-130">2. Create a report</span></span>
<span data-ttu-id="f9b27-131">您現在已準備好使用 Power BI 來分析 AdventureWorksDW 範例資料。</span><span class="sxs-lookup"><span data-stu-id="f9b27-131">You are now ready to use Power BI to analyze your AdventureWorksDW sample data.</span></span> <span data-ttu-id="f9b27-132">為了執行分析，AdventureWorksDW 有一個稱為 AggregateSales 的檢視。</span><span class="sxs-lookup"><span data-stu-id="f9b27-132">To perform the analysis, AdventureWorksDW has a view called AggregateSales.</span></span> <span data-ttu-id="f9b27-133">這個檢視包含用來分析公司銷售的一些重要指標。</span><span class="sxs-lookup"><span data-stu-id="f9b27-133">This view contains a few of the key metrics for analyzing the sales of the company.</span></span>

1. <span data-ttu-id="f9b27-134">若要根據郵遞區號建立銷售金額的對應圖，請在右手邊欄位窗格中按一下 AggregateSales 檢視以展開它。</span><span class="sxs-lookup"><span data-stu-id="f9b27-134">To create a map of sales amount according to postal code, in the right-hand fields pane, click the AggregateSales view to expand it.</span></span> <span data-ttu-id="f9b27-135">按一下 [PostalCode] 和 [SalesAmount] 資料行來選取它們。</span><span class="sxs-lookup"><span data-stu-id="f9b27-135">Click the PostalCode and SalesAmount columns to select them.</span></span>
   
    ![Power BI 選取 AggregateSales][6]
   
    <span data-ttu-id="f9b27-137">Power BI 會自動將此辨識為地理資料，並將它放入地圖中。</span><span class="sxs-lookup"><span data-stu-id="f9b27-137">Power BI automatically recognizes this is geographic data and put it in a map for you.</span></span>
   
    ![Power BI 對應圖][7]
2. <span data-ttu-id="f9b27-139">這個步驟會建立橫條圖，顯示每個客戶收入的銷售金額。</span><span class="sxs-lookup"><span data-stu-id="f9b27-139">This step creates a bar graph that shows amount of sales per customer income.</span></span> <span data-ttu-id="f9b27-140">若要建立此項，請移至展開的 AggregateSales 檢視。</span><span class="sxs-lookup"><span data-stu-id="f9b27-140">To create this go to the expanded AggregateSales view.</span></span> <span data-ttu-id="f9b27-141">按一下 [SalesAmount] 欄位。</span><span class="sxs-lookup"><span data-stu-id="f9b27-141">Click the SalesAmount field.</span></span> <span data-ttu-id="f9b27-142">將 [客戶收入] 欄位向左拖放到座標軸。</span><span class="sxs-lookup"><span data-stu-id="f9b27-142">Drag the Customer Income field to the left and drop it into Axis.</span></span>
   
    ![Power BI 選取軸][8]
   
    <span data-ttu-id="f9b27-144">我們已將橫條圖移到左邊。</span><span class="sxs-lookup"><span data-stu-id="f9b27-144">We moved the bar chart over the left.</span></span>
   
    ![Power BI 長條圖][9]
3. <span data-ttu-id="f9b27-146">這個步驟會建立折線圖，顯示每個訂單日期的銷售金額。</span><span class="sxs-lookup"><span data-stu-id="f9b27-146">This step creates a line chart that shows sales amount per order date.</span></span> <span data-ttu-id="f9b27-147">若要建立此項，請移至展開的 AggregateSales 檢視。</span><span class="sxs-lookup"><span data-stu-id="f9b27-147">To create this go to the expanded AggregateSales view.</span></span> <span data-ttu-id="f9b27-148">按一下 [SalesAmount] 和 [OrderDate]。</span><span class="sxs-lookup"><span data-stu-id="f9b27-148">Click SalesAmount and OrderDate.</span></span> <span data-ttu-id="f9b27-149">在 [視覺效果] 資料行中按一下 [折線圖] 圖示；這是視覺效果下第二行中的第一個圖示。</span><span class="sxs-lookup"><span data-stu-id="f9b27-149">In the Visualizations column click the Line Chart icon; this is the first icon in the second line under visualizations.</span></span>
   
    ![Power BI 選取折線圖][10]
   
    <span data-ttu-id="f9b27-151">您現在有一份報告，顯示資料的三種不同視覺效果。</span><span class="sxs-lookup"><span data-stu-id="f9b27-151">You now have a report that shows three different visualizations of the data.</span></span>
   
    ![Power BI 折線圖][11]

<span data-ttu-id="f9b27-153">您也可以隨時按一下 [檔案]，並選取 [儲存] 來儲存您的進度。</span><span class="sxs-lookup"><span data-stu-id="f9b27-153">You can save your progress at any time by clicking **File** and selecting **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9b27-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f9b27-154">Next steps</span></span>
<span data-ttu-id="f9b27-155">既然我們已經提供您一些時間，讓您利用範例資料進入狀況，接著請查看如何進行[開發][develop]、[載入][load]或[移轉][migrate]。</span><span class="sxs-lookup"><span data-stu-id="f9b27-155">Now that we've given you some time to warm up with the sample data, see how to [develop][develop], [load][load], or [migrate][migrate].</span></span> <span data-ttu-id="f9b27-156">或者，看一下 [Power BI 網站][Power BI website]。</span><span class="sxs-lookup"><span data-stu-id="f9b27-156">Or take a look at the [Power BI website][Power BI website].</span></span>

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
[connecting to SQL Data Warehouse]: sql-data-warehouse-integrate-power-bi.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md

<!--Other-->
[Azure portal]: https://portal.azure.com/
[Power BI website]: http://www.powerbi.com/
