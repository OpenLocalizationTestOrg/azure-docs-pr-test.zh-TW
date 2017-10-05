---
title: "將 SQL Server DB 移轉至 Azure SQL Database | Microsoft Docs"
description: "學習如何將 SQL Server Database 移轉至 Azure SQL Database。"
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
ms.openlocfilehash: 375d3ea0230e7d3fd0fc02ca7e0b8a7a76c24a27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-your-sql-server-database-to-azure-sql-database"></a><span data-ttu-id="0871d-103">將 SQL Server Database 移轉至 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="0871d-103">Migrate your SQL Server database to Azure SQL Database</span></span>

<span data-ttu-id="0871d-104">將 SQL Server 資料庫移動到 Azure SQL Database 的程序需要三個步驟：先準備資料庫，接著匯出資料庫，然後匯入資料庫。</span><span class="sxs-lookup"><span data-stu-id="0871d-104">Moving your SQL Server database to Azure SQL Database is a three part process - you first prepare, then export, and then import the database.</span></span> <span data-ttu-id="0871d-105">您會在本教學課程中學到：</span><span class="sxs-lookup"><span data-stu-id="0871d-105">In this tutorial, you learn to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0871d-106">使用 [Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) (DMA) 來準備 SQL Server 中的資料庫，以便將資料庫移轉至 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="0871d-106">Prepare a database in a SQL Server for migration to Azure SQL Database using the [Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) (DMA)</span></span>
> * <span data-ttu-id="0871d-107">將資料庫匯出至 BACPAC 檔案</span><span class="sxs-lookup"><span data-stu-id="0871d-107">Export the database to a BACPAC file</span></span>
> * <span data-ttu-id="0871d-108">將 BACPAC 檔案匯入 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="0871d-108">Import the BACPAC file into an Azure SQL Database</span></span>

<span data-ttu-id="0871d-109">如果您沒有 Azure 訂用帳戶，請在開始之前先[建立免費帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="0871d-109">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0871d-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="0871d-110">Prerequisites</span></span>

<span data-ttu-id="0871d-111">若要完成本教學課程，請確定已完成下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="0871d-111">To complete this tutorial, make sure the following prerequisites are completed:</span></span>

- <span data-ttu-id="0871d-112">已安裝最新版的 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS)。</span><span class="sxs-lookup"><span data-stu-id="0871d-112">Installed the newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span></span> <span data-ttu-id="0871d-113">安裝 SSMS 時亦會安裝最新版的 SQLPackage，此命令列公用程式可用於自動化處理資料庫開發工作的範圍。</span><span class="sxs-lookup"><span data-stu-id="0871d-113">Installing SSMS also installs the newest version of SQLPackage, a command-line utility that can be used to automate a range of database development tasks.</span></span> 
- <span data-ttu-id="0871d-114">已安裝 [Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) (DMA)。</span><span class="sxs-lookup"><span data-stu-id="0871d-114">Installed the [Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) (DMA).</span></span>
- <span data-ttu-id="0871d-115">您已識別並可存取要移轉的資料庫。</span><span class="sxs-lookup"><span data-stu-id="0871d-115">You have identified and have access to a database to migrate.</span></span> <span data-ttu-id="0871d-116">本教學課程使用 SQL Server 2008R2 或更新版本執行個體上的 [SQL Server 2008R2 AdventureWorks OLTP 資料庫](https://msftdbprodsamples.codeplex.com/releases/view/59211)，不過您亦可使用任何選擇的資料庫。</span><span class="sxs-lookup"><span data-stu-id="0871d-116">This tutorial uses the [SQL Server 2008R2 AdventureWorks OLTP database](https://msftdbprodsamples.codeplex.com/releases/view/59211) on an instance of SQL Server 2008R2 or newer, but you can use any database of your choice.</span></span> <span data-ttu-id="0871d-117">若要修正相容性問題，請使用 [SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)。</span><span class="sxs-lookup"><span data-stu-id="0871d-117">To fix compatibility issues, use [SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)</span></span>

## <a name="prepare-for-migration"></a><span data-ttu-id="0871d-118">為移轉做準備</span><span class="sxs-lookup"><span data-stu-id="0871d-118">Prepare for migration</span></span>

<span data-ttu-id="0871d-119">您已準備好執行移轉。</span><span class="sxs-lookup"><span data-stu-id="0871d-119">You are ready to prepare for migration.</span></span> <span data-ttu-id="0871d-120">遵循以下步驟，使用 **[Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595)** 評估資料庫對於移轉至 Azure SQL Database 的整備程度。</span><span class="sxs-lookup"><span data-stu-id="0871d-120">Follow these steps to use the **[Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595)** to assess the readiness of your database for migration to Azure SQL Database.</span></span>

1. <span data-ttu-id="0871d-121">開啟 **Data Migration Assistant**。</span><span class="sxs-lookup"><span data-stu-id="0871d-121">Open the **Data Migration Assistant**.</span></span> <span data-ttu-id="0871d-122">您可在連線至內含規劃移轉資料庫之 SQL Server 執行個體的任何電腦上執行 DMA，而無須在裝載 SQL Server 執行個體的電腦上將其安裝。</span><span class="sxs-lookup"><span data-stu-id="0871d-122">You can run DMA on any computer with connectivity to the SQL Server instance containing the database that you plan to migrate, you do not need to install it on the computer hosting the SQL Server instance.</span></span>

     ![開啟 data migration assistant](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-open.png)

2. <span data-ttu-id="0871d-124">在左側功能表中，按一下 [新增]以建立 [評估] 專案。</span><span class="sxs-lookup"><span data-stu-id="0871d-124">In the left-hand menu, click **+ New** to create an **Assessment** project.</span></span> <span data-ttu-id="0871d-125">填寫表單的 [專案名稱] \(其他所有值應保留預設值)，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="0871d-125">Fill in the form with a **Project name** (all other values should be left at their default values) and click **Create**.</span></span> <span data-ttu-id="0871d-126">此時會開啟 [選項]  頁面。</span><span class="sxs-lookup"><span data-stu-id="0871d-126">The **Options** page opens.</span></span>

     ![新 data migration assistant 專案](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-new-project.png)

3. <span data-ttu-id="0871d-128">在 [選項] 頁面上，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="0871d-128">On the **Options** page, click **Next**.</span></span> <span data-ttu-id="0871d-129">此時會開啟 [選取來源] 頁面。</span><span class="sxs-lookup"><span data-stu-id="0871d-129">The **Select sources** page opens.</span></span>

     ![新資料移轉選項](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-options.png) 

4. <span data-ttu-id="0871d-131">在 [選取來源] 頁面上，輸入內含規劃移轉伺服器的 SQL Server 執行個體名稱。</span><span class="sxs-lookup"><span data-stu-id="0871d-131">On the **Select sources** page, enter the name of SQL Server instance containing the server you plan to migrate.</span></span> <span data-ttu-id="0871d-132">視需要變更此頁面上的其他值。</span><span class="sxs-lookup"><span data-stu-id="0871d-132">Change the other values on this page if necessary.</span></span> <span data-ttu-id="0871d-133">按一下 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="0871d-133">Click **Connect**.</span></span>

     ![新資料移轉選取來源](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-sources.png)

5. <span data-ttu-id="0871d-135">在 [選取來源] 頁面的 [新增來源] 部分，針對要測試相容性的資料庫選取核取方塊。</span><span class="sxs-lookup"><span data-stu-id="0871d-135">In the **Add sources** portion of the **Select sources** page, select the checkboxes for the databases to be tested for compatibility.</span></span> <span data-ttu-id="0871d-136">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="0871d-136">Click **Add**.</span></span>

     ![新資料移轉選取來源](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-sources-add.png)

6. <span data-ttu-id="0871d-138">按一下 [開始評估]。</span><span class="sxs-lookup"><span data-stu-id="0871d-138">Click **Start Assessment**.</span></span>

     ![新資料移轉開始評估](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-start-assessment.png)

7. <span data-ttu-id="0871d-140">完成評估後，先查看資料庫是否充分相容可供執行移轉。</span><span class="sxs-lookup"><span data-stu-id="0871d-140">When the assessment completes, first look to see if the database is sufficiently compatible to migrate.</span></span> <span data-ttu-id="0871d-141">尋找以綠色圓圈標示的核取記號。</span><span class="sxs-lookup"><span data-stu-id="0871d-141">Look for the checkmark in a green circle.</span></span>

     ![新資料移轉評估結果相容](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-assessment-results-compatible.png)

8. <span data-ttu-id="0871d-143">檢閱結果。</span><span class="sxs-lookup"><span data-stu-id="0871d-143">Review the results.</span></span> <span data-ttu-id="0871d-144">顯示的 **SQL Server 功能同位檢查**結果是要檢閱的預設結果。</span><span class="sxs-lookup"><span data-stu-id="0871d-144">The **SQL Server feature parity** results shown are the default results to review.</span></span> <span data-ttu-id="0871d-145">特別是檢閱不支援和部分支援功能的相關資訊，以及關於建議動作的提供資訊。</span><span class="sxs-lookup"><span data-stu-id="0871d-145">Specifically review the information about unsupported and partially supported features, and the provided information about recommended actions.</span></span> 

     ![新資料移轉評估同位檢查](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-assessment-results-parity.png)

9. <span data-ttu-id="0871d-147">按一下左上角的選項，以檢閱**相容性問題**。</span><span class="sxs-lookup"><span data-stu-id="0871d-147">Review the **Compatibility issues** by clicking that option in the upper left.</span></span> <span data-ttu-id="0871d-148">特別是針對每個相容性層級，檢閱關於移轉封鎖程式、行為變更和已取代的功能等資訊。</span><span class="sxs-lookup"><span data-stu-id="0871d-148">Specifically review the information about migration blockers, behavior changes, and deprecated features for each compatibility level.</span></span> <span data-ttu-id="0871d-149">針對 AdventureWorks2008R2 資料庫，檢閱自 SQL Server 2008 以來執行的全文檢索搜尋變更，以及自 SQL Server 2000 以來執行的 SERVERPROPERTY('LCID') 變更。</span><span class="sxs-lookup"><span data-stu-id="0871d-149">For the AdventureWorks2008R2 database, review the changes to Full-Text Search since SQL Server 2008 and the changes to SERVERPROPERTY('LCID') since SQL Server 2000.</span></span> <span data-ttu-id="0871d-150">如需這些變更的詳細資訊，請參閱提供的詳細資訊連結。</span><span class="sxs-lookup"><span data-stu-id="0871d-150">For details on these changes, links for more information is provided.</span></span> <span data-ttu-id="0871d-151">全文檢索搜尋的許多選項和設定皆已變更</span><span class="sxs-lookup"><span data-stu-id="0871d-151">Many search options and settings for Full-Text Search have changed</span></span> 

   > [!IMPORTANT] 
   > <span data-ttu-id="0871d-152">您將資料庫移轉至 Azure SQL Database 後，可選擇於目前的相容性層級 (針對 AdventureWorks2008R2 資料庫為等級 100) 或更高等級運作資料庫。</span><span class="sxs-lookup"><span data-stu-id="0871d-152">After you migrate your database to Azure SQL Database, you can choose to operate the database at its current compatibility level (level 100 for the AdventureWorks2008R2 database) or at a higher level.</span></span> <span data-ttu-id="0871d-153">如需於特定相容性層級操作資料庫的含意與選項詳細資訊，請參閱 [ALTER DATABASE 相容性層級 (ALTER DATABASE Compatibility Level)](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)。</span><span class="sxs-lookup"><span data-stu-id="0871d-153">For more information on the implications and options for operating a database at a specific compatibility level, see [ALTER DATABASE Compatibility Level](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span></span> <span data-ttu-id="0871d-154">如需相容性層級其他相關資料庫等級設定的資訊，另請參閱 [ALTER DATABASE 範圍組態 (ALTER DATABASE SCOPED CONFIGURATION)](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql)。</span><span class="sxs-lookup"><span data-stu-id="0871d-154">See also [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) for information about additional database-level settings related to compatibility levels.</span></span>
   >

10. <span data-ttu-id="0871d-155">或是按一下 [Export report (匯出報告)]，以將報告另存為 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="0871d-155">Optionally, click **Export report** to save the report as a JSON file.</span></span>
11. <span data-ttu-id="0871d-156">關閉 Data Migration Assistant。</span><span class="sxs-lookup"><span data-stu-id="0871d-156">Close the Data Migration Assistant.</span></span>

## <a name="export-to-bacpac-file"></a><span data-ttu-id="0871d-157">匯出至 BACPAC 檔案</span><span class="sxs-lookup"><span data-stu-id="0871d-157">Export to BACPAC file</span></span> 

<span data-ttu-id="0871d-158">BACPAC 檔案是一種副檔名為 BACPAC 的 ZIP 檔案，其包含來自 SQL Server Database 的中繼資料和資料。</span><span class="sxs-lookup"><span data-stu-id="0871d-158">A BACPAC file is a ZIP file with an extension of BACPAC containing the metadata and data from a SQL Server database.</span></span> <span data-ttu-id="0871d-159">BACPAC 檔案可以儲存在 Azure Blob 儲存體或是本機儲存體，以供封存或移轉用途 - 例如從 SQL Server 到 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="0871d-159">A BACPAC file can be stored in Azure blob storage or in local storage for archiving or for migration - such as from SQL Server to Azure SQL Database.</span></span> <span data-ttu-id="0871d-160">為維持匯出作業的交易一致性，您必須確保在執行匯出時未執行任何寫入活動。</span><span class="sxs-lookup"><span data-stu-id="0871d-160">For an export to be transactionally consistent, you must ensure either that no write activity is occurring during the export.</span></span>

<span data-ttu-id="0871d-161">遵循以下步驟，使用 SQLPackage 命令列公用程式將 AdventureWorks2008R2 資料庫匯出至本機儲存體。</span><span class="sxs-lookup"><span data-stu-id="0871d-161">Follow these steps to use the SQLPackage command-line utility to export the AdventureWorks2008R2 database to local storage.</span></span>

1. <span data-ttu-id="0871d-162">開啟 Windows 命令提示字元，並將目錄變更為具有 **130** 版本 SQLPackage 的資料夾 - 例如 **C:\Program Files (x86)\Microsoft SQL Server\130\DAC\bin**。</span><span class="sxs-lookup"><span data-stu-id="0871d-162">Open a Windows command prompt and change your directory to a folder in which you have the **130** version of SQLPackage - such as **C:\Program Files (x86)\Microsoft SQL Server\130\DAC\bin**.</span></span>

2. <span data-ttu-id="0871d-163">在命令提示字元中執行下列 SQLPackage 命令，以將 **AdventureWorks2008R2** 資料庫從 **localhost** 匯出至 **AdventureWorks2008R2.bacpac**。</span><span class="sxs-lookup"><span data-stu-id="0871d-163">Execute the following SQLPackage command at the command prompt to export the **AdventureWorks2008R2** database from **localhost** to **AdventureWorks2008R2.bacpac**.</span></span> <span data-ttu-id="0871d-164">將這些值變更為適合您環境的值。</span><span class="sxs-lookup"><span data-stu-id="0871d-164">Change any of these values as appropriate to your environment.</span></span>

    ```SQLPackage
    sqlpackage.exe /Action:Export /ssn:localhost /sdn:AdventureWorks2008R2 /tf:AdventureWorks2008R2.bacpac
    ```

    ![sqlpackage 匯出](./media/sql-database-migrate-your-sql-server-database/sqlpackage-export.png)

<span data-ttu-id="0871d-166">執行完成後，產生的 BACPAC 檔案即會儲存於 sqlpackage 可執行檔的所在目錄。</span><span class="sxs-lookup"><span data-stu-id="0871d-166">Once the execution is complete the generated BACPAC file is stored in the directory where the sqlpackage executable is located.</span></span> <span data-ttu-id="0871d-167">在本範例中為 C:\Program Files (x86)\Microsoft SQL Server\130\DAC\bin。</span><span class="sxs-lookup"><span data-stu-id="0871d-167">In this example C:\Program Files (x86)\Microsoft SQL Server\130\DAC\bin.</span></span> 

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="0871d-168">登入 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="0871d-168">Log in to the Azure portal</span></span>

<span data-ttu-id="0871d-169">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="0871d-169">Log in to the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="0871d-170">從執行 SQLPackage 命令列公用程式的所在電腦登入，可使步驟 5 中的防火牆規則建立作業更加輕鬆。</span><span class="sxs-lookup"><span data-stu-id="0871d-170">Logging on from the computer from which you are running the SQLPackage command-line utility eases the creation of the firewall rule in step 5.</span></span>

## <a name="create-a-sql-server-logical-server"></a><span data-ttu-id="0871d-171">建立 SQL Server 邏輯伺服器</span><span class="sxs-lookup"><span data-stu-id="0871d-171">Create a SQL server logical server</span></span>

<span data-ttu-id="0871d-172">[SQL Server 邏輯伺服器](sql-database-features.md)會作為多個資料庫的中央管理點。</span><span class="sxs-lookup"><span data-stu-id="0871d-172">A [SQL server logical server](sql-database-features.md) acts as a central administrative point for multiple databases.</span></span> <span data-ttu-id="0871d-173">遵循以下步驟建立 SQL Server 邏輯伺服器，以包含完成移轉的 Adventure Works OLTP SQL Server Database。</span><span class="sxs-lookup"><span data-stu-id="0871d-173">Follow these steps to create a SQL server logical server to contain the migrated Adventure Works OLTP SQL Server database.</span></span> 

1. <span data-ttu-id="0871d-174">按一下 Azure 入口網站左上角的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0871d-174">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="0871d-175">在 [新增] 頁面的搜尋視窗中鍵入 **sql server**，然後從篩選清單中選取 [SQL Database (邏輯伺服器)]。</span><span class="sxs-lookup"><span data-stu-id="0871d-175">Type **sql server** in the search window on the **New** page, and select **SQL database (logical server)** from the filtered list.</span></span>

    ![選取邏輯伺服器](./media/sql-database-migrate-your-sql-server-database/logical-server.png)

3. <span data-ttu-id="0871d-177">在 [所有項目] 頁面上按一下 [SQL Server (邏輯伺服器)]，然後在 [SQL Server (邏輯伺服器)] 頁面上按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="0871d-177">On the **Everything** page, click **SQL server (logical server)** and then click **Create** on the **SQL Server (logical server)** page.</span></span>

    ![建立邏輯伺服器](./media/sql-database-migrate-your-sql-server-database/logical-server-create.png)

4. <span data-ttu-id="0871d-179">使用下列資訊填寫 SQL Server (邏輯伺服器) 表單，如上圖所示︰</span><span class="sxs-lookup"><span data-stu-id="0871d-179">Fill out the SQL server (logical server) form with the following information, as shown on the preceding image:</span></span>     

   | <span data-ttu-id="0871d-180">設定</span><span class="sxs-lookup"><span data-stu-id="0871d-180">Setting</span></span>       | <span data-ttu-id="0871d-181">建議的值</span><span class="sxs-lookup"><span data-stu-id="0871d-181">Suggested value</span></span> | <span data-ttu-id="0871d-182">說明</span><span class="sxs-lookup"><span data-stu-id="0871d-182">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="0871d-183">**伺服器名稱**</span><span class="sxs-lookup"><span data-stu-id="0871d-183">**Server name**</span></span> | <span data-ttu-id="0871d-184">輸入任何全域唯一名稱</span><span class="sxs-lookup"><span data-stu-id="0871d-184">Enter any globally unique name</span></span> | <span data-ttu-id="0871d-185">如需有效的伺服器名稱，請參閱[命名規則和限制](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions)。</span><span class="sxs-lookup"><span data-stu-id="0871d-185">For valid server names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> | 
   | <span data-ttu-id="0871d-186">**伺服器管理員登入**</span><span class="sxs-lookup"><span data-stu-id="0871d-186">**Server admin login**</span></span> | <span data-ttu-id="0871d-187">輸入任何有效名稱</span><span class="sxs-lookup"><span data-stu-id="0871d-187">Enter any valid name</span></span> | <span data-ttu-id="0871d-188">如需有效的登入名稱，請參閱[資料庫識別碼](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers)。</span><span class="sxs-lookup"><span data-stu-id="0871d-188">For valid login names, see [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers).</span></span> |
   | <span data-ttu-id="0871d-189">**密碼**</span><span class="sxs-lookup"><span data-stu-id="0871d-189">**Password**</span></span> | <span data-ttu-id="0871d-190">輸入任何有效密碼</span><span class="sxs-lookup"><span data-stu-id="0871d-190">Enter any valid password</span></span> | <span data-ttu-id="0871d-191">您的密碼至少要有 8 個字元，而且必須包含下列幾種字元的其中三種︰大寫字元、小寫字元、數字和非英數字元。</span><span class="sxs-lookup"><span data-stu-id="0871d-191">Your password must have at least 8 characters and must contain characters from three of the following categories: upper case characters, lower case characters, numbers, and non-alphanumeric characters.</span></span> |
   | <span data-ttu-id="0871d-192">**訂用帳戶**</span><span class="sxs-lookup"><span data-stu-id="0871d-192">**Subscription**</span></span> | <span data-ttu-id="0871d-193">選取一個訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0871d-193">Select a subscription</span></span> | <span data-ttu-id="0871d-194">如需訂用帳戶的詳細資訊，請參閱[訂用帳戶](https://account.windowsazure.com/Subscriptions)。</span><span class="sxs-lookup"><span data-stu-id="0871d-194">For details about your subscriptions, see [Subscriptions](https://account.windowsazure.com/Subscriptions).</span></span> |
   | <span data-ttu-id="0871d-195">**資源群組**</span><span class="sxs-lookup"><span data-stu-id="0871d-195">**Resource group**</span></span> | <span data-ttu-id="0871d-196">選擇現有資源群組，或建立新群組，例如 **myResourceGroup**。</span><span class="sxs-lookup"><span data-stu-id="0871d-196">Choose an existing resource group or create a new group, such as **myResourceGroup**</span></span> |  <span data-ttu-id="0871d-197">如需有效的資源群組名稱，請參閱[命名規則和限制](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions)。</span><span class="sxs-lookup"><span data-stu-id="0871d-197">For valid resource group names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> |
   | <span data-ttu-id="0871d-198">**位置**</span><span class="sxs-lookup"><span data-stu-id="0871d-198">**Location**</span></span> | <span data-ttu-id="0871d-199">輸入新伺服器的任何有效位置</span><span class="sxs-lookup"><span data-stu-id="0871d-199">Enter any valid location for the new server</span></span> | <span data-ttu-id="0871d-200">如需區域的相關資訊，請參閱 [Azure 區域](https://azure.microsoft.com/regions/)。</span><span class="sxs-lookup"><span data-stu-id="0871d-200">For information about regions, see [Azure Regions](https://azure.microsoft.com/regions/).</span></span> |

   ![建立邏輯伺服器完成表單](./media/sql-database-migrate-your-sql-server-database/logical-server-create-completed.png)

5. <span data-ttu-id="0871d-202">按一下 [建立] 以佈建邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="0871d-202">Click **Create** to provision the logical server.</span></span> <span data-ttu-id="0871d-203">佈建需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="0871d-203">Provisioning takes a few minutes.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="0871d-204">請記住您的伺服器名稱、伺服器系統管理員登入名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="0871d-204">Remember your server name, server admin login name, and password.</span></span> <span data-ttu-id="0871d-205">在本教學課程後續的內容中，您會需要這些值。</span><span class="sxs-lookup"><span data-stu-id="0871d-205">You need these values later in this tutorial.</span></span>
>

## <a name="create-a-server-level-firewall-rule"></a><span data-ttu-id="0871d-206">建立伺服器層級防火牆規則</span><span class="sxs-lookup"><span data-stu-id="0871d-206">Create a server-level firewall rule</span></span>

<span data-ttu-id="0871d-207">SQL Database 服務會[在伺服器層級建立防火牆](sql-database-firewall-configure.md)，防止外部應用程式和工具連線到伺服器或伺服器上的任何資料庫，除非建立防火牆規則以針對特定的 IP 位址開啟防火牆。</span><span class="sxs-lookup"><span data-stu-id="0871d-207">The SQL Database service creates a [firewall at the server-level](sql-database-firewall-configure.md) that prevents external applications and tools from connecting to the server or any databases on the server unless a firewall rule is created to open the firewall for specific IP addresses.</span></span> <span data-ttu-id="0871d-208">遵循以下步驟，針對您執行 SQLPackage 命令列公用程式所在電腦的 IP 位址，建立 SQL Database 伺服器層級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="0871d-208">Follow these steps to create a SQL Database server-level firewall rule for the IP address of the computer from which you are running the SQLPackage command-line utility.</span></span> <span data-ttu-id="0871d-209">這可讓 SQLPackage 透過 Azure SQL Database 防火牆連線至 SQL Server Database 邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="0871d-209">This enables SQLPackage to connect to the SQL serverDatabase logical server through the Azure SQL Database firewall.</span></span> 

1. <span data-ttu-id="0871d-210">在左側功能表中按一下 [所有資源]，然後在 [所有資源] 頁面按一下新伺服器。</span><span class="sxs-lookup"><span data-stu-id="0871d-210">Click **All resources** from the left-hand menu and click your new server on the **All resources** page.</span></span> <span data-ttu-id="0871d-211">伺服器的概觀頁面隨即開啟，並提供可進行進一步設定的選項。</span><span class="sxs-lookup"><span data-stu-id="0871d-211">The overview page for your server opens and provides options for further configuration.</span></span>

     ![邏輯伺服器概觀](./media/sql-database-migrate-your-sql-server-database/logical-server-overview.png)

2. <span data-ttu-id="0871d-213">在概覽頁面 [設定] 下方的左側功能表中，按一下 [防火牆]。</span><span class="sxs-lookup"><span data-stu-id="0871d-213">Click **Firewall** in the left-hand menu under **Settings** on the overview page.</span></span> <span data-ttu-id="0871d-214">SQL Database 伺服器的 [防火牆設定] 頁面隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="0871d-214">The **Firewall settings** page for the SQL Database server opens.</span></span> 

3. <span data-ttu-id="0871d-215">按一下工具列上的 [新增用戶端 IP]，以新增您目前所用電腦的 IP 位址，然後再按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="0871d-215">Click **Add client IP** on the toolbar to add the IP address of the computer you are currently using and then click **Save**.</span></span> <span data-ttu-id="0871d-216">系統會為此 IP 位址建立伺服器層級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="0871d-216">A server-level firewall rule is created for this IP address.</span></span>

     ![設定伺服器防火牆規則](./media/sql-database-migrate-your-sql-server-database/server-firewall-rule-set.png)

4. <span data-ttu-id="0871d-218">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="0871d-218">Click **OK**.</span></span>

<span data-ttu-id="0871d-219">您現在可以運用 SQL Server Management Studio 或您選擇的其他工具，使用先前建立的伺服器管理帳戶從此 IP 位址連線至此伺服器上的所有資料庫。</span><span class="sxs-lookup"><span data-stu-id="0871d-219">You can now connect to all databases on this server using SQL Server Management Studio or another tool of your choice from this IP address using the server admin account created previously.</span></span>

> [!NOTE]
> <span data-ttu-id="0871d-220">SQL Database 會透過連接埠 1433 通訊。</span><span class="sxs-lookup"><span data-stu-id="0871d-220">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="0871d-221">如果您嘗試從公司網路進行連線，您網路的防火牆可能不允許透過連接埠 1433 的輸出流量。</span><span class="sxs-lookup"><span data-stu-id="0871d-221">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="0871d-222">若情況如此，除非 IT 部門開啟連接埠 1433，否則您無法連線至 Azure SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="0871d-222">If so, you cannot connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="import-a-bacpac-file-to-azure-sql-database"></a><span data-ttu-id="0871d-223">將 BACPAC 檔案匯入到 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="0871d-223">Import a BACPAC file to Azure SQL Database</span></span> 

<span data-ttu-id="0871d-224">最新版本的 SQLPackage 命令列公用程式，支援於指定[服務層和效能等級](sql-database-service-tiers.md)建立 Azure SQL Databose。</span><span class="sxs-lookup"><span data-stu-id="0871d-224">The newest versions of the SQLPackage command-line utility provide support for creating an Azure SQL database at a specified [service tier and performance level](sql-database-service-tiers.md).</span></span> <span data-ttu-id="0871d-225">為了在匯入時取得最佳效能，若服務層與效能等級高於您立即所需，請選取高服務層和效能等級，然後在完成匯入後相應減少。</span><span class="sxs-lookup"><span data-stu-id="0871d-225">For best performance during import, select a high service tier and performance level and then scale down after import if the service tier and performance level is higher than you need immediately.</span></span>

<span data-ttu-id="0871d-226">遵循以下步驟，使用 SQLPackage 命令列公用程式將 AdventureWorks2008R2 資料庫匯入至 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="0871d-226">Follow these steps use the SQLPackage command-line utility to import the AdventureWorks2008R2 database to Azure SQL Database.</span></span> <span data-ttu-id="0871d-227">雖然您可以針對這項工作使用 SQL Server Management Studio，但是 SQLPackage 是大部分實際執行環境的慣用方法，可獲得最大彈性和最佳效能。</span><span class="sxs-lookup"><span data-stu-id="0871d-227">While you can use SQL Server Management Studio for this task, SQLPackage is the preferred method for most production environments for maximum flexibility and best performance.</span></span> <span data-ttu-id="0871d-228">請參閱[使用 BACPAC 檔案從 SQL Server 移轉至 Azure SQL Database](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/)。</span><span class="sxs-lookup"><span data-stu-id="0871d-228">See [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>

- <span data-ttu-id="0871d-229">在命令提示字元中執行下列 SQLPackage 命令，以將 **AdventureWorks2008R2** 資料庫從本機儲存體匯入至您先前建立到新資料庫、[進階] 服務層以及 P6 服務目標的 SQL Server 邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="0871d-229">Execute the following SQLPackage command at the command prompt to import the **AdventureWorks2008R2** database from local storage to the SQL server logical server that you previously created to a new database, a service tier of **Premium**, and a Service Objective of **P6**.</span></span> <span data-ttu-id="0871d-230">將角括號中的值取代為 SQL Server 邏輯伺服器的適當值，並指定新資料庫的名稱 (也會取代角括號)。</span><span class="sxs-lookup"><span data-stu-id="0871d-230">Replace the values in angle brackets with appropriate values for your SQL server logical server and specify a name for the new database (also replace the angle brackets).</span></span> <span data-ttu-id="0871d-231">您也可以選擇將資料庫版本和服務目標的值變更成適合您的環境。</span><span class="sxs-lookup"><span data-stu-id="0871d-231">You can also choose to change the values for database edition and service objectgive as appropriate to your environment.</span></span> <span data-ttu-id="0871d-232">基於本教學課程的用途，已移轉的資料庫稱為 **myMigratedDatabase**。</span><span class="sxs-lookup"><span data-stu-id="0871d-232">For the purpose of this tutorial, the migrated database is called **myMigratedDatabase**.</span></span>

    ```
    SqlPackage.exe /a:import /tcs:"Data Source=<your_server_name>.database.windows.net;Initial Catalog=<your_new_database_name>;User Id=<change_to_your_admin_user_account>;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
    ```

   ![sqlpackage 匯入](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> <span data-ttu-id="0871d-234">SQL Server 邏輯伺服器會接聽連接埠 1433。</span><span class="sxs-lookup"><span data-stu-id="0871d-234">A SQL server logical server listens on port 1433.</span></span> <span data-ttu-id="0871d-235">如果您嘗試從公司防火牆連線至 SQL Server 邏輯伺服器，則必須在公司防火牆中開啟此連接埠，才能成功連線。</span><span class="sxs-lookup"><span data-stu-id="0871d-235">If you are attempting to connect to a SQL server logical server from within a corporate firewall, this port must be open in the corporate firewall for you to successfully connect.</span></span>
>

## <a name="connect-using-sql-server-management-studio-ssms"></a><span data-ttu-id="0871d-236">使用 SQL Server Management Studio (SSMS) 連線</span><span class="sxs-lookup"><span data-stu-id="0871d-236">Connect using SQL Server Management Studio (SSMS)</span></span>

<span data-ttu-id="0871d-237">使用 SQL Server Management Studio，建立對 Azure SQL Database 伺服器與新近已移轉資料庫 (在此教學課程中稱為 **myMigratedDatabase**) 的連線。</span><span class="sxs-lookup"><span data-stu-id="0871d-237">Use SQL Server Management Studio to establish a connection to your Azure SQL Database server and newly migrated database, called **myMigratedDatabase** in this tutorial.</span></span> <span data-ttu-id="0871d-238">若您在執行 SQLPackage 的另一部所處電腦上執行 SQL Server Management Studio，請使用先前程序中說明的步驟，建立此電腦的防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="0871d-238">If you are running SQL Server Management Studio on a different computer from which you ran SQLPackage, create a firewall rule for this computer using the steps in the previous procedure.</span></span>

1. <span data-ttu-id="0871d-239">開啟 SQL Server Management Studio。</span><span class="sxs-lookup"><span data-stu-id="0871d-239">Open SQL Server Management Studio.</span></span>

2. <span data-ttu-id="0871d-240">在 [連接到伺服器] 對話方塊中，輸入下列資訊：</span><span class="sxs-lookup"><span data-stu-id="0871d-240">In the **Connect to Server** dialog box, enter the following information:</span></span>
   - <span data-ttu-id="0871d-241">**伺服器類型**：指定資料庫引擎</span><span class="sxs-lookup"><span data-stu-id="0871d-241">**Server type**: Specify Database engine</span></span>
   - <span data-ttu-id="0871d-242">**伺服器名稱**︰輸入您的完整伺服器名稱，例如 **mynewserver20170403.database.windows.net**</span><span class="sxs-lookup"><span data-stu-id="0871d-242">**Server name**: Enter your fully qualified server name, such as **mynewserver20170403.database.windows.net**</span></span>
   - <span data-ttu-id="0871d-243">**驗證**：指定 SQL Server 驗證</span><span class="sxs-lookup"><span data-stu-id="0871d-243">**Authentication**: Specify SQL Server Authentication</span></span>
   - <span data-ttu-id="0871d-244">**登入**︰輸入您的伺服器管理帳戶</span><span class="sxs-lookup"><span data-stu-id="0871d-244">**Login**: Enter your server admin account</span></span>
   - <span data-ttu-id="0871d-245">**密碼**：輸入伺服器管理帳戶的密碼</span><span class="sxs-lookup"><span data-stu-id="0871d-245">**Password**: Enter the password for your server admin account</span></span>
 
    ![以 ssms 連線](./media/sql-database-migrate-your-sql-server-database/connect-ssms.png)

3. <span data-ttu-id="0871d-247">按一下 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="0871d-247">Click **Connect**.</span></span> <span data-ttu-id="0871d-248">此時會開啟 [物件總管] 視窗。</span><span class="sxs-lookup"><span data-stu-id="0871d-248">The Object Explorer window opens.</span></span> 

4. <span data-ttu-id="0871d-249">在 [物件總管] 中，展開 [資料庫]，然後展開 [myMigratedDatabase] 以檢視範例資料庫中的物件。</span><span class="sxs-lookup"><span data-stu-id="0871d-249">In Object Explorer, expand **Databases** and then expand **myMigratedDatabase** to view the objects in the sample database.</span></span>

## <a name="change-database-properties"></a><span data-ttu-id="0871d-250">變更資料庫屬性</span><span class="sxs-lookup"><span data-stu-id="0871d-250">Change database properties</span></span>

<span data-ttu-id="0871d-251">您可使用 SQL Server Management Studio 變更服務層、效能等級和相容性層級。</span><span class="sxs-lookup"><span data-stu-id="0871d-251">You can change the service tier, performance level, and compatibility level using SQL Server Management Studio.</span></span> <span data-ttu-id="0871d-252">在匯入階段，建議您匯入至更高的效能層級資料庫以獲得最佳效能，但您可以在匯入完成之後相應減少該資料庫以節省成本，直到您準備好主動使用匯入的資料庫為止。</span><span class="sxs-lookup"><span data-stu-id="0871d-252">During the import phase, we recommend that you import to a higher performance tier database for best performance, but that you scale down after the import completes to save money until you are ready to actively use the imported database.</span></span> <span data-ttu-id="0871d-253">變更相容性層級可能會產生較佳的效能，並存取 Azure SQL Database 服務的最新功能。</span><span class="sxs-lookup"><span data-stu-id="0871d-253">Changing the compatibility level may yield better performance and access to the newest capabilities of the Azure SQL Database service.</span></span> <span data-ttu-id="0871d-254">當您移轉較舊的資料庫時，會在與所匯入資料庫相容的最低支援層級維護其資料庫相容性層級。</span><span class="sxs-lookup"><span data-stu-id="0871d-254">When you migrate an older database, its database compatibility level is maintained at the lowest supported level that is compatible with the database being imported.</span></span> <span data-ttu-id="0871d-255">如需詳細資訊，請參閱[改善 Azure SQL Database 中相容性層級 130 的查詢效能](sql-database-compatibility-level-query-performance-130.md).</span><span class="sxs-lookup"><span data-stu-id="0871d-255">For more information, see [Improved query performance with compatibility Level 130 in Azure SQL Database](sql-database-compatibility-level-query-performance-130.md).</span></span>

1. <span data-ttu-id="0871d-256">在 [物件總管] 中，於 [myMigratedDatabase] 上按一下滑鼠右鍵，然後按一下 [新增查詢]。</span><span class="sxs-lookup"><span data-stu-id="0871d-256">In Object Explorer, right-click **myMigratedDatabase** and click **New Query**.</span></span> <span data-ttu-id="0871d-257">此時會開啟已連線到您資料庫的查詢視窗。</span><span class="sxs-lookup"><span data-stu-id="0871d-257">A query window opens connected to your database.</span></span>

2. <span data-ttu-id="0871d-258">執行下列命令，將服務層設定為 [標準]，並將效能等級設定為 [S1]。</span><span class="sxs-lookup"><span data-stu-id="0871d-258">Execute the following command to set the service tier to **Standard** and the performance level to **S1**.</span></span>

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

3. <span data-ttu-id="0871d-260">執行下列命令，將資料庫相容性層級變更為 **130**。</span><span class="sxs-lookup"><span data-stu-id="0871d-260">Execute the following command to change the database compatibility level to **130**.</span></span>

    ```
    ALTER DATABASE myMigratedDatabase  
    SET COMPATIBILITY_LEVEL = 130;
    ```

   ![變更相容性層級](./media/sql-database-migrate-your-sql-server-database/compat-level.png)

## <a name="next-steps"></a><span data-ttu-id="0871d-262">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0871d-262">Next steps</span></span> 
<span data-ttu-id="0871d-263">在本教學課程中，您已準備、匯出和匯入資料庫。</span><span class="sxs-lookup"><span data-stu-id="0871d-263">In this tutorial you prepared, exported and imported your database.</span></span> <span data-ttu-id="0871d-264">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="0871d-264">You learned to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0871d-265">準備 SQL Server 中的資料庫，以便將資料庫移轉至 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="0871d-265">Prepare a database in a SQL Server for migration to Azure SQL Database</span></span>
> * <span data-ttu-id="0871d-266">將資料庫匯出至 BACPAC 檔案</span><span class="sxs-lookup"><span data-stu-id="0871d-266">Export the database to a BACPAC file</span></span>
> * <span data-ttu-id="0871d-267">將 BACPAC 檔案匯入 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="0871d-267">Import the BACPAC file into an Azure SQL Database</span></span>

<span data-ttu-id="0871d-268">前進至下一個教學課程，以了解如何保護資料庫。</span><span class="sxs-lookup"><span data-stu-id="0871d-268">Advance to the next tutorial to learn how to secure your database.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="0871d-269">[保護 Azure SQL Database](sql-database-security-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="0871d-269">[Secure your Azure SQL Database](sql-database-security-tutorial.md).</span></span>


