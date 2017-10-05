---
title: "還原 Azure SQL 資料倉儲 (REST API) | Microsoft Docs"
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
ms.openlocfilehash: 8656607611e7518e42b51b91774f55abec15c228
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="restore-an-azure-sql-data-warehouse-rest-api"></a><span data-ttu-id="c51eb-103">還原 Azure SQL 資料倉儲 (REST API)</span><span class="sxs-lookup"><span data-stu-id="c51eb-103">Restore an Azure SQL Data Warehouse (REST API)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="c51eb-104">[概觀][Overview]</span><span class="sxs-lookup"><span data-stu-id="c51eb-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="c51eb-105">[入口網站][Portal]</span><span class="sxs-lookup"><span data-stu-id="c51eb-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="c51eb-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="c51eb-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="c51eb-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="c51eb-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="c51eb-108">在本文中，您將了解如何使用 REST API 來還原 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="c51eb-108">In this article you will learn how to restore an Azure SQL Data Warehouse using the REST API.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c51eb-109">開始之前</span><span class="sxs-lookup"><span data-stu-id="c51eb-109">Before you begin</span></span>
<span data-ttu-id="c51eb-110">**請驗證您的 DTU 容量。**</span><span class="sxs-lookup"><span data-stu-id="c51eb-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="c51eb-111">每個 SQL 資料倉儲均由具有預設 DTU 配額的 SQL 伺服器裝載 (例如 myserver.database.windows.net)。</span><span class="sxs-lookup"><span data-stu-id="c51eb-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="c51eb-112">在您還原 SQL 資料倉儲之前，請確認您的 SQL 伺服器有足夠的剩餘 DTU 配額供要還原的資料庫使用。</span><span class="sxs-lookup"><span data-stu-id="c51eb-112">Before you can restore a SQL Data Warehouse, verify that the your SQL server has enough remaining DTU quota for the database being restored.</span></span> <span data-ttu-id="c51eb-113">若要了解如何計算所需 DTU 或要求更多 DTU，請參閱[要求 DTU 配額變更][Request a DTU quota change]。</span><span class="sxs-lookup"><span data-stu-id="c51eb-113">To learn how to calculate DTU needed or to request more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="c51eb-114">還原作用中或已暫停的資料庫</span><span class="sxs-lookup"><span data-stu-id="c51eb-114">Restore an active or paused database</span></span>
<span data-ttu-id="c51eb-115">還原資料庫：</span><span class="sxs-lookup"><span data-stu-id="c51eb-115">To restore a database:</span></span>

1. <span data-ttu-id="c51eb-116">使用 Get 資料庫還原點作業取得資料庫還原點清單。</span><span class="sxs-lookup"><span data-stu-id="c51eb-116">Get the list of database restore points using the Get Database Restore Points operation.</span></span>
2. <span data-ttu-id="c51eb-117">使用[建立資料庫還原要求][Create database restore request]作業來開始還原。</span><span class="sxs-lookup"><span data-stu-id="c51eb-117">Begin your restore by using the [Create database restore request][Create database restore request] operation.</span></span>
3. <span data-ttu-id="c51eb-118">使用[資料庫作業狀態][Database operation status]作業來追蹤還原狀態。</span><span class="sxs-lookup"><span data-stu-id="c51eb-118">Track the status of your restore by using the [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="c51eb-119">還原完成後，您可以遵循[在復原之後設定資料庫][Configure your database after recovery]來設定復原的資料庫。</span><span class="sxs-lookup"><span data-stu-id="c51eb-119">After the restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="c51eb-120">還原已刪除的資料庫</span><span class="sxs-lookup"><span data-stu-id="c51eb-120">Restore a deleted database</span></span>
<span data-ttu-id="c51eb-121">還原已刪除的資料庫：</span><span class="sxs-lookup"><span data-stu-id="c51eb-121">To restore a deleted database:</span></span>

1. <span data-ttu-id="c51eb-122">使用[列出可還原的已卸除資料庫][List restorable dropped databases]作業來列出所有可還原的已刪除資料庫。</span><span class="sxs-lookup"><span data-stu-id="c51eb-122">List all of your restorable deleted databases by using the [List restorable dropped databases][List restorable dropped databases] operation.</span></span>
2. <span data-ttu-id="c51eb-123">使用[取得可還原的已卸除資料庫][Get restorable dropped database]作業來取得您想要還原之已刪除資料庫的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c51eb-123">Get the details for the deleted database you want to restore by using the [Get restorable dropped database][Get restorable dropped database] operation.</span></span>
3. <span data-ttu-id="c51eb-124">使用[建立資料庫還原要求][Create database restore request]作業來開始還原。</span><span class="sxs-lookup"><span data-stu-id="c51eb-124">Begin your restore by using the [Create database restore request][Create database restore request] operation.</span></span>
4. <span data-ttu-id="c51eb-125">使用[資料庫作業狀態][Database operation status]作業來追蹤還原狀態。</span><span class="sxs-lookup"><span data-stu-id="c51eb-125">Track the status of your restore by using the [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="c51eb-126">若要在還原完成之後設定資料庫，請參閱[在復原之後設定資料庫][Configure your database after recovery]。</span><span class="sxs-lookup"><span data-stu-id="c51eb-126">To configure your database after the restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="c51eb-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c51eb-127">Next steps</span></span>
<span data-ttu-id="c51eb-128">若要深入了解 Azure SQL Database 版本的商務持續性功能，請閱讀 [Azure SQL Database 商務持續性概觀][Azure SQL Database business continuity overview]。</span><span class="sxs-lookup"><span data-stu-id="c51eb-128">To learn about the business continuity features of Azure SQL Database editions, please read the [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How to install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
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
