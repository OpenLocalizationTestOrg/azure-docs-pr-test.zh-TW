---
title: "Azure SQL Database 防火牆規則 | Microsoft Docs"
description: "了解如何以伺服器層級和資料庫層級防火牆規則設定 SQL Database 防火牆，以管理存取權。"
keywords: "資料庫防火牆"
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: ac57f84c-35c3-4975-9903-241c8059011e
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 04/10/2017
ms.author: rickbyh
ms.openlocfilehash: 583c91376418d20d34db17d57d3fa14a1e71cd3b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-sql-database-server-level-and-database-level-firewall-rules"></a><span data-ttu-id="3ee51-104">Azure SQL Database 伺服器層級和資料庫層級防火牆規則</span><span class="sxs-lookup"><span data-stu-id="3ee51-104">Azure SQL Database server-level and database-level firewall rules</span></span> 

<span data-ttu-id="3ee51-105">Microsoft Azure SQL Database 為 Azure 和其他網際網路式應用程式提供關聯式資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="3ee51-105">Microsoft Azure SQL Database provides a relational database service for Azure and other Internet-based applications.</span></span> <span data-ttu-id="3ee51-106">為了協助保護您的資料，防火牆會防止對您的資料庫伺服器的所有存取，直到您指定哪些電腦擁有權限。</span><span class="sxs-lookup"><span data-stu-id="3ee51-106">To help protect your data, firewalls prevent all access to your database server until you specify which computers have permission.</span></span> <span data-ttu-id="3ee51-107">此防火牆會根據每一個要求的來源 IP 位址來授與資料庫存取權。</span><span class="sxs-lookup"><span data-stu-id="3ee51-107">The firewall grants access to databases based on the originating IP address of each request.</span></span>

## <a name="overview"></a><span data-ttu-id="3ee51-108">概觀</span><span class="sxs-lookup"><span data-stu-id="3ee51-108">Overview</span></span>

<span data-ttu-id="3ee51-109">一開始，防火牆會封鎖對您的 Azure SQL Server 的所有 Transact-SQL 存取。</span><span class="sxs-lookup"><span data-stu-id="3ee51-109">Initially, all Transact-SQL access to your Azure SQL server is blocked by the firewall.</span></span> <span data-ttu-id="3ee51-110">若要開始使用 Azure SQL Server，您必須指定一或多個伺服器層級防火牆規則，啟用您的 Azure SQL Server 存取。</span><span class="sxs-lookup"><span data-stu-id="3ee51-110">To begin using your Azure SQL server, you must specify one or more server-level firewall rules that enable access to your Azure SQL server.</span></span> <span data-ttu-id="3ee51-111">使用防火牆規則來指定允許網際網路的哪些 IP 位址範圍，以及 Azure 應用程式是否可以嘗試連接到 Azure SQL Server。</span><span class="sxs-lookup"><span data-stu-id="3ee51-111">Use the firewall rules to specify which IP address ranges from the Internet are allowed, and whether Azure applications can attempt to connect to your Azure SQL server.</span></span>

<span data-ttu-id="3ee51-112">若只要選擇性地授與 Azure SQL 伺服器上其中一個資料庫的存取權，您必須為所需的資料庫建立資料庫層級規則。</span><span class="sxs-lookup"><span data-stu-id="3ee51-112">To selectively grant access to just one of the databases in your Azure SQL server, you must create a database-level rule for the required database.</span></span> <span data-ttu-id="3ee51-113">請為資料庫防火牆規則指定一個 IP 位址範圍，該範圍需在伺服器層級防火牆規則中指定的範圍之外，並確認用戶端的 IP 位址在資料庫層級規則中指定的範圍之內。</span><span class="sxs-lookup"><span data-stu-id="3ee51-113">Specify an IP address range for the database firewall rule that is beyond the IP address range specified in the server-level firewall rule, and ensure that the IP address of the client falls in the range specified in the database-level rule.</span></span>

<span data-ttu-id="3ee51-114">來自網際網路和 Azure 的連線嘗試必須先通過防火牆，才能到達您的 Azure SQL Server 或 SQL Database，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="3ee51-114">Connection attempts from the Internet and Azure must first pass through the firewall before they can reach your Azure SQL server or SQL Database, as shown in the following diagram:</span></span>

   ![圖解防火牆設定。][1]

* <span data-ttu-id="3ee51-116">**伺服器層級防火牆規則：** 這些規則可讓用戶端存取整個 Azure SQL Server，也就是相同邏輯伺服器內的所有資料庫。</span><span class="sxs-lookup"><span data-stu-id="3ee51-116">**Server-level firewall rules:** These rules enable clients to access your entire Azure SQL server, that is, all the databases within the same logical server.</span></span> <span data-ttu-id="3ee51-117">這些規則會儲存在 **master** 資料庫。</span><span class="sxs-lookup"><span data-stu-id="3ee51-117">These rules are stored in the **master** database.</span></span> <span data-ttu-id="3ee51-118">使用入口網站或使用 Transact-SQL 陳述式即可設定伺服器層級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="3ee51-118">Server-level firewall rules can be configured by using the portal or by using Transact-SQL statements.</span></span> <span data-ttu-id="3ee51-119">若要使用 Azure 入口網站或 PowerShell 建立伺服器層級的防火牆規則，您必須是訂用帳戶擁有者或訂用帳戶參與者。</span><span class="sxs-lookup"><span data-stu-id="3ee51-119">To create server-level firewall rules using the Azure portal or PowerShell, you must be the subscription owner or a subscription contributor.</span></span> <span data-ttu-id="3ee51-120">若要使用 Transact-SQL 建立伺服器層級的防火牆規則，您必須以伺服器層級的主體登入或 Azure Active Directory 系統管理員身分連接到 SQL 資料庫執行個體 (這表示具有 Azure 層級權限的使用者必須先建立伺服器層級的防火牆規則)。</span><span class="sxs-lookup"><span data-stu-id="3ee51-120">To create a server-level firewall rule using Transact-SQL, you must connect to the SQL Database instance as the server-level principal login or the Azure Active Directory administrator (which means that a server-level firewall rule must first be created by a user with Azure-level permissions).</span></span>
* <span data-ttu-id="3ee51-121">**資料庫層級防火牆規則：** 這些規則可讓用戶端存取同部邏輯伺服器內的特定 (安全) 資料庫。</span><span class="sxs-lookup"><span data-stu-id="3ee51-121">**Database-level firewall rules:** These rules enable clients to access certain (secure) databases within the same logical server.</span></span> <span data-ttu-id="3ee51-122">您可針對每個資料庫 (包括 **master** database0) 建立這些規則，其會存放在個別的資料庫中。</span><span class="sxs-lookup"><span data-stu-id="3ee51-122">You can create these rules for each database (including the **master** database0) and they are stored in the individual databases.</span></span> <span data-ttu-id="3ee51-123">資料庫層級防火牆規則只能使用 Transact-SQL 陳述式設定，且僅可在您已設定第一個伺服器層級防火牆之後進行設定。</span><span class="sxs-lookup"><span data-stu-id="3ee51-123">Database-level firewall rules can only be configured by using Transact-SQL statements and only after you have configured the first server-level firewall.</span></span> <span data-ttu-id="3ee51-124">如果您在資料庫層級防火牆規則中指定的 IP 位址範圍是在伺服器層級防火牆規則中指定的範圍之外，只有具有資料庫層級範圍中的 IP 位址的那些用戶端才可以存取資料庫。</span><span class="sxs-lookup"><span data-stu-id="3ee51-124">If you specify an IP address range in the database-level firewall rule that is outside the range specified in the server-level firewall rule, only those clients that have IP addresses in the database-level range can access the database.</span></span> <span data-ttu-id="3ee51-125">對於資料庫，您最多可以有 128 個資料庫層級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="3ee51-125">You can have a maximum of 128 database-level firewall rules for a database.</span></span> <span data-ttu-id="3ee51-126">主要與使用者資料庫的資料庫層級防火牆規則，僅可透過 Transact-SQL 來建立和管理。</span><span class="sxs-lookup"><span data-stu-id="3ee51-126">Database-level firewall rules for master and user databases can only be created and managed through Transact-SQL.</span></span> <span data-ttu-id="3ee51-127">如需設定資料庫層級防火牆規則的詳細資訊，請參閱稍後述於 [sp_set_database_firewall_rule (Azure SQL Databases)](https://msdn.microsoft.com/library/dn270010.aspx) 的範例。</span><span class="sxs-lookup"><span data-stu-id="3ee51-127">For more information on configuring database-level firewall rules, see the example later in this article and see [sp_set_database_firewall_rule (Azure SQL Databases)](https://msdn.microsoft.com/library/dn270010.aspx).</span></span>

<span data-ttu-id="3ee51-128">**建議：**Microsoft 建議在可行時使用資料庫層級防火牆規則來增強安全性，並且讓您的資料庫更具有可攜性。</span><span class="sxs-lookup"><span data-stu-id="3ee51-128">**Recommendation:** Microsoft recommends using database-level firewall rules whenever possible to enhance security and to make your database more portable.</span></span> <span data-ttu-id="3ee51-129">當您有多個資料庫具有相同存取需求，且不想花時間個別設定每個資料庫時，請對系統管理員使用伺服器層級的防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="3ee51-129">Use server-level firewall rules for administrators and when you have many databases that have the same access requirements and you don't want to spend time configuring each database individually.</span></span>

> [!Note]
> <span data-ttu-id="3ee51-130">如需可讓業務持續運作的可攜式資料庫資訊，請參閱[災害復原的驗證需求](sql-database-geo-replication-security-config.md)。</span><span class="sxs-lookup"><span data-stu-id="3ee51-130">For information about portable databases in the context of business continuity, see [Authentication requirements for disaster recovery](sql-database-geo-replication-security-config.md).</span></span>
>

### <a name="connecting-from-the-internet"></a><span data-ttu-id="3ee51-131">從網際網路連線</span><span class="sxs-lookup"><span data-stu-id="3ee51-131">Connecting from the Internet</span></span>

<span data-ttu-id="3ee51-132">當電腦嘗試從網際網路連線到資料庫伺服器時，防火牆會先根據資料庫層級的防火牆規則，檢查連線所要求之資料庫的來源 IP 位址︰</span><span class="sxs-lookup"><span data-stu-id="3ee51-132">When a computer attempts to connect to your database server from the Internet, the firewall first checks the originating IP address of the request against the database-level firewall rules, for the database that the connection is requesting:</span></span>

* <span data-ttu-id="3ee51-133">如果要求的 IP 位址在資料庫層級防火牆規則中指定的其中一個範圍內，就會允許連線至包含規則的 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="3ee51-133">If the IP address of the request is within one of the ranges specified in the database-level firewall rules, the connection is granted to the SQL Database that contains the rule.</span></span>
* <span data-ttu-id="3ee51-134">如果要求的 IP 位址不在資料庫層級防火牆規則中指定的其中一個範圍內，則會檢查伺服器層級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="3ee51-134">If the IP address of the request is not within one of the ranges specified in the database-level firewall rule, the server-level firewall rules are checked.</span></span> <span data-ttu-id="3ee51-135">如果要求的 IP 位址在伺服器層級防火牆規則中指定的其中一個範圍內，就會允許連線。</span><span class="sxs-lookup"><span data-stu-id="3ee51-135">If the IP address of the request is within one of the ranges specified in the server-level firewall rules, the connection is granted.</span></span> <span data-ttu-id="3ee51-136">伺服器層級防火牆規則適用於 Azure SQL Server 上的所有 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="3ee51-136">Server-level firewall rules apply to all SQL databases on the Azure SQL server.</span></span>  
* <span data-ttu-id="3ee51-137">如果要求的 IP 位址不在任何資料庫層級或伺服器層級防火牆規則中指定的範圍內，連線要求會失敗。</span><span class="sxs-lookup"><span data-stu-id="3ee51-137">If the IP address of the request is not within the ranges specified in any of the database-level or server-level firewall rules, the connection request fails.</span></span>

> [!NOTE]
> <span data-ttu-id="3ee51-138">若要從您的本機電腦存取 Azure SQL Database，請確定您的網路和本機電腦上的防火牆允許 TCP 連接埠 1433 上的傳出通訊。</span><span class="sxs-lookup"><span data-stu-id="3ee51-138">To access Azure SQL Database from your local computer, ensure the firewall on your network and local computer allows outgoing communication on TCP port 1433.</span></span>
> 

### <a name="connecting-from-azure"></a><span data-ttu-id="3ee51-139">從 Azure 連線</span><span class="sxs-lookup"><span data-stu-id="3ee51-139">Connecting from Azure</span></span>
<span data-ttu-id="3ee51-140">若要允許應用程式從 Azure 連接到您的 Azure SQL Server，必須啟用 Azure 連接。</span><span class="sxs-lookup"><span data-stu-id="3ee51-140">To allow applications from Azure to connect to your Azure SQL server, Azure connections must be enabled.</span></span> <span data-ttu-id="3ee51-141">當 Azure 的應用程式嘗試連線到您的資料庫伺服器時，防火牆會確認是否允許 Azure 連線。</span><span class="sxs-lookup"><span data-stu-id="3ee51-141">When an application from Azure attempts to connect to your database server, the firewall verifies that Azure connections are allowed.</span></span> <span data-ttu-id="3ee51-142">開始和結束位址等於 0.0.0.0 的防火牆設定表示允許這些連線。</span><span class="sxs-lookup"><span data-stu-id="3ee51-142">A firewall setting with starting and ending address equal to 0.0.0.0 indicates these connections are allowed.</span></span> <span data-ttu-id="3ee51-143">如果不允許連線嘗試，要求就不會到達 Azure SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="3ee51-143">If the connection attempt is not allowed, the request does not reach the Azure SQL Database server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3ee51-144">這個選項會設定防火牆，以允許所有來自 Azure 的連線，包括來自其他客戶訂用帳戶的連線。</span><span class="sxs-lookup"><span data-stu-id="3ee51-144">This option configures the firewall to allow all connections from Azure including connections from the subscriptions of other customers.</span></span> <span data-ttu-id="3ee51-145">選取這個選項時，請確定您的登入和使用者權限會限制為只有授權的使用者才能存取。</span><span class="sxs-lookup"><span data-stu-id="3ee51-145">When selecting this option, make sure your login and user permissions limit access to only authorized users.</span></span>
> 

## <a name="creating-and-managing-firewall-rules"></a><span data-ttu-id="3ee51-146">建立和管理防火牆規則</span><span class="sxs-lookup"><span data-stu-id="3ee51-146">Creating and managing firewall rules</span></span>
<span data-ttu-id="3ee51-147">您可使用 [Azure 入口網站](https://portal.azure.com/)，或是以程式設計方式使用 [Azure PowerShell](https://msdn.microsoft.com/library/azure/dn546724.aspx)、[Azure CLI](/cli/azure/sql/server/firewall-rule#create) 或 [REST API](https://msdn.microsoft.com/library/azure/dn505712.aspx)，建立第一個伺服器層級防火牆設定。</span><span class="sxs-lookup"><span data-stu-id="3ee51-147">The first server-level firewall setting can be created using the [Azure portal](https://portal.azure.com/) or programmatically using [Azure PowerShell](https://msdn.microsoft.com/library/azure/dn546724.aspx), [Azure CLI](/cli/azure/sql/server/firewall-rule#create), or the [REST API](https://msdn.microsoft.com/library/azure/dn505712.aspx).</span></span> <span data-ttu-id="3ee51-148">後續的伺服器層級防火牆規則可以使用這些方法，以及透過 Transact-SQL 來建立和管理。</span><span class="sxs-lookup"><span data-stu-id="3ee51-148">Subsequent server-level firewall rules can be created and managed using these methods, and through Transact-SQL.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="3ee51-149">資料庫層級防火牆規則只能使用 Transact-SQL 來建立和管理。</span><span class="sxs-lookup"><span data-stu-id="3ee51-149">Database-level firewall rules can only be created and managed using Transact-SQL.</span></span> 
>

<span data-ttu-id="3ee51-150">為了改進效能，系統會暫時在資料庫層級快取伺服器層級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="3ee51-150">To improve performance, server-level firewall rules are temporarily cached at the database level.</span></span> <span data-ttu-id="3ee51-151">若應重新整理快取，請參閱 [DBCC FLUSHAUTHCACHE](https://msdn.microsoft.com/library/mt627793.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3ee51-151">To refresh the cache, see [DBCC FLUSHAUTHCACHE](https://msdn.microsoft.com/library/mt627793.aspx).</span></span> 

> [!TIP]
> <span data-ttu-id="3ee51-152">您可以使用 [SQL Database 稽核](sql-database-auditing.md)來稽核伺服器等級和資料庫等級防火牆的變更。</span><span class="sxs-lookup"><span data-stu-id="3ee51-152">You can use [SQL Database Auditing](sql-database-auditing.md) to audit server-level and database-level firewall changes.</span></span>
>

### <a name="azure-portal"></a><span data-ttu-id="3ee51-153">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="3ee51-153">Azure portal</span></span>

<span data-ttu-id="3ee51-154">若要在 Azure 入口網站中設定伺服器層級防火牆規則，您可前往 Azure SQL Database 的 [概觀] 頁面，或是 Azure Database 邏輯伺服器的 [概觀] 頁面。</span><span class="sxs-lookup"><span data-stu-id="3ee51-154">To set a server-level firewall rule in the Azure portal, you can either go to the Overview page for your Azure SQL database or the Overview page for your Azure Database logical server.</span></span>

> [!TIP]
> <span data-ttu-id="3ee51-155">如需教學課程，請參閱[使用 Azure 入口網站建立 DB](sql-database-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="3ee51-155">For a tutorial, see [Create a DB using the Azure portal](sql-database-get-started-portal.md).</span></span>
>

<span data-ttu-id="3ee51-156">**從資料庫概觀頁面**</span><span class="sxs-lookup"><span data-stu-id="3ee51-156">**From database overview page**</span></span>

1. <span data-ttu-id="3ee51-157">若要從資料庫概觀頁面設定伺服器層級防火牆規則，請依下圖所示按一下工作列上的 [設定伺服器防火牆]：此時會開啟 [防火牆設定] 頁面。</span><span class="sxs-lookup"><span data-stu-id="3ee51-157">To set a server-level firewall rule from the database overview page, click **Set server firewall** on the toolbar as shown in the following image: The **Firewall settings** page for the SQL Database server opens.</span></span>

      ![伺服器防火牆規則](./media/sql-database-get-started-portal/server-firewall-rule.png) 

2. <span data-ttu-id="3ee51-159">按一下工具列上的 [新增用戶端 IP]，以新增您目前所用電腦的 IP 位址，然後再按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="3ee51-159">Click **Add client IP** on the toolbar to add the IP address of the computer you are currently using and then click **Save**.</span></span> <span data-ttu-id="3ee51-160">系統便會為目前的 IP 位址建立伺服器層級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="3ee51-160">A server-level firewall rule is created for your current IP address.</span></span>

      ![設定伺服器防火牆規則](./media/sql-database-get-started-portal/server-firewall-rule-set.png) 

<span data-ttu-id="3ee51-162">**從伺服器概觀頁面**</span><span class="sxs-lookup"><span data-stu-id="3ee51-162">**From server overview page**</span></span>

<span data-ttu-id="3ee51-163">伺服器的概觀頁面隨即開啟，其中會顯示完整伺服器名稱 (例如 **mynewserver20170403.database.windows.net**)，並提供進一步的組態選項。</span><span class="sxs-lookup"><span data-stu-id="3ee51-163">The overview page for your server opens, showing you the fully qualified server name (such as **mynewserver20170403.database.windows.net**) and provides options for further configuration.</span></span>

1. <span data-ttu-id="3ee51-164">若要從伺服器概觀頁面設定伺服器層級規則，請按一下左側功能表中 [設定] 下方的 [防火牆]，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="3ee51-164">To set a server-level rule from server overview page, click **Firewall** in the left-hand menu under Settings as showed in the following image:</span></span> 

     ![邏輯伺服器概觀](./media/sql-database-migrate-your-sql-server-database/logical-server-overview.png)

2. <span data-ttu-id="3ee51-166">按一下工具列上的 [新增用戶端 IP]，以新增您目前所用電腦的 IP 位址，然後再按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="3ee51-166">Click **Add client IP** on the toolbar to add the IP address of the computer you are currently using and then click **Save**.</span></span> <span data-ttu-id="3ee51-167">系統便會為目前的 IP 位址建立伺服器層級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="3ee51-167">A server-level firewall rule is created for your current IP address.</span></span>

     ![設定伺服器防火牆規則](./media/sql-database-migrate-your-sql-server-database/server-firewall-rule-set.png)

### <a name="transact-sql"></a><span data-ttu-id="3ee51-169">Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="3ee51-169">Transact-SQL</span></span>
| <span data-ttu-id="3ee51-170">目錄檢視或預存程序</span><span class="sxs-lookup"><span data-stu-id="3ee51-170">Catalog View or Stored Procedure</span></span> | <span data-ttu-id="3ee51-171">等級</span><span class="sxs-lookup"><span data-stu-id="3ee51-171">Level</span></span> | <span data-ttu-id="3ee51-172">說明</span><span class="sxs-lookup"><span data-stu-id="3ee51-172">Description</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="3ee51-173">sys.firewall_rules</span><span class="sxs-lookup"><span data-stu-id="3ee51-173">sys.firewall_rules</span></span>](https://msdn.microsoft.com/library/dn269980.aspx) |<span data-ttu-id="3ee51-174">伺服器</span><span class="sxs-lookup"><span data-stu-id="3ee51-174">Server</span></span> |<span data-ttu-id="3ee51-175">顯示目前的伺服器層級防火牆規則</span><span class="sxs-lookup"><span data-stu-id="3ee51-175">Displays the current server-level firewall rules</span></span> |
| [<span data-ttu-id="3ee51-176">sp_set_firewall_rule</span><span class="sxs-lookup"><span data-stu-id="3ee51-176">sp_set_firewall_rule</span></span>](https://msdn.microsoft.com/library/dn270017.aspx) |<span data-ttu-id="3ee51-177">伺服器</span><span class="sxs-lookup"><span data-stu-id="3ee51-177">Server</span></span> |<span data-ttu-id="3ee51-178">建立或更新伺服器層級防火牆規則</span><span class="sxs-lookup"><span data-stu-id="3ee51-178">Creates or updates server-level firewall rules</span></span> |
| [<span data-ttu-id="3ee51-179">sp_delete_firewall_rule</span><span class="sxs-lookup"><span data-stu-id="3ee51-179">sp_delete_firewall_rule</span></span>](https://msdn.microsoft.com/library/dn270024.aspx) |<span data-ttu-id="3ee51-180">伺服器</span><span class="sxs-lookup"><span data-stu-id="3ee51-180">Server</span></span> |<span data-ttu-id="3ee51-181">移除伺服器層級防火牆規則</span><span class="sxs-lookup"><span data-stu-id="3ee51-181">Removes server-level firewall rules</span></span> |
| [<span data-ttu-id="3ee51-182">sys.database_firewall_rules</span><span class="sxs-lookup"><span data-stu-id="3ee51-182">sys.database_firewall_rules</span></span>](https://msdn.microsoft.com/library/dn269982.aspx) |<span data-ttu-id="3ee51-183">資料庫</span><span class="sxs-lookup"><span data-stu-id="3ee51-183">Database</span></span> |<span data-ttu-id="3ee51-184">顯示目前的伺服器層級防火牆規則</span><span class="sxs-lookup"><span data-stu-id="3ee51-184">Displays the current database-level firewall rules</span></span> |
| [<span data-ttu-id="3ee51-185">sp_set_database_firewall_rule</span><span class="sxs-lookup"><span data-stu-id="3ee51-185">sp_set_database_firewall_rule</span></span>](https://msdn.microsoft.com/library/dn270010.aspx) |<span data-ttu-id="3ee51-186">資料庫</span><span class="sxs-lookup"><span data-stu-id="3ee51-186">Database</span></span> |<span data-ttu-id="3ee51-187">建立或更新伺服器層級防火牆規則</span><span class="sxs-lookup"><span data-stu-id="3ee51-187">Creates or updates the database-level firewall rules</span></span> |
| [<span data-ttu-id="3ee51-188">sp_delete_database_firewall_rule</span><span class="sxs-lookup"><span data-stu-id="3ee51-188">sp_delete_database_firewall_rule</span></span>](https://msdn.microsoft.com/library/dn270030.aspx) |<span data-ttu-id="3ee51-189">資料庫</span><span class="sxs-lookup"><span data-stu-id="3ee51-189">Databases</span></span> |<span data-ttu-id="3ee51-190">移除資料庫層級防火牆規則</span><span class="sxs-lookup"><span data-stu-id="3ee51-190">Removes database-level firewall rules</span></span> |


<span data-ttu-id="3ee51-191">下列範例會檢閱現有的規則、在 Contoso 伺服器上啟用 IP 位址範圍，以及刪除防火牆規則：</span><span class="sxs-lookup"><span data-stu-id="3ee51-191">The following examples review the existing rules, enable a range of IP addresses on the server Contoso, and deletes a firewall rule:</span></span>
   
```sql
SELECT * FROM sys.firewall_rules ORDER BY name;
```
  
<span data-ttu-id="3ee51-192">接著，加入防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="3ee51-192">Next, add a firewall rule.</span></span>
   
```sql
EXECUTE sp_set_firewall_rule @name = N'ContosoFirewallRule',
   @start_ip_address = '192.168.1.1', @end_ip_address = '192.168.1.10'
```

<span data-ttu-id="3ee51-193">若要刪除伺服器層級防火牆規則，請執行 sp_delete_firewall_rule 預存程序。</span><span class="sxs-lookup"><span data-stu-id="3ee51-193">To delete a server-level firewall rule, execute the sp_delete_firewall_rule stored procedure.</span></span> <span data-ttu-id="3ee51-194">下列範例會刪除名為 ContosoFirewallRule 的規則：</span><span class="sxs-lookup"><span data-stu-id="3ee51-194">The following example deletes the rule named ContosoFirewallRule:</span></span>
   
```sql
EXECUTE sp_delete_firewall_rule @name = N'ContosoFirewallRule'
```   

### <a name="azure-powershell"></a><span data-ttu-id="3ee51-195">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ee51-195">Azure PowerShell</span></span>
| <span data-ttu-id="3ee51-196">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="3ee51-196">Cmdlet</span></span> | <span data-ttu-id="3ee51-197">等級</span><span class="sxs-lookup"><span data-stu-id="3ee51-197">Level</span></span> | <span data-ttu-id="3ee51-198">說明</span><span class="sxs-lookup"><span data-stu-id="3ee51-198">Description</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="3ee51-199">Get-AzureSqlDatabaseServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="3ee51-199">Get-AzureSqlDatabaseServerFirewallRule</span></span>](https://msdn.microsoft.com/library/azure/dn546731.aspx) |<span data-ttu-id="3ee51-200">伺服器</span><span class="sxs-lookup"><span data-stu-id="3ee51-200">Server</span></span> |<span data-ttu-id="3ee51-201">返回目前的伺服器層級防火牆規則</span><span class="sxs-lookup"><span data-stu-id="3ee51-201">Returns the current server-level firewall rules</span></span> |
| [<span data-ttu-id="3ee51-202">New-AzureSqlDatabaseServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="3ee51-202">New-AzureSqlDatabaseServerFirewallRule</span></span>](https://msdn.microsoft.com/library/azure/dn546724.aspx) |<span data-ttu-id="3ee51-203">伺服器</span><span class="sxs-lookup"><span data-stu-id="3ee51-203">Server</span></span> |<span data-ttu-id="3ee51-204">建立新的伺服器層級防火牆規則</span><span class="sxs-lookup"><span data-stu-id="3ee51-204">Creates a new server-level firewall rule</span></span> |
| [<span data-ttu-id="3ee51-205">Set-AzureSqlDatabaseServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="3ee51-205">Set-AzureSqlDatabaseServerFirewallRule</span></span>](https://msdn.microsoft.com/library/azure/dn546739.aspx) |<span data-ttu-id="3ee51-206">伺服器</span><span class="sxs-lookup"><span data-stu-id="3ee51-206">Server</span></span> |<span data-ttu-id="3ee51-207">更新現有伺服器層級防火牆規則的屬性</span><span class="sxs-lookup"><span data-stu-id="3ee51-207">Updates the properties of an existing server-level firewall rule</span></span> |
| [<span data-ttu-id="3ee51-208">Remove-AzureSqlDatabaseServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="3ee51-208">Remove-AzureSqlDatabaseServerFirewallRule</span></span>](https://msdn.microsoft.com/library/azure/dn546727.aspx) |<span data-ttu-id="3ee51-209">伺服器</span><span class="sxs-lookup"><span data-stu-id="3ee51-209">Server</span></span> |<span data-ttu-id="3ee51-210">移除伺服器層級防火牆規則</span><span class="sxs-lookup"><span data-stu-id="3ee51-210">Removes server-level firewall rules</span></span> |


<span data-ttu-id="3ee51-211">下列範例會使用 PowerShell 設定伺服器層級防火牆規則：</span><span class="sxs-lookup"><span data-stu-id="3ee51-211">The following example sets a server-level firewall rule using PowerShell:</span></span>

```powershell
New-AzureRmSqlServerFirewallRule -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -FirewallRuleName "AllowSome" -StartIpAddress "0.0.0.0" -EndIpAddress "0.0.0.0"
```

> [!TIP]
> <span data-ttu-id="3ee51-212">如需快速入門內容中的 PowerShell 範例資訊，請參閱[建立 DB - PowerShell](sql-database-get-started-powershell.md)以及[使用 PowerShell 建立單一資料庫和設定防火牆規則](scripts/sql-database-create-and-configure-database-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="3ee51-212">For PowerShell examples in the context of a quick start, see [Create DB - PowerShell](sql-database-get-started-powershell.md) and [Create a single database and configure a firewall rule using PowerShell](scripts/sql-database-create-and-configure-database-powershell.md)</span></span>
>

### <a name="azure-cli"></a><span data-ttu-id="3ee51-213">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3ee51-213">Azure CLI</span></span>
| <span data-ttu-id="3ee51-214">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="3ee51-214">Cmdlet</span></span> | <span data-ttu-id="3ee51-215">等級</span><span class="sxs-lookup"><span data-stu-id="3ee51-215">Level</span></span> | <span data-ttu-id="3ee51-216">說明</span><span class="sxs-lookup"><span data-stu-id="3ee51-216">Description</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="3ee51-217">az sql server firewall create</span><span class="sxs-lookup"><span data-stu-id="3ee51-217">az sql server firewall create</span></span>](/cli/azure/sql/server/firewall-rule#create) | <span data-ttu-id="3ee51-218">建立防火牆規則以允許從輸入的 IP 位址範圍存取伺服器上的所有 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="3ee51-218">Creates a firewall rule to allow access to all SQL Databases on the server from the entered IP address range.</span></span>|
| [<span data-ttu-id="3ee51-219">az sql server firewall delete</span><span class="sxs-lookup"><span data-stu-id="3ee51-219">az sql server firewall delete</span></span>](/cli/azure/sql/server/firewall-rule#delete)| <span data-ttu-id="3ee51-220">刪除防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="3ee51-220">Deletes a firewall rule.</span></span>|
| [<span data-ttu-id="3ee51-221">az sql server firewall list</span><span class="sxs-lookup"><span data-stu-id="3ee51-221">az sql server firewall list</span></span>](/cli/azure/sql/server/firewall-rule#list)| <span data-ttu-id="3ee51-222">列出防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="3ee51-222">Lists the firewall rules.</span></span>|
| [<span data-ttu-id="3ee51-223">az sql server firewall rule show</span><span class="sxs-lookup"><span data-stu-id="3ee51-223">az sql server firewall rule show</span></span>](/cli/azure/sql/server/firewall-rule#show)| <span data-ttu-id="3ee51-224">顯示防火牆規則的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3ee51-224">Shows the details of a firewall rule.</span></span>|
| [<span data-ttu-id="3ee51-225">ax sql server firewall rule update</span><span class="sxs-lookup"><span data-stu-id="3ee51-225">ax sql server firewall rule update</span></span>](/cli/azure/sql/server/firewall-rule#update)| <span data-ttu-id="3ee51-226">更新防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="3ee51-226">Updates a firewall rule.</span></span>

<span data-ttu-id="3ee51-227">下列範例會使用 Azure CLI 設定伺服器層級防火牆規則：</span><span class="sxs-lookup"><span data-stu-id="3ee51-227">The following example sets a server-level firewall rule using the Azure CLI:</span></span> 

```azurecli-interactive
az sql server firewall-rule create --resource-group myResourceGroup --server $servername \
    -n AllowYourIp --start-ip-address 0.0.0.0 --end-ip-address 0.0.0.0
```

> [!TIP]
> <span data-ttu-id="3ee51-228">如需快速入門內容中的 Azure CLI 範例資訊，請參閱[建立 DB - Azure CLI](sql-database-get-started-cli.md) 以及[使用 Azure CLI 建立單一資料庫和設定防火牆規則](scripts/sql-database-create-and-configure-database-cli.md)</span><span class="sxs-lookup"><span data-stu-id="3ee51-228">For an Azure CLI example in the context of a quick start, see [Create DDB - Azure CLI](sql-database-get-started-cli.md) and [Create a single database and configure a firewall rule using the Azure CLI](scripts/sql-database-create-and-configure-database-cli.md)</span></span>
>

### <a name="rest-api"></a><span data-ttu-id="3ee51-229">REST API</span><span class="sxs-lookup"><span data-stu-id="3ee51-229">REST API</span></span>
| <span data-ttu-id="3ee51-230">API</span><span class="sxs-lookup"><span data-stu-id="3ee51-230">API</span></span> | <span data-ttu-id="3ee51-231">等級</span><span class="sxs-lookup"><span data-stu-id="3ee51-231">Level</span></span> | <span data-ttu-id="3ee51-232">說明</span><span class="sxs-lookup"><span data-stu-id="3ee51-232">Description</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="3ee51-233">列出防火牆規則</span><span class="sxs-lookup"><span data-stu-id="3ee51-233">List Firewall Rules</span></span>](https://msdn.microsoft.com/library/azure/dn505715.aspx) |<span data-ttu-id="3ee51-234">伺服器</span><span class="sxs-lookup"><span data-stu-id="3ee51-234">Server</span></span> |<span data-ttu-id="3ee51-235">顯示目前的伺服器層級防火牆規則</span><span class="sxs-lookup"><span data-stu-id="3ee51-235">Displays the current server-level firewall rules</span></span> |
| [<span data-ttu-id="3ee51-236">建立防火牆規則</span><span class="sxs-lookup"><span data-stu-id="3ee51-236">Create Firewall Rule</span></span>](https://msdn.microsoft.com/library/azure/dn505712.aspx) |<span data-ttu-id="3ee51-237">伺服器</span><span class="sxs-lookup"><span data-stu-id="3ee51-237">Server</span></span> |<span data-ttu-id="3ee51-238">建立或更新伺服器層級防火牆規則</span><span class="sxs-lookup"><span data-stu-id="3ee51-238">Creates or updates server-level firewall rules</span></span> |
| [<span data-ttu-id="3ee51-239">設定防火牆規則</span><span class="sxs-lookup"><span data-stu-id="3ee51-239">Set Firewall Rule</span></span>](https://msdn.microsoft.com/library/azure/dn505707.aspx) |<span data-ttu-id="3ee51-240">伺服器</span><span class="sxs-lookup"><span data-stu-id="3ee51-240">Server</span></span> |<span data-ttu-id="3ee51-241">更新現有伺服器層級防火牆規則的屬性</span><span class="sxs-lookup"><span data-stu-id="3ee51-241">Updates the properties of an existing server-level firewall rule</span></span> |
| [<span data-ttu-id="3ee51-242">刪除防火牆規則</span><span class="sxs-lookup"><span data-stu-id="3ee51-242">Delete Firewall Rule</span></span>](https://msdn.microsoft.com/library/azure/dn505706.aspx) |<span data-ttu-id="3ee51-243">伺服器</span><span class="sxs-lookup"><span data-stu-id="3ee51-243">Server</span></span> |<span data-ttu-id="3ee51-244">移除伺服器層級防火牆規則</span><span class="sxs-lookup"><span data-stu-id="3ee51-244">Removes server-level firewall rules</span></span> |

## <a name="server-level-firewall-rule-versus-a-database-level-firewall-rule"></a><span data-ttu-id="3ee51-245">伺服器層級防火牆規則與資料庫層級防火牆規則</span><span class="sxs-lookup"><span data-stu-id="3ee51-245">Server-level firewall rule versus a database-level firewall rule</span></span>
<span data-ttu-id="3ee51-246">問：</span><span class="sxs-lookup"><span data-stu-id="3ee51-246">Q.</span></span> <span data-ttu-id="3ee51-247">某個資料庫的使用者是否應該完全與另一個資料庫隔離？</span><span class="sxs-lookup"><span data-stu-id="3ee51-247">Should users of one database be fully isolated from another database?</span></span>   
  <span data-ttu-id="3ee51-248">如果是，請使用資料庫層級防火牆規則授與存取權。</span><span class="sxs-lookup"><span data-stu-id="3ee51-248">If yes, grant access using database-level firewall rules.</span></span> <span data-ttu-id="3ee51-249">這可避免使用伺服器層級防火牆規則，該規則允許透過防火牆存取所有資料庫，這樣會使得您的防禦程度降低。</span><span class="sxs-lookup"><span data-stu-id="3ee51-249">This avoids using server-level firewall rules, which permit access through the firewall to all databases, reducing the depth of your defenses.</span></span>   
 
<span data-ttu-id="3ee51-250">問：</span><span class="sxs-lookup"><span data-stu-id="3ee51-250">Q.</span></span> <span data-ttu-id="3ee51-251">IP 位址的使用者是否需要存取所有資料庫？</span><span class="sxs-lookup"><span data-stu-id="3ee51-251">Do users at the IP address’s need access to all databases?</span></span>   
  <span data-ttu-id="3ee51-252">使用伺服器層級防火牆規則來減少您必須設定防火牆規則的次數。</span><span class="sxs-lookup"><span data-stu-id="3ee51-252">Use server-level firewall rules to reduce the number of times you must configure firewall rules.</span></span>   

<span data-ttu-id="3ee51-253">問：</span><span class="sxs-lookup"><span data-stu-id="3ee51-253">Q.</span></span> <span data-ttu-id="3ee51-254">設定防火牆規則的人員或小組是否只能透過 Azure 入口網站、PowerShell 或 REST API 進行存取？</span><span class="sxs-lookup"><span data-stu-id="3ee51-254">Does the person or team configuring the firewall rules only have access through the Azure portal, PowerShell, or the REST API?</span></span>   
  <span data-ttu-id="3ee51-255">您必須使用伺服器層級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="3ee51-255">You must use server-level firewall rules.</span></span> <span data-ttu-id="3ee51-256">資料庫層級防火牆規則只能使用 Transact-SQL 來設定。</span><span class="sxs-lookup"><span data-stu-id="3ee51-256">Database-level firewall rules can only be configured using Transact-SQL.</span></span>  

<span data-ttu-id="3ee51-257">問：</span><span class="sxs-lookup"><span data-stu-id="3ee51-257">Q.</span></span> <span data-ttu-id="3ee51-258">設定防火牆規則的人員或小組是否不被允許具有資料庫層級的高層級權限？</span><span class="sxs-lookup"><span data-stu-id="3ee51-258">Is the person or team configuring the firewall rules prohibited from having high-level permission at the database level?</span></span>   
  <span data-ttu-id="3ee51-259">使用伺服器層級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="3ee51-259">Use server-level firewall rules.</span></span> <span data-ttu-id="3ee51-260">若要使用 Transact-SQL 設定資料庫層級防火牆規則，至少需要資料庫層級的 `CONTROL DATABASE` 權限。</span><span class="sxs-lookup"><span data-stu-id="3ee51-260">Configuring database-level firewall rules using Transact-SQL, requires at least `CONTROL DATABASE` permission at the database level.</span></span>  

<span data-ttu-id="3ee51-261">問：</span><span class="sxs-lookup"><span data-stu-id="3ee51-261">Q.</span></span> <span data-ttu-id="3ee51-262">設定或稽核防火牆規則的人員或小組，是否正在為許多 (也許數百個) 資料庫集中管理防火牆規則？</span><span class="sxs-lookup"><span data-stu-id="3ee51-262">Is the person or team configuring or auditing the firewall rules, centrally managing firewall rules for many (perhaps 100s) of databases?</span></span>   
  <span data-ttu-id="3ee51-263">此選項取決於您的需求和環境。</span><span class="sxs-lookup"><span data-stu-id="3ee51-263">This selection depends upon your needs and environment.</span></span> <span data-ttu-id="3ee51-264">伺服器層級防火牆規則可能會比較容易設定，但是指令碼可以設定資料庫層級的規則。</span><span class="sxs-lookup"><span data-stu-id="3ee51-264">Server-level firewall rules might be easier to configure, but scripting can configure rules at the database-level.</span></span> <span data-ttu-id="3ee51-265">即使您使用伺服器層級防火牆規則，您可能需要稽核資料庫防火牆規則，以查看具備資料庫 `CONTROL` 權限的使用者是否已建立資料庫層級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="3ee51-265">And even if you use server-level firewall rules, you might need to audit the database-firewall rules, to see if users with `CONTROL` permission on the database have created database-level firewall rules.</span></span>   

<span data-ttu-id="3ee51-266">問：</span><span class="sxs-lookup"><span data-stu-id="3ee51-266">Q.</span></span> <span data-ttu-id="3ee51-267">我是否可以混合使用伺服器層級和資料庫層級防火牆規則？</span><span class="sxs-lookup"><span data-stu-id="3ee51-267">Can I use a mix of both server-level and database-level firewall rules?</span></span>   
  <span data-ttu-id="3ee51-268">是。</span><span class="sxs-lookup"><span data-stu-id="3ee51-268">Yes.</span></span> <span data-ttu-id="3ee51-269">部分使用者 (例如系統管理員) 可能需要伺服器層級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="3ee51-269">Some users, such as administrators might need server-level firewall rules.</span></span> <span data-ttu-id="3ee51-270">其他使用者 (例如資料庫應用程式的使用者) 可能需要資料庫層級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="3ee51-270">Other users, such as users of a database application, might need database-level firewall rules.</span></span>   

## <a name="troubleshooting-the-database-firewall"></a><span data-ttu-id="3ee51-271">針對資料庫防火牆問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="3ee51-271">Troubleshooting the database firewall</span></span>
<span data-ttu-id="3ee51-272">當對於 Microsoft Azure SQL Database 服務的存取未如預期運作時，請考慮下列幾點：</span><span class="sxs-lookup"><span data-stu-id="3ee51-272">Consider the following points when access to the Microsoft Azure SQL Database service does not behave as you expect:</span></span>

* <span data-ttu-id="3ee51-273">**本機防火牆組態：** 在您的電腦可以存取 Azure SQL Database 之前，您可能需要在電腦上為 TCP 連接埠 1433 建立防火牆例外狀況。</span><span class="sxs-lookup"><span data-stu-id="3ee51-273">**Local firewall configuration:** Before your computer can access Azure SQL Database, you may need to create a firewall exception on your computer for TCP port 1433.</span></span> <span data-ttu-id="3ee51-274">如果您是在 Azure 雲端界限內建立連接，您可能必須開啟其他連接埠。</span><span class="sxs-lookup"><span data-stu-id="3ee51-274">If you are making connections inside the Azure cloud boundary, you may have to open additional ports.</span></span> <span data-ttu-id="3ee51-275">如需詳細資訊，請參閱[針對 ADO.NET 4.5 及 SQL Database 的 1433 以外的連接埠](sql-database-develop-direct-route-ports-adonet-v12.md)的〈**SQL Database：外部與內部**〉一節。</span><span class="sxs-lookup"><span data-stu-id="3ee51-275">For more information, see the **SQL Database: Outside vs inside** section of [Ports beyond 1433 for ADO.NET 4.5 and SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>
* <span data-ttu-id="3ee51-276">**網路位址轉譯 (NAT)：** 由於 NAT，您的電腦用來連接到 Azure SQL Database 的 IP 位址，可能會不同於您電腦 IP 組態設定中顯示的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="3ee51-276">**Network address translation (NAT):** Due to NAT, the IP address used by your computer to connect to Azure SQL Database may be different than the IP address shown in your computer IP configuration settings.</span></span> <span data-ttu-id="3ee51-277">若要檢視電腦用來連接到 Azure 的 IP 位址，請登入入口網站，並在裝載您資料庫的伺服器上瀏覽至 [設定] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3ee51-277">To view the IP address your computer is using to connect to Azure, log in to the portal and navigate to the **Configure** tab on the server that hosts your database.</span></span> <span data-ttu-id="3ee51-278">在 [允許的 IP 位址] 區段底下，[目前的用戶端 IP 位址] 隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="3ee51-278">Under the **Allowed IP Addresses** section, the **Current Client IP Address** is displayed.</span></span> <span data-ttu-id="3ee51-279">對 [允許的 IP 位址] 按一下 [新增]，以允許此電腦存取伺服器。</span><span class="sxs-lookup"><span data-stu-id="3ee51-279">Click **Add** to the **Allowed IP Addresses** to allow this computer to access the server.</span></span>
* <span data-ttu-id="3ee51-280">**允許清單的變更尚未生效：** Azure SQL Database 防火牆組態變更可能會延遲最多 5 分鐘才能生效。</span><span class="sxs-lookup"><span data-stu-id="3ee51-280">**Changes to the allow list have not taken effect yet:** There may be as much as a five-minute delay for changes to the Azure SQL Database firewall configuration to take effect.</span></span>
* <span data-ttu-id="3ee51-281">**登入未獲授權或使用不正確的密碼：** 如果 Azure SQL Database 伺服器上的登入沒有權限，或所使用的密碼不正確，與 Azure SQL Database 伺服器的連線就會遭到拒絕。</span><span class="sxs-lookup"><span data-stu-id="3ee51-281">**The login is not authorized or an incorrect password was used:** If a login does not have permissions on the Azure SQL Database server or the password used is incorrect, the connection to the Azure SQL Database server is denied.</span></span> <span data-ttu-id="3ee51-282">建立防火牆設定只會讓用戶端有機會嘗試連線至您的伺服器；每個用戶端必須提供必要的安全性認證。</span><span class="sxs-lookup"><span data-stu-id="3ee51-282">Creating a firewall setting only provides clients with an opportunity to attempt connecting to your server; each client must provide the necessary security credentials.</span></span> <span data-ttu-id="3ee51-283">如需準備登入的詳細資訊，請參閱「管理 Azure SQL Database 中的資料庫、登入和使用者」。</span><span class="sxs-lookup"><span data-stu-id="3ee51-283">For more information about preparing logins, see Managing Databases, Logins, and Users in Azure SQL Database.</span></span>
* <span data-ttu-id="3ee51-284">**動態 IP 位址：** 如果您有使用動態 IP 位址的網際網路連線，並且在通過防火牆時遇到問題，您可以嘗試下列其中一個解決方案：</span><span class="sxs-lookup"><span data-stu-id="3ee51-284">**Dynamic IP address:** If you have an Internet connection with dynamic IP addressing and you are having trouble getting through the firewall, you could try one of the following solutions:</span></span>
  
  * <span data-ttu-id="3ee51-285">要求您的網際網路服務提供者 (ISP) 將可以存取 Azure SQL Database 伺服器的 IP 位址範圍指派給您的用戶端電腦，然後將 IP 位址範圍新增為防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="3ee51-285">Ask your Internet Service Provider (ISP) for the IP address range assigned to your client computers that access the Azure SQL Database server, and then add the IP address range as a firewall rule.</span></span>
  * <span data-ttu-id="3ee51-286">改為針對您的用戶端電腦取得靜態 IP 位址，然後將 IP 位址新增為防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="3ee51-286">Get static IP addressing instead for your client computers, and then add the IP addresses as firewall rules.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ee51-287">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3ee51-287">Next steps</span></span>

- <span data-ttu-id="3ee51-288">如需建立資料庫和伺服器層級防火牆規則的快速入門，請參閱[建立 Azure SQL Database](sql-database-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="3ee51-288">For a quick start on creating a database and a server-level firewall rule, see [Create an Azure SQL database](sql-database-get-started-portal.md).</span></span>
- <span data-ttu-id="3ee51-289">如需從開放原始碼或協力廠商應用程式連接到 Azure SQL Database 的說明，請參閱 [SQL Database 的用戶端快速入門程式碼範例](https://msdn.microsoft.com/library/azure/ee336282.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3ee51-289">For help in connecting to an Azure SQL database from open source or third-party applications, see [Client quick-start code samples to SQL Database](https://msdn.microsoft.com/library/azure/ee336282.aspx).</span></span>
- <span data-ttu-id="3ee51-290">如需詳細資訊，請參閱[針對 ADO.NET 4.5 及 SQL Database 的 1433 以外的連接埠](sql-database-develop-direct-route-ports-adonet-v12.md)的〈**SQL Database：外部與內部**〉一節</span><span class="sxs-lookup"><span data-stu-id="3ee51-290">For information on additional ports that you may need to open, see the **SQL Database: Outside vs inside** section of [Ports beyond 1433 for ADO.NET 4.5 and SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md)</span></span>
- <span data-ttu-id="3ee51-291">如需 Azure SQL Database 安全性的概觀，請參閱[保護您的資料庫](sql-database-security-overview.md)</span><span class="sxs-lookup"><span data-stu-id="3ee51-291">For an overview of Azure SQL Database security, see [Securing your database](sql-database-security-overview.md)</span></span>

<!--Image references-->
[1]: ./media/sql-database-firewall-configure/sqldb-firewall-1.png
