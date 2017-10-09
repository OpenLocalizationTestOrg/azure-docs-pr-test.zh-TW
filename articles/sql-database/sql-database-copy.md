---
title: "Azure SQL database aaaCopy |Microsoft 文件"
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
ms.openlocfilehash: 64a297d819d6da89600fda60abe8394ae405abfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="copy-an-azure-sql-database"></a><span data-ttu-id="1896d-103">複製 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="1896d-103">Copy an Azure SQL database</span></span>

<span data-ttu-id="1896d-104">Azure SQL Database 提供數種方法來建立交易一致的複本的現有的 Azure SQL 資料庫上任一 hello 相同伺服器或不同的伺服器。</span><span class="sxs-lookup"><span data-stu-id="1896d-104">Azure SQL Database provides several methods for creating a transactionally consistent copy of an existing Azure SQL database on either hello same server or a different server.</span></span> <span data-ttu-id="1896d-105">您可以使用 hello Azure 入口網站、 PowerShell 或 T-SQL 複製 SQL database。</span><span class="sxs-lookup"><span data-stu-id="1896d-105">You can copy a SQL database by using hello Azure portal, PowerShell, or T-SQL.</span></span> 

## <a name="overview"></a><span data-ttu-id="1896d-106">概觀</span><span class="sxs-lookup"><span data-stu-id="1896d-106">Overview</span></span>

<span data-ttu-id="1896d-107">資料庫複本是 hello hello 的 hello 複製要求的時間為準的來源資料庫的快照集。</span><span class="sxs-lookup"><span data-stu-id="1896d-107">A database copy is a snapshot of hello source database as of hello time of hello copy request.</span></span> <span data-ttu-id="1896d-108">您可以選取相同的伺服器或另一部伺服器、 其服務層和效能層級或不同的效能層級內 hello hello 相同服務層 （版本）。</span><span class="sxs-lookup"><span data-stu-id="1896d-108">You can select hello same server or a different server, its service tier and performance level, or a different performance level within hello same service tier (edition).</span></span> <span data-ttu-id="1896d-109">Hello 複製程序完成之後，它會變成完全正常運作且獨立的資料庫。</span><span class="sxs-lookup"><span data-stu-id="1896d-109">After hello copy is complete, it becomes a fully functional, independent database.</span></span> <span data-ttu-id="1896d-110">此時，您可以升級或降級 tooany 版本。</span><span class="sxs-lookup"><span data-stu-id="1896d-110">At this point, you can upgrade or downgrade it tooany edition.</span></span> <span data-ttu-id="1896d-111">hello 登入、 使用者和權限可以分開管理。</span><span class="sxs-lookup"><span data-stu-id="1896d-111">hello logins, users, and permissions can be managed independently.</span></span>  

## <a name="logins-in-hello-database-copy"></a><span data-ttu-id="1896d-112">Hello 資料庫副本中的登入</span><span class="sxs-lookup"><span data-stu-id="1896d-112">Logins in hello database copy</span></span>

<span data-ttu-id="1896d-113">當您複製資料庫 toohello 相同邏輯伺服器，可以使用相同的登入，這兩個資料庫的 hello。</span><span class="sxs-lookup"><span data-stu-id="1896d-113">When you copy a database toohello same logical server, hello same logins can be used on both databases.</span></span> <span data-ttu-id="1896d-114">hello 安全性主體使用 toocopy hello 資料庫變成 hello hello 新資料庫上的資料庫擁有者。</span><span class="sxs-lookup"><span data-stu-id="1896d-114">hello security principal you use toocopy hello database becomes hello database owner on hello new database.</span></span> <span data-ttu-id="1896d-115">所有資料庫使用者、 其權限，以及它們的安全性識別碼 (Sid) 被複製 toohello 資料庫副本。</span><span class="sxs-lookup"><span data-stu-id="1896d-115">All database users, their permissions, and their security identifiers (SIDs) are copied toohello database copy.</span></span>  

<span data-ttu-id="1896d-116">當您複製資料庫 tooa 不同的邏輯伺服器時，hello 安全性主體 hello 新的伺服器上會變成 hello hello 新資料庫上的資料庫擁有者。</span><span class="sxs-lookup"><span data-stu-id="1896d-116">When you copy a database tooa different logical server, hello security principal on hello new server becomes hello database owner on hello new database.</span></span> <span data-ttu-id="1896d-117">如果您使用[自主資料庫使用者](sql-database-manage-logins.md)資料存取，請確定兩者 hello 主要，以及次要資料庫一律會有相同的使用者認證，因此，hello 複製完成後您可以立即存取的 hello 與 hello 相同認證。</span><span class="sxs-lookup"><span data-stu-id="1896d-117">If you use [contained database users](sql-database-manage-logins.md) for data access, ensure that both hello primary and secondary databases always have hello same user credentials, so that after hello copy is complete you can immediately access it with hello same credentials.</span></span> 

<span data-ttu-id="1896d-118">如果您使用[Azure Active Directory](../active-directory/active-directory-whatis.md)，您可以完全排除 hello 需要管理 hello 複本中的認證。</span><span class="sxs-lookup"><span data-stu-id="1896d-118">If you use [Azure Active Directory](../active-directory/active-directory-whatis.md), you can completely eliminate hello need for managing credentials in hello copy.</span></span> <span data-ttu-id="1896d-119">不過，當您複製 hello 資料庫 tooa 新伺服器，hello 登入為基礎的存取可能無法運作，因為 hello 登入不存在 hello 新的伺服器上。</span><span class="sxs-lookup"><span data-stu-id="1896d-119">However, when you copy hello database tooa new server, hello login-based access might not work, because hello logins do not exist on hello new server.</span></span> <span data-ttu-id="1896d-120">toolearn 有關管理登入，當您複製資料庫 tooa 不同的邏輯伺服器，請參閱[toomanage Azure SQL 資料庫安全性之後嚴重損壞修復](sql-database-geo-replication-security-config.md)。</span><span class="sxs-lookup"><span data-stu-id="1896d-120">toolearn about managing logins when you copy a database tooa different logical server, see [How toomanage Azure SQL database security after disaster recovery](sql-database-geo-replication-security-config.md).</span></span> 

<span data-ttu-id="1896d-121">Hello 複製成功之後，會重新對應其他使用者之前，只有 hello 起始登入複製的 hello hello 資料庫擁有者，可以登入 toohello 新資料庫。</span><span class="sxs-lookup"><span data-stu-id="1896d-121">After hello copying succeeds and before other users are remapped, only hello login that initiated hello copying, hello database owner, can log in toohello new database.</span></span> <span data-ttu-id="1896d-122">tooresolve 登入之後 hello 複製作業已完成，請參閱[解決登入](#resolve-logins)。</span><span class="sxs-lookup"><span data-stu-id="1896d-122">tooresolve logins after hello copying operation is complete, see [Resolve logins](#resolve-logins).</span></span>

## <a name="copy-a-database-by-using-hello-azure-portal"></a><span data-ttu-id="1896d-123">使用 hello Azure 入口網站中複製資料庫</span><span class="sxs-lookup"><span data-stu-id="1896d-123">Copy a database by using hello Azure portal</span></span>

<span data-ttu-id="1896d-124">使用資料庫 hello Azure 入口網站，為您的資料庫中，開啟 hello 頁面，然後按一下的 toocopy**複製**。</span><span class="sxs-lookup"><span data-stu-id="1896d-124">toocopy a database by using hello Azure portal, open hello page for your database, and then click **Copy**.</span></span> 

   ![資料庫複本](./media/sql-database-copy/database-copy.png)

## <a name="copy-a-database-by-using-powershell"></a><span data-ttu-id="1896d-126">使用 PowerShell 來複製資料庫</span><span class="sxs-lookup"><span data-stu-id="1896d-126">Copy a database by using PowerShell</span></span>

<span data-ttu-id="1896d-127">使用 PowerShell，使用 hello 資料庫 toocopy[新增 AzureRmSqlDatabaseCopy](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="1896d-127">toocopy a database by using PowerShell, use hello [New-AzureRmSqlDatabaseCopy](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) cmdlet.</span></span> 

```PowerShell
New-AzureRmSqlDatabaseCopy -ResourceGroupName "myResourceGroup" `
    -ServerName $sourceserver `
    -DatabaseName "MySampleDatabase" `
    -CopyResourceGroupName "myResourceGroup" `
    -CopyServerName $targetserver `
    -CopyDatabaseName "CopyOfMySampleDatabase"
```

<span data-ttu-id="1896d-128">如需完整的範例指令碼，請參閱[複製 tooa 新資料庫的伺服器](scripts/sql-database-copy-database-to-new-server-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="1896d-128">For a complete sample script, see [Copy a database tooa new server](scripts/sql-database-copy-database-to-new-server-powershell.md).</span></span>

## <a name="copy-a-database-by-using-transact-sql"></a><span data-ttu-id="1896d-129">使用 Transact-SQL 來複製資料庫</span><span class="sxs-lookup"><span data-stu-id="1896d-129">Copy a database by using Transact-SQL</span></span>

<span data-ttu-id="1896d-130">登入 toohello master 資料庫與 hello 伺服器層級主體登入或建立您想要 toocopy hello 資料庫 hello 登入。</span><span class="sxs-lookup"><span data-stu-id="1896d-130">Log in toohello master database with hello server-level principal login or hello login that created hello database you want toocopy.</span></span> <span data-ttu-id="1896d-131">資料庫複製 toosucceed，不是 hello 伺服器層級主體登入必須 hello dbmanager 角色的成員。</span><span class="sxs-lookup"><span data-stu-id="1896d-131">For database copying toosucceed, logins that are not hello server-level principal must be members of hello dbmanager role.</span></span> <span data-ttu-id="1896d-132">如需登入和連線 toohello 伺服器的詳細資訊，請參閱[管理登入](sql-database-manage-logins.md)。</span><span class="sxs-lookup"><span data-stu-id="1896d-132">For more information about logins and connecting toohello server, see [Manage logins](sql-database-manage-logins.md).</span></span>

<span data-ttu-id="1896d-133">開始複製 hello 來源資料庫與 hello [CREATE DATABASE](https://msdn.microsoft.com/library/ms176061.aspx)陳述式。</span><span class="sxs-lookup"><span data-stu-id="1896d-133">Start copying hello source database with hello [CREATE DATABASE](https://msdn.microsoft.com/library/ms176061.aspx) statement.</span></span> <span data-ttu-id="1896d-134">執行這個陳述式會起始 hello 資料庫複製程序。</span><span class="sxs-lookup"><span data-stu-id="1896d-134">Executing this statement initiates hello database copying process.</span></span> <span data-ttu-id="1896d-135">複製資料庫是非同步程序，因為 hello CREATE DATABASE 陳述式會傳回前 hello 資料庫複製便已完成。</span><span class="sxs-lookup"><span data-stu-id="1896d-135">Because copying a database is an asynchronous process, hello CREATE DATABASE statement returns before hello database copying is complete.</span></span>

### <a name="copy-a-sql-database-toohello-same-server"></a><span data-ttu-id="1896d-136">複製 SQL 資料庫 toohello 相同的伺服器</span><span class="sxs-lookup"><span data-stu-id="1896d-136">Copy a SQL database toohello same server</span></span>
<span data-ttu-id="1896d-137">登入 toohello master 資料庫與 hello 伺服器層級主體登入或建立您想要 toocopy hello 資料庫 hello 登入。</span><span class="sxs-lookup"><span data-stu-id="1896d-137">Log in toohello master database with hello server-level principal login or hello login that created hello database you want toocopy.</span></span> <span data-ttu-id="1896d-138">資料庫複製 toosucceed，不是 hello 伺服器層級主體登入必須 hello dbmanager 角色的成員。</span><span class="sxs-lookup"><span data-stu-id="1896d-138">For database copying toosucceed, logins that are not hello server-level principal must be members of hello dbmanager role.</span></span>

<span data-ttu-id="1896d-139">此命令會將複製 hello 上名為 Database2 Database1 tooa 新資料庫相同的伺服器。</span><span class="sxs-lookup"><span data-stu-id="1896d-139">This command copies Database1 tooa new database named Database2 on hello same server.</span></span> <span data-ttu-id="1896d-140">根據資料庫的 hello 大小，hello 複製作業可能需要一些時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="1896d-140">Depending on hello size of your database, hello copying operation might take some time toocomplete.</span></span>

    -- Execute on hello master database.
    -- Start copying.
    CREATE DATABASE Database1_copy AS COPY OF Database1;

### <a name="copy-a-sql-database-tooa-different-server"></a><span data-ttu-id="1896d-141">複製 SQL database tooa 不同伺服器</span><span class="sxs-lookup"><span data-stu-id="1896d-141">Copy a SQL database tooa different server</span></span>

<span data-ttu-id="1896d-142">登入 toohello master hello 目的地伺服器 hello 新資料庫所在 toobe 建立 hello SQL 資料庫伺服器的資料庫。</span><span class="sxs-lookup"><span data-stu-id="1896d-142">Log in toohello master database of hello destination server, hello SQL database server where hello new database is toobe created.</span></span> <span data-ttu-id="1896d-143">使用具有相同名稱和密碼 hello hello hello hello 來源 SQL 資料庫伺服器上的來源資料庫的資料庫擁有者的登入。</span><span class="sxs-lookup"><span data-stu-id="1896d-143">Use a login that has hello same name and password as hello database owner of hello source database on hello source SQL database server.</span></span> <span data-ttu-id="1896d-144">hello hello 目的地伺服器上的登入也必須是 hello dbmanager 角色的成員，或者是 hello 伺服器層級主體登入。</span><span class="sxs-lookup"><span data-stu-id="1896d-144">hello login on hello destination server must also be a member of hello dbmanager role or be hello server-level principal login.</span></span>

<span data-ttu-id="1896d-145">這個命令會將 Database1 server2 上名為 Database2 server1 tooa 新資料庫上。</span><span class="sxs-lookup"><span data-stu-id="1896d-145">This command copies Database1 on server1 tooa new database named Database2 on server2.</span></span> <span data-ttu-id="1896d-146">根據資料庫的 hello 大小，hello 複製作業可能需要一些時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="1896d-146">Depending on hello size of your database, hello copying operation might take some time toocomplete.</span></span>

    -- Execute on hello master database of hello target server (server2)
    -- Start copying from Server1 tooServer2
    CREATE DATABASE Database1_copy AS COPY OF server1.Database1;


### <a name="monitor-hello-progress-of-hello-copying-operation"></a><span data-ttu-id="1896d-147">監視複製作業的 hello hello 進度</span><span class="sxs-lookup"><span data-stu-id="1896d-147">Monitor hello progress of hello copying operation</span></span>

<span data-ttu-id="1896d-148">監視複製程序 hello hello sys.databases 和 sys.dm_database_copies 檢視進行查詢。</span><span class="sxs-lookup"><span data-stu-id="1896d-148">Monitor hello copying process by querying hello sys.databases and sys.dm_database_copies views.</span></span> <span data-ttu-id="1896d-149">Hello 複製正在進行時，hello **state_desc** hello 新資料庫的 hello sys.databases 檢視資料行設定得**複製**。</span><span class="sxs-lookup"><span data-stu-id="1896d-149">While hello copying is in progress, hello **state_desc** column of hello sys.databases view for hello new database is set too**COPYING**.</span></span>

* <span data-ttu-id="1896d-150">如果 hello 複製失敗，hello **state_desc** hello 新資料庫的 hello sys.databases 檢視資料行設定得**懷疑**。</span><span class="sxs-lookup"><span data-stu-id="1896d-150">If hello copying fails, hello **state_desc** column of hello sys.databases view for hello new database is set too**SUSPECT**.</span></span> <span data-ttu-id="1896d-151">Hello 新的資料庫上執行 hello DROP 陳述式，並再試一次。</span><span class="sxs-lookup"><span data-stu-id="1896d-151">Execute hello DROP statement on hello new database, and try again later.</span></span>
* <span data-ttu-id="1896d-152">如果 hello 複製成功，hello **state_desc** hello 新資料庫的 hello sys.databases 檢視資料行設定得**線上**。</span><span class="sxs-lookup"><span data-stu-id="1896d-152">If hello copying succeeds, hello **state_desc** column of hello sys.databases view for hello new database is set too**ONLINE**.</span></span> <span data-ttu-id="1896d-153">hello 複製已完成，且 hello 新的資料庫是可以變更不會影響 hello 來源資料庫的一般資料庫。</span><span class="sxs-lookup"><span data-stu-id="1896d-153">hello copying is complete, and hello new database is a regular database that can be changed independent of hello source database.</span></span>

> [!NOTE]
> <span data-ttu-id="1896d-154">如果您決定 toocancel hello 複製正在進行時，執行 hello [DROP DATABASE](https://msdn.microsoft.com/library/ms178613.aspx) hello 新資料庫上的陳述式。</span><span class="sxs-lookup"><span data-stu-id="1896d-154">If you decide toocancel hello copying while it is in progress, execute hello [DROP DATABASE](https://msdn.microsoft.com/library/ms178613.aspx) statement on hello new database.</span></span> <span data-ttu-id="1896d-155">或者，在 hello 來源資料庫上執行 hello DROP DATABASE 陳述式也會取消複製程序的 hello。</span><span class="sxs-lookup"><span data-stu-id="1896d-155">Alternatively, executing hello DROP DATABASE statement on hello source database also cancels hello copying process.</span></span>
> 

## <a name="resolve-logins"></a><span data-ttu-id="1896d-156">解析登入</span><span class="sxs-lookup"><span data-stu-id="1896d-156">Resolve logins</span></span>

<span data-ttu-id="1896d-157">Hello 新資料庫在線上 hello 目的地伺服器上之後，請使用 hello [ALTER USER](https://msdn.microsoft.com/library/ms176060.aspx) hello 陳述式 tooremap hello 使用者新資料庫 toologins hello 目的地伺服器上的。</span><span class="sxs-lookup"><span data-stu-id="1896d-157">After hello new database is online on hello destination server, use hello [ALTER USER](https://msdn.microsoft.com/library/ms176060.aspx) statement tooremap hello users from hello new database toologins on hello destination server.</span></span> <span data-ttu-id="1896d-158">tooresolve 被遺棄使用者，請參閱[被遺棄使用者疑難排解](https://msdn.microsoft.com/library/ms175475.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1896d-158">tooresolve orphaned users, see [Troubleshoot Orphaned Users](https://msdn.microsoft.com/library/ms175475.aspx).</span></span> <span data-ttu-id="1896d-159">另請參閱[toomanage Azure SQL 資料庫安全性之後嚴重損壞修復](sql-database-geo-replication-security-config.md)。</span><span class="sxs-lookup"><span data-stu-id="1896d-159">See also [How toomanage Azure SQL database security after disaster recovery](sql-database-geo-replication-security-config.md).</span></span>

<span data-ttu-id="1896d-160">Hello 新資料庫中的所有使用者都保有 hello 來源資料庫中的 hello 權限。</span><span class="sxs-lookup"><span data-stu-id="1896d-160">All users in hello new database retain hello permissions that they had in hello source database.</span></span> <span data-ttu-id="1896d-161">起始 hello 資料庫副本的 hello 使用者成為 hello hello 新資料庫的資料庫擁有者，並指派新的安全性識別碼 (SID)。</span><span class="sxs-lookup"><span data-stu-id="1896d-161">hello user who initiated hello database copy becomes hello database owner of hello new database and is assigned a new security identifier (SID).</span></span> <span data-ttu-id="1896d-162">Hello 複製成功之後，會重新對應其他使用者之前，只有 hello 起始登入複製的 hello hello 資料庫擁有者，可以登入 toohello 新資料庫。</span><span class="sxs-lookup"><span data-stu-id="1896d-162">After hello copying succeeds and before other users are remapped, only hello login that initiated hello copying, hello database owner, can log in toohello new database.</span></span>

<span data-ttu-id="1896d-163">toolearn 有關管理使用者與登入，當您複製資料庫 tooa 不同的邏輯伺服器，請參閱[toomanage Azure SQL 資料庫安全性之後嚴重損壞修復](sql-database-geo-replication-security-config.md)。</span><span class="sxs-lookup"><span data-stu-id="1896d-163">toolearn about managing users and logins when you copy a database tooa different logical server, see [How toomanage Azure SQL database security after disaster recovery](sql-database-geo-replication-security-config.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1896d-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1896d-164">Next steps</span></span>

* <span data-ttu-id="1896d-165">如需登入資訊，請參閱[管理登入](sql-database-manage-logins.md)和[toomanage Azure SQL 資料庫安全性之後嚴重損壞修復](sql-database-geo-replication-security-config.md)。</span><span class="sxs-lookup"><span data-stu-id="1896d-165">For information about logins, see [Manage logins](sql-database-manage-logins.md) and [How toomanage Azure SQL database security after disaster recovery](sql-database-geo-replication-security-config.md).</span></span>
* <span data-ttu-id="1896d-166">tooexport 資料庫，請參閱[匯出 hello 資料庫 tooa BACPAC](sql-database-export.md)。</span><span class="sxs-lookup"><span data-stu-id="1896d-166">tooexport a database, see [Export hello database tooa BACPAC](sql-database-export.md).</span></span>
