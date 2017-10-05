---
title: "SharePoint 伺服器陣列至 Azure 的 DPM/Azure 備份伺服器保護 | Microsoft Docs"
description: "這篇文章概述 SharePoint 伺服器陣列至 Azure 的 DPM/Azure 備份伺服器保護"
services: backup
documentationcenter: 
author: adigan
manager: Nkolli1
editor: 
ms.assetid: e0c0c252-dc1d-4072-b777-7222c13950b0
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: adigan;giridham;jimpark;trinadhk;markgal
ms.openlocfilehash: 1bbf3233169fa9966e3dd0fac18ee448f26caa6b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-a-sharepoint-farm-to-azure"></a><span data-ttu-id="bc9e2-103">將 SharePoint 伺服器陣列備份到 Azure</span><span class="sxs-lookup"><span data-stu-id="bc9e2-103">Back up a SharePoint farm to Azure</span></span>
<span data-ttu-id="bc9e2-104">您可以使用 System Center Data Protection Manager (DPM)，將 SharePoint 伺服器陣列備份到 Microsoft Azure，其方法與備份其他資料來源極為類似。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-104">You back up a SharePoint farm to Microsoft Azure by using System Center Data Protection Manager (DPM) in much the same way that you back up other data sources.</span></span> <span data-ttu-id="bc9e2-105">Azure 備份提供靈活的備份排程來建立每日、每週、每月或每年備份點，並可讓您針對各種備份點執行保留原則選項。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-105">Azure Backup provides flexibility in the backup schedule to create daily, weekly, monthly, or yearly backup points and gives you retention policy options for various backup points.</span></span> <span data-ttu-id="bc9e2-106">DPM 可讓您儲存本機磁碟複本來快速達成復原時間目標 (RTO)，也可以將複本儲存到 Azure 來進行經濟實惠的長期保留。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-106">DPM provides the capability to store local disk copies for quick recovery-time objectives (RTO) and to store copies to Azure for economical, long-term retention.</span></span>

## <a name="sharepoint-supported-versions-and-related-protection-scenarios"></a><span data-ttu-id="bc9e2-107">SharePoint 支援的版本與相關保護案例</span><span class="sxs-lookup"><span data-stu-id="bc9e2-107">SharePoint supported versions and related protection scenarios</span></span>
<span data-ttu-id="bc9e2-108">DPM 的 Azure 備份支援下列案例：</span><span class="sxs-lookup"><span data-stu-id="bc9e2-108">Azure Backup for DPM supports the following scenarios:</span></span>

| <span data-ttu-id="bc9e2-109">工作負載</span><span class="sxs-lookup"><span data-stu-id="bc9e2-109">Workload</span></span> | <span data-ttu-id="bc9e2-110">版本</span><span class="sxs-lookup"><span data-stu-id="bc9e2-110">Version</span></span> | <span data-ttu-id="bc9e2-111">SharePoint 部署</span><span class="sxs-lookup"><span data-stu-id="bc9e2-111">SharePoint deployment</span></span> | <span data-ttu-id="bc9e2-112">DPM 部署類型</span><span class="sxs-lookup"><span data-stu-id="bc9e2-112">DPM deployment type</span></span> | <span data-ttu-id="bc9e2-113">DPM - System Center 2012 R2</span><span class="sxs-lookup"><span data-stu-id="bc9e2-113">DPM - System Center 2012 R2</span></span> | <span data-ttu-id="bc9e2-114">保護和復原</span><span class="sxs-lookup"><span data-stu-id="bc9e2-114">Protection and recovery</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="bc9e2-115">SharePoint</span><span class="sxs-lookup"><span data-stu-id="bc9e2-115">SharePoint</span></span> |<span data-ttu-id="bc9e2-116">SharePoint 2013、SharePoint 2010、SharePoint 2007、SharePoint 3.0</span><span class="sxs-lookup"><span data-stu-id="bc9e2-116">SharePoint 2013, SharePoint 2010, SharePoint 2007, SharePoint 3.0</span></span> |<span data-ttu-id="bc9e2-117">部署為實體伺服器或 Hyper-V/VMware 虛擬機器的 SharePoint </span><span class="sxs-lookup"><span data-stu-id="bc9e2-117">SharePoint deployed as a physical server or Hyper-V/VMware virtual machine</span></span> <br> -------------- <br> <span data-ttu-id="bc9e2-118">SQL AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="bc9e2-118">SQL AlwaysOn</span></span> |<span data-ttu-id="bc9e2-119">實體伺服器或內部部署 Hyper-V 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="bc9e2-119">Physical server or on-premises Hyper-V virtual machine</span></span> |<span data-ttu-id="bc9e2-120">支援從更新彙總套件 5 備份至 Azure</span><span class="sxs-lookup"><span data-stu-id="bc9e2-120">Supports backup to Azure from Update Rollup 5</span></span> |<span data-ttu-id="bc9e2-121">保護 SharePoint 伺服器陣列復原選項：來自磁碟復原點的復原伺服器陣列、資料庫及檔案或清單項目</span><span class="sxs-lookup"><span data-stu-id="bc9e2-121">Protect SharePoint Farm recovery options: Recovery farm, database, and file or list item from disk recovery points.</span></span>  <span data-ttu-id="bc9e2-122">來自 Azure 復原點的伺服器陣列和資料庫復原。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-122">Farm and database recovery from Azure recovery points.</span></span> |

## <a name="before-you-start"></a><span data-ttu-id="bc9e2-123">開始之前</span><span class="sxs-lookup"><span data-stu-id="bc9e2-123">Before you start</span></span>
<span data-ttu-id="bc9e2-124">您需要先確定幾件事，再將 SharePoint 伺服器陣列備份至 Azure。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-124">There are a few things you need to confirm before you back up a SharePoint farm to Azure.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="bc9e2-125">必要條件</span><span class="sxs-lookup"><span data-stu-id="bc9e2-125">Prerequisites</span></span>
<span data-ttu-id="bc9e2-126">繼續之前，請確定 [使用 Microsoft Azure 備份來保護工作負載的所有必要條件](backup-azure-dpm-introduction.md#prerequisites) 已滿足。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-126">Before you proceed, make sure that you have met all the [prerequisites for using Microsoft Azure Backup](backup-azure-dpm-introduction.md#prerequisites) to protect workloads.</span></span> <span data-ttu-id="bc9e2-127">一些滿足必要條件的工作包括︰建立備份保存庫、下載保存庫認證、安裝 Azure 備份代理程式，以及向保存庫註冊 DPM/Azure 備份伺服器。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-127">Some tasks for prerequisites include: create a backup vault, download vault credentials, install Azure Backup Agent, and register DPM/Azure Backup Server with the vault.</span></span>

### <a name="dpm-agent"></a><span data-ttu-id="bc9e2-128">DPM 代理程式</span><span class="sxs-lookup"><span data-stu-id="bc9e2-128">DPM agent</span></span>
<span data-ttu-id="bc9e2-129">DPM 代理程式必須安裝在執行 SharePoint 的伺服器、執行 SQL Server 的伺服器，以及隸屬於 SharePoint 伺服器陣列的其他任何伺服器上。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-129">The DPM agent must be installed on the server that's running SharePoint, the servers that are running SQL Server, and all other servers that are part of the SharePoint farm.</span></span> <span data-ttu-id="bc9e2-130">如需設定保護代理程式的詳細資訊，請參閱[設定保護代理程式](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx)。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-130">For more information about how to set up the protection agent, see [Setup Protection Agent](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).</span></span>  <span data-ttu-id="bc9e2-131">唯一的例外是您只能在單一 Web 前端 (WFE) 伺服器上安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-131">The one exception is that you install the agent only on a single web front end (WFE) server.</span></span> <span data-ttu-id="bc9e2-132">DPM 只需要將 WFE 伺服器上的代理程式做為保護的進入點。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-132">DPM needs the agent on one WFE server only to serve as the entry point for protection.</span></span>

### <a name="sharepoint-farm"></a><span data-ttu-id="bc9e2-133">SharePoint 伺服器陣列</span><span class="sxs-lookup"><span data-stu-id="bc9e2-133">SharePoint farm</span></span>
<span data-ttu-id="bc9e2-134">針對伺服器陣列中每 1000 萬個項目，必須有至少 2 GB 的磁碟區空間來放置 DPM 資料夾。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-134">For every 10 million items in the farm, there must be at least 2 GB of space on the volume where the DPM folder is located.</span></span> <span data-ttu-id="bc9e2-135">此空間對目錄產生是必要的。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-135">This space is required for catalog generation.</span></span> <span data-ttu-id="bc9e2-136">若要讓 DPM 復原特定項目 (網站集合、網站、清單、文件庫、資料夾、個別的文件與清單項目)，目錄產生會建立一份包含在每個內容資料庫內的 URL 清單。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-136">For DPM to recover specific items (site collections, sites, lists, document libraries, folders, individual documents, and list items), catalog generation creates a list of the URLs that are contained within each content database.</span></span> <span data-ttu-id="bc9e2-137">您可以在 DPM 系統管理員主控台的 [復原]  工作區中，檢視 [可復原項目] 窗格中的 URL 清單。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-137">You can view the list of URLs in the recoverable item pane in the **Recovery** task area of DPM Administrator Console.</span></span>

### <a name="sql-server"></a><span data-ttu-id="bc9e2-138">SQL Server</span><span class="sxs-lookup"><span data-stu-id="bc9e2-138">SQL Server</span></span>
<span data-ttu-id="bc9e2-139">DPM 會以 LocalSystem 帳戶身分執行。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-139">DPM runs as a LocalSystem account.</span></span> <span data-ttu-id="bc9e2-140">若要備份 SQL Server 資料庫，DPM 需要執行 SQL Server 之伺服器上該帳戶的 sysadmin 權限。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-140">To back up SQL Server databases, DPM needs sysadmin privileges on that account for the server that's running SQL Server.</span></span> <span data-ttu-id="bc9e2-141">備份之前，將執行 SQL Server 之伺服器上的 NT AUTHORITY\SYSTEM 設定為 *sysadmin*。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-141">Set NT AUTHORITY\SYSTEM to *sysadmin* on the server that's running SQL Server before you back it up.</span></span>

<span data-ttu-id="bc9e2-142">如果 SharePoint 伺服器陣列有使用 SQL Server 別名設定的 SQL Server 資料庫，請在 DPM 將保護的前端 Web 伺服器上安裝 SQL Server 用戶端元件。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-142">If the SharePoint farm has SQL Server databases that are configured with SQL Server aliases, install the SQL Server client components on the front-end Web server that DPM will protect.</span></span>

### <a name="sharepoint-server"></a><span data-ttu-id="bc9e2-143">SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="bc9e2-143">SharePoint Server</span></span>
<span data-ttu-id="bc9e2-144">雖然效能取決於許多因素，例如 SharePoint 伺服器陣列的大小，但一般的做法是將一部 DPM 伺服器用來保護 25 TB SharePoint 伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-144">While performance depends on many factors such as size of SharePoint farm, as general guidance one DPM server can protect a 25 TB SharePoint farm.</span></span>

### <a name="dpm-update-rollup-5"></a><span data-ttu-id="bc9e2-145">DPM 更新彙總套件 5</span><span class="sxs-lookup"><span data-stu-id="bc9e2-145">DPM Update Rollup 5</span></span>
<span data-ttu-id="bc9e2-146">若要開始針對 Azure 保護 SharePoint 伺服器，您需要安裝 DPM 更新彙總套件 5 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-146">To begin protection of a SharePoint farm to Azure, you need to install DPM Update Rollup 5 or later.</span></span> <span data-ttu-id="bc9e2-147">更新彙總套件 5 提供針對 Azure 保護 SharePoint 伺服器陣列的功能 (如果已使用 SQL AlwaysOn 設定伺服器陣列)。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-147">Update Rollup 5 provides the ability to protect a SharePoint farm to Azure if the farm is configured by using SQL AlwaysOn.</span></span>
<span data-ttu-id="bc9e2-148">如需詳細資訊，請參閱介紹 [DPM 更新彙總套件 5](http://blogs.technet.com/b/dpm/archive/2015/02/11/update-rollup-5-for-system-center-2012-r2-data-protection-manager-is-now-available.aspx)</span><span class="sxs-lookup"><span data-stu-id="bc9e2-148">For more information, see the blog post that introduces [DPM Update Rollup 5](http://blogs.technet.com/b/dpm/archive/2015/02/11/update-rollup-5-for-system-center-2012-r2-data-protection-manager-is-now-available.aspx)</span></span>

### <a name="whats-not-supported"></a><span data-ttu-id="bc9e2-149">不支援的內容</span><span class="sxs-lookup"><span data-stu-id="bc9e2-149">What's not supported</span></span>
* <span data-ttu-id="bc9e2-150">保護 SharePoint 伺服器陣列的 DPM 不會保護搜尋索引或應用程式服務資料庫。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-150">DPM that protects a SharePoint farm does not protect search indexes or application service databases.</span></span> <span data-ttu-id="bc9e2-151">您必須個別設定這些資料庫的保護。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-151">You will need to configure the protection of these databases separately.</span></span>
* <span data-ttu-id="bc9e2-152">DPM 不提供相應放大檔案伺服器 (SOFS) 共用所裝載的 SharePoint SQL Server 資料庫備份。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-152">DPM does not provide backup of SharePoint SQL Server databases that are hosted on scale-out file server (SOFS) shares.</span></span>

## <a name="configure-sharepoint-protection"></a><span data-ttu-id="bc9e2-153">設定 SharePoint 保護</span><span class="sxs-lookup"><span data-stu-id="bc9e2-153">Configure SharePoint protection</span></span>
<span data-ttu-id="bc9e2-154">您必須先使用 **ConfigureSharePoint.exe**來設定「SharePoint VSS 寫入器」服務 (「WSS 寫入器」服務)，才能使用 DPM 來保護 SharePoint。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-154">Before you can use DPM to protect SharePoint, you must configure the SharePoint VSS Writer service (WSS Writer service) by using **ConfigureSharePoint.exe**.</span></span>

<span data-ttu-id="bc9e2-155">您可以在前端 Web 伺服器的 [DPM 安裝路徑]\bin 資料夾中找到 **ConfigureSharePoint.exe**。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-155">You can find **ConfigureSharePoint.exe** in the [DPM Installation Path]\bin folder on the front-end web server.</span></span> <span data-ttu-id="bc9e2-156">這項工具可將 SharePoint 伺服器陣列的認證提供給保護代理程式。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-156">This tool provides the protection agent with the credentials for the SharePoint farm.</span></span> <span data-ttu-id="bc9e2-157">您在單一 WFE 伺服器上執行。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-157">You run it on a single WFE server.</span></span> <span data-ttu-id="bc9e2-158">如果您有多部 WFE 伺服器，在設定保護群組時請選取其中一部。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-158">If you have multiple WFE servers, select just one when you configure a protection group.</span></span>

### <a name="to-configure-the-sharepoint-vss-writer-service"></a><span data-ttu-id="bc9e2-159">設定 SharePoint VSS 寫入器服務</span><span class="sxs-lookup"><span data-stu-id="bc9e2-159">To configure the SharePoint VSS Writer service</span></span>
1. <span data-ttu-id="bc9e2-160">在 WFE 伺服器上，在命令提示字元中移至 [DPM 安裝位置]\bin\\</span><span class="sxs-lookup"><span data-stu-id="bc9e2-160">On the WFE server, at a command prompt, go to [DPM installation location]\bin\\</span></span>
2. <span data-ttu-id="bc9e2-161">輸入 ConfigureSharePoint -EnableSharePointProtection</span><span class="sxs-lookup"><span data-stu-id="bc9e2-161">Enter ConfigureSharePoint -EnableSharePointProtection.</span></span>
3. <span data-ttu-id="bc9e2-162">輸入伺服器陣列系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-162">Enter the farm administrator credentials.</span></span> <span data-ttu-id="bc9e2-163">這個帳戶應該是 WFE 伺服器上本機 Administrator 群組的成員。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-163">This account should be a member of the local Administrator group on the WFE server.</span></span> <span data-ttu-id="bc9e2-164">如果伺服器陣列系統管理員不是本機系統管理員，請授與 WFE 伺服器上的下列權限：</span><span class="sxs-lookup"><span data-stu-id="bc9e2-164">If the farm administrator isn’t a local admin grant the following permissions on the WFE server:</span></span>
   * <span data-ttu-id="bc9e2-165">授與 DPM 資料夾的 WSS_Admin_WPG 群組完整控制權 (%Program Files%\Microsoft Data Protection Manager\DPM)。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-165">Grant the WSS_Admin_WPG group full control to the DPM folder (%Program Files%\Microsoft Data Protection Manager\DPM).</span></span>
   * <span data-ttu-id="bc9e2-166">將 DPM 登錄機碼的讀取權授與 WSS_Admin_WPG 群組 (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager)。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-166">Grant the WSS_Admin_WPG group read access to the DPM Registry key (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).</span></span>

> [!NOTE]
> <span data-ttu-id="bc9e2-167">每當 SharePoint 伺服器陣列系統管理員認證變更時，就必須重新執行 ConfigureSharePoint.exe。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-167">You’ll need to rerun ConfigureSharePoint.exe whenever there’s a change in the SharePoint farm administrator credentials.</span></span>
> 
> 

## <a name="back-up-a-sharepoint-farm-by-using-dpm"></a><span data-ttu-id="bc9e2-168">使用 DPM 備份 SharePoint 伺服器陣列</span><span class="sxs-lookup"><span data-stu-id="bc9e2-168">Back up a SharePoint farm by using DPM</span></span>
<span data-ttu-id="bc9e2-169">在設定 DPM 和 SharePoint 伺服器陣列 (如上所述) 之後，SharePoint 就可以受 DPM 保護。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-169">After you have configured DPM and the SharePoint farm as explained previously, SharePoint can be protected by DPM.</span></span>

### <a name="to-protect-a-sharepoint-farm"></a><span data-ttu-id="bc9e2-170">保護 SharePoint 伺服器陣列</span><span class="sxs-lookup"><span data-stu-id="bc9e2-170">To protect a SharePoint farm</span></span>
1. <span data-ttu-id="bc9e2-171">從 [DPM 管理主控台] 的 [保護] 索引標籤中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-171">From the **Protection** tab of the DPM Administrator Console, click **New**.</span></span>
    <span data-ttu-id="bc9e2-172">![[新增保護] 索引標籤](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)</span><span class="sxs-lookup"><span data-stu-id="bc9e2-172">![New Protection Tab](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)</span></span>
2. <span data-ttu-id="bc9e2-173">在 [建立新保護群組] 精靈的 [選擇保護群組類型] 頁面上，選取 [伺服器]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-173">On the **Select Protection Group Type** page of the **Create New Protection Group** wizard, select **Servers**, and then click **Next**.</span></span>
   
    ![選擇保護群組類型](./media/backup-azure-backup-sharepoint/select-protection-group-type.png)
3. <span data-ttu-id="bc9e2-175">在 [選擇群組成員] 畫面上，選取您想要保護的 SharePoint 伺服器的核取方塊，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-175">On the **Select Group Members** screen, select the check box for the SharePoint server you want to protect and click **Next**.</span></span>
   
    ![選擇群組成員](./media/backup-azure-backup-sharepoint/select-group-members2.png)
   
   > [!NOTE]
   > <span data-ttu-id="bc9e2-177">在已安裝 DPM 代理程式的情況下，您會在精靈中看到伺服器。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-177">With the DPM agent installed, you can see the server in the wizard.</span></span> <span data-ttu-id="bc9e2-178">DPM 也會顯示其結構。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-178">DPM also shows its structure.</span></span> <span data-ttu-id="bc9e2-179">由於已執行 ConfigureSharePoint.exe，DPM 會與 SharePoint VSS 寫入器服務及其對應的 SQL 資料庫通訊，並辨識 SharePoint 伺服器陣列結構、相關聯的內容資料庫和任何對應的項目。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-179">Because you ran ConfigureSharePoint.exe, DPM communicates with the SharePoint VSS Writer service and its corresponding SQL Server databases and recognizes the SharePoint farm structure, the associated content databases, and any corresponding items.</span></span>
   > 
   > 
4. <span data-ttu-id="bc9e2-180">在 [選擇資料保護方式] 頁面上，輸入**保護群組**的名稱，然後選取您偏好的*保護方式*。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-180">On the **Select Data Protection Method** page, enter the name of the **Protection Group**, and select your preferred *protection methods*.</span></span> <span data-ttu-id="bc9e2-181">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-181">Click **Next**.</span></span>
   
    ![選擇資料保護方式](./media/backup-azure-backup-sharepoint/select-data-protection-method1.png)
   
   > [!NOTE]
   > <span data-ttu-id="bc9e2-183">磁碟保護方法有助於達成短暫的復原時間目標。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-183">The disk protection method helps to meet short recovery-time objectives.</span></span> <span data-ttu-id="bc9e2-184">相較於磁帶，Azure 是經濟實惠的長期保護目標。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-184">Azure is an economical, long-term protection target compared to tapes.</span></span> <span data-ttu-id="bc9e2-185">如需詳細資訊，請參閱 [使用 Azure 備份來取代您的磁帶基礎結構](https://azure.microsoft.com/documentation/articles/backup-azure-backup-cloud-as-tape/)</span><span class="sxs-lookup"><span data-stu-id="bc9e2-185">For more information, see [Use Azure Backup to replace your tape infrastructure](https://azure.microsoft.com/documentation/articles/backup-azure-backup-cloud-as-tape/)</span></span>
   > 
   > 
5. <span data-ttu-id="bc9e2-186">在 [指定短期目標] 頁面上，選取您偏好的**保留範圍**，然後識別您想要進行備份的時間。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-186">On the **Specify Short-Term Goals** page, select your preferred **Retention range** and identify when you want backups to occur.</span></span>
   
    ![指定短期目標](./media/backup-azure-backup-sharepoint/specify-short-term-goals2.png)
   
   > [!NOTE]
   > <span data-ttu-id="bc9e2-188">由於復原大部分是針對少於五天的資料進行，因此我們針對此範例選取磁碟上五天保留範圍，並確保在非生產時段進行備份。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-188">Because recovery is most often required for data that's less than five days old, we selected a retention range of five days on disk and ensured that the backup happens during non-production hours, for this example.</span></span>
   > 
   > 
6. <span data-ttu-id="bc9e2-189">檢閱為保護群組配置的存放集區磁碟空間，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-189">Review the storage pool disk space allocated for the protection group, and click then **Next**.</span></span>
7. <span data-ttu-id="bc9e2-190">針對每個保護群組，DPM 會配置磁碟空間來儲存和管理複本。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-190">For every protection group, DPM allocates disk space to store and manage replicas.</span></span> <span data-ttu-id="bc9e2-191">此時，DPM 必須建立所選資料的複本。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-191">At this point, DPM must create a copy of the selected data.</span></span> <span data-ttu-id="bc9e2-192">選取您希望建立複本的方式和時間，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-192">Select how and when you want the replica created, and then click **Next**.</span></span>
   
    ![選擇複本的建立方式](./media/backup-azure-backup-sharepoint/choose-replica-creation-method.png)
   
   > [!NOTE]
   > <span data-ttu-id="bc9e2-194">若要確保不影響網路流量，請選取生產時段之外的時間。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-194">To make sure that network traffic is not effected, select a time outside production hours.</span></span>
   > 
   > 
8. <span data-ttu-id="bc9e2-195">DPM 可為複本執行一致性檢查，以確保資料完整性。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-195">DPM ensures data integrity by performing consistency checks on the replica.</span></span> <span data-ttu-id="bc9e2-196">有兩個可用的選項。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-196">There are two available options.</span></span> <span data-ttu-id="bc9e2-197">您可以定義執行一致性檢查的排程，DPM 也可以在複本變得不一致時自動執行一致性檢查。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-197">You can define a schedule to run consistency checks, or DPM can run consistency checks automatically on the replica whenever it becomes inconsistent.</span></span> <span data-ttu-id="bc9e2-198">選取您慣用的選項，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-198">Select your preferred option, and then click **Next**.</span></span>
   
    ![一致性檢查](./media/backup-azure-backup-sharepoint/consistency-check.png)
9. <span data-ttu-id="bc9e2-200">在 [指定線上保護資料] 頁面上，選取您想要保護的 SharePoint 伺服器陣列，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-200">On the **Specify Online Protection Data** page, select the SharePoint farm that you want to protect, and then click **Next**.</span></span>
   
    ![DPM SharePoint Protection1](./media/backup-azure-backup-sharepoint/select-online-protection1.png)
10. <span data-ttu-id="bc9e2-202">在 [指定線上備份排程] 頁面上，選取您慣用的排程，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-202">On the **Specify Online Backup Schedule** page, select your preferred schedule, and then click **Next**.</span></span>
    
    ![Online_backup_schedule](./media/backup-azure-backup-sharepoint/specify-online-backup-schedule.png)
    
    > [!NOTE]
    > <span data-ttu-id="bc9e2-204">DPM 允許您在每天不同時間以 Azure 為目標執行兩次備份。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-204">DPM provides a maximum of two daily backups to Azure at different times.</span></span> <span data-ttu-id="bc9e2-205">Azure 備份也可以利用 [Azure 備份網路節流](https://azure.microsoft.com/en-in/documentation/articles/backup-configure-vault/#enable-network-throttling)來控制尖峰和離峰時間用於備份的 WAN 頻寬。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-205">Azure Backup can also control the amount of WAN bandwidth that can be used for backups in peak and off-peak hours by using [Azure Backup Network Throttling](https://azure.microsoft.com/en-in/documentation/articles/backup-configure-vault/#enable-network-throttling).</span></span>
    > 
    > 
11. <span data-ttu-id="bc9e2-206">依選取的備份排程，請在 [ **指定線上保留原則** ] 頁面上，選取每日、每週、每月和每年備份點的保留原則。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-206">Depending on the backup schedule that you selected, on the **Specify Online Retention Policy** page, select the retention policy for daily, weekly, monthly, and yearly backup points.</span></span>
    
    ![Online_retention_policy](./media/backup-azure-backup-sharepoint/specify-online-retention.png)
    
    > [!NOTE]
    > <span data-ttu-id="bc9e2-208">DPM 會使用 grandfather-father-son 配置，可讓您為不同的備份時間點選擇不同的保留原則。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-208">DPM uses a grandfather-father-son retention scheme in which a different retention policy can be chosen for different backup points.</span></span>
    > 
    > 
12. <span data-ttu-id="bc9e2-209">類似於磁碟，需要在 Azure 中建立初始參考點複本。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-209">Similar to disk, an initial reference point replica needs to be created in Azure.</span></span> <span data-ttu-id="bc9e2-210">選取用於在 Azure 中建立初始備份複本的慣用選項，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-210">Select your preferred option to create an initial backup copy to Azure, and then click **Next**.</span></span>
    
    ![Online_replica](./media/backup-azure-backup-sharepoint/online-replication.png)
13. <span data-ttu-id="bc9e2-212">在 [摘要] 頁面上檢閱您選取的設定，然後按一下 [建立群組]。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-212">Review your selected settings on the **Summary** page, and then click **Create Group**.</span></span> <span data-ttu-id="bc9e2-213">建立保護群組之後，您會看到成功訊息。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-213">You will see a success message after the protection group has been created.</span></span>
    
    ![摘要](./media/backup-azure-backup-sharepoint/summary.png)

## <a name="restore-a-sharepoint-item-from-disk-by-using-dpm"></a><span data-ttu-id="bc9e2-215">使用 DPM 從磁碟還原 SharePoint 項目</span><span class="sxs-lookup"><span data-stu-id="bc9e2-215">Restore a SharePoint item from disk by using DPM</span></span>
<span data-ttu-id="bc9e2-216">在下列範例中， *Recovering SharePoint item* 已被意外刪除，而需要復原。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-216">In the following example, the *Recovering SharePoint item* has been accidentally deleted and needs to be recovered.</span></span>
<span data-ttu-id="bc9e2-217">![DPM SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)</span><span class="sxs-lookup"><span data-stu-id="bc9e2-217">![DPM SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)</span></span>

1. <span data-ttu-id="bc9e2-218">開啟 [DPM 管理主控台] 。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-218">Open the **DPM Administrator Console**.</span></span> <span data-ttu-id="bc9e2-219">DPM 保護的所有 SharePoint 伺服器陣列都會顯示在 [保護]  索引標籤中。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-219">All SharePoint farms that are protected by DPM are shown in the **Protection** tab.</span></span>
   
    ![DPM SharePoint Protection3](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection4.png)
2. <span data-ttu-id="bc9e2-221">若要開始復原項目，請選取 [復原]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-221">To begin to recover the item, select the **Recovery** tab.</span></span>
   
    ![DPM SharePoint Protection5](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection6.png)
3. <span data-ttu-id="bc9e2-223">您可以使用萬用字元型搜尋，在復原點範圍內搜尋 SharePoint 中的 *Recovering SharePoint item* 。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-223">You can search SharePoint for *Recovering SharePoint item* by using a wildcard-based search within a recovery point range.</span></span>
   
    ![DPM SharePoint Protection6](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection7.png)
4. <span data-ttu-id="bc9e2-225">從搜尋結果中選取適當的復原點，以滑鼠右鍵按一下項目，然後選取 [復原]。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-225">Select the appropriate recovery point from the search results, right-click the item, and then select **Recover**.</span></span>
5. <span data-ttu-id="bc9e2-226">您也可以瀏覽不同的復原點，並選取要復原的資料庫或項目。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-226">You can also browse through various recovery points and select a database or item to recover.</span></span> <span data-ttu-id="bc9e2-227">選取 [日期] > [復原時間]，然後選取正確的 [資料庫] > [SharePoint 伺服器陣列] > [復原點] > [項目]。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-227">Select **Date > Recovery time**, and then select the correct **Database > SharePoint farm > Recovery point > Item**.</span></span>
   
    ![DPM SharePoint Protection7](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection8.png)
6. <span data-ttu-id="bc9e2-229">在該項目上按一下滑鼠右鍵，然後選取 [復原] 以開啟 [復原精靈]。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-229">Right-click the item, and then select **Recover** to open the **Recovery Wizard**.</span></span> <span data-ttu-id="bc9e2-230">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-230">Click **Next**.</span></span>
   
    ![檢閱復原選項](./media/backup-azure-backup-sharepoint/review-recovery-selection.png)
7. <span data-ttu-id="bc9e2-232">選取您想要執行的復原類型，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-232">Select the type of recovery that you want to perform, and then click **Next**.</span></span>
   
    ![復原類型](./media/backup-azure-backup-sharepoint/select-recovery-type.png)
   
   > [!NOTE]
   > <span data-ttu-id="bc9e2-234">範例中選取的 [復原到原始] 會將項目復原到原始的 SharePoint 網站。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-234">The selection of **Recover to original** in the example recovers the item to the original SharePoint site.</span></span>
   > 
   > 
8. <span data-ttu-id="bc9e2-235">選取您想要使用的 [復原程序]  。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-235">Select the **Recovery Process** that you want to use.</span></span>
   
   * <span data-ttu-id="bc9e2-236">如果 SharePoint 伺服器陣列並未變更，並且與正在還原的復原點相同，請選取 [不使用復原伺服器陣列執行復原]  。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-236">Select **Recover without using a recovery farm** if the SharePoint farm has not changed and is the same as the recovery point that is being restored.</span></span>
   * <span data-ttu-id="bc9e2-237">如果 SharePoint 伺服器陣列自建立復原點後已變更，請選取 [使用復原伺服器陣列執行復原]  。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-237">Select **Recover using a recovery farm** if the SharePoint farm has changed since the recovery point was created.</span></span>
     
     ![復原程序](./media/backup-azure-backup-sharepoint/recovery-process.png)
9. <span data-ttu-id="bc9e2-239">提供暫時復原資料庫的預備 SQL Server 執行個體位置，並在要復原項目的 DPM 伺服器和執行 SharePoint 的伺服器上提供預備檔案共用。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-239">Provide a staging SQL Server instance location to recover the database temporarily, and provide a staging file share on the DPM server and the server that's running SharePoint to recover the item.</span></span>
   
    ![Staging Location1](./media/backup-azure-backup-sharepoint/staging-location1.png)
   
    <span data-ttu-id="bc9e2-241">DPM 會將裝載 SharePoint 項目的內容資料庫附加至暫存 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-241">DPM attaches the content database that is hosting the SharePoint item to the temporary SQL Server instance.</span></span> <span data-ttu-id="bc9e2-242">從內容資料庫，DPM 伺服器會復原項目，並將它放在 DPM 伺服器上的預備檔案位置。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-242">From the content database, the DPM server recovers the item and puts it on the staging file location on the DPM server.</span></span> <span data-ttu-id="bc9e2-243">在 DPM 伺服器預備位置上的復原項目，現在需要匯出至 SharePoint 伺服器陣列上的預備位置。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-243">The recovered item that's on the staging location of the DPM server now needs to be exported to the staging location on the SharePoint farm.</span></span>
   
    ![Staging Location2](./media/backup-azure-backup-sharepoint/staging-location2.png)
10. <span data-ttu-id="bc9e2-245">選取 [指定復原選項] ，並將安全性設定套用至 SharePoint 伺服器陣列，或套用復原點的安全性設定。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-245">Select **Specify recovery options**, and apply security settings to the SharePoint farm or apply the security settings of the recovery point.</span></span> <span data-ttu-id="bc9e2-246">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-246">Click **Next**.</span></span>
    
    ![修復選項](./media/backup-azure-backup-sharepoint/recovery-options.png)
    
    > [!NOTE]
    > <span data-ttu-id="bc9e2-248">您可以選擇調節網路頻寬使用量。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-248">You can choose to throttle the network bandwidth usage.</span></span> <span data-ttu-id="bc9e2-249">這會對生產時段的生產伺服器產生最小的影響。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-249">This minimizes impact to the production server during production hours.</span></span>
    > 
    > 
11. <span data-ttu-id="bc9e2-250">檢閱摘要資訊，然後按一下 [復原]  以開始復原檔案。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-250">Review the summary information, and then click **Recover** to begin recovery of the file.</span></span>
    
    ![復原摘要](./media/backup-azure-backup-sharepoint/recovery-summary.png)
12. <span data-ttu-id="bc9e2-252">現在，在 [DPM 管理主控台] 中選取 [監視] 索引標籤，以檢視復原的**狀態**。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-252">Now select the **Monitoring** tab in the **DPM Administrator Console** to view the **Status** of the recovery.</span></span>
    
    ![復原狀態](./media/backup-azure-backup-sharepoint/recovery-monitoring.png)
    
    > [!NOTE]
    > <span data-ttu-id="bc9e2-254">現在即可還原檔案。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-254">The file is now restored.</span></span> <span data-ttu-id="bc9e2-255">您可以重新整理 SharePoint 網站來檢查已還原的檔案。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-255">You can refresh the SharePoint site to check the restored file.</span></span>
    > 
    > 

## <a name="restore-a-sharepoint-database-from-azure-by-using-dpm"></a><span data-ttu-id="bc9e2-256">使用 DPM 從 Azure 中還原 SharePoint 資料庫</span><span class="sxs-lookup"><span data-stu-id="bc9e2-256">Restore a SharePoint database from Azure by using DPM</span></span>
1. <span data-ttu-id="bc9e2-257">若要復原 SharePoint 內容資料庫，請瀏覽各種復原點 (如上所示)，並選取要還原的復原點。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-257">To recover a SharePoint content database, browse through various recovery points (as shown previously), and select the recovery point that you want to restore.</span></span>
   
    ![DPM SharePoint Protection8](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection9.png)
2. <span data-ttu-id="bc9e2-259">按兩下 SharePoint 復原點以顯示可用的 SharePoint 目錄資訊。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-259">Double-click the SharePoint recovery point to show the available SharePoint catalog information.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="bc9e2-260">由於 SharePoint 伺服器陣列在 Azure 中受長期保留保護，因此 DPM 伺服器上沒有可用的目錄資訊 (元資料)。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-260">Because the SharePoint farm is protected for long-term retention in Azure, no catalog information (metadata) is available on the DPM server.</span></span> <span data-ttu-id="bc9e2-261">如此一來，每當需要復原時間點 SharePoint 內容資料庫，您就需要重新編目 SharePoint 伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-261">As a result, whenever a point-in-time SharePoint content database needs to be recovered, you need to catalog the SharePoint farm again.</span></span>
   > 
   > 
3. <span data-ttu-id="bc9e2-262">按一下 [重新編目] 。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-262">Click **Re-catalog**.</span></span>
   
    ![DPM SharePoint Protection10](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection12.png)
   
    <span data-ttu-id="bc9e2-264">[雲端重新編目]  狀態視窗隨即會開啟。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-264">The **Cloud Recatalog** status window opens.</span></span>
   
    ![DPM SharePoint Protection11](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection13.png)
   
    <span data-ttu-id="bc9e2-266">完成編目後，狀態會變更為 [成功] 。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-266">After cataloging is finished, the status changes to *Success*.</span></span> <span data-ttu-id="bc9e2-267">按一下 [關閉] 。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-267">Click **Close**.</span></span>
   
    ![DPM SharePoint Protection12](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection14.png)
4. <span data-ttu-id="bc9e2-269">按一下 DPM [復原]  索引標籤中顯示的 SharePoint 物件，以取得內容資料庫結構。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-269">Click the SharePoint object shown in the DPM **Recovery** tab to get the content database structure.</span></span> <span data-ttu-id="bc9e2-270">在項目上按一下滑鼠右鍵，然後按一下 [復原] 。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-270">Right-click the item, and then click **Recover**.</span></span>
   
    ![DPM SharePoint Protection13](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection15.png)
5. <span data-ttu-id="bc9e2-272">此時，依照 [本文前述的復原步驟](#restore-a-sharepoint-item-from-disk-using-dpm) ，從磁碟復原 Sharepoint 內容資料庫。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-272">At this point, follow the [recovery steps earlier in this article](#restore-a-sharepoint-item-from-disk-using-dpm) to recover a SharePoint content database from disk.</span></span>

## <a name="faqs"></a><span data-ttu-id="bc9e2-273">常見問題集</span><span class="sxs-lookup"><span data-stu-id="bc9e2-273">FAQs</span></span>
<span data-ttu-id="bc9e2-274">問︰哪些版本的 DPM 支援 SQL Server 2014 和 SQL 2012 (SP2)？</span><span class="sxs-lookup"><span data-stu-id="bc9e2-274">Q: Which versions of DPM support SQL Server 2014 and SQL 2012 (SP2)?</span></span><br>
<span data-ttu-id="bc9e2-275">答︰DPM 2012 R2 更新彙總套件 4 支援兩者。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-275">A: DPM 2012 R2 with Update Rollup 4 supports both.</span></span>

<span data-ttu-id="bc9e2-276">問：如果使用 SQL AlwaysOn (使用磁碟上保護) 設定 SharePoint，我是否能將 SharePoint 項目復原到原始位置？</span><span class="sxs-lookup"><span data-stu-id="bc9e2-276">Q: Can I recover a SharePoint item to the original location if SharePoint is configured by using SQL AlwaysOn (with protection on disk)?</span></span><br>
<span data-ttu-id="bc9e2-277">答：可以，項目可以復原到原始的 SharePoint 網站。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-277">A: Yes, the item can be recovered to the original SharePoint site.</span></span>

<span data-ttu-id="bc9e2-278">問：如果使用 SQL AlwaysOn 設定 SharePoint，我是否能將 SharePoint 資料庫復原到原始位置？</span><span class="sxs-lookup"><span data-stu-id="bc9e2-278">Q: Can I recover a SharePoint database to the original location if SharePoint is configured by using SQL AlwaysOn?</span></span><br>
<span data-ttu-id="bc9e2-279">答：由於 SharePoint 資料庫是在 SQL AlwaysOn 中設定，所以除非移除可用性群組，否則無法修改它們。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-279">A: Because SharePoint databases are configured in SQL AlwaysOn, they cannot be modified unless the availability group is removed.</span></span> <span data-ttu-id="bc9e2-280">因此，DPM 無法將資料庫還原到原始位置。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-280">As a result, DPM cannot restore a database to the original location.</span></span> <span data-ttu-id="bc9e2-281">您可以將 SQL Server 資料庫復原到其他 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="bc9e2-281">You can recover a SQL Server database to another SQL Server instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc9e2-282">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bc9e2-282">Next steps</span></span>
* <span data-ttu-id="bc9e2-283">深入了解 DPM 的 SharePoint 保護 - 請參閱 [影片系列 - DPM 的 SharePoint 保護](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)</span><span class="sxs-lookup"><span data-stu-id="bc9e2-283">Learn more about DPM Protection of SharePoint - see [Video Series - DPM Protection of SharePoint](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)</span></span>
* <span data-ttu-id="bc9e2-284">檢閱 [System Center 2012 - Data Protection Manager 版本資訊](https://technet.microsoft.com/library/jj860415.aspx)</span><span class="sxs-lookup"><span data-stu-id="bc9e2-284">Review [Release Notes for System Center 2012 - Data Protection Manager](https://technet.microsoft.com/library/jj860415.aspx)</span></span>
* <span data-ttu-id="bc9e2-285">檢閱 [System Center 2012 SP1 的 Data Protection Manager 版本資訊](https://technet.microsoft.com/library/jj860394.aspx)</span><span class="sxs-lookup"><span data-stu-id="bc9e2-285">Review [Release Notes for Data Protection Manager in System Center 2012 SP1](https://technet.microsoft.com/library/jj860394.aspx)</span></span>

