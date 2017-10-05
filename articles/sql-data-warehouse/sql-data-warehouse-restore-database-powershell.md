---
title: "還原 Azure SQL 資料倉儲 (PowerShell) | Microsoft Docs"
description: "還原 Azure SQL 資料倉儲的 PowerShell 工作。"
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: ac62f154-c8b0-4c33-9c42-f480808aa1d2
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: 6286c0e682bae2d3bf0435a25b8077a53b117b25
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="restore-an-azure-sql-data-warehouse-powershell"></a><span data-ttu-id="b7ccf-103">還原 Azure SQL 資料倉儲 (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="b7ccf-103">Restore an Azure SQL Data Warehouse (PowerShell)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="b7ccf-104">[概觀][Overview]</span><span class="sxs-lookup"><span data-stu-id="b7ccf-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="b7ccf-105">[入口網站][Portal]</span><span class="sxs-lookup"><span data-stu-id="b7ccf-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="b7ccf-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="b7ccf-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="b7ccf-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="b7ccf-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="b7ccf-108">在本文中，您將了解如何使用 PowerShell 來還原 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="b7ccf-108">In this article you will learn how to restore an Azure SQL Data Warehouse using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b7ccf-109">開始之前</span><span class="sxs-lookup"><span data-stu-id="b7ccf-109">Before you begin</span></span>
<span data-ttu-id="b7ccf-110">**請驗證您的 DTU 容量。**</span><span class="sxs-lookup"><span data-stu-id="b7ccf-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="b7ccf-111">每個 SQL 資料倉儲均由具有預設 DTU 配額的 SQL 伺服器裝載 (例如 myserver.database.windows.net)。</span><span class="sxs-lookup"><span data-stu-id="b7ccf-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="b7ccf-112">在您還原 SQL 資料倉儲之前，請確認您的 SQL 伺服器有足夠的剩餘 DTU 配額供要還原的資料庫使用。</span><span class="sxs-lookup"><span data-stu-id="b7ccf-112">Before you can restore a SQL Data Warehouse, verify that the your SQL server has enough remaining DTU quota for the database being restored.</span></span> <span data-ttu-id="b7ccf-113">若要了解如何計算所需 DTU 或要求更多 DTU，請參閱[要求 DTU 配額變更][Request a DTU quota change]。</span><span class="sxs-lookup"><span data-stu-id="b7ccf-113">To learn how to calculate DTU needed or to request more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="b7ccf-114">安裝 PowerShell</span><span class="sxs-lookup"><span data-stu-id="b7ccf-114">Install PowerShell</span></span>
<span data-ttu-id="b7ccf-115">若要搭配使用 Azure Powershell 與 SQL 資料倉儲，您需要安裝 Azure PowerShell 1.0 版或更高版本。</span><span class="sxs-lookup"><span data-stu-id="b7ccf-115">In order to use Azure PowerShell with SQL Data Warehouse, you will need to install Azure PowerShell version 1.0 or greater.</span></span>  <span data-ttu-id="b7ccf-116">您可以執行 **Get-Module -ListAvailable -Name AzureRM**來檢查您的版本。</span><span class="sxs-lookup"><span data-stu-id="b7ccf-116">You can check your version by running **Get-Module -ListAvailable -Name AzureRM**.</span></span>  <span data-ttu-id="b7ccf-117">可透過 [Microsoft Web Platform Installer][Microsoft Web Platform Installer]安裝最新的版本。</span><span class="sxs-lookup"><span data-stu-id="b7ccf-117">The latest version can be installed from  [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="b7ccf-118">如需安裝最新版本的詳細資訊，請參閱[如何安裝和設定 Azure PowerShell][How to install and configure Azure PowerShell]。</span><span class="sxs-lookup"><span data-stu-id="b7ccf-118">For more information on installing the latest version, see [How to install and configure Azure PowerShell][How to install and configure Azure PowerShell].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="b7ccf-119">還原作用中或已暫停的資料庫</span><span class="sxs-lookup"><span data-stu-id="b7ccf-119">Restore an active or paused database</span></span>
<span data-ttu-id="b7ccf-120">若要從快照還原資料庫，請使用 [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b7ccf-120">To restore a database from a snapshot use the [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] PowerShell cmdlet.</span></span>

1. <span data-ttu-id="b7ccf-121">開啟 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="b7ccf-121">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="b7ccf-122">連接到您的 Azure 帳戶，然後列出與您帳戶關聯的所有訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b7ccf-122">Connect to your Azure account and list all the subscriptions associated with your account.</span></span>
3. <span data-ttu-id="b7ccf-123">選取包含要還原之資料庫的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b7ccf-123">Select the subscription that contains the database to be restored.</span></span>
4. <span data-ttu-id="b7ccf-124">列出資料庫的還原點。</span><span class="sxs-lookup"><span data-stu-id="b7ccf-124">List the restore points for the database.</span></span>
5. <span data-ttu-id="b7ccf-125">使用 RestorePointCreationDate 挑選出想要的還原點。</span><span class="sxs-lookup"><span data-stu-id="b7ccf-125">Pick the desired restore point using the RestorePointCreationDate.</span></span>
6. <span data-ttu-id="b7ccf-126">將資料庫還原到想要的還原點。</span><span class="sxs-lookup"><span data-stu-id="b7ccf-126">Restore the database to the desired restore point.</span></span>
7. <span data-ttu-id="b7ccf-127">確認還原的資料庫在線上。</span><span class="sxs-lookup"><span data-stu-id="b7ccf-127">Verify that the restored database is online.</span></span>

```Powershell

$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# List the last 10 database restore points
((Get-AzureRMSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName ($DatabaseName).RestorePointCreationDate)[-10 .. -1]

# Or list all restore points
Get-AzureRmSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Get the specific database to restore
$Database = Get-AzureRmSqlDatabase -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Pick desired restore point using RestorePointCreationDate
$PointInTime="<RestorePointCreationDate>"  

# Restore database from a restore point
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromPointInTimeBackup –PointInTime $PointInTime -ResourceGroupName $Database.ResourceGroupName -ServerName $Database.$ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $Database.ResourceID

# Verify the status of restored database
$RestoredDatabase.status

```

> [!NOTE]
> <span data-ttu-id="b7ccf-128">還原完成後，您可以遵循[在復原之後設定資料庫][Configure your database after recovery]來設定復原的資料庫。</span><span class="sxs-lookup"><span data-stu-id="b7ccf-128">After the restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="b7ccf-129">還原已刪除的資料庫</span><span class="sxs-lookup"><span data-stu-id="b7ccf-129">Restore a deleted database</span></span>
<span data-ttu-id="b7ccf-130">若要還原已刪除的資料庫，請使用 [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b7ccf-130">To restore a deleted database, use the [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="b7ccf-131">開啟 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="b7ccf-131">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="b7ccf-132">連接到您的 Azure 帳戶，然後列出與您帳戶關聯的所有訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b7ccf-132">Connect to your Azure account and list all the subscriptions associated with your account.</span></span>
3. <span data-ttu-id="b7ccf-133">選取包含要還原之已刪除資料庫的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b7ccf-133">Select the subscription that contains the deleted database to be restored.</span></span>
4. <span data-ttu-id="b7ccf-134">取得已刪除的特定資料庫。</span><span class="sxs-lookup"><span data-stu-id="b7ccf-134">Get the specific deleted database.</span></span>
5. <span data-ttu-id="b7ccf-135">還原已刪除的資料庫。</span><span class="sxs-lookup"><span data-stu-id="b7ccf-135">Restore the deleted database.</span></span>
6. <span data-ttu-id="b7ccf-136">確認還原的資料庫在線上。</span><span class="sxs-lookup"><span data-stu-id="b7ccf-136">Verify that the restored database is online.</span></span>

```Powershell
$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# Get the deleted database to restore
$DeletedDatabase = Get-AzureRmSqlDeletedDatabaseBackup -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Restore deleted database
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromDeletedDatabaseBackup –DeletionDate $DeletedDatabase.DeletionDate -ResourceGroupName $DeletedDatabase.ResourceGroupName -ServerName $DeletedDatabase.ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $DeletedDatabase.ResourceID

# Verify the status of restored database
$RestoredDatabase.status
```

> [!NOTE]
> <span data-ttu-id="b7ccf-137">還原完成後，您可以遵循[在復原之後設定資料庫][Configure your database after recovery]來設定復原的資料庫。</span><span class="sxs-lookup"><span data-stu-id="b7ccf-137">After the restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-from-an-azure-geographical-region"></a><span data-ttu-id="b7ccf-138">從 Azure 地理區域還原</span><span class="sxs-lookup"><span data-stu-id="b7ccf-138">Restore from an Azure geographical region</span></span>
<span data-ttu-id="b7ccf-139">若要還原資料庫，請使用 [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b7ccf-139">To recover a database, use the [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="b7ccf-140">開啟 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="b7ccf-140">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="b7ccf-141">連接到您的 Azure 帳戶，然後列出與您帳戶關聯的所有訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b7ccf-141">Connect to your Azure account and list all the subscriptions associated with your account.</span></span>
3. <span data-ttu-id="b7ccf-142">選取包含要還原之資料庫的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b7ccf-142">Select the subscription that contains the database to be restored.</span></span>
4. <span data-ttu-id="b7ccf-143">取得您想要復原的資料庫。</span><span class="sxs-lookup"><span data-stu-id="b7ccf-143">Get the database you want to recover.</span></span>
5. <span data-ttu-id="b7ccf-144">建立資料庫的復原要求。</span><span class="sxs-lookup"><span data-stu-id="b7ccf-144">Create the recovery request for the database.</span></span>
6. <span data-ttu-id="b7ccf-145">確認異地還原資料庫的狀態。</span><span class="sxs-lookup"><span data-stu-id="b7ccf-145">Verify the status of the geo-restored database.</span></span>

```Powershell
Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName "<Subscription_name>"

# Get the database you want to recover
$GeoBackup = Get-AzureRmSqlDatabaseGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourServerName>" -DatabaseName "<YourDatabaseName>"

# Recover database
$GeoRestoredDatabase = Restore-AzureRmSqlDatabase –FromGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourTargetServer>" -TargetDatabaseName "<NewDatabaseName>" –ResourceId $GeoBackup.ResourceID

# Verify that the geo-restored database is online
$GeoRestoredDatabase.status
```

> [!NOTE]
> <span data-ttu-id="b7ccf-146">若要在還原完成之後設定資料庫，請參閱[在復原之後設定資料庫][Configure your database after recovery]。</span><span class="sxs-lookup"><span data-stu-id="b7ccf-146">To configure your database after the restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

<span data-ttu-id="b7ccf-147">如果來源資料庫是啟用 TDE，則復原的資料庫將是啟用 TDE。</span><span class="sxs-lookup"><span data-stu-id="b7ccf-147">The recovered database will be TDE-enabled if the source database is TDE-enabled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7ccf-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b7ccf-148">Next steps</span></span>
<span data-ttu-id="b7ccf-149">若要深入了解 Azure SQL Database 版本的商務持續性功能，請閱讀 [Azure SQL Database 商務持續性概觀][Azure SQL Database business continuity overview]。</span><span class="sxs-lookup"><span data-stu-id="b7ccf-149">To learn about the business continuity features of Azure SQL Database editions, please read the [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

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
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery

<!--MSDN references-->
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx

<!--Other Web references-->
[Azure Portal]: https://portal.azure.com/
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
