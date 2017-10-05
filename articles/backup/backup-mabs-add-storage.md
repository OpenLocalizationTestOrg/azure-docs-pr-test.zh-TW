---
title: "在 Azure 備份伺服器 v2 中使用新式備份儲存體 | Microsoft Docs"
description: "了解 Azure 備份伺服器 v2 中的新功能。 本文說明如何升級您的備份伺服器安裝。"
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
ms.openlocfilehash: 751b9b495fd368dff1f72429707f5f33a0ccb569
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="add-storage-to-azure-backup-server-v2"></a><span data-ttu-id="9faa1-104">在 Azure 備份伺服器 v2 中新增儲存體</span><span class="sxs-lookup"><span data-stu-id="9faa1-104">Add storage to Azure Backup Server v2</span></span>

<span data-ttu-id="9faa1-105">Azure 備份伺服器 v2 隨附 System Center 2016 Data Protection Manager 新式備份儲存體。</span><span class="sxs-lookup"><span data-stu-id="9faa1-105">Azure Backup Server v2 comes with System Center 2016 Data Protection Manager Modern Backup Storage.</span></span> <span data-ttu-id="9faa1-106">新式備份儲存體可節省 50% 的儲存空間、備份速度快三倍，且更具儲存效率。</span><span class="sxs-lookup"><span data-stu-id="9faa1-106">Modern Backup Storage offers storage savings of 50 percent, backups that are three times faster, and more efficient storage.</span></span> <span data-ttu-id="9faa1-107">它也提供可感知工作負載的儲存體。</span><span class="sxs-lookup"><span data-stu-id="9faa1-107">It also offers workload-aware storage.</span></span> 

> [!NOTE]
> <span data-ttu-id="9faa1-108">若要使用新式備份儲存體，您必須在 Windows Server 2016 上執行備份伺服器 v2。</span><span class="sxs-lookup"><span data-stu-id="9faa1-108">To use Modern Backup Storage, you must run Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="9faa1-109">如果您在舊版 Windows Server 上執行備份伺服器 v2，Azure 備份伺服器將無法利用新式備份儲存體。</span><span class="sxs-lookup"><span data-stu-id="9faa1-109">If you run Backup Server v2 on an earlier version of Windows Server, Azure Backup Server can't take advantage of Modern Backup Storage.</span></span> <span data-ttu-id="9faa1-110">相反地，它保護工作負載的方式會和備份伺服器 v1 一樣。</span><span class="sxs-lookup"><span data-stu-id="9faa1-110">Instead, it protects workloads as it does with Backup Server v1.</span></span> <span data-ttu-id="9faa1-111">如需詳細資訊，請參閱備份伺服器版本[保護對照表](backup-mabs-protection-matrix.md)。</span><span class="sxs-lookup"><span data-stu-id="9faa1-111">For more information, see the Backup Server version [protection matrix](backup-mabs-protection-matrix.md).</span></span>

## <a name="volumes-in-backup-server-v2"></a><span data-ttu-id="9faa1-112">備份伺服器 v2 中的磁碟區</span><span class="sxs-lookup"><span data-stu-id="9faa1-112">Volumes in Backup Server v2</span></span>

<span data-ttu-id="9faa1-113">備份伺服器 v2 接受儲存體磁碟區。</span><span class="sxs-lookup"><span data-stu-id="9faa1-113">Backup Server v2 accepts storage volumes.</span></span> <span data-ttu-id="9faa1-114">當您新增磁碟區時，備份伺服器會將磁碟區格式化為新式備份儲存體所需要的復原檔案系統 (ReFS)。</span><span class="sxs-lookup"><span data-stu-id="9faa1-114">When you add a volume, Backup Server formats the volume to Resilient File System (ReFS), which Modern Backup Storage requires.</span></span> <span data-ttu-id="9faa1-115">若要新增磁碟區，並於稍後需要時加以擴充，建議您使用此工作流程：</span><span class="sxs-lookup"><span data-stu-id="9faa1-115">To add a volume, and to expand it later if you need to, we suggest that you use this workflow:</span></span>

1.  <span data-ttu-id="9faa1-116">在 VM 上設定備份伺服器 v2。</span><span class="sxs-lookup"><span data-stu-id="9faa1-116">Set up Backup Server v2 on a VM.</span></span>
2.  <span data-ttu-id="9faa1-117">在儲存集區的虛擬磁碟上建立磁碟區：</span><span class="sxs-lookup"><span data-stu-id="9faa1-117">Create a volume on a virtual disk in a storage pool:</span></span>
    1.  <span data-ttu-id="9faa1-118">在儲存集區中新增磁碟，並建立簡單配置的虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="9faa1-118">Add a disk to a storage pool and create a virtual disk with simple layout.</span></span>
    2.  <span data-ttu-id="9faa1-119">新增其他磁碟，並擴充虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="9faa1-119">Add any additional disks, and extend the virtual disk.</span></span>
    3.  <span data-ttu-id="9faa1-120">在虛擬磁碟上建立磁碟區。</span><span class="sxs-lookup"><span data-stu-id="9faa1-120">Create volumes on the virtual disk.</span></span>
3.  <span data-ttu-id="9faa1-121">在備份伺服器中新增磁碟區。</span><span class="sxs-lookup"><span data-stu-id="9faa1-121">Add the volumes to Backup Server.</span></span>
4.  <span data-ttu-id="9faa1-122">設定可感知工作負載的儲存體。</span><span class="sxs-lookup"><span data-stu-id="9faa1-122">Configure workload-aware storage.</span></span>

## <a name="create-a-volume-for-modern-backup-storage"></a><span data-ttu-id="9faa1-123">為新式備份儲存體建立磁碟區</span><span class="sxs-lookup"><span data-stu-id="9faa1-123">Create a volume for Modern Backup Storage</span></span>

<span data-ttu-id="9faa1-124">以磁碟區作為磁碟儲存體來使用備份伺服器 v2 可協助您掌控儲存體。</span><span class="sxs-lookup"><span data-stu-id="9faa1-124">Using Backup Server v2 with volumes as disk storage can help you maintain control over storage.</span></span> <span data-ttu-id="9faa1-125">磁碟區可以是單一磁碟。</span><span class="sxs-lookup"><span data-stu-id="9faa1-125">A volume can be a single disk.</span></span> <span data-ttu-id="9faa1-126">不過，如果您日後想要擴充儲存體，請從使用儲存體空間所建立的磁碟中建立磁碟區。</span><span class="sxs-lookup"><span data-stu-id="9faa1-126">However, if you want to extend storage in the future, create a volume out of a disk created by using storage spaces.</span></span> <span data-ttu-id="9faa1-127">如果您想要擴充磁碟區以供儲存備份，這麼做會有所幫助。</span><span class="sxs-lookup"><span data-stu-id="9faa1-127">This can help if you want to expand the volume for backup storage.</span></span> <span data-ttu-id="9faa1-128">本節會提供最佳做法，讓您了解如何建立具有此設定的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="9faa1-128">This section offers best practices for creating a volume with this setup.</span></span>

1. <span data-ttu-id="9faa1-129">在 [伺服器管理員] 中，選取 [檔案和存放服務] > [磁碟區] > [儲存集區]。</span><span class="sxs-lookup"><span data-stu-id="9faa1-129">In Server Manager, select **File and Storage Services** > **Volumes** > **Storage Pools**.</span></span> <span data-ttu-id="9faa1-130">在 [實體磁碟] 底下，選取 [新增儲存集區]。</span><span class="sxs-lookup"><span data-stu-id="9faa1-130">Under **PHYSICAL DISKS**, select **New Storage Pool**.</span></span> 

    ![建立新的儲存集區](./media/backup-mabs-add-storage/mabs-add-storage-1.png)

2. <span data-ttu-id="9faa1-132">在 [工作] 下拉式方塊中，選取 [新增虛擬磁碟]。</span><span class="sxs-lookup"><span data-stu-id="9faa1-132">In the **TASKS** drop-down box, select **New Virtual Disk**.</span></span>

    ![新增虛擬磁碟](./media/backup-mabs-add-storage/mabs-add-storage-2.png)

3. <span data-ttu-id="9faa1-134">選取儲存集區，然後選取 [新增實體磁碟]。</span><span class="sxs-lookup"><span data-stu-id="9faa1-134">Select the storage pool, and then select **Add Physical Disk**.</span></span>

    ![新增實體磁碟](./media/backup-mabs-add-storage/mabs-add-storage-3.png)

4. <span data-ttu-id="9faa1-136">選取實體磁碟，然後選取 [擴充虛擬磁碟]。</span><span class="sxs-lookup"><span data-stu-id="9faa1-136">Select the physical disk, and then select **Extend Virtual Disk**.</span></span>

    ![擴充虛擬磁碟](./media/backup-mabs-add-storage/mabs-add-storage-4.png)

5. <span data-ttu-id="9faa1-138">選取虛擬磁碟，然後選取 [新增磁碟區]。</span><span class="sxs-lookup"><span data-stu-id="9faa1-138">Select the virtual disk, and then select **New Volume**.</span></span>

    ![建立新的磁碟區](./media/backup-mabs-add-storage/mabs-add-storage-5.png)

6. <span data-ttu-id="9faa1-140">在 [選取伺服器和磁碟] 對話方塊中，選取伺服器和新的磁碟。</span><span class="sxs-lookup"><span data-stu-id="9faa1-140">In the **Select the server and disk** dialog, select the server and the new disk.</span></span> <span data-ttu-id="9faa1-141">然後，選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="9faa1-141">Then, select **Next**.</span></span>

    ![選取伺服器和磁碟](./media/backup-mabs-add-storage/mabs-add-storage-6.png)

## <a name="add-volumes-to-backup-server-disk-storage"></a><span data-ttu-id="9faa1-143">在備份伺服器磁碟儲存體中新增磁碟區</span><span class="sxs-lookup"><span data-stu-id="9faa1-143">Add volumes to Backup Server disk storage</span></span>

<span data-ttu-id="9faa1-144">若要在備份伺服器中新增磁碟區，請於 [管理] 窗格重新掃描儲存體，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="9faa1-144">To add a volume to Backup Server, in the **Management** pane, rescan the storage, and then select **Add**.</span></span> <span data-ttu-id="9faa1-145">隨即會出現可供為備份伺服器儲存體新增的所有磁碟區清單。</span><span class="sxs-lookup"><span data-stu-id="9faa1-145">A list of all the volumes available to be added for Backup Server Storage appears.</span></span> <span data-ttu-id="9faa1-146">在可用的磁碟區新增到已選取的磁碟區清單後，您可以為他們提供易記名稱，以方便您管理這些磁碟區。</span><span class="sxs-lookup"><span data-stu-id="9faa1-146">After available volumes are added to the list of selected volumes, you can give them a friendly name to help you manage them.</span></span> <span data-ttu-id="9faa1-147">若要將這些磁碟區格式化為 ReFS，讓備份伺服器可以利用新式備份儲存體的好處，請選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="9faa1-147">To format these volumes to ReFS so Backup Server can use the benefits of Modern Backup Storage, select **OK**.</span></span>

![新增可用的磁碟區](./media/backup-mabs-add-storage/mabs-add-storage-7.png)

## <a name="set-up-workload-aware-storage"></a><span data-ttu-id="9faa1-149">設定可感知工作負載的儲存體</span><span class="sxs-lookup"><span data-stu-id="9faa1-149">Set up workload-aware storage</span></span>

<span data-ttu-id="9faa1-150">在可感知工作負載的儲存體中，您可以選取會優先儲存某些工作負載類型的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="9faa1-150">With workload-aware storage, you can select the volumes that preferentially store certain kinds of workloads.</span></span> <span data-ttu-id="9faa1-151">例如，您可以將支援大量每秒輸入/輸出作業 (IOPS) 的高度耗費資源磁碟區，設定為僅儲存需要頻繁且大量備份的工作負載。</span><span class="sxs-lookup"><span data-stu-id="9faa1-151">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) to store only the workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="9faa1-152">舉例來說，具有交易記錄的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="9faa1-152">An example is SQL Server with transaction logs.</span></span> <span data-ttu-id="9faa1-153">備份頻率不高的其他工作負載 (像是 VM)，則可備份到低成本磁碟區。</span><span class="sxs-lookup"><span data-stu-id="9faa1-153">Other workloads that are backed up less frequently, like VMs, can be backed up to low-cost volumes.</span></span>

### <a name="update-dpmdiskstorage"></a><span data-ttu-id="9faa1-154">Update-DPMDiskStorage</span><span class="sxs-lookup"><span data-stu-id="9faa1-154">Update-DPMDiskStorage</span></span>

<span data-ttu-id="9faa1-155">您可以使用 PowerShell Cmdlet Update-DPMDiskStorage 來設定可感知工作負載的儲存體，此 Cmdlet 會更新 Data Protection Manager 伺服器儲存集區的磁碟區屬性。</span><span class="sxs-lookup"><span data-stu-id="9faa1-155">You can set up workload-aware storage by using the PowerShell cmdlet Update-DPMDiskStorage, which updates the properties of a volume in the storage pool on a Data Protection Manager server.</span></span>

<span data-ttu-id="9faa1-156">語法：</span><span class="sxs-lookup"><span data-stu-id="9faa1-156">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```
<span data-ttu-id="9faa1-157">下列螢幕擷取畫面會顯示 PowerShell 視窗中的 Update-DPMDiskStorage Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="9faa1-157">The following screenshot shows the Update-DPMDiskStorage cmdlet in the PowerShell window.</span></span>

![PowerShell 視窗中的 Update-DPMDiskStorage 命令](./media/backup-mabs-add-storage/mabs-add-storage-8.png)

<span data-ttu-id="9faa1-159">您使用 PowerShell 所進行的變更會反映在備份伺服器管理員主控台中。</span><span class="sxs-lookup"><span data-stu-id="9faa1-159">The changes you make by using PowerShell are reflected in the Backup Server Administrator Console.</span></span>

![管理員主控台中的磁碟和磁碟區](./media/backup-mabs-add-storage/mabs-add-storage-9.png)

## <a name="next-steps"></a><span data-ttu-id="9faa1-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9faa1-161">Next steps</span></span>
<span data-ttu-id="9faa1-162">在安裝備份伺服器之後，請了解如何準備您的伺服器或開始保護工作負載。</span><span class="sxs-lookup"><span data-stu-id="9faa1-162">After you install Backup Server, learn how to prepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="9faa1-163">準備備份伺服器工作負載</span><span class="sxs-lookup"><span data-stu-id="9faa1-163">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="9faa1-164">使用備份伺服器來備份 VMware 伺服器</span><span class="sxs-lookup"><span data-stu-id="9faa1-164">Use Backup Server to back up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="9faa1-165">使用備份伺服器來備份 SQL Server</span><span class="sxs-lookup"><span data-stu-id="9faa1-165">Use Backup Server to back up SQL Server</span></span>](backup-azure-sql-mabs.md)

