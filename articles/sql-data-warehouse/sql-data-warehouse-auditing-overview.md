---
title: "Azure SQL 資料倉儲中的稽核 | Microsoft Docs"
description: "開始使用 Azure SQL 資料倉儲中的稽核"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: 0e6af148-b218-4b43-bb5f-907917d20330
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 08/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: f851c82ebeaa647f663d499a4d327c3479e36121
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="auditing-in-azure-sql-data-warehouse"></a><span data-ttu-id="2b222-103">Azure SQL 資料倉儲中的稽核</span><span class="sxs-lookup"><span data-stu-id="2b222-103">Auditing in Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2b222-104">稽核</span><span class="sxs-lookup"><span data-stu-id="2b222-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="2b222-105">威脅偵測</span><span class="sxs-lookup"><span data-stu-id="2b222-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

<span data-ttu-id="2b222-106">SQL 資料倉儲稽核可讓您將資料庫中的事件記錄到 Azure 儲存體帳戶中的稽核記錄。</span><span class="sxs-lookup"><span data-stu-id="2b222-106">SQL Data Warehouse auditing allows you to record events in your database to an audit log in your Azure Storage account.</span></span> <span data-ttu-id="2b222-107">稽核可協助您保持法規遵循、了解資料庫活動，以及深入了解可指出商務考量或疑似安全違規的不一致和異常。</span><span class="sxs-lookup"><span data-stu-id="2b222-107">Auditing can help you maintain regulatory compliance, understand  database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span> <span data-ttu-id="2b222-108">SQL 資料倉儲稽核也整合了 Microsoft Power BI，具備向下鑽研報告和分析的功能。</span><span class="sxs-lookup"><span data-stu-id="2b222-108">SQL Data Warehouse auditing also integrates with Microsoft Power BI for drill-down reporting and analysis.</span></span>

<span data-ttu-id="2b222-109">稽核工具啟用及推動遵循法規標準，但不保證符合法規。</span><span class="sxs-lookup"><span data-stu-id="2b222-109">Auditing tools enable and facilitate adherence to compliance standards but don't guarantee compliance.</span></span> <span data-ttu-id="2b222-110">如需有關支援標準法規的 Azure 程式詳細資訊，請參閱 <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure 信任中心</a>。</span><span class="sxs-lookup"><span data-stu-id="2b222-110">For more information about Azure programs that support standards compliance, see the <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure Trust Center</a>.</span></span>

* <span data-ttu-id="2b222-111">[資料庫稽核基本概念]</span><span class="sxs-lookup"><span data-stu-id="2b222-111">[Database Auditing basics]</span></span>
* <span data-ttu-id="2b222-112">[設定資料庫的稽核]</span><span class="sxs-lookup"><span data-stu-id="2b222-112">[Set up auditing for your database]</span></span>
* <span data-ttu-id="2b222-113">[分析稽核記錄和報告]</span><span class="sxs-lookup"><span data-stu-id="2b222-113">[Analyze audit logs and reports]</span></span>

## <span data-ttu-id="2b222-114"><a id="subheading-1"></a>Azure SQL 資料倉儲資料庫稽核基本概念</span><span class="sxs-lookup"><span data-stu-id="2b222-114"><a id="subheading-1"></a>Azure SQL Data Warehouse Database Auditing basics</span></span>
<span data-ttu-id="2b222-115">SQL 資料倉儲資料庫稽核可讓您：</span><span class="sxs-lookup"><span data-stu-id="2b222-115">SQL Data Warehouse database auditing allows you to:</span></span>

* <span data-ttu-id="2b222-116">**保留** 所選事件的稽核記錄。</span><span class="sxs-lookup"><span data-stu-id="2b222-116">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="2b222-117">您可以定義要稽核的資料庫動作類別。</span><span class="sxs-lookup"><span data-stu-id="2b222-117">You can define categories of database actions  to be audited.</span></span>
* <span data-ttu-id="2b222-118">**報告** 資料庫活動。</span><span class="sxs-lookup"><span data-stu-id="2b222-118">**Report** on database activity.</span></span> <span data-ttu-id="2b222-119">您可以使用預先設定的報告和儀表板，以便快速開始使用活動和事件報告。</span><span class="sxs-lookup"><span data-stu-id="2b222-119">You can use preconfigured reports and a dashboard to get started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="2b222-120">**分析** 報告。</span><span class="sxs-lookup"><span data-stu-id="2b222-120">**Analyze** reports.</span></span> <span data-ttu-id="2b222-121">您可以尋找可疑事件、異常活動及趨勢。</span><span class="sxs-lookup"><span data-stu-id="2b222-121">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="2b222-122">您可以設定下列事件類別的稽核：</span><span class="sxs-lookup"><span data-stu-id="2b222-122">You can configure auditing for the following event categories:</span></span>

<span data-ttu-id="2b222-123">**一般 SQL** 和**參數化 SQL**，且為它們所收集的稽核記錄歸類為</span><span class="sxs-lookup"><span data-stu-id="2b222-123">**Plain SQL** and **Parameterized SQL** for which the collected audit logs are classified as</span></span>  

* <span data-ttu-id="2b222-124">**資料存取**</span><span class="sxs-lookup"><span data-stu-id="2b222-124">**Access to data**</span></span>
* <span data-ttu-id="2b222-125">**結構描述變更 (DDL)**</span><span class="sxs-lookup"><span data-stu-id="2b222-125">**Schema changes (DDL)**</span></span>
* <span data-ttu-id="2b222-126">**資料變更 (DML)**</span><span class="sxs-lookup"><span data-stu-id="2b222-126">**Data changes (DML)**</span></span>
* <span data-ttu-id="2b222-127">**帳戶、角色和權限 (DCL)**</span><span class="sxs-lookup"><span data-stu-id="2b222-127">**Accounts, roles, and permissions (DCL)**</span></span>
* <span data-ttu-id="2b222-128">**預存程序**、**登入**以及**交易管理**。</span><span class="sxs-lookup"><span data-stu-id="2b222-128">**Stored Procedure**, **Login** and, **Transaction Management**.</span></span>

<span data-ttu-id="2b222-129">針對每個事件類別，分別設定**成功**和**失敗**作業的稽核。</span><span class="sxs-lookup"><span data-stu-id="2b222-129">For each Event Category, Auditing of **Success** and **Failure** operations are configured separately.</span></span>

<span data-ttu-id="2b222-130">如需已稽核之活動和事件的詳細資訊，請參閱<a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">稽核記錄格式參考 (doc 檔案下載)</a>。</span><span class="sxs-lookup"><span data-stu-id="2b222-130">For more information about the activities and events audited, see the <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">Audit Log Format Reference (doc file download)</a>.</span></span>

<span data-ttu-id="2b222-131">稽核記錄會儲存在 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="2b222-131">Audit logs are stored in your Azure storage account.</span></span> <span data-ttu-id="2b222-132">您可以定義稽核記錄保留期間。</span><span class="sxs-lookup"><span data-stu-id="2b222-132">You can define an audit log retention period.</span></span>

<span data-ttu-id="2b222-133">可以針對特定資料庫定義稽核原則，或將稽核原則定義為預設伺服器原則。</span><span class="sxs-lookup"><span data-stu-id="2b222-133">An auditing policy can be defined for a specific database or as a default server policy.</span></span> <span data-ttu-id="2b222-134">預設伺服器稽核原則會套用至伺服器上的所有資料庫，其中該伺服器並沒有定義特定覆寫的資料庫稽核原則。</span><span class="sxs-lookup"><span data-stu-id="2b222-134">A default server auditing policy applies to all databases on a server, which do not have a specific overriding database auditing policy defined.</span></span>

<span data-ttu-id="2b222-135">在設定稽核之前，請檢查您是否正在使用[「下層用戶端」](sql-data-warehouse-auditing-downlevel-clients.md)。</span><span class="sxs-lookup"><span data-stu-id="2b222-135">Before setting up audit auditing check if you are using a ["Downlevel Client."](sql-data-warehouse-auditing-downlevel-clients.md)</span></span>

## <span data-ttu-id="2b222-136"><a id="subheading-2"></a>設定資料庫的稽核</span><span class="sxs-lookup"><span data-stu-id="2b222-136"><a id="subheading-2"></a>Set up auditing for your database</span></span>
1. <span data-ttu-id="2b222-137">啟動 <a href="https://portal.azure.com" target="_blank">Azure 入口網站</a>。</span><span class="sxs-lookup"><span data-stu-id="2b222-137">Launch the <a href="https://portal.azure.com" target="_blank">Azure portal</a>.</span></span>
2. <span data-ttu-id="2b222-138">移至您想要稽核之 SQL 資料倉儲的 [設定] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2b222-138">Go to the **Settings** blade of the SQL Data Warehouse you want to audit.</span></span> <span data-ttu-id="2b222-139">在 [設定] 刀鋒視窗中，選取 [稽核與威脅偵測]。</span><span class="sxs-lookup"><span data-stu-id="2b222-139">In the **Settings** blade, select **Auditing & Threat detection**.</span></span>
   
    ![][1]
3. <span data-ttu-id="2b222-140">接下來，按一下 [開啟]  按鈕，來啟用稽核。</span><span class="sxs-lookup"><span data-stu-id="2b222-140">Next, enable auditing by clicking the **ON** button.</span></span>
   
    ![][3]
4. <span data-ttu-id="2b222-141">在 [稽核組態] 刀鋒視窗中，選取 [儲存體詳細資料]，以開啟 [稽核記錄儲存體] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2b222-141">In the auditing configuration blade, select **STORAGE DETAILS** to open the Audit Logs Storage blade.</span></span> <span data-ttu-id="2b222-142">選取將儲存記錄的 Azure 儲存體帳戶以及保留期間。</span><span class="sxs-lookup"><span data-stu-id="2b222-142">Select the Azure storage account where logs will be saved and, the retention period.</span></span> 
>[!TIP]
><span data-ttu-id="2b222-143">在所有稽核的資料庫中使用相同的儲存體帳戶，以充分利用預先設定的報告範本。</span><span class="sxs-lookup"><span data-stu-id="2b222-143">Use the same storage account for all audited databases to get the most out of the pre-configured reports templates.</span></span>
   
    ![][4]
5. <span data-ttu-id="2b222-144">按一下 [確定]  按鈕，以儲存儲存體的詳細資料組態。</span><span class="sxs-lookup"><span data-stu-id="2b222-144">Click the **OK** button to save the storage details configuration.</span></span>
6. <span data-ttu-id="2b222-145">在 [依事件記錄] 下，按一下 [成功] 和 [失敗] 以記錄所有事件，或選擇個別的事件類別。</span><span class="sxs-lookup"><span data-stu-id="2b222-145">Under **LOGGING BY EVENT**, click **SUCCESS** and **FAILURE** to log all events, or choose individual event categories.</span></span>
7. <span data-ttu-id="2b222-146">如果您正在為資料庫設定稽核，您可能需要變更用戶端的連接字串，以確保系統會正確擷取資料稽核。</span><span class="sxs-lookup"><span data-stu-id="2b222-146">If you are configuring Auditing for a database, you may need to alter the connection string of your client to ensure data auditing is correctly captured.</span></span> <span data-ttu-id="2b222-147">請參閱 [修改連接字串中的伺服器 FDQN](sql-data-warehouse-auditing-downlevel-clients.md) 主題，以取得下層用戶端連線。</span><span class="sxs-lookup"><span data-stu-id="2b222-147">Check the [Modify Server FDQN in the connection string](sql-data-warehouse-auditing-downlevel-clients.md) topic for downlevel client connections.</span></span>
8. <span data-ttu-id="2b222-148">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="2b222-148">Click **OK**.</span></span>

## <span data-ttu-id="2b222-149"><a id="subheading-3"></a>分析稽核記錄和報告</span><span class="sxs-lookup"><span data-stu-id="2b222-149"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="2b222-150">在安裝期間，會在所選擇的 Azure 儲存體帳戶之具有 **SQLDBAuditLogs** 首碼的 [儲存資料表] 集合中彙總稽核記錄。</span><span class="sxs-lookup"><span data-stu-id="2b222-150">Audit logs are aggregated in a collection of Store Tables with a **SQLDBAuditLogs** prefix in the Azure storage account you chose during setup.</span></span> <span data-ttu-id="2b222-151">您可以使用工具 (例如 <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Azure 儲存體總管</a>) 來檢視記錄檔。</span><span class="sxs-lookup"><span data-stu-id="2b222-151">You can view log files using a tool such as <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Azure Storage Explorer</a>.</span></span>

<span data-ttu-id="2b222-152">預先設定的儀表板報告範本會以<a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">可下載的 Excel 試算表</a>形式提供，以協助您快速分析記錄資料。</span><span class="sxs-lookup"><span data-stu-id="2b222-152">A preconfigured dashboard report template is available as a <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">downloadable Excel spreadsheet</a> to help you quickly analyze log data.</span></span> <span data-ttu-id="2b222-153">若要在稽核記錄上使用範本，您需要 Excel 2013 (或更新版本) 和 Power Query (您可從<a href="http://www.microsoft.com/download/details.aspx?id=39379">此處</a>下載)。</span><span class="sxs-lookup"><span data-stu-id="2b222-153">To use the template on your audit logs, you need Excel 2013 or later and Power Query, which you can download <a href="http://www.microsoft.com/download/details.aspx?id=39379">here</a>.</span></span>

<span data-ttu-id="2b222-154">範本中包含虛構的範例資料，您可以設定 Power Query 直接從 Azure 儲存體帳戶匯入稽核記錄。</span><span class="sxs-lookup"><span data-stu-id="2b222-154">The template has fictional sample data in it, and you can set up Power Query to import your audit log directly from your Azure storage account.</span></span>

## <span data-ttu-id="2b222-155"><a id="subheading-4"></a>儲存體金鑰重新產生</span><span class="sxs-lookup"><span data-stu-id="2b222-155"><a id="subheading-4"></a>Storage key regeneration</span></span>
<span data-ttu-id="2b222-156">在生產中，您可能會定期重新整理儲存體金鑰。</span><span class="sxs-lookup"><span data-stu-id="2b222-156">In production, you are likely to refresh your storage keys periodically.</span></span> <span data-ttu-id="2b222-157">重新整理金鑰時，您需要儲存該原則。</span><span class="sxs-lookup"><span data-stu-id="2b222-157">When refreshing your keys, you need to save the policy.</span></span> <span data-ttu-id="2b222-158">程序如下：</span><span class="sxs-lookup"><span data-stu-id="2b222-158">The process is as follows:</span></span>

1. <span data-ttu-id="2b222-159">在 [稽核組態] 刀鋒視窗中 (如以上的設定稽核一節所述)，將 [儲存體存取金鑰] 從 [主要] 切換為 [次要]，並按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="2b222-159">In the auditing configuration blade (described above in the setup auditing section) switch the **Storage Access Key** from *Primary* to *Secondary* and **SAVE**.</span></span>

   ![][4]
2. <span data-ttu-id="2b222-160">進入 [儲存體組態] 刀鋒視窗，並**重新產生***主要存取金鑰*。</span><span class="sxs-lookup"><span data-stu-id="2b222-160">Go to the storage configuration blade and **regenerate** the *Primary Access Key*.</span></span>
3. <span data-ttu-id="2b222-161">返回 [稽核組態] 刀鋒視窗，並且將 [儲存體存取金鑰] 從 [次要]切換為 [主要]，然後按下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="2b222-161">Go back to the auditing configuration blade, switch the **Storage Access Key** from *Secondary* to *Primary* and press **SAVE**.</span></span>
4. <span data-ttu-id="2b222-162">返回儲存體 UI 並**重新產生**「次要存取金鑰」 (為了下一個金鑰重新整理週期做準備)。</span><span class="sxs-lookup"><span data-stu-id="2b222-162">Go back to the storage UI and **regenerate** the *Secondary Access Key* (as preparation for the next keys refresh cycle.</span></span>

## <span data-ttu-id="2b222-163"><a id="subheading-5"></a>自動化 (PowerShell/REST API)</span><span class="sxs-lookup"><span data-stu-id="2b222-163"><a id="subheading-5"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="2b222-164">您也可以使用下列自動化工具在 Azure SQL 資料倉儲中設定稽核：</span><span class="sxs-lookup"><span data-stu-id="2b222-164">You can also configure auditing in Azure SQL Data Warehouse by using the following automation tools:</span></span>

* <span data-ttu-id="2b222-165">**PowerShell Cmdlet**：</span><span class="sxs-lookup"><span data-stu-id="2b222-165">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="2b222-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="2b222-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="2b222-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="2b222-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="2b222-168">[Remove-AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="2b222-168">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="2b222-169">[Remove-AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="2b222-169">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="2b222-170">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="2b222-170">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="2b222-171">[Set-AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="2b222-171">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="2b222-172">[Use-AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="2b222-172">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

<!--Anchors-->
[資料庫稽核基本概念]: #subheading-1
[設定資料庫的稽核]: #subheading-2
[分析稽核記錄和報告]: #subheading-3


<!--Image references-->
[1]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing.png
[2]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-inherit.png
[3]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-enable.png
[4]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-storage-account.png
[5]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-dashboard.png


<!--Link references-->
[101]: /powershell/module/azurerm.sql/get-azurermsqldatabaseauditingpolicy
[102]: /powershell/module/azurerm.sql/Get-AzureRMSqlServerAuditingPolicy
[103]: /powershell/module/azurerm.sql/Remove-AzureRMSqlDatabaseAuditing
[104]: /powershell/module/azurerm.sql/Remove-AzureRMSqlServerAuditing
[105]: /powershell/module/azurerm.sql/Set-AzureRMSqlDatabaseAuditingPolicy
[106]: /powershell/module/azurerm.sql/Set-AzureRMSqlServerAuditingPolicy
[107]: /powershell/module/azurerm.sql/Use-AzureRMSqlServerAuditingPolicy