---
title: "Azure 備份伺服器 v2 aaaUse 現代的備份儲存體 |Microsoft 文件"
description: "深入了解 Azure 備份伺服器 v2 中的 hello 新功能。 本文說明如何 tooupgrade 備份伺服器安裝。"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: masaran;markgal
ms.openlocfilehash: b2a1ed27a6a682bd611fea1d2df9ef93314404e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-storage-tooazure-backup-server-v2"></a><span data-ttu-id="f05b1-104">新增儲存體 tooAzure 備份伺服器 v2</span><span class="sxs-lookup"><span data-stu-id="f05b1-104">Add storage tooAzure Backup Server v2</span></span>

<span data-ttu-id="f05b1-105">Azure 備份伺服器 v2 隨附 System Center 2016 Data Protection Manager 新式備份儲存體。</span><span class="sxs-lookup"><span data-stu-id="f05b1-105">Azure Backup Server v2 comes with System Center 2016 Data Protection Manager Modern Backup Storage.</span></span> <span data-ttu-id="f05b1-106">新式備份儲存體可節省 50% 的儲存空間、備份速度快三倍，且更具儲存效率。</span><span class="sxs-lookup"><span data-stu-id="f05b1-106">Modern Backup Storage offers storage savings of 50 percent, backups that are three times faster, and more efficient storage.</span></span> <span data-ttu-id="f05b1-107">它也提供可感知工作負載的儲存體。</span><span class="sxs-lookup"><span data-stu-id="f05b1-107">It also offers workload-aware storage.</span></span> 

> [!NOTE]
> <span data-ttu-id="f05b1-108">toouse 現代的備份儲存體，您必須在 Windows Server 2016 上執行備份伺服器 v2。</span><span class="sxs-lookup"><span data-stu-id="f05b1-108">toouse Modern Backup Storage, you must run Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="f05b1-109">如果您在舊版 Windows Server 上執行備份伺服器 v2，Azure 備份伺服器將無法利用新式備份儲存體。</span><span class="sxs-lookup"><span data-stu-id="f05b1-109">If you run Backup Server v2 on an earlier version of Windows Server, Azure Backup Server can't take advantage of Modern Backup Storage.</span></span> <span data-ttu-id="f05b1-110">相反地，它保護工作負載的方式會和備份伺服器 v1 一樣。</span><span class="sxs-lookup"><span data-stu-id="f05b1-110">Instead, it protects workloads as it does with Backup Server v1.</span></span> <span data-ttu-id="f05b1-111">如需詳細資訊，請參閱 hello 備份伺服器版本[保護矩陣](backup-mabs-protection-matrix.md)。</span><span class="sxs-lookup"><span data-stu-id="f05b1-111">For more information, see hello Backup Server version [protection matrix](backup-mabs-protection-matrix.md).</span></span>

## <a name="volumes-in-backup-server-v2"></a><span data-ttu-id="f05b1-112">備份伺服器 v2 中的磁碟區</span><span class="sxs-lookup"><span data-stu-id="f05b1-112">Volumes in Backup Server v2</span></span>

<span data-ttu-id="f05b1-113">備份伺服器 v2 接受儲存體磁碟區。</span><span class="sxs-lookup"><span data-stu-id="f05b1-113">Backup Server v2 accepts storage volumes.</span></span> <span data-ttu-id="f05b1-114">當您將磁碟區時，備份伺服器將會格式化 hello 磁碟區 tooResilient 檔案系統 (ReFS)、 現代的備份儲存體需要。</span><span class="sxs-lookup"><span data-stu-id="f05b1-114">When you add a volume, Backup Server formats hello volume tooResilient File System (ReFS), which Modern Backup Storage requires.</span></span> <span data-ttu-id="f05b1-115">tooadd 磁碟區，和 tooexpand 於稍後如果您需要我們建議您使用此工作流程：</span><span class="sxs-lookup"><span data-stu-id="f05b1-115">tooadd a volume, and tooexpand it later if you need to, we suggest that you use this workflow:</span></span>

1.  <span data-ttu-id="f05b1-116">在 VM 上設定備份伺服器 v2。</span><span class="sxs-lookup"><span data-stu-id="f05b1-116">Set up Backup Server v2 on a VM.</span></span>
2.  <span data-ttu-id="f05b1-117">在儲存集區的虛擬磁碟上建立磁碟區：</span><span class="sxs-lookup"><span data-stu-id="f05b1-117">Create a volume on a virtual disk in a storage pool:</span></span>
    1.  <span data-ttu-id="f05b1-118">新增磁碟 tooa 存放集區並將虛擬磁碟以建立簡單的版面配置。</span><span class="sxs-lookup"><span data-stu-id="f05b1-118">Add a disk tooa storage pool and create a virtual disk with simple layout.</span></span>
    2.  <span data-ttu-id="f05b1-119">新增任何額外的磁碟，並擴充 hello 虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="f05b1-119">Add any additional disks, and extend hello virtual disk.</span></span>
    3.  <span data-ttu-id="f05b1-120">Hello 虛擬磁碟上建立磁碟區。</span><span class="sxs-lookup"><span data-stu-id="f05b1-120">Create volumes on hello virtual disk.</span></span>
3.  <span data-ttu-id="f05b1-121">新增 hello 磁碟區 tooBackup 伺服器。</span><span class="sxs-lookup"><span data-stu-id="f05b1-121">Add hello volumes tooBackup Server.</span></span>
4.  <span data-ttu-id="f05b1-122">設定可感知工作負載的儲存體。</span><span class="sxs-lookup"><span data-stu-id="f05b1-122">Configure workload-aware storage.</span></span>

## <a name="create-a-volume-for-modern-backup-storage"></a><span data-ttu-id="f05b1-123">為新式備份儲存體建立磁碟區</span><span class="sxs-lookup"><span data-stu-id="f05b1-123">Create a volume for Modern Backup Storage</span></span>

<span data-ttu-id="f05b1-124">以磁碟區作為磁碟儲存體來使用備份伺服器 v2 可協助您掌控儲存體。</span><span class="sxs-lookup"><span data-stu-id="f05b1-124">Using Backup Server v2 with volumes as disk storage can help you maintain control over storage.</span></span> <span data-ttu-id="f05b1-125">磁碟區可以是單一磁碟。</span><span class="sxs-lookup"><span data-stu-id="f05b1-125">A volume can be a single disk.</span></span> <span data-ttu-id="f05b1-126">不過，如果您想在 hello tooextend 儲存體未來，建立使用儲存空間建立磁碟的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="f05b1-126">However, if you want tooextend storage in hello future, create a volume out of a disk created by using storage spaces.</span></span> <span data-ttu-id="f05b1-127">這可協助您是否 tooexpand hello 磁碟區備份存放區。</span><span class="sxs-lookup"><span data-stu-id="f05b1-127">This can help if you want tooexpand hello volume for backup storage.</span></span> <span data-ttu-id="f05b1-128">本節會提供最佳做法，讓您了解如何建立具有此設定的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="f05b1-128">This section offers best practices for creating a volume with this setup.</span></span>

1. <span data-ttu-id="f05b1-129">在 [伺服器管理員] 中，選取 [檔案和存放服務] > [磁碟區] > [儲存集區]。</span><span class="sxs-lookup"><span data-stu-id="f05b1-129">In Server Manager, select **File and Storage Services** > **Volumes** > **Storage Pools**.</span></span> <span data-ttu-id="f05b1-130">在 [實體磁碟] 底下，選取 [新增儲存集區]。</span><span class="sxs-lookup"><span data-stu-id="f05b1-130">Under **PHYSICAL DISKS**, select **New Storage Pool**.</span></span> 

    ![建立新的儲存集區](./media/backup-mabs-add-storage/mabs-add-storage-1.png)

2. <span data-ttu-id="f05b1-132">在 hello**工作**下拉式清單方塊中，選取**新虛擬磁碟**。</span><span class="sxs-lookup"><span data-stu-id="f05b1-132">In hello **TASKS** drop-down box, select **New Virtual Disk**.</span></span>

    ![新增虛擬磁碟](./media/backup-mabs-add-storage/mabs-add-storage-2.png)

3. <span data-ttu-id="f05b1-134">選取 hello 儲存集區，然後再選取**新增實體磁碟**。</span><span class="sxs-lookup"><span data-stu-id="f05b1-134">Select hello storage pool, and then select **Add Physical Disk**.</span></span>

    ![新增實體磁碟](./media/backup-mabs-add-storage/mabs-add-storage-3.png)

4. <span data-ttu-id="f05b1-136">選取 hello 實體磁碟，然後選取**擴充虛擬磁碟**。</span><span class="sxs-lookup"><span data-stu-id="f05b1-136">Select hello physical disk, and then select **Extend Virtual Disk**.</span></span>

    ![擴充 hello 虛擬磁碟](./media/backup-mabs-add-storage/mabs-add-storage-4.png)

5. <span data-ttu-id="f05b1-138">選取 hello 虛擬磁碟，然後選取**新的磁碟區**。</span><span class="sxs-lookup"><span data-stu-id="f05b1-138">Select hello virtual disk, and then select **New Volume**.</span></span>

    ![建立新的磁碟區](./media/backup-mabs-add-storage/mabs-add-storage-5.png)

6. <span data-ttu-id="f05b1-140">在 hello**選取 hello 伺服器和磁碟**對話方塊中，選取 hello 伺服器和 hello 新磁碟。</span><span class="sxs-lookup"><span data-stu-id="f05b1-140">In hello **Select hello server and disk** dialog, select hello server and hello new disk.</span></span> <span data-ttu-id="f05b1-141">然後，選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="f05b1-141">Then, select **Next**.</span></span>

    ![選取 hello 伺服器和磁碟](./media/backup-mabs-add-storage/mabs-add-storage-6.png)

## <a name="add-volumes-toobackup-server-disk-storage"></a><span data-ttu-id="f05b1-143">新增磁碟區 tooBackup 伺服器磁碟儲存體</span><span class="sxs-lookup"><span data-stu-id="f05b1-143">Add volumes tooBackup Server disk storage</span></span>

<span data-ttu-id="f05b1-144">tooadd hello 中的磁碟區 tooBackup 伺服器**管理** 窗格中，掃描 hello 存放裝置，然後選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="f05b1-144">tooadd a volume tooBackup Server, in hello **Management** pane, rescan hello storage, and then select **Add**.</span></span> <span data-ttu-id="f05b1-145">所有 hello 磁碟區可用 toobe 加入備份伺服器存放裝置的清單隨即出現。</span><span class="sxs-lookup"><span data-stu-id="f05b1-145">A list of all hello volumes available toobe added for Backup Server Storage appears.</span></span> <span data-ttu-id="f05b1-146">可用的磁碟區加入選取的磁碟區 toohello 清單之後，您可以讓您管理這些易記名稱 toohelp。</span><span class="sxs-lookup"><span data-stu-id="f05b1-146">After available volumes are added toohello list of selected volumes, you can give them a friendly name toohelp you manage them.</span></span> <span data-ttu-id="f05b1-147">這些磁碟區 tooReFS，因此備份伺服器可以使用現代的備份儲存體的 hello 優點選取的 tooformat**確定**。</span><span class="sxs-lookup"><span data-stu-id="f05b1-147">tooformat these volumes tooReFS so Backup Server can use hello benefits of Modern Backup Storage, select **OK**.</span></span>

![新增可用的磁碟區](./media/backup-mabs-add-storage/mabs-add-storage-7.png)

## <a name="set-up-workload-aware-storage"></a><span data-ttu-id="f05b1-149">設定可感知工作負載的儲存體</span><span class="sxs-lookup"><span data-stu-id="f05b1-149">Set up workload-aware storage</span></span>

<span data-ttu-id="f05b1-150">使用可感知工作負載的儲存體，您可以選取 hello 儲存磁碟區的優先特定種類的工作負載。</span><span class="sxs-lookup"><span data-stu-id="f05b1-150">With workload-aware storage, you can select hello volumes that preferentially store certain kinds of workloads.</span></span> <span data-ttu-id="f05b1-151">例如，您可以設定昂貴支援大量輸入/輸出作業每個第二個 (IOPS) toostore hello 工作負載，需要大量的頻繁備份的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="f05b1-151">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) toostore only hello workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="f05b1-152">舉例來說，具有交易記錄的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="f05b1-152">An example is SQL Server with transaction logs.</span></span> <span data-ttu-id="f05b1-153">備份頻率，像是 Vm，其他工作負載可以備份 toolow 成本磁碟區。</span><span class="sxs-lookup"><span data-stu-id="f05b1-153">Other workloads that are backed up less frequently, like VMs, can be backed up toolow-cost volumes.</span></span>

### <a name="update-dpmdiskstorage"></a><span data-ttu-id="f05b1-154">Update-DPMDiskStorage</span><span class="sxs-lookup"><span data-stu-id="f05b1-154">Update-DPMDiskStorage</span></span>

<span data-ttu-id="f05b1-155">您可以設定工作負載感知儲存區，使用 hello PowerShell 指令程式更新-DPMDiskStorage，就會更新 hello hello Data Protection Manager 伺服器上的存放集區中的磁碟區的屬性。</span><span class="sxs-lookup"><span data-stu-id="f05b1-155">You can set up workload-aware storage by using hello PowerShell cmdlet Update-DPMDiskStorage, which updates hello properties of a volume in hello storage pool on a Data Protection Manager server.</span></span>

<span data-ttu-id="f05b1-156">語法：</span><span class="sxs-lookup"><span data-stu-id="f05b1-156">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```
<span data-ttu-id="f05b1-157">hello 下列螢幕擷取畫面顯示 hello 更新 DPMDiskStorage cmdlet hello PowerShell 視窗中。</span><span class="sxs-lookup"><span data-stu-id="f05b1-157">hello following screenshot shows hello Update-DPMDiskStorage cmdlet in hello PowerShell window.</span></span>

![hello hello PowerShell 視窗中的更新 DPMDiskStorage 命令](./media/backup-mabs-add-storage/mabs-add-storage-8.png)

<span data-ttu-id="f05b1-159">使用 PowerShell 的 hello 變更會反映在 hello 備份伺服器系統管理員主控台。</span><span class="sxs-lookup"><span data-stu-id="f05b1-159">hello changes you make by using PowerShell are reflected in hello Backup Server Administrator Console.</span></span>

![磁碟與 hello 系統管理員主控台中的磁碟區](./media/backup-mabs-add-storage/mabs-add-storage-9.png)

## <a name="next-steps"></a><span data-ttu-id="f05b1-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f05b1-161">Next steps</span></span>
<span data-ttu-id="f05b1-162">安裝備份伺服器之後，了解如何 tooprepare 您的伺服器，或開始進行保護工作負載。</span><span class="sxs-lookup"><span data-stu-id="f05b1-162">After you install Backup Server, learn how tooprepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="f05b1-163">準備備份伺服器工作負載</span><span class="sxs-lookup"><span data-stu-id="f05b1-163">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="f05b1-164">使用 VMware 伺服器的備份伺服器 tooback</span><span class="sxs-lookup"><span data-stu-id="f05b1-164">Use Backup Server tooback up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="f05b1-165">使用 SQL server 備份伺服器 tooback</span><span class="sxs-lookup"><span data-stu-id="f05b1-165">Use Backup Server tooback up SQL Server</span></span>](backup-azure-sql-mabs.md)

