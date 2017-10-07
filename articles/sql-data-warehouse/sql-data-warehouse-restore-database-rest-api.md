---
title: "aaaRestore Azure SQL 資料倉儲 (REST API) |Microsoft 文件"
description: "還原 Azure SQL 資料倉儲的 REST API 工作。"
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: fca922c6-b675-49c7-907e-5dcf26d451dd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: cf6678d71aafff71b1ea715f447e41e25f20d1b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-data-warehouse-rest-api"></a>還原 Azure SQL 資料倉儲 (REST API)
> [!div class="op_single_selector"]
> * [概觀][Overview]
> * [入口網站][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
> 
> 

在本文中，您將學習如何使用 Azure SQL 資料倉儲的 toorestore hello REST API。

## <a name="before-you-begin"></a>開始之前
**請驗證您的 DTU 容量。** 每個 SQL 資料倉儲均由具有預設 DTU 配額的 SQL 伺服器裝載 (例如 myserver.database.windows.net)。  您可以還原 SQL 資料倉儲之前，請確認您的 SQL server 有足夠的剩餘 hello 要還原的資料庫的 DTU 配額該 hello。 toolearn toocalculate DTU 的所需或 toorequest 更多 DTU，請參閱[要求 DTU 配額變更][Request a DTU quota change]。

## <a name="restore-an-active-or-paused-database"></a>還原作用中或已暫停的資料庫
toorestore 資料庫：

1. 取得使用 hello 取得資料庫還原點作業的資料庫還原點 hello 清單。
2. 開始使用 hello 還原[建立資料庫還原要求][ Create database restore request]作業。
3. 使用 hello 追蹤您還原 hello 狀態[資料庫作業狀態][ Database operation status]作業。

> [!NOTE]
> Hello 還原完成之後，您可以依照下列設定復原的資料庫[設定您的資料庫復原後][Configure your database after recovery]。
> 
> 

## <a name="restore-a-deleted-database"></a>還原已刪除的資料庫
toorestore 已刪除的資料庫：

1. 列出所有可還原已刪除資料庫的使用 hello[清單可還原的已卸除資料庫][ List restorable dropped databases]作業。
2. 取得 hello 詳細資料為您想要刪除的 hello 資料庫 toorestore 使用 hello [Get 可還原的已卸除資料庫][ Get restorable dropped database]作業。
3. 開始使用 hello 還原[建立資料庫還原要求][ Create database restore request]作業。
4. 使用 hello 追蹤您還原 hello 狀態[資料庫作業狀態][ Database operation status]作業。

> [!NOTE]
> tooconfigure 資料庫之後 hello 還原完成後，請參閱[設定您的資料庫復原後][Configure your database after recovery]。
> 
> 

## <a name="next-steps"></a>後續步驟
toolearn 有關 hello 業務續航力功能的 Azure SQL Database 的版本，請閱讀 hello [Azure SQL Database 業務持續性概觀][Azure SQL Database business continuity overview]。

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md

<!--MSDN references-->
[Create database restore request]: https://msdn.microsoft.com/library/azure/dn509571.aspx
[Database operation status]: https://msdn.microsoft.com/library/azure/dn720371.aspx
[Get restorable dropped database]: https://msdn.microsoft.com/library/azure/dn509574.aspx
[List restorable dropped databases]: https://msdn.microsoft.com/library/azure/dn509562.aspx
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx

<!--Other Web references-->
[Azure Portal]: https://portal.azure.com/
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
