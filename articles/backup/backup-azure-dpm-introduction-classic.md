---
title: "將 DPM 工作負載備份至 Azure 傳統入口網站 | Microsoft Docs"
description: "使用 Azure 備份服務來備份 DPM 伺服器的簡介"
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
ms.openlocfilehash: a9a516cfdfaf4b95c4f0121a66e90f6e71206e9f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="preparing-to-back-up-workloads-to-azure-with-dpm"></a><span data-ttu-id="aaef5-104">準備使用 DPM 將工作負載備份到 Azure</span><span class="sxs-lookup"><span data-stu-id="aaef5-104">Preparing to back up workloads to Azure with DPM</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="aaef5-105">Azure 備份伺服器</span><span class="sxs-lookup"><span data-stu-id="aaef5-105">Azure Backup Server</span></span>](backup-azure-microsoft-azure-backup.md)
> * [<span data-ttu-id="aaef5-106">SCDPM</span><span class="sxs-lookup"><span data-stu-id="aaef5-106">SCDPM</span></span>](backup-azure-dpm-introduction.md)
> * [<span data-ttu-id="aaef5-107">Azure 備份伺服器 (傳統)</span><span class="sxs-lookup"><span data-stu-id="aaef5-107">Azure Backup Server (Classic)</span></span>](backup-azure-microsoft-azure-backup-classic.md)
> * [<span data-ttu-id="aaef5-108">SCDPM (傳統)</span><span class="sxs-lookup"><span data-stu-id="aaef5-108">SCDPM (Classic)</span></span>](backup-azure-dpm-introduction-classic.md)
>
>

<span data-ttu-id="aaef5-109">本文簡介如何使用 Microsoft Azure 備份來保護 System Center Data Protection Manager (DPM) 伺服器和工作負載。</span><span class="sxs-lookup"><span data-stu-id="aaef5-109">This article provides an introduction to using Microsoft Azure Backup to protect your System Center Data Protection Manager (DPM) servers and workloads.</span></span> <span data-ttu-id="aaef5-110">在閱讀本文後，您將了解：</span><span class="sxs-lookup"><span data-stu-id="aaef5-110">By reading it, you’ll understand:</span></span>

* <span data-ttu-id="aaef5-111">Azure DPM 伺服器備份的運作方式</span><span class="sxs-lookup"><span data-stu-id="aaef5-111">How Azure DPM server backup works</span></span>
* <span data-ttu-id="aaef5-112">使備份流暢的必要條件</span><span class="sxs-lookup"><span data-stu-id="aaef5-112">The prerequisites to achieve a smooth backup experience</span></span>
* <span data-ttu-id="aaef5-113">遇到的一般錯誤以及如何排除</span><span class="sxs-lookup"><span data-stu-id="aaef5-113">The typical errors encountered and how to deal with them</span></span>
* <span data-ttu-id="aaef5-114">支援的案例</span><span class="sxs-lookup"><span data-stu-id="aaef5-114">Supported scenarios</span></span>

<span data-ttu-id="aaef5-115">System Center DPM 會備份檔案和應用程式資料。</span><span class="sxs-lookup"><span data-stu-id="aaef5-115">System Center DPM backs up file and application data.</span></span> <span data-ttu-id="aaef5-116">備份到 DPM 的資料可以儲存在磁帶、磁碟上，或使用 Microsoft Azure 備份來備份到 Azure。</span><span class="sxs-lookup"><span data-stu-id="aaef5-116">Data backed up to DPM can be stored on tape, on disk, or backed up to Azure with Microsoft Azure Backup.</span></span> <span data-ttu-id="aaef5-117">DPM 與 Azure 備份的互動方式如下：</span><span class="sxs-lookup"><span data-stu-id="aaef5-117">DPM interacts with Azure Backup as follows:</span></span>

* <span data-ttu-id="aaef5-118">**DPM 部署為實體伺服器或內部部署虛擬機器** — 如果 DPM 部署為實體伺服器或內部部署 HYPER-V 虛擬機器，除了備份到磁碟和磁帶上，您還可以將資料備份到 Azure 備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="aaef5-118">**DPM deployed as a physical server or on-premises virtual machine** — If DPM is deployed as a physical server or as an on-premises Hyper-V virtual machine you can back up data to an Azure Backup vault in addition to disk and tape backup.</span></span>
* <span data-ttu-id="aaef5-119">**DPM 部署為 Azure 虛擬機器** — 從 System Center 2012 R2 Update 3 開始，DPM 可以部署為 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="aaef5-119">**DPM deployed as an Azure virtual machine** — From System Center 2012 R2 with Update 3, DPM can be deployed as an Azure virtual machine.</span></span> <span data-ttu-id="aaef5-120">如果 DPM 部署為 Azure 虛擬機器，您可以將資料備份到連接至 DPM Azure 虛擬機器的 Azure 磁碟，或者您也可以將資料備份到 Azure 備份保存庫以卸載資料儲存體。</span><span class="sxs-lookup"><span data-stu-id="aaef5-120">If DPM is deployed as an Azure virtual machine you can back up data to Azure disks attached to the DPM Azure virtual machine, or you can offload the data storage by backing it up to an Azure Backup vault.</span></span>

## <a name="why-backup-your-dpm-servers"></a><span data-ttu-id="aaef5-121">為何要備份 DPM 伺服器？</span><span class="sxs-lookup"><span data-stu-id="aaef5-121">Why backup your DPM servers?</span></span>
<span data-ttu-id="aaef5-122">使用 Azure 備份來備份 DPM 伺服器的商業利益包括：</span><span class="sxs-lookup"><span data-stu-id="aaef5-122">The business benefits of using Azure Backup for backing up DPM servers include:</span></span>

* <span data-ttu-id="aaef5-123">在內部部署 DPM 部署中，您可以使用 Azure 備份來替代長期的磁帶部署。</span><span class="sxs-lookup"><span data-stu-id="aaef5-123">For on-premises DPM deployment, you can use Azure backup as an alternative to long-term deployment to tape.</span></span>
* <span data-ttu-id="aaef5-124">在 Azure 的 DPM 部署中，Azure 備份可讓您卸載 Azure 磁碟中的儲存體，進而透過將較舊的資料儲存在 Azure 備份上而將較新的資料儲存在磁碟上來進行擴充。</span><span class="sxs-lookup"><span data-stu-id="aaef5-124">For DPM deployments in Azure, Azure Backup allows you to offload storage from the Azure disk, allowing you to scale up by storing older data in Azure Backup and new data on disk.</span></span>

## <a name="how-does-dpm-server-backup-work"></a><span data-ttu-id="aaef5-125">DPM 伺服器備份的運作方式</span><span class="sxs-lookup"><span data-stu-id="aaef5-125">How does DPM server backup work?</span></span>
<span data-ttu-id="aaef5-126">若要備份虛擬機器，首先需要資料的時間點快照集。</span><span class="sxs-lookup"><span data-stu-id="aaef5-126">To back up a virtual machine, first a point-in-time snapshot of the data is needed.</span></span> <span data-ttu-id="aaef5-127">Azure 備份服務在排定的時間初始備份作業，並觸發備份延伸模組以建立快照集。</span><span class="sxs-lookup"><span data-stu-id="aaef5-127">The Azure Backup service initiates the backup job at the scheduled time, and triggers the backup extension to take a snapshot.</span></span> <span data-ttu-id="aaef5-128">備份延伸模組與客體的 VSS 服務進行協調以達到一致性，達到一致性後將叫用 Azure 儲存體服務的 blob 快照集 API。</span><span class="sxs-lookup"><span data-stu-id="aaef5-128">The backup extension coordinates with the in-guest VSS service to achieve consistency, and invokes the blob snapshot API of the Azure Storage service once consistency has been reached.</span></span> <span data-ttu-id="aaef5-129">這可以讓虛擬機器不需關機即可獲取一致性的磁碟快照集。</span><span class="sxs-lookup"><span data-stu-id="aaef5-129">This is done to get a consistent snapshot of the disks of the virtual machine, without having to shut it down.</span></span>

<span data-ttu-id="aaef5-130">在擷取快照集之後，Azure 備份服務會將資料傳送到備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="aaef5-130">After the snapshot has been taken, the data is transferred by the Azure Backup service to the backup vault.</span></span> <span data-ttu-id="aaef5-131">服務會負責識別上次備份後有所變更的區塊並只傳送這些區塊，讓備份儲存體和網路更有效率。</span><span class="sxs-lookup"><span data-stu-id="aaef5-131">The service takes care of identifying and transferring only the blocks that have changed from the last backup making the backups storage and network efficient.</span></span> <span data-ttu-id="aaef5-132">資料傳送完畢時將移除快照集，並建立復原點。</span><span class="sxs-lookup"><span data-stu-id="aaef5-132">When the data transfer is completed, the snapshot is removed and a recovery point is created.</span></span> <span data-ttu-id="aaef5-133">Azure 傳統入口網站中可以查看此復原點。</span><span class="sxs-lookup"><span data-stu-id="aaef5-133">This recovery point can be seen in the  Azure classic portal.</span></span>

> [!NOTE]
> <span data-ttu-id="aaef5-134">Linux 虛擬機器只能進行檔案一致性的備份。</span><span class="sxs-lookup"><span data-stu-id="aaef5-134">For Linux virtual machines, only file-consistent backup is possible.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="aaef5-135">必要條件</span><span class="sxs-lookup"><span data-stu-id="aaef5-135">Prerequisites</span></span>
<span data-ttu-id="aaef5-136">如下所示讓 Azure 備份做好備份 DPM 資料的準備：</span><span class="sxs-lookup"><span data-stu-id="aaef5-136">Prepare Azure Backup to back up DPM data as follows:</span></span>

1. <span data-ttu-id="aaef5-137">**建立備份保存庫**。</span><span class="sxs-lookup"><span data-stu-id="aaef5-137">**Create a Backup vault**.</span></span> <span data-ttu-id="aaef5-138">如果您尚未在訂用帳戶中建立備份保存庫，請參閱[準備使用 DPM 將工作負載備份至 Azure](backup-azure-dpm-introduction.md) 這篇文章的 Azure 入口網站版本。</span><span class="sxs-lookup"><span data-stu-id="aaef5-138">If you haven't created a Backup vault in your subscription, see the Azure portal version of this article - [Prepare to back up workloads to Azure with DPM](backup-azure-dpm-introduction.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="aaef5-139">從 2017 年 3 月開始，您無法再使用傳統入口網站來建立備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="aaef5-139">Starting March 2017, you can no longer use the classic portal to create Backup vaults.</span></span>
  > <span data-ttu-id="aaef5-140">您現在可以將備份保存庫升級至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="aaef5-140">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="aaef5-141">如需詳細資訊，請參閱[將備份保存庫升級至復原服務保存庫](backup-azure-upgrade-backup-to-recovery-services.md)文章。</span><span class="sxs-lookup"><span data-stu-id="aaef5-141">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="aaef5-142">Microsoft 鼓勵您將備份保存庫升級至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="aaef5-142">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="aaef5-143">在 2017 年 10 月 15 日之後，您就不能使用 PowerShell 建立備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="aaef5-143">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="aaef5-144">**在 2017 年 11 月 1 日以前**：</span><span class="sxs-lookup"><span data-stu-id="aaef5-144">**By November 1, 2017**:</span></span>
  >- <span data-ttu-id="aaef5-145">所有其餘的備份保存庫都會自動升級至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="aaef5-145">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
  >- <span data-ttu-id="aaef5-146">您將無法在傳統入口網站中存取您的備份資料。</span><span class="sxs-lookup"><span data-stu-id="aaef5-146">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="aaef5-147">相反地，使用 Azure 入口網站來存取您在復原服務保存庫中的備份資料。</span><span class="sxs-lookup"><span data-stu-id="aaef5-147">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
  >

2. <span data-ttu-id="aaef5-148">**下載保存庫認證** — 在 Azure 備份中，將您建立的管理憑證上傳到保存庫。</span><span class="sxs-lookup"><span data-stu-id="aaef5-148">**Download vault credentials** — In Azure Backup, upload the management certificate you created to the vault.</span></span>
3. <span data-ttu-id="aaef5-149">**安裝 Azure 備份代理程式並註冊伺服器** — 從 Azure 備份，在每一部 DPM 伺服器上安裝代理程式，並在備份保存庫中註冊 DPM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="aaef5-149">**Install the Azure Backup Agent and register the server** — From Azure Backup, install the agent on each DPM server and register the DPM server in the backup vault.</span></span>

[!INCLUDE [backup-download-credentials](../../includes/backup-download-credentials.md)]

[!INCLUDE [backup-install-agent](../../includes/backup-install-agent.md)]

## <a name="requirements-and-limitations"></a><span data-ttu-id="aaef5-150">需求 (和限制)</span><span class="sxs-lookup"><span data-stu-id="aaef5-150">Requirements (and limitations)</span></span>
* <span data-ttu-id="aaef5-151">DPM 可以做為實體伺服器或 System Center 2012 SP1 或 System Center 2012 R2 上安裝的 HYPER-V 虛擬機器來執行。</span><span class="sxs-lookup"><span data-stu-id="aaef5-151">DPM can be running as a physical server or a Hyper-V virtual machine installed on System Center 2012 SP1 or System Center 2012 R2.</span></span> <span data-ttu-id="aaef5-152">它也可以做為 System Center 2012 R2 (至少含 DPM 2012 R2 更新彙總套件 3) 上執行的 Azure 虛擬機器，或 System Center 2012 R2 (至少含更新彙總套件 5) 上執行之 VMWare 中的 Windows 虛擬機器來執行。</span><span class="sxs-lookup"><span data-stu-id="aaef5-152">It can also be running as an Azure virtual machine running on System Center 2012 R2 with at least DPM 2012 R2 Update Rollup 3 or a Windows virtual machine in VMWare running on System Center 2012 R2 with at least Update Rollup 5.</span></span>
* <span data-ttu-id="aaef5-153">如果您使用 System Center 2012 SP1 來執行 DPM，則應該安裝 System Center Data Protection Manager SP1 的更新彙總套件 2。</span><span class="sxs-lookup"><span data-stu-id="aaef5-153">If you’re running DPM with System Center 2012 SP1, you should install Update Rollup 2 for System Center Data Protection Manager SP1.</span></span> <span data-ttu-id="aaef5-154">要有此軟體才能安裝 Azure 備份代理程式。</span><span class="sxs-lookup"><span data-stu-id="aaef5-154">This is required before you can install the Azure Backup Agent.</span></span>
* <span data-ttu-id="aaef5-155">DPM 伺服器應該已安裝 Windows PowerShell 和 .Net Framework 4.5。</span><span class="sxs-lookup"><span data-stu-id="aaef5-155">The DPM server should have Windows PowerShell and .Net Framework 4.5 installed.</span></span>
* <span data-ttu-id="aaef5-156">DPM 可以將大部分的工作負載備份至 Azure 備份。</span><span class="sxs-lookup"><span data-stu-id="aaef5-156">DPM can back up most workloads to Azure Backup.</span></span> <span data-ttu-id="aaef5-157">如需所支援項目的完整清單，請參閱下面的 Azure 備份支援項目。</span><span class="sxs-lookup"><span data-stu-id="aaef5-157">For a full list of what’s supported see the Azure Backup support items below.</span></span>
* <span data-ttu-id="aaef5-158">使用 [複製到磁帶] 選項無法復原 Azure 備份中儲存的資料。</span><span class="sxs-lookup"><span data-stu-id="aaef5-158">Data stored in Azure Backup can’t be recovered with the “copy to tape” option.</span></span>
* <span data-ttu-id="aaef5-159">您需要已啟用 Azure 備份功能的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="aaef5-159">You’ll need an Azure account with the Azure Backup feature enabled.</span></span> <span data-ttu-id="aaef5-160">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="aaef5-160">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="aaef5-161">請閱讀 [Azure 備份定價](https://azure.microsoft.com/pricing/details/backup/)。</span><span class="sxs-lookup"><span data-stu-id="aaef5-161">Read about [Azure Backup pricing](https://azure.microsoft.com/pricing/details/backup/).</span></span>
* <span data-ttu-id="aaef5-162">要使用 Azure 備份，就必須在您想要備份的伺服器上安裝 Azure 備份代理程式。</span><span class="sxs-lookup"><span data-stu-id="aaef5-162">Using Azure Backup requires the Azure Backup Agent to be installed on the servers you want to back up.</span></span> <span data-ttu-id="aaef5-163">每個伺服器必須至少具有所要備份之資料大小的 10 % 做為本機可用儲存空間。</span><span class="sxs-lookup"><span data-stu-id="aaef5-163">Each server must have at least 10% of the size of the data that is being backed up, available as local free storage.</span></span> <span data-ttu-id="aaef5-164">例如，備份 100GB 的資料時，在臨時位置中至少需要 10 GB 的可用空間。</span><span class="sxs-lookup"><span data-stu-id="aaef5-164">For example, backing up 100 GB of data requires a minimum of 10 GB of free space in the scratch location.</span></span> <span data-ttu-id="aaef5-165">雖然最小值是 10%，但是建議使用 15% 的可用本機儲存空間來做為快取位置。</span><span class="sxs-lookup"><span data-stu-id="aaef5-165">While the minimum is 10%, 15% of free local storage space to be used for the cache location is recommended.</span></span>
* <span data-ttu-id="aaef5-166">資料會儲存在 Azure 保存庫儲存體中。</span><span class="sxs-lookup"><span data-stu-id="aaef5-166">Data will be stored in the Azure vault storage.</span></span> <span data-ttu-id="aaef5-167">可以備份至 Azure 備份保存庫的資料數量沒有限制，但是資料來源 (例如虛擬機器或資料庫) 的大小不應超過 54400 GB。</span><span class="sxs-lookup"><span data-stu-id="aaef5-167">There’s no limit to the amount of data you can back up to an Azure Backup vault but the size of a data source (for example a virtual machine or database) shouldn’t exceed 54,400 GB.</span></span>

<span data-ttu-id="aaef5-168">下列檔案類型可支援備份至 Azure：</span><span class="sxs-lookup"><span data-stu-id="aaef5-168">These file types are supported for back up to Azure:</span></span>

* <span data-ttu-id="aaef5-169">加密 (僅限完整備份)</span><span class="sxs-lookup"><span data-stu-id="aaef5-169">Encrypted (Full backups only)</span></span>
* <span data-ttu-id="aaef5-170">壓縮 (支援增量備份)</span><span class="sxs-lookup"><span data-stu-id="aaef5-170">Compressed (Incremental backups supported)</span></span>
* <span data-ttu-id="aaef5-171">疏鬆 (支援增量備份)</span><span class="sxs-lookup"><span data-stu-id="aaef5-171">Sparse (Incremental backups supported)</span></span>
* <span data-ttu-id="aaef5-172">壓縮和疏鬆 (視為疏鬆來處理)</span><span class="sxs-lookup"><span data-stu-id="aaef5-172">Compressed and sparse (Treated as Sparse)</span></span>

<span data-ttu-id="aaef5-173">下列為不支援的類型：</span><span class="sxs-lookup"><span data-stu-id="aaef5-173">And these are unsupported:</span></span>

* <span data-ttu-id="aaef5-174">不支援區分大小寫的檔案系統上的伺服器。</span><span class="sxs-lookup"><span data-stu-id="aaef5-174">Servers on case-sensitive file systems aren’t supported.</span></span>
* <span data-ttu-id="aaef5-175">硬式連結 (略過)</span><span class="sxs-lookup"><span data-stu-id="aaef5-175">Hard links (Skipped)</span></span>
* <span data-ttu-id="aaef5-176">重新分析點 (略過)</span><span class="sxs-lookup"><span data-stu-id="aaef5-176">Reparse points (Skipped)</span></span>
* <span data-ttu-id="aaef5-177">加密和壓縮 (略過)</span><span class="sxs-lookup"><span data-stu-id="aaef5-177">Encrypted and compressed (Skipped)</span></span>
* <span data-ttu-id="aaef5-178">加密和疏鬆 (略過)</span><span class="sxs-lookup"><span data-stu-id="aaef5-178">Encrypted and sparse (Skipped)</span></span>
* <span data-ttu-id="aaef5-179">壓縮資料流</span><span class="sxs-lookup"><span data-stu-id="aaef5-179">Compressed stream</span></span>
* <span data-ttu-id="aaef5-180">疏鬆資料流</span><span class="sxs-lookup"><span data-stu-id="aaef5-180">Sparse stream</span></span>

> [!NOTE]
> <span data-ttu-id="aaef5-181">從 System Center 2012 DPM SP1 開始，您可以使用 Microsoft Azure 備份將受到 DPM 保護的工作負載備份至 Azure。</span><span class="sxs-lookup"><span data-stu-id="aaef5-181">From in System Center 2012 DPM with SP1 onwards, you can backup up workloads protected by DPM to Azure using Microsoft Azure Backup.</span></span>
>
>
