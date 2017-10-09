---
title: "針對 HDInsight 上的 Hadoop 進行偵錯：檢視記錄與解譯錯誤訊息 - Azure | Microsoft Docs"
description: "深入了解管理 HDInsight PowerShell 及步驟可讓您 toorecover 使用時，您可能會收到 hello 錯誤訊息。"
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
ms.openlocfilehash: 2f12a40e9dcac32ce2e11d66d60d8b3b212ecb53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-hdinsight-logs"></a><span data-ttu-id="b5b9c-103">分析 HDInsight 記錄檔</span><span class="sxs-lookup"><span data-stu-id="b5b9c-103">Analyze HDInsight logs</span></span>
<span data-ttu-id="b5b9c-104">Azure HDInsight 中的每個 Hadoop 叢集具有做為 hello 預設的檔案系統的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-104">Each Hadoop cluster in Azure HDInsight has an Azure storage account used as hello default file system.</span></span> <span data-ttu-id="b5b9c-105">hello 儲存體帳戶會稱為 hello 預設儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-105">hello storage account is referred as hello default Storage account.</span></span> <span data-ttu-id="b5b9c-106">叢集將使用 hello Azure 資料表儲存體和 hello Blob 儲存體 hello 預設儲存體帳戶 toostore 上其記錄檔。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-106">Cluster uses hello Azure Table storage and hello Blob storage on hello default Storage account toostore its logs.</span></span>  <span data-ttu-id="b5b9c-107">toofind 出 hello 預設儲存體帳戶用於您的叢集，請參閱[在 HDInsight 中的管理 Hadoop 叢集](hdinsight-administer-use-management-portal.md#find-the-default-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-107">toofind out hello default storage account for your cluster, see [Manage Hadoop clusters in HDInsight](hdinsight-administer-use-management-portal.md#find-the-default-storage-account).</span></span> <span data-ttu-id="b5b9c-108">hello 記錄檔會保留 hello 儲存體帳戶，即使 hello 叢集刪除。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-108">hello logs retain in hello Storage account even after hello cluster is deleted.</span></span>

## <a name="logs-written-tooazure-tables"></a><span data-ttu-id="b5b9c-109">記錄寫入 tooAzure 資料表</span><span class="sxs-lookup"><span data-stu-id="b5b9c-109">Logs written tooAzure Tables</span></span>
<span data-ttu-id="b5b9c-110">hello 寫入 tooAzure 資料表的記錄檔提供一層的深入了解發生什麼事與 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-110">hello logs written tooAzure Tables provide one level of insight into what is happening with an HDInsight cluster.</span></span>

<span data-ttu-id="b5b9c-111">當您建立的 HDInsight 叢集時，6 資料表會自動建立 linux 叢集 hello 預設資料表儲存體中：</span><span class="sxs-lookup"><span data-stu-id="b5b9c-111">When you create an HDInsight cluster, 6 tables are automatically created for Linux-based clusters in hello default Table storage:</span></span>

* <span data-ttu-id="b5b9c-112">hdinsightagentlog</span><span class="sxs-lookup"><span data-stu-id="b5b9c-112">hdinsightagentlog</span></span>
* <span data-ttu-id="b5b9c-113">syslog</span><span class="sxs-lookup"><span data-stu-id="b5b9c-113">syslog</span></span>
* <span data-ttu-id="b5b9c-114">daemonlog</span><span class="sxs-lookup"><span data-stu-id="b5b9c-114">daemonlog</span></span>
* <span data-ttu-id="b5b9c-115">hadoopservicelog</span><span class="sxs-lookup"><span data-stu-id="b5b9c-115">hadoopservicelog</span></span>
* <span data-ttu-id="b5b9c-116">ambariserverlog</span><span class="sxs-lookup"><span data-stu-id="b5b9c-116">ambariserverlog</span></span>
* <span data-ttu-id="b5b9c-117">ambariagentlog</span><span class="sxs-lookup"><span data-stu-id="b5b9c-117">ambariagentlog</span></span>

<span data-ttu-id="b5b9c-118">針對 Windows 型叢集建立 3 個資料表：</span><span class="sxs-lookup"><span data-stu-id="b5b9c-118">3 tables are created for Windows-based clusters:</span></span>

* <span data-ttu-id="b5b9c-119">setuplog：佈建/設定 HDInsight 叢集時發生的事件/例外狀況的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-119">setuplog: Log of events/exceptions encountered in provisioning/setting up of HDInsight clusters.</span></span>
* <span data-ttu-id="b5b9c-120">hadoopinstalllog: hello 叢集上安裝 Hadoop 時發生的事件/例外狀況記錄。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-120">hadoopinstalllog: Log of events/exceptions encountered when installing Hadoop on hello cluster.</span></span> <span data-ttu-id="b5b9c-121">此資料表可能有助於偵錯問題相關 tooclusters 建立使用自訂參數。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-121">This table may be useful in debugging issues related tooclusters created with custom parameters.</span></span>
* <span data-ttu-id="b5b9c-122">hadoopservicelog：所有 Hadoop 服務記錄的事件/例外狀況的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-122">hadoopservicelog: Log of events/exceptions recorded by all Hadoop services.</span></span> <span data-ttu-id="b5b9c-123">此資料表可能有助於偵錯在 HDInsight 叢集上的問題相關的 toojob 失敗。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-123">This table may be useful in debugging issues related toojob failures on HDInsight clusters.</span></span>

<span data-ttu-id="b5b9c-124">hello 資料表的檔案名稱會是**u<ClusterName>DDMonYYYYatHHMMSSsss<TableName>**。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-124">hello table file names are **u<ClusterName>DDMonYYYYatHHMMSSsss<TableName>**.</span></span>

<span data-ttu-id="b5b9c-125">這些資料表包含下列欄位的 hello:</span><span class="sxs-lookup"><span data-stu-id="b5b9c-125">These tables contains hello following fields:</span></span>

* <span data-ttu-id="b5b9c-126">ClusterDnsName</span><span class="sxs-lookup"><span data-stu-id="b5b9c-126">ClusterDnsName</span></span>
* <span data-ttu-id="b5b9c-127">ComponentName</span><span class="sxs-lookup"><span data-stu-id="b5b9c-127">ComponentName</span></span>
* <span data-ttu-id="b5b9c-128">EventTimestamp</span><span class="sxs-lookup"><span data-stu-id="b5b9c-128">EventTimestamp</span></span>
* <span data-ttu-id="b5b9c-129">Host</span><span class="sxs-lookup"><span data-stu-id="b5b9c-129">Host</span></span>
* <span data-ttu-id="b5b9c-130">MALoggingHash</span><span class="sxs-lookup"><span data-stu-id="b5b9c-130">MALoggingHash</span></span>
* <span data-ttu-id="b5b9c-131">訊息</span><span class="sxs-lookup"><span data-stu-id="b5b9c-131">Message</span></span>
* <span data-ttu-id="b5b9c-132">N</span><span class="sxs-lookup"><span data-stu-id="b5b9c-132">N</span></span>
* <span data-ttu-id="b5b9c-133">PreciseTimeStamp</span><span class="sxs-lookup"><span data-stu-id="b5b9c-133">PreciseTimeStamp</span></span>
* <span data-ttu-id="b5b9c-134">角色</span><span class="sxs-lookup"><span data-stu-id="b5b9c-134">Role</span></span>
* <span data-ttu-id="b5b9c-135">RowIndex</span><span class="sxs-lookup"><span data-stu-id="b5b9c-135">RowIndex</span></span>
* <span data-ttu-id="b5b9c-136">租用戶</span><span class="sxs-lookup"><span data-stu-id="b5b9c-136">Tenant</span></span>
* <span data-ttu-id="b5b9c-137">時間戳記</span><span class="sxs-lookup"><span data-stu-id="b5b9c-137">TIMESTAMP</span></span>
* <span data-ttu-id="b5b9c-138">TraceLevel</span><span class="sxs-lookup"><span data-stu-id="b5b9c-138">TraceLevel</span></span>

### <a name="tools-for-accessing-hello-logs"></a><span data-ttu-id="b5b9c-139">適用於存取 hello 記錄工具</span><span class="sxs-lookup"><span data-stu-id="b5b9c-139">Tools for accessing hello logs</span></span>
<span data-ttu-id="b5b9c-140">有許多工具可用來存取這些資料表中的資料：</span><span class="sxs-lookup"><span data-stu-id="b5b9c-140">There are many tools available for accessing data in these tables:</span></span>

* <span data-ttu-id="b5b9c-141">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b5b9c-141">Visual Studio</span></span>
* <span data-ttu-id="b5b9c-142">Azure 儲存體總管</span><span class="sxs-lookup"><span data-stu-id="b5b9c-142">Azure Storage Explorer</span></span>
* <span data-ttu-id="b5b9c-143">Power Query for Excel</span><span class="sxs-lookup"><span data-stu-id="b5b9c-143">Power Query for Excel</span></span>

#### <a name="use-power-query-for-excel"></a><span data-ttu-id="b5b9c-144">使用 Power Query for Excel</span><span class="sxs-lookup"><span data-stu-id="b5b9c-144">Use Power Query for Excel</span></span>
<span data-ttu-id="b5b9c-145">您可以從 [www.microsoft.com/en-us/download/details.aspx?id=39379](http://www.microsoft.com/en-us/download/details.aspx?id=39379) 安裝 Power Query。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-145">Power Query can be installed from [www.microsoft.com/en-us/download/details.aspx?id=39379](http://www.microsoft.com/en-us/download/details.aspx?id=39379).</span></span> <span data-ttu-id="b5b9c-146">請參閱 hello hello 系統需求的下載頁面</span><span class="sxs-lookup"><span data-stu-id="b5b9c-146">See hello download page for hello system requirements</span></span>

<span data-ttu-id="b5b9c-147">**toouse Power Query tooopen 和分析 hello 服務記錄檔**</span><span class="sxs-lookup"><span data-stu-id="b5b9c-147">**toouse Power Query tooopen and analyze hello service log**</span></span>

1. <span data-ttu-id="b5b9c-148">開啟 **Microsoft Excel**。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-148">Open **Microsoft Excel**.</span></span>
2. <span data-ttu-id="b5b9c-149">從 hello **Power Query**功能表上，按一下 **從 Azure**，然後按一下**從 Microsoft Azure 資料表儲存體**。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-149">From hello **Power Query** menu, click **From Azure**, and then click **From Microsoft Azure Table storage**.</span></span>
   
    ![HDInsight Hadoop Excel PowerQuery 開啟 Azure 資料表儲存體](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-using-excel-power-query-open.png)
3. <span data-ttu-id="b5b9c-151">輸入 hello 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-151">Enter hello storage account name.</span></span> <span data-ttu-id="b5b9c-152">這可以是 hello 簡短名稱或 hello FQDN。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-152">This can be either hello short name or hello FQDN.</span></span>
4. <span data-ttu-id="b5b9c-153">輸入 hello 儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-153">Enter hello storage account key.</span></span> <span data-ttu-id="b5b9c-154">您應該會看到一份資料表清單：</span><span class="sxs-lookup"><span data-stu-id="b5b9c-154">You shall see a list of tables:</span></span>
   
    ![儲存在 Azure 資料表儲存體中的 HDInsight Hadoop 記錄檔](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-table-names.png)
5. <span data-ttu-id="b5b9c-156">以滑鼠右鍵按一下 hello hadoopservicelog 資料表在 hello**導覽**窗格，然後選取**編輯**。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-156">Right-click hello hadoopservicelog table in hello **Navigator** pane and select **Edit**.</span></span> <span data-ttu-id="b5b9c-157">您應該會看到 4 個資料行。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-157">You shall see 4 columns.</span></span> <span data-ttu-id="b5b9c-158">選擇性地刪除 hello**資料分割索引鍵**，**資料列索引鍵**，和**時間戳記**資料行，只要選取它們，然後按一下**移除資料行**從 hello 功能區中的 hello 選項。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-158">Optionally, delete hello **Partition Key**, **Row Key**, and **Timestamp** columns by selecting them, then clicking **Remove Columns** from hello options in hello ribbon.</span></span>
6. <span data-ttu-id="b5b9c-159">按一下 hello 展開圖示上 hello 內容要 tooimport hello Excel 試算表的資料行 toochoose hello 資料行。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-159">Click hello expand icon on hello Content column toochoose hello columns you want tooimport into hello Excel spreadsheet.</span></span> <span data-ttu-id="b5b9c-160">在此示範中，我選擇 TraceLevel 和 ComponentName：它可以提供一些基本資訊讓我知道哪些元件有問題。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-160">For this demonstration, I chose TraceLevel, and ComponentName: It can give me some basic information on which components had issues.</span></span>
   
    ![HDInsight Hadoop 記錄檔選擇資料行](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-using-excel-power-query-filter.png)
7. <span data-ttu-id="b5b9c-162">按一下**確定**tooimport hello 資料。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-162">Click **OK** tooimport hello data.</span></span>
8. <span data-ttu-id="b5b9c-163">選取 hello **TraceLevel**，角色和**ComponentName**資料行，然後再按一下**Group By** hello 功能區中的控制項。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-163">Select hello **TraceLevel**, Role, and **ComponentName** columns, and then click **Group By** control in hello ribbon.</span></span>
9. <span data-ttu-id="b5b9c-164">按一下**確定**hello Group By 對話方塊中</span><span class="sxs-lookup"><span data-stu-id="b5b9c-164">Click **OK** in hello Group By dialog box</span></span>
10. <span data-ttu-id="b5b9c-165">按一下 [套用並關閉]。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-165">Click** Apply & Close**.</span></span>

<span data-ttu-id="b5b9c-166">您現在可以視需要使用 Excel toofilter 和排序。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-166">You can now use Excel toofilter and sort as necessary.</span></span> <span data-ttu-id="b5b9c-167">很明顯地，您可能想 tooinclude 中向下的順序 toodrill 其他資料行 （例如訊息） 問題發生，但選取並群組 hello 上面所述的資料行提供不錯圖片的 Hadoop 服務發生什麼事時。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-167">Obviously, you may want tooinclude other columns (e.g. Message) in order toodrill down into issues when they occur, but selecting and grouping hello columns described above provides a decent picture of what is happening with Hadoop services.</span></span> <span data-ttu-id="b5b9c-168">hello 相同概念可以套用的 toohello setuplog 和 hadoopinstalllog 資料表。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-168">hello same idea can be applied toohello setuplog and hadoopinstalllog tables.</span></span>

#### <a name="use-visual-studio"></a><span data-ttu-id="b5b9c-169">使用 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b5b9c-169">Use Visual Studio</span></span>
<span data-ttu-id="b5b9c-170">**toouse Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="b5b9c-170">**toouse Visual Studio**</span></span>

1. <span data-ttu-id="b5b9c-171">開啟 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-171">Open Visual Studio.</span></span>
2. <span data-ttu-id="b5b9c-172">從 hello**檢視**功能表上，按一下  **Cloud Explorer**。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-172">From hello **View** menu, click **Cloud Explorer**.</span></span> <span data-ttu-id="b5b9c-173">或直接按一下 **CTRL+\, CTRL+X**。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-173">Or simply click **CTRL+\, CTRL+X**.</span></span>
3. <span data-ttu-id="b5b9c-174">從 [Cloud Explorer] 中，選取 [資源類型]。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-174">From **Cloud Explorer**, select **Resource Types**.</span></span>  <span data-ttu-id="b5b9c-175">hello 其他可用的選項是**資源群組**。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-175">hello other available option is **Resource Groups**.</span></span>
4. <span data-ttu-id="b5b9c-176">展開**儲存體帳戶**，hello 叢集中的預設儲存體帳戶，然後**資料表**。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-176">Expand **Storage Accounts**, hello default storage account for your cluster, and then **Tables**.</span></span>
5. <span data-ttu-id="b5b9c-177">按兩下 [hadoopservicelog]。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-177">Double-click **hadoopservicelog**.</span></span>
6. <span data-ttu-id="b5b9c-178">新增篩選器。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-178">Add a filter.</span></span> <span data-ttu-id="b5b9c-179">例如：</span><span class="sxs-lookup"><span data-stu-id="b5b9c-179">For example:</span></span>
   
        TraceLevel eq 'ERROR'
   
    ![HDInsight Hadoop 記錄檔選擇資料行](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-visual-studio-filter.png)
   
    <span data-ttu-id="b5b9c-181">如需建構篩選條件的詳細資訊，請參閱[hello 資料表設計工具建構篩選字串](../vs-azure-tools-table-designer-construct-filter-strings.md)。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-181">For more information about constructing filters, see [Construct Filter Strings for hello Table Designer](../vs-azure-tools-table-designer-construct-filter-strings.md).</span></span>

## <a name="logs-written-tooazure-blob-storage"></a><span data-ttu-id="b5b9c-182">記錄檔寫入 tooAzure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="b5b9c-182">Logs Written tooAzure Blob Storage</span></span>
<span data-ttu-id="b5b9c-183">[hello 記錄寫入的 tooAzure 資料表](#log-written-to-azure-tables)提供一個層級的深入了解發生什麼事與 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-183">[hello logs written tooAzure Tables](#log-written-to-azure-tables) provide one level of insight into what is happening with an HDInsight cluster.</span></span> <span data-ttu-id="b5b9c-184">不過，這些資料表並不會提供工作層級記錄檔，這些記錄檔有助於發生問題時進一步深入探索。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-184">However, these tables do not provide task-level logs, which can be helpful in drilling further into issues when they occur.</span></span> <span data-ttu-id="b5b9c-185">tooprovide 這個下一個層級的詳細資料，HDInsight 叢集會設定 toowrite 工作記錄檔 tooyour Blob 儲存體帳戶透過 Templeton 送出任何工作。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-185">tooprovide this next level of detail, HDInsight clusters are configured toowrite task logs tooyour Blob Storage account for any job that is submitted through Templeton.</span></span> <span data-ttu-id="b5b9c-186">實際上，這表示使用 hello Microsoft Azure PowerShell cmdlet 或 hello.NET 作業提交應用程式開發介面，不透過 RDP/命令列存取 toohello 叢集提交的工作提交的工作。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-186">Practically, this means jobs submitted using hello Microsoft Azure PowerShell cmdlets or hello .NET Job Submission APIs, not jobs submitted through RDP/command-line access toohello cluster.</span></span> 

<span data-ttu-id="b5b9c-187">tooview hello 記錄，請參閱 <<c0> [ 存取 YARN 應用程式記錄檔以 Linux 為基礎的 HDInsight 上](hdinsight-hadoop-access-yarn-app-logs-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-187">tooview hello logs, see [Access YARN application logs on Linux-based HDInsight](hdinsight-hadoop-access-yarn-app-logs-linux.md).</span></span>

<span data-ttu-id="b5b9c-188">如需應用程式記錄檔的詳細資訊，請參閱 [簡化 YARN 的使用者記錄檔管理和存取](http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/)。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-188">For more information about application logs, see [Simplifying user-logs management and access in YARN](http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/).</span></span>

## <a name="view-cluster-health-and-job-logs"></a><span data-ttu-id="b5b9c-189">檢視叢集健康情況和工作記錄檔</span><span class="sxs-lookup"><span data-stu-id="b5b9c-189">View cluster health and job logs</span></span>
### <a name="access-hadoop-ui"></a><span data-ttu-id="b5b9c-190">存取 Hadoop UI</span><span class="sxs-lookup"><span data-stu-id="b5b9c-190">Access Hadoop UI</span></span>
<span data-ttu-id="b5b9c-191">從 hello Azure 入口網站，按一下 HDInsight 叢集名稱 tooopen hello 叢集刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-191">From hello Azure portal, click an HDInsight cluster name tooopen hello cluster blade.</span></span> <span data-ttu-id="b5b9c-192">從 hello 叢集刀鋒視窗中，按一下 **儀表板**。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-192">From hello cluster blade, click **Dashboard**.</span></span>

![啟動叢集儀表板](./media/hdinsight-debug-jobs/hdi-debug-launch-dashboard.png)

<span data-ttu-id="b5b9c-194">出現提示時，輸入 hello 叢集系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-194">When prompted, enter hello cluster administrator credentials.</span></span> <span data-ttu-id="b5b9c-195">在 hello 開啟的查詢主控台中，按一下  **Hadoop UI**。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-195">In hello Query Console that opens, click **Hadoop UI**.</span></span>

![啟動 Hadoop UI](./media/hdinsight-debug-jobs/hdi-debug-launch-dashboard-hadoop-ui.png)

### <a name="access-hello-yarn-ui"></a><span data-ttu-id="b5b9c-197">存取 hello Yarn UI</span><span class="sxs-lookup"><span data-stu-id="b5b9c-197">Access hello Yarn UI</span></span>
<span data-ttu-id="b5b9c-198">從 hello Azure 入口網站，按一下 HDInsight 叢集名稱 tooopen hello 叢集刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-198">From hello Azure portal, click an HDInsight cluster name tooopen hello cluster blade.</span></span> <span data-ttu-id="b5b9c-199">從 hello 叢集刀鋒視窗中，按一下 **儀表板**。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-199">From hello cluster blade, click **Dashboard**.</span></span> <span data-ttu-id="b5b9c-200">出現提示時，輸入 hello 叢集系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-200">When prompted, enter hello cluster administrator credentials.</span></span> <span data-ttu-id="b5b9c-201">在 hello 開啟的查詢主控台中，按一下  **YARN UI**。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-201">In hello Query Console that opens, click **YARN UI**.</span></span>

<span data-ttu-id="b5b9c-202">您可以使用 hello YARN UI toodo hello 下列：</span><span class="sxs-lookup"><span data-stu-id="b5b9c-202">You can use hello YARN UI toodo hello following:</span></span>

* <span data-ttu-id="b5b9c-203">**取得叢集狀態**。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-203">**Get cluster status**.</span></span> <span data-ttu-id="b5b9c-204">從 hello 左窗格中，展開**叢集**，然後按一下**有關**。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-204">From hello left pane, expand **Cluster**, and click **About**.</span></span> <span data-ttu-id="b5b9c-205">此存在叢集狀態詳細資料，例如配置記憶體、 核心使用，總共 hello 叢集資源管理員的狀態時，叢集版本等等。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-205">This present cluster status details like total allocated memory, cores used, state of hello cluster resource manager, cluster version etc.</span></span>
  
    ![啟動叢集儀表板](./media/hdinsight-debug-jobs/hdi-debug-yarn-cluster-state.png)
* <span data-ttu-id="b5b9c-207">**取得節點狀態**。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-207">**Get node status**.</span></span> <span data-ttu-id="b5b9c-208">從 hello 左窗格中，展開**叢集**，然後按一下**節點**。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-208">From hello left pane, expand **Cluster**, and click **Nodes**.</span></span> <span data-ttu-id="b5b9c-209">這會列示在 hello 叢集，每個節點、 資源配置的 tooeach 節點和其他內容的 HTTP 位址的所有 hello 節點。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-209">This lists all hello nodes in hello cluster, HTTP address of each node, resources allocated tooeach node, etc.</span></span>
* <span data-ttu-id="b5b9c-210">**監視工作狀態**。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-210">**Monitor job status**.</span></span> <span data-ttu-id="b5b9c-211">從 hello 左窗格中，展開**叢集**，然後按一下**應用程式**toolist 所有 hello hello 叢集中的作業。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-211">From hello left pane, expand **Cluster**, and then click **Applications** toolist all hello jobs in hello cluster.</span></span> <span data-ttu-id="b5b9c-212">如果您想在特定的工作 toolook 狀態 （例如新送出，執行等），按一下 [hello] 下方的適當連結**應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-212">If you want toolook at jobs in a specific state (such as new, submitted, running, etc.), click hello appropriate link under **Applications**.</span></span> <span data-ttu-id="b5b9c-213">您可以進一步按一下 hello 作業名稱 toofind hello 工作這類包括 hello 輸出、 記錄檔等深入了解。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-213">You can further click hello job name toofind out more about hello job such including hello output, logs, etc.</span></span>

### <a name="access-hello-hbase-ui"></a><span data-ttu-id="b5b9c-214">存取 hello HBase UI</span><span class="sxs-lookup"><span data-stu-id="b5b9c-214">Access hello HBase UI</span></span>
<span data-ttu-id="b5b9c-215">從 hello Azure 入口網站，按一下 HDInsight HBase 叢集名稱 tooopen hello 叢集刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-215">From hello Azure portal, click an HDInsight HBase cluster name tooopen hello cluster blade.</span></span> <span data-ttu-id="b5b9c-216">從 hello 叢集刀鋒視窗中，按一下 **儀表板**。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-216">From hello cluster blade, click **Dashboard**.</span></span> <span data-ttu-id="b5b9c-217">出現提示時，輸入 hello 叢集系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-217">When prompted, enter hello cluster administrator credentials.</span></span> <span data-ttu-id="b5b9c-218">在 hello 開啟的查詢主控台中，按一下  **HBase UI**。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-218">In hello Query Console that opens, click **HBase UI**.</span></span>

## <a name="hdinsight-error-codes"></a><span data-ttu-id="b5b9c-219">HDInsight 錯誤代碼</span><span class="sxs-lookup"><span data-stu-id="b5b9c-219">HDInsight error codes</span></span>
<span data-ttu-id="b5b9c-220">hello 分本節中的錯誤訊息所提供的 Azure HDInsight 中的 Hadoop toohelp hello 使用者了解可能的錯誤狀況，他們可以在管理使用 Azure PowerShell 及 tooadvise hello 服務時遇到在 hello 步驟這可以採取 toorecover hello 錯誤。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-220">hello error messages itemized in this section are provided toohelp hello users of Hadoop in Azure HDInsight understand possible error conditions that they can encounter when administering hello service using Azure PowerShell and tooadvise them on hello steps which can be taken toorecover from hello error.</span></span>

<span data-ttu-id="b5b9c-221">其中某些錯誤訊息可能也會出現在 hello Azure 入口網站時使用的 toomanage HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-221">Some of these error messages could also be seen in hello Azure portal when it is used toomanage HDInsight clusters.</span></span> <span data-ttu-id="b5b9c-222">但您可能會遇到其他錯誤訊息有較不精細到期 toohello hello 修復動作可能在此內容中的條件約束。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-222">But other error messages you might encounter there are less granular due toohello constraints on hello remedial actions possible in this context.</span></span> <span data-ttu-id="b5b9c-223">Hello 緩和所在明顯 hello 內容提供的其他錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-223">Other error messages are provided in hello contexts where hello mitigation is obvious.</span></span> 

### <span data-ttu-id="b5b9c-224"><a id="AtleastOneSqlMetastoreMustBeProvided"></a>AtleastOneSqlMetastoreMustBeProvided</span><span class="sxs-lookup"><span data-stu-id="b5b9c-224"><a id="AtleastOneSqlMetastoreMustBeProvided"></a>AtleastOneSqlMetastoreMustBeProvided</span></span>
* <span data-ttu-id="b5b9c-225">**描述**： 請提供 Azure SQL database 詳細資料至少一個元件中順序 toouse Hive 和 Oozie 中繼存放區的自訂設定。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-225">**Description**: Please provide Azure SQL database details for at least one component in order toouse custom settings for Hive and Oozie metastores.</span></span>
* <span data-ttu-id="b5b9c-226">**風險降低**: hello 使用者需要 toosupply 為有效 SQL Azure 中繼存放區，然後重試 hello 的要求。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-226">**Mitigation**: hello user needs toosupply a valid SQL Azure metastore and retry hello request.</span></span>  

### <span data-ttu-id="b5b9c-227"><a id="AzureRegionNotSupported"></a>AzureRegionNotSupported</span><span class="sxs-lookup"><span data-stu-id="b5b9c-227"><a id="AzureRegionNotSupported"></a>AzureRegionNotSupported</span></span>
* <span data-ttu-id="b5b9c-228">**描述**：無法在區域 *nameOfYourRegion*中建立叢集。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-228">**Description**: Could not create cluster in region *nameOfYourRegion*.</span></span> <span data-ttu-id="b5b9c-229">請使用有效的 HDInsight 區域，然後重試要求。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-229">Use a valid HDInsight region and retry request.</span></span>
* <span data-ttu-id="b5b9c-230">**風險降低**： 客戶應該建立目前支援它們的 hello 叢區域： 東南亞、 西歐、 北歐、 美國東部、 或美國西部。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-230">**Mitigation**: Customer should create hello cluster region that currently supports them: Southeast Asia, West Europe, North Europe, East US, or West US.</span></span>  

### <span data-ttu-id="b5b9c-231"><a id="ClusterContainerRecordNotFound"></a>ClusterContainerRecordNotFound</span><span class="sxs-lookup"><span data-stu-id="b5b9c-231"><a id="ClusterContainerRecordNotFound"></a>ClusterContainerRecordNotFound</span></span>
* <span data-ttu-id="b5b9c-232">**描述**: hello 伺服器找不到 hello 要求叢集記錄。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-232">**Description**: hello server could not find hello requested cluster record.</span></span>  
* <span data-ttu-id="b5b9c-233">**風險降低**: hello 作業重試一次。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-233">**Mitigation**: Retry hello operation.</span></span>

### <span data-ttu-id="b5b9c-234"><a id="ClusterDnsNameInvalidReservedWord"></a>ClusterDnsNameInvalidReservedWord</span><span class="sxs-lookup"><span data-stu-id="b5b9c-234"><a id="ClusterDnsNameInvalidReservedWord"></a>ClusterDnsNameInvalidReservedWord</span></span>
* <span data-ttu-id="b5b9c-235">**描述**：叢集 DNS 名稱 *yourDnsName* 無效。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-235">**Description**: Cluster DNS name *yourDnsName* is invalid.</span></span> <span data-ttu-id="b5b9c-236">請確定名稱以英數字元開始和結束，且只包含 '-' 特殊字元</span><span class="sxs-lookup"><span data-stu-id="b5b9c-236">Please ensure name starts and ends with alphanumeric and can only contain '-' special character</span></span>  
* <span data-ttu-id="b5b9c-237">**風險降低**： 請確定您使用的是有效的 DNS 名稱為您的叢集，開頭和結尾是英數字元，並不包含任何特殊字元而不是 hello 虛線 '-'，然後重試 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-237">**Mitigation**: Make sure that you have used a valid DNS name for your cluster that starts and ends with alphanumeric and contains no special characters other than hello dash '-' and then retry hello operation.</span></span>

### <span data-ttu-id="b5b9c-238"><a id="ClusterNameUnavailable"></a>ClusterNameUnavailable</span><span class="sxs-lookup"><span data-stu-id="b5b9c-238"><a id="ClusterNameUnavailable"></a>ClusterNameUnavailable</span></span>
* <span data-ttu-id="b5b9c-239">**描述**：叢集名稱 *yourClusterName* 無法使用。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-239">**Description**: Cluster name *yourClusterName* is unavailable.</span></span> <span data-ttu-id="b5b9c-240">請挑選其他名稱。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-240">Please pick another name.</span></span>  
* <span data-ttu-id="b5b9c-241">**風險降低**: hello 使用者應該指定唯一 clustername 並不存在，然後再試一次。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-241">**Mitigation**: hello user should specify a clustername that is unique and does not exist and retry.</span></span> <span data-ttu-id="b5b9c-242">如果 hello 使用者正在使用 hello 入口網站，UI 會通知方式如果叢集名稱已在 hello 期間使用的 hello 建立步驟。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-242">If hello user is using hello Portal, hello UI will notify them if a cluster name is already being used during hello create steps.</span></span>

### <span data-ttu-id="b5b9c-243"><a id="ClusterPasswordInvalid"></a>ClusterPasswordInvalid</span><span class="sxs-lookup"><span data-stu-id="b5b9c-243"><a id="ClusterPasswordInvalid"></a>ClusterPasswordInvalid</span></span>
* <span data-ttu-id="b5b9c-244">**描述**：叢集密碼無效。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-244">**Description**: Cluster password is invalid.</span></span> <span data-ttu-id="b5b9c-245">密碼必須至少 10 個字元，必須包含至少一個數字、 大寫字母、 小寫字母和不含空格的特殊字元，且不能包含 hello 做為其一部分的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-245">Password must be at least 10 characters long and must contain at least one number, uppercase letter, lowercase letter and special character with no spaces and should not contain hello username as part of it.</span></span>  
* <span data-ttu-id="b5b9c-246">**風險降低**： 提供有效的叢集密碼，然後重試 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-246">**Mitigation**: Provide a valid cluster password and retry hello operation.</span></span>

### <span data-ttu-id="b5b9c-247"><a id="ClusterUserNameInvalid"></a>ClusterUserNameInvalid</span><span class="sxs-lookup"><span data-stu-id="b5b9c-247"><a id="ClusterUserNameInvalid"></a>ClusterUserNameInvalid</span></span>
* <span data-ttu-id="b5b9c-248">**描述**：叢集使用者名稱無效。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-248">**Description**: Cluster username is invalid.</span></span> <span data-ttu-id="b5b9c-249">請確定使用者名稱不含特殊字元或空格。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-249">Please ensure username doesn't contain special characters or spaces.</span></span>  
* <span data-ttu-id="b5b9c-250">**風險降低**： 提供有效的叢集使用者名稱，然後重試 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-250">**Mitigation**: Provide a valid cluster username and retry hello operation.</span></span>

### <span data-ttu-id="b5b9c-251"><a id="ClusterUserNameInvalidReservedWord"></a>ClusterUserNameInvalidReservedWord</span><span class="sxs-lookup"><span data-stu-id="b5b9c-251"><a id="ClusterUserNameInvalidReservedWord"></a>ClusterUserNameInvalidReservedWord</span></span>
* <span data-ttu-id="b5b9c-252">**描述**：叢集 DNS 名稱 *yourDnsClusterName* 無效。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-252">**Description**: Cluster DNS name *yourDnsClusterName* is invalid.</span></span> <span data-ttu-id="b5b9c-253">請確定名稱以英數字元開始和結束，且只包含 '-' 特殊字元</span><span class="sxs-lookup"><span data-stu-id="b5b9c-253">Please ensure name starts and ends with alphanumeric and can only contain '-' special character</span></span>  
* <span data-ttu-id="b5b9c-254">**風險降低**： 提供有效的 DNS 叢集使用者名稱，然後重試 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-254">**Mitigation**: Provide a valid DNS cluster username and retry hello operation.</span></span>

### <span data-ttu-id="b5b9c-255"><a id="ContainerNameMisMatchWithDnsName"></a>ContainerNameMisMatchWithDnsName</span><span class="sxs-lookup"><span data-stu-id="b5b9c-255"><a id="ContainerNameMisMatchWithDnsName"></a>ContainerNameMisMatchWithDnsName</span></span>
* <span data-ttu-id="b5b9c-256">**描述**: URI 中的容器名稱*yourcontainerURI*和 DNS 名稱*yourDnsName*在要求主體必須是 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-256">**Description**: Container name in URI *yourcontainerURI* and DNS name *yourDnsName* in request body must be hello same.</span></span>  
* <span data-ttu-id="b5b9c-257">**風險降低**： 請確定您的容器名稱和您的 DNS 名稱 hello 相同，然後重試 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-257">**Mitigation**: Make sure that your container Name and your DNS name are hello same and retry hello operation.</span></span>

### <span data-ttu-id="b5b9c-258"><a id="DataNodeDefinitionNotFound"></a>DataNodeDefinitionNotFound</span><span class="sxs-lookup"><span data-stu-id="b5b9c-258"><a id="DataNodeDefinitionNotFound"></a>DataNodeDefinitionNotFound</span></span>
* <span data-ttu-id="b5b9c-259">**描述**：叢集組態無效。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-259">**Description**: Invalid cluster configuration.</span></span> <span data-ttu-id="b5b9c-260">無法 toofind 任何資料節點中的定義節點大小。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-260">Unable toofind any data node definitions in node size.</span></span>  
* <span data-ttu-id="b5b9c-261">**風險降低**: hello 作業重試一次。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-261">**Mitigation**: Retry hello operation.</span></span>

### <span data-ttu-id="b5b9c-262"><a id="DeploymentDeletionFailure"></a>DeploymentDeletionFailure</span><span class="sxs-lookup"><span data-stu-id="b5b9c-262"><a id="DeploymentDeletionFailure"></a>DeploymentDeletionFailure</span></span>
* <span data-ttu-id="b5b9c-263">**描述**: hello 叢集無法刪除部署</span><span class="sxs-lookup"><span data-stu-id="b5b9c-263">**Description**: Deletion of deployment failed for hello Cluster</span></span>  
* <span data-ttu-id="b5b9c-264">**風險降低**: hello 刪除作業重試一次。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-264">**Mitigation**: Retry hello delete operation.</span></span>

### <span data-ttu-id="b5b9c-265"><a id="DnsMappingNotFound"></a>DnsMappingNotFound</span><span class="sxs-lookup"><span data-stu-id="b5b9c-265"><a id="DnsMappingNotFound"></a>DnsMappingNotFound</span></span>
* <span data-ttu-id="b5b9c-266">**描述**：服務組態錯誤。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-266">**Description**: Service configuration error.</span></span> <span data-ttu-id="b5b9c-267">找不到必要的 DNS 對應資訊。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-267">Required DNS mapping information not found.</span></span>  
* <span data-ttu-id="b5b9c-268">**緩和**：刪除叢集，然後建立新的叢集。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-268">**Mitigation**: Delete cluster and create a new cluster.</span></span>

### <span data-ttu-id="b5b9c-269"><a id="DuplicateClusterContainerRequest"></a>DuplicateClusterContainerRequest</span><span class="sxs-lookup"><span data-stu-id="b5b9c-269"><a id="DuplicateClusterContainerRequest"></a>DuplicateClusterContainerRequest</span></span>
* <span data-ttu-id="b5b9c-270">**描述**：嘗試建立重複的叢集容器。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-270">**Description**: Duplicate cluster container creation attempt.</span></span> <span data-ttu-id="b5b9c-271">已存在 *nameOfYourContainer* 的記錄，但 Etag 不符。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-271">Record exists for *nameOfYourContainer* but Etags do not match.</span></span>
* <span data-ttu-id="b5b9c-272">**風險降低**: hello 容器和重試 hello 建立操作提供唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-272">**Mitigation**: Provide a unique name for hello container and retry hello create operation.</span></span>

### <span data-ttu-id="b5b9c-273"><a id="DuplicateClusterInHostedService"></a>DuplicateClusterInHostedService</span><span class="sxs-lookup"><span data-stu-id="b5b9c-273"><a id="DuplicateClusterInHostedService"></a>DuplicateClusterInHostedService</span></span>
* <span data-ttu-id="b5b9c-274">**描述**：代管服務 *nameOfYourHostedService* 已包含叢集。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-274">**Description**: Hosted service *nameOfYourHostedService* already contains a cluster.</span></span> <span data-ttu-id="b5b9c-275">代管服務不可包含多個叢集</span><span class="sxs-lookup"><span data-stu-id="b5b9c-275">A hosted service cannot contain multiple clusters</span></span>  
* <span data-ttu-id="b5b9c-276">**風險降低**： 主機 hello 叢集在另一個託管服務。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-276">**Mitigation**: Host hello cluster in another hosted service.</span></span>

### <span data-ttu-id="b5b9c-277"><a id="FailureToUpdateDeploymentStatus"></a>FailureToUpdateDeploymentStatus</span><span class="sxs-lookup"><span data-stu-id="b5b9c-277"><a id="FailureToUpdateDeploymentStatus"></a>FailureToUpdateDeploymentStatus</span></span>
* <span data-ttu-id="b5b9c-278">**描述**: hello server 無法更新 hello 叢集部署的 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-278">**Description**: hello server could not update hello state of hello cluster deployment.</span></span>  
* <span data-ttu-id="b5b9c-279">**風險降低**: hello 作業重試一次。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-279">**Mitigation**: Retry hello operation.</span></span> <span data-ttu-id="b5b9c-280">如果此情況發生多次，請連絡 CSS。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-280">If this happens multiple times, contact CSS.</span></span>

### <span data-ttu-id="b5b9c-281"><a id="HdiRestoreClusterAltered"></a>HdiRestoreClusterAltered</span><span class="sxs-lookup"><span data-stu-id="b5b9c-281"><a id="HdiRestoreClusterAltered"></a>HdiRestoreClusterAltered</span></span>
* <span data-ttu-id="b5b9c-282">**描述**：維護時已刪除叢集 *yourClusterName* 。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-282">**Description**: Cluster *yourClusterName* was deleted as part of maintenance.</span></span> <span data-ttu-id="b5b9c-283">請重新建立 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-283">Please recreate hello cluster.</span></span>
* <span data-ttu-id="b5b9c-284">**風險降低**： 重新建立 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-284">**Mitigation**: Recreate hello cluster.</span></span>

### <span data-ttu-id="b5b9c-285"><a id="HeadNodeConfigNotFound"></a>HeadNodeConfigNotFound</span><span class="sxs-lookup"><span data-stu-id="b5b9c-285"><a id="HeadNodeConfigNotFound"></a>HeadNodeConfigNotFound</span></span>
* <span data-ttu-id="b5b9c-286">**描述**：叢集組態無效。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-286">**Description**: Invalid cluster configuration.</span></span> <span data-ttu-id="b5b9c-287">在節點大小中找不到必要的前端節點組態。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-287">Required head node configuration not found in node sizes.</span></span>
* <span data-ttu-id="b5b9c-288">**風險降低**: hello 作業重試一次。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-288">**Mitigation**: Retry hello operation.</span></span>

### <span data-ttu-id="b5b9c-289"><a id="HostedServiceCreationFailure"></a>HostedServiceCreationFailure</span><span class="sxs-lookup"><span data-stu-id="b5b9c-289"><a id="HostedServiceCreationFailure"></a>HostedServiceCreationFailure</span></span>
* <span data-ttu-id="b5b9c-290">**描述**： 無法 toocreate 託管服務*nameOfYourHostedService*。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-290">**Description**: Unable toocreate hosted service *nameOfYourHostedService*.</span></span> <span data-ttu-id="b5b9c-291">請重試要求。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-291">Please retry request.</span></span>  
* <span data-ttu-id="b5b9c-292">**風險降低**: hello 的重試要求。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-292">**Mitigation**: Retry hello request.</span></span>

### <span data-ttu-id="b5b9c-293"><a id="HostedServiceHasProductionDeployment"></a>HostedServiceHasProductionDeployment</span><span class="sxs-lookup"><span data-stu-id="b5b9c-293"><a id="HostedServiceHasProductionDeployment"></a>HostedServiceHasProductionDeployment</span></span>
* <span data-ttu-id="b5b9c-294">**描述**：託管服務「nameOfYourHostedService」已有生產部署。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-294">**Description**: Hosted Service *nameOfYourHostedService* already has a production deployment.</span></span> <span data-ttu-id="b5b9c-295">代管服務不可包含多個生產部署</span><span class="sxs-lookup"><span data-stu-id="b5b9c-295">A hosted service cannot contain multiple production deployments.</span></span> <span data-ttu-id="b5b9c-296">重試 hello 要求以不同的叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-296">Retry hello request with a different cluster name.</span></span>
* <span data-ttu-id="b5b9c-297">**風險降低**： 使用不同的叢集名稱，然後重試 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-297">**Mitigation**: Use a different cluster name and retry hello request.</span></span>

### <span data-ttu-id="b5b9c-298"><a id="HostedServiceNotFound"></a>HostedServiceNotFound</span><span class="sxs-lookup"><span data-stu-id="b5b9c-298"><a id="HostedServiceNotFound"></a>HostedServiceNotFound</span></span>
* <span data-ttu-id="b5b9c-299">**描述**： 託管服務*nameOfYourHostedService*找不到 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-299">**Description**: Hosted Service *nameOfYourHostedService* for hello cluster could not be found.</span></span>  
* <span data-ttu-id="b5b9c-300">**風險降低**: hello 叢集處於錯誤狀態時，如果刪除它，並再試一次。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-300">**Mitigation**: If hello cluster is in error state, delete it and then try again.</span></span>

### <span data-ttu-id="b5b9c-301"><a id="HostedServiceWithNoDeployment"></a>HostedServiceWithNoDeployment</span><span class="sxs-lookup"><span data-stu-id="b5b9c-301"><a id="HostedServiceWithNoDeployment"></a>HostedServiceWithNoDeployment</span></span>
* <span data-ttu-id="b5b9c-302">**描述**：代管服務 *nameOfYourHostedService* 沒有相關聯的部署。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-302">**Description**: Hosted Service *nameOfYourHostedService* has no associated deployment.</span></span>  
* <span data-ttu-id="b5b9c-303">**風險降低**: hello 叢集處於錯誤狀態時，如果刪除它，並再試一次。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-303">**Mitigation**: If hello cluster is in error state, delete it and then try again.</span></span>

### <span data-ttu-id="b5b9c-304"><a id="InsufficientResourcesCores"></a>InsufficientResourcesCores</span><span class="sxs-lookup"><span data-stu-id="b5b9c-304"><a id="InsufficientResourcesCores"></a>InsufficientResourcesCores</span></span>
* <span data-ttu-id="b5b9c-305">**描述**: hello SubscriptionId *yourSubscriptionId*沒有核心左的 toocreate 叢集*yourClusterName*。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-305">**Description**: hello SubscriptionId *yourSubscriptionId* does not have cores left toocreate cluster *yourClusterName*.</span></span> <span data-ttu-id="b5b9c-306">必要：「resourcesRequired」、可用：「resourcesAvailable」。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-306">Required: *resourcesRequired*, Available: *resourcesAvailable*.</span></span>  
* <span data-ttu-id="b5b9c-307">**風險降低**： 釋放您的訂用帳戶中的資源或增加 hello 資源可用 toohello 訂用帳戶然後再試一次 toocreate hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-307">**Mitigation**: Free up resources in your subscription or increase hello resources available toohello subscription and try toocreate hello cluster again.</span></span>

### <span data-ttu-id="b5b9c-308"><a id="InsufficientResourcesHostedServices"></a>InsufficientResourcesHostedServices</span><span class="sxs-lookup"><span data-stu-id="b5b9c-308"><a id="InsufficientResourcesHostedServices"></a>InsufficientResourcesHostedServices</span></span>
* <span data-ttu-id="b5b9c-309">**描述**： 訂用帳戶 ID *yourSubscriptionId*沒有配額，以便為新的託管服務 toocreate 叢集*yourClusterName*。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-309">**Description**: Subscription ID *yourSubscriptionId* does not have quota for a new HostedService toocreate cluster *yourClusterName*.</span></span>  
* <span data-ttu-id="b5b9c-310">**風險降低**： 釋放您的訂用帳戶中的資源或增加 hello 資源可用 toohello 訂用帳戶然後再試一次 toocreate hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-310">**Mitigation**: Free up resources in your subscription or increase hello resources available toohello subscription and try toocreate hello cluster again.</span></span>

### <span data-ttu-id="b5b9c-311"><a id="InternalErrorRetryRequest"></a>InternalErrorRetryRequest</span><span class="sxs-lookup"><span data-stu-id="b5b9c-311"><a id="InternalErrorRetryRequest"></a>InternalErrorRetryRequest</span></span>
* <span data-ttu-id="b5b9c-312">**描述**: hello 伺服器發生內部錯誤。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-312">**Description**: hello server encountered an internal error.</span></span> <span data-ttu-id="b5b9c-313">請重試要求。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-313">Please retry request.</span></span>  
* <span data-ttu-id="b5b9c-314">**風險降低**: hello 的重試要求。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-314">**Mitigation**: Retry hello request.</span></span>

### <span data-ttu-id="b5b9c-315"><a id="InvalidAzureStorageLocation"></a>InvalidAzureStorageLocation</span><span class="sxs-lookup"><span data-stu-id="b5b9c-315"><a id="InvalidAzureStorageLocation"></a>InvalidAzureStorageLocation</span></span>
* <span data-ttu-id="b5b9c-316">**描述**：Azure 儲存體位置 *dataRegionName* 不是有效的位置。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-316">**Description**: Azure Storage location *dataRegionName* is not a valid location.</span></span> <span data-ttu-id="b5b9c-317">請確定 hello 區域正確，然後重試要求。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-317">Make sure hello region is correct and retry request.</span></span>
* <span data-ttu-id="b5b9c-318">**風險降低**： 選取支援 HDInsight 的存放位置，請檢查您的叢集已共然後重試 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-318">**Mitigation**: Select a Storage location that supports HDInsight, check that your cluster is co-located and retry hello operation.</span></span>

### <span data-ttu-id="b5b9c-319"><a id="InvalidNodeSizeForDataNode"></a>InvalidNodeSizeForDataNode</span><span class="sxs-lookup"><span data-stu-id="b5b9c-319"><a id="InvalidNodeSizeForDataNode"></a>InvalidNodeSizeForDataNode</span></span>
* <span data-ttu-id="b5b9c-320">**描述**：資源節點的 VM 大小無效。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-320">**Description**: Invalid VM size for data nodes.</span></span> <span data-ttu-id="b5b9c-321">所有資料節點僅支援 'Large VM' 大小。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-321">Only 'Large VM' size is supported for all data nodes.</span></span>  
* <span data-ttu-id="b5b9c-322">**風險降低**： 指定支援的 hello 節點大小的 hello 資料節點，然後重試 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-322">**Mitigation**: Specify hello supported node size for hello data node and retry hello operation.</span></span>

### <span data-ttu-id="b5b9c-323"><a id="InvalidNodeSizeForHeadNode"></a>InvalidNodeSizeForHeadNode</span><span class="sxs-lookup"><span data-stu-id="b5b9c-323"><a id="InvalidNodeSizeForHeadNode"></a>InvalidNodeSizeForHeadNode</span></span>
* <span data-ttu-id="b5b9c-324">**描述**：前端節點的 VM 大小無效。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-324">**Description**: Invalid VM size for head node.</span></span> <span data-ttu-id="b5b9c-325">前端節點僅支援 'ExtraLarge VM' 大小。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-325">Only 'ExtraLarge VM' size is supported for head node.</span></span>  
* <span data-ttu-id="b5b9c-326">**風險降低**： 指定支援的 hello hello 前端節點的節點大小，然後重試 hello 作業</span><span class="sxs-lookup"><span data-stu-id="b5b9c-326">**Mitigation**: Specify hello supported node size for hello head node and retry hello operation</span></span>

### <span data-ttu-id="b5b9c-327"><a id="InvalidRightsForDeploymentDeletion"></a>InvalidRightsForDeploymentDeletion</span><span class="sxs-lookup"><span data-stu-id="b5b9c-327"><a id="InvalidRightsForDeploymentDeletion"></a>InvalidRightsForDeploymentDeletion</span></span>
* <span data-ttu-id="b5b9c-328">**描述**： 訂用帳戶 ID *yourSubscriptionId*正在使用沒有叢集的足夠權限 tooexecute 刪除作業*yourClusterName*。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-328">**Description**: Subscription ID *yourSubscriptionId* being used does not have sufficient permissions tooexecute delete operation for cluster *yourClusterName*.</span></span>  
* <span data-ttu-id="b5b9c-329">**風險降低**: hello 叢集處於錯誤狀態時，如果卸除它，並再試一次。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-329">**Mitigation**: If hello cluster is in error state, drop it and then try again.</span></span>  

### <span data-ttu-id="b5b9c-330"><a id="InvalidStorageAccountBlobContainerName"></a>InvalidStorageAccountBlobContainerName</span><span class="sxs-lookup"><span data-stu-id="b5b9c-330"><a id="InvalidStorageAccountBlobContainerName"></a>InvalidStorageAccountBlobContainerName</span></span>
* <span data-ttu-id="b5b9c-331">**描述**：外部儲存帳戶 Blob 容器名稱 *yourContainerName* 無效。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-331">**Description**: External storage account blob container name *yourContainerName* is invalid.</span></span> <span data-ttu-id="b5b9c-332">請確定名稱以字母開頭，且只包含小寫字母、數字和虛線。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-332">Make sure name starts with a letter and contains only lowercase letters, numbers and dash.</span></span>  
* <span data-ttu-id="b5b9c-333">**風險降低**： 指定有效的儲存體帳戶 blob 容器名稱，然後重試 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-333">**Mitigation**: Specify a valid storage account blob container name and retry hello operation.</span></span>

### <span data-ttu-id="b5b9c-334"><a id="InvalidStorageAccountConfigurationSecretKey"></a>InvalidStorageAccountConfigurationSecretKey</span><span class="sxs-lookup"><span data-stu-id="b5b9c-334"><a id="InvalidStorageAccountConfigurationSecretKey"></a>InvalidStorageAccountConfigurationSecretKey</span></span>
* <span data-ttu-id="b5b9c-335">**描述**： 外部儲存體帳戶的組態*yourStorageAccountName*祕密金鑰的詳細資料是必要的 toohave toobe 組。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-335">**Description**: Configuration for external storage account *yourStorageAccountName* is required toohave secret key details toobe set.</span></span>  
* <span data-ttu-id="b5b9c-336">**風險降低**： 指定有效的密碼金鑰 hello 儲存體帳戶，然後重試 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-336">**Mitigation**: Specify a valid secret key for hello storage account and retry hello operation.</span></span>

### <span data-ttu-id="b5b9c-337"><a id="InvalidVersionHeaderFormat"></a>InvalidVersionHeaderFormat</span><span class="sxs-lookup"><span data-stu-id="b5b9c-337"><a id="InvalidVersionHeaderFormat"></a>InvalidVersionHeaderFormat</span></span>
* <span data-ttu-id="b5b9c-338">**描述**：版本標頭 *yourVersionHeader* 不是有效格式 yyyy-mm-dd。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-338">**Description**: Version header *yourVersionHeader* is not in valid format of yyyy-mm-dd.</span></span>  
* <span data-ttu-id="b5b9c-339">**風險降低**： 指定有效的格式為 hello 版本標頭，然後重試 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-339">**Mitigation**: Specify a valid format for hello version-header and retry hello request.</span></span>

### <span data-ttu-id="b5b9c-340"><a id="MoreThanOneHeadNode"></a>MoreThanOneHeadNode</span><span class="sxs-lookup"><span data-stu-id="b5b9c-340"><a id="MoreThanOneHeadNode"></a>MoreThanOneHeadNode</span></span>
* <span data-ttu-id="b5b9c-341">**描述**：叢集組態無效。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-341">**Description**: Invalid cluster configuration.</span></span> <span data-ttu-id="b5b9c-342">發現多個前端節點組態。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-342">Found more than one head node configuration.</span></span>  
* <span data-ttu-id="b5b9c-343">**風險降低**： 編輯 hello 組態，使得只有一個前端節點指定。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-343">**Mitigation**: Edit hello configuration so that only one head node is specified.</span></span>

### <span data-ttu-id="b5b9c-344"><a id="OperationTimedOutRetryRequest"></a>OperationTimedOutRetryRequest</span><span class="sxs-lookup"><span data-stu-id="b5b9c-344"><a id="OperationTimedOutRetryRequest"></a>OperationTimedOutRetryRequest</span></span>
* <span data-ttu-id="b5b9c-345">**描述**: hello 作業無法完成 hello 允許的時間內或 hello 最大重試嘗試盡量。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-345">**Description**: hello operation could not be completed within hello permitted time or hello maximum retry attempts possible.</span></span> <span data-ttu-id="b5b9c-346">請重試要求。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-346">Please retry request.</span></span>  
* <span data-ttu-id="b5b9c-347">**風險降低**: hello 的重試要求。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-347">**Mitigation**: Retry hello request.</span></span>

### <span data-ttu-id="b5b9c-348"><a id="ParameterNullOrEmpty"></a>ParameterNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="b5b9c-348"><a id="ParameterNullOrEmpty"></a>ParameterNullOrEmpty</span></span>
* <span data-ttu-id="b5b9c-349">**描述**：參數 *yourParameterName* 不可為 Null 或空白。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-349">**Description**: Parameter *yourParameterName* cannot be null or empty.</span></span>  
* <span data-ttu-id="b5b9c-350">**風險降低**： 指定有效的值為 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-350">**Mitigation**: Specify a valid value for hello parameter.</span></span>

### <span data-ttu-id="b5b9c-351"><a id="PreClusterCreationValidationFailure"></a>PreClusterCreationValidationFailure</span><span class="sxs-lookup"><span data-stu-id="b5b9c-351"><a id="PreClusterCreationValidationFailure"></a>PreClusterCreationValidationFailure</span></span>
* <span data-ttu-id="b5b9c-352">**描述**： 一或多個 hello 叢集建立要求輸入無效。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-352">**Description**: One or more of hello cluster creation request inputs is not valid.</span></span> <span data-ttu-id="b5b9c-353">請確定 hello 輸入的值正確，然後重試要求。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-353">Make sure hello input values are correct and retry request.</span></span>  
* <span data-ttu-id="b5b9c-354">**風險降低**： 請確定 hello 輸入的值是否正確，然後重試要求。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-354">**Mitigation**: Make sure hello input values are correct and retry request.</span></span>

### <span data-ttu-id="b5b9c-355"><a id="RegionCapabilityNotAvailable"></a>RegionCapabilityNotAvailable</span><span class="sxs-lookup"><span data-stu-id="b5b9c-355"><a id="RegionCapabilityNotAvailable"></a>RegionCapabilityNotAvailable</span></span>
* <span data-ttu-id="b5b9c-356">**描述**：區域「yourRegionName」和訂用帳戶識別碼「yourSubscriptionId」無法使用區域功能。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-356">**Description**: Region capability not available for region *yourRegionName* and Subscription ID *yourSubscriptionId*.</span></span>  
* <span data-ttu-id="b5b9c-357">**緩和**：請指定支援 HDInsight 叢集的區域。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-357">**Mitigation**: Specify a region that supports HDInsight clusters.</span></span> <span data-ttu-id="b5b9c-358">公開支援 hello 區域是一種： 東南亞、 西歐、 北歐、 美國東部、 或美國西部。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-358">hello publicly supported regions are: Southeast Asia, West Europe, North Europe, East US, or West US.</span></span>

### <span data-ttu-id="b5b9c-359"><a id="StorageAccountNotColocated"></a>StorageAccountNotColocated</span><span class="sxs-lookup"><span data-stu-id="b5b9c-359"><a id="StorageAccountNotColocated"></a>StorageAccountNotColocated</span></span>
* <span data-ttu-id="b5b9c-360">**描述**：儲存體帳戶「yourStorageAccountName」位於區域「currentRegionName」中。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-360">**Description**: Storage account *yourStorageAccountName* is in region *currentRegionName*.</span></span> <span data-ttu-id="b5b9c-361">它應該是相同 hello 叢區域*yourClusterRegionName*。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-361">It should be same as hello cluster region *yourClusterRegionName*.</span></span>  
* <span data-ttu-id="b5b9c-362">**風險降低**： 指定儲存體帳戶在 hello 叢集位於相同區域中，或如果您的資料已經 hello 儲存體帳戶中，建立新叢集 hello 與 hello 現有儲存體帳戶相同的區域。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-362">**Mitigation**: Either specify a storage account in hello same region that your cluster is in or if your data is already in hello storage account, create a new cluster in hello same region as hello existing storage account.</span></span> <span data-ttu-id="b5b9c-363">如果您使用 hello 入口網站，hello UI 會事先通知他們這個問題。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-363">If you are using hello Portal, hello UI will notify them of this issue in advance.</span></span>

### <span data-ttu-id="b5b9c-364"><a id="SubscriptionIdNotActive"></a>SubscriptionIdNotActive</span><span class="sxs-lookup"><span data-stu-id="b5b9c-364"><a id="SubscriptionIdNotActive"></a>SubscriptionIdNotActive</span></span>
* <span data-ttu-id="b5b9c-365">**描述**：並未使用指定的訂用帳戶識別碼 *yourSubscriptionId* 。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-365">**Description**: Given Subscription ID *yourSubscriptionId* is not active.</span></span>  
* <span data-ttu-id="b5b9c-366">**緩和**：請重新啟用訂用帳戶，或取得新的有效訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-366">**Mitigation**: Re-activate your subscription or get a new valid subscription.</span></span>

### <span data-ttu-id="b5b9c-367"><a id="SubscriptionIdNotFound"></a>SubscriptionIdNotFound</span><span class="sxs-lookup"><span data-stu-id="b5b9c-367"><a id="SubscriptionIdNotFound"></a>SubscriptionIdNotFound</span></span>
* <span data-ttu-id="b5b9c-368">**描述**：找不到訂用帳戶識別碼 *yourSubscriptionId* 。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-368">**Description**: Subscription ID *yourSubscriptionId* could not be found.</span></span>  
* <span data-ttu-id="b5b9c-369">**風險降低**： 請檢查您的訂用帳戶識別碼是否有效，然後重試 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-369">**Mitigation**: Check that your subscription ID is valid and retry hello operation.</span></span>

### <span data-ttu-id="b5b9c-370"><a id="UnableToResolveDNS"></a>UnableToResolveDNS</span><span class="sxs-lookup"><span data-stu-id="b5b9c-370"><a id="UnableToResolveDNS"></a>UnableToResolveDNS</span></span>
* <span data-ttu-id="b5b9c-371">**描述**： 無法 tooresolve DNS *yourDnsUrl*。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-371">**Description**: Unable tooresolve DNS *yourDnsUrl*.</span></span> <span data-ttu-id="b5b9c-372">請中提供 hello blob 端點，確定 hello 完整 URL。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-372">Please ensure hello fully qualified URL for hello blob endpoint is provided.</span></span>  
* <span data-ttu-id="b5b9c-373">**緩和**：提供有效的 Blob URL。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-373">**Mitigation**: Supply a valid blob URL.</span></span> <span data-ttu-id="b5b9c-374">hello URL 必須是完整有效的包括開頭*http://*中和結束*.com*。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-374">hello URL MUST be fully valid, including starting with *http://* and ending in *.com*.</span></span>

### <span data-ttu-id="b5b9c-375"><a id="UnableToVerifyLocationOfResource"></a>UnableToVerifyLocationOfResource</span><span class="sxs-lookup"><span data-stu-id="b5b9c-375"><a id="UnableToVerifyLocationOfResource"></a>UnableToVerifyLocationOfResource</span></span>
* <span data-ttu-id="b5b9c-376">**描述**： 資源無法 tooverify 位置*yourDnsUrl*。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-376">**Description**: Unable tooverify location of resource *yourDnsUrl*.</span></span> <span data-ttu-id="b5b9c-377">請中提供 hello blob 端點，確定 hello 完整 URL。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-377">Please ensure hello fully qualified URL for hello blob endpoint is provided.</span></span>  
* <span data-ttu-id="b5b9c-378">**緩和**：提供有效的 Blob URL。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-378">**Mitigation**: Supply a valid blob URL.</span></span> <span data-ttu-id="b5b9c-379">hello URL 必須是完整有效的包括開頭*http://*中和結束*.com*。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-379">hello URL MUST be fully valid, including starting with *http://* and ending in *.com*.</span></span>

### <span data-ttu-id="b5b9c-380"><a id="VersionCapabilityNotAvailable"></a>VersionCapabilityNotAvailable</span><span class="sxs-lookup"><span data-stu-id="b5b9c-380"><a id="VersionCapabilityNotAvailable"></a>VersionCapabilityNotAvailable</span></span>
* <span data-ttu-id="b5b9c-381">**描述**：版本「specifiedVersion」和訂用帳戶識別碼「yourSubscriptionId」無法使用版本功能。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-381">**Description**: Version capability not available for version *specifiedVersion* and Subscription ID *yourSubscriptionId*.</span></span>  
* <span data-ttu-id="b5b9c-382">**風險降低**： 選擇可用的版本，然後重試 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-382">**Mitigation**: Choose a version that is available and retry hello operation.</span></span>

### <span data-ttu-id="b5b9c-383"><a id="VersionNotSupported"></a>VersionNotSupported</span><span class="sxs-lookup"><span data-stu-id="b5b9c-383"><a id="VersionNotSupported"></a>VersionNotSupported</span></span>
* <span data-ttu-id="b5b9c-384">**描述**：不支援版本 *specifiedVersion* 。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-384">**Description**: Version *specifiedVersion* not supported.</span></span>
* <span data-ttu-id="b5b9c-385">**風險降低**： 選擇支援的版本，然後重試 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-385">**Mitigation**: Choose a version that is supported and retry hello operation.</span></span>

### <span data-ttu-id="b5b9c-386"><a id="VersionNotSupportedInRegion"></a>VersionNotSupportedInRegion</span><span class="sxs-lookup"><span data-stu-id="b5b9c-386"><a id="VersionNotSupportedInRegion"></a>VersionNotSupportedInRegion</span></span>
* <span data-ttu-id="b5b9c-387">**描述**：Azure 區域「specifiedRegion」中無法使用版本「specifiedVersion」。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-387">**Description**: Version *specifiedVersion* is not available in Azure region *specifiedRegion*.</span></span>  
* <span data-ttu-id="b5b9c-388">**風險降低**： 選擇支援指定的 hello 區域中的版本，然後重試 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-388">**Mitigation**: Choose a version that is supported in hello region specified and retry hello operation.</span></span>

### <span data-ttu-id="b5b9c-389"><a id="WasbAccountConfigNotFound"></a>WasbAccountConfigNotFound</span><span class="sxs-lookup"><span data-stu-id="b5b9c-389"><a id="WasbAccountConfigNotFound"></a>WasbAccountConfigNotFound</span></span>
* <span data-ttu-id="b5b9c-390">**描述**：叢集組態無效。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-390">**Description**: Invalid cluster configuration.</span></span> <span data-ttu-id="b5b9c-391">在外部帳戶中找不到必要的 WASB 帳戶組態。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-391">Required WASB account configuration not found in external accounts.</span></span>  
* <span data-ttu-id="b5b9c-392">**風險降低**： 確認 hello 帳戶存在，而且是正常作業中指定的組態，然後重試 hello。</span><span class="sxs-lookup"><span data-stu-id="b5b9c-392">**Mitigation**: Verify that hello account exists and is properly specified in configuration and retry hello operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5b9c-393">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b5b9c-393">Next steps</span></span>
* [<span data-ttu-id="b5b9c-394">HDInsight 上使用 Ambari 檢視 toodebug Tez 作業</span><span class="sxs-lookup"><span data-stu-id="b5b9c-394">Use Ambari Views toodebug Tez Jobs on HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)
* [<span data-ttu-id="b5b9c-395">在以 Linux 為基礎的 HDInsight 上啟用 Hadoop 服務的堆積傾印</span><span class="sxs-lookup"><span data-stu-id="b5b9c-395">Enable heap dumps for Hadoop services on Linux-based HDInsight</span></span>](hdinsight-hadoop-collect-debug-heap-dump-linux.md)
* [<span data-ttu-id="b5b9c-396">使用 hello Ambari Web UI 來管理 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="b5b9c-396">Manage HDInsight clusters by using hello Ambari Web UI</span></span>](hdinsight-hadoop-manage-ambari.md)

