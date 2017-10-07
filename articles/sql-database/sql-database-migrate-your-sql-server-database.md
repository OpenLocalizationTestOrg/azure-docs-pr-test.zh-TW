---
title: "aaaMigrate SQL 資料庫的 SQL Server DB tooAzure |Microsoft 文件"
description: "了解 toomigrate 您 SQL Server 資料庫 tooAzure SQL 資料庫。"
services: sql-database
documentationcenter: 
author: janeng
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,load & move data
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/27/2017
ms.author: janeng
ms.openlocfilehash: d10ad1d26576194f1dd6858bae5c3e7c1ec4fb91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-sql-server-database-tooazure-sql-database"></a><span data-ttu-id="d4aff-103">移轉您的 SQL Server 資料庫 tooAzure SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="d4aff-103">Migrate your SQL Server database tooAzure SQL Database</span></span>

<span data-ttu-id="d4aff-104">移動您的 SQL Server 資料庫 tooAzure SQL Database 是程序包含三個部分-先準備，然後匯出，然後匯入 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="d4aff-104">Moving your SQL Server database tooAzure SQL Database is a three part process - you first prepare, then export, and then import hello database.</span></span> <span data-ttu-id="d4aff-105">您會在本教學課程中學到：</span><span class="sxs-lookup"><span data-stu-id="d4aff-105">In this tutorial, you learn to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d4aff-106">準備移轉 tooAzure SQL 資料庫的 SQL Server 中的資料庫使用 hello[資料移轉小幫手](https://www.microsoft.com/download/details.aspx?id=53595)(DMA)</span><span class="sxs-lookup"><span data-stu-id="d4aff-106">Prepare a database in a SQL Server for migration tooAzure SQL Database using hello [Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) (DMA)</span></span>
> * <span data-ttu-id="d4aff-107">Hello 資料庫 tooa BACPAC 檔案匯出</span><span class="sxs-lookup"><span data-stu-id="d4aff-107">Export hello database tooa BACPAC file</span></span>
> * <span data-ttu-id="d4aff-108">Hello BACPAC 檔案匯入到 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="d4aff-108">Import hello BACPAC file into an Azure SQL Database</span></span>

<span data-ttu-id="d4aff-109">如果您沒有 Azure 訂用帳戶，請在開始之前先[建立免費帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="d4aff-109">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4aff-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="d4aff-110">Prerequisites</span></span>

<span data-ttu-id="d4aff-111">toocomplete 完成本教學課程，請確定 hello 下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="d4aff-111">toocomplete this tutorial, make sure hello following prerequisites are completed:</span></span>

- <span data-ttu-id="d4aff-112">已安裝的 hello 最新版本的[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS)。</span><span class="sxs-lookup"><span data-stu-id="d4aff-112">Installed hello newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span></span> <span data-ttu-id="d4aff-113">安裝 SSMS 也會安裝 hello SQLPackage，可以是使用的 tooautomate 範圍內的資料庫開發工作的命令列公用程式最新版本。</span><span class="sxs-lookup"><span data-stu-id="d4aff-113">Installing SSMS also installs hello newest version of SQLPackage, a command-line utility that can be used tooautomate a range of database development tasks.</span></span> 
- <span data-ttu-id="d4aff-114">已安裝的 hello[資料移轉小幫手](https://www.microsoft.com/download/details.aspx?id=53595)(DMA)。</span><span class="sxs-lookup"><span data-stu-id="d4aff-114">Installed hello [Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) (DMA).</span></span>
- <span data-ttu-id="d4aff-115">您已識別，且有存取 tooa 資料庫 toomigrate。</span><span class="sxs-lookup"><span data-stu-id="d4aff-115">You have identified and have access tooa database toomigrate.</span></span> <span data-ttu-id="d4aff-116">本教學課程使用 hello [SQL Server 2008 r2 AdventureWorks OLTP 資料庫](https://msftdbprodsamples.codeplex.com/releases/view/59211)的 SQL Server 2008 r2 或更新版本中，執行個體上，但您可以使用您選擇的任何資料庫。</span><span class="sxs-lookup"><span data-stu-id="d4aff-116">This tutorial uses hello [SQL Server 2008R2 AdventureWorks OLTP database](https://msftdbprodsamples.codeplex.com/releases/view/59211) on an instance of SQL Server 2008R2 or newer, but you can use any database of your choice.</span></span> <span data-ttu-id="d4aff-117">toofix 相容性問題，使用[SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)</span><span class="sxs-lookup"><span data-stu-id="d4aff-117">toofix compatibility issues, use [SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)</span></span>

## <a name="prepare-for-migration"></a><span data-ttu-id="d4aff-118">為移轉做準備</span><span class="sxs-lookup"><span data-stu-id="d4aff-118">Prepare for migration</span></span>

<span data-ttu-id="d4aff-119">您已準備好 tooprepare 進行移轉。</span><span class="sxs-lookup"><span data-stu-id="d4aff-119">You are ready tooprepare for migration.</span></span> <span data-ttu-id="d4aff-120">請遵循這些步驟 toouse hello **[資料移轉小幫手](https://www.microsoft.com/download/details.aspx?id=53595)** tooassess hello 整備向您的資料庫移轉 tooAzure SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="d4aff-120">Follow these steps toouse hello **[Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595)** tooassess hello readiness of your database for migration tooAzure SQL Database.</span></span>

1. <span data-ttu-id="d4aff-121">開啟 hello**資料移轉小幫手**。</span><span class="sxs-lookup"><span data-stu-id="d4aff-121">Open hello **Data Migration Assistant**.</span></span> <span data-ttu-id="d4aff-122">您計劃 toomigrate，，您不需要 tooinstall 它 hello 電腦主控上 hello SQL Server 執行個體，您可以執行 DMA 連線 toohello SQL Server 執行個體包含 hello 資料庫的任何電腦上。</span><span class="sxs-lookup"><span data-stu-id="d4aff-122">You can run DMA on any computer with connectivity toohello SQL Server instance containing hello database that you plan toomigrate, you do not need tooinstall it on hello computer hosting hello SQL Server instance.</span></span>

     ![開啟 data migration assistant](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-open.png)

2. <span data-ttu-id="d4aff-124">Hello 左側功能表中，按一下**+ 新增**toocreate**評估**專案。</span><span class="sxs-lookup"><span data-stu-id="d4aff-124">In hello left-hand menu, click **+ New** toocreate an **Assessment** project.</span></span> <span data-ttu-id="d4aff-125">填寫表單 hello**專案名稱**（所有其他值應該留在其預設值），按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="d4aff-125">Fill in hello form with a **Project name** (all other values should be left at their default values) and click **Create**.</span></span> <span data-ttu-id="d4aff-126">hello**選項**頁面隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="d4aff-126">hello **Options** page opens.</span></span>

     ![新 data migration assistant 專案](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-new-project.png)

3. <span data-ttu-id="d4aff-128">在 hello**選項**頁面上，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="d4aff-128">On hello **Options** page, click **Next**.</span></span> <span data-ttu-id="d4aff-129">hello**選取來源**頁面隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="d4aff-129">hello **Select sources** page opens.</span></span>

     ![新資料移轉選項](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-options.png) 

4. <span data-ttu-id="d4aff-131">在 hello**選取來源**頁面上，輸入 hello 包含您計劃 toomigrate hello 伺服器的 SQL Server 執行個體名稱。</span><span class="sxs-lookup"><span data-stu-id="d4aff-131">On hello **Select sources** page, enter hello name of SQL Server instance containing hello server you plan toomigrate.</span></span> <span data-ttu-id="d4aff-132">如有必要，變更 hello 這個頁面上的其他值。</span><span class="sxs-lookup"><span data-stu-id="d4aff-132">Change hello other values on this page if necessary.</span></span> <span data-ttu-id="d4aff-133">按一下 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="d4aff-133">Click **Connect**.</span></span>

     ![新資料移轉選取來源](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-sources.png)

5. <span data-ttu-id="d4aff-135">在 hello**加入來源**hello 部分**選取來源**頁面上，選取測試的相容性的 hello 資料庫 toobe hello 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="d4aff-135">In hello **Add sources** portion of hello **Select sources** page, select hello checkboxes for hello databases toobe tested for compatibility.</span></span> <span data-ttu-id="d4aff-136">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="d4aff-136">Click **Add**.</span></span>

     ![新資料移轉選取來源](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-sources-add.png)

6. <span data-ttu-id="d4aff-138">按一下 [開始評估]。</span><span class="sxs-lookup"><span data-stu-id="d4aff-138">Click **Start Assessment**.</span></span>

     ![新資料移轉開始評估](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-start-assessment.png)

7. <span data-ttu-id="d4aff-140">Hello 評估完成時，先在 hello 資料庫是否完全相容 toomigrate 尋找 toosee。</span><span class="sxs-lookup"><span data-stu-id="d4aff-140">When hello assessment completes, first look toosee if hello database is sufficiently compatible toomigrate.</span></span> <span data-ttu-id="d4aff-141">尋找 hello 核取記號的綠色圓圈。</span><span class="sxs-lookup"><span data-stu-id="d4aff-141">Look for hello checkmark in a green circle.</span></span>

     ![新資料移轉評估結果相容](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-assessment-results-compatible.png)

8. <span data-ttu-id="d4aff-143">檢閱 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="d4aff-143">Review hello results.</span></span> <span data-ttu-id="d4aff-144">hello **SQL Server 功能同位檢查**結果所示為 hello 預設結果 tooreview。</span><span class="sxs-lookup"><span data-stu-id="d4aff-144">hello **SQL Server feature parity** results shown are hello default results tooreview.</span></span> <span data-ttu-id="d4aff-145">特別是檢閱 hello 不支援和部分支援功能的資訊和建議的動作的 hello 提供資訊。</span><span class="sxs-lookup"><span data-stu-id="d4aff-145">Specifically review hello information about unsupported and partially supported features, and hello provided information about recommended actions.</span></span> 

     ![新資料移轉評估同位檢查](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-assessment-results-parity.png)

9. <span data-ttu-id="d4aff-147">檢閱 hello**相容性問題**按一下該選項在 hello 左上方。</span><span class="sxs-lookup"><span data-stu-id="d4aff-147">Review hello **Compatibility issues** by clicking that option in hello upper left.</span></span> <span data-ttu-id="d4aff-148">特別是檢閱 hello 移轉封鎖器，行為變更的相關資訊，並已被取代每個相容性層級的功能。</span><span class="sxs-lookup"><span data-stu-id="d4aff-148">Specifically review hello information about migration blockers, behavior changes, and deprecated features for each compatibility level.</span></span> <span data-ttu-id="d4aff-149">Hello AdventureWorks2008R2 資料庫中，檢閱 hello 變更 tooFull 文字搜尋，因為 SQL Server 2008 和 hello 變更 tooSERVERPROPERTY('LCID') 自 SQL Server 2000。</span><span class="sxs-lookup"><span data-stu-id="d4aff-149">For hello AdventureWorks2008R2 database, review hello changes tooFull-Text Search since SQL Server 2008 and hello changes tooSERVERPROPERTY('LCID') since SQL Server 2000.</span></span> <span data-ttu-id="d4aff-150">如需這些變更的詳細資訊，請參閱提供的詳細資訊連結。</span><span class="sxs-lookup"><span data-stu-id="d4aff-150">For details on these changes, links for more information is provided.</span></span> <span data-ttu-id="d4aff-151">全文檢索搜尋的許多選項和設定皆已變更</span><span class="sxs-lookup"><span data-stu-id="d4aff-151">Many search options and settings for Full-Text Search have changed</span></span> 

   > [!IMPORTANT] 
   > <span data-ttu-id="d4aff-152">移轉您的資料庫 tooAzure SQL 資料庫之後，您可以選擇 toooperate hello 資料庫在其目前的相容性層級 （層級 100 hello AdventureWorks2008R2 資料庫） 或更高的層級。</span><span class="sxs-lookup"><span data-stu-id="d4aff-152">After you migrate your database tooAzure SQL Database, you can choose toooperate hello database at its current compatibility level (level 100 for hello AdventureWorks2008R2 database) or at a higher level.</span></span> <span data-ttu-id="d4aff-153">如需有關 hello 含意與作業系統特定的相容性層級的資料庫選項的詳細資訊，請參閱[ALTER DATABASE 相容性層級](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)。</span><span class="sxs-lookup"><span data-stu-id="d4aff-153">For more information on hello implications and options for operating a database at a specific compatibility level, see [ALTER DATABASE Compatibility Level](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span></span> <span data-ttu-id="d4aff-154">另請參閱[ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql)對於其他資料庫層級設定的相關資訊與相關 toocompatibility 層級。</span><span class="sxs-lookup"><span data-stu-id="d4aff-154">See also [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) for information about additional database-level settings related toocompatibility levels.</span></span>
   >

10. <span data-ttu-id="d4aff-155">（選擇性） 按一下**將報表匯出**toosave hello 報表成為 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="d4aff-155">Optionally, click **Export report** toosave hello report as a JSON file.</span></span>
11. <span data-ttu-id="d4aff-156">關閉 hello 資料移轉小幫手。</span><span class="sxs-lookup"><span data-stu-id="d4aff-156">Close hello Data Migration Assistant.</span></span>

## <a name="export-toobacpac-file"></a><span data-ttu-id="d4aff-157">匯出 tooBACPAC 檔案</span><span class="sxs-lookup"><span data-stu-id="d4aff-157">Export tooBACPAC file</span></span> 

<span data-ttu-id="d4aff-158">BACPAC 檔案是包含 hello 中繼資料和資料從 SQL Server 資料庫的 BACPAC 的延伸模組 ZIP 檔案。</span><span class="sxs-lookup"><span data-stu-id="d4aff-158">A BACPAC file is a ZIP file with an extension of BACPAC containing hello metadata and data from a SQL Server database.</span></span> <span data-ttu-id="d4aff-159">BACPAC 檔案可以儲存在 Azure blob 儲存體，或為了封存或移轉為本機的儲存體中例如從 SQL Server tooAzure SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="d4aff-159">A BACPAC file can be stored in Azure blob storage or in local storage for archiving or for migration - such as from SQL Server tooAzure SQL Database.</span></span> <span data-ttu-id="d4aff-160">對於匯出 toobe 交易一致性，您必須確定任一個的任何寫入 hello 匯出期間正在進行活動。</span><span class="sxs-lookup"><span data-stu-id="d4aff-160">For an export toobe transactionally consistent, you must ensure either that no write activity is occurring during hello export.</span></span>

<span data-ttu-id="d4aff-161">請遵循這些步驟 toouse hello SQLPackage 命令列公用程式 tooexport hello AdventureWorks2008R2 資料庫 toolocal 儲存體。</span><span class="sxs-lookup"><span data-stu-id="d4aff-161">Follow these steps toouse hello SQLPackage command-line utility tooexport hello AdventureWorks2008R2 database toolocal storage.</span></span>

1. <span data-ttu-id="d4aff-162">開啟 Windows 命令提示字元並變更您擁有 hello 您目錄 tooa 資料夾**130**版本 SQLPackage-例如**C:\Program Files (x86) \Microsoft SQL Server\130\DAC\bin**。</span><span class="sxs-lookup"><span data-stu-id="d4aff-162">Open a Windows command prompt and change your directory tooa folder in which you have hello **130** version of SQLPackage - such as **C:\Program Files (x86)\Microsoft SQL Server\130\DAC\bin**.</span></span>

2. <span data-ttu-id="d4aff-163">執行下列 SQLPackage 命令在 hello 命令提示字元 tooexport hello hello **AdventureWorks2008R2**資料庫從**localhost**太**AdventureWorks2008R2.bacpac**.</span><span class="sxs-lookup"><span data-stu-id="d4aff-163">Execute hello following SQLPackage command at hello command prompt tooexport hello **AdventureWorks2008R2** database from **localhost** too**AdventureWorks2008R2.bacpac**.</span></span> <span data-ttu-id="d4aff-164">變更這些值做為適當的 tooyour 環境。</span><span class="sxs-lookup"><span data-stu-id="d4aff-164">Change any of these values as appropriate tooyour environment.</span></span>

    ```SQLPackage
    sqlpackage.exe /Action:Export /ssn:localhost /sdn:AdventureWorks2008R2 /tf:AdventureWorks2008R2.bacpac
    ```

    ![sqlpackage 匯出](./media/sql-database-migrate-your-sql-server-database/sqlpackage-export.png)

<span data-ttu-id="d4aff-166">Hello 執行完成之後產生的 hello BACPAC 檔案會儲存在 hello hello sqlpackage 可執行檔所在的目錄。</span><span class="sxs-lookup"><span data-stu-id="d4aff-166">Once hello execution is complete hello generated BACPAC file is stored in hello directory where hello sqlpackage executable is located.</span></span> <span data-ttu-id="d4aff-167">在本範例中為 C:\Program Files (x86)\Microsoft SQL Server\130\DAC\bin。</span><span class="sxs-lookup"><span data-stu-id="d4aff-167">In this example C:\Program Files (x86)\Microsoft SQL Server\130\DAC\bin.</span></span> 

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="d4aff-168">登入 toohello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="d4aff-168">Log in toohello Azure portal</span></span>

<span data-ttu-id="d4aff-169">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="d4aff-169">Log in toohello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="d4aff-170">從執行 hello SQLPackage 命令列公用程式的 hello 電腦登入在步驟 5 中減輕 hello 建立 hello 防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="d4aff-170">Logging on from hello computer from which you are running hello SQLPackage command-line utility eases hello creation of hello firewall rule in step 5.</span></span>

## <a name="create-a-sql-server-logical-server"></a><span data-ttu-id="d4aff-171">建立 SQL Server 邏輯伺服器</span><span class="sxs-lookup"><span data-stu-id="d4aff-171">Create a SQL server logical server</span></span>

<span data-ttu-id="d4aff-172">[SQL Server 邏輯伺服器](sql-database-features.md)會作為多個資料庫的中央管理點。</span><span class="sxs-lookup"><span data-stu-id="d4aff-172">A [SQL server logical server](sql-database-features.md) acts as a central administrative point for multiple databases.</span></span> <span data-ttu-id="d4aff-173">請遵循下列步驟 toocreate SQL server 的邏輯伺服器 toocontain hello 移轉 Adventure Works OLTP 的 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="d4aff-173">Follow these steps toocreate a SQL server logical server toocontain hello migrated Adventure Works OLTP SQL Server database.</span></span> 

1. <span data-ttu-id="d4aff-174">按一下 hello**新增**hello 的左上角 hello Azure 入口網站上找到的按鈕。</span><span class="sxs-lookup"><span data-stu-id="d4aff-174">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="d4aff-175">型別**sql server**在 hello 搜尋視窗上 hello**新增**頁面，然後選取**SQL database （邏輯伺服器）** hello 從篩選清單。</span><span class="sxs-lookup"><span data-stu-id="d4aff-175">Type **sql server** in hello search window on hello **New** page, and select **SQL database (logical server)** from hello filtered list.</span></span>

    ![選取邏輯伺服器](./media/sql-database-migrate-your-sql-server-database/logical-server.png)

3. <span data-ttu-id="d4aff-177">在 hello**的所有項目**頁面上，按一下**SQL server （邏輯伺服器）** ，然後按一下**建立**上 hello **SQL Server （邏輯伺服器）**頁面.</span><span class="sxs-lookup"><span data-stu-id="d4aff-177">On hello **Everything** page, click **SQL server (logical server)** and then click **Create** on hello **SQL Server (logical server)** page.</span></span>

    ![建立邏輯伺服器](./media/sql-database-migrate-your-sql-server-database/logical-server-create.png)

4. <span data-ttu-id="d4aff-179">填寫表單 hello SQL 伺服器 （邏輯伺服器） 以 hello 下列資訊，hello 前面影像所示：</span><span class="sxs-lookup"><span data-stu-id="d4aff-179">Fill out hello SQL server (logical server) form with hello following information, as shown on hello preceding image:</span></span>     

   | <span data-ttu-id="d4aff-180">設定</span><span class="sxs-lookup"><span data-stu-id="d4aff-180">Setting</span></span>       | <span data-ttu-id="d4aff-181">建議的值</span><span class="sxs-lookup"><span data-stu-id="d4aff-181">Suggested value</span></span> | <span data-ttu-id="d4aff-182">說明</span><span class="sxs-lookup"><span data-stu-id="d4aff-182">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="d4aff-183">**伺服器名稱**</span><span class="sxs-lookup"><span data-stu-id="d4aff-183">**Server name**</span></span> | <span data-ttu-id="d4aff-184">輸入任何全域唯一名稱</span><span class="sxs-lookup"><span data-stu-id="d4aff-184">Enter any globally unique name</span></span> | <span data-ttu-id="d4aff-185">如需有效的伺服器名稱，請參閱[命名規則和限制](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions)。</span><span class="sxs-lookup"><span data-stu-id="d4aff-185">For valid server names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> | 
   | <span data-ttu-id="d4aff-186">**伺服器管理員登入**</span><span class="sxs-lookup"><span data-stu-id="d4aff-186">**Server admin login**</span></span> | <span data-ttu-id="d4aff-187">輸入任何有效名稱</span><span class="sxs-lookup"><span data-stu-id="d4aff-187">Enter any valid name</span></span> | <span data-ttu-id="d4aff-188">如需有效的登入名稱，請參閱[資料庫識別碼](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers)。</span><span class="sxs-lookup"><span data-stu-id="d4aff-188">For valid login names, see [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers).</span></span> |
   | <span data-ttu-id="d4aff-189">**密碼**</span><span class="sxs-lookup"><span data-stu-id="d4aff-189">**Password**</span></span> | <span data-ttu-id="d4aff-190">輸入任何有效密碼</span><span class="sxs-lookup"><span data-stu-id="d4aff-190">Enter any valid password</span></span> | <span data-ttu-id="d4aff-191">您的密碼必須至少為 8 個字元，且必須包含下列類別目錄的 hello 的其中三種字元： 大寫字母、 小寫字元、 數字和非英數字元。</span><span class="sxs-lookup"><span data-stu-id="d4aff-191">Your password must have at least 8 characters and must contain characters from three of hello following categories: upper case characters, lower case characters, numbers, and non-alphanumeric characters.</span></span> |
   | <span data-ttu-id="d4aff-192">**訂用帳戶**</span><span class="sxs-lookup"><span data-stu-id="d4aff-192">**Subscription**</span></span> | <span data-ttu-id="d4aff-193">選取一個訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d4aff-193">Select a subscription</span></span> | <span data-ttu-id="d4aff-194">如需訂用帳戶的詳細資訊，請參閱[訂用帳戶](https://account.windowsazure.com/Subscriptions)。</span><span class="sxs-lookup"><span data-stu-id="d4aff-194">For details about your subscriptions, see [Subscriptions](https://account.windowsazure.com/Subscriptions).</span></span> |
   | <span data-ttu-id="d4aff-195">**資源群組**</span><span class="sxs-lookup"><span data-stu-id="d4aff-195">**Resource group**</span></span> | <span data-ttu-id="d4aff-196">選擇現有資源群組，或建立新群組，例如 **myResourceGroup**。</span><span class="sxs-lookup"><span data-stu-id="d4aff-196">Choose an existing resource group or create a new group, such as **myResourceGroup**</span></span> |  <span data-ttu-id="d4aff-197">如需有效的資源群組名稱，請參閱[命名規則和限制](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions)。</span><span class="sxs-lookup"><span data-stu-id="d4aff-197">For valid resource group names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> |
   | <span data-ttu-id="d4aff-198">**位置**</span><span class="sxs-lookup"><span data-stu-id="d4aff-198">**Location**</span></span> | <span data-ttu-id="d4aff-199">輸入 hello 新伺服器的任何有效的位置</span><span class="sxs-lookup"><span data-stu-id="d4aff-199">Enter any valid location for hello new server</span></span> | <span data-ttu-id="d4aff-200">如需區域的相關資訊，請參閱 [Azure 區域](https://azure.microsoft.com/regions/)。</span><span class="sxs-lookup"><span data-stu-id="d4aff-200">For information about regions, see [Azure Regions](https://azure.microsoft.com/regions/).</span></span> |

   ![建立邏輯伺服器完成表單](./media/sql-database-migrate-your-sql-server-database/logical-server-create-completed.png)

5. <span data-ttu-id="d4aff-202">按一下**建立**tooprovision hello 邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="d4aff-202">Click **Create** tooprovision hello logical server.</span></span> <span data-ttu-id="d4aff-203">佈建需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="d4aff-203">Provisioning takes a few minutes.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="d4aff-204">請記住您的伺服器名稱、伺服器系統管理員登入名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="d4aff-204">Remember your server name, server admin login name, and password.</span></span> <span data-ttu-id="d4aff-205">在本教學課程後續的內容中，您會需要這些值。</span><span class="sxs-lookup"><span data-stu-id="d4aff-205">You need these values later in this tutorial.</span></span>
>

## <a name="create-a-server-level-firewall-rule"></a><span data-ttu-id="d4aff-206">建立伺服器層級防火牆規則</span><span class="sxs-lookup"><span data-stu-id="d4aff-206">Create a server-level firewall rule</span></span>

<span data-ttu-id="d4aff-207">建立 SQL Database 服務 hello [hello 伺服器層級防火牆](sql-database-firewall-configure.md)可避免外部應用程式和工具連接 toohello 伺服器或 hello 伺服器上的任何資料庫，除非 tooopen hello 就會建立防火牆規則針對特定的 IP 位址的防火牆。</span><span class="sxs-lookup"><span data-stu-id="d4aff-207">hello SQL Database service creates a [firewall at hello server-level](sql-database-firewall-configure.md) that prevents external applications and tools from connecting toohello server or any databases on hello server unless a firewall rule is created tooopen hello firewall for specific IP addresses.</span></span> <span data-ttu-id="d4aff-208">請遵循這些步驟 toocreate hello 電腦 IP 位址的 hello 執行 hello SQLPackage 命令列公用程式的 SQL Database 伺服器層級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="d4aff-208">Follow these steps toocreate a SQL Database server-level firewall rule for hello IP address of hello computer from which you are running hello SQLPackage command-line utility.</span></span> <span data-ttu-id="d4aff-209">這可讓 SQLPackage tooconnect toohello SQL 伺服器資料庫的邏輯伺服器透過 hello Azure SQL Database 防火牆。</span><span class="sxs-lookup"><span data-stu-id="d4aff-209">This enables SQLPackage tooconnect toohello SQL serverDatabase logical server through hello Azure SQL Database firewall.</span></span> 

1. <span data-ttu-id="d4aff-210">按一下**所有資源**hello 左側功能表中，按一下 新伺服器上 hello**所有資源**頁面。</span><span class="sxs-lookup"><span data-stu-id="d4aff-210">Click **All resources** from hello left-hand menu and click your new server on hello **All resources** page.</span></span> <span data-ttu-id="d4aff-211">為您的伺服器 hello [概觀] 頁面會開啟，並提供進一步組態的選項。</span><span class="sxs-lookup"><span data-stu-id="d4aff-211">hello overview page for your server opens and provides options for further configuration.</span></span>

     ![邏輯伺服器概觀](./media/sql-database-migrate-your-sql-server-database/logical-server-overview.png)

2. <span data-ttu-id="d4aff-213">按一下**防火牆**在底下的 hello 左側功能表中**設定**hello 概觀 頁面上。</span><span class="sxs-lookup"><span data-stu-id="d4aff-213">Click **Firewall** in hello left-hand menu under **Settings** on hello overview page.</span></span> <span data-ttu-id="d4aff-214">hello**防火牆設定**hello SQL 資料庫伺服器 頁面隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="d4aff-214">hello **Firewall settings** page for hello SQL Database server opens.</span></span> 

3. <span data-ttu-id="d4aff-215">按一下**新增用戶端 IP** hello 工具列 tooadd hello 電腦的 IP 位址 hello 上您目前正在使用，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="d4aff-215">Click **Add client IP** on hello toolbar tooadd hello IP address of hello computer you are currently using and then click **Save**.</span></span> <span data-ttu-id="d4aff-216">系統會為此 IP 位址建立伺服器層級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="d4aff-216">A server-level firewall rule is created for this IP address.</span></span>

     ![設定伺服器防火牆規則](./media/sql-database-migrate-your-sql-server-database/server-firewall-rule-set.png)

4. <span data-ttu-id="d4aff-218">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="d4aff-218">Click **OK**.</span></span>

<span data-ttu-id="d4aff-219">您現在可以連接此伺服器上使用 SQL Server Management Studio 或您選擇從這個 IP 位址，使用先前建立的 hello 伺服器系統管理員帳戶的另一個工具 tooall 資料庫。</span><span class="sxs-lookup"><span data-stu-id="d4aff-219">You can now connect tooall databases on this server using SQL Server Management Studio or another tool of your choice from this IP address using hello server admin account created previously.</span></span>

> [!NOTE]
> <span data-ttu-id="d4aff-220">SQL Database 會透過連接埠 1433 通訊。</span><span class="sxs-lookup"><span data-stu-id="d4aff-220">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="d4aff-221">如果您嘗試 tooconnect 從公司網路內，由您的網路防火牆可能不允許透過通訊埠 1433年的輸出流量。</span><span class="sxs-lookup"><span data-stu-id="d4aff-221">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="d4aff-222">如果是這樣，您無法連接 tooyour Azure SQL Database 伺服器，除非您的 IT 部門會開啟通訊埠 1433年。</span><span class="sxs-lookup"><span data-stu-id="d4aff-222">If so, you cannot connect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="import-a-bacpac-file-tooazure-sql-database"></a><span data-ttu-id="d4aff-223">匯入 BACPAC 檔案 tooAzure SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="d4aff-223">Import a BACPAC file tooAzure SQL Database</span></span> 

<span data-ttu-id="d4aff-224">hello hello SQLPackage 命令列公用程式最新版本提供支援建立在指定的 Azure SQL database[服務層和效能層級](sql-database-service-tiers.md)。</span><span class="sxs-lookup"><span data-stu-id="d4aff-224">hello newest versions of hello SQLPackage command-line utility provide support for creating an Azure SQL database at a specified [service tier and performance level](sql-database-service-tiers.md).</span></span> <span data-ttu-id="d4aff-225">為了達到最佳效能，在匯入期間，選取最高的服務層和效能層級，然後向下延展匯入後如果 hello 服務層和效能層級高於您需要立即。</span><span class="sxs-lookup"><span data-stu-id="d4aff-225">For best performance during import, select a high service tier and performance level and then scale down after import if hello service tier and performance level is higher than you need immediately.</span></span>

<span data-ttu-id="d4aff-226">請遵循這些步驟使用 hello SQLPackage 命令列公用程式 tooimport hello AdventureWorks2008R2 資料庫 tooAzure SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="d4aff-226">Follow these steps use hello SQLPackage command-line utility tooimport hello AdventureWorks2008R2 database tooAzure SQL Database.</span></span> <span data-ttu-id="d4aff-227">雖然您可以使用 SQL Server Management Studio，這項工作，SQLPackage 是最大的彈性和達到最佳效能的大部分實際執行環境的 hello 慣用方法。</span><span class="sxs-lookup"><span data-stu-id="d4aff-227">While you can use SQL Server Management Studio for this task, SQLPackage is hello preferred method for most production environments for maximum flexibility and best performance.</span></span> <span data-ttu-id="d4aff-228">請參閱[從 SQL Server tooAzure 使用 BACPAC 檔案的 SQL Database 移轉](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/)。</span><span class="sxs-lookup"><span data-stu-id="d4aff-228">See [Migrating from SQL Server tooAzure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>

- <span data-ttu-id="d4aff-229">執行下列 SQLPackage 命令在 hello 命令提示字元 tooimport hello hello **AdventureWorks2008R2**資料庫從本機儲存體 toohello SQL server 邏輯伺服器，您先前建立的 tooa 新資料庫，服務層**Premium**，以及服務目標的**P6**。</span><span class="sxs-lookup"><span data-stu-id="d4aff-229">Execute hello following SQLPackage command at hello command prompt tooimport hello **AdventureWorks2008R2** database from local storage toohello SQL server logical server that you previously created tooa new database, a service tier of **Premium**, and a Service Objective of **P6**.</span></span> <span data-ttu-id="d4aff-230">角括弧括住的 hello 值取代為適當的值，SQL server 的邏輯伺服器，並指定 hello 新資料庫 （也取代 hello 角括號） 的名稱。</span><span class="sxs-lookup"><span data-stu-id="d4aff-230">Replace hello values in angle brackets with appropriate values for your SQL server logical server and specify a name for hello new database (also replace hello angle brackets).</span></span> <span data-ttu-id="d4aff-231">您也可以選擇資料庫版本和服務 objectgive toochange hello 值做為適當的 tooyour 環境。</span><span class="sxs-lookup"><span data-stu-id="d4aff-231">You can also choose toochange hello values for database edition and service objectgive as appropriate tooyour environment.</span></span> <span data-ttu-id="d4aff-232">基於本教學課程的 hello 目的，稱為 hello 移轉的資料庫**myMigratedDatabase**。</span><span class="sxs-lookup"><span data-stu-id="d4aff-232">For hello purpose of this tutorial, hello migrated database is called **myMigratedDatabase**.</span></span>

    ```
    SqlPackage.exe /a:import /tcs:"Data Source=<your_server_name>.database.windows.net;Initial Catalog=<your_new_database_name>;User Id=<change_to_your_admin_user_account>;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
    ```

   ![sqlpackage 匯入](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> <span data-ttu-id="d4aff-234">SQL Server 邏輯伺服器會接聽連接埠 1433。</span><span class="sxs-lookup"><span data-stu-id="d4aff-234">A SQL server logical server listens on port 1433.</span></span> <span data-ttu-id="d4aff-235">如果您正嘗試 tooconnect tooa SQL server 內的邏輯伺服器從公司防火牆，此連接埠必須在 hello 公司防火牆中開啟您 toosuccessfully 連線。</span><span class="sxs-lookup"><span data-stu-id="d4aff-235">If you are attempting tooconnect tooa SQL server logical server from within a corporate firewall, this port must be open in hello corporate firewall for you toosuccessfully connect.</span></span>
>

## <a name="connect-using-sql-server-management-studio-ssms"></a><span data-ttu-id="d4aff-236">使用 SQL Server Management Studio (SSMS) 連線</span><span class="sxs-lookup"><span data-stu-id="d4aff-236">Connect using SQL Server Management Studio (SSMS)</span></span>

<span data-ttu-id="d4aff-237">使用 SQL Server Management Studio tooestablish 連接 tooyour Azure SQL Database 伺服器和剛移轉的資料庫，呼叫**myMigratedDatabase**在本教學課程。</span><span class="sxs-lookup"><span data-stu-id="d4aff-237">Use SQL Server Management Studio tooestablish a connection tooyour Azure SQL Database server and newly migrated database, called **myMigratedDatabase** in this tutorial.</span></span> <span data-ttu-id="d4aff-238">如果您執行 SQLPackage 一部電腦上執行 SQL Server Management Studio，建立使用 hello 前程序中的 hello 步驟這台電腦的防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="d4aff-238">If you are running SQL Server Management Studio on a different computer from which you ran SQLPackage, create a firewall rule for this computer using hello steps in hello previous procedure.</span></span>

1. <span data-ttu-id="d4aff-239">開啟 SQL Server Management Studio。</span><span class="sxs-lookup"><span data-stu-id="d4aff-239">Open SQL Server Management Studio.</span></span>

2. <span data-ttu-id="d4aff-240">在 hello**連接 tooServer**對話方塊方塊中，輸入下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="d4aff-240">In hello **Connect tooServer** dialog box, enter hello following information:</span></span>
   - <span data-ttu-id="d4aff-241">**伺服器類型**：指定資料庫引擎</span><span class="sxs-lookup"><span data-stu-id="d4aff-241">**Server type**: Specify Database engine</span></span>
   - <span data-ttu-id="d4aff-242">**伺服器名稱**︰輸入您的完整伺服器名稱，例如 **mynewserver20170403.database.windows.net**</span><span class="sxs-lookup"><span data-stu-id="d4aff-242">**Server name**: Enter your fully qualified server name, such as **mynewserver20170403.database.windows.net**</span></span>
   - <span data-ttu-id="d4aff-243">**驗證**：指定 SQL Server 驗證</span><span class="sxs-lookup"><span data-stu-id="d4aff-243">**Authentication**: Specify SQL Server Authentication</span></span>
   - <span data-ttu-id="d4aff-244">**登入**︰輸入您的伺服器管理帳戶</span><span class="sxs-lookup"><span data-stu-id="d4aff-244">**Login**: Enter your server admin account</span></span>
   - <span data-ttu-id="d4aff-245">**密碼**: hello 密碼輸入伺服器系統管理員帳戶</span><span class="sxs-lookup"><span data-stu-id="d4aff-245">**Password**: Enter hello password for your server admin account</span></span>
 
    ![以 ssms 連線](./media/sql-database-migrate-your-sql-server-database/connect-ssms.png)

3. <span data-ttu-id="d4aff-247">按一下 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="d4aff-247">Click **Connect**.</span></span> <span data-ttu-id="d4aff-248">hello 物件總管 視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="d4aff-248">hello Object Explorer window opens.</span></span> 

4. <span data-ttu-id="d4aff-249">在 物件總管 中，展開**資料庫**，然後展開  **myMigratedDatabase** tooview hello 範例資料庫中的 hello 物件。</span><span class="sxs-lookup"><span data-stu-id="d4aff-249">In Object Explorer, expand **Databases** and then expand **myMigratedDatabase** tooview hello objects in hello sample database.</span></span>

## <a name="change-database-properties"></a><span data-ttu-id="d4aff-250">變更資料庫屬性</span><span class="sxs-lookup"><span data-stu-id="d4aff-250">Change database properties</span></span>

<span data-ttu-id="d4aff-251">您可以變更 hello 服務層、 效能層級，以及使用 SQL Server Management Studio 的相容性層級。</span><span class="sxs-lookup"><span data-stu-id="d4aff-251">You can change hello service tier, performance level, and compatibility level using SQL Server Management Studio.</span></span> <span data-ttu-id="d4aff-252">在 hello 匯入階段中，我們建議您匯入 tooa 較高的效能層資料庫獲得最佳效能，但是，您向下調整 hello 匯入完成 toosave 金額，直到您準備好 tooactively 使用 hello 匯入的資料庫之後。</span><span class="sxs-lookup"><span data-stu-id="d4aff-252">During hello import phase, we recommend that you import tooa higher performance tier database for best performance, but that you scale down after hello import completes toosave money until you are ready tooactively use hello imported database.</span></span> <span data-ttu-id="d4aff-253">變更 hello 相容性層級可能會產生較佳的效能和存取 toohello 最新功能的 hello Azure SQL Database 服務。</span><span class="sxs-lookup"><span data-stu-id="d4aff-253">Changing hello compatibility level may yield better performance and access toohello newest capabilities of hello Azure SQL Database service.</span></span> <span data-ttu-id="d4aff-254">當您移轉較舊的資料庫時，就會在與 hello 資料庫匯入相容的 hello 最低的支援層級維護其資料庫相容性層級。</span><span class="sxs-lookup"><span data-stu-id="d4aff-254">When you migrate an older database, its database compatibility level is maintained at hello lowest supported level that is compatible with hello database being imported.</span></span> <span data-ttu-id="d4aff-255">如需詳細資訊，請參閱[改善 Azure SQL Database 中相容性層級 130 的查詢效能](sql-database-compatibility-level-query-performance-130.md).</span><span class="sxs-lookup"><span data-stu-id="d4aff-255">For more information, see [Improved query performance with compatibility Level 130 in Azure SQL Database](sql-database-compatibility-level-query-performance-130.md).</span></span>

1. <span data-ttu-id="d4aff-256">在 物件總管 中，於 myMigratedDatabase 上按一下滑鼠右鍵，然後按一下新增查詢。</span><span class="sxs-lookup"><span data-stu-id="d4aff-256">In Object Explorer, right-click **myMigratedDatabase** and click **New Query**.</span></span> <span data-ttu-id="d4aff-257">查詢視窗中開啟連接的 tooyour 資料庫。</span><span class="sxs-lookup"><span data-stu-id="d4aff-257">A query window opens connected tooyour database.</span></span>

2. <span data-ttu-id="d4aff-258">執行太遵循命令 tooset hello 服務層的 hello**標準**太 hello 效能層級和**S1**。</span><span class="sxs-lookup"><span data-stu-id="d4aff-258">Execute hello following command tooset hello service tier too**Standard** and hello performance level too**S1**.</span></span>

    ```
    ALTER DATABASE myMigratedDatabase 
    MODIFY 
        (
        EDITION = 'Standard'
        , MAXSIZE = 250 GB
        , SERVICE_OBJECTIVE = 'S1'
    );
    ```

    ![變更服務層](./media/sql-database-migrate-your-sql-server-database/service-tier.png)

3. <span data-ttu-id="d4aff-260">執行下列命令 toochange hello 資料庫相容性層級太 hello**130**。</span><span class="sxs-lookup"><span data-stu-id="d4aff-260">Execute hello following command toochange hello database compatibility level too**130**.</span></span>

    ```
    ALTER DATABASE myMigratedDatabase  
    SET COMPATIBILITY_LEVEL = 130;
    ```

   ![變更相容性層級](./media/sql-database-migrate-your-sql-server-database/compat-level.png)

## <a name="next-steps"></a><span data-ttu-id="d4aff-262">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d4aff-262">Next steps</span></span> 
<span data-ttu-id="d4aff-263">在本教學課程中，您已準備、匯出和匯入資料庫。</span><span class="sxs-lookup"><span data-stu-id="d4aff-263">In this tutorial you prepared, exported and imported your database.</span></span> <span data-ttu-id="d4aff-264">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="d4aff-264">You learned to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d4aff-265">準備移轉 tooAzure SQL 資料庫的 SQL Server 中的資料庫</span><span class="sxs-lookup"><span data-stu-id="d4aff-265">Prepare a database in a SQL Server for migration tooAzure SQL Database</span></span>
> * <span data-ttu-id="d4aff-266">Hello 資料庫 tooa BACPAC 檔案匯出</span><span class="sxs-lookup"><span data-stu-id="d4aff-266">Export hello database tooa BACPAC file</span></span>
> * <span data-ttu-id="d4aff-267">Hello BACPAC 檔案匯入到 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="d4aff-267">Import hello BACPAC file into an Azure SQL Database</span></span>

<span data-ttu-id="d4aff-268">如何前進 toohello 下一個教學課程 toolearn toosecure 您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="d4aff-268">Advance toohello next tutorial toolearn how toosecure your database.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="d4aff-269">[保護 Azure SQL Database](sql-database-security-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="d4aff-269">[Secure your Azure SQL Database](sql-database-security-tutorial.md).</span></span>


