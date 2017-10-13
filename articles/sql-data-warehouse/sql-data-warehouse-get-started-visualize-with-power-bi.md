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
# <a name="visualize-data-with-power-bi"></a>使用 Power BI 視覺化資料
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

本教學課程會示範如何使用 Power BI 來連接到 SQL 資料倉儲，並建立一些基本的視覺效果。

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Data-Warehouse-Sample-Data-and-PowerBI/player]
> 
> 

## <a name="prerequisites"></a>必要條件
若要逐步執行本教學課程，您需要：

* 預先載入 AdventureWorksDW 資料庫的 SQL 資料倉儲。 若要進行佈建，請參閱[建立 SQL 資料倉儲][Create a SQL Data Warehouse]並選擇載入範例資料。 如果您已經有資料倉儲但沒有範例資料，您可以[手動載入範例資料][load sample data manually]。

## <a name="1-connect-to-your-database"></a>1.連接到您的資料庫
若要開啟 Power BI 並連接到您的 AdventureWorksDW 資料庫：

1. 登入 [Azure 入口網站][Azure portal]。
2. 按一下 [SQL 資料庫]  ，並選擇您的 AdventureWorks SQL 資料倉儲資料庫。
   
    ![尋找您的資料庫][1]
3. 按一下 [在 Power BI 中開啟] 按鈕。
   
    ![Power BI 按鈕][2]
4. 您現在應該會看到 SQL 資料倉儲連接頁面顯示您的資料庫網址。 按 [下一步]。
   
    ![Power BI 連接][3]
5. 輸入您的 Azure SQL Server 使用者名稱和密碼，隨後會將您完全連接到 SQL 資料倉儲資料庫。
   
    ![Power BI 登入][4]
6. 一旦登入了 Power BI，請在左刀鋒視窗上按一下  AdventureWorksDW 資料集。 這會開啟資料庫。
   
    ![Power BI 開啟 AdventureWorksDW][5]

## <a name="2-create-a-report"></a>2.建立報表
您現在已準備好使用 Power BI 來分析 AdventureWorksDW 範例資料。 為了執行分析，AdventureWorksDW 有一個稱為 AggregateSales 的檢視。 這個檢視包含用來分析公司銷售的一些重要指標。

1. 若要根據郵遞區號建立銷售金額的對應圖，請在右手邊欄位窗格中按一下 AggregateSales 檢視以展開它。 按一下 [PostalCode] 和 [SalesAmount] 資料行來選取它們。
   
    ![Power BI 選取 AggregateSales][6]
   
    Power BI 會自動將此辨識為地理資料，並將它放入地圖中。
   
    ![Power BI 對應圖][7]
2. 這個步驟會建立橫條圖，顯示每個客戶收入的銷售金額。 若要建立此項，請移至展開的 AggregateSales 檢視。 按一下 [SalesAmount] 欄位。 將 [客戶收入] 欄位向左拖放到座標軸。
   
    ![Power BI 選取軸][8]
   
    我們已將橫條圖移到左邊。
   
    ![Power BI 長條圖][9]
3. 這個步驟會建立折線圖，顯示每個訂單日期的銷售金額。 若要建立此項，請移至展開的 AggregateSales 檢視。 按一下 [SalesAmount] 和 [OrderDate]。 在 [視覺效果] 資料行中按一下 [折線圖] 圖示；這是視覺效果下第二行中的第一個圖示。
   
    ![Power BI 選取折線圖][10]
   
    您現在有一份報告，顯示資料的三種不同視覺效果。
   
    ![Power BI 折線圖][11]

您也可以隨時按一下 [檔案]，並選取 [儲存] 來儲存您的進度。

## <a name="next-steps"></a>後續步驟
既然我們已經提供您一些時間，讓您利用範例資料進入狀況，接著請查看如何進行[開發][develop]、[載入][load]或[移轉][migrate]。 或者，看一下 [Power BI 網站][Power BI website]。

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
