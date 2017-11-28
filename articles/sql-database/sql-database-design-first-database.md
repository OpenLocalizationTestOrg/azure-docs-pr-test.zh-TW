---
title: "設計您的第一個 Azure SQL Database | Microsoft Docs"
description: "了解如何設計您的第一個 Azure SQL Database。"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,develop databases
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 08/03/2017
ms.author: carlrab
ms.openlocfilehash: 69cfffdae5ce2db53acc6d668dbe468c3ef22dc2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="design-your-first-azure-sql-database"></a><span data-ttu-id="123f8-103">設計您的第一個 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="123f8-103">Design your first Azure SQL database</span></span>

<span data-ttu-id="123f8-104">Azure SQL Database 是 Microsoft 雲端 ("Azure") 中的關聯式資料庫即服務 (DBaaS)。</span><span class="sxs-lookup"><span data-stu-id="123f8-104">Azure SQL Database is a relational database-as-a service (DBaaS) in the Microsoft Cloud ("Azure").</span></span> <span data-ttu-id="123f8-105">在本教學課程中，您會了解如何使用 Azure 入口網站和 [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS)：</span><span class="sxs-lookup"><span data-stu-id="123f8-105">In this tutorial, you learn how to use the Azure portal and [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="123f8-106">在 Azure 入口網站中建立資料庫</span><span class="sxs-lookup"><span data-stu-id="123f8-106">Create a database in the Azure portal</span></span>
> * <span data-ttu-id="123f8-107">在 Azure 入口網站中設定伺服器層級的防火牆規則</span><span class="sxs-lookup"><span data-stu-id="123f8-107">Set up a server-level firewall rule in the Azure portal</span></span>
> * <span data-ttu-id="123f8-108">使用 SSMS 連接到資料庫</span><span class="sxs-lookup"><span data-stu-id="123f8-108">Connect to the database with SSMS</span></span>
> * <span data-ttu-id="123f8-109">使用 SSMS 建立資料表</span><span class="sxs-lookup"><span data-stu-id="123f8-109">Create tables with SSMS</span></span>
> * <span data-ttu-id="123f8-110">使用 BCP 大量載入資料</span><span class="sxs-lookup"><span data-stu-id="123f8-110">Bulk load data with BCP</span></span>
> * <span data-ttu-id="123f8-111">使用 SSMS 查詢該資料</span><span class="sxs-lookup"><span data-stu-id="123f8-111">Query that data with SSMS</span></span>
> * <span data-ttu-id="123f8-112">在 Azure 入口網站中將資料庫還原到先前的[時間點還原](sql-database-recovery-using-backups.md#point-in-time-restore)</span><span class="sxs-lookup"><span data-stu-id="123f8-112">Restore the database to a previous [point in time restore](sql-database-recovery-using-backups.md#point-in-time-restore) in the Azure portal</span></span>

<span data-ttu-id="123f8-113">如果您沒有 Azure 訂用帳戶，請在開始之前先[建立免費帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="123f8-113">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="123f8-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="123f8-114">Prerequisites</span></span>

<span data-ttu-id="123f8-115">若要完成本教學課程，請確定您已安裝︰</span><span class="sxs-lookup"><span data-stu-id="123f8-115">To complete this tutorial, make sure you have installed:</span></span>
- <span data-ttu-id="123f8-116">最新版的 [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS)。</span><span class="sxs-lookup"><span data-stu-id="123f8-116">The newest version of [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS).</span></span>
- <span data-ttu-id="123f8-117">最新版的 [BCP 和 SQLCMD](https://www.microsoft.com/download/details.aspx?id=36433)。</span><span class="sxs-lookup"><span data-stu-id="123f8-117">The newest version of [BCP and SQLCMD](https://www.microsoft.com/download/details.aspx?id=36433).</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="123f8-118">登入 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="123f8-118">Log in to the Azure portal</span></span>

<span data-ttu-id="123f8-119">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="123f8-119">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-blank-sql-database"></a><span data-ttu-id="123f8-120">建立空白 SQL Database</span><span class="sxs-lookup"><span data-stu-id="123f8-120">Create a blank SQL database</span></span>

<span data-ttu-id="123f8-121">Azure SQL Database 會使用一組定義的[計算和儲存體資源](sql-database-service-tiers.md)建立。</span><span class="sxs-lookup"><span data-stu-id="123f8-121">An Azure SQL database is created with a defined set of [compute and storage resources](sql-database-service-tiers.md).</span></span> <span data-ttu-id="123f8-122">此資料庫建立於 [Azure 資源群組](../azure-resource-manager/resource-group-overview.md)和 [Azure SQL Database 邏輯伺服器](sql-database-features.md)內。</span><span class="sxs-lookup"><span data-stu-id="123f8-122">The database is created within an [Azure resource group](../azure-resource-manager/resource-group-overview.md) and in an [Azure SQL Database logical server](sql-database-features.md).</span></span> 

<span data-ttu-id="123f8-123">遵循以下步驟來建立空白 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="123f8-123">Follow these steps to create a blank SQL database.</span></span> 

1. <span data-ttu-id="123f8-124">按一下 Azure 入口網站左上角的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="123f8-124">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="123f8-125">從 [新增] 頁面中選取 [資料庫]，然後從 [資料庫] 頁面中選取 [SQL Database]。</span><span class="sxs-lookup"><span data-stu-id="123f8-125">Select **Databases** from the **New** page, and select **SQL Database** from the **Databases** page.</span></span> 

   ![建立空白資料庫](./media/sql-database-design-first-database/create-empty-database.png)

3. <span data-ttu-id="123f8-127">使用下列資訊填寫 SQL Database 表單，如上圖所示︰</span><span class="sxs-lookup"><span data-stu-id="123f8-127">Fill out the SQL Database form with the following information, as shown on the preceding image:</span></span>   

   | <span data-ttu-id="123f8-128">設定</span><span class="sxs-lookup"><span data-stu-id="123f8-128">Setting</span></span>       | <span data-ttu-id="123f8-129">建議的值</span><span class="sxs-lookup"><span data-stu-id="123f8-129">Suggested value</span></span> | <span data-ttu-id="123f8-130">說明</span><span class="sxs-lookup"><span data-stu-id="123f8-130">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="123f8-131">**資料庫名稱**</span><span class="sxs-lookup"><span data-stu-id="123f8-131">**Database name**</span></span> | <span data-ttu-id="123f8-132">mySampleDatabase</span><span class="sxs-lookup"><span data-stu-id="123f8-132">mySampleDatabase</span></span> | <span data-ttu-id="123f8-133">如需有效的資料庫名稱，請參閱[資料庫識別碼](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers)。</span><span class="sxs-lookup"><span data-stu-id="123f8-133">For valid database names, see [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers).</span></span> | 
   | <span data-ttu-id="123f8-134">**訂用帳戶**</span><span class="sxs-lookup"><span data-stu-id="123f8-134">**Subscription**</span></span> | <span data-ttu-id="123f8-135">您的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="123f8-135">Your subscription</span></span>  | <span data-ttu-id="123f8-136">如需訂用帳戶的詳細資訊，請參閱[訂用帳戶](https://account.windowsazure.com/Subscriptions)。</span><span class="sxs-lookup"><span data-stu-id="123f8-136">For details about your subscriptions, see [Subscriptions](https://account.windowsazure.com/Subscriptions).</span></span> |
   | <span data-ttu-id="123f8-137">**資源群組**</span><span class="sxs-lookup"><span data-stu-id="123f8-137">**Resource group**</span></span> | <span data-ttu-id="123f8-138">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="123f8-138">myResourceGroup</span></span> | <span data-ttu-id="123f8-139">如需有效的資源群組名稱，請參閱[命名規則和限制](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions)。</span><span class="sxs-lookup"><span data-stu-id="123f8-139">For valid resource group names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> |
   | <span data-ttu-id="123f8-140">**選取來源**</span><span class="sxs-lookup"><span data-stu-id="123f8-140">**Select source**</span></span> | <span data-ttu-id="123f8-141">空白資料庫</span><span class="sxs-lookup"><span data-stu-id="123f8-141">Blank database</span></span> | <span data-ttu-id="123f8-142">指定應建立空白資料庫。</span><span class="sxs-lookup"><span data-stu-id="123f8-142">Specifies that a blank database should be created.</span></span> |

4. <span data-ttu-id="123f8-143">按一下 [伺服器] 為您的新資料庫建立及設定新的伺服器。</span><span class="sxs-lookup"><span data-stu-id="123f8-143">Click **Server** to create and configure a new server for your new database.</span></span> <span data-ttu-id="123f8-144">在**新伺服器表單**表單中填寫下列資訊︰</span><span class="sxs-lookup"><span data-stu-id="123f8-144">Fill out the **New server form** with the following information:</span></span> 

   | <span data-ttu-id="123f8-145">設定</span><span class="sxs-lookup"><span data-stu-id="123f8-145">Setting</span></span>       | <span data-ttu-id="123f8-146">建議的值</span><span class="sxs-lookup"><span data-stu-id="123f8-146">Suggested value</span></span> | <span data-ttu-id="123f8-147">說明</span><span class="sxs-lookup"><span data-stu-id="123f8-147">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="123f8-148">**伺服器名稱**</span><span class="sxs-lookup"><span data-stu-id="123f8-148">**Server name**</span></span> | <span data-ttu-id="123f8-149">任何全域唯一名稱</span><span class="sxs-lookup"><span data-stu-id="123f8-149">Any globally unique name</span></span> | <span data-ttu-id="123f8-150">如需有效的伺服器名稱，請參閱[命名規則和限制](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions)。</span><span class="sxs-lookup"><span data-stu-id="123f8-150">For valid server names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> | 
   | <span data-ttu-id="123f8-151">**伺服器管理員登入**</span><span class="sxs-lookup"><span data-stu-id="123f8-151">**Server admin login**</span></span> | <span data-ttu-id="123f8-152">任何有效名稱</span><span class="sxs-lookup"><span data-stu-id="123f8-152">Any valid name</span></span> | <span data-ttu-id="123f8-153">如需有效的登入名稱，請參閱[資料庫識別碼](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers)。</span><span class="sxs-lookup"><span data-stu-id="123f8-153">For valid login names, see [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers).</span></span>|
   | <span data-ttu-id="123f8-154">**密碼**</span><span class="sxs-lookup"><span data-stu-id="123f8-154">**Password**</span></span> | <span data-ttu-id="123f8-155">任何有效密碼</span><span class="sxs-lookup"><span data-stu-id="123f8-155">Any valid password</span></span> | <span data-ttu-id="123f8-156">您的密碼至少要有 8 個字元，而且必須包含下列幾種字元的其中三種︰大寫字元、小寫字元、數字和非英數字元。</span><span class="sxs-lookup"><span data-stu-id="123f8-156">Your password must have at least 8 characters and must contain characters from three of the following categories: upper case characters, lower case characters, numbers, and non-alphanumeric characters.</span></span> |
   | <span data-ttu-id="123f8-157">**位置**</span><span class="sxs-lookup"><span data-stu-id="123f8-157">**Location**</span></span> | <span data-ttu-id="123f8-158">任何有效位置</span><span class="sxs-lookup"><span data-stu-id="123f8-158">Any valid location</span></span> | <span data-ttu-id="123f8-159">如需區域的相關資訊，請參閱 [Azure 區域](https://azure.microsoft.com/regions/)。</span><span class="sxs-lookup"><span data-stu-id="123f8-159">For information about regions, see [Azure Regions](https://azure.microsoft.com/regions/).</span></span> |

   ![建立資料庫伺服器](./media//sql-database-design-first-database/create-database-server.png)

5. <span data-ttu-id="123f8-161">按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="123f8-161">Click **Select**.</span></span>

6. <span data-ttu-id="123f8-162">按一下 [定價層] 指定新資料庫的服務層和效能等級。</span><span class="sxs-lookup"><span data-stu-id="123f8-162">Click **Pricing tier** to specify the service tier and performance level for your new database.</span></span> <span data-ttu-id="123f8-163">針對此快速入門，選取 [20 DTUs (20 個 DTU)] 和 [250] GB 儲存體。</span><span class="sxs-lookup"><span data-stu-id="123f8-163">For this tutorial, select **20 DTUs** and **250** GB of storage.</span></span>

   ![建立資料庫-s1](./media/sql-database-design-first-database/create-empty-database-pricing-tier.png)

7. <span data-ttu-id="123f8-165">按一下 [Apply (套用)] 。</span><span class="sxs-lookup"><span data-stu-id="123f8-165">Click **Apply**.</span></span>  

8. <span data-ttu-id="123f8-166">為空白資料庫選取**定序** (此教學課程中使用預設值)。</span><span class="sxs-lookup"><span data-stu-id="123f8-166">Select a **collation** for the blank database (for this tutorial, use the default value).</span></span> <span data-ttu-id="123f8-167">如需定序的詳細資訊，請參閱[定序](https://docs.microsoft.com/sql/t-sql/statements/collations)。</span><span class="sxs-lookup"><span data-stu-id="123f8-167">For more information about collations, see [Collations](https://docs.microsoft.com/sql/t-sql/statements/collations)</span></span>

9. <span data-ttu-id="123f8-168">按一下 [建立] 即可佈建資料庫。</span><span class="sxs-lookup"><span data-stu-id="123f8-168">Click **Create** to provision the database.</span></span> <span data-ttu-id="123f8-169">佈建完成所需時間約 1.5 分。</span><span class="sxs-lookup"><span data-stu-id="123f8-169">Provisioning takes about a minute and a half to complete.</span></span> 

10. <span data-ttu-id="123f8-170">在工具列上，按一下 [通知] 以監視部署程序。</span><span class="sxs-lookup"><span data-stu-id="123f8-170">On the toolbar, click **Notifications** to monitor the deployment process.</span></span>

   ![通知](./media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule"></a><span data-ttu-id="123f8-172">建立伺服器層級防火牆規則</span><span class="sxs-lookup"><span data-stu-id="123f8-172">Create a server-level firewall rule</span></span>

<span data-ttu-id="123f8-173">SQL Database 服務會在伺服器層級建立防火牆，防止外部應用程式和工具連線到伺服器或伺服器上的任何資料庫，除非建立防火牆規則以針對特定的 IP 位址開啟防火牆。</span><span class="sxs-lookup"><span data-stu-id="123f8-173">The SQL Database service creates a firewall at the server-level that prevents external applications and tools from connecting to the server or any databases on the server unless a firewall rule is created to open the firewall for specific IP addresses.</span></span> <span data-ttu-id="123f8-174">請遵循下列步驟來為您用戶端的 IP 位址建立 [SQL Database 伺服器層級防火牆規則](sql-database-firewall-configure.md)，並讓外部連線僅能夠穿過您 IP 位址的 SQL Database 防火牆。</span><span class="sxs-lookup"><span data-stu-id="123f8-174">Follow these steps to create a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your client's IP address and enable external connectivity through the SQL Database firewall for your IP address only.</span></span> 

> [!NOTE]
> <span data-ttu-id="123f8-175">SQL Database 會透過連接埠 1433 通訊。</span><span class="sxs-lookup"><span data-stu-id="123f8-175">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="123f8-176">如果您嘗試從公司網路進行連線，您網路的防火牆可能不允許透過連接埠 1433 的輸出流量。</span><span class="sxs-lookup"><span data-stu-id="123f8-176">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="123f8-177">若情況如此，除非 IT 部門開啟連接埠 1433，否則您無法連線至 Azure SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="123f8-177">If so, you cannot connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

1. <span data-ttu-id="123f8-178">部署完成之後，按一下左側功能表中的 [SQL Database]，然後按一下 [SQL Database] 頁面上的 [mySampleDatabase]。</span><span class="sxs-lookup"><span data-stu-id="123f8-178">After the deployment completes, click **SQL databases** from the left-hand menu and then click **mySampleDatabase** on the **SQL databases** page.</span></span> <span data-ttu-id="123f8-179">資料庫的 [概觀] 頁面隨即開啟，其中會顯示完整伺服器名稱 (例如 **mynewserver20170313.database.windows.net**)，並提供進一步的組態選項。</span><span class="sxs-lookup"><span data-stu-id="123f8-179">The overview page for your database opens, showing you the fully qualified server name (such as **mynewserver20170313.database.windows.net**) and provides options for further configuration.</span></span> <span data-ttu-id="123f8-180">將這個完整伺服器名稱複製起來，以供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="123f8-180">Copy this fully qualified server name for use later.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="123f8-181">在後續的快速入門中，您需要此完整伺服器名稱才能連線到伺服器及其資料庫。</span><span class="sxs-lookup"><span data-stu-id="123f8-181">You need this fully qualified server name to connect to your server and its databases in subsequent quick starts.</span></span>
   > 

   ![伺服器名稱](./media/sql-database-connect-query-dotnet/server-name.png) 

2. <span data-ttu-id="123f8-183">如先前映像所示，按一下工具列上的 [設定伺服器防火牆]。</span><span class="sxs-lookup"><span data-stu-id="123f8-183">Click **Set server firewall** on the toolbar as shown in the previous image.</span></span> <span data-ttu-id="123f8-184">SQL Database 伺服器的 [防火牆設定] 頁面隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="123f8-184">The **Firewall settings** page for the SQL Database server opens.</span></span> 

   ![伺服器防火牆規則](./media/sql-database-get-started-portal/server-firewall-rule.png) 


3. <span data-ttu-id="123f8-186">按一下工具列上的 [新增用戶端 IP]，將目前的 IP 位址新增至新的防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="123f8-186">Click **Add client IP** on the toolbar to add your current IP address to a new firewall rule.</span></span> <span data-ttu-id="123f8-187">防火牆規則可以針對單一 IP 位址或 IP 位址範圍開啟連接埠 1433。</span><span class="sxs-lookup"><span data-stu-id="123f8-187">A firewall rule can open port 1433 for a single IP address or a range of IP addresses.</span></span>

4. <span data-ttu-id="123f8-188">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="123f8-188">Click **Save**.</span></span> <span data-ttu-id="123f8-189">系統便會為目前的 IP 位址建立伺服器層級防火牆規則，以便在邏輯伺服器上開啟連接埠 1433。</span><span class="sxs-lookup"><span data-stu-id="123f8-189">A server-level firewall rule is created for your current IP address opening port 1433 on the logical server.</span></span>

   ![設定伺服器防火牆規則](./media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. <span data-ttu-id="123f8-191">依序按一下 [確定]，然後關閉 [防火牆設定] 頁面。</span><span class="sxs-lookup"><span data-stu-id="123f8-191">Click **OK** and then close the **Firewall settings** page.</span></span>

<span data-ttu-id="123f8-192">您現在可以利用 SQL Server Management Studio 或選擇的其他工具，使用先前建立的伺服器管理帳戶從這個 IP 位址連線至 SQL Database 伺服器及其資料庫。</span><span class="sxs-lookup"><span data-stu-id="123f8-192">You can now connect to the SQL Database server and its databases using SQL Server Management Studio or another tool of your choice from this IP address using the server admin account created previously.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="123f8-193">根據預設，已對所有 Azure 服務啟用透過 SQL Database 防火牆存取。</span><span class="sxs-lookup"><span data-stu-id="123f8-193">By default, access through the SQL Database firewall is enabled for all Azure services.</span></span> <span data-ttu-id="123f8-194">按一下此頁面上的 [關閉] 即可對所有 Azure 服務停用。</span><span class="sxs-lookup"><span data-stu-id="123f8-194">Click **OFF** on this page to disable for all Azure services.</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="123f8-195">SQL Server 連線資訊</span><span class="sxs-lookup"><span data-stu-id="123f8-195">SQL server connection information</span></span>

<span data-ttu-id="123f8-196">在 Azure 入口網站中取得 Azure SQL Database 伺服器的完整伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="123f8-196">Get the fully qualified server name for your Azure SQL Database server in the Azure portal.</span></span> <span data-ttu-id="123f8-197">透過 SQL Server Management Studio，您可使用此完整伺服器名稱連接到您的伺服器。</span><span class="sxs-lookup"><span data-stu-id="123f8-197">You use the fully qualified server name to connect to your server using SQL Server Management Studio.</span></span>

1. <span data-ttu-id="123f8-198">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="123f8-198">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="123f8-199">從左側功能表中選取 [SQL Database]，按一下 [SQL Database]頁面上您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="123f8-199">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="123f8-200">在 Azure 入口網站中您資料庫的 [基本資訊] 窗格中，找到後複製 [伺服器名稱]。</span><span class="sxs-lookup"><span data-stu-id="123f8-200">In the **Essentials** pane in the Azure portal page for your database, locate and then copy the **Server name**.</span></span>

   ![連線資訊](./media/sql-database-connect-query-dotnet/server-name.png)

## <a name="connect-to-the-database-with-ssms"></a><span data-ttu-id="123f8-202">使用 SSMS 連接到資料庫</span><span class="sxs-lookup"><span data-stu-id="123f8-202">Connect to the database with SSMS</span></span>

<span data-ttu-id="123f8-203">使用 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) 建立對 Azure SQL Database 伺服器的連線。</span><span class="sxs-lookup"><span data-stu-id="123f8-203">Use [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) to establish a connection to your Azure SQL Database server.</span></span>

1. <span data-ttu-id="123f8-204">開啟 SQL Server Management Studio。</span><span class="sxs-lookup"><span data-stu-id="123f8-204">Open SQL Server Management Studio.</span></span>

2. <span data-ttu-id="123f8-205">在 [連接到伺服器] 對話方塊中，輸入下列資訊：</span><span class="sxs-lookup"><span data-stu-id="123f8-205">In the **Connect to Server** dialog box, enter the following information:</span></span>

   | <span data-ttu-id="123f8-206">設定</span><span class="sxs-lookup"><span data-stu-id="123f8-206">Setting</span></span>       | <span data-ttu-id="123f8-207">建議的值</span><span class="sxs-lookup"><span data-stu-id="123f8-207">Suggested value</span></span> | <span data-ttu-id="123f8-208">說明</span><span class="sxs-lookup"><span data-stu-id="123f8-208">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="123f8-209">伺服器類型</span><span class="sxs-lookup"><span data-stu-id="123f8-209">Server type</span></span> | <span data-ttu-id="123f8-210">資料庫引擎</span><span class="sxs-lookup"><span data-stu-id="123f8-210">Database engine</span></span> | <span data-ttu-id="123f8-211">這是必要值</span><span class="sxs-lookup"><span data-stu-id="123f8-211">This value is required</span></span> |
   | <span data-ttu-id="123f8-212">伺服器名稱</span><span class="sxs-lookup"><span data-stu-id="123f8-212">Server name</span></span> | <span data-ttu-id="123f8-213">完整伺服器名稱</span><span class="sxs-lookup"><span data-stu-id="123f8-213">The fully qualified server name</span></span> | <span data-ttu-id="123f8-214">此名稱應該類似這樣︰**mynewserver20170313.database.windows.net**。</span><span class="sxs-lookup"><span data-stu-id="123f8-214">The name should be something like this: **mynewserver20170313.database.windows.net**.</span></span> |
   | <span data-ttu-id="123f8-215">驗證</span><span class="sxs-lookup"><span data-stu-id="123f8-215">Authentication</span></span> | <span data-ttu-id="123f8-216">SQL Server 驗證</span><span class="sxs-lookup"><span data-stu-id="123f8-216">SQL Server Authentication</span></span> | <span data-ttu-id="123f8-217">在本教學課程中，我們只設定了 SQL 驗證這個驗證類型。</span><span class="sxs-lookup"><span data-stu-id="123f8-217">SQL Authentication is the only authentication type that we have configured in this tutorial.</span></span> |
   | <span data-ttu-id="123f8-218">登入</span><span class="sxs-lookup"><span data-stu-id="123f8-218">Login</span></span> | <span data-ttu-id="123f8-219">伺服器管理帳戶</span><span class="sxs-lookup"><span data-stu-id="123f8-219">The server admin account</span></span> | <span data-ttu-id="123f8-220">這是您在建立伺服器時所指定的帳戶。</span><span class="sxs-lookup"><span data-stu-id="123f8-220">This is the account that you specified when you created the server.</span></span> |
   | <span data-ttu-id="123f8-221">密碼</span><span class="sxs-lookup"><span data-stu-id="123f8-221">Password</span></span> | <span data-ttu-id="123f8-222">伺服器管理帳戶的密碼</span><span class="sxs-lookup"><span data-stu-id="123f8-222">The password for your server admin account</span></span> | <span data-ttu-id="123f8-223">這是您在建立伺服器時所指定的密碼。</span><span class="sxs-lookup"><span data-stu-id="123f8-223">This is the password that you specified when you created the server.</span></span> |

   ![連接到伺服器](./media/sql-database-connect-query-ssms/connect.png)

3. <span data-ttu-id="123f8-225">按一下 [連接到伺服器] 對話方塊中的 [選項]。</span><span class="sxs-lookup"><span data-stu-id="123f8-225">Click **Options** in the **Connect to server** dialog box.</span></span> <span data-ttu-id="123f8-226">在 [連線到資料庫] 區段中，輸入 **mySampleDatabase** 以連線到這個資料庫。</span><span class="sxs-lookup"><span data-stu-id="123f8-226">In the **Connect to database** section, enter **mySampleDatabase** to connect to this database.</span></span>

   ![連線到伺服器上的 DB](./media/sql-database-connect-query-ssms/options-connect-to-db.png)  

4. <span data-ttu-id="123f8-228">按一下 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="123f8-228">Click **Connect**.</span></span> <span data-ttu-id="123f8-229">[物件總管] 視窗隨即在 SSMS 中開啟。</span><span class="sxs-lookup"><span data-stu-id="123f8-229">The Object Explorer window opens in SSMS.</span></span> 

5. <span data-ttu-id="123f8-230">在 [物件總管] 中，展開 [資料庫]，然後展開 [mySampleDatabase] 以檢視範例資料庫中的物件。</span><span class="sxs-lookup"><span data-stu-id="123f8-230">In Object Explorer, expand **Databases** and then expand **mySampleDatabase** to view the objects in the sample database.</span></span>

   ![資料庫物件](./media/sql-database-connect-query-ssms/connected.png)  

## <a name="create-tables-in-the-database"></a><span data-ttu-id="123f8-232">在資料庫中建立資料表</span><span class="sxs-lookup"><span data-stu-id="123f8-232">Create tables in the database</span></span> 

<span data-ttu-id="123f8-233">使用四個資料表建立資料庫結構描述，其會使用 [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference) 建立大學的學生管理系統模型：</span><span class="sxs-lookup"><span data-stu-id="123f8-233">Create a database schema with four tables that model a student management system for universities using [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference):</span></span>

- <span data-ttu-id="123f8-234">Person</span><span class="sxs-lookup"><span data-stu-id="123f8-234">Person</span></span>
- <span data-ttu-id="123f8-235">課程</span><span class="sxs-lookup"><span data-stu-id="123f8-235">Course</span></span>
- <span data-ttu-id="123f8-236">學生</span><span class="sxs-lookup"><span data-stu-id="123f8-236">Student</span></span>
- <span data-ttu-id="123f8-237">建立大學專屬學生管理系統的信用額度</span><span class="sxs-lookup"><span data-stu-id="123f8-237">Credit that model a student management system for universities</span></span>

<span data-ttu-id="123f8-238">下圖顯示這些資料表是如何彼此相互關聯。</span><span class="sxs-lookup"><span data-stu-id="123f8-238">The following diagram shows how these tables are related to each other.</span></span> <span data-ttu-id="123f8-239">在這當中有部分資料表會參考其他資料表的資料欄。</span><span class="sxs-lookup"><span data-stu-id="123f8-239">Some of these tables reference columns in other tables.</span></span> <span data-ttu-id="123f8-240">例如，[Student (學生)] 資料表會參考 [Person (人員)] 資料表的 [PersonId] 資料欄。</span><span class="sxs-lookup"><span data-stu-id="123f8-240">For example, the Student table references the **PersonId** column of the **Person** table.</span></span> <span data-ttu-id="123f8-241">研究圖表，以了解在本教學課程中資料表彼此關連的方式。</span><span class="sxs-lookup"><span data-stu-id="123f8-241">Study the diagram to understand how the tables in this tutorial are related to one another.</span></span> <span data-ttu-id="123f8-242">如需深入了解建立有效資料庫資料表的方式，請參閱[建立有效資料庫資料表 ](https://msdn.microsoft.com/library/cc505842.aspx)。</span><span class="sxs-lookup"><span data-stu-id="123f8-242">For an in-depth look at how to create effective database tables, see [Create effective database tables](https://msdn.microsoft.com/library/cc505842.aspx).</span></span> <span data-ttu-id="123f8-243">如需選擇資料類型的相關資訊，請參閱[資料類型 (英文)](https://docs.microsoft.com/sql/t-sql/data-types/data-types-transact-sql)。</span><span class="sxs-lookup"><span data-stu-id="123f8-243">For information about choosing data types, see [Data types](https://docs.microsoft.com/sql/t-sql/data-types/data-types-transact-sql).</span></span>

> [!NOTE]
> <span data-ttu-id="123f8-244">您亦可使用 [SQL Server Management Studio 中的資料表設計工具](https://msdn.microsoft.com/library/hh272695.aspx)，建立和設計您的資料表。</span><span class="sxs-lookup"><span data-stu-id="123f8-244">You can also use the [table designer in SQL Server Management Studio](https://msdn.microsoft.com/library/hh272695.aspx) to create and design your tables.</span></span> 

![資料表關聯性](./media/sql-database-design-first-database/tutorial-database-tables.png)

1. <span data-ttu-id="123f8-246">在 [物件總管] 中，於 **mySampleDatabase** 上按一下滑鼠右鍵，然後按一下 [新增查詢]。</span><span class="sxs-lookup"><span data-stu-id="123f8-246">In Object Explorer, right-click **mySampleDatabase** and click **New Query**.</span></span> <span data-ttu-id="123f8-247">隨即開啟已連線到您資料庫的空白查詢視窗。</span><span class="sxs-lookup"><span data-stu-id="123f8-247">A blank query window opens that is connected to your database.</span></span>

2. <span data-ttu-id="123f8-248">在查詢視窗中，執行下列查詢以在資料庫中建立四個資料表︰</span><span class="sxs-lookup"><span data-stu-id="123f8-248">In the query window, execute the following query to create four tables in your database:</span></span> 

   ```sql 
   -- Create Person table

   CREATE TABLE Person
   (
   PersonId   INT IDENTITY PRIMARY KEY,
   FirstName   NVARCHAR(128) NOT NULL,
   MiddelInitial NVARCHAR(10),
   LastName   NVARCHAR(128) NOT NULL,
   DateOfBirth   DATE NOT NULL
   )
   
   -- Create Student table
 
   CREATE TABLE Student
   (
   StudentId INT IDENTITY PRIMARY KEY,
   PersonId  INT REFERENCES Person (PersonId),
   Email   NVARCHAR(256)
   )
   
   -- Create Course table
 
   CREATE TABLE Course
   (
   CourseId  INT IDENTITY PRIMARY KEY,
   Name   NVARCHAR(50) NOT NULL,
   Teacher   NVARCHAR(256) NOT NULL
   ) 

   -- Create Credit table
 
   CREATE TABLE Credit
   (
   StudentId   INT REFERENCES Student (StudentId),
   CourseId   INT REFERENCES Course (CourseId),
   Grade   DECIMAL(5,2) CHECK (Grade <= 100.00),
   Attempt   TINYINT,
   CONSTRAINT  [UQ_studentgrades] UNIQUE CLUSTERED
   (
   StudentId, CourseId, Grade, Attempt
   )
   )
   ```

   ![建立資料表](./media/sql-database-design-first-database/create-tables.png)

3. <span data-ttu-id="123f8-250">在 SQL Server Management Studio 物件總管中展開「資料表」節點，以查看您建立的資料表。</span><span class="sxs-lookup"><span data-stu-id="123f8-250">Expand the 'tables' node in the SQL Server Management Studio Object explorer to see the tables you created.</span></span>

   ![建立 ssms 資料表](./media/sql-database-design-first-database/ssms-tables-created.png)

## <a name="load-data-into-the-tables"></a><span data-ttu-id="123f8-252">將資料載入到資料表</span><span class="sxs-lookup"><span data-stu-id="123f8-252">Load data into the tables</span></span>

1. <span data-ttu-id="123f8-253">在 [下載] 資料夾中建立一個名為 **SampleTableData** 的資料夾，以存放您資料庫的範例資料。</span><span class="sxs-lookup"><span data-stu-id="123f8-253">Create a folder called **SampleTableData** in your Downloads folder to store sample data for your database.</span></span> 

2. <span data-ttu-id="123f8-254">以滑鼠右鍵按一下下列連結，將其儲存至 **SampleTableData** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="123f8-254">Right-click the following links and save them into the **SampleTableData** folder.</span></span> 

   - [<span data-ttu-id="123f8-255">SampleCourseData</span><span class="sxs-lookup"><span data-stu-id="123f8-255">SampleCourseData</span></span>](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleCourseData)
   - [<span data-ttu-id="123f8-256">SamplePersonData</span><span class="sxs-lookup"><span data-stu-id="123f8-256">SamplePersonData</span></span>](https://sqldbtutorial.blob.core.windows.net/tutorials/SamplePersonData)
   - [<span data-ttu-id="123f8-257">SampleStudentData</span><span class="sxs-lookup"><span data-stu-id="123f8-257">SampleStudentData</span></span>](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleStudentData)
   - [<span data-ttu-id="123f8-258">SampleCreditData</span><span class="sxs-lookup"><span data-stu-id="123f8-258">SampleCreditData</span></span>](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleCreditData)

3. <span data-ttu-id="123f8-259">開啟命令提示字元視窗，並瀏覽至 SampleTableData 資料夾。</span><span class="sxs-lookup"><span data-stu-id="123f8-259">Open a command prompt window and navigate to the SampleTableData folder.</span></span>

4. <span data-ttu-id="123f8-260">執行下列命令以將範例資料列插入至資料表中，其中以適用於您環境的值取代 **ServerName**、**DatabaseName**、**UserName** 及 **Password** 的值。</span><span class="sxs-lookup"><span data-stu-id="123f8-260">Execute the following commands to insert sample data into the tables replacing the values for **ServerName**, **DatabaseName**, **UserName**, and **Password** with the values for your environment.</span></span>
  
   ```bcp
   bcp Course in SampleCourseData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Person in SamplePersonData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Student in SampleStudentData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Credit in SampleCreditData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   ```

<span data-ttu-id="123f8-261">您現在已將範例資料載入至先前建立的資料表。</span><span class="sxs-lookup"><span data-stu-id="123f8-261">You have now loaded sample data into the tables you created earlier.</span></span>

## <a name="query-data"></a><span data-ttu-id="123f8-262">查詢資料</span><span class="sxs-lookup"><span data-stu-id="123f8-262">Query data</span></span>

<span data-ttu-id="123f8-263">執行下列查詢，以從資料庫資料表中擷取資訊。</span><span class="sxs-lookup"><span data-stu-id="123f8-263">Execute the following queries to retrieve information from the database tables.</span></span> <span data-ttu-id="123f8-264">如需深入了解關於撰寫 SQL 查詢的資訊，請參閱[撰寫 SQL 查詢 (英文)](https://technet.microsoft.com/library/bb264565.aspx)。</span><span class="sxs-lookup"><span data-stu-id="123f8-264">See [Writing SQL Queries](https://technet.microsoft.com/library/bb264565.aspx) to learn more about writing SQL queries.</span></span> <span data-ttu-id="123f8-265">第一個查詢會聯結所有四個資料表，以尋找由「Dominick Pope」授課且成績高於全班 75% 學生的所有學生。</span><span class="sxs-lookup"><span data-stu-id="123f8-265">The first query joins all four tables to find all the students taught by 'Dominick Pope' who have a grade higher than 75% in his class.</span></span> <span data-ttu-id="123f8-266">第二個查詢會連結所有四個資料表，以尋找「Noe Coleman」曾註冊的所有課程。</span><span class="sxs-lookup"><span data-stu-id="123f8-266">The second query joins all four tables and finds all courses in which 'Noe Coleman' has ever enrolled.</span></span>

1. <span data-ttu-id="123f8-267">在 [SQL Server Management Studio] 查詢視窗中，執行下列查詢︰</span><span class="sxs-lookup"><span data-stu-id="123f8-267">In a SQL Server Management Studio query window, execute the following query:</span></span>

   ```sql 
   -- Find the students taught by Dominick Pope who have a grade higher than 75%

   SELECT  person.FirstName,
   person.LastName,
   course.Name,
   credit.Grade
   FROM  Person AS person
   INNER JOIN Student AS student ON person.PersonId = student.PersonId
   INNER JOIN Credit AS credit ON student.StudentId = credit.StudentId
   INNER JOIN Course AS course ON credit.CourseId = course.courseId
   WHERE course.Teacher = 'Dominick Pope' 
   AND Grade > 75
   ```

2. <span data-ttu-id="123f8-268">在 [SQL Server Management Studio] 查詢視窗中，執行下列查詢︰</span><span class="sxs-lookup"><span data-stu-id="123f8-268">In a SQL Server Management Studio query window, execute following query:</span></span>

   ```sql
   -- Find all the courses in which Noe Coleman has ever enrolled

   SELECT  course.Name,
   course.Teacher,
   credit.Grade
   FROM  Course AS course
   INNER JOIN Credit AS credit ON credit.CourseId = course.CourseId
   INNER JOIN Student AS student ON student.StudentId = credit.StudentId
   INNER JOIN Person AS person ON person.PersonId = student.PersonId
   WHERE person.FirstName = 'Noe'
   AND person.LastName = 'Coleman'
   ```

## <a name="restore-a-database-to-a-previous-point-in-time"></a><span data-ttu-id="123f8-269">將資料庫還原至先前的時間點</span><span class="sxs-lookup"><span data-stu-id="123f8-269">Restore a database to a previous point in time</span></span>

<span data-ttu-id="123f8-270">假設您不小心刪除了資料表。</span><span class="sxs-lookup"><span data-stu-id="123f8-270">Imagine you have accidentally deleted a table.</span></span> <span data-ttu-id="123f8-271">這是您無法輕易復原的情況。</span><span class="sxs-lookup"><span data-stu-id="123f8-271">This is something you cannot easily recover from.</span></span> <span data-ttu-id="123f8-272">Azure SQL Database 可讓您返回至最長過去 35 天內的任何時間點，並將此時間點還原至新資料庫。</span><span class="sxs-lookup"><span data-stu-id="123f8-272">Azure SQL Database allows you to go back to any point in time in the last up to 35 days and restore this point in time to a new database.</span></span> <span data-ttu-id="123f8-273">您可使用此資料庫來復原已刪除的資料。</span><span class="sxs-lookup"><span data-stu-id="123f8-273">You can you this database to recover your deleted data.</span></span> <span data-ttu-id="123f8-274">下列步驟會將範例資料庫還原至新增資料表之前的時間點。</span><span class="sxs-lookup"><span data-stu-id="123f8-274">The following steps restore the sample database to a point before the tables were added.</span></span>

1. <span data-ttu-id="123f8-275">在資料庫的 [SQL Database] 頁面上，按一下工具列上的 [還原]。</span><span class="sxs-lookup"><span data-stu-id="123f8-275">On the SQL Database page for your database, click **Restore** on the toolbar.</span></span> <span data-ttu-id="123f8-276">[還原] 頁面隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="123f8-276">The **Restore** page opens.</span></span>

   ![還原](./media/sql-database-design-first-database/restore.png)

2. <span data-ttu-id="123f8-278">在 [還原] 表單中填入必要資訊︰</span><span class="sxs-lookup"><span data-stu-id="123f8-278">Fill out the **Restore** form with the required information:</span></span>
    * <span data-ttu-id="123f8-279">資料庫名稱︰提供資料庫名稱</span><span class="sxs-lookup"><span data-stu-id="123f8-279">Database name: Provide a database name</span></span> 
    * <span data-ttu-id="123f8-280">時間點：選取 [還原] 表單上的 [時間點] 索引標籤</span><span class="sxs-lookup"><span data-stu-id="123f8-280">Point-in-time: Select the **Point-in-time** tab on the Restore form</span></span> 
    * <span data-ttu-id="123f8-281">還原點：選取一個在變更資料庫之前的時間</span><span class="sxs-lookup"><span data-stu-id="123f8-281">Restore point: Select a time that occurs before the database was changed</span></span>
    * <span data-ttu-id="123f8-282">目標伺服器︰還原資料庫時，您無法變更此值</span><span class="sxs-lookup"><span data-stu-id="123f8-282">Target server: You cannot change this value when restoring a database</span></span> 
    * <span data-ttu-id="123f8-283">彈性資料庫集區：選取 [無]</span><span class="sxs-lookup"><span data-stu-id="123f8-283">Elastic database pool: Select **None**</span></span>  
    * <span data-ttu-id="123f8-284">定價層：選取 [20 DTU] 和 [250 GB] 的儲存體。</span><span class="sxs-lookup"><span data-stu-id="123f8-284">Pricing tier: Select **20 DTUs** and **250 GB** of storage.</span></span>

   ![還原點](./media/sql-database-design-first-database/restore-point.png)

3. <span data-ttu-id="123f8-286">按一下 [確定]，以將資料庫[還原至新增資料表之前的時間點](sql-database-recovery-using-backups.md#point-in-time-restore)。</span><span class="sxs-lookup"><span data-stu-id="123f8-286">Click **OK** to restore the database to [restore to a point in time](sql-database-recovery-using-backups.md#point-in-time-restore) before the tables were added.</span></span> <span data-ttu-id="123f8-287">若將資料庫還原至不同的時間點，系統即會從您指定的時間點 (只要位於[服務層](sql-database-service-tiers.md)的保留期限內) 開始，在與原始資料庫相同的伺服器中建立重複的資料庫。</span><span class="sxs-lookup"><span data-stu-id="123f8-287">Restoring a database to a different point in time creates a duplicate database in the same server as the original database as of the point in time you specify, as long as it is within the retention period for your [service tier](sql-database-service-tiers.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="123f8-288">後續步驟</span><span class="sxs-lookup"><span data-stu-id="123f8-288">Next Steps</span></span> 
<span data-ttu-id="123f8-289">在本教學課程中，您已了解基本的資料庫工作，例如建立資料庫和資料表、載入和查詢資料，以及將資料庫還原至先前的時間點。</span><span class="sxs-lookup"><span data-stu-id="123f8-289">In this tutorial, you learned basic database tasks such as create a database and tables, load and query data, and restore the database to a previous point in time.</span></span> <span data-ttu-id="123f8-290">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="123f8-290">You learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="123f8-291">建立資料庫</span><span class="sxs-lookup"><span data-stu-id="123f8-291">Create a database</span></span>
> * <span data-ttu-id="123f8-292">設定防火牆規則</span><span class="sxs-lookup"><span data-stu-id="123f8-292">Set up a firewall rule</span></span>
> * <span data-ttu-id="123f8-293">使用 [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) 來連線到資料庫</span><span class="sxs-lookup"><span data-stu-id="123f8-293">Connect to the database with [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS)</span></span>
> * <span data-ttu-id="123f8-294">建立資料表</span><span class="sxs-lookup"><span data-stu-id="123f8-294">Create tables</span></span>
> * <span data-ttu-id="123f8-295">大量載入資料</span><span class="sxs-lookup"><span data-stu-id="123f8-295">Bulk load data</span></span>
> * <span data-ttu-id="123f8-296">查詢該資料</span><span class="sxs-lookup"><span data-stu-id="123f8-296">Query that data</span></span>
> * <span data-ttu-id="123f8-297">使用 SQL Database [還原時間點](sql-database-recovery-using-backups.md#point-in-time-restore)功能，將資料庫還原至先前的時間點</span><span class="sxs-lookup"><span data-stu-id="123f8-297">Restore the database to a previous point in time using SQL Database [point in time restore](sql-database-recovery-using-backups.md#point-in-time-restore) capabilities</span></span>

<span data-ttu-id="123f8-298">前進到下一個教學課程，了解如何使用 Visual Studio 和 C# 設計資料庫。</span><span class="sxs-lookup"><span data-stu-id="123f8-298">Advance to the next tutorial to learn about designing a database using Visual Studio and C#.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="123f8-299">設計 Azure SQL Database 並連接 C# 和 ADO.NET</span><span class="sxs-lookup"><span data-stu-id="123f8-299">Design an Azure SQL database and connect with C# and ADO.NET</span></span>](sql-database-design-first-database-csharp.md)
