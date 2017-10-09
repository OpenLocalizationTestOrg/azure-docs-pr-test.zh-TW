---
title: "aaaConfigure 災害復原的 Azure SQL Database 安全性 |Microsoft 文件"
description: "本主題說明設定和管理安全性資料庫還原或容錯移轉 tooa 中的次要伺服器 hello 事件的資料中心中斷或其他災害後的安全性考量"
services: sql-database
documentationcenter: na
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: c7c898c9-69d4-4e16-8b7e-720bbb3353dd
ms.service: sql-database
ms.custom: business continuity
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 10/13/2016
ms.author: sashan
ms.openlocfilehash: c3172568e1b8ad2a53958200aa6cf19b4a9434ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-manage-azure-sql-database-security-for-geo-restore-or-failover"></a><span data-ttu-id="487dc-103">建立和管理 Azure SQL Database 安全性以供異地還原或容錯移轉使用</span><span class="sxs-lookup"><span data-stu-id="487dc-103">Configure and manage Azure SQL Database security for geo-restore or failover</span></span> 

> [!NOTE]
> <span data-ttu-id="487dc-104">[作用中異地複寫](sql-database-geo-replication-overview.md)現在可供所有服務層中的所有資料庫使用。</span><span class="sxs-lookup"><span data-stu-id="487dc-104">[Active geo-replication](sql-database-geo-replication-overview.md) is now available for all databases in all service tiers.</span></span>
>  

## <a name="overview-of-authentication-requirements-for-disaster-recovery"></a><span data-ttu-id="487dc-105">災害復原的驗證需求概觀</span><span class="sxs-lookup"><span data-stu-id="487dc-105">Overview of authentication requirements for disaster recovery</span></span>
<span data-ttu-id="487dc-106">本主題說明 hello 驗證需求 tooconfigure 和控制[作用中地理複寫](sql-database-geo-replication-overview.md)及 hello 的步驟需要的 tooset 使用者存取 toohello 次要資料庫。</span><span class="sxs-lookup"><span data-stu-id="487dc-106">This topic describes hello authentication requirements tooconfigure and control [active geo-replication](sql-database-geo-replication-overview.md) and hello steps required tooset up user access toohello secondary database.</span></span> <span data-ttu-id="487dc-107">它也會說明如何啟用 access toohello 復原的資料庫之後使用[異地還原](sql-database-recovery-using-backups.md#geo-restore)。</span><span class="sxs-lookup"><span data-stu-id="487dc-107">It also describes how enable access toohello recovered database after using [geo-restore](sql-database-recovery-using-backups.md#geo-restore).</span></span> <span data-ttu-id="487dc-108">如需復原選項的詳細資訊，請參閱 [商務持續性概觀](sql-database-business-continuity.md)。</span><span class="sxs-lookup"><span data-stu-id="487dc-108">For more information on recovery options, see [Business Continuity Overview](sql-database-business-continuity.md).</span></span>

## <a name="disaster-recovery-with-contained-users"></a><span data-ttu-id="487dc-109">災害復原與自主使用者</span><span class="sxs-lookup"><span data-stu-id="487dc-109">Disaster recovery with contained users</span></span>
<span data-ttu-id="487dc-110">不同於傳統的使用者必須是對應 toologins hello master 資料庫中的，包含的使用者完全由 hello 資料庫本身所管理。</span><span class="sxs-lookup"><span data-stu-id="487dc-110">Unlike traditional users, which must be mapped toologins in hello master database, a contained user is managed completely by hello database itself.</span></span> <span data-ttu-id="487dc-111">這樣有兩個優點。</span><span class="sxs-lookup"><span data-stu-id="487dc-111">This has two benefits.</span></span> <span data-ttu-id="487dc-112">在 hello 災害復原案例中，hello 使用者可以繼續 tooconnect toohello 新主要資料庫或 hello 復原的資料庫使用地理還原而不需要任何額外的設定，因為 hello 資料庫管理 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="487dc-112">In hello disaster recovery scenario, hello users can continue tooconnect toohello new primary database or hello database recovered using geo-restore without any additional configuration, because hello database manages hello users.</span></span> <span data-ttu-id="487dc-113">從登入的觀點來看，這個組態也有潛在的延展性和效能優勢。</span><span class="sxs-lookup"><span data-stu-id="487dc-113">There are also potential scalability and performance benefits from this configuration from a login perspective.</span></span> <span data-ttu-id="487dc-114">如需詳細資訊，請參閱 [自主資料庫使用者 - 讓資料庫具有可攜性](https://msdn.microsoft.com/library/ff929188.aspx)。</span><span class="sxs-lookup"><span data-stu-id="487dc-114">For more information, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span> 

<span data-ttu-id="487dc-115">hello 主要取捨是管理 hello 大規模災害復原程序是更具挑戰性。</span><span class="sxs-lookup"><span data-stu-id="487dc-115">hello main trade-off is that managing hello disaster recovery process at scale is more challenging.</span></span> <span data-ttu-id="487dc-116">當您有多個資料庫維護 hello 認證使用的相同登入包含該使用 hello 多個資料庫中的使用者可能會否定 hello 優點包含的使用者。</span><span class="sxs-lookup"><span data-stu-id="487dc-116">When you have multiple databases that use hello same login, maintaining hello credentials using contained users in multiple databases may negate hello benefits of contained users.</span></span> <span data-ttu-id="487dc-117">例如，hello 密碼輪動原則需要進行變更以一致的方式在多個資料庫，而非 hello 登入的變更 hello 密碼一次 hello master 資料庫中。</span><span class="sxs-lookup"><span data-stu-id="487dc-117">For example, hello password rotation policy requires that changes be made consistently in multiple databases rather than changing hello password for hello login once in hello master database.</span></span> <span data-ttu-id="487dc-118">基於這個理由，如果您有多個資料庫的使用 hello 相同的使用者名稱和密碼，不建議使用包含的使用者。</span><span class="sxs-lookup"><span data-stu-id="487dc-118">For this reason, if you have multiple databases that use hello same user name and password, using contained users is not recommended.</span></span> 

## <a name="how-tooconfigure-logins-and-users"></a><span data-ttu-id="487dc-119">如何 tooconfigure 登入和使用者</span><span class="sxs-lookup"><span data-stu-id="487dc-119">How tooconfigure logins and users</span></span>
<span data-ttu-id="487dc-120">如果您使用的登入和使用者 （而不是包含的使用者），您必須採取額外的步驟 tooinsure 存在相同的登入該 hello hello master 資料庫中。</span><span class="sxs-lookup"><span data-stu-id="487dc-120">If you are using logins and users (rather than contained users), you must take extra steps tooinsure that hello same logins exist in hello master database.</span></span> <span data-ttu-id="487dc-121">hello 下列各節簡述 hello 步驟涉及和其他考量。</span><span class="sxs-lookup"><span data-stu-id="487dc-121">hello following sections outline hello steps involved and additional considerations.</span></span>

### <a name="set-up-user-access-tooa-secondary-or-recovered-database"></a><span data-ttu-id="487dc-122">設定使用者存取 tooa 次要或復原資料庫</span><span class="sxs-lookup"><span data-stu-id="487dc-122">Set up user access tooa secondary or recovered database</span></span>
<span data-ttu-id="487dc-123">為了讓 hello 次要資料庫 toobe 可用為唯讀的次要資料庫和 tooensure 適當的存取權 toohello 新的主要資料庫或 hello 資料庫使用地理還原復原 hello 主要 hello 目標伺服器的資料庫必須具有 hello在 hello 復原之前就定位適當的安全性設定。</span><span class="sxs-lookup"><span data-stu-id="487dc-123">In order for hello secondary database toobe usable as a read-only secondary database, and tooensure proper access toohello new primary database or hello database recovered using geo-restore, hello master database of hello target server must have hello appropriate security configuration in place before hello recovery.</span></span>

<span data-ttu-id="487dc-124">在本主題稍後描述 hello 針對每個步驟的特定權限。</span><span class="sxs-lookup"><span data-stu-id="487dc-124">hello specific permissions for each step are described later in this topic.</span></span>

<span data-ttu-id="487dc-125">準備使用者存取 tooa 應該做為設定地理複寫的一部分執行地理複寫的次要資料庫。</span><span class="sxs-lookup"><span data-stu-id="487dc-125">Preparing user access tooa geo-replication secondary should be performed as part configuring geo-replication.</span></span> <span data-ttu-id="487dc-126">準備 toohello 異地還原的資料庫使用者的存取權應該執行隨時 hello 原始伺服器在線上時 （例如為 hello DR 向下切入的一部分）。</span><span class="sxs-lookup"><span data-stu-id="487dc-126">Preparing user access toohello geo-restored databases should be performed at any time when hello original server is online (e.g. as part of hello DR drill).</span></span>

> [!NOTE]
> <span data-ttu-id="487dc-127">如果您無法移轉或異地還原 tooa 伺服器沒有正確設定的登入存取 tooit 會限制的 toohello 伺服器系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="487dc-127">If you fail over or geo-restore tooa server that does not have properly configured logins, access tooit will be limited toohello server admin account.</span></span>
> 
> 

<span data-ttu-id="487dc-128">設定登入 hello 目標伺服器上包含下列 3 個步驟：</span><span class="sxs-lookup"><span data-stu-id="487dc-128">Setting up logins on hello target server involves three steps outlined below:</span></span>

#### <a name="1-determine-logins-with-access-toohello-primary-database"></a><span data-ttu-id="487dc-129">1.判斷具有存取 toohello 主要資料庫的登入：</span><span class="sxs-lookup"><span data-stu-id="487dc-129">1. Determine logins with access toohello primary database:</span></span>
<span data-ttu-id="487dc-130">hello hello 程序的第一個步驟是的 toodetermine hello 目標伺服器複製哪些登入。</span><span class="sxs-lookup"><span data-stu-id="487dc-130">hello first step of hello process is toodetermine which logins must be duplicated on hello target server.</span></span> <span data-ttu-id="487dc-131">這是具有一對 SELECT 陳述式，一個在 hello 邏輯 master 資料庫中 hello 來源伺服器上，一個在 hello 主要資料庫本身。</span><span class="sxs-lookup"><span data-stu-id="487dc-131">This is accomplished with a pair of SELECT statements, one in hello logical master database on hello source server and one in hello primary database itself.</span></span>

<span data-ttu-id="487dc-132">只有 hello 伺服器管理員或成員的 hello **LoginManager**伺服器角色可以決定 hello 來源伺服器上的 hello 登入以 hello 下列 SELECT 陳述式。</span><span class="sxs-lookup"><span data-stu-id="487dc-132">Only hello server admin or a member of hello **LoginManager** server role can determine hello logins on hello source server with hello following SELECT statement.</span></span> 

    SELECT [name], [sid] 
    FROM [sys].[sql_logins] 
    WHERE [type_desc] = 'SQL_Login'

<span data-ttu-id="487dc-133">只有 hello db_owner 資料庫角色、 hello dbo 使用者或伺服器管理員的成員可以決定所有 hello 主要資料庫中的 hello 資料庫使用者主體。</span><span class="sxs-lookup"><span data-stu-id="487dc-133">Only a member of hello db_owner database role, hello dbo user, or server admin, can determine all of hello database user principals in hello primary database.</span></span>

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

#### <a name="2-find-hello-sid-for-hello-logins-identified-in-step-1"></a><span data-ttu-id="487dc-134">2.找出在步驟 1 所識別的 hello 登入 hello SID:</span><span class="sxs-lookup"><span data-stu-id="487dc-134">2. Find hello SID for hello logins identified in step 1:</span></span>
<span data-ttu-id="487dc-135">藉由比較 hello 查詢從 hello 上一節和比對 hello Sid 的 hello 輸出，您可以對應 hello 伺服器登入 toodatabase 使用者。</span><span class="sxs-lookup"><span data-stu-id="487dc-135">By comparing hello output of hello queries from hello previous section and matching hello SIDs, you can map hello server login toodatabase user.</span></span> <span data-ttu-id="487dc-136">具有相符 SID 與資料庫使用者的登入具有使用者存取 toothat 資料庫主體資料庫使用者的身分。</span><span class="sxs-lookup"><span data-stu-id="487dc-136">Logins that have a database user with a matching SID have user access toothat database as that database user principal.</span></span> 

<span data-ttu-id="487dc-137">hello 下列查詢可使用的 toosee 所有 hello 使用者主體及其 Sid 在資料庫中的。</span><span class="sxs-lookup"><span data-stu-id="487dc-137">hello following query can be used toosee all of hello user principals and their SIDs in a database.</span></span> <span data-ttu-id="487dc-138">只有 hello db_owner 資料庫角色或伺服器管理員的成員才能執行此查詢。</span><span class="sxs-lookup"><span data-stu-id="487dc-138">Only a member of hello db_owner database role or server admin can run this query.</span></span>

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

> [!NOTE]
> <span data-ttu-id="487dc-139">hello **INFORMATION_SCHEMA**和**sys**使用者擁有*NULL* Sid 和 hello**客體**SID 是**0x00**。</span><span class="sxs-lookup"><span data-stu-id="487dc-139">hello **INFORMATION_SCHEMA** and **sys** users have *NULL* SIDs, and hello **guest** SID is **0x00**.</span></span> <span data-ttu-id="487dc-140">hello **dbo** SID 可能開頭*0x01060000000001648000000000048454 開頭*，如果 hello 資料庫建立者即 hello 伺服器管理員，而不是屬於**DbManager**。</span><span class="sxs-lookup"><span data-stu-id="487dc-140">hello **dbo** SID may start with *0x01060000000001648000000000048454*, if hello database creator was hello server admin instead of a member of **DbManager**.</span></span>
> 
> 

#### <a name="3-create-hello-logins-on-hello-target-server"></a><span data-ttu-id="487dc-141">3.Hello 目標伺服器上建立 hello 登入：</span><span class="sxs-lookup"><span data-stu-id="487dc-141">3. Create hello logins on hello target server:</span></span>
<span data-ttu-id="487dc-142">hello 最後一個步驟是 toogo toohello 目標伺服器或伺服器，並產生以 hello hello 登入適當的 Sid。</span><span class="sxs-lookup"><span data-stu-id="487dc-142">hello last step is toogo toohello target server, or servers, and generate hello logins with hello appropriate SIDs.</span></span> <span data-ttu-id="487dc-143">hello 基本語法如下所示。</span><span class="sxs-lookup"><span data-stu-id="487dc-143">hello basic syntax is as follows.</span></span>

    CREATE LOGIN [<login name>]
    WITH PASSWORD = <login password>,
    SID = <desired login SID>

> [!NOTE]
> <span data-ttu-id="487dc-144">如果您想要 toogrant 使用者存取 toohello 次要資料庫，而不是 toohello 主要，您可以會使用下列語法的 hello 改變 hello hello 主要伺服器上的使用者登入。</span><span class="sxs-lookup"><span data-stu-id="487dc-144">If you want toogrant user access toohello secondary, but not toohello primary, you can do that by altering hello user login on hello primary server by using hello following syntax.</span></span>
> 
> <span data-ttu-id="487dc-145">ALTER LOGIN <login name> DISABLE</span><span class="sxs-lookup"><span data-stu-id="487dc-145">ALTER LOGIN <login name> DISABLE</span></span>
> 
> <span data-ttu-id="487dc-146">停用不會變更 hello 密碼，因此總是可以啟用它，如有需要。</span><span class="sxs-lookup"><span data-stu-id="487dc-146">DISABLE doesn’t change hello password, so you can always enable it if needed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="487dc-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="487dc-147">Next steps</span></span>
* <span data-ttu-id="487dc-148">如需管理資料庫存取和登入的詳細資訊，請參閱 [SQL Database 安全性︰管理資料庫存取與登入安全性](sql-database-manage-logins.md)。</span><span class="sxs-lookup"><span data-stu-id="487dc-148">For more information on managing database access and logins, see [SQL Database security: Manage database access and login security](sql-database-manage-logins.md).</span></span>
* <span data-ttu-id="487dc-149">如需自主資料庫使用者的詳細資訊，請參閱 [自主資料庫使用者 - 使資料庫可攜](https://msdn.microsoft.com/library/ff929188.aspx)。</span><span class="sxs-lookup"><span data-stu-id="487dc-149">For more information on contained database users, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span>
* <span data-ttu-id="487dc-150">如需使用和設定主動式異地複寫的相關資訊，請參閱[主動式異地複寫](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="487dc-150">For information about using and configuring active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md)</span></span>
* <span data-ttu-id="487dc-151">如需使用異地還原的相關資訊，請參閱[異地還原](sql-database-recovery-using-backups.md#geo-restore)</span><span class="sxs-lookup"><span data-stu-id="487dc-151">For information about using geo-restore, see [geo-restore](sql-database-recovery-using-backups.md#geo-restore)</span></span>

