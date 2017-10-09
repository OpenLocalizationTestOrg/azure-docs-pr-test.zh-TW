---
title: "aaaGetting 開始使用 Azure SQL 資料同步 （預覽） |Microsoft 文件"
description: "本教學課程可協助您開始使用 Azure SQL 資料同步 (預覽)。"
services: sql-database
documentationcenter: 
author: douglaslms
manager: craigg
editor: 
ms.assetid: a295a768-7ff2-4a86-a253-0090281c8efa
ms.service: sql-database
ms.custom: load & move data
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: douglasl
ms.openlocfilehash: 666d09237e42acc23ae3c8c81e60734a413f5949
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-sql-data-sync-preview"></a><span data-ttu-id="b41d0-103">開始使用 Azure SQL 資料同步 (預覽)</span><span class="sxs-lookup"><span data-stu-id="b41d0-103">Getting Started with Azure SQL Data Sync (Preview)</span></span>
<span data-ttu-id="b41d0-104">在此教學課程中，您學會如何藉由建立混合式同步處理群組設定 Azure SQL 資料同步 tooset 包含 Azure SQL Database 和 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="b41d0-104">In this tutorial, you learn how tooset up Azure SQL Data Sync by creating a hybrid sync group that contains both Azure SQL Database and SQL Server instances.</span></span> <span data-ttu-id="b41d0-105">hello 新同步處理群組完整設定，並在您設定的 hello 排程同步處理。</span><span class="sxs-lookup"><span data-stu-id="b41d0-105">hello new sync group is fully configured and synchronizes on hello schedule you set.</span></span>

<span data-ttu-id="b41d0-106">本教學課程假設您先前至少有一些使用 SQL Database 和 SQL Server 的經驗。</span><span class="sxs-lookup"><span data-stu-id="b41d0-106">This tutorial assumes that you have at least some prior experience with SQL Database and with SQL Server.</span></span> 

<span data-ttu-id="b41d0-107">如需 SQL 資料同步處理的概觀，請參閱[同步資料](sql-database-sync-data.md)。</span><span class="sxs-lookup"><span data-stu-id="b41d0-107">For an overview of SQL Data Sync, see [Sync data](sql-database-sync-data.md).</span></span>

<span data-ttu-id="b41d0-108">如需完整 PowerShell 範例顯示如何 tooconfigure SQL 資料同步處理，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="b41d0-108">For complete PowerShell examples that show how tooconfigure SQL Data Sync, see hello following articles:</span></span>
-   [<span data-ttu-id="b41d0-109">使用多個 Azure SQL database 之間的 PowerShell toosync</span><span class="sxs-lookup"><span data-stu-id="b41d0-109">Use PowerShell toosync between multiple Azure SQL databases</span></span>](scripts/sql-database-sync-data-between-sql-databases.md)
-   [<span data-ttu-id="b41d0-110">使用 Azure SQL Database 和 SQL Server 在內部部署資料庫之間的 PowerShell toosync</span><span class="sxs-lookup"><span data-stu-id="b41d0-110">Use PowerShell toosync between an Azure SQL Database and a SQL Server on-premises database</span></span>](scripts/sql-database-sync-data-between-azure-onprem.md)

> [!NOTE]
> <span data-ttu-id="b41d0-111">hello 完成技術文件集 Azure SQL 資料同步先前位於 MSDN，可做為。PDF 文件。</span><span class="sxs-lookup"><span data-stu-id="b41d0-111">hello complete technical documentation set for Azure SQL Data Sync, formerly located on MSDN, is available as a .PDF document.</span></span> <span data-ttu-id="b41d0-112">在 [這裡](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)下載。</span><span class="sxs-lookup"><span data-stu-id="b41d0-112">Download it [here](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true).</span></span>

## <a name="step-1---create-sync-group"></a><span data-ttu-id="b41d0-113">步驟 1 - 建立同步群組</span><span class="sxs-lookup"><span data-stu-id="b41d0-113">Step 1 - Create sync group</span></span>

### <a name="locate-hello-data-sync-settings"></a><span data-ttu-id="b41d0-114">找出 hello 資料同步處理設定</span><span class="sxs-lookup"><span data-stu-id="b41d0-114">Locate hello Data Sync settings</span></span>

1.  <span data-ttu-id="b41d0-115">在瀏覽器中瀏覽 toohello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="b41d0-115">In your browser, navigate toohello Azure portal.</span></span>

2.  <span data-ttu-id="b41d0-116">在 hello 入口網站中，找出 hello 工具列上的 SQL 資料庫從儀表板或 hello SQL 資料庫的圖示。</span><span class="sxs-lookup"><span data-stu-id="b41d0-116">In hello portal, locate your SQL databases from your Dashboard or from hello SQL Databases icon on hello toolbar.</span></span>

    ![Azure SQL 資料庫清單](media/sql-database-get-started-sql-data-sync/datasync-preview-sqldbs.png)

3.  <span data-ttu-id="b41d0-118">在 hello **SQL 資料庫**刀鋒視窗中，選取 hello 的 toouse hello 中樞資料庫的資料同步處理。 hello SQL 資料庫刀鋒視窗中開啟現有 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="b41d0-118">On hello **SQL databases** blade, select hello existing SQL database that you want toouse as hello hub database for Data Sync. hello SQL database blade opens.</span></span>

4.  <span data-ttu-id="b41d0-119">在 hello hello 選取資料庫的 SQL 資料庫刀鋒視窗，選取 **同步 tooother 資料庫**。</span><span class="sxs-lookup"><span data-stu-id="b41d0-119">On hello SQL database blade for hello selected database, select **Sync tooother databases**.</span></span> <span data-ttu-id="b41d0-120">hello 資料同步 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="b41d0-120">hello Data Sync blade opens.</span></span>

    ![Sync tooother 資料庫選項](media/sql-database-get-started-sql-data-sync/datasync-preview-newsyncgroup.png)

### <a name="create-a-new-sync-group"></a><span data-ttu-id="b41d0-122">建立新的同步群組</span><span class="sxs-lookup"><span data-stu-id="b41d0-122">Create a new Sync Group</span></span>

1.  <span data-ttu-id="b41d0-123">在 hello 資料同步刀鋒視窗中，選取 **新同步處理群組**。</span><span class="sxs-lookup"><span data-stu-id="b41d0-123">On hello Data Sync blade, select **New Sync Group**.</span></span> <span data-ttu-id="b41d0-124">hello**新同步處理群組**使用步驟 1 中，開啟刀鋒視窗**建立同步處理群組**，反白顯示。</span><span class="sxs-lookup"><span data-stu-id="b41d0-124">hello **New sync group** blade opens with Step 1, **Create sync group**, highlighted.</span></span> <span data-ttu-id="b41d0-125">hello**建立的資料同步處理群組**也會開啟刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b41d0-125">hello **Create Data Sync Group** blade also opens.</span></span>

2.  <span data-ttu-id="b41d0-126">在 hello**建立的資料同步處理群組**刀鋒視窗中，請勿 hello 下列事項：</span><span class="sxs-lookup"><span data-stu-id="b41d0-126">On hello **Create Data Sync Group** blade, do hello following things:</span></span>

    1.  <span data-ttu-id="b41d0-127">在 hello**同步群組名稱**欄位中，輸入 hello 新同步處理群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="b41d0-127">In hello **Sync Group Name** field, enter a name for hello new sync group.</span></span>

    2.  <span data-ttu-id="b41d0-128">在 hello**同步處理中繼資料資料庫**區段中，選擇是否 toocreate 新的資料庫 （建議選項） 或 toouse 的現有資料庫。</span><span class="sxs-lookup"><span data-stu-id="b41d0-128">In hello **Sync Metadata Database** section, choose whether toocreate a new database (recommended) or toouse an existing database.</span></span>

        > [!NOTE]
        > <span data-ttu-id="b41d0-129">Microsoft 建議您建立新的空白資料庫 toouse 為 hello 同步處理中繼資料資料庫。</span><span class="sxs-lookup"><span data-stu-id="b41d0-129">Microsoft recommends that you create a new, empty database toouse as hello Sync Metadata Database.</span></span> <span data-ttu-id="b41d0-130">資料同步會在此資料庫中建立資料表，並頻繁執行工作負載。</span><span class="sxs-lookup"><span data-stu-id="b41d0-130">Data Sync creates tables in this database and runs a frequent workload.</span></span> <span data-ttu-id="b41d0-131">這個資料庫會自動已經共用為 hello hello 所選資料區域中同步處理群組的所有同步處理中繼資料資料庫中。</span><span class="sxs-lookup"><span data-stu-id="b41d0-131">This database is automatically shared as hello Sync Metadata Database for all of your Sync groups in hello selected region.</span></span> <span data-ttu-id="b41d0-132">您無法變更 hello 同步處理中繼資料資料庫、 其名稱或其 service 層級，但不卸除它。</span><span class="sxs-lookup"><span data-stu-id="b41d0-132">You can't change hello Sync Metadata Database, its name, or its service level without dropping it.</span></span>

        <span data-ttu-id="b41d0-133">如果您選擇 [新資料庫]，請選取 [建立新的資料庫]。</span><span class="sxs-lookup"><span data-stu-id="b41d0-133">If you chose **New database**, select **Create new database.**</span></span> <span data-ttu-id="b41d0-134">hello **SQL Database**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="b41d0-134">hello **SQL Database** blade opens.</span></span> <span data-ttu-id="b41d0-135">在 hello **SQL Database**刀鋒視窗中，命名，並設定 hello 新資料庫。</span><span class="sxs-lookup"><span data-stu-id="b41d0-135">On hello **SQL Database** blade, name and configure hello new database.</span></span> <span data-ttu-id="b41d0-136">然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="b41d0-136">Then select **OK**.</span></span>

        <span data-ttu-id="b41d0-137">如果您選擇**使用現有的資料庫**，選取從 hello 清單 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="b41d0-137">If you chose **Use existing database**, select hello database from hello list.</span></span>

    3.  <span data-ttu-id="b41d0-138">在 hello**自動同步處理**區段中，第一次選取**上**或**關閉**。</span><span class="sxs-lookup"><span data-stu-id="b41d0-138">In hello **Automatic Sync** section, first select **On** or **Off**.</span></span>

        <span data-ttu-id="b41d0-139">如果您選擇**上**，在 hello**同步處理頻率**區段中，輸入的數字，然後選取秒、 分鐘、 小時或天。</span><span class="sxs-lookup"><span data-stu-id="b41d0-139">If you chose **On**, in hello **Sync Frequency** section, enter a number and select Seconds, Minutes, Hours, or Days.</span></span>

        ![指定同步處理頻率](media/sql-database-get-started-sql-data-sync/datasync-preview-syncfreq.png)

    4.  <span data-ttu-id="b41d0-141">在 hello**衝突解決**區段中，選取 「 中樞獲勝 」 或 「"成員 wins。</span><span class="sxs-lookup"><span data-stu-id="b41d0-141">In hello **Conflict Resolution** section, select "Hub wins" or "Member wins."</span></span>

        ![指定解決衝突的方式](media/sql-database-get-started-sql-data-sync/datasync-preview-conflictres.png)

    5.  <span data-ttu-id="b41d0-143">選取**確定**並等候 hello 新同步處理群組 toobe 建立和部署。</span><span class="sxs-lookup"><span data-stu-id="b41d0-143">Select **OK** and wait for hello new sync group toobe created and deployed.</span></span>

## <a name="step-2---add-sync-members"></a><span data-ttu-id="b41d0-144">步驟 2 - 新增同步成員</span><span class="sxs-lookup"><span data-stu-id="b41d0-144">Step 2 - Add sync members</span></span>

<span data-ttu-id="b41d0-145">建立及部署，步驟 2 hello 新同步處理群組之後**加入同步處理成員**，會反白顯示在 hello**新同步處理群組**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b41d0-145">After hello new sync group is created and deployed, Step 2, **Add sync members**, is highlighted in hello **New sync group** blade.</span></span>

<span data-ttu-id="b41d0-146">在 hello**中樞資料庫**區段中，輸入 hello 現有認證的 hello SQL 資料庫所在的伺服器上的 hello 中樞資料庫。</span><span class="sxs-lookup"><span data-stu-id="b41d0-146">In hello **Hub Database** section, enter hello existing credentials for hello SQL Database server on which hello hub database is located.</span></span> <span data-ttu-id="b41d0-147">請不要在此區段輸入「新」的認證。</span><span class="sxs-lookup"><span data-stu-id="b41d0-147">Don't enter *new* credentials in this section.</span></span>

![已加入中樞資料庫 toosync 群組](media/sql-database-get-started-sql-data-sync/datasync-preview-hubadded.png)

## <a name="add-an-azure-sql-database"></a><span data-ttu-id="b41d0-149">新增 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="b41d0-149">Add an Azure SQL Database</span></span>

<span data-ttu-id="b41d0-150">在 hello**成員資料庫**區段中，選擇性地選取 加入 Azure SQL Database toohello 同步處理群組**加入 Azure 的資料庫**。</span><span class="sxs-lookup"><span data-stu-id="b41d0-150">In hello **Member Database** section, optionally add an Azure SQL Database toohello sync group by selecting **Add an Azure Database**.</span></span> <span data-ttu-id="b41d0-151">hello**設定 Azure Database**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="b41d0-151">hello **Configure Azure Database** blade opens.</span></span>

<span data-ttu-id="b41d0-152">在 hello**設定 Azure Database**刀鋒視窗中，執行下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="b41d0-152">On hello **Configure Azure Database** blade, do hello following things:</span></span>

1.  <span data-ttu-id="b41d0-153">在 hello**同步成員名稱**欄位中，提供 hello 新同步處理成員的名稱。</span><span class="sxs-lookup"><span data-stu-id="b41d0-153">In hello **Sync Member Name** field, provide a name for hello new sync member.</span></span> <span data-ttu-id="b41d0-154">這個名稱是 hello 資料庫本身 hello 名稱有所區別。</span><span class="sxs-lookup"><span data-stu-id="b41d0-154">This name is distinct from hello name of hello database itself.</span></span>

2.  <span data-ttu-id="b41d0-155">在 hello**訂用帳戶**欄位時，選取 hello 相關聯的 Azure 訂用帳戶計費。</span><span class="sxs-lookup"><span data-stu-id="b41d0-155">In hello **Subscription** field, select hello associated Azure subscription for billing purposes.</span></span>

3.  <span data-ttu-id="b41d0-156">在 hello **Azure SQL Server** hello 欄位時，選取現有的 SQL 資料庫伺服器。</span><span class="sxs-lookup"><span data-stu-id="b41d0-156">In hello **Azure SQL Server** field, select hello existing SQL database server.</span></span>

4.  <span data-ttu-id="b41d0-157">在 hello **Azure SQL Database** hello 欄位時，選取現有的 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="b41d0-157">In hello **Azure SQL Database** field, select hello existing SQL database.</span></span>

5.  <span data-ttu-id="b41d0-158">在 hello**同步處理方向**欄位中，選取 雙向同步處理 toohello 中樞，或從 hello 中樞。</span><span class="sxs-lookup"><span data-stu-id="b41d0-158">In hello **Sync Directions** field, select Bi-directional Sync, toohello Hub, or From hello Hub.</span></span>

    ![新增 SQL Database 同步處理成員](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadding.png)

6.  <span data-ttu-id="b41d0-160">在 hello **Username**和**密碼**欄位中，輸入 hello 現有認證的 hello SQL 資料庫所在的伺服器上的 hello 成員資料庫。</span><span class="sxs-lookup"><span data-stu-id="b41d0-160">In hello **Username** and **Password** fields, enter hello existing credentials for hello SQL Database server on which hello member database is located.</span></span> <span data-ttu-id="b41d0-161">請不要在此區段輸入「新」的認證。</span><span class="sxs-lookup"><span data-stu-id="b41d0-161">Don't enter *new* credentials in this section.</span></span>

7.  <span data-ttu-id="b41d0-162">選取**確定**並等候 hello 新同步處理成員 toobe 建立和部署。</span><span class="sxs-lookup"><span data-stu-id="b41d0-162">Select **OK** and wait for hello new sync member toobe created and deployed.</span></span>

    ![已新增 SQL Database 同步處理成員](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadded.png)

## <a name="add-an-on-premises-sql-server-database"></a><span data-ttu-id="b41d0-164">新增內部部署 SQL Server 資料庫</span><span class="sxs-lookup"><span data-stu-id="b41d0-164">Add an on-premises SQL Server database</span></span>

<span data-ttu-id="b41d0-165">在 hello**成員資料庫**區段中，選擇性地加入內部部署 SQL Server toohello 同步處理群組選取**加入內部資料庫**。</span><span class="sxs-lookup"><span data-stu-id="b41d0-165">In hello **Member Database** section, optionally add an on-premises SQL Server toohello sync group by selecting **Add an On-Premises Database**.</span></span> <span data-ttu-id="b41d0-166">hello**設定內部部署**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="b41d0-166">hello **Configure On-Premises** blade opens.</span></span>

<span data-ttu-id="b41d0-167">在 hello**設定內部部署**刀鋒視窗中，請勿 hello 下列事項：</span><span class="sxs-lookup"><span data-stu-id="b41d0-167">On hello **Configure On-Premises** blade, do hello following things:</span></span>

1.  <span data-ttu-id="b41d0-168">選取**選擇 hello 同步代理程式的閘道**。</span><span class="sxs-lookup"><span data-stu-id="b41d0-168">Select **Choose hello Sync Agent Gateway**.</span></span> <span data-ttu-id="b41d0-169">hello**選取同步處理代理程式**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="b41d0-169">hello **Select Sync Agent** blade opens.</span></span>

    ![選擇 hello 同步代理程式閘道](media/sql-database-get-started-sql-data-sync/datasync-preview-choosegateway.png)

2.  <span data-ttu-id="b41d0-171">在 hello**選擇 hello 同步代理程式的閘道**刀鋒視窗中，選擇是否 toouse 現有代理程式，或建立新的代理程式。</span><span class="sxs-lookup"><span data-stu-id="b41d0-171">On hello **Choose hello Sync Agent Gateway** blade, choose whether toouse an existing agent or create a new agent.</span></span>

    <span data-ttu-id="b41d0-172">如果您選擇**現有代理程式**，選取 hello hello 清單從現有的代理程式。</span><span class="sxs-lookup"><span data-stu-id="b41d0-172">If you chose **Existing agents**, select hello existing agent from hello list.</span></span>

    <span data-ttu-id="b41d0-173">如果您選擇**建立新的代理程式**，請勿 hello 下列事項：</span><span class="sxs-lookup"><span data-stu-id="b41d0-173">If you chose **Create a new agent**, do hello following things:</span></span>

    1.  <span data-ttu-id="b41d0-174">Hello 用戶端同步代理程式軟體從提供的 hello 連結上下載並安裝它 hello hello SQL Server 所在的電腦。</span><span class="sxs-lookup"><span data-stu-id="b41d0-174">Download hello client sync agent software from hello link provided and install it on hello computer where hello SQL Server is located.</span></span>
 
        > [!IMPORTANT]
        > <span data-ttu-id="b41d0-175">您有 tooopen 傳出 TCP 通訊埠 1433 hello 防火牆 toolet hello 用戶端代理程式中的與 hello 伺服器通訊。</span><span class="sxs-lookup"><span data-stu-id="b41d0-175">You have tooopen outbound TCP port 1433 in hello firewall toolet hello client agent communicate with hello server.</span></span>


    2.  <span data-ttu-id="b41d0-176">輸入 hello 代理程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="b41d0-176">Enter a name for hello agent.</span></span>

    3.  <span data-ttu-id="b41d0-177">選取 [建立並產生金鑰]。</span><span class="sxs-lookup"><span data-stu-id="b41d0-177">Select **Create and Generate Key**.</span></span>

    4.  <span data-ttu-id="b41d0-178">將複製 hello 代理程式金鑰 toohello 剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="b41d0-178">Copy hello agent key toohello clipboard.</span></span>
        
        ![建立新同步代理程式](media/sql-database-get-started-sql-data-sync/datasync-preview-selectsyncagent.png)

    5.  <span data-ttu-id="b41d0-180">選取**確定**tooclose hello**選取同步處理代理程式**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b41d0-180">Select **OK** tooclose hello **Select Sync Agent** blade.</span></span>

    6.  <span data-ttu-id="b41d0-181">Hello SQL Server 電腦上，找出並執行 hello 用戶端同步代理程式的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b41d0-181">On hello SQL Server computer, locate and run hello Client Sync Agent app.</span></span>

        ![hello 資料同步用戶端代理程式的應用程式](media/sql-database-get-started-sql-data-sync/datasync-preview-clientagent.png)

    7.  <span data-ttu-id="b41d0-183">在 hello 同步代理程式應用程式中，選取 **提交代理程式金鑰**。</span><span class="sxs-lookup"><span data-stu-id="b41d0-183">In hello sync agent app, select **Submit Agent Key**.</span></span> <span data-ttu-id="b41d0-184">hello**同步處理中繼資料資料庫組態**對話方塊隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="b41d0-184">hello **Sync Metadata Database Configuration** dialog box opens.</span></span>

    8.  <span data-ttu-id="b41d0-185">在 hello**同步處理中繼資料資料庫組態**對話方塊中，貼上的 從 hello Azure 入口網站複製的 hello 代理程式金鑰。</span><span class="sxs-lookup"><span data-stu-id="b41d0-185">In hello **Sync Metadata Database Configuration** dialog box, paste in hello agent key copied from hello Azure portal.</span></span> <span data-ttu-id="b41d0-186">也提供 hello 現有 hello Azure SQL Database 所在的伺服器上的 hello 中繼資料資料庫認證。</span><span class="sxs-lookup"><span data-stu-id="b41d0-186">Also provide hello existing credentials for hello Azure SQL Database server on which hello metadata database is located.</span></span> <span data-ttu-id="b41d0-187">(如果您建立新的中繼資料資料庫時，這個資料庫是在 hello 與 hello 中樞資料庫相同的伺服器。)選取**確定**並等候 hello 設定 toofinish。</span><span class="sxs-lookup"><span data-stu-id="b41d0-187">(If you created a new metadata database, this database is on hello same server as hello hub database.) Select **OK** and wait for hello configuration toofinish.</span></span>

        ![輸入 hello 代理程式金鑰及伺服器認證](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-enterkey.png)

        >   [!NOTE] 
        >   <span data-ttu-id="b41d0-189">如果此時您會收到防火牆錯誤，您必須 toocreate 防火牆規則上 Azure tooallow 從 hello SQL Server 電腦的連入流量。</span><span class="sxs-lookup"><span data-stu-id="b41d0-189">If you get a firewall error at this point, you have toocreate a firewall rule on Azure tooallow incoming traffic from hello SQL Server computer.</span></span> <span data-ttu-id="b41d0-190">您可以手動建立 hello 規則，在 hello 入口網站，但您可能會發現它更容易 toocreate 它在 SQL Server Management Studio (SSMS)。</span><span class="sxs-lookup"><span data-stu-id="b41d0-190">You can create hello rule manually in hello portal, but you may find it easier toocreate it in SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="b41d0-191">在 SSMS 中，請嘗試在 Azure 上的 tooconnect toohello 中樞資料庫。</span><span class="sxs-lookup"><span data-stu-id="b41d0-191">In SSMS, try tooconnect toohello hub database on Azure.</span></span> <span data-ttu-id="b41d0-192">請將其名稱輸入為 \<hub_database_name\>.database.windows.net。</span><span class="sxs-lookup"><span data-stu-id="b41d0-192">Enter its name as \<hub_database_name\>.database.windows.net.</span></span> <span data-ttu-id="b41d0-193">請遵循 hello hello 對話方塊方塊 tooconfigure hello Azure 防火牆規則中的步驟。</span><span class="sxs-lookup"><span data-stu-id="b41d0-193">Follow hello steps in hello dialog box tooconfigure hello Azure firewall rule.</span></span> <span data-ttu-id="b41d0-194">然後傳回 toohello 用戶端同步代理程式的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b41d0-194">Then return toohello Client Sync Agent app.</span></span>

    9.  <span data-ttu-id="b41d0-195">在 hello 用戶端同步代理程式應用程式中，按一下 **註冊**tooregister hello 代理程式的 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="b41d0-195">In hello Client Sync Agent app, click **Register** tooregister a SQL Server database with hello agent.</span></span> <span data-ttu-id="b41d0-196">hello **SQL Server 組態**對話方塊隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="b41d0-196">hello **SQL Server Configuration** dialog box opens.</span></span>

        ![新增和設定 SQL Server 資料庫](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-adddb.png)

    10. <span data-ttu-id="b41d0-198">在 hello **SQL Server 組態**對話方塊方塊中，選擇是否 tooconnect 使用 SQL Server 驗證或 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="b41d0-198">In hello **SQL Server Configuration** dialog box, choose whether tooconnect by using SQL Server authentication or Windows authentication.</span></span> <span data-ttu-id="b41d0-199">如果您選擇 SQL Server 驗證，請輸入 hello 現有的認證。</span><span class="sxs-lookup"><span data-stu-id="b41d0-199">If you chose SQL Server authentication, enter hello existing credentials.</span></span> <span data-ttu-id="b41d0-200">提供您想 toosync hello SQL Server 名稱和 hello hello 資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="b41d0-200">Provide hello SQL Server name and hello name of hello database that you want toosync.</span></span> <span data-ttu-id="b41d0-201">選取**測試連接**tootest 您的設定。</span><span class="sxs-lookup"><span data-stu-id="b41d0-201">Select **Test connection** tootest your settings.</span></span> <span data-ttu-id="b41d0-202">然後選取 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="b41d0-202">Then select **Save**.</span></span> <span data-ttu-id="b41d0-203">hello 註冊的資料庫會出現在 [hello] 清單。</span><span class="sxs-lookup"><span data-stu-id="b41d0-203">hello registered database appears in hello list.</span></span>

        ![現在已註冊 SQL Server 資料庫](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-dbadded.png)

    11. <span data-ttu-id="b41d0-205">您現在可以關閉 hello 用戶端同步代理程式的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b41d0-205">You can now close hello Client Sync Agent app.</span></span>

    12. <span data-ttu-id="b41d0-206">在 hello 入口網站上 hello**設定內部部署**刀鋒視窗中，選取**選取 hello 資料庫。**</span><span class="sxs-lookup"><span data-stu-id="b41d0-206">In hello portal, on hello **Configure On-Premises** blade, select **Select hello Database.**</span></span> <span data-ttu-id="b41d0-207">hello**選取資料庫**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="b41d0-207">hello **Select Database** blade opens.</span></span>

    13. <span data-ttu-id="b41d0-208">在 hello**選取資料庫**刀鋒視窗中的，在 hello**同步成員名稱**欄位中，提供 hello 新同步處理成員的名稱。</span><span class="sxs-lookup"><span data-stu-id="b41d0-208">On hello **Select Database** blade, in hello **Sync Member Name** field, provide a name for hello new sync member.</span></span> <span data-ttu-id="b41d0-209">這個名稱是 hello 資料庫本身 hello 名稱有所區別。</span><span class="sxs-lookup"><span data-stu-id="b41d0-209">This name is distinct from hello name of hello database itself.</span></span> <span data-ttu-id="b41d0-210">Hello 清單中選取 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="b41d0-210">Select hello database from hello list.</span></span> <span data-ttu-id="b41d0-211">在 hello**同步處理方向**欄位中，選取 雙向同步處理 toohello 中樞，或從 hello 中樞。</span><span class="sxs-lookup"><span data-stu-id="b41d0-211">In hello **Sync Directions** field, select Bi-directional Sync, toohello Hub, or From hello Hub.</span></span>

        ![選取在內部部署資料庫上的 hello](media/sql-database-get-started-sql-data-sync/datasync-preview-selectdb.png)

    14. <span data-ttu-id="b41d0-213">選取**確定**tooclose hello**選取資料庫**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b41d0-213">Select **OK** tooclose hello **Select Database** blade.</span></span> <span data-ttu-id="b41d0-214">然後選取**確定**tooclose hello**設定內部部署**刀鋒視窗，然後等候 hello 新同步處理成員 toobe 建立和部署。</span><span class="sxs-lookup"><span data-stu-id="b41d0-214">Then select **OK** tooclose hello **Configure On-Premises** blade and wait for hello new sync member toobe created and deployed.</span></span> <span data-ttu-id="b41d0-215">最後，按一下 **確定**tooclose hello**選取同步處理成員**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b41d0-215">Finally, click **OK** tooclose hello **Select sync members** blade.</span></span>

        ![內部部署資料庫上加入 toosync 群組](media/sql-database-get-started-sql-data-sync/datasync-preview-onpremadded.png)

3.  <span data-ttu-id="b41d0-217">tooconnect tooSQL 資料同步處理與 hello 本機代理程式，新增您的使用者名稱 toohello 角色`DataSync_Executor`。</span><span class="sxs-lookup"><span data-stu-id="b41d0-217">tooconnect tooSQL Data Sync and hello local agent, add your user name toohello role `DataSync_Executor`.</span></span> <span data-ttu-id="b41d0-218">資料同步 hello SQL Server 執行個體上建立此角色。</span><span class="sxs-lookup"><span data-stu-id="b41d0-218">Data Sync creates this role on hello SQL Server instance.</span></span>

## <a name="step-3---configure-sync-group"></a><span data-ttu-id="b41d0-219">步驟 3 - 設定同步群組</span><span class="sxs-lookup"><span data-stu-id="b41d0-219">Step 3 - Configure sync group</span></span>

<span data-ttu-id="b41d0-220">Hello 新同步處理群組成員建立和部署，第 3 步驟之後**設定同步處理群組**，會反白顯示在 hello**新同步處理群組**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b41d0-220">After hello new sync group members are created and deployed, Step 3, **Configure sync group**, is highlighted in hello **New sync group** blade.</span></span>

1.  <span data-ttu-id="b41d0-221">在 hello**資料表**刀鋒視窗中，選取資料庫的同步處理的 hello 清單從群組成員，然後選取**重新整理結構描述**。</span><span class="sxs-lookup"><span data-stu-id="b41d0-221">On hello **Tables** blade, select a database from hello list of sync group members, and then select **Refresh schema**.</span></span>

2.  <span data-ttu-id="b41d0-222">從 hello 的可用資料表清單，選取您想 toosync hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="b41d0-222">From hello list of available tables, select hello tables that you want toosync.</span></span>

    ![選擇資料表 toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables.png)

3.  <span data-ttu-id="b41d0-224">根據預設，會選取 hello 資料表中的所有資料行。</span><span class="sxs-lookup"><span data-stu-id="b41d0-224">By default, all columns in hello table are selected.</span></span> <span data-ttu-id="b41d0-225">如果您不想 toosync hello 的所有資料行，停用 hello 核取方塊，您不想 toosync hello 資料行。</span><span class="sxs-lookup"><span data-stu-id="b41d0-225">If you don't want toosync all hello columns, disable hello checkbox for hello columns that you don't want toosync.</span></span> <span data-ttu-id="b41d0-226">請確定 tooleave hello 主索引鍵資料行選取。</span><span class="sxs-lookup"><span data-stu-id="b41d0-226">Be sure tooleave hello primary key column selected.</span></span>

    ![選取欄位 toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables2.png)

4.  <span data-ttu-id="b41d0-228">最後，選取 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="b41d0-228">Finally, select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b41d0-229">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b41d0-229">Next steps</span></span>
<span data-ttu-id="b41d0-230">恭喜！</span><span class="sxs-lookup"><span data-stu-id="b41d0-230">Congratulations.</span></span> <span data-ttu-id="b41d0-231">您已建立一個同時包含 SQL Database 執行個體與 SQL Server 資料庫的同步群組。</span><span class="sxs-lookup"><span data-stu-id="b41d0-231">You have created a sync group that includes both a SQL Database instance and a SQL Server database.</span></span>

<span data-ttu-id="b41d0-232">如需 SQL Database 和 SQL 資料同步的詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="b41d0-232">For more info about SQL Database and SQL Data Sync, see:</span></span>

-   [<span data-ttu-id="b41d0-233">下載 hello 完整 SQL 資料同步技術文件</span><span class="sxs-lookup"><span data-stu-id="b41d0-233">Download hello complete SQL Data Sync technical documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)
-   [<span data-ttu-id="b41d0-234">下載 SQL 資料同步處理的 REST API 文件以 hello</span><span class="sxs-lookup"><span data-stu-id="b41d0-234">Download hello SQL Data Sync REST API documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)
-   [<span data-ttu-id="b41d0-235">SQL Database 概觀</span><span class="sxs-lookup"><span data-stu-id="b41d0-235">SQL Database Overview</span></span>](sql-database-technical-overview.md)
-   [<span data-ttu-id="b41d0-236">資料庫生命週期管理</span><span class="sxs-lookup"><span data-stu-id="b41d0-236">Database Lifecycle Management</span></span>](https://msdn.microsoft.com/library/jj907294.aspx)
