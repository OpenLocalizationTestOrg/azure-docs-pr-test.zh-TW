---
title: "aaaSecure SQL 資料倉儲中的資料庫 |Microsoft 文件"
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
ms.openlocfilehash: 5ef4d760e00be46bfe7808bc95dbe1e4b3a51165
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-database-in-sql-data-warehouse"></a><span data-ttu-id="0400f-103">保護 SQL 資料倉儲中的資料庫</span><span class="sxs-lookup"><span data-stu-id="0400f-103">Secure a database in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0400f-104">安全性概觀</span><span class="sxs-lookup"><span data-stu-id="0400f-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="0400f-105">驗證</span><span class="sxs-lookup"><span data-stu-id="0400f-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="0400f-106">加密 (入口網站)</span><span class="sxs-lookup"><span data-stu-id="0400f-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="0400f-107">加密 (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="0400f-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

<span data-ttu-id="0400f-108">本文逐步 hello 的保護您的 Azure SQL 資料倉儲資料庫的基本概念。</span><span class="sxs-lookup"><span data-stu-id="0400f-108">This article walks through hello basics of securing your Azure SQL Data Warehouse database.</span></span> <span data-ttu-id="0400f-109">本文尤其著重於協助您開始利用資源，在資料庫上限制存取、保護資料，以及監視活動。</span><span class="sxs-lookup"><span data-stu-id="0400f-109">In particular, this article will get you started with resources for limiting access, protecting data, and monitoring activities on a database.</span></span>

## <a name="connection-security"></a><span data-ttu-id="0400f-110">連接安全性</span><span class="sxs-lookup"><span data-stu-id="0400f-110">Connection security</span></span>
<span data-ttu-id="0400f-111">連線安全性是指的 toohow 您限制及保護 tooyour 資料庫的連接使用防火牆規則和連線加密。</span><span class="sxs-lookup"><span data-stu-id="0400f-111">Connection Security refers toohow you restrict and secure connections tooyour database using firewall rules and connection encryption.</span></span>

<span data-ttu-id="0400f-112">防火牆規則會使用兩個 hello 伺服器與 hello 資料庫 tooreject 連線嘗試從尚未明確允許的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0400f-112">Firewall rules are used by both hello server and hello database tooreject connection attempts from IP addresses that have not been explicitly whitelisted.</span></span> <span data-ttu-id="0400f-113">從您的應用程式或用戶端電腦的公用 IP 位址的 tooallow 連線，您必須先建立 hello Azure 入口網站、 REST API 或 PowerShell，使用的伺服器層級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="0400f-113">tooallow connections from your application or client machine's public IP address, you must first create a server-level firewall rule using hello Azure Portal, REST API, or PowerShell.</span></span> <span data-ttu-id="0400f-114">最佳做法，您應該限制 hello 盡可能透過您伺服器的防火牆允許的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="0400f-114">As a best practice, you should restrict hello IP address ranges allowed through your server firewall as much as possible.</span></span>  <span data-ttu-id="0400f-115">tooaccess Azure SQL 資料倉儲從本機電腦，請確定 hello 網路和本機電腦上的防火牆允許 TCP 通訊埠 1433年上的傳出通訊。</span><span class="sxs-lookup"><span data-stu-id="0400f-115">tooaccess Azure SQL Data Warehouse from your local computer, ensure hello firewall on your network and local computer allows outgoing communication on TCP port 1433.</span></span>  <span data-ttu-id="0400f-116">如需詳細資訊，請參閱 [Azure SQL Database 防火牆][Azure SQL Database firewall]、[sp_set_firewall_rule][sp_set_firewall_rule] 和 [sp_set_database_firewall_rule][sp_set_database_firewall_rule]。</span><span class="sxs-lookup"><span data-stu-id="0400f-116">For more information, see [Azure SQL Database firewall][Azure SQL Database firewall], [sp_set_firewall_rule][sp_set_firewall_rule], and [sp_set_database_firewall_rule][sp_set_database_firewall_rule].</span></span>

<span data-ttu-id="0400f-117">依預設會加密連接 tooyour SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="0400f-117">Connections tooyour SQL Data Warehouse are encrypted by default.</span></span>  <span data-ttu-id="0400f-118">修改連線設定 toodisable 加密會被忽略。</span><span class="sxs-lookup"><span data-stu-id="0400f-118">Modifying connection settings toodisable encryption are ignored.</span></span>

## <a name="authentication"></a><span data-ttu-id="0400f-119">驗證</span><span class="sxs-lookup"><span data-stu-id="0400f-119">Authentication</span></span>
<span data-ttu-id="0400f-120">驗證是指 toohow 連接 toohello 資料庫時，證明您的身分識別。</span><span class="sxs-lookup"><span data-stu-id="0400f-120">Authentication refers toohow you prove your identity when connecting toohello database.</span></span> <span data-ttu-id="0400f-121">SQL 資料倉儲目前支援使用使用者名稱和密碼的 SQL Server 驗證，以及 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="0400f-121">SQL Data Warehouse currently supports SQL Server Authentication with a username and password as well as a Azure Active Directory.</span></span> 

<span data-ttu-id="0400f-122">當您為您的資料庫建立 hello 邏輯伺服器時，您可以指定 「 伺服器管理員 」 的登入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="0400f-122">When you created hello logical server for your database, you specified a "server admin" login with a username and password.</span></span> <span data-ttu-id="0400f-123">您可以使用這些認證，驗證 tooany hello 資料庫擁有者或透過 SQL Server 驗證的"dbo"與該伺服器上的資料庫。</span><span class="sxs-lookup"><span data-stu-id="0400f-123">Using these credentials, you can authenticate tooany database on that server as hello database owner, or "dbo" through SQL Server Authentication.</span></span>

<span data-ttu-id="0400f-124">不過，最佳做法，貴組織的使用者應該使用不同的帳戶 tooauthenticate。</span><span class="sxs-lookup"><span data-stu-id="0400f-124">However, as a best practice, your organization’s users should use a different account tooauthenticate.</span></span> <span data-ttu-id="0400f-125">如此一來您可以限制 hello 權限授與 toohello 應用程式，並減少惡意活動的 hello 風險，應用程式程式碼是很容易遭受 tooa SQL 資料隱碼攻擊。</span><span class="sxs-lookup"><span data-stu-id="0400f-125">This way you can limit hello permissions granted toohello application and reduce hello risks of malicious activity in case your application code is vulnerable tooa SQL injection attack.</span></span> 

<span data-ttu-id="0400f-126">SQL Server 驗證使用者，toocreate 連接 toohello**主要**與伺服器的系統管理員登入您伺服器上的資料庫，並建立新的伺服器登入。</span><span class="sxs-lookup"><span data-stu-id="0400f-126">toocreate a SQL Server Authenticated user, connect toohello **master** database on your server with your server admin login and create a new server login.</span></span>  <span data-ttu-id="0400f-127">此外，也會建議 toocreate 使用者的 Azure SQL 資料倉儲使用者 hello master 資料庫中。</span><span class="sxs-lookup"><span data-stu-id="0400f-127">Additionally, it is a good idea toocreate a user in hello master database for Azure SQL Data Warehouse users.</span></span> <span data-ttu-id="0400f-128">在 master 中建立使用者，可讓使用者 toologin 使用 SSMS 等工具，而不指定資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="0400f-128">Creating a user in master allows a user toologin using tools like SSMS without specifying a database name.</span></span>  <span data-ttu-id="0400f-129">它也可讓它們 toouse hello 物件總管 中 tooview SQL server 的所有資料庫。</span><span class="sxs-lookup"><span data-stu-id="0400f-129">It also allows them toouse hello object explorer tooview all databases on a SQL server.</span></span>

```sql
-- Connect toomaster database and create a login
CREATE LOGIN ApplicationLogin WITH PASSWORD = 'Str0ng_password';
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

<span data-ttu-id="0400f-130">然後，連接 tooyour **SQL 資料倉儲資料庫**與伺服器的系統管理員登入並建立根據 hello 伺服器登入您剛才建立的資料庫使用者。</span><span class="sxs-lookup"><span data-stu-id="0400f-130">Then, connect tooyour **SQL Data Warehouse database** with your server admin login and create a database user based on hello server login you just created.</span></span>

```sql
-- Connect tooSQL DW database and create a database user
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

<span data-ttu-id="0400f-131">如果使用者將會執行其他作業，例如建立登入或建立新的資料庫，他們也需要指派 toobe toohello`Loginmanager`和`dbmanager`hello master 資料庫中的角色。</span><span class="sxs-lookup"><span data-stu-id="0400f-131">If a user will be doing additional operations such as creating logins or creating new databases, they will also need toobe assigned toohello `Loginmanager` and `dbmanager` roles in hello master database.</span></span> <span data-ttu-id="0400f-132">如需有關這些其他角色和驗證 tooa SQL 資料庫的詳細資訊，請參閱[管理資料庫和 Azure SQL Database 中的登入][Managing databases and logins in Azure SQL Database]。</span><span class="sxs-lookup"><span data-stu-id="0400f-132">For more information on these additonal roles and authenticating tooa SQL Database, see [Managing databases and logins in Azure SQL Database][Managing databases and logins in Azure SQL Database].</span></span>  <span data-ttu-id="0400f-133">如需有關 SQL 資料倉儲的 Azure AD 的詳細資訊，請參閱[連接 tooSQL 資料倉儲使用 Azure Active Directory 驗證][Connecting tooSQL Data Warehouse By Using Azure Active Directory Authentication]。</span><span class="sxs-lookup"><span data-stu-id="0400f-133">For more details on Azure AD for SQL Data Warehouse, see [Connecting tooSQL Data Warehouse By Using Azure Active Directory Authentication][Connecting tooSQL Data Warehouse By Using Azure Active Directory Authentication].</span></span>

## <a name="authorization"></a><span data-ttu-id="0400f-134">Authorization</span><span class="sxs-lookup"><span data-stu-id="0400f-134">Authorization</span></span>
<span data-ttu-id="0400f-135">授權是指 toowhat，您可以在 Azure SQL 資料倉儲資料庫，以及這由使用者帳戶的角色成員資格和權限。</span><span class="sxs-lookup"><span data-stu-id="0400f-135">Authorization refers toowhat you can do within an Azure SQL Data Warehouse database, and this is controlled by your user account's role memberships and permissions.</span></span> <span data-ttu-id="0400f-136">最佳做法，您應該授與使用者 hello 最低必要權限。</span><span class="sxs-lookup"><span data-stu-id="0400f-136">As a best practice, you should grant users hello least privileges necessary.</span></span> <span data-ttu-id="0400f-137">Azure SQL 資料倉儲會讓角色與此簡單 toomanage T-SQL 中：</span><span class="sxs-lookup"><span data-stu-id="0400f-137">Azure SQL Data Warehouse makes this easy toomanage with roles in T-SQL:</span></span>

```sql
EXEC sp_addrolemember 'db_datareader', 'ApplicationUser'; -- allows ApplicationUser tooread data
EXEC sp_addrolemember 'db_datawriter', 'ApplicationUser'; -- allows ApplicationUser toowrite data
```

<span data-ttu-id="0400f-138">hello 您所連接的伺服器系統管理員帳戶是具有授權 toodo hello 資料庫內的任何項目 db_owner 的成員。</span><span class="sxs-lookup"><span data-stu-id="0400f-138">hello server admin account you are connecting with is a member of db_owner, which has authority toodo anything within hello database.</span></span> <span data-ttu-id="0400f-139">請儲存此帳戶，以便部署結構描述升級及其他管理作業。</span><span class="sxs-lookup"><span data-stu-id="0400f-139">Save this account for deploying schema upgrades and other management operations.</span></span> <span data-ttu-id="0400f-140">使用具有更多限制的權限 tooconnect 從您的應用程式 toohello 資料庫以 hello hello"ApplicationUser"帳戶應用程式所需的最低權限。</span><span class="sxs-lookup"><span data-stu-id="0400f-140">Use hello "ApplicationUser" account with more limited permissions tooconnect from your application toohello database with hello least privileges needed by your application.</span></span>

<span data-ttu-id="0400f-141">有方法 toofurther 限制使用者可以使用 Azure SQL Database:</span><span class="sxs-lookup"><span data-stu-id="0400f-141">There are ways toofurther limit what a user can do with Azure SQL Database:</span></span>

* <span data-ttu-id="0400f-142">細微[權限][ Permissions]可讓您控制哪些作業，您可以執行個別的資料行、 資料表、 檢視、 程序和其他 hello 資料庫中的物件。</span><span class="sxs-lookup"><span data-stu-id="0400f-142">Granular [Permissions][Permissions] let you control which operations you can do on individual columns, tables, views, procedures, and other objects in hello database.</span></span> <span data-ttu-id="0400f-143">使用細微的權限 toohave hello 最佳控制權，並授與 hello 最低必要權限。</span><span class="sxs-lookup"><span data-stu-id="0400f-143">Use granular permissions toohave hello most control and grant hello minimum permissions necessary.</span></span> <span data-ttu-id="0400f-144">hello 細微權限系統稍微複雜，所以需要某些研究 toouse 有效。</span><span class="sxs-lookup"><span data-stu-id="0400f-144">hello granular permission system is somewhat complicated and will require some study toouse effectively.</span></span>
* <span data-ttu-id="0400f-145">[資料庫角色][ Database roles]以外 db_datareader 和 db_datawriter 可以是使用的 toocreate 功能更強大的應用程式使用者帳戶或較不強大的管理帳戶。</span><span class="sxs-lookup"><span data-stu-id="0400f-145">[Database roles][Database roles] other than db_datareader and db_datawriter can be used toocreate more powerful application user accounts or less powerful management accounts.</span></span> <span data-ttu-id="0400f-146">hello 內建的固定的資料庫角色提供簡單的方式 toogrant 權限，但可能會導致授與超出所需的權限。</span><span class="sxs-lookup"><span data-stu-id="0400f-146">hello built-in fixed database roles provide an easy way toogrant permissions, but can result in granting more permissions than are necessary.</span></span>
* <span data-ttu-id="0400f-147">[預存程序][ Stored procedures]可以是使用的 toolimit 可以 hello 資料庫製作的 hello 動作。</span><span class="sxs-lookup"><span data-stu-id="0400f-147">[Stored procedures][Stored procedures] can be used toolimit hello actions that can be taken on hello database.</span></span>

<span data-ttu-id="0400f-148">從 hello Azure 傳統入口網站管理資料庫和邏輯伺服器，或使用 hello Azure 資源管理員 API 是由您的入口網站的使用者帳戶的角色指派控制。</span><span class="sxs-lookup"><span data-stu-id="0400f-148">Managing databases and logical servers from hello Azure Classic Portal or using hello Azure Resource Manager API is controlled by your portal user account's role assignments.</span></span> <span data-ttu-id="0400f-149">如需有關此主題的詳細資訊，請參閱 [Azure 入口網站中的角色型存取控制][Role-based access control in Azure Portal]。</span><span class="sxs-lookup"><span data-stu-id="0400f-149">For more information on this topic, see [Role-based access control in Azure Portal][Role-based access control in Azure Portal].</span></span>

## <a name="encryption"></a><span data-ttu-id="0400f-150">加密</span><span class="sxs-lookup"><span data-stu-id="0400f-150">Encryption</span></span>
<span data-ttu-id="0400f-151">Azure SQL 資料倉儲透明資料加密 (TDE) 可協助防範惡意活動的 hello 威脅所執行的即時加密與解密的靜止資料。</span><span class="sxs-lookup"><span data-stu-id="0400f-151">Azure SQL Data Warehouse Transparent Data Encryption (TDE) helps protect against hello threat of malicious activity by performing real-time encryption and decryption of your data at rest.</span></span>  <span data-ttu-id="0400f-152">當您加密您的資料庫時，相關聯的備份和交易記錄檔會加密而不需要任何變更 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0400f-152">When you encrypt your database, associated backups and transaction log files are encrypted without requiring any changes tooyour applications.</span></span> <span data-ttu-id="0400f-153">TDE 會使用對稱金鑰的呼叫的 hello 資料庫加密金鑰將整個資料庫的 hello 儲存體。</span><span class="sxs-lookup"><span data-stu-id="0400f-153">TDE encrypts hello storage of an entire database by using a symmetric key called hello database encryption key.</span></span> <span data-ttu-id="0400f-154">SQL Database 中 hello 資料庫加密金鑰受到由內建的伺服器憑證。</span><span class="sxs-lookup"><span data-stu-id="0400f-154">In SQL Database hello database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="0400f-155">hello 內建伺服器憑證是唯一的每個 SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="0400f-155">hello built-in server certificate is unique for each SQL Database server.</span></span> <span data-ttu-id="0400f-156">Microsoft 至少每 90 天會自動替換這些憑證。</span><span class="sxs-lookup"><span data-stu-id="0400f-156">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="0400f-157">SQL 資料倉儲所使用的 hello 加密演算法是 AES 256。</span><span class="sxs-lookup"><span data-stu-id="0400f-157">hello encryption algorithm used by SQL Data Warehouse is AES-256.</span></span> <span data-ttu-id="0400f-158">如需 TDE 的一般描述，請參閱[透明資料加密][Transparent Data Encryption]。</span><span class="sxs-lookup"><span data-stu-id="0400f-158">For a general description of TDE, see [Transparent Data Encryption][Transparent Data Encryption].</span></span>

<span data-ttu-id="0400f-159">您可以使用加密資料庫 hello [Azure 入口網站][ Encryption with Portal]或[T-SQL][Encryption with TSQL]。</span><span class="sxs-lookup"><span data-stu-id="0400f-159">You can encrypt your database using hello [Azure Portal][Encryption with Portal] or [T-SQL][Encryption with TSQL].</span></span>

## <a name="next-steps"></a><span data-ttu-id="0400f-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0400f-160">Next steps</span></span>
<span data-ttu-id="0400f-161">如需詳細資訊和 tooyour SQL 資料倉儲連接不同的通訊協定的範例，請參閱[連接 tooSQL 資料倉儲][Connect tooSQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="0400f-161">For details and examples on connecting tooyour SQL Data Warehouse with different protocols, see [Connect tooSQL Data Warehouse][Connect tooSQL Data Warehouse].</span></span>

<!--Image references-->

<!--Article references-->
[Connect tooSQL Data Warehouse]: ./sql-data-warehouse-connect-overview.md
[Encryption with Portal]: ./sql-data-warehouse-encryption-tde.md
[Encryption with TSQL]: ./sql-data-warehouse-encryption-tde-tsql.md
[Connecting tooSQL Data Warehouse By Using Azure Active Directory Authentication]: ./sql-data-warehouse-authentication.md

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
