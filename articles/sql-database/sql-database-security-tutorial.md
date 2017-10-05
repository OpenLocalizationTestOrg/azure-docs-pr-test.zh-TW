---
title: "保護 Azure SQL Database | Microsoft Docs"
description: "深入了解保護 Azure SQL Database 的技術和功能。"
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
ms.openlocfilehash: 4bc09ad13ed0c9dc9257e9c75ec6f9ff3d689a0b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="secure-your-azure-sql-database"></a><span data-ttu-id="cf528-103">保護 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="cf528-103">Secure your Azure SQL Database</span></span>

<span data-ttu-id="cf528-104">SQL Database 使用防火牆規則、要求使用者證明其身分的驗證機制，以及透過角色型成員資格與權限和透過資料列層級安全性與動態資料遮罩的資料授權來限制資料庫的存取，進而保護您的資料。</span><span class="sxs-lookup"><span data-stu-id="cf528-104">SQL Database secures your data by limiting access to your database using firewall rules, authentication mechanisms requiring users to prove their identity, and authorization to data through role-based memberships and permissions, as well as through row-level security and dynamic data masking.</span></span>

<span data-ttu-id="cf528-105">只需要幾個簡單步驟，您就可以讓資料庫預防惡意使用者或未經授權的存取。</span><span class="sxs-lookup"><span data-stu-id="cf528-105">You can improve the protection of your database against malicious users or unauthorized access with just a few simple steps.</span></span> <span data-ttu-id="cf528-106">您會在本教學課程中學到：</span><span class="sxs-lookup"><span data-stu-id="cf528-106">In this tutorial you learn to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="cf528-107">在 Azure 入口網站中，為伺服器設定伺服器層級的防火牆規則</span><span class="sxs-lookup"><span data-stu-id="cf528-107">Set up server-level firewall rules for your server in the Azure portal</span></span>
> * <span data-ttu-id="cf528-108">使用 SSMS 為資料庫設定資料庫層級的防火牆規則</span><span class="sxs-lookup"><span data-stu-id="cf528-108">Set up database-level firewall rules for your database using SSMS</span></span>
> * <span data-ttu-id="cf528-109">使用安全的連接字串來與資料庫連線</span><span class="sxs-lookup"><span data-stu-id="cf528-109">Connect to your database using a secure connection string</span></span>
> * <span data-ttu-id="cf528-110">管理使用者的存取</span><span class="sxs-lookup"><span data-stu-id="cf528-110">Manage user access</span></span>
> * <span data-ttu-id="cf528-111">使用加密來保護您的資料</span><span class="sxs-lookup"><span data-stu-id="cf528-111">Protect your data with encryption</span></span>
> * <span data-ttu-id="cf528-112">啟用 SQL Database 稽核</span><span class="sxs-lookup"><span data-stu-id="cf528-112">Enable SQL Database auditing</span></span>
> * <span data-ttu-id="cf528-113">啟用 SQL Database 威脅偵測</span><span class="sxs-lookup"><span data-stu-id="cf528-113">Enable SQL Database threat detection</span></span>

<span data-ttu-id="cf528-114">如果您沒有 Azure 訂用帳戶，請在開始之前先[建立免費帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="cf528-114">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf528-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="cf528-115">Prerequisites</span></span>

<span data-ttu-id="cf528-116">若要完成本教學課程，請確定您具有下列項目︰</span><span class="sxs-lookup"><span data-stu-id="cf528-116">To complete this tutorial, make sure you have the following:</span></span>

- <span data-ttu-id="cf528-117">已安裝最新版的 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS)。</span><span class="sxs-lookup"><span data-stu-id="cf528-117">Installed the newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span></span> 
- <span data-ttu-id="cf528-118">已安裝 Microsoft Excel</span><span class="sxs-lookup"><span data-stu-id="cf528-118">Installed Microsoft Excel</span></span>
- <span data-ttu-id="cf528-119">已建立 Azure SQL Server 和 SQL Database - 請參閱[在 Azure 入口網站中建立 Azure SQL Database](sql-database-get-started-portal.md)、[使用 Azure CLI 建立單一 Azure SQL Database](sql-database-get-started-cli.md) 和[使用 PowerShell 建立單一 Azure SQL Database](sql-database-get-started-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="cf528-119">Created an Azure SQL server and database - See [Create an Azure SQL database in the Azure portal](sql-database-get-started-portal.md), [Create a single Azure SQL database using the Azure CLI](sql-database-get-started-cli.md), and [Create a single Azure SQL database using PowerShell](sql-database-get-started-powershell.md).</span></span> 

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="cf528-120">登入 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="cf528-120">Log in to the Azure portal</span></span>

<span data-ttu-id="cf528-121">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="cf528-121">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-server-level-firewall-rule-in-the-azure-portal"></a><span data-ttu-id="cf528-122">在 Azure 入口網站中建立伺服器層級的防火牆規則</span><span class="sxs-lookup"><span data-stu-id="cf528-122">Create a server-level firewall rule in the Azure portal</span></span>

<span data-ttu-id="cf528-123">Azure 的防火牆會保護 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="cf528-123">SQL databases are protected by a firewall in Azure.</span></span> <span data-ttu-id="cf528-124">依預設，伺服器與其內部資料庫的所有連線皆會遭拒，除非是來自其他 Azure 服務的連線。</span><span class="sxs-lookup"><span data-stu-id="cf528-124">By default, all connections to the server and the databases inside the server are rejected except for connections from other Azure services.</span></span> <span data-ttu-id="cf528-125">如需詳細資訊，請參閱 [Azure SQL Database 伺服器層級和資料庫層級防火牆規則](sql-database-firewall-configure.md)</span><span class="sxs-lookup"><span data-stu-id="cf528-125">For more information, see [Azure SQL Database server-level and database-level firewall rules](sql-database-firewall-configure.md).</span></span>

<span data-ttu-id="cf528-126">最安全的設定是將「允許存取 Azure 服務」設定為「關閉」。</span><span class="sxs-lookup"><span data-stu-id="cf528-126">The most secure configuration is to set 'Allow access to Azure services' to OFF.</span></span> <span data-ttu-id="cf528-127">如果您需要從 Azure VM 或雲端服務連線到資料庫，您應建立[保留的 IP](../virtual-network/virtual-networks-reserved-public-ip.md)，並僅允許保留的 IP 位址可通過防火牆進行存取。</span><span class="sxs-lookup"><span data-stu-id="cf528-127">If you need to connect to the database from an Azure VM or cloud service, you should create a [Reserved IP](../virtual-network/virtual-networks-reserved-public-ip.md) and allow only the reserved IP address access through the firewall.</span></span> 

<span data-ttu-id="cf528-128">遵循以下步驟建立 [SQL Database 伺服器層級防火牆規則](sql-database-firewall-configure.md)，以讓您的伺服器允許來自特定 IP 位址的連線。</span><span class="sxs-lookup"><span data-stu-id="cf528-128">Follow these steps to create a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your server to allow connections from a specific IP address.</span></span> 

> [!NOTE]
> <span data-ttu-id="cf528-129">如果您已使用先前其中一個教學課程或快速入門在 Azure 中建立範例資料庫，而且您執行此教學課程的電腦與逐步進行那些教學課程時的電腦有相同的 IP 位址，表示您已建立伺服器層級的防火牆規則，所以您就可以略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="cf528-129">If you have created a sample database in Azure using one of the previous tutorials or quickstarts and are performing this tutorial on a computer with the same IP address that it had when you walked through those tutorials, you can skip this step as you will have already created a server-level firewall rule.</span></span>
>

1. <span data-ttu-id="cf528-130">按一下左側功能表上的 [SQL Database]，然後在 [SQL Database] 頁面上按一下您要設定防火牆規則的資料庫。</span><span class="sxs-lookup"><span data-stu-id="cf528-130">Click **SQL databases** from the left-hand menu and click the database you would like to configure the firewall rule for on the **SQL databases** page.</span></span> <span data-ttu-id="cf528-131">資料庫的概觀頁面隨即開啟，其中會顯示完整伺服器名稱 (例如 **mynewserver20170313.database.windows.net**)，並提供進一步的組態選項。</span><span class="sxs-lookup"><span data-stu-id="cf528-131">The overview page for your database opens, showing you the fully qualified server name (such as **mynewserver-20170313.database.windows.net**) and provides options for further configuration.</span></span>

      ![伺服器防火牆規則](./media/sql-database-security-tutorial/server-firewall-rule.png) 

2. <span data-ttu-id="cf528-133">如先前映像所示，按一下工具列上的 [設定伺服器防火牆]。</span><span class="sxs-lookup"><span data-stu-id="cf528-133">Click **Set server firewall** on the toolbar as shown in the previous image.</span></span> <span data-ttu-id="cf528-134">SQL Database 伺服器的 [防火牆設定] 頁面隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="cf528-134">The **Firewall settings** page for the SQL Database server opens.</span></span> 

3. <span data-ttu-id="cf528-135">按一下工具列上的 [新增用戶端 IP]，新增與入口網站連線的電腦公用 IP 位址，或手動輸入防火牆規則並按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="cf528-135">Click **Add client IP** on the toolbar to add the public IP address of the computer connected to the portal with or enter the firewall rule manually and then click **Save**.</span></span>

      ![設定伺服器防火牆規則](./media/sql-database-security-tutorial/server-firewall-rule-set.png) 

4. <span data-ttu-id="cf528-137">依序按一下 [確定] 和 [X] 以關閉 [防火牆設定] 頁面。</span><span class="sxs-lookup"><span data-stu-id="cf528-137">Click **OK** and then click the **X** to close the **Firewall settings** page.</span></span>

<span data-ttu-id="cf528-138">您現在可以連線到資料庫中任何具有指定 IP 位址或 IP 位址範圍的伺服器。</span><span class="sxs-lookup"><span data-stu-id="cf528-138">You can now connect to any database in the server with the specified IP address or IP address range.</span></span>

> [!NOTE]
> <span data-ttu-id="cf528-139">SQL Database 會透過連接埠 1433 通訊。</span><span class="sxs-lookup"><span data-stu-id="cf528-139">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="cf528-140">如果您嘗試從公司網路進行連線，您網路的防火牆可能不允許透過連接埠 1433 的輸出流量。</span><span class="sxs-lookup"><span data-stu-id="cf528-140">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="cf528-141">若是如此，除非 IT 部門開啟連接埠 1433，否則將無法連線至 Azure SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="cf528-141">If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-level-firewall-rule-using-ssms"></a><span data-ttu-id="cf528-142">使用 SSMS 建立資料庫層級防火牆規則</span><span class="sxs-lookup"><span data-stu-id="cf528-142">Create a database-level firewall rule using SSMS</span></span>

<span data-ttu-id="cf528-143">資料庫層級防火牆規則可讓您在相同邏輯伺服器內為不同資料庫建立不同的防火牆設定，以及建立具有可攜性的防火牆規則 - 表示這些規則在[容錯移轉](sql-database-geo-replication-overview.md)期間是跟隨著資料庫而不是儲存在 SQL Server 中。</span><span class="sxs-lookup"><span data-stu-id="cf528-143">Database-level firewall rules enable you to create different firewall settings for different databases within the same logical server and to create firewall rules that are portable - meaning that they follow the database during a [failover](sql-database-geo-replication-overview.md) rather than being stored on the SQL server.</span></span> <span data-ttu-id="cf528-144">資料庫層級的防火牆規則只能使用 Transact-SQL 陳述式設定，且僅可在您已設定第一個伺服器層級防火牆規則之後進行設定。</span><span class="sxs-lookup"><span data-stu-id="cf528-144">Database-level firewall rules can only be configured by using Transact-SQL statements and only after you have configured the first server-level firewall rule.</span></span> <span data-ttu-id="cf528-145">如需詳細資訊，請參閱 [Azure SQL Database 伺服器層級和資料庫層級防火牆規則](sql-database-firewall-configure.md)</span><span class="sxs-lookup"><span data-stu-id="cf528-145">For more information, see [Azure SQL Database server-level and database-level firewall rules](sql-database-firewall-configure.md).</span></span>

<span data-ttu-id="cf528-146">請依照下列步驟來建立資料庫專屬的防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="cf528-146">Follows these steps to create a database-specific firewall rule.</span></span>

1. <span data-ttu-id="cf528-147">連線至您的資料庫，例如使用 [SQL Server Management Studio](./sql-database-connect-query-ssms.md)。</span><span class="sxs-lookup"><span data-stu-id="cf528-147">Connect to your database, for example using [SQL Server Management Studio](./sql-database-connect-query-ssms.md).</span></span>

2. <span data-ttu-id="cf528-148">在物件總管中，以滑鼠右鍵按一下您要新增防火牆規則的資料庫，然後按一下[新增查詢]。</span><span class="sxs-lookup"><span data-stu-id="cf528-148">In Object Explorer, right-click on the database you want to add a firewall rule for and click **New Query**.</span></span> <span data-ttu-id="cf528-149">隨即開啟已連線到您資料庫的空白查詢視窗。</span><span class="sxs-lookup"><span data-stu-id="cf528-149">A blank query window opens that is connected to your database.</span></span>

3. <span data-ttu-id="cf528-150">在查詢視窗中，將 IP 位址修改為您的公用 IP 位址，然後執行下列查詢：</span><span class="sxs-lookup"><span data-stu-id="cf528-150">In the query window, modify the IP address to your public IP address and then execute the following query:</span></span>

    ```sql
    EXECUTE sp_set_database_firewall_rule N'Example DB Rule','0.0.0.4','0.0.0.4';
    ```

4. <span data-ttu-id="cf528-151">在工具列上按一下 [執行]以建立防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="cf528-151">On the toolbar, click **Execute** to create the firewall rule.</span></span>

## <a name="view-how-to-connect-an-application-to-your-database-using-a-secure-connection-string"></a><span data-ttu-id="cf528-152">檢視如何使用安全的連接字串讓應用程式與資料庫連線</span><span class="sxs-lookup"><span data-stu-id="cf528-152">View how to connect an application to your database using a secure connection string</span></span>

<span data-ttu-id="cf528-153">若要確保用戶端應用程式與 SQL Database 之間有安全且加密的連線，連接字串必須設定為：</span><span class="sxs-lookup"><span data-stu-id="cf528-153">To ensure a secure, encrypted connection between a client application and SQL Database, the connection string has to be configured to:</span></span>

- <span data-ttu-id="cf528-154">要求加密的連線，並且</span><span class="sxs-lookup"><span data-stu-id="cf528-154">Request an encrypted connection, and</span></span>
- <span data-ttu-id="cf528-155">不要信任伺服器憑證。</span><span class="sxs-lookup"><span data-stu-id="cf528-155">To not trust the server certificate.</span></span> 

<span data-ttu-id="cf528-156">此動作會建立使用傳輸層安全性 (TLS) 的連線，並降低發生攔截式攻擊的風險。</span><span class="sxs-lookup"><span data-stu-id="cf528-156">This establishes a connection using Transport Layer Security (TLS) and reduces the risk of man-in-the-middle attacks.</span></span> <span data-ttu-id="cf528-157">從 Azure 入口網站，您可以取得受支援用戶端驅動程式的 SQL Database 連接字串 (已正確設定)，如同此螢幕截圖中的 ADO.net 所示。</span><span class="sxs-lookup"><span data-stu-id="cf528-157">You can obtain correctly configured connection strings for your SQL Database for supported client drivers from the Azure portal as shown for ADO.net in this screenshot.</span></span>

1. <span data-ttu-id="cf528-158">從左側功能表中選取 [SQL Database]，按一下 [SQL Database] 頁面上您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="cf528-158">Select **SQL databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span>

2. <span data-ttu-id="cf528-159">在您資料庫的 [概觀]頁面上，按一下 [顯示資料庫連接字串]。</span><span class="sxs-lookup"><span data-stu-id="cf528-159">On the **Overview** page for your database, click **Show database connection strings**.</span></span>

3. <span data-ttu-id="cf528-160">檢閱完整的 **ADO.NET** 連接字串。</span><span class="sxs-lookup"><span data-stu-id="cf528-160">Review the complete **ADO.NET** connection string.</span></span>

    ![ADO.NET 連接字串](./media/sql-database-security-tutorial/adonet-connection-string.png)

## <a name="creating-database-users"></a><span data-ttu-id="cf528-162">建立資料庫使用者</span><span class="sxs-lookup"><span data-stu-id="cf528-162">Creating database users</span></span>

<span data-ttu-id="cf528-163">建立任何使用者之前，您必須先選取一個或兩個 Azure SQL Database 支援的驗證類型：</span><span class="sxs-lookup"><span data-stu-id="cf528-163">Before creating any users, you must first choose from one of two authentication types supported by Azure SQL Database:</span></span> 

<span data-ttu-id="cf528-164">**SQL 驗證**，使用登入作業和使用者適用的使用者名稱和密碼，而登入作業和使用者僅在邏輯伺服器內的特定資料庫環境中有效。</span><span class="sxs-lookup"><span data-stu-id="cf528-164">**SQL Authentication**, which uses username and password for logins and users that are valid only in the context of a specific database within a logical server.</span></span> 

<span data-ttu-id="cf528-165">**Azure Active Directory 驗證**，使用由 Azure Active Directory 管理的身分識別。</span><span class="sxs-lookup"><span data-stu-id="cf528-165">**Azure Active Directory Authentication**, which uses identities managed by Azure Active Directory.</span></span> 

<span data-ttu-id="cf528-166">如果您想要使用 [Azure Active Directory](./sql-database-aad-authentication.md) 對 SQL Database 進行驗證，則必須有填入的 Azure Active Directory 才可繼續。</span><span class="sxs-lookup"><span data-stu-id="cf528-166">If you want to use [Azure Active Directory](./sql-database-aad-authentication.md) to authenticate against SQL Database, a populated Azure Active Directory must exist before you can proceed.</span></span>

<span data-ttu-id="cf528-167">請遵循以下步驟使用 SQL Authentication 建立使用者：</span><span class="sxs-lookup"><span data-stu-id="cf528-167">Follow these steps to create a user using SQL Authentication:</span></span>

1. <span data-ttu-id="cf528-168">使用 [SQL Server Management Studio](./sql-database-connect-query-ssms.md) 等方式以使用您的伺服器系統管理員認證與資料庫連線。</span><span class="sxs-lookup"><span data-stu-id="cf528-168">Connect to your database, for example using [SQL Server Management Studio](./sql-database-connect-query-ssms.md) using your server admin credentials.</span></span>

2. <span data-ttu-id="cf528-169">在物件總管中，以滑鼠右鍵按一下您要新增使用者的資料庫，然後按一下[新增查詢]。</span><span class="sxs-lookup"><span data-stu-id="cf528-169">In Object Explorer, right-click on the database you want to add a new user on and click **New Query**.</span></span> <span data-ttu-id="cf528-170">隨即開啟已連線到所選資料庫的空白查詢視窗。</span><span class="sxs-lookup"><span data-stu-id="cf528-170">A blank query window opens that is connected to the selected database.</span></span>

3. <span data-ttu-id="cf528-171">在查詢視窗中，輸入下列查詢︰</span><span class="sxs-lookup"><span data-stu-id="cf528-171">In the query window, enter the following query:</span></span>

    ```sql
    CREATE USER ApplicationUser WITH PASSWORD = 'YourStrongPassword1';
    ```

4. <span data-ttu-id="cf528-172">在工具列上按一下 [執行] 以建立使用者。</span><span class="sxs-lookup"><span data-stu-id="cf528-172">On the toolbar, click **Execute** to create the user.</span></span>

5. <span data-ttu-id="cf528-173">依預設，使用者可與資料庫連線，但沒有權限可讀取或寫入資料。</span><span class="sxs-lookup"><span data-stu-id="cf528-173">By default, the user can connect to the database, but has no permissions to read or write data.</span></span> <span data-ttu-id="cf528-174">若要將這些權限授與新建立的使用者，請在新的查詢視窗中執行下列兩個命令</span><span class="sxs-lookup"><span data-stu-id="cf528-174">To grant these permissions to the newly created user, execute the following two commands in a new query window</span></span>

    ```sql
    ALTER ROLE db_datareader ADD MEMBER ApplicationUser;
    ALTER ROLE db_datawriter ADD MEMBER ApplicationUser;
    ```

<span data-ttu-id="cf528-175">若要在資料庫層級建立這些非系統管理員帳戶來與您資料庫連線，這是最佳的作法，除非您需要執行如建立新使用者的系統管理員工作。</span><span class="sxs-lookup"><span data-stu-id="cf528-175">It is best practice to create these non-administrator accounts at the database level to connect to your database unless you need to execute administrator tasks like creating new users.</span></span> <span data-ttu-id="cf528-176">請檢閱 [Azure Active Directory 教學課程](./sql-database-aad-authentication-configure.md)以了解如何使用 Azure Active Directory 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="cf528-176">Please review the [Azure Active Directory tutorial](./sql-database-aad-authentication-configure.md) on how to authenticate using Azure Active Directory.</span></span>


## <a name="protect-your-data-with-encryption"></a><span data-ttu-id="cf528-177">使用加密來保護您的資料</span><span class="sxs-lookup"><span data-stu-id="cf528-177">Protect your data with encryption</span></span>

<span data-ttu-id="cf528-178">Azure SQL Database 透明資料加密 (TDE) 會自動為您的待用資料加密，且應用程式不須做任何變更來存取加密的資料庫。</span><span class="sxs-lookup"><span data-stu-id="cf528-178">Azure SQL Database transparent data encryption (TDE) automatically encrypts your data at rest, without requiring any changes to the application accessing the encrypted database.</span></span> <span data-ttu-id="cf528-179">如果是新建立的資料庫，TDE 預設為開啟。</span><span class="sxs-lookup"><span data-stu-id="cf528-179">For newly created databases, TDE is on by default.</span></span> <span data-ttu-id="cf528-180">若要為您的資料庫啟用 TDE，或確認已開啟 TDE，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="cf528-180">To enable TDE for your database or to verify that TDE is on, follow these steps:</span></span>

1. <span data-ttu-id="cf528-181">從左側功能表中選取 [SQL Database]，按一下 [SQL Database] 頁面上您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="cf528-181">Select **SQL databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 

2. <span data-ttu-id="cf528-182">按一下 [透明資料加密] 以開啟 TDE 的組態頁面。</span><span class="sxs-lookup"><span data-stu-id="cf528-182">Click on **Transparent data encryption** to open the configuration page for TDE.</span></span>

    ![透明資料加密](./media/sql-database-security-tutorial/transparent-data-encryption-enabled.png)

3. <span data-ttu-id="cf528-184">如有必要，請將 [資料加密] 設為「開啟」，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="cf528-184">If necessary, set **Data encryption** to ON and click **Save**.</span></span>

<span data-ttu-id="cf528-185">加密程序會在背景中啟動。</span><span class="sxs-lookup"><span data-stu-id="cf528-185">The encryption process starts in the background.</span></span> <span data-ttu-id="cf528-186">您可以使用 [SQL Server Management Studio](./sql-database-connect-query-ssms.md) 來連線至 SQL Database，並查詢 `sys.dm_database_encryption_keys` 檢視的 encryption_state 資料行，以監視進度。</span><span class="sxs-lookup"><span data-stu-id="cf528-186">You can monitor the progress by connecting to SQL Database using [SQL Server Management Studio](./sql-database-connect-query-ssms.md) by querying the encryption_state column of the `sys.dm_database_encryption_keys` view.</span></span>

## <a name="enable-sql-database-auditing-if-necessary"></a><span data-ttu-id="cf528-187">啟用 SQL Database 稽核 (如有必要)</span><span class="sxs-lookup"><span data-stu-id="cf528-187">Enable SQL Database auditing, if necessary</span></span>

<span data-ttu-id="cf528-188">Azure SQL Database 稽核會追蹤資料庫事件並將事件寫入您 Azure 儲存體帳戶中的稽核記錄。</span><span class="sxs-lookup"><span data-stu-id="cf528-188">Azure SQL Database Auditing tracks database events and writes them to an audit log in your Azure Storage account.</span></span> <span data-ttu-id="cf528-189">稽核可協助您保持法規合規性、了解資料庫活動，以及深入了解可能指出潛在安全違規的不一致和異常。</span><span class="sxs-lookup"><span data-stu-id="cf528-189">Auditing can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate potential security violations.</span></span> <span data-ttu-id="cf528-190">請遵循下列步驟為 SQL Database 建立預設的稽核原則︰</span><span class="sxs-lookup"><span data-stu-id="cf528-190">Follow these steps to create a default auditing policy for your SQL database:</span></span>

1. <span data-ttu-id="cf528-191">從左側功能表中選取 [SQL Database]，按一下 [SQL Database] 頁面上您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="cf528-191">Select **SQL databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 

2. <span data-ttu-id="cf528-192">在 [設定] 刀鋒視窗中，選取 [稽核和威脅偵測]。</span><span class="sxs-lookup"><span data-stu-id="cf528-192">In the Settings blade, select **Auditing & Threat Detection**.</span></span> <span data-ttu-id="cf528-193">請注意，伺服器層級稽核已停用，而且有一個**檢視伺服器設定**連結，可讓您從此內容檢視或修改伺服器稽核設定。</span><span class="sxs-lookup"><span data-stu-id="cf528-193">Notice that sever-level auditing is diabled and that there is a **View server settings** link that allows you to view or modify the server auditing settings from this context.</span></span>

    ![稽核刀鋒視窗](./media/sql-database-security-tutorial/auditing-get-started-settings.png)

3. <span data-ttu-id="cf528-195">如果您想要啟用的稽核類型 (或位置？) 與伺服器層級所指定的類型不同，請**開啟**稽核，並選擇 [Blob] 稽核類型。</span><span class="sxs-lookup"><span data-stu-id="cf528-195">If you prefer to enable an Audit type (or location?) different from the one specified at the server level, turn **ON** Auditing, and choose the **Blob** Auditing Type.</span></span> <span data-ttu-id="cf528-196">如果已經啟用伺服器 Blob 稽核，資料庫設定的稽核將會與伺服器 Blob 稽核並存。</span><span class="sxs-lookup"><span data-stu-id="cf528-196">If server Blob auditing is enabled, the database configured audit will exist side by side with the server Blob audit.</span></span>

    ![開啟稽核](./media/sql-database-security-tutorial/auditing-get-started-turn-on.png)

4. <span data-ttu-id="cf528-198">選取 [儲存體詳細資料] 以開啟 [稽核記錄儲存體] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="cf528-198">Select **Storage Details** to open the Audit Logs Storage Blade.</span></span> <span data-ttu-id="cf528-199">選取將儲存記錄的 Azure 儲存體帳戶，以及將舊記錄刪除之前的保留期間，然後按一下底部的 [確定]。</span><span class="sxs-lookup"><span data-stu-id="cf528-199">Select the Azure storage account where logs will be saved, and the retention period, after which the old logs will be deleted, then click **OK** at the bottom.</span></span> 

   > [!TIP]
   > <span data-ttu-id="cf528-200">讓所有稽核的資料庫都使用相同的儲存體帳戶，以充分利用稽核報告範本。</span><span class="sxs-lookup"><span data-stu-id="cf528-200">Use the same storage account for all audited databases to get the most out of the auditing reports templates.</span></span>
   > 

5. <span data-ttu-id="cf528-201">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="cf528-201">Click **Save**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cf528-202">如果您想要自訂稽核事件，您可以透過 PowerShell 或 REST API 來自訂- 請參閱[自動化 (PowerShell / REST API)](sql-database-auditing.md#subheading-7) 一節以了解更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="cf528-202">If you want to customize the audited events, you can do this via PowerShell or REST API - see the [Automation (PowerShell / REST API)](sql-database-auditing.md#subheading-7) section for more details.</span></span>
>

## <a name="enable-sql-database-threat-detection"></a><span data-ttu-id="cf528-203">啟用 SQL Database 威脅偵測</span><span class="sxs-lookup"><span data-stu-id="cf528-203">Enable SQL Database threat detection</span></span>

<span data-ttu-id="cf528-204">威脅偵測提供新的一層安全性，在發生異常活動時會提供安全性警示，讓客戶偵測並回應潛在威脅。</span><span class="sxs-lookup"><span data-stu-id="cf528-204">Threat Detection provides a new layer of security, which enables customers to detect and respond to potential threats as they occur by providing security alerts on anomalous activities.</span></span> <span data-ttu-id="cf528-205">使用者可以使用 SQL Database 稽核來探索可疑的事件，以判斷事件的原因是否是有人嘗試存取、破壞或利用資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="cf528-205">Users can explore the suspicious events using SQL Database Auditing to determine if they result from an attempt to access, breach or exploit data in the database.</span></span> <span data-ttu-id="cf528-206">您不必是安全性專家，也不需要管理進階的安全性監視系統，威脅偵測讓您輕鬆解決資料庫的潛在威脅。</span><span class="sxs-lookup"><span data-stu-id="cf528-206">Threat Detection makes it simple to address potential threats to the database without the need to be a security expert or manage advanced security monitoring systems.</span></span>
<span data-ttu-id="cf528-207">威脅偵測會偵測異常資料庫活動，指出潛在的 SQL 插入式攻擊。</span><span class="sxs-lookup"><span data-stu-id="cf528-207">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="cf528-208">SQL 插入式攻擊是網際網路上常見的 Web 應用程式安全性問題之一，用於攻擊資料導向應用程式。</span><span class="sxs-lookup"><span data-stu-id="cf528-208">SQL injection is one of the common Web application security issues on the Internet, used to attack data-driven applications.</span></span> <span data-ttu-id="cf528-209">攻擊者利用應用程式弱點將惡意的 SQL 陳述式插入應用程式輸入欄位，以破壞或修改資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="cf528-209">Attackers take advantage of application vulnerabilities to inject malicious SQL statements into application entry fields, for breaching or modifying data in the database.</span></span>

1. <span data-ttu-id="cf528-210">瀏覽至您要監視的 SQL Database 組態刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="cf528-210">Navigate to the configuration blade of the SQL database you want to monitor.</span></span> <span data-ttu-id="cf528-211">在 [設定] 刀鋒視窗中，選取 [稽核和威脅偵測]。</span><span class="sxs-lookup"><span data-stu-id="cf528-211">In the Settings blade, select **Auditing & Threat Detection**.</span></span>

    ![瀏覽窗格](./media/sql-database-security-tutorial/auditing-get-started-settings.png)
2. <span data-ttu-id="cf528-213">在 [稽核與威脅偵測] 組態刀鋒視窗中，[開啟] 稽核，這會顯示威脅偵測設定。</span><span class="sxs-lookup"><span data-stu-id="cf528-213">In the **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display the threat detection settings.</span></span>

3. <span data-ttu-id="cf528-214">[開啟] 威脅偵測。</span><span class="sxs-lookup"><span data-stu-id="cf528-214">Turn **ON** threat detection.</span></span>

4. <span data-ttu-id="cf528-215">設定在偵測到異常資料庫活動時將收到安全性警示的電子郵件清單。</span><span class="sxs-lookup"><span data-stu-id="cf528-215">Configure the list of emails that will receive security alerts upon detection of anomalous database activities.</span></span>

5. <span data-ttu-id="cf528-216">按一下 [稽核與威脅偵測] 刀鋒視窗中的 [儲存]，以儲存新的或已更新的稽核與威脅偵測原則。</span><span class="sxs-lookup"><span data-stu-id="cf528-216">Click **Save** in the **Auditing & Threat detection** blade to save the new or updated auditing and threat detection policy.</span></span>

    ![導覽窗格](./media/sql-database-security-tutorial/td-turn-on-threat-detection.png)

    <span data-ttu-id="cf528-218">如果偵測到異常的資料庫活動，您會在一偵測到異常的資料庫活動時，就收到電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="cf528-218">If anomalous database activities are detected, you will receive an email notification upon detection of anomalous database activities.</span></span> <span data-ttu-id="cf528-219">電子郵件將提供可疑安全性事件的相關資訊，包括異常活動的性質、資料庫名稱、伺服器名稱和事件時間。</span><span class="sxs-lookup"><span data-stu-id="cf528-219">The email will provide information on the suspicious security event including the nature of the anomalous activities, database name, server name and the event time.</span></span> <span data-ttu-id="cf528-220">此外，還會提供可能原因和建議動作的相關資訊，以協助您調查和減輕資料庫的潛在威脅。</span><span class="sxs-lookup"><span data-stu-id="cf528-220">In addition, it will provide information on possible causes and recommended actions to investigate and mitigate the potential threat to the database.</span></span> <span data-ttu-id="cf528-221">以下步驟會逐步說明收到以下類型的電子郵件時，您該怎麼做：</span><span class="sxs-lookup"><span data-stu-id="cf528-221">The next steps walk you through what to do should you receive such an email:</span></span>

    ![威脅偵測電子郵件](./media/sql-database-threat-detection-get-started/4_td_email.png)

6. <span data-ttu-id="cf528-223">在電子郵件中，按一下 [Azure SQL 稽核記錄] 連結會啟動 Azure 入口網站，並顯示可疑事件發生時間前後的相關稽核記錄。</span><span class="sxs-lookup"><span data-stu-id="cf528-223">In the email, click on the **Azure SQL Auditing Log** link, which will launch the Azure portal and show the relevant auditing records around the time of the suspicious event.</span></span>

    ![稽核記錄](./media/sql-database-threat-detection-get-started/5_td_audit_records.png)

7. <span data-ttu-id="cf528-225">按一下稽核記錄以檢視可疑資料庫活動的詳細資訊，例如 SQL 陳述式、失敗原因和用戶端的 IP。</span><span class="sxs-lookup"><span data-stu-id="cf528-225">Click on the audit records to view more details on the suspicious database activities such as SQL statement, failure reason and client IP.</span></span>

    ![記錄詳細資料](./media/sql-database-security-tutorial/6_td_audit_record_details.png)

8. <span data-ttu-id="cf528-227">在 [稽核記錄] 刀鋒視窗中，按一下 [在 Excel 中開啟] 開啟預先設定的 Excel 範本，以匯入可疑事件前後的稽核記錄，執行更深入的分析。</span><span class="sxs-lookup"><span data-stu-id="cf528-227">In the Auditing Records blade, click  **Open in Excel** to open a pre-configured excel template to import and run deeper analysis of the audit log around the time of the suspicious event.</span></span>

    > [!NOTE]
    > <span data-ttu-id="cf528-228">在 Excel 2010 或更新版本中，必須要有 Power Query 和 [快速合併] 設定。</span><span class="sxs-lookup"><span data-stu-id="cf528-228">In Excel 2010 or later, Power Query and the **Fast Combine** setting is required.</span></span>

    ![在 Excel 中開啟記錄](./media/sql-database-threat-detection-get-started/7_td_audit_records_open_excel.png)

9. <span data-ttu-id="cf528-230">若要設定 [快速合併] 設定 - 在 [POWER QUERY] 功能區索引標籤中，選取 [選項] 以顯示 [選項] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="cf528-230">To configure the **Fast Combine** setting - In the **POWER QUERY** ribbon tab, select **Options** to display the Options dialog.</span></span> <span data-ttu-id="cf528-231">選取 [隱私權] 區段，選擇第二個選項 - [忽略隱私權等級並可能改善效能]：</span><span class="sxs-lookup"><span data-stu-id="cf528-231">Select the Privacy section and choose the second option - 'Ignore the Privacy Levels and potentially improve performance':</span></span>

    ![Excel 快速合併](./media/sql-database-threat-detection-get-started/8_td_excel_fast_combine.png)

10. <span data-ttu-id="cf528-233">若要載入 SQL 稽核記錄檔，請確定 [設定] 索引標籤中的參數已正確設定，然後選取 [資料] 功能區，並按一下 [全部重新整理] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cf528-233">To load SQL audit logs, ensure that the parameters in the settings tab are set correctly and then select the 'Data' ribbon and click the 'Refresh All' button.</span></span>

    ![Excel 參數](./media/sql-database-threat-detection-get-started/9_td_excel_parameters.png)

11. <span data-ttu-id="cf528-235">結果會出現在 [SQL 稽核記錄檔]  工作表，可讓您對偵測到的異常活動執行更深入的分析，減輕應用程式中的安全性事件造成的影響。</span><span class="sxs-lookup"><span data-stu-id="cf528-235">The results appear in the **SQL Audit Logs** sheet which enables you to run deeper analysis of the anomalous activities that were detected, and mitigate the impact of the security event in your application.</span></span>


## <a name="next-steps"></a><span data-ttu-id="cf528-236">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cf528-236">Next steps</span></span>
<span data-ttu-id="cf528-237">只需要幾個簡單步驟，您就可以讓資料庫預防惡意使用者或未經授權的存取。</span><span class="sxs-lookup"><span data-stu-id="cf528-237">You can improve the protection of your database against malicious users or unauthorized access with just a few simple steps.</span></span> <span data-ttu-id="cf528-238">您會在本教學課程中學到：</span><span class="sxs-lookup"><span data-stu-id="cf528-238">In this tutorial you learn to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="cf528-239">設定伺服器和/或資料庫的防火牆規則</span><span class="sxs-lookup"><span data-stu-id="cf528-239">Set up firewall rules for your sever and or database</span></span>
> * <span data-ttu-id="cf528-240">使用安全的連接字串來與資料庫連線</span><span class="sxs-lookup"><span data-stu-id="cf528-240">Connect to your database using a secure connection string</span></span>
> * <span data-ttu-id="cf528-241">管理使用者的存取</span><span class="sxs-lookup"><span data-stu-id="cf528-241">Manage user access</span></span>
> * <span data-ttu-id="cf528-242">使用加密來保護您的資料</span><span class="sxs-lookup"><span data-stu-id="cf528-242">Protect your data with encryption</span></span>
> * <span data-ttu-id="cf528-243">啟用 SQL Database 稽核</span><span class="sxs-lookup"><span data-stu-id="cf528-243">Enable SQL Database auditing</span></span>
> * <span data-ttu-id="cf528-244">啟用 SQL Database 威脅偵測</span><span class="sxs-lookup"><span data-stu-id="cf528-244">Enable SQL Database threat detection</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="cf528-245">改善 SQL Database 效能</span><span class="sxs-lookup"><span data-stu-id="cf528-245">Improve SQL Database performance</span></span>](sql-database-performance-tutorial.md)

