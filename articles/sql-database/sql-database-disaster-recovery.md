---
title: "aaaSQL Database 災害復原 |Microsoft 文件"
description: "了解如何 toorecover 資料庫地區資料中心中斷或發生錯誤 hello Azure SQL Database 作用中地理複寫及異地復原功能。"
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: 4800960e-3f9d-40ce-9e55-fb7f2784c067
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/14/2017
ms.author: sashan
ms.openlocfilehash: bae08485863067748107ec4808e52d8e88e2de0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-database-or-failover-tooa-secondary"></a><span data-ttu-id="dd104-103">還原次要的 Azure SQL Database 或容錯移轉 tooa</span><span class="sxs-lookup"><span data-stu-id="dd104-103">Restore an Azure SQL Database or failover tooa secondary</span></span>
<span data-ttu-id="dd104-104">Azure SQL Database 提供下列功能從中斷復原 hello:</span><span class="sxs-lookup"><span data-stu-id="dd104-104">Azure SQL Database offers hello following capabilities for recovering from an outage:</span></span>

* [<span data-ttu-id="dd104-105">主動式異地複寫</span><span class="sxs-lookup"><span data-stu-id="dd104-105">Active geo-replication</span></span>](sql-database-geo-replication-overview.md)
* [<span data-ttu-id="dd104-106">異地還原</span><span class="sxs-lookup"><span data-stu-id="dd104-106">Geo-restore</span></span>](sql-database-recovery-using-backups.md#point-in-time-restore)

<span data-ttu-id="dd104-107">toolearn 有關業務持續性案例和 hello 功能支援這些案例中，請參閱[業務續航力](sql-database-business-continuity.md)。</span><span class="sxs-lookup"><span data-stu-id="dd104-107">toolearn about business continuity scenarios and hello features supporting these scenarios, see [Business continuity](sql-database-business-continuity.md).</span></span>

### <a name="prepare-for-hello-event-of-an-outage"></a><span data-ttu-id="dd104-108">準備中斷的 hello 事件</span><span class="sxs-lookup"><span data-stu-id="dd104-108">Prepare for hello event of an outage</span></span>
<span data-ttu-id="dd104-109">對於成功使用作用中地理複寫或異地備援備份復原 tooanother 資料區時，您需要 tooprepare 中另一個資料中心中斷 toobecome hello 新的主要伺服器的伺服器應該 hello 需要發生，以及具有妥善定義的步驟已歸檔，並經過測試 tooensure smooth 復原。</span><span class="sxs-lookup"><span data-stu-id="dd104-109">For success with recovery tooanother data region using either active geo-replication or geo-redundant backups, you need tooprepare a server in another data center outage toobecome hello new primary server should hello need arise as well as have well-defined steps documented and tested tooensure a smooth recovery.</span></span> <span data-ttu-id="dd104-110">這些準備步驟包括︰</span><span class="sxs-lookup"><span data-stu-id="dd104-110">These preparation steps include:</span></span>

* <span data-ttu-id="dd104-111">識別在另一個區域 toobecome hello 新的主要伺服器中的 hello 邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="dd104-111">Identify hello logical server in another region toobecome hello new primary server.</span></span> <span data-ttu-id="dd104-112">使用中的異地複寫，這會是至少一個，或許每一個 hello 次要伺服器。</span><span class="sxs-lookup"><span data-stu-id="dd104-112">With active geo-replication, this will be at least one and perhaps each of hello secondary servers.</span></span> <span data-ttu-id="dd104-113">地理還原，這通常是伺服器在 hello[配對的區域](../best-practices-availability-paired-regions.md)hello 資料庫所在的區域。</span><span class="sxs-lookup"><span data-stu-id="dd104-113">For geo-restore, this will generally be a server in hello [paired region](../best-practices-availability-paired-regions.md) for hello region in which your database is located.</span></span>
* <span data-ttu-id="dd104-114">識別，並選擇性地定義，hello 伺服器層級防火牆規則，需要在使用者 tooaccess hello 新的主要資料庫。</span><span class="sxs-lookup"><span data-stu-id="dd104-114">Identify, and optionally define, hello server-level firewall rules needed on for users tooaccess hello new primary database.</span></span>
* <span data-ttu-id="dd104-115">決定要如何 tooredirect 使用者 toohello 新的主要伺服器，例如變更連接字串，或是變更 DNS 項目。</span><span class="sxs-lookup"><span data-stu-id="dd104-115">Determine how you are going tooredirect users toohello new primary server, such as by changing connection strings or by changing DNS entries.</span></span>
* <span data-ttu-id="dd104-116">識別，並選擇性地建立，hello 登入必須存在於 hello master 資料庫 hello 新主要伺服器上，並且確定這些登入適當的權限 hello master 資料庫中，如果有的話。</span><span class="sxs-lookup"><span data-stu-id="dd104-116">Identify, and optionally create, hello logins that must be present in hello master database on hello new primary server, and ensure these logins have appropriate permissions in hello master database, if any.</span></span> <span data-ttu-id="dd104-117">如需詳細資訊，請參閱 [災害復原後的 SQL Database 安全性](sql-database-geo-replication-security-config.md)</span><span class="sxs-lookup"><span data-stu-id="dd104-117">For more information, see [SQL Database security after disaster recovery](sql-database-geo-replication-security-config.md)</span></span>
* <span data-ttu-id="dd104-118">識別需要 toobe 更新的 toomap toohello 新的主要資料庫的警示規則。</span><span class="sxs-lookup"><span data-stu-id="dd104-118">Identify alert rules that will need toobe updated toomap toohello new primary database.</span></span>
* <span data-ttu-id="dd104-119">Hello 目前的主要資料庫上的文件 hello 稽核設定</span><span class="sxs-lookup"><span data-stu-id="dd104-119">Document hello auditing configuration on hello current primary database</span></span>
* <span data-ttu-id="dd104-120">執行 [災害復原演練](sql-database-disaster-recovery-drills.md)。</span><span class="sxs-lookup"><span data-stu-id="dd104-120">Perform a [disaster recovery drill](sql-database-disaster-recovery-drills.md).</span></span> <span data-ttu-id="dd104-121">toosimulate 異地還原的中斷，您可以刪除或重新命名 hello 來源資料庫 toocause 應用程式連線失敗。</span><span class="sxs-lookup"><span data-stu-id="dd104-121">toosimulate an outage for geo-restore, you can delete or rename hello source database toocause application connectivity failure.</span></span> <span data-ttu-id="dd104-122">toosimulate 中斷的作用中地理複寫，您可以停用 hello web 應用程式或連接的虛擬機器 toohello 資料庫或容錯移轉 hello 資料庫 toocause 應用程式連線失敗。</span><span class="sxs-lookup"><span data-stu-id="dd104-122">toosimulate an outage for active geo-replication, you can disable hello web application or virtual machine connected toohello database or failover hello database toocause application connectivity failures.</span></span>

## <a name="when-tooinitiate-recovery"></a><span data-ttu-id="dd104-123">當 tooinitiate 復原</span><span class="sxs-lookup"><span data-stu-id="dd104-123">When tooinitiate recovery</span></span>
<span data-ttu-id="dd104-124">hello 復原作業會影響 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="dd104-124">hello recovery operation impacts hello application.</span></span> <span data-ttu-id="dd104-125">它需要變更 hello SQL 連接字串或使用 DNS 的重新導向，並可能導致資料永久遺失。</span><span class="sxs-lookup"><span data-stu-id="dd104-125">It requires changing hello SQL connection string or redirection using DNS and could result in permanent data loss.</span></span> <span data-ttu-id="dd104-126">因此，它應該在完成時，才 hello 中斷可能 toolast 超過您的應用程式復原時間目標。</span><span class="sxs-lookup"><span data-stu-id="dd104-126">Therefore, it should be done only when hello outage is likely toolast longer than your application's recovery time objective.</span></span> <span data-ttu-id="dd104-127">當 hello 的應用程式部署的 tooproduction 您應該執行的 hello 應用程式健全狀況規則監視，並使用 hello 下列 hello 復原的點 tooassert 已獲得保證的資料：</span><span class="sxs-lookup"><span data-stu-id="dd104-127">When hello application is deployed tooproduction you should perform regular monitoring of hello application health and use hello following data points tooassert that hello recovery is warranted:</span></span>

1. <span data-ttu-id="dd104-128">從 hello 應用程式層 toohello 資料庫永久的連線失敗。</span><span class="sxs-lookup"><span data-stu-id="dd104-128">Permanent connectivity failure from hello application tier toohello database.</span></span>
2. <span data-ttu-id="dd104-129">hello Azure 入口網站在 hello 廣泛的影響區域中顯示事件的相關警示。</span><span class="sxs-lookup"><span data-stu-id="dd104-129">hello Azure portal shows an alert about an incident in hello region with broad impact.</span></span>
3. <span data-ttu-id="dd104-130">hello Azure SQL Database 伺服器標示為降級狀態。</span><span class="sxs-lookup"><span data-stu-id="dd104-130">hello Azure SQL Database server is marked as degraded.</span></span>

<span data-ttu-id="dd104-131">根據您應用程式容錯 toodowntime 和可能的商務負擔，您可以考慮 hello 下列修復選項。</span><span class="sxs-lookup"><span data-stu-id="dd104-131">Depending on your application tolerance toodowntime and possible business liability you can consider hello following recovery options.</span></span>

<span data-ttu-id="dd104-132">使用 hello[取得可復原的資料庫](https://msdn.microsoft.com/library/dn800985.aspx)(*LastAvailableBackupDate*) tooget hello 最新的地理複寫的還原點。</span><span class="sxs-lookup"><span data-stu-id="dd104-132">Use hello [Get Recoverable Database](https://msdn.microsoft.com/library/dn800985.aspx) (*LastAvailableBackupDate*) tooget hello latest Geo-replicated restore point.</span></span>

## <a name="wait-for-service-recovery"></a><span data-ttu-id="dd104-133">等候服務復原</span><span class="sxs-lookup"><span data-stu-id="dd104-133">Wait for service recovery</span></span>
<span data-ttu-id="dd104-134">hello Azure 團隊工作努力 toorestore 服務可用性為快速越好，但根據 hello 根本原因可能需要數小時或天。</span><span class="sxs-lookup"><span data-stu-id="dd104-134">hello Azure teams work diligently toorestore service availability as quickly as possible but depending on hello root cause it can take hours or days.</span></span>  <span data-ttu-id="dd104-135">如果您的應用程式可以容忍您只可以等候 hello 復原 toocomplete 顯著的停機時間。</span><span class="sxs-lookup"><span data-stu-id="dd104-135">If your application can tolerate significant downtime you can simply wait for hello recovery toocomplete.</span></span> <span data-ttu-id="dd104-136">在此情況下，您不需要採取任何動作。</span><span class="sxs-lookup"><span data-stu-id="dd104-136">In this case, no action on your part is required.</span></span> <span data-ttu-id="dd104-137">您可以看到 hello 目前服務的狀態上我們[Azure 服務健全狀況儀表板](https://azure.microsoft.com/status/)。</span><span class="sxs-lookup"><span data-stu-id="dd104-137">You can see hello current service status on our [Azure Service Health Dashboard](https://azure.microsoft.com/status/).</span></span> <span data-ttu-id="dd104-138">Hello 區域 hello 復原後將還原應用程式的可用性。</span><span class="sxs-lookup"><span data-stu-id="dd104-138">After hello recovery of hello region your application’s availability will be restored.</span></span>

## <a name="fail-over-toogeo-replicated-secondary-database"></a><span data-ttu-id="dd104-139">容錯移轉 toogeo 複寫的次要資料庫</span><span class="sxs-lookup"><span data-stu-id="dd104-139">Fail over toogeo-replicated secondary database</span></span>
<span data-ttu-id="dd104-140">如果您應用程式的停機可能會導致商務責任，您應該在應用程式中使用異地複寫的資料庫。</span><span class="sxs-lookup"><span data-stu-id="dd104-140">If your application’s downtime can result in business liability you should be using geo-replicated database(s) in your application.</span></span> <span data-ttu-id="dd104-141">它可讓 hello 應用程式 tooquickly 還原可用性不同的區域發生中斷。</span><span class="sxs-lookup"><span data-stu-id="dd104-141">It will enable hello application tooquickly restore availability in a different region in case of an outage.</span></span> <span data-ttu-id="dd104-142">了解如何太[設定異地複寫](sql-database-geo-replication-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="dd104-142">Learn how too[configure geo-replication](sql-database-geo-replication-portal.md).</span></span>

<span data-ttu-id="dd104-143">hello toorestore 可用性資料庫，您需要 tooinitiate hello 容錯移轉 toohello 異地備援次要使用其中一種支援的 hello 方法。</span><span class="sxs-lookup"><span data-stu-id="dd104-143">toorestore availability of hello database(s) you need tooinitiate hello failover toohello geo-replicated secondary using one of hello supported methods.</span></span>

<span data-ttu-id="dd104-144">使用其中一種下列指南 toofail tooa 異地備援的次要資料庫上的 hello:</span><span class="sxs-lookup"><span data-stu-id="dd104-144">Use one of hello following guides toofail over tooa geo-replicated secondary database:</span></span>

* [<span data-ttu-id="dd104-145">容錯移轉 tooa 異地備援次要資料庫使用 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="dd104-145">Fail over tooa geo-replicated secondary using Azure Portal</span></span>](sql-database-geo-replication-portal.md)
* [<span data-ttu-id="dd104-146">容錯移轉 tooa 異地備援的次要資料庫使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd104-146">Fail over tooa geo-replicated secondary using PowerShell</span></span>](scripts/sql-database-setup-geodr-and-failover-database-powershell.md)
* [<span data-ttu-id="dd104-147">容錯移轉 tooa 異地備援次要資料庫使用 T-SQL</span><span class="sxs-lookup"><span data-stu-id="dd104-147">Fail over tooa geo-replicated secondary using T-SQL</span></span>](sql-database-geo-replication-transact-sql.md)

## <a name="recover-using-geo-restore"></a><span data-ttu-id="dd104-148">使用異地還原進行復原</span><span class="sxs-lookup"><span data-stu-id="dd104-148">Recover using geo-restore</span></span>
<span data-ttu-id="dd104-149">如果您的應用程式停機時間並不會導致商務責任您可以使用[異地還原](sql-database-recovery-using-backups.md)方法 toorecover 為您的應用程式資料庫。</span><span class="sxs-lookup"><span data-stu-id="dd104-149">If your application’s downtime does not result in business liability you can use [geo-restore](sql-database-recovery-using-backups.md) as a method toorecover your application database(s).</span></span> <span data-ttu-id="dd104-150">從其最新的異地備援備份建立 hello 資料庫的複本。</span><span class="sxs-lookup"><span data-stu-id="dd104-150">It creates a copy of hello database from its latest geo-redundant backup.</span></span>

## <a name="configure-your-database-after-recovery"></a><span data-ttu-id="dd104-151">在復原之後設定資料庫</span><span class="sxs-lookup"><span data-stu-id="dd104-151">Configure your database after recovery</span></span>
<span data-ttu-id="dd104-152">如果您使用地理複寫容錯移轉或異地還原 toorecover 從中斷，您必須確定 hello 連線 toohello 新的資料庫已正確設定，以便可以繼續 hello 一般應用程式函式。</span><span class="sxs-lookup"><span data-stu-id="dd104-152">If you are using either geo-replication failover or geo-restore toorecover from an outage, you must make sure that hello connectivity toohello new databases is properly configured so that hello normal application function can be resumed.</span></span> <span data-ttu-id="dd104-153">這是復原的資料庫的實際執行的工作 tooget 的檢查清單。</span><span class="sxs-lookup"><span data-stu-id="dd104-153">This is a checklist of tasks tooget your recovered database production ready.</span></span>

### <a name="update-connection-strings"></a><span data-ttu-id="dd104-154">更新連接字串</span><span class="sxs-lookup"><span data-stu-id="dd104-154">Update connection strings</span></span>
<span data-ttu-id="dd104-155">因為您已復原的資料庫會位於不同的伺服器，您需要 tooupdate 應用程式的連接字串 toopoint toothat 伺服器。</span><span class="sxs-lookup"><span data-stu-id="dd104-155">Because your recovered database will reside in a different server, you need tooupdate your application’s connection string toopoint toothat server.</span></span>

<span data-ttu-id="dd104-156">如需有關如何變更連接字串的詳細資訊，請參閱適當的開發語言 hello 您[連線庫](sql-database-libraries.md)。</span><span class="sxs-lookup"><span data-stu-id="dd104-156">For more information about changing connection strings, see hello appropriate development language for your [connection library](sql-database-libraries.md).</span></span>

### <a name="configure-firewall-rules"></a><span data-ttu-id="dd104-157">設定防火牆規則</span><span class="sxs-lookup"><span data-stu-id="dd104-157">Configure Firewall Rules</span></span>
<span data-ttu-id="dd104-158">您需要 toomake 確定 hello 防火牆規則設定伺服器和 hello 資料庫相符項目上的 hello 主要伺服器與主要資料庫上的設定。</span><span class="sxs-lookup"><span data-stu-id="dd104-158">You need toomake sure that hello firewall rules configured on server and on hello database match those that were configured on hello primary server and primary database.</span></span> <span data-ttu-id="dd104-159">如需詳細資訊，請參閱 [如何：進行防火牆設定 (Azure SQL Database)](sql-database-configure-firewall-settings.md)。</span><span class="sxs-lookup"><span data-stu-id="dd104-159">For more information, see [How to: Configure Firewall Settings (Azure SQL Database)](sql-database-configure-firewall-settings.md).</span></span>

### <a name="configure-logins-and-database-users"></a><span data-ttu-id="dd104-160">設定登入和資料庫使用者</span><span class="sxs-lookup"><span data-stu-id="dd104-160">Configure logins and database users</span></span>
<span data-ttu-id="dd104-161">您必須確定所有應用程式所使用的 hello 登入都存在 hello 伺服器裝載您復原的資料庫上 toomake。</span><span class="sxs-lookup"><span data-stu-id="dd104-161">You need toomake sure that all hello logins used by your application exist on hello server which is hosting your recovered database.</span></span> <span data-ttu-id="dd104-162">如需詳細資訊，請參閱[異地複寫的安全性設定](sql-database-geo-replication-security-config.md)。</span><span class="sxs-lookup"><span data-stu-id="dd104-162">For more information, see [Security Configuration for geo-replication](sql-database-geo-replication-security-config.md).</span></span>

> [!NOTE]
> <span data-ttu-id="dd104-163">您應該在災害復原演練期間設定和測試伺服器防火牆規則與登入 (及其權限)。</span><span class="sxs-lookup"><span data-stu-id="dd104-163">You should configure and test your server firewall rules and logins (and their permissions) during a disaster recovery drill.</span></span> <span data-ttu-id="dd104-164">這些伺服器層級物件，而且其設定可能無法使用 hello 中斷期間。</span><span class="sxs-lookup"><span data-stu-id="dd104-164">These server-level objects and their configuration may not be available during hello outage.</span></span>
> 
> 

### <a name="setup-telemetry-alerts"></a><span data-ttu-id="dd104-165">設定遙測警示</span><span class="sxs-lookup"><span data-stu-id="dd104-165">Setup telemetry alerts</span></span>
<span data-ttu-id="dd104-166">您需要 toomake 確定您現有的警示規則設定是更新的 toomap toohello 復原的資料庫與 hello 不同的伺服器。</span><span class="sxs-lookup"><span data-stu-id="dd104-166">You need toomake sure your existing alert rule settings are updated toomap toohello recovered database and hello different server.</span></span>

<span data-ttu-id="dd104-167">如需有關資料庫警示規則的詳細資訊，請參閱[接收警示通知](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)和[追蹤服務健全狀況](../monitoring-and-diagnostics/insights-service-health.md)。</span><span class="sxs-lookup"><span data-stu-id="dd104-167">For more information about database alert rules, see [Receive Alert Notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) and [Track Service Health](../monitoring-and-diagnostics/insights-service-health.md).</span></span>

### <a name="enable-auditing"></a><span data-ttu-id="dd104-168">啟用稽核</span><span class="sxs-lookup"><span data-stu-id="dd104-168">Enable auditing</span></span>
<span data-ttu-id="dd104-169">如果稽核為必要的 tooaccess 您的資料庫，您需要 tooenable hello 資料庫復原後的稽核。</span><span class="sxs-lookup"><span data-stu-id="dd104-169">If auditing is required tooaccess your database, you need tooenable Auditing after hello database recovery.</span></span> <span data-ttu-id="dd104-170">如需詳細資訊，請參閱[資料庫稽核 (英文)](sql-database-auditing.md)。</span><span class="sxs-lookup"><span data-stu-id="dd104-170">For more information, see [Database auditing](sql-database-auditing.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd104-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dd104-171">Next steps</span></span>
* <span data-ttu-id="dd104-172">toolearn 有關自動化 Azure SQL Database 備份，請參閱[SQL 資料庫自動備份](sql-database-automated-backups.md)</span><span class="sxs-lookup"><span data-stu-id="dd104-172">toolearn about Azure SQL Database automated backups, see [SQL Database automated backups](sql-database-automated-backups.md)</span></span>
* <span data-ttu-id="dd104-173">toolearn 有關業務持續性設計及修復案例，請參閱[持續性案例](sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="dd104-173">toolearn about business continuity design and recovery scenarios, see [Continuity scenarios](sql-database-business-continuity.md)</span></span>
* <span data-ttu-id="dd104-174">toolearn 有關使用自動的備份進行復原，請參閱[hello 服務起始的備份還原的資料庫](sql-database-recovery-using-backups.md)</span><span class="sxs-lookup"><span data-stu-id="dd104-174">toolearn about using automated backups for recovery, see [restore a database from hello service-initiated backups](sql-database-recovery-using-backups.md)</span></span>

