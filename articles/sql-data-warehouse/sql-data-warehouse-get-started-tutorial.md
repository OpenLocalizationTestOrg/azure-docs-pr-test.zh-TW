---
title: "Azure SQL 資料倉儲 - 快速入門教學課程 | Microsoft Docs"
description: "本教學課程會教您如何佈建，並將資料載入 Azure SQL 資料倉儲。 您也將學習調整、暫停和微調的基本概念。"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: barbkess
ms.assetid: 52DFC191-E094-4B04-893F-B64D5828A900
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: quickstart
ms.date: 01/26/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: 95e14824ba3b705bb909ec983652dd3305b98805
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-sql-data-warehouse"></a><span data-ttu-id="3de2e-104">開始使用 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="3de2e-104">Get started with SQL Data Warehouse</span></span>

<span data-ttu-id="3de2e-105">本教學課程會說明如何佈建，並將資料載入 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="3de2e-105">This tutorial shows how to provision and load data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="3de2e-106">您也將學習調整、暫停和微調的基本概念。</span><span class="sxs-lookup"><span data-stu-id="3de2e-106">You’ll also learn the basics about scaling, pausing, and tuning.</span></span> <span data-ttu-id="3de2e-107">完成時，您就能查詢及瀏覽資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="3de2e-107">When you’re finished, you’ll be ready to query and explore your data warehouse.</span></span>

<span data-ttu-id="3de2e-108">**預估完成時間︰**這是內含範例程式碼的端對端教學課程，在您完成必要條件後，需耗時約 30 分鐘才能完成。</span><span class="sxs-lookup"><span data-stu-id="3de2e-108">**Estimated time to complete:** This is an end-to-end tutorial with example code that takes about 30 minutes to complete once you have met the prerequisites.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3de2e-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="3de2e-109">Prerequisites</span></span>

<span data-ttu-id="3de2e-110">此教學課程假設您熟悉 SQL 資料倉儲基本概念。</span><span class="sxs-lookup"><span data-stu-id="3de2e-110">The tutorial assumes you are familiar with SQL Data Warehouse basic concepts.</span></span> <span data-ttu-id="3de2e-111">如果您需要簡介，請參閱[什麼是 SQL 資料倉儲？](sql-data-warehouse-overview-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="3de2e-111">If you need an introduction, see [What is SQL Data Warehouse?](sql-data-warehouse-overview-what-is.md)</span></span> 

### <a name="sign-up-for-microsoft-azure"></a><span data-ttu-id="3de2e-112">註冊 Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="3de2e-112">Sign up for Microsoft Azure</span></span>
<span data-ttu-id="3de2e-113">如果您還沒有 Microsoft Azure 帳戶，則必須註冊帳戶才能使用這項服務。</span><span class="sxs-lookup"><span data-stu-id="3de2e-113">If you don't already have a Microsoft Azure account, you need to sign up for one to use this service.</span></span> <span data-ttu-id="3de2e-114">如果您已經有帳戶，則可以跳過此步驟。</span><span class="sxs-lookup"><span data-stu-id="3de2e-114">If you already have an account, you may skip this step.</span></span> 

1. <span data-ttu-id="3de2e-115">瀏覽至帳戶頁面 [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)</span><span class="sxs-lookup"><span data-stu-id="3de2e-115">Navigate to the account pages [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)</span></span>
2. <span data-ttu-id="3de2e-116">建立免費的 Azure 帳戶，或購買帳戶。</span><span class="sxs-lookup"><span data-stu-id="3de2e-116">Create a free Azure account, or purchase an account.</span></span>
3. <span data-ttu-id="3de2e-117">遵循指示進行</span><span class="sxs-lookup"><span data-stu-id="3de2e-117">Follow the instructions</span></span>

### <a name="install-appropriate-sql-client-drivers-and-tools"></a><span data-ttu-id="3de2e-118">安裝適當的 SQL 用戶端驅動程式和工具</span><span class="sxs-lookup"><span data-stu-id="3de2e-118">Install appropriate SQL client drivers and tools</span></span>

<span data-ttu-id="3de2e-119">大部分的 SQL 用戶端工具都可以使用 JDBC、ODBC 或 ADO.net 連線到 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="3de2e-119">Most SQL client tools can connect to SQL Data Warehouse by using JDBC, ODBC, or ADO.NET.</span></span> <span data-ttu-id="3de2e-120">由於 SQL 資料倉儲支援大量 T-SQL 功能，部分用戶端應用程式不會與 SQL 資料倉儲完全相容。</span><span class="sxs-lookup"><span data-stu-id="3de2e-120">Due to the large number of T-SQL features that SQL Data Warehouse supports, some client applications are not fully compatible with SQL Data Warehouse.</span></span>

<span data-ttu-id="3de2e-121">如果您執行的是 Windows 作業系統，建議您使用 [Visual Studio] 或 [SQL Server Management Studio]。</span><span class="sxs-lookup"><span data-stu-id="3de2e-121">If you are running a Windows operating system, we recommend using either [Visual Studio] or [SQL Server Management Studio].</span></span>

[!INCLUDE [Create a new logical server](../../includes/sql-data-warehouse-create-logical-server.md)] 

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="3de2e-122">建立 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="3de2e-122">Create a SQL Data Warehouse</span></span>

<span data-ttu-id="3de2e-123">SQL 資料倉儲是一種特殊類型的資料庫，其設計用來進行大量平行處理。</span><span class="sxs-lookup"><span data-stu-id="3de2e-123">A SQL Data Warehouse is a special type of database that is designed for massively parallel processing.</span></span> <span data-ttu-id="3de2e-124">將跨多個節點分散資料庫，且資料庫可平行處理查詢。</span><span class="sxs-lookup"><span data-stu-id="3de2e-124">The database is distributed across multiple nodes and processes queries in parallel.</span></span> <span data-ttu-id="3de2e-125">SQL 資料倉儲具有控制節點，其可協調所有節點的活動。</span><span class="sxs-lookup"><span data-stu-id="3de2e-125">SQL Data Warehouse has a control node that orchestrates the activities of all the nodes.</span></span> <span data-ttu-id="3de2e-126">節點本身會使用 SQL Database 來管理資料。</span><span class="sxs-lookup"><span data-stu-id="3de2e-126">The nodes themselves use SQL Database to manage your data.</span></span>  

> [!NOTE]
> <span data-ttu-id="3de2e-127">建立 SQL 資料倉儲可能會導致新的可計費服務。</span><span class="sxs-lookup"><span data-stu-id="3de2e-127">Creating a SQL Data Warehouse might result in a new billable service.</span></span>  <span data-ttu-id="3de2e-128">如需詳細資訊，請參閱 [SQL 資料倉儲價格](https://azure.microsoft.com/pricing/details/sql-data-warehouse/)。</span><span class="sxs-lookup"><span data-stu-id="3de2e-128">For more information, see [SQL Data Warehouse pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>
>

### <a name="create-a-data-warehouse"></a><span data-ttu-id="3de2e-129">建立資料倉儲</span><span class="sxs-lookup"><span data-stu-id="3de2e-129">Create a data warehouse</span></span>

1. <span data-ttu-id="3de2e-130">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="3de2e-130">Sign into the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3de2e-131">按一下 [新增] > [資料庫] > [SQL 資料倉儲]。</span><span class="sxs-lookup"><span data-stu-id="3de2e-131">Click **New** > **Databases** > **SQL Data Warehouse**.</span></span>

    <span data-ttu-id="3de2e-132">![NewBlade](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png) ![SelectDW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)</span><span class="sxs-lookup"><span data-stu-id="3de2e-132">![NewBlade](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png) ![SelectDW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)</span></span>

3. <span data-ttu-id="3de2e-133">填寫部署詳細資料</span><span class="sxs-lookup"><span data-stu-id="3de2e-133">Fill out deployment details</span></span>

    <span data-ttu-id="3de2e-134">**資料庫名稱**︰挑選您想要的名稱。</span><span class="sxs-lookup"><span data-stu-id="3de2e-134">**Database Name**: Pick anything you'd like.</span></span> <span data-ttu-id="3de2e-135">如果您有多個資料倉儲，建議您在名稱中包含詳細資料，例如其區域、環境等，例如 *mydw-westus-1-test*。</span><span class="sxs-lookup"><span data-stu-id="3de2e-135">If you have multiple data warehouses, we recommend your names include details such as the region, environment, for example *mydw-westus-1-test*.</span></span>

    <span data-ttu-id="3de2e-136">**訂用帳戶**：您的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3de2e-136">**Subscription**: Your Azure subscription</span></span>

    <span data-ttu-id="3de2e-137">**資源群組**：建立新的資源群組，或使用現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="3de2e-137">**Resource Group**: Create a resource group or use an existing resource group.</span></span>
    > [!NOTE]
    > <span data-ttu-id="3de2e-138">資源群組適合用來管理資源，例如界定存取控制和樣板化部署的範圍。</span><span class="sxs-lookup"><span data-stu-id="3de2e-138">Resource groups are useful for resource administration such as scoping access control and templated deployment.</span></span> <span data-ttu-id="3de2e-139">您可以[在此](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)深入了解 Azure 資源群組和最佳作法</span><span class="sxs-lookup"><span data-stu-id="3de2e-139">Read more about Azure resource groups and best practices [here](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)</span></span>

    <span data-ttu-id="3de2e-140">**來源**：空白資料庫</span><span class="sxs-lookup"><span data-stu-id="3de2e-140">**Source**: Blank Database</span></span>

    <span data-ttu-id="3de2e-141">**伺服器**︰選取您在[必要條件]中建立的伺服器。</span><span class="sxs-lookup"><span data-stu-id="3de2e-141">**Server**: Select the server you created in [Prerequisites].</span></span>

    <span data-ttu-id="3de2e-142">**定序**：保留預設定序 SQL_Latin1_General_CP1_CI_AS。</span><span class="sxs-lookup"><span data-stu-id="3de2e-142">**Collation**: Leave the default collation SQL_Latin1_General_CP1_CI_AS.</span></span>

    <span data-ttu-id="3de2e-143">**選取效能**︰建議您使用標準的 400 DWU。</span><span class="sxs-lookup"><span data-stu-id="3de2e-143">**Select performance**: We recommend starting with the standard 400DWU.</span></span>

4. <span data-ttu-id="3de2e-144">選擇 [釘選到儀表板] ![釘選到儀表板](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="3de2e-144">Choose **Pin to dashboard** ![Pin To Dashboard](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)</span></span>

5. <span data-ttu-id="3de2e-145">稍候一會，讓資料倉儲進行部署！</span><span class="sxs-lookup"><span data-stu-id="3de2e-145">Sit back and wait for your data warehouse to deploy!</span></span> <span data-ttu-id="3de2e-146">正常來說，此程序需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="3de2e-146">It's normal for this process to take several minutes.</span></span> <span data-ttu-id="3de2e-147">資料倉儲可供使用時，入口網站會通知您。</span><span class="sxs-lookup"><span data-stu-id="3de2e-147">The portal notifies you when your data warehouse is ready to use.</span></span> 

## <a name="connect-to-sql-data-warehouse"></a><span data-ttu-id="3de2e-148">連線到 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="3de2e-148">Connect to SQL Data Warehouse</span></span>

<span data-ttu-id="3de2e-149">本教學課程使用 SQL Server Management Studio (SSMS) 來連線到資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="3de2e-149">This tutorial uses SQL Server Management Studio (SSMS) to connect to the data warehouse.</span></span> <span data-ttu-id="3de2e-150">您透過下列支援連接器連線到 SQL 資料倉儲︰ADO.NET、JDBC、ODBC 和 PHP。</span><span class="sxs-lookup"><span data-stu-id="3de2e-150">You can connect to SQL Data Warehouse through these supported connectors: ADO.NET, JDBC, ODBC, and PHP.</span></span> <span data-ttu-id="3de2e-151">請記住，非 Microsoft 支援工具的功能可能會受限。</span><span class="sxs-lookup"><span data-stu-id="3de2e-151">Remember, functionality might be limited for tools that are not supported by Microsoft.</span></span>


### <a name="get-connection-information"></a><span data-ttu-id="3de2e-152">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="3de2e-152">Get connection information</span></span>

<span data-ttu-id="3de2e-153">若要連線到資料倉儲，您必須透過在[必要條件]中所建立的邏輯 SQL Server 進行連線。</span><span class="sxs-lookup"><span data-stu-id="3de2e-153">To connect to your data warehouse, you need to connect through the logical SQL server you created in [Prerequisites].</span></span>

1. <span data-ttu-id="3de2e-154">從儀表板選取資料倉儲，或在您的資源中進行搜尋。</span><span class="sxs-lookup"><span data-stu-id="3de2e-154">Select your data warehouse from the dashboard or search for it in your resources.</span></span>

    ![SQL 資料倉儲儀表板](./media/sql-data-warehouse-get-started-tutorial/sql-dw-dashboard.png)

2. <span data-ttu-id="3de2e-156">尋找邏輯 SQL Server 的完整名稱。</span><span class="sxs-lookup"><span data-stu-id="3de2e-156">Find the full name for the logical SQL server.</span></span>

    ![選取伺服器名稱](./media/sql-data-warehouse-get-started-tutorial/select-server.png)

3. <span data-ttu-id="3de2e-158">開啟 SSMS，並使用物件總管以使用您在[必要條件]中所建立的伺服器系統管理員認證連線到此伺服器</span><span class="sxs-lookup"><span data-stu-id="3de2e-158">Open SSMS and use object explorer to connect to this server using the server admin credentials you created in [Prerequisites]</span></span>

    ![以 SSMS 連線](./media/sql-data-warehouse-get-started-tutorial/ssms-connect.png)

<span data-ttu-id="3de2e-160">如果一切正常，您現在應該已連線到邏輯 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="3de2e-160">If all goes correctly, you should now be connected to your logical SQL server.</span></span> <span data-ttu-id="3de2e-161">因為您以伺服器系統管理員的身分登入，您可以連接到伺服器裝載的任何資料庫，包括主要資料庫。</span><span class="sxs-lookup"><span data-stu-id="3de2e-161">Since you logged in as the server admin, you can connect to any database hosted by the server, including the master database.</span></span> 

<span data-ttu-id="3de2e-162">只有一個伺服器系統管理帳戶，而且它有所有使用者的大部分權限。</span><span class="sxs-lookup"><span data-stu-id="3de2e-162">There is only one server admin account and it has the most privileges of any user.</span></span> <span data-ttu-id="3de2e-163">請小心不要讓組織中的太多人員知道管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="3de2e-163">Be careful not to allow too many people in your organization to know the admin password.</span></span> 

<span data-ttu-id="3de2e-164">您也可以擁有 Azure Active Directory 系統管理帳戶。</span><span class="sxs-lookup"><span data-stu-id="3de2e-164">You can also have an Azure active directory admin account.</span></span> <span data-ttu-id="3de2e-165">我們不會在此提供詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3de2e-165">We don't provide the details here.</span></span> <span data-ttu-id="3de2e-166">如果您想要進一步了解 Azure Active Directory 驗證的使用，請參閱 [Azure AD 驗證](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication)。</span><span class="sxs-lookup"><span data-stu-id="3de2e-166">If you want to learn more about using Azure Active Directory authentication, see [Azure AD authentication](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).</span></span>

<span data-ttu-id="3de2e-167">接下來，我們將探討建立其他登入和使用者。</span><span class="sxs-lookup"><span data-stu-id="3de2e-167">Next, we explore creating additional logins and users.</span></span>


## <a name="create-a-database-user"></a><span data-ttu-id="3de2e-168">建立資料庫使用者</span><span class="sxs-lookup"><span data-stu-id="3de2e-168">Create a database user</span></span>

<span data-ttu-id="3de2e-169">在此步驟中，您會建立使用者帳戶來存取資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="3de2e-169">In this step, you create a user account to access your data warehouse.</span></span> <span data-ttu-id="3de2e-170">我們也會說明如何讓使用者能夠執行需使用大量的記憶體和 CPU 資源的查詢。</span><span class="sxs-lookup"><span data-stu-id="3de2e-170">We also show you how to give that user the ability to run queries with a large amount of memory and CPU resources.</span></span>

### <a name="notes-about-resource-classes-for-allocating-resources-to-queries"></a><span data-ttu-id="3de2e-171">配置查詢資源之資源類別的相關事項</span><span class="sxs-lookup"><span data-stu-id="3de2e-171">Notes about resource classes for allocating resources to queries</span></span>

- <span data-ttu-id="3de2e-172">若要保護您的資料，請不要使用伺服器系統管理員對您的生產資料庫執行查詢。</span><span class="sxs-lookup"><span data-stu-id="3de2e-172">To keep your data safe, don't use the server admin to run queries on your production databases.</span></span> <span data-ttu-id="3de2e-173">它具有所有使用者的大部分權限，且使用它在使用者資料上執行作業會讓您的資料面臨風險。</span><span class="sxs-lookup"><span data-stu-id="3de2e-173">It has the most privileges of any user and using it to perform operations on user data puts your data at risk.</span></span> <span data-ttu-id="3de2e-174">此外，因為伺服器管理員是要執行管理作業，它僅會使用小型配置的記憶體和 CPU 資源來執行作業。</span><span class="sxs-lookup"><span data-stu-id="3de2e-174">Also, since the server admin is meant to perform management operations, it runs operations with only a small allocation of memory and CPU resources.</span></span> 

- <span data-ttu-id="3de2e-175">SQL 資料倉儲會使用預先定義的資料庫角色 (名為資源類別)，來配置記憶體、CPU 資源和並行存取插槽的不同數量的使用者。</span><span class="sxs-lookup"><span data-stu-id="3de2e-175">SQL Data Warehouse uses pre-defined database roles, called resource classes, to allocate different amounts of memory, CPU resources, and concurrency slots to users.</span></span> <span data-ttu-id="3de2e-176">每個使用者可屬於小型、中型、大型或超大型資源類別。</span><span class="sxs-lookup"><span data-stu-id="3de2e-176">Each user can belong to a small, medium, large, or extra-large resource class.</span></span> <span data-ttu-id="3de2e-177">使用者的資源類別會決定使用者執行查詢和載入作業所擁有的資源。</span><span class="sxs-lookup"><span data-stu-id="3de2e-177">The user's resource class determines the resources the user has to run queries and load operations.</span></span>

- <span data-ttu-id="3de2e-178">對於最佳資料壓縮，使用者必須載入大型或超大型資源配置。</span><span class="sxs-lookup"><span data-stu-id="3de2e-178">For optimal data compression, the user may need to load with large or extra large resource allocations.</span></span> <span data-ttu-id="3de2e-179">請[在此](./sql-data-warehouse-develop-concurrency.md#resource-classes)深入了解資源類別：</span><span class="sxs-lookup"><span data-stu-id="3de2e-179">Read more about resource classes [here](./sql-data-warehouse-develop-concurrency.md#resource-classes):</span></span>

### <a name="create-an-account-that-can-control-a-database"></a><span data-ttu-id="3de2e-180">建立一個可以控制資料庫的帳戶</span><span class="sxs-lookup"><span data-stu-id="3de2e-180">Create an account that can control a database</span></span>

<span data-ttu-id="3de2e-181">因為您目前以伺服器管理員的身分登入，即擁有建立登入和使用者的權限。</span><span class="sxs-lookup"><span data-stu-id="3de2e-181">Since you are currently logged in as the server admin you have permissions to create logins and users.</span></span>

1. <span data-ttu-id="3de2e-182">使用 SSMS 或另一個查詢用戶端，開啟對**主要**的新查詢。</span><span class="sxs-lookup"><span data-stu-id="3de2e-182">Using SSMS or another query client, open a new query for **master**.</span></span>

    ![主要資料庫上的新增查詢](./media/sql-data-warehouse-get-started-tutorial/query-on-server.png)

    ![主要資料庫上的新增查詢 1](./media/sql-data-warehouse-get-started-tutorial/query-on-master.png)

2. <span data-ttu-id="3de2e-185">在查詢視窗中，執行此 T-SQL 命令來建立名為 MedRCLogin 的登入以及名為 LoadingUser 的使用者。</span><span class="sxs-lookup"><span data-stu-id="3de2e-185">In the query window, run this T-SQL command to create a login named MedRCLogin and user named LoadingUser.</span></span> <span data-ttu-id="3de2e-186">此登入可以連接到邏輯 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="3de2e-186">This login can connect to the logical SQL server.</span></span>

    ```sql
    CREATE LOGIN MedRCLogin WITH PASSWORD = 'a123reallySTRONGpassword!';
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

3. <span data-ttu-id="3de2e-187">現在查詢 *SQL 資料倉儲資料庫*，根據您建立用來對資料庫存取和執行作業的登入來建立資料庫使用者。</span><span class="sxs-lookup"><span data-stu-id="3de2e-187">Now querying the *SQL Data Warehouse database*, create a database user based on the login you created to access and perform operations on the database.</span></span>

    ```sql
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

4. <span data-ttu-id="3de2e-188">提供資料庫使用者控制權限，讓其可控制名為 NYT 的資料庫。</span><span class="sxs-lookup"><span data-stu-id="3de2e-188">Give the database user control permissions to the database called NYT.</span></span> 

    ```sql
    GRANT CONTROL ON DATABASE::[NYT] to LoadingUser;
    ```
    > [!NOTE]
    > <span data-ttu-id="3de2e-189">如果資料庫名稱中有連字號，請務必以括弧括住！</span><span class="sxs-lookup"><span data-stu-id="3de2e-189">If your database name has hyphens in it, be sure to wrap it in brackets!</span></span> 
    >

### <a name="give-the-user-medium-resource-allocations"></a><span data-ttu-id="3de2e-190">提供使用者中型資源配置</span><span class="sxs-lookup"><span data-stu-id="3de2e-190">Give the user medium resource allocations</span></span>

1. <span data-ttu-id="3de2e-191">執行此 T-SQL 命令，使其成為名為 mediumrc 之中型資源類別的成員。</span><span class="sxs-lookup"><span data-stu-id="3de2e-191">Run this T-SQL command to make it a member of the medium resource class, which is called mediumrc.</span></span> 

    ```sql
    EXEC sp_addrolemember 'mediumrc', 'LoadingUser';
    ```
    > [!NOTE]
    > <span data-ttu-id="3de2e-192">按一下[這裡](sql-data-warehouse-develop-concurrency.md#resource-classes)以深入了解並行和資源類別！</span><span class="sxs-lookup"><span data-stu-id="3de2e-192">Click [here](sql-data-warehouse-develop-concurrency.md#resource-classes) to learn more about concurrency and resource classes!</span></span> 
    >

2. <span data-ttu-id="3de2e-193">使用新認證，連接到邏輯伺服器</span><span class="sxs-lookup"><span data-stu-id="3de2e-193">Connect to the logical server with the new credentials</span></span>

    ![使用新登入進行登入](./media/sql-data-warehouse-get-started-tutorial/new-login.png)


## <a name="load-data-from-azure-blob-storage"></a><span data-ttu-id="3de2e-195">從 Azure blob 儲存體載入資料</span><span class="sxs-lookup"><span data-stu-id="3de2e-195">Load data from Azure blob storage</span></span>

<span data-ttu-id="3de2e-196">現已可將資料載入資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="3de2e-196">You are now ready to load data into your data warehouse.</span></span> <span data-ttu-id="3de2e-197">此步驟說明如何從公用 Azure 儲存體 blob 載入紐約市計程車封包資料。</span><span class="sxs-lookup"><span data-stu-id="3de2e-197">This step shows you how to load New York City taxi cab data from a public Azure storage blob.</span></span> 

- <span data-ttu-id="3de2e-198">將資料載入 SQL 資料倉儲的常見方式是先將資料移至 Azure blob 儲存體，然後將其載入至資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="3de2e-198">A common way to load data into SQL Data Warehouse is to first move the data to Azure blob storage, and then load it into your data warehouse.</span></span> <span data-ttu-id="3de2e-199">為了讓您輕鬆了解載入的方式，我們在公開 Azure 儲存體 blob 中已裝載紐約市計程車資料。</span><span class="sxs-lookup"><span data-stu-id="3de2e-199">To make it easier to understand how to load, we have New York taxi cab data already hosted in a public Azure storage blob.</span></span> 

- <span data-ttu-id="3de2e-200">如需日後參考，要了解如何將您的資料置於 Azure blob 儲存體，或直接從您的來源將資料載入 SQL 資料倉儲，請參閱[載入概觀](sql-data-warehouse-overview-load.md)。</span><span class="sxs-lookup"><span data-stu-id="3de2e-200">For future reference, to learn how to get your data to Azure blob storage or to load it directly from your source into SQL Data Warehouse, see the [loading overview](sql-data-warehouse-overview-load.md).</span></span>


### <a name="define-external-data"></a><span data-ttu-id="3de2e-201">定義外部資料</span><span class="sxs-lookup"><span data-stu-id="3de2e-201">Define external data</span></span>

1. <span data-ttu-id="3de2e-202">建立建立主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="3de2e-202">Create a master key.</span></span> <span data-ttu-id="3de2e-203">您只需要為每個資料庫建立一次主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="3de2e-203">You only need to create a master key once per database.</span></span> 

    ```sql
    CREATE MASTER KEY;
    ```

2. <span data-ttu-id="3de2e-204">定義內含計程車封包資料的 Azure blob 的位置。</span><span class="sxs-lookup"><span data-stu-id="3de2e-204">Define the location of the Azure blob that contains the taxi cab data.</span></span>  

    ```sql
    CREATE EXTERNAL DATA SOURCE NYTPublic
    WITH
    (
        TYPE = Hadoop,
        LOCATION = 'wasbs://2013@nytpublic.blob.core.windows.net/'
    );
    ```

3. <span data-ttu-id="3de2e-205">定義外部檔案格式</span><span class="sxs-lookup"><span data-stu-id="3de2e-205">Define the external file formats</span></span>

    <span data-ttu-id="3de2e-206">可使用 ```CREATE EXTERNAL FILE FORMAT``` 命令來指定內含外部資料的檔案格式。</span><span class="sxs-lookup"><span data-stu-id="3de2e-206">The ```CREATE EXTERNAL FILE FORMAT``` command is used to specify the format of files that contain the external data.</span></span> <span data-ttu-id="3de2e-207">其中包含以一或多個名為分隔符號字元分隔的文字。</span><span class="sxs-lookup"><span data-stu-id="3de2e-207">They contain text separated by one or more characters called delimiters.</span></span> <span data-ttu-id="3de2e-208">基於示範目的，計程車封包資料以未壓縮的資料和 gzip 壓縮資料的形式儲存。</span><span class="sxs-lookup"><span data-stu-id="3de2e-208">For demonstration purposes, the taxi cab data is stored both as uncompressed data and as gzip compressed data.</span></span>

    <span data-ttu-id="3de2e-209">執行這些 T-SQL 命令，來定義兩個不同的格式︰未壓縮和壓縮。</span><span class="sxs-lookup"><span data-stu-id="3de2e-209">Run these T-SQL commands to define two different formats: uncompressed and compressed.</span></span>

    ```sql
    CREATE EXTERNAL FILE FORMAT uncompressedcsv
    WITH (
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( 
            FIELD_TERMINATOR = ',',
            STRING_DELIMITER = '',
            DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        )
    );

    CREATE EXTERNAL FILE FORMAT compressedcsv
    WITH ( 
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( FIELD_TERMINATOR = '|',
            STRING_DELIMITER = '',
        DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        ),
        DATA_COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'
    );
    ```

4.  <span data-ttu-id="3de2e-210">建立外部檔案格式的結構描述。</span><span class="sxs-lookup"><span data-stu-id="3de2e-210">Create a schema for your external file format.</span></span> 

    ```sql
    CREATE SCHEMA ext;
    ```
5. <span data-ttu-id="3de2e-211">建立外部資料表。</span><span class="sxs-lookup"><span data-stu-id="3de2e-211">Create the external tables.</span></span> <span data-ttu-id="3de2e-212">這些資料表會參考 Azure Blob 儲存體中儲存的資料。</span><span class="sxs-lookup"><span data-stu-id="3de2e-212">These tables reference data stored in Azure blob storage.</span></span> <span data-ttu-id="3de2e-213">執行下列 T-SQL 命令來建立數個外部資料表，而這些資料表都指向我們先前在外部資料來源中定義的 Azure blob。</span><span class="sxs-lookup"><span data-stu-id="3de2e-213">Run the following T-SQL commands to create several external tables that all point to the Azure blob we defined previously in our external data source.</span></span>

```sql
    CREATE EXTERNAL TABLE [ext].[Date] 
    (
        [DateID] int NOT NULL,
        [Date] datetime NULL,
        [DateBKey] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DaySuffix] varchar(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeek] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfQuarter] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfYear] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfMonth] varchar(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Month] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Quarter] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [QuarterName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Year] char(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [YearName] char(7) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthYear] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MMYYYY] char(6) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FirstDayOfMonth] date NULL,
        [LastDayOfMonth] date NULL,
        [FirstDayOfQuarter] date NULL,
        [LastDayOfQuarter] date NULL,
        [FirstDayOfYear] date NULL,
        [LastDayOfYear] date NULL,
        [IsHolidayUSA] bit NULL,
        [IsWeekday] bit NULL,
        [HolidayUSA] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Date',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    );
    
    CREATE EXTERNAL TABLE [ext].[Geography]
    (
        [GeographyID] int NOT NULL,
        [ZipCodeBKey] varchar(10) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [County] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [City] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [State] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Country] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [ZipCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Geography',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0 
    );
        
    
    CREATE EXTERNAL TABLE [ext].[HackneyLicense]
    (
        [HackneyLicenseID] int NOT NULL,
        [HackneyLicenseBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HackneyLicenseCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'HackneyLicense',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    
    CREATE EXTERNAL TABLE [ext].[Medallion]
    (
        [MedallionID] int NOT NULL,
        [MedallionBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [MedallionCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Medallion',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    CREATE EXTERNAL TABLE [ext].[Time]
    (
        [TimeID] int NOT NULL,
        [TimeBKey] varchar(8) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HourNumber] tinyint NOT NULL,
        [MinuteNumber] tinyint NOT NULL,
        [SecondNumber] tinyint NOT NULL,
        [TimeInSecond] int NOT NULL,
        [HourlyBucket] varchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [DayTimeBucketGroupKey] int NOT NULL,
        [DayTimeBucket] varchar(100) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL
    )
    WITH
    (
        LOCATION = 'Time',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    
    CREATE EXTERNAL TABLE [ext].[Trip]
    (
        [DateID] int NOT NULL,
        [MedallionID] int NOT NULL,
        [HackneyLicenseID] int NOT NULL,
        [PickupTimeID] int NOT NULL,
        [DropoffTimeID] int NOT NULL,
        [PickupGeographyID] int NULL,
        [DropoffGeographyID] int NULL,
        [PickupLatitude] float NULL,
        [PickupLongitude] float NULL,
        [PickupLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DropoffLatitude] float NULL,
        [DropoffLongitude] float NULL,
        [DropoffLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [PassengerCount] int NULL,
        [TripDurationSeconds] int NULL,
        [TripDistanceMiles] float NULL,
        [PaymentType] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FareAmount] money NULL,
        [SurchargeAmount] money NULL,
        [TaxAmount] money NULL,
        [TipAmount] money NULL,
        [TollsAmount] money NULL,
        [TotalAmount] money NULL
    )
    WITH
    (
        LOCATION = 'Trip2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = compressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    CREATE EXTERNAL TABLE [ext].[Weather]
    (
        [DateID] int NOT NULL,
        [GeographyID] int NOT NULL,
        [PrecipitationInches] float NOT NULL,
        [AvgTemperatureFahrenheit] float NOT NULL
    )
    WITH
    (
        LOCATION = 'Weather2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
```

### <a name="import-the-data-from-azure-blob-storage"></a><span data-ttu-id="3de2e-214">從 Azure Blob 儲存體匯入資料。</span><span class="sxs-lookup"><span data-stu-id="3de2e-214">Import the data from Azure blob storage.</span></span>

<span data-ttu-id="3de2e-215">SQL 資料倉儲支援稱為 CREATE TABLE AS SELECT (CTAS) 的重要陳述式。</span><span class="sxs-lookup"><span data-stu-id="3de2e-215">SQL Data Warehouse supports a key statement called CREATE TABLE AS SELECT (CTAS).</span></span> <span data-ttu-id="3de2e-216">此陳述式會根據 select 陳述式的結果建立新的資料表。</span><span class="sxs-lookup"><span data-stu-id="3de2e-216">This statement creates a new table based on the results of a select statement.</span></span> <span data-ttu-id="3de2e-217">新的資料表擁有和 select 陳述式結果相同的資料行和資料類型。</span><span class="sxs-lookup"><span data-stu-id="3de2e-217">The new table has the same columns and data types as the results of the select statement.</span></span>  <span data-ttu-id="3de2e-218">這是將資料從 Azure Blob 儲存體匯入 SQL 資料倉儲的最佳方式。</span><span class="sxs-lookup"><span data-stu-id="3de2e-218">This is an elegant way to import data from Azure blob storage into SQL Data Warehouse.</span></span>

1. <span data-ttu-id="3de2e-219">執行這個指令碼來匯入資料。</span><span class="sxs-lookup"><span data-stu-id="3de2e-219">Run this script to import your data.</span></span>

    ```sql
    CREATE TABLE [dbo].[Date]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Date]
    OPTION (LABEL = 'CTAS : Load [dbo].[Date]')
    ;
    
    CREATE TABLE [dbo].[Geography]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS
    SELECT * FROM [ext].[Geography]
    OPTION (LABEL = 'CTAS : Load [dbo].[Geography]')
    ;
    
    CREATE TABLE [dbo].[HackneyLicense]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[HackneyLicense]
    OPTION (LABEL = 'CTAS : Load [dbo].[HackneyLicense]')
    ;
    
    CREATE TABLE [dbo].[Medallion]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Medallion]
    OPTION (LABEL = 'CTAS : Load [dbo].[Medallion]')
    ;
    
    CREATE TABLE [dbo].[Time]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Time]
    OPTION (LABEL = 'CTAS : Load [dbo].[Time]')
    ;
    
    CREATE TABLE [dbo].[Weather]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Weather]
    OPTION (LABEL = 'CTAS : Load [dbo].[Weather]')
    ;
    
    CREATE TABLE [dbo].[Trip]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Trip]
    OPTION (LABEL = 'CTAS : Load [dbo].[Trip]')
    ;
    ```

2. <span data-ttu-id="3de2e-220">檢視載入中的資料。</span><span class="sxs-lookup"><span data-stu-id="3de2e-220">View your data as it loads.</span></span>

   <span data-ttu-id="3de2e-221">您會載入數 GB 的資料，並將其壓縮成高效能的叢集資料行存放區索引。</span><span class="sxs-lookup"><span data-stu-id="3de2e-221">You’re loading several GBs of data and compressing it into highly performant clustered columnstore indexes.</span></span> <span data-ttu-id="3de2e-222">執行下列會使用動態管理檢視 (DMV) 來顯示載入狀態的查詢。</span><span class="sxs-lookup"><span data-stu-id="3de2e-222">Run the following query that uses a dynamic management views (DMVs) to show the status of the load.</span></span> <span data-ttu-id="3de2e-223">啟動查詢之後，喝咖啡吃點心等候 SQL 資料倉儲進行一些繁重的工作。</span><span class="sxs-lookup"><span data-stu-id="3de2e-223">After starting the query, grab a coffee and a snack while SQL Data Warehouse does some heavy lifting.</span></span>
    
    ```sql
    SELECT
        r.command,
        s.request_id,
        r.status,
        count(distinct input_name) as nbr_files,
        sum(s.bytes_processed)/1024/1024/1024 as gb_processed
    FROM 
        sys.dm_pdw_exec_requests r
        INNER JOIN sys.dm_pdw_dms_external_work s
        ON r.request_id = s.request_id
    WHERE
        r.[label] = 'CTAS : Load [dbo].[Date]' OR
        r.[label] = 'CTAS : Load [dbo].[Geography]' OR
        r.[label] = 'CTAS : Load [dbo].[HackneyLicense]' OR
        r.[label] = 'CTAS : Load [dbo].[Medallion]' OR
        r.[label] = 'CTAS : Load [dbo].[Time]' OR
        r.[label] = 'CTAS : Load [dbo].[Weather]' OR
        r.[label] = 'CTAS : Load [dbo].[Trip]'
    GROUP BY
        r.command,
        s.request_id,
        r.status
    ORDER BY
        nbr_files desc, 
        gb_processed desc;
    ```

3. <span data-ttu-id="3de2e-224">檢視所有系統查詢。</span><span class="sxs-lookup"><span data-stu-id="3de2e-224">View all system queries.</span></span>

    ```sql
    SELECT * FROM sys.dm_pdw_exec_requests;
    ```

4. <span data-ttu-id="3de2e-225">輕鬆地看著資料順利載入至 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="3de2e-225">Enjoy seeing your data nicely loaded into your Azure SQL Data Warehouse.</span></span>

    ![看著資料載入](./media/sql-data-warehouse-get-started-tutorial/see-data-loaded.png)


## <a name="improve-query-performance"></a><span data-ttu-id="3de2e-227">改善查詢效能</span><span class="sxs-lookup"><span data-stu-id="3de2e-227">Improve query performance</span></span>

<span data-ttu-id="3de2e-228">有數種方式可以改善查詢效能，並達到 SQL 資料倉儲依設計所能提供的高速效能。</span><span class="sxs-lookup"><span data-stu-id="3de2e-228">There are several ways to improve query performance and to achieve the high-speed performance that SQL Data Warehouse is designed to provide.</span></span>  

### <a name="see-the-effect-of-scaling-on-query-performance"></a><span data-ttu-id="3de2e-229">查看調整查詢效能時的影響</span><span class="sxs-lookup"><span data-stu-id="3de2e-229">See the effect of scaling on query performance</span></span> 

<span data-ttu-id="3de2e-230">改善查詢效能的方法之一是藉由變更資料倉儲的 DWU 服務層級來調整資源。</span><span class="sxs-lookup"><span data-stu-id="3de2e-230">One way to improve query performance is to scale resources by changing the DWU service level for your data warehouse.</span></span> <span data-ttu-id="3de2e-231">每個服務等級的成本會往上增加，但您可以隨時調整回來或暫停資源。</span><span class="sxs-lookup"><span data-stu-id="3de2e-231">Each service level costs more, but you can scale back or pause resources at any time.</span></span> 

<span data-ttu-id="3de2e-232">在此步驟中，您將會比較兩個不同 DWU 設定的效能。</span><span class="sxs-lookup"><span data-stu-id="3de2e-232">In this step, you compare performance at two different DWU settings.</span></span>

<span data-ttu-id="3de2e-233">首先，讓我們將規模下調為 100 DWU，以便了解單一計算節點本身的可能執行效能。</span><span class="sxs-lookup"><span data-stu-id="3de2e-233">First, let's scale the sizing down to 100 DWU so we can get an idea of how one compute node might perform on its own.</span></span>

1. <span data-ttu-id="3de2e-234">移至入口網站，並選取 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="3de2e-234">Go to the portal and select your SQL Data Warehouse.</span></span>

2. <span data-ttu-id="3de2e-235">在 [SQL 資料倉儲] 刀鋒視窗中選取 [調整]。</span><span class="sxs-lookup"><span data-stu-id="3de2e-235">Select scale in the SQL Data Warehouse blade.</span></span> 

    ![從入口網站調整 DW](./media/sql-data-warehouse-get-started-tutorial/scale-dw.png)

3. <span data-ttu-id="3de2e-237">將效能列縮小到 100 DWU，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="3de2e-237">Scale down the performance bar to 100 DWU and hit save.</span></span>

    ![調整並儲存](./media/sql-data-warehouse-get-started-tutorial/scale-and-save.png)

4. <span data-ttu-id="3de2e-239">等候調整作業完成。</span><span class="sxs-lookup"><span data-stu-id="3de2e-239">Wait for your scale operation to finish.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3de2e-240">變更規模時無法執行查詢。</span><span class="sxs-lookup"><span data-stu-id="3de2e-240">Queries cannot run while changing the scale.</span></span> <span data-ttu-id="3de2e-241">調整會**刪除**目前執行的查詢。</span><span class="sxs-lookup"><span data-stu-id="3de2e-241">Scaling **kills** your currently running queries.</span></span> <span data-ttu-id="3de2e-242">您可以在作業完成時重新啟動查詢。</span><span class="sxs-lookup"><span data-stu-id="3de2e-242">You can restart them when the operation is finished.</span></span>
    >
    
5. <span data-ttu-id="3de2e-243">對車程資料執行掃描作業，選取所有資料行的前 1 百萬個項目。</span><span class="sxs-lookup"><span data-stu-id="3de2e-243">Do a scan operation on the trip data, selecting the top million entries for all the columns.</span></span> <span data-ttu-id="3de2e-244">如果您想要進展快一點，可放心地選取較少的資料列。</span><span class="sxs-lookup"><span data-stu-id="3de2e-244">If you're eager to move on quickly, feel free to select fewer rows.</span></span> <span data-ttu-id="3de2e-245">記下執行這項作業所花費的時間。</span><span class="sxs-lookup"><span data-stu-id="3de2e-245">Take note of the time it takes to run this operation.</span></span>

    ```sql
    SELECT TOP(1000000) * FROM dbo.[Trip]
    ```
6. <span data-ttu-id="3de2e-246">將資料倉儲調回 400 DWU。</span><span class="sxs-lookup"><span data-stu-id="3de2e-246">Scale your data warehouse back to 400 DWU.</span></span> <span data-ttu-id="3de2e-247">請記住，每上調 100 DWU 就會再新增一個計算節點至您的 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="3de2e-247">Remember, each 100 DWU is adding another compute node to your Azure SQL Data Warehouse.</span></span>

7. <span data-ttu-id="3de2e-248">再次執行查詢！</span><span class="sxs-lookup"><span data-stu-id="3de2e-248">Run the query again!</span></span> <span data-ttu-id="3de2e-249">您應該會發現顯著差異。</span><span class="sxs-lookup"><span data-stu-id="3de2e-249">You should notice a significant difference.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="3de2e-250">因為查詢傳回大量資料，所以執行 SSMS 之電腦的頻寬可用性可能是效能瓶頸。</span><span class="sxs-lookup"><span data-stu-id="3de2e-250">Because the query returns a lot of data, the bandwidth availability of the machine running SSMS may be a performance bottleneck.</span></span> <span data-ttu-id="3de2e-251">這會導致您看不到任何效能改善！</span><span class="sxs-lookup"><span data-stu-id="3de2e-251">This can result in you not seeing any performance improvements!</span></span>

> [!NOTE]
> <span data-ttu-id="3de2e-252">SQL 資料倉儲會使用大量平行處理。</span><span class="sxs-lookup"><span data-stu-id="3de2e-252">Since SQL Data Warehouse uses massively parallel processing.</span></span> <span data-ttu-id="3de2e-253">因此，對數百萬個資料列掃描或執行分析函式將可體驗到 Azure SQL 資料倉儲的真正威力。</span><span class="sxs-lookup"><span data-stu-id="3de2e-253">Queries that scan or perform analytic functions on millions of rows experience the true power of Azure SQL Data Warehouse.</span></span>
>

### <a name="see-the-effect-of-statistics-on-query-performance"></a><span data-ttu-id="3de2e-254">查看查詢效能統計資料的影響</span><span class="sxs-lookup"><span data-stu-id="3de2e-254">See the effect of statistics on query performance</span></span>

1. <span data-ttu-id="3de2e-255">執行聯結了日期資料表與車程資料表的查詢</span><span class="sxs-lookup"><span data-stu-id="3de2e-255">Run a query that joins the Date table with the Trip table</span></span>

    ```sql
    SELECT TOP (1000000) 
        dt.[DayOfWeek],
        tr.[MedallionID],
        tr.[HackneyLicenseID],
        tr.[PickupTimeID],
        tr.[DropoffTimeID],
        tr.[PickupGeographyID],
        tr.[DropoffGeographyID],
        tr.[PickupLatitude],
        tr.[PickupLongitude],
        tr.[PickupLatLong],
        tr.[DropoffLatitude],
        tr.[DropoffLongitude],
        tr.[DropoffLatLong],
        tr.[PassengerCount],
        tr.[TripDurationSeconds],
        tr.[TripDistanceMiles],
        tr.[PaymentType],
        tr.[FareAmount],
        tr.[SurchargeAmount],
        tr.[TaxAmount],
        tr.[TipAmount],
        tr.[TollsAmount],
        tr.[TotalAmount]
    FROM [dbo].[Trip] as tr
        JOIN dbo.[Date] as dt
        ON  tr.DateID = dt.DateID
    ```

    <span data-ttu-id="3de2e-256">SQL 資料倉儲必須先隨機處理資料才能執行聯結，因此這項查詢需要進行一段時間。</span><span class="sxs-lookup"><span data-stu-id="3de2e-256">This query takes a while because SQL Data Warehouse has to shuffle data before it can perform the join.</span></span> <span data-ttu-id="3de2e-257">若聯結依設計會以散佈資料時的相同方式來聯結資料，則不必隨機處理資料。</span><span class="sxs-lookup"><span data-stu-id="3de2e-257">Joins do not have to shuffle data if they are designed to join data in the same way it is distributed.</span></span> <span data-ttu-id="3de2e-258">這是更深入的主題了。</span><span class="sxs-lookup"><span data-stu-id="3de2e-258">That's a deeper subject.</span></span> 

2. <span data-ttu-id="3de2e-259">統計資料會造成差異。</span><span class="sxs-lookup"><span data-stu-id="3de2e-259">Statistics make a difference.</span></span> 
3. <span data-ttu-id="3de2e-260">執行此陳述式來建立聯結資料行的統計資料。</span><span class="sxs-lookup"><span data-stu-id="3de2e-260">Run this statement to create statistics on the join columns.</span></span>

    ```sql
    CREATE STATISTICS [dbo.Date DateID stats] ON dbo.Date (DateID);
    CREATE STATISTICS [dbo.Trip DateID stats] ON dbo.Trip (DateID);
    ```

    > [!NOTE]
    > <span data-ttu-id="3de2e-261">SQL DW 不會自動管理您的統計資料。</span><span class="sxs-lookup"><span data-stu-id="3de2e-261">SQL DW does not automatically manage statistics for you.</span></span> <span data-ttu-id="3de2e-262">統計資料對於查詢的效能很重要，因此強烈建議您建立和更新統計資料。</span><span class="sxs-lookup"><span data-stu-id="3de2e-262">Statistics are important for query performance and it is highly recommended you create and update statistics.</span></span>
    > 
    > <span data-ttu-id="3de2e-263">**對牽涉聯結的資料行、WHERE 子句中使用的資料行、在 GROUP BY 中找到的資料行加以統計資料，可以獲得最大效益。**</span><span class="sxs-lookup"><span data-stu-id="3de2e-263">**You gain the most benefit by having statistics on columns involved in joins, columns used in the WHERE clause and columns found in GROUP BY.**</span></span>
    >

3. <span data-ttu-id="3de2e-264">再次從必要條件執行查詢，並觀察效能差異。</span><span class="sxs-lookup"><span data-stu-id="3de2e-264">Run the query from Prerequisites again and observe any performance differences.</span></span> <span data-ttu-id="3de2e-265">雖然查詢效能的差異幅度不會和上調規模一樣巨大，但您應該會發現速度有所增加。</span><span class="sxs-lookup"><span data-stu-id="3de2e-265">While the differences in query performance will not be as drastic as scaling up, you should notice a  speed-up.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3de2e-266">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3de2e-266">Next steps</span></span>

<span data-ttu-id="3de2e-267">您現在已準備就緒，可以開始查詢和探索。</span><span class="sxs-lookup"><span data-stu-id="3de2e-267">You're now ready to query and explore.</span></span> <span data-ttu-id="3de2e-268">請查看我們的最佳作法或提示。</span><span class="sxs-lookup"><span data-stu-id="3de2e-268">Check out our best practices or tips.</span></span>

<span data-ttu-id="3de2e-269">如果您當天的探索已完成，請務必暫停您的執行個體！</span><span class="sxs-lookup"><span data-stu-id="3de2e-269">If you're done exploring for the day, make sure to pause your instance!</span></span> <span data-ttu-id="3de2e-270">在生產環境中，您可以藉由暫停和調整大小以符合商務需求來省下大額成本。</span><span class="sxs-lookup"><span data-stu-id="3de2e-270">In production, you can experience enormous savings by pausing and scaling to meet your business needs.</span></span>

![暫停](./media/sql-data-warehouse-get-started-tutorial/pause.png)

## <a name="useful-readings"></a><span data-ttu-id="3de2e-272">實用內容</span><span class="sxs-lookup"><span data-stu-id="3de2e-272">Useful readings</span></span>

<span data-ttu-id="3de2e-273">[並行和工作負載管理][]</span><span class="sxs-lookup"><span data-stu-id="3de2e-273">[Concurrency and Workload Management][]</span></span>

<span data-ttu-id="3de2e-274">[Azure SQL 資料倉儲最佳做法][]</span><span class="sxs-lookup"><span data-stu-id="3de2e-274">[Best practices for Azure SQL Data Warehouse][]</span></span>

<span data-ttu-id="3de2e-275">[查詢監視][]</span><span class="sxs-lookup"><span data-stu-id="3de2e-275">[Query Monitoring][]</span></span>

<span data-ttu-id="3de2e-276">[建立大規模關聯式資料倉儲的 10 大最佳作法][]</span><span class="sxs-lookup"><span data-stu-id="3de2e-276">[Top 10 Best Practices for Building a Large Scale Relational Data Warehouse][]</span></span>

<span data-ttu-id="3de2e-277">[將資料移轉至 Azure SQL 資料倉儲][]</span><span class="sxs-lookup"><span data-stu-id="3de2e-277">[Migrating Data to Azure SQL Data Warehouse][]</span></span>

[並行和工作負載管理]: sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example
[Azure SQL 資料倉儲最佳做法]: sql-data-warehouse-best-practices.md#hash-distribute-large-tables
[查詢監視]: sql-data-warehouse-manage-monitor.md
[建立大規模關聯式資料倉儲的 10 大最佳作法]: https://blogs.msdn.microsoft.com/sqlcat/2013/09/16/top-10-best-practices-for-building-a-large-scale-relational-data-warehouse/
[將資料移轉至 Azure SQL 資料倉儲]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/



[!INCLUDE [Additional Resources](../../includes/sql-data-warehouse-article-footer.md)]

<!-- Internal Links -->
[必要條件]: sql-data-warehouse-get-started-tutorial.md#prerequisites

<!--Other Web references-->
[Visual Studio]: https://www.visualstudio.com/
[SQL Server Management Studio]: https://msdn.microsoft.com/en-us/library/mt238290.aspx
