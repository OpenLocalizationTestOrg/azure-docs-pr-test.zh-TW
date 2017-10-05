---
title: "開始使用 Azure SQL 資料庫稽核 | Microsoft Docs"
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
ms.openlocfilehash: f4324a59b5fa4c2e1ab5b1d7fc7e5fe986ea80f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-sql-database-auditing"></a><span data-ttu-id="c1243-103">開始使用 SQL Database 稽核</span><span class="sxs-lookup"><span data-stu-id="c1243-103">Get started with SQL database auditing</span></span>
<span data-ttu-id="c1243-104">Azure SQL 資料庫稽核會追蹤資料庫事件，並將事件寫入您 Azure 儲存體帳戶中的稽核記錄。</span><span class="sxs-lookup"><span data-stu-id="c1243-104">Azure SQL database auditing tracks database events and writes them to an audit log in your Azure storage account.</span></span> <span data-ttu-id="c1243-105">稽核也具備下列功能：</span><span class="sxs-lookup"><span data-stu-id="c1243-105">Auditing also:</span></span>

* <span data-ttu-id="c1243-106">協助您保持法規遵循、了解資料庫活動，以及深入了解可指出商務考量或疑似安全違規的不一致和異常。</span><span class="sxs-lookup"><span data-stu-id="c1243-106">Helps you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

* <span data-ttu-id="c1243-107">啟用及推動遵循法規標準，但不保證符合法規。</span><span class="sxs-lookup"><span data-stu-id="c1243-107">Enables and facilitates adherence to compliance standards, although it doesn't guarantee compliance.</span></span> <span data-ttu-id="c1243-108">如需有關支援標準法規的 Azure 程式詳細資訊，請參閱 [Azure 信任中心](https://azure.microsoft.com/support/trust-center/compliance/)。</span><span class="sxs-lookup"><span data-stu-id="c1243-108">For more information about Azure programs that support standards compliance, see the [Azure Trust Center](https://azure.microsoft.com/support/trust-center/compliance/).</span></span>


## <span data-ttu-id="c1243-109"><a id="subheading-1"></a>Azure SQL 資料庫稽核概觀</span><span class="sxs-lookup"><span data-stu-id="c1243-109"><a id="subheading-1"></a>Azure SQL database auditing overview</span></span>
<span data-ttu-id="c1243-110">您可以使用 SQL 資料庫稽核完成下列工作：</span><span class="sxs-lookup"><span data-stu-id="c1243-110">You can use SQL database auditing to:</span></span>


* <span data-ttu-id="c1243-111">**保留** 所選事件的稽核記錄。</span><span class="sxs-lookup"><span data-stu-id="c1243-111">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="c1243-112">您可以定義要稽核的資料庫動作類別。</span><span class="sxs-lookup"><span data-stu-id="c1243-112">You can define categories of database actions to be audited.</span></span>
* <span data-ttu-id="c1243-113">**報告** 資料庫活動。</span><span class="sxs-lookup"><span data-stu-id="c1243-113">**Report** on database activity.</span></span> <span data-ttu-id="c1243-114">您可以使用預先設定的報告和儀表板，以便快速開始使用活動和事件報告。</span><span class="sxs-lookup"><span data-stu-id="c1243-114">You can use preconfigured reports and a dashboard to get started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="c1243-115">**分析** 報告。</span><span class="sxs-lookup"><span data-stu-id="c1243-115">**Analyze** reports.</span></span> <span data-ttu-id="c1243-116">您可以尋找可疑事件、異常活動及趨勢。</span><span class="sxs-lookup"><span data-stu-id="c1243-116">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="c1243-117">您可以依照[設定資料庫的稽核](#subheading-2)一節中的說明，針對不同類型的事件類別設定稽核。</span><span class="sxs-lookup"><span data-stu-id="c1243-117">You can configure auditing for different types of event categories, as explained in the [Set up auditing for your database](#subheading-2) section.</span></span>

<span data-ttu-id="c1243-118">系統會將稽核記錄檔寫入 Azure 訂用帳戶的 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="c1243-118">Audit logs are written to Azure Blob storage on your Azure subscription.</span></span>


## <span data-ttu-id="c1243-119"><a id="subheading-8"></a>定義伺服器層級與資料庫層級的稽核原則</span><span class="sxs-lookup"><span data-stu-id="c1243-119"><a id="subheading-8"></a>Define server-level vs. database-level auditing policy</span></span>

<span data-ttu-id="c1243-120">您可以針對特定資料庫定義稽核原則，或將稽核原則定義為預設伺服器原則：</span><span class="sxs-lookup"><span data-stu-id="c1243-120">An auditing policy can be defined for a specific database or as a default server policy:</span></span>

* <span data-ttu-id="c1243-121">伺服器原則會套用至伺服器上所有現有和新建立的資料庫。</span><span class="sxs-lookup"><span data-stu-id="c1243-121">A server policy applies to all existing and newly created databases on the server.</span></span>

* <span data-ttu-id="c1243-122">如果伺服器 Blob 稽核已啟用，它一律會套用到資料庫 (也就是將會稽核資料庫)，不論資料庫稽核設定為何。</span><span class="sxs-lookup"><span data-stu-id="c1243-122">If *server blob auditing is enabled*, it *always applies to the database* (that is, the database will be audited), regardless of the database auditing settings.</span></span>

* <span data-ttu-id="c1243-123">如果在伺服器和資料庫上都啟用 Blob 稽核，這將「不會」覆寫或變更伺服器 Blob 稽核的任何設定。</span><span class="sxs-lookup"><span data-stu-id="c1243-123">Enabling blob auditing on the database, in addition to enabling it on the server, will *not* override or change any of the settings of the server blob auditing.</span></span> <span data-ttu-id="c1243-124">這兩種稽核將會並存。</span><span class="sxs-lookup"><span data-stu-id="c1243-124">Both audits will exist side by side.</span></span> <span data-ttu-id="c1243-125">換句話說，系統將會對資料庫進行兩次相同的稽核 (一次是由伺服器原則，一次是由資料庫原則)。</span><span class="sxs-lookup"><span data-stu-id="c1243-125">In other words, the database will be audited twice in parallel (once by the server policy and once by the database policy).</span></span>

   > [!NOTE]
   > <span data-ttu-id="c1243-126">您應該避免同時啟用伺服器 Blob 稽核與資料庫 Blob 稽核，除非：</span><span class="sxs-lookup"><span data-stu-id="c1243-126">You should avoid enabling both server blob auditing and database blob auditing together, unless:</span></span>
    > * <span data-ttu-id="c1243-127">您需要為特定資料庫使用不同的儲存體帳戶或保留期間。</span><span class="sxs-lookup"><span data-stu-id="c1243-127">You want to use a different *storage account* or *retention period* for a specific database.</span></span>
    > * <span data-ttu-id="c1243-128">您想要針對特定資料庫稽核不同於伺服器上其餘資料庫所稽核的事件類型或類別。</span><span class="sxs-lookup"><span data-stu-id="c1243-128">You want to audit event types or categories for a specific database that differ from event types or categories that are being audited for the rest of the databases on the server.</span></span> <span data-ttu-id="c1243-129">例如，您可能只需要針對特定資料庫稽核資料表插入。</span><span class="sxs-lookup"><span data-stu-id="c1243-129">For example, you might have table inserts that need to be audited only for a specific database.</span></span>
   > 
   > <span data-ttu-id="c1243-130">否則，建議只啟用伺服器層級 Blob 稽核，並讓所有資料庫的資料庫層級稽核保留在停用狀態。</span><span class="sxs-lookup"><span data-stu-id="c1243-130">Otherwise, we recommended that you enable only server-level blob auditing and leave the database-level auditing disabled for all databases.</span></span>


## <span data-ttu-id="c1243-131"><a id="subheading-2"></a>設定資料庫的稽核</span><span class="sxs-lookup"><span data-stu-id="c1243-131"><a id="subheading-2"></a>Set up auditing for your database</span></span>
<span data-ttu-id="c1243-132">下節描述使用 Azure 入口網站進行稽核的設定。</span><span class="sxs-lookup"><span data-stu-id="c1243-132">The following section describes the configuration of auditing using the Azure portal.</span></span>

1. <span data-ttu-id="c1243-133">移至 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="c1243-133">Go to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c1243-134">移至您想要稽核的 SQL 資料庫/SQL 伺服器 [設定] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c1243-134">Go to the **Settings** blade of the SQL database/SQL server you want to audit.</span></span> <span data-ttu-id="c1243-135">在 [設定] 刀鋒視窗中，選取 [稽核與威脅偵測]。</span><span class="sxs-lookup"><span data-stu-id="c1243-135">In the **Settings** blade, select **Auditing & Threat detection**.</span></span>

    <span data-ttu-id="c1243-136"><a id="auditing-screenshot"></a> ![導覽窗格][1]</span><span class="sxs-lookup"><span data-stu-id="c1243-136"><a id="auditing-screenshot"></a> ![Navigation pane][1]</span></span>
3. <span data-ttu-id="c1243-137">如果您想要設定伺服器稽核原則 (其將套用至此伺服器上所有現有和新建立的資料庫)，您可以選取資料庫稽核刀鋒視窗中的 [檢視伺服器設定] 連結。</span><span class="sxs-lookup"><span data-stu-id="c1243-137">If you prefer to set up a server auditing policy (which will apply to all existing and newly created databases on this server), you can select the **View server settings** link in the database auditing blade.</span></span> <span data-ttu-id="c1243-138">然後，您可以檢視或修改伺服器稽核設定。</span><span class="sxs-lookup"><span data-stu-id="c1243-138">You can then view or modify the server auditing settings.</span></span>

    ![導覽窗格][2]
4. <span data-ttu-id="c1243-140">如果您想要啟用資料庫層級的 Blob 稽核 (同時啟用或不啟用伺服器層級的稽核)，請針對 [稽核] 選取 [開啟]，並針對 [稽核類型] 選取 [Blob]。</span><span class="sxs-lookup"><span data-stu-id="c1243-140">If you prefer to enable blob auditing on the database level (in addition to or instead of server-level auditing), for **Auditing**, select **ON**, and for **Auditing type**, select  **Blob**.</span></span>

    <span data-ttu-id="c1243-141">如果已啟用伺服器 Blob 稽核，資料庫設定的稽核將會與伺服器 Blob 稽核並存。</span><span class="sxs-lookup"><span data-stu-id="c1243-141">If server blob auditing is enabled, the database-configured audit will exist side by side with the server blob audit.</span></span>  

    ![導覽窗格][3]
5. <span data-ttu-id="c1243-143">若要開啟 [稽核記錄儲存體] 刀鋒視窗，請選取 [儲存體詳細資料]。</span><span class="sxs-lookup"><span data-stu-id="c1243-143">To open the **Audit Logs Storage** blade, select **Storage Details**.</span></span> <span data-ttu-id="c1243-144">選取將儲存記錄的 Azure 儲存體帳戶，然後選取將舊記錄刪除之前的保留期間。</span><span class="sxs-lookup"><span data-stu-id="c1243-144">Select the Azure storage account where logs will be saved, and then select the retention period, after which the old logs will be deleted.</span></span> <span data-ttu-id="c1243-145">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="c1243-145">Then click **OK**.</span></span> 
   >[!TIP] 
   ><span data-ttu-id="c1243-146">若要充分利用稽核報告範本，請讓所有稽核的資料庫都使用相同的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c1243-146">To get the most out of the auditing reports templates, use the same storage account for all audited databases.</span></span> 

    <span data-ttu-id="c1243-147"><a id="storage-screenshot"></a> ![導覽窗格][4]</span><span class="sxs-lookup"><span data-stu-id="c1243-147"><a id="storage-screenshot"></a> ![Navigation pane][4]</span></span>
6. <span data-ttu-id="c1243-148">如果您想要自訂稽核的事件，您可以透過 PowerShell 或 REST API 來自訂。</span><span class="sxs-lookup"><span data-stu-id="c1243-148">If you want to customize the audited events, you can do this via PowerShell or the REST API.</span></span> <span data-ttu-id="c1243-149">如需詳細資訊，請參閱[自動化 (PowerShell/REST API)](#subheading-7) 一節。</span><span class="sxs-lookup"><span data-stu-id="c1243-149">For more details, see the [Automation (PowerShell/REST API)](#subheading-7) section.</span></span>
7. <span data-ttu-id="c1243-150">設定您的稽核設定之後，您可以開啟新的威脅偵測功能，並設定電子郵件以接收安全性警示。</span><span class="sxs-lookup"><span data-stu-id="c1243-150">After you've configured your auditing settings, you can turn on the new threat detection feature and configure emails to receive security alerts.</span></span> <span data-ttu-id="c1243-151">使用威脅偵測時，您會接收與指示潛在安全性威脅的異常資料庫活動相關的主動式警示。</span><span class="sxs-lookup"><span data-stu-id="c1243-151">When you use threat detection, you receive proactive alerts on anomalous database activities that can indicate potential security threats.</span></span> <span data-ttu-id="c1243-152">如需詳細資訊，請參閱[開始使用威脅偵測](sql-database-threat-detection-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="c1243-152">For more details, see [Getting started with threat detection](sql-database-threat-detection-get-started.md).</span></span>
8. <span data-ttu-id="c1243-153">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="c1243-153">Click **Save**.</span></span>





## <span data-ttu-id="c1243-154"><a id="subheading-3"></a>分析稽核記錄和報告</span><span class="sxs-lookup"><span data-stu-id="c1243-154"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="c1243-155">稽核記錄會在您於安裝期間選擇的 Azure 儲存體帳戶中彙總。</span><span class="sxs-lookup"><span data-stu-id="c1243-155">Audit logs are aggregated in the Azure storage account you chose during setup.</span></span> <span data-ttu-id="c1243-156">您可以使用工具 (例如 [Azure 儲存體總管](http://storageexplorer.com/)) 來查看稽核記錄。</span><span class="sxs-lookup"><span data-stu-id="c1243-156">You can explore audit logs by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="c1243-157">Blob 稽核記錄是以 Blob 檔案集合的方式儲存在名為 **sqldbauditlogs** 的容器內。</span><span class="sxs-lookup"><span data-stu-id="c1243-157">Blob auditing logs are saved as a collection of blob files within a container named **sqldbauditlogs**.</span></span>

<span data-ttu-id="c1243-158">如需有關 Blob 稽核記錄儲存體資料夾階層、Blob 命名慣例和記錄格式的進一步詳細資訊，請參閱 [Blob 稽核記錄格式參考 (.docx 檔案下載)](https://go.microsoft.com/fwlink/?linkid=829599) (英文)。</span><span class="sxs-lookup"><span data-stu-id="c1243-158">For further details about the hierarchy of the blob audit logs storage folder, blob naming conventions, and log format, see the [Blob Audit Log Format Reference (.docx file download)](https://go.microsoft.com/fwlink/?linkid=829599).</span></span>

<span data-ttu-id="c1243-159">有幾種方法可以用於檢視 Blob 稽核記錄：</span><span class="sxs-lookup"><span data-stu-id="c1243-159">There are several methods you can use to view blob auditing logs:</span></span>

* <span data-ttu-id="c1243-160">使用 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="c1243-160">Use the [Azure portal](https://portal.azure.com).</span></span>  <span data-ttu-id="c1243-161">開啟相關的資料庫。</span><span class="sxs-lookup"><span data-stu-id="c1243-161">Open the relevant database.</span></span> <span data-ttu-id="c1243-162">在資料庫的 [稽核與威脅偵測] 刀鋒視窗的頂端，按一下 [檢視稽核記錄]。</span><span class="sxs-lookup"><span data-stu-id="c1243-162">At the top of the database's **Auditing & Threat detection** blade, click **View audit logs**.</span></span>

    ![導覽窗格][7]

    <span data-ttu-id="c1243-164">隨即開啟 [稽核記錄] 刀鋒視窗，您可以在其中檢視記錄。</span><span class="sxs-lookup"><span data-stu-id="c1243-164">An **Audit records** blade opens, from which you'll be able to view the logs.</span></span>

    - <span data-ttu-id="c1243-165">您可以按一下 [稽核記錄] 刀鋒視窗頂端的 [篩選] 來檢視特定日期。</span><span class="sxs-lookup"><span data-stu-id="c1243-165">You can view specific dates by clicking **Filter** at the top of the **Audit records** blade.</span></span>
    - <span data-ttu-id="c1243-166">您可以在由伺服器原則或資料庫原則稽核建立的稽核記錄之間切換。</span><span class="sxs-lookup"><span data-stu-id="c1243-166">You can switch between audit records that were created by a server policy or database policy audit.</span></span>

       ![導覽窗格][8]

* <span data-ttu-id="c1243-168">使用系統函數 **sys.fn_get_audit_file** (T-SQL) 以表格格式傳回稽核記錄資料。</span><span class="sxs-lookup"><span data-stu-id="c1243-168">Use the system function **sys.fn_get_audit_file** (T-SQL) to return the audit log data in tabular format.</span></span> <span data-ttu-id="c1243-169">如需有關如何使用此函數的詳細資訊，請參閱 [sys.fn_get_audit_file 文件](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql) (英文)。</span><span class="sxs-lookup"><span data-stu-id="c1243-169">For more information on using this function, see the [sys.fn_get_audit_file documentation](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span></span>


* <span data-ttu-id="c1243-170">使用 SQL Server Management Studio (SSMS 17 或更新版本) 中的 [合併稽核檔案]：</span><span class="sxs-lookup"><span data-stu-id="c1243-170">Use **Merge Audit Files** in SQL Server Management Studio (starting with SSMS 17):</span></span>  
    1. <span data-ttu-id="c1243-171">從 SSMS 功能表選取 [檔案] > [開啟] > [合併稽核檔案]。</span><span class="sxs-lookup"><span data-stu-id="c1243-171">From the SSMS menu, select **File** > **Open** > **Merge Audit Files**.</span></span>

        ![導覽窗格][9]
    2. <span data-ttu-id="c1243-173">隨即開啟 [新增稽核檔案] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="c1243-173">The **Add Audit Files** dialog box opens.</span></span> <span data-ttu-id="c1243-174">選取其中一個 [新增] 選項以選擇是否要從本機磁碟合併稽核檔案，或從 Azure 儲存體匯入稽核檔案 (您將需要提供您的 Azure 儲存體詳細資料和帳戶金鑰)。</span><span class="sxs-lookup"><span data-stu-id="c1243-174">Select one of the **Add** options to choose whether to merge audit files from a local disk or import them from Azure Storage (you will be required to provide your Azure Storage details and account key).</span></span>

    3. <span data-ttu-id="c1243-175">已新增要合併的所有檔案之後，請按一下 [確定] 以完成合併作業。</span><span class="sxs-lookup"><span data-stu-id="c1243-175">After all files to merge have been added, click **OK** to complete the merge operation.</span></span>

    4. <span data-ttu-id="c1243-176">合併的檔案會在 SSMS 中開啟，您可以在其中檢視和分析該檔案，以及將其匯出至 XEL 或 CSV 檔案或資料表。</span><span class="sxs-lookup"><span data-stu-id="c1243-176">The merged file opens in SSMS, where you can view and analyze it, as well as export it to an XEL or CSV file or to a table.</span></span>

* <span data-ttu-id="c1243-177">使用我們建立的[同步應用程式](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration)。</span><span class="sxs-lookup"><span data-stu-id="c1243-177">Use the [sync application](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) that we have created.</span></span> <span data-ttu-id="c1243-178">其會在 Azure 中執行，並利用 Operations Management Suite (OMS) Log Analytics 公開 API 將 SQL 稽核記錄推送至 OMS。</span><span class="sxs-lookup"><span data-stu-id="c1243-178">It runs in Azure and utilizes Operations Management Suite (OMS) Log Analytics public APIs to push SQL audit logs into OMS.</span></span> <span data-ttu-id="c1243-179">同步應用程式會透過 OMS Log Analytics 儀表板，將 SQL 稽核記錄推送至 OMS Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="c1243-179">The sync application pushes SQL audit logs into OMS Log Analytics for consumption via the OMS Log Analytics dashboard.</span></span> 

* <span data-ttu-id="c1243-180">使用 Power BI。</span><span class="sxs-lookup"><span data-stu-id="c1243-180">Use Power BI.</span></span> <span data-ttu-id="c1243-181">您可以在 Power BI 中檢視和分析稽核記錄資料。</span><span class="sxs-lookup"><span data-stu-id="c1243-181">You can view and analyze audit log data in Power BI.</span></span> <span data-ttu-id="c1243-182">深入了解 [Power BI，並存取可下載的範本](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/)。</span><span class="sxs-lookup"><span data-stu-id="c1243-182">Learn more about [Power BI, and access a downloadable template](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span></span>

* <span data-ttu-id="c1243-183">透過入口網站或使用工具 (例如 [Azure 儲存體總管](http://storageexplorer.com/)) 從 Azure 儲存體 Blob 容器下載記錄檔。</span><span class="sxs-lookup"><span data-stu-id="c1243-183">Download log files from your Azure Storage blob container via the portal or by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
    * <span data-ttu-id="c1243-184">在您將記錄檔下載到本機之後，您可以按兩下檔案，以在 SSMS 中開啟、檢視及分析記錄。</span><span class="sxs-lookup"><span data-stu-id="c1243-184">After you have downloaded a log file locally, you can double-click the file to open, view, and analyze the logs in SSMS.</span></span>
    * <span data-ttu-id="c1243-185">您也可以透過 Azure 儲存體總管同時下載多個檔案。</span><span class="sxs-lookup"><span data-stu-id="c1243-185">You can also download multiple files simultaneously via Azure Storage Explorer.</span></span> <span data-ttu-id="c1243-186">以滑鼠右鍵按一下特定子資料夾 (例如，包含特定日期所有記錄檔的子資料夾)，然後選取 [另存新檔] 以儲存在本機資料夾中。</span><span class="sxs-lookup"><span data-stu-id="c1243-186">Right-click a specific subfolder (for example, a subfolder that includes all log files for a specific date) and select **Save as** to save in a local folder.</span></span>

* <span data-ttu-id="c1243-187">其他方法：</span><span class="sxs-lookup"><span data-stu-id="c1243-187">Additional methods:</span></span>
   * <span data-ttu-id="c1243-188">下載多個檔案 (或包含一整天記錄檔的子資料夾，如本清單中上一個項目中所述) 之後，您可以在本機合併這些檔案，如稍早所述的 SSMS 合併稽核檔案指示中所述。</span><span class="sxs-lookup"><span data-stu-id="c1243-188">After downloading several files (or a subfolder that includes log files for an entire day, as described in the previous item in this list), you can merge them locally as described in the SSMS Merge Audit Files instructions described earlier.</span></span>

   * <span data-ttu-id="c1243-189">以程式設計方式檢視 Blob 稽核記錄：</span><span class="sxs-lookup"><span data-stu-id="c1243-189">View blob auditing logs programmatically:</span></span>

     * <span data-ttu-id="c1243-190">使用[擴充事件讀取器](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) C# 程式庫。</span><span class="sxs-lookup"><span data-stu-id="c1243-190">Use the [Extended Events Reader](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) C# library.</span></span>
     * <span data-ttu-id="c1243-191">使用 PowerShell [查詢擴充事件檔案](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/)。</span><span class="sxs-lookup"><span data-stu-id="c1243-191">[Query Extended Events Files](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) by using PowerShell.</span></span>




## <span data-ttu-id="c1243-192"><a id="subheading-5"></a>實際作法</span><span class="sxs-lookup"><span data-stu-id="c1243-192"><a id="subheading-5"></a>Production practices</span></span>
<!--The description in this section refers to preceding screen captures.-->

### <span data-ttu-id="c1243-193"><a id="subheading-6">稽核異地複寫資料庫</a></span><span class="sxs-lookup"><span data-stu-id="c1243-193"><a id="subheading-6">Auditing geo-replicated databases</a></span></span>
<span data-ttu-id="c1243-194">使用異地複寫資料庫時，您可以在主要資料庫、次要資料庫或兩者 (需視稽核類型而定) 設定稽核。</span><span class="sxs-lookup"><span data-stu-id="c1243-194">When you use geo-replicated databases, it is possible to set up auditing on either the primary database, the secondary database, or both, depending on the audit type.</span></span>

<span data-ttu-id="c1243-195">請遵循這些指示 (請記住，您只能從主要資料庫稽核設定開啟或關閉 Blob 稽核)：</span><span class="sxs-lookup"><span data-stu-id="c1243-195">Follow these instructions (remember that blob auditing can be turned on or off only from the primary database auditing settings):</span></span>

* <span data-ttu-id="c1243-196">**主要資料庫**。</span><span class="sxs-lookup"><span data-stu-id="c1243-196">**Primary database**.</span></span> <span data-ttu-id="c1243-197">依照[設定資料庫的稽核](#subheading-2)一節所述，在伺服器或資料庫本身開啟 Blob 稽核。</span><span class="sxs-lookup"><span data-stu-id="c1243-197">Turn on blob auditing, either on the server or on the database itself, as described in the [Set up auditing for your database](#subheading-2) section.</span></span>
* <span data-ttu-id="c1243-198">**次要資料庫**。</span><span class="sxs-lookup"><span data-stu-id="c1243-198">**Secondary database**.</span></span> <span data-ttu-id="c1243-199">依照[設定資料庫的稽核](#subheading-2)一節所述，在主要資料庫上開啟 Blob 稽核。</span><span class="sxs-lookup"><span data-stu-id="c1243-199">Turn on blob auditing on the primary database, as described in the [Set up auditing for your database](#subheading-2) section.</span></span> 
   * <span data-ttu-id="c1243-200">必須在「主要資料庫本身」 (而不是在伺服器上) 啟用 Blob 稽核。</span><span class="sxs-lookup"><span data-stu-id="c1243-200">Blob auditing must be enabled on the *primary database itself*, not the server.</span></span>
   * <span data-ttu-id="c1243-201">在主要資料庫上啟用 Blob 稽核之後，它也會在次要資料庫上變成啟用狀態。</span><span class="sxs-lookup"><span data-stu-id="c1243-201">After blob auditing is enabled on the primary database, it will also become enabled on the secondary database.</span></span>

     >[!IMPORTANT]
     ><span data-ttu-id="c1243-202">根據預設值，次要資料庫的儲存體設定將會和主要資料庫上的設定完全相同，這會導致跨地區流量。</span><span class="sxs-lookup"><span data-stu-id="c1243-202">By default, the storage settings for the secondary database will be identical to those of the primary database, causing cross-regional traffic.</span></span> <span data-ttu-id="c1243-203">您可以在次要伺服器上啟用 Blob 稽核，並在次要伺服器儲存體設定中設定本機儲存體，以避免此情況。</span><span class="sxs-lookup"><span data-stu-id="c1243-203">You can avoid this by enabling blob auditing on the secondary server and configuring local storage in the secondary server storage settings.</span></span> <span data-ttu-id="c1243-204">這將覆寫次要資料庫的儲存位置，並導致每個資料庫都將其稽核記錄儲存至本機儲存體。</span><span class="sxs-lookup"><span data-stu-id="c1243-204">This will override the storage location for the secondary database and result in each database saving its audit logs to local storage.</span></span>  
<br>

### <span data-ttu-id="c1243-205"><a id="subheading-6">儲存體金鑰重新產生</a></span><span class="sxs-lookup"><span data-stu-id="c1243-205"><a id="subheading-6">Storage key regeneration</a></span></span>
<span data-ttu-id="c1243-206">在生產中，您可能會定期重新整理儲存體金鑰。</span><span class="sxs-lookup"><span data-stu-id="c1243-206">In production, you are likely to refresh your storage keys periodically.</span></span> <span data-ttu-id="c1243-207">重新整理金鑰時，您需要重新儲存稽核原則。</span><span class="sxs-lookup"><span data-stu-id="c1243-207">When refreshing your keys, you need to resave the auditing policy.</span></span> <span data-ttu-id="c1243-208">程序如下：</span><span class="sxs-lookup"><span data-stu-id="c1243-208">The process is as follows:</span></span>

1. <span data-ttu-id="c1243-209">開啟 [儲存體詳細資料] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c1243-209">Open the **Storage Details** blade.</span></span> <span data-ttu-id="c1243-210">在 [儲存體存取金鑰] 方塊中，選取 [次要]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="c1243-210">In the **Storage Access Key** box, select **Secondary**, and click **OK**.</span></span> <span data-ttu-id="c1243-211">然後按一下稽核組態刀鋒視窗頂端的 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="c1243-211">Then click **Save** at the top of the auditing configuration blade.</span></span>

    ![導覽窗格][5]
2. <span data-ttu-id="c1243-213">移至儲存體組態刀鋒視窗，並重新產生主要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="c1243-213">Go to the storage configuration blade and regenerate the primary access key.</span></span>

    ![導覽窗格][6]
3. <span data-ttu-id="c1243-215">返回稽核組態刀鋒視窗，將儲存體存取金鑰從次要切換成主要，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="c1243-215">Go back to the auditing configuration blade, switch the storage access key from secondary to primary, and then click **OK**.</span></span> <span data-ttu-id="c1243-216">然後按一下稽核組態刀鋒視窗頂端的 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="c1243-216">Then click **Save** at the top of the auditing configuration blade.</span></span>
4. <span data-ttu-id="c1243-217">返回儲存體組態刀鋒視窗，並重新產生次要存取金鑰 (為下一個金鑰重新整理週期做準備)。</span><span class="sxs-lookup"><span data-stu-id="c1243-217">Go back to the storage configuration blade and regenerate the secondary access key (in preparation for the next key's refresh cycle).</span></span>

## <span data-ttu-id="c1243-218"><a id="subheading-7"></a>自動化 (PowerShell/REST API)</span><span class="sxs-lookup"><span data-stu-id="c1243-218"><a id="subheading-7"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="c1243-219">您也可以使用下列自動化工具在 Azure SQL Database 中設定稽核：</span><span class="sxs-lookup"><span data-stu-id="c1243-219">You can also configure auditing in Azure SQL Database by using the following automation tools:</span></span>

* <span data-ttu-id="c1243-220">**PowerShell Cmdlet**：</span><span class="sxs-lookup"><span data-stu-id="c1243-220">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="c1243-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="c1243-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="c1243-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="c1243-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="c1243-223">[Remove-AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="c1243-223">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="c1243-224">[Remove-AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="c1243-224">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="c1243-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="c1243-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="c1243-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="c1243-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="c1243-227">[Use-AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="c1243-227">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

   <span data-ttu-id="c1243-228">如需指令碼範例，請參閱[使用 PowerShell 設定稽核與威脅偵測](scripts/sql-database-auditing-and-threat-detection-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="c1243-228">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

* <span data-ttu-id="c1243-229">**REST API - Blob 稽核**：</span><span class="sxs-lookup"><span data-stu-id="c1243-229">**REST API - Blob auditing**:</span></span>

   * [<span data-ttu-id="c1243-230">建立或更新資料庫 Blob 稽核原則</span><span class="sxs-lookup"><span data-stu-id="c1243-230">Create or Update Database Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt695939.aspx)
   * [<span data-ttu-id="c1243-231">建立或更新伺服器 Blob 稽核原則</span><span class="sxs-lookup"><span data-stu-id="c1243-231">Create or Update Server Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt771861.aspx)
   * [<span data-ttu-id="c1243-232">取得資料庫 Blob 稽核原則</span><span class="sxs-lookup"><span data-stu-id="c1243-232">Get Database Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt695938.aspx)
   * [<span data-ttu-id="c1243-233">取得伺服器 Blob 稽核原則</span><span class="sxs-lookup"><span data-stu-id="c1243-233">Get Server Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt771860.aspx)
   * [<span data-ttu-id="c1243-234">取得伺服器 Blob 稽核操作結果</span><span class="sxs-lookup"><span data-stu-id="c1243-234">Get Server Blob Auditing Operation Result</span></span>](https://msdn.microsoft.com/library/azure/mt771862.aspx)


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
