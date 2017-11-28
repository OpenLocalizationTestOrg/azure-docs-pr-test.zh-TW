---
title: "複製 Azure SQL Database | Microsoft Docs"
description: "建立 Azure SQL Database 的複本"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 5aaf6bcd-3839-49b5-8c77-cbdf786e359b
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.date: 06/15/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 8c1e3c80b9f24089dc99463d6ea8ae5d0ea7b19d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="copy-an-azure-sql-database"></a><span data-ttu-id="1f61d-103">複製 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="1f61d-103">Copy an Azure SQL database</span></span>

<span data-ttu-id="1f61d-104">Azure SQL Database 提供數種方式，可讓您在同個伺服器或不同的伺服器上，建立現有 Azure SQL Database 的交易一致性複本。</span><span class="sxs-lookup"><span data-stu-id="1f61d-104">Azure SQL Database provides several methods for creating a transactionally consistent copy of an existing Azure SQL database on either the same server or a different server.</span></span> <span data-ttu-id="1f61d-105">若要複製 SQL Database，您可使用 Azure 入口網站、PowerShell 或 T-SQL。</span><span class="sxs-lookup"><span data-stu-id="1f61d-105">You can copy a SQL database by using the Azure portal, PowerShell, or T-SQL.</span></span> 

## <a name="overview"></a><span data-ttu-id="1f61d-106">概觀</span><span class="sxs-lookup"><span data-stu-id="1f61d-106">Overview</span></span>

<span data-ttu-id="1f61d-107">資料庫複本是發生複製要求時的來源資料庫快照集。</span><span class="sxs-lookup"><span data-stu-id="1f61d-107">A database copy is a snapshot of the source database as of the time of the copy request.</span></span> <span data-ttu-id="1f61d-108">您可選取同個伺服器或不同的伺服器、其服務層級和效能等級，或同個服務層級 (版本) 中的不同效能等級。</span><span class="sxs-lookup"><span data-stu-id="1f61d-108">You can select the same server or a different server, its service tier and performance level, or a different performance level within the same service tier (edition).</span></span> <span data-ttu-id="1f61d-109">複製完成之後，複本會變成功能完整的獨立資料庫。</span><span class="sxs-lookup"><span data-stu-id="1f61d-109">After the copy is complete, it becomes a fully functional, independent database.</span></span> <span data-ttu-id="1f61d-110">此時，您可以將它升級或降級成任何版本。</span><span class="sxs-lookup"><span data-stu-id="1f61d-110">At this point, you can upgrade or downgrade it to any edition.</span></span> <span data-ttu-id="1f61d-111">可以個別管理登入、使用者和權限。</span><span class="sxs-lookup"><span data-stu-id="1f61d-111">The logins, users, and permissions can be managed independently.</span></span>  

## <a name="logins-in-the-database-copy"></a><span data-ttu-id="1f61d-112">資料庫複本中的登入</span><span class="sxs-lookup"><span data-stu-id="1f61d-112">Logins in the database copy</span></span>

<span data-ttu-id="1f61d-113">當您將資料庫複製到相同的邏輯伺服器時，可以在這兩個資料庫上使用相同的登入。</span><span class="sxs-lookup"><span data-stu-id="1f61d-113">When you copy a database to the same logical server, the same logins can be used on both databases.</span></span> <span data-ttu-id="1f61d-114">您用來複製資料庫的安全性主體會變成新資料庫的資料庫擁有者。</span><span class="sxs-lookup"><span data-stu-id="1f61d-114">The security principal you use to copy the database becomes the database owner on the new database.</span></span> <span data-ttu-id="1f61d-115">所有資料庫使用者、其權限及其安全性識別碼 (SID) 都會複製到資料庫副本。</span><span class="sxs-lookup"><span data-stu-id="1f61d-115">All database users, their permissions, and their security identifiers (SIDs) are copied to the database copy.</span></span>  

<span data-ttu-id="1f61d-116">當您將資料庫複製到不同的邏輯伺服器時，新伺服器上的安全性主體就會變成新資料庫上的資料庫擁有者。</span><span class="sxs-lookup"><span data-stu-id="1f61d-116">When you copy a database to a different logical server, the security principal on the new server becomes the database owner on the new database.</span></span> <span data-ttu-id="1f61d-117">如果您使用[自主資料庫使用者](sql-database-manage-logins.md)來進行資料存取，請確保主要和次要資料庫一律具有相同的使用者認證，以便在複製完成時，您可以使用相同的認證立即存取它。</span><span class="sxs-lookup"><span data-stu-id="1f61d-117">If you use [contained database users](sql-database-manage-logins.md) for data access, ensure that both the primary and secondary databases always have the same user credentials, so that after the copy is complete you can immediately access it with the same credentials.</span></span> 

<span data-ttu-id="1f61d-118">如果您使用 [Azure Active Directory](../active-directory/active-directory-whatis.md)，則可以完全不需管理副本中的認證。</span><span class="sxs-lookup"><span data-stu-id="1f61d-118">If you use [Azure Active Directory](../active-directory/active-directory-whatis.md), you can completely eliminate the need for managing credentials in the copy.</span></span> <span data-ttu-id="1f61d-119">不過，當您將資料庫複製到新的伺服器時，以登入為基礎的存取可能無法運作，因為登入不存在於新的伺服器上。</span><span class="sxs-lookup"><span data-stu-id="1f61d-119">However, when you copy the database to a new server, the login-based access might not work, because the logins do not exist on the new server.</span></span> <span data-ttu-id="1f61d-120">若要了解如何在將資料庫複製到不同的邏輯伺服器時管理登入，請參閱[如何管理災害復原後的 Azure SQL Database 安全性](sql-database-geo-replication-security-config.md)。</span><span class="sxs-lookup"><span data-stu-id="1f61d-120">To learn about managing logins when you copy a database to a different logical server, see [How to manage Azure SQL database security after disaster recovery](sql-database-geo-replication-security-config.md).</span></span> 

<span data-ttu-id="1f61d-121">在複製成功之後，重新對應其他使用者之前，只有起始複製的登入 (也就是資料庫擁有者) 可以登入新的資料庫。</span><span class="sxs-lookup"><span data-stu-id="1f61d-121">After the copying succeeds and before other users are remapped, only the login that initiated the copying, the database owner, can log in to the new database.</span></span> <span data-ttu-id="1f61d-122">若要在複製作業完成之後解析登入，請參閱 [解析登入](#resolve-logins)。</span><span class="sxs-lookup"><span data-stu-id="1f61d-122">To resolve logins after the copying operation is complete, see [Resolve logins](#resolve-logins).</span></span>

## <a name="copy-a-database-by-using-the-azure-portal"></a><span data-ttu-id="1f61d-123">使用 Azure 入口網站來複製資料庫</span><span class="sxs-lookup"><span data-stu-id="1f61d-123">Copy a database by using the Azure portal</span></span>

<span data-ttu-id="1f61d-124">若要使用 Azure 入口網站來複製資料庫，請開啟資料庫頁面，然後按一下 [複製]。</span><span class="sxs-lookup"><span data-stu-id="1f61d-124">To copy a database by using the Azure portal, open the page for your database, and then click **Copy**.</span></span> 

   ![資料庫複本](./media/sql-database-copy/database-copy.png)

## <a name="copy-a-database-by-using-powershell"></a><span data-ttu-id="1f61d-126">使用 PowerShell 來複製資料庫</span><span class="sxs-lookup"><span data-stu-id="1f61d-126">Copy a database by using PowerShell</span></span>

<span data-ttu-id="1f61d-127">若要使用 PowerShell 來複製資料庫，請使用 [New-AzureRmSqlDatabaseCopy](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="1f61d-127">To copy a database by using PowerShell, use the [New-AzureRmSqlDatabaseCopy](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) cmdlet.</span></span> 

```PowerShell
New-AzureRmSqlDatabaseCopy -ResourceGroupName "myResourceGroup" `
    -ServerName $sourceserver `
    -DatabaseName "MySampleDatabase" `
    -CopyResourceGroupName "myResourceGroup" `
    -CopyServerName $targetserver `
    -CopyDatabaseName "CopyOfMySampleDatabase"
```

<span data-ttu-id="1f61d-128">如需完整範例指令碼，請參閱[將資料庫複製到新伺服器](scripts/sql-database-copy-database-to-new-server-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="1f61d-128">For a complete sample script, see [Copy a database to a new server](scripts/sql-database-copy-database-to-new-server-powershell.md).</span></span>

## <a name="copy-a-database-by-using-transact-sql"></a><span data-ttu-id="1f61d-129">使用 Transact-SQL 來複製資料庫</span><span class="sxs-lookup"><span data-stu-id="1f61d-129">Copy a database by using Transact-SQL</span></span>

<span data-ttu-id="1f61d-130">使用伺服器層級主體登入或建立您要複製之資料庫的登入來登入 master 資料庫。</span><span class="sxs-lookup"><span data-stu-id="1f61d-130">Log in to the master database with the server-level principal login or the login that created the database you want to copy.</span></span> <span data-ttu-id="1f61d-131">若要成功複製資料庫，不是伺服器層級主體的登入必須是 dbmanager 角色的成員。</span><span class="sxs-lookup"><span data-stu-id="1f61d-131">For database copying to succeed, logins that are not the server-level principal must be members of the dbmanager role.</span></span> <span data-ttu-id="1f61d-132">如需登入與連接到伺服器的詳細資訊，請參閱 [管理登入](sql-database-manage-logins.md)。</span><span class="sxs-lookup"><span data-stu-id="1f61d-132">For more information about logins and connecting to the server, see [Manage logins](sql-database-manage-logins.md).</span></span>

<span data-ttu-id="1f61d-133">使用 [CREATE DATABASE](https://msdn.microsoft.com/library/ms176061.aspx) 陳述式，開始複製來源資料庫。</span><span class="sxs-lookup"><span data-stu-id="1f61d-133">Start copying the source database with the [CREATE DATABASE](https://msdn.microsoft.com/library/ms176061.aspx) statement.</span></span> <span data-ttu-id="1f61d-134">執行此陳述式會起始資料庫複製程序。</span><span class="sxs-lookup"><span data-stu-id="1f61d-134">Executing this statement initiates the database copying process.</span></span> <span data-ttu-id="1f61d-135">因為複製資料庫是非同步程序，所以 CREATE DATABASE 陳述式會在資料庫完成複製之前傳回。</span><span class="sxs-lookup"><span data-stu-id="1f61d-135">Because copying a database is an asynchronous process, the CREATE DATABASE statement returns before the database copying is complete.</span></span>

### <a name="copy-a-sql-database-to-the-same-server"></a><span data-ttu-id="1f61d-136">將 SQL Database 複製到相同伺服器</span><span class="sxs-lookup"><span data-stu-id="1f61d-136">Copy a SQL database to the same server</span></span>
<span data-ttu-id="1f61d-137">使用伺服器層級主體登入或建立您要複製之資料庫的登入來登入 master 資料庫。</span><span class="sxs-lookup"><span data-stu-id="1f61d-137">Log in to the master database with the server-level principal login or the login that created the database you want to copy.</span></span> <span data-ttu-id="1f61d-138">若要成功複製資料庫，不是伺服器層級主體的登入必須是 dbmanager 角色的成員。</span><span class="sxs-lookup"><span data-stu-id="1f61d-138">For database copying to succeed, logins that are not the server-level principal must be members of the dbmanager role.</span></span>

<span data-ttu-id="1f61d-139">此命令會將 Database1 複製到相同伺服器上名為 Database2 的新資料庫。</span><span class="sxs-lookup"><span data-stu-id="1f61d-139">This command copies Database1 to a new database named Database2 on the same server.</span></span> <span data-ttu-id="1f61d-140">視資料庫大小而定，複製作業可能需要一些時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="1f61d-140">Depending on the size of your database, the copying operation might take some time to complete.</span></span>

    -- Execute on the master database.
    -- Start copying.
    CREATE DATABASE Database1_copy AS COPY OF Database1;

### <a name="copy-a-sql-database-to-a-different-server"></a><span data-ttu-id="1f61d-141">將 SQL Database 複製到不同伺服器</span><span class="sxs-lookup"><span data-stu-id="1f61d-141">Copy a SQL database to a different server</span></span>

<span data-ttu-id="1f61d-142">登入目的地伺服器的 master 資料庫，也就是即將建立新資料庫的 SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="1f61d-142">Log in to the master database of the destination server, the SQL database server where the new database is to be created.</span></span> <span data-ttu-id="1f61d-143">使用具有與來源 SQL Database 伺服器上來源資料庫的資料庫擁有者相同之名稱和密碼的登入。</span><span class="sxs-lookup"><span data-stu-id="1f61d-143">Use a login that has the same name and password as the database owner of the source database on the source SQL database server.</span></span> <span data-ttu-id="1f61d-144">目的地伺服器上的登入必須也是 dbmanager 角色的成員或是伺服器層級主體登入。</span><span class="sxs-lookup"><span data-stu-id="1f61d-144">The login on the destination server must also be a member of the dbmanager role or be the server-level principal login.</span></span>

<span data-ttu-id="1f61d-145">此命令會將 server1 上的 Database1 複製到 server2 上名為 Database2 的新資料庫。</span><span class="sxs-lookup"><span data-stu-id="1f61d-145">This command copies Database1 on server1 to a new database named Database2 on server2.</span></span> <span data-ttu-id="1f61d-146">視資料庫大小而定，複製作業可能需要一些時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="1f61d-146">Depending on the size of your database, the copying operation might take some time to complete.</span></span>

    -- Execute on the master database of the target server (server2)
    -- Start copying from Server1 to Server2
    CREATE DATABASE Database1_copy AS COPY OF server1.Database1;


### <a name="monitor-the-progress-of-the-copying-operation"></a><span data-ttu-id="1f61d-147">監視複製作業的進度</span><span class="sxs-lookup"><span data-stu-id="1f61d-147">Monitor the progress of the copying operation</span></span>

<span data-ttu-id="1f61d-148">藉由查詢 sys.databases 和 sys.dm_database_copies 檢視來監視複製程序。</span><span class="sxs-lookup"><span data-stu-id="1f61d-148">Monitor the copying process by querying the sys.databases and sys.dm_database_copies views.</span></span> <span data-ttu-id="1f61d-149">當複製正在進行時，新資料庫的 sys.databases 檢視的 **state_desc** 資料行會設定為 **COPYING**。</span><span class="sxs-lookup"><span data-stu-id="1f61d-149">While the copying is in progress, the **state_desc** column of the sys.databases view for the new database is set to **COPYING**.</span></span>

* <span data-ttu-id="1f61d-150">如果複製失敗，新資料庫的 sys.databases 檢視的 **state_desc** 資料行會設定為 **SUSPECT**。</span><span class="sxs-lookup"><span data-stu-id="1f61d-150">If the copying fails, the **state_desc** column of the sys.databases view for the new database is set to **SUSPECT**.</span></span> <span data-ttu-id="1f61d-151">在新的資料庫上執行 DROP 陳述式，稍後再試一次。</span><span class="sxs-lookup"><span data-stu-id="1f61d-151">Execute the DROP statement on the new database, and try again later.</span></span>
* <span data-ttu-id="1f61d-152">如果複製成功，新資料庫的 sys.databases 檢視的 **state_desc** 資料行會設定為 **ONLINE**。</span><span class="sxs-lookup"><span data-stu-id="1f61d-152">If the copying succeeds, the **state_desc** column of the sys.databases view for the new database is set to **ONLINE**.</span></span> <span data-ttu-id="1f61d-153">複製已完成且新資料庫是一般資料庫，能夠與來源資料庫分開進行變更。</span><span class="sxs-lookup"><span data-stu-id="1f61d-153">The copying is complete, and the new database is a regular database that can be changed independent of the source database.</span></span>

> [!NOTE]
> <span data-ttu-id="1f61d-154">如果您決定在進行複製時予以取消，請在新資料庫上執行 [DROP DATABASE](https://msdn.microsoft.com/library/ms178613.aspx) 陳述式。</span><span class="sxs-lookup"><span data-stu-id="1f61d-154">If you decide to cancel the copying while it is in progress, execute the [DROP DATABASE](https://msdn.microsoft.com/library/ms178613.aspx) statement on the new database.</span></span> <span data-ttu-id="1f61d-155">或者，在來源資料庫上執行 DROP DATABASE 陳述式也會取消複製程序。</span><span class="sxs-lookup"><span data-stu-id="1f61d-155">Alternatively, executing the DROP DATABASE statement on the source database also cancels the copying process.</span></span>
> 

## <a name="resolve-logins"></a><span data-ttu-id="1f61d-156">解析登入</span><span class="sxs-lookup"><span data-stu-id="1f61d-156">Resolve logins</span></span>

<span data-ttu-id="1f61d-157">在新資料庫於目的地伺服器上線之後，使用 [ALTER USER](https://msdn.microsoft.com/library/ms176060.aspx) 陳述式將使用者從新的資料庫重新對應至目的地伺服器上的登入。</span><span class="sxs-lookup"><span data-stu-id="1f61d-157">After the new database is online on the destination server, use the [ALTER USER](https://msdn.microsoft.com/library/ms176060.aspx) statement to remap the users from the new database to logins on the destination server.</span></span> <span data-ttu-id="1f61d-158">若要解析被遺棄的使用者，請參閱 [被遺棄使用者疑難排解](https://msdn.microsoft.com/library/ms175475.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1f61d-158">To resolve orphaned users, see [Troubleshoot Orphaned Users](https://msdn.microsoft.com/library/ms175475.aspx).</span></span> <span data-ttu-id="1f61d-159">另請參閱 [如何管理災害復原後的 Azure SQL Database 安全性](sql-database-geo-replication-security-config.md)。</span><span class="sxs-lookup"><span data-stu-id="1f61d-159">See also [How to manage Azure SQL database security after disaster recovery](sql-database-geo-replication-security-config.md).</span></span>

<span data-ttu-id="1f61d-160">新資料庫中的所有使用者都保有其在來源資料庫中原有的權限。</span><span class="sxs-lookup"><span data-stu-id="1f61d-160">All users in the new database retain the permissions that they had in the source database.</span></span> <span data-ttu-id="1f61d-161">起始資料庫複製的使用者會變成新資料庫的資料庫擁有者，並且被指派新的安全性識別碼 (SID)。</span><span class="sxs-lookup"><span data-stu-id="1f61d-161">The user who initiated the database copy becomes the database owner of the new database and is assigned a new security identifier (SID).</span></span> <span data-ttu-id="1f61d-162">在複製成功之後，重新對應其他使用者之前，只有起始複製的登入 (也就是資料庫擁有者) 可以登入新的資料庫。</span><span class="sxs-lookup"><span data-stu-id="1f61d-162">After the copying succeeds and before other users are remapped, only the login that initiated the copying, the database owner, can log in to the new database.</span></span>

<span data-ttu-id="1f61d-163">若要了解將資料庫複製到不同的邏輯伺服器時如何管理使用者與登入，請參閱[如何管理災害復原後的 Azure SQL 資料庫安全性](sql-database-geo-replication-security-config.md)。</span><span class="sxs-lookup"><span data-stu-id="1f61d-163">To learn about managing users and logins when you copy a database to a different logical server, see [How to manage Azure SQL database security after disaster recovery](sql-database-geo-replication-security-config.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f61d-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1f61d-164">Next steps</span></span>

* <span data-ttu-id="1f61d-165">如需登入相關資訊，請參閱[管理登入](sql-database-manage-logins.md)以及[如何管理災害復原後的 Azure SQL Database 安全性](sql-database-geo-replication-security-config.md)。</span><span class="sxs-lookup"><span data-stu-id="1f61d-165">For information about logins, see [Manage logins](sql-database-manage-logins.md) and [How to manage Azure SQL database security after disaster recovery](sql-database-geo-replication-security-config.md).</span></span>
* <span data-ttu-id="1f61d-166">若要匯出資料庫，請參閱[將資料庫匯出至 BACPAC](sql-database-export.md)。</span><span class="sxs-lookup"><span data-stu-id="1f61d-166">To export a database, see [Export the database to a BACPAC](sql-database-export.md).</span></span>
