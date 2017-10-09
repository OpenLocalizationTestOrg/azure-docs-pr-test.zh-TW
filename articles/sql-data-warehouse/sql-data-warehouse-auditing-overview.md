---
title: "在 Azure SQL 資料倉儲 aaaAuditing |Microsoft 文件"
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
ms.openlocfilehash: 948de74fa052ef206cf1aa65c0d81f084b18cb00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="auditing-in-azure-sql-data-warehouse"></a><span data-ttu-id="faa6a-103">Azure SQL 資料倉儲中的稽核</span><span class="sxs-lookup"><span data-stu-id="faa6a-103">Auditing in Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="faa6a-104">稽核</span><span class="sxs-lookup"><span data-stu-id="faa6a-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="faa6a-105">威脅偵測</span><span class="sxs-lookup"><span data-stu-id="faa6a-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

<span data-ttu-id="faa6a-106">SQL 資料倉儲稽核可讓您 toorecord 事件資料庫 tooan 稽核登入您的 Azure 儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="faa6a-106">SQL Data Warehouse auditing allows you toorecord events in your database tooan audit log in your Azure Storage account.</span></span> <span data-ttu-id="faa6a-107">稽核可協助您保持法規遵循、了解資料庫活動，以及深入了解可指出商務考量或疑似安全違規的不一致和異常。</span><span class="sxs-lookup"><span data-stu-id="faa6a-107">Auditing can help you maintain regulatory compliance, understand  database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span> <span data-ttu-id="faa6a-108">SQL 資料倉儲稽核也整合了 Microsoft Power BI，具備向下鑽研報告和分析的功能。</span><span class="sxs-lookup"><span data-stu-id="faa6a-108">SQL Data Warehouse auditing also integrates with Microsoft Power BI for drill-down reporting and analysis.</span></span>

<span data-ttu-id="faa6a-109">稽核工具啟用及促進遵循 toocompliance 標準，但不保證相容性。</span><span class="sxs-lookup"><span data-stu-id="faa6a-109">Auditing tools enable and facilitate adherence toocompliance standards but don't guarantee compliance.</span></span> <span data-ttu-id="faa6a-110">如需有關 Azure 程式該支援標準相容性，請參閱 < hello <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure 信任中心</a>。</span><span class="sxs-lookup"><span data-stu-id="faa6a-110">For more information about Azure programs that support standards compliance, see hello <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure Trust Center</a>.</span></span>

* <span data-ttu-id="faa6a-111">[資料庫稽核基本概念]</span><span class="sxs-lookup"><span data-stu-id="faa6a-111">[Database Auditing basics]</span></span>
* <span data-ttu-id="faa6a-112">[設定資料庫的稽核]</span><span class="sxs-lookup"><span data-stu-id="faa6a-112">[Set up auditing for your database]</span></span>
* <span data-ttu-id="faa6a-113">[分析稽核記錄和報告]</span><span class="sxs-lookup"><span data-stu-id="faa6a-113">[Analyze audit logs and reports]</span></span>

## <span data-ttu-id="faa6a-114"><a id="subheading-1"></a>Azure SQL 資料倉儲資料庫稽核基本概念</span><span class="sxs-lookup"><span data-stu-id="faa6a-114"><a id="subheading-1"></a>Azure SQL Data Warehouse Database Auditing basics</span></span>
<span data-ttu-id="faa6a-115">SQL 資料倉儲資料庫稽核可讓您：</span><span class="sxs-lookup"><span data-stu-id="faa6a-115">SQL Data Warehouse database auditing allows you to:</span></span>

* <span data-ttu-id="faa6a-116">**保留** 所選事件的稽核記錄。</span><span class="sxs-lookup"><span data-stu-id="faa6a-116">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="faa6a-117">您可以定義資料庫動作 toobe 稽核的類別。</span><span class="sxs-lookup"><span data-stu-id="faa6a-117">You can define categories of database actions  toobe audited.</span></span>
* <span data-ttu-id="faa6a-118">**報告** 資料庫活動。</span><span class="sxs-lookup"><span data-stu-id="faa6a-118">**Report** on database activity.</span></span> <span data-ttu-id="faa6a-119">您可以使用預先設定的報表和儀表板 tooget 快速地開始使用活動和事件報告。</span><span class="sxs-lookup"><span data-stu-id="faa6a-119">You can use preconfigured reports and a dashboard tooget started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="faa6a-120">**分析** 報告。</span><span class="sxs-lookup"><span data-stu-id="faa6a-120">**Analyze** reports.</span></span> <span data-ttu-id="faa6a-121">您可以尋找可疑事件、異常活動及趨勢。</span><span class="sxs-lookup"><span data-stu-id="faa6a-121">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="faa6a-122">您可以設定下列事件類別目錄的 hello 的稽核：</span><span class="sxs-lookup"><span data-stu-id="faa6a-122">You can configure auditing for hello following event categories:</span></span>

<span data-ttu-id="faa6a-123">**一般 SQL**和**參數化 SQL**收集的稽核記錄檔分類為哪些 hello</span><span class="sxs-lookup"><span data-stu-id="faa6a-123">**Plain SQL** and **Parameterized SQL** for which hello collected audit logs are classified as</span></span>  

* <span data-ttu-id="faa6a-124">**存取 toodata**</span><span class="sxs-lookup"><span data-stu-id="faa6a-124">**Access toodata**</span></span>
* <span data-ttu-id="faa6a-125">**結構描述變更 (DDL)**</span><span class="sxs-lookup"><span data-stu-id="faa6a-125">**Schema changes (DDL)**</span></span>
* <span data-ttu-id="faa6a-126">**資料變更 (DML)**</span><span class="sxs-lookup"><span data-stu-id="faa6a-126">**Data changes (DML)**</span></span>
* <span data-ttu-id="faa6a-127">**帳戶、角色和權限 (DCL)**</span><span class="sxs-lookup"><span data-stu-id="faa6a-127">**Accounts, roles, and permissions (DCL)**</span></span>
* <span data-ttu-id="faa6a-128">**預存程序**、**登入**以及**交易管理**。</span><span class="sxs-lookup"><span data-stu-id="faa6a-128">**Stored Procedure**, **Login** and, **Transaction Management**.</span></span>

<span data-ttu-id="faa6a-129">針對每個事件類別，分別設定**成功**和**失敗**作業的稽核。</span><span class="sxs-lookup"><span data-stu-id="faa6a-129">For each Event Category, Auditing of **Success** and **Failure** operations are configured separately.</span></span>

<span data-ttu-id="faa6a-130">如需有關 hello 活動和稽核事件的詳細資訊，請參閱 hello<a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">稽核記錄檔格式參考 （文件檔案下載）</a>。</span><span class="sxs-lookup"><span data-stu-id="faa6a-130">For more information about hello activities and events audited, see hello <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">Audit Log Format Reference (doc file download)</a>.</span></span>

<span data-ttu-id="faa6a-131">稽核記錄會儲存在 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="faa6a-131">Audit logs are stored in your Azure storage account.</span></span> <span data-ttu-id="faa6a-132">您可以定義稽核記錄保留期間。</span><span class="sxs-lookup"><span data-stu-id="faa6a-132">You can define an audit log retention period.</span></span>

<span data-ttu-id="faa6a-133">可以針對特定資料庫定義稽核原則，或將稽核原則定義為預設伺服器原則。</span><span class="sxs-lookup"><span data-stu-id="faa6a-133">An auditing policy can be defined for a specific database or as a default server policy.</span></span> <span data-ttu-id="faa6a-134">預設伺服器稽核原則會套用 tooall 資料庫並沒有特定覆寫資料庫稽核原則定義的伺服器上。</span><span class="sxs-lookup"><span data-stu-id="faa6a-134">A default server auditing policy applies tooall databases on a server, which do not have a specific overriding database auditing policy defined.</span></span>

<span data-ttu-id="faa6a-135">在設定稽核之前，請檢查您是否正在使用[「下層用戶端」](sql-data-warehouse-auditing-downlevel-clients.md)。</span><span class="sxs-lookup"><span data-stu-id="faa6a-135">Before setting up audit auditing check if you are using a ["Downlevel Client."](sql-data-warehouse-auditing-downlevel-clients.md)</span></span>

## <span data-ttu-id="faa6a-136"><a id="subheading-2"></a>設定資料庫的稽核</span><span class="sxs-lookup"><span data-stu-id="faa6a-136"><a id="subheading-2"></a>Set up auditing for your database</span></span>
1. <span data-ttu-id="faa6a-137">啟動 hello <a href="https://portal.azure.com" target="_blank">Azure 入口網站</a>。</span><span class="sxs-lookup"><span data-stu-id="faa6a-137">Launch hello <a href="https://portal.azure.com" target="_blank">Azure portal</a>.</span></span>
2. <span data-ttu-id="faa6a-138">移 toohello**設定**刀鋒視窗中的 hello 想 tooaudit SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="faa6a-138">Go toohello **Settings** blade of hello SQL Data Warehouse you want tooaudit.</span></span> <span data-ttu-id="faa6a-139">在 hello**設定**刀鋒視窗中，選取**稽核與威脅偵測**。</span><span class="sxs-lookup"><span data-stu-id="faa6a-139">In hello **Settings** blade, select **Auditing & Threat detection**.</span></span>
   
    ![][1]
3. <span data-ttu-id="faa6a-140">接下來，啟用 稽核，即可 hello **ON**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="faa6a-140">Next, enable auditing by clicking hello **ON** button.</span></span>
   
    ![][3]
4. <span data-ttu-id="faa6a-141">在 hello 稽核組態刀鋒視窗中，選取 **儲存詳細資料**tooopen hello 稽核記錄檔儲存體 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="faa6a-141">In hello auditing configuration blade, select **STORAGE DETAILS** tooopen hello Audit Logs Storage blade.</span></span> <span data-ttu-id="faa6a-142">選取要儲存記錄檔的 Azure 儲存體帳戶 hello 和 hello 保留期限。</span><span class="sxs-lookup"><span data-stu-id="faa6a-142">Select hello Azure storage account where logs will be saved and, hello retention period.</span></span> 
>[!TIP]
><span data-ttu-id="faa6a-143">使用相同的儲存體帳戶的所有稽核的資料庫 tooget hello 充分利用 hello 預先設定的 hello 報告範本。</span><span class="sxs-lookup"><span data-stu-id="faa6a-143">Use hello same storage account for all audited databases tooget hello most out of hello pre-configured reports templates.</span></span>
   
    ![][4]
5. <span data-ttu-id="faa6a-144">按一下 hello**確定**按鈕 toosave hello 儲存體的詳細資料設定。</span><span class="sxs-lookup"><span data-stu-id="faa6a-144">Click hello **OK** button toosave hello storage details configuration.</span></span>
6. <span data-ttu-id="faa6a-145">在下**記錄的事件**，按一下 **成功**和**失敗**toolog 所有事件，或選擇個別的事件類別。</span><span class="sxs-lookup"><span data-stu-id="faa6a-145">Under **LOGGING BY EVENT**, click **SUCCESS** and **FAILURE** toolog all events, or choose individual event categories.</span></span>
7. <span data-ttu-id="faa6a-146">如果您要針對資料庫設定稽核，您可能需要您正確地擷取資料稽核的用戶端 tooensure tooalter hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="faa6a-146">If you are configuring Auditing for a database, you may need tooalter hello connection string of your client tooensure data auditing is correctly captured.</span></span> <span data-ttu-id="faa6a-147">檢查 hello [hello 連接字串中修改伺服器 FDQN](sql-data-warehouse-auditing-downlevel-clients.md)下層用戶端連線的主題。</span><span class="sxs-lookup"><span data-stu-id="faa6a-147">Check hello [Modify Server FDQN in hello connection string](sql-data-warehouse-auditing-downlevel-clients.md) topic for downlevel client connections.</span></span>
8. <span data-ttu-id="faa6a-148">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="faa6a-148">Click **OK**.</span></span>

## <span data-ttu-id="faa6a-149"><a id="subheading-3"></a>分析稽核記錄和報告</span><span class="sxs-lookup"><span data-stu-id="faa6a-149"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="faa6a-150">稽核記錄檔彙總集合中的存放區資料表與**SQLDBAuditLogs** hello 您在安裝期間所選擇的 Azure 儲存體帳戶中的前置詞。</span><span class="sxs-lookup"><span data-stu-id="faa6a-150">Audit logs are aggregated in a collection of Store Tables with a **SQLDBAuditLogs** prefix in hello Azure storage account you chose during setup.</span></span> <span data-ttu-id="faa6a-151">您可以使用工具 (例如 <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Azure 儲存體總管</a>) 來檢視記錄檔。</span><span class="sxs-lookup"><span data-stu-id="faa6a-151">You can view log files using a tool such as <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Azure Storage Explorer</a>.</span></span>

<span data-ttu-id="faa6a-152">預先設定的儀表板報表範本可做為<a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">可下載的 Excel 試算表</a>toohelp 您快速地分析記錄資料。</span><span class="sxs-lookup"><span data-stu-id="faa6a-152">A preconfigured dashboard report template is available as a <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">downloadable Excel spreadsheet</a> toohelp you quickly analyze log data.</span></span> <span data-ttu-id="faa6a-153">在稽核記錄 toouse hello 範本，您需要 Excel 2013 或更新版本，以及 Power Query，您可以下載<a href="http://www.microsoft.com/download/details.aspx?id=39379">這裡</a>。</span><span class="sxs-lookup"><span data-stu-id="faa6a-153">toouse hello template on your audit logs, you need Excel 2013 or later and Power Query, which you can download <a href="http://www.microsoft.com/download/details.aspx?id=39379">here</a>.</span></span>

<span data-ttu-id="faa6a-154">hello 範本中，有虛構範例資料，您可以設定 Power Query tooimport 稽核記錄直接從您的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="faa6a-154">hello template has fictional sample data in it, and you can set up Power Query tooimport your audit log directly from your Azure storage account.</span></span>

## <span data-ttu-id="faa6a-155"><a id="subheading-4"></a>儲存體金鑰重新產生</span><span class="sxs-lookup"><span data-stu-id="faa6a-155"><a id="subheading-4"></a>Storage key regeneration</span></span>
<span data-ttu-id="faa6a-156">實際執行環境，您就有可能您的儲存體金鑰定期的 toorefresh。</span><span class="sxs-lookup"><span data-stu-id="faa6a-156">In production, you are likely toorefresh your storage keys periodically.</span></span> <span data-ttu-id="faa6a-157">當重新整理您的金鑰，您會需要 toosave hello 原則。</span><span class="sxs-lookup"><span data-stu-id="faa6a-157">When refreshing your keys, you need toosave hello policy.</span></span> <span data-ttu-id="faa6a-158">hello 程序如下所示：</span><span class="sxs-lookup"><span data-stu-id="faa6a-158">hello process is as follows:</span></span>

1. <span data-ttu-id="faa6a-159">在 hello 稽核 （上面所述在 hello 稽核 > 一節的安裝程式） 的組態刀鋒視窗中切換 hello**儲存體存取金鑰**從*主要*太*次要*和**儲存**。</span><span class="sxs-lookup"><span data-stu-id="faa6a-159">In hello auditing configuration blade (described above in hello setup auditing section) switch hello **Storage Access Key** from *Primary* too*Secondary* and **SAVE**.</span></span>

   ![][4]
2. <span data-ttu-id="faa6a-160">移 toohello 存放裝置設定 刀鋒視窗和**重新產生**hello*主要存取金鑰*。</span><span class="sxs-lookup"><span data-stu-id="faa6a-160">Go toohello storage configuration blade and **regenerate** hello *Primary Access Key*.</span></span>
3. <span data-ttu-id="faa6a-161">返回 toohello 稽核組態刀鋒視窗中，交換器 hello**儲存體存取金鑰**從*次要*太*主要*按**儲存**。</span><span class="sxs-lookup"><span data-stu-id="faa6a-161">Go back toohello auditing configuration blade, switch hello **Storage Access Key** from *Secondary* too*Primary* and press **SAVE**.</span></span>
4. <span data-ttu-id="faa6a-162">返回 toohello 儲存 UI 和**重新產生**hello*次要存取金鑰*（hello 準備為下一個索引鍵重新整理週期。</span><span class="sxs-lookup"><span data-stu-id="faa6a-162">Go back toohello storage UI and **regenerate** hello *Secondary Access Key* (as preparation for hello next keys refresh cycle.</span></span>

## <span data-ttu-id="faa6a-163"><a id="subheading-5"></a>自動化 (PowerShell/REST API)</span><span class="sxs-lookup"><span data-stu-id="faa6a-163"><a id="subheading-5"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="faa6a-164">您也可以設定 Azure SQL 資料倉儲中的稽核使用 hello 遵循自動化工具：</span><span class="sxs-lookup"><span data-stu-id="faa6a-164">You can also configure auditing in Azure SQL Data Warehouse by using hello following automation tools:</span></span>

* <span data-ttu-id="faa6a-165">**PowerShell Cmdlet**：</span><span class="sxs-lookup"><span data-stu-id="faa6a-165">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="faa6a-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="faa6a-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="faa6a-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="faa6a-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="faa6a-168">[Remove-AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="faa6a-168">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="faa6a-169">[Remove-AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="faa6a-169">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="faa6a-170">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="faa6a-170">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="faa6a-171">[Set-AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="faa6a-171">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="faa6a-172">[Use-AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="faa6a-172">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

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