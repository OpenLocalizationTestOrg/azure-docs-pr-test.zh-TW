---
title: "aaaCreate hello Azure 入口網站中的 SQL 資料倉儲 |Microsoft 文件"
description: "了解如何 toocreate Azure SQL 資料倉儲中的 hello Azure 入口網站"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: 552e496e-d560-419c-9996-6bbc80c521cb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: f5be6e3f2936e3af9d099854a468f8ce66fd8fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-sql-data-warehouse"></a>建立 Azure SQL 資料倉儲
> [!div class="op_single_selector"]
> * [Azure 入口網站](sql-data-warehouse-get-started-provision.md)
> * [TSQL](sql-data-warehouse-get-started-create-database-tsql.md)
> * [PowerShell](sql-data-warehouse-get-started-provision-powershell.md)
>
>

本教學課程使用 hello Azure 入口網站 toocreate 包含 AdventureWorksDW 範例資料庫的 SQL 資料倉儲。

## <a name="prerequisites"></a>必要條件
tooget 開始，您需要：

* **Azure 帳戶**： 瀏覽[Azure 免費試用][ Azure Free Trial]或[MSDN Azure 信用額度][ MSDN Azure Credits] toocreate 帳戶。
* **Azure SQL server**： 請參閱[以 hello Azure 入口網站建立 Azure SQL database] [ Create an Azure SQL database in hello Azure portal]如需詳細資訊。

> [!NOTE]
> 建立 SQL 資料倉儲可能會導致新的可計費服務。  如需詳細資訊，請參閱 [SQL 資料倉儲價格][SQL Data Warehouse pricing]。
>
>

## <a name="create-a-sql-data-warehouse"></a>建立 SQL 資料倉儲
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 按一下 [+ 新增] > [資料庫] > [SQL 資料倉儲]。

    ![建立](./media/sql-data-warehouse-get-started-provision/create-sample.gif)
3. 在 hello **SQL 資料倉儲**刀鋒視窗中，填入 hello 所需資訊，然後按 建立 5d toocreate。

    ![建立資料庫](./media/sql-data-warehouse-get-started-provision/create-database.png)

   * **伺服器**︰我們建議您先選取您的伺服器。  
   * **資料庫名稱**: hello 為使用的 tooreference hello SQL 資料倉儲的名稱。  它必須是唯一的 toohello 伺服器。
   * **效能**：我們建議從 400 [DWU][DWU] 開始。 您可以移動保留的 hello 滑桿 toohello，或以滑鼠右鍵 tooadjust hello 效能資料倉儲或小數位數的向上或向下建立之後。  toolearn 深入了解 dwu 調整，請參閱我們的文件上[調整](sql-data-warehouse-manage-compute-overview.md)或我們[定價頁面][SQL Data Warehouse pricing]。
   * **訂用帳戶**： 選取 hello[訂用帳戶]，將付款人此 SQL 資料倉儲。
   * **資源群組**:[資源群組][ Resource group]所設計的容器 toohelp 管理 Azure 資源的集合。 深入了解[資源群組](../azure-resource-manager/resource-group-overview.md)。
   * **選取來源**：按一下 [選取來源] > [範例]。 Azure 會自動填入 hello**選取範例**AdventureWorksDW 的選項。

   > [!NOTE]
   > hello SQL 資料倉儲的預設定序為 SQL_Latin1_General_CP1_CI_AS。 如果需要不同的定序， [T-SQL] [ T-SQL]可以是使用的 toocreate hello 資料庫具有不同的定序。
   >
   >

1. 按一下**建立**toocreate SQL 資料倉儲。
2. 等候幾分鐘的時間。 準備您的資料倉儲時，您應該傳回 toohello [Azure 入口網站](https://portal.azure.com)。 您可以尋找您的 SQL 資料倉儲儀表板上，列在您的 SQL 資料庫，或在 hello 資源群組，您使用 toocreate 它。

    ![入口網站檢視](./media/sql-data-warehouse-get-started-provision/database-portal-view.png)

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="next-steps"></a>後續步驟
現在您已經建立 SQL 資料倉儲，您就可以準備太[連接](sql-data-warehouse-connect-overview.md)並開始查詢。

tooload 資料到 SQL 資料倉儲，請參閱 hello[載入概觀](sql-data-warehouse-overview-load.md)。

如果您嘗試 toomigrate 現有的資料庫 tooSQL 資料倉儲時，請參閱 hello[移轉概觀](sql-data-warehouse-overview-migrate.md)或使用[移轉公用程式](sql-data-warehouse-migrate-migration-utility.md)。

也可以使用 Transact-SQL 來設定防火牆規則。 如需詳細資訊，請參閱 [sp_set_firewall_rule][sp_set_firewall_rule] 和 [sp_set_database_firewall_rule][sp_set_database_firewall_rule]。

它也是很好的想法 toolook 在 hello[最佳做法][Best practices]。

<!--Article references-->
[Create an Azure SQL database in hello Azure portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[resource groups]: ../azure-resource-manager/resource-group-template-deploy-portal.md
[Best practices]: sql-data-warehouse-best-practices.md
[DWU]: sql-data-warehouse-overview-what-is.md
[訂用帳戶]: ../azure-glossary-cloud-terminology.md#subscription
[resource group]: ../azure-glossary-cloud-terminology.md#resource-group
[T-SQL]: ./sql-data-warehouse-get-started-create-database-tsql.md

<!--MSDN references-->
[sp_set_firewall_rule]: https://msdn.microsoft.com/library/dn270017.aspx
[sp_set_database_firewall_rule]: https://msdn.microsoft.com/library/dn270010.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
