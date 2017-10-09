---
title: "Azure 備份伺服器 v2 aaaInstall |Microsoft 文件"
description: "Azure 備份伺服器 v2 可提供您經過強化的備份功能，讓您保護 VM、檔案和資料夾以及工作負載等項目。 深入了解如何 tooinstall 或升級 tooAzure 備份伺服器 v2。"
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
ms.openlocfilehash: 5b1699dadd3a173f1c0ef91a1a600bc5e12f20ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-azure-backup-server-v2"></a><span data-ttu-id="9ad87-104">安裝 Azure 備份伺服器 v2</span><span class="sxs-lookup"><span data-stu-id="9ad87-104">Install Azure Backup Server v2</span></span>

<span data-ttu-id="9ad87-105">Azure 備份伺服器可協助保護您的虛擬機器 (VM)、工作負載以及檔案和資料夾等項目。</span><span class="sxs-lookup"><span data-stu-id="9ad87-105">Azure Backup Server helps protect your virtual machines (VMs), workloads, files and folders, and more.</span></span> <span data-ttu-id="9ad87-106">Azure 備份伺服器 v2 是以 Azure 備份伺服器 v1 作為建置基礎，並可提供您 v1 所沒有的新功能。</span><span class="sxs-lookup"><span data-stu-id="9ad87-106">Azure Backup Server v2 builds on Azure Backup Server v1, and gives you new features that are not available in v1.</span></span> <span data-ttu-id="9ad87-107">如需 v1 和 v2 的功能比較，請參閱 [Azure 備份伺服器保護對照表](backup-mabs-protection-matrix.md)。</span><span class="sxs-lookup"><span data-stu-id="9ad87-107">For a comparison of features between v1 and v2, see [Azure Backup Server protection matrix](backup-mabs-protection-matrix.md).</span></span> 

<span data-ttu-id="9ad87-108">hello 備份伺服器 v2 中的其他功能，包括備份伺服器 v1 升級。</span><span class="sxs-lookup"><span data-stu-id="9ad87-108">hello additional features in Backup Server v2 are an upgrade from Backup Server v1.</span></span> <span data-ttu-id="9ad87-109">不過，並非一定要有備份伺服器 v1 才能安裝備份伺服器 v2。</span><span class="sxs-lookup"><span data-stu-id="9ad87-109">However, Backup Server v1 is not a prerequisite for installing Backup Server v2.</span></span> <span data-ttu-id="9ad87-110">如果您要從備份伺服器 v1 tooBackup 伺服器 v2 tooupgrade，安裝備份伺服器 v2 hello 備份伺服器保護伺服器上。</span><span class="sxs-lookup"><span data-stu-id="9ad87-110">If you want tooupgrade from Backup Server v1 tooBackup Server v2, install Backup Server v2 on hello Backup Server protection server.</span></span> <span data-ttu-id="9ad87-111">您現有的備份伺服器設定會保持不變。</span><span class="sxs-lookup"><span data-stu-id="9ad87-111">Your existing Backup Server settings remain intact.</span></span>

<span data-ttu-id="9ad87-112">您可以在 Windows Server 2012 R2 或 Windows Server 2016 上安裝備份伺服器 v2。</span><span class="sxs-lookup"><span data-stu-id="9ad87-112">You can install Backup Server v2 on Windows Server 2012 R2 or Windows Server 2016.</span></span> <span data-ttu-id="9ad87-113">tootake 使用新的功能類似 System Center 2016 的資料保護管理員現代化備份存放裝置，您必須安裝 Windows Server 2016 上的備份伺服器 v2。</span><span class="sxs-lookup"><span data-stu-id="9ad87-113">tootake advantage of new features like System Center 2016 Data Protection Manager Modern Backup Storage, you must install Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="9ad87-114">升級 tooor 安裝 v2 備份伺服器之前，請閱讀 hello[安裝必要條件](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="9ad87-114">Before you upgrade tooor install Backup Server v2, read about hello [installation prerequisites](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites).</span></span>

> [!NOTE]
> <span data-ttu-id="9ad87-115">Azure 備份伺服器具有 hello 相同程式碼基底為 System Center Data Protection Manager。</span><span class="sxs-lookup"><span data-stu-id="9ad87-115">Azure Backup Server has hello same code base as System Center Data Protection Manager.</span></span> <span data-ttu-id="9ad87-116">備份伺服器 v1 相等 tooData Protection Manager 2012 R2 中，並備份伺服器 v2 是對等 tooData Protection Manager 2016。</span><span class="sxs-lookup"><span data-stu-id="9ad87-116">Backup Server v1 is equivalent tooData Protection Manager 2012 R2, and Backup Server v2 is equivalent tooData Protection Manager 2016.</span></span> <span data-ttu-id="9ad87-117">這篇文章偶爾會參考 hello Data Protection Manager 文件。</span><span class="sxs-lookup"><span data-stu-id="9ad87-117">This article occasionally references hello Data Protection Manager documentation.</span></span>
>
>

## <a name="upgrade-backup-server-toov2"></a><span data-ttu-id="9ad87-118">升級備份伺服器 toov2</span><span class="sxs-lookup"><span data-stu-id="9ad87-118">Upgrade Backup Server toov2</span></span>
<span data-ttu-id="9ad87-119">從備份伺服器 v1 tooBackup 伺服器 v2 tooupgrade 請確定您的安裝具有所需的 hello 更新：</span><span class="sxs-lookup"><span data-stu-id="9ad87-119">tooupgrade from Backup Server v1 tooBackup Server v2, make sure your installation has hello required updates:</span></span>

- <span data-ttu-id="9ad87-120">[Hello 保護代理程式更新](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent)hello 上受保護的伺服器。</span><span class="sxs-lookup"><span data-stu-id="9ad87-120">[Update hello protection agents](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent) on hello protected servers.</span></span>
- <span data-ttu-id="9ad87-121">升級 Windows Server 2012 R2 tooWindows Server 2016。</span><span class="sxs-lookup"><span data-stu-id="9ad87-121">Upgrade Windows Server 2012 R2 tooWindows Server 2016.</span></span>
- <span data-ttu-id="9ad87-122">在所有生產伺服器上升級 Azure 備份伺服器遠端系統管理員。</span><span class="sxs-lookup"><span data-stu-id="9ad87-122">Upgrade Azure Backup Server Remote Administrator on all production servers.</span></span>
- <span data-ttu-id="9ad87-123">確定備份設定 toocontinue 不需要重新啟動您的實際伺服器。</span><span class="sxs-lookup"><span data-stu-id="9ad87-123">Ensure that backups are set toocontinue without restarting your production server.</span></span>


### <a name="upgrade-steps-for-backup-server-v2"></a><span data-ttu-id="9ad87-124">備份伺服器 v2 的升級步驟</span><span class="sxs-lookup"><span data-stu-id="9ad87-124">Upgrade steps for Backup Server v2</span></span>

1. <span data-ttu-id="9ad87-125">在 hello Download Center[下載 hello 升級安裝程式](https://go.microsoft.com/fwlink/?LinkId=626082)。</span><span class="sxs-lookup"><span data-stu-id="9ad87-125">In hello Download Center, [download hello upgrade installer](https://go.microsoft.com/fwlink/?LinkId=626082).</span></span>

2. <span data-ttu-id="9ad87-126">擷取 hello 安裝精靈之後，請確定**執行 setup.exe**已選取，然後選取**完成**。</span><span class="sxs-lookup"><span data-stu-id="9ad87-126">After you extract hello setup wizard, make sure that **Execute setup.exe** is selected, and then select **Finish**.</span></span>

  ![設定安裝程式 - 執行設定](./media/backup-mabs-upgrade-to-v2/run-setup.png)

3. <span data-ttu-id="9ad87-128">在 hello Microsoft Azure 備份伺服器精靈 在**安裝**，選取**Microsoft Azure 備份伺服器**。</span><span class="sxs-lookup"><span data-stu-id="9ad87-128">In hello Microsoft Azure Backup Server wizard, under **Install**, select **Microsoft Azure Backup Server**.</span></span>

  ![設定安裝程式 - 選取安裝](./media/backup-mabs-upgrade-to-v2/mabs-installer-s1.png)

4. <span data-ttu-id="9ad87-130">在 hello ** 褖畫惎**頁面上，檢閱 hello 警告，然後選取**下一步**。</span><span class="sxs-lookup"><span data-stu-id="9ad87-130">On hello **Welcome** page, review hello warnings, and then select **Next**.</span></span>

  ![設定安裝程式 - [歡迎使用] 頁面](./media/backup-mabs-upgrade-to-v2/mabs-installer-s2.png)

5. <span data-ttu-id="9ad87-132">hello 安裝精靈會執行必要條件檢查 toomake 確定可以升級您的環境。</span><span class="sxs-lookup"><span data-stu-id="9ad87-132">hello setup wizard performs prerequisite checks toomake sure your environment can upgrade.</span></span> <span data-ttu-id="9ad87-133">在 hello **Prerequisite Checks**頁面上，選取**檢查**。</span><span class="sxs-lookup"><span data-stu-id="9ad87-133">On hello **Prerequisite Checks** page, select **Check**.</span></span>

  ![設定安裝程式 - [必要條件檢查] 頁面](./media/backup-mabs-upgrade-to-v2/mabs-installer-s3-perform-checks.png)

6. <span data-ttu-id="9ad87-135">您的環境必須通過 hello 必要條件檢查。</span><span class="sxs-lookup"><span data-stu-id="9ad87-135">Your environment must pass hello prerequisite checks.</span></span> <span data-ttu-id="9ad87-136">如果您的環境未通過 hello 檢查，請注意 hello 問題並加以修正。</span><span class="sxs-lookup"><span data-stu-id="9ad87-136">If your environment doesn't pass hello checks, note hello issues and fix them.</span></span> <span data-ttu-id="9ad87-137">然後，選取 [再檢查一次]。</span><span class="sxs-lookup"><span data-stu-id="9ad87-137">Then, select **Check Again**.</span></span> <span data-ttu-id="9ad87-138">您傳遞 hello 必要條件檢查之後，請選取**下一步**。</span><span class="sxs-lookup"><span data-stu-id="9ad87-138">After you pass hello prerequisite checks, select **Next**.</span></span>

  ![設定安裝程式 - [再檢查一次] 按鈕](./media/backup-mabs-upgrade-to-v2/mabs-installer-s4-pass-checks.png)

7. <span data-ttu-id="9ad87-140">在 hello **SQL 設定**頁面上，選取您的 SQL 安裝的 hello 相關選項，然後選取**檢查並安裝**。</span><span class="sxs-lookup"><span data-stu-id="9ad87-140">On hello **SQL Settings** page, select hello relevant option for your SQL installation, and then select **Check and Install**.</span></span>

  ![設定安裝程式 - [SQL 設定] 頁面](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5-sql-settings.png)

  <span data-ttu-id="9ad87-142">hello 檢查可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="9ad87-142">hello checks might take a few minutes.</span></span> <span data-ttu-id="9ad87-143">當 hello 檢查是否已完成，請選取**下一步**。</span><span class="sxs-lookup"><span data-stu-id="9ad87-143">When hello checks are finished, select **Next**.</span></span>

  ![設定安裝程式 - [SQL 設定] 的 [檢查並安裝] 按鈕](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5a-check-and fix-settings.png)

8. <span data-ttu-id="9ad87-145">在 hello**安裝設定**頁面上，進行備份伺服器安裝所在的任何變更 toohello 位置或 toohello 可用位置。</span><span class="sxs-lookup"><span data-stu-id="9ad87-145">On hello **Installation Settings** page, make any changes toohello location where Backup Server is installed, or toohello Scratch Location.</span></span> <span data-ttu-id="9ad87-146">選取 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="9ad87-146">Select **Next**.</span></span>

  ![設定安裝程式 - [安裝設定] 頁面](./media/backup-mabs-upgrade-to-v2/mabs-installer-s6-installation-settings.png)

9. <span data-ttu-id="9ad87-148">toofinish hello 安裝精靈中，選取**完成**。</span><span class="sxs-lookup"><span data-stu-id="9ad87-148">toofinish hello setup wizard, select **Finish**.</span></span>

  ![設定安裝程式 - 完成](./media/backup-mabs-upgrade-to-v2/run-setup.png)



## <a name="add-storage-for-modern-backup-storage"></a><span data-ttu-id="9ad87-150">為新式備份儲存體新增儲存體</span><span class="sxs-lookup"><span data-stu-id="9ad87-150">Add storage for Modern Backup Storage</span></span>

<span data-ttu-id="9ad87-151">tooimprove 備份儲存體效率，備份伺服器 v2 加入磁碟區的支援。</span><span class="sxs-lookup"><span data-stu-id="9ad87-151">tooimprove backup storage efficiency, Backup Server v2 adds support for volumes.</span></span> <span data-ttu-id="9ad87-152">和備份伺服器 v1 一樣，備份伺服器 v2 也支援磁碟。</span><span class="sxs-lookup"><span data-stu-id="9ad87-152">Like Backup Server v1, Backup Server v2 supports disks.</span></span>

### <a name="add-volumes-and-disks"></a><span data-ttu-id="9ad87-153">新增磁碟區和磁碟</span><span class="sxs-lookup"><span data-stu-id="9ad87-153">Add volumes and disks</span></span>
<span data-ttu-id="9ad87-154">如果您在 Windows Server 2016 上執行備份伺服器 v2，您可以使用磁碟區 toostore 備份資料。</span><span class="sxs-lookup"><span data-stu-id="9ad87-154">If you run Backup Server v2 on Windows Server 2016, you can use volumes toostore backup data.</span></span> <span data-ttu-id="9ad87-155">磁碟區可節省儲存空間並提高備份速度。</span><span class="sxs-lookup"><span data-stu-id="9ad87-155">Volumes offer storage savings and faster backups.</span></span> <span data-ttu-id="9ad87-156">因為磁碟區是新 tooBackup 伺服器，您必須將其加入。</span><span class="sxs-lookup"><span data-stu-id="9ad87-156">Because volumes are new tooBackup Server, you must add them.</span></span> 

<span data-ttu-id="9ad87-157">當您新增的磁碟區 tooBackup 伺服器時，您可以提供 hello 磁碟區的好記名稱。</span><span class="sxs-lookup"><span data-stu-id="9ad87-157">When you add a volume tooBackup Server, you can give hello volume a friendly name.</span></span> <span data-ttu-id="9ad87-158">按一下 hello**易記名稱**資料行要 tooname 的 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="9ad87-158">Click hello **Friendly Name** column of hello volume you want tooname.</span></span> <span data-ttu-id="9ad87-159">如有必要，您可以稍後變更 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="9ad87-159">You can change hello name later, if necessary.</span></span> <span data-ttu-id="9ad87-160">您也可以使用 PowerShell tooadd 或變更磁碟區的好記名稱。</span><span class="sxs-lookup"><span data-stu-id="9ad87-160">You also can use PowerShell tooadd or change friendly names for volumes.</span></span>

<span data-ttu-id="9ad87-161">tooadd hello 系統管理員主控台中的磁碟區：</span><span class="sxs-lookup"><span data-stu-id="9ad87-161">tooadd a volume in hello Administrator Console:</span></span>

1. <span data-ttu-id="9ad87-162">在 hello Azure 備份伺服器系統管理員主控台中，選取 **管理** > **磁碟儲存體** > **新增**。</span><span class="sxs-lookup"><span data-stu-id="9ad87-162">In hello Azure Backup Server Administrator Console, select **Management** > **Disk Storage** > **Add**.</span></span>

    ![開啟 hello 加入磁碟儲存體精靈](./media//backup-mabs-upgrade-to-v2/open-add-disk-storage-wizard.png)

    <span data-ttu-id="9ad87-164">這會開啟 hello 加入磁碟儲存體精靈。</span><span class="sxs-lookup"><span data-stu-id="9ad87-164">This opens hello Add Disk Storage wizard.</span></span>

2. <span data-ttu-id="9ad87-165">在 hello**加入磁碟儲存體**] 頁面的 hello**可用的磁碟區**，選取 [磁碟區，然後選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="9ad87-165">On hello **Add Disk Storage** page, in hello **Available volumes** box, select a volume, and then select **Add**.</span></span>
3. <span data-ttu-id="9ad87-166">在 hello**選取磁碟區**方塊、 輸入 hello 磁碟區的好記名稱，然後選取**確定**。</span><span class="sxs-lookup"><span data-stu-id="9ad87-166">In hello **Selected volumes** box, enter a friendly name for hello volume, and then select **OK**.</span></span>

      ![新增磁碟儲存體精靈 - 新增磁碟區](./media/backup-mabs-upgrade-to-v2/add-volume.png)

  <span data-ttu-id="9ad87-168">如果您想 tooadd 磁碟，hello 磁碟必須屬於 tooa 保護群組具有傳統存放裝置。</span><span class="sxs-lookup"><span data-stu-id="9ad87-168">If you want tooadd a disk, hello disk must belong tooa protection group that has legacy storage.</span></span> <span data-ttu-id="9ad87-169">這些磁碟僅能用於這些保護群組。</span><span class="sxs-lookup"><span data-stu-id="9ad87-169">These disks can only be used for these protection groups.</span></span> <span data-ttu-id="9ad87-170">備份伺服器並沒有有舊版保護的來源，如果未列出 hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="9ad87-170">If Backup Server doesn't have sources that have legacy protection, hello disk isn't listed.</span></span>

  <span data-ttu-id="9ad87-171">如需新增磁碟的詳細資訊，請參閱[新增磁碟 tooincrease 傳統儲存體](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage)。</span><span class="sxs-lookup"><span data-stu-id="9ad87-171">For more information about adding disks, see [Adding disks tooincrease legacy storage](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage).</span></span> <span data-ttu-id="9ad87-172">您不能對磁碟賦予易記名稱。</span><span class="sxs-lookup"><span data-stu-id="9ad87-172">You can't give a disk a friendly name.</span></span>


### <a name="assign-workloads-toovolumes"></a><span data-ttu-id="9ad87-173">指定工作負載 toovolumes</span><span class="sxs-lookup"><span data-stu-id="9ad87-173">Assign workloads toovolumes</span></span>

<span data-ttu-id="9ad87-174">備份伺服器，在您指定的工作負載指派 toowhich 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="9ad87-174">In Backup Server, you specify which workloads are assigned toowhich volumes.</span></span> <span data-ttu-id="9ad87-175">例如，您可以設定昂貴支援大量輸入/輸出作業每個第二個 (IOPS) toostore 唯一需要的工作負載高容量頻繁備份的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="9ad87-175">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) toostore only workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="9ad87-176">舉例來說，具有交易記錄的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="9ad87-176">An example is SQL Server with transaction logs.</span></span>

#### <a name="update-dpmdiskstorage"></a><span data-ttu-id="9ad87-177">Update-DPMDiskStorage</span><span class="sxs-lookup"><span data-stu-id="9ad87-177">Update-DPMDiskStorage</span></span>

<span data-ttu-id="9ad87-178">備份伺服器 hello 存放集區中的磁碟區 tooupdate hello 屬性，請使用 PowerShell 指令程式更新 DPMDiskStorage hello。</span><span class="sxs-lookup"><span data-stu-id="9ad87-178">tooupdate hello properties of a volume in hello storage pool in Backup Server, use hello PowerShell cmdlet Update-DPMDiskStorage.</span></span>

<span data-ttu-id="9ad87-179">語法：</span><span class="sxs-lookup"><span data-stu-id="9ad87-179">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

<span data-ttu-id="9ad87-180">使用 PowerShell 進行的所有變更會都反映在 hello UI。</span><span class="sxs-lookup"><span data-stu-id="9ad87-180">All changes that you make by using PowerShell are reflected in hello UI.</span></span>


## <a name="protect-data-sources"></a><span data-ttu-id="9ad87-181">保護資料來源</span><span class="sxs-lookup"><span data-stu-id="9ad87-181">Protect data sources</span></span>
<span data-ttu-id="9ad87-182">toobegin 保護資料來源，建立保護群組。</span><span class="sxs-lookup"><span data-stu-id="9ad87-182">toobegin protecting data sources, create a protection group.</span></span> <span data-ttu-id="9ad87-183">hello 遵循步驟反白顯示變更或新增 toohello 新保護群組精靈。</span><span class="sxs-lookup"><span data-stu-id="9ad87-183">hello following steps highlight changes or additions toohello New Protection Group wizard.</span></span>

<span data-ttu-id="9ad87-184">toocreate 保護群組：</span><span class="sxs-lookup"><span data-stu-id="9ad87-184">toocreate a protection group:</span></span>

1. <span data-ttu-id="9ad87-185">在 hello 備份伺服器系統管理員主控台中，選取 **保護**。</span><span class="sxs-lookup"><span data-stu-id="9ad87-185">In hello Backup Server Administrator Console, select **Protection**.</span></span>

2. <span data-ttu-id="9ad87-186">在 hello 工具功能區中，選取 **新增**。</span><span class="sxs-lookup"><span data-stu-id="9ad87-186">On hello tool ribbon, select **New**.</span></span>

    <span data-ttu-id="9ad87-187">這會開啟 hello 建立新保護群組精靈。</span><span class="sxs-lookup"><span data-stu-id="9ad87-187">This opens hello Create New Protection Group wizard.</span></span>

  ![建立新保護群組精靈](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-1.png)

3. <span data-ttu-id="9ad87-189">在 hello ** 褖畫惎**頁面上，選取**下一步**。</span><span class="sxs-lookup"><span data-stu-id="9ad87-189">On hello **Welcome** page, select **Next**.</span></span>
4. <span data-ttu-id="9ad87-190">在 hello**選取保護群組類型**頁面上，選取您想 toocreate，，然後選取保護群組的 hello 類型**下一步**。</span><span class="sxs-lookup"><span data-stu-id="9ad87-190">On hello **Select Protection Group Type** page, select hello type of protection group you want toocreate, and then select **Next**.</span></span>

  ![[選取保護群組類型] 頁面](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-2.png)

5. <span data-ttu-id="9ad87-192">在 hello**選擇群組成員** 頁面的 hello**可用成員**窗格中，保護代理程式會列出與 hello 成員。</span><span class="sxs-lookup"><span data-stu-id="9ad87-192">On hello **Select Group Members** page, in hello **Available members** pane, hello members with protection agents are listed.</span></span> <span data-ttu-id="9ad87-193">針對此範例中，選取 磁碟區 D:\ 和 E:\ 並將其新增 toohello**選取的成員**窗格。</span><span class="sxs-lookup"><span data-stu-id="9ad87-193">For this example, select volume D:\ and E:\ and add them toohello **Selected members** pane.</span></span> <span data-ttu-id="9ad87-194">選取 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="9ad87-194">Select **Next**.</span></span>

  ![[選取群組成員] 頁面](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-3.png)

6. <span data-ttu-id="9ad87-196">在 [hello**選擇資料保護方式**頁面上，輸入**保護群組名稱**選取 hello 保護方式，，然後選取**下一步]**。</span><span class="sxs-lookup"><span data-stu-id="9ad87-196">On hello **Select Data Protection Method** page, enter a **Protection group name**, select hello protection method, and then select **Next**.</span></span> <span data-ttu-id="9ad87-197">如果您想要短期保護，您必須選取 hello**磁碟**備份方法。</span><span class="sxs-lookup"><span data-stu-id="9ad87-197">If you want short-term protection, you must select hello **Disk** backup method.</span></span>

  ![[選取資料保護方式] 頁面](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-4.png)

7. <span data-ttu-id="9ad87-199">在 hello**指定短期目標**頁面上，選取 hello 詳細資料**保留範圍**和**同步處理頻率**。</span><span class="sxs-lookup"><span data-stu-id="9ad87-199">On hello **Specify Short-Term Goals** page, select hello details for **Retention range** and **Synchronization frequency**.</span></span> <span data-ttu-id="9ad87-200">然後，選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="9ad87-200">Then, select **Next**.</span></span> <span data-ttu-id="9ad87-201">（選擇性） toochange hello 排程復原點時所建立，請選取**修改**。</span><span class="sxs-lookup"><span data-stu-id="9ad87-201">Optionally, toochange hello schedule for when recovery points are taken, select **Modify**.</span></span>

  ![[指定短期目標] 頁面](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-5.png)

8. <span data-ttu-id="9ad87-203">在 hello**檢閱磁碟儲存體配置**頁面檢閱有關 hello 您選取的資料來源的詳細資料、 大小和 hello 空間 toobe 佈建的值，並 hello 目標儲存體磁碟區。</span><span class="sxs-lookup"><span data-stu-id="9ad87-203">On hello **Review Disk Storage Allocation** page, review details about hello data sources you selected, their size, and  values for hello space toobe provisioned and hello target storage volume.</span></span>

  ![[檢閱磁碟儲存體配置] 頁面](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-6.png)

  <span data-ttu-id="9ad87-205">存放磁碟區依據 hello （使用 PowerShell 設定） 的工作負載磁碟區配置和 hello 可用的存放裝置。</span><span class="sxs-lookup"><span data-stu-id="9ad87-205">Storage volumes are based on hello workload volume allocation (set by using PowerShell) and hello available storage.</span></span> <span data-ttu-id="9ad87-206">您可以變更 hello 存放磁碟區 hello 下拉式選單中選取其他磁碟區。</span><span class="sxs-lookup"><span data-stu-id="9ad87-206">You can change hello storage volumes by selecting other volumes in hello drop-down menu.</span></span> <span data-ttu-id="9ad87-207">如果您變更 hello 值**目標儲存體**，hello 值**可用的磁碟儲存體**tooreflect 值底下會動態變更**可用空間**和**Underprovisioned 空間**。</span><span class="sxs-lookup"><span data-stu-id="9ad87-207">If you change hello value for **Target Storage**, hello value for **Available disk storage** dynamically changes tooreflect values under **Free Space** and **Underprovisioned Space**.</span></span>

  <span data-ttu-id="9ad87-208">Hello 資料來源成長為已規劃，hello 值 hello **Underprovisioned 空間**中的資料行**可用的磁碟儲存體**反映 hello 額外的存放裝置所需的數量。</span><span class="sxs-lookup"><span data-stu-id="9ad87-208">If hello data sources grow as planned, hello value for hello **Underprovisioned Space** column in **Available disk storage** reflects hello amount of additional storage that's needed.</span></span> <span data-ttu-id="9ad87-209">使用您的儲存體需要 smooth 備份此值 toohelp 計劃。</span><span class="sxs-lookup"><span data-stu-id="9ad87-209">Use this value toohelp plan your storage needs for smooth backups.</span></span> <span data-ttu-id="9ad87-210">Hello 值為零中, 有任何儲存體可能造成的問題 hello 可預見未來。</span><span class="sxs-lookup"><span data-stu-id="9ad87-210">If hello value is zero, there are no potential problems with storage in hello foreseeable future.</span></span> <span data-ttu-id="9ad87-211">Hello 值為非零的數字，如果您沒有足夠的儲存空間配置 （根據您保護原則 hello 資料大小和受保護的成員）。</span><span class="sxs-lookup"><span data-stu-id="9ad87-211">If hello value is a number other than zero, you do not have sufficient storage allocated  (based on your protection policy and hello data size of your protected members).</span></span>

  ![配置不足的磁碟儲存體](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-7.png)

   <span data-ttu-id="9ad87-213">建立保護群組、 完整 hello 精靈 toofinish。</span><span class="sxs-lookup"><span data-stu-id="9ad87-213">toofinish creating your protection group, complete hello wizard.</span></span>

## <a name="migrate-legacy-storage-toomodern-backup-storage"></a><span data-ttu-id="9ad87-214">移轉舊版的儲存體 tooModern 備份儲存體</span><span class="sxs-lookup"><span data-stu-id="9ad87-214">Migrate legacy storage tooModern Backup Storage</span></span>
<span data-ttu-id="9ad87-215">Tooor 安裝備份伺服器 v2 和升級 hello 作業系統 tooWindows Server 2016 的升級之後，更新您的保護群組 toouse 現代的備份儲存體。</span><span class="sxs-lookup"><span data-stu-id="9ad87-215">After you upgrade tooor install Backup Server v2 and upgrade hello operating system tooWindows Server 2016, update your protection groups toouse Modern Backup Storage.</span></span> <span data-ttu-id="9ad87-216">根據預設，系統不會變更保護群組。</span><span class="sxs-lookup"><span data-stu-id="9ad87-216">By default, protection groups are not changed.</span></span> <span data-ttu-id="9ad87-217">他們可以繼續 toofunction 它們一開始所設定。</span><span class="sxs-lookup"><span data-stu-id="9ad87-217">They continue toofunction as they were initially set up.</span></span> 

<span data-ttu-id="9ad87-218">更新保護群組 toouse 現代的備份儲存體是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="9ad87-218">Updating protection groups toouse Modern Backup Storage is optional.</span></span> <span data-ttu-id="9ad87-219">tooupdate hello 保護群組時，使用 hello 的所有資料來源停止保護保留資料選項。</span><span class="sxs-lookup"><span data-stu-id="9ad87-219">tooupdate hello protection group, stop protection of all data sources by using hello retain data option.</span></span> <span data-ttu-id="9ad87-220">然後，加入 hello 資料來源 tooa 新的保護群組。</span><span class="sxs-lookup"><span data-stu-id="9ad87-220">Then, add hello data sources tooa new protection group.</span></span>

1. <span data-ttu-id="9ad87-221">在 hello 系統管理員主控台中，選取 hello**保護**功能。</span><span class="sxs-lookup"><span data-stu-id="9ad87-221">In hello Administrator Console, select hello **Protection** feature.</span></span> <span data-ttu-id="9ad87-222">在 hello**保護群組成員**清單中，以滑鼠右鍵按一下 hello 成員，然後選取**停止保護成員**。</span><span class="sxs-lookup"><span data-stu-id="9ad87-222">In hello **Protection Group Member** list, right-click hello member, and then select **Stop protection of member**.</span></span>

  ![停止保護成員](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-stop-protection1.png)

2. <span data-ttu-id="9ad87-224">在 [hello**從群組移除**] 對話方塊中，檢閱 hello 使用磁碟空間和 hello 可用空間 hello 存放集區。</span><span class="sxs-lookup"><span data-stu-id="9ad87-224">In hello **Remove from Group** dialog box, review hello used disk space and hello available free space for hello storage pool.</span></span> <span data-ttu-id="9ad87-225">hello 預設值為 hello 磁碟上的 tooleave hello 復原點，而且允許這些 tooexpire 每個關聯的保留原則。</span><span class="sxs-lookup"><span data-stu-id="9ad87-225">hello default is tooleave hello recovery points on hello disk and allow them tooexpire per their associated retention policy.</span></span> <span data-ttu-id="9ad87-226">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="9ad87-226">Click **OK**.</span></span>

  <span data-ttu-id="9ad87-227">如果您想 tooimmediately 傳回 hello 使用磁碟空間 toohello 可用儲存集區，選取 hello**刪除磁碟上的複本**與成員相關的核取方塊 toodelete hello 備份資料 （和復原點）。</span><span class="sxs-lookup"><span data-stu-id="9ad87-227">If you want tooimmediately return hello used disk space toohello free storage pool, select hello **Delete replica on disk** check box toodelete hello backup data (and recovery points) associated with that member.</span></span>

  ![[從群組中移除] 對話方塊](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-retain-data.png)

3. <span data-ttu-id="9ad87-229">建立使用新式備份儲存體的保護群組。</span><span class="sxs-lookup"><span data-stu-id="9ad87-229">Create a protection group that uses Modern Backup Storage.</span></span> <span data-ttu-id="9ad87-230">包含 hello 未受保護資料來源。</span><span class="sxs-lookup"><span data-stu-id="9ad87-230">Include hello unprotected data sources.</span></span>


## <a name="add-disks-tooincrease-legacy-storage"></a><span data-ttu-id="9ad87-231">新增磁碟 tooincrease 傳統存放裝置</span><span class="sxs-lookup"><span data-stu-id="9ad87-231">Add disks tooincrease legacy storage</span></span>

<span data-ttu-id="9ad87-232">如果您想 toouse 傳統存放裝置，且備份伺服器，您可能需要 tooadd 磁碟 tooincrease 傳統儲存體。</span><span class="sxs-lookup"><span data-stu-id="9ad87-232">If you want toouse legacy storage with Backup Server, you might need tooadd disks tooincrease legacy storage.</span></span> 

<span data-ttu-id="9ad87-233">tooadd 磁碟儲存體：</span><span class="sxs-lookup"><span data-stu-id="9ad87-233">tooadd disk storage:</span></span>

1. <span data-ttu-id="9ad87-234">在 hello 系統管理員主控台中，選取 **管理** > **磁碟儲存體** > **新增**。</span><span class="sxs-lookup"><span data-stu-id="9ad87-234">In hello Administrator Console, select **Management** > **Disk Storage** > **Add**.</span></span>

    ![[新增磁碟儲存體] 對話方塊](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-add-disk-storage.png)

4. <span data-ttu-id="9ad87-236">在 hello**加入磁碟儲存體**對話方塊中，選取**新增磁碟**。</span><span class="sxs-lookup"><span data-stu-id="9ad87-236">In hello **Add Disk Storage** dialog, select **Add disks**.</span></span>

5. <span data-ttu-id="9ad87-237">Hello 在清單中可用的磁碟，請選取您想要選取 tooadd 的 hello 磁碟**新增**，然後選取**確定**。</span><span class="sxs-lookup"><span data-stu-id="9ad87-237">In hello list of available disks, select hello disks you want tooadd, select **Add**, and then select **OK**.</span></span>

## <a name="update-hello-data-protection-manager-protection-agent"></a><span data-ttu-id="9ad87-238">更新 hello Data Protection Manager 保護代理程式</span><span class="sxs-lookup"><span data-stu-id="9ad87-238">Update hello Data Protection Manager protection agent</span></span>

<span data-ttu-id="9ad87-239">備份伺服器使用 hello System Center Data Protection Manager 保護代理程式更新。</span><span class="sxs-lookup"><span data-stu-id="9ad87-239">Backup Server uses hello System Center Data Protection Manager protection agent for updates.</span></span> <span data-ttu-id="9ad87-240">如果您要升級保護代理程式未連接的 toohello 網路，您無法使用 hello 資料保護 Manager 系統管理員主控台 toocomplete 連接的代理程式升級。</span><span class="sxs-lookup"><span data-stu-id="9ad87-240">If you are upgrading a protection agent that is not connected toohello network, you cannot use hello Data Protection Manager Administrator Console toocomplete a connected agent upgrade.</span></span> <span data-ttu-id="9ad87-241">您必須先升級非作用中網域環境中的 hello 保護代理程式。</span><span class="sxs-lookup"><span data-stu-id="9ad87-241">You must upgrade hello protection agent in a nonactive domain environment.</span></span> <span data-ttu-id="9ad87-242">連接的 toohello 網路 hello 用戶端電腦之前，資料保護 Manager 系統管理員主控台會顯示該 hello 保護代理程式更新的 hello 已暫止。</span><span class="sxs-lookup"><span data-stu-id="9ad87-242">Until hello client computer is connected toohello network, hello Data Protection Manager Administrator Console shows that hello protection agent update is pending.</span></span>

<span data-ttu-id="9ad87-243">hello 下列各節說明如何 tooupdate 連線的用戶端電腦和未連接的用戶端電腦的保護代理程式。</span><span class="sxs-lookup"><span data-stu-id="9ad87-243">hello following sections describe how tooupdate protection agents for client computers that are connected and client computers that are not connected.</span></span>

### <a name="update-a-protection-agent-for-a-connected-client-computer"></a><span data-ttu-id="9ad87-244">更新已連線用戶端電腦的保護代理程式</span><span class="sxs-lookup"><span data-stu-id="9ad87-244">Update a protection agent for a connected client computer</span></span>

1. <span data-ttu-id="9ad87-245">在 hello 備份伺服器系統管理員主控台中，選取 **管理** > **代理程式**。</span><span class="sxs-lookup"><span data-stu-id="9ad87-245">In hello Backup Server Administrator Console, select **Management** > **Agents**.</span></span>

2. <span data-ttu-id="9ad87-246">Hello 顯示窗格中，選取您要為其 tooupdate hello 保護代理程式的 hello 用戶端電腦。</span><span class="sxs-lookup"><span data-stu-id="9ad87-246">In hello display pane, select hello client computers for which you want tooupdate hello protection agent.</span></span>

  > [!NOTE]
  > <span data-ttu-id="9ad87-247">hello**代理程式更新**欄位指出當保護代理程式更新為適用於每個受保護的電腦。</span><span class="sxs-lookup"><span data-stu-id="9ad87-247">hello **Agent Updates** column indicates when a protection agent update is available for each protected computer.</span></span> <span data-ttu-id="9ad87-248">在 hello**動作**窗格中，hello**更新**動作可用，只會選取受保護的電腦，並更新可供使用。</span><span class="sxs-lookup"><span data-stu-id="9ad87-248">In hello **Actions** pane, hello **Update** action is available only when a protected computer is selected and updates are available.</span></span>
  >
  >

3. <span data-ttu-id="9ad87-249">tooinstall 更新保護代理程式選取 hello 在電腦上，在 hello**動作**窗格中，選取**更新**。</span><span class="sxs-lookup"><span data-stu-id="9ad87-249">tooinstall updated protection agents on hello selected computers, in hello **Actions** pane, select **Update**.</span></span>

### <a name="update-a-protection-agent-on-a-client-computer-that-is-not-connected"></a><span data-ttu-id="9ad87-250">在未連線用戶端電腦上更新保護代理程式</span><span class="sxs-lookup"><span data-stu-id="9ad87-250">Update a protection agent on a client computer that is not connected</span></span>

1. <span data-ttu-id="9ad87-251">在 hello 備份伺服器系統管理員主控台中，選取 **管理** > **代理程式**。</span><span class="sxs-lookup"><span data-stu-id="9ad87-251">In hello Backup Server Administrator Console, select **Management** > **Agents**.</span></span>

2. <span data-ttu-id="9ad87-252">Hello 顯示窗格中，選取您要為其 tooupdate hello 保護代理程式的 hello 用戶端電腦。</span><span class="sxs-lookup"><span data-stu-id="9ad87-252">In hello display pane, select hello client computers for which you want tooupdate hello protection agent.</span></span>

  > [!NOTE]
   > <span data-ttu-id="9ad87-253">hello**代理程式更新**欄位指出當保護代理程式更新為適用於每個受保護的電腦。</span><span class="sxs-lookup"><span data-stu-id="9ad87-253">hello **Agent Updates** column indicates when a protection agent update is available for each protected computer.</span></span> <span data-ttu-id="9ad87-254">在 hello**動作**窗格中，hello**更新**動作時，無法使用選取的受保護的電腦，除非有可用的更新。</span><span class="sxs-lookup"><span data-stu-id="9ad87-254">In hello **Actions** pane, hello **Update** action is not available when a protected computer is selected unless updates are available.</span></span>
  >
  >

3. <span data-ttu-id="9ad87-255">tooinstall 更新保護代理程式選取 hello 在電腦上，選取**更新**。</span><span class="sxs-lookup"><span data-stu-id="9ad87-255">tooinstall updated protection agents on hello selected computers, select **Update**.</span></span>

4. <span data-ttu-id="9ad87-256">Hello 電腦是連線的 toohello 網路之前，不是用戶端電腦已連接 toohello 網路，hello**代理程式狀態**資料行會顯示狀態為**更新擱置**。</span><span class="sxs-lookup"><span data-stu-id="9ad87-256">For a client computer that is not connected toohello network, until hello computer is connected toohello network, hello **Agent Status** column shows a status of **Update Pending**.</span></span>

  <span data-ttu-id="9ad87-257">用戶端電腦是連線的 toohello 網路之後，hello**代理程式更新**hello 用戶端電腦的資料行會顯示狀態為**更新**。</span><span class="sxs-lookup"><span data-stu-id="9ad87-257">After a client computer is connected toohello network, hello **Agent Updates** column for hello client computer shows a status of **Updating**.</span></span>
  
### <a name="move-legacy-protection-groups-from-old-version-and-sync-hello-new-version-with-azure"></a><span data-ttu-id="9ad87-258">移動從舊的版本，以及與 Azure 同步 hello 新版本的舊版保護群組</span><span class="sxs-lookup"><span data-stu-id="9ad87-258">Move legacy Protection groups from old version and sync hello new version with Azure</span></span>

<span data-ttu-id="9ad87-259">一旦 Azure 備份伺服器和 hello 作業系統會同時更新，您就準備好 tooprotect 新的資料來源使用現代的備份儲存體。</span><span class="sxs-lookup"><span data-stu-id="9ad87-259">Once Azure Backup Server and hello OS are both updated, you are ready tooprotect new data sources using Modern Backup Storage.</span></span> <span data-ttu-id="9ad87-260">不過已受保護的資料來源將會繼續 toobe hello 舊版中受保護的方式與 Azure 備份伺服器 中，但是所有新的保護將會使用現代的備份存放裝置。</span><span class="sxs-lookup"><span data-stu-id="9ad87-260">However already protected data sources will continue toobe protected in hello legacy way as they were in Azure Backup Server but all new protection will use Modern Backup Storage.</span></span>

<span data-ttu-id="9ad87-261">下列步驟是 toomigrate 資料來源從保護 tooModern 備份儲存體的傳統模式。</span><span class="sxs-lookup"><span data-stu-id="9ad87-261">Below steps are toomigrate data sources from legacy  mode of protection tooModern backup storage.</span></span>

<span data-ttu-id="9ad87-262">• 新增 hello 新磁碟區 toohello DPM 存放集區，並視需要指派易記名稱和資料來源的標記。</span><span class="sxs-lookup"><span data-stu-id="9ad87-262">• Add hello new volume(s) toohello DPM storage pool and assign friendly names and data source tags if desired.</span></span>
<span data-ttu-id="9ad87-263">• 在舊版模式下，停止保護 hello 資料來源和 「 保留受保護的資料 」 的每個資料來源。</span><span class="sxs-lookup"><span data-stu-id="9ad87-263">• For each data source that is in legacy mode, stop protection of hello data sources and “Retain Protected Data”.</span></span>  <span data-ttu-id="9ad87-264">這允許在移轉之後復原舊的復原點。</span><span class="sxs-lookup"><span data-stu-id="9ad87-264">This will allow recovery of old recovery points after migration.</span></span>

<span data-ttu-id="9ad87-265">• 建立新的 PG，然後選取 hello toobe 使用新格式儲存的資料來源。</span><span class="sxs-lookup"><span data-stu-id="9ad87-265">• Create a new PG and select hello data sources that are toobe stored using new format.</span></span>
<span data-ttu-id="9ad87-266">• DPM 將執行從 hello 舊版備份儲存體複本複製到 hello 本機現代的備份存放磁碟區。</span><span class="sxs-lookup"><span data-stu-id="9ad87-266">• DPM will do a replica copy from hello legacy backup storage into hello Modern Backup Storage volume locally.</span></span>
<span data-ttu-id="9ad87-267">注意：這會被視為復原後作業 • 所有新的同步處理和復原點則會儲存在新式備份儲存體中。</span><span class="sxs-lookup"><span data-stu-id="9ad87-267">Note: This will be seen as a post-recovery operation job • All new sync and recovery points will then be stored in Modern Backup Storage.</span></span>
<span data-ttu-id="9ad87-268">將出剪除 • 舊的復原點，視為過期，而且最後釋出 hello 磁碟空間。</span><span class="sxs-lookup"><span data-stu-id="9ad87-268">• Old recovery points will be pruned out as they expire and eventually free up hello disk space.</span></span>
<span data-ttu-id="9ad87-269">• 從 hello 舊的存放裝置 hello 磁碟中刪除所有與 hello 傳統的磁碟區之後可以從 Azure 的備份與 hello 系統中移除。</span><span class="sxs-lookup"><span data-stu-id="9ad87-269">• Once all hello legacy volumes are deleted from hello old storage, hello disk can be removed from Azure backup and hello system.</span></span>
<span data-ttu-id="9ad87-270">• 進行 hello Azure DPMDB 的備份。</span><span class="sxs-lookup"><span data-stu-id="9ad87-270">• Take a backup of hello  Azure DPMDB.</span></span>

<span data-ttu-id="9ad87-271">第 2 部分:-重要的項目 > hello 新伺服器將需要 toobe 為 hello 原始的 Azure 備份伺服器名稱相同。</span><span class="sxs-lookup"><span data-stu-id="9ad87-271">Part 2: -Important items> hello new server will need toobe named same as hello original Azure Backup server.</span></span> <span data-ttu-id="9ad87-272">如果您想 toouse 舊的存放集區和 DPMDB tooretain 復原點-必須有 DPMDB 備份，因為它必須 toobe 還原，您無法變更 hello hello 新的 Azure 備份伺服器名稱</span><span class="sxs-lookup"><span data-stu-id="9ad87-272">You cannot change hello name of hello new Azure backup server if you want toouse old storage pool and DPMDB tooretain recovery points -Must have backup of DPMDB  as it will need toobe restored</span></span>

1) <span data-ttu-id="9ad87-273">關機 hello 原始的 Azure 備份伺服器，或起飛 hello 網路。</span><span class="sxs-lookup"><span data-stu-id="9ad87-273">Shutdown hello original Azure backup server or take it off hello wire.</span></span>
2) <span data-ttu-id="9ad87-274">重設 active directory 中的 hello 機器帳戶。</span><span class="sxs-lookup"><span data-stu-id="9ad87-274">Reset hello machine account in active directory.</span></span>
3) <span data-ttu-id="9ad87-275">安裝 Server 2016 新電腦上以及其 hello hello 原始的 Azure 備份伺服器機器名稱相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="9ad87-275">Install Server 2016 on new machine and name it hello same machine name as hello original Azure Backup server.</span></span>
4) <span data-ttu-id="9ad87-276">加入 hello 網域</span><span class="sxs-lookup"><span data-stu-id="9ad87-276">Join hello Domain</span></span>
5) <span data-ttu-id="9ad87-277">安裝 Azure 備份伺服器 V2 (從舊伺服器中移出 DPM 儲存集區並匯入)</span><span class="sxs-lookup"><span data-stu-id="9ad87-277">Install Azure Backup server V2 (Move DPM Storage pool disks from old server and import)</span></span>
6) <span data-ttu-id="9ad87-278">還原取自第 2 部分結束 DPMDB hello</span><span class="sxs-lookup"><span data-stu-id="9ad87-278">Restore hello DPMDB taken from end of part 2</span></span>
7) <span data-ttu-id="9ad87-279">將 hello 存放裝置連接從 hello 原始備份伺服器 toohello 新伺服器。</span><span class="sxs-lookup"><span data-stu-id="9ad87-279">Attach hello storage from hello original backup server toohello new server.</span></span>
8) <span data-ttu-id="9ad87-280">從 SQL 還原 hello DPMDB</span><span class="sxs-lookup"><span data-stu-id="9ad87-280">From SQL Restore hello DPMDB</span></span>
9) <span data-ttu-id="9ad87-281">新的伺服器 cd tooMicrosoft Azure 備份的系統管理員命令列安裝位置和 bin 資料夾</span><span class="sxs-lookup"><span data-stu-id="9ad87-281">From admin command line on new server cd tooMicrosoft Azure Backup install location and bin folder</span></span>

<span data-ttu-id="9ad87-282">路徑範例：C:\windows\system32>cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\\</span><span class="sxs-lookup"><span data-stu-id="9ad87-282">Path example: C:\windows\system32>cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\\</span></span>
<span data-ttu-id="9ad87-283">tooAzure 備份執行 DPMSYNC-SYNC</span><span class="sxs-lookup"><span data-stu-id="9ad87-283">tooAzure backup Run DPMSYNC -SYNC</span></span>

10) <span data-ttu-id="9ad87-284">執行 DPMSYNC-SYNC 附註如果加入了新磁碟 toohello DPM 存放集區而不需要移動 hello 舊的然後執行 DPMSYNC-Reallocatereplica</span><span class="sxs-lookup"><span data-stu-id="9ad87-284">Run DPMSYNC -SYNC Note If you have added NEW disks toohello DPM Storage pool instead of moving hello old ones, then run DPMSYNC -Reallocatereplica</span></span>

## <a name="new-powershell-cmdlets-in-v2"></a><span data-ttu-id="9ad87-285">v2 中的新 PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="9ad87-285">New PowerShell cmdlets in v2</span></span>

<span data-ttu-id="9ad87-286">當您在安裝 Azure 備份伺服器 v2 時，系統有兩個新的 Cmdlet 可供使用：</span><span class="sxs-lookup"><span data-stu-id="9ad87-286">When you install Azure Backup Server v2, two new cmdlets are available:</span></span> 
* [<span data-ttu-id="9ad87-287">Mount-DPMRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="9ad87-287">Mount-DPMRecoveryPoint</span></span>](https://technet.microsoft.com/library/mt787159.aspx)
* [<span data-ttu-id="9ad87-288">Dismount-DPMRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="9ad87-288">Dismount-DPMRecoveryPoint</span></span>](https://technet.microsoft.com/library/mt787158.aspx)

## <a name="next-steps"></a><span data-ttu-id="9ad87-289">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9ad87-289">Next steps</span></span>

<span data-ttu-id="9ad87-290">深入了解如何 tooprepare 您的伺服器或開始進行保護工作負載：</span><span class="sxs-lookup"><span data-stu-id="9ad87-290">Learn how tooprepare your server or begin protecting a workload:</span></span>
- [<span data-ttu-id="9ad87-291">準備備份伺服器工作負載</span><span class="sxs-lookup"><span data-stu-id="9ad87-291">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="9ad87-292">使用 VMware 伺服器的備份伺服器 tooback</span><span class="sxs-lookup"><span data-stu-id="9ad87-292">Use Backup Server tooback up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="9ad87-293">使用 SQL server 備份伺服器 tooback</span><span class="sxs-lookup"><span data-stu-id="9ad87-293">Use Backup Server tooback up SQL Server</span></span>](backup-azure-sql-mabs.md)
- [<span data-ttu-id="9ad87-294">在備份伺服器中使用新式備份儲存體</span><span class="sxs-lookup"><span data-stu-id="9ad87-294">Use Modern Backup Storage with Backup Server</span></span>](backup-mabs-add-storage.md)

