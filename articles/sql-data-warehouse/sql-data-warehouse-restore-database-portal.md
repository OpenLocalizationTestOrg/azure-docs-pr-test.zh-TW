---
title: "aaaRestore Azure SQL 資料倉儲 （Azure 入口網站） |Microsoft 文件"
description: "還原 Azure SQL 資料倉儲的 Azure 入口網站工作。"
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: barbkess
editor: 
ms.assetid: b0aef539-7657-4b0e-9899-74098f5c21bc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 09/21/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: cb225d2a21b61acab70a51b69c266f8d3ffacc9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="restore-azure-sql-data-warehouse-portal"></a>還原 Azure SQL 資料倉儲 (入口網站)
> [!div class="op_single_selector"]
> * [概觀][Overview]
> * [入口網站][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
>
>
在本文中，您將學習如何使用的 Azure SQL 資料倉儲 toorestore hello Azure 入口網站。

## <a name="before-you-begin"></a>開始之前
**請驗證您的 DTU 容量。** SQL 資料倉儲的每個執行個體均由具有預設資料配額單位 (DTU) 的 SQL Database 裝載 (例如，myserver.database.windows.net)。 您可以還原 SQL 資料倉儲之前，請確認您的 SQL server 有足夠的剩餘 hello 資料庫的還原目的地的 DTU 配額。 toolearn 如何 toocalculate DTU 配額或 toorequest 更多 Dtu，請參閱[要求 DTU 配額變更][Request a DTU quota change]。

## <a name="restore-an-active-or-paused-database"></a>還原作用中或已暫停的資料庫
toorestore 資料庫：

1. 登入 toohello [Azure 入口網站][Azure portal]。
2. Hello 左窗格中，選取**瀏覽**，然後選取**SQL 伺服器**。

    ![選取 [瀏覽] > [SQL Server]](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. 尋找您的伺服器，然後選取它。

    ![選取您的伺服器](./media/sql-data-warehouse-restore-database-portal/01-select-server.png)
4. 您想要從，toorestore，，然後選取它，請尋找 hello SQL 資料倉儲執行個體。

    ![選取 SQL 資料倉儲 toorestore hello 執行個體](./media/sql-data-warehouse-restore-database-portal/01-select-active-dw.png)
5. 在 [hello hello 資料倉儲] 刀鋒視窗頂端，選取**還原**。

    ![選取 [還原]](./media/sql-data-warehouse-restore-database-portal/01-select-restore-from-active.png)
6. 指定新的 **資料庫名稱**。
7. 最新的選取 hello**還原點**。

   請確定您選擇 hello 最新的還原點。 以國際標準時間 (UTC) 顯示還原點，因為 hello 預設選項，可能無法 hello 最新的還原點。

      ![選取還原點](./media/sql-data-warehouse-restore-database-portal/01-restore-blade-from-active.png)
8. 選取 [確定] 。
9. hello 資料庫還原程序會開始，而且您可以使用**通知**toomonitor hello 程序。

> [!NOTE]
> Hello 還原完成後，您可以依照下列設定復原的資料庫[設定您的資料庫復原後][Configure your database after recovery]。
>
>

## <a name="restore-a-deleted-database"></a>還原已刪除的資料庫
toorestore 已刪除的資料庫：

1. 登入 toohello [Azure 入口網站][Azure portal]。
2. Hello 左窗格中，選取**瀏覽**，然後選取**SQL 伺服器**。

    ![選取 [瀏覽] > [SQL Server]](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. 尋找您的伺服器，然後選取它。

    ![選取您的伺服器](./media/sql-data-warehouse-restore-database-portal/02-select-server.png)
4. 捲動 toohello**作業**> 一節，在您的伺服器 刀鋒視窗。
5. 選取 hello**已刪除資料庫**磚。

    ![選取 hello 已刪除資料庫並排顯示](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dws.png)
6. 選取您想 toorestore hello 刪除資料庫。

    ![選取資料庫 toorestore](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dw.png)
7. 指定新的 **資料庫名稱**。

    ![新增 hello 資料庫的名稱](./media/sql-data-warehouse-restore-database-portal/02-restore-blade-from-deleted.png)
8. 選取 [確定] 。
9. hello 資料庫還原程序會開始，而且您可以使用**通知**toomonitor hello 程序。

> [!NOTE]
> tooconfigure 資料庫 hello 還原完成之後，請參閱[設定您的資料庫復原後][Configure your database after recovery]。
>
>

## <a name="next-steps"></a>後續步驟
關於 hello 業務續航力功能的 Azure SQL Database 版本中，讀取 hello toolearn [Azure SQL Database 業務持續性概觀][Azure SQL Database business continuity overview]。

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change

<!--MSDN references-->

<!--Blog references-->

<!--Other Web references-->
[Azure portal]: https://portal.azure.com/
