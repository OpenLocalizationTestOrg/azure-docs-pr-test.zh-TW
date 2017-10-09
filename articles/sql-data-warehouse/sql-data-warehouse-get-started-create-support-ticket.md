---
title: "aaaHow toocreate SQL 資料倉儲的支援票證 |Microsoft 文件"
description: "如何 toocreate 支援票證中 Azure SQL 資料倉儲。"
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: a91d1f53-03cb-464b-9d5b-4a9c1a194ed3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 72f7eac82112fb7f1bfb05abca4ce40aeb3c828c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-support-ticket-for-sql-data-warehouse"></a>如何 toocreate 支援票證 SQL 資料倉儲
如果您的 SQL 資料倉儲有任何問題，請建立支援票證，以便我們的工程小組協助您。

> [!NOTE] 
> 從 2016/12/20，開始 hello Azure 入口網站中的 hello 資源健全狀況檢查不精確。 我們正積極 toofix 此問題。 


## <a name="create-a-support-ticket"></a>建立支援票證
1. 開啟 hello [Azure 入口網站][Azure portal]。
2. Hello 首頁畫面上，按一下 hello**說明 + 支援**磚。
   
    ![說明 + 支援](./media/sql-data-warehouse-get-started-create-support-ticket/help-support.png)
3. 在 hello 說明 + 支援刀鋒視窗中，按一下 **建立支援要求**。
   
    ![新增支援要求](./media/sql-data-warehouse-get-started-create-support-ticket/create-support-request.png)
   
    <a name="request-quota-change"></a> 
4. 選取 hello**要求類型**。
   
    ![要求類型](./media/sql-data-warehouse-get-started-create-support-ticket/request-type.png)
   
   > [!NOTE]
   > 根據預設，每個 SQL Server (例如 myserver.database.windows.net) 的 **DTU 配額** 為 45,000。 此配額僅是安全限制。 您可以藉由建立支援票證，並選取 增加配額*配額*hello 要求類型。 toocalculate 乘您 DTU 需求時，由 hello 總 hello 7.5 [DWU] [ DWU]所需。 例如，您想要 toohost 兩 DW6000s 上一個 SQL server，則您應該要求 90000 的 DTU 配額。  您可以在 hello 入口網站中檢視您目前的 DTU 耗用量的 hello SQL server 刀鋒視窗。 已暫停且未暫停資料庫會計入 hello DTU 配額。 
   > 
   > 
5. 選取 hello**訂用帳戶**主機 hello hello 解決問題，您所回報的資料庫。
   
    ![訂用帳戶](./media/sql-data-warehouse-get-started-create-support-ticket/subscription.png)
6. 選取**SQL 資料倉儲**為 hello 資源。
   
    ![資源](./media/sql-data-warehouse-get-started-create-support-ticket/resource.png)
7. 選取 [Azure 支援計劃][Azure support plan]。
   
   * **帳單、配額及訂用帳戶管理** 支援。
   * **協助修正**支援則透過[開發人員][Developer]、[標準][Standard]、[專業直導][Professional Direct]支援或[頂級][Premier]支援來提供。 中斷的修復問題會同時使用 Azure 客戶所發生的問題是合理預期，導致 Microsoft hello 問題。
   * **開發人員顧問**和**諮詢服務**位於 hello [Professional 直接][ Professional Direct]和[頂級][ Premier]支援層級。 
     
     如果您有頂級支援計劃，您也可以報告 SQL 資料倉儲相關問題上 hello [Microsoft Premier online 入口網站][Microsoft Premier online portal]。  請參閱[Azure 支援計劃][ Azure support plan] toolearn 深入了解各種支援計劃，包括範圍，回應時間、 定價，hello 等等。如需有關 Azure 支援的常見問題集，請參閱 [Azure 支援常見問題集][Azure support FAQs]。  
     
     ![支援計劃](./media/sql-data-warehouse-get-started-create-support-ticket/support-plan.png)
8. 選取 hello**問題類型**和**類別**。 我們已在此範例中，選擇 [工具] 當做 hello 問題類型和做為 hello 類別目錄的 「 用戶端工具 」。 
   
    ![問題類型類別](./media/sql-data-warehouse-get-started-create-support-ticket/problem-type-category.png)
9. 描述 hello 問題，然後選擇商務影響的 hello 層級。
   
    ![問題說明](./media/sql-data-warehouse-get-started-create-support-ticket/problem-description.png)
10. 將預先填入此支援票證的您的 **連絡資訊** 。 必要時更新此項目。
    
    ![連絡資訊](./media/sql-data-warehouse-get-started-create-support-ticket/contact-info.png)
11. 按一下**建立**toosubmit hello 支援要求。

## <a name="monitor-a-support-ticket"></a>監視支援票證
提交 hello 支援要求之後，hello Azure 支援小組會與您連絡。 toocheck 您要求的狀態和詳細資訊，請按一下**管理支援要求**hello 儀表板上。

![檢查狀態](./media/sql-data-warehouse-get-started-create-support-ticket/check-status.png)

## <a name="other-resources"></a>其他資源
此外，您可以連線以 hello SQL 資料倉儲社群上[堆疊溢位][ Stack Overflow]或 hello [Azure SQL 資料倉儲 MSDN 論壇][ Azure SQL Data Warehouse MSDN forum].

<!--Image references--> 

<!--Article references--> 
[DWU]: ./sql-data-warehouse-overview-what-is.md

<!--MSDN references--> 

<!--Other web references--> 
[Azure portal]: https://portal.azure.com/
[Azure support plan]: https://azure.microsoft.com/support/plans/?WT.mc_id=Support_Plan_510979/  
[Developer]: https://azure.microsoft.com/support/plans/developer/  
[Standard]: https://azure.microsoft.com/support/plans/standard/  
[Professional Direct]: https://azure.microsoft.com/support/plans/prodirect/  
[Premier]: https://azure.microsoft.com/support/plans/premier/  
[Azure support FAQs]: https://azure.microsoft.com/support/faq/
[Microsoft Premier online portal]: https://premier.microsoft.com/
[Stack Overflow]: https://stackoverflow.com/questions/tagged/azure-sqldw/
[Azure SQL Data Warehouse MSDN forum]: https://social.msdn.microsoft.com/Forums/home?forum=AzureSQLDataWarehouse/

