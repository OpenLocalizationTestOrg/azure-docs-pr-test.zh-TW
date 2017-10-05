---
title: "SQL Database 災害復原 | Microsoft Docs"
description: "了解如何使用 Azure SQL Database 的作用中異地複寫和異地還原功能，從區域資料中心中斷或失敗情況復原資料庫。"
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
ms.openlocfilehash: e33f69bf04b32a31aae3c311c41aa44e4da5016a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="restore-an-azure-sql-database-or-failover-to-a-secondary"></a><span data-ttu-id="9284e-103">還原 Azure SQL Database 或容錯移轉到次要資料庫</span><span class="sxs-lookup"><span data-stu-id="9284e-103">Restore an Azure SQL Database or failover to a secondary</span></span>
<span data-ttu-id="9284e-104">Azure SQL Database 提供下列功能，以從中斷復原：</span><span class="sxs-lookup"><span data-stu-id="9284e-104">Azure SQL Database offers the following capabilities for recovering from an outage:</span></span>

* [<span data-ttu-id="9284e-105">主動式異地複寫</span><span class="sxs-lookup"><span data-stu-id="9284e-105">Active geo-replication</span></span>](sql-database-geo-replication-overview.md)
* [<span data-ttu-id="9284e-106">異地還原</span><span class="sxs-lookup"><span data-stu-id="9284e-106">Geo-restore</span></span>](sql-database-recovery-using-backups.md#point-in-time-restore)

<span data-ttu-id="9284e-107">若要了解商務持續性案例，以及支援這些案例的功能，請參閱 [商務持續性](sql-database-business-continuity.md)。</span><span class="sxs-lookup"><span data-stu-id="9284e-107">To learn about business continuity scenarios and the features supporting these scenarios, see [Business continuity](sql-database-business-continuity.md).</span></span>

### <a name="prepare-for-the-event-of-an-outage"></a><span data-ttu-id="9284e-108">準備中斷事件</span><span class="sxs-lookup"><span data-stu-id="9284e-108">Prepare for the event of an outage</span></span>
<span data-ttu-id="9284e-109">如果要使用主動式異地複寫或異地備援備份成功復原到另一個資料區域，您必須準備一台伺服器，以便在另一個資料中心中斷時成為新的主要伺服器，以及將定義好的步驟寫成文件並經過測試，以確保順利復原。</span><span class="sxs-lookup"><span data-stu-id="9284e-109">For success with recovery to another data region using either active geo-replication or geo-redundant backups, you need to prepare a server in another data center outage to become the new primary server should the need arise as well as have well-defined steps documented and tested to ensure a smooth recovery.</span></span> <span data-ttu-id="9284e-110">這些準備步驟包括︰</span><span class="sxs-lookup"><span data-stu-id="9284e-110">These preparation steps include:</span></span>

* <span data-ttu-id="9284e-111">識別在另一個區域中要成為新主要伺服器的邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="9284e-111">Identify the logical server in another region to become the new primary server.</span></span> <span data-ttu-id="9284e-112">至少要有一部或者每部次要伺服器都具有主動式異地複寫。</span><span class="sxs-lookup"><span data-stu-id="9284e-112">With active geo-replication, this will be at least one and perhaps each of the secondary servers.</span></span> <span data-ttu-id="9284e-113">如果是異地還原，這通常會是在資料庫所在區域的[配對區域](../best-practices-availability-paired-regions.md)中的伺服器。</span><span class="sxs-lookup"><span data-stu-id="9284e-113">For geo-restore, this will generally be a server in the [paired region](../best-practices-availability-paired-regions.md) for the region in which your database is located.</span></span>
* <span data-ttu-id="9284e-114">識別並選擇性地定義所需的伺服器層級防火牆規則，讓使用者可以存取新的主要資料庫。</span><span class="sxs-lookup"><span data-stu-id="9284e-114">Identify, and optionally define, the server-level firewall rules needed on for users to access the new primary database.</span></span>
* <span data-ttu-id="9284e-115">決定要如何重新導向使用者至新的主要伺服器，例如變更連接字串或變更 DNS 項目。</span><span class="sxs-lookup"><span data-stu-id="9284e-115">Determine how you are going to redirect users to the new primary server, such as by changing connection strings or by changing DNS entries.</span></span>
* <span data-ttu-id="9284e-116">識別並選擇性地建立登入，新主要伺服器的 master 資料庫中必須有這些登入，並確保這些登入在 master 資料庫中有適當的權限 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="9284e-116">Identify, and optionally create, the logins that must be present in the master database on the new primary server, and ensure these logins have appropriate permissions in the master database, if any.</span></span> <span data-ttu-id="9284e-117">如需詳細資訊，請參閱 [災害復原後的 SQL Database 安全性](sql-database-geo-replication-security-config.md)</span><span class="sxs-lookup"><span data-stu-id="9284e-117">For more information, see [SQL Database security after disaster recovery](sql-database-geo-replication-security-config.md)</span></span>
* <span data-ttu-id="9284e-118">識別需要更新的警示規則以對應至新的主要資料庫。</span><span class="sxs-lookup"><span data-stu-id="9284e-118">Identify alert rules that will need to be updated to map to the new primary database.</span></span>
* <span data-ttu-id="9284e-119">將目前主要資料庫上的稽核設定整理成文件</span><span class="sxs-lookup"><span data-stu-id="9284e-119">Document the auditing configuration on the current primary database</span></span>
* <span data-ttu-id="9284e-120">執行 [災害復原演練](sql-database-disaster-recovery-drills.md)。</span><span class="sxs-lookup"><span data-stu-id="9284e-120">Perform a [disaster recovery drill](sql-database-disaster-recovery-drills.md).</span></span> <span data-ttu-id="9284e-121">若要模擬異地還原中斷，您可以刪除或重新命名來源資料庫，讓應用程式連線失敗。</span><span class="sxs-lookup"><span data-stu-id="9284e-121">To simulate an outage for geo-restore, you can delete or rename the source database to cause application connectivity failure.</span></span> <span data-ttu-id="9284e-122">若要模擬主動式異地複寫中斷，您可以停用 Web 應用程式或連接到資料庫的的虛擬機器，或是容錯移轉資料庫，讓應用程式連線失敗。</span><span class="sxs-lookup"><span data-stu-id="9284e-122">To simulate an outage for active geo-replication, you can disable the web application or virtual machine connected to the database or failover the database to cause application connectivity failures.</span></span>

## <a name="when-to-initiate-recovery"></a><span data-ttu-id="9284e-123">何時起始復原</span><span class="sxs-lookup"><span data-stu-id="9284e-123">When to initiate recovery</span></span>
<span data-ttu-id="9284e-124">復原作業會影響應用程式。</span><span class="sxs-lookup"><span data-stu-id="9284e-124">The recovery operation impacts the application.</span></span> <span data-ttu-id="9284e-125">它需要變更 SQL 連接字串，或使用 DNS 重新導向，並且可能會導致永久的資料遺失。</span><span class="sxs-lookup"><span data-stu-id="9284e-125">It requires changing the SQL connection string or redirection using DNS and could result in permanent data loss.</span></span> <span data-ttu-id="9284e-126">因此，只有在中斷情況可能持續超過應用程式的復原時間目標時，才應該執行這項作業。</span><span class="sxs-lookup"><span data-stu-id="9284e-126">Therefore, it should be done only when the outage is likely to last longer than your application's recovery time objective.</span></span> <span data-ttu-id="9284e-127">將應用程式部署至生產環境之後，您應該定期監視應用程式健全狀況，並利用下列資料點判斷是否需要復原：</span><span class="sxs-lookup"><span data-stu-id="9284e-127">When the application is deployed to production you should perform regular monitoring of the application health and use the following data points to assert that the recovery is warranted:</span></span>

1. <span data-ttu-id="9284e-128">從應用程式層到資料庫的連接發生永久性失敗。</span><span class="sxs-lookup"><span data-stu-id="9284e-128">Permanent connectivity failure from the application tier to the database.</span></span>
2. <span data-ttu-id="9284e-129">Azure 入口網站顯示有關區域中影響廣泛之事件的警示。</span><span class="sxs-lookup"><span data-stu-id="9284e-129">The Azure portal shows an alert about an incident in the region with broad impact.</span></span>
3. <span data-ttu-id="9284e-130">Azure SQL Database 伺服器標示為已降級。</span><span class="sxs-lookup"><span data-stu-id="9284e-130">The Azure SQL Database server is marked as degraded.</span></span>

<span data-ttu-id="9284e-131">視您應用程式的停機容忍度和可能的商務責任而定，您可以考慮下列復原選項。</span><span class="sxs-lookup"><span data-stu-id="9284e-131">Depending on your application tolerance to downtime and possible business liability you can consider the following recovery options.</span></span>

<span data-ttu-id="9284e-132">使用 [取得可復原資料庫](https://msdn.microsoft.com/library/dn800985.aspx) (*LastAvailableBackupDate*) 以取得異地複寫的最近還原點。</span><span class="sxs-lookup"><span data-stu-id="9284e-132">Use the [Get Recoverable Database](https://msdn.microsoft.com/library/dn800985.aspx) (*LastAvailableBackupDate*) to get the latest Geo-replicated restore point.</span></span>

## <a name="wait-for-service-recovery"></a><span data-ttu-id="9284e-133">等候服務復原</span><span class="sxs-lookup"><span data-stu-id="9284e-133">Wait for service recovery</span></span>
<span data-ttu-id="9284e-134">Azure 團隊會努力儘快還原服務可用性，但需視根本原因而言，有可能需要數小時或數天的時間。</span><span class="sxs-lookup"><span data-stu-id="9284e-134">The Azure teams work diligently to restore service availability as quickly as possible but depending on the root cause it can take hours or days.</span></span>  <span data-ttu-id="9284e-135">如果您的應用程式可以容忍長時間停機，您可以等待復原完成。</span><span class="sxs-lookup"><span data-stu-id="9284e-135">If your application can tolerate significant downtime you can simply wait for the recovery to complete.</span></span> <span data-ttu-id="9284e-136">在此情況下，您不需要採取任何動作。</span><span class="sxs-lookup"><span data-stu-id="9284e-136">In this case, no action on your part is required.</span></span> <span data-ttu-id="9284e-137">您可以在 [Azure 服務健康狀態儀表板](https://azure.microsoft.com/status/)上看見目前的服務狀態。</span><span class="sxs-lookup"><span data-stu-id="9284e-137">You can see the current service status on our [Azure Service Health Dashboard](https://azure.microsoft.com/status/).</span></span> <span data-ttu-id="9284e-138">在區域復原後，您應用程式的可用性將會還原。</span><span class="sxs-lookup"><span data-stu-id="9284e-138">After the recovery of the region your application’s availability will be restored.</span></span>

## <a name="fail-over-to-geo-replicated-secondary-database"></a><span data-ttu-id="9284e-139">容錯移轉至異地複寫的次要資料庫</span><span class="sxs-lookup"><span data-stu-id="9284e-139">Fail over to geo-replicated secondary database</span></span>
<span data-ttu-id="9284e-140">如果您應用程式的停機可能會導致商務責任，您應該在應用程式中使用異地複寫的資料庫。</span><span class="sxs-lookup"><span data-stu-id="9284e-140">If your application’s downtime can result in business liability you should be using geo-replicated database(s) in your application.</span></span> <span data-ttu-id="9284e-141">這可讓應用程式在發生中斷時，快速還原不同區域的可用性。</span><span class="sxs-lookup"><span data-stu-id="9284e-141">It will enable the application to quickly restore availability in a different region in case of an outage.</span></span> <span data-ttu-id="9284e-142">了解如何[設定異地複寫](sql-database-geo-replication-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="9284e-142">Learn how to [configure geo-replication](sql-database-geo-replication-portal.md).</span></span>

<span data-ttu-id="9284e-143">若要還原資料庫的可用性，您必須使用其中一種支援的方法，開始容錯移轉到異地複寫的次要資料庫。</span><span class="sxs-lookup"><span data-stu-id="9284e-143">To restore availability of the database(s) you need to initiate the failover to the geo-replicated secondary using one of the supported methods.</span></span>

<span data-ttu-id="9284e-144">使用下列其中一份指南，容錯移轉至異地複寫的次要資料庫：</span><span class="sxs-lookup"><span data-stu-id="9284e-144">Use one of the following guides to fail over to a geo-replicated secondary database:</span></span>

* [<span data-ttu-id="9284e-145">使用 Azure 入口網站容錯移轉至異地複寫的次要資料庫</span><span class="sxs-lookup"><span data-stu-id="9284e-145">Fail over to a geo-replicated secondary using Azure Portal</span></span>](sql-database-geo-replication-portal.md)
* [<span data-ttu-id="9284e-146">使用 PowerShell 容錯移轉至異地複寫的次要資料庫</span><span class="sxs-lookup"><span data-stu-id="9284e-146">Fail over to a geo-replicated secondary using PowerShell</span></span>](scripts/sql-database-setup-geodr-and-failover-database-powershell.md)
* [<span data-ttu-id="9284e-147">使用 T-SQL 容錯移轉至異地複寫的次要資料庫</span><span class="sxs-lookup"><span data-stu-id="9284e-147">Fail over to a geo-replicated secondary using T-SQL</span></span>](sql-database-geo-replication-transact-sql.md)

## <a name="recover-using-geo-restore"></a><span data-ttu-id="9284e-148">使用異地還原進行復原</span><span class="sxs-lookup"><span data-stu-id="9284e-148">Recover using geo-restore</span></span>
<span data-ttu-id="9284e-149">如果您應用程式的停機不會導致任何商務責任，您可以使用[異地還原](sql-database-recovery-using-backups.md)來作為復原應用程式資料庫的方法。</span><span class="sxs-lookup"><span data-stu-id="9284e-149">If your application’s downtime does not result in business liability you can use [geo-restore](sql-database-recovery-using-backups.md) as a method to recover your application database(s).</span></span> <span data-ttu-id="9284e-150">它會從其最新的異地備援備份建立資料庫的複本。</span><span class="sxs-lookup"><span data-stu-id="9284e-150">It creates a copy of the database from its latest geo-redundant backup.</span></span>

## <a name="configure-your-database-after-recovery"></a><span data-ttu-id="9284e-151">在復原之後設定資料庫</span><span class="sxs-lookup"><span data-stu-id="9284e-151">Configure your database after recovery</span></span>
<span data-ttu-id="9284e-152">如果您使用異地複寫容錯移轉或異地復原來從中斷復原，您必須確定已正確設定新資料庫的連接，才能繼續執行正常的應用程式功能。</span><span class="sxs-lookup"><span data-stu-id="9284e-152">If you are using either geo-replication failover or geo-restore to recover from an outage, you must make sure that the connectivity to the new databases is properly configured so that the normal application function can be resumed.</span></span> <span data-ttu-id="9284e-153">以下工作檢查清單可協助您準備產生復原的資料庫。</span><span class="sxs-lookup"><span data-stu-id="9284e-153">This is a checklist of tasks to get your recovered database production ready.</span></span>

### <a name="update-connection-strings"></a><span data-ttu-id="9284e-154">更新連接字串</span><span class="sxs-lookup"><span data-stu-id="9284e-154">Update connection strings</span></span>
<span data-ttu-id="9284e-155">因為復原的資料庫將位於不同的伺服器，所以您必須更新應用程式的連接字串以指向該伺服器。</span><span class="sxs-lookup"><span data-stu-id="9284e-155">Because your recovered database will reside in a different server, you need to update your application’s connection string to point to that server.</span></span>

<span data-ttu-id="9284e-156">如需變更連接字串的詳細資訊，請參閱 [連線庫](sql-database-libraries.md)的適當開發語言。</span><span class="sxs-lookup"><span data-stu-id="9284e-156">For more information about changing connection strings, see the appropriate development language for your [connection library](sql-database-libraries.md).</span></span>

### <a name="configure-firewall-rules"></a><span data-ttu-id="9284e-157">設定防火牆規則</span><span class="sxs-lookup"><span data-stu-id="9284e-157">Configure Firewall Rules</span></span>
<span data-ttu-id="9284e-158">您需要確認伺服器和資料庫上設定的防火牆規則符合主要伺服器與主要資料庫上設定的防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="9284e-158">You need to make sure that the firewall rules configured on server and on the database match those that were configured on the primary server and primary database.</span></span> <span data-ttu-id="9284e-159">如需詳細資訊，請參閱 [如何：進行防火牆設定 (Azure SQL Database)](sql-database-configure-firewall-settings.md)。</span><span class="sxs-lookup"><span data-stu-id="9284e-159">For more information, see [How to: Configure Firewall Settings (Azure SQL Database)](sql-database-configure-firewall-settings.md).</span></span>

### <a name="configure-logins-and-database-users"></a><span data-ttu-id="9284e-160">設定登入和資料庫使用者</span><span class="sxs-lookup"><span data-stu-id="9284e-160">Configure logins and database users</span></span>
<span data-ttu-id="9284e-161">您需要確定應用程式使用的所有登入，都存在於主控已復原資料庫的伺服器上。</span><span class="sxs-lookup"><span data-stu-id="9284e-161">You need to make sure that all the logins used by your application exist on the server which is hosting your recovered database.</span></span> <span data-ttu-id="9284e-162">如需詳細資訊，請參閱[異地複寫的安全性設定](sql-database-geo-replication-security-config.md)。</span><span class="sxs-lookup"><span data-stu-id="9284e-162">For more information, see [Security Configuration for geo-replication](sql-database-geo-replication-security-config.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9284e-163">您應該在災害復原演練期間設定和測試伺服器防火牆規則與登入 (及其權限)。</span><span class="sxs-lookup"><span data-stu-id="9284e-163">You should configure and test your server firewall rules and logins (and their permissions) during a disaster recovery drill.</span></span> <span data-ttu-id="9284e-164">這些伺服器層級物件及其設定可能無法在中斷期間使用。</span><span class="sxs-lookup"><span data-stu-id="9284e-164">These server-level objects and their configuration may not be available during the outage.</span></span>
> 
> 

### <a name="setup-telemetry-alerts"></a><span data-ttu-id="9284e-165">設定遙測警示</span><span class="sxs-lookup"><span data-stu-id="9284e-165">Setup telemetry alerts</span></span>
<span data-ttu-id="9284e-166">您必須確定現有的警示規則設定已更新，才能對應至復原的資料庫和不同的伺服器。</span><span class="sxs-lookup"><span data-stu-id="9284e-166">You need to make sure your existing alert rule settings are updated to map to the recovered database and the different server.</span></span>

<span data-ttu-id="9284e-167">如需有關資料庫警示規則的詳細資訊，請參閱[接收警示通知](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)和[追蹤服務健全狀況](../monitoring-and-diagnostics/insights-service-health.md)。</span><span class="sxs-lookup"><span data-stu-id="9284e-167">For more information about database alert rules, see [Receive Alert Notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) and [Track Service Health](../monitoring-and-diagnostics/insights-service-health.md).</span></span>

### <a name="enable-auditing"></a><span data-ttu-id="9284e-168">啟用稽核</span><span class="sxs-lookup"><span data-stu-id="9284e-168">Enable auditing</span></span>
<span data-ttu-id="9284e-169">如果需要稽核才能存取您的資料庫，則您必須在資料庫復原之後啟用稽核。</span><span class="sxs-lookup"><span data-stu-id="9284e-169">If auditing is required to access your database, you need to enable Auditing after the database recovery.</span></span> <span data-ttu-id="9284e-170">如需詳細資訊，請參閱[資料庫稽核 (英文)](sql-database-auditing.md)。</span><span class="sxs-lookup"><span data-stu-id="9284e-170">For more information, see [Database auditing](sql-database-auditing.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9284e-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9284e-171">Next steps</span></span>
* <span data-ttu-id="9284e-172">若要了解 Azure SQL Database 自動備份，請參閱 [SQL Database 自動備份](sql-database-automated-backups.md)</span><span class="sxs-lookup"><span data-stu-id="9284e-172">To learn about Azure SQL Database automated backups, see [SQL Database automated backups](sql-database-automated-backups.md)</span></span>
* <span data-ttu-id="9284e-173">若要了解商務持續性設計及復原案例，請參閱 [持續性案例](sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="9284e-173">To learn about business continuity design and recovery scenarios, see [Continuity scenarios](sql-database-business-continuity.md)</span></span>
* <span data-ttu-id="9284e-174">若要了解如何使用自動備份進行復原，請參閱 [從服務起始的備份還原資料庫](sql-database-recovery-using-backups.md)</span><span class="sxs-lookup"><span data-stu-id="9284e-174">To learn about using automated backups for recovery, see [restore a database from the service-initiated backups](sql-database-recovery-using-backups.md)</span></span>

