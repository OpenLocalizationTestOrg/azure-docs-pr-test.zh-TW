---
title: "aaaConnect tooAzure SQL 資料倉儲-SSMS |Microsoft 文件"
description: "使用 SQL Server Management Studio (SSMS) tooconnect tooand 查詢 Azure SQL 資料倉儲。"
services: sql-data-warehouse
documentationcenter: 
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 299e50b3-e68a-471c-8aee-b0b9874781bd
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: bcbaf7139d2e5183b388b8d58c015cf5ad726722
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-sql-server-management-studio-ssms"></a>使用 SQL Server Management Studio (SSMS) 連接 tooSQL 資料倉儲
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

使用 SQL Server Management Studio (SSMS) tooconnect tooand 查詢 Azure SQL 資料倉儲。 

## <a name="prerequisites"></a>必要條件
toouse 本教學課程中，您需要：

* 現有的 SQL 資料倉儲。 toocreate 其中一個，請參閱[建立 SQL 資料倉儲][Create a SQL Data Warehouse]。
* SQL Server Management Studio (SSMS) 已安裝。 如果您尚未安裝，可以免費[安裝 SSMS][Install SSMS]。
* hello 完整 SQL server 名稱。 toofind，請參閱[連接 tooSQL 資料倉儲][Connect tooSQL Data Warehouse]。

## <a name="1-connect-tooyour-sql-data-warehouse"></a>1.連接 tooyour SQL 資料倉儲
1. 開啟 SSMS。
2. 開啟物件總管。 toodo 這個，請選取**檔案** > **連接物件總管**。
   
    ![SQL Server 物件總管][1]
3. 填寫 hello 連接 tooServer 視窗中的 hello 欄位。
   
    ![連接 tooServer][2]
   
   * **伺服器名稱**。 輸入 hello**伺服器名稱**先前所識別。
   * **驗證**。 選取 [SQL Server 驗證] 或 [Active Directory 整合式驗證]。
   * [使用者名稱] 和 [密碼]。 如果上面已選取 [SQL Server 驗證]，請輸入使用者名稱和密碼。
   * 按一下 [ **連接**]。
4. tooexplore，展開您的 Azure SQL server。 您可以檢視 hello hello 伺服器相關聯的資料庫。 展開範例資料庫 AdventureWorksDW toosee hello 資料表。
   
    ![探索 AdventureWorksDW][3]

## <a name="2-run-a-sample-query"></a>2.執行範例查詢
現在，連線已建立的 tooyour 資料庫，讓我們來撰寫查詢。

1. 在 [SQL Server 物件總管] 中您的資料庫上按一下滑鼠右鍵。
2. 選取 [新增查詢] 。 新的查詢視窗隨即開啟。
   
    ![新增查詢][4]
3. 將這個 TSQL 查詢複製到查詢視窗中 hello:
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. 執行 hello 查詢。 toodo 此，依序按一下`Execute`或使用 hello 下列快顯： `F5`。
   
    ![執行查詢][5]
5. 查看 hello 查詢結果。 在此範例中，hello FactInternetSales 資料表會有 60398 資料列。
   
    ![查詢結果][6]

## <a name="next-steps"></a>後續步驟
現在，您可以連接並查詢，再試一次[視覺化 hello 資料與 PowerBI][visualizing hello data with PowerBI]。

tooconfigure 環境以使用 Azure Active Directory 驗證，請參閱[驗證資料倉儲 tooSQL][Authenticate tooSQL Data Warehouse]。

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md 

<!--Other-->
[Azure portal]: https://portal.azure.com
[Install SSMS]: https://msdn.microsoft.com/en-US/library/hh213248.aspx


<!--Image references-->

[1]: media/sql-data-warehouse-query-ssms/connect-object-explorer.png
[2]: media/sql-data-warehouse-query-ssms/connect-object-explorer1.png
[3]: media/sql-data-warehouse-query-ssms/explore-tables.png
[4]: media/sql-data-warehouse-query-ssms/new-query.png
[5]: media/sql-data-warehouse-query-ssms/execute-query.png
[6]: media/sql-data-warehouse-query-ssms/results.png
