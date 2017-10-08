---
title: "aaaDPM/Azure 備份伺服器保護的 SharePoint 伺服器陣列 tooAzure |Microsoft 文件"
description: "本文提供 DPM/Azure 備份伺服器保護的 SharePoint 伺服器陣列 tooAzure 的概觀"
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
ms.openlocfilehash: 726d59320b8d9f14b38e0f041308019eebcfb77b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-sharepoint-farm-tooazure"></a><span data-ttu-id="81dbf-103">備份 SharePoint 伺服器陣列 tooAzure</span><span class="sxs-lookup"><span data-stu-id="81dbf-103">Back up a SharePoint farm tooAzure</span></span>
<span data-ttu-id="81dbf-104">備份 SharePoint 伺服器陣列 tooMicrosoft Azure 利用 System Center Data Protection Manager (DPM) 中多 hello 您備份其他資料來源的相同方式。</span><span class="sxs-lookup"><span data-stu-id="81dbf-104">You back up a SharePoint farm tooMicrosoft Azure by using System Center Data Protection Manager (DPM) in much hello same way that you back up other data sources.</span></span> <span data-ttu-id="81dbf-105">Azure 備份提供具彈性的 hello 備份排程 toocreate 每日、 每週、 每月或每年備份點，並提供您各種備份點保留原則選項。</span><span class="sxs-lookup"><span data-stu-id="81dbf-105">Azure Backup provides flexibility in hello backup schedule toocreate daily, weekly, monthly, or yearly backup points and gives you retention policy options for various backup points.</span></span> <span data-ttu-id="81dbf-106">DPM 提供快速的復原時間目標 (RTO) 的 hello 功能 toostore 本機磁碟的複本，並 toostore 複製 tooAzure 經濟、 長期保留的。</span><span class="sxs-lookup"><span data-stu-id="81dbf-106">DPM provides hello capability toostore local disk copies for quick recovery-time objectives (RTO) and toostore copies tooAzure for economical, long-term retention.</span></span>

## <a name="sharepoint-supported-versions-and-related-protection-scenarios"></a><span data-ttu-id="81dbf-107">SharePoint 支援的版本與相關保護案例</span><span class="sxs-lookup"><span data-stu-id="81dbf-107">SharePoint supported versions and related protection scenarios</span></span>
<span data-ttu-id="81dbf-108">DPM 的 azure 備份支援下列案例的 hello:</span><span class="sxs-lookup"><span data-stu-id="81dbf-108">Azure Backup for DPM supports hello following scenarios:</span></span>

| <span data-ttu-id="81dbf-109">工作負載</span><span class="sxs-lookup"><span data-stu-id="81dbf-109">Workload</span></span> | <span data-ttu-id="81dbf-110">版本</span><span class="sxs-lookup"><span data-stu-id="81dbf-110">Version</span></span> | <span data-ttu-id="81dbf-111">SharePoint 部署</span><span class="sxs-lookup"><span data-stu-id="81dbf-111">SharePoint deployment</span></span> | <span data-ttu-id="81dbf-112">DPM 部署類型</span><span class="sxs-lookup"><span data-stu-id="81dbf-112">DPM deployment type</span></span> | <span data-ttu-id="81dbf-113">DPM - System Center 2012 R2</span><span class="sxs-lookup"><span data-stu-id="81dbf-113">DPM - System Center 2012 R2</span></span> | <span data-ttu-id="81dbf-114">保護和復原</span><span class="sxs-lookup"><span data-stu-id="81dbf-114">Protection and recovery</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="81dbf-115">SharePoint</span><span class="sxs-lookup"><span data-stu-id="81dbf-115">SharePoint</span></span> |<span data-ttu-id="81dbf-116">SharePoint 2013、SharePoint 2010、SharePoint 2007、SharePoint 3.0</span><span class="sxs-lookup"><span data-stu-id="81dbf-116">SharePoint 2013, SharePoint 2010, SharePoint 2007, SharePoint 3.0</span></span> |<span data-ttu-id="81dbf-117">部署為實體伺服器或 Hyper-V/VMware 虛擬機器的 SharePoint </span><span class="sxs-lookup"><span data-stu-id="81dbf-117">SharePoint deployed as a physical server or Hyper-V/VMware virtual machine</span></span> <br> -------------- <br> <span data-ttu-id="81dbf-118">SQL AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="81dbf-118">SQL AlwaysOn</span></span> |<span data-ttu-id="81dbf-119">實體伺服器或內部部署 Hyper-V 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="81dbf-119">Physical server or on-premises Hyper-V virtual machine</span></span> |<span data-ttu-id="81dbf-120">支援備份 tooAzure 從更新彙總套件 5</span><span class="sxs-lookup"><span data-stu-id="81dbf-120">Supports backup tooAzure from Update Rollup 5</span></span> |<span data-ttu-id="81dbf-121">保護 SharePoint 伺服器陣列復原選項：來自磁碟復原點的復原伺服器陣列、資料庫及檔案或清單項目</span><span class="sxs-lookup"><span data-stu-id="81dbf-121">Protect SharePoint Farm recovery options: Recovery farm, database, and file or list item from disk recovery points.</span></span>  <span data-ttu-id="81dbf-122">來自 Azure 復原點的伺服器陣列和資料庫復原。</span><span class="sxs-lookup"><span data-stu-id="81dbf-122">Farm and database recovery from Azure recovery points.</span></span> |

## <a name="before-you-start"></a><span data-ttu-id="81dbf-123">開始之前</span><span class="sxs-lookup"><span data-stu-id="81dbf-123">Before you start</span></span>
<span data-ttu-id="81dbf-124">有幾件事您備份 SharePoint 伺服器陣列 tooAzure 之前，需要 tooconfirm。</span><span class="sxs-lookup"><span data-stu-id="81dbf-124">There are a few things you need tooconfirm before you back up a SharePoint farm tooAzure.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="81dbf-125">必要條件</span><span class="sxs-lookup"><span data-stu-id="81dbf-125">Prerequisites</span></span>
<span data-ttu-id="81dbf-126">在繼續之前，請確定您已符合所有 hello[使用 Microsoft Azure 備份的必要條件](backup-azure-dpm-introduction.md#prerequisites)tooprotect 工作負載。</span><span class="sxs-lookup"><span data-stu-id="81dbf-126">Before you proceed, make sure that you have met all hello [prerequisites for using Microsoft Azure Backup](backup-azure-dpm-introduction.md#prerequisites) tooprotect workloads.</span></span> <span data-ttu-id="81dbf-127">某些必要條件的工作包括： 建立備份保存庫、 下載保存庫認證、 安裝 Azure 備份代理程式和 hello 保存庫中註冊 DPM/Azure 備份伺服器。</span><span class="sxs-lookup"><span data-stu-id="81dbf-127">Some tasks for prerequisites include: create a backup vault, download vault credentials, install Azure Backup Agent, and register DPM/Azure Backup Server with hello vault.</span></span>

### <a name="dpm-agent"></a><span data-ttu-id="81dbf-128">DPM 代理程式</span><span class="sxs-lookup"><span data-stu-id="81dbf-128">DPM agent</span></span>
<span data-ttu-id="81dbf-129">hello DPM 代理程式必須執行 SharePoint 的 hello 伺服器、 hello 執行 SQL Server 的伺服器和 hello SharePoint 伺服陣列一部分的其他所有伺服器上安裝。</span><span class="sxs-lookup"><span data-stu-id="81dbf-129">hello DPM agent must be installed on hello server that's running SharePoint, hello servers that are running SQL Server, and all other servers that are part of hello SharePoint farm.</span></span> <span data-ttu-id="81dbf-130">如需有關如何 tooset hello 保護代理程式，請參閱[安裝保護代理程式](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx)。</span><span class="sxs-lookup"><span data-stu-id="81dbf-130">For more information about how tooset up hello protection agent, see [Setup Protection Agent](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).</span></span>  <span data-ttu-id="81dbf-131">hello 一個例外狀況是您只能在單一的 web 前端 (WFE) 伺服器上安裝 hello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="81dbf-131">hello one exception is that you install hello agent only on a single web front end (WFE) server.</span></span> <span data-ttu-id="81dbf-132">為保護的 hello 進入點，DPM 需要在上一個 WFE 伺服器只有 tooserve hello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="81dbf-132">DPM needs hello agent on one WFE server only tooserve as hello entry point for protection.</span></span>

### <a name="sharepoint-farm"></a><span data-ttu-id="81dbf-133">SharePoint 伺服器陣列</span><span class="sxs-lookup"><span data-stu-id="81dbf-133">SharePoint farm</span></span>
<span data-ttu-id="81dbf-134">Hello 伺服陣列中每隔 10 百萬個項目，必須有至少 2 GB 的空間 hello 磁碟區上 hello DPM 資料夾所在的位置。</span><span class="sxs-lookup"><span data-stu-id="81dbf-134">For every 10 million items in hello farm, there must be at least 2 GB of space on hello volume where hello DPM folder is located.</span></span> <span data-ttu-id="81dbf-135">此空間對目錄產生是必要的。</span><span class="sxs-lookup"><span data-stu-id="81dbf-135">This space is required for catalog generation.</span></span> <span data-ttu-id="81dbf-136">對於 DPM toorecover 特定項目 （網站集合、 網站、 清單、 文件庫、 資料夾、 個別的文件和清單項目），類別目錄產生會建立每個內容資料庫內所包含的 hello Url 的清單。</span><span class="sxs-lookup"><span data-stu-id="81dbf-136">For DPM toorecover specific items (site collections, sites, lists, document libraries, folders, individual documents, and list items), catalog generation creates a list of hello URLs that are contained within each content database.</span></span> <span data-ttu-id="81dbf-137">您可以在 hello hello 可復原的項目] 窗格中檢視 Url hello 清單**復原**工作區的 [DPM 系統管理員主控台。</span><span class="sxs-lookup"><span data-stu-id="81dbf-137">You can view hello list of URLs in hello recoverable item pane in hello **Recovery** task area of DPM Administrator Console.</span></span>

### <a name="sql-server"></a><span data-ttu-id="81dbf-138">SQL Server</span><span class="sxs-lookup"><span data-stu-id="81dbf-138">SQL Server</span></span>
<span data-ttu-id="81dbf-139">DPM 會以 LocalSystem 帳戶身分執行。</span><span class="sxs-lookup"><span data-stu-id="81dbf-139">DPM runs as a LocalSystem account.</span></span> <span data-ttu-id="81dbf-140">tooback SQL Server 資料庫，DPM 在執行 SQL Server 的 hello 伺服器需要該帳戶上的 sysadmin 權限。</span><span class="sxs-lookup"><span data-stu-id="81dbf-140">tooback up SQL Server databases, DPM needs sysadmin privileges on that account for hello server that's running SQL Server.</span></span> <span data-ttu-id="81dbf-141">將 NT AUTHORITY\SYSTEM 太*sysadmin* hello 才能執行 SQL Server 的伺服器上加以備份。</span><span class="sxs-lookup"><span data-stu-id="81dbf-141">Set NT AUTHORITY\SYSTEM too*sysadmin* on hello server that's running SQL Server before you back it up.</span></span>

<span data-ttu-id="81dbf-142">如果 hello SharePoint 伺服器陣列已使用 SQL Server 別名設定的 SQL Server 資料庫，hello SQL Server 用戶端元件 hello 前端網頁伺服器上安裝 DPM 將保護。</span><span class="sxs-lookup"><span data-stu-id="81dbf-142">If hello SharePoint farm has SQL Server databases that are configured with SQL Server aliases, install hello SQL Server client components on hello front-end Web server that DPM will protect.</span></span>

### <a name="sharepoint-server"></a><span data-ttu-id="81dbf-143">SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="81dbf-143">SharePoint Server</span></span>
<span data-ttu-id="81dbf-144">雖然效能取決於許多因素，例如 SharePoint 伺服器陣列的大小，但一般的做法是將一部 DPM 伺服器用來保護 25 TB SharePoint 伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="81dbf-144">While performance depends on many factors such as size of SharePoint farm, as general guidance one DPM server can protect a 25 TB SharePoint farm.</span></span>

### <a name="dpm-update-rollup-5"></a><span data-ttu-id="81dbf-145">DPM 更新彙總套件 5</span><span class="sxs-lookup"><span data-stu-id="81dbf-145">DPM Update Rollup 5</span></span>
<span data-ttu-id="81dbf-146">SharePoint 伺服器陣列 tooAzure toobegin 保護，您需要 tooinstall DPM 更新彙總套件 5 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="81dbf-146">toobegin protection of a SharePoint farm tooAzure, you need tooinstall DPM Update Rollup 5 or later.</span></span> <span data-ttu-id="81dbf-147">更新彙總套件 5 提供 hello 能力 tooprotect SharePoint 伺服器陣列 tooAzure hello 伺服陣列已使用 SQL AlwaysOn。</span><span class="sxs-lookup"><span data-stu-id="81dbf-147">Update Rollup 5 provides hello ability tooprotect a SharePoint farm tooAzure if hello farm is configured by using SQL AlwaysOn.</span></span>
<span data-ttu-id="81dbf-148">如需詳細資訊，請參閱 hello 部落格文章，將會介紹[DPM 更新彙總套件 5](http://blogs.technet.com/b/dpm/archive/2015/02/11/update-rollup-5-for-system-center-2012-r2-data-protection-manager-is-now-available.aspx)</span><span class="sxs-lookup"><span data-stu-id="81dbf-148">For more information, see hello blog post that introduces [DPM Update Rollup 5](http://blogs.technet.com/b/dpm/archive/2015/02/11/update-rollup-5-for-system-center-2012-r2-data-protection-manager-is-now-available.aspx)</span></span>

### <a name="whats-not-supported"></a><span data-ttu-id="81dbf-149">不支援的內容</span><span class="sxs-lookup"><span data-stu-id="81dbf-149">What's not supported</span></span>
* <span data-ttu-id="81dbf-150">保護 SharePoint 伺服器陣列的 DPM 不會保護搜尋索引或應用程式服務資料庫。</span><span class="sxs-lookup"><span data-stu-id="81dbf-150">DPM that protects a SharePoint farm does not protect search indexes or application service databases.</span></span> <span data-ttu-id="81dbf-151">您將分別需要 tooconfigure hello 保護的資料庫。</span><span class="sxs-lookup"><span data-stu-id="81dbf-151">You will need tooconfigure hello protection of these databases separately.</span></span>
* <span data-ttu-id="81dbf-152">DPM 不提供相應放大檔案伺服器 (SOFS) 共用所裝載的 SharePoint SQL Server 資料庫備份。</span><span class="sxs-lookup"><span data-stu-id="81dbf-152">DPM does not provide backup of SharePoint SQL Server databases that are hosted on scale-out file server (SOFS) shares.</span></span>

## <a name="configure-sharepoint-protection"></a><span data-ttu-id="81dbf-153">設定 SharePoint 保護</span><span class="sxs-lookup"><span data-stu-id="81dbf-153">Configure SharePoint protection</span></span>
<span data-ttu-id="81dbf-154">您可以使用 DPM tooprotect SharePoint 之前，您必須設定 hello SharePoint VSS 寫入器服務 （WSS 寫入器服務） 使用**ConfigureSharePoint.exe**。</span><span class="sxs-lookup"><span data-stu-id="81dbf-154">Before you can use DPM tooprotect SharePoint, you must configure hello SharePoint VSS Writer service (WSS Writer service) by using **ConfigureSharePoint.exe**.</span></span>

<span data-ttu-id="81dbf-155">您可以找到**ConfigureSharePoint.exe** hello 前端 web 伺服器上的 [DPM 安裝路徑] hello \bin 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="81dbf-155">You can find **ConfigureSharePoint.exe** in hello [DPM Installation Path]\bin folder on hello front-end web server.</span></span> <span data-ttu-id="81dbf-156">這項工具提供 hello SharePoint 伺服器陣列的 hello 與 hello 認證的保護代理程式。</span><span class="sxs-lookup"><span data-stu-id="81dbf-156">This tool provides hello protection agent with hello credentials for hello SharePoint farm.</span></span> <span data-ttu-id="81dbf-157">您在單一 WFE 伺服器上執行。</span><span class="sxs-lookup"><span data-stu-id="81dbf-157">You run it on a single WFE server.</span></span> <span data-ttu-id="81dbf-158">如果您有多部 WFE 伺服器，在設定保護群組時請選取其中一部。</span><span class="sxs-lookup"><span data-stu-id="81dbf-158">If you have multiple WFE servers, select just one when you configure a protection group.</span></span>

### <a name="tooconfigure-hello-sharepoint-vss-writer-service"></a><span data-ttu-id="81dbf-159">tooconfigure hello SharePoint VSS 寫入器服務</span><span class="sxs-lookup"><span data-stu-id="81dbf-159">tooconfigure hello SharePoint VSS Writer service</span></span>
1. <span data-ttu-id="81dbf-160">Hello WFE 伺服器上，在命令提示字元中，跳過 [DPM 安裝位置] \bin\\</span><span class="sxs-lookup"><span data-stu-id="81dbf-160">On hello WFE server, at a command prompt, go too[DPM installation location]\bin\\</span></span>
2. <span data-ttu-id="81dbf-161">輸入 ConfigureSharePoint -EnableSharePointProtection</span><span class="sxs-lookup"><span data-stu-id="81dbf-161">Enter ConfigureSharePoint -EnableSharePointProtection.</span></span>
3. <span data-ttu-id="81dbf-162">輸入 hello 伺服陣列系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="81dbf-162">Enter hello farm administrator credentials.</span></span> <span data-ttu-id="81dbf-163">此帳戶應該是 hello WFE 伺服器上 hello 本機系統管理員群組的成員。</span><span class="sxs-lookup"><span data-stu-id="81dbf-163">This account should be a member of hello local Administrator group on hello WFE server.</span></span> <span data-ttu-id="81dbf-164">如果 hello 伺服陣列管理員不下列 hello WFE 伺服器上的權限的本機系統管理員授與 hello:</span><span class="sxs-lookup"><span data-stu-id="81dbf-164">If hello farm administrator isn’t a local admin grant hello following permissions on hello WFE server:</span></span>
   * <span data-ttu-id="81dbf-165">授與 hello WSS_Admin_WPG 群組完全控制 toohello DPM 資料夾 （%Program Files%\Microsoft Data Protection Manager\DPM）。</span><span class="sxs-lookup"><span data-stu-id="81dbf-165">Grant hello WSS_Admin_WPG group full control toohello DPM folder (%Program Files%\Microsoft Data Protection Manager\DPM).</span></span>
   * <span data-ttu-id="81dbf-166">授與 hello WSS_Admin_WPG 群組讀取權限 toohello DPM 登錄機碼 (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager)。</span><span class="sxs-lookup"><span data-stu-id="81dbf-166">Grant hello WSS_Admin_WPG group read access toohello DPM Registry key (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).</span></span>

> [!NOTE]
> <span data-ttu-id="81dbf-167">Hello SharePoint 伺服器陣列系統管理員認證變更時，您將需要 toorerun ConfigureSharePoint.exe。</span><span class="sxs-lookup"><span data-stu-id="81dbf-167">You’ll need toorerun ConfigureSharePoint.exe whenever there’s a change in hello SharePoint farm administrator credentials.</span></span>
> 
> 

## <a name="back-up-a-sharepoint-farm-by-using-dpm"></a><span data-ttu-id="81dbf-168">使用 DPM 備份 SharePoint 伺服器陣列</span><span class="sxs-lookup"><span data-stu-id="81dbf-168">Back up a SharePoint farm by using DPM</span></span>
<span data-ttu-id="81dbf-169">設定 DPM 和 hello 與先前所述的 SharePoint 伺服陣列之後，dpm 可保護 SharePoint。</span><span class="sxs-lookup"><span data-stu-id="81dbf-169">After you have configured DPM and hello SharePoint farm as explained previously, SharePoint can be protected by DPM.</span></span>

### <a name="tooprotect-a-sharepoint-farm"></a><span data-ttu-id="81dbf-170">tooprotect SharePoint 伺服器陣列</span><span class="sxs-lookup"><span data-stu-id="81dbf-170">tooprotect a SharePoint farm</span></span>
1. <span data-ttu-id="81dbf-171">從 hello**保護**hello DPM 系統管理員主控台 索引標籤按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="81dbf-171">From hello **Protection** tab of hello DPM Administrator Console, click **New**.</span></span>
    <span data-ttu-id="81dbf-172">![[新增保護] 索引標籤](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)</span><span class="sxs-lookup"><span data-stu-id="81dbf-172">![New Protection Tab](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)</span></span>
2. <span data-ttu-id="81dbf-173">在 hello**選取保護群組類型**hello 頁面**建立新保護群組**精靈、 選取**伺服器**，然後按一下**下一步**.</span><span class="sxs-lookup"><span data-stu-id="81dbf-173">On hello **Select Protection Group Type** page of hello **Create New Protection Group** wizard, select **Servers**, and then click **Next**.</span></span>
   
    ![選擇保護群組類型](./media/backup-azure-backup-sharepoint/select-protection-group-type.png)
3. <span data-ttu-id="81dbf-175">在 hello**選擇群組成員**螢幕、 選取 hello hello SharePoint 伺服器 tooprotect 然後按一下核取方塊**下一步**。</span><span class="sxs-lookup"><span data-stu-id="81dbf-175">On hello **Select Group Members** screen, select hello check box for hello SharePoint server you want tooprotect and click **Next**.</span></span>
   
    ![選擇群組成員](./media/backup-azure-backup-sharepoint/select-group-members2.png)
   
   > [!NOTE]
   > <span data-ttu-id="81dbf-177">Hello 已安裝的 DPM 代理程式，您可以看到 hello hello 精靈中的伺服器。</span><span class="sxs-lookup"><span data-stu-id="81dbf-177">With hello DPM agent installed, you can see hello server in hello wizard.</span></span> <span data-ttu-id="81dbf-178">DPM 也會顯示其結構。</span><span class="sxs-lookup"><span data-stu-id="81dbf-178">DPM also shows its structure.</span></span> <span data-ttu-id="81dbf-179">由於您已執行 ConfigureSharePoint.exe，DPM 會與 hello SharePoint VSS 寫入器服務和其相對應的 SQL Server 資料庫通訊，並且辨識 hello SharePoint 伺服器陣列結構，hello 相關聯的內容資料庫中和任何對應的項目。</span><span class="sxs-lookup"><span data-stu-id="81dbf-179">Because you ran ConfigureSharePoint.exe, DPM communicates with hello SharePoint VSS Writer service and its corresponding SQL Server databases and recognizes hello SharePoint farm structure, hello associated content databases, and any corresponding items.</span></span>
   > 
   > 
4. <span data-ttu-id="81dbf-180">在 hello**選擇資料保護方式**頁面上，輸入 hello hello 名稱**保護群組**，然後選取您慣用*保護方法*。</span><span class="sxs-lookup"><span data-stu-id="81dbf-180">On hello **Select Data Protection Method** page, enter hello name of hello **Protection Group**, and select your preferred *protection methods*.</span></span> <span data-ttu-id="81dbf-181">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="81dbf-181">Click **Next**.</span></span>
   
    ![選擇資料保護方式](./media/backup-azure-backup-sharepoint/select-data-protection-method1.png)
   
   > [!NOTE]
   > <span data-ttu-id="81dbf-183">hello 磁碟保護的方法可協助 toomeet 簡短的復原時間目標。</span><span class="sxs-lookup"><span data-stu-id="81dbf-183">hello disk protection method helps toomeet short recovery-time objectives.</span></span> <span data-ttu-id="81dbf-184">Azure 是經濟、 長期保護目標比較 tootapes。</span><span class="sxs-lookup"><span data-stu-id="81dbf-184">Azure is an economical, long-term protection target compared tootapes.</span></span> <span data-ttu-id="81dbf-185">如需詳細資訊，請參閱[使用 Azure Backup tooreplace 磁帶基礎結構](https://azure.microsoft.com/documentation/articles/backup-azure-backup-cloud-as-tape/)</span><span class="sxs-lookup"><span data-stu-id="81dbf-185">For more information, see [Use Azure Backup tooreplace your tape infrastructure](https://azure.microsoft.com/documentation/articles/backup-azure-backup-cloud-as-tape/)</span></span>
   > 
   > 
5. <span data-ttu-id="81dbf-186">在 hello**指定短期目標**頁面上，選取您慣用**保留範圍**並找出您想要備份 toooccur 時。</span><span class="sxs-lookup"><span data-stu-id="81dbf-186">On hello **Specify Short-Term Goals** page, select your preferred **Retention range** and identify when you want backups toooccur.</span></span>
   
    ![指定短期目標](./media/backup-azure-backup-sharepoint/specify-short-term-goals2.png)
   
   > [!NOTE]
   > <span data-ttu-id="81dbf-188">最常需要的是少於 5 天的資料復原，因為我們會選取在磁碟上的五天的保留範圍，並確保該 hello 備份發生在非生產時段，此範例中。</span><span class="sxs-lookup"><span data-stu-id="81dbf-188">Because recovery is most often required for data that's less than five days old, we selected a retention range of five days on disk and ensured that hello backup happens during non-production hours, for this example.</span></span>
   > 
   > 
6. <span data-ttu-id="81dbf-189">檢閱 hello 存放集區磁碟空間配置給 hello 保護群組，然後按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="81dbf-189">Review hello storage pool disk space allocated for hello protection group, and click then **Next**.</span></span>
7. <span data-ttu-id="81dbf-190">對於每個保護群組，DPM 會配置磁碟空間 toostore 及管理複本。</span><span class="sxs-lookup"><span data-stu-id="81dbf-190">For every protection group, DPM allocates disk space toostore and manage replicas.</span></span> <span data-ttu-id="81dbf-191">此時，DPM 必須建立 hello 選取資料的複本。</span><span class="sxs-lookup"><span data-stu-id="81dbf-191">At this point, DPM must create a copy of hello selected data.</span></span> <span data-ttu-id="81dbf-192">選取如何及何時您希望 hello 複本建立，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="81dbf-192">Select how and when you want hello replica created, and then click **Next**.</span></span>
   
    ![選擇複本的建立方式](./media/backup-azure-backup-sharepoint/choose-replica-creation-method.png)
   
   > [!NOTE]
   > <span data-ttu-id="81dbf-194">toomake 確定的網路流量不會受影響，會選取生產的時間之外的時間。</span><span class="sxs-lookup"><span data-stu-id="81dbf-194">toomake sure that network traffic is not effected, select a time outside production hours.</span></span>
   > 
   > 
8. <span data-ttu-id="81dbf-195">DPM 可透過執行 hello 複本上的一致性檢查，確保資料完整性。</span><span class="sxs-lookup"><span data-stu-id="81dbf-195">DPM ensures data integrity by performing consistency checks on hello replica.</span></span> <span data-ttu-id="81dbf-196">有兩個可用的選項。</span><span class="sxs-lookup"><span data-stu-id="81dbf-196">There are two available options.</span></span> <span data-ttu-id="81dbf-197">您可以定義排程 toorun 一致性檢查，或 DPM 變得不一致時執行一致性檢查，會自動在 hello 複本上的。</span><span class="sxs-lookup"><span data-stu-id="81dbf-197">You can define a schedule toorun consistency checks, or DPM can run consistency checks automatically on hello replica whenever it becomes inconsistent.</span></span> <span data-ttu-id="81dbf-198">選取您慣用的選項，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="81dbf-198">Select your preferred option, and then click **Next**.</span></span>
   
    ![一致性檢查](./media/backup-azure-backup-sharepoint/consistency-check.png)
9. <span data-ttu-id="81dbf-200">在 hello**指定線上保護資料**頁面上，選取您想 tooprotect，，然後按一下的 hello SharePoint 伺服器陣列**下一步**。</span><span class="sxs-lookup"><span data-stu-id="81dbf-200">On hello **Specify Online Protection Data** page, select hello SharePoint farm that you want tooprotect, and then click **Next**.</span></span>
   
    ![DPM SharePoint Protection1](./media/backup-azure-backup-sharepoint/select-online-protection1.png)
10. <span data-ttu-id="81dbf-202">在 hello**指定線上備份排程**頁面上，選取您偏好的排程，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="81dbf-202">On hello **Specify Online Backup Schedule** page, select your preferred schedule, and then click **Next**.</span></span>
    
    ![Online_backup_schedule](./media/backup-azure-backup-sharepoint/specify-online-backup-schedule.png)
    
    > [!NOTE]
    > <span data-ttu-id="81dbf-204">DPM 可提供最高的兩個每日備份 tooAzure 在不同的時間。</span><span class="sxs-lookup"><span data-stu-id="81dbf-204">DPM provides a maximum of two daily backups tooAzure at different times.</span></span> <span data-ttu-id="81dbf-205">Azure 備份也可以控制可以用於尖峰和離峰時間中的備份所使用的 WAN 頻寬的 hello 數量[Azure 備份網路節流設定](https://azure.microsoft.com/en-in/documentation/articles/backup-configure-vault/#enable-network-throttling)。</span><span class="sxs-lookup"><span data-stu-id="81dbf-205">Azure Backup can also control hello amount of WAN bandwidth that can be used for backups in peak and off-peak hours by using [Azure Backup Network Throttling](https://azure.microsoft.com/en-in/documentation/articles/backup-configure-vault/#enable-network-throttling).</span></span>
    > 
    > 
11. <span data-ttu-id="81dbf-206">根據您選取在 hello hello 備份排程**指定線上保留原則**頁面上，選取 hello 每日、 每週、 每月和每年備份點保留原則。</span><span class="sxs-lookup"><span data-stu-id="81dbf-206">Depending on hello backup schedule that you selected, on hello **Specify Online Retention Policy** page, select hello retention policy for daily, weekly, monthly, and yearly backup points.</span></span>
    
    ![Online_retention_policy](./media/backup-azure-backup-sharepoint/specify-online-retention.png)
    
    > [!NOTE]
    > <span data-ttu-id="81dbf-208">DPM 會使用 grandfather-father-son 配置，可讓您為不同的備份時間點選擇不同的保留原則。</span><span class="sxs-lookup"><span data-stu-id="81dbf-208">DPM uses a grandfather-father-son retention scheme in which a different retention policy can be chosen for different backup points.</span></span>
    > 
    > 
12. <span data-ttu-id="81dbf-209">類似的 toodisk 初始的參考點複本需要 toobe 在 Azure 中建立。</span><span class="sxs-lookup"><span data-stu-id="81dbf-209">Similar toodisk, an initial reference point replica needs toobe created in Azure.</span></span> <span data-ttu-id="81dbf-210">選取您慣用的選項 toocreate 初始備份複本 tooAzure，，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="81dbf-210">Select your preferred option toocreate an initial backup copy tooAzure, and then click **Next**.</span></span>
    
    ![Online_replica](./media/backup-azure-backup-sharepoint/online-replication.png)
13. <span data-ttu-id="81dbf-212">檢閱您選取的設定，在 hello**摘要**頁面，然後再按一下**建立群組**。</span><span class="sxs-lookup"><span data-stu-id="81dbf-212">Review your selected settings on hello **Summary** page, and then click **Create Group**.</span></span> <span data-ttu-id="81dbf-213">建立 hello 保護群組之後，您會看到成功訊息。</span><span class="sxs-lookup"><span data-stu-id="81dbf-213">You will see a success message after hello protection group has been created.</span></span>
    
    ![摘要](./media/backup-azure-backup-sharepoint/summary.png)

## <a name="restore-a-sharepoint-item-from-disk-by-using-dpm"></a><span data-ttu-id="81dbf-215">使用 DPM 從磁碟還原 SharePoint 項目</span><span class="sxs-lookup"><span data-stu-id="81dbf-215">Restore a SharePoint item from disk by using DPM</span></span>
<span data-ttu-id="81dbf-216">在下列範例的 hello，hello*復原 SharePoint 項目*被意外刪除，而且需要 toobe 復原。</span><span class="sxs-lookup"><span data-stu-id="81dbf-216">In hello following example, hello *Recovering SharePoint item* has been accidentally deleted and needs toobe recovered.</span></span>
<span data-ttu-id="81dbf-217">![DPM SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)</span><span class="sxs-lookup"><span data-stu-id="81dbf-217">![DPM SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)</span></span>

1. <span data-ttu-id="81dbf-218">開啟 hello **DPM 系統管理員主控台**。</span><span class="sxs-lookup"><span data-stu-id="81dbf-218">Open hello **DPM Administrator Console**.</span></span> <span data-ttu-id="81dbf-219">DPM 所保護的所有 SharePoint 伺服器陣列所都示 hello**保護** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="81dbf-219">All SharePoint farms that are protected by DPM are shown in hello **Protection** tab.</span></span>
   
    ![DPM SharePoint Protection3](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection4.png)
2. <span data-ttu-id="81dbf-221">toobegin toorecover hello 項目，請選取 hello**復原** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="81dbf-221">toobegin toorecover hello item, select hello **Recovery** tab.</span></span>
   
    ![DPM SharePoint Protection5](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection6.png)
3. <span data-ttu-id="81dbf-223">您可以使用萬用字元型搜尋，在復原點範圍內搜尋 SharePoint 中的 *Recovering SharePoint item* 。</span><span class="sxs-lookup"><span data-stu-id="81dbf-223">You can search SharePoint for *Recovering SharePoint item* by using a wildcard-based search within a recovery point range.</span></span>
   
    ![DPM SharePoint Protection6](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection7.png)
4. <span data-ttu-id="81dbf-225">從 hello 搜尋結果中選取 hello 適當的復原點，hello 項目，以滑鼠右鍵按一下，然後選取**復原**。</span><span class="sxs-lookup"><span data-stu-id="81dbf-225">Select hello appropriate recovery point from hello search results, right-click hello item, and then select **Recover**.</span></span>
5. <span data-ttu-id="81dbf-226">您也可以瀏覽不同的復原點，並選取資料庫或項目 toorecover。</span><span class="sxs-lookup"><span data-stu-id="81dbf-226">You can also browse through various recovery points and select a database or item toorecover.</span></span> <span data-ttu-id="81dbf-227">選取**日期 > 復原時間**，然後選取正確的 hello**資料庫 > SharePoint 伺服器陣列 > 復原點 > 項目**。</span><span class="sxs-lookup"><span data-stu-id="81dbf-227">Select **Date > Recovery time**, and then select hello correct **Database > SharePoint farm > Recovery point > Item**.</span></span>
   
    ![DPM SharePoint Protection7](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection8.png)
6. <span data-ttu-id="81dbf-229">Hello 項目，以滑鼠右鍵按一下，然後選取**復原**tooopen hello**復原精靈**。</span><span class="sxs-lookup"><span data-stu-id="81dbf-229">Right-click hello item, and then select **Recover** tooopen hello **Recovery Wizard**.</span></span> <span data-ttu-id="81dbf-230">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="81dbf-230">Click **Next**.</span></span>
   
    ![檢閱復原選項](./media/backup-azure-backup-sharepoint/review-recovery-selection.png)
7. <span data-ttu-id="81dbf-232">選取您想 tooperform，然後再按一下復原 hello 類型**下一步**。</span><span class="sxs-lookup"><span data-stu-id="81dbf-232">Select hello type of recovery that you want tooperform, and then click **Next**.</span></span>
   
    ![復原類型](./media/backup-azure-backup-sharepoint/select-recovery-type.png)
   
   > [!NOTE]
   > <span data-ttu-id="81dbf-234">hello 選取**復原 toooriginal** hello 範例會復原 hello 項目 toohello 原始 SharePoint 網站。</span><span class="sxs-lookup"><span data-stu-id="81dbf-234">hello selection of **Recover toooriginal** in hello example recovers hello item toohello original SharePoint site.</span></span>
   > 
   > 
8. <span data-ttu-id="81dbf-235">選取 hello**復原程序**想 toouse。</span><span class="sxs-lookup"><span data-stu-id="81dbf-235">Select hello **Recovery Process** that you want toouse.</span></span>
   
   * <span data-ttu-id="81dbf-236">選取**復原，而不使用復原伺服器陣列**如果 hello SharePoint 伺服陣列並未變更，而且的 hello 相同 hello 復原點，進行還原。</span><span class="sxs-lookup"><span data-stu-id="81dbf-236">Select **Recover without using a recovery farm** if hello SharePoint farm has not changed and is hello same as hello recovery point that is being restored.</span></span>
   * <span data-ttu-id="81dbf-237">選取**使用復原伺服器陣列復原**hello SharePoint 伺服器陣列在之後建立 hello 復原點已變更。</span><span class="sxs-lookup"><span data-stu-id="81dbf-237">Select **Recover using a recovery farm** if hello SharePoint farm has changed since hello recovery point was created.</span></span>
     
     ![復原程序](./media/backup-azure-backup-sharepoint/recovery-process.png)
9. <span data-ttu-id="81dbf-239">提供暫存 SQL Server 執行個體位置 toorecover hello 資料庫暫時，並提供暫存的檔案共用 hello DPM 伺服器和執行 SharePoint toorecover hello 項目中的 hello 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="81dbf-239">Provide a staging SQL Server instance location toorecover hello database temporarily, and provide a staging file share on hello DPM server and hello server that's running SharePoint toorecover hello item.</span></span>
   
    ![Staging Location1](./media/backup-azure-backup-sharepoint/staging-location1.png)
   
    <span data-ttu-id="81dbf-241">DPM 會將附加 hello 裝載 hello SharePoint 項目 toohello 暫存 SQL Server 執行個體的內容資料庫。</span><span class="sxs-lookup"><span data-stu-id="81dbf-241">DPM attaches hello content database that is hosting hello SharePoint item toohello temporary SQL Server instance.</span></span> <span data-ttu-id="81dbf-242">從內容資料庫 hello，hello DPM 伺服器復原 hello 項目，並將它放在 hello 預備 hello DPM 伺服器上的檔案位置。</span><span class="sxs-lookup"><span data-stu-id="81dbf-242">From hello content database, hello DPM server recovers hello item and puts it on hello staging file location on hello DPM server.</span></span> <span data-ttu-id="81dbf-243">hello hello 現在預備 hello DPM 伺服器的位置上的復原項目需要 toobe 匯出 toohello 預備 hello SharePoint 伺服器陣列上的位置。</span><span class="sxs-lookup"><span data-stu-id="81dbf-243">hello recovered item that's on hello staging location of hello DPM server now needs toobe exported toohello staging location on hello SharePoint farm.</span></span>
   
    ![Staging Location2](./media/backup-azure-backup-sharepoint/staging-location2.png)
10. <span data-ttu-id="81dbf-245">選取**指定復原選項**，以及套用安全性設定 toohello SharePoint 伺服器陣列，或套用 hello hello 復原點的安全性設定。</span><span class="sxs-lookup"><span data-stu-id="81dbf-245">Select **Specify recovery options**, and apply security settings toohello SharePoint farm or apply hello security settings of hello recovery point.</span></span> <span data-ttu-id="81dbf-246">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="81dbf-246">Click **Next**.</span></span>
    
    ![修復選項](./media/backup-azure-backup-sharepoint/recovery-options.png)
    
    > [!NOTE]
    > <span data-ttu-id="81dbf-248">您可以選擇 toothrottle hello 網路頻寬使用量。</span><span class="sxs-lookup"><span data-stu-id="81dbf-248">You can choose toothrottle hello network bandwidth usage.</span></span> <span data-ttu-id="81dbf-249">這可降低影響 toohello 實際執行伺服器生產小時期間。</span><span class="sxs-lookup"><span data-stu-id="81dbf-249">This minimizes impact toohello production server during production hours.</span></span>
    > 
    > 
11. <span data-ttu-id="81dbf-250">檢閱 hello 摘要資訊，然後按一下**復原**toobegin hello 檔案復原。</span><span class="sxs-lookup"><span data-stu-id="81dbf-250">Review hello summary information, and then click **Recover** toobegin recovery of hello file.</span></span>
    
    ![復原摘要](./media/backup-azure-backup-sharepoint/recovery-summary.png)
12. <span data-ttu-id="81dbf-252">現在選取 hello**監視** 索引標籤中 hello **DPM 系統管理員主控台**tooview hello**狀態**的 hello 復原。</span><span class="sxs-lookup"><span data-stu-id="81dbf-252">Now select hello **Monitoring** tab in hello **DPM Administrator Console** tooview hello **Status** of hello recovery.</span></span>
    
    ![復原狀態](./media/backup-azure-backup-sharepoint/recovery-monitoring.png)
    
    > [!NOTE]
    > <span data-ttu-id="81dbf-254">hello 檔案現已還原。</span><span class="sxs-lookup"><span data-stu-id="81dbf-254">hello file is now restored.</span></span> <span data-ttu-id="81dbf-255">您可以重新整理 hello SharePoint 站台 toocheck hello 還原檔案。</span><span class="sxs-lookup"><span data-stu-id="81dbf-255">You can refresh hello SharePoint site toocheck hello restored file.</span></span>
    > 
    > 

## <a name="restore-a-sharepoint-database-from-azure-by-using-dpm"></a><span data-ttu-id="81dbf-256">使用 DPM 從 Azure 中還原 SharePoint 資料庫</span><span class="sxs-lookup"><span data-stu-id="81dbf-256">Restore a SharePoint database from Azure by using DPM</span></span>
1. <span data-ttu-id="81dbf-257">toorecover SharePoint 內容資料庫中，瀏覽各種復原點 （如先前所示），並選取您想 toorestore hello 復原點。</span><span class="sxs-lookup"><span data-stu-id="81dbf-257">toorecover a SharePoint content database, browse through various recovery points (as shown previously), and select hello recovery point that you want toorestore.</span></span>
   
    ![DPM SharePoint Protection8](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection9.png)
2. <span data-ttu-id="81dbf-259">按兩下 hello SharePoint 復原點 tooshow hello 可用 SharePoint 類別目錄資訊。</span><span class="sxs-lookup"><span data-stu-id="81dbf-259">Double-click hello SharePoint recovery point tooshow hello available SharePoint catalog information.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="81dbf-260">Hello SharePoint 伺服器陣列受到保護供長期保存在 Azure 中，因為沒有類別目錄資訊 （中繼資料） 是可用 hello DPM 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="81dbf-260">Because hello SharePoint farm is protected for long-term retention in Azure, no catalog information (metadata) is available on hello DPM server.</span></span> <span data-ttu-id="81dbf-261">如此一來，每次的時間點的 SharePoint 內容資料庫需要 toobe 復原，您需要 toocatalog hello SharePoint 伺服陣列一次。</span><span class="sxs-lookup"><span data-stu-id="81dbf-261">As a result, whenever a point-in-time SharePoint content database needs toobe recovered, you need toocatalog hello SharePoint farm again.</span></span>
   > 
   > 
3. <span data-ttu-id="81dbf-262">按一下 [重新編目] 。</span><span class="sxs-lookup"><span data-stu-id="81dbf-262">Click **Re-catalog**.</span></span>
   
    ![DPM SharePoint Protection10](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection12.png)
   
    <span data-ttu-id="81dbf-264">hello**雲端重新編目**狀態 視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="81dbf-264">hello **Cloud Recatalog** status window opens.</span></span>
   
    ![DPM SharePoint Protection11](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection13.png)
   
    <span data-ttu-id="81dbf-266">Hello 狀態編目完成後，變更太*成功*。</span><span class="sxs-lookup"><span data-stu-id="81dbf-266">After cataloging is finished, hello status changes too*Success*.</span></span> <span data-ttu-id="81dbf-267">按一下 [關閉] 。</span><span class="sxs-lookup"><span data-stu-id="81dbf-267">Click **Close**.</span></span>
   
    ![DPM SharePoint Protection12](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection14.png)
4. <span data-ttu-id="81dbf-269">按一下 顯示 hello DPM 中的 hello SharePoint 物件**復原**tooget hello 內容資料庫結構索引標籤上。</span><span class="sxs-lookup"><span data-stu-id="81dbf-269">Click hello SharePoint object shown in hello DPM **Recovery** tab tooget hello content database structure.</span></span> <span data-ttu-id="81dbf-270">Hello 項目，以滑鼠右鍵按一下，然後按一下**復原**。</span><span class="sxs-lookup"><span data-stu-id="81dbf-270">Right-click hello item, and then click **Recover**.</span></span>
   
    ![DPM SharePoint Protection13](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection15.png)
5. <span data-ttu-id="81dbf-272">此時，請遵循 hello[本文稍早的復原步驟](#restore-a-sharepoint-item-from-disk-using-dpm)toorecover 從磁碟的 SharePoint 內容資料庫。</span><span class="sxs-lookup"><span data-stu-id="81dbf-272">At this point, follow hello [recovery steps earlier in this article](#restore-a-sharepoint-item-from-disk-using-dpm) toorecover a SharePoint content database from disk.</span></span>

## <a name="faqs"></a><span data-ttu-id="81dbf-273">常見問題集</span><span class="sxs-lookup"><span data-stu-id="81dbf-273">FAQs</span></span>
<span data-ttu-id="81dbf-274">問︰哪些版本的 DPM 支援 SQL Server 2014 和 SQL 2012 (SP2)？</span><span class="sxs-lookup"><span data-stu-id="81dbf-274">Q: Which versions of DPM support SQL Server 2014 and SQL 2012 (SP2)?</span></span><br>
<span data-ttu-id="81dbf-275">答︰DPM 2012 R2 更新彙總套件 4 支援兩者。</span><span class="sxs-lookup"><span data-stu-id="81dbf-275">A: DPM 2012 R2 with Update Rollup 4 supports both.</span></span>

<span data-ttu-id="81dbf-276">問： 是否如果使用 （與在磁碟上的保護） 的 SQL AlwaysOn 設定 SharePoint 可以復原 SharePoint 項目 toohello 原始位置？</span><span class="sxs-lookup"><span data-stu-id="81dbf-276">Q: Can I recover a SharePoint item toohello original location if SharePoint is configured by using SQL AlwaysOn (with protection on disk)?</span></span><br>
<span data-ttu-id="81dbf-277">答: [是]，hello 項目可以是復原的 toohello 原始的 SharePoint 網站。</span><span class="sxs-lookup"><span data-stu-id="81dbf-277">A: Yes, hello item can be recovered toohello original SharePoint site.</span></span>

<span data-ttu-id="81dbf-278">問： 是否如果使用 SQL AlwaysOn 設定 SharePoint 可以復原 SharePoint 資料庫 toohello 原始位置？</span><span class="sxs-lookup"><span data-stu-id="81dbf-278">Q: Can I recover a SharePoint database toohello original location if SharePoint is configured by using SQL AlwaysOn?</span></span><br>
<span data-ttu-id="81dbf-279">答： 因為 SharePoint 資料庫在 SQL AlwaysOn 設定，無法修改它們除非 hello 可用性群組。</span><span class="sxs-lookup"><span data-stu-id="81dbf-279">A: Because SharePoint databases are configured in SQL AlwaysOn, they cannot be modified unless hello availability group is removed.</span></span> <span data-ttu-id="81dbf-280">如此一來，DPM 無法還原資料庫 toohello 原始位置。</span><span class="sxs-lookup"><span data-stu-id="81dbf-280">As a result, DPM cannot restore a database toohello original location.</span></span> <span data-ttu-id="81dbf-281">您可以復原的 SQL Server 資料庫 tooanother SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="81dbf-281">You can recover a SQL Server database tooanother SQL Server instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81dbf-282">後續步驟</span><span class="sxs-lookup"><span data-stu-id="81dbf-282">Next steps</span></span>
* <span data-ttu-id="81dbf-283">深入了解 DPM 的 SharePoint 保護 - 請參閱 [影片系列 - DPM 的 SharePoint 保護](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)</span><span class="sxs-lookup"><span data-stu-id="81dbf-283">Learn more about DPM Protection of SharePoint - see [Video Series - DPM Protection of SharePoint](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)</span></span>
* <span data-ttu-id="81dbf-284">檢閱 [System Center 2012 - Data Protection Manager 版本資訊](https://technet.microsoft.com/library/jj860415.aspx)</span><span class="sxs-lookup"><span data-stu-id="81dbf-284">Review [Release Notes for System Center 2012 - Data Protection Manager](https://technet.microsoft.com/library/jj860415.aspx)</span></span>
* <span data-ttu-id="81dbf-285">檢閱 [System Center 2012 SP1 的 Data Protection Manager 版本資訊](https://technet.microsoft.com/library/jj860394.aspx)</span><span class="sxs-lookup"><span data-stu-id="81dbf-285">Review [Release Notes for Data Protection Manager in System Center 2012 SP1](https://technet.microsoft.com/library/jj860394.aspx)</span></span>

