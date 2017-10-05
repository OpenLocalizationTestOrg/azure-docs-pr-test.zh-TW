---
title: "針對 HDInsight 上的 Hadoop 進行偵錯：檢視記錄與解譯錯誤訊息 - Azure | Microsoft Docs"
description: "了解您使用 PowerShell 來管理 HDInsight 時可能收到的錯誤訊息，以及可採取來回復的步驟。"
services: hdinsight
tags: azure-portal
editor: cgronlun
manager: jhubbard
author: mumian
documentationcenter: 
ms.assetid: 7e6ceb0e-8be8-4911-bc80-20714030a3ad
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jgao
ms.openlocfilehash: 3031644e2975fd59edff13c7a9da1efa418e8abd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-hdinsight-logs"></a><span data-ttu-id="61c11-103">分析 HDInsight 記錄檔</span><span class="sxs-lookup"><span data-stu-id="61c11-103">Analyze HDInsight logs</span></span>
<span data-ttu-id="61c11-104">Azure HDInsight 中的每個 Hadoop 叢集都有一個 Azure 儲存體帳戶作為預設檔案系統。</span><span class="sxs-lookup"><span data-stu-id="61c11-104">Each Hadoop cluster in Azure HDInsight has an Azure storage account used as the default file system.</span></span> <span data-ttu-id="61c11-105">這個儲存體帳戶稱為預設儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="61c11-105">The storage account is referred as the default Storage account.</span></span> <span data-ttu-id="61c11-106">叢集使用預設儲存體帳戶上的 Azure 資料表儲存體和 Blob 儲存體來儲存其記錄檔。</span><span class="sxs-lookup"><span data-stu-id="61c11-106">Cluster uses the Azure Table storage and the Blob storage on the default Storage account to store its logs.</span></span>  <span data-ttu-id="61c11-107">若要找出叢集的預設儲存體帳戶，請參閱[在 HDInsight 中管理 Hadoop 叢集](hdinsight-administer-use-management-portal.md#find-the-default-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="61c11-107">To find out the default storage account for your cluster, see [Manage Hadoop clusters in HDInsight](hdinsight-administer-use-management-portal.md#find-the-default-storage-account).</span></span> <span data-ttu-id="61c11-108">即使在刪除叢集之後，記錄檔仍會保留在儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="61c11-108">The logs retain in the Storage account even after the cluster is deleted.</span></span>

## <a name="logs-written-to-azure-tables"></a><span data-ttu-id="61c11-109">寫入 Azure 資料表的記錄檔</span><span class="sxs-lookup"><span data-stu-id="61c11-109">Logs written to Azure Tables</span></span>
<span data-ttu-id="61c11-110">寫入 Azure 資料表的記錄檔可讓人更深入了解 HDInsight 叢集發生的情形。</span><span class="sxs-lookup"><span data-stu-id="61c11-110">The logs written to Azure Tables provide one level of insight into what is happening with an HDInsight cluster.</span></span>

<span data-ttu-id="61c11-111">建立 HDInsight 叢集時，會在預設資料表儲存體中自動為 Linux 叢集建立 6 個資料表：</span><span class="sxs-lookup"><span data-stu-id="61c11-111">When you create an HDInsight cluster, 6 tables are automatically created for Linux-based clusters in the default Table storage:</span></span>

* <span data-ttu-id="61c11-112">hdinsightagentlog</span><span class="sxs-lookup"><span data-stu-id="61c11-112">hdinsightagentlog</span></span>
* <span data-ttu-id="61c11-113">syslog</span><span class="sxs-lookup"><span data-stu-id="61c11-113">syslog</span></span>
* <span data-ttu-id="61c11-114">daemonlog</span><span class="sxs-lookup"><span data-stu-id="61c11-114">daemonlog</span></span>
* <span data-ttu-id="61c11-115">hadoopservicelog</span><span class="sxs-lookup"><span data-stu-id="61c11-115">hadoopservicelog</span></span>
* <span data-ttu-id="61c11-116">ambariserverlog</span><span class="sxs-lookup"><span data-stu-id="61c11-116">ambariserverlog</span></span>
* <span data-ttu-id="61c11-117">ambariagentlog</span><span class="sxs-lookup"><span data-stu-id="61c11-117">ambariagentlog</span></span>

<span data-ttu-id="61c11-118">針對 Windows 型叢集建立 3 個資料表：</span><span class="sxs-lookup"><span data-stu-id="61c11-118">3 tables are created for Windows-based clusters:</span></span>

* <span data-ttu-id="61c11-119">setuplog：佈建/設定 HDInsight 叢集時發生的事件/例外狀況的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="61c11-119">setuplog: Log of events/exceptions encountered in provisioning/setting up of HDInsight clusters.</span></span>
* <span data-ttu-id="61c11-120">hadoopinstalllog：在叢集上安裝 Hadoop 時發生的事件/例外狀況的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="61c11-120">hadoopinstalllog: Log of events/exceptions encountered when installing Hadoop on the cluster.</span></span> <span data-ttu-id="61c11-121">針對以自訂參數建立的叢集，此資料表適用於相關問題的偵錯。</span><span class="sxs-lookup"><span data-stu-id="61c11-121">This table may be useful in debugging issues related to clusters created with custom parameters.</span></span>
* <span data-ttu-id="61c11-122">hadoopservicelog：所有 Hadoop 服務記錄的事件/例外狀況的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="61c11-122">hadoopservicelog: Log of events/exceptions recorded by all Hadoop services.</span></span> <span data-ttu-id="61c11-123">針對 HDInsight 叢集上的作業失敗，此資料表適用於相關問題的偵錯。</span><span class="sxs-lookup"><span data-stu-id="61c11-123">This table may be useful in debugging issues related to job failures on HDInsight clusters.</span></span>

<span data-ttu-id="61c11-124">資料表檔案名稱為 **u<ClusterName>DDMonYYYYatHHMMSSsss<TableName>**。</span><span class="sxs-lookup"><span data-stu-id="61c11-124">The table file names are **u<ClusterName>DDMonYYYYatHHMMSSsss<TableName>**.</span></span>

<span data-ttu-id="61c11-125">這些資料表包含下列欄位：</span><span class="sxs-lookup"><span data-stu-id="61c11-125">These tables contains the following fields:</span></span>

* <span data-ttu-id="61c11-126">ClusterDnsName</span><span class="sxs-lookup"><span data-stu-id="61c11-126">ClusterDnsName</span></span>
* <span data-ttu-id="61c11-127">ComponentName</span><span class="sxs-lookup"><span data-stu-id="61c11-127">ComponentName</span></span>
* <span data-ttu-id="61c11-128">EventTimestamp</span><span class="sxs-lookup"><span data-stu-id="61c11-128">EventTimestamp</span></span>
* <span data-ttu-id="61c11-129">Host</span><span class="sxs-lookup"><span data-stu-id="61c11-129">Host</span></span>
* <span data-ttu-id="61c11-130">MALoggingHash</span><span class="sxs-lookup"><span data-stu-id="61c11-130">MALoggingHash</span></span>
* <span data-ttu-id="61c11-131">訊息</span><span class="sxs-lookup"><span data-stu-id="61c11-131">Message</span></span>
* <span data-ttu-id="61c11-132">N</span><span class="sxs-lookup"><span data-stu-id="61c11-132">N</span></span>
* <span data-ttu-id="61c11-133">PreciseTimeStamp</span><span class="sxs-lookup"><span data-stu-id="61c11-133">PreciseTimeStamp</span></span>
* <span data-ttu-id="61c11-134">角色</span><span class="sxs-lookup"><span data-stu-id="61c11-134">Role</span></span>
* <span data-ttu-id="61c11-135">RowIndex</span><span class="sxs-lookup"><span data-stu-id="61c11-135">RowIndex</span></span>
* <span data-ttu-id="61c11-136">租用戶</span><span class="sxs-lookup"><span data-stu-id="61c11-136">Tenant</span></span>
* <span data-ttu-id="61c11-137">時間戳記</span><span class="sxs-lookup"><span data-stu-id="61c11-137">TIMESTAMP</span></span>
* <span data-ttu-id="61c11-138">TraceLevel</span><span class="sxs-lookup"><span data-stu-id="61c11-138">TraceLevel</span></span>

### <a name="tools-for-accessing-the-logs"></a><span data-ttu-id="61c11-139">用於存取記錄檔的工具</span><span class="sxs-lookup"><span data-stu-id="61c11-139">Tools for accessing the logs</span></span>
<span data-ttu-id="61c11-140">有許多工具可用來存取這些資料表中的資料：</span><span class="sxs-lookup"><span data-stu-id="61c11-140">There are many tools available for accessing data in these tables:</span></span>

* <span data-ttu-id="61c11-141">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="61c11-141">Visual Studio</span></span>
* <span data-ttu-id="61c11-142">Azure 儲存體總管</span><span class="sxs-lookup"><span data-stu-id="61c11-142">Azure Storage Explorer</span></span>
* <span data-ttu-id="61c11-143">Power Query for Excel</span><span class="sxs-lookup"><span data-stu-id="61c11-143">Power Query for Excel</span></span>

#### <a name="use-power-query-for-excel"></a><span data-ttu-id="61c11-144">使用 Power Query for Excel</span><span class="sxs-lookup"><span data-stu-id="61c11-144">Use Power Query for Excel</span></span>
<span data-ttu-id="61c11-145">您可以從 [www.microsoft.com/en-us/download/details.aspx?id=39379](http://www.microsoft.com/en-us/download/details.aspx?id=39379) 安裝 Power Query。</span><span class="sxs-lookup"><span data-stu-id="61c11-145">Power Query can be installed from [www.microsoft.com/en-us/download/details.aspx?id=39379](http://www.microsoft.com/en-us/download/details.aspx?id=39379).</span></span> <span data-ttu-id="61c11-146">查看下載頁面上的系統需求</span><span class="sxs-lookup"><span data-stu-id="61c11-146">See the download page for the system requirements</span></span>

<span data-ttu-id="61c11-147">**使用 Power Query 來開啟和分析服務記錄**</span><span class="sxs-lookup"><span data-stu-id="61c11-147">**To use Power Query to open and analyze the service log**</span></span>

1. <span data-ttu-id="61c11-148">開啟 **Microsoft Excel**。</span><span class="sxs-lookup"><span data-stu-id="61c11-148">Open **Microsoft Excel**.</span></span>
2. <span data-ttu-id="61c11-149">從 [Power Query] 功能表中，按一下 [從 Azure]，然後按一下 [從 Microsoft Azure 資料表儲存體]。</span><span class="sxs-lookup"><span data-stu-id="61c11-149">From the **Power Query** menu, click **From Azure**, and then click **From Microsoft Azure Table storage**.</span></span>
   
    ![HDInsight Hadoop Excel PowerQuery 開啟 Azure 資料表儲存體](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-using-excel-power-query-open.png)
3. <span data-ttu-id="61c11-151">輸入儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="61c11-151">Enter the storage account name.</span></span> <span data-ttu-id="61c11-152">這可以是簡短名稱或 FQDN。</span><span class="sxs-lookup"><span data-stu-id="61c11-152">This can be either the short name or the FQDN.</span></span>
4. <span data-ttu-id="61c11-153">輸入儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="61c11-153">Enter the storage account key.</span></span> <span data-ttu-id="61c11-154">您應該會看到一份資料表清單：</span><span class="sxs-lookup"><span data-stu-id="61c11-154">You shall see a list of tables:</span></span>
   
    ![儲存在 Azure 資料表儲存體中的 HDInsight Hadoop 記錄檔](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-table-names.png)
5. <span data-ttu-id="61c11-156">在 [導覽器] 窗格中以滑鼠右鍵按一下 hadoopservicelog 資料表，然後選取 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="61c11-156">Right-click the hadoopservicelog table in the **Navigator** pane and select **Edit**.</span></span> <span data-ttu-id="61c11-157">您應該會看到 4 個資料行。</span><span class="sxs-lookup"><span data-stu-id="61c11-157">You shall see 4 columns.</span></span> <span data-ttu-id="61c11-158">選擇性地選取 [分割區索引鍵]、[資料列索引鍵] 和 [時間戳記] 資料行，然後從功能區的選項中按一下 [移除資料行]，將它們刪除。</span><span class="sxs-lookup"><span data-stu-id="61c11-158">Optionally, delete the **Partition Key**, **Row Key**, and **Timestamp** columns by selecting them, then clicking **Remove Columns** from the options in the ribbon.</span></span>
6. <span data-ttu-id="61c11-159">按一下 [內容] 資料行上的展開圖示，選擇您要匯入至 Excel 試算表的資料行。</span><span class="sxs-lookup"><span data-stu-id="61c11-159">Click the expand icon on the Content column to choose the columns you want to import into the Excel spreadsheet.</span></span> <span data-ttu-id="61c11-160">在此示範中，我選擇 TraceLevel 和 ComponentName：它可以提供一些基本資訊讓我知道哪些元件有問題。</span><span class="sxs-lookup"><span data-stu-id="61c11-160">For this demonstration, I chose TraceLevel, and ComponentName: It can give me some basic information on which components had issues.</span></span>
   
    ![HDInsight Hadoop 記錄檔選擇資料行](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-using-excel-power-query-filter.png)
7. <span data-ttu-id="61c11-162">按一下 [確定] 以匯入資料。</span><span class="sxs-lookup"><span data-stu-id="61c11-162">Click **OK** to import the data.</span></span>
8. <span data-ttu-id="61c11-163">選取 [TraceLevel]、[Role] 和 [ComponentName] 資料行，然後按一下功能區的 [群組依據] 控制項。</span><span class="sxs-lookup"><span data-stu-id="61c11-163">Select the **TraceLevel**, Role, and **ComponentName** columns, and then click **Group By** control in the ribbon.</span></span>
9. <span data-ttu-id="61c11-164">按一下 [群組依據] 對話方塊中的 [確定]</span><span class="sxs-lookup"><span data-stu-id="61c11-164">Click **OK** in the Group By dialog box</span></span>
10. <span data-ttu-id="61c11-165">按一下 [套用並關閉]。</span><span class="sxs-lookup"><span data-stu-id="61c11-165">Click** Apply & Close**.</span></span>

<span data-ttu-id="61c11-166">您現在可以視需要使用 Excel 來篩選和排序。</span><span class="sxs-lookup"><span data-stu-id="61c11-166">You can now use Excel to filter and sort as necessary.</span></span> <span data-ttu-id="61c11-167">很明顯地，您需要包含其他資料行 (例如 Message)，以便在問題發生時深入探索，但如上所述選取和分組資料行有助於了解 Hadoop 服務發生的情形。</span><span class="sxs-lookup"><span data-stu-id="61c11-167">Obviously, you may want to include other columns (e.g. Message) in order to drill down into issues when they occur, but selecting and grouping the columns described above provides a decent picture of what is happening with Hadoop services.</span></span> <span data-ttu-id="61c11-168">相同的概念也適用於 setuplog 和 hadoopinstalllog 資料表。</span><span class="sxs-lookup"><span data-stu-id="61c11-168">The same idea can be applied to the setuplog and hadoopinstalllog tables.</span></span>

#### <a name="use-visual-studio"></a><span data-ttu-id="61c11-169">使用 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="61c11-169">Use Visual Studio</span></span>
<span data-ttu-id="61c11-170">**使用 Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="61c11-170">**To use Visual Studio**</span></span>

1. <span data-ttu-id="61c11-171">開啟 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="61c11-171">Open Visual Studio.</span></span>
2. <span data-ttu-id="61c11-172">從 [檢視] 功能表中，按一下 [Cloud Explorer]。</span><span class="sxs-lookup"><span data-stu-id="61c11-172">From the **View** menu, click **Cloud Explorer**.</span></span> <span data-ttu-id="61c11-173">或直接按一下 **CTRL+\, CTRL+X**。</span><span class="sxs-lookup"><span data-stu-id="61c11-173">Or simply click **CTRL+\, CTRL+X**.</span></span>
3. <span data-ttu-id="61c11-174">從 [Cloud Explorer] 中，選取 [資源類型]。</span><span class="sxs-lookup"><span data-stu-id="61c11-174">From **Cloud Explorer**, select **Resource Types**.</span></span>  <span data-ttu-id="61c11-175">另一個可用的選項是 [資源群組] 。</span><span class="sxs-lookup"><span data-stu-id="61c11-175">The other available option is **Resource Groups**.</span></span>
4. <span data-ttu-id="61c11-176">展開 [儲存體帳戶]、您叢集的預設儲存體帳戶，然後是 [資料表]。</span><span class="sxs-lookup"><span data-stu-id="61c11-176">Expand **Storage Accounts**, the default storage account for your cluster, and then **Tables**.</span></span>
5. <span data-ttu-id="61c11-177">按兩下 [hadoopservicelog]。</span><span class="sxs-lookup"><span data-stu-id="61c11-177">Double-click **hadoopservicelog**.</span></span>
6. <span data-ttu-id="61c11-178">新增篩選器。</span><span class="sxs-lookup"><span data-stu-id="61c11-178">Add a filter.</span></span> <span data-ttu-id="61c11-179">例如：</span><span class="sxs-lookup"><span data-stu-id="61c11-179">For example:</span></span>
   
        TraceLevel eq 'ERROR'
   
    ![HDInsight Hadoop 記錄檔選擇資料行](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-visual-studio-filter.png)
   
    <span data-ttu-id="61c11-181">如需建構篩選器的詳細資訊，請參閱[建構資料表設計工具的篩選字串](../vs-azure-tools-table-designer-construct-filter-strings.md)。</span><span class="sxs-lookup"><span data-stu-id="61c11-181">For more information about constructing filters, see [Construct Filter Strings for the Table Designer](../vs-azure-tools-table-designer-construct-filter-strings.md).</span></span>

## <a name="logs-written-to-azure-blob-storage"></a><span data-ttu-id="61c11-182">寫入 Azure Blob 儲存體的記錄檔</span><span class="sxs-lookup"><span data-stu-id="61c11-182">Logs Written to Azure Blob Storage</span></span>
<span data-ttu-id="61c11-183">[寫入 Azure 資料表的記錄檔](#log-written-to-azure-tables)可讓人更深入了解 HDInsight 叢集發生的情形。</span><span class="sxs-lookup"><span data-stu-id="61c11-183">[The logs written to Azure Tables](#log-written-to-azure-tables) provide one level of insight into what is happening with an HDInsight cluster.</span></span> <span data-ttu-id="61c11-184">不過，這些資料表並不會提供工作層級記錄檔，這些記錄檔有助於發生問題時進一步深入探索。</span><span class="sxs-lookup"><span data-stu-id="61c11-184">However, these tables do not provide task-level logs, which can be helpful in drilling further into issues when they occur.</span></span> <span data-ttu-id="61c11-185">為了提供這一層更深入的詳細資料，針對透過 Templeton 提交的任何作業，HDInsight 叢集設定成將工作記錄檔寫入 Blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="61c11-185">To provide this next level of detail, HDInsight clusters are configured to write task logs to your Blob Storage account for any job that is submitted through Templeton.</span></span> <span data-ttu-id="61c11-186">實際上，這代表使用 Microsoft Azure PowerShell Cmdlet 或 .NET Job Submission API 提交的作業，而不是透過叢集的 RDP/命令列存取所提交的作業。</span><span class="sxs-lookup"><span data-stu-id="61c11-186">Practically, this means jobs submitted using the Microsoft Azure PowerShell cmdlets or the .NET Job Submission APIs, not jobs submitted through RDP/command-line access to the cluster.</span></span> 

<span data-ttu-id="61c11-187">若要檢視記錄檔，請參閱[在 Linux 型 HDInsight 上存取 YARN 應用程式記錄檔](hdinsight-hadoop-access-yarn-app-logs-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="61c11-187">To view the logs, see [Access YARN application logs on Linux-based HDInsight](hdinsight-hadoop-access-yarn-app-logs-linux.md).</span></span>

<span data-ttu-id="61c11-188">如需應用程式記錄檔的詳細資訊，請參閱 [簡化 YARN 的使用者記錄檔管理和存取](http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/)。</span><span class="sxs-lookup"><span data-stu-id="61c11-188">For more information about application logs, see [Simplifying user-logs management and access in YARN](http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/).</span></span>

## <a name="view-cluster-health-and-job-logs"></a><span data-ttu-id="61c11-189">檢視叢集健康情況和工作記錄檔</span><span class="sxs-lookup"><span data-stu-id="61c11-189">View cluster health and job logs</span></span>
### <a name="access-hadoop-ui"></a><span data-ttu-id="61c11-190">存取 Hadoop UI</span><span class="sxs-lookup"><span data-stu-id="61c11-190">Access Hadoop UI</span></span>
<span data-ttu-id="61c11-191">從 Azure 入口網站中，按一下 HDInsight 叢集名稱以開啟叢集刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="61c11-191">From the Azure portal, click an HDInsight cluster name to open the cluster blade.</span></span> <span data-ttu-id="61c11-192">從叢集刀鋒視窗中，按一下 [儀表板] 。</span><span class="sxs-lookup"><span data-stu-id="61c11-192">From the cluster blade, click **Dashboard**.</span></span>

![啟動叢集儀表板](./media/hdinsight-debug-jobs/hdi-debug-launch-dashboard.png)

<span data-ttu-id="61c11-194">出現提示時，輸入叢集系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="61c11-194">When prompted, enter the cluster administrator credentials.</span></span> <span data-ttu-id="61c11-195">在開啟的查詢主控台中，按一下 [Hadoop UI] 。</span><span class="sxs-lookup"><span data-stu-id="61c11-195">In the Query Console that opens, click **Hadoop UI**.</span></span>

![啟動 Hadoop UI](./media/hdinsight-debug-jobs/hdi-debug-launch-dashboard-hadoop-ui.png)

### <a name="access-the-yarn-ui"></a><span data-ttu-id="61c11-197">存取 Yarn UI</span><span class="sxs-lookup"><span data-stu-id="61c11-197">Access the Yarn UI</span></span>
<span data-ttu-id="61c11-198">從 Azure 入口網站中，按一下 HDInsight 叢集名稱以開啟叢集刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="61c11-198">From the Azure portal, click an HDInsight cluster name to open the cluster blade.</span></span> <span data-ttu-id="61c11-199">從叢集刀鋒視窗中，按一下 [儀表板] 。</span><span class="sxs-lookup"><span data-stu-id="61c11-199">From the cluster blade, click **Dashboard**.</span></span> <span data-ttu-id="61c11-200">出現提示時，輸入叢集系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="61c11-200">When prompted, enter the cluster administrator credentials.</span></span> <span data-ttu-id="61c11-201">在開啟的查詢主控台中，按一下 [YARN UI] 。</span><span class="sxs-lookup"><span data-stu-id="61c11-201">In the Query Console that opens, click **YARN UI**.</span></span>

<span data-ttu-id="61c11-202">您可以使用 YARN UI 來執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="61c11-202">You can use the YARN UI to do the following:</span></span>

* <span data-ttu-id="61c11-203">**取得叢集狀態**。</span><span class="sxs-lookup"><span data-stu-id="61c11-203">**Get cluster status**.</span></span> <span data-ttu-id="61c11-204">從左窗格中展開 [叢集]，然後按一下 [關於]。</span><span class="sxs-lookup"><span data-stu-id="61c11-204">From the left pane, expand **Cluster**, and click **About**.</span></span> <span data-ttu-id="61c11-205">這樣即會顯示叢集狀態詳細資料，例如，配置的記憶體總和、使用的核心數目、叢集資源管理員的狀態、叢集版本等。</span><span class="sxs-lookup"><span data-stu-id="61c11-205">This present cluster status details like total allocated memory, cores used, state of the cluster resource manager, cluster version etc.</span></span>
  
    ![啟動叢集儀表板](./media/hdinsight-debug-jobs/hdi-debug-yarn-cluster-state.png)
* <span data-ttu-id="61c11-207">**取得節點狀態**。</span><span class="sxs-lookup"><span data-stu-id="61c11-207">**Get node status**.</span></span> <span data-ttu-id="61c11-208">從左窗格中展開 [叢集]，然後按一下 [節點]。</span><span class="sxs-lookup"><span data-stu-id="61c11-208">From the left pane, expand **Cluster**, and click **Nodes**.</span></span> <span data-ttu-id="61c11-209">這樣會列出叢集中的所有節點、每個節點的 HTTP 位址、配置給每個節點的資源等資訊。</span><span class="sxs-lookup"><span data-stu-id="61c11-209">This lists all the nodes in the cluster, HTTP address of each node, resources allocated to each node, etc.</span></span>
* <span data-ttu-id="61c11-210">**監視工作狀態**。</span><span class="sxs-lookup"><span data-stu-id="61c11-210">**Monitor job status**.</span></span> <span data-ttu-id="61c11-211">從左窗格展開 [叢集]，然後按一下 [應用程式] 以列出叢集中的所有工作。</span><span class="sxs-lookup"><span data-stu-id="61c11-211">From the left pane, expand **Cluster**, and then click **Applications** to list all the jobs in the cluster.</span></span> <span data-ttu-id="61c11-212">如果您想要查看處於特定狀態 (例如，新增、已提交、執行中等狀態) 的工作，可按一下[應用程式] 底下的適當連結。</span><span class="sxs-lookup"><span data-stu-id="61c11-212">If you want to look at jobs in a specific state (such as new, submitted, running, etc.), click the appropriate link under **Applications**.</span></span> <span data-ttu-id="61c11-213">您可以進一步按一下工作名稱來深入了解該工作，例如包含輸出、記錄等相關資訊。</span><span class="sxs-lookup"><span data-stu-id="61c11-213">You can further click the job name to find out more about the job such including the output, logs, etc.</span></span>

### <a name="access-the-hbase-ui"></a><span data-ttu-id="61c11-214">存取 HBase UI</span><span class="sxs-lookup"><span data-stu-id="61c11-214">Access the HBase UI</span></span>
<span data-ttu-id="61c11-215">從 Azure 入口網站中，按一下 HDInsight HBase 叢集名稱以開啟叢集刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="61c11-215">From the Azure portal, click an HDInsight HBase cluster name to open the cluster blade.</span></span> <span data-ttu-id="61c11-216">從叢集刀鋒視窗中，按一下 [儀表板] 。</span><span class="sxs-lookup"><span data-stu-id="61c11-216">From the cluster blade, click **Dashboard**.</span></span> <span data-ttu-id="61c11-217">出現提示時，輸入叢集系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="61c11-217">When prompted, enter the cluster administrator credentials.</span></span> <span data-ttu-id="61c11-218">在開啟的查詢主控台中，按一下 [HBase UI] 。</span><span class="sxs-lookup"><span data-stu-id="61c11-218">In the Query Console that opens, click **HBase UI**.</span></span>

## <a name="hdinsight-error-codes"></a><span data-ttu-id="61c11-219">HDInsight 錯誤代碼</span><span class="sxs-lookup"><span data-stu-id="61c11-219">HDInsight error codes</span></span>
<span data-ttu-id="61c11-220">本節列舉的錯誤訊息可協助 Azure HDInsight 的 Hadoop 使用者了解，他們在使用 Azure PowerShell 來管理服務時可能遭遇的錯誤狀況，並建議一些步驟供他們從錯誤中回復。</span><span class="sxs-lookup"><span data-stu-id="61c11-220">The error messages itemized in this section are provided to help the users of Hadoop in Azure HDInsight understand possible error conditions that they can encounter when administering the service using Azure PowerShell and to advise them on the steps which can be taken to recover from the error.</span></span>

<span data-ttu-id="61c11-221">使用 Azure 入口網站管理 HDinsight 叢集時也可能會看到其中某些錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="61c11-221">Some of these error messages could also be seen in the Azure portal when it is used to manage HDInsight clusters.</span></span> <span data-ttu-id="61c11-222">但由於此情況下可能採取的補救動作有其限制，您可能看到的其他錯誤訊息比較不詳細。</span><span class="sxs-lookup"><span data-stu-id="61c11-222">But other error messages you might encounter there are less granular due to the constraints on the remedial actions possible in this context.</span></span> <span data-ttu-id="61c11-223">在很顯然有緩和措施的情況下，則會提供其他錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="61c11-223">Other error messages are provided in the contexts where the mitigation is obvious.</span></span> 

### <span data-ttu-id="61c11-224"><a id="AtleastOneSqlMetastoreMustBeProvided"></a>AtleastOneSqlMetastoreMustBeProvided</span><span class="sxs-lookup"><span data-stu-id="61c11-224"><a id="AtleastOneSqlMetastoreMustBeProvided"></a>AtleastOneSqlMetastoreMustBeProvided</span></span>
* <span data-ttu-id="61c11-225">**描述**：請至少提供一個元件的 Azure SQL Database 詳細資料，以便使用 Hive 和 Oozie metastore 的自訂設定。</span><span class="sxs-lookup"><span data-stu-id="61c11-225">**Description**: Please provide Azure SQL database details for at least one component in order to use custom settings for Hive and Oozie metastores.</span></span>
* <span data-ttu-id="61c11-226">**緩和**：使用者必須提供有效的 SQL Azure metastore，然後重試要求。</span><span class="sxs-lookup"><span data-stu-id="61c11-226">**Mitigation**: The user needs to supply a valid SQL Azure metastore and retry the request.</span></span>  

### <span data-ttu-id="61c11-227"><a id="AzureRegionNotSupported"></a>AzureRegionNotSupported</span><span class="sxs-lookup"><span data-stu-id="61c11-227"><a id="AzureRegionNotSupported"></a>AzureRegionNotSupported</span></span>
* <span data-ttu-id="61c11-228">**描述**：無法在區域 *nameOfYourRegion*中建立叢集。</span><span class="sxs-lookup"><span data-stu-id="61c11-228">**Description**: Could not create cluster in region *nameOfYourRegion*.</span></span> <span data-ttu-id="61c11-229">請使用有效的 HDInsight 區域，然後重試要求。</span><span class="sxs-lookup"><span data-stu-id="61c11-229">Use a valid HDInsight region and retry request.</span></span>
* <span data-ttu-id="61c11-230">**緩和**：客戶應該建立目前支援的叢集區域：東南亞、西歐、北歐、美國東部和美國西部。</span><span class="sxs-lookup"><span data-stu-id="61c11-230">**Mitigation**: Customer should create the cluster region that currently supports them: Southeast Asia, West Europe, North Europe, East US, or West US.</span></span>  

### <span data-ttu-id="61c11-231"><a id="ClusterContainerRecordNotFound"></a>ClusterContainerRecordNotFound</span><span class="sxs-lookup"><span data-stu-id="61c11-231"><a id="ClusterContainerRecordNotFound"></a>ClusterContainerRecordNotFound</span></span>
* <span data-ttu-id="61c11-232">**描述**：伺服器找不到所要求的叢集記錄。</span><span class="sxs-lookup"><span data-stu-id="61c11-232">**Description**: The server could not find the requested cluster record.</span></span>  
* <span data-ttu-id="61c11-233">**緩和**：重試作業。</span><span class="sxs-lookup"><span data-stu-id="61c11-233">**Mitigation**: Retry the operation.</span></span>

### <span data-ttu-id="61c11-234"><a id="ClusterDnsNameInvalidReservedWord"></a>ClusterDnsNameInvalidReservedWord</span><span class="sxs-lookup"><span data-stu-id="61c11-234"><a id="ClusterDnsNameInvalidReservedWord"></a>ClusterDnsNameInvalidReservedWord</span></span>
* <span data-ttu-id="61c11-235">**描述**：叢集 DNS 名稱 *yourDnsName* 無效。</span><span class="sxs-lookup"><span data-stu-id="61c11-235">**Description**: Cluster DNS name *yourDnsName* is invalid.</span></span> <span data-ttu-id="61c11-236">請確定名稱以英數字元開始和結束，且只包含 '-' 特殊字元</span><span class="sxs-lookup"><span data-stu-id="61c11-236">Please ensure name starts and ends with alphanumeric and can only contain '-' special character</span></span>  
* <span data-ttu-id="61c11-237">**緩和**：請確定叢集的 DNS 名稱有效，開頭和結束是英數字元，且不含虛線 '-' 以外的特殊字元，然後重試作業。</span><span class="sxs-lookup"><span data-stu-id="61c11-237">**Mitigation**: Make sure that you have used a valid DNS name for your cluster that starts and ends with alphanumeric and contains no special characters other than the dash '-' and then retry the operation.</span></span>

### <span data-ttu-id="61c11-238"><a id="ClusterNameUnavailable"></a>ClusterNameUnavailable</span><span class="sxs-lookup"><span data-stu-id="61c11-238"><a id="ClusterNameUnavailable"></a>ClusterNameUnavailable</span></span>
* <span data-ttu-id="61c11-239">**描述**：叢集名稱 *yourClusterName* 無法使用。</span><span class="sxs-lookup"><span data-stu-id="61c11-239">**Description**: Cluster name *yourClusterName* is unavailable.</span></span> <span data-ttu-id="61c11-240">請挑選其他名稱。</span><span class="sxs-lookup"><span data-stu-id="61c11-240">Please pick another name.</span></span>  
* <span data-ttu-id="61c11-241">**緩和**：使用者應該指定唯一且尚不存在的叢集名稱，然後重試。</span><span class="sxs-lookup"><span data-stu-id="61c11-241">**Mitigation**: The user should specify a clustername that is unique and does not exist and retry.</span></span> <span data-ttu-id="61c11-242">如果使用者在使用入口網站，當建立步驟中已使用叢集名稱時，UI 會通知使用者。</span><span class="sxs-lookup"><span data-stu-id="61c11-242">If the user is using the Portal, the UI will notify them if a cluster name is already being used during the create steps.</span></span>

### <span data-ttu-id="61c11-243"><a id="ClusterPasswordInvalid"></a>ClusterPasswordInvalid</span><span class="sxs-lookup"><span data-stu-id="61c11-243"><a id="ClusterPasswordInvalid"></a>ClusterPasswordInvalid</span></span>
* <span data-ttu-id="61c11-244">**描述**：叢集密碼無效。</span><span class="sxs-lookup"><span data-stu-id="61c11-244">**Description**: Cluster password is invalid.</span></span> <span data-ttu-id="61c11-245">密碼長度至少必須為 10 個字元，且至少必須包含一個數字、大寫字母、小寫字母和特殊字元，不可有空格，而且不得包含使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="61c11-245">Password must be at least 10 characters long and must contain at least one number, uppercase letter, lowercase letter and special character with no spaces and should not contain the username as part of it.</span></span>  
* <span data-ttu-id="61c11-246">**緩和**：請提供有效的叢集密碼，然後重試作業。</span><span class="sxs-lookup"><span data-stu-id="61c11-246">**Mitigation**: Provide a valid cluster password and retry the operation.</span></span>

### <span data-ttu-id="61c11-247"><a id="ClusterUserNameInvalid"></a>ClusterUserNameInvalid</span><span class="sxs-lookup"><span data-stu-id="61c11-247"><a id="ClusterUserNameInvalid"></a>ClusterUserNameInvalid</span></span>
* <span data-ttu-id="61c11-248">**描述**：叢集使用者名稱無效。</span><span class="sxs-lookup"><span data-stu-id="61c11-248">**Description**: Cluster username is invalid.</span></span> <span data-ttu-id="61c11-249">請確定使用者名稱不含特殊字元或空格。</span><span class="sxs-lookup"><span data-stu-id="61c11-249">Please ensure username doesn't contain special characters or spaces.</span></span>  
* <span data-ttu-id="61c11-250">**緩和**：請提供有效的叢集使用者名稱，然後重試作業。</span><span class="sxs-lookup"><span data-stu-id="61c11-250">**Mitigation**: Provide a valid cluster username and retry the operation.</span></span>

### <span data-ttu-id="61c11-251"><a id="ClusterUserNameInvalidReservedWord"></a>ClusterUserNameInvalidReservedWord</span><span class="sxs-lookup"><span data-stu-id="61c11-251"><a id="ClusterUserNameInvalidReservedWord"></a>ClusterUserNameInvalidReservedWord</span></span>
* <span data-ttu-id="61c11-252">**描述**：叢集 DNS 名稱 *yourDnsClusterName* 無效。</span><span class="sxs-lookup"><span data-stu-id="61c11-252">**Description**: Cluster DNS name *yourDnsClusterName* is invalid.</span></span> <span data-ttu-id="61c11-253">請確定名稱以英數字元開始和結束，且只包含 '-' 特殊字元</span><span class="sxs-lookup"><span data-stu-id="61c11-253">Please ensure name starts and ends with alphanumeric and can only contain '-' special character</span></span>  
* <span data-ttu-id="61c11-254">**緩和**：請提供有效的 DNS 使用者名稱，然後重試作業。</span><span class="sxs-lookup"><span data-stu-id="61c11-254">**Mitigation**: Provide a valid DNS cluster username and retry the operation.</span></span>

### <span data-ttu-id="61c11-255"><a id="ContainerNameMisMatchWithDnsName"></a>ContainerNameMisMatchWithDnsName</span><span class="sxs-lookup"><span data-stu-id="61c11-255"><a id="ContainerNameMisMatchWithDnsName"></a>ContainerNameMisMatchWithDnsName</span></span>
* <span data-ttu-id="61c11-256">**描述**：URI「yourcontainerURI」中的容器名稱和要求內文中的 DNS 名稱「yourDnsName」必須相同。</span><span class="sxs-lookup"><span data-stu-id="61c11-256">**Description**: Container name in URI *yourcontainerURI* and DNS name *yourDnsName* in request body must be the same.</span></span>  
* <span data-ttu-id="61c11-257">**緩和**：請確定容器名稱和 DNS 名稱相同，然後重試作業。</span><span class="sxs-lookup"><span data-stu-id="61c11-257">**Mitigation**: Make sure that your container Name and your DNS name are the same and retry the operation.</span></span>

### <span data-ttu-id="61c11-258"><a id="DataNodeDefinitionNotFound"></a>DataNodeDefinitionNotFound</span><span class="sxs-lookup"><span data-stu-id="61c11-258"><a id="DataNodeDefinitionNotFound"></a>DataNodeDefinitionNotFound</span></span>
* <span data-ttu-id="61c11-259">**描述**：叢集組態無效。</span><span class="sxs-lookup"><span data-stu-id="61c11-259">**Description**: Invalid cluster configuration.</span></span> <span data-ttu-id="61c11-260">在節點大小中找不到任何資料節點定義。</span><span class="sxs-lookup"><span data-stu-id="61c11-260">Unable to find any data node definitions in node size.</span></span>  
* <span data-ttu-id="61c11-261">**緩和**：重試作業。</span><span class="sxs-lookup"><span data-stu-id="61c11-261">**Mitigation**: Retry the operation.</span></span>

### <span data-ttu-id="61c11-262"><a id="DeploymentDeletionFailure"></a>DeploymentDeletionFailure</span><span class="sxs-lookup"><span data-stu-id="61c11-262"><a id="DeploymentDeletionFailure"></a>DeploymentDeletionFailure</span></span>
* <span data-ttu-id="61c11-263">**描述**：刪除叢集的部署失敗。</span><span class="sxs-lookup"><span data-stu-id="61c11-263">**Description**: Deletion of deployment failed for the Cluster</span></span>  
* <span data-ttu-id="61c11-264">**緩和**：重試刪除作業。</span><span class="sxs-lookup"><span data-stu-id="61c11-264">**Mitigation**: Retry the delete operation.</span></span>

### <span data-ttu-id="61c11-265"><a id="DnsMappingNotFound"></a>DnsMappingNotFound</span><span class="sxs-lookup"><span data-stu-id="61c11-265"><a id="DnsMappingNotFound"></a>DnsMappingNotFound</span></span>
* <span data-ttu-id="61c11-266">**描述**：服務組態錯誤。</span><span class="sxs-lookup"><span data-stu-id="61c11-266">**Description**: Service configuration error.</span></span> <span data-ttu-id="61c11-267">找不到必要的 DNS 對應資訊。</span><span class="sxs-lookup"><span data-stu-id="61c11-267">Required DNS mapping information not found.</span></span>  
* <span data-ttu-id="61c11-268">**緩和**：刪除叢集，然後建立新的叢集。</span><span class="sxs-lookup"><span data-stu-id="61c11-268">**Mitigation**: Delete cluster and create a new cluster.</span></span>

### <span data-ttu-id="61c11-269"><a id="DuplicateClusterContainerRequest"></a>DuplicateClusterContainerRequest</span><span class="sxs-lookup"><span data-stu-id="61c11-269"><a id="DuplicateClusterContainerRequest"></a>DuplicateClusterContainerRequest</span></span>
* <span data-ttu-id="61c11-270">**描述**：嘗試建立重複的叢集容器。</span><span class="sxs-lookup"><span data-stu-id="61c11-270">**Description**: Duplicate cluster container creation attempt.</span></span> <span data-ttu-id="61c11-271">已存在 *nameOfYourContainer* 的記錄，但 Etag 不符。</span><span class="sxs-lookup"><span data-stu-id="61c11-271">Record exists for *nameOfYourContainer* but Etags do not match.</span></span>
* <span data-ttu-id="61c11-272">**緩和**：請提供容器的唯一名稱，然後重試建立作業。</span><span class="sxs-lookup"><span data-stu-id="61c11-272">**Mitigation**: Provide a unique name for the container and retry the create operation.</span></span>

### <span data-ttu-id="61c11-273"><a id="DuplicateClusterInHostedService"></a>DuplicateClusterInHostedService</span><span class="sxs-lookup"><span data-stu-id="61c11-273"><a id="DuplicateClusterInHostedService"></a>DuplicateClusterInHostedService</span></span>
* <span data-ttu-id="61c11-274">**描述**：代管服務 *nameOfYourHostedService* 已包含叢集。</span><span class="sxs-lookup"><span data-stu-id="61c11-274">**Description**: Hosted service *nameOfYourHostedService* already contains a cluster.</span></span> <span data-ttu-id="61c11-275">代管服務不可包含多個叢集</span><span class="sxs-lookup"><span data-stu-id="61c11-275">A hosted service cannot contain multiple clusters</span></span>  
* <span data-ttu-id="61c11-276">**緩和**：將叢集裝載於其他代管服務中。</span><span class="sxs-lookup"><span data-stu-id="61c11-276">**Mitigation**: Host the cluster in another hosted service.</span></span>

### <span data-ttu-id="61c11-277"><a id="FailureToUpdateDeploymentStatus"></a>FailureToUpdateDeploymentStatus</span><span class="sxs-lookup"><span data-stu-id="61c11-277"><a id="FailureToUpdateDeploymentStatus"></a>FailureToUpdateDeploymentStatus</span></span>
* <span data-ttu-id="61c11-278">**描述**：伺服器無法更新叢集部署的狀態。</span><span class="sxs-lookup"><span data-stu-id="61c11-278">**Description**: The server could not update the state of the cluster deployment.</span></span>  
* <span data-ttu-id="61c11-279">**緩和**：重試作業。</span><span class="sxs-lookup"><span data-stu-id="61c11-279">**Mitigation**: Retry the operation.</span></span> <span data-ttu-id="61c11-280">如果此情況發生多次，請連絡 CSS。</span><span class="sxs-lookup"><span data-stu-id="61c11-280">If this happens multiple times, contact CSS.</span></span>

### <span data-ttu-id="61c11-281"><a id="HdiRestoreClusterAltered"></a>HdiRestoreClusterAltered</span><span class="sxs-lookup"><span data-stu-id="61c11-281"><a id="HdiRestoreClusterAltered"></a>HdiRestoreClusterAltered</span></span>
* <span data-ttu-id="61c11-282">**描述**：維護時已刪除叢集 *yourClusterName* 。</span><span class="sxs-lookup"><span data-stu-id="61c11-282">**Description**: Cluster *yourClusterName* was deleted as part of maintenance.</span></span> <span data-ttu-id="61c11-283">請重新建立叢集。</span><span class="sxs-lookup"><span data-stu-id="61c11-283">Please recreate the cluster.</span></span>
* <span data-ttu-id="61c11-284">**緩和**：重新建立叢集。</span><span class="sxs-lookup"><span data-stu-id="61c11-284">**Mitigation**: Recreate the cluster.</span></span>

### <span data-ttu-id="61c11-285"><a id="HeadNodeConfigNotFound"></a>HeadNodeConfigNotFound</span><span class="sxs-lookup"><span data-stu-id="61c11-285"><a id="HeadNodeConfigNotFound"></a>HeadNodeConfigNotFound</span></span>
* <span data-ttu-id="61c11-286">**描述**：叢集組態無效。</span><span class="sxs-lookup"><span data-stu-id="61c11-286">**Description**: Invalid cluster configuration.</span></span> <span data-ttu-id="61c11-287">在節點大小中找不到必要的前端節點組態。</span><span class="sxs-lookup"><span data-stu-id="61c11-287">Required head node configuration not found in node sizes.</span></span>
* <span data-ttu-id="61c11-288">**緩和**：重試作業。</span><span class="sxs-lookup"><span data-stu-id="61c11-288">**Mitigation**: Retry the operation.</span></span>

### <span data-ttu-id="61c11-289"><a id="HostedServiceCreationFailure"></a>HostedServiceCreationFailure</span><span class="sxs-lookup"><span data-stu-id="61c11-289"><a id="HostedServiceCreationFailure"></a>HostedServiceCreationFailure</span></span>
* <span data-ttu-id="61c11-290">**描述**：無法建立代管服務 *nameOfYourHostedService*。</span><span class="sxs-lookup"><span data-stu-id="61c11-290">**Description**: Unable to create hosted service *nameOfYourHostedService*.</span></span> <span data-ttu-id="61c11-291">請重試要求。</span><span class="sxs-lookup"><span data-stu-id="61c11-291">Please retry request.</span></span>  
* <span data-ttu-id="61c11-292">**緩和**：重試要求。</span><span class="sxs-lookup"><span data-stu-id="61c11-292">**Mitigation**: Retry the request.</span></span>

### <span data-ttu-id="61c11-293"><a id="HostedServiceHasProductionDeployment"></a>HostedServiceHasProductionDeployment</span><span class="sxs-lookup"><span data-stu-id="61c11-293"><a id="HostedServiceHasProductionDeployment"></a>HostedServiceHasProductionDeployment</span></span>
* <span data-ttu-id="61c11-294">**描述**：託管服務「nameOfYourHostedService」已有生產部署。</span><span class="sxs-lookup"><span data-stu-id="61c11-294">**Description**: Hosted Service *nameOfYourHostedService* already has a production deployment.</span></span> <span data-ttu-id="61c11-295">代管服務不可包含多個生產部署</span><span class="sxs-lookup"><span data-stu-id="61c11-295">A hosted service cannot contain multiple production deployments.</span></span> <span data-ttu-id="61c11-296">請以不同的叢集名稱來重試要求。</span><span class="sxs-lookup"><span data-stu-id="61c11-296">Retry the request with a different cluster name.</span></span>
* <span data-ttu-id="61c11-297">**緩和**：請使用不同的叢集名稱，然後重試要求。</span><span class="sxs-lookup"><span data-stu-id="61c11-297">**Mitigation**: Use a different cluster name and retry the request.</span></span>

### <span data-ttu-id="61c11-298"><a id="HostedServiceNotFound"></a>HostedServiceNotFound</span><span class="sxs-lookup"><span data-stu-id="61c11-298"><a id="HostedServiceNotFound"></a>HostedServiceNotFound</span></span>
* <span data-ttu-id="61c11-299">**描述**：找不到叢集的代管服務 *nameOfYourHostedService* 。</span><span class="sxs-lookup"><span data-stu-id="61c11-299">**Description**: Hosted Service *nameOfYourHostedService* for the cluster could not be found.</span></span>  
* <span data-ttu-id="61c11-300">**緩和**：如果叢集處於錯誤狀態，請刪除叢集，然後再試一次。</span><span class="sxs-lookup"><span data-stu-id="61c11-300">**Mitigation**: If the cluster is in error state, delete it and then try again.</span></span>

### <span data-ttu-id="61c11-301"><a id="HostedServiceWithNoDeployment"></a>HostedServiceWithNoDeployment</span><span class="sxs-lookup"><span data-stu-id="61c11-301"><a id="HostedServiceWithNoDeployment"></a>HostedServiceWithNoDeployment</span></span>
* <span data-ttu-id="61c11-302">**描述**：代管服務 *nameOfYourHostedService* 沒有相關聯的部署。</span><span class="sxs-lookup"><span data-stu-id="61c11-302">**Description**: Hosted Service *nameOfYourHostedService* has no associated deployment.</span></span>  
* <span data-ttu-id="61c11-303">**緩和**：如果叢集處於錯誤狀態，請刪除叢集，然後再試一次。</span><span class="sxs-lookup"><span data-stu-id="61c11-303">**Mitigation**: If the cluster is in error state, delete it and then try again.</span></span>

### <span data-ttu-id="61c11-304"><a id="InsufficientResourcesCores"></a>InsufficientResourcesCores</span><span class="sxs-lookup"><span data-stu-id="61c11-304"><a id="InsufficientResourcesCores"></a>InsufficientResourcesCores</span></span>
* <span data-ttu-id="61c11-305">**描述**：SubscriptionId「yourSubscriptionId」沒有剩餘的核心可建立叢集「yourClusterName」。</span><span class="sxs-lookup"><span data-stu-id="61c11-305">**Description**: The SubscriptionId *yourSubscriptionId* does not have cores left to create cluster *yourClusterName*.</span></span> <span data-ttu-id="61c11-306">必要：「resourcesRequired」、可用：「resourcesAvailable」。</span><span class="sxs-lookup"><span data-stu-id="61c11-306">Required: *resourcesRequired*, Available: *resourcesAvailable*.</span></span>  
* <span data-ttu-id="61c11-307">**緩和**：釋出訂用帳戶中的資源，或增加可供訂用帳戶的資源，然後重試建立叢集。</span><span class="sxs-lookup"><span data-stu-id="61c11-307">**Mitigation**: Free up resources in your subscription or increase the resources available to the subscription and try to create the cluster again.</span></span>

### <span data-ttu-id="61c11-308"><a id="InsufficientResourcesHostedServices"></a>InsufficientResourcesHostedServices</span><span class="sxs-lookup"><span data-stu-id="61c11-308"><a id="InsufficientResourcesHostedServices"></a>InsufficientResourcesHostedServices</span></span>
* <span data-ttu-id="61c11-309">**描述**：訂用帳戶識別碼「yourSubscriptionId」沒有配額可供新的 HostedService 建立叢集「yourClusterName」。</span><span class="sxs-lookup"><span data-stu-id="61c11-309">**Description**: Subscription ID *yourSubscriptionId* does not have quota for a new HostedService to create cluster *yourClusterName*.</span></span>  
* <span data-ttu-id="61c11-310">**緩和**：釋出訂用帳戶中的資源，或增加可供訂用帳戶的資源，然後重試建立叢集。</span><span class="sxs-lookup"><span data-stu-id="61c11-310">**Mitigation**: Free up resources in your subscription or increase the resources available to the subscription and try to create the cluster again.</span></span>

### <span data-ttu-id="61c11-311"><a id="InternalErrorRetryRequest"></a>InternalErrorRetryRequest</span><span class="sxs-lookup"><span data-stu-id="61c11-311"><a id="InternalErrorRetryRequest"></a>InternalErrorRetryRequest</span></span>
* <span data-ttu-id="61c11-312">**描述**：伺服器發生內部錯誤。</span><span class="sxs-lookup"><span data-stu-id="61c11-312">**Description**: The server encountered an internal error.</span></span> <span data-ttu-id="61c11-313">請重試要求。</span><span class="sxs-lookup"><span data-stu-id="61c11-313">Please retry request.</span></span>  
* <span data-ttu-id="61c11-314">**緩和**：重試要求。</span><span class="sxs-lookup"><span data-stu-id="61c11-314">**Mitigation**: Retry the request.</span></span>

### <span data-ttu-id="61c11-315"><a id="InvalidAzureStorageLocation"></a>InvalidAzureStorageLocation</span><span class="sxs-lookup"><span data-stu-id="61c11-315"><a id="InvalidAzureStorageLocation"></a>InvalidAzureStorageLocation</span></span>
* <span data-ttu-id="61c11-316">**描述**：Azure 儲存體位置 *dataRegionName* 不是有效的位置。</span><span class="sxs-lookup"><span data-stu-id="61c11-316">**Description**: Azure Storage location *dataRegionName* is not a valid location.</span></span> <span data-ttu-id="61c11-317">請確定區域正確，然後重試要求。</span><span class="sxs-lookup"><span data-stu-id="61c11-317">Make sure the region is correct and retry request.</span></span>
* <span data-ttu-id="61c11-318">**緩和**：請選取支援 HDInsight 的儲存體位置，檢查您的叢集已並存，然後重試作業。</span><span class="sxs-lookup"><span data-stu-id="61c11-318">**Mitigation**: Select a Storage location that supports HDInsight, check that your cluster is co-located and retry the operation.</span></span>

### <span data-ttu-id="61c11-319"><a id="InvalidNodeSizeForDataNode"></a>InvalidNodeSizeForDataNode</span><span class="sxs-lookup"><span data-stu-id="61c11-319"><a id="InvalidNodeSizeForDataNode"></a>InvalidNodeSizeForDataNode</span></span>
* <span data-ttu-id="61c11-320">**描述**：資源節點的 VM 大小無效。</span><span class="sxs-lookup"><span data-stu-id="61c11-320">**Description**: Invalid VM size for data nodes.</span></span> <span data-ttu-id="61c11-321">所有資料節點僅支援 'Large VM' 大小。</span><span class="sxs-lookup"><span data-stu-id="61c11-321">Only 'Large VM' size is supported for all data nodes.</span></span>  
* <span data-ttu-id="61c11-322">**緩和**：請為資料節點指定支援的節點大小，然後重試作業。</span><span class="sxs-lookup"><span data-stu-id="61c11-322">**Mitigation**: Specify the supported node size for the data node and retry the operation.</span></span>

### <span data-ttu-id="61c11-323"><a id="InvalidNodeSizeForHeadNode"></a>InvalidNodeSizeForHeadNode</span><span class="sxs-lookup"><span data-stu-id="61c11-323"><a id="InvalidNodeSizeForHeadNode"></a>InvalidNodeSizeForHeadNode</span></span>
* <span data-ttu-id="61c11-324">**描述**：前端節點的 VM 大小無效。</span><span class="sxs-lookup"><span data-stu-id="61c11-324">**Description**: Invalid VM size for head node.</span></span> <span data-ttu-id="61c11-325">前端節點僅支援 'ExtraLarge VM' 大小。</span><span class="sxs-lookup"><span data-stu-id="61c11-325">Only 'ExtraLarge VM' size is supported for head node.</span></span>  
* <span data-ttu-id="61c11-326">**緩和**：請為前端節點指定支援的節點大小，然後重試作業。</span><span class="sxs-lookup"><span data-stu-id="61c11-326">**Mitigation**: Specify the supported node size for the head node and retry the operation</span></span>

### <span data-ttu-id="61c11-327"><a id="InvalidRightsForDeploymentDeletion"></a>InvalidRightsForDeploymentDeletion</span><span class="sxs-lookup"><span data-stu-id="61c11-327"><a id="InvalidRightsForDeploymentDeletion"></a>InvalidRightsForDeploymentDeletion</span></span>
* <span data-ttu-id="61c11-328">**描述**：使用的訂用帳戶識別碼「yourSubscriptionId」權限不足，無法對叢集「yourClusterName」執行刪除作業。</span><span class="sxs-lookup"><span data-stu-id="61c11-328">**Description**: Subscription ID *yourSubscriptionId* being used does not have sufficient permissions to execute delete operation for cluster *yourClusterName*.</span></span>  
* <span data-ttu-id="61c11-329">**緩和**：如果叢集處於錯誤狀態，請卸除叢集，然後再試一次。</span><span class="sxs-lookup"><span data-stu-id="61c11-329">**Mitigation**: If the cluster is in error state, drop it and then try again.</span></span>  

### <span data-ttu-id="61c11-330"><a id="InvalidStorageAccountBlobContainerName"></a>InvalidStorageAccountBlobContainerName</span><span class="sxs-lookup"><span data-stu-id="61c11-330"><a id="InvalidStorageAccountBlobContainerName"></a>InvalidStorageAccountBlobContainerName</span></span>
* <span data-ttu-id="61c11-331">**描述**：外部儲存帳戶 Blob 容器名稱 *yourContainerName* 無效。</span><span class="sxs-lookup"><span data-stu-id="61c11-331">**Description**: External storage account blob container name *yourContainerName* is invalid.</span></span> <span data-ttu-id="61c11-332">請確定名稱以字母開頭，且只包含小寫字母、數字和虛線。</span><span class="sxs-lookup"><span data-stu-id="61c11-332">Make sure name starts with a letter and contains only lowercase letters, numbers and dash.</span></span>  
* <span data-ttu-id="61c11-333">**緩和**：請指定有效的儲存體帳戶 Blob 容器名稱，然後重試作業。</span><span class="sxs-lookup"><span data-stu-id="61c11-333">**Mitigation**: Specify a valid storage account blob container name and retry the operation.</span></span>

### <span data-ttu-id="61c11-334"><a id="InvalidStorageAccountConfigurationSecretKey"></a>InvalidStorageAccountConfigurationSecretKey</span><span class="sxs-lookup"><span data-stu-id="61c11-334"><a id="InvalidStorageAccountConfigurationSecretKey"></a>InvalidStorageAccountConfigurationSecretKey</span></span>
* <span data-ttu-id="61c11-335">**描述**：需要有密碼詳細資料，才能設定外部儲存體帳戶 *yourStorageAccountName* 的組態。</span><span class="sxs-lookup"><span data-stu-id="61c11-335">**Description**: Configuration for external storage account *yourStorageAccountName* is required to have secret key details to be set.</span></span>  
* <span data-ttu-id="61c11-336">**緩和**：請為儲存體帳戶指定有效的密碼，然後重試作業。</span><span class="sxs-lookup"><span data-stu-id="61c11-336">**Mitigation**: Specify a valid secret key for the storage account and retry the operation.</span></span>

### <span data-ttu-id="61c11-337"><a id="InvalidVersionHeaderFormat"></a>InvalidVersionHeaderFormat</span><span class="sxs-lookup"><span data-stu-id="61c11-337"><a id="InvalidVersionHeaderFormat"></a>InvalidVersionHeaderFormat</span></span>
* <span data-ttu-id="61c11-338">**描述**：版本標頭 *yourVersionHeader* 不是有效格式 yyyy-mm-dd。</span><span class="sxs-lookup"><span data-stu-id="61c11-338">**Description**: Version header *yourVersionHeader* is not in valid format of yyyy-mm-dd.</span></span>  
* <span data-ttu-id="61c11-339">**緩和**：請為版本標頭指定有效格式，然後重試要求。</span><span class="sxs-lookup"><span data-stu-id="61c11-339">**Mitigation**: Specify a valid format for the version-header and retry the request.</span></span>

### <span data-ttu-id="61c11-340"><a id="MoreThanOneHeadNode"></a>MoreThanOneHeadNode</span><span class="sxs-lookup"><span data-stu-id="61c11-340"><a id="MoreThanOneHeadNode"></a>MoreThanOneHeadNode</span></span>
* <span data-ttu-id="61c11-341">**描述**：叢集組態無效。</span><span class="sxs-lookup"><span data-stu-id="61c11-341">**Description**: Invalid cluster configuration.</span></span> <span data-ttu-id="61c11-342">發現多個前端節點組態。</span><span class="sxs-lookup"><span data-stu-id="61c11-342">Found more than one head node configuration.</span></span>  
* <span data-ttu-id="61c11-343">**緩和**：請編輯組態，僅指定一個前端節點。</span><span class="sxs-lookup"><span data-stu-id="61c11-343">**Mitigation**: Edit the configuration so that only one head node is specified.</span></span>

### <span data-ttu-id="61c11-344"><a id="OperationTimedOutRetryRequest"></a>OperationTimedOutRetryRequest</span><span class="sxs-lookup"><span data-stu-id="61c11-344"><a id="OperationTimedOutRetryRequest"></a>OperationTimedOutRetryRequest</span></span>
* <span data-ttu-id="61c11-345">**描述**：無法於允許的時間內完成作業，或已達到重試次數上限。</span><span class="sxs-lookup"><span data-stu-id="61c11-345">**Description**: The operation could not be completed within the permitted time or the maximum retry attempts possible.</span></span> <span data-ttu-id="61c11-346">請重試要求。</span><span class="sxs-lookup"><span data-stu-id="61c11-346">Please retry request.</span></span>  
* <span data-ttu-id="61c11-347">**緩和**：重試要求。</span><span class="sxs-lookup"><span data-stu-id="61c11-347">**Mitigation**: Retry the request.</span></span>

### <span data-ttu-id="61c11-348"><a id="ParameterNullOrEmpty"></a>ParameterNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="61c11-348"><a id="ParameterNullOrEmpty"></a>ParameterNullOrEmpty</span></span>
* <span data-ttu-id="61c11-349">**描述**：參數 *yourParameterName* 不可為 Null 或空白。</span><span class="sxs-lookup"><span data-stu-id="61c11-349">**Description**: Parameter *yourParameterName* cannot be null or empty.</span></span>  
* <span data-ttu-id="61c11-350">**緩和**：請為參數指定有效值。</span><span class="sxs-lookup"><span data-stu-id="61c11-350">**Mitigation**: Specify a valid value for the parameter.</span></span>

### <span data-ttu-id="61c11-351"><a id="PreClusterCreationValidationFailure"></a>PreClusterCreationValidationFailure</span><span class="sxs-lookup"><span data-stu-id="61c11-351"><a id="PreClusterCreationValidationFailure"></a>PreClusterCreationValidationFailure</span></span>
* <span data-ttu-id="61c11-352">**描述**：一或多個叢集建立要求輸入無效。</span><span class="sxs-lookup"><span data-stu-id="61c11-352">**Description**: One or more of the cluster creation request inputs is not valid.</span></span> <span data-ttu-id="61c11-353">請確定輸入值正確，然後重試要求。</span><span class="sxs-lookup"><span data-stu-id="61c11-353">Make sure the input values are correct and retry request.</span></span>  
* <span data-ttu-id="61c11-354">**緩和**：請確定輸入值正確，然後重試要求。</span><span class="sxs-lookup"><span data-stu-id="61c11-354">**Mitigation**: Make sure the input values are correct and retry request.</span></span>

### <span data-ttu-id="61c11-355"><a id="RegionCapabilityNotAvailable"></a>RegionCapabilityNotAvailable</span><span class="sxs-lookup"><span data-stu-id="61c11-355"><a id="RegionCapabilityNotAvailable"></a>RegionCapabilityNotAvailable</span></span>
* <span data-ttu-id="61c11-356">**描述**：區域「yourRegionName」和訂用帳戶識別碼「yourSubscriptionId」無法使用區域功能。</span><span class="sxs-lookup"><span data-stu-id="61c11-356">**Description**: Region capability not available for region *yourRegionName* and Subscription ID *yourSubscriptionId*.</span></span>  
* <span data-ttu-id="61c11-357">**緩和**：請指定支援 HDInsight 叢集的區域。</span><span class="sxs-lookup"><span data-stu-id="61c11-357">**Mitigation**: Specify a region that supports HDInsight clusters.</span></span> <span data-ttu-id="61c11-358">公開支援的區域為：東南亞、西歐、北歐、美國東部或美國西部。</span><span class="sxs-lookup"><span data-stu-id="61c11-358">The publicly supported regions are: Southeast Asia, West Europe, North Europe, East US, or West US.</span></span>

### <span data-ttu-id="61c11-359"><a id="StorageAccountNotColocated"></a>StorageAccountNotColocated</span><span class="sxs-lookup"><span data-stu-id="61c11-359"><a id="StorageAccountNotColocated"></a>StorageAccountNotColocated</span></span>
* <span data-ttu-id="61c11-360">**描述**：儲存體帳戶「yourStorageAccountName」位於區域「currentRegionName」中。</span><span class="sxs-lookup"><span data-stu-id="61c11-360">**Description**: Storage account *yourStorageAccountName* is in region *currentRegionName*.</span></span> <span data-ttu-id="61c11-361">必須與叢集區域 *yourClusterRegionName*相同。</span><span class="sxs-lookup"><span data-stu-id="61c11-361">It should be same as the cluster region *yourClusterRegionName*.</span></span>  
* <span data-ttu-id="61c11-362">**緩和**：請指定您的叢集所在相同區域中的儲存體帳戶，或者，如果您的資料已在儲存帳戶中，請在現有儲存體帳戶所在的相同區域中建立新的叢集。</span><span class="sxs-lookup"><span data-stu-id="61c11-362">**Mitigation**: Either specify a storage account in the same region that your cluster is in or if your data is already in the storage account, create a new cluster in the same region as the existing storage account.</span></span> <span data-ttu-id="61c11-363">如果您在使用入口網站，UI 會事先通知此問題。</span><span class="sxs-lookup"><span data-stu-id="61c11-363">If you are using the Portal, the UI will notify them of this issue in advance.</span></span>

### <span data-ttu-id="61c11-364"><a id="SubscriptionIdNotActive"></a>SubscriptionIdNotActive</span><span class="sxs-lookup"><span data-stu-id="61c11-364"><a id="SubscriptionIdNotActive"></a>SubscriptionIdNotActive</span></span>
* <span data-ttu-id="61c11-365">**描述**：並未使用指定的訂用帳戶識別碼 *yourSubscriptionId* 。</span><span class="sxs-lookup"><span data-stu-id="61c11-365">**Description**: Given Subscription ID *yourSubscriptionId* is not active.</span></span>  
* <span data-ttu-id="61c11-366">**緩和**：請重新啟用訂用帳戶，或取得新的有效訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="61c11-366">**Mitigation**: Re-activate your subscription or get a new valid subscription.</span></span>

### <span data-ttu-id="61c11-367"><a id="SubscriptionIdNotFound"></a>SubscriptionIdNotFound</span><span class="sxs-lookup"><span data-stu-id="61c11-367"><a id="SubscriptionIdNotFound"></a>SubscriptionIdNotFound</span></span>
* <span data-ttu-id="61c11-368">**描述**：找不到訂用帳戶識別碼 *yourSubscriptionId* 。</span><span class="sxs-lookup"><span data-stu-id="61c11-368">**Description**: Subscription ID *yourSubscriptionId* could not be found.</span></span>  
* <span data-ttu-id="61c11-369">**緩和**：請檢查訂用帳戶識別碼有效，然後重試作業。</span><span class="sxs-lookup"><span data-stu-id="61c11-369">**Mitigation**: Check that your subscription ID is valid and retry the operation.</span></span>

### <span data-ttu-id="61c11-370"><a id="UnableToResolveDNS"></a>UnableToResolveDNS</span><span class="sxs-lookup"><span data-stu-id="61c11-370"><a id="UnableToResolveDNS"></a>UnableToResolveDNS</span></span>
* <span data-ttu-id="61c11-371">**描述**：無法解析 DNS *yourDnsUrl*。</span><span class="sxs-lookup"><span data-stu-id="61c11-371">**Description**: Unable to resolve DNS *yourDnsUrl*.</span></span> <span data-ttu-id="61c11-372">請確定您提供 Blob 端點的完整 URL。</span><span class="sxs-lookup"><span data-stu-id="61c11-372">Please ensure the fully qualified URL for the blob endpoint is provided.</span></span>  
* <span data-ttu-id="61c11-373">**緩和**：提供有效的 Blob URL。</span><span class="sxs-lookup"><span data-stu-id="61c11-373">**Mitigation**: Supply a valid blob URL.</span></span> <span data-ttu-id="61c11-374">URL「必須」完全有效，包括以*http://*開頭，以*.com*結尾。</span><span class="sxs-lookup"><span data-stu-id="61c11-374">The URL MUST be fully valid, including starting with *http://* and ending in *.com*.</span></span>

### <span data-ttu-id="61c11-375"><a id="UnableToVerifyLocationOfResource"></a>UnableToVerifyLocationOfResource</span><span class="sxs-lookup"><span data-stu-id="61c11-375"><a id="UnableToVerifyLocationOfResource"></a>UnableToVerifyLocationOfResource</span></span>
* <span data-ttu-id="61c11-376">**描述**：無法驗證資源的 *yourDnsUrl*的位置。</span><span class="sxs-lookup"><span data-stu-id="61c11-376">**Description**: Unable to verify location of resource *yourDnsUrl*.</span></span> <span data-ttu-id="61c11-377">請確定您提供 Blob 端點的完整 URL。</span><span class="sxs-lookup"><span data-stu-id="61c11-377">Please ensure the fully qualified URL for the blob endpoint is provided.</span></span>  
* <span data-ttu-id="61c11-378">**緩和**：提供有效的 Blob URL。</span><span class="sxs-lookup"><span data-stu-id="61c11-378">**Mitigation**: Supply a valid blob URL.</span></span> <span data-ttu-id="61c11-379">URL「必須」完全有效，包括以*http://*開頭，以*.com*結尾。</span><span class="sxs-lookup"><span data-stu-id="61c11-379">The URL MUST be fully valid, including starting with *http://* and ending in *.com*.</span></span>

### <span data-ttu-id="61c11-380"><a id="VersionCapabilityNotAvailable"></a>VersionCapabilityNotAvailable</span><span class="sxs-lookup"><span data-stu-id="61c11-380"><a id="VersionCapabilityNotAvailable"></a>VersionCapabilityNotAvailable</span></span>
* <span data-ttu-id="61c11-381">**描述**：版本「specifiedVersion」和訂用帳戶識別碼「yourSubscriptionId」無法使用版本功能。</span><span class="sxs-lookup"><span data-stu-id="61c11-381">**Description**: Version capability not available for version *specifiedVersion* and Subscription ID *yourSubscriptionId*.</span></span>  
* <span data-ttu-id="61c11-382">**緩和**：請選擇可用的版本，然後重試作業。</span><span class="sxs-lookup"><span data-stu-id="61c11-382">**Mitigation**: Choose a version that is available and retry the operation.</span></span>

### <span data-ttu-id="61c11-383"><a id="VersionNotSupported"></a>VersionNotSupported</span><span class="sxs-lookup"><span data-stu-id="61c11-383"><a id="VersionNotSupported"></a>VersionNotSupported</span></span>
* <span data-ttu-id="61c11-384">**描述**：不支援版本 *specifiedVersion* 。</span><span class="sxs-lookup"><span data-stu-id="61c11-384">**Description**: Version *specifiedVersion* not supported.</span></span>
* <span data-ttu-id="61c11-385">**緩和**：請選擇支援的版本，然後重試作業。</span><span class="sxs-lookup"><span data-stu-id="61c11-385">**Mitigation**: Choose a version that is supported and retry the operation.</span></span>

### <span data-ttu-id="61c11-386"><a id="VersionNotSupportedInRegion"></a>VersionNotSupportedInRegion</span><span class="sxs-lookup"><span data-stu-id="61c11-386"><a id="VersionNotSupportedInRegion"></a>VersionNotSupportedInRegion</span></span>
* <span data-ttu-id="61c11-387">**描述**：Azure 區域「specifiedRegion」中無法使用版本「specifiedVersion」。</span><span class="sxs-lookup"><span data-stu-id="61c11-387">**Description**: Version *specifiedVersion* is not available in Azure region *specifiedRegion*.</span></span>  
* <span data-ttu-id="61c11-388">**緩和**：請選擇指定區域中支援的版本，然後重試作業。</span><span class="sxs-lookup"><span data-stu-id="61c11-388">**Mitigation**: Choose a version that is supported in the region specified and retry the operation.</span></span>

### <span data-ttu-id="61c11-389"><a id="WasbAccountConfigNotFound"></a>WasbAccountConfigNotFound</span><span class="sxs-lookup"><span data-stu-id="61c11-389"><a id="WasbAccountConfigNotFound"></a>WasbAccountConfigNotFound</span></span>
* <span data-ttu-id="61c11-390">**描述**：叢集組態無效。</span><span class="sxs-lookup"><span data-stu-id="61c11-390">**Description**: Invalid cluster configuration.</span></span> <span data-ttu-id="61c11-391">在外部帳戶中找不到必要的 WASB 帳戶組態。</span><span class="sxs-lookup"><span data-stu-id="61c11-391">Required WASB account configuration not found in external accounts.</span></span>  
* <span data-ttu-id="61c11-392">**緩和**：請驗證帳戶已存在且於組態中指定正確，然後重試作業。</span><span class="sxs-lookup"><span data-stu-id="61c11-392">**Mitigation**: Verify that the account exists and is properly specified in configuration and retry the operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="61c11-393">後續步驟</span><span class="sxs-lookup"><span data-stu-id="61c11-393">Next steps</span></span>
* [<span data-ttu-id="61c11-394">在 HDInsight 上使用 Ambari 檢視來為 Tez 作業偵錯</span><span class="sxs-lookup"><span data-stu-id="61c11-394">Use Ambari Views to debug Tez Jobs on HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)
* [<span data-ttu-id="61c11-395">在 Linux 型 HDInsight 上啟用 Hadoop 服務的堆積傾印</span><span class="sxs-lookup"><span data-stu-id="61c11-395">Enable heap dumps for Hadoop services on Linux-based HDInsight</span></span>](hdinsight-hadoop-collect-debug-heap-dump-linux.md)
* [<span data-ttu-id="61c11-396">使用 Ambari Web UI 管理 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="61c11-396">Manage HDInsight clusters by using the Ambari Web UI</span></span>](hdinsight-hadoop-manage-ambari.md)

