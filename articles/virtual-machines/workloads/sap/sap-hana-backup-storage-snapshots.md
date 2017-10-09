---
title: "aaaSAP HANA Azure 備份為基礎儲存快照集 |Microsoft 文件"
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
ms.openlocfilehash: 32bb80f5a928a2cf63699bfe4f4cf5bbad81e6fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-backup-based-on-storage-snapshots"></a><span data-ttu-id="46e76-103">以儲存體快照集為基礎的 SAP HANA 備份</span><span class="sxs-lookup"><span data-stu-id="46e76-103">SAP HANA backup based on storage snapshots</span></span>

## <a name="introduction"></a><span data-ttu-id="46e76-104">簡介</span><span class="sxs-lookup"><span data-stu-id="46e76-104">Introduction</span></span>

<span data-ttu-id="46e76-105">這是與 SAP HANA 備份相關的三篇系列文章的其中一篇。</span><span class="sxs-lookup"><span data-stu-id="46e76-105">This is part of a three-part series of related articles on SAP HANA backup.</span></span> <span data-ttu-id="46e76-106">[備份指南的 SAP HANA Azure 虛擬機器上](sap-hana-backup-guide.md)上開始使用提供的概觀和資訊和[SAP HANA Azure 備份檔案層級上](sap-hana-backup-file-level.md)涵蓋 hello 以檔案為基礎的備份選項。</span><span class="sxs-lookup"><span data-stu-id="46e76-106">[Backup guide for SAP HANA on Azure Virtual Machines](sap-hana-backup-guide.md) provides an overview and information on getting started, and [SAP HANA Azure Backup on file level](sap-hana-backup-file-level.md) covers hello file-based backup option.</span></span>

<span data-ttu-id="46e76-107">當使用單一執行個體全部的一個示範系統的 VM 備份的功能，其中一個應該考慮而不是管理在 hello 作業系統層級的 HANA 備份 VM 備份。</span><span class="sxs-lookup"><span data-stu-id="46e76-107">When using a VM backup feature for a single-instance all-in-one demo system, one should consider doing a VM backup instead of managing HANA backups at hello OS level.</span></span> <span data-ttu-id="46e76-108">替代方式是 tootake Azure blob 快照集 toocreate 份個別的虛擬磁碟，也就是附加的 tooa 虛擬機器，然後保留 hello HANA 資料檔案。</span><span class="sxs-lookup"><span data-stu-id="46e76-108">An alternative is tootake Azure blob snapshots toocreate copies of individual virtual disks, which are attached tooa virtual machine, and keep hello HANA data files.</span></span> <span data-ttu-id="46e76-109">但是，關鍵在於當建立 VM 的備份或磁碟快照時 hello 系統已啟動並執行應用程式一致性。</span><span class="sxs-lookup"><span data-stu-id="46e76-109">But a critical point is app consistency when creating a VM backup or disk snapshot while hello system is up and running.</span></span> <span data-ttu-id="46e76-110">請參閱_建立儲存體的快照集時，SAP HANA 資料一致性_hello 相關文件中[備份指南的 SAP HANA Azure 虛擬機器上](sap-hana-backup-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="46e76-110">See _SAP HANA data consistency when taking storage snapshots_ in hello related article [Backup guide for SAP HANA on Azure Virtual Machines](sap-hana-backup-guide.md).</span></span> <span data-ttu-id="46e76-111">SAP HANA 有個功能支援這類的儲存體快照集。</span><span class="sxs-lookup"><span data-stu-id="46e76-111">SAP HANA has a feature that supports these kinds of storage snapshots.</span></span>

## <a name="sap-hana-snapshots"></a><span data-ttu-id="46e76-112">SAP HANA 快照集</span><span class="sxs-lookup"><span data-stu-id="46e76-112">SAP HANA snapshots</span></span>

<span data-ttu-id="46e76-113">SAP HANA 中有個功能支援建立儲存體快照集。</span><span class="sxs-lookup"><span data-stu-id="46e76-113">There is a feature in SAP HANA that supports taking a storage snapshot.</span></span> <span data-ttu-id="46e76-114">不過，年 12 月從 2016年開始，沒有限制 toosingle 容器系統。</span><span class="sxs-lookup"><span data-stu-id="46e76-114">However, as of December 2016, there is a restriction toosingle-container systems.</span></span> <span data-ttu-id="46e76-115">多租用戶容器設定不支援這類資料庫快照集 (請參閱[建立儲存體快照集 (SAP HANA Studio)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/a0/3f8f08501e44d89115db3c5aa08e3f/content.htm))。</span><span class="sxs-lookup"><span data-stu-id="46e76-115">Multitenant container configurations do not support this kind of database snapshot (see [Create a Storage Snapshot (SAP HANA Studio)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/a0/3f8f08501e44d89115db3c5aa08e3f/content.htm)).</span></span>

<span data-ttu-id="46e76-116">其運作如下：</span><span class="sxs-lookup"><span data-stu-id="46e76-116">It works as follows:</span></span>

- <span data-ttu-id="46e76-117">起始 hello SAP HANA 快照集，準備儲存快照集</span><span class="sxs-lookup"><span data-stu-id="46e76-117">Prepare for a storage snapshot by initiating hello SAP HANA snapshot</span></span>
- <span data-ttu-id="46e76-118">執行 hello 儲存快照集 (快照集，例如 Azure blob)</span><span class="sxs-lookup"><span data-stu-id="46e76-118">Run hello storage snapshot (Azure blob snapshot, for example)</span></span>
- <span data-ttu-id="46e76-119">確認 hello SAP HANA 快照集</span><span class="sxs-lookup"><span data-stu-id="46e76-119">Confirm hello SAP HANA snapshot</span></span>

![這個螢幕擷取畫面顯示透過 SQL 陳述式建立的 SAP HANA 資料快照集](media/sap-hana-backup-storage-snapshots/image011.png)

<span data-ttu-id="46e76-121">這個螢幕擷取畫面顯示透過 SQL 陳述式建立的 SAP HANA 資料快照集。</span><span class="sxs-lookup"><span data-stu-id="46e76-121">This screenshot shows that an SAP HANA data snapshot can be created via a SQL statement.</span></span>

![hello 然後快照集也會出現在 SAP HANA Studio 中的 hello 備份類別目錄](media/sap-hana-backup-storage-snapshots/image012.png)

<span data-ttu-id="46e76-123">hello 然後快照集也會出現在 SAP HANA Studio 中的 hello 備份類別目錄。</span><span class="sxs-lookup"><span data-stu-id="46e76-123">hello snapshot then also appears in hello backup catalog in SAP HANA Studio.</span></span>

![在磁碟上，hello 快照集顯示在 hello SAP HANA 資料目錄](media/sap-hana-backup-storage-snapshots/image013.png)

<span data-ttu-id="46e76-125">在磁碟上，hello 快照會在顯示 hello SAP HANA 資料目錄。</span><span class="sxs-lookup"><span data-stu-id="46e76-125">On disk, hello snapshot shows up in hello SAP HANA data directory.</span></span>

<span data-ttu-id="46e76-126">其中一個有 tooensure hello 檔案系統一致性也會保證在 SAP HANA hello 快照準備模式時，執行 hello 儲存快照集之前。</span><span class="sxs-lookup"><span data-stu-id="46e76-126">One has tooensure that hello file system consistency is also guaranteed before running hello storage snapshot while SAP HANA is in hello snapshot preparation mode.</span></span> <span data-ttu-id="46e76-127">請參閱_建立儲存體的快照集時，SAP HANA 資料一致性_hello 相關文件中[備份指南的 SAP HANA Azure 虛擬機器上](sap-hana-backup-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="46e76-127">See _SAP HANA data consistency when taking storage snapshots_ in hello related article [Backup guide for SAP HANA on Azure Virtual Machines](sap-hana-backup-guide.md).</span></span>

<span data-ttu-id="46e76-128">一旦完成 hello 儲存快照集後，就會是重要 tooconfirm hello SAP HANA 快照集。</span><span class="sxs-lookup"><span data-stu-id="46e76-128">Once hello storage snapshot is done, it is critical tooconfirm hello SAP HANA snapshot.</span></span> <span data-ttu-id="46e76-129">沒有對應的 SQL 陳述式 toorun： 備份資料關閉快照集 (請參閱[備份資料關閉快照集陳述式 （備份和復原）](https://help.sap.com/saphelp_hanaplatform/helpdata/en/c3/9739966f7f4bd5818769ad4ce6a7f8/content.htm))。</span><span class="sxs-lookup"><span data-stu-id="46e76-129">There is a corresponding SQL statement toorun: BACKUP DATA CLOSE SNAPSHOT (see [BACKUP DATA CLOSE SNAPSHOT Statement (Backup and Recovery)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/c3/9739966f7f4bd5818769ad4ce6a7f8/content.htm)).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="46e76-130">確認 hello HANA 快照集。</span><span class="sxs-lookup"><span data-stu-id="46e76-130">Confirm hello HANA snapshot.</span></span> <span data-ttu-id="46e76-131">因為太&quot;上寫入複製&quot;SAP HANA 可能需要額外的磁碟空間，在快照集準備模式中，而且不可能 toostart 新的備份之前確認 hello SAP HANA 快照集。</span><span class="sxs-lookup"><span data-stu-id="46e76-131">Due too&quot;Copy-on-Write,&quot; SAP HANA might require additional disk space in snapshot-prepare mode, and it is not possible toostart new backups until hello SAP HANA snapshot is confirmed.</span></span>

## <a name="hana-vm-backup-via-azure-backup-service"></a><span data-ttu-id="46e76-132">透過 Azure 備份服務備份 HANA VM</span><span class="sxs-lookup"><span data-stu-id="46e76-132">HANA VM backup via Azure Backup service</span></span>

<span data-ttu-id="46e76-133">年 12 月從 2016年開始，不是適用於 Linux Vm hello hello Azure 備份服務的備份代理程式。</span><span class="sxs-lookup"><span data-stu-id="46e76-133">As of December 2016, hello backup agent of hello Azure Backup service is not available for Linux VMs.</span></span> <span data-ttu-id="46e76-134">使用 Azure 備份 toomake hello 檔案/目錄層級，其中會複製 SAP HANA 備份檔案 tooa Windows VM，然後使用 hello 備份代理程式。</span><span class="sxs-lookup"><span data-stu-id="46e76-134">toomake use of Azure backup on hello file/directory level, one would copy SAP HANA backup files tooa Windows VM and then use hello backup agent.</span></span> <span data-ttu-id="46e76-135">否則，完整 Linux VM 備份是可透過 hello Azure Backup 服務。</span><span class="sxs-lookup"><span data-stu-id="46e76-135">Otherwise, only a full Linux VM backup is possible via hello Azure Backup service.</span></span> <span data-ttu-id="46e76-136">請參閱[中 Azure Backup 功能概觀 hello](../../../backup/backup-introduction-to-azure-backup.md) toofind 深入了解。</span><span class="sxs-lookup"><span data-stu-id="46e76-136">See [Overview of hello features in Azure Backup](../../../backup/backup-introduction-to-azure-backup.md) toofind out more.</span></span>

<span data-ttu-id="46e76-137">hello Azure 備份服務提供選項 tooback，並還原 VM。</span><span class="sxs-lookup"><span data-stu-id="46e76-137">hello Azure Backup service offers an option tooback up and restore a VM.</span></span> <span data-ttu-id="46e76-138">此服務和其運作方式的詳細資訊可以在 hello 文章中找到[規劃 VM 備份基礎結構在 Azure 中的](../../../backup/backup-azure-vms-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="46e76-138">More information about this service and how it works can be found in hello article [Plan your VM backup infrastructure in Azure](../../../backup/backup-azure-vms-introduction.md).</span></span>

<span data-ttu-id="46e76-139">有兩個重要的考量，根據 toothat 發行項：</span><span class="sxs-lookup"><span data-stu-id="46e76-139">There are two important considerations according toothat article:</span></span>

<span data-ttu-id="46e76-140">_&quot;針對 Linux 虛擬機器，檔案一致的備份是可行的因為 Linux 沒有對等平台 tooVSS。&quot;_</span><span class="sxs-lookup"><span data-stu-id="46e76-140">_&quot;For Linux virtual machines, only file-consistent backups are possible, since Linux does not have an equivalent platform tooVSS.&quot;_</span></span>

<span data-ttu-id="46e76-141">_&quot;應用程式需要 tooimplement 自己&quot;v-table 修正&quot;機制 hello 上的還原資料。&quot;_</span><span class="sxs-lookup"><span data-stu-id="46e76-141">_&quot;Applications need tooimplement their own &quot;fix-up&quot; mechanism on hello restored data.&quot;_</span></span>

<span data-ttu-id="46e76-142">因此，一個具有 toomake 確定 hello 備份啟動時，SAP HANA 是一致的狀態，在磁碟上。</span><span class="sxs-lookup"><span data-stu-id="46e76-142">Therefore, one has toomake sure SAP HANA is in a consistent state on disk when hello backup starts.</span></span> <span data-ttu-id="46e76-143">請參閱_SAP HANA 快照_hello 文件稍早所述。</span><span class="sxs-lookup"><span data-stu-id="46e76-143">See _SAP HANA snapshots_ described earlier in hello document.</span></span> <span data-ttu-id="46e76-144">但是當 SAP HANA 保持在此快照集準備模式中時，還有潛在的問題。</span><span class="sxs-lookup"><span data-stu-id="46e76-144">But there is a potential issue when SAP HANA stays in this snapshot preparation mode.</span></span> <span data-ttu-id="46e76-145">如需詳細資訊，請參閱[建立儲存體快照集 (SAP HANA Studio)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/a0/3f8f08501e44d89115db3c5aa08e3f/content.htm)。</span><span class="sxs-lookup"><span data-stu-id="46e76-145">See [Create a Storage Snapshot (SAP HANA Studio)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/a0/3f8f08501e44d89115db3c5aa08e3f/content.htm) for more information.</span></span>

<span data-ttu-id="46e76-146">這篇文章中提到︰</span><span class="sxs-lookup"><span data-stu-id="46e76-146">That article states:</span></span>

<span data-ttu-id="46e76-147">_&quot;強烈建議 tooconfirm 或已在建立之後儘速放棄儲存體的快照集。正在準備 hello 儲存快照集，或建立，hello 時遭到凍結時快照集相關的資料。在 hello 快照集相關的資料仍已凍結，仍可以進行變更 hello 資料庫中。這類變更不會凍結變更的快照集相關的資料 toobe hello。相反地，hello 變更寫入 toopositions hello 分開 hello 儲存快照集的資料區域中。變更也會寫入 toohello 記錄檔。不過，hello 長 hello 快照相關資料會保留已凍結，hello 多個資料磁碟區可以成長的 hello。&quot;_</span><span class="sxs-lookup"><span data-stu-id="46e76-147">_&quot;It is strongly recommended tooconfirm or abandon a storage snapshot as soon as possible after it has been created. While hello storage snapshot is being prepared or created, hello snapshot-relevant data is frozen. While hello snapshot-relevant data remains frozen, changes can still be made in hello database. Such changes will not cause hello frozen snapshot-relevant data toobe changed. Instead, hello changes are written toopositions in hello data area that are separate from hello storage snapshot. Changes are also written toohello log. However, hello longer hello snapshot-relevant data is kept frozen, hello more hello data volume can grow.&quot;_</span></span>

<span data-ttu-id="46e76-148">Azure 備份會負責 hello 檔案系統一致性，透過 Azure VM 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="46e76-148">Azure Backup takes care of hello file system consistency via Azure VM extensions.</span></span> <span data-ttu-id="46e76-149">這些擴充功能沒有獨立版本，只能結合 Azure 備份服務使用。</span><span class="sxs-lookup"><span data-stu-id="46e76-149">These extensions are not available standalone, and work only in combination with Azure Backup service.</span></span> <span data-ttu-id="46e76-150">不過，它仍然是需求 toomanage SAP HANA 快照 tooguarantee 應用程式一致性。</span><span class="sxs-lookup"><span data-stu-id="46e76-150">Nevertheless, it is still a requirement toomanage an SAP HANA snapshot tooguarantee app consistency.</span></span>

<span data-ttu-id="46e76-151">Azure 備份有兩個主要階段︰</span><span class="sxs-lookup"><span data-stu-id="46e76-151">Azure Backup has two major phases:</span></span>

- <span data-ttu-id="46e76-152">建立快照集</span><span class="sxs-lookup"><span data-stu-id="46e76-152">Take Snapshot</span></span>
- <span data-ttu-id="46e76-153">傳送資料 toovault</span><span class="sxs-lookup"><span data-stu-id="46e76-153">Transfer data toovault</span></span>

<span data-ttu-id="46e76-154">一旦完成 hello Azure 備份服務階段的快照，所以無法確認 hello SAP HANA 快照集。</span><span class="sxs-lookup"><span data-stu-id="46e76-154">So one could confirm hello SAP HANA snapshot once hello Azure Backup service phase of taking a snapshot is completed.</span></span> <span data-ttu-id="46e76-155">可能需要幾分鐘的時間 toosee hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="46e76-155">It might take several minutes toosee in hello Azure portal.</span></span>

![此圖將顯示在 Azure 備份服務的 hello 備份工作清單的一部分](media/sap-hana-backup-storage-snapshots/image014.png)

<span data-ttu-id="46e76-157">此圖顯示 hello Azure Backup 服務，這是使用的 tooback hello HANA 測試 VM 的備份工作清單的一部分。</span><span class="sxs-lookup"><span data-stu-id="46e76-157">This figure shows part of hello backup job list of an Azure Backup service, which was used tooback up hello HANA test VM.</span></span>

![tooshow hello 工作詳細資料，按一下 hello hello Azure 入口網站中的備份工作](media/sap-hana-backup-storage-snapshots/image015.png)

<span data-ttu-id="46e76-159">tooshow hello 工作詳細資料，按一下 hello hello Azure 入口網站中的備份作業。</span><span class="sxs-lookup"><span data-stu-id="46e76-159">tooshow hello job details, click hello backup job in hello Azure portal.</span></span> <span data-ttu-id="46e76-160">在這裡，其中一個可以看到 hello 兩個階段。</span><span class="sxs-lookup"><span data-stu-id="46e76-160">Here, one can see hello two phases.</span></span> <span data-ttu-id="46e76-161">可能需要幾分鐘的時間之前為已完成，它會顯示 hello 快照集 」 階段。</span><span class="sxs-lookup"><span data-stu-id="46e76-161">It might take a few minutes until it shows hello snapshot phase as completed.</span></span> <span data-ttu-id="46e76-162">大部分的 hello 時間花在 hello 資料傳輸的階段。</span><span class="sxs-lookup"><span data-stu-id="46e76-162">Most of hello time is spent in hello data transfer phase.</span></span>

## <a name="hana-vm-backup-automation-via-azure-backup-service"></a><span data-ttu-id="46e76-163">透過 Azure 備份服務進行 HANA VM 自動備份</span><span class="sxs-lookup"><span data-stu-id="46e76-163">HANA VM backup automation via Azure Backup service</span></span>

<span data-ttu-id="46e76-164">一旦完成 hello Azure Backup 的快照集階段，如稍早所述但很有幫助 tooconsider 自動化，因為系統管理員可能無法監視 hello hello Azure 入口網站中的備份工作清單，其中一個無法手動確認 hello SAP HANA 快照集。</span><span class="sxs-lookup"><span data-stu-id="46e76-164">One could manually confirm hello SAP HANA snapshot once hello Azure Backup snapshot phase is completed, as described earlier, but it is helpful tooconsider automation because an admin might not monitor hello backup job list in hello Azure portal.</span></span>

<span data-ttu-id="46e76-165">以下說明如何透過 Azure PowerShell Cmdlet 達成。</span><span class="sxs-lookup"><span data-stu-id="46e76-165">Here is an explanation how it could be accomplished via Azure PowerShell cmdlets.</span></span>

![建立 hello 名稱 hana backup vault 的 Azure 備份服務](media/sap-hana-backup-storage-snapshots/image016.png)

<span data-ttu-id="46e76-167">Azure Backup 服務建立 hello 名稱&quot;hana-備份-保存庫。&quot; hello PS 命令**Get AzureRmRecoveryServicesVault-命名 hana 備份保存庫**擷取 hello 對應的物件。</span><span class="sxs-lookup"><span data-stu-id="46e76-167">An Azure Backup service was created with hello name &quot;hana-backup-vault.&quot; hello PS command **Get-AzureRmRecoveryServicesVault -Name hana-backup-vault** retrieves hello corresponding object.</span></span> <span data-ttu-id="46e76-168">這是物件然後 hello 下圖所示，使用的 tooset hello 備份內容。</span><span class="sxs-lookup"><span data-stu-id="46e76-168">This object is then used tooset hello backup context as seen on hello next figure.</span></span>

![Hello 備份工作正在進行中的使用者可以檢查](media/sap-hana-backup-storage-snapshots/image017.png)

<span data-ttu-id="46e76-170">之後設定 hello 正確內容中，一個可檢查 hello 備份工作目前正在進行，然後尋找其工作詳細資料。</span><span class="sxs-lookup"><span data-stu-id="46e76-170">After setting hello correct context, one can check for hello backup job currently in progress, and then look for its job details.</span></span> <span data-ttu-id="46e76-171">hello 項子工作清單顯示是否 hello 快照 hello Azure 備份的工作階段已完成：</span><span class="sxs-lookup"><span data-stu-id="46e76-171">hello subtask list shows if hello snapshot phase of hello Azure backup job is already completed:</span></span>

```
$ars = Get-AzureRmRecoveryServicesVault -Name hana-backup-vault
Set-AzureRmRecoveryServicesVaultContext -Vault $ars
$jid = Get-AzureRmRecoveryServicesBackupJob -Status InProgress | select -ExpandProperty jobid
Get-AzureRmRecoveryServicesBackupJobDetails -Jobid $jid | select -ExpandProperty subtasks
```

![在迴圈直到結果 tooCompleted 輪詢 hello 值](media/sap-hana-backup-storage-snapshots/image018.png)

<span data-ttu-id="46e76-173">一旦 hello 工作詳細資料儲存在變數中，它是只需 PS 語法 tooget toohello 第一個陣列的項目，並擷取 hello 狀態值。</span><span class="sxs-lookup"><span data-stu-id="46e76-173">Once hello job details are stored in a variable, it is simply PS syntax tooget toohello first array entry and retrieve hello status value.</span></span> <span data-ttu-id="46e76-174">toocomplete hello 自動化指令碼，直到迴圈中的輪詢 hello 值會太&quot;已完成。&quot;</span><span class="sxs-lookup"><span data-stu-id="46e76-174">toocomplete hello automation script, poll hello value in a loop until it turns too&quot;Completed.&quot;</span></span>

```
$st = Get-AzureRmRecoveryServicesBackupJobDetails -Jobid $jid | select -ExpandProperty subtasks
$st[0] | select -ExpandProperty status
```

## <a name="hana-license-key-and-vm-restore-via-azure-backup-service"></a><span data-ttu-id="46e76-175">透過 Azure 備份服務的 HANA 授權金鑰和 VM 還原</span><span class="sxs-lookup"><span data-stu-id="46e76-175">HANA license key and VM restore via Azure Backup service</span></span>

<span data-ttu-id="46e76-176">hello Azure 備份服務是設計的 toocreate 新的 VM 進行還原。</span><span class="sxs-lookup"><span data-stu-id="46e76-176">hello Azure Backup service is designed toocreate a new VM during restore.</span></span> <span data-ttu-id="46e76-177">沒有計畫就在此時 toodo&quot;就地&quot;還原現有的 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="46e76-177">There is no plan right now toodo an &quot;in-place&quot; restore of an existing Azure VM.</span></span>

![此圖將顯示 hello Azure 入口網站中的 hello Azure 服務的 hello 還原選項](media/sap-hana-backup-storage-snapshots/image019.png)

<span data-ttu-id="46e76-179">此圖會顯示 hello Azure 入口網站中的 hello Azure 服務的 hello 還原選項。</span><span class="sxs-lookup"><span data-stu-id="46e76-179">This figure shows hello restore option of hello Azure service in hello Azure portal.</span></span> <span data-ttu-id="46e76-180">其中一個可以選擇在還原期間建立的 VM，或還原 hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="46e76-180">One can choose between creating a VM during restore or restoring hello disks.</span></span> <span data-ttu-id="46e76-181">還原 hello 磁碟，之後仍然需要有 toocreate 其最上層的新 VM。</span><span class="sxs-lookup"><span data-stu-id="46e76-181">After restoring hello disks, it is still necessary toocreate a new VM on top of it.</span></span> <span data-ttu-id="46e76-182">每當建立新的 VM 取得 Azure 的 hello 唯一 VM 識別碼變更 (請參閱[存取和使用 Azure VM 的唯一識別碼](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/))。</span><span class="sxs-lookup"><span data-stu-id="46e76-182">Whenever a new VM gets created on Azure hello unique VM ID changes (see [Accessing and Using Azure VM Unique ID](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/)).</span></span>

![此圖將顯示 hello Azure VM 的唯一識別碼之前和之後透過 Azure 備份服務的 hello 還原](media/sap-hana-backup-storage-snapshots/image020.png)

<span data-ttu-id="46e76-184">透過 Azure 備份服務的 hello 還原前後，此圖會顯示 hello Azure VM 的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="46e76-184">This figure shows hello Azure VM unique ID before and after hello restore via Azure Backup service.</span></span> <span data-ttu-id="46e76-185">hello SAP 硬體，該金鑰用於 SAP 的授權，使用此唯一 VM 識別碼。</span><span class="sxs-lookup"><span data-stu-id="46e76-185">hello SAP hardware key, which is used for SAP licensing, is using this unique VM ID.</span></span> <span data-ttu-id="46e76-186">因此，新的 SAP 授權有 toobe VM 還原之後才安裝。</span><span class="sxs-lookup"><span data-stu-id="46e76-186">As a consequence, a new SAP license has toobe installed after a VM restore.</span></span>

<span data-ttu-id="46e76-187">期間 hello 建立這個備份指南在預覽模式中輸入新的 Azure 備份功能。</span><span class="sxs-lookup"><span data-stu-id="46e76-187">A new Azure Backup feature was presented in preview mode during hello creation of this backup guide.</span></span> <span data-ttu-id="46e76-188">它可讓檔案層級還原，根據拍攝 hello VM 備份的 hello VM 快照集。</span><span class="sxs-lookup"><span data-stu-id="46e76-188">It allows a file level restore based on hello VM snapshot that was taken for hello VM backup.</span></span> <span data-ttu-id="46e76-189">這可避免 hello 需要 toodeploy 新的 VM，因此唯一 VM 識別碼會保留 hello hello 相同，而且無須任何新的 SAP HANA 授權金鑰。</span><span class="sxs-lookup"><span data-stu-id="46e76-189">This avoids hello need toodeploy a new VM, and therefore hello unique VM ID stays hello same and no new SAP HANA license key is required.</span></span> <span data-ttu-id="46e76-190">有關這項功能的詳細文件，將會在經過完整測試之後提供。</span><span class="sxs-lookup"><span data-stu-id="46e76-190">More documentation on this feature will be provided after it is fully tested.</span></span>

<span data-ttu-id="46e76-191">Azure 備份將最終允許備份的個別 Azure 的虛擬磁碟，加上檔案及目錄內 hello VM。</span><span class="sxs-lookup"><span data-stu-id="46e76-191">Azure Backup will eventually allow backup of individual Azure virtual disks, plus files and directories from inside hello VM.</span></span> <span data-ttu-id="46e76-192">Azure 備份的主要優點是其所有 hello 備份，毋需 toodo 儲存 hello 客戶的管理它。</span><span class="sxs-lookup"><span data-stu-id="46e76-192">A major advantage of Azure Backup is its management of all hello backups, saving hello customer from having toodo it.</span></span> <span data-ttu-id="46e76-193">如果還原有必要，Azure 備份將會選取 hello 正確備份 toouse。</span><span class="sxs-lookup"><span data-stu-id="46e76-193">If a restore becomes necessary, Azure Backup will select hello correct backup toouse.</span></span>

## <a name="sap-hana-vm-backup-via-manual-disk-snapshot"></a><span data-ttu-id="46e76-194">透過手動磁碟快照集進行 SAP HANA VM 備份</span><span class="sxs-lookup"><span data-stu-id="46e76-194">SAP HANA VM backup via manual disk snapshot</span></span>

<span data-ttu-id="46e76-195">而不是使用 hello Azure Backup 服務，其中一個可以設定個別的備份解決方案，藉由建立的手動透過 PowerShell 的 Azure Vhd blob 快照集。</span><span class="sxs-lookup"><span data-stu-id="46e76-195">Instead of using hello Azure Backup service, one could configure an individual backup solution by creating blob snapshots of Azure VHDs manually via PowerShell.</span></span> <span data-ttu-id="46e76-196">請參閱[使用 blob 快照集，使用 PowerShell](https://blogs.msdn.microsoft.com/cie/2016/05/17/using-blob-snapshots-with-powershell/) hello 步驟的說明。</span><span class="sxs-lookup"><span data-stu-id="46e76-196">See [Using blob snapshots with PowerShell](https://blogs.msdn.microsoft.com/cie/2016/05/17/using-blob-snapshots-with-powershell/) for a description of hello steps.</span></span>

<span data-ttu-id="46e76-197">它提供更大的彈性，但無法解析 hello 本文件稍早所述的問題：</span><span class="sxs-lookup"><span data-stu-id="46e76-197">It provides more flexibility but does not resolve hello issues explained earlier in this document:</span></span>

- <span data-ttu-id="46e76-198">您仍然必須確定 SAP HANA 處於一致的狀態</span><span class="sxs-lookup"><span data-stu-id="46e76-198">One still must make sure that SAP HANA is in a consistent state</span></span>
- <span data-ttu-id="46e76-199">無法覆寫 hello 作業系統磁碟，即使有的 hello VM 解除配置的錯誤訊息因為租用。</span><span class="sxs-lookup"><span data-stu-id="46e76-199">hello OS disk cannot be overwritten even if hello VM is deallocated because of an error stating that a lease exists.</span></span> <span data-ttu-id="46e76-200">僅適用於之後刪除 hello VM，而這樣會導致 tooa 新唯一 VM 識別碼和 hello 需要 tooinstall 新的 SAP 授權。</span><span class="sxs-lookup"><span data-stu-id="46e76-200">It only works after deleting hello VM, which would lead tooa new unique VM ID and hello need tooinstall a new SAP license.</span></span>

![它是可能 toorestore 只有 hello 資料磁碟的 Azure VM](media/sap-hana-backup-storage-snapshots/image021.png)

<span data-ttu-id="46e76-202">它可能 toorestore 只有 hello 資料磁碟的 Azure VM，避免取得新的唯一 VM 識別碼 hello 問題，因此，失效 hello SAP 授權：</span><span class="sxs-lookup"><span data-stu-id="46e76-202">It is possible toorestore only hello data disks of an Azure VM, avoiding hello problem of getting a new unique VM ID and, therefore, invalidated hello SAP license:</span></span>

- <span data-ttu-id="46e76-203">Hello 測試兩個 Azure 資料磁碟已附加的 tooa VM，並在其上已定義的軟體 RAID</span><span class="sxs-lookup"><span data-stu-id="46e76-203">For hello test, two Azure data disks were attached tooa VM and software RAID was defined on top of them</span></span> 
- <span data-ttu-id="46e76-204">已經利用 SAP HANA 快照集功能確認的 SAP HANA 處於一致的狀態</span><span class="sxs-lookup"><span data-stu-id="46e76-204">It was confirmed that SAP HANA was in a consistent state by SAP HANA snapshot feature</span></span>
- <span data-ttu-id="46e76-205">檔案系統凍結 (請參閱_建立儲存體的快照集時，SAP HANA 資料一致性_hello 相關文件中[備份指南的 SAP HANA Azure 虛擬機器上](sap-hana-backup-guide.md))</span><span class="sxs-lookup"><span data-stu-id="46e76-205">File system freeze (see _SAP HANA data consistency when taking storage snapshots_ in hello related article [Backup guide for SAP HANA on Azure Virtual Machines](sap-hana-backup-guide.md))</span></span>
- <span data-ttu-id="46e76-206">從這兩個資料磁碟建立 blob 快照集</span><span class="sxs-lookup"><span data-stu-id="46e76-206">Blob snapshots were taken from both data disks</span></span>
- <span data-ttu-id="46e76-207">檔案系統解除凍結</span><span class="sxs-lookup"><span data-stu-id="46e76-207">File system unfreeze</span></span>
- <span data-ttu-id="46e76-208">確認 SAP HANA 快照集</span><span class="sxs-lookup"><span data-stu-id="46e76-208">SAP HANA snapshot confirmation</span></span>
- <span data-ttu-id="46e76-209">toorestore hello 資料磁碟，hello VM 已關閉，而這兩個磁碟中斷連結</span><span class="sxs-lookup"><span data-stu-id="46e76-209">toorestore hello data disks, hello VM was shut down and both disks detached</span></span>
- <span data-ttu-id="46e76-210">Hello 磁碟中斷連結之後才已被覆寫 hello 先前的 blob 快照集</span><span class="sxs-lookup"><span data-stu-id="46e76-210">After detaching hello disks, they were overwritten with hello former blob snapshots</span></span>
- <span data-ttu-id="46e76-211">附加 hello 還原虛擬磁碟，然後再次 toohello VM</span><span class="sxs-lookup"><span data-stu-id="46e76-211">Then hello restored virtual disks were attached again toohello VM</span></span>
- <span data-ttu-id="46e76-212">起始 hello VM hello 軟體 RAID 可以正常運作正常，而且已設定回 toohello blob 上的所有快照集時間之後</span><span class="sxs-lookup"><span data-stu-id="46e76-212">After starting hello VM, everything on hello software RAID worked fine and was set back toohello blob snapshot time</span></span>
- <span data-ttu-id="46e76-213">HANA 已設定回 toohello HANA 快照集</span><span class="sxs-lookup"><span data-stu-id="46e76-213">HANA was set back toohello HANA snapshot</span></span>

<span data-ttu-id="46e76-214">如果資料可能 tooshut 向 SAP HANA hello blob 快照集之前，會是較不複雜 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="46e76-214">If it was possible tooshut down SAP HANA before hello blob snapshots, hello procedure would be less complex.</span></span> <span data-ttu-id="46e76-215">在此情況下，其中一個無法略過 hello HANA 快照集，如果沒有其他正在進行的作業在 hello 系統中，也略過 hello 檔案系統凍結。</span><span class="sxs-lookup"><span data-stu-id="46e76-215">In that case, one could skip hello HANA snapshot and, if nothing else is going on in hello system, also skip hello file system freeze.</span></span> <span data-ttu-id="46e76-216">增加的複雜度進入 hello 圖片時，它需要 toodo 快照集的所有項目仍在線上運作。</span><span class="sxs-lookup"><span data-stu-id="46e76-216">Added complexity comes into hello picture when it is necessary toodo snapshots while everything is online.</span></span> <span data-ttu-id="46e76-217">請參閱_建立儲存體的快照集時，SAP HANA 資料一致性_hello 相關文件中[備份指南的 SAP HANA Azure 虛擬機器上](sap-hana-backup-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="46e76-217">See _SAP HANA data consistency when taking storage snapshots_ in hello related article [Backup guide for SAP HANA on Azure Virtual Machines](sap-hana-backup-guide.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="46e76-218">後續步驟</span><span class="sxs-lookup"><span data-stu-id="46e76-218">Next steps</span></span>
* <span data-ttu-id="46e76-219">[Azure 虛擬機器上 SAP HANA 的備份指南](sap-hana-backup-guide.md)提供快速入門的概觀和詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="46e76-219">[Backup guide for SAP HANA on Azure Virtual Machines](sap-hana-backup-guide.md) gives an overview and information on getting started.</span></span>
* <span data-ttu-id="46e76-220">[SAP HANA 備份為基礎的檔案層級](sap-hana-backup-file-level.md)涵蓋 hello 以檔案為基礎的備份選項。</span><span class="sxs-lookup"><span data-stu-id="46e76-220">[SAP HANA backup based on file level](sap-hana-backup-file-level.md) covers hello file-based backup option.</span></span>
* <span data-ttu-id="46e76-221">toolearn tooestablish 高可用性和 Azure （大型執行個體） 上的 SAP HANA 災害復原計劃的看到[SAP HANA （大型執行個體） 高可用性和災害復原在 Azure 上的](hana-overview-high-availability-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="46e76-221">toolearn how tooestablish high availability and plan for disaster recovery of SAP HANA on Azure (large instances), see [SAP HANA (large instances) high availability and disaster recovery on Azure](hana-overview-high-availability-disaster-recovery.md).</span></span>
