---
title: "aaaSecure Azure SQL 資料庫 |Microsoft 文件"
description: "了解技術和功能 toosecure Azure SQL database。"
services: sql-database
documentationcenter: 
author: DRediske
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/28/2017
ms.author: daredis
ms.openlocfilehash: 1450d633d6f65faf1b8a2dc0dc7dfe996fb0719d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="secure-your-azure-sql-database"></a><span data-ttu-id="5981d-103">保護 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="5981d-103">Secure your Azure SQL Database</span></span>

<span data-ttu-id="5981d-104">SQL Database，方法是限制存取 tooyour 資料庫使用的防火牆規則，驗證其身分識別及授權 toodata 透過以角色為基礎的成員資格和權限，以及透過需要使用者 tooprove 的機制保護您的資料資料列層級安全性和動態資料遮罩。</span><span class="sxs-lookup"><span data-stu-id="5981d-104">SQL Database secures your data by limiting access tooyour database using firewall rules, authentication mechanisms requiring users tooprove their identity, and authorization toodata through role-based memberships and permissions, as well as through row-level security and dynamic data masking.</span></span>

<span data-ttu-id="5981d-105">您可以改善 hello 保護您的資料庫在對惡意使用者或未經授權的存取，執行幾個簡單的步驟。</span><span class="sxs-lookup"><span data-stu-id="5981d-105">You can improve hello protection of your database against malicious users or unauthorized access with just a few simple steps.</span></span> <span data-ttu-id="5981d-106">您會在本教學課程中學到：</span><span class="sxs-lookup"><span data-stu-id="5981d-106">In this tutorial you learn to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="5981d-107">設定您伺服器 hello Azure 入口網站中的伺服器層級防火牆規則</span><span class="sxs-lookup"><span data-stu-id="5981d-107">Set up server-level firewall rules for your server in hello Azure portal</span></span>
> * <span data-ttu-id="5981d-108">使用 SSMS 為資料庫設定資料庫層級的防火牆規則</span><span class="sxs-lookup"><span data-stu-id="5981d-108">Set up database-level firewall rules for your database using SSMS</span></span>
> * <span data-ttu-id="5981d-109">連接 tooyour 資料庫使用安全的連接字串</span><span class="sxs-lookup"><span data-stu-id="5981d-109">Connect tooyour database using a secure connection string</span></span>
> * <span data-ttu-id="5981d-110">管理使用者的存取</span><span class="sxs-lookup"><span data-stu-id="5981d-110">Manage user access</span></span>
> * <span data-ttu-id="5981d-111">使用加密來保護您的資料</span><span class="sxs-lookup"><span data-stu-id="5981d-111">Protect your data with encryption</span></span>
> * <span data-ttu-id="5981d-112">啟用 SQL Database 稽核</span><span class="sxs-lookup"><span data-stu-id="5981d-112">Enable SQL Database auditing</span></span>
> * <span data-ttu-id="5981d-113">啟用 SQL Database 威脅偵測</span><span class="sxs-lookup"><span data-stu-id="5981d-113">Enable SQL Database threat detection</span></span>

<span data-ttu-id="5981d-114">如果您沒有 Azure 訂用帳戶，請在開始之前先[建立免費帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="5981d-114">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5981d-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="5981d-115">Prerequisites</span></span>

<span data-ttu-id="5981d-116">toocomplete 此教學課程，請確定您有下列的 hello:</span><span class="sxs-lookup"><span data-stu-id="5981d-116">toocomplete this tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="5981d-117">已安裝的 hello 最新版本的[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS)。</span><span class="sxs-lookup"><span data-stu-id="5981d-117">Installed hello newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span></span> 
- <span data-ttu-id="5981d-118">已安裝 Microsoft Excel</span><span class="sxs-lookup"><span data-stu-id="5981d-118">Installed Microsoft Excel</span></span>
- <span data-ttu-id="5981d-119">建立 Azure SQL server 和資料庫-請參閱[hello Azure 入口網站中建立 Azure SQL database](sql-database-get-started-portal.md)，[建立單一的 Azure SQL database，使用 Azure CLI hello](sql-database-get-started-cli.md)，和[建立單一的 Azure SQL資料庫使用 PowerShell](sql-database-get-started-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="5981d-119">Created an Azure SQL server and database - See [Create an Azure SQL database in hello Azure portal](sql-database-get-started-portal.md), [Create a single Azure SQL database using hello Azure CLI](sql-database-get-started-cli.md), and [Create a single Azure SQL database using PowerShell](sql-database-get-started-powershell.md).</span></span> 

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="5981d-120">登入 toohello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="5981d-120">Log in toohello Azure portal</span></span>

<span data-ttu-id="5981d-121">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="5981d-121">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="5981d-122">在 hello Azure 入口網站中建立伺服器層級防火牆規則</span><span class="sxs-lookup"><span data-stu-id="5981d-122">Create a server-level firewall rule in hello Azure portal</span></span>

<span data-ttu-id="5981d-123">Azure 的防火牆會保護 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="5981d-123">SQL databases are protected by a firewall in Azure.</span></span> <span data-ttu-id="5981d-124">根據預設，所有連線 toohello 伺服器和 hello 資料庫 hello 伺服器內將會都拒絕從其他 Azure 服務的連接除外。</span><span class="sxs-lookup"><span data-stu-id="5981d-124">By default, all connections toohello server and hello databases inside hello server are rejected except for connections from other Azure services.</span></span> <span data-ttu-id="5981d-125">如需詳細資訊，請參閱 [Azure SQL Database 伺服器層級和資料庫層級防火牆規則](sql-database-firewall-configure.md)</span><span class="sxs-lookup"><span data-stu-id="5981d-125">For more information, see [Azure SQL Database server-level and database-level firewall rules](sql-database-firewall-configure.md).</span></span>

<span data-ttu-id="5981d-126">tooset '允許存取 tooAzure services' tooOFF hello 最安全的設定。</span><span class="sxs-lookup"><span data-stu-id="5981d-126">hello most secure configuration is tooset 'Allow access tooAzure services' tooOFF.</span></span> <span data-ttu-id="5981d-127">如果您需要 tooconnect toohello 資料庫從 Azure VM 或雲端服務，您應該建立[保留 IP](../virtual-network/virtual-networks-reserved-public-ip.md)和僅允許 hello 保留 IP 位址存取透過 hello 防火牆。</span><span class="sxs-lookup"><span data-stu-id="5981d-127">If you need tooconnect toohello database from an Azure VM or cloud service, you should create a [Reserved IP](../virtual-network/virtual-networks-reserved-public-ip.md) and allow only hello reserved IP address access through hello firewall.</span></span> 

<span data-ttu-id="5981d-128">請遵循這些步驟 toocreate [SQL Database 伺服器層級防火牆規則](sql-database-firewall-configure.md)伺服器 tooallow 連線從特定的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5981d-128">Follow these steps toocreate a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your server tooallow connections from a specific IP address.</span></span> 

> [!NOTE]
> <span data-ttu-id="5981d-129">如果您使用其中一個 hello 先前的教學課程或快速入門和都是在 Azure 中建立範例資料庫以 hello 在電腦上執行此教學課程中相同 IP 位址，就在您逐步進行這些教學課程作業時，您可以略過此步驟將有已建立伺服器層級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="5981d-129">If you have created a sample database in Azure using one of hello previous tutorials or quickstarts and are performing this tutorial on a computer with hello same IP address that it had when you walked through those tutorials, you can skip this step as you will have already created a server-level firewall rule.</span></span>
>

1. <span data-ttu-id="5981d-130">按一下**SQL 資料庫**hello 左側功能表，然後按一下 hello 資料庫從您想要 tooconfigure hello 上防火牆規則的 hello **SQL 資料庫**頁面。</span><span class="sxs-lookup"><span data-stu-id="5981d-130">Click **SQL databases** from hello left-hand menu and click hello database you would like tooconfigure hello firewall rule for on hello **SQL databases** page.</span></span> <span data-ttu-id="5981d-131">hello 概觀 頁面的資料庫會開啟，顯示您 hello 完全符合規定的伺服器名稱 (例如**mynewserver 20170313.database.windows.net**)，並提供進一步組態的選項。</span><span class="sxs-lookup"><span data-stu-id="5981d-131">hello overview page for your database opens, showing you hello fully qualified server name (such as **mynewserver-20170313.database.windows.net**) and provides options for further configuration.</span></span>

      ![伺服器防火牆規則](./media/sql-database-security-tutorial/server-firewall-rule.png) 

2. <span data-ttu-id="5981d-133">按一下**設定伺服器防火牆**hello 工具列 hello 如上圖所示。</span><span class="sxs-lookup"><span data-stu-id="5981d-133">Click **Set server firewall** on hello toolbar as shown in hello previous image.</span></span> <span data-ttu-id="5981d-134">hello**防火牆設定**hello SQL 資料庫伺服器 頁面隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="5981d-134">hello **Firewall settings** page for hello SQL Database server opens.</span></span> 

3. <span data-ttu-id="5981d-135">按一下**新增用戶端 IP**在 hello 工具列 tooadd hello 公用 IP 位址的 hello 與電腦連接的 toohello 入口網站，或手動輸入 hello 防火牆規則，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="5981d-135">Click **Add client IP** on hello toolbar tooadd hello public IP address of hello computer connected toohello portal with or enter hello firewall rule manually and then click **Save**.</span></span>

      ![設定伺服器防火牆規則](./media/sql-database-security-tutorial/server-firewall-rule-set.png) 

4. <span data-ttu-id="5981d-137">按一下**確定**然後按一下hello **X** tooclose hello**防火牆設定**頁面。</span><span class="sxs-lookup"><span data-stu-id="5981d-137">Click **OK** and then click hello **X** tooclose hello **Firewall settings** page.</span></span>

<span data-ttu-id="5981d-138">您現在可以連接 tooany hello 伺服器資料庫，以指定的 hello IP 位址或 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="5981d-138">You can now connect tooany database in hello server with hello specified IP address or IP address range.</span></span>

> [!NOTE]
> <span data-ttu-id="5981d-139">SQL Database 會透過連接埠 1433 通訊。</span><span class="sxs-lookup"><span data-stu-id="5981d-139">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="5981d-140">如果您嘗試 tooconnect 從公司網路內，由您的網路防火牆可能不允許透過通訊埠 1433年的輸出流量。</span><span class="sxs-lookup"><span data-stu-id="5981d-140">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="5981d-141">如果是的話，就能 tooconnect tooyour Azure SQL Database 伺服器除非您的 IT 部門會開啟通訊埠 1433年。</span><span class="sxs-lookup"><span data-stu-id="5981d-141">If so, you will not be able tooconnect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-level-firewall-rule-using-ssms"></a><span data-ttu-id="5981d-142">使用 SSMS 建立資料庫層級防火牆規則</span><span class="sxs-lookup"><span data-stu-id="5981d-142">Create a database-level firewall rule using SSMS</span></span>

<span data-ttu-id="5981d-143">資料庫層級防火牆規則可讓您將不同的防火牆設定 toocreate hello 相同邏輯伺服器和 toocreate 防火牆規則，具有可攜性-這表示它們遵循下列 hello 資料庫在期間內的不同資料庫的[容錯移轉](sql-database-geo-replication-overview.md)而不是儲存在 hello SQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="5981d-143">Database-level firewall rules enable you toocreate different firewall settings for different databases within hello same logical server and toocreate firewall rules that are portable - meaning that they follow hello database during a [failover](sql-database-geo-replication-overview.md) rather than being stored on hello SQL server.</span></span> <span data-ttu-id="5981d-144">資料庫層級防火牆規則只能使用 Transact SQL 陳述式設定，而且只在設定第一個伺服器層級防火牆規則 hello 之後。</span><span class="sxs-lookup"><span data-stu-id="5981d-144">Database-level firewall rules can only be configured by using Transact-SQL statements and only after you have configured hello first server-level firewall rule.</span></span> <span data-ttu-id="5981d-145">如需詳細資訊，請參閱 [Azure SQL Database 伺服器層級和資料庫層級防火牆規則](sql-database-firewall-configure.md)</span><span class="sxs-lookup"><span data-stu-id="5981d-145">For more information, see [Azure SQL Database server-level and database-level firewall rules](sql-database-firewall-configure.md).</span></span>

<span data-ttu-id="5981d-146">遵循這些步驟 toocreate 特定資料庫的防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="5981d-146">Follows these steps toocreate a database-specific firewall rule.</span></span>

1. <span data-ttu-id="5981d-147">連接 tooyour 資料庫，例如使用[SQL Server Management Studio](./sql-database-connect-query-ssms.md)。</span><span class="sxs-lookup"><span data-stu-id="5981d-147">Connect tooyour database, for example using [SQL Server Management Studio](./sql-database-connect-query-ssms.md).</span></span>

2. <span data-ttu-id="5981d-148">在 [物件總管] 中，以滑鼠右鍵按一下您想要的防火牆規則，以及按一下的 tooadd hello 資料庫**新查詢**。</span><span class="sxs-lookup"><span data-stu-id="5981d-148">In Object Explorer, right-click on hello database you want tooadd a firewall rule for and click **New Query**.</span></span> <span data-ttu-id="5981d-149">空白查詢視窗，也就是開啟連接的 tooyour 資料庫。</span><span class="sxs-lookup"><span data-stu-id="5981d-149">A blank query window opens that is connected tooyour database.</span></span>

3. <span data-ttu-id="5981d-150">在 hello 查詢視窗中，修改 hello IP 位址 tooyour 公用 IP 位址，然後執行下列查詢的 hello:</span><span class="sxs-lookup"><span data-stu-id="5981d-150">In hello query window, modify hello IP address tooyour public IP address and then execute hello following query:</span></span>

    ```sql
    EXECUTE sp_set_database_firewall_rule N'Example DB Rule','0.0.0.4','0.0.0.4';
    ```

4. <span data-ttu-id="5981d-151">在 [hello] 工具列上按一下**Execute** toocreate hello 防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="5981d-151">On hello toolbar, click **Execute** toocreate hello firewall rule.</span></span>

## <a name="view-how-tooconnect-an-application-tooyour-database-using-a-secure-connection-string"></a><span data-ttu-id="5981d-152">檢視應用程式 tooyour tooconnect 資料庫使用安全的連接字串</span><span class="sxs-lookup"><span data-stu-id="5981d-152">View how tooconnect an application tooyour database using a secure connection string</span></span>

<span data-ttu-id="5981d-153">tooensure 用戶端應用程式與 SQL Database 之間的安全且加密連接，hello 連接字串具有 toobe 設定為：</span><span class="sxs-lookup"><span data-stu-id="5981d-153">tooensure a secure, encrypted connection between a client application and SQL Database, hello connection string has toobe configured to:</span></span>

- <span data-ttu-id="5981d-154">要求加密的連線，並且</span><span class="sxs-lookup"><span data-stu-id="5981d-154">Request an encrypted connection, and</span></span>
- <span data-ttu-id="5981d-155">toonot 信任 hello 伺服器憑證。</span><span class="sxs-lookup"><span data-stu-id="5981d-155">toonot trust hello server certificate.</span></span> 

<span data-ttu-id="5981d-156">這會建立使用傳輸層安全性 (TLS) 的連接，並減少 hello 攻擊的風險，攔截層。</span><span class="sxs-lookup"><span data-stu-id="5981d-156">This establishes a connection using Transport Layer Security (TLS) and reduces hello risk of man-in-the-middle attacks.</span></span> <span data-ttu-id="5981d-157">您可以取得正確設定的連接字串 SQL database 支援的用戶端驅動程式從 hello Azure 入口網站如 ado.net 這個螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="5981d-157">You can obtain correctly configured connection strings for your SQL Database for supported client drivers from hello Azure portal as shown for ADO.net in this screenshot.</span></span>

1. <span data-ttu-id="5981d-158">選取**SQL 資料庫**從 hello 左側功能表中，按一下您的資料庫上 hello **SQL 資料庫**頁面。</span><span class="sxs-lookup"><span data-stu-id="5981d-158">Select **SQL databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span>

2. <span data-ttu-id="5981d-159">在 hello**概觀**為您的資料庫頁面上，按一下**顯示資料庫的連接字串**。</span><span class="sxs-lookup"><span data-stu-id="5981d-159">On hello **Overview** page for your database, click **Show database connection strings**.</span></span>

3. <span data-ttu-id="5981d-160">完成檢閱 hello **ADO.NET**連接字串。</span><span class="sxs-lookup"><span data-stu-id="5981d-160">Review hello complete **ADO.NET** connection string.</span></span>

    ![ADO.NET 連接字串](./media/sql-database-security-tutorial/adonet-connection-string.png)

## <a name="creating-database-users"></a><span data-ttu-id="5981d-162">建立資料庫使用者</span><span class="sxs-lookup"><span data-stu-id="5981d-162">Creating database users</span></span>

<span data-ttu-id="5981d-163">建立任何使用者之前，您必須先選取一個或兩個 Azure SQL Database 支援的驗證類型：</span><span class="sxs-lookup"><span data-stu-id="5981d-163">Before creating any users, you must first choose from one of two authentication types supported by Azure SQL Database:</span></span> 

<span data-ttu-id="5981d-164">**SQL 驗證**、 使用使用者名稱和密碼登入和使用者的有效只在 hello 邏輯伺服器內的特定資料庫的內容。</span><span class="sxs-lookup"><span data-stu-id="5981d-164">**SQL Authentication**, which uses username and password for logins and users that are valid only in hello context of a specific database within a logical server.</span></span> 

<span data-ttu-id="5981d-165">**Azure Active Directory 驗證**，使用由 Azure Active Directory 管理的身分識別。</span><span class="sxs-lookup"><span data-stu-id="5981d-165">**Azure Active Directory Authentication**, which uses identities managed by Azure Active Directory.</span></span> 

<span data-ttu-id="5981d-166">如果您想 toouse [Azure Active Directory](./sql-database-aad-authentication.md) tooauthenticate 針對 SQL Database，填入的 Azure Active Directory 必須存在後才能繼續。</span><span class="sxs-lookup"><span data-stu-id="5981d-166">If you want toouse [Azure Active Directory](./sql-database-aad-authentication.md) tooauthenticate against SQL Database, a populated Azure Active Directory must exist before you can proceed.</span></span>

<span data-ttu-id="5981d-167">請遵循這些步驟 toocreate 使用 SQL 驗證使用者：</span><span class="sxs-lookup"><span data-stu-id="5981d-167">Follow these steps toocreate a user using SQL Authentication:</span></span>

1. <span data-ttu-id="5981d-168">連接 tooyour 資料庫，例如使用[SQL Server Management Studio](./sql-database-connect-query-ssms.md)使用您的伺服器系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="5981d-168">Connect tooyour database, for example using [SQL Server Management Studio](./sql-database-connect-query-ssms.md) using your server admin credentials.</span></span>

2. <span data-ttu-id="5981d-169">在物件總管] 中，以滑鼠右鍵按一下您希望 tooadd 新的使用者上，按一下 [hello 資料庫**新查詢**。</span><span class="sxs-lookup"><span data-stu-id="5981d-169">In Object Explorer, right-click on hello database you want tooadd a new user on and click **New Query**.</span></span> <span data-ttu-id="5981d-170">空白查詢視窗也就是開啟連接的 toohello 選取的資料庫。</span><span class="sxs-lookup"><span data-stu-id="5981d-170">A blank query window opens that is connected toohello selected database.</span></span>

3. <span data-ttu-id="5981d-171">在 hello 查詢視窗中，輸入下列查詢的 hello:</span><span class="sxs-lookup"><span data-stu-id="5981d-171">In hello query window, enter hello following query:</span></span>

    ```sql
    CREATE USER ApplicationUser WITH PASSWORD = 'YourStrongPassword1';
    ```

4. <span data-ttu-id="5981d-172">在 [hello] 工具列上按一下**Execute** toocreate hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="5981d-172">On hello toolbar, click **Execute** toocreate hello user.</span></span>

5. <span data-ttu-id="5981d-173">根據預設，hello 使用者可以連接 toohello 資料庫，但沒有權限 tooread 或寫入資料。</span><span class="sxs-lookup"><span data-stu-id="5981d-173">By default, hello user can connect toohello database, but has no permissions tooread or write data.</span></span> <span data-ttu-id="5981d-174">toogrant 這些權限 toohello 新建立的使用者，請執行下列兩個新的查詢視窗中命令的 hello</span><span class="sxs-lookup"><span data-stu-id="5981d-174">toogrant these permissions toohello newly created user, execute hello following two commands in a new query window</span></span>

    ```sql
    ALTER ROLE db_datareader ADD MEMBER ApplicationUser;
    ALTER ROLE db_datawriter ADD MEMBER ApplicationUser;
    ```

<span data-ttu-id="5981d-175">它是最佳的作法 toocreate 在 hello 資料庫層級 tooconnect tooyour 這些非系統管理員帳戶資料庫，除非您需要 tooexecute 系統管理員工作，例如建立新的使用者。</span><span class="sxs-lookup"><span data-stu-id="5981d-175">It is best practice toocreate these non-administrator accounts at hello database level tooconnect tooyour database unless you need tooexecute administrator tasks like creating new users.</span></span> <span data-ttu-id="5981d-176">請檢閱 hello [Azure Active Directory 教學課程](./sql-database-aad-authentication-configure.md)如何使用 Azure Active Directory tooauthenticate。</span><span class="sxs-lookup"><span data-stu-id="5981d-176">Please review hello [Azure Active Directory tutorial](./sql-database-aad-authentication-configure.md) on how tooauthenticate using Azure Active Directory.</span></span>


## <a name="protect-your-data-with-encryption"></a><span data-ttu-id="5981d-177">使用加密來保護您的資料</span><span class="sxs-lookup"><span data-stu-id="5981d-177">Protect your data with encryption</span></span>

<span data-ttu-id="5981d-178">Azure SQL Database 透明資料加密 (TDE) 會自動加密而不需要任何變更 toohello 應用程式存取 hello 加密的資料庫的靜止資料。</span><span class="sxs-lookup"><span data-stu-id="5981d-178">Azure SQL Database transparent data encryption (TDE) automatically encrypts your data at rest, without requiring any changes toohello application accessing hello encrypted database.</span></span> <span data-ttu-id="5981d-179">如果是新建立的資料庫，TDE 預設為開啟。</span><span class="sxs-lookup"><span data-stu-id="5981d-179">For newly created databases, TDE is on by default.</span></span> <span data-ttu-id="5981d-180">您的資料庫或已開啟 TDE 的 tooverify tooenable TDE 會執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5981d-180">tooenable TDE for your database or tooverify that TDE is on, follow these steps:</span></span>

1. <span data-ttu-id="5981d-181">選取**SQL 資料庫**從 hello 左側功能表中，按一下您的資料庫上 hello **SQL 資料庫**頁面。</span><span class="sxs-lookup"><span data-stu-id="5981d-181">Select **SQL databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 

2. <span data-ttu-id="5981d-182">按一下**透明資料加密**TDE tooopen hello 組態頁面。</span><span class="sxs-lookup"><span data-stu-id="5981d-182">Click on **Transparent data encryption** tooopen hello configuration page for TDE.</span></span>

    ![透明資料加密](./media/sql-database-security-tutorial/transparent-data-encryption-enabled.png)

3. <span data-ttu-id="5981d-184">如有必要，設定**資料加密**tooON 按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="5981d-184">If necessary, set **Data encryption** tooON and click **Save**.</span></span>

<span data-ttu-id="5981d-185">在 hello 背景啟動 hello 加密程序。</span><span class="sxs-lookup"><span data-stu-id="5981d-185">hello encryption process starts in hello background.</span></span> <span data-ttu-id="5981d-186">您可以監視連線 tooSQL 資料庫使用的 hello 進度[SQL Server Management Studio](./sql-database-connect-query-ssms.md)藉由查詢 sys.dm_database_encryption_keys 資料行 hello hello`sys.dm_database_encryption_keys`檢視。</span><span class="sxs-lookup"><span data-stu-id="5981d-186">You can monitor hello progress by connecting tooSQL Database using [SQL Server Management Studio](./sql-database-connect-query-ssms.md) by querying hello encryption_state column of hello `sys.dm_database_encryption_keys` view.</span></span>

## <a name="enable-sql-database-auditing-if-necessary"></a><span data-ttu-id="5981d-187">啟用 SQL Database 稽核 (如有必要)</span><span class="sxs-lookup"><span data-stu-id="5981d-187">Enable SQL Database auditing, if necessary</span></span>

<span data-ttu-id="5981d-188">Azure SQL Database 稽核會追蹤資料庫事件，並將它們 tooan 稽核記錄您 Azure 儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="5981d-188">Azure SQL Database Auditing tracks database events and writes them tooan audit log in your Azure Storage account.</span></span> <span data-ttu-id="5981d-189">稽核可協助您保持法規合規性、了解資料庫活動，以及深入了解可能指出潛在安全違規的不一致和異常。</span><span class="sxs-lookup"><span data-stu-id="5981d-189">Auditing can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate potential security violations.</span></span> <span data-ttu-id="5981d-190">請遵循這些步驟 toocreate SQL 資料庫的預設稽核原則：</span><span class="sxs-lookup"><span data-stu-id="5981d-190">Follow these steps toocreate a default auditing policy for your SQL database:</span></span>

1. <span data-ttu-id="5981d-191">選取**SQL 資料庫**從 hello 左側功能表中，按一下您的資料庫上 hello **SQL 資料庫**頁面。</span><span class="sxs-lookup"><span data-stu-id="5981d-191">Select **SQL databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 

2. <span data-ttu-id="5981d-192">在 hello 設定刀鋒視窗中，選取 **稽核與威脅偵測**。</span><span class="sxs-lookup"><span data-stu-id="5981d-192">In hello Settings blade, select **Auditing & Threat Detection**.</span></span> <span data-ttu-id="5981d-193">請注意，伺服器層級稽核已停用，而且有**檢視伺服器設定**可讓您 tooview 或修改 hello 伺服器稽核設定從這個內容的連結。</span><span class="sxs-lookup"><span data-stu-id="5981d-193">Notice that sever-level auditing is diabled and that there is a **View server settings** link that allows you tooview or modify hello server auditing settings from this context.</span></span>

    ![稽核刀鋒視窗](./media/sql-database-security-tutorial/auditing-get-started-settings.png)

3. <span data-ttu-id="5981d-195">如果您偏好 tooenable 稽核類型 （或位置嗎？） 不同於 hello 所指定的伺服器層級 hello，開啟**ON**稽核，並選擇 hello **Blob**稽核類型。</span><span class="sxs-lookup"><span data-stu-id="5981d-195">If you prefer tooenable an Audit type (or location?) different from hello one specified at hello server level, turn **ON** Auditing, and choose hello **Blob** Auditing Type.</span></span> <span data-ttu-id="5981d-196">如果伺服器 Blob 稽核已啟用，就會並存 hello 伺服器 Blob 稽核存在 hello 設定資料庫稽核。</span><span class="sxs-lookup"><span data-stu-id="5981d-196">If server Blob auditing is enabled, hello database configured audit will exist side by side with hello server Blob audit.</span></span>

    ![開啟稽核](./media/sql-database-security-tutorial/auditing-get-started-turn-on.png)

4. <span data-ttu-id="5981d-198">選取**儲存詳細資料**tooopen hello 稽核記錄檔儲存體 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="5981d-198">Select **Storage Details** tooopen hello Audit Logs Storage Blade.</span></span> <span data-ttu-id="5981d-199">其中會儲存記錄檔，選取 hello Azure 儲存體帳戶和 hello 保留期限，將會刪除舊的記錄檔之後的 hello，然後按一下**確定**hello 底部。</span><span class="sxs-lookup"><span data-stu-id="5981d-199">Select hello Azure storage account where logs will be saved, and hello retention period, after which hello old logs will be deleted, then click **OK** at hello bottom.</span></span> 

   > [!TIP]
   > <span data-ttu-id="5981d-200">使用 hello 相同儲存體帳戶的所有稽核的資料庫 tooget hello 充分利用 hello 稽核報告範本。</span><span class="sxs-lookup"><span data-stu-id="5981d-200">Use hello same storage account for all audited databases tooget hello most out of hello auditing reports templates.</span></span>
   > 

5. <span data-ttu-id="5981d-201">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="5981d-201">Click **Save**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5981d-202">如果您想 toocustomize hello 稽核事件，您可以透過 PowerShell 或 REST API-請參閱 hello[自動化 (PowerShell / REST API)](sql-database-auditing.md#subheading-7) > 一節以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="5981d-202">If you want toocustomize hello audited events, you can do this via PowerShell or REST API - see hello [Automation (PowerShell / REST API)](sql-database-auditing.md#subheading-7) section for more details.</span></span>
>

## <a name="enable-sql-database-threat-detection"></a><span data-ttu-id="5981d-203">啟用 SQL Database 威脅偵測</span><span class="sxs-lookup"><span data-stu-id="5981d-203">Enable SQL Database threat detection</span></span>

<span data-ttu-id="5981d-204">威脅偵測提供新的圖層的安全性，這可讓客戶 toodetect 及回應 toopotential 威脅，在發生異常的活動提供安全性警示。</span><span class="sxs-lookup"><span data-stu-id="5981d-204">Threat Detection provides a new layer of security, which enables customers toodetect and respond toopotential threats as they occur by providing security alerts on anomalous activities.</span></span> <span data-ttu-id="5981d-205">使用者可以瀏覽 hello 如果會導致從嘗試 tooaccess，漏洞，或利用 hello 資料庫中的資料，請使用 SQL Database 稽核 toodetermine 可疑的事件。</span><span class="sxs-lookup"><span data-stu-id="5981d-205">Users can explore hello suspicious events using SQL Database Auditing toodetermine if they result from an attempt tooaccess, breach or exploit data in hello database.</span></span> <span data-ttu-id="5981d-206">威脅偵測會使簡單 tooaddress 潛在威脅 toohello 資料庫沒有 hello 需要 toobe 安全性專家或管理進階監視系統的安全性。</span><span class="sxs-lookup"><span data-stu-id="5981d-206">Threat Detection makes it simple tooaddress potential threats toohello database without hello need toobe a security expert or manage advanced security monitoring systems.</span></span>
<span data-ttu-id="5981d-207">威脅偵測會偵測異常資料庫活動，指出潛在的 SQL 插入式攻擊。</span><span class="sxs-lookup"><span data-stu-id="5981d-207">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="5981d-208">SQL 資料隱碼是 hello 常見的 Web 應用程式的安全性問題在 hello 網際網路，使用的 tooattack 資料導向應用程式。</span><span class="sxs-lookup"><span data-stu-id="5981d-208">SQL injection is one of hello common Web application security issues on hello Internet, used tooattack data-driven applications.</span></span> <span data-ttu-id="5981d-209">攻擊者利用的應用程式的弱點可能會 tooinject 惡意的 SQL 陳述式到違反或修改 hello 資料庫中的資料的應用程式項目欄位。</span><span class="sxs-lookup"><span data-stu-id="5981d-209">Attackers take advantage of application vulnerabilities tooinject malicious SQL statements into application entry fields, for breaching or modifying data in hello database.</span></span>

1. <span data-ttu-id="5981d-210">瀏覽 toohello 組態刀鋒視窗中的 hello 想 toomonitor 的 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="5981d-210">Navigate toohello configuration blade of hello SQL database you want toomonitor.</span></span> <span data-ttu-id="5981d-211">在 hello 設定刀鋒視窗中，選取 **稽核與威脅偵測**。</span><span class="sxs-lookup"><span data-stu-id="5981d-211">In hello Settings blade, select **Auditing & Threat Detection**.</span></span>

    ![瀏覽窗格](./media/sql-database-security-tutorial/auditing-get-started-settings.png)
2. <span data-ttu-id="5981d-213">在 hello**稽核與威脅偵測**組態刀鋒視窗中開啟**ON**稽核，這會顯示 hello 威脅偵測設定。</span><span class="sxs-lookup"><span data-stu-id="5981d-213">In hello **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display hello threat detection settings.</span></span>

3. <span data-ttu-id="5981d-214">[開啟] 威脅偵測。</span><span class="sxs-lookup"><span data-stu-id="5981d-214">Turn **ON** threat detection.</span></span>

4. <span data-ttu-id="5981d-215">設定將會收到偵測的異常資料庫活動時的安全性警示的電子郵件的 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="5981d-215">Configure hello list of emails that will receive security alerts upon detection of anomalous database activities.</span></span>

5. <span data-ttu-id="5981d-216">按一下**儲存**在 hello**稽核與威脅偵測**刀鋒視窗 toosave hello 新的或更新稽核和威脅偵測原則。</span><span class="sxs-lookup"><span data-stu-id="5981d-216">Click **Save** in hello **Auditing & Threat detection** blade toosave hello new or updated auditing and threat detection policy.</span></span>

    ![瀏覽窗格](./media/sql-database-security-tutorial/td-turn-on-threat-detection.png)

    <span data-ttu-id="5981d-218">如果偵測到異常的資料庫活動，您會在一偵測到異常的資料庫活動時，就收到電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="5981d-218">If anomalous database activities are detected, you will receive an email notification upon detection of anomalous database activities.</span></span> <span data-ttu-id="5981d-219">hello 電子郵件會提供資訊，包括 hello 性質 hello 異常活動、 資料庫名稱、 伺服器名稱和 hello 事件時間的 hello 可疑安全性事件。</span><span class="sxs-lookup"><span data-stu-id="5981d-219">hello email will provide information on hello suspicious security event including hello nature of hello anomalous activities, database name, server name and hello event time.</span></span> <span data-ttu-id="5981d-220">此外，它會提供資訊的可能原因和建議動作 tooinvestigate 並減輕潛在威脅 toohello 資料庫 hello。</span><span class="sxs-lookup"><span data-stu-id="5981d-220">In addition, it will provide information on possible causes and recommended actions tooinvestigate and mitigate hello potential threat toohello database.</span></span> <span data-ttu-id="5981d-221">您應透過何種 toodo 您 hello 下一個步驟查核行程收到這類電子郵件：</span><span class="sxs-lookup"><span data-stu-id="5981d-221">hello next steps walk you through what toodo should you receive such an email:</span></span>

    ![威脅偵測電子郵件](./media/sql-database-threat-detection-get-started/4_td_email.png)

6. <span data-ttu-id="5981d-223">在 hello 電子郵件，按一下 hello **Azure SQL 稽核記錄檔**連結，也會啟動 hello Azure 入口網站，並顯示 hello 相關稽核的記錄周圍 hello hello 可疑事件時間。</span><span class="sxs-lookup"><span data-stu-id="5981d-223">In hello email, click on hello **Azure SQL Auditing Log** link, which will launch hello Azure portal and show hello relevant auditing records around hello time of hello suspicious event.</span></span>

    ![稽核記錄](./media/sql-database-threat-detection-get-started/5_td_audit_records.png)

7. <span data-ttu-id="5981d-225">按一下 hello 稽核記錄 tooview hello 可疑的資料庫活動，例如 SQL 陳述式的詳細失敗的原因與用戶端 IP。</span><span class="sxs-lookup"><span data-stu-id="5981d-225">Click on hello audit records tooview more details on hello suspicious database activities such as SQL statement, failure reason and client IP.</span></span>

    ![記錄詳細資料](./media/sql-database-security-tutorial/6_td_audit_record_details.png)

8. <span data-ttu-id="5981d-227">在 hello 稽核記錄刀鋒視窗中，按一下 **在 Excel 中開啟**tooopen 預先設定的 excel 範本 tooimport 和 hello 周圍 hello 事件時間的 hello 可疑的稽核記錄檔執行深入分析。</span><span class="sxs-lookup"><span data-stu-id="5981d-227">In hello Auditing Records blade, click  **Open in Excel** tooopen a pre-configured excel template tooimport and run deeper analysis of hello audit log around hello time of hello suspicious event.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5981d-228">在 Excel 2010 或更新版本的 Power Query 和 hello**快速合併**是必要設定。</span><span class="sxs-lookup"><span data-stu-id="5981d-228">In Excel 2010 or later, Power Query and hello **Fast Combine** setting is required.</span></span>

    ![在 Excel 中開啟記錄](./media/sql-database-threat-detection-get-started/7_td_audit_records_open_excel.png)

9. <span data-ttu-id="5981d-230">tooconfigure hello**快速合併**設定位在 hello **POWER QUERY**功能區索引標籤上，選取**選項**toodisplay hello 選項 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="5981d-230">tooconfigure hello **Fast Combine** setting - In hello **POWER QUERY** ribbon tab, select **Options** toodisplay hello Options dialog.</span></span> <span data-ttu-id="5981d-231">選取 hello 隱私權區段，然後選擇 hello 第二個選項-[忽略 hello 隱私權等級並可能會改善效能]:</span><span class="sxs-lookup"><span data-stu-id="5981d-231">Select hello Privacy section and choose hello second option - 'Ignore hello Privacy Levels and potentially improve performance':</span></span>

    ![Excel 快速合併](./media/sql-database-threat-detection-get-started/8_td_excel_fast_combine.png)

10. <span data-ttu-id="5981d-233">tooload SQL 稽核記錄檔，請務必 hello 設定 索引標籤中的 hello 參數正確設定，然後選取 hello 「 資料 」 功能區按一下 hello 全部重新整理 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5981d-233">tooload SQL audit logs, ensure that hello parameters in hello settings tab are set correctly and then select hello 'Data' ribbon and click hello 'Refresh All' button.</span></span>

    ![Excel 參數](./media/sql-database-threat-detection-get-started/9_td_excel_parameters.png)

11. <span data-ttu-id="5981d-235">hello 結果會出現在 hello **SQL 稽核記錄檔**可讓您的 hello 異常活動偵測到，並減少應用程式中的 hello 安全性事件 hello 影響 toorun 深入分析的工作表。</span><span class="sxs-lookup"><span data-stu-id="5981d-235">hello results appear in hello **SQL Audit Logs** sheet which enables you toorun deeper analysis of hello anomalous activities that were detected, and mitigate hello impact of hello security event in your application.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5981d-236">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5981d-236">Next steps</span></span>
<span data-ttu-id="5981d-237">您可以改善 hello 保護您的資料庫在對惡意使用者或未經授權的存取，執行幾個簡單的步驟。</span><span class="sxs-lookup"><span data-stu-id="5981d-237">You can improve hello protection of your database against malicious users or unauthorized access with just a few simple steps.</span></span> <span data-ttu-id="5981d-238">您會在本教學課程中學到：</span><span class="sxs-lookup"><span data-stu-id="5981d-238">In this tutorial you learn to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="5981d-239">設定伺服器和/或資料庫的防火牆規則</span><span class="sxs-lookup"><span data-stu-id="5981d-239">Set up firewall rules for your sever and or database</span></span>
> * <span data-ttu-id="5981d-240">連接 tooyour 資料庫使用安全的連接字串</span><span class="sxs-lookup"><span data-stu-id="5981d-240">Connect tooyour database using a secure connection string</span></span>
> * <span data-ttu-id="5981d-241">管理使用者的存取</span><span class="sxs-lookup"><span data-stu-id="5981d-241">Manage user access</span></span>
> * <span data-ttu-id="5981d-242">使用加密來保護您的資料</span><span class="sxs-lookup"><span data-stu-id="5981d-242">Protect your data with encryption</span></span>
> * <span data-ttu-id="5981d-243">啟用 SQL Database 稽核</span><span class="sxs-lookup"><span data-stu-id="5981d-243">Enable SQL Database auditing</span></span>
> * <span data-ttu-id="5981d-244">啟用 SQL Database 威脅偵測</span><span class="sxs-lookup"><span data-stu-id="5981d-244">Enable SQL Database threat detection</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="5981d-245">改善 SQL Database 效能</span><span class="sxs-lookup"><span data-stu-id="5981d-245">Improve SQL Database performance</span></span>](sql-database-performance-tutorial.md)

