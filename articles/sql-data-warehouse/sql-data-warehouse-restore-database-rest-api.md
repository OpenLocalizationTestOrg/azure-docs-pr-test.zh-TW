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
# <a name="restore-an-azure-sql-data-warehouse-rest-api"></a><span data-ttu-id="824da-103">還原 Azure SQL 資料倉儲 (REST API)</span><span class="sxs-lookup"><span data-stu-id="824da-103">Restore an Azure SQL Data Warehouse (REST API)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="824da-104">[概觀][Overview]</span><span class="sxs-lookup"><span data-stu-id="824da-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="824da-105">[入口網站][Portal]</span><span class="sxs-lookup"><span data-stu-id="824da-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="824da-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="824da-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="824da-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="824da-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="824da-108">在本文中，您將學習如何使用 Azure SQL 資料倉儲的 toorestore hello REST API。</span><span class="sxs-lookup"><span data-stu-id="824da-108">In this article you will learn how toorestore an Azure SQL Data Warehouse using hello REST API.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="824da-109">開始之前</span><span class="sxs-lookup"><span data-stu-id="824da-109">Before you begin</span></span>
<span data-ttu-id="824da-110">**請驗證您的 DTU 容量。**</span><span class="sxs-lookup"><span data-stu-id="824da-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="824da-111">每個 SQL 資料倉儲均由具有預設 DTU 配額的 SQL 伺服器裝載 (例如 myserver.database.windows.net)。</span><span class="sxs-lookup"><span data-stu-id="824da-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="824da-112">您可以還原 SQL 資料倉儲之前，請確認您的 SQL server 有足夠的剩餘 hello 要還原的資料庫的 DTU 配額該 hello。</span><span class="sxs-lookup"><span data-stu-id="824da-112">Before you can restore a SQL Data Warehouse, verify that hello your SQL server has enough remaining DTU quota for hello database being restored.</span></span> <span data-ttu-id="824da-113">toolearn toocalculate DTU 的所需或 toorequest 更多 DTU，請參閱[要求 DTU 配額變更][Request a DTU quota change]。</span><span class="sxs-lookup"><span data-stu-id="824da-113">toolearn how toocalculate DTU needed or toorequest more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="824da-114">還原作用中或已暫停的資料庫</span><span class="sxs-lookup"><span data-stu-id="824da-114">Restore an active or paused database</span></span>
<span data-ttu-id="824da-115">toorestore 資料庫：</span><span class="sxs-lookup"><span data-stu-id="824da-115">toorestore a database:</span></span>

1. <span data-ttu-id="824da-116">取得使用 hello 取得資料庫還原點作業的資料庫還原點 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="824da-116">Get hello list of database restore points using hello Get Database Restore Points operation.</span></span>
2. <span data-ttu-id="824da-117">開始使用 hello 還原[建立資料庫還原要求][ Create database restore request]作業。</span><span class="sxs-lookup"><span data-stu-id="824da-117">Begin your restore by using hello [Create database restore request][Create database restore request] operation.</span></span>
3. <span data-ttu-id="824da-118">使用 hello 追蹤您還原 hello 狀態[資料庫作業狀態][ Database operation status]作業。</span><span class="sxs-lookup"><span data-stu-id="824da-118">Track hello status of your restore by using hello [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="824da-119">Hello 還原完成之後，您可以依照下列設定復原的資料庫[設定您的資料庫復原後][Configure your database after recovery]。</span><span class="sxs-lookup"><span data-stu-id="824da-119">After hello restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="824da-120">還原已刪除的資料庫</span><span class="sxs-lookup"><span data-stu-id="824da-120">Restore a deleted database</span></span>
<span data-ttu-id="824da-121">toorestore 已刪除的資料庫：</span><span class="sxs-lookup"><span data-stu-id="824da-121">toorestore a deleted database:</span></span>

1. <span data-ttu-id="824da-122">列出所有可還原已刪除資料庫的使用 hello[清單可還原的已卸除資料庫][ List restorable dropped databases]作業。</span><span class="sxs-lookup"><span data-stu-id="824da-122">List all of your restorable deleted databases by using hello [List restorable dropped databases][List restorable dropped databases] operation.</span></span>
2. <span data-ttu-id="824da-123">取得 hello 詳細資料為您想要刪除的 hello 資料庫 toorestore 使用 hello [Get 可還原的已卸除資料庫][ Get restorable dropped database]作業。</span><span class="sxs-lookup"><span data-stu-id="824da-123">Get hello details for hello deleted database you want toorestore by using hello [Get restorable dropped database][Get restorable dropped database] operation.</span></span>
3. <span data-ttu-id="824da-124">開始使用 hello 還原[建立資料庫還原要求][ Create database restore request]作業。</span><span class="sxs-lookup"><span data-stu-id="824da-124">Begin your restore by using hello [Create database restore request][Create database restore request] operation.</span></span>
4. <span data-ttu-id="824da-125">使用 hello 追蹤您還原 hello 狀態[資料庫作業狀態][ Database operation status]作業。</span><span class="sxs-lookup"><span data-stu-id="824da-125">Track hello status of your restore by using hello [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="824da-126">tooconfigure 資料庫之後 hello 還原完成後，請參閱[設定您的資料庫復原後][Configure your database after recovery]。</span><span class="sxs-lookup"><span data-stu-id="824da-126">tooconfigure your database after hello restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="824da-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="824da-127">Next steps</span></span>
<span data-ttu-id="824da-128">toolearn 有關 hello 業務續航力功能的 Azure SQL Database 的版本，請閱讀 hello [Azure SQL Database 業務持續性概觀][Azure SQL Database business continuity overview]。</span><span class="sxs-lookup"><span data-stu-id="824da-128">toolearn about hello business continuity features of Azure SQL Database editions, please read hello [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

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
