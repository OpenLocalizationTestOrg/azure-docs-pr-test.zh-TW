---
title: "aaaLoad 資料從 SQL Server 到 Azure SQL 資料倉儲 (SSIS) |Microsoft 文件"
description: "示範如何從各種不同的資料的 SQL Server Integration Services (SSIS) 封裝 toomove 資料 toocreate 來源 tooSQL 資料倉儲。"
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: e2c252e9-0828-47c2-a808-e3bea46c134a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 03/30/2017
ms.author: cakarst;douglasl;barbkess
ms.openlocfilehash: bb28a08807a5b07832b85f2f074c2acf912c1dc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-ssis"></a>將資料從 SQL Server 載入 Azure SQL 資料倉儲 (SSIS)
> [!div class="op_single_selector"]
> * [SSIS](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [PolyBase](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [bcp](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

從 SQL Server 中建立 SQL Server Integration Services (SSIS) 封裝 tooload 資料到 Azure SQL 資料倉儲中。 您可以選擇性地重建、 轉換及清理 hello 資料通過 hello SSIS 資料流程。

在本教學課程中，您將：

* 在 Visual Studio 中建立新的整合服務專案
* 連接 toodata 來源，包括 SQL Server （做為來源） 和 SQL 資料倉儲 （做為目的地）。
* 設計 hello 來源中的資料載入 hello 目的地的 SSIS 封裝。
* 執行 hello SSIS 封裝 tooload hello 資料。

本教學課程會使用 SQL Server 作為 hello 資料來源。 SQL Server 可在內部部署或在 Azure 虛擬機器上執行。

## <a name="basic-concepts"></a>基本概念
hello 封裝是工作的 hello 在 SSIS 中單位。 相關的封裝集成群組則為專案。 在 Visual Studio 中使用 SQL Server Data Tools 建立專案和設計封裝。 hello 設計程序是視覺化的程序中您拖放元件 hello 工具箱 toohello 設計介面，從連接它們，並設定其屬性。 完成您的封裝之後，您可以選擇性地部署 tooSQL 伺服器的全方位管理、 監視及安全性。

## <a name="options-for-loading-data-with-ssis"></a>以 SSIS 載入資料的選項
SQL Server Integration Services (SSIS) 是彈性的工具組合，提供連接至 SQL 資料倉儲、並將資料載入 SQL 資料倉儲的各種選項。

1. 使用 ADO NET 目的地 tooconnect tooSQL 資料倉儲。 本教學課程會使用 ADO NET 目的地，因為它有 hello 最少的組態選項。
2. 使用 OLE DB 目的地 tooconnect tooSQL 資料倉儲。 這個選項可能會提供稍微較佳的效能比 hello ADO NET 目的地。
3. 使用 Azure Blob 儲存體中的 hello Azure Blob 上傳工作 toostage hello 資料。 然後，使用 hello SSIS 執行 SQL 工作 toolaunch hello 資料載入 SQL 資料倉儲 Polybase 指令碼。 此選項提供 hello 的 hello 此處所列的三個選項的最佳效能。 tooget hello Azure Blob 上傳工作，下載 hello [Microsoft SQL Server 2016 Integration Services 功能套件 azure][Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]。 toolearn 深入了解 Polybase，請參閱[PolyBase 指南][PolyBase Guide]。

## <a name="before-you-start"></a>開始之前
在本教學課程 toostep，您需要：

1. **SQL Server Integration Services (SSIS)**。 SSIS 是 SQL Server 的元件，需有試用版或授權版的 SQL Server。 tooget 評估版的 SQL Server 2016 Preview，請參閱[SQL Server 評估版][SQL Server Evaluations]。
2. **Visual Studio**。 tooget hello 免費的 Visual Studio Community Edition，請參閱[Visual Studio Community][Visual Studio Community]。
3. **SQL Server Data Tools for Visual Studio (SSDT)**。 tooget SQL Server Data Tools for Visual Studio，請參閱[下載 SQL Server Data Tools (SSDT)][Download SQL Server Data Tools (SSDT)]。
4. **範例資料**。 本教學課程使用範例資料為 hello 載入 SQL 資料倉儲的來源資料 toobe hello AdventureWorks 範例資料庫中儲存在 SQL Server。 tooget hello AdventureWorks 範例資料庫，請參閱[AdventureWorks 2014 範例資料庫][AdventureWorks 2014 Sample Databases]。
5. **SQL 資料倉儲資料庫和權限**。 本教學課程 tooa SQL 資料倉儲執行個體連接並載入資料。 您有 toohave 權限 toocreate 資料表和 tooload 資料。
6. **防火牆規則**。 Toocreate 防火牆規則含有上有 SQL 資料倉儲 hello 您本機電腦的 IP 位址之前，您可以上傳資料 toohello SQL 資料倉儲。

## <a name="step-1-create-a-new-integration-services-project"></a>步驟 1：建立新的 Integration Services 專案
1. 啟動 Visual Studio。
2. 在 hello**檔案**功能表上，選取**新增 |專案**。
3. 瀏覽 toohello**已安裝 |範本 |Business Intelligence |Integration Services**專案類型。
4. 選取 [整合服務專案] 。 提供 [名稱] 和 [位置] 的值，然後選取 [確定]。

Visual Studio 隨即開啟，並建立新的整合服務 (SSIS) 專案。 然後 Visual Studio 會在 hello 專案開啟 hello hello 單一新的 SSIS 封裝 (Package.dtsx) 的設計工具。 您會看到下列畫面區域的 hello:

* Hello 左側 hello**工具箱**的 SSIS 元件。
* Hello 中間 hello 與多個索引標籤的設計介面。 您通常會使用至少 hello**控制流程**和 hello**資料流程**索引標籤。
* 在右邊的 hello，hello**方案總管 中**和 hello**屬性**窗格。
  
    ![][01]

## <a name="step-2-create-hello-basic-data-flow"></a>步驟 2： 建立 hello 基本資料流程
1. 資料流程工作拖曳 hello 設計介面的 hello 工具箱 toohello 中心 (在 hello**控制流程** 索引標籤)。
   
    ![][02]
2. 按兩下 hello Data Flow Task tooswitch toohello 資料流程 索引標籤。
3. 從 hello [其他來源] 清單中 hello 工具箱，拖曳 ADO.NET 來源 toohello 設計介面。 Hello 仍已選取的來源配接器，變更其名稱太**SQL Server 來源**在 hello**屬性**窗格。
4. 從 hello 工具箱中的 hello 其他目的地清單，拖曳 hello ADO.NET 來源下的 ADO.NET 目的地 toohello 設計介面。 Hello 仍已選取的目的地配接器，變更其名稱太**SQL DW 目的地**在 hello**屬性**窗格。
   
    ![][09]

## <a name="step-3-configure-hello-source-adapter"></a>步驟 3： 設定 hello 來源配接器
1. 按兩下 hello 來源配接器 tooopen hello **ADO.NET 來源編輯器**。
   
    ![][03]
2. 在 hello**連線管理員**hello 索引標籤**ADO.NET 來源編輯器**，按一下 hello**新增**按鈕的下一個 toohello **ADO.NET 連接管理員**清單 tooopen hello**設定 ADO.NET 連接管理員**對話方塊並建立本教學課程將資料載入從中 hello SQL Server 資料庫的連接設定。
   
    ![][04]
3. 在 hello**設定 ADO.NET 連接管理員**對話方塊方塊中，按一下 hello**新增**按鈕 tooopen hello**連線管理員**對話方塊並建立新的資料連接。
   
    ![][05]
4. 在 hello**連線管理員**對話方塊方塊中，執行下列項目 hello。
   
   1. 如**提供者**，選取 hello SqlClient 資料提供者。
   2. 如**伺服器名稱**，輸入 hello SQL Server 名稱。
   3. 在 hello **toohello 伺服器上的記錄**區段中，選取或輸入驗證資訊。
   4. 在 hello**連接 tooa 資料庫**區段中，選取 hello AdventureWorks 範例資料庫。
   5. 按一下 [測試連接] 。
      
       ![][06]
   6. 在 報告 hello hello 連線測試結果的 hello 對話方塊中，按一下 **確定**tooreturn toohello**連接管理員** 對話方塊。
   7. 在 hello**連接管理員**對話方塊中，按一下 [**確定**tooreturn toohello**設定 ADO.NET 連接管理員**] 對話方塊。
5. 在 hello**設定 ADO.NET 連接管理員**對話方塊中，按一下**確定**tooreturn toohello **ADO.NET 來源編輯器**。
6. 在 hello **ADO.NET 來源編輯器**，在 hello **hello 資料表或檢視 hello 名稱**清單中，選取 hello **Sales.SalesOrderDetail**資料表。
   
    ![][07]
7. 按一下**預覽**toosee hello hello hello 中的來源資料表中資料的前 200 個資料列**預覽 Query Results**  對話方塊。
   
    ![][08]
8. 在 hello**預覽 Query Results**對話方塊中，按一下 **關閉**tooreturn toohello **ADO.NET 來源編輯器**。
9. 在 hello **ADO.NET 來源編輯器**，按一下**確定**toofinish 設定 hello 資料來源。

## <a name="step-4-connect-hello-source-adapter-toohello-destination-adapter"></a>步驟 4： 連接 hello 來源配接器 toohello 目的地配接器
1. 選取 hello hello 設計介面上的來源配接器。
2. 選取 hello 來源配接器從延伸的 hello 藍色箭號，並將它拖曳 toohello 目的地編輯器，直到它的地方貼齊。
   
    ![][10]
   
    在典型的 SSIS 封裝中，您可以使用其他元件從 hello SSIS 工具箱 之間 hello 來源和 hello 目的地 toorestructure、 轉換的數字，並清理通過 hello SSIS 資料流程的資料。 tookeep 越簡單越好這個範例中，我們正在連接 hello 直接來源 toohello 目的地。

## <a name="step-5-configure-hello-destination-adapter"></a>步驟 5： 設定 hello 目的地配接器
1. 按兩下 hello 目的地配接器 tooopen hello **ADO.NET 目的地編輯器**。
   
    ![][11]
2. 在 hello**連線管理員**hello 索引標籤**ADO.NET 目的地編輯器**，按一下 hello**新增**按鈕的下一個 toohello**連線管理員**清單 tooopen hello**設定 ADO.NET 連接管理員**對話方塊並建立本教學課程將資料載入到其中的 hello Azure SQL 資料倉儲資料庫的連接設定。
3. 在 hello**設定 ADO.NET 連接管理員**對話方塊方塊中，按一下 hello**新增**按鈕 tooopen hello**連線管理員**對話方塊並建立新的資料連接。
4. 在 hello**連線管理員**對話方塊方塊中，執行下列項目 hello。
   1. 如**提供者**，選取 hello SqlClient 資料提供者。
   2. 如**伺服器名稱**，輸入 hello SQL 資料倉儲的名稱。
   3. 在 hello **toohello 伺服器上的記錄**區段中，選取**使用 SQL Server 驗證**並輸入驗證資訊。
   4. 在 hello**連接 tooa 資料庫**區段中，選取現有的 SQL 資料倉儲資料庫。
   5. 按一下 [測試連接] 。
   6. 在 報告 hello hello 連線測試結果的 hello 對話方塊中，按一下 **確定**tooreturn toohello**連接管理員** 對話方塊。
   7. 在 hello**連接管理員**對話方塊中，按一下 [**確定**tooreturn toohello**設定 ADO.NET 連接管理員**] 對話方塊。
5. 在 hello**設定 ADO.NET 連接管理員**對話方塊中，按一下**確定**tooreturn toohello **ADO.NET 目的地編輯器**。
6. 在 hello **ADO.NET 目的地編輯器**，按一下 **新增**下一步 toohello**使用資料表或檢視**清單 tooopen hello **Create Table**對話方塊toocreate 具有符合 hello 來源資料表的資料行清單的新目的地資料表。
   
    ![][12a]
7. 在 hello **Create Table**對話方塊方塊中，執行下列項目 hello。
   
   1. 變更 hello hello 目的地資料表名稱太**SalesOrderDetail**。
   2. 移除 hello **rowguid**資料行。 hello **uniqueidentifier** SQL 資料倉儲中不支援資料類型。
   3. 變更資料型別 hello hello **LineTotal**資料行太**money**。 hello**十進位**SQL 資料倉儲中不支援資料類型。 如需支援的資料類型資訊，請參閱[建立資料表 (Azure SQL 資料倉儲，平行資料倉儲)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)]。
      
       ![][12b]
   4. 按一下**確定**toocreate hello 資料表並傳回 toohello **ADO.NET 目的地編輯器**。
8. 在 hello **ADO.NET 目的地編輯器**，選取 hello**對應**toosee 索引標籤上 hello 來源中的資料行的方式對應 toocolumns hello 目的地中的。
   
    ![][13]
9. 按一下**確定**toofinish 設定 hello 資料來源。

## <a name="step-6-run-hello-package-tooload-hello-data"></a>步驟 6： 執行 hello 封裝 tooload hello 資料
依序按一下 hello 執行的 hello 封裝**啟動**按鈕 hello 工具列上，或選取其中一個 hello**執行**hello 選項**偵錯**功能表。

Hello 封裝開始 toorun，您會看到黃色旋轉滾輪 tooindicate 活動與 hello 處理資料列數目為止。

![][14]

當 hello 封裝完成執行時，您看到綠色的核取記號 tooindicate 成功以及 hello 從 hello 來源 toohello 目的地載入資料的資料列總數。

![][15]

恭喜！ 您已成功使用 SQL Server Integration Services tooload 資料到 Azure SQL 資料倉儲。

## <a name="next-steps"></a>後續步驟
* 深入了解 SSIS 資料流程 hello。 從這裡開始：[資料流程][Data Flow]。
* 深入了解如何 toodebug 和疑難排解您在 hello 設計環境中的封裝權限。 從這裡開始：[套件開發的疑難排解工具][Troubleshooting Tools for Package Development]。
* 了解 toodeploy 您 SSIS 專案，並封裝 tooIntegration 服務伺服器或 tooanother 儲存位置。 從這裡開始：[部署專案和套件][Deployment of Projects and Packages]。

<!-- Image references -->
[01]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-designer-01.png
[02]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-data-flow-task-02.png
[03]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-03.png
[04]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-manager-04.png
[05]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-05.png
[06]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/test-connection-06.png
[07]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-07.png
[08]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/preview-data-08.png
[09]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/source-destination-09.png
[10]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/connect-source-destination-10.png
[11]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-destination-11.png
[12a]: ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-before-12a.png
[12b]: ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-after-12b.png
[13]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/column-mapping-13.png
[14]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-running-14.png
[15]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-success-15.png

<!-- Article references -->

<!-- MSDN references -->
[PolyBase Guide]: https://msdn.microsoft.com/library/mt143171.aspx
[Download SQL Server Data Tools (SSDT)]: https://msdn.microsoft.com/library/mt204009.aspx
[CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)]: https://msdn.microsoft.com/library/mt203953.aspx
[Data Flow]: https://msdn.microsoft.com/library/ms140080.aspx
[Troubleshooting Tools for Package Development]: https://msdn.microsoft.com/library/ms137625.aspx
[Deployment of Projects and Packages]: https://msdn.microsoft.com/library/hh213290.aspx

<!--Other Web references-->
[Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]: http://go.microsoft.com/fwlink/?LinkID=626967
[SQL Server Evaluations]: https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016
[Visual Studio Community]: https://www.visualstudio.com/en-us/products/visual-studio-community-vs.aspx
[AdventureWorks 2014 Sample Databases]: https://msftdbprodsamples.codeplex.com/releases/view/125550
