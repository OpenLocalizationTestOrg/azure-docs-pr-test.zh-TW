---
title: "使用 Azure 備份伺服器將 SharePoint 伺服器陣列備份至 Azure | Microsoft Docs"
description: "使用 Azure 備份伺服器來備份和還原 SharePoint 資料。 本文提供設定 SharePoint 伺服器陣列，讓所需的資料可以儲存在 Azure 中的相關資訊。 您可以從磁碟或 Azure 還原受保護的 SharePoint 資料。"
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
ms.assetid: 34ba87a4-91f1-4054-a4a1-272af1e15496
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: 3ed000affd326eb1bd7c99773ec021ad6e03cc3b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-a-sharepoint-farm-to-azure"></a><span data-ttu-id="88c8b-105">將 SharePoint 伺服器陣列備份到 Azure</span><span class="sxs-lookup"><span data-stu-id="88c8b-105">Back up a SharePoint farm to Azure</span></span>
<span data-ttu-id="88c8b-106">您可以使用 Microsoft Azure 備份伺服器 (MABS)，將 SharePoint 伺服器陣列備份到 Microsoft Azure，其方法與備份其他資料來源極為類似。</span><span class="sxs-lookup"><span data-stu-id="88c8b-106">You back up a SharePoint farm to Microsoft Azure by using Microsoft Azure Backup Server (MABS) in much the same way that you back up other data sources.</span></span> <span data-ttu-id="88c8b-107">Azure 備份提供靈活的備份排程來建立每日、每週、每月或每年備份點，並可讓您針對各種備份點執行保留原則選項。</span><span class="sxs-lookup"><span data-stu-id="88c8b-107">Azure Backup provides flexibility in the backup schedule to create daily, weekly, monthly, or yearly backup points and gives you retention policy options for various backup points.</span></span> <span data-ttu-id="88c8b-108">它也可以讓您儲存本機磁碟複本來快速達成復原時間目標 (RTO)，以及將複本儲存到 Azure 來進行經濟實惠的長期保留。</span><span class="sxs-lookup"><span data-stu-id="88c8b-108">It also provides the capability to store local disk copies for quick recovery-time objectives (RTO) and to store copies to Azure for economical, long-term retention.</span></span>

## <a name="sharepoint-supported-versions-and-related-protection-scenarios"></a><span data-ttu-id="88c8b-109">SharePoint 支援的版本與相關保護案例</span><span class="sxs-lookup"><span data-stu-id="88c8b-109">SharePoint supported versions and related protection scenarios</span></span>
<span data-ttu-id="88c8b-110">DPM 的 Azure 備份支援下列案例：</span><span class="sxs-lookup"><span data-stu-id="88c8b-110">Azure Backup for DPM supports the following scenarios:</span></span>

| <span data-ttu-id="88c8b-111">工作負載</span><span class="sxs-lookup"><span data-stu-id="88c8b-111">Workload</span></span> | <span data-ttu-id="88c8b-112">版本</span><span class="sxs-lookup"><span data-stu-id="88c8b-112">Version</span></span> | <span data-ttu-id="88c8b-113">SharePoint 部署</span><span class="sxs-lookup"><span data-stu-id="88c8b-113">SharePoint deployment</span></span> | <span data-ttu-id="88c8b-114">保護和復原</span><span class="sxs-lookup"><span data-stu-id="88c8b-114">Protection and recovery</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="88c8b-115">SharePoint</span><span class="sxs-lookup"><span data-stu-id="88c8b-115">SharePoint</span></span> |<span data-ttu-id="88c8b-116">SharePoint 2013、SharePoint 2010、SharePoint 2007、SharePoint 3.0</span><span class="sxs-lookup"><span data-stu-id="88c8b-116">SharePoint 2013, SharePoint 2010, SharePoint 2007, SharePoint 3.0</span></span> |<span data-ttu-id="88c8b-117">部署為實體伺服器或 Hyper-V/VMware 虛擬機器的 SharePoint </span><span class="sxs-lookup"><span data-stu-id="88c8b-117">SharePoint deployed as a physical server or Hyper-V/VMware virtual machine</span></span> <br> -------------- <br> <span data-ttu-id="88c8b-118">SQL AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="88c8b-118">SQL AlwaysOn</span></span> | <span data-ttu-id="88c8b-119">保護 SharePoint 伺服器陣列復原選項：來自磁碟復原點的復原伺服器陣列、資料庫及檔案或清單項目</span><span class="sxs-lookup"><span data-stu-id="88c8b-119">Protect SharePoint Farm recovery options: Recovery farm, database, and file or list item from disk recovery points.</span></span>  <span data-ttu-id="88c8b-120">來自 Azure 復原點的伺服器陣列和資料庫復原。</span><span class="sxs-lookup"><span data-stu-id="88c8b-120">Farm and database recovery from Azure recovery points.</span></span> |

## <a name="before-you-start"></a><span data-ttu-id="88c8b-121">開始之前</span><span class="sxs-lookup"><span data-stu-id="88c8b-121">Before you start</span></span>
<span data-ttu-id="88c8b-122">您需要先確定幾件事，再將 SharePoint 伺服器陣列備份至 Azure。</span><span class="sxs-lookup"><span data-stu-id="88c8b-122">There are a few things you need to confirm before you back up a SharePoint farm to Azure.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="88c8b-123">必要條件</span><span class="sxs-lookup"><span data-stu-id="88c8b-123">Prerequisites</span></span>
<span data-ttu-id="88c8b-124">繼續之前，請確定您已[安裝並備妥 Azure 備份伺服器](backup-azure-microsoft-azure-backup.md)來保護工作負載。</span><span class="sxs-lookup"><span data-stu-id="88c8b-124">Before you proceed, make sure that you have [installed and prepared the Azure Backup Server](backup-azure-microsoft-azure-backup.md) to protect workloads.</span></span>

### <a name="protection-agent"></a><span data-ttu-id="88c8b-125">保護代理程式</span><span class="sxs-lookup"><span data-stu-id="88c8b-125">Protection agent</span></span>
<span data-ttu-id="88c8b-126">保護代理程式必須安裝在執行 SharePoint 的伺服器、執行 SQL Server 的伺服器，以及隸屬於 SharePoint 伺服器陣列的所有其他伺服器上。</span><span class="sxs-lookup"><span data-stu-id="88c8b-126">The Protection agent must be installed on the server that's running SharePoint, the servers that are running SQL Server, and all other servers that are part of the SharePoint farm.</span></span> <span data-ttu-id="88c8b-127">如需設定保護代理程式的詳細資訊，請參閱[設定保護代理程式](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx)。</span><span class="sxs-lookup"><span data-stu-id="88c8b-127">For more information about how to set up the protection agent, see [Setup Protection Agent](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).</span></span>  <span data-ttu-id="88c8b-128">唯一的例外是您只能在單一 Web 前端 (WFE) 伺服器上安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="88c8b-128">The one exception is that you install the agent only on a single web front end (WFE) server.</span></span> <span data-ttu-id="88c8b-129">DPM 只需要將 WFE 伺服器上的代理程式做為保護的進入點。</span><span class="sxs-lookup"><span data-stu-id="88c8b-129">DPM needs the agent on one WFE server only to serve as the entry point for protection.</span></span>

### <a name="sharepoint-farm"></a><span data-ttu-id="88c8b-130">SharePoint 伺服器陣列</span><span class="sxs-lookup"><span data-stu-id="88c8b-130">SharePoint farm</span></span>
<span data-ttu-id="88c8b-131">針對伺服器陣列中每 1000 萬個項目，必須有至少 2 GB 的磁碟區空間來放置 MABS 資料夾。</span><span class="sxs-lookup"><span data-stu-id="88c8b-131">For every 10 million items in the farm, there must be at least 2 GB of space on the volume where the MABS folder is located.</span></span> <span data-ttu-id="88c8b-132">此空間對目錄產生是必要的。</span><span class="sxs-lookup"><span data-stu-id="88c8b-132">This space is required for catalog generation.</span></span> <span data-ttu-id="88c8b-133">若要讓 MABS 復原特定項目 (網站集合、網站、清單、文件庫、資料夾、個別的文件與清單項目)，目錄產生會建立一份包含在每個內容資料庫內的 URL 清單。</span><span class="sxs-lookup"><span data-stu-id="88c8b-133">For MABS to recover specific items (site collections, sites, lists, document libraries, folders, individual documents, and list items), catalog generation creates a list of the URLs that are contained within each content database.</span></span> <span data-ttu-id="88c8b-134">您可以在 [MABS 系統管理員主控台] 的 [復原] 工作區中，檢視 [可復原的項目] 窗格中的 URL 清單。</span><span class="sxs-lookup"><span data-stu-id="88c8b-134">You can view the list of URLs in the recoverable item pane in the **Recovery** task area of MABS Administrator Console.</span></span>

### <a name="sql-server"></a><span data-ttu-id="88c8b-135">SQL Server</span><span class="sxs-lookup"><span data-stu-id="88c8b-135">SQL Server</span></span>
<span data-ttu-id="88c8b-136">MABS 會以 LocalSystem 帳戶執行。</span><span class="sxs-lookup"><span data-stu-id="88c8b-136">MABS runs as a LocalSystem account.</span></span> <span data-ttu-id="88c8b-137">若要備份 SQL Server 資料庫，MABS 需要執行 SQL Server 之伺服器上該帳戶的 sysadmin 權限。</span><span class="sxs-lookup"><span data-stu-id="88c8b-137">To back up SQL Server databases, MABS needs sysadmin privileges on that account for the server that's running SQL Server.</span></span> <span data-ttu-id="88c8b-138">備份之前，將執行 SQL Server 之伺服器上的 NT AUTHORITY\SYSTEM 設定為 *sysadmin*。</span><span class="sxs-lookup"><span data-stu-id="88c8b-138">Set NT AUTHORITY\SYSTEM to *sysadmin* on the server that's running SQL Server before you back it up.</span></span>

<span data-ttu-id="88c8b-139">如果 SharePoint 伺服器陣列具有使用 SQL Server 別名設定的 SQL Server 資料庫，請在 MABS 將保護的前端 Web 伺服器上安裝 SQL Server 用戶端元件。</span><span class="sxs-lookup"><span data-stu-id="88c8b-139">If the SharePoint farm has SQL Server databases that are configured with SQL Server aliases, install the SQL Server client components on the front-end Web server that MABS will protect.</span></span>

### <a name="sharepoint-server"></a><span data-ttu-id="88c8b-140">SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="88c8b-140">SharePoint Server</span></span>
<span data-ttu-id="88c8b-141">雖然效能取決於許多因素，例如 SharePoint 伺服器陣列的大小，但一般做法是一部 MABS 可以保護一個 25 TB 的 SharePoint 伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="88c8b-141">While performance depends on many factors such as size of SharePoint farm, as general guidance one MABS can protect a 25 TB SharePoint farm.</span></span>

### <a name="whats-not-supported"></a><span data-ttu-id="88c8b-142">不支援的內容</span><span class="sxs-lookup"><span data-stu-id="88c8b-142">What's not supported</span></span>
* <span data-ttu-id="88c8b-143">保護 SharePoint 伺服器陣列的 MABS 不會保護搜尋索引或應用程式服務資料庫。</span><span class="sxs-lookup"><span data-stu-id="88c8b-143">MABS that protects a SharePoint farm does not protect search indexes or application service databases.</span></span> <span data-ttu-id="88c8b-144">您必須個別設定這些資料庫的保護。</span><span class="sxs-lookup"><span data-stu-id="88c8b-144">You will need to configure the protection of these databases separately.</span></span>
* <span data-ttu-id="88c8b-145">MABS 不提供相應放大檔案伺服器 (SOFS) 共用所裝載的 SharePoint SQL Server 資料庫備份。</span><span class="sxs-lookup"><span data-stu-id="88c8b-145">MABS does not provide backup of SharePoint SQL Server databases that are hosted on scale-out file server (SOFS) shares.</span></span>

## <a name="configure-sharepoint-protection"></a><span data-ttu-id="88c8b-146">設定 SharePoint 保護</span><span class="sxs-lookup"><span data-stu-id="88c8b-146">Configure SharePoint protection</span></span>
<span data-ttu-id="88c8b-147">您必須先使用 **ConfigureSharePoint.exe** 來設定 SharePoint VSS 寫入器服務 (WSS 寫入器服務)，才能使用 MABS 來保護 SharePoint。</span><span class="sxs-lookup"><span data-stu-id="88c8b-147">Before you can use MABS to protect SharePoint, you must configure the SharePoint VSS Writer service (WSS Writer service) by using **ConfigureSharePoint.exe**.</span></span>

<span data-ttu-id="88c8b-148">您可以在前端 Web 伺服器的 [MABS 安裝路徑]\bin 資料夾中找到 **ConfigureSharePoint.exe**。</span><span class="sxs-lookup"><span data-stu-id="88c8b-148">You can find **ConfigureSharePoint.exe** in the [MABS Installation Path]\bin folder on the front-end web server.</span></span> <span data-ttu-id="88c8b-149">這項工具可將 SharePoint 伺服器陣列的認證提供給保護代理程式。</span><span class="sxs-lookup"><span data-stu-id="88c8b-149">This tool provides the protection agent with the credentials for the SharePoint farm.</span></span> <span data-ttu-id="88c8b-150">您在單一 WFE 伺服器上執行。</span><span class="sxs-lookup"><span data-stu-id="88c8b-150">You run it on a single WFE server.</span></span> <span data-ttu-id="88c8b-151">如果您有多部 WFE 伺服器，在設定保護群組時請選取其中一部。</span><span class="sxs-lookup"><span data-stu-id="88c8b-151">If you have multiple WFE servers, select just one when you configure a protection group.</span></span>

### <a name="to-configure-the-sharepoint-vss-writer-service"></a><span data-ttu-id="88c8b-152">設定 SharePoint VSS 寫入器服務</span><span class="sxs-lookup"><span data-stu-id="88c8b-152">To configure the SharePoint VSS Writer service</span></span>
1. <span data-ttu-id="88c8b-153">在 WFE 伺服器上，在命令提示字元中移至 [MABS 安裝位置]\bin\\</span><span class="sxs-lookup"><span data-stu-id="88c8b-153">On the WFE server, at a command prompt, go to [MABS installation location]\bin\\</span></span>
2. <span data-ttu-id="88c8b-154">輸入 ConfigureSharePoint -EnableSharePointProtection</span><span class="sxs-lookup"><span data-stu-id="88c8b-154">Enter ConfigureSharePoint -EnableSharePointProtection.</span></span>
3. <span data-ttu-id="88c8b-155">輸入伺服器陣列系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="88c8b-155">Enter the farm administrator credentials.</span></span> <span data-ttu-id="88c8b-156">這個帳戶應該是 WFE 伺服器上本機 Administrator 群組的成員。</span><span class="sxs-lookup"><span data-stu-id="88c8b-156">This account should be a member of the local Administrator group on the WFE server.</span></span> <span data-ttu-id="88c8b-157">如果伺服器陣列系統管理員不是本機系統管理員，請授與 WFE 伺服器上的下列權限：</span><span class="sxs-lookup"><span data-stu-id="88c8b-157">If the farm administrator isn’t a local admin grant the following permissions on the WFE server:</span></span>
   * <span data-ttu-id="88c8b-158">授與 WSS_Admin_WPG 群組 DPM 資料夾 (%Program Files%\Microsoft Azure Backup\DPM) 的完整控制權。</span><span class="sxs-lookup"><span data-stu-id="88c8b-158">Grant the WSS_Admin_WPG group full control to the DPM folder (%Program Files%\Microsoft Azure Backup\DPM).</span></span>
   * <span data-ttu-id="88c8b-159">將 DPM 登錄機碼的讀取權授與 WSS_Admin_WPG 群組 (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager)。</span><span class="sxs-lookup"><span data-stu-id="88c8b-159">Grant the WSS_Admin_WPG group read access to the DPM Registry key (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).</span></span>

> [!NOTE]
> <span data-ttu-id="88c8b-160">每當 SharePoint 伺服器陣列系統管理員認證變更時，就必須重新執行 ConfigureSharePoint.exe。</span><span class="sxs-lookup"><span data-stu-id="88c8b-160">You’ll need to rerun ConfigureSharePoint.exe whenever there’s a change in the SharePoint farm administrator credentials.</span></span>
>
>

## <a name="back-up-a-sharepoint-farm-by-using-mabs"></a><span data-ttu-id="88c8b-161">使用 MABS 備份 SharePoint 伺服器陣列</span><span class="sxs-lookup"><span data-stu-id="88c8b-161">Back up a SharePoint farm by using MABS</span></span>
<span data-ttu-id="88c8b-162">設定 MABS 和 SharePoint 伺服器陣列 (如上所述) 之後，SharePoint 就可以受 MABS 保護。</span><span class="sxs-lookup"><span data-stu-id="88c8b-162">After you have configured MABS and the SharePoint farm as explained previously, SharePoint can be protected by MABS.</span></span>

### <a name="to-protect-a-sharepoint-farm"></a><span data-ttu-id="88c8b-163">保護 SharePoint 伺服器陣列</span><span class="sxs-lookup"><span data-stu-id="88c8b-163">To protect a SharePoint farm</span></span>
1. <span data-ttu-id="88c8b-164">從 [MABS 系統管理員主控台] 的 [保護] 索引標籤中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="88c8b-164">From the **Protection** tab of the MABS Administrator Console, click **New**.</span></span>
    <span data-ttu-id="88c8b-165">![[新增保護] 索引標籤](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)</span><span class="sxs-lookup"><span data-stu-id="88c8b-165">![New Protection Tab](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)</span></span>
2. <span data-ttu-id="88c8b-166">在 [建立新保護群組] 精靈的 [選擇保護群組類型] 頁面上，選取 [伺服器]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="88c8b-166">On the **Select Protection Group Type** page of the **Create New Protection Group** wizard, select **Servers**, and then click **Next**.</span></span>

    ![選擇保護群組類型](./media/backup-azure-backup-sharepoint/select-protection-group-type.png)
3. <span data-ttu-id="88c8b-168">在 [選擇群組成員] 畫面上，選取您想要保護的 SharePoint 伺服器的核取方塊，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="88c8b-168">On the **Select Group Members** screen, select the check box for the SharePoint server you want to protect and click **Next**.</span></span>

    ![選擇群組成員](./media/backup-azure-backup-sharepoint/select-group-members2.png)

   > [!NOTE]
   > <span data-ttu-id="88c8b-170">若已安裝保護代理程式，您就能在精靈中看到該伺服器。</span><span class="sxs-lookup"><span data-stu-id="88c8b-170">With the protection agent installed, you can see the server in the wizard.</span></span> <span data-ttu-id="88c8b-171">MABS 也會顯示其結構。</span><span class="sxs-lookup"><span data-stu-id="88c8b-171">MABS also shows its structure.</span></span> <span data-ttu-id="88c8b-172">由於已執行 ConfigureSharePoint.exe，MABS 會與 SharePoint VSS 寫入器服務及其對應的 SQL Server 資料庫通訊，並辨識 SharePoint 伺服器陣列結構、相關聯的內容資料庫和任何對應的項目。</span><span class="sxs-lookup"><span data-stu-id="88c8b-172">Because you ran ConfigureSharePoint.exe, MABS communicates with the SharePoint VSS Writer service and its corresponding SQL Server databases and recognizes the SharePoint farm structure, the associated content databases, and any corresponding items.</span></span>
   >
   >
4. <span data-ttu-id="88c8b-173">在 [選擇資料保護方式] 頁面上，輸入**保護群組**的名稱，然後選取您偏好的*保護方式*。</span><span class="sxs-lookup"><span data-stu-id="88c8b-173">On the **Select Data Protection Method** page, enter the name of the **Protection Group**, and select your preferred *protection methods*.</span></span> <span data-ttu-id="88c8b-174">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="88c8b-174">Click **Next**.</span></span>

    ![選擇資料保護方式](./media/backup-azure-backup-sharepoint/select-data-protection-method1.png)

   > [!NOTE]
   > <span data-ttu-id="88c8b-176">磁碟保護方法有助於達成短暫的復原時間目標。</span><span class="sxs-lookup"><span data-stu-id="88c8b-176">The disk protection method helps to meet short recovery-time objectives.</span></span>
   >
   >
5. <span data-ttu-id="88c8b-177">在 [指定短期目標] 頁面上，選取您偏好的**保留範圍**，然後識別您想要進行備份的時間。</span><span class="sxs-lookup"><span data-stu-id="88c8b-177">On the **Specify Short-Term Goals** page, select your preferred **Retention range** and identify when you want backups to occur.</span></span>

    ![指定短期目標](./media/backup-azure-backup-sharepoint/specify-short-term-goals2.png)

   > [!NOTE]
   > <span data-ttu-id="88c8b-179">由於復原大部分是針對少於五天的資料進行，因此我們針對此範例選取磁碟上五天保留範圍，並確保在非生產時段進行備份。</span><span class="sxs-lookup"><span data-stu-id="88c8b-179">Because recovery is most often required for data that's less than five days old, we selected a retention range of five days on disk and ensured that the backup happens during non-production hours, for this example.</span></span>
   >
   >
6. <span data-ttu-id="88c8b-180">檢閱為保護群組配置的存放集區磁碟空間，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="88c8b-180">Review the storage pool disk space allocated for the protection group, and click then **Next**.</span></span>
7. <span data-ttu-id="88c8b-181">針對每個保護群組，MABS 會配置磁碟空間來儲存和管理複本。</span><span class="sxs-lookup"><span data-stu-id="88c8b-181">For every protection group, MABS allocates disk space to store and manage replicas.</span></span> <span data-ttu-id="88c8b-182">此時，MABS 必須建立所選資料的複本。</span><span class="sxs-lookup"><span data-stu-id="88c8b-182">At this point, MABS must create a copy of the selected data.</span></span> <span data-ttu-id="88c8b-183">選取您希望建立複本的方式和時間，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="88c8b-183">Select how and when you want the replica created, and then click **Next**.</span></span>

    ![選擇複本的建立方式](./media/backup-azure-backup-sharepoint/choose-replica-creation-method.png)

   > [!NOTE]
   > <span data-ttu-id="88c8b-185">若要確保不影響網路流量，請選取生產時段之外的時間。</span><span class="sxs-lookup"><span data-stu-id="88c8b-185">To make sure that network traffic is not effected, select a time outside production hours.</span></span>
   >
   >
8. <span data-ttu-id="88c8b-186">MABS 可為複本執行一致性檢查，以確保資料完整性。</span><span class="sxs-lookup"><span data-stu-id="88c8b-186">MABS ensures data integrity by performing consistency checks on the replica.</span></span> <span data-ttu-id="88c8b-187">有兩個可用的選項。</span><span class="sxs-lookup"><span data-stu-id="88c8b-187">There are two available options.</span></span> <span data-ttu-id="88c8b-188">您可以定義執行一致性檢查的排程，DPM 也可以在複本變得不一致時自動執行一致性檢查。</span><span class="sxs-lookup"><span data-stu-id="88c8b-188">You can define a schedule to run consistency checks, or DPM can run consistency checks automatically on the replica whenever it becomes inconsistent.</span></span> <span data-ttu-id="88c8b-189">選取您慣用的選項，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="88c8b-189">Select your preferred option, and then click **Next**.</span></span>

    ![一致性檢查](./media/backup-azure-backup-sharepoint/consistency-check.png)
9. <span data-ttu-id="88c8b-191">在 [指定線上保護資料] 頁面上，選取您想要保護的 SharePoint 伺服器陣列，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="88c8b-191">On the **Specify Online Protection Data** page, select the SharePoint farm that you want to protect, and then click **Next**.</span></span>

    ![DPM SharePoint Protection1](./media/backup-azure-backup-sharepoint/select-online-protection1.png)
10. <span data-ttu-id="88c8b-193">在 [指定線上備份排程] 頁面上，選取您慣用的排程，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="88c8b-193">On the **Specify Online Backup Schedule** page, select your preferred schedule, and then click **Next**.</span></span>

    ![Online_backup_schedule](./media/backup-azure-backup-sharepoint/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="88c8b-195">MABS 可以從當時可用的最新磁碟備份點開始，為 Azure 最多提供兩個每日備份。</span><span class="sxs-lookup"><span data-stu-id="88c8b-195">MABS provides a maximum of two daily backups to Azure from the then available latest disk backup point.</span></span> <span data-ttu-id="88c8b-196">Azure 備份也可以利用 [Azure 備份網路節流](https://azure.microsoft.com/documentation/articles/backup-configure-vault/#enable-network-throttling)來控制尖峰和離峰時間用於備份的 WAN 頻寬。</span><span class="sxs-lookup"><span data-stu-id="88c8b-196">Azure Backup can also control the amount of WAN bandwidth that can be used for backups in peak and off-peak hours by using [Azure Backup Network Throttling](https://azure.microsoft.com/documentation/articles/backup-configure-vault/#enable-network-throttling).</span></span>
    >
    >
11. <span data-ttu-id="88c8b-197">依選取的備份排程，請在 [ **指定線上保留原則** ] 頁面上，選取每日、每週、每月和每年備份點的保留原則。</span><span class="sxs-lookup"><span data-stu-id="88c8b-197">Depending on the backup schedule that you selected, on the **Specify Online Retention Policy** page, select the retention policy for daily, weekly, monthly, and yearly backup points.</span></span>

    ![Online_retention_policy](./media/backup-azure-backup-sharepoint/specify-online-retention.png)

    > [!NOTE]
    > <span data-ttu-id="88c8b-199">MABS 會使用 grandfather-father-son 保留配置，可讓您為不同的備份時間點選擇不同的保留原則。</span><span class="sxs-lookup"><span data-stu-id="88c8b-199">MABS uses a grandfather-father-son retention scheme in which a different retention policy can be chosen for different backup points.</span></span>
    >
    >
12. <span data-ttu-id="88c8b-200">類似於磁碟，需要在 Azure 中建立初始參考點複本。</span><span class="sxs-lookup"><span data-stu-id="88c8b-200">Similar to disk, an initial reference point replica needs to be created in Azure.</span></span> <span data-ttu-id="88c8b-201">選取用於在 Azure 中建立初始備份複本的慣用選項，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="88c8b-201">Select your preferred option to create an initial backup copy to Azure, and then click **Next**.</span></span>

    ![Online_replica](./media/backup-azure-backup-sharepoint/online-replication.png)
13. <span data-ttu-id="88c8b-203">在 [摘要] 頁面上檢閱您選取的設定，然後按一下 [建立群組]。</span><span class="sxs-lookup"><span data-stu-id="88c8b-203">Review your selected settings on the **Summary** page, and then click **Create Group**.</span></span> <span data-ttu-id="88c8b-204">建立保護群組之後，您會看到成功訊息。</span><span class="sxs-lookup"><span data-stu-id="88c8b-204">You will see a success message after the protection group has been created.</span></span>

    ![摘要](./media/backup-azure-backup-sharepoint/summary.png)

## <a name="restore-a-sharepoint-item-from-disk-by-using-mabs"></a><span data-ttu-id="88c8b-206">使用 MABS 從磁碟還原 SharePoint 項目</span><span class="sxs-lookup"><span data-stu-id="88c8b-206">Restore a SharePoint item from disk by using MABS</span></span>
<span data-ttu-id="88c8b-207">在下列範例中， *Recovering SharePoint item* 已被意外刪除，而需要復原。</span><span class="sxs-lookup"><span data-stu-id="88c8b-207">In the following example, the *Recovering SharePoint item* has been accidentally deleted and needs to be recovered.</span></span>
<span data-ttu-id="88c8b-208">![MABS SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)</span><span class="sxs-lookup"><span data-stu-id="88c8b-208">![MABS SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)</span></span>

1. <span data-ttu-id="88c8b-209">開啟 [DPM 管理主控台] 。</span><span class="sxs-lookup"><span data-stu-id="88c8b-209">Open the **DPM Administrator Console**.</span></span> <span data-ttu-id="88c8b-210">DPM 保護的所有 SharePoint 伺服器陣列都會顯示在 [保護]  索引標籤中。</span><span class="sxs-lookup"><span data-stu-id="88c8b-210">All SharePoint farms that are protected by DPM are shown in the **Protection** tab.</span></span>

    ![MABS SharePoint Protection3](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection4.png)
2. <span data-ttu-id="88c8b-212">若要開始復原項目，請選取 [復原]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="88c8b-212">To begin to recover the item, select the **Recovery** tab.</span></span>

    ![MABS SharePoint Protection5](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection6.png)
3. <span data-ttu-id="88c8b-214">您可以使用萬用字元型搜尋，在復原點範圍內搜尋 SharePoint 中的 *Recovering SharePoint item* 。</span><span class="sxs-lookup"><span data-stu-id="88c8b-214">You can search SharePoint for *Recovering SharePoint item* by using a wildcard-based search within a recovery point range.</span></span>

    ![MABS SharePoint Protection6](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection7.png)
4. <span data-ttu-id="88c8b-216">從搜尋結果中選取適當的復原點，以滑鼠右鍵按一下項目，然後選取 [復原]。</span><span class="sxs-lookup"><span data-stu-id="88c8b-216">Select the appropriate recovery point from the search results, right-click the item, and then select **Recover**.</span></span>
5. <span data-ttu-id="88c8b-217">您也可以瀏覽不同的復原點，並選取要復原的資料庫或項目。</span><span class="sxs-lookup"><span data-stu-id="88c8b-217">You can also browse through various recovery points and select a database or item to recover.</span></span> <span data-ttu-id="88c8b-218">選取 [日期] > [復原時間]，然後選取正確的 [資料庫] > [SharePoint 伺服器陣列] > [復原點] > [項目]。</span><span class="sxs-lookup"><span data-stu-id="88c8b-218">Select **Date > Recovery time**, and then select the correct **Database > SharePoint farm > Recovery point > Item**.</span></span>

    ![MABS SharePoint Protection7](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection8.png)
6. <span data-ttu-id="88c8b-220">在該項目上按一下滑鼠右鍵，然後選取 [復原] 以開啟 [復原精靈]。</span><span class="sxs-lookup"><span data-stu-id="88c8b-220">Right-click the item, and then select **Recover** to open the **Recovery Wizard**.</span></span> <span data-ttu-id="88c8b-221">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="88c8b-221">Click **Next**.</span></span>

    ![檢閱復原選項](./media/backup-azure-backup-sharepoint/review-recovery-selection.png)
7. <span data-ttu-id="88c8b-223">選取您想要執行的復原類型，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="88c8b-223">Select the type of recovery that you want to perform, and then click **Next**.</span></span>

    ![復原類型](./media/backup-azure-backup-sharepoint/select-recovery-type.png)

   > [!NOTE]
   > <span data-ttu-id="88c8b-225">範例中選取的 [復原到原始] 會將項目復原到原始的 SharePoint 網站。</span><span class="sxs-lookup"><span data-stu-id="88c8b-225">The selection of **Recover to original** in the example recovers the item to the original SharePoint site.</span></span>
   >
   >
8. <span data-ttu-id="88c8b-226">選取您想要使用的 [復原程序]  。</span><span class="sxs-lookup"><span data-stu-id="88c8b-226">Select the **Recovery Process** that you want to use.</span></span>

   * <span data-ttu-id="88c8b-227">如果 SharePoint 伺服器陣列並未變更，並且與正在還原的復原點相同，請選取 [不使用復原伺服器陣列執行復原]  。</span><span class="sxs-lookup"><span data-stu-id="88c8b-227">Select **Recover without using a recovery farm** if the SharePoint farm has not changed and is the same as the recovery point that is being restored.</span></span>
   * <span data-ttu-id="88c8b-228">如果 SharePoint 伺服器陣列自建立復原點後已變更，請選取 [使用復原伺服器陣列執行復原]  。</span><span class="sxs-lookup"><span data-stu-id="88c8b-228">Select **Recover using a recovery farm** if the SharePoint farm has changed since the recovery point was created.</span></span>

     ![復原程序](./media/backup-azure-backup-sharepoint/recovery-process.png)
9. <span data-ttu-id="88c8b-230">提供暫時復原資料庫的預備 SQL Server 執行個體位置，並在要復原項目的 MABS 和執行 SharePoint 的伺服器上提供預備檔案共用。</span><span class="sxs-lookup"><span data-stu-id="88c8b-230">Provide a staging SQL Server instance location to recover the database temporarily, and provide a staging file share on MABS and the server that's running SharePoint to recover the item.</span></span>

    ![Staging Location1](./media/backup-azure-backup-sharepoint/staging-location1.png)

    <span data-ttu-id="88c8b-232">MABS 會將裝載 SharePoint 項目的內容資料庫連接至暫存 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="88c8b-232">MABS attaches the content database that is hosting the SharePoint item to the temporary SQL Server instance.</span></span> <span data-ttu-id="88c8b-233">它會從內容資料庫復原項目，並將它放在 MABS 上的預備檔案位置。</span><span class="sxs-lookup"><span data-stu-id="88c8b-233">From the content database, it recovers the item and puts it on the staging file location on MABS.</span></span> <span data-ttu-id="88c8b-234">位於預備位置上的復原項目，現在需要匯出至 SharePoint 伺服器陣列上的預備位置。</span><span class="sxs-lookup"><span data-stu-id="88c8b-234">The recovered item that's on the staging location now needs to be exported to the staging location on the SharePoint farm.</span></span>

    ![Staging Location2](./media/backup-azure-backup-sharepoint/staging-location2.png)
10. <span data-ttu-id="88c8b-236">選取 [指定復原選項] ，並將安全性設定套用至 SharePoint 伺服器陣列，或套用復原點的安全性設定。</span><span class="sxs-lookup"><span data-stu-id="88c8b-236">Select **Specify recovery options**, and apply security settings to the SharePoint farm or apply the security settings of the recovery point.</span></span> <span data-ttu-id="88c8b-237">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="88c8b-237">Click **Next**.</span></span>

    ![修復選項](./media/backup-azure-backup-sharepoint/recovery-options.png)

    > [!NOTE]
    > <span data-ttu-id="88c8b-239">您可以選擇調節網路頻寬使用量。</span><span class="sxs-lookup"><span data-stu-id="88c8b-239">You can choose to throttle the network bandwidth usage.</span></span> <span data-ttu-id="88c8b-240">這會對生產時段的生產伺服器產生最小的影響。</span><span class="sxs-lookup"><span data-stu-id="88c8b-240">This minimizes impact to the production server during production hours.</span></span>
    >
    >
11. <span data-ttu-id="88c8b-241">檢閱摘要資訊，然後按一下 [復原]  以開始復原檔案。</span><span class="sxs-lookup"><span data-stu-id="88c8b-241">Review the summary information, and then click **Recover** to begin recovery of the file.</span></span>

    ![復原摘要](./media/backup-azure-backup-sharepoint/recovery-summary.png)
12. <span data-ttu-id="88c8b-243">現在，在 [MABS 系統管理員主控台] 中選取 [監視] 索引標籤，以檢視復原的**狀態**。</span><span class="sxs-lookup"><span data-stu-id="88c8b-243">Now select the **Monitoring** tab in the **MABS Administrator Console** to view the **Status** of the recovery.</span></span>

    ![復原狀態](./media/backup-azure-backup-sharepoint/recovery-monitoring.png)

    > [!NOTE]
    > <span data-ttu-id="88c8b-245">現在即可還原檔案。</span><span class="sxs-lookup"><span data-stu-id="88c8b-245">The file is now restored.</span></span> <span data-ttu-id="88c8b-246">您可以重新整理 SharePoint 網站來檢查已還原的檔案。</span><span class="sxs-lookup"><span data-stu-id="88c8b-246">You can refresh the SharePoint site to check the restored file.</span></span>
    >
    >

## <a name="restore-a-sharepoint-database-from-azure-by-using-dpm"></a><span data-ttu-id="88c8b-247">使用 DPM 從 Azure 中還原 SharePoint 資料庫</span><span class="sxs-lookup"><span data-stu-id="88c8b-247">Restore a SharePoint database from Azure by using DPM</span></span>
1. <span data-ttu-id="88c8b-248">若要復原 SharePoint 內容資料庫，請瀏覽各種復原點 (如上所示)，並選取要還原的復原點。</span><span class="sxs-lookup"><span data-stu-id="88c8b-248">To recover a SharePoint content database, browse through various recovery points (as shown previously), and select the recovery point that you want to restore.</span></span>

    ![MABS SharePoint Protection8](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection9.png)
2. <span data-ttu-id="88c8b-250">按兩下 SharePoint 復原點以顯示可用的 SharePoint 目錄資訊。</span><span class="sxs-lookup"><span data-stu-id="88c8b-250">Double-click the SharePoint recovery point to show the available SharePoint catalog information.</span></span>

   > [!NOTE]
   > <span data-ttu-id="88c8b-251">由於 SharePoint 伺服器陣列在 Azure 中受到長期保留保護，因此 MABS 上沒有可用的目錄資訊 (中繼資料)。</span><span class="sxs-lookup"><span data-stu-id="88c8b-251">Because the SharePoint farm is protected for long-term retention in Azure, no catalog information (metadata) is available on MABS.</span></span> <span data-ttu-id="88c8b-252">如此一來，每當需要復原時間點 SharePoint 內容資料庫，您就需要重新編目 SharePoint 伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="88c8b-252">As a result, whenever a point-in-time SharePoint content database needs to be recovered, you need to catalog the SharePoint farm again.</span></span>
   >
   >
3. <span data-ttu-id="88c8b-253">按一下 [重新編目] 。</span><span class="sxs-lookup"><span data-stu-id="88c8b-253">Click **Re-catalog**.</span></span>

    ![MABS SharePoint Protection10](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection12.png)

    <span data-ttu-id="88c8b-255">[雲端重新編目]  狀態視窗隨即會開啟。</span><span class="sxs-lookup"><span data-stu-id="88c8b-255">The **Cloud Recatalog** status window opens.</span></span>

    ![MABS SharePoint Protection11](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection13.png)

    <span data-ttu-id="88c8b-257">完成編目後，狀態會變更為 [成功] 。</span><span class="sxs-lookup"><span data-stu-id="88c8b-257">After cataloging is finished, the status changes to *Success*.</span></span> <span data-ttu-id="88c8b-258">按一下 [關閉] 。</span><span class="sxs-lookup"><span data-stu-id="88c8b-258">Click **Close**.</span></span>

    ![MABS SharePoint Protection12](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection14.png)
4. <span data-ttu-id="88c8b-260">按一下 MABS [復原] 索引標籤中顯示的 SharePoint 物件，以取得內容資料庫結構。</span><span class="sxs-lookup"><span data-stu-id="88c8b-260">Click the SharePoint object shown in the MABS **Recovery** tab to get the content database structure.</span></span> <span data-ttu-id="88c8b-261">在項目上按一下滑鼠右鍵，然後按一下 [復原] 。</span><span class="sxs-lookup"><span data-stu-id="88c8b-261">Right-click the item, and then click **Recover**.</span></span>

    ![MABS SharePoint Protection13](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection15.png)
5. <span data-ttu-id="88c8b-263">此時，依照 [本文前述的復原步驟](#restore-a-sharepoint-item-from-disk-using-dpm) ，從磁碟復原 Sharepoint 內容資料庫。</span><span class="sxs-lookup"><span data-stu-id="88c8b-263">At this point, follow the [recovery steps earlier in this article](#restore-a-sharepoint-item-from-disk-using-dpm) to recover a SharePoint content database from disk.</span></span>

## <a name="faqs"></a><span data-ttu-id="88c8b-264">常見問題集</span><span class="sxs-lookup"><span data-stu-id="88c8b-264">FAQs</span></span>
<span data-ttu-id="88c8b-265">問：如果使用 SQL AlwaysOn (使用磁碟上保護) 設定 SharePoint，我是否能將 SharePoint 項目復原到原始位置？</span><span class="sxs-lookup"><span data-stu-id="88c8b-265">Q: Can I recover a SharePoint item to the original location if SharePoint is configured by using SQL AlwaysOn (with protection on disk)?</span></span><br>
<span data-ttu-id="88c8b-266">答：可以，項目可以復原到原始的 SharePoint 網站。</span><span class="sxs-lookup"><span data-stu-id="88c8b-266">A: Yes, the item can be recovered to the original SharePoint site.</span></span>

<span data-ttu-id="88c8b-267">問：如果使用 SQL AlwaysOn 設定 SharePoint，我是否能將 SharePoint 資料庫復原到原始位置？</span><span class="sxs-lookup"><span data-stu-id="88c8b-267">Q: Can I recover a SharePoint database to the original location if SharePoint is configured by using SQL AlwaysOn?</span></span><br>
<span data-ttu-id="88c8b-268">答：由於 SharePoint 資料庫是在 SQL AlwaysOn 中設定，所以除非移除可用性群組，否則無法修改它們。</span><span class="sxs-lookup"><span data-stu-id="88c8b-268">A: Because SharePoint databases are configured in SQL AlwaysOn, they cannot be modified unless the availability group is removed.</span></span> <span data-ttu-id="88c8b-269">因此，MABS 無法將資料庫還原到原始位置。</span><span class="sxs-lookup"><span data-stu-id="88c8b-269">As a result, MABS cannot restore a database to the original location.</span></span> <span data-ttu-id="88c8b-270">您可以將 SQL Server 資料庫復原到其他 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="88c8b-270">You can recover a SQL Server database to another SQL Server instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="88c8b-271">後續步驟</span><span class="sxs-lookup"><span data-stu-id="88c8b-271">Next steps</span></span>
* <span data-ttu-id="88c8b-272">深入了解 SharePoint 的 MABS 保護 - 請參閱[影片系列 - SharePoint 的 DPM 保護 (英文)](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)</span><span class="sxs-lookup"><span data-stu-id="88c8b-272">Learn more about MABS Protection of SharePoint - see [Video Series - DPM Protection of SharePoint](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)</span></span>
