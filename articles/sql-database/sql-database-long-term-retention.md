---
title: "儲存多達 10 年的 Azure SQL Database 備份 | Microsoft Docs"
description: "了解 Azure SQL Database 如何支援多達 10 年的儲存備份。"
keywords: 
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: 
ms.assetid: 66fdb8b8-5903-4d3a-802e-af08d204566e
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 12/22/2016
ms.author: sashan
ms.openlocfilehash: 25e651203f804fbf32d632b5f83145a3f3f72a7f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="store-azure-sql-database-backups-for-up-to-10-years"></a><span data-ttu-id="75a69-103">儲存多達 10 年的 Azure SQL Database 備份</span><span class="sxs-lookup"><span data-stu-id="75a69-103">Store Azure SQL Database backups for up to 10 years</span></span>
<span data-ttu-id="75a69-104">許多應用程式具有法規、相容性或其他商務用途，需要您保留 Azure SQL Database [自動備份](sql-database-automated-backups.md)所提供超過 7-35 天的資料庫備份。</span><span class="sxs-lookup"><span data-stu-id="75a69-104">Many applications have regulatory, compliance, or other business purposes that require you to retain database backups beyond the 7-35 days provided by Azure SQL Database [automatic backups](sql-database-automated-backups.md).</span></span> <span data-ttu-id="75a69-105">使用長期備份保留功能可讓您將 SQL Database 備份儲存在 Azure 復原服務保存庫中多達 10 年。</span><span class="sxs-lookup"><span data-stu-id="75a69-105">By using the long-term backup retention feature, you can store your SQL database backups in an Azure Recovery Services vault for up to 10 years.</span></span> <span data-ttu-id="75a69-106">每個保存庫最多可以儲存 1000 個資料庫。</span><span class="sxs-lookup"><span data-stu-id="75a69-106">You can store up to 1,000 databases per vault.</span></span> <span data-ttu-id="75a69-107">您接著可以選取資料庫中的任何備份以將其還原為新的保存庫。</span><span class="sxs-lookup"><span data-stu-id="75a69-107">You then can select any backup in the vault to restore it as a new database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="75a69-108">長期備份保留期目前為預覽版本，可在下列區域使用︰澳大利亞東部、澳大利亞東南部、巴西南部、美國中部、東亞、美國東部、美國東部 2、印度中部、印度南部、日本東部、日本西部、美國中北部、北歐、美國中南部、東南亞、西歐和美國西部。</span><span class="sxs-lookup"><span data-stu-id="75a69-108">Long-term backup retention is currently in preview and available in the following regions: Australia East, Australia Southeast, Brazil South, Central US, East Asia, East US, East US 2, India Central, India South, Japan East, Japan West, North Central US, North Europe, South Central US, Southeast Asia, West Europe, and West US.</span></span>
>

> [!NOTE]
> <span data-ttu-id="75a69-109">您可以在 24 小時期間在每個保存庫啟用多達 200 個資料庫。</span><span class="sxs-lookup"><span data-stu-id="75a69-109">You can enable up to 200 databases per vault during a 24-hour period.</span></span> <span data-ttu-id="75a69-110">我們建議您對每一部伺服器使用個別的保存庫，以將這項限制的影響降到最低。</span><span class="sxs-lookup"><span data-stu-id="75a69-110">We recommend that you use a separate vault for each server to minimize the impact of this limit.</span></span> 
> 

## <a name="how-sql-database-long-term-backup-retention-works"></a><span data-ttu-id="75a69-111">SQL Database 長期備份保留的運作方式</span><span class="sxs-lookup"><span data-stu-id="75a69-111">How SQL Database long-term backup retention works</span></span>

<span data-ttu-id="75a69-112">使用長期備份保留可以建立 SQL Database 伺服器與 Azure 復原服務保存庫的關聯。</span><span class="sxs-lookup"><span data-stu-id="75a69-112">With long-term backup retention, you can associate a SQL database server with an Azure Recovery Services vault.</span></span> 

* <span data-ttu-id="75a69-113">您必須在與建立 SQL 伺服器相同的 Azure 訂用帳戶中，以及相同的地理區域和資源群組中建立保存庫。</span><span class="sxs-lookup"><span data-stu-id="75a69-113">You must create the vault in the same Azure subscription that created the SQL server and in the same geographic region and resource group.</span></span> 
* <span data-ttu-id="75a69-114">接著，您可以針對任何資料庫設定保留原則。</span><span class="sxs-lookup"><span data-stu-id="75a69-114">You then configure a retention policy for any database.</span></span> <span data-ttu-id="75a69-115">原則會使每週的完整資料庫備份複製到復原服務保存庫，並保留指定的保留週期 (最多 10 年)。</span><span class="sxs-lookup"><span data-stu-id="75a69-115">The policy causes the weekly full database backups to be copied to the Recovery Services vault and retained for the specified retention period (up to 10 years).</span></span> 
* <span data-ttu-id="75a69-116">接著，您可以從任何備份將資料庫還原至訂用帳戶中任何伺服器的新資料庫。</span><span class="sxs-lookup"><span data-stu-id="75a69-116">You can then restore the database from any of these backups to a new database in any server in the subscription.</span></span> <span data-ttu-id="75a69-117">Azure 儲存體會從現有的備份建立複本，且此複本不影響現有資料庫的效能。</span><span class="sxs-lookup"><span data-stu-id="75a69-117">Azure storage creates a copy from existing backups, and the copy has no performance impact on the existing database.</span></span>

> [!TIP]
> <span data-ttu-id="75a69-118">如需作法指南，請參閱[設定 Azure SQL Database 長期備份保留並從中還原](sql-database-long-term-backup-retention-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="75a69-118">For a how-to guide, see [Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="enable-long-term-backup-retention"></a><span data-ttu-id="75a69-119">啟用長期備份保留</span><span class="sxs-lookup"><span data-stu-id="75a69-119">Enable long-term backup retention</span></span>

<span data-ttu-id="75a69-120">若要設定資料庫的長期備份保留︰</span><span class="sxs-lookup"><span data-stu-id="75a69-120">To configure long-term backup retention for a database:</span></span>

1. <span data-ttu-id="75a69-121">在相同的區域、訂用帳戶與資源群組中建立 Azure 復原服務保存庫做為 SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="75a69-121">Create an Azure Recovery Services vault in the same region, subscription, and resource group as your SQL database server.</span></span> 
2. <span data-ttu-id="75a69-122">向保存庫註冊伺服器。</span><span class="sxs-lookup"><span data-stu-id="75a69-122">Register the server to the vault.</span></span>
3. <span data-ttu-id="75a69-123">建立 Azure 復原服務保護原則。</span><span class="sxs-lookup"><span data-stu-id="75a69-123">Create an Azure Recovery Services protection policy.</span></span>
4. <span data-ttu-id="75a69-124">將保護原則套用到需要長期備份保留的資料庫。</span><span class="sxs-lookup"><span data-stu-id="75a69-124">Apply the protection policy to the databases that require long-term backup retention.</span></span>

<span data-ttu-id="75a69-125">請執行下列作業之一，在 Azure 復原服務保存庫中設定、管理自動備份的長期保留並從該保留還原：</span><span class="sxs-lookup"><span data-stu-id="75a69-125">To configure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault, do either of the following:</span></span>

* <span data-ttu-id="75a69-126">使用 Azure 入口網站：按一下 [長期備份保留] 並選取資料庫，然後按一下 [設定]。</span><span class="sxs-lookup"><span data-stu-id="75a69-126">Using the Azure portal: Click **Long-term backup retention**, select a database, and then click **Configure**.</span></span> 

   ![選取進行長期備份保留的資料庫](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

* <span data-ttu-id="75a69-128">使用 PowerShell：請移至[設定 Azure SQL Database 長期備份保留並從中還原](sql-database-long-term-backup-retention-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="75a69-128">Using PowerShell: Go to [Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="restore-a-database-thats-stored-with-the-long-term-backup-retention-feature"></a><span data-ttu-id="75a69-129">還原以長期備份保留功能儲存的資料庫</span><span class="sxs-lookup"><span data-stu-id="75a69-129">Restore a database that's stored with the long-term backup retention feature</span></span>

<span data-ttu-id="75a69-130">從長期備份保留備份復原︰</span><span class="sxs-lookup"><span data-stu-id="75a69-130">To recover from a long-term backup retention backup:</span></span>

1. <span data-ttu-id="75a69-131">列出儲存備份的保存庫。</span><span class="sxs-lookup"><span data-stu-id="75a69-131">List the vault where the backup is stored.</span></span>
2. <span data-ttu-id="75a69-132">列出對應至您邏輯伺服器的容器。</span><span class="sxs-lookup"><span data-stu-id="75a69-132">List the container that is mapped to your logical server.</span></span>
3. <span data-ttu-id="75a69-133">列出對應至資料庫之保存庫內的資料來源。</span><span class="sxs-lookup"><span data-stu-id="75a69-133">List the data source within the vault that is mapped to your database.</span></span>
4. <span data-ttu-id="75a69-134">列出可用來還原的復原點。</span><span class="sxs-lookup"><span data-stu-id="75a69-134">List the recovery points that are available to restore.</span></span>
5. <span data-ttu-id="75a69-135">從復原點將資料庫還原到您訂用帳戶內的目標伺服器。</span><span class="sxs-lookup"><span data-stu-id="75a69-135">Restore the database from the recovery point to the target server within your subscription.</span></span>

<span data-ttu-id="75a69-136">請執行下列作業之一，在 Azure 復原服務保存庫中設定、管理自動備份的長期保留並從該保留還原：</span><span class="sxs-lookup"><span data-stu-id="75a69-136">To configure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault, do either of the following:</span></span>

* <span data-ttu-id="75a69-137">使用 Azure 入口網站：請移至[使用 Azure 入口網站管理長期備份保留](sql-database-long-term-backup-retention-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="75a69-137">Using the Azure portal: Go to [Manage long-term backup retention using the Azure portal](sql-database-long-term-backup-retention-configure.md).</span></span> 

* <span data-ttu-id="75a69-138">使用 PowerShell：請移至[使用 PowerShell 管理長期備份保留](sql-database-long-term-backup-retention-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="75a69-138">Using PowerShell: Go to [Manage long-term backup retention using PowerShell](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="get-pricing-for-long-term-backup-retention"></a><span data-ttu-id="75a69-139">取得長期備份保留的價格</span><span class="sxs-lookup"><span data-stu-id="75a69-139">Get pricing for long-term backup retention</span></span>

<span data-ttu-id="75a69-140">SQL Database 的長期備份保留是根據 [Azure 備份服務定價費率](https://azure.microsoft.com/pricing/details/backup/)收費。</span><span class="sxs-lookup"><span data-stu-id="75a69-140">Long-term backup retention of a SQL database is charged according to the [Azure backup services pricing rates](https://azure.microsoft.com/pricing/details/backup/).</span></span>

<span data-ttu-id="75a69-141">SQL Database 伺服器註冊至保存庫之後，您需支付儲存在保存庫中之每週備份所使用的總儲存體。</span><span class="sxs-lookup"><span data-stu-id="75a69-141">After the SQL database server is registered to the vault, you are charged for the total storage that's used by the weekly backups stored in the vault.</span></span>

## <a name="view-available-backups-that-are-stored-in-long-term-backup-retention"></a><span data-ttu-id="75a69-142">檢視以長期備份保留儲存的可用備份</span><span class="sxs-lookup"><span data-stu-id="75a69-142">View available backups that are stored in long-term backup retention</span></span>

<span data-ttu-id="75a69-143">請執行下列作業之一，使用 Azure 入口網站，在 Azure 復原服務保存庫中設定、管理自動備份的長期保留，並從該保留還原：</span><span class="sxs-lookup"><span data-stu-id="75a69-143">To configure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault by using the Azure portal, do either of the following:</span></span>

* <span data-ttu-id="75a69-144">使用 Azure 入口網站：請移至[使用 Azure 入口網站管理長期備份保留](sql-database-long-term-backup-retention-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="75a69-144">Using the Azure portal: Go to [Manage long-term backup retention using the Azure portal](sql-database-long-term-backup-retention-configure.md).</span></span> 

* <span data-ttu-id="75a69-145">使用 PowerShell：請移至[使用 PowerShell 管理長期備份保留](sql-database-long-term-backup-retention-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="75a69-145">Using PowerShell: Go to [Manage long-term backup retention using PowerShell](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="disable-long-term-retention"></a><span data-ttu-id="75a69-146">停用長期保留</span><span class="sxs-lookup"><span data-stu-id="75a69-146">Disable long-term retention</span></span>

<span data-ttu-id="75a69-147">復原服務會根據提供的保留原則自動處理備份的清除。</span><span class="sxs-lookup"><span data-stu-id="75a69-147">The recovery service automatically handles the cleanup of backups based on the provided retention policy.</span></span> 

<span data-ttu-id="75a69-148">若要停止將特定資料庫的備份傳送到保存庫，請移除該資料庫的保留原則。</span><span class="sxs-lookup"><span data-stu-id="75a69-148">To stop sending the backups for a specific database to the vault, remove the retention policy for that database.</span></span>
  
```
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName 'RG1' -ServerName 'Server1' -DatabaseName 'DB1' -State 'Disabled' -ResourceId $policy.Id
```

> [!NOTE]
> <span data-ttu-id="75a69-149">保存庫中已有的備份不會受到影響。</span><span class="sxs-lookup"><span data-stu-id="75a69-149">The backups that are already in the vault are unaffected.</span></span> <span data-ttu-id="75a69-150">當保留期限到期時，復原服務會自動刪除它們。</span><span class="sxs-lookup"><span data-stu-id="75a69-150">They are automatically deleted by the recovery service when their retention period expires.</span></span>

## <a name="long-term-backup-retention-faq"></a><span data-ttu-id="75a69-151">長期備份保留常見問題集</span><span class="sxs-lookup"><span data-stu-id="75a69-151">Long-term backup retention FAQ</span></span>

<span data-ttu-id="75a69-152">**可以手動刪除保存庫中的特定備份嗎？**</span><span class="sxs-lookup"><span data-stu-id="75a69-152">**Can I manually delete specific backups in the vault?**</span></span>

<span data-ttu-id="75a69-153">目前不支援。</span><span class="sxs-lookup"><span data-stu-id="75a69-153">Not currently.</span></span> <span data-ttu-id="75a69-154">當保留期限已過期時，保存庫會自動清除備份。</span><span class="sxs-lookup"><span data-stu-id="75a69-154">The vault automatically cleans up backups when the retention period has expired.</span></span>

<span data-ttu-id="75a69-155">**是否可以註冊我的伺服器來將備份儲存至多個保存庫？**</span><span class="sxs-lookup"><span data-stu-id="75a69-155">**Can I register my server to store backups to more than one vault?**</span></span>

<span data-ttu-id="75a69-156">否，備份目前一次只能儲存到一個保存庫。</span><span class="sxs-lookup"><span data-stu-id="75a69-156">No, you can currently store backups to only one vault at a time.</span></span>

<span data-ttu-id="75a69-157">**我可以在不同的訂用帳戶中有保存庫與伺服器嗎？**</span><span class="sxs-lookup"><span data-stu-id="75a69-157">**Can I have a vault and server in different subscriptions?**</span></span>

<span data-ttu-id="75a69-158">否，目前保存庫與伺服器必須位於相同的訂用帳戶和資源群組。</span><span class="sxs-lookup"><span data-stu-id="75a69-158">No, currently the vault and server must be in the same subscription and resource group.</span></span>

<span data-ttu-id="75a69-159">**我可以使用在不同於伺服器區域的區域中建立的保存庫嗎？**</span><span class="sxs-lookup"><span data-stu-id="75a69-159">**Can I use a vault that I created in a region that's different from my server’s region?**</span></span>

<span data-ttu-id="75a69-160">否，保存庫與伺服器必須位於相同的區域，以將複製時間降至最低，並避免產生流量費用。</span><span class="sxs-lookup"><span data-stu-id="75a69-160">No, the vault and server must be in the same region to minimize copy time and avoid traffic charges.</span></span>

<span data-ttu-id="75a69-161">**我可以在一個保存庫中儲存幾個資料庫？**</span><span class="sxs-lookup"><span data-stu-id="75a69-161">**How many databases can I store in one vault?**</span></span>

<span data-ttu-id="75a69-162">目前每個保存庫最多可支援 1000 個資料庫。</span><span class="sxs-lookup"><span data-stu-id="75a69-162">Currently, we support up to 1,000 databases per vault.</span></span> 

<span data-ttu-id="75a69-163">**每個訂用帳戶可以建立幾個保存庫？**</span><span class="sxs-lookup"><span data-stu-id="75a69-163">**How many vaults can I create per subscription?**</span></span>

<span data-ttu-id="75a69-164">每個訂用帳戶最多可以建立 25 個保存庫。</span><span class="sxs-lookup"><span data-stu-id="75a69-164">You can create up to 25 vaults per subscription.</span></span>

<span data-ttu-id="75a69-165">**每個保存庫每天可以設定幾個資料庫？**</span><span class="sxs-lookup"><span data-stu-id="75a69-165">**How many databases can I configure per day per vault?**</span></span>

<span data-ttu-id="75a69-166">每個保存庫每天最多可以設定 200 個資料庫。</span><span class="sxs-lookup"><span data-stu-id="75a69-166">You can set up 200 databases per day per vault.</span></span>

<span data-ttu-id="75a69-167">**長期備份保留是否可與彈性集區搭配運作？**</span><span class="sxs-lookup"><span data-stu-id="75a69-167">**Does long-term backup retention work with elastic pools?**</span></span>

<span data-ttu-id="75a69-168">是。</span><span class="sxs-lookup"><span data-stu-id="75a69-168">Yes.</span></span> <span data-ttu-id="75a69-169">集區中的任何資料庫可以使用保留原則設定。</span><span class="sxs-lookup"><span data-stu-id="75a69-169">Any database in the pool can be configured with the retention policy.</span></span>

<span data-ttu-id="75a69-170">**是否可以選擇建立備份的時間？**</span><span class="sxs-lookup"><span data-stu-id="75a69-170">**Can I choose the time at which the backup is created?**</span></span>

<span data-ttu-id="75a69-171">否，SQL Database 會控制備份排程，以便將資料庫上的效能影響降到最低。</span><span class="sxs-lookup"><span data-stu-id="75a69-171">No, SQL Database controls the backup schedule to minimize the performance impact on your databases.</span></span>

<span data-ttu-id="75a69-172">**我的資料庫啟用了透明資料加密。可以用在保存庫嗎？**</span><span class="sxs-lookup"><span data-stu-id="75a69-172">**I have transparent data encryption enabled for my database. Can I use it with the vault?**</span></span> 

<span data-ttu-id="75a69-173">是，支援透明資料加密。</span><span class="sxs-lookup"><span data-stu-id="75a69-173">Yes, transparent data encryption is supported.</span></span> <span data-ttu-id="75a69-174">即使原始資料庫不存在，您也可以從保存庫還原資料庫。</span><span class="sxs-lookup"><span data-stu-id="75a69-174">You can restore the database from the vault even if the original database no longer exists.</span></span>

<span data-ttu-id="75a69-175">**如果我的訂用帳戶已暫止，則保存庫中的備份會發生什麼事？**</span><span class="sxs-lookup"><span data-stu-id="75a69-175">**What happens with the backups in the vault if my subscription is suspended?**</span></span> 

<span data-ttu-id="75a69-176">如果您的訂用帳戶已暫停，我們會保留現有的資料庫和備份。</span><span class="sxs-lookup"><span data-stu-id="75a69-176">If your subscription is suspended, we retain the existing databases and backups.</span></span> <span data-ttu-id="75a69-177">新的備份不會複製到保存庫。</span><span class="sxs-lookup"><span data-stu-id="75a69-177">New backups are not copied to the vault.</span></span> <span data-ttu-id="75a69-178">在您重新啟動訂用帳戶之後，服務會繼續將備份複製到保存庫。</span><span class="sxs-lookup"><span data-stu-id="75a69-178">After you reactivate the subscription, the service resumes copying backups to the vault.</span></span> <span data-ttu-id="75a69-179">您的保存庫會在訂用帳戶暫止之前，使用已在該處複製的備份，供還原作業存取。</span><span class="sxs-lookup"><span data-stu-id="75a69-179">Your vault becomes accessible to the restore operations by using the backups that were copied there before the subscription was suspended.</span></span> 

<span data-ttu-id="75a69-180">**是否可存取 SQL Database 備份檔案，以便下載或還原至 SQL Server？**</span><span class="sxs-lookup"><span data-stu-id="75a69-180">**Can I get access to the SQL database backup files so I can download or restore them to the SQL server?**</span></span>

<span data-ttu-id="75a69-181">否，目前無法。</span><span class="sxs-lookup"><span data-stu-id="75a69-181">No, not currently.</span></span>

<span data-ttu-id="75a69-182">**SQL 保留原則內是否可以有多個排程 (每日、每週、每月、每年)？**</span><span class="sxs-lookup"><span data-stu-id="75a69-182">**Is it possible to have multiple schedules (daily, weekly, monthly, yearly) within a SQL retention policy.**</span></span>

<span data-ttu-id="75a69-183">否，目前僅虛擬機器備份提供多個排程。</span><span class="sxs-lookup"><span data-stu-id="75a69-183">No, multiple schedules are currently available only for virtual machine backups.</span></span>

<span data-ttu-id="75a69-184">**如果我們在使用中的異地複寫次要資料庫上設定長期備份保留，會發生什麼情況？**</span><span class="sxs-lookup"><span data-stu-id="75a69-184">**What if we set up long-term backup retention on a database that is an active geo-replication secondary database?**</span></span>

<span data-ttu-id="75a69-185">因為複本不留備份，所以目前沒有在次要資料庫上進行長期備份保留的選項。</span><span class="sxs-lookup"><span data-stu-id="75a69-185">Because we don't take backups on replicas, there is currently no option for long-term backup retention on secondary databases.</span></span> <span data-ttu-id="75a69-186">不過，對使用者來說，對使用中的異地複寫次要資料庫設定長期備份保留相當重要，原因如下：</span><span class="sxs-lookup"><span data-stu-id="75a69-186">However, it is important for users to set up long-term backup retention on an active geo-replication secondary database for these reasons:</span></span>
* <span data-ttu-id="75a69-187">當容錯移轉發生而資料庫變成主要資料庫時，我們會進行完整備份，並將此完整備份上傳到保存庫。</span><span class="sxs-lookup"><span data-stu-id="75a69-187">When a failover happens and the database becomes a primary database, we take a full backup, which is uploaded to vault.</span></span>
* <span data-ttu-id="75a69-188">客戶不用為設定次要資料庫的長期備份保留另行付費。</span><span class="sxs-lookup"><span data-stu-id="75a69-188">There is no extra cost to the customer for setting up long-term backup retention on a secondary database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="75a69-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="75a69-189">Next steps</span></span>
<span data-ttu-id="75a69-190">因為資料庫備份可保護資料免於意外損毀或刪除，是商務持續性和災害復原策略中不可或缺的一環。</span><span class="sxs-lookup"><span data-stu-id="75a69-190">Because database backups protect data from accidental corruption or deletion, they're an essential part of any business continuity and disaster recovery strategy.</span></span> <span data-ttu-id="75a69-191">若要深入了解其他 SQL Database 商務持續性解決方案，請參閱[商務持續性概觀](sql-database-business-continuity.md)。</span><span class="sxs-lookup"><span data-stu-id="75a69-191">To learn about the other SQL Database business-continuity solutions, see [Business continuity overview](sql-database-business-continuity.md).</span></span>
