---
title: "保護 SQL 資料倉儲中的資料庫 | Microsoft Docs"
description: "保護 Azure SQL 資料倉儲中的資料庫以便開發解決方案的秘訣。"
services: sql-data-warehouse
documentationcenter: NA
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: 8fa2f5ca-4cf5-4418-99a2-4dc745799850
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 6ea45c40bc428282faf24b4a08f8b0d345adb3fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="secure-a-database-in-sql-data-warehouse"></a><span data-ttu-id="a21f7-103">保護 SQL 資料倉儲中的資料庫</span><span class="sxs-lookup"><span data-stu-id="a21f7-103">Secure a database in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a21f7-104">安全性概觀</span><span class="sxs-lookup"><span data-stu-id="a21f7-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="a21f7-105">驗證</span><span class="sxs-lookup"><span data-stu-id="a21f7-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="a21f7-106">加密 (入口網站)</span><span class="sxs-lookup"><span data-stu-id="a21f7-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="a21f7-107">加密 (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="a21f7-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

<span data-ttu-id="a21f7-108">本文逐步解說保護 Azure SQL 資料倉儲資料庫的基本概念。</span><span class="sxs-lookup"><span data-stu-id="a21f7-108">This article walks through the basics of securing your Azure SQL Data Warehouse database.</span></span> <span data-ttu-id="a21f7-109">本文尤其著重於協助您開始利用資源，在資料庫上限制存取、保護資料，以及監視活動。</span><span class="sxs-lookup"><span data-stu-id="a21f7-109">In particular, this article will get you started with resources for limiting access, protecting data, and monitoring activities on a database.</span></span>

## <a name="connection-security"></a><span data-ttu-id="a21f7-110">連接安全性</span><span class="sxs-lookup"><span data-stu-id="a21f7-110">Connection security</span></span>
<span data-ttu-id="a21f7-111">「連線安全性」是指如何使用防火牆規則和連線加密，限制和保護資料庫的連線。</span><span class="sxs-lookup"><span data-stu-id="a21f7-111">Connection Security refers to how you restrict and secure connections to your database using firewall rules and connection encryption.</span></span>

<span data-ttu-id="a21f7-112">伺服器和資料庫兩者都可使用防火牆規則，拒絕來自未明確設為允許清單的 IP 位址的連線嘗試。</span><span class="sxs-lookup"><span data-stu-id="a21f7-112">Firewall rules are used by both the server and the database to reject connection attempts from IP addresses that have not been explicitly whitelisted.</span></span> <span data-ttu-id="a21f7-113">若要允許來自應用程式或用戶端機器的公用 IP 位址的連接，您必須先使用 Azure 入口網站、REST API 或 PowerShell 建立伺服器層級的防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="a21f7-113">To allow connections from your application or client machine's public IP address, you must first create a server-level firewall rule using the Azure Portal, REST API, or PowerShell.</span></span> <span data-ttu-id="a21f7-114">最好的作法是，您應該盡可能限制允許穿透您伺服器防火牆的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="a21f7-114">As a best practice, you should restrict the IP address ranges allowed through your server firewall as much as possible.</span></span>  <span data-ttu-id="a21f7-115">若要從您的本機電腦存取 Azure SQL 資料倉儲，請確定您的網路和本機電腦上的防火牆允許 TCP 連接埠 1433 上的傳出通訊。</span><span class="sxs-lookup"><span data-stu-id="a21f7-115">To access Azure SQL Data Warehouse from your local computer, ensure the firewall on your network and local computer allows outgoing communication on TCP port 1433.</span></span>  <span data-ttu-id="a21f7-116">如需詳細資訊，請參閱 [Azure SQL Database 防火牆][Azure SQL Database firewall]、[sp_set_firewall_rule][sp_set_firewall_rule] 和 [sp_set_database_firewall_rule][sp_set_database_firewall_rule]。</span><span class="sxs-lookup"><span data-stu-id="a21f7-116">For more information, see [Azure SQL Database firewall][Azure SQL Database firewall], [sp_set_firewall_rule][sp_set_firewall_rule], and [sp_set_database_firewall_rule][sp_set_database_firewall_rule].</span></span>

<span data-ttu-id="a21f7-117">預設會加密與 SQL 資料倉儲的連線。</span><span class="sxs-lookup"><span data-stu-id="a21f7-117">Connections to your SQL Data Warehouse are encrypted by default.</span></span>  <span data-ttu-id="a21f7-118">停用加密的修改連線設定會被忽略。</span><span class="sxs-lookup"><span data-stu-id="a21f7-118">Modifying connection settings to disable encryption are ignored.</span></span>

## <a name="authentication"></a><span data-ttu-id="a21f7-119">驗證</span><span class="sxs-lookup"><span data-stu-id="a21f7-119">Authentication</span></span>
<span data-ttu-id="a21f7-120">「驗證」是指連線到資料庫時如何證明身分識別。</span><span class="sxs-lookup"><span data-stu-id="a21f7-120">Authentication refers to how you prove your identity when connecting to the database.</span></span> <span data-ttu-id="a21f7-121">SQL 資料倉儲目前支援使用使用者名稱和密碼的 SQL Server 驗證，以及 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="a21f7-121">SQL Data Warehouse currently supports SQL Server Authentication with a username and password as well as a Azure Active Directory.</span></span> 

<span data-ttu-id="a21f7-122">當您為資料庫建立邏輯伺服器時，採取使用者名稱和密碼指定了「伺服器管理員」登入。</span><span class="sxs-lookup"><span data-stu-id="a21f7-122">When you created the logical server for your database, you specified a "server admin" login with a username and password.</span></span> <span data-ttu-id="a21f7-123">使用這些認證，您就可以透過 SQL Server 驗證，使用資料庫擁有者或 "dbo" 的身分驗證該伺服器上的任何資料庫。</span><span class="sxs-lookup"><span data-stu-id="a21f7-123">Using these credentials, you can authenticate to any database on that server as the database owner, or "dbo" through SQL Server Authentication.</span></span>

<span data-ttu-id="a21f7-124">不過，最佳作法是，貴組織的使用者應該使用不同的帳戶來驗證。</span><span class="sxs-lookup"><span data-stu-id="a21f7-124">However, as a best practice, your organization’s users should use a different account to authenticate.</span></span> <span data-ttu-id="a21f7-125">因為萬一應用程式的程式碼容易受到 SQL 插入式攻擊，您就可以限制授與應用程式的權限，並降低惡意活動的風險。</span><span class="sxs-lookup"><span data-stu-id="a21f7-125">This way you can limit the permissions granted to the application and reduce the risks of malicious activity in case your application code is vulnerable to a SQL injection attack.</span></span> 

<span data-ttu-id="a21f7-126">若要建立 SQL Server 驗證使用者，請使用伺服器管理員登入連接到您伺服器上的 **master** 資料庫，並建立新的伺服器登入。</span><span class="sxs-lookup"><span data-stu-id="a21f7-126">To create a SQL Server Authenticated user, connect to the **master** database on your server with your server admin login and create a new server login.</span></span>  <span data-ttu-id="a21f7-127">此外，在主要資料庫中建立一個使用者做為 Azure SQL 資料倉儲使用者是不錯的主意。</span><span class="sxs-lookup"><span data-stu-id="a21f7-127">Additionally, it is a good idea to create a user in the master database for Azure SQL Data Warehouse users.</span></span> <span data-ttu-id="a21f7-128">在主要資料庫中建立使用者，使用者就能使用類似 SSMS 的工具登入而不用指定資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="a21f7-128">Creating a user in master allows a user to login using tools like SSMS without specifying a database name.</span></span>  <span data-ttu-id="a21f7-129">它也可讓使用者使用物件總管來檢視 SQL Server 上的所有資料庫。</span><span class="sxs-lookup"><span data-stu-id="a21f7-129">It also allows them to use the object explorer to view all databases on a SQL server.</span></span>

```sql
-- Connect to master database and create a login
CREATE LOGIN ApplicationLogin WITH PASSWORD = 'Str0ng_password';
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

<span data-ttu-id="a21f7-130">然後使用您的伺服器管理員登入，連接到 **SQL 資料倉儲資料庫** ，並根據您剛建立的伺服器登入建立資料庫使用者。</span><span class="sxs-lookup"><span data-stu-id="a21f7-130">Then, connect to your **SQL Data Warehouse database** with your server admin login and create a database user based on the server login you just created.</span></span>

```sql
-- Connect to SQL DW database and create a database user
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

<span data-ttu-id="a21f7-131">如果使用者將會進行其他作業，例如建立登入或建立新資料庫，則也需要為他們指派主要資料庫中的 `Loginmanager` 和 `dbmanager` 角色。</span><span class="sxs-lookup"><span data-stu-id="a21f7-131">If a user will be doing additional operations such as creating logins or creating new databases, they will also need to be assigned to the `Loginmanager` and `dbmanager` roles in the master database.</span></span> <span data-ttu-id="a21f7-132">如需有關這些額外角色及向 SQL Database 驗證的詳細資訊，請參閱[管理 Azure SQL Database 中的資料庫和登入][Managing databases and logins in Azure SQL Database]。</span><span class="sxs-lookup"><span data-stu-id="a21f7-132">For more information on these additonal roles and authenticating to a SQL Database, see [Managing databases and logins in Azure SQL Database][Managing databases and logins in Azure SQL Database].</span></span>  <span data-ttu-id="a21f7-133">如需更多將 Azure AD 用於 SQL 資料倉儲的詳細資料，請參閱[使用 Azure Active Directory 驗證連線到 SQL 資料倉儲][Connecting to SQL Data Warehouse By Using Azure Active Directory Authentication]。</span><span class="sxs-lookup"><span data-stu-id="a21f7-133">For more details on Azure AD for SQL Data Warehouse, see [Connecting to SQL Data Warehouse By Using Azure Active Directory Authentication][Connecting to SQL Data Warehouse By Using Azure Active Directory Authentication].</span></span>

## <a name="authorization"></a><span data-ttu-id="a21f7-134">Authorization</span><span class="sxs-lookup"><span data-stu-id="a21f7-134">Authorization</span></span>
<span data-ttu-id="a21f7-135">「授權」是指在 Azure SQL 資料倉儲內可以執行的動作，這是由使用者帳戶的角色成員資格和權限所控制。</span><span class="sxs-lookup"><span data-stu-id="a21f7-135">Authorization refers to what you can do within an Azure SQL Data Warehouse database, and this is controlled by your user account's role memberships and permissions.</span></span> <span data-ttu-id="a21f7-136">最好的作法是，您應該授與使用者所需的最低權限。</span><span class="sxs-lookup"><span data-stu-id="a21f7-136">As a best practice, you should grant users the least privileges necessary.</span></span> <span data-ttu-id="a21f7-137">Azure SQL 資料倉儲可讓您輕鬆地透過 T-SQL 中的角色進行上述管理：</span><span class="sxs-lookup"><span data-stu-id="a21f7-137">Azure SQL Data Warehouse makes this easy to manage with roles in T-SQL:</span></span>

```sql
EXEC sp_addrolemember 'db_datareader', 'ApplicationUser'; -- allows ApplicationUser to read data
EXEC sp_addrolemember 'db_datawriter', 'ApplicationUser'; -- allows ApplicationUser to write data
```

<span data-ttu-id="a21f7-138">您所連線的伺服器管理員帳戶是 db_owner 的成員，有權限在資料庫中執行任何動作。</span><span class="sxs-lookup"><span data-stu-id="a21f7-138">The server admin account you are connecting with is a member of db_owner, which has authority to do anything within the database.</span></span> <span data-ttu-id="a21f7-139">請儲存此帳戶，以便部署結構描述升級及其他管理作業。</span><span class="sxs-lookup"><span data-stu-id="a21f7-139">Save this account for deploying schema upgrades and other management operations.</span></span> <span data-ttu-id="a21f7-140">請使用具更多有限權限的 "ApplicationUser" 帳戶，從應用程式連線到具應用程式所需之最低權限的資料庫。</span><span class="sxs-lookup"><span data-stu-id="a21f7-140">Use the "ApplicationUser" account with more limited permissions to connect from your application to the database with the least privileges needed by your application.</span></span>

<span data-ttu-id="a21f7-141">有許多方式可以進一步限制使用者透過 Azure SQL Database 可以執行的動作：</span><span class="sxs-lookup"><span data-stu-id="a21f7-141">There are ways to further limit what a user can do with Azure SQL Database:</span></span>

* <span data-ttu-id="a21f7-142">細微的[權限][Permissions]可讓您控制您可以對資料庫中個別資料行、資料表、檢視、程序和其他物件執行哪些作業。</span><span class="sxs-lookup"><span data-stu-id="a21f7-142">Granular [Permissions][Permissions] let you control which operations you can do on individual columns, tables, views, procedures, and other objects in the database.</span></span> <span data-ttu-id="a21f7-143">使用細微權限，以擁有最大控制權，並授與所需的最小權限。</span><span class="sxs-lookup"><span data-stu-id="a21f7-143">Use granular permissions to have the most control and grant the minimum permissions necessary.</span></span> <span data-ttu-id="a21f7-144">細微權限系統有點複雜，而且需要進行一些研究才能有效地使用。</span><span class="sxs-lookup"><span data-stu-id="a21f7-144">The granular permission system is somewhat complicated and will require some study to use effectively.</span></span>
* <span data-ttu-id="a21f7-145">除了 db_datareader 和 db_datawriter 以外，[資料庫角色][Database roles]均可以用來建立權力較大的應用程式使用者帳戶，或權力較小的管理帳戶。</span><span class="sxs-lookup"><span data-stu-id="a21f7-145">[Database roles][Database roles] other than db_datareader and db_datawriter can be used to create more powerful application user accounts or less powerful management accounts.</span></span> <span data-ttu-id="a21f7-146">內建固定資料庫角色提供簡單的方式來授與權限，但可能會導致授與的權限多於所需的權限。</span><span class="sxs-lookup"><span data-stu-id="a21f7-146">The built-in fixed database roles provide an easy way to grant permissions, but can result in granting more permissions than are necessary.</span></span>
* <span data-ttu-id="a21f7-147">[預存程序][Stored procedures]可用來限制對資料庫可採取的動作。</span><span class="sxs-lookup"><span data-stu-id="a21f7-147">[Stored procedures][Stored procedures] can be used to limit the actions that can be taken on the database.</span></span>

<span data-ttu-id="a21f7-148">要從 Azure 傳統入口網站或使用 Azure 資源管理員 API 管理資料庫和邏輯伺服器，是由入口網站使用者帳戶的角色指派所控制。</span><span class="sxs-lookup"><span data-stu-id="a21f7-148">Managing databases and logical servers from the Azure Classic Portal or using the Azure Resource Manager API is controlled by your portal user account's role assignments.</span></span> <span data-ttu-id="a21f7-149">如需有關此主題的詳細資訊，請參閱 [Azure 入口網站中的角色型存取控制][Role-based access control in Azure Portal]。</span><span class="sxs-lookup"><span data-stu-id="a21f7-149">For more information on this topic, see [Role-based access control in Azure Portal][Role-based access control in Azure Portal].</span></span>

## <a name="encryption"></a><span data-ttu-id="a21f7-150">加密</span><span class="sxs-lookup"><span data-stu-id="a21f7-150">Encryption</span></span>
<span data-ttu-id="a21f7-151">Azure SQL 資料倉儲透明資料加密 (TDE) 可以對待用資料執行即時加密和解密，協助防止惡意活動的威脅。</span><span class="sxs-lookup"><span data-stu-id="a21f7-151">Azure SQL Data Warehouse Transparent Data Encryption (TDE) helps protect against the threat of malicious activity by performing real-time encryption and decryption of your data at rest.</span></span>  <span data-ttu-id="a21f7-152">當您加密資料庫時，相關聯的備份和交易記錄檔就會加密，完全不需要變更您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="a21f7-152">When you encrypt your database, associated backups and transaction log files are encrypted without requiring any changes to your applications.</span></span> <span data-ttu-id="a21f7-153">TDE 會使用稱為資料庫加密金鑰的對稱金鑰來加密整個資料庫的儲存體。</span><span class="sxs-lookup"><span data-stu-id="a21f7-153">TDE encrypts the storage of an entire database by using a symmetric key called the database encryption key.</span></span> <span data-ttu-id="a21f7-154">在 SQL Database 中，資料庫加密金鑰是由內建伺服器憑證保護。</span><span class="sxs-lookup"><span data-stu-id="a21f7-154">In SQL Database the database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="a21f7-155">內建伺服器憑證對每個 SQL Database 伺服器都是唯一的。</span><span class="sxs-lookup"><span data-stu-id="a21f7-155">The built-in server certificate is unique for each SQL Database server.</span></span> <span data-ttu-id="a21f7-156">Microsoft 至少每 90 天會自動替換這些憑證。</span><span class="sxs-lookup"><span data-stu-id="a21f7-156">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="a21f7-157">「SQL 資料倉儲」使用的加密演算法是 AES-256。</span><span class="sxs-lookup"><span data-stu-id="a21f7-157">The encryption algorithm used by SQL Data Warehouse is AES-256.</span></span> <span data-ttu-id="a21f7-158">如需 TDE 的一般描述，請參閱[透明資料加密][Transparent Data Encryption]。</span><span class="sxs-lookup"><span data-stu-id="a21f7-158">For a general description of TDE, see [Transparent Data Encryption][Transparent Data Encryption].</span></span>

<span data-ttu-id="a21f7-159">您可以使用 [Azure 入口網站][Encryption with Portal]或 [T-SQL][Encryption with TSQL] 將資料庫加密。</span><span class="sxs-lookup"><span data-stu-id="a21f7-159">You can encrypt your database using the [Azure Portal][Encryption with Portal] or [T-SQL][Encryption with TSQL].</span></span>

## <a name="next-steps"></a><span data-ttu-id="a21f7-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a21f7-160">Next steps</span></span>
<span data-ttu-id="a21f7-161">如需使用不同通訊協定連接到您的 SQL 資料倉儲的詳細資訊和範例，請參閱[連接到 SQL 資料倉儲][Connect to SQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="a21f7-161">For details and examples on connecting to your SQL Data Warehouse with different protocols, see [Connect to SQL Data Warehouse][Connect to SQL Data Warehouse].</span></span>

<!--Image references-->

<!--Article references-->
[Connect to SQL Data Warehouse]: ./sql-data-warehouse-connect-overview.md
[Encryption with Portal]: ./sql-data-warehouse-encryption-tde.md
[Encryption with TSQL]: ./sql-data-warehouse-encryption-tde-tsql.md
[Connecting to SQL Data Warehouse By Using Azure Active Directory Authentication]: ./sql-data-warehouse-authentication.md

<!--MSDN references-->
[Azure SQL Database firewall]: https://msdn.microsoft.com/library/ee621782.aspx
[sp_set_firewall_rule]: https://msdn.microsoft.com/library/dn270017.aspx
[sp_set_database_firewall_rule]: https://msdn.microsoft.com/library/dn270010.aspx
[Database roles]: https://msdn.microsoft.com/library/ms189121.aspx
[Managing databases and logins in Azure SQL Database]: https://msdn.microsoft.com/library/ee336235.aspx
[Permissions]: https://msdn.microsoft.com/library/ms191291.aspx
[Stored procedures]: https://msdn.microsoft.com/library/ms190782.aspx
[Transparent Data Encryption]: https://msdn.microsoft.com/library/bb934049.aspx
[Azure portal]: https://portal.azure.com/

<!--Other Web references-->
[Role-based access control in Azure Portal]: https://azure.microsoft.com/documentation/articles/role-based-access-control-configure
