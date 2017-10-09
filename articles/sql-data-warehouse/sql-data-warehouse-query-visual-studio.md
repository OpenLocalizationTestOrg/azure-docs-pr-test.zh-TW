---
title: "aaaConnect tooAzure SQL 資料倉儲-VSTS |Microsoft 文件"
description: "使用 Visual Studio 查詢 SQL 資料倉儲。"
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: daace889-95e5-4826-b2fc-047eac9d6d95
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 55eef4dff3e0647be5a735295bc89b43eb456079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-visual-studio-and-ssdt"></a>與 Visual Studio 和 SSDT 連接 tooSQL 資料倉儲
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

使用 Visual Studio tooquery Azure SQL 資料倉儲短短幾分鐘內。 這個方法會使用 Visual Studio 中的 hello SQL Server Data Tools (SSDT) 延伸模組。 

## <a name="prerequisites"></a>必要條件
toouse 本教學課程中，您需要：

* 現有的 SQL 資料倉儲。 toocreate 其中一個，請參閱[建立 SQL 資料倉儲][Create a SQL Data Warehouse]。
* 適用於 Visual Studio 的 SSDT。 如果您有 Visual Studio，您可能已經有此 SSDT。 如需安裝指示和選項，請參閱 [安裝 Visual Studio 和 SSDT][Installing Visual Studio and SSDT]。
* hello 完整 SQL server 名稱。 toofind，請參閱[連接 tooSQL 資料倉儲][Connect tooSQL Data Warehouse]。

## <a name="1-connect-tooyour-sql-data-warehouse"></a>1.連接 tooyour SQL 資料倉儲
1. 開啟 Visual Studio 2013 或 2015。
2. 開啟 [SQL Server 物件總管]。 toodo 這個，請選取**檢視** > **SQL Server 物件總管**。
   
    ![SQL Server 物件總管][1]
3. 按一下 hello**加入 SQL Server**圖示。
   
    ![加入 SQL Server][2]
4. 填寫 hello 連接 tooServer 視窗中的 hello 欄位。
   
    ![連接 tooServer][3]
   
   * **伺服器名稱**。 輸入 hello**伺服器名稱**先前所識別。
   * **驗證**。 選取 [SQL Server 驗證] 或 [Active Directory 整合式驗證]。
   * [使用者名稱] 和 [密碼]。 如果上面已選取 [SQL Server 驗證]，請輸入使用者名稱和密碼。
   * 按一下 [ **連接**]。
5. tooexplore，展開您的 Azure SQL server。 您可以檢視 hello hello 伺服器相關聯的資料庫。 展開範例資料庫 AdventureWorksDW toosee hello 資料表。
   
    ![探索 AdventureWorksDW][4]

## <a name="2-run-a-sample-query"></a>2.執行範例查詢
現在，連線已建立的 tooyour 資料庫，讓我們來撰寫查詢。

1. 在 [SQL Server 物件總管] 中您的資料庫上按一下滑鼠右鍵。
2. 選取 [新增查詢] 。 新的查詢視窗隨即開啟。
   
    ![新增查詢][5]
3. 將這個 TSQL 查詢複製到查詢視窗中 hello:
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. 執行 hello 查詢。 toodo，按一下 hello 綠色箭號，或使用下列捷徑 hello: `CTRL` + `SHIFT` + `E`。
   
    ![執行查詢][6]
5. 查看 hello 查詢結果。 在此範例中，hello FactInternetSales 資料表會有 60398 資料列。
   
    ![查詢結果][7]

## <a name="next-steps"></a>後續步驟
現在，您可以連接並查詢，再試一次[視覺化 hello 資料與 PowerBI][visualizing hello data with PowerBI]。

tooconfigure 環境以使用 Azure Active Directory 驗證，請參閱[驗證資料倉儲 tooSQL][Authenticate tooSQL Data Warehouse]。

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md  

<!--Other-->
[Azure portal]: https://portal.azure.com

<!--Image references-->

[1]: media/sql-data-warehouse-query-visual-studio/open-ssdt.png
[2]: media/sql-data-warehouse-query-visual-studio/add-server.png
[3]: media/sql-data-warehouse-query-visual-studio/connection-dialog.png
[4]: media/sql-data-warehouse-query-visual-studio/explore-sample.png
[5]: media/sql-data-warehouse-query-visual-studio/new-query2.png
[6]: media/sql-data-warehouse-query-visual-studio/run-query.png
[7]: media/sql-data-warehouse-query-visual-studio/query-results.png
