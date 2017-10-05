---
title: "設定 Azure SQL Database 安全性以供災害復原使用 | Microsoft Docs"
description: "本主題說明如果發生資料中心服務中斷或其他災害，在資料庫還原或容錯移轉至次要伺服器之後，設定和管理安全性時的安全性考量"
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
ms.openlocfilehash: de5e1732dab570b80692efcdd08e4ed2d8c98800
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-and-manage-azure-sql-database-security-for-geo-restore-or-failover"></a><span data-ttu-id="9116a-103">建立和管理 Azure SQL Database 安全性以供異地還原或容錯移轉使用</span><span class="sxs-lookup"><span data-stu-id="9116a-103">Configure and manage Azure SQL Database security for geo-restore or failover</span></span> 

> [!NOTE]
> <span data-ttu-id="9116a-104">[作用中異地複寫](sql-database-geo-replication-overview.md)現在可供所有服務層中的所有資料庫使用。</span><span class="sxs-lookup"><span data-stu-id="9116a-104">[Active geo-replication](sql-database-geo-replication-overview.md) is now available for all databases in all service tiers.</span></span>
>  

## <a name="overview-of-authentication-requirements-for-disaster-recovery"></a><span data-ttu-id="9116a-105">災害復原的驗證需求概觀</span><span class="sxs-lookup"><span data-stu-id="9116a-105">Overview of authentication requirements for disaster recovery</span></span>
<span data-ttu-id="9116a-106">本主題描述設定和控制[主動式異地複寫](sql-database-geo-replication-overview.md)的驗證需求，以及設定次要資料庫之使用者存取所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="9116a-106">This topic describes the authentication requirements to configure and control [active geo-replication](sql-database-geo-replication-overview.md) and the steps required to set up user access to the secondary database.</span></span> <span data-ttu-id="9116a-107">它也會描述如何在使用 [異地還原](sql-database-recovery-using-backups.md#geo-restore)之後啟用復原資料庫的存取權。</span><span class="sxs-lookup"><span data-stu-id="9116a-107">It also describes how enable access to the recovered database after using [geo-restore](sql-database-recovery-using-backups.md#geo-restore).</span></span> <span data-ttu-id="9116a-108">如需復原選項的詳細資訊，請參閱 [商務持續性概觀](sql-database-business-continuity.md)。</span><span class="sxs-lookup"><span data-stu-id="9116a-108">For more information on recovery options, see [Business Continuity Overview](sql-database-business-continuity.md).</span></span>

## <a name="disaster-recovery-with-contained-users"></a><span data-ttu-id="9116a-109">災害復原與自主使用者</span><span class="sxs-lookup"><span data-stu-id="9116a-109">Disaster recovery with contained users</span></span>
<span data-ttu-id="9116a-110">不同於傳統的使用者必須對應到 master 資料庫中的登入，自主使用者完全由資料庫本身管理。</span><span class="sxs-lookup"><span data-stu-id="9116a-110">Unlike traditional users, which must be mapped to logins in the master database, a contained user is managed completely by the database itself.</span></span> <span data-ttu-id="9116a-111">這樣有兩個優點。</span><span class="sxs-lookup"><span data-stu-id="9116a-111">This has two benefits.</span></span> <span data-ttu-id="9116a-112">在災害復原案例中，使用者可以繼續連線到新的主要資料庫或使用異地還原復原的資料庫，而不需任何額外的組態，因為資料庫可管理使用者。</span><span class="sxs-lookup"><span data-stu-id="9116a-112">In the disaster recovery scenario, the users can continue to connect to the new primary database or the database recovered using geo-restore without any additional configuration, because the database manages the users.</span></span> <span data-ttu-id="9116a-113">從登入的觀點來看，這個組態也有潛在的延展性和效能優勢。</span><span class="sxs-lookup"><span data-stu-id="9116a-113">There are also potential scalability and performance benefits from this configuration from a login perspective.</span></span> <span data-ttu-id="9116a-114">如需詳細資訊，請參閱 [自主資料庫使用者 - 讓資料庫具有可攜性](https://msdn.microsoft.com/library/ff929188.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9116a-114">For more information, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span> 

<span data-ttu-id="9116a-115">主要的缺點是管理大規模災害復原程序更具挑戰性。</span><span class="sxs-lookup"><span data-stu-id="9116a-115">The main trade-off is that managing the disaster recovery process at scale is more challenging.</span></span> <span data-ttu-id="9116a-116">當您有使用相同登入的多個資料庫時，維護在多個資料庫中使用自主使用者的認證可能不利於自主使用者。</span><span class="sxs-lookup"><span data-stu-id="9116a-116">When you have multiple databases that use the same login, maintaining the credentials using contained users in multiple databases may negate the benefits of contained users.</span></span> <span data-ttu-id="9116a-117">例如，密碼替換原則需要在多個資料庫中進行一致的變更，而不是在主要資料庫一次變更登入的密碼。</span><span class="sxs-lookup"><span data-stu-id="9116a-117">For example, the password rotation policy requires that changes be made consistently in multiple databases rather than changing the password for the login once in the master database.</span></span> <span data-ttu-id="9116a-118">基於這個理由，如果您有使用相同使用者名稱和密碼的多個資料庫，則不建議使用自主使用者。</span><span class="sxs-lookup"><span data-stu-id="9116a-118">For this reason, if you have multiple databases that use the same user name and password, using contained users is not recommended.</span></span> 

## <a name="how-to-configure-logins-and-users"></a><span data-ttu-id="9116a-119">如何設定登入和使用者</span><span class="sxs-lookup"><span data-stu-id="9116a-119">How to configure logins and users</span></span>
<span data-ttu-id="9116a-120">如果您使用登入和使用者 (而非自主使用者)，必須採取額外步驟以確保主要資料庫中具有相同的登入。</span><span class="sxs-lookup"><span data-stu-id="9116a-120">If you are using logins and users (rather than contained users), you must take extra steps to insure that the same logins exist in the master database.</span></span> <span data-ttu-id="9116a-121">下列各節概述涉及的步驟和其他考量。</span><span class="sxs-lookup"><span data-stu-id="9116a-121">The following sections outline the steps involved and additional considerations.</span></span>

### <a name="set-up-user-access-to-a-secondary-or-recovered-database"></a><span data-ttu-id="9116a-122">設定次要或復原資料庫的使用者存取</span><span class="sxs-lookup"><span data-stu-id="9116a-122">Set up user access to a secondary or recovered database</span></span>
<span data-ttu-id="9116a-123">為了讓次要資料庫可做為唯讀次要資料庫使用，並確保可適當存取新的主要資料庫或使用異地還原復原的資料庫，目標伺服器的主要資料庫必須在復原之前具有適當的安全性組態。</span><span class="sxs-lookup"><span data-stu-id="9116a-123">In order for the secondary database to be usable as a read-only secondary database, and to ensure proper access to the new primary database or the database recovered using geo-restore, the master database of the target server must have the appropriate security configuration in place before the recovery.</span></span>

<span data-ttu-id="9116a-124">本主題稍後說明每個步驟的特定權限。</span><span class="sxs-lookup"><span data-stu-id="9116a-124">The specific permissions for each step are described later in this topic.</span></span>

<span data-ttu-id="9116a-125">使用者對異地複寫次要資料庫的存取權準備工作，應該是在設定異地複寫的期間執行。</span><span class="sxs-lookup"><span data-stu-id="9116a-125">Preparing user access to a geo-replication secondary should be performed as part configuring geo-replication.</span></span> <span data-ttu-id="9116a-126">使用者對異地還原資料庫的存取權準備工作，應該是在原始伺服器處於線上狀態的任何時間執行 (例如在 DR 演習期間)。</span><span class="sxs-lookup"><span data-stu-id="9116a-126">Preparing user access to the geo-restored databases should be performed at any time when the original server is online (e.g. as part of the DR drill).</span></span>

> [!NOTE]
> <span data-ttu-id="9116a-127">如果您容錯移轉或異地還原至沒有正確設定登入存取權的伺服器，它會受限於伺服器管理帳戶。</span><span class="sxs-lookup"><span data-stu-id="9116a-127">If you fail over or geo-restore to a server that does not have properly configured logins, access to it will be limited to the server admin account.</span></span>
> 
> 

<span data-ttu-id="9116a-128">設定目標伺服器上的登入包含下列概述的三個步驟︰</span><span class="sxs-lookup"><span data-stu-id="9116a-128">Setting up logins on the target server involves three steps outlined below:</span></span>

#### <a name="1-determine-logins-with-access-to-the-primary-database"></a><span data-ttu-id="9116a-129">1.決定具備主要資料庫存取權的登入：</span><span class="sxs-lookup"><span data-stu-id="9116a-129">1. Determine logins with access to the primary database:</span></span>
<span data-ttu-id="9116a-130">程序的第一個步驟是判斷目標伺服器上必須複製哪些登入。</span><span class="sxs-lookup"><span data-stu-id="9116a-130">The first step of the process is to determine which logins must be duplicated on the target server.</span></span> <span data-ttu-id="9116a-131">這是以一組 SELECT 陳述式完成，一個在來源伺服器上的邏輯 master 資料庫中，一個在主要資料庫本身。</span><span class="sxs-lookup"><span data-stu-id="9116a-131">This is accomplished with a pair of SELECT statements, one in the logical master database on the source server and one in the primary database itself.</span></span>

<span data-ttu-id="9116a-132">只有伺服器系統管理員或 **LoginManager** 伺服器角色的成員可以利用下列 SELECT 陳述式判斷來源伺服器上的登入。</span><span class="sxs-lookup"><span data-stu-id="9116a-132">Only the server admin or a member of the **LoginManager** server role can determine the logins on the source server with the following SELECT statement.</span></span> 

    SELECT [name], [sid] 
    FROM [sys].[sql_logins] 
    WHERE [type_desc] = 'SQL_Login'

<span data-ttu-id="9116a-133">只有 db_owner 資料庫角色的成員、dbo 使用者或伺服器系統管理員可以判斷主要資料庫中的所有資料庫使用者主體。</span><span class="sxs-lookup"><span data-stu-id="9116a-133">Only a member of the db_owner database role, the dbo user, or server admin, can determine all of the database user principals in the primary database.</span></span>

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

#### <a name="2-find-the-sid-for-the-logins-identified-in-step-1"></a><span data-ttu-id="9116a-134">2.尋找在步驟 1 中識別的登入 SID：</span><span class="sxs-lookup"><span data-stu-id="9116a-134">2. Find the SID for the logins identified in step 1:</span></span>
<span data-ttu-id="9116a-135">藉由比較上一節查詢的輸出並比對 SID，您可以將伺服器登入對應到資料庫使用者。</span><span class="sxs-lookup"><span data-stu-id="9116a-135">By comparing the output of the queries from the previous section and matching the SIDs, you can map the server login to database user.</span></span> <span data-ttu-id="9116a-136">具有資料庫使用者及相符 SID 的登入也會有該資料庫的使用者存取權做為資料庫使用者主體。</span><span class="sxs-lookup"><span data-stu-id="9116a-136">Logins that have a database user with a matching SID have user access to that database as that database user principal.</span></span> 

<span data-ttu-id="9116a-137">下列查詢可用來查看資料庫中的所有使用者主體及其 SID。</span><span class="sxs-lookup"><span data-stu-id="9116a-137">The following query can be used to see all of the user principals and their SIDs in a database.</span></span> <span data-ttu-id="9116a-138">只有 db_owner 資料庫角色的成員或伺服器系統管理員才能執行此查詢。</span><span class="sxs-lookup"><span data-stu-id="9116a-138">Only a member of the db_owner database role or server admin can run this query.</span></span>

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

> [!NOTE]
> <span data-ttu-id="9116a-139">**INFORMATION_SCHEMA** 和 **sys** 使用者有「NULL」SID，而**來賓**的 SID 是 **0x00**。</span><span class="sxs-lookup"><span data-stu-id="9116a-139">The **INFORMATION_SCHEMA** and **sys** users have *NULL* SIDs, and the **guest** SID is **0x00**.</span></span> <span data-ttu-id="9116a-140">如果資料庫建立者是伺服器系統管理員，而不是 **DbManager** 的成員，**dbo** SID 可能會以 *0x01060000000001648000000000048454* 開頭。</span><span class="sxs-lookup"><span data-stu-id="9116a-140">The **dbo** SID may start with *0x01060000000001648000000000048454*, if the database creator was the server admin instead of a member of **DbManager**.</span></span>
> 
> 

#### <a name="3-create-the-logins-on-the-target-server"></a><span data-ttu-id="9116a-141">3.在目標伺服器上建立登入：</span><span class="sxs-lookup"><span data-stu-id="9116a-141">3. Create the logins on the target server:</span></span>
<span data-ttu-id="9116a-142">最後一個步驟是移至目標伺服器或伺服器，並以適當的 SID 產生登入。</span><span class="sxs-lookup"><span data-stu-id="9116a-142">The last step is to go to the target server, or servers, and generate the logins with the appropriate SIDs.</span></span> <span data-ttu-id="9116a-143">基本語法如下所示。</span><span class="sxs-lookup"><span data-stu-id="9116a-143">The basic syntax is as follows.</span></span>

    CREATE LOGIN [<login name>]
    WITH PASSWORD = <login password>,
    SID = <desired login SID>

> [!NOTE]
> <span data-ttu-id="9116a-144">如果您想要授與使用者次要資料庫的存取權，而不是主要資料庫的，您可以藉由使用下列語法在主要伺服器上改變使用者登入，即可完成。</span><span class="sxs-lookup"><span data-stu-id="9116a-144">If you want to grant user access to the secondary, but not to the primary, you can do that by altering the user login on the primary server by using the following syntax.</span></span>
> 
> <span data-ttu-id="9116a-145">ALTER LOGIN <login name> DISABLE</span><span class="sxs-lookup"><span data-stu-id="9116a-145">ALTER LOGIN <login name> DISABLE</span></span>
> 
> <span data-ttu-id="9116a-146">DISABLE 不會變更密碼，因此必要時可以永遠啟用。</span><span class="sxs-lookup"><span data-stu-id="9116a-146">DISABLE doesn’t change the password, so you can always enable it if needed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="9116a-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9116a-147">Next steps</span></span>
* <span data-ttu-id="9116a-148">如需管理資料庫存取和登入的詳細資訊，請參閱 [SQL Database 安全性︰管理資料庫存取與登入安全性](sql-database-manage-logins.md)。</span><span class="sxs-lookup"><span data-stu-id="9116a-148">For more information on managing database access and logins, see [SQL Database security: Manage database access and login security](sql-database-manage-logins.md).</span></span>
* <span data-ttu-id="9116a-149">如需自主資料庫使用者的詳細資訊，請參閱 [自主資料庫使用者 - 使資料庫可攜](https://msdn.microsoft.com/library/ff929188.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9116a-149">For more information on contained database users, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span>
* <span data-ttu-id="9116a-150">如需使用和設定主動式異地複寫的相關資訊，請參閱[主動式異地複寫](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="9116a-150">For information about using and configuring active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md)</span></span>
* <span data-ttu-id="9116a-151">如需使用異地還原的相關資訊，請參閱[異地還原](sql-database-recovery-using-backups.md#geo-restore)</span><span class="sxs-lookup"><span data-stu-id="9116a-151">For information about using geo-restore, see [geo-restore](sql-database-recovery-using-backups.md#geo-restore)</span></span>

