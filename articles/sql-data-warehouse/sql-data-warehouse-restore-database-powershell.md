---
title: "aaaRestore Azure SQL 資料倉儲 (PowerShell) |Microsoft 文件"
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
ms.openlocfilehash: aa29a315080b1ed477cc6a051ce15a3202630cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-data-warehouse-powershell"></a><span data-ttu-id="efe9a-103">還原 Azure SQL 資料倉儲 (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="efe9a-103">Restore an Azure SQL Data Warehouse (PowerShell)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="efe9a-104">[概觀][Overview]</span><span class="sxs-lookup"><span data-stu-id="efe9a-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="efe9a-105">[入口網站][Portal]</span><span class="sxs-lookup"><span data-stu-id="efe9a-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="efe9a-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="efe9a-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="efe9a-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="efe9a-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="efe9a-108">在本文中，您將學習如何 toorestore Azure SQL 資料倉儲使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="efe9a-108">In this article you will learn how toorestore an Azure SQL Data Warehouse using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="efe9a-109">開始之前</span><span class="sxs-lookup"><span data-stu-id="efe9a-109">Before you begin</span></span>
<span data-ttu-id="efe9a-110">**請驗證您的 DTU 容量。**</span><span class="sxs-lookup"><span data-stu-id="efe9a-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="efe9a-111">每個 SQL 資料倉儲均由具有預設 DTU 配額的 SQL 伺服器裝載 (例如 myserver.database.windows.net)。</span><span class="sxs-lookup"><span data-stu-id="efe9a-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="efe9a-112">您可以還原 SQL 資料倉儲之前，請確認您的 SQL server 有足夠的剩餘 hello 要還原的資料庫的 DTU 配額該 hello。</span><span class="sxs-lookup"><span data-stu-id="efe9a-112">Before you can restore a SQL Data Warehouse, verify that hello your SQL server has enough remaining DTU quota for hello database being restored.</span></span> <span data-ttu-id="efe9a-113">toolearn toocalculate DTU 的所需或 toorequest 更多 DTU，請參閱[要求 DTU 配額變更][Request a DTU quota change]。</span><span class="sxs-lookup"><span data-stu-id="efe9a-113">toolearn how toocalculate DTU needed or toorequest more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="efe9a-114">安裝 PowerShell</span><span class="sxs-lookup"><span data-stu-id="efe9a-114">Install PowerShell</span></span>
<span data-ttu-id="efe9a-115">在順序 toouse 向 SQL 資料倉儲的 Azure PowerShell，您必須 tooinstall 版本的 Azure PowerShell 1.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="efe9a-115">In order toouse Azure PowerShell with SQL Data Warehouse, you will need tooinstall Azure PowerShell version 1.0 or greater.</span></span>  <span data-ttu-id="efe9a-116">您可以執行 **Get-Module -ListAvailable -Name AzureRM**來檢查您的版本。</span><span class="sxs-lookup"><span data-stu-id="efe9a-116">You can check your version by running **Get-Module -ListAvailable -Name AzureRM**.</span></span>  <span data-ttu-id="efe9a-117">hello 最新版本可以從安裝[Microsoft Web Platform Installer][Microsoft Web Platform Installer]。</span><span class="sxs-lookup"><span data-stu-id="efe9a-117">hello latest version can be installed from  [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="efe9a-118">如需有關如何安裝 hello 最新版本的詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell][How tooinstall and configure Azure PowerShell]。</span><span class="sxs-lookup"><span data-stu-id="efe9a-118">For more information on installing hello latest version, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="efe9a-119">還原作用中或已暫停的資料庫</span><span class="sxs-lookup"><span data-stu-id="efe9a-119">Restore an active or paused database</span></span>
<span data-ttu-id="efe9a-120">toorestore 從快照集資料庫使用 hello[還原 AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="efe9a-120">toorestore a database from a snapshot use hello [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] PowerShell cmdlet.</span></span>

1. <span data-ttu-id="efe9a-121">開啟 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="efe9a-121">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="efe9a-122">連接 tooyour Azure 帳戶，然後列出與您的帳戶相關聯的所有 hello 訂閱。</span><span class="sxs-lookup"><span data-stu-id="efe9a-122">Connect tooyour Azure account and list all hello subscriptions associated with your account.</span></span>
3. <span data-ttu-id="efe9a-123">選取包含還原 hello 資料庫 toobe hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="efe9a-123">Select hello subscription that contains hello database toobe restored.</span></span>
4. <span data-ttu-id="efe9a-124">清單 hello 的還原點 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="efe9a-124">List hello restore points for hello database.</span></span>
5. <span data-ttu-id="efe9a-125">挑選使用 hello RestorePointCreationDate hello 需要還原點。</span><span class="sxs-lookup"><span data-stu-id="efe9a-125">Pick hello desired restore point using hello RestorePointCreationDate.</span></span>
6. <span data-ttu-id="efe9a-126">還原 hello 資料庫所需的 toohello 還原點。</span><span class="sxs-lookup"><span data-stu-id="efe9a-126">Restore hello database toohello desired restore point.</span></span>
7. <span data-ttu-id="efe9a-127">請確認該 hello 還原資料庫在線上。</span><span class="sxs-lookup"><span data-stu-id="efe9a-127">Verify that hello restored database is online.</span></span>

```Powershell

$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# List hello last 10 database restore points
((Get-AzureRMSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName ($DatabaseName).RestorePointCreationDate)[-10 .. -1]

# Or list all restore points
Get-AzureRmSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Get hello specific database toorestore
$Database = Get-AzureRmSqlDatabase -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Pick desired restore point using RestorePointCreationDate
$PointInTime="<RestorePointCreationDate>"  

# Restore database from a restore point
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromPointInTimeBackup –PointInTime $PointInTime -ResourceGroupName $Database.ResourceGroupName -ServerName $Database.$ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $Database.ResourceID

# Verify hello status of restored database
$RestoredDatabase.status

```

> [!NOTE]
> <span data-ttu-id="efe9a-128">Hello 還原完成之後，您可以依照下列設定復原的資料庫[設定您的資料庫復原後][Configure your database after recovery]。</span><span class="sxs-lookup"><span data-stu-id="efe9a-128">After hello restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="efe9a-129">還原已刪除的資料庫</span><span class="sxs-lookup"><span data-stu-id="efe9a-129">Restore a deleted database</span></span>
<span data-ttu-id="efe9a-130">toorestore 已刪除的資料庫，使用 hello[還原 AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet。</span><span class="sxs-lookup"><span data-stu-id="efe9a-130">toorestore a deleted database, use hello [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="efe9a-131">開啟 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="efe9a-131">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="efe9a-132">連接 tooyour Azure 帳戶，然後列出與您的帳戶相關聯的所有 hello 訂閱。</span><span class="sxs-lookup"><span data-stu-id="efe9a-132">Connect tooyour Azure account and list all hello subscriptions associated with your account.</span></span>
3. <span data-ttu-id="efe9a-133">選取包含還原刪除的 hello 資料庫 toobe hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="efe9a-133">Select hello subscription that contains hello deleted database toobe restored.</span></span>
4. <span data-ttu-id="efe9a-134">取得 hello 刪除特定資料庫。</span><span class="sxs-lookup"><span data-stu-id="efe9a-134">Get hello specific deleted database.</span></span>
5. <span data-ttu-id="efe9a-135">還原 hello 刪除資料庫。</span><span class="sxs-lookup"><span data-stu-id="efe9a-135">Restore hello deleted database.</span></span>
6. <span data-ttu-id="efe9a-136">請確認該 hello 還原資料庫在線上。</span><span class="sxs-lookup"><span data-stu-id="efe9a-136">Verify that hello restored database is online.</span></span>

```Powershell
$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# Get hello deleted database toorestore
$DeletedDatabase = Get-AzureRmSqlDeletedDatabaseBackup -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Restore deleted database
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromDeletedDatabaseBackup –DeletionDate $DeletedDatabase.DeletionDate -ResourceGroupName $DeletedDatabase.ResourceGroupName -ServerName $DeletedDatabase.ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $DeletedDatabase.ResourceID

# Verify hello status of restored database
$RestoredDatabase.status
```

> [!NOTE]
> <span data-ttu-id="efe9a-137">Hello 還原完成之後，您可以依照下列設定復原的資料庫[設定您的資料庫復原後][Configure your database after recovery]。</span><span class="sxs-lookup"><span data-stu-id="efe9a-137">After hello restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-from-an-azure-geographical-region"></a><span data-ttu-id="efe9a-138">從 Azure 地理區域還原</span><span class="sxs-lookup"><span data-stu-id="efe9a-138">Restore from an Azure geographical region</span></span>
<span data-ttu-id="efe9a-139">toorecover 資料庫中，使用 hello[還原 AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet。</span><span class="sxs-lookup"><span data-stu-id="efe9a-139">toorecover a database, use hello [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="efe9a-140">開啟 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="efe9a-140">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="efe9a-141">連接 tooyour Azure 帳戶，然後列出與您的帳戶相關聯的所有 hello 訂閱。</span><span class="sxs-lookup"><span data-stu-id="efe9a-141">Connect tooyour Azure account and list all hello subscriptions associated with your account.</span></span>
3. <span data-ttu-id="efe9a-142">選取包含還原 hello 資料庫 toobe hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="efe9a-142">Select hello subscription that contains hello database toobe restored.</span></span>
4. <span data-ttu-id="efe9a-143">取得您想要的 hello 資料庫 toorecover。</span><span class="sxs-lookup"><span data-stu-id="efe9a-143">Get hello database you want toorecover.</span></span>
5. <span data-ttu-id="efe9a-144">建立 hello hello 資料庫復原要求。</span><span class="sxs-lookup"><span data-stu-id="efe9a-144">Create hello recovery request for hello database.</span></span>
6. <span data-ttu-id="efe9a-145">確認 hello hello 異地還原的資料庫狀態。</span><span class="sxs-lookup"><span data-stu-id="efe9a-145">Verify hello status of hello geo-restored database.</span></span>

```Powershell
Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName "<Subscription_name>"

# Get hello database you want toorecover
$GeoBackup = Get-AzureRmSqlDatabaseGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourServerName>" -DatabaseName "<YourDatabaseName>"

# Recover database
$GeoRestoredDatabase = Restore-AzureRmSqlDatabase –FromGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourTargetServer>" -TargetDatabaseName "<NewDatabaseName>" –ResourceId $GeoBackup.ResourceID

# Verify that hello geo-restored database is online
$GeoRestoredDatabase.status
```

> [!NOTE]
> <span data-ttu-id="efe9a-146">tooconfigure 資料庫之後 hello 還原完成後，請參閱[設定您的資料庫復原後][Configure your database after recovery]。</span><span class="sxs-lookup"><span data-stu-id="efe9a-146">tooconfigure your database after hello restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

<span data-ttu-id="efe9a-147">hello 復原的資料庫會啟用 TDE hello 來源資料庫是啟用 TDE。</span><span class="sxs-lookup"><span data-stu-id="efe9a-147">hello recovered database will be TDE-enabled if hello source database is TDE-enabled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="efe9a-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="efe9a-148">Next steps</span></span>
<span data-ttu-id="efe9a-149">toolearn 有關 hello 業務續航力功能的 Azure SQL Database 的版本，請閱讀 hello [Azure SQL Database 業務持續性概觀][Azure SQL Database business continuity overview]。</span><span class="sxs-lookup"><span data-stu-id="efe9a-149">toolearn about hello business continuity features of Azure SQL Database editions, please read hello [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

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
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery

<!--MSDN references-->
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx

<!--Other Web references-->
[Azure Portal]: https://portal.azure.com/
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
