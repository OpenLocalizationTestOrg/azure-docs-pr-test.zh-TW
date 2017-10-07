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
# <a name="visualize-data-with-power-bi"></a>使用 Power BI 視覺化資料
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

本教學課程示範如何 toouse Power BI tooconnect tooSQL 資料倉儲，並建立一些基本的視覺效果。

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Data-Warehouse-Sample-Data-and-PowerBI/player]
> 
> 

## <a name="prerequisites"></a>必要條件
在本教學課程 toostep，您需要：

* SQL 資料倉儲預先載入與 hello AdventureWorksDW 資料庫。 tooprovision，請參閱[建立 SQL 資料倉儲][ Create a SQL Data Warehouse]選擇 tooload hello 範例資料。 如果您已經有資料倉儲但沒有範例資料，您可以[手動載入範例資料][load sample data manually]。

## <a name="1-connect-tooyour-database"></a>1.連接 tooyour 資料庫
tooopen Power BI，並連接 tooyour AdventureWorksDW 資料庫：

1. 登入 hello [Azure 入口網站][Azure portal]。
2. 按一下 [SQL 資料庫]  ，並選擇您的 AdventureWorks SQL 資料倉儲資料庫。
   
    ![尋找您的資料庫][1]
3. 按一下 hello 'Power BI 中開啟 按鈕。
   
    ![Power BI 按鈕][2]
4. 您現在應該會看到 hello SQL 資料倉儲連接頁面顯示您資料庫的網址。 按 [下一步]。
   
    ![Power BI 連接][3]
5. 輸入您的 Azure SQL server 使用者名稱和密碼，然後您將無法完全連接的 tooyour SQL 資料倉儲資料庫。
   
    ![Power BI 登入][4]
6. 一旦您已登入 Power BI 中，按一下 hello 左刀鋒視窗上的 hello AdventureWorksDW 資料集。 這會開啟 hello 資料庫。
   
    ![Power BI 開啟 AdventureWorksDW][5]

## <a name="2-create-a-report"></a>2.建立報表
您會立即準備 toouse Power BI tooanalyze AdventureWorksDW 範例資料。 tooperform hello 分析 AdventureWorksDW 有一個稱為 AggregateSales 的檢視。 這個檢視包含幾個 hello 分析 hello hello 公司銷售的關鍵計量。

1. 按一下 [hello AggregateSales 檢視 tooexpand toocreate 的銷售量 toopostal 的程式碼中，在 hello 右邊的欄位] 窗格中，根據對應它。 按一下 hello [郵遞區號] 和 [salesamount] 資料行 tooselect 它們。
   
    ![Power BI 選取 AggregateSales][6]
   
    Power BI 會自動將此辨識為地理資料，並將它放入地圖中。
   
    ![Power BI 對應圖][7]
2. 這個步驟會建立橫條圖，顯示每個客戶收入的銷售金額。 toocreate 此移 toohello 展開 AggregateSales 檢視。 按一下 hello [salesamount] 欄位。 Hello 客戶收入欄位 toohello 向左拖曳，並將其放置到座標軸。
   
    ![Power BI 選取軸][8]
   
    我們透過 hello 左移動 hello 橫條圖。
   
    ![Power BI 長條圖][9]
3. 這個步驟會建立折線圖，顯示每個訂單日期的銷售金額。 toocreate 此移 toohello 展開 AggregateSales 檢視。 按一下 [SalesAmount] 和 [OrderDate]。 Hello 視覺效果的資料行中按一下 hello 折線圖圖示。這是在視覺效果的 hello 第二行 hello 第一個圖示。
   
    ![Power BI 選取折線圖][10]
   
    您現在有顯示 hello 資料的三個不同的視覺效果的報表。
   
    ![Power BI 折線圖][11]

您也可以隨時按一下 [檔案]，並選取 [儲存] 來儲存您的進度。

## <a name="next-steps"></a>後續步驟
現在，我們提供了一些時間 toowarm hello 範例資料，請參閱如何太[開發][develop]，[載入][load]，或[移轉][migrate]。 看看 hello 或者[Power BI 網站][Power BI website]。

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
