---
title: "Azure 資料倉儲中的本機和異地備援 aaaRestore |Microsoft 文件"
description: "復原資料庫，以在 Azure SQL 資料倉儲中的 hello 資料庫還原選項的概觀。"
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: 3e01c65c-6708-4fd7-82f5-4e1b5f61d304
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: a96b898372b29d420e1416ca93a172ff8af47fc7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-restore"></a>SQL 資料倉儲還原
> [!div class="op_single_selector"]
> * [概觀][Overview]
> * [入口網站][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
> 
> 

「SQL 資料倉儲」提供本機和異地還原作為其資料倉儲災害復原功能的一部分。 使用資料倉儲備份 toorestore 資料倉儲 tooa 還原點在 hello 主要區域中，或使用異地備援備份 toorestore tooa 不同的地理區域。 本文說明還原資料倉儲的 hello 的細節。

## <a name="what-is-a-data-warehouse-restore"></a>什麼是資料倉儲還原？
資料倉儲還原係指從現有或已刪除之資料倉儲的備份建立的新資料倉儲。 hello 還原的資料倉儲重新建立在特定時間的 hello 備份資料倉儲。 由於「SQL 資料倉儲」是一個分散式系統，因此會從儲存在 Azure Blob 中的許多備份檔案建立一個資料倉儲還原。 

資料庫還原是所有商務持續性和災害復原策略中不可或缺的一部分，因為它可在您的資料發生意外損毀或刪除之後重新建立該資料。

如需詳細資訊，請參閱：

* [SQL 資料倉儲備份](sql-data-warehouse-backups.md)
* [商務持續性概觀](../sql-database/sql-database-business-continuity.md)

## <a name="data-warehouse-restore-points"></a>資料倉儲還原點
使用 Azure 高階儲存體的優點，作為 SQL 資料倉儲會使用 Azure 儲存體 Blob 快照集 toobackup hello 主要資料倉儲。 每個快照集具有代表 hello 時間的還原點啟動 hello 快照集。 toorestore 資料倉儲，您選擇還原點，然後發出 restore 命令。  

SQL 資料倉儲一律會還原 hello 備份 tooa 新的資料倉儲。 您可以保留 hello 還原的資料倉儲和 hello 目前一個，或刪除其中一個。 如果您想 tooreplace hello 目前資料倉儲以 hello 還原資料倉儲，您可以重新命名。

如果您需要 toorestore 已刪除或已暫停資料倉儲時，您可以[建立支援票證](sql-data-warehouse-get-started-create-support-ticket.md)。 

<!-- 
### Can I restore a deleted data warehouse?

Yes, you can restore hello last available restore point.

Yes, for hello next seven calendar days. When you delete a data warehouse, SQL Data Warehouse actually keeps hello data warehouse and its snapshots for seven days just in case you need hello data. After seven days, you won't be able toorestore tooany of hello restore points. -->

## <a name="geo-redundant-restore"></a>異地備援還原
您可以還原您支援您所選擇的效能層級的 Azure SQL 資料倉儲的資料倉儲 tooany 區域。 請注意，9000 和 18000 DWU 不支援在所有區域 hello 預覽期間。

> [!NOTE]
> 您必須不選擇用這項功能的地理備援 tooperform 還原。
> 
> 

## <a name="restore-timeline"></a>還原時間軸
您可以還原過去七天內 hello 的資料庫 tooany 可用還原時間點。 快照集開始每四個 tooeight 小時，且有七天。 當快照集存在時間超過七天，它就會過期，而且無法再使用其還原點。

## <a name="restore-costs"></a>還原成本
hello hello 還原的資料倉儲儲存體費用是 hello Azure 高階儲存體費率計費。 

如果您暫停還原的資料倉儲時，您將支付儲存體費率 hello Azure 高階儲存體。 暫停 hello 優點是您不需付費的 hello DWU 運算資源。

如需 SQL 資料倉儲價格的相關詳細資訊，請參閱 [SQL 資料倉儲價格](https://azure.microsoft.com/pricing/details/sql-data-warehouse/)。

## <a name="uses-for-restore"></a>還原的用途
hello 主要用於資料倉儲還原資料意外遺失或損毀之後 toorecover 資料。

您也可以使用資料倉儲還原 tooretain 備份的時間超過七天。 Hello 備份還原之後，您會擁有 hello 資料倉儲線上的連線，並且可以暫停它無限期 toosave 計算成本。 hello 已暫停的資料庫會產生 hello Azure 高階儲存體費率的儲存體費用。 

## <a name="related-topics"></a>相關主題
### <a name="scenarios"></a>案例
* 如需商務持續性概觀，請參閱[商務持續性概觀](../sql-database/sql-database-business-continuity.md)

<!-- ### Tasks -->

資料倉儲 tooperform 還原，請使用還原：

* Azure 入口網站，請參閱[還原資料倉儲使用 hello Azure 入口網站](sql-data-warehouse-restore-database-portal.md)
* PowerShell Cmdlet - 請參閱[使用 PowerShell Cmdlet 來還原資料倉儲](sql-data-warehouse-restore-database-powershell.md)
* REST Api，請參閱[還原使用 hello REST Api 的資料倉儲](sql-data-warehouse-restore-database-rest-api.md)

<!-- ### Tutorials -->

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md

<!--MSDN references-->


<!--Other Web references-->
