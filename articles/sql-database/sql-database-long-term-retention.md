---
title: "總 too10 年的 aaaStore Azure SQL Database 備份 |Microsoft 文件"
description: "了解 Azure SQL Database 支援儲存備份的 too10 年的方式。"
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
ms.openlocfilehash: 5825ebd4e3bd66b59b13aea603d377ef814a1df3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="store-azure-sql-database-backups-for-up-too10-years"></a><span data-ttu-id="a83cd-103">儲存註冊 too10 年的 Azure SQL Database 備份</span><span class="sxs-lookup"><span data-stu-id="a83cd-103">Store Azure SQL Database backups for up too10 years</span></span>
<span data-ttu-id="a83cd-104">許多應用程式有法規，相容性或其他商務用途，需要 tooretain 資料庫備份，超出 hello Azure SQL Database 所提供的 7-35 天[自動備份](sql-database-automated-backups.md)。</span><span class="sxs-lookup"><span data-stu-id="a83cd-104">Many applications have regulatory, compliance, or other business purposes that require you tooretain database backups beyond hello 7-35 days provided by Azure SQL Database [automatic backups](sql-database-automated-backups.md).</span></span> <span data-ttu-id="a83cd-105">使用 hello 長期備份保留功能，您可以向上 too10 年的 Azure 復原服務保存庫中儲存您的 SQL 資料庫備份。</span><span class="sxs-lookup"><span data-stu-id="a83cd-105">By using hello long-term backup retention feature, you can store your SQL database backups in an Azure Recovery Services vault for up too10 years.</span></span> <span data-ttu-id="a83cd-106">您可以儲存長達 too1，000 資料庫每個保存庫。</span><span class="sxs-lookup"><span data-stu-id="a83cd-106">You can store up too1,000 databases per vault.</span></span> <span data-ttu-id="a83cd-107">然後，您可以選取任何備份在 hello 保存庫 toorestore 它做為新的資料庫。</span><span class="sxs-lookup"><span data-stu-id="a83cd-107">You then can select any backup in hello vault toorestore it as a new database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a83cd-108">長期備份的保留為目前處於預覽狀態，並提供下列區域的 hello： 澳洲東部、 澳洲東南部、 巴西南部、 美國中部、 東亞、 美國東部、 美國東部 2、 印度中部、 印度南部、 日本東部、 日本西部、 美國中北部、 North歐洲、 中南部、 東南亞、 西歐、 和美國西部。</span><span class="sxs-lookup"><span data-stu-id="a83cd-108">Long-term backup retention is currently in preview and available in hello following regions: Australia East, Australia Southeast, Brazil South, Central US, East Asia, East US, East US 2, India Central, India South, Japan East, Japan West, North Central US, North Europe, South Central US, Southeast Asia, West Europe, and West US.</span></span>
>

> [!NOTE]
> <span data-ttu-id="a83cd-109">您可以在 24 小時期間內啟用 too200 資料庫，每個保存庫。</span><span class="sxs-lookup"><span data-stu-id="a83cd-109">You can enable up too200 databases per vault during a 24-hour period.</span></span> <span data-ttu-id="a83cd-110">我們建議您針對這項限制每個伺服器 toominimize hello 影響使用不同的保存庫。</span><span class="sxs-lookup"><span data-stu-id="a83cd-110">We recommend that you use a separate vault for each server toominimize hello impact of this limit.</span></span> 
> 

## <a name="how-sql-database-long-term-backup-retention-works"></a><span data-ttu-id="a83cd-111">SQL Database 長期備份保留的運作方式</span><span class="sxs-lookup"><span data-stu-id="a83cd-111">How SQL Database long-term backup retention works</span></span>

<span data-ttu-id="a83cd-112">使用長期備份保留可以建立 SQL Database 伺服器與 Azure 復原服務保存庫的關聯。</span><span class="sxs-lookup"><span data-stu-id="a83cd-112">With long-term backup retention, you can associate a SQL database server with an Azure Recovery Services vault.</span></span> 

* <span data-ttu-id="a83cd-113">您必須建立 hello 保存庫在 hello 相同 Azure 訂用帳戶建立 hello SQL server，並在 hello 相同地理區域和資源群組。</span><span class="sxs-lookup"><span data-stu-id="a83cd-113">You must create hello vault in hello same Azure subscription that created hello SQL server and in hello same geographic region and resource group.</span></span> 
* <span data-ttu-id="a83cd-114">接著，您可以針對任何資料庫設定保留原則。</span><span class="sxs-lookup"><span data-stu-id="a83cd-114">You then configure a retention policy for any database.</span></span> <span data-ttu-id="a83cd-115">hello 原則原因 hello 每週完整資料庫備份 toobe 複製 toohello 復原服務保存庫，並保留 hello 指定的保留週期 （向上 too10 年）。</span><span class="sxs-lookup"><span data-stu-id="a83cd-115">hello policy causes hello weekly full database backups toobe copied toohello Recovery Services vault and retained for hello specified retention period (up too10 years).</span></span> 
* <span data-ttu-id="a83cd-116">然後，您就可以從這些備份 tooa 新的資料庫中任何伺服器 hello 訂用帳戶中的任何還原 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="a83cd-116">You can then restore hello database from any of these backups tooa new database in any server in hello subscription.</span></span> <span data-ttu-id="a83cd-117">Azure 儲存體從現有的備份，建立複本並 hello 複製 hello 現有資料庫上具有任何效能影響。</span><span class="sxs-lookup"><span data-stu-id="a83cd-117">Azure storage creates a copy from existing backups, and hello copy has no performance impact on hello existing database.</span></span>

> [!TIP]
> <span data-ttu-id="a83cd-118">Tooguide 如何，請參閱[設定與還原自 Azure SQL Database 的長期備份保留](sql-database-long-term-backup-retention-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="a83cd-118">For a how-tooguide, see [Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="enable-long-term-backup-retention"></a><span data-ttu-id="a83cd-119">啟用長期備份保留</span><span class="sxs-lookup"><span data-stu-id="a83cd-119">Enable long-term backup retention</span></span>

<span data-ttu-id="a83cd-120">tooconfigure 長期的備份保留的資料庫：</span><span class="sxs-lookup"><span data-stu-id="a83cd-120">tooconfigure long-term backup retention for a database:</span></span>

1. <span data-ttu-id="a83cd-121">建立 Azure 復原服務保存庫在 hello 與 SQL 資料庫伺服器相同的地區、 訂用帳戶和資源群組。</span><span class="sxs-lookup"><span data-stu-id="a83cd-121">Create an Azure Recovery Services vault in hello same region, subscription, and resource group as your SQL database server.</span></span> 
2. <span data-ttu-id="a83cd-122">註冊 hello 伺服器 toohello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="a83cd-122">Register hello server toohello vault.</span></span>
3. <span data-ttu-id="a83cd-123">建立 Azure 復原服務保護原則。</span><span class="sxs-lookup"><span data-stu-id="a83cd-123">Create an Azure Recovery Services protection policy.</span></span>
4. <span data-ttu-id="a83cd-124">適用於 hello 保護原則 toohello 資料庫需要長期備份的保留。</span><span class="sxs-lookup"><span data-stu-id="a83cd-124">Apply hello protection policy toohello databases that require long-term backup retention.</span></span>

<span data-ttu-id="a83cd-125">tooconfigure，管理，並還原 Azure 復原服務保存庫中的自動備份的長期備份保留的資料庫，執行 hello 下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="a83cd-125">tooconfigure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault, do either of hello following:</span></span>

* <span data-ttu-id="a83cd-126">使用 hello Azure 入口網站： 按一下**長期備份的保留**，選取 [資料庫]，然後按一下**設定**。</span><span class="sxs-lookup"><span data-stu-id="a83cd-126">Using hello Azure portal: Click **Long-term backup retention**, select a database, and then click **Configure**.</span></span> 

   ![選取進行長期備份保留的資料庫](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

* <span data-ttu-id="a83cd-128">使用 PowerShell： 跳過[設定與還原自 Azure SQL Database 的長期備份保留](sql-database-long-term-backup-retention-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="a83cd-128">Using PowerShell: Go too[Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="restore-a-database-thats-stored-with-hello-long-term-backup-retention-feature"></a><span data-ttu-id="a83cd-129">還原資料庫儲存的 hello 長期備份保留的功能</span><span class="sxs-lookup"><span data-stu-id="a83cd-129">Restore a database that's stored with hello long-term backup retention feature</span></span>

<span data-ttu-id="a83cd-130">從長期的備份保留備份 toorecover:</span><span class="sxs-lookup"><span data-stu-id="a83cd-130">toorecover from a long-term backup retention backup:</span></span>

1. <span data-ttu-id="a83cd-131">Hello 備份儲存位置清單 hello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="a83cd-131">List hello vault where hello backup is stored.</span></span>
2. <span data-ttu-id="a83cd-132">是對應的 tooyour 邏輯伺服器的清單 hello 容器。</span><span class="sxs-lookup"><span data-stu-id="a83cd-132">List hello container that is mapped tooyour logical server.</span></span>
3. <span data-ttu-id="a83cd-133">清單 hello hello 保存庫所對應的 tooyour 資料庫內的資料來源。</span><span class="sxs-lookup"><span data-stu-id="a83cd-133">List hello data source within hello vault that is mapped tooyour database.</span></span>
4. <span data-ttu-id="a83cd-134">會使用 toorestore 清單 hello 復原點。</span><span class="sxs-lookup"><span data-stu-id="a83cd-134">List hello recovery points that are available toorestore.</span></span>
5. <span data-ttu-id="a83cd-135">Hello 從還原資料庫 hello 復原點 toohello 您訂用帳戶內的目標伺服器。</span><span class="sxs-lookup"><span data-stu-id="a83cd-135">Restore hello database from hello recovery point toohello target server within your subscription.</span></span>

<span data-ttu-id="a83cd-136">tooconfigure，管理，並還原 Azure 復原服務保存庫中的自動備份的長期備份保留的資料庫，執行 hello 下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="a83cd-136">tooconfigure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault, do either of hello following:</span></span>

* <span data-ttu-id="a83cd-137">使用 hello Azure 入口網站： 跳過[長期備份保留使用管理 hello Azure 入口網站](sql-database-long-term-backup-retention-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="a83cd-137">Using hello Azure portal: Go too[Manage long-term backup retention using hello Azure portal](sql-database-long-term-backup-retention-configure.md).</span></span> 

* <span data-ttu-id="a83cd-138">使用 PowerShell： 跳過[管理使用 PowerShell 的長期備份保留](sql-database-long-term-backup-retention-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="a83cd-138">Using PowerShell: Go too[Manage long-term backup retention using PowerShell](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="get-pricing-for-long-term-backup-retention"></a><span data-ttu-id="a83cd-139">取得長期備份保留的價格</span><span class="sxs-lookup"><span data-stu-id="a83cd-139">Get pricing for long-term backup retention</span></span>

<span data-ttu-id="a83cd-140">SQL database 的長期備份保留負責根據 toohello[定價率的 Azure 備份服務](https://azure.microsoft.com/pricing/details/backup/)。</span><span class="sxs-lookup"><span data-stu-id="a83cd-140">Long-term backup retention of a SQL database is charged according toohello [Azure backup services pricing rates](https://azure.microsoft.com/pricing/details/backup/).</span></span>

<span data-ttu-id="a83cd-141">Hello SQL 資料庫伺服器已註冊的 toohello 保存庫之後，您必須支付 hello hello 每週備份儲存在 hello 保存庫使用的總儲存。</span><span class="sxs-lookup"><span data-stu-id="a83cd-141">After hello SQL database server is registered toohello vault, you are charged for hello total storage that's used by hello weekly backups stored in hello vault.</span></span>

## <a name="view-available-backups-that-are-stored-in-long-term-backup-retention"></a><span data-ttu-id="a83cd-142">檢視以長期備份保留儲存的可用備份</span><span class="sxs-lookup"><span data-stu-id="a83cd-142">View available backups that are stored in long-term backup retention</span></span>

<span data-ttu-id="a83cd-143">tooconfigure，會管理，並使用 hello Azure 入口網站的 Azure 復原服務保存庫中的自動備份的長期備份保留還原的資料庫，執行 hello 下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="a83cd-143">tooconfigure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault by using hello Azure portal, do either of hello following:</span></span>

* <span data-ttu-id="a83cd-144">使用 hello Azure 入口網站： 跳過[長期備份保留使用管理 hello Azure 入口網站](sql-database-long-term-backup-retention-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="a83cd-144">Using hello Azure portal: Go too[Manage long-term backup retention using hello Azure portal](sql-database-long-term-backup-retention-configure.md).</span></span> 

* <span data-ttu-id="a83cd-145">使用 PowerShell： 跳過[管理使用 PowerShell 的長期備份保留](sql-database-long-term-backup-retention-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="a83cd-145">Using PowerShell: Go too[Manage long-term backup retention using PowerShell](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="disable-long-term-retention"></a><span data-ttu-id="a83cd-146">停用長期保留</span><span class="sxs-lookup"><span data-stu-id="a83cd-146">Disable long-term retention</span></span>

<span data-ttu-id="a83cd-147">hello 復原服務會自動處理 hello 清除的 hello 提供保留原則為基礎的備份。</span><span class="sxs-lookup"><span data-stu-id="a83cd-147">hello recovery service automatically handles hello cleanup of backups based on hello provided retention policy.</span></span> 

<span data-ttu-id="a83cd-148">toostop 傳送嗨備份特定資料庫 toohello 保存庫中，移除該資料庫的 hello 保留原則。</span><span class="sxs-lookup"><span data-stu-id="a83cd-148">toostop sending hello backups for a specific database toohello vault, remove hello retention policy for that database.</span></span>
  
```
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName 'RG1' -ServerName 'Server1' -DatabaseName 'DB1' -State 'Disabled' -ResourceId $policy.Id
```

> [!NOTE]
> <span data-ttu-id="a83cd-149">已經在 hello 保存庫中的 hello 備份不受影響。</span><span class="sxs-lookup"><span data-stu-id="a83cd-149">hello backups that are already in hello vault are unaffected.</span></span> <span data-ttu-id="a83cd-150">會自動刪除由 hello 復原服務的保留期限到期時。</span><span class="sxs-lookup"><span data-stu-id="a83cd-150">They are automatically deleted by hello recovery service when their retention period expires.</span></span>

## <a name="long-term-backup-retention-faq"></a><span data-ttu-id="a83cd-151">長期備份保留常見問題集</span><span class="sxs-lookup"><span data-stu-id="a83cd-151">Long-term backup retention FAQ</span></span>

<span data-ttu-id="a83cd-152">**我可以手動刪除 hello 保存庫中的特定備份嗎？**</span><span class="sxs-lookup"><span data-stu-id="a83cd-152">**Can I manually delete specific backups in hello vault?**</span></span>

<span data-ttu-id="a83cd-153">目前不支援。</span><span class="sxs-lookup"><span data-stu-id="a83cd-153">Not currently.</span></span> <span data-ttu-id="a83cd-154">hello 保存庫會 hello 保留期限已過期時，會自動清除備份。</span><span class="sxs-lookup"><span data-stu-id="a83cd-154">hello vault automatically cleans up backups when hello retention period has expired.</span></span>

<span data-ttu-id="a83cd-155">**可以註冊一個保存庫與 my server toostore 備份 toomore 嗎？**</span><span class="sxs-lookup"><span data-stu-id="a83cd-155">**Can I register my server toostore backups toomore than one vault?**</span></span>

<span data-ttu-id="a83cd-156">否，您可以一次目前儲存備份 tooonly 一個保存庫。</span><span class="sxs-lookup"><span data-stu-id="a83cd-156">No, you can currently store backups tooonly one vault at a time.</span></span>

<span data-ttu-id="a83cd-157">**我可以在不同的訂用帳戶中有保存庫與伺服器嗎？**</span><span class="sxs-lookup"><span data-stu-id="a83cd-157">**Can I have a vault and server in different subscriptions?**</span></span>

<span data-ttu-id="a83cd-158">否，目前 hello 保存庫和伺服器必須位在 hello 相同的訂用帳戶和資源群組。</span><span class="sxs-lookup"><span data-stu-id="a83cd-158">No, currently hello vault and server must be in hello same subscription and resource group.</span></span>

<span data-ttu-id="a83cd-159">**我可以使用在不同於伺服器區域的區域中建立的保存庫嗎？**</span><span class="sxs-lookup"><span data-stu-id="a83cd-159">**Can I use a vault that I created in a region that's different from my server’s region?**</span></span>

<span data-ttu-id="a83cd-160">否，hello 保存庫和伺服器必須在 hello 相同區域 toominimize 複製時間並避免流量費用。</span><span class="sxs-lookup"><span data-stu-id="a83cd-160">No, hello vault and server must be in hello same region toominimize copy time and avoid traffic charges.</span></span>

<span data-ttu-id="a83cd-161">**我可以在一個保存庫中儲存幾個資料庫？**</span><span class="sxs-lookup"><span data-stu-id="a83cd-161">**How many databases can I store in one vault?**</span></span>

<span data-ttu-id="a83cd-162">目前，我們支援 too1，000 資料庫每個保存庫註冊。</span><span class="sxs-lookup"><span data-stu-id="a83cd-162">Currently, we support up too1,000 databases per vault.</span></span> 

<span data-ttu-id="a83cd-163">**每個訂用帳戶可以建立幾個保存庫？**</span><span class="sxs-lookup"><span data-stu-id="a83cd-163">**How many vaults can I create per subscription?**</span></span>

<span data-ttu-id="a83cd-164">您可以建立每個訂閱 too25 保存庫註冊。</span><span class="sxs-lookup"><span data-stu-id="a83cd-164">You can create up too25 vaults per subscription.</span></span>

<span data-ttu-id="a83cd-165">**每個保存庫每天可以設定幾個資料庫？**</span><span class="sxs-lookup"><span data-stu-id="a83cd-165">**How many databases can I configure per day per vault?**</span></span>

<span data-ttu-id="a83cd-166">每個保存庫每天最多可以設定 200 個資料庫。</span><span class="sxs-lookup"><span data-stu-id="a83cd-166">You can set up 200 databases per day per vault.</span></span>

<span data-ttu-id="a83cd-167">**長期備份保留是否可與彈性集區搭配運作？**</span><span class="sxs-lookup"><span data-stu-id="a83cd-167">**Does long-term backup retention work with elastic pools?**</span></span>

<span data-ttu-id="a83cd-168">是。</span><span class="sxs-lookup"><span data-stu-id="a83cd-168">Yes.</span></span> <span data-ttu-id="a83cd-169">Hello 集區中的任何資料庫可以具有 hello 保留原則設定。</span><span class="sxs-lookup"><span data-stu-id="a83cd-169">Any database in hello pool can be configured with hello retention policy.</span></span>

<span data-ttu-id="a83cd-170">**可以選擇 hello 備份建立 hello 時間嗎？**</span><span class="sxs-lookup"><span data-stu-id="a83cd-170">**Can I choose hello time at which hello backup is created?**</span></span>

<span data-ttu-id="a83cd-171">否，SQL Database 控制 hello 備份排程 toominimize hello 對效能影響您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="a83cd-171">No, SQL Database controls hello backup schedule toominimize hello performance impact on your databases.</span></span>

<span data-ttu-id="a83cd-172">**我的資料庫啟用了透明資料加密。我可以使用它與 hello 保存庫？**</span><span class="sxs-lookup"><span data-stu-id="a83cd-172">**I have transparent data encryption enabled for my database. Can I use it with hello vault?**</span></span> 

<span data-ttu-id="a83cd-173">是，支援透明資料加密。</span><span class="sxs-lookup"><span data-stu-id="a83cd-173">Yes, transparent data encryption is supported.</span></span> <span data-ttu-id="a83cd-174">即使 hello 原始資料庫不存在，您可以從 hello 保存庫還原 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="a83cd-174">You can restore hello database from hello vault even if hello original database no longer exists.</span></span>

<span data-ttu-id="a83cd-175">**發生什麼情況與 hello 保存庫中的 hello 備份我的訂用帳戶已暫止？**</span><span class="sxs-lookup"><span data-stu-id="a83cd-175">**What happens with hello backups in hello vault if my subscription is suspended?**</span></span> 

<span data-ttu-id="a83cd-176">如果您的訂用帳戶已暫止，我們會保留 hello 現有的資料庫和備份。</span><span class="sxs-lookup"><span data-stu-id="a83cd-176">If your subscription is suspended, we retain hello existing databases and backups.</span></span> <span data-ttu-id="a83cd-177">新的備份不會複製的 toohello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="a83cd-177">New backups are not copied toohello vault.</span></span> <span data-ttu-id="a83cd-178">您重新啟動 hello 訂用帳戶之後，hello 服務會繼續複製備份 toohello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="a83cd-178">After you reactivate hello subscription, hello service resumes copying backups toohello vault.</span></span> <span data-ttu-id="a83cd-179">您的保存庫會使用 hello 訂用帳戶暫止之前那里複製的 hello 備份變成可存取 toohello 還原作業。</span><span class="sxs-lookup"><span data-stu-id="a83cd-179">Your vault becomes accessible toohello restore operations by using hello backups that were copied there before hello subscription was suspended.</span></span> 

<span data-ttu-id="a83cd-180">**可以取得存取 toohello SQL 資料庫的備份檔案，我可以下載，或將它們還原 toohello SQL 伺服器？**</span><span class="sxs-lookup"><span data-stu-id="a83cd-180">**Can I get access toohello SQL database backup files so I can download or restore them toohello SQL server?**</span></span>

<span data-ttu-id="a83cd-181">否，目前無法。</span><span class="sxs-lookup"><span data-stu-id="a83cd-181">No, not currently.</span></span>

<span data-ttu-id="a83cd-182">**它是可能 toohave SQL 保留原則內多個排程每日、 每週、 每月 （每年）。**</span><span class="sxs-lookup"><span data-stu-id="a83cd-182">**Is it possible toohave multiple schedules (daily, weekly, monthly, yearly) within a SQL retention policy.**</span></span>

<span data-ttu-id="a83cd-183">否，目前僅虛擬機器備份提供多個排程。</span><span class="sxs-lookup"><span data-stu-id="a83cd-183">No, multiple schedules are currently available only for virtual machine backups.</span></span>

<span data-ttu-id="a83cd-184">**如果我們在使用中的異地複寫次要資料庫上設定長期備份保留，會發生什麼情況？**</span><span class="sxs-lookup"><span data-stu-id="a83cd-184">**What if we set up long-term backup retention on a database that is an active geo-replication secondary database?**</span></span>

<span data-ttu-id="a83cd-185">因為複本不留備份，所以目前沒有在次要資料庫上進行長期備份保留的選項。</span><span class="sxs-lookup"><span data-stu-id="a83cd-185">Because we don't take backups on replicas, there is currently no option for long-term backup retention on secondary databases.</span></span> <span data-ttu-id="a83cd-186">不過，最好向上作用中地理複寫的次要資料庫上的長期備份保留使用者 tooset 基於這些理由：</span><span class="sxs-lookup"><span data-stu-id="a83cd-186">However, it is important for users tooset up long-term backup retention on an active geo-replication secondary database for these reasons:</span></span>
* <span data-ttu-id="a83cd-187">當發生容錯移轉時 hello 資料庫會變成主要資料庫，我們進行完整備份，也就是上傳的 toovault。</span><span class="sxs-lookup"><span data-stu-id="a83cd-187">When a failover happens and hello database becomes a primary database, we take a full backup, which is uploaded toovault.</span></span>
* <span data-ttu-id="a83cd-188">沒有不需額外成本 toohello 客戶設定次要資料庫上的長期備份保留。</span><span class="sxs-lookup"><span data-stu-id="a83cd-188">There is no extra cost toohello customer for setting up long-term backup retention on a secondary database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a83cd-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a83cd-189">Next steps</span></span>
<span data-ttu-id="a83cd-190">因為資料庫備份可保護資料免於意外損毀或刪除，是商務持續性和災害復原策略中不可或缺的一環。</span><span class="sxs-lookup"><span data-stu-id="a83cd-190">Because database backups protect data from accidental corruption or deletion, they're an essential part of any business continuity and disaster recovery strategy.</span></span> <span data-ttu-id="a83cd-191">toolearn hello 其他 SQL Database 業務持續性解決方案，請參閱[商務持續性概觀](sql-database-business-continuity.md)。</span><span class="sxs-lookup"><span data-stu-id="a83cd-191">toolearn about hello other SQL Database business-continuity solutions, see [Business continuity overview](sql-database-business-continuity.md).</span></span>
