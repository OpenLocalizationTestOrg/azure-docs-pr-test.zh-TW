---
title: "Azure SQL database 稽核入門 aaaGet |Microsoft 文件"
description: "開始使用 Azure SQL 資料庫稽核"
services: sql-database
documentationcenter: 
author: giladm
manager: jhubbard
editor: giladm
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: giladm
ms.openlocfilehash: 5494c602d702ac41992520f900c393a98cc7c989
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-database-auditing"></a><span data-ttu-id="f7c9e-103">開始使用 SQL Database 稽核</span><span class="sxs-lookup"><span data-stu-id="f7c9e-103">Get started with SQL database auditing</span></span>
<span data-ttu-id="f7c9e-104">Azure SQL database 稽核會追蹤資料庫事件，並將它們 tooan 稽核記錄您 Azure 儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-104">Azure SQL database auditing tracks database events and writes them tooan audit log in your Azure storage account.</span></span> <span data-ttu-id="f7c9e-105">稽核也具備下列功能：</span><span class="sxs-lookup"><span data-stu-id="f7c9e-105">Auditing also:</span></span>

* <span data-ttu-id="f7c9e-106">協助您保持法規遵循、了解資料庫活動，以及深入了解可指出商務考量或疑似安全違規的不一致和異常。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-106">Helps you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

* <span data-ttu-id="f7c9e-107">啟用，並有助於遵循 toocompliance 標準，雖然它不能保證相容性。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-107">Enables and facilitates adherence toocompliance standards, although it doesn't guarantee compliance.</span></span> <span data-ttu-id="f7c9e-108">如需有關 Azure 程式該支援標準相容性，請參閱 < hello [Azure 信任中心](https://azure.microsoft.com/support/trust-center/compliance/)。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-108">For more information about Azure programs that support standards compliance, see hello [Azure Trust Center](https://azure.microsoft.com/support/trust-center/compliance/).</span></span>


## <span data-ttu-id="f7c9e-109"><a id="subheading-1"></a>Azure SQL 資料庫稽核概觀</span><span class="sxs-lookup"><span data-stu-id="f7c9e-109"><a id="subheading-1"></a>Azure SQL database auditing overview</span></span>
<span data-ttu-id="f7c9e-110">您可以使用 SQL 資料庫稽核完成下列工作：</span><span class="sxs-lookup"><span data-stu-id="f7c9e-110">You can use SQL database auditing to:</span></span>


* <span data-ttu-id="f7c9e-111">**保留** 所選事件的稽核記錄。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-111">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="f7c9e-112">您可以定義資料庫動作 toobe 稽核的類別。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-112">You can define categories of database actions toobe audited.</span></span>
* <span data-ttu-id="f7c9e-113">**報告** 資料庫活動。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-113">**Report** on database activity.</span></span> <span data-ttu-id="f7c9e-114">您可以使用預先設定的報表和儀表板 tooget 快速地開始使用活動和事件報告。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-114">You can use preconfigured reports and a dashboard tooget started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="f7c9e-115">**分析** 報告。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-115">**Analyze** reports.</span></span> <span data-ttu-id="f7c9e-116">您可以尋找可疑事件、異常活動及趨勢。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-116">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="f7c9e-117">您可以設定不同類型的事件類別目錄中，稽核 hello 中所述[為您的資料庫設定稽核](#subheading-2)> 一節。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-117">You can configure auditing for different types of event categories, as explained in hello [Set up auditing for your database](#subheading-2) section.</span></span>

<span data-ttu-id="f7c9e-118">稽核記錄檔會寫入 tooAzure Blob 儲存體，在您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-118">Audit logs are written tooAzure Blob storage on your Azure subscription.</span></span>


## <span data-ttu-id="f7c9e-119"><a id="subheading-8"></a>定義伺服器層級與資料庫層級的稽核原則</span><span class="sxs-lookup"><span data-stu-id="f7c9e-119"><a id="subheading-8"></a>Define server-level vs. database-level auditing policy</span></span>

<span data-ttu-id="f7c9e-120">您可以針對特定資料庫定義稽核原則，或將稽核原則定義為預設伺服器原則：</span><span class="sxs-lookup"><span data-stu-id="f7c9e-120">An auditing policy can be defined for a specific database or as a default server policy:</span></span>

* <span data-ttu-id="f7c9e-121">伺服器原則 hello 伺服器上，套用 tooall 現有和新建立的資料庫。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-121">A server policy applies tooall existing and newly created databases on hello server.</span></span>

* <span data-ttu-id="f7c9e-122">如果*server blob 稽核已啟用*，它*一律套用 toohello 資料庫*（也就是 hello 資料庫會稽核），不論 hello 資料庫稽核設定。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-122">If *server blob auditing is enabled*, it *always applies toohello database* (that is, hello database will be audited), regardless of hello database auditing settings.</span></span>

* <span data-ttu-id="f7c9e-123">啟用稽核 hello 在資料庫上，在加法 tooenabling 它 hello 伺服器上的 blob 將*不*覆寫或變更的任何 hello hello server blob 稽核設定。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-123">Enabling blob auditing on hello database, in addition tooenabling it on hello server, will *not* override or change any of hello settings of hello server blob auditing.</span></span> <span data-ttu-id="f7c9e-124">這兩種稽核將會並存。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-124">Both audits will exist side by side.</span></span> <span data-ttu-id="f7c9e-125">換句話說，hello 資料庫將稽核兩次以平行方式 （一次由 hello 伺服器原則和一次程式 hello 資料庫原則）。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-125">In other words, hello database will be audited twice in parallel (once by hello server policy and once by hello database policy).</span></span>

   > [!NOTE]
   > <span data-ttu-id="f7c9e-126">您應該避免同時啟用伺服器 Blob 稽核與資料庫 Blob 稽核，除非：</span><span class="sxs-lookup"><span data-stu-id="f7c9e-126">You should avoid enabling both server blob auditing and database blob auditing together, unless:</span></span>
    > * <span data-ttu-id="f7c9e-127">您想要不同的 toouse*儲存體帳戶*或*保留期限*特定資料庫。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-127">You want toouse a different *storage account* or *retention period* for a specific database.</span></span>
    > * <span data-ttu-id="f7c9e-128">您想要 tooaudit 事件類型或分類的不同事件類型的特定資料庫或稽核 hello 伺服器上的資料庫 hello hello 其餘的類別。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-128">You want tooaudit event types or categories for a specific database that differ from event types or categories that are being audited for hello rest of hello databases on hello server.</span></span> <span data-ttu-id="f7c9e-129">例如，您可能需要稽核 toobe 只針對特定資料庫的資料表插入。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-129">For example, you might have table inserts that need toobe audited only for a specific database.</span></span>
   > 
   > <span data-ttu-id="f7c9e-130">否則，我們建議您啟用只有伺服器層級 blob 稽核和保持 hello 資料庫層級的稽核所有資料庫停都用。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-130">Otherwise, we recommended that you enable only server-level blob auditing and leave hello database-level auditing disabled for all databases.</span></span>


## <span data-ttu-id="f7c9e-131"><a id="subheading-2"></a>設定資料庫的稽核</span><span class="sxs-lookup"><span data-stu-id="f7c9e-131"><a id="subheading-2"></a>Set up auditing for your database</span></span>
<span data-ttu-id="f7c9e-132">hello 下一節描述 hello 的稽核，以使用 hello Azure 入口網站的組態。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-132">hello following section describes hello configuration of auditing using hello Azure portal.</span></span>

1. <span data-ttu-id="f7c9e-133">移 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-133">Go toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f7c9e-134">移 toohello**設定**刀鋒視窗中的 hello 想 tooaudit SQL 資料庫/SQL server。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-134">Go toohello **Settings** blade of hello SQL database/SQL server you want tooaudit.</span></span> <span data-ttu-id="f7c9e-135">在 hello**設定**刀鋒視窗中，選取**稽核與威脅偵測**。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-135">In hello **Settings** blade, select **Auditing & Threat detection**.</span></span>

    <span data-ttu-id="f7c9e-136"><a id="auditing-screenshot"></a> ![導覽窗格][1]</span><span class="sxs-lookup"><span data-stu-id="f7c9e-136"><a id="auditing-screenshot"></a> ![Navigation pane][1]</span></span>
3. <span data-ttu-id="f7c9e-137">如果您偏好 tooset 註冊的伺服器稽核原則 （將此伺服器套用 tooall 現有和新建立的資料庫），您可以選取 hello**檢視伺服器設定**hello 資料庫稽核刀鋒視窗中的連結。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-137">If you prefer tooset up a server auditing policy (which will apply tooall existing and newly created databases on this server), you can select hello **View server settings** link in hello database auditing blade.</span></span> <span data-ttu-id="f7c9e-138">您可以接著檢視或修改 hello 伺服器稽核設定。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-138">You can then view or modify hello server auditing settings.</span></span>

    ![瀏覽窗格][2]
4. <span data-ttu-id="f7c9e-140">如果您想 tooenable hello 資料庫層級 （加法 tooor 而不是伺服器層級的稽核)，稽核 blob**稽核**，選取**ON**，以及**稽核類型**選取**Blob**。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-140">If you prefer tooenable blob auditing on hello database level (in addition tooor instead of server-level auditing), for **Auditing**, select **ON**, and for **Auditing type**, select  **Blob**.</span></span>

    <span data-ttu-id="f7c9e-141">如果伺服器 blob 稽核已啟用，就會並存 hello 伺服器 blob 稽核存在 hello 資料庫設定稽核。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-141">If server blob auditing is enabled, hello database-configured audit will exist side by side with hello server blob audit.</span></span>  

    ![瀏覽窗格][3]
5. <span data-ttu-id="f7c9e-143">tooopen hello**稽核記錄檔儲存體**刀鋒視窗中，選取**儲存詳細資料**。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-143">tooopen hello **Audit Logs Storage** blade, select **Storage Details**.</span></span> <span data-ttu-id="f7c9e-144">選取記錄檔將儲存的位置，，然後選取 hello 保留期限，將會刪除舊的記錄檔之後的 hello hello Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-144">Select hello Azure storage account where logs will be saved, and then select hello retention period, after which hello old logs will be deleted.</span></span> <span data-ttu-id="f7c9e-145">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-145">Then click **OK**.</span></span> 
   >[!TIP] 
   ><span data-ttu-id="f7c9e-146">充分利用 hello 的稽核報表範本，而使用 tooget hello hello 所有稽核資料庫的相同儲存體的帳戶。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-146">tooget hello most out of hello auditing reports templates, use hello same storage account for all audited databases.</span></span> 

    <span data-ttu-id="f7c9e-147"><a id="storage-screenshot"></a> ![導覽窗格][4]</span><span class="sxs-lookup"><span data-stu-id="f7c9e-147"><a id="storage-screenshot"></a> ![Navigation pane][4]</span></span>
6. <span data-ttu-id="f7c9e-148">如果您想 toocustomize hello 稽核事件，您可以透過 PowerShell 執行這項操作，或 hello REST API。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-148">If you want toocustomize hello audited events, you can do this via PowerShell or hello REST API.</span></span> <span data-ttu-id="f7c9e-149">如需詳細資訊，請參閱 hello[自動化 (PowerShell/REST API)](#subheading-7) > 一節。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-149">For more details, see hello [Automation (PowerShell/REST API)](#subheading-7) section.</span></span>
7. <span data-ttu-id="f7c9e-150">設定您的稽核設定之後，您可以開啟 hello 新威脅偵測功能，並設定電子郵件 tooreceive 安全性警示。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-150">After you've configured your auditing settings, you can turn on hello new threat detection feature and configure emails tooreceive security alerts.</span></span> <span data-ttu-id="f7c9e-151">使用威脅偵測時，您會接收與指示潛在安全性威脅的異常資料庫活動相關的主動式警示。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-151">When you use threat detection, you receive proactive alerts on anomalous database activities that can indicate potential security threats.</span></span> <span data-ttu-id="f7c9e-152">如需詳細資訊，請參閱[開始使用威脅偵測](sql-database-threat-detection-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-152">For more details, see [Getting started with threat detection](sql-database-threat-detection-get-started.md).</span></span>
8. <span data-ttu-id="f7c9e-153">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-153">Click **Save**.</span></span>





## <span data-ttu-id="f7c9e-154"><a id="subheading-3"></a>分析稽核記錄和報告</span><span class="sxs-lookup"><span data-stu-id="f7c9e-154"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="f7c9e-155">稽核記錄檔會彙總 hello 您在安裝期間所選擇的 Azure 儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-155">Audit logs are aggregated in hello Azure storage account you chose during setup.</span></span> <span data-ttu-id="f7c9e-156">您可以使用工具 (例如 [Azure 儲存體總管](http://storageexplorer.com/)) 來查看稽核記錄。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-156">You can explore audit logs by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="f7c9e-157">Blob 稽核記錄是以 Blob 檔案集合的方式儲存在名為 **sqldbauditlogs** 的容器內。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-157">Blob auditing logs are saved as a collection of blob files within a container named **sqldbauditlogs**.</span></span>

<span data-ttu-id="f7c9e-158">如需 hello 階層 hello blob 稽核記錄檔儲存體資料夾及 blob 的命名慣例，記錄檔格式的進一步詳細資訊，請參閱 hello [Blob 稽核記錄檔格式參考 （.docx 檔案下載）](https://go.microsoft.com/fwlink/?linkid=829599)。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-158">For further details about hello hierarchy of hello blob audit logs storage folder, blob naming conventions, and log format, see hello [Blob Audit Log Format Reference (.docx file download)](https://go.microsoft.com/fwlink/?linkid=829599).</span></span>

<span data-ttu-id="f7c9e-159">有數種方法，您可以使用稽核記錄的 tooview blob:</span><span class="sxs-lookup"><span data-stu-id="f7c9e-159">There are several methods you can use tooview blob auditing logs:</span></span>

* <span data-ttu-id="f7c9e-160">使用 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-160">Use hello [Azure portal](https://portal.azure.com).</span></span>  <span data-ttu-id="f7c9e-161">開啟 hello 相關資料庫。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-161">Open hello relevant database.</span></span> <span data-ttu-id="f7c9e-162">在 hello 頂端 hello 資料庫**稽核與威脅偵測**刀鋒視窗中，按一下 **檢視稽核記錄檔**。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-162">At hello top of hello database's **Auditing & Threat detection** blade, click **View audit logs**.</span></span>

    ![瀏覽窗格][7]

    <span data-ttu-id="f7c9e-164">**稽核記錄**刀鋒視窗隨即開啟，從中您應該能夠 tooview hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-164">An **Audit records** blade opens, from which you'll be able tooview hello logs.</span></span>

    - <span data-ttu-id="f7c9e-165">按一下即可檢視特定日期**篩選**頂端的 hello hello**稽核記錄**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-165">You can view specific dates by clicking **Filter** at hello top of hello **Audit records** blade.</span></span>
    - <span data-ttu-id="f7c9e-166">您可以在由伺服器原則或資料庫原則稽核建立的稽核記錄之間切換。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-166">You can switch between audit records that were created by a server policy or database policy audit.</span></span>

       ![瀏覽窗格][8]

* <span data-ttu-id="f7c9e-168">使用 hello 系統函數**sys.fn_get_audit_file** (T-SQL) tooreturn hello 稽核記錄檔中的資料表格格式。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-168">Use hello system function **sys.fn_get_audit_file** (T-SQL) tooreturn hello audit log data in tabular format.</span></span> <span data-ttu-id="f7c9e-169">如需有關如何使用這個函式的詳細資訊，請參閱 hello [sys.fn_get_audit_file 文件](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql)。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-169">For more information on using this function, see hello [sys.fn_get_audit_file documentation](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span></span>


* <span data-ttu-id="f7c9e-170">使用 SQL Server Management Studio (SSMS 17 或更新版本) 中的 [合併稽核檔案]：</span><span class="sxs-lookup"><span data-stu-id="f7c9e-170">Use **Merge Audit Files** in SQL Server Management Studio (starting with SSMS 17):</span></span>  
    1. <span data-ttu-id="f7c9e-171">從 hello SSMS 功能表上，選取**檔案** > **開啟** > **合併稽核檔案**。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-171">From hello SSMS menu, select **File** > **Open** > **Merge Audit Files**.</span></span>

        ![瀏覽窗格][9]
    2. <span data-ttu-id="f7c9e-173">hello**加入稽核檔案**對話方塊隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-173">hello **Add Audit Files** dialog box opens.</span></span> <span data-ttu-id="f7c9e-174">選取其中一個 hello**新增**選項可以選擇是否 toomerge 稽核檔案從本機磁碟，或從 Azure 儲存體匯入 (您將需要的 tooprovide，您的 Azure 儲存體的詳細資訊和帳戶金鑰)。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-174">Select one of hello **Add** options to choose whether toomerge audit files from a local disk or import them from Azure Storage (you will be required tooprovide your Azure Storage details and account key).</span></span>

    3. <span data-ttu-id="f7c9e-175">已新增所有的檔案 toomerge 之後，請按一下**確定**toocomplete hello 合併作業。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-175">After all files toomerge have been added, click **OK** toocomplete hello merge operation.</span></span>

    4. <span data-ttu-id="f7c9e-176">在 SSMS 中，您可以在其中檢視和分析，以及匯出它 tooan XEL 或 CSV 檔案或 tooa 資料表中，開啟 hello 合併的檔案。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-176">hello merged file opens in SSMS, where you can view and analyze it, as well as export it tooan XEL or CSV file or tooa table.</span></span>

* <span data-ttu-id="f7c9e-177">使用 hello[同步應用程式](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration)，我們建立了。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-177">Use hello [sync application](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) that we have created.</span></span> <span data-ttu-id="f7c9e-178">它會在 Azure 中執行，並且利用到 OMS 的 Operations Management Suite (OMS) 的記錄分析公用 Api toopush SQL 稽核記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-178">It runs in Azure and utilizes Operations Management Suite (OMS) Log Analytics public APIs toopush SQL audit logs into OMS.</span></span> <span data-ttu-id="f7c9e-179">hello 同步處理應用程式將發送 SQL 稽核記錄檔至 OMS 記錄分析取用透過 hello OMS 記錄分析儀表板。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-179">hello sync application pushes SQL audit logs into OMS Log Analytics for consumption via hello OMS Log Analytics dashboard.</span></span> 

* <span data-ttu-id="f7c9e-180">使用 Power BI。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-180">Use Power BI.</span></span> <span data-ttu-id="f7c9e-181">您可以在 Power BI 中檢視和分析稽核記錄資料。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-181">You can view and analyze audit log data in Power BI.</span></span> <span data-ttu-id="f7c9e-182">深入了解 [Power BI，並存取可下載的範本](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/)。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-182">Learn more about [Power BI, and access a downloadable template](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span></span>

* <span data-ttu-id="f7c9e-183">下載記錄檔從您的 Azure 儲存體 blob 容器透過 hello 入口網站，或使用一種工具，像是[Azure 儲存體總管](http://storageexplorer.com/)。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-183">Download log files from your Azure Storage blob container via hello portal or by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
    * <span data-ttu-id="f7c9e-184">您已下載記錄檔在本機上之後，您可以按兩下 hello 檔案 tooopen，檢視及分析在 SSMS 中的 hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-184">After you have downloaded a log file locally, you can double-click hello file tooopen, view, and analyze hello logs in SSMS.</span></span>
    * <span data-ttu-id="f7c9e-185">您也可以透過 Azure 儲存體總管同時下載多個檔案。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-185">You can also download multiple files simultaneously via Azure Storage Explorer.</span></span> <span data-ttu-id="f7c9e-186">以滑鼠右鍵按一下特定的子資料夾 （例如，子資料夾中包含特定日期的所有記錄檔），然後選取**存**toosave 本機資料夾中的。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-186">Right-click a specific subfolder (for example, a subfolder that includes all log files for a specific date) and select **Save as** toosave in a local folder.</span></span>

* <span data-ttu-id="f7c9e-187">其他方法：</span><span class="sxs-lookup"><span data-stu-id="f7c9e-187">Additional methods:</span></span>
   * <span data-ttu-id="f7c9e-188">下載多個檔案 （或子資料夾，以記錄檔包含一整天，這份清單中的 hello 上一個項目中所述） 之後, 您可以合併它們在本機中稍早所述的 hello SSMS 合併稽核檔案指示所述。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-188">After downloading several files (or a subfolder that includes log files for an entire day, as described in hello previous item in this list), you can merge them locally as described in hello SSMS Merge Audit Files instructions described earlier.</span></span>

   * <span data-ttu-id="f7c9e-189">以程式設計方式檢視 Blob 稽核記錄：</span><span class="sxs-lookup"><span data-stu-id="f7c9e-189">View blob auditing logs programmatically:</span></span>

     * <span data-ttu-id="f7c9e-190">使用 hello[擴充事件讀取器](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/)C# 程式庫。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-190">Use hello [Extended Events Reader](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) C# library.</span></span>
     * <span data-ttu-id="f7c9e-191">使用 PowerShell [查詢擴充事件檔案](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/)。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-191">[Query Extended Events Files](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) by using PowerShell.</span></span>




## <span data-ttu-id="f7c9e-192"><a id="subheading-5"></a>實際作法</span><span class="sxs-lookup"><span data-stu-id="f7c9e-192"><a id="subheading-5"></a>Production practices</span></span>
<!--hello description in this section refers toopreceding screen captures.-->

### <span data-ttu-id="f7c9e-193"><a id="subheading-6">稽核異地複寫資料庫</a></span><span class="sxs-lookup"><span data-stu-id="f7c9e-193"><a id="subheading-6">Auditing geo-replicated databases</a></span></span>
<span data-ttu-id="f7c9e-194">當您使用地理複寫的資料庫時，很可能 tooset 向上 hello 主要資料庫、 hello 次要資料庫，或兩者，根據 hello 稽核類型上的稽核。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-194">When you use geo-replicated databases, it is possible tooset up auditing on either hello primary database, hello secondary database, or both, depending on hello audit type.</span></span>

<span data-ttu-id="f7c9e-195">請遵循這些指示 （請記住，blob 稽核可以開啟或關閉只能從 hello 主要資料庫稽核設定）：</span><span class="sxs-lookup"><span data-stu-id="f7c9e-195">Follow these instructions (remember that blob auditing can be turned on or off only from hello primary database auditing settings):</span></span>

* <span data-ttu-id="f7c9e-196">**主要資料庫**。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-196">**Primary database**.</span></span> <span data-ttu-id="f7c9e-197">開啟 blob 稽核 hello 伺服器上或在 hello 資料庫本身，hello 中所述[為您的資料庫設定稽核](#subheading-2)> 一節。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-197">Turn on blob auditing, either on hello server or on hello database itself, as described in hello [Set up auditing for your database](#subheading-2) section.</span></span>
* <span data-ttu-id="f7c9e-198">**次要資料庫**。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-198">**Secondary database**.</span></span> <span data-ttu-id="f7c9e-199">Blob 上開啟稽核 hello 主要資料庫，hello 中所述[為您的資料庫設定稽核](#subheading-2)> 一節。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-199">Turn on blob auditing on hello primary database, as described in hello [Set up auditing for your database](#subheading-2) section.</span></span> 
   * <span data-ttu-id="f7c9e-200">Blob 稽核上必須啟用 hello*主要資料庫本身*，非 hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-200">Blob auditing must be enabled on hello *primary database itself*, not hello server.</span></span>
   * <span data-ttu-id="f7c9e-201">Blob 稽核 hello 主要資料庫上啟用之後，它也會變成 hello 次要資料庫上啟用。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-201">After blob auditing is enabled on hello primary database, it will also become enabled on hello secondary database.</span></span>

     >[!IMPORTANT]
     ><span data-ttu-id="f7c9e-202">根據預設，hello 儲存體 hello 次要資料庫會設定相同的 hello 主要資料庫，toothose 導致跨地區的流量。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-202">By default, hello storage settings for hello secondary database will be identical toothose of hello primary database, causing cross-regional traffic.</span></span> <span data-ttu-id="f7c9e-203">您可以避免這個狀況啟用稽核 hello 次要伺服器上的 blob 和 hello 次要伺服器儲存體設定中設定本機儲存體。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-203">You can avoid this by enabling blob auditing on hello secondary server and configuring local storage in hello secondary server storage settings.</span></span> <span data-ttu-id="f7c9e-204">這會覆寫 hello hello 次要資料庫並儲存其稽核記錄檔 toolocal 儲存體的每個資料庫中的結果的儲存位置。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-204">This will override hello storage location for hello secondary database and result in each database saving its audit logs toolocal storage.</span></span>  
<br>

### <span data-ttu-id="f7c9e-205"><a id="subheading-6">儲存體金鑰重新產生</a></span><span class="sxs-lookup"><span data-stu-id="f7c9e-205"><a id="subheading-6">Storage key regeneration</a></span></span>
<span data-ttu-id="f7c9e-206">實際執行環境，您就有可能您的儲存體金鑰定期的 toorefresh。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-206">In production, you are likely toorefresh your storage keys periodically.</span></span> <span data-ttu-id="f7c9e-207">當重新整理您的金鑰，您會需要 tooresave hello 稽核原則。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-207">When refreshing your keys, you need tooresave hello auditing policy.</span></span> <span data-ttu-id="f7c9e-208">hello 程序如下所示：</span><span class="sxs-lookup"><span data-stu-id="f7c9e-208">hello process is as follows:</span></span>

1. <span data-ttu-id="f7c9e-209">開啟 hello**儲存詳細資料**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-209">Open hello **Storage Details** blade.</span></span> <span data-ttu-id="f7c9e-210">在 hello**儲存體存取金鑰**方塊中，選取**次要**，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-210">In hello **Storage Access Key** box, select **Secondary**, and click **OK**.</span></span> <span data-ttu-id="f7c9e-211">然後按一下 **儲存**在 hello hello 稽核組態刀鋒視窗最上方。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-211">Then click **Save** at hello top of hello auditing configuration blade.</span></span>

    ![瀏覽窗格][5]
2. <span data-ttu-id="f7c9e-213">請 toohello 存放裝置設定 刀鋒視窗，並重新產生 hello 主要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-213">Go toohello storage configuration blade and regenerate hello primary access key.</span></span>

    ![瀏覽窗格][6]
3. <span data-ttu-id="f7c9e-215">返回 toohello 稽核組態刀鋒視窗中，切換 hello 儲存體存取金鑰，從次要 tooprimary，，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-215">Go back toohello auditing configuration blade, switch hello storage access key from secondary tooprimary, and then click **OK**.</span></span> <span data-ttu-id="f7c9e-216">然後按一下 **儲存**在 hello hello 稽核組態刀鋒視窗最上方。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-216">Then click **Save** at hello top of hello auditing configuration blade.</span></span>
4. <span data-ttu-id="f7c9e-217">返回 toohello 儲存體組態刀鋒視窗，然後重新產生 hello 次要存取金鑰 （在準備 hello 下一個索引鍵的重新整理循環）。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-217">Go back toohello storage configuration blade and regenerate hello secondary access key (in preparation for hello next key's refresh cycle).</span></span>

## <span data-ttu-id="f7c9e-218"><a id="subheading-7"></a>自動化 (PowerShell/REST API)</span><span class="sxs-lookup"><span data-stu-id="f7c9e-218"><a id="subheading-7"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="f7c9e-219">您也可以設定稽核 Azure SQL Database 中使用下列的自動化工具 hello:</span><span class="sxs-lookup"><span data-stu-id="f7c9e-219">You can also configure auditing in Azure SQL Database by using hello following automation tools:</span></span>

* <span data-ttu-id="f7c9e-220">**PowerShell Cmdlet**：</span><span class="sxs-lookup"><span data-stu-id="f7c9e-220">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="f7c9e-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="f7c9e-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="f7c9e-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="f7c9e-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="f7c9e-223">[Remove-AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="f7c9e-223">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="f7c9e-224">[Remove-AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="f7c9e-224">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="f7c9e-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="f7c9e-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="f7c9e-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="f7c9e-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="f7c9e-227">[Use-AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="f7c9e-227">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

   <span data-ttu-id="f7c9e-228">如需指令碼範例，請參閱[使用 PowerShell 設定稽核與威脅偵測](scripts/sql-database-auditing-and-threat-detection-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="f7c9e-228">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

* <span data-ttu-id="f7c9e-229">**REST API - Blob 稽核**：</span><span class="sxs-lookup"><span data-stu-id="f7c9e-229">**REST API - Blob auditing**:</span></span>

   * [<span data-ttu-id="f7c9e-230">建立或更新資料庫 Blob 稽核原則</span><span class="sxs-lookup"><span data-stu-id="f7c9e-230">Create or Update Database Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt695939.aspx)
   * [<span data-ttu-id="f7c9e-231">建立或更新伺服器 Blob 稽核原則</span><span class="sxs-lookup"><span data-stu-id="f7c9e-231">Create or Update Server Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt771861.aspx)
   * [<span data-ttu-id="f7c9e-232">取得資料庫 Blob 稽核原則</span><span class="sxs-lookup"><span data-stu-id="f7c9e-232">Get Database Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt695938.aspx)
   * [<span data-ttu-id="f7c9e-233">取得伺服器 Blob 稽核原則</span><span class="sxs-lookup"><span data-stu-id="f7c9e-233">Get Server Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt771860.aspx)
   * [<span data-ttu-id="f7c9e-234">取得伺服器 Blob 稽核操作結果</span><span class="sxs-lookup"><span data-stu-id="f7c9e-234">Get Server Blob Auditing Operation Result</span></span>](https://msdn.microsoft.com/library/azure/mt771862.aspx)


<!--Anchors-->
[Azure SQL Database Auditing overview]: #subheading-1
[Set up auditing for your database]: #subheading-2
[Analyze audit logs and reports]: #subheading-3
[Practices for usage in production]: #subheading-5
[Storage Key Regeneration]: #subheading-6
[Automation (PowerShell / REST API)]: #subheading-7
[Blob/Table differences in Server auditing policy inheritance]: (#subheading-8)  

<!--Image references-->
[1]: ./media/sql-database-auditing-get-started/1_auditing_get_started_settings.png
[2]: ./media/sql-database-auditing-get-started/2_auditing_get_started_server_inherit.png
[3]: ./media/sql-database-auditing-get-started/3_auditing_get_started_turn_on.png
[4]: ./media/sql-database-auditing-get-started/4_auditing_get_started_storage_details.png
[5]: ./media/sql-database-auditing-get-started/5_auditing_get_started_storage_key_regeneration.png
[6]: ./media/sql-database-auditing-get-started/6_auditing_get_started_regenerate_key.png
[7]: ./media/sql-database-auditing-get-started/7_auditing_get_started_blob_view_audit_logs.png
[8]: ./media/sql-database-auditing-get-started/8_auditing_get_started_blob_audit_records.png
[9]: ./media/sql-database-auditing-get-started/9_auditing_get_started_ssms_1.png
[10]: ./media/sql-database-auditing-get-started/10_auditing_get_started_ssms_2.png

[101]: /powershell/module/azurerm.sql/get-azurermsqldatabaseauditingpolicy
[102]: /powershell/module/azurerm.sql/Get-AzureRMSqlServerAuditingPolicy
[103]: /powershell/module/azurerm.sql/Remove-AzureRMSqlDatabaseAuditing
[104]: /powershell/module/azurerm.sql/Remove-AzureRMSqlServerAuditing
[105]: /powershell/module/azurerm.sql/Set-AzureRMSqlDatabaseAuditingPolicy
[106]: /powershell/module/azurerm.sql/Set-AzureRMSqlServerAuditingPolicy
[107]: /powershell/module/azurerm.sql/Use-AzureRMSqlServerAuditingPolicy
