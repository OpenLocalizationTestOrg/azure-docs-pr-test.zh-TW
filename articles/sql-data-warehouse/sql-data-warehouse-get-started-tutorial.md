---
title: "aaaAzure SQL 資料倉儲-快速入門教學課程 |Microsoft 文件"
description: "本教學課程將教導您如何 tooprovision 和載入資料到 Azure SQL 資料倉儲。 您也將學習 hello 調整、 暫停和微調有關的基本概念。"
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
ms.openlocfilehash: edd2a21b0fe49ca8e9792c7c512310339a822c55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-data-warehouse"></a><span data-ttu-id="e60e4-104">開始使用 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="e60e4-104">Get started with SQL Data Warehouse</span></span>

<span data-ttu-id="e60e4-105">本教學課程示範如何將 Azure SQL 資料倉儲的 tooprovision 和載入資料。</span><span class="sxs-lookup"><span data-stu-id="e60e4-105">This tutorial shows how tooprovision and load data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="e60e4-106">您也將學習 hello 調整、 暫停和微調有關的基本概念。</span><span class="sxs-lookup"><span data-stu-id="e60e4-106">You’ll also learn hello basics about scaling, pausing, and tuning.</span></span> <span data-ttu-id="e60e4-107">當您完成時，您將會是準備 tooquery 並且瀏覽您的資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="e60e4-107">When you’re finished, you’ll be ready tooquery and explore your data warehouse.</span></span>

<span data-ttu-id="e60e4-108">**估計時間 toocomplete:**這是一個端對端教學課程，採用約 30 分鐘 toocomplete，一旦您已符合 hello 先決條件的範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="e60e4-108">**Estimated time toocomplete:** This is an end-to-end tutorial with example code that takes about 30 minutes toocomplete once you have met hello prerequisites.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e60e4-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="e60e4-109">Prerequisites</span></span>

<span data-ttu-id="e60e4-110">hello 教學課程假設您熟悉 SQL 資料倉儲基本概念。</span><span class="sxs-lookup"><span data-stu-id="e60e4-110">hello tutorial assumes you are familiar with SQL Data Warehouse basic concepts.</span></span> <span data-ttu-id="e60e4-111">如果您需要簡介，請參閱[什麼是 SQL 資料倉儲？](sql-data-warehouse-overview-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="e60e4-111">If you need an introduction, see [What is SQL Data Warehouse?](sql-data-warehouse-overview-what-is.md)</span></span> 

### <a name="sign-up-for-microsoft-azure"></a><span data-ttu-id="e60e4-112">註冊 Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="e60e4-112">Sign up for Microsoft Azure</span></span>
<span data-ttu-id="e60e4-113">如果您還沒有 Microsoft Azure 帳戶，您需要註冊一個 toouse toosign 這項服務。</span><span class="sxs-lookup"><span data-stu-id="e60e4-113">If you don't already have a Microsoft Azure account, you need toosign up for one toouse this service.</span></span> <span data-ttu-id="e60e4-114">如果您已經有帳戶，則可以跳過此步驟。</span><span class="sxs-lookup"><span data-stu-id="e60e4-114">If you already have an account, you may skip this step.</span></span> 

1. <span data-ttu-id="e60e4-115">瀏覽 toohello 帳戶頁面[https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)</span><span class="sxs-lookup"><span data-stu-id="e60e4-115">Navigate toohello account pages [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)</span></span>
2. <span data-ttu-id="e60e4-116">建立免費的 Azure 帳戶，或購買帳戶。</span><span class="sxs-lookup"><span data-stu-id="e60e4-116">Create a free Azure account, or purchase an account.</span></span>
3. <span data-ttu-id="e60e4-117">請依照下列指示 hello</span><span class="sxs-lookup"><span data-stu-id="e60e4-117">Follow hello instructions</span></span>

### <a name="install-appropriate-sql-client-drivers-and-tools"></a><span data-ttu-id="e60e4-118">安裝適當的 SQL 用戶端驅動程式和工具</span><span class="sxs-lookup"><span data-stu-id="e60e4-118">Install appropriate SQL client drivers and tools</span></span>

<span data-ttu-id="e60e4-119">大部分的 SQL 用戶端工具可以使用 JDBC、 ODBC 或 ADO.NET 連接 tooSQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="e60e4-119">Most SQL client tools can connect tooSQL Data Warehouse by using JDBC, ODBC, or ADO.NET.</span></span> <span data-ttu-id="e60e4-120">Toohello 大量 SQL Data Warehouse 支援的 T-SQL 功能，因為某些用戶端應用程式不會與 SQL 資料倉儲完全相容。</span><span class="sxs-lookup"><span data-stu-id="e60e4-120">Due toohello large number of T-SQL features that SQL Data Warehouse supports, some client applications are not fully compatible with SQL Data Warehouse.</span></span>

<span data-ttu-id="e60e4-121">如果您執行的是 Windows 作業系統，建議您使用 [Visual Studio] 或 [SQL Server Management Studio]。</span><span class="sxs-lookup"><span data-stu-id="e60e4-121">If you are running a Windows operating system, we recommend using either [Visual Studio] or [SQL Server Management Studio].</span></span>

[!INCLUDE [Create a new logical server](../../includes/sql-data-warehouse-create-logical-server.md)] 

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="e60e4-122">建立 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="e60e4-122">Create a SQL Data Warehouse</span></span>

<span data-ttu-id="e60e4-123">SQL 資料倉儲是一種特殊類型的資料庫，其設計用來進行大量平行處理。</span><span class="sxs-lookup"><span data-stu-id="e60e4-123">A SQL Data Warehouse is a special type of database that is designed for massively parallel processing.</span></span> <span data-ttu-id="e60e4-124">hello 資料庫分散到多個節點，並處理以平行方式查詢。</span><span class="sxs-lookup"><span data-stu-id="e60e4-124">hello database is distributed across multiple nodes and processes queries in parallel.</span></span> <span data-ttu-id="e60e4-125">SQL 資料倉儲具有協調所有 hello 節點的 hello 活動為控制節點。</span><span class="sxs-lookup"><span data-stu-id="e60e4-125">SQL Data Warehouse has a control node that orchestrates hello activities of all hello nodes.</span></span> <span data-ttu-id="e60e4-126">hello 節點本身會使用 SQL Database toomanage 您的資料。</span><span class="sxs-lookup"><span data-stu-id="e60e4-126">hello nodes themselves use SQL Database toomanage your data.</span></span>  

> [!NOTE]
> <span data-ttu-id="e60e4-127">建立 SQL 資料倉儲可能會導致新的可計費服務。</span><span class="sxs-lookup"><span data-stu-id="e60e4-127">Creating a SQL Data Warehouse might result in a new billable service.</span></span>  <span data-ttu-id="e60e4-128">如需詳細資訊，請參閱 [SQL 資料倉儲價格](https://azure.microsoft.com/pricing/details/sql-data-warehouse/)。</span><span class="sxs-lookup"><span data-stu-id="e60e4-128">For more information, see [SQL Data Warehouse pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>
>

### <a name="create-a-data-warehouse"></a><span data-ttu-id="e60e4-129">建立資料倉儲</span><span class="sxs-lookup"><span data-stu-id="e60e4-129">Create a data warehouse</span></span>

1. <span data-ttu-id="e60e4-130">登入 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="e60e4-130">Sign into hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e60e4-131">按一下 [新增] > [資料庫] > [SQL 資料倉儲]。</span><span class="sxs-lookup"><span data-stu-id="e60e4-131">Click **New** > **Databases** > **SQL Data Warehouse**.</span></span>

    <span data-ttu-id="e60e4-132">![NewBlade](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png) ![SelectDW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)</span><span class="sxs-lookup"><span data-stu-id="e60e4-132">![NewBlade](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png) ![SelectDW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)</span></span>

3. <span data-ttu-id="e60e4-133">填寫部署詳細資料</span><span class="sxs-lookup"><span data-stu-id="e60e4-133">Fill out deployment details</span></span>

    <span data-ttu-id="e60e4-134">**資料庫名稱**︰挑選您想要的名稱。</span><span class="sxs-lookup"><span data-stu-id="e60e4-134">**Database Name**: Pick anything you'd like.</span></span> <span data-ttu-id="e60e4-135">如果您有多個資料倉儲時，我們建議您的名稱包含詳細資料，例如 hello 區域中，環境中，例如*mydw uswest 1-測試*。</span><span class="sxs-lookup"><span data-stu-id="e60e4-135">If you have multiple data warehouses, we recommend your names include details such as hello region, environment, for example *mydw-westus-1-test*.</span></span>

    <span data-ttu-id="e60e4-136">**訂用帳戶**：您的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e60e4-136">**Subscription**: Your Azure subscription</span></span>

    <span data-ttu-id="e60e4-137">**資源群組**：建立新的資源群組，或使用現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="e60e4-137">**Resource Group**: Create a resource group or use an existing resource group.</span></span>
    > [!NOTE]
    > <span data-ttu-id="e60e4-138">資源群組適合用來管理資源，例如界定存取控制和樣板化部署的範圍。</span><span class="sxs-lookup"><span data-stu-id="e60e4-138">Resource groups are useful for resource administration such as scoping access control and templated deployment.</span></span> <span data-ttu-id="e60e4-139">您可以[在此](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)深入了解 Azure 資源群組和最佳作法</span><span class="sxs-lookup"><span data-stu-id="e60e4-139">Read more about Azure resource groups and best practices [here](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)</span></span>

    <span data-ttu-id="e60e4-140">**來源**：空白資料庫</span><span class="sxs-lookup"><span data-stu-id="e60e4-140">**Source**: Blank Database</span></span>

    <span data-ttu-id="e60e4-141">**伺服器**： 您在建立選取 hello 伺服器[必要條件]。</span><span class="sxs-lookup"><span data-stu-id="e60e4-141">**Server**: Select hello server you created in [Prerequisites].</span></span>

    <span data-ttu-id="e60e4-142">**定序**： 保留 hello 預設定序 SQL_Latin1_General_CP1_CI_AS。</span><span class="sxs-lookup"><span data-stu-id="e60e4-142">**Collation**: Leave hello default collation SQL_Latin1_General_CP1_CI_AS.</span></span>

    <span data-ttu-id="e60e4-143">**選取 效能**： 我們建議您從 hello 標準 400DWU 開始。</span><span class="sxs-lookup"><span data-stu-id="e60e4-143">**Select performance**: We recommend starting with hello standard 400DWU.</span></span>

4. <span data-ttu-id="e60e4-144">選擇**Pin toodashboard** ![Pin tooDashboard](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="e60e4-144">Choose **Pin toodashboard** ![Pin tooDashboard](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)</span></span>

5. <span data-ttu-id="e60e4-145">耐心和等候您的資料倉儲 toodeploy ！</span><span class="sxs-lookup"><span data-stu-id="e60e4-145">Sit back and wait for your data warehouse toodeploy!</span></span> <span data-ttu-id="e60e4-146">這是正常的這個程序 tootake 幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="e60e4-146">It's normal for this process tootake several minutes.</span></span> <span data-ttu-id="e60e4-147">當資料倉儲就緒 toouse hello 入口網站會通知您。</span><span class="sxs-lookup"><span data-stu-id="e60e4-147">hello portal notifies you when your data warehouse is ready toouse.</span></span> 

## <a name="connect-toosql-data-warehouse"></a><span data-ttu-id="e60e4-148">連接 tooSQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="e60e4-148">Connect tooSQL Data Warehouse</span></span>

<span data-ttu-id="e60e4-149">本教學課程會使用 SQL Server Management Studio (SSMS) tooconnect toohello 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="e60e4-149">This tutorial uses SQL Server Management Studio (SSMS) tooconnect toohello data warehouse.</span></span> <span data-ttu-id="e60e4-150">您可以透過這些支援的連接器連接 tooSQL 資料倉儲： ADO.NET、 JDBC、 ODBC 和 PHP。</span><span class="sxs-lookup"><span data-stu-id="e60e4-150">You can connect tooSQL Data Warehouse through these supported connectors: ADO.NET, JDBC, ODBC, and PHP.</span></span> <span data-ttu-id="e60e4-151">請記住，非 Microsoft 支援工具的功能可能會受限。</span><span class="sxs-lookup"><span data-stu-id="e60e4-151">Remember, functionality might be limited for tools that are not supported by Microsoft.</span></span>


### <a name="get-connection-information"></a><span data-ttu-id="e60e4-152">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="e60e4-152">Get connection information</span></span>

<span data-ttu-id="e60e4-153">tooconnect tooyour 資料倉儲，您需要透過 hello 您在建立邏輯 SQL server tooconnect[必要條件]。</span><span class="sxs-lookup"><span data-stu-id="e60e4-153">tooconnect tooyour data warehouse, you need tooconnect through hello logical SQL server you created in [Prerequisites].</span></span>

1. <span data-ttu-id="e60e4-154">從 hello 儀表板或搜尋您的資源中選取您的資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="e60e4-154">Select your data warehouse from hello dashboard or search for it in your resources.</span></span>

    ![SQL 資料倉儲儀表板](./media/sql-data-warehouse-get-started-tutorial/sql-dw-dashboard.png)

2. <span data-ttu-id="e60e4-156">尋找 hello hello 邏輯 SQL server 的完整名稱。</span><span class="sxs-lookup"><span data-stu-id="e60e4-156">Find hello full name for hello logical SQL server.</span></span>

    ![選取伺服器名稱](./media/sql-data-warehouse-get-started-tutorial/select-server.png)

3. <span data-ttu-id="e60e4-158">開啟 SSMS，並使用物件總管 中 tooconnect toothis 伺服器使用您在建立 hello 伺服器系統管理員認證[必要條件]</span><span class="sxs-lookup"><span data-stu-id="e60e4-158">Open SSMS and use object explorer tooconnect toothis server using hello server admin credentials you created in [Prerequisites]</span></span>

    ![以 SSMS 連線](./media/sql-data-warehouse-get-started-tutorial/ssms-connect.png)

<span data-ttu-id="e60e4-160">如果一切正確，您現在應該連接的 tooyour 邏輯 SQL server。</span><span class="sxs-lookup"><span data-stu-id="e60e4-160">If all goes correctly, you should now be connected tooyour logical SQL server.</span></span> <span data-ttu-id="e60e4-161">因為您登入 hello 伺服器系統管理員，您可以連接 tooany hello 伺服器，包括 hello master 資料庫所裝載的資料庫。</span><span class="sxs-lookup"><span data-stu-id="e60e4-161">Since you logged in as hello server admin, you can connect tooany database hosted by hello server, including hello master database.</span></span> 

<span data-ttu-id="e60e4-162">有一個伺服器系統管理員帳戶，而且它有 hello 大部分的權限的任何使用者。</span><span class="sxs-lookup"><span data-stu-id="e60e4-162">There is only one server admin account and it has hello most privileges of any user.</span></span> <span data-ttu-id="e60e4-163">請小心不 tooallow 太多人在您的組織 tooknow hello 的系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="e60e4-163">Be careful not tooallow too many people in your organization tooknow hello admin password.</span></span> 

<span data-ttu-id="e60e4-164">您也可以擁有 Azure Active Directory 系統管理帳戶。</span><span class="sxs-lookup"><span data-stu-id="e60e4-164">You can also have an Azure active directory admin account.</span></span> <span data-ttu-id="e60e4-165">我們不提供 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e60e4-165">We don't provide hello details here.</span></span> <span data-ttu-id="e60e4-166">如果您想 toolearn 深入了解使用 Azure Active Directory 驗證時，請參閱[Azure AD 驗證](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication)。</span><span class="sxs-lookup"><span data-stu-id="e60e4-166">If you want toolearn more about using Azure Active Directory authentication, see [Azure AD authentication](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).</span></span>

<span data-ttu-id="e60e4-167">接下來，我們將探討建立其他登入和使用者。</span><span class="sxs-lookup"><span data-stu-id="e60e4-167">Next, we explore creating additional logins and users.</span></span>


## <a name="create-a-database-user"></a><span data-ttu-id="e60e4-168">建立資料庫使用者</span><span class="sxs-lookup"><span data-stu-id="e60e4-168">Create a database user</span></span>

<span data-ttu-id="e60e4-169">在此步驟中，您建立使用者帳戶 tooaccess 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="e60e4-169">In this step, you create a user account tooaccess your data warehouse.</span></span> <span data-ttu-id="e60e4-170">我們也會示範如何 toogive 該使用者 hello 能力 toorun 查詢具有大量的記憶體和 CPU 資源。</span><span class="sxs-lookup"><span data-stu-id="e60e4-170">We also show you how toogive that user hello ability toorun queries with a large amount of memory and CPU resources.</span></span>

### <a name="notes-about-resource-classes-for-allocating-resources-tooqueries"></a><span data-ttu-id="e60e4-171">配置資源 tooqueries 資源類別的相關注意事項</span><span class="sxs-lookup"><span data-stu-id="e60e4-171">Notes about resource classes for allocating resources tooqueries</span></span>

- <span data-ttu-id="e60e4-172">tookeep 資料安全，不要將生產資料庫上使用 hello 伺服器系統管理員 toorun 查詢。</span><span class="sxs-lookup"><span data-stu-id="e60e4-172">tookeep your data safe, don't use hello server admin toorun queries on your production databases.</span></span> <span data-ttu-id="e60e4-173">它具有 hello 大部分的權限的任何使用者，並使用它 tooperform 使用者資料的作業會讓您的資料面臨風險。</span><span class="sxs-lookup"><span data-stu-id="e60e4-173">It has hello most privileges of any user and using it tooperform operations on user data puts your data at risk.</span></span> <span data-ttu-id="e60e4-174">此外，hello 伺服器系統管理員就是 tooperform 管理作業，因為它會執行作業只提供較小的配置的記憶體和 CPU 資源。</span><span class="sxs-lookup"><span data-stu-id="e60e4-174">Also, since hello server admin is meant tooperform management operations, it runs operations with only a small allocation of memory and CPU resources.</span></span> 

- <span data-ttu-id="e60e4-175">SQL 資料倉儲會使用預先定義的資料庫角色，稱為資源類別、 記憶體、 CPU 資源，以及並行插槽 toousers tooallocate 不同量。</span><span class="sxs-lookup"><span data-stu-id="e60e4-175">SQL Data Warehouse uses pre-defined database roles, called resource classes, tooallocate different amounts of memory, CPU resources, and concurrency slots toousers.</span></span> <span data-ttu-id="e60e4-176">每個使用者可隸屬 tooa 小型、 中型、 大型或超大資源類別。</span><span class="sxs-lookup"><span data-stu-id="e60e4-176">Each user can belong tooa small, medium, large, or extra-large resource class.</span></span> <span data-ttu-id="e60e4-177">hello 使用者的資源類別決定 hello 資源 hello 使用者有 toorun 查詢和載入作業。</span><span class="sxs-lookup"><span data-stu-id="e60e4-177">hello user's resource class determines hello resources hello user has toorun queries and load operations.</span></span>

- <span data-ttu-id="e60e4-178">最佳的資料壓縮 hello 使用者可能需要 tooload 與大型或超大型資源配置。</span><span class="sxs-lookup"><span data-stu-id="e60e4-178">For optimal data compression, hello user may need tooload with large or extra large resource allocations.</span></span> <span data-ttu-id="e60e4-179">請[在此](./sql-data-warehouse-develop-concurrency.md#resource-classes)深入了解資源類別：</span><span class="sxs-lookup"><span data-stu-id="e60e4-179">Read more about resource classes [here](./sql-data-warehouse-develop-concurrency.md#resource-classes):</span></span>

### <a name="create-an-account-that-can-control-a-database"></a><span data-ttu-id="e60e4-180">建立一個可以控制資料庫的帳戶</span><span class="sxs-lookup"><span data-stu-id="e60e4-180">Create an account that can control a database</span></span>

<span data-ttu-id="e60e4-181">由於您目前在如 hello 伺服器系統管理員登您有權限 toocreate 登入和使用者。</span><span class="sxs-lookup"><span data-stu-id="e60e4-181">Since you are currently logged in as hello server admin you have permissions toocreate logins and users.</span></span>

1. <span data-ttu-id="e60e4-182">使用 SSMS 或另一個查詢用戶端，開啟對**主要**的新查詢。</span><span class="sxs-lookup"><span data-stu-id="e60e4-182">Using SSMS or another query client, open a new query for **master**.</span></span>

    ![主要資料庫上的新增查詢](./media/sql-data-warehouse-get-started-tutorial/query-on-server.png)

    ![主要資料庫上的新增查詢 1](./media/sql-data-warehouse-get-started-tutorial/query-on-master.png)

2. <span data-ttu-id="e60e4-185">在 hello 查詢視窗中，執行此 T-SQL 命令 toocreate 名為 MedRCLogin 登入和名為 LoadingUser 使用者。</span><span class="sxs-lookup"><span data-stu-id="e60e4-185">In hello query window, run this T-SQL command toocreate a login named MedRCLogin and user named LoadingUser.</span></span> <span data-ttu-id="e60e4-186">此登入可以連接 toohello 邏輯 SQL server。</span><span class="sxs-lookup"><span data-stu-id="e60e4-186">This login can connect toohello logical SQL server.</span></span>

    ```sql
    CREATE LOGIN MedRCLogin WITH PASSWORD = 'a123reallySTRONGpassword!';
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

3. <span data-ttu-id="e60e4-187">現在查詢 hello *SQL 資料倉儲資料庫*，建立資料庫使用者基礎 hello 登入建立 tooaccess 且 hello 資料庫上執行作業。</span><span class="sxs-lookup"><span data-stu-id="e60e4-187">Now querying hello *SQL Data Warehouse database*, create a database user based on hello login you created tooaccess and perform operations on hello database.</span></span>

    ```sql
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

4. <span data-ttu-id="e60e4-188">提供 hello 資料庫使用者控制的權限 toohello 資料庫呼叫 NYT。</span><span class="sxs-lookup"><span data-stu-id="e60e4-188">Give hello database user control permissions toohello database called NYT.</span></span> 

    ```sql
    GRANT CONTROL ON DATABASE::[NYT] tooLoadingUser;
    ```
    > [!NOTE]
    > <span data-ttu-id="e60e4-189">如果您的資料庫名稱中連字號，以確定 toowrap 在方括號 ！</span><span class="sxs-lookup"><span data-stu-id="e60e4-189">If your database name has hyphens in it, be sure toowrap it in brackets!</span></span> 
    >

### <a name="give-hello-user-medium-resource-allocations"></a><span data-ttu-id="e60e4-190">授與 hello 使用者中資源配置</span><span class="sxs-lookup"><span data-stu-id="e60e4-190">Give hello user medium resource allocations</span></span>

1. <span data-ttu-id="e60e4-191">執行這個 T-SQL 命令 toomake 為稱為 mediumrc hello 中資源類別的成員。</span><span class="sxs-lookup"><span data-stu-id="e60e4-191">Run this T-SQL command toomake it a member of hello medium resource class, which is called mediumrc.</span></span> 

    ```sql
    EXEC sp_addrolemember 'mediumrc', 'LoadingUser';
    ```
    > [!NOTE]
    > <span data-ttu-id="e60e4-192">按一下[這裡](sql-data-warehouse-develop-concurrency.md#resource-classes)toolearn 更多關於並行與資源類別 ！</span><span class="sxs-lookup"><span data-stu-id="e60e4-192">Click [here](sql-data-warehouse-develop-concurrency.md#resource-classes) toolearn more about concurrency and resource classes!</span></span> 
    >

2. <span data-ttu-id="e60e4-193">Hello 新的認證與連線 toohello 邏輯伺服器</span><span class="sxs-lookup"><span data-stu-id="e60e4-193">Connect toohello logical server with hello new credentials</span></span>

    ![使用新登入進行登入](./media/sql-data-warehouse-get-started-tutorial/new-login.png)


## <a name="load-data-from-azure-blob-storage"></a><span data-ttu-id="e60e4-195">從 Azure blob 儲存體載入資料</span><span class="sxs-lookup"><span data-stu-id="e60e4-195">Load data from Azure blob storage</span></span>

<span data-ttu-id="e60e4-196">現在您已經準備就緒 tooload 資料到資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="e60e4-196">You are now ready tooload data into your data warehouse.</span></span> <span data-ttu-id="e60e4-197">此步驟說明如何 tooload New York City 趕赴從公用 Azure 儲存體的封包資料的 blob。</span><span class="sxs-lookup"><span data-stu-id="e60e4-197">This step shows you how tooload New York City taxi cab data from a public Azure storage blob.</span></span> 

- <span data-ttu-id="e60e4-198">Tooload 資料到 SQL 資料倉儲是 toofirst 的常見方式移動 hello 資料 tooAzure blob 儲存體，，然後將它載入您的資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="e60e4-198">A common way tooload data into SQL Data Warehouse is toofirst move hello data tooAzure blob storage, and then load it into your data warehouse.</span></span> <span data-ttu-id="e60e4-199">toomake 它更容易 toounderstand tooload，如何當我們有紐約計程車封包資料已裝載公用 Azure 儲存體 blob 中。</span><span class="sxs-lookup"><span data-stu-id="e60e4-199">toomake it easier toounderstand how tooload, we have New York taxi cab data already hosted in a public Azure storage blob.</span></span> 

- <span data-ttu-id="e60e4-200">供日後參考，toolearn 如何 tooget 資料 tooAzure blob 儲存體或它直接從您到 SQL 資料倉儲的來源，請參閱的 tooload hello[載入概觀](sql-data-warehouse-overview-load.md)。</span><span class="sxs-lookup"><span data-stu-id="e60e4-200">For future reference, toolearn how tooget your data tooAzure blob storage or tooload it directly from your source into SQL Data Warehouse, see hello [loading overview](sql-data-warehouse-overview-load.md).</span></span>


### <a name="define-external-data"></a><span data-ttu-id="e60e4-201">定義外部資料</span><span class="sxs-lookup"><span data-stu-id="e60e4-201">Define external data</span></span>

1. <span data-ttu-id="e60e4-202">建立建立主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="e60e4-202">Create a master key.</span></span> <span data-ttu-id="e60e4-203">您只需要 toocreate 每個資料庫主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="e60e4-203">You only need toocreate a master key once per database.</span></span> 

    ```sql
    CREATE MASTER KEY;
    ```

2. <span data-ttu-id="e60e4-204">定義 hello hello Azure blob 可包含 hello 計程車封包資料位置。</span><span class="sxs-lookup"><span data-stu-id="e60e4-204">Define hello location of hello Azure blob that contains hello taxi cab data.</span></span>  

    ```sql
    CREATE EXTERNAL DATA SOURCE NYTPublic
    WITH
    (
        TYPE = Hadoop,
        LOCATION = 'wasbs://2013@nytpublic.blob.core.windows.net/'
    );
    ```

3. <span data-ttu-id="e60e4-205">定義 hello 外部檔案格式</span><span class="sxs-lookup"><span data-stu-id="e60e4-205">Define hello external file formats</span></span>

    <span data-ttu-id="e60e4-206">hello```CREATE EXTERNAL FILE FORMAT```命令是使用的 toospecify 包含 hello 外部資料的檔案格式。</span><span class="sxs-lookup"><span data-stu-id="e60e4-206">hello ```CREATE EXTERNAL FILE FORMAT``` command is used toospecify the format of files that contain hello external data.</span></span> <span data-ttu-id="e60e4-207">其中包含以一或多個名為分隔符號字元分隔的文字。</span><span class="sxs-lookup"><span data-stu-id="e60e4-207">They contain text separated by one or more characters called delimiters.</span></span> <span data-ttu-id="e60e4-208">針對示範用途，hello 計程車封包資料會儲存為未壓縮的資料，做為 gzip 壓縮資料。</span><span class="sxs-lookup"><span data-stu-id="e60e4-208">For demonstration purposes, hello taxi cab data is stored both as uncompressed data and as gzip compressed data.</span></span>

    <span data-ttu-id="e60e4-209">T-SQL 執行這些命令 toodefine 兩個不同的格式： 未壓縮和壓縮。</span><span class="sxs-lookup"><span data-stu-id="e60e4-209">Run these T-SQL commands toodefine two different formats: uncompressed and compressed.</span></span>

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

4.  <span data-ttu-id="e60e4-210">建立外部檔案格式的結構描述。</span><span class="sxs-lookup"><span data-stu-id="e60e4-210">Create a schema for your external file format.</span></span> 

    ```sql
    CREATE SCHEMA ext;
    ```
5. <span data-ttu-id="e60e4-211">建立 hello 外部資料表。</span><span class="sxs-lookup"><span data-stu-id="e60e4-211">Create hello external tables.</span></span> <span data-ttu-id="e60e4-212">這些資料表會參考 Azure Blob 儲存體中儲存的資料。</span><span class="sxs-lookup"><span data-stu-id="e60e4-212">These tables reference data stored in Azure blob storage.</span></span> <span data-ttu-id="e60e4-213">執行下列 T-SQL 命令 toocreate hello 所有點 toohello Azure blob 我們先前在中定義之外部資料來源的多個外部資料表。</span><span class="sxs-lookup"><span data-stu-id="e60e4-213">Run hello following T-SQL commands toocreate several external tables that all point toohello Azure blob we defined previously in our external data source.</span></span>

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

### <a name="import-hello-data-from-azure-blob-storage"></a><span data-ttu-id="e60e4-214">從 Azure blob 儲存體的 hello 資料匯入。</span><span class="sxs-lookup"><span data-stu-id="e60e4-214">Import hello data from Azure blob storage.</span></span>

<span data-ttu-id="e60e4-215">SQL 資料倉儲支援稱為 CREATE TABLE AS SELECT (CTAS) 的重要陳述式。</span><span class="sxs-lookup"><span data-stu-id="e60e4-215">SQL Data Warehouse supports a key statement called CREATE TABLE AS SELECT (CTAS).</span></span> <span data-ttu-id="e60e4-216">這個陳述式建立新的資料表，根據 hello select 陳述式的結果。</span><span class="sxs-lookup"><span data-stu-id="e60e4-216">This statement creates a new table based on hello results of a select statement.</span></span> <span data-ttu-id="e60e4-217">hello 新的資料表有 hello 相同資料行和資料類型，如 hello hello 結果 select 陳述式。</span><span class="sxs-lookup"><span data-stu-id="e60e4-217">hello new table has hello same columns and data types as hello results of hello select statement.</span></span>  <span data-ttu-id="e60e4-218">這是適合用來 tooimport 來自資料到 SQL 資料倉儲的 Azure blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="e60e4-218">This is an elegant way tooimport data from Azure blob storage into SQL Data Warehouse.</span></span>

1. <span data-ttu-id="e60e4-219">執行這個指令碼 tooimport 您的資料。</span><span class="sxs-lookup"><span data-stu-id="e60e4-219">Run this script tooimport your data.</span></span>

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

2. <span data-ttu-id="e60e4-220">檢視載入中的資料。</span><span class="sxs-lookup"><span data-stu-id="e60e4-220">View your data as it loads.</span></span>

   <span data-ttu-id="e60e4-221">您會載入數 GB 的資料，並將其壓縮成高效能的叢集資料行存放區索引。</span><span class="sxs-lookup"><span data-stu-id="e60e4-221">You’re loading several GBs of data and compressing it into highly performant clustered columnstore indexes.</span></span> <span data-ttu-id="e60e4-222">執行下列查詢會使用動態管理檢視 (Dmv) tooshow hello 狀態 hello 負載 hello。</span><span class="sxs-lookup"><span data-stu-id="e60e4-222">Run hello following query that uses a dynamic management views (DMVs) tooshow hello status of hello load.</span></span> <span data-ttu-id="e60e4-223">啟動之後 hello 查詢，請抓取咖啡和零食但 SQL 資料倉儲會有些困難。</span><span class="sxs-lookup"><span data-stu-id="e60e4-223">After starting hello query, grab a coffee and a snack while SQL Data Warehouse does some heavy lifting.</span></span>
    
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

3. <span data-ttu-id="e60e4-224">檢視所有系統查詢。</span><span class="sxs-lookup"><span data-stu-id="e60e4-224">View all system queries.</span></span>

    ```sql
    SELECT * FROM sys.dm_pdw_exec_requests;
    ```

4. <span data-ttu-id="e60e4-225">輕鬆地看著資料順利載入至 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="e60e4-225">Enjoy seeing your data nicely loaded into your Azure SQL Data Warehouse.</span></span>

    ![看著資料載入](./media/sql-data-warehouse-get-started-tutorial/see-data-loaded.png)


## <a name="improve-query-performance"></a><span data-ttu-id="e60e4-227">改善查詢效能</span><span class="sxs-lookup"><span data-stu-id="e60e4-227">Improve query performance</span></span>

<span data-ttu-id="e60e4-228">有數種方式 tooimprove 查詢效能和 tooachieve hello 高速效能 SQL 資料倉儲的設計 tooprovide。</span><span class="sxs-lookup"><span data-stu-id="e60e4-228">There are several ways tooimprove query performance and tooachieve hello high-speed performance that SQL Data Warehouse is designed tooprovide.</span></span>  

### <a name="see-hello-effect-of-scaling-on-query-performance"></a><span data-ttu-id="e60e4-229">請參閱 hello 的縮放比例，查詢效能的影響</span><span class="sxs-lookup"><span data-stu-id="e60e4-229">See hello effect of scaling on query performance</span></span> 

<span data-ttu-id="e60e4-230">其中一種方式 tooimprove 查詢效能是 tooscale 資源變更您的資料倉儲的 hello DWU 服務層級。</span><span class="sxs-lookup"><span data-stu-id="e60e4-230">One way tooimprove query performance is tooscale resources by changing hello DWU service level for your data warehouse.</span></span> <span data-ttu-id="e60e4-231">每個服務等級的成本會往上增加，但您可以隨時調整回來或暫停資源。</span><span class="sxs-lookup"><span data-stu-id="e60e4-231">Each service level costs more, but you can scale back or pause resources at any time.</span></span> 

<span data-ttu-id="e60e4-232">在此步驟中，您將會比較兩個不同 DWU 設定的效能。</span><span class="sxs-lookup"><span data-stu-id="e60e4-232">In this step, you compare performance at two different DWU settings.</span></span>

<span data-ttu-id="e60e4-233">首先，讓我們來調整關閉 too100 DWU，因此我們可以得到了解如何計算節點可能會執行本身的 hello 調整大小。</span><span class="sxs-lookup"><span data-stu-id="e60e4-233">First, let's scale hello sizing down too100 DWU so we can get an idea of how one compute node might perform on its own.</span></span>

1. <span data-ttu-id="e60e4-234">移 toohello 入口網站，然後選取您的 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="e60e4-234">Go toohello portal and select your SQL Data Warehouse.</span></span>

2. <span data-ttu-id="e60e4-235">選取在 hello SQL 資料倉儲刀鋒視窗中的小數位數。</span><span class="sxs-lookup"><span data-stu-id="e60e4-235">Select scale in hello SQL Data Warehouse blade.</span></span> 

    ![從入口網站調整 DW](./media/sql-data-warehouse-get-started-tutorial/scale-dw.png)

3. <span data-ttu-id="e60e4-237">縮放列 too100 DWU hello 效能和儲存叫用。</span><span class="sxs-lookup"><span data-stu-id="e60e4-237">Scale down hello performance bar too100 DWU and hit save.</span></span>

    ![調整並儲存](./media/sql-data-warehouse-get-started-tutorial/scale-and-save.png)

4. <span data-ttu-id="e60e4-239">等候您的標尺作業 toofinish。</span><span class="sxs-lookup"><span data-stu-id="e60e4-239">Wait for your scale operation toofinish.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e60e4-240">變更 hello 小數位數時，無法執行查詢。</span><span class="sxs-lookup"><span data-stu-id="e60e4-240">Queries cannot run while changing hello scale.</span></span> <span data-ttu-id="e60e4-241">調整會**刪除**目前執行的查詢。</span><span class="sxs-lookup"><span data-stu-id="e60e4-241">Scaling **kills** your currently running queries.</span></span> <span data-ttu-id="e60e4-242">Hello 作業完成時，您可以重新加以啟動。</span><span class="sxs-lookup"><span data-stu-id="e60e4-242">You can restart them when hello operation is finished.</span></span>
    >
    
5. <span data-ttu-id="e60e4-243">執行掃描作業上選取 hello 頂端百萬個項目 hello 的所有資料行的 hello 路線資料。</span><span class="sxs-lookup"><span data-stu-id="e60e4-243">Do a scan operation on hello trip data, selecting hello top million entries for all hello columns.</span></span> <span data-ttu-id="e60e4-244">如果您積極式 toomove 上快速，則可以免費 tooselect 較少的資料列。</span><span class="sxs-lookup"><span data-stu-id="e60e4-244">If you're eager toomove on quickly, feel free tooselect fewer rows.</span></span> <span data-ttu-id="e60e4-245">記下 hello 花的時間 toorun 這項作業。</span><span class="sxs-lookup"><span data-stu-id="e60e4-245">Take note of hello time it takes toorun this operation.</span></span>

    ```sql
    SELECT TOP(1000000) * FROM dbo.[Trip]
    ```
6. <span data-ttu-id="e60e4-246">調整您的資料倉儲回 too400 DWU。</span><span class="sxs-lookup"><span data-stu-id="e60e4-246">Scale your data warehouse back too400 DWU.</span></span> <span data-ttu-id="e60e4-247">請記住，每個 100 DWU 新增另一個計算節點 tooyour Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="e60e4-247">Remember, each 100 DWU is adding another compute node tooyour Azure SQL Data Warehouse.</span></span>

7. <span data-ttu-id="e60e4-248">再次執行查詢 hello ！</span><span class="sxs-lookup"><span data-stu-id="e60e4-248">Run hello query again!</span></span> <span data-ttu-id="e60e4-249">您應該會發現顯著差異。</span><span class="sxs-lookup"><span data-stu-id="e60e4-249">You should notice a significant difference.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="e60e4-250">由於 hello 查詢傳回大量資料，執行 SSMS hello 機器 hello 頻寬可用性可能會造成效能瓶頸。</span><span class="sxs-lookup"><span data-stu-id="e60e4-250">Because hello query returns a lot of data, hello bandwidth availability of hello machine running SSMS may be a performance bottleneck.</span></span> <span data-ttu-id="e60e4-251">這會導致您看不到任何效能改善！</span><span class="sxs-lookup"><span data-stu-id="e60e4-251">This can result in you not seeing any performance improvements!</span></span>

> [!NOTE]
> <span data-ttu-id="e60e4-252">SQL 資料倉儲會使用大量平行處理。</span><span class="sxs-lookup"><span data-stu-id="e60e4-252">Since SQL Data Warehouse uses massively parallel processing.</span></span> <span data-ttu-id="e60e4-253">掃描或數百萬個資料列上執行分析函式的查詢遇到 hello 真正強大的 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="e60e4-253">Queries that scan or perform analytic functions on millions of rows experience hello true power of Azure SQL Data Warehouse.</span></span>
>

### <a name="see-hello-effect-of-statistics-on-query-performance"></a><span data-ttu-id="e60e4-254">查看對查詢效能的統計資料的 hello 效果</span><span class="sxs-lookup"><span data-stu-id="e60e4-254">See hello effect of statistics on query performance</span></span>

1. <span data-ttu-id="e60e4-255">執行查詢聯結 hello hello 路線資料表與日期資料表</span><span class="sxs-lookup"><span data-stu-id="e60e4-255">Run a query that joins hello Date table with hello Trip table</span></span>

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

    <span data-ttu-id="e60e4-256">因為它可以執行 hello 聯結前 SQL 資料倉儲 tooshuffle 資料，這項查詢需要一些時間。</span><span class="sxs-lookup"><span data-stu-id="e60e4-256">This query takes a while because SQL Data Warehouse has tooshuffle data before it can perform hello join.</span></span> <span data-ttu-id="e60e4-257">聯結沒有 tooshuffle 資料所設計的 toojoin hello 資料散發的方式相同。</span><span class="sxs-lookup"><span data-stu-id="e60e4-257">Joins do not have tooshuffle data if they are designed toojoin data in hello same way it is distributed.</span></span> <span data-ttu-id="e60e4-258">這是更深入的主題了。</span><span class="sxs-lookup"><span data-stu-id="e60e4-258">That's a deeper subject.</span></span> 

2. <span data-ttu-id="e60e4-259">統計資料會造成差異。</span><span class="sxs-lookup"><span data-stu-id="e60e4-259">Statistics make a difference.</span></span> 
3. <span data-ttu-id="e60e4-260">Hello 聯結資料行上執行此陳述式 toocreate 統計資料。</span><span class="sxs-lookup"><span data-stu-id="e60e4-260">Run this statement toocreate statistics on hello join columns.</span></span>

    ```sql
    CREATE STATISTICS [dbo.Date DateID stats] ON dbo.Date (DateID);
    CREATE STATISTICS [dbo.Trip DateID stats] ON dbo.Trip (DateID);
    ```

    > [!NOTE]
    > <span data-ttu-id="e60e4-261">SQL DW 不會自動管理您的統計資料。</span><span class="sxs-lookup"><span data-stu-id="e60e4-261">SQL DW does not automatically manage statistics for you.</span></span> <span data-ttu-id="e60e4-262">統計資料對於查詢的效能很重要，因此強烈建議您建立和更新統計資料。</span><span class="sxs-lookup"><span data-stu-id="e60e4-262">Statistics are important for query performance and it is highly recommended you create and update statistics.</span></span>
    > 
    > <span data-ttu-id="e60e4-263">**您可以 hello 最大效益，到的資料行聯結，使用 hello 子句資料行找到和 GROUP BY 中的資料行中具有統計資料。**</span><span class="sxs-lookup"><span data-stu-id="e60e4-263">**You gain hello most benefit by having statistics on columns involved in joins, columns used in hello WHERE clause and columns found in GROUP BY.**</span></span>
    >

3. <span data-ttu-id="e60e4-264">再次執行必要條件的 hello 查詢，並觀察效能差異。</span><span class="sxs-lookup"><span data-stu-id="e60e4-264">Run hello query from Prerequisites again and observe any performance differences.</span></span> <span data-ttu-id="e60e4-265">雖然無法以向上擴充為極端 hello 差異查詢的效能，您應該會注意到加速。</span><span class="sxs-lookup"><span data-stu-id="e60e4-265">While hello differences in query performance will not be as drastic as scaling up, you should notice a  speed-up.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e60e4-266">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e60e4-266">Next steps</span></span>

<span data-ttu-id="e60e4-267">您現在已經準備就緒 tooquery 及探索。</span><span class="sxs-lookup"><span data-stu-id="e60e4-267">You're now ready tooquery and explore.</span></span> <span data-ttu-id="e60e4-268">請查看我們的最佳作法或提示。</span><span class="sxs-lookup"><span data-stu-id="e60e4-268">Check out our best practices or tips.</span></span>

<span data-ttu-id="e60e4-269">如果您完成 hello 天，瀏覽您的執行個體請確定 toopause ！</span><span class="sxs-lookup"><span data-stu-id="e60e4-269">If you're done exploring for hello day, make sure toopause your instance!</span></span> <span data-ttu-id="e60e4-270">實際執行環境，您可以暫停並調整 toomeet 體驗龐大的節省您的業務需求。</span><span class="sxs-lookup"><span data-stu-id="e60e4-270">In production, you can experience enormous savings by pausing and scaling toomeet your business needs.</span></span>

![暫停](./media/sql-data-warehouse-get-started-tutorial/pause.png)

## <a name="useful-readings"></a><span data-ttu-id="e60e4-272">實用內容</span><span class="sxs-lookup"><span data-stu-id="e60e4-272">Useful readings</span></span>

<span data-ttu-id="e60e4-273">[並行和工作負載管理][]</span><span class="sxs-lookup"><span data-stu-id="e60e4-273">[Concurrency and Workload Management][]</span></span>

<span data-ttu-id="e60e4-274">[Azure SQL 資料倉儲最佳做法][]</span><span class="sxs-lookup"><span data-stu-id="e60e4-274">[Best practices for Azure SQL Data Warehouse][]</span></span>

<span data-ttu-id="e60e4-275">[查詢監視][]</span><span class="sxs-lookup"><span data-stu-id="e60e4-275">[Query Monitoring][]</span></span>

<span data-ttu-id="e60e4-276">[建立大規模關聯式資料倉儲的 10 大最佳作法][]</span><span class="sxs-lookup"><span data-stu-id="e60e4-276">[Top 10 Best Practices for Building a Large Scale Relational Data Warehouse][]</span></span>

<span data-ttu-id="e60e4-277">[移轉資料 tooAzure SQL 資料倉儲][]</span><span class="sxs-lookup"><span data-stu-id="e60e4-277">[Migrating Data tooAzure SQL Data Warehouse][]</span></span>

[並行和工作負載管理]: sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example
[Azure SQL 資料倉儲最佳做法]: sql-data-warehouse-best-practices.md#hash-distribute-large-tables
[查詢監視]: sql-data-warehouse-manage-monitor.md
[建立大規模關聯式資料倉儲的 10 大最佳作法]: https://blogs.msdn.microsoft.com/sqlcat/2013/09/16/top-10-best-practices-for-building-a-large-scale-relational-data-warehouse/
[移轉資料 tooAzure SQL 資料倉儲]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/



[!INCLUDE [Additional Resources](../../includes/sql-data-warehouse-article-footer.md)]

<!-- Internal Links -->
[必要條件]: sql-data-warehouse-get-started-tutorial.md#prerequisites

<!--Other Web references-->
[Visual Studio]: https://www.visualstudio.com/
[SQL Server Management Studio]: https://msdn.microsoft.com/en-us/library/mt238290.aspx
