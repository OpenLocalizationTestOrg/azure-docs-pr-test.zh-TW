---
title: "儲存體快照集為基礎的 SAP HANA 備份 | Microsoft Docs"
description: "備份 Azure 虛擬機器上的 SAP HANA 有兩種主要做法，本文涵蓋以儲存體快照集為基礎的 SAP HANA 備份"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ums.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 3/13/2017
ms.author: rclaus
ms.openlocfilehash: f332b8ac091b75a23489ac27f15ad1fd10d24ec6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="sap-hana-backup-based-on-storage-snapshots"></a><span data-ttu-id="cbb9c-103">以儲存體快照集為基礎的 SAP HANA 備份</span><span class="sxs-lookup"><span data-stu-id="cbb9c-103">SAP HANA backup based on storage snapshots</span></span>

## <a name="introduction"></a><span data-ttu-id="cbb9c-104">簡介</span><span class="sxs-lookup"><span data-stu-id="cbb9c-104">Introduction</span></span>

<span data-ttu-id="cbb9c-105">這是與 SAP HANA 備份相關的三篇系列文章的其中一篇。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-105">This is part of a three-part series of related articles on SAP HANA backup.</span></span> <span data-ttu-id="cbb9c-106">[Azure 虛擬機器上 SAP HANA 的備份指南](sap-hana-backup-guide.md)提供開始使用的概觀和資訊，[檔案層級的 SAP HANA Azure 備份](sap-hana-backup-file-level.md)涵蓋以檔案為基礎的備份選項。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-106">[Backup guide for SAP HANA on Azure Virtual Machines](sap-hana-backup-guide.md) provides an overview and information on getting started, and [SAP HANA Azure Backup on file level](sap-hana-backup-file-level.md) covers the file-based backup option.</span></span>

<span data-ttu-id="cbb9c-107">在單一執行個體全方位示範系統中使用 VM 備份功能時，應該考慮進行 VM 備份，而不是在作業系統層級管理 HANA 備份。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-107">When using a VM backup feature for a single-instance all-in-one demo system, one should consider doing a VM backup instead of managing HANA backups at the OS level.</span></span> <span data-ttu-id="cbb9c-108">另一個替代方法是採用 Azure blob 快照集，建立連結至虛擬機器之個別虛擬磁碟的複本，並保留 HANA 資料檔案。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-108">An alternative is to take Azure blob snapshots to create copies of individual virtual disks, which are attached to a virtual machine, and keep the HANA data files.</span></span> <span data-ttu-id="cbb9c-109">但關鍵點在於，當系統正在執行中，建立 VM 備份或磁碟快照集的一致性。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-109">But a critical point is app consistency when creating a VM backup or disk snapshot while the system is up and running.</span></span> <span data-ttu-id="cbb9c-110">請參閱相關文章 [Azure 虛擬機器上 SAP HANA 的備份指南](sap-hana-backup-guide.md)中的＜建立儲存體快照集時，SAP HANA 資料的一致性＞。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-110">See _SAP HANA data consistency when taking storage snapshots_ in the related article [Backup guide for SAP HANA on Azure Virtual Machines](sap-hana-backup-guide.md).</span></span> <span data-ttu-id="cbb9c-111">SAP HANA 有個功能支援這類的儲存體快照集。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-111">SAP HANA has a feature that supports these kinds of storage snapshots.</span></span>

## <a name="sap-hana-snapshots"></a><span data-ttu-id="cbb9c-112">SAP HANA 快照集</span><span class="sxs-lookup"><span data-stu-id="cbb9c-112">SAP HANA snapshots</span></span>

<span data-ttu-id="cbb9c-113">SAP HANA 中有個功能支援建立儲存體快照集。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-113">There is a feature in SAP HANA that supports taking a storage snapshot.</span></span> <span data-ttu-id="cbb9c-114">不過，自 2016 年 12 月 起，有單一容器系統的限制。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-114">However, as of December 2016, there is a restriction to single-container systems.</span></span> <span data-ttu-id="cbb9c-115">多租用戶容器設定不支援這類資料庫快照集 (請參閱[建立儲存體快照集 (SAP HANA Studio)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/a0/3f8f08501e44d89115db3c5aa08e3f/content.htm))。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-115">Multitenant container configurations do not support this kind of database snapshot (see [Create a Storage Snapshot (SAP HANA Studio)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/a0/3f8f08501e44d89115db3c5aa08e3f/content.htm)).</span></span>

<span data-ttu-id="cbb9c-116">其運作如下：</span><span class="sxs-lookup"><span data-stu-id="cbb9c-116">It works as follows:</span></span>

- <span data-ttu-id="cbb9c-117">起始 SAP HANA 快照集，為儲存體快照做準備</span><span class="sxs-lookup"><span data-stu-id="cbb9c-117">Prepare for a storage snapshot by initiating the SAP HANA snapshot</span></span>
- <span data-ttu-id="cbb9c-118">執行儲存體快照集 (例如 Azure blob 快照集)</span><span class="sxs-lookup"><span data-stu-id="cbb9c-118">Run the storage snapshot (Azure blob snapshot, for example)</span></span>
- <span data-ttu-id="cbb9c-119">確認 SAP HANA 快照集</span><span class="sxs-lookup"><span data-stu-id="cbb9c-119">Confirm the SAP HANA snapshot</span></span>

![這個螢幕擷取畫面顯示透過 SQL 陳述式建立的 SAP HANA 資料快照集](media/sap-hana-backup-storage-snapshots/image011.png)

<span data-ttu-id="cbb9c-121">這個螢幕擷取畫面顯示透過 SQL 陳述式建立的 SAP HANA 資料快照集。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-121">This screenshot shows that an SAP HANA data snapshot can be created via a SQL statement.</span></span>

![然後快照集也會出現在 SAP HANA Studio 的備份目錄中](media/sap-hana-backup-storage-snapshots/image012.png)

<span data-ttu-id="cbb9c-123">然後快照集也會出現在 SAP HANA Studio 的備份目錄中。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-123">The snapshot then also appears in the backup catalog in SAP HANA Studio.</span></span>

![快照集會出現在磁碟上的 SAP HANA 資料目錄中](media/sap-hana-backup-storage-snapshots/image013.png)

<span data-ttu-id="cbb9c-125">快照集會出現在磁碟上的 SAP HANA 資料目錄中。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-125">On disk, the snapshot shows up in the SAP HANA data directory.</span></span>

<span data-ttu-id="cbb9c-126">當 SAP HANA 處於快照集準備模式時，執行儲存體快照集之前，您必須確定也能保證檔案系統一致性。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-126">One has to ensure that the file system consistency is also guaranteed before running the storage snapshot while SAP HANA is in the snapshot preparation mode.</span></span> <span data-ttu-id="cbb9c-127">請參閱相關文章 [Azure 虛擬機器上 SAP HANA 的備份指南](sap-hana-backup-guide.md)中的＜建立儲存體快照集時，SAP HANA 資料的一致性＞。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-127">See _SAP HANA data consistency when taking storage snapshots_ in the related article [Backup guide for SAP HANA on Azure Virtual Machines](sap-hana-backup-guide.md).</span></span>

<span data-ttu-id="cbb9c-128">完成儲存體快照集時，務必確認 SAP HANA 快照集。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-128">Once the storage snapshot is done, it is critical to confirm the SAP HANA snapshot.</span></span> <span data-ttu-id="cbb9c-129">有個對應的 SQL 陳述式可以執行︰BACKUP DATA CLOSE SNAPSHOT (請參閱 [BACKUP DATA CLOSE SNAPSHOT陳述式 (備份和復原)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/c3/9739966f7f4bd5818769ad4ce6a7f8/content.htm)。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-129">There is a corresponding SQL statement to run: BACKUP DATA CLOSE SNAPSHOT (see [BACKUP DATA CLOSE SNAPSHOT Statement (Backup and Recovery)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/c3/9739966f7f4bd5818769ad4ce6a7f8/content.htm)).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cbb9c-130">確認 HANA 快照集。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-130">Confirm the HANA snapshot.</span></span> <span data-ttu-id="cbb9c-131">由於「寫入時複製」&quot;&quot;的特性，SAP HANA 在快照集準備模式可能需要額外的磁碟空間，而且不確認 SAP HANA 快照集就不能啟動新的備份。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-131">Due to &quot;Copy-on-Write,&quot; SAP HANA might require additional disk space in snapshot-prepare mode, and it is not possible to start new backups until the SAP HANA snapshot is confirmed.</span></span>

## <a name="hana-vm-backup-via-azure-backup-service"></a><span data-ttu-id="cbb9c-132">透過 Azure 備份服務備份 HANA VM</span><span class="sxs-lookup"><span data-stu-id="cbb9c-132">HANA VM backup via Azure Backup service</span></span>

<span data-ttu-id="cbb9c-133">自 2016 年 12 月起，Azure 備份服務的備份代理程式不再適用於 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-133">As of December 2016, the backup agent of the Azure Backup service is not available for Linux VMs.</span></span> <span data-ttu-id="cbb9c-134">若要進行檔案/目錄層級的 Azure 備份，可以將 SAP HANA 備份檔案複製到 Windows VM，然後使用該備份代理程式。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-134">To make use of Azure backup on the file/directory level, one would copy SAP HANA backup files to a Windows VM and then use the backup agent.</span></span> <span data-ttu-id="cbb9c-135">否則，只能透過 Azure 備份服務進行完整的 Linux VM 備份。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-135">Otherwise, only a full Linux VM backup is possible via the Azure Backup service.</span></span> <span data-ttu-id="cbb9c-136">詳細資訊請參閱 [Azure 備份中的功能概觀](../../../backup/backup-introduction-to-azure-backup.md)。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-136">See [Overview of the features in Azure Backup](../../../backup/backup-introduction-to-azure-backup.md) to find out more.</span></span>

<span data-ttu-id="cbb9c-137">Azure 備份服務提供備份和還原 VM 的選項。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-137">The Azure Backup service offers an option to back up and restore a VM.</span></span> <span data-ttu-id="cbb9c-138">關於此服務和運作方式的詳細資訊，可在[在 Azure 中規劃 VM 備份基礎結構](../../../backup/backup-azure-vms-introduction.md)中找到。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-138">More information about this service and how it works can be found in the article [Plan your VM backup infrastructure in Azure](../../../backup/backup-azure-vms-introduction.md).</span></span>

<span data-ttu-id="cbb9c-139">根據這篇文章，有兩個重要的考量︰</span><span class="sxs-lookup"><span data-stu-id="cbb9c-139">There are two important considerations according to that article:</span></span>

<span data-ttu-id="cbb9c-140">「Linux 虛擬機器則只能進行檔案一致的備份，因為 Linux 沒有相當於 VSS 的平台。」_&quot;&quot;_</span><span class="sxs-lookup"><span data-stu-id="cbb9c-140">_&quot;For Linux virtual machines, only file-consistent backups are possible, since Linux does not have an equivalent platform to VSS.&quot;_</span></span>

<span data-ttu-id="cbb9c-141">「應用程式需要在還原的資料上實作自己的「修正」機制。」_&quot;&quot;&quot;&quot;_</span><span class="sxs-lookup"><span data-stu-id="cbb9c-141">_&quot;Applications need to implement their own &quot;fix-up&quot; mechanism on the restored data.&quot;_</span></span>

<span data-ttu-id="cbb9c-142">因此，您必須確定備份啟動時，磁碟上的 SAP HANA 是處於一致的狀態。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-142">Therefore, one has to make sure SAP HANA is in a consistent state on disk when the backup starts.</span></span> <span data-ttu-id="cbb9c-143">請參閱本文稍早的＜SAP HANA 快照集＞。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-143">See _SAP HANA snapshots_ described earlier in the document.</span></span> <span data-ttu-id="cbb9c-144">但是當 SAP HANA 保持在此快照集準備模式中時，還有潛在的問題。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-144">But there is a potential issue when SAP HANA stays in this snapshot preparation mode.</span></span> <span data-ttu-id="cbb9c-145">如需詳細資訊，請參閱[建立儲存體快照集 (SAP HANA Studio)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/a0/3f8f08501e44d89115db3c5aa08e3f/content.htm)。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-145">See [Create a Storage Snapshot (SAP HANA Studio)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/a0/3f8f08501e44d89115db3c5aa08e3f/content.htm) for more information.</span></span>

<span data-ttu-id="cbb9c-146">這篇文章中提到︰</span><span class="sxs-lookup"><span data-stu-id="cbb9c-146">That article states:</span></span>

<span data-ttu-id="cbb9c-147">_&quot;「強烈建議建立儲存體快照集之後，儘速確認或放棄它。準備或建立儲存體快照集時，與快照集相關的資料會被凍結。當快照集相關資料處於凍結，資料庫中仍然可以進行變更。這類變更不會使凍結的快照集相關資料跟著變更。相反地，變更會寫入資料區域中與儲存體快照集分開的位置。變更也會寫入記錄。不過，快照集相關資料凍結愈久，資料磁碟區可以成長愈多。」&quot;_</span><span class="sxs-lookup"><span data-stu-id="cbb9c-147">_&quot;It is strongly recommended to confirm or abandon a storage snapshot as soon as possible after it has been created. While the storage snapshot is being prepared or created, the snapshot-relevant data is frozen. While the snapshot-relevant data remains frozen, changes can still be made in the database. Such changes will not cause the frozen snapshot-relevant data to be changed. Instead, the changes are written to positions in the data area that are separate from the storage snapshot. Changes are also written to the log. However, the longer the snapshot-relevant data is kept frozen, the more the data volume can grow.&quot;_</span></span>

<span data-ttu-id="cbb9c-148">Azure 備份會透過 Azure VM 的擴充功能來處理檔案系統的一致性。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-148">Azure Backup takes care of the file system consistency via Azure VM extensions.</span></span> <span data-ttu-id="cbb9c-149">這些擴充功能沒有獨立版本，只能結合 Azure 備份服務使用。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-149">These extensions are not available standalone, and work only in combination with Azure Backup service.</span></span> <span data-ttu-id="cbb9c-150">不過，它仍然是管理 SAP HANA 快照集以確保應用程式一致性的必要功能。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-150">Nevertheless, it is still a requirement to manage an SAP HANA snapshot to guarantee app consistency.</span></span>

<span data-ttu-id="cbb9c-151">Azure 備份有兩個主要階段︰</span><span class="sxs-lookup"><span data-stu-id="cbb9c-151">Azure Backup has two major phases:</span></span>

- <span data-ttu-id="cbb9c-152">建立快照集</span><span class="sxs-lookup"><span data-stu-id="cbb9c-152">Take Snapshot</span></span>
- <span data-ttu-id="cbb9c-153">將資料傳輸至保存庫</span><span class="sxs-lookup"><span data-stu-id="cbb9c-153">Transfer data to vault</span></span>

<span data-ttu-id="cbb9c-154">一旦 Azure 備份服務的建立快照集階段完成，就可以確認 SAP HANA 快照集。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-154">So one could confirm the SAP HANA snapshot once the Azure Backup service phase of taking a snapshot is completed.</span></span> <span data-ttu-id="cbb9c-155">可能要等幾分鐘後才會在 Azure 入口網站看到。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-155">It might take several minutes to see in the Azure portal.</span></span>

![本圖顯示 Azure 備份服務的部分備份作業清單](media/sap-hana-backup-storage-snapshots/image014.png)

<span data-ttu-id="cbb9c-157">本圖顯示 Azure 備份服務的部分備份作業清單，這個服務用於備份 HANA 測試 VM。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-157">This figure shows part of the backup job list of an Azure Backup service, which was used to back up the HANA test VM.</span></span>

![若要顯示作業詳細資料，按一下 Azure 入口網站中的備份作業](media/sap-hana-backup-storage-snapshots/image015.png)

<span data-ttu-id="cbb9c-159">若要顯示作業詳細資料，按一下 Azure 入口網站中的備份作業。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-159">To show the job details, click the backup job in the Azure portal.</span></span> <span data-ttu-id="cbb9c-160">在這裡可以看到兩個階段。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-160">Here, one can see the two phases.</span></span> <span data-ttu-id="cbb9c-161">可能需要幾分鐘，快照集階段才會顯示為已完成。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-161">It might take a few minutes until it shows the snapshot phase as completed.</span></span> <span data-ttu-id="cbb9c-162">大部分的時間花在資料傳輸階段。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-162">Most of the time is spent in the data transfer phase.</span></span>

## <a name="hana-vm-backup-automation-via-azure-backup-service"></a><span data-ttu-id="cbb9c-163">透過 Azure 備份服務進行 HANA VM 自動備份</span><span class="sxs-lookup"><span data-stu-id="cbb9c-163">HANA VM backup automation via Azure Backup service</span></span>

<span data-ttu-id="cbb9c-164">如先前所述，Azure 備份的快照集階段一旦完成，便可以手動確認 SAP HANA 快照集，但最好考慮自動化，因為管理員可能無法監視 Azure 入口網站中列出的備份作業清單。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-164">One could manually confirm the SAP HANA snapshot once the Azure Backup snapshot phase is completed, as described earlier, but it is helpful to consider automation because an admin might not monitor the backup job list in the Azure portal.</span></span>

<span data-ttu-id="cbb9c-165">以下說明如何透過 Azure PowerShell Cmdlet 達成。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-165">Here is an explanation how it could be accomplished via Azure PowerShell cmdlets.</span></span>

![Azure 備份服務是以 hana-backup-vault 的名稱建立](media/sap-hana-backup-storage-snapshots/image016.png)

<span data-ttu-id="cbb9c-167">Azure 備份服務是以 &quot;hana-backup-vault&quot; 的名稱建立。PS 命令 **Get-AzureRmRecoveryServicesVault -Name hana-backup-vault** 會擷取對應的物件。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-167">An Azure Backup service was created with the name &quot;hana-backup-vault.&quot; The PS command **Get-AzureRmRecoveryServicesVault -Name hana-backup-vault** retrieves the corresponding object.</span></span> <span data-ttu-id="cbb9c-168">然後這個物件會被用來設定備份的內容，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-168">This object is then used to set the backup context as seen on the next figure.</span></span>

![可以查看正在進行的備份作業](media/sap-hana-backup-storage-snapshots/image017.png)

<span data-ttu-id="cbb9c-170">設定正確的內容之後，可以查看目前正在進行的備份作業，並查看其作業詳細資料。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-170">After setting the correct context, one can check for the backup job currently in progress, and then look for its job details.</span></span> <span data-ttu-id="cbb9c-171">子作業清單會顯示 Azure 備份作業的快照集階段是否已經完成︰</span><span class="sxs-lookup"><span data-stu-id="cbb9c-171">The subtask list shows if the snapshot phase of the Azure backup job is already completed:</span></span>

```
$ars = Get-AzureRmRecoveryServicesVault -Name hana-backup-vault
Set-AzureRmRecoveryServicesVaultContext -Vault $ars
$jid = Get-AzureRmRecoveryServicesBackupJob -Status InProgress | select -ExpandProperty jobid
Get-AzureRmRecoveryServicesBackupJobDetails -Jobid $jid | select -ExpandProperty subtasks
```

![在迴圈中輪詢值，直到狀態變成已完成](media/sap-hana-backup-storage-snapshots/image018.png)

<span data-ttu-id="cbb9c-173">作業詳細資料儲存在變數中之後，只要用 PS 語法便可取得第一個陣列項目，並擷取狀態值。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-173">Once the job details are stored in a variable, it is simply PS syntax to get to the first array entry and retrieve the status value.</span></span> <span data-ttu-id="cbb9c-174">若要完成自動化指令碼，在迴圈中輪詢值，直到狀態變成 &quot;Completed&quot;。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-174">To complete the automation script, poll the value in a loop until it turns to &quot;Completed.&quot;</span></span>

```
$st = Get-AzureRmRecoveryServicesBackupJobDetails -Jobid $jid | select -ExpandProperty subtasks
$st[0] | select -ExpandProperty status
```

## <a name="hana-license-key-and-vm-restore-via-azure-backup-service"></a><span data-ttu-id="cbb9c-175">透過 Azure 備份服務的 HANA 授權金鑰和 VM 還原</span><span class="sxs-lookup"><span data-stu-id="cbb9c-175">HANA license key and VM restore via Azure Backup service</span></span>

<span data-ttu-id="cbb9c-176">Azure 備份服務為了在還原期間建立新 VM 而設計。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-176">The Azure Backup service is designed to create a new VM during restore.</span></span> <span data-ttu-id="cbb9c-177">目前還沒有&quot;就地&quot;還原現有 Azure VM 的規劃。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-177">There is no plan right now to do an &quot;in-place&quot; restore of an existing Azure VM.</span></span>

![此圖顯示 Azure 入口網站中 Azure 服務的還原選項](media/sap-hana-backup-storage-snapshots/image019.png)

<span data-ttu-id="cbb9c-179">此圖顯示 Azure 入口網站中 Azure 服務的還原選項。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-179">This figure shows the restore option of the Azure service in the Azure portal.</span></span> <span data-ttu-id="cbb9c-180">可以選擇在還原期間建立 VM，或還原磁碟。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-180">One can choose between creating a VM during restore or restoring the disks.</span></span> <span data-ttu-id="cbb9c-181">還原磁碟後，仍然必須在其之上建立新的 VM。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-181">After restoring the disks, it is still necessary to create a new VM on top of it.</span></span> <span data-ttu-id="cbb9c-182">每次在 Azure 上建立新的 VM，唯一 VM 識別碼就會變更 (請參閱[存取和使用 Azure VM 唯一識別碼](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/))。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-182">Whenever a new VM gets created on Azure the unique VM ID changes (see [Accessing and Using Azure VM Unique ID](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/)).</span></span>

![此圖顯示透過 Azure 備份服務進行還原前後的 Azure VM 唯一識別碼](media/sap-hana-backup-storage-snapshots/image020.png)

<span data-ttu-id="cbb9c-184">此圖顯示透過 Azure 備份服務進行還原前後的 Azure VM 唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-184">This figure shows the Azure VM unique ID before and after the restore via Azure Backup service.</span></span> <span data-ttu-id="cbb9c-185">SAP 硬體機碼 (用於 SAP 授權) 會使用這個唯一的 VM 識別碼。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-185">The SAP hardware key, which is used for SAP licensing, is using this unique VM ID.</span></span> <span data-ttu-id="cbb9c-186">因此，必須在 VM 還原後安裝新的 SAP 授權。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-186">As a consequence, a new SAP license has to be installed after a VM restore.</span></span>

<span data-ttu-id="cbb9c-187">在編寫本備份指南的期間，預覽模式中有了新的 Azure 備份功能。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-187">A new Azure Backup feature was presented in preview mode during the creation of this backup guide.</span></span> <span data-ttu-id="cbb9c-188">可以根據之前為了 VM 備份而建立的 VM 快照集，進行檔案層級的還原。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-188">It allows a file level restore based on the VM snapshot that was taken for the VM backup.</span></span> <span data-ttu-id="cbb9c-189">這樣就不必部署新的 VM，因此唯一 VM 識別碼維持不變，不需要新的 SAP HANA 授權金鑰。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-189">This avoids the need to deploy a new VM, and therefore the unique VM ID stays the same and no new SAP HANA license key is required.</span></span> <span data-ttu-id="cbb9c-190">有關這項功能的詳細文件，將會在經過完整測試之後提供。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-190">More documentation on this feature will be provided after it is fully tested.</span></span>

<span data-ttu-id="cbb9c-191">Azure 備份最終將會允許備份個別 Azure 虛擬磁碟，加上虛擬機器內部的檔案和目錄。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-191">Azure Backup will eventually allow backup of individual Azure virtual disks, plus files and directories from inside the VM.</span></span> <span data-ttu-id="cbb9c-192">Azure 備份的主要優點，是它可以管理所有備份，讓客戶不需要做這件事。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-192">A major advantage of Azure Backup is its management of all the backups, saving the customer from having to do it.</span></span> <span data-ttu-id="cbb9c-193">如果需要還原，Azure 備份會選取正確的備份來使用。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-193">If a restore becomes necessary, Azure Backup will select the correct backup to use.</span></span>

## <a name="sap-hana-vm-backup-via-manual-disk-snapshot"></a><span data-ttu-id="cbb9c-194">透過手動磁碟快照集進行 SAP HANA VM 備份</span><span class="sxs-lookup"><span data-stu-id="cbb9c-194">SAP HANA VM backup via manual disk snapshot</span></span>

<span data-ttu-id="cbb9c-195">除了使用 Azure 備份服務，您也可以設定個別備份解決方案，透過 PowerShell 手動建立 Azure VHD 的 blob 快照集。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-195">Instead of using the Azure Backup service, one could configure an individual backup solution by creating blob snapshots of Azure VHDs manually via PowerShell.</span></span> <span data-ttu-id="cbb9c-196">如需步驟說明，請參閱[以 PowerShell 使用 blob 快照集](https://blogs.msdn.microsoft.com/cie/2016/05/17/using-blob-snapshots-with-powershell/)。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-196">See [Using blob snapshots with PowerShell](https://blogs.msdn.microsoft.com/cie/2016/05/17/using-blob-snapshots-with-powershell/) for a description of the steps.</span></span>

<span data-ttu-id="cbb9c-197">它提供更大的彈性，但不能解決本文件稍早所述的問題︰</span><span class="sxs-lookup"><span data-stu-id="cbb9c-197">It provides more flexibility but does not resolve the issues explained earlier in this document:</span></span>

- <span data-ttu-id="cbb9c-198">您仍然必須確定 SAP HANA 處於一致的狀態</span><span class="sxs-lookup"><span data-stu-id="cbb9c-198">One still must make sure that SAP HANA is in a consistent state</span></span>
- <span data-ttu-id="cbb9c-199">即使因為有「有租用存在」錯誤而將 VM 解除配置，仍然無法覆寫作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-199">The OS disk cannot be overwritten even if the VM is deallocated because of an error stating that a lease exists.</span></span> <span data-ttu-id="cbb9c-200">必須要在刪除 VM之後才能覆寫，而這會導致新的唯一 VM 識別碼，故需要安裝新的 SAP 授權。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-200">It only works after deleting the VM, which would lead to a new unique VM ID and the need to install a new SAP license.</span></span>

![可以只還原 Azure VM 的資料磁碟](media/sap-hana-backup-storage-snapshots/image021.png)

<span data-ttu-id="cbb9c-202">可以只還原 Azure VM 的資料磁碟，避免取得新的唯一 VM 識別碼進而使 SAP 授權失效的問題︰</span><span class="sxs-lookup"><span data-stu-id="cbb9c-202">It is possible to restore only the data disks of an Azure VM, avoiding the problem of getting a new unique VM ID and, therefore, invalidated the SAP license:</span></span>

- <span data-ttu-id="cbb9c-203">測試中將兩個 Azure 資料磁碟連結至 VM，並在其上定義軟體 RAID</span><span class="sxs-lookup"><span data-stu-id="cbb9c-203">For the test, two Azure data disks were attached to a VM and software RAID was defined on top of them</span></span> 
- <span data-ttu-id="cbb9c-204">已經利用 SAP HANA 快照集功能確認的 SAP HANA 處於一致的狀態</span><span class="sxs-lookup"><span data-stu-id="cbb9c-204">It was confirmed that SAP HANA was in a consistent state by SAP HANA snapshot feature</span></span>
- <span data-ttu-id="cbb9c-205">檔案系統凍結 (請參閱相關文章 [Azure 虛擬機器上 SAP HANA 的備份指南](sap-hana-backup-guide.md)中的＜建立儲存體快照集時，SAP HANA 資料的一致性＞)</span><span class="sxs-lookup"><span data-stu-id="cbb9c-205">File system freeze (see _SAP HANA data consistency when taking storage snapshots_ in the related article [Backup guide for SAP HANA on Azure Virtual Machines](sap-hana-backup-guide.md))</span></span>
- <span data-ttu-id="cbb9c-206">從這兩個資料磁碟建立 blob 快照集</span><span class="sxs-lookup"><span data-stu-id="cbb9c-206">Blob snapshots were taken from both data disks</span></span>
- <span data-ttu-id="cbb9c-207">檔案系統解除凍結</span><span class="sxs-lookup"><span data-stu-id="cbb9c-207">File system unfreeze</span></span>
- <span data-ttu-id="cbb9c-208">確認 SAP HANA 快照集</span><span class="sxs-lookup"><span data-stu-id="cbb9c-208">SAP HANA snapshot confirmation</span></span>
- <span data-ttu-id="cbb9c-209">為了還原資料磁碟，已關閉 VM，並中斷兩個磁碟的連結</span><span class="sxs-lookup"><span data-stu-id="cbb9c-209">To restore the data disks, the VM was shut down and both disks detached</span></span>
- <span data-ttu-id="cbb9c-210">中斷連結磁碟之後，以先前的 blob 快照集覆寫磁碟</span><span class="sxs-lookup"><span data-stu-id="cbb9c-210">After detaching the disks, they were overwritten with the former blob snapshots</span></span>
- <span data-ttu-id="cbb9c-211">然後將還原後的虛擬磁碟再次連結至 VM</span><span class="sxs-lookup"><span data-stu-id="cbb9c-211">Then the restored virtual disks were attached again to the VM</span></span>
- <span data-ttu-id="cbb9c-212">啟動 VM 後，軟體 RAID 上的所有項目正常運作，並已回到 blob 快照集時間的狀態</span><span class="sxs-lookup"><span data-stu-id="cbb9c-212">After starting the VM, everything on the software RAID worked fine and was set back to the blob snapshot time</span></span>
- <span data-ttu-id="cbb9c-213">HANA 已回到 HANA 快照集的狀態</span><span class="sxs-lookup"><span data-stu-id="cbb9c-213">HANA was set back to the HANA snapshot</span></span>

<span data-ttu-id="cbb9c-214">如果可以在進行 blob 快照集之前關閉 SAP HANA，程序會比較不複雜。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-214">If it was possible to shut down SAP HANA before the blob snapshots, the procedure would be less complex.</span></span> <span data-ttu-id="cbb9c-215">在此情況下，可以略過 HANA 快照集，而且如果系統上沒有在進行其他作業，也可以略過檔案系統凍結。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-215">In that case, one could skip the HANA snapshot and, if nothing else is going on in the system, also skip the file system freeze.</span></span> <span data-ttu-id="cbb9c-216">當需要在所有項目都在線上時執行快照集，複雜度就會增加。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-216">Added complexity comes into the picture when it is necessary to do snapshots while everything is online.</span></span> <span data-ttu-id="cbb9c-217">請參閱相關文章 [Azure 虛擬機器上 SAP HANA 的備份指南](sap-hana-backup-guide.md)中的＜建立儲存體快照集時，SAP HANA 資料的一致性＞。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-217">See _SAP HANA data consistency when taking storage snapshots_ in the related article [Backup guide for SAP HANA on Azure Virtual Machines](sap-hana-backup-guide.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cbb9c-218">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cbb9c-218">Next steps</span></span>
* <span data-ttu-id="cbb9c-219">[Azure 虛擬機器上 SAP HANA 的備份指南](sap-hana-backup-guide.md)提供快速入門的概觀和詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-219">[Backup guide for SAP HANA on Azure Virtual Machines](sap-hana-backup-guide.md) gives an overview and information on getting started.</span></span>
* <span data-ttu-id="cbb9c-220">[檔案層級的 SAP HANA 備份](sap-hana-backup-file-level.md)說明以檔案為基礎的備份選項。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-220">[SAP HANA backup based on file level](sap-hana-backup-file-level.md) covers the file-based backup option.</span></span>
* <span data-ttu-id="cbb9c-221">若要了解如何建立高可用性並為 Azure 上的 SAP HANA 規劃災害復原，請參閱 [Azure 上的 SAP HANA (大型執行個體) 高可用性和災害復原](hana-overview-high-availability-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="cbb9c-221">To learn how to establish high availability and plan for disaster recovery of SAP HANA on Azure (large instances), see [SAP HANA (large instances) high availability and disaster recovery on Azure](hana-overview-high-availability-disaster-recovery.md).</span></span>
