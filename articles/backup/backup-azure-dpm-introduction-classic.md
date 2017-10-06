---
title: "DPM 工作負載 tooAzure 傳統入口網站註冊 aaaBack |Microsoft 文件"
description: "DPM 伺服器使用 hello Azure 備份服務簡介 toobacking"
services: backup
documentationcenter: 
author: Nkolli1
manager: shreeshd
editor: 
keywords: "System Center Data Protection Manager, Data Protection Manager, DPM 備份"
ms.assetid: 8f23972b-d167-4231-b331-e198db3b18b4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: nkolli;giridham;markgal
ms.openlocfilehash: f408957db69d45f745d5e89bd97030a341405b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-tooazure-with-dpm"></a><span data-ttu-id="8c1c1-104">準備註冊與 DPM 工作負載 tooAzure tooback</span><span class="sxs-lookup"><span data-stu-id="8c1c1-104">Preparing tooback up workloads tooAzure with DPM</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8c1c1-105">Azure 備份伺服器</span><span class="sxs-lookup"><span data-stu-id="8c1c1-105">Azure Backup Server</span></span>](backup-azure-microsoft-azure-backup.md)
> * [<span data-ttu-id="8c1c1-106">SCDPM</span><span class="sxs-lookup"><span data-stu-id="8c1c1-106">SCDPM</span></span>](backup-azure-dpm-introduction.md)
> * [<span data-ttu-id="8c1c1-107">Azure 備份伺服器 (傳統)</span><span class="sxs-lookup"><span data-stu-id="8c1c1-107">Azure Backup Server (Classic)</span></span>](backup-azure-microsoft-azure-backup-classic.md)
> * [<span data-ttu-id="8c1c1-108">SCDPM (傳統)</span><span class="sxs-lookup"><span data-stu-id="8c1c1-108">SCDPM (Classic)</span></span>](backup-azure-dpm-introduction-classic.md)
>
>

<span data-ttu-id="8c1c1-109">本文章提供簡介 toousing Microsoft Azure 備份 tooprotect System Center Data Protection Manager (DPM) 伺服器和工作負載。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-109">This article provides an introduction toousing Microsoft Azure Backup tooprotect your System Center Data Protection Manager (DPM) servers and workloads.</span></span> <span data-ttu-id="8c1c1-110">在閱讀本文後，您將了解：</span><span class="sxs-lookup"><span data-stu-id="8c1c1-110">By reading it, you’ll understand:</span></span>

* <span data-ttu-id="8c1c1-111">Azure DPM 伺服器備份的運作方式</span><span class="sxs-lookup"><span data-stu-id="8c1c1-111">How Azure DPM server backup works</span></span>
* <span data-ttu-id="8c1c1-112">hello 必要條件 tooachieve smooth 備份體驗</span><span class="sxs-lookup"><span data-stu-id="8c1c1-112">hello prerequisites tooachieve a smooth backup experience</span></span>
* <span data-ttu-id="8c1c1-113">hello 發生一般錯誤以及如何與它們 toodeal</span><span class="sxs-lookup"><span data-stu-id="8c1c1-113">hello typical errors encountered and how toodeal with them</span></span>
* <span data-ttu-id="8c1c1-114">支援的案例</span><span class="sxs-lookup"><span data-stu-id="8c1c1-114">Supported scenarios</span></span>

<span data-ttu-id="8c1c1-115">System Center DPM 會備份檔案和應用程式資料。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-115">System Center DPM backs up file and application data.</span></span> <span data-ttu-id="8c1c1-116">可以儲存在磁帶上，在磁碟上，或備份至 Microsoft Azure 備份 tooAzure tooDPM 所備份的資料。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-116">Data backed up tooDPM can be stored on tape, on disk, or backed up tooAzure with Microsoft Azure Backup.</span></span> <span data-ttu-id="8c1c1-117">DPM 與 Azure 備份的互動方式如下：</span><span class="sxs-lookup"><span data-stu-id="8c1c1-117">DPM interacts with Azure Backup as follows:</span></span>

* <span data-ttu-id="8c1c1-118">**DPM 部署為實體伺服器或內部部署虛擬機器**— 如果 DPM 部署為實體伺服器或內部部署 HYPER-V 虛擬機器，您可以將組成資料 tooan Azure 備份保存庫此外 toodisk 並磁帶備份。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-118">**DPM deployed as a physical server or on-premises virtual machine** — If DPM is deployed as a physical server or as an on-premises Hyper-V virtual machine you can back up data tooan Azure Backup vault in addition toodisk and tape backup.</span></span>
* <span data-ttu-id="8c1c1-119">**DPM 部署為 Azure 虛擬機器** — 從 System Center 2012 R2 Update 3 開始，DPM 可以部署為 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-119">**DPM deployed as an Azure virtual machine** — From System Center 2012 R2 with Update 3, DPM can be deployed as an Azure virtual machine.</span></span> <span data-ttu-id="8c1c1-120">如果 DPM 部署為 Azure 虛擬機器您可以備份資料 tooAzure 磁碟附加 toohello DPM Azure 虛擬機器，或您可以將 hello 資料儲存區卸載備份 tooan Azure 備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-120">If DPM is deployed as an Azure virtual machine you can back up data tooAzure disks attached toohello DPM Azure virtual machine, or you can offload hello data storage by backing it up tooan Azure Backup vault.</span></span>

## <a name="why-backup-your-dpm-servers"></a><span data-ttu-id="8c1c1-121">為何要備份 DPM 伺服器？</span><span class="sxs-lookup"><span data-stu-id="8c1c1-121">Why backup your DPM servers?</span></span>
<span data-ttu-id="8c1c1-122">使用 Azure 備份來備份 DPM 伺服器 hello 商業優勢包括：</span><span class="sxs-lookup"><span data-stu-id="8c1c1-122">hello business benefits of using Azure Backup for backing up DPM servers include:</span></span>

* <span data-ttu-id="8c1c1-123">在內部部署 DPM 部署，您可以使用 Azure 備份做為替代 toolong 詞彙部署 tootape。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-123">For on-premises DPM deployment, you can use Azure backup as an alternative toolong-term deployment tootape.</span></span>
* <span data-ttu-id="8c1c1-124">若是在 Azure 中的 DPM 部署，Azure Backup 可讓您 toooffload 存放裝置與 hello Azure 磁碟，您 tooscale 向上藉由將較舊的資料儲存在 Azure 備份，在磁碟上的新資料。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-124">For DPM deployments in Azure, Azure Backup allows you toooffload storage from hello Azure disk, allowing you tooscale up by storing older data in Azure Backup and new data on disk.</span></span>

## <a name="how-does-dpm-server-backup-work"></a><span data-ttu-id="8c1c1-125">DPM 伺服器備份的運作方式</span><span class="sxs-lookup"><span data-stu-id="8c1c1-125">How does DPM server backup work?</span></span>
<span data-ttu-id="8c1c1-126">新的虛擬機器，需要 hello 資料的時間點快照集的第一個 tooback。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-126">tooback up a virtual machine, first a point-in-time snapshot of hello data is needed.</span></span> <span data-ttu-id="8c1c1-127">hello Azure 備份服務會起始 hello 備份作業在 hello 排定的時間，而且觸發程序 hello 備用分機號碼 tootake 快照集。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-127">hello Azure Backup service initiates hello backup job at hello scheduled time, and triggers hello backup extension tootake a snapshot.</span></span> <span data-ttu-id="8c1c1-128">hello 備用分機號碼座標與 hello 客體 VSS 服務 tooachieve 一致性，並叫用的 hello Azure 儲存體服務的 hello blob 快照 API，一旦達到一致性。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-128">hello backup extension coordinates with hello in-guest VSS service tooachieve consistency, and invokes hello blob snapshot API of hello Azure Storage service once consistency has been reached.</span></span> <span data-ttu-id="8c1c1-129">這是完成 tooget hello 磁碟 hello 虛擬機器的一致快照集，而不需要 tooshut 向下。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-129">This is done tooget a consistent snapshot of hello disks of hello virtual machine, without having tooshut it down.</span></span>

<span data-ttu-id="8c1c1-130">已擷取 hello 快照之後，hello Azure 備份服務 toohello 備份保存庫會傳送 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-130">After hello snapshot has been taken, hello data is transferred by hello Azure Backup service toohello backup vault.</span></span> <span data-ttu-id="8c1c1-131">hello 服務會負責找出並傳送只有 hello 從 hello hello 備份儲存體和網路進行有效率的最後一個備份已變更的區塊。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-131">hello service takes care of identifying and transferring only hello blocks that have changed from hello last backup making hello backups storage and network efficient.</span></span> <span data-ttu-id="8c1c1-132">Hello 資料傳輸完成時，會移除 hello 快照集並建立復原點。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-132">When hello data transfer is completed, hello snapshot is removed and a recovery point is created.</span></span> <span data-ttu-id="8c1c1-133">Hello Azure 傳統入口網站中可以看到此復原點。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-133">This recovery point can be seen in hello  Azure classic portal.</span></span>

> [!NOTE]
> <span data-ttu-id="8c1c1-134">Linux 虛擬機器只能進行檔案一致性的備份。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-134">For Linux virtual machines, only file-consistent backup is possible.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="8c1c1-135">必要條件</span><span class="sxs-lookup"><span data-stu-id="8c1c1-135">Prerequisites</span></span>
<span data-ttu-id="8c1c1-136">準備 Azure Backup tooback DPM 資料備份，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8c1c1-136">Prepare Azure Backup tooback up DPM data as follows:</span></span>

1. <span data-ttu-id="8c1c1-137">**建立備份保存庫**。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-137">**Create a Backup vault**.</span></span> <span data-ttu-id="8c1c1-138">如果您尚未建立備份保存庫中您訂用帳戶，請參閱 hello Azure 入口網站的版本，這篇文章-[準備與 DPM 工作負載 tooAzure 向上 tooback](backup-azure-dpm-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-138">If you haven't created a Backup vault in your subscription, see hello Azure portal version of this article - [Prepare tooback up workloads tooAzure with DPM](backup-azure-dpm-introduction.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="8c1c1-139">從開始 2017 年 3 月，您無法再使用 hello 傳統入口網站 toocreate 備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-139">Starting March 2017, you can no longer use hello classic portal toocreate Backup vaults.</span></span>
  > <span data-ttu-id="8c1c1-140">您現在可以升級您備份保存庫 tooRecovery 服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-140">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="8c1c1-141">如需詳細資訊，請參閱 hello 文章[升級復原服務保存庫備份保存庫 tooa](backup-azure-upgrade-backup-to-recovery-services.md)。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-141">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="8c1c1-142">Microsoft 會鼓勵 tooupgrade 您備份保存庫 tooRecovery 服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-142">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="8c1c1-143">2017 年 10 月 15 之後，您無法使用 PowerShell toocreate 備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-143">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="8c1c1-144">**在 2017 年 11 月 1 日以前**：</span><span class="sxs-lookup"><span data-stu-id="8c1c1-144">**By November 1, 2017**:</span></span>
  >- <span data-ttu-id="8c1c1-145">所有剩餘的備份保存庫會自動升級的 tooRecovery 服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-145">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
  >- <span data-ttu-id="8c1c1-146">您將無法 tooaccess hello 傳統入口網站中無法備份資料。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-146">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="8c1c1-147">相反地，使用 Azure 入口網站 tooaccess hello 備份資料復原服務保存庫中。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-147">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
  >

2. <span data-ttu-id="8c1c1-148">**下載保存庫認證**— 在 Azure Backup 上, 傳您建立 toohello 保存庫的 hello 管理憑證。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-148">**Download vault credentials** — In Azure Backup, upload hello management certificate you created toohello vault.</span></span>
3. <span data-ttu-id="8c1c1-149">**安裝 hello Azure 備份代理程式並註冊 hello 伺服器**— 從 Azure Backup，在每一部 DPM 伺服器上安裝 hello 代理程式和 hello 備份保存庫中註冊 hello DPM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-149">**Install hello Azure Backup Agent and register hello server** — From Azure Backup, install hello agent on each DPM server and register hello DPM server in hello backup vault.</span></span>

[!INCLUDE [backup-download-credentials](../../includes/backup-download-credentials.md)]

[!INCLUDE [backup-install-agent](../../includes/backup-install-agent.md)]

## <a name="requirements-and-limitations"></a><span data-ttu-id="8c1c1-150">需求 (和限制)</span><span class="sxs-lookup"><span data-stu-id="8c1c1-150">Requirements (and limitations)</span></span>
* <span data-ttu-id="8c1c1-151">DPM 可以做為實體伺服器或 System Center 2012 SP1 或 System Center 2012 R2 上安裝的 HYPER-V 虛擬機器來執行。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-151">DPM can be running as a physical server or a Hyper-V virtual machine installed on System Center 2012 SP1 or System Center 2012 R2.</span></span> <span data-ttu-id="8c1c1-152">它也可以做為 System Center 2012 R2 (至少含 DPM 2012 R2 更新彙總套件 3) 上執行的 Azure 虛擬機器，或 System Center 2012 R2 (至少含更新彙總套件 5) 上執行之 VMWare 中的 Windows 虛擬機器來執行。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-152">It can also be running as an Azure virtual machine running on System Center 2012 R2 with at least DPM 2012 R2 Update Rollup 3 or a Windows virtual machine in VMWare running on System Center 2012 R2 with at least Update Rollup 5.</span></span>
* <span data-ttu-id="8c1c1-153">如果您使用 System Center 2012 SP1 來執行 DPM，則應該安裝 System Center Data Protection Manager SP1 的更新彙總套件 2。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-153">If you’re running DPM with System Center 2012 SP1, you should install Update Rollup 2 for System Center Data Protection Manager SP1.</span></span> <span data-ttu-id="8c1c1-154">這是必要的才能安裝 hello Azure Backup Agent。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-154">This is required before you can install hello Azure Backup Agent.</span></span>
* <span data-ttu-id="8c1c1-155">hello DPM 伺服器應該使用 Windows PowerShell 和.Net Framework 4.5 安裝。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-155">hello DPM server should have Windows PowerShell and .Net Framework 4.5 installed.</span></span>
* <span data-ttu-id="8c1c1-156">DPM 可以備份大部分的工作負載 tooAzure 備份。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-156">DPM can back up most workloads tooAzure Backup.</span></span> <span data-ttu-id="8c1c1-157">如需完整清單，支援功能的請參閱 hello Azure Backup 支援以下項目。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-157">For a full list of what’s supported see hello Azure Backup support items below.</span></span>
* <span data-ttu-id="8c1c1-158">Azure 備份中儲存的資料無法復原使用 hello 「 複製 tootape 」 選項。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-158">Data stored in Azure Backup can’t be recovered with hello “copy tootape” option.</span></span>
* <span data-ttu-id="8c1c1-159">您需要 Azure 帳戶啟用 hello Azure Backup 功能。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-159">You’ll need an Azure account with hello Azure Backup feature enabled.</span></span> <span data-ttu-id="8c1c1-160">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-160">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="8c1c1-161">請閱讀 [Azure 備份定價](https://azure.microsoft.com/pricing/details/backup/)。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-161">Read about [Azure Backup pricing](https://azure.microsoft.com/pricing/details/backup/).</span></span>
* <span data-ttu-id="8c1c1-162">使用 Azure Backup 必須安裝在您想 tooback hello 伺服器 hello Azure Backup Agent toobe。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-162">Using Azure Backup requires hello Azure Backup Agent toobe installed on hello servers you want tooback up.</span></span> <span data-ttu-id="8c1c1-163">每一部伺服器必須至少 10%的 hello 正在備份，可做為本機可用儲存體的 hello 資料大小。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-163">Each server must have at least 10% of hello size of hello data that is being backed up, available as local free storage.</span></span> <span data-ttu-id="8c1c1-164">例如，備份 100 GB 的資料所需要的最小值為 10 GB 的可用空間 hello 臨時位置。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-164">For example, backing up 100 GB of data requires a minimum of 10 GB of free space in hello scratch location.</span></span> <span data-ttu-id="8c1c1-165">雖然 hello 最小值為 10%，建議使用 15%的可用本機儲存空間 toobe hello 快取位置使用。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-165">While hello minimum is 10%, 15% of free local storage space toobe used for hello cache location is recommended.</span></span>
* <span data-ttu-id="8c1c1-166">資料會儲存在 hello Azure 保存庫儲存體中。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-166">Data will be stored in hello Azure vault storage.</span></span> <span data-ttu-id="8c1c1-167">您可以備份 tooan Azure 備份保存庫的資料沒有限制 toohello 數量但 hello 大小的資料來源 （例如虛擬機器或資料庫） 不應該超過 54,400 GB。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-167">There’s no limit toohello amount of data you can back up tooan Azure Backup vault but hello size of a data source (for example a virtual machine or database) shouldn’t exceed 54,400 GB.</span></span>

<span data-ttu-id="8c1c1-168">這些檔案類型支援 tooAzure 備份：</span><span class="sxs-lookup"><span data-stu-id="8c1c1-168">These file types are supported for back up tooAzure:</span></span>

* <span data-ttu-id="8c1c1-169">加密 (僅限完整備份)</span><span class="sxs-lookup"><span data-stu-id="8c1c1-169">Encrypted (Full backups only)</span></span>
* <span data-ttu-id="8c1c1-170">壓縮 (支援增量備份)</span><span class="sxs-lookup"><span data-stu-id="8c1c1-170">Compressed (Incremental backups supported)</span></span>
* <span data-ttu-id="8c1c1-171">疏鬆 (支援增量備份)</span><span class="sxs-lookup"><span data-stu-id="8c1c1-171">Sparse (Incremental backups supported)</span></span>
* <span data-ttu-id="8c1c1-172">壓縮和疏鬆 (視為疏鬆來處理)</span><span class="sxs-lookup"><span data-stu-id="8c1c1-172">Compressed and sparse (Treated as Sparse)</span></span>

<span data-ttu-id="8c1c1-173">下列為不支援的類型：</span><span class="sxs-lookup"><span data-stu-id="8c1c1-173">And these are unsupported:</span></span>

* <span data-ttu-id="8c1c1-174">不支援區分大小寫的檔案系統上的伺服器。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-174">Servers on case-sensitive file systems aren’t supported.</span></span>
* <span data-ttu-id="8c1c1-175">硬式連結 (略過)</span><span class="sxs-lookup"><span data-stu-id="8c1c1-175">Hard links (Skipped)</span></span>
* <span data-ttu-id="8c1c1-176">重新分析點 (略過)</span><span class="sxs-lookup"><span data-stu-id="8c1c1-176">Reparse points (Skipped)</span></span>
* <span data-ttu-id="8c1c1-177">加密和壓縮 (略過)</span><span class="sxs-lookup"><span data-stu-id="8c1c1-177">Encrypted and compressed (Skipped)</span></span>
* <span data-ttu-id="8c1c1-178">加密和疏鬆 (略過)</span><span class="sxs-lookup"><span data-stu-id="8c1c1-178">Encrypted and sparse (Skipped)</span></span>
* <span data-ttu-id="8c1c1-179">壓縮資料流</span><span class="sxs-lookup"><span data-stu-id="8c1c1-179">Compressed stream</span></span>
* <span data-ttu-id="8c1c1-180">疏鬆資料流</span><span class="sxs-lookup"><span data-stu-id="8c1c1-180">Sparse stream</span></span>

> [!NOTE]
> <span data-ttu-id="8c1c1-181">從 System Center 2012 DPM with SP1 開始，在您可以備份使用 Microsoft Azure 備份的 DPM tooAzure 所保護的工作負載。</span><span class="sxs-lookup"><span data-stu-id="8c1c1-181">From in System Center 2012 DPM with SP1 onwards, you can backup up workloads protected by DPM tooAzure using Microsoft Azure Backup.</span></span>
>
>
