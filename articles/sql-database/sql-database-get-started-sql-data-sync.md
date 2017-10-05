---
title: "開始使用 Azure SQL 資料同步 (預覽) | Microsoft Docs"
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
ms.openlocfilehash: 2d0f9d7f32ad79f49d58165d734b9df4af862835
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="getting-started-with-azure-sql-data-sync-preview"></a><span data-ttu-id="374fe-103">開始使用 Azure SQL 資料同步 (預覽)</span><span class="sxs-lookup"><span data-stu-id="374fe-103">Getting Started with Azure SQL Data Sync (Preview)</span></span>
<span data-ttu-id="374fe-104">在本教學課程中，您將了解如何使用包含 Azure SQL Database 和 SQL Server 執行個體的混合式同步群組設定 Azure SQL 資料同步。</span><span class="sxs-lookup"><span data-stu-id="374fe-104">In this tutorial, you learn how to set up Azure SQL Data Sync by creating a hybrid sync group that contains both Azure SQL Database and SQL Server instances.</span></span> <span data-ttu-id="374fe-105">新的同步處理群組會依照您設定的排程完整設定和同步。</span><span class="sxs-lookup"><span data-stu-id="374fe-105">The new sync group is fully configured and synchronizes on the schedule you set.</span></span>

<span data-ttu-id="374fe-106">本教學課程假設您先前至少有一些使用 SQL Database 和 SQL Server 的經驗。</span><span class="sxs-lookup"><span data-stu-id="374fe-106">This tutorial assumes that you have at least some prior experience with SQL Database and with SQL Server.</span></span> 

<span data-ttu-id="374fe-107">如需 SQL 資料同步處理的概觀，請參閱[同步資料](sql-database-sync-data.md)。</span><span class="sxs-lookup"><span data-stu-id="374fe-107">For an overview of SQL Data Sync, see [Sync data](sql-database-sync-data.md).</span></span>

<span data-ttu-id="374fe-108">如需示範如何設定 SQL 資料同步的完整 PowerShell 範例，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="374fe-108">For complete PowerShell examples that show how to configure SQL Data Sync, see the following articles:</span></span>
-   [<span data-ttu-id="374fe-109">使用 PowerShell 在多個 Azure SQL Database 之間進行同步處理</span><span class="sxs-lookup"><span data-stu-id="374fe-109">Use PowerShell to sync between multiple Azure SQL databases</span></span>](scripts/sql-database-sync-data-between-sql-databases.md)
-   [<span data-ttu-id="374fe-110">使用 PowerShell 設定「資料同步」在內部部署的 Azure SQL Database 和 SQL Server 之間進行同步處理</span><span class="sxs-lookup"><span data-stu-id="374fe-110">Use PowerShell to sync between an Azure SQL Database and a SQL Server on-premises database</span></span>](scripts/sql-database-sync-data-between-azure-onprem.md)

> [!NOTE]
> <span data-ttu-id="374fe-111">Azure SQL 資料同步的完整技術文件集 (先前位於 MSDN 上) 現已透過 .PDF 文件提供使用。</span><span class="sxs-lookup"><span data-stu-id="374fe-111">The complete technical documentation set for Azure SQL Data Sync, formerly located on MSDN, is available as a .PDF document.</span></span> <span data-ttu-id="374fe-112">在 [這裡](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)下載。</span><span class="sxs-lookup"><span data-stu-id="374fe-112">Download it [here](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true).</span></span>

## <a name="step-1---create-sync-group"></a><span data-ttu-id="374fe-113">步驟 1 - 建立同步群組</span><span class="sxs-lookup"><span data-stu-id="374fe-113">Step 1 - Create sync group</span></span>

### <a name="locate-the-data-sync-settings"></a><span data-ttu-id="374fe-114">尋找資料同步設定</span><span class="sxs-lookup"><span data-stu-id="374fe-114">Locate the Data Sync settings</span></span>

1.  <span data-ttu-id="374fe-115">在瀏覽器中導覽至 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="374fe-115">In your browser, navigate to the Azure portal.</span></span>

2.  <span data-ttu-id="374fe-116">在入口網站中，從您的儀表板或從工具列上的 SQL Database 圖示找出 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="374fe-116">In the portal, locate your SQL databases from your Dashboard or from the SQL Databases icon on the toolbar.</span></span>

    ![Azure SQL 資料庫清單](media/sql-database-get-started-sql-data-sync/datasync-preview-sqldbs.png)

3.  <span data-ttu-id="374fe-118">在 [SQL 資料庫] 刀鋒視窗中，選取您想要作為資料同步的中樞資料庫使用的現有 SQL 資料庫。[SQL 資料庫] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="374fe-118">On the **SQL databases** blade, select the existing SQL database that you want to use as the hub database for Data Sync. The SQL database blade opens.</span></span>

4.  <span data-ttu-id="374fe-119">在所選取資料庫的 [SQL 資料庫] 刀鋒視窗上，選取 [同步至其他資料庫]。</span><span class="sxs-lookup"><span data-stu-id="374fe-119">On the SQL database blade for the selected database, select **Sync to other databases**.</span></span> <span data-ttu-id="374fe-120">[資料同步] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="374fe-120">The Data Sync blade opens.</span></span>

    ![[同步至其他資料庫] 選項](media/sql-database-get-started-sql-data-sync/datasync-preview-newsyncgroup.png)

### <a name="create-a-new-sync-group"></a><span data-ttu-id="374fe-122">建立新的同步群組</span><span class="sxs-lookup"><span data-stu-id="374fe-122">Create a new Sync Group</span></span>

1.  <span data-ttu-id="374fe-123">在 [資料同步] 刀鋒視窗中，選取 [新的同步群組]。</span><span class="sxs-lookup"><span data-stu-id="374fe-123">On the Data Sync blade, select **New Sync Group**.</span></span> <span data-ttu-id="374fe-124">[新的同步群組] 刀鋒視窗隨即開啟，反白顯示步驟 1 [建立同步群組]。</span><span class="sxs-lookup"><span data-stu-id="374fe-124">The **New sync group** blade opens with Step 1, **Create sync group**, highlighted.</span></span> <span data-ttu-id="374fe-125">還會開啟 [建立資料同步群組] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="374fe-125">The **Create Data Sync Group** blade also opens.</span></span>

2.  <span data-ttu-id="374fe-126">在 [建立資料同步群組] 刀鋒視窗中，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="374fe-126">On the **Create Data Sync Group** blade, do the following things:</span></span>

    1.  <span data-ttu-id="374fe-127">在 [同步群組名稱] 欄位中，輸入新同步群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="374fe-127">In the **Sync Group Name** field, enter a name for the new sync group.</span></span>

    2.  <span data-ttu-id="374fe-128">在 [同步中繼資料的資料庫] 區段中，選擇要建立新的資料庫 (建議) 或使用現有的資料庫。</span><span class="sxs-lookup"><span data-stu-id="374fe-128">In the **Sync Metadata Database** section, choose whether to create a new database (recommended) or to use an existing database.</span></span>

        > [!NOTE]
        > <span data-ttu-id="374fe-129">Microsoft 建議您建立新的空白資料庫作為同步中繼資料的資料庫。</span><span class="sxs-lookup"><span data-stu-id="374fe-129">Microsoft recommends that you create a new, empty database to use as the Sync Metadata Database.</span></span> <span data-ttu-id="374fe-130">資料同步會在此資料庫中建立資料表，並頻繁執行工作負載。</span><span class="sxs-lookup"><span data-stu-id="374fe-130">Data Sync creates tables in this database and runs a frequent workload.</span></span> <span data-ttu-id="374fe-131">這個資料庫會作為同步中繼資料的資料庫，自動和選取區域中所有同步群組共用。</span><span class="sxs-lookup"><span data-stu-id="374fe-131">This database is automatically shared as the Sync Metadata Database for all of your Sync groups in the selected region.</span></span> <span data-ttu-id="374fe-132">您必須先卸除同步中繼資料的資料庫之後，才能變更它、它的名稱或其服務等級。</span><span class="sxs-lookup"><span data-stu-id="374fe-132">You can't change the Sync Metadata Database, its name, or its service level without dropping it.</span></span>

        <span data-ttu-id="374fe-133">如果您選擇 [新資料庫]，請選取 [建立新的資料庫]。</span><span class="sxs-lookup"><span data-stu-id="374fe-133">If you chose **New database**, select **Create new database.**</span></span> <span data-ttu-id="374fe-134">[SQL Database] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="374fe-134">The **SQL Database** blade opens.</span></span> <span data-ttu-id="374fe-135">在 [SQL Database] 刀鋒視窗中，命名並設定新的資料庫。</span><span class="sxs-lookup"><span data-stu-id="374fe-135">On the **SQL Database** blade, name and configure the new database.</span></span> <span data-ttu-id="374fe-136">然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="374fe-136">Then select **OK**.</span></span>

        <span data-ttu-id="374fe-137">如果您選擇 [現有的資料庫]，請從清單中選取資料庫。</span><span class="sxs-lookup"><span data-stu-id="374fe-137">If you chose **Use existing database**, select the database from the list.</span></span>

    3.  <span data-ttu-id="374fe-138">在 [自動同步] 區段中，先選取 [開啟] 或 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="374fe-138">In the **Automatic Sync** section, first select **On** or **Off**.</span></span>

        <span data-ttu-id="374fe-139">如果您選擇 [開啟]，請在 [同步處理頻率] 區段中輸入數字，然後選取 [秒]、[分鐘]、[小時] 或 [天]。</span><span class="sxs-lookup"><span data-stu-id="374fe-139">If you chose **On**, in the **Sync Frequency** section, enter a number and select Seconds, Minutes, Hours, or Days.</span></span>

        ![指定同步處理頻率](media/sql-database-get-started-sql-data-sync/datasync-preview-syncfreq.png)

    4.  <span data-ttu-id="374fe-141">在 [衝突解決] 區段中，選取 [中樞獲勝] 或 [成員獲勝]。</span><span class="sxs-lookup"><span data-stu-id="374fe-141">In the **Conflict Resolution** section, select "Hub wins" or "Member wins."</span></span>

        ![指定解決衝突的方式](media/sql-database-get-started-sql-data-sync/datasync-preview-conflictres.png)

    5.  <span data-ttu-id="374fe-143">選取 [確定] 並等候新的同步群組建立和部署完成。</span><span class="sxs-lookup"><span data-stu-id="374fe-143">Select **OK** and wait for the new sync group to be created and deployed.</span></span>

## <a name="step-2---add-sync-members"></a><span data-ttu-id="374fe-144">步驟 2 - 新增同步成員</span><span class="sxs-lookup"><span data-stu-id="374fe-144">Step 2 - Add sync members</span></span>

<span data-ttu-id="374fe-145">在建立和部署新的同步群組之後，會反白顯示 [新的同步群組] 刀鋒視窗中的步驟 2 [新增同步成員]。</span><span class="sxs-lookup"><span data-stu-id="374fe-145">After the new sync group is created and deployed, Step 2, **Add sync members**, is highlighted in the **New sync group** blade.</span></span>

<span data-ttu-id="374fe-146">在 [中樞資料庫] 區段中，輸入中樞資料庫所在 SQL Database 伺服器的現有認證。</span><span class="sxs-lookup"><span data-stu-id="374fe-146">In the **Hub Database** section, enter the existing credentials for the SQL Database server on which the hub database is located.</span></span> <span data-ttu-id="374fe-147">請不要在此區段輸入「新」的認證。</span><span class="sxs-lookup"><span data-stu-id="374fe-147">Don't enter *new* credentials in this section.</span></span>

![中樞資料庫已新增至同步群組](media/sql-database-get-started-sql-data-sync/datasync-preview-hubadded.png)

## <a name="add-an-azure-sql-database"></a><span data-ttu-id="374fe-149">新增 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="374fe-149">Add an Azure SQL Database</span></span>

<span data-ttu-id="374fe-150">在 [成員資料庫] 區段中，選取 [新增 Azure 資料庫]，可選擇性地將 Azure SQL Database 新增至同步群組。</span><span class="sxs-lookup"><span data-stu-id="374fe-150">In the **Member Database** section, optionally add an Azure SQL Database to the sync group by selecting **Add an Azure Database**.</span></span> <span data-ttu-id="374fe-151">[設定 Azure 資料庫] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="374fe-151">The **Configure Azure Database** blade opens.</span></span>

<span data-ttu-id="374fe-152">在 [設定 Azure 資料庫] 刀鋒視窗中，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="374fe-152">On the **Configure Azure Database** blade, do the following things:</span></span>

1.  <span data-ttu-id="374fe-153">在 [同步成員名稱] 欄位中，提供新同步成員的名稱。</span><span class="sxs-lookup"><span data-stu-id="374fe-153">In the **Sync Member Name** field, provide a name for the new sync member.</span></span> <span data-ttu-id="374fe-154">這個名稱與資料庫本身的名稱不同。</span><span class="sxs-lookup"><span data-stu-id="374fe-154">This name is distinct from the name of the database itself.</span></span>

2.  <span data-ttu-id="374fe-155">在 [訂用帳戶] 欄位中，選取相關聯的 Azure 訂用帳戶以便計費。</span><span class="sxs-lookup"><span data-stu-id="374fe-155">In the **Subscription** field, select the associated Azure subscription for billing purposes.</span></span>

3.  <span data-ttu-id="374fe-156">在 [Azure SQL Server] 欄位中，選取現有的 SQL 資料庫伺服器。</span><span class="sxs-lookup"><span data-stu-id="374fe-156">In the **Azure SQL Server** field, select the existing SQL database server.</span></span>

4.  <span data-ttu-id="374fe-157">在 [Azure SQL Database] 欄位中，選取現有的 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="374fe-157">In the **Azure SQL Database** field, select the existing SQL database.</span></span>

5.  <span data-ttu-id="374fe-158">在 [同步方向] 欄位中，選取 [雙向同步]、[至中樞] 或 [來自中樞]。</span><span class="sxs-lookup"><span data-stu-id="374fe-158">In the **Sync Directions** field, select Bi-directional Sync, To the Hub, or From the Hub.</span></span>

    ![新增 SQL Database 同步處理成員](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadding.png)

6.  <span data-ttu-id="374fe-160">在 [使用者名稱] 和 [密碼] 欄位中，輸入成員資料庫所在 SQL Database 伺服器的現有認證。</span><span class="sxs-lookup"><span data-stu-id="374fe-160">In the **Username** and **Password** fields, enter the existing credentials for the SQL Database server on which the member database is located.</span></span> <span data-ttu-id="374fe-161">請不要在此區段輸入「新」的認證。</span><span class="sxs-lookup"><span data-stu-id="374fe-161">Don't enter *new* credentials in this section.</span></span>

7.  <span data-ttu-id="374fe-162">選取 [確定] 並等候新的同步成員建立和部署完成。</span><span class="sxs-lookup"><span data-stu-id="374fe-162">Select **OK** and wait for the new sync member to be created and deployed.</span></span>

    ![已新增 SQL Database 同步處理成員](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadded.png)

## <a name="add-an-on-premises-sql-server-database"></a><span data-ttu-id="374fe-164">新增內部部署 SQL Server 資料庫</span><span class="sxs-lookup"><span data-stu-id="374fe-164">Add an on-premises SQL Server database</span></span>

<span data-ttu-id="374fe-165">在 [成員資料庫] 區段中，選取 [新增內部部署資料庫]，可選擇性地將內部部署 SQL Server 新增至同步群組。</span><span class="sxs-lookup"><span data-stu-id="374fe-165">In the **Member Database** section, optionally add an on-premises SQL Server to the sync group by selecting **Add an On-Premises Database**.</span></span> <span data-ttu-id="374fe-166">[設定內部部署] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="374fe-166">The **Configure On-Premises** blade opens.</span></span>

<span data-ttu-id="374fe-167">在 [設定內部部署] 刀鋒視窗中，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="374fe-167">On the **Configure On-Premises** blade, do the following things:</span></span>

1.  <span data-ttu-id="374fe-168">選取 [選擇同步代理程式閘道]。</span><span class="sxs-lookup"><span data-stu-id="374fe-168">Select **Choose the Sync Agent Gateway**.</span></span> <span data-ttu-id="374fe-169">[選取同步代理程式] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="374fe-169">The **Select Sync Agent** blade opens.</span></span>

    ![選擇同步代理程式閘道](media/sql-database-get-started-sql-data-sync/datasync-preview-choosegateway.png)

2.  <span data-ttu-id="374fe-171">在 [選擇同步代理程式閘道] 刀鋒視窗中，選擇要使用現有的代理程式，或建立新的代理程式。</span><span class="sxs-lookup"><span data-stu-id="374fe-171">On the **Choose the Sync Agent Gateway** blade, choose whether to use an existing agent or create a new agent.</span></span>

    <span data-ttu-id="374fe-172">如果您選擇 [現有代理程式]，請從清單中選取現有的代理程式。</span><span class="sxs-lookup"><span data-stu-id="374fe-172">If you chose **Existing agents**, select the existing agent from the list.</span></span>

    <span data-ttu-id="374fe-173">在 [建立新的代理程式] 刀鋒視窗中，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="374fe-173">If you chose **Create a new agent**, do the following things:</span></span>

    1.  <span data-ttu-id="374fe-174">從提供的連結下載用戶端同步代理程式軟體，並安裝在 SQL Server 所在的電腦上。</span><span class="sxs-lookup"><span data-stu-id="374fe-174">Download the client sync agent software from the link provided and install it on the computer where the SQL Server is located.</span></span>
 
        > [!IMPORTANT]
        > <span data-ttu-id="374fe-175">您必須在防火牆開啟輸出 TCP 連接埠 1433，以讓用戶端代理程式和伺服器通訊。</span><span class="sxs-lookup"><span data-stu-id="374fe-175">You have to open outbound TCP port 1433 in the firewall to let the client agent communicate with the server.</span></span>


    2.  <span data-ttu-id="374fe-176">輸入代理程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="374fe-176">Enter a name for the agent.</span></span>

    3.  <span data-ttu-id="374fe-177">選取 [建立並產生金鑰]。</span><span class="sxs-lookup"><span data-stu-id="374fe-177">Select **Create and Generate Key**.</span></span>

    4.  <span data-ttu-id="374fe-178">將代理程式金鑰複製到剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="374fe-178">Copy the agent key to the clipboard.</span></span>
        
        ![建立新同步代理程式](media/sql-database-get-started-sql-data-sync/datasync-preview-selectsyncagent.png)

    5.  <span data-ttu-id="374fe-180">選取 [確定] 以關閉 [選取同步代理程式] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="374fe-180">Select **OK** to close the **Select Sync Agent** blade.</span></span>

    6.  <span data-ttu-id="374fe-181">在 SQL Server 電腦上，找出並執行用戶端同步代理程式應用程式。</span><span class="sxs-lookup"><span data-stu-id="374fe-181">On the SQL Server computer, locate and run the Client Sync Agent app.</span></span>

        ![資料同步用戶端代理程式應用程式](media/sql-database-get-started-sql-data-sync/datasync-preview-clientagent.png)

    7.  <span data-ttu-id="374fe-183">在同步處理代理程式應用程式中，選取 [提交代理程式金鑰]。</span><span class="sxs-lookup"><span data-stu-id="374fe-183">In the sync agent app, select **Submit Agent Key**.</span></span> <span data-ttu-id="374fe-184">[同步中繼資料的資料庫組態] 對話方塊隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="374fe-184">The **Sync Metadata Database Configuration** dialog box opens.</span></span>

    8.  <span data-ttu-id="374fe-185">在 [同步中繼資料的資料庫組態] 對話方塊中，貼上從 Azure 入口網站複製的代理程式金鑰。</span><span class="sxs-lookup"><span data-stu-id="374fe-185">In the **Sync Metadata Database Configuration** dialog box, paste in the agent key copied from the Azure portal.</span></span> <span data-ttu-id="374fe-186">還要提供輸入中繼資料資料庫所在 Azure SQL Database 伺服器的現有認證。</span><span class="sxs-lookup"><span data-stu-id="374fe-186">Also provide the existing credentials for the Azure SQL Database server on which the metadata database is located.</span></span> <span data-ttu-id="374fe-187">(如果您已建立新的中繼資料資料庫，此資料庫會位在和中樞資料庫相同的伺服器)。選取 [確定] 並等待完成組態。</span><span class="sxs-lookup"><span data-stu-id="374fe-187">(If you created a new metadata database, this database is on the same server as the hub database.) Select **OK** and wait for the configuration to finish.</span></span>

        ![輸入代理程式金鑰和伺服器認證](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-enterkey.png)

        >   [!NOTE] 
        >   <span data-ttu-id="374fe-189">如果在此時收到防火牆錯誤，您必須在 Azure 上建立防火牆規則，以允許來自 SQL Server 電腦的傳入流量。</span><span class="sxs-lookup"><span data-stu-id="374fe-189">If you get a firewall error at this point, you have to create a firewall rule on Azure to allow incoming traffic from the SQL Server computer.</span></span> <span data-ttu-id="374fe-190">您可以在入口網站手動建立規則，但在 SQL Server Management Studio (SSMS) 中建立可能會更容易。</span><span class="sxs-lookup"><span data-stu-id="374fe-190">You can create the rule manually in the portal, but you may find it easier to create it in SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="374fe-191">在 SSMS 中，嘗試連線到 Azure 上的中樞資料庫。</span><span class="sxs-lookup"><span data-stu-id="374fe-191">In SSMS, try to connect to the hub database on Azure.</span></span> <span data-ttu-id="374fe-192">請將其名稱輸入為 \<hub_database_name\>.database.windows.net。</span><span class="sxs-lookup"><span data-stu-id="374fe-192">Enter its name as \<hub_database_name\>.database.windows.net.</span></span> <span data-ttu-id="374fe-193">依照對話方塊中的步驟進行來設定 Azure 防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="374fe-193">Follow the steps in the dialog box to configure the Azure firewall rule.</span></span> <span data-ttu-id="374fe-194">然後返回用戶端同步代理程式應用程式。</span><span class="sxs-lookup"><span data-stu-id="374fe-194">Then return to the Client Sync Agent app.</span></span>

    9.  <span data-ttu-id="374fe-195">在用戶端同步代理程式應用程式中，按一下 [註冊]，以向代理程式註冊 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="374fe-195">In the Client Sync Agent app, click **Register** to register a SQL Server database with the agent.</span></span> <span data-ttu-id="374fe-196">[SQL Server 組態] 對話方塊隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="374fe-196">The **SQL Server Configuration** dialog box opens.</span></span>

        ![新增和設定 SQL Server 資料庫](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-adddb.png)

    10. <span data-ttu-id="374fe-198">在 [SQL Server 組態] 對話方塊方塊中，選擇要使用 SQL Server 驗證或 Windows 驗證來連線。</span><span class="sxs-lookup"><span data-stu-id="374fe-198">In the **SQL Server Configuration** dialog box, choose whether to connect by using SQL Server authentication or Windows authentication.</span></span> <span data-ttu-id="374fe-199">如果您選擇 SQL Server 驗證，請輸入現有的認證。</span><span class="sxs-lookup"><span data-stu-id="374fe-199">If you chose SQL Server authentication, enter the existing credentials.</span></span> <span data-ttu-id="374fe-200">提供 SQL Server 名稱和您要同步之資料庫的名稱。選取 [測試連接] 來測試您的設定。</span><span class="sxs-lookup"><span data-stu-id="374fe-200">Provide the SQL Server name and the name of the database that you want to sync. Select **Test connection** to test your settings.</span></span> <span data-ttu-id="374fe-201">然後選取 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="374fe-201">Then select **Save**.</span></span> <span data-ttu-id="374fe-202">已註冊的資料庫會出現在清單中。</span><span class="sxs-lookup"><span data-stu-id="374fe-202">The registered database appears in the list.</span></span>

        ![現在已註冊 SQL Server 資料庫](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-dbadded.png)

    11. <span data-ttu-id="374fe-204">您現在可以關閉用戶端同步代理程式應用程式。</span><span class="sxs-lookup"><span data-stu-id="374fe-204">You can now close the Client Sync Agent app.</span></span>

    12. <span data-ttu-id="374fe-205">在入口網站的 [設定內部部署] 刀鋒視窗上，選取 [選取資料庫] 。</span><span class="sxs-lookup"><span data-stu-id="374fe-205">In the portal, on the **Configure On-Premises** blade, select **Select the Database.**</span></span> <span data-ttu-id="374fe-206">[選取資料庫] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="374fe-206">The **Select Database** blade opens.</span></span>

    13. <span data-ttu-id="374fe-207">在 [選取資料庫] 刀鋒視窗上的 [同步成員名稱] 欄位中，提供新同步成員的名稱。</span><span class="sxs-lookup"><span data-stu-id="374fe-207">On the **Select Database** blade, in the **Sync Member Name** field, provide a name for the new sync member.</span></span> <span data-ttu-id="374fe-208">這個名稱與資料庫本身的名稱不同。</span><span class="sxs-lookup"><span data-stu-id="374fe-208">This name is distinct from the name of the database itself.</span></span> <span data-ttu-id="374fe-209">從清單中選取資料庫。</span><span class="sxs-lookup"><span data-stu-id="374fe-209">Select the database from the list.</span></span> <span data-ttu-id="374fe-210">在 [同步方向] 欄位中，選取 [雙向同步]、[至中樞] 或 [來自中樞]。</span><span class="sxs-lookup"><span data-stu-id="374fe-210">In the **Sync Directions** field, select Bi-directional Sync, To the Hub, or From the Hub.</span></span>

        ![選取內部部署資料庫](media/sql-database-get-started-sql-data-sync/datasync-preview-selectdb.png)

    14. <span data-ttu-id="374fe-212">選取 [確定] 以關閉 [選取資料庫] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="374fe-212">Select **OK** to close the **Select Database** blade.</span></span> <span data-ttu-id="374fe-213">然後選取 [確定] 以關閉 [設定內部部署] 刀鋒視窗，並等候新的同步成員建立和部署完成。</span><span class="sxs-lookup"><span data-stu-id="374fe-213">Then select **OK** to close the **Configure On-Premises** blade and wait for the new sync member to be created and deployed.</span></span> <span data-ttu-id="374fe-214">最後，按一下 [確定] 以關閉 [選取同步成員] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="374fe-214">Finally, click **OK** to close the **Select sync members** blade.</span></span>

        ![內部部署資料庫已新增至同步群組](media/sql-database-get-started-sql-data-sync/datasync-preview-onpremadded.png)

3.  <span data-ttu-id="374fe-216">若要連接到 [SQL 資料同步] 和本機代理程式，請將您的使用者名稱新增至 `DataSync_Executor` 角色。</span><span class="sxs-lookup"><span data-stu-id="374fe-216">To connect to SQL Data Sync and the local agent, add your user name to the role `DataSync_Executor`.</span></span> <span data-ttu-id="374fe-217">資料同步會在 SQL Server 執行個體上建立此角色。</span><span class="sxs-lookup"><span data-stu-id="374fe-217">Data Sync creates this role on the SQL Server instance.</span></span>

## <a name="step-3---configure-sync-group"></a><span data-ttu-id="374fe-218">步驟 3 - 設定同步群組</span><span class="sxs-lookup"><span data-stu-id="374fe-218">Step 3 - Configure sync group</span></span>

<span data-ttu-id="374fe-219">在建立和部署新的同步群組成員之後，會反白顯示 [新的同步群組] 刀鋒視窗中的步驟 3 [設定同步群組]。</span><span class="sxs-lookup"><span data-stu-id="374fe-219">After the new sync group members are created and deployed, Step 3, **Configure sync group**, is highlighted in the **New sync group** blade.</span></span>

1.  <span data-ttu-id="374fe-220">在 [資料表] 刀鋒視窗上，從同步群組成員清單中選取資料庫，然後選取 [重新整理結構描述]。</span><span class="sxs-lookup"><span data-stu-id="374fe-220">On the **Tables** blade, select a database from the list of sync group members, and then select **Refresh schema**.</span></span>

2.  <span data-ttu-id="374fe-221">從可用資料表清單中，選取您想要同步的資料表。</span><span class="sxs-lookup"><span data-stu-id="374fe-221">From the list of available tables, select the tables that you want to sync.</span></span>

    ![選取要同步的資料表](media/sql-database-get-started-sql-data-sync/datasync-preview-tables.png)

3.  <span data-ttu-id="374fe-223">預設會選取資料表中的所有資料行。</span><span class="sxs-lookup"><span data-stu-id="374fe-223">By default, all columns in the table are selected.</span></span> <span data-ttu-id="374fe-224">如果您不想同步所有資料行，請取消選取您不想要同步的資料行核取方塊。請務必保留選取的主索引鍵資料行。</span><span class="sxs-lookup"><span data-stu-id="374fe-224">If you don't want to sync all the columns, disable the checkbox for the columns that you don't want to sync. Be sure to leave the primary key column selected.</span></span>

    ![選取要同步的欄位](media/sql-database-get-started-sql-data-sync/datasync-preview-tables2.png)

4.  <span data-ttu-id="374fe-226">最後，選取 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="374fe-226">Finally, select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="374fe-227">後續步驟</span><span class="sxs-lookup"><span data-stu-id="374fe-227">Next steps</span></span>
<span data-ttu-id="374fe-228">恭喜！</span><span class="sxs-lookup"><span data-stu-id="374fe-228">Congratulations.</span></span> <span data-ttu-id="374fe-229">您已建立一個同時包含 SQL Database 執行個體與 SQL Server 資料庫的同步群組。</span><span class="sxs-lookup"><span data-stu-id="374fe-229">You have created a sync group that includes both a SQL Database instance and a SQL Server database.</span></span>

<span data-ttu-id="374fe-230">如需 SQL Database 和 SQL 資料同步的詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="374fe-230">For more info about SQL Database and SQL Data Sync, see:</span></span>

-   [<span data-ttu-id="374fe-231">下載完整的 SQL 資料同步技術文件</span><span class="sxs-lookup"><span data-stu-id="374fe-231">Download the complete SQL Data Sync technical documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)
-   [<span data-ttu-id="374fe-232">下載 SQL 資料同步 REST API 文件</span><span class="sxs-lookup"><span data-stu-id="374fe-232">Download the SQL Data Sync REST API documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)
-   [<span data-ttu-id="374fe-233">SQL Database 概觀</span><span class="sxs-lookup"><span data-stu-id="374fe-233">SQL Database Overview</span></span>](sql-database-technical-overview.md)
-   [<span data-ttu-id="374fe-234">資料庫生命週期管理</span><span class="sxs-lookup"><span data-stu-id="374fe-234">Database Lifecycle Management</span></span>](https://msdn.microsoft.com/library/jj907294.aspx)
