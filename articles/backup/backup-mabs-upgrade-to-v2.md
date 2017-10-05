---
title: "安裝 Azure 備份伺服器 v2 | Microsoft Docs"
description: "Azure 備份伺服器 v2 可提供您經過強化的備份功能，讓您保護 VM、檔案和資料夾以及工作負載等項目。 了解如何安裝或升級為 Azure 備份伺服器 v2。"
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
ms.openlocfilehash: 1bbb16afef7940933b4c3ae23873f212770137e0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="install-azure-backup-server-v2"></a><span data-ttu-id="b1eb6-104">安裝 Azure 備份伺服器 v2</span><span class="sxs-lookup"><span data-stu-id="b1eb6-104">Install Azure Backup Server v2</span></span>

<span data-ttu-id="b1eb6-105">Azure 備份伺服器可協助保護您的虛擬機器 (VM)、工作負載以及檔案和資料夾等項目。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-105">Azure Backup Server helps protect your virtual machines (VMs), workloads, files and folders, and more.</span></span> <span data-ttu-id="b1eb6-106">Azure 備份伺服器 v2 是以 Azure 備份伺服器 v1 作為建置基礎，並可提供您 v1 所沒有的新功能。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-106">Azure Backup Server v2 builds on Azure Backup Server v1, and gives you new features that are not available in v1.</span></span> <span data-ttu-id="b1eb6-107">如需 v1 和 v2 的功能比較，請參閱 [Azure 備份伺服器保護對照表](backup-mabs-protection-matrix.md)。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-107">For a comparison of features between v1 and v2, see [Azure Backup Server protection matrix](backup-mabs-protection-matrix.md).</span></span> 

<span data-ttu-id="b1eb6-108">備份伺服器 v2 中新增的功能是備份伺服器 v1 的升級。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-108">The additional features in Backup Server v2 are an upgrade from Backup Server v1.</span></span> <span data-ttu-id="b1eb6-109">不過，並非一定要有備份伺服器 v1 才能安裝備份伺服器 v2。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-109">However, Backup Server v1 is not a prerequisite for installing Backup Server v2.</span></span> <span data-ttu-id="b1eb6-110">如果您想要從備份伺服器 v1 升級為備份伺服器 v2，請在備份伺服器保護伺服器上安裝備份伺服器 v2。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-110">If you want to upgrade from Backup Server v1 to Backup Server v2, install Backup Server v2 on the Backup Server protection server.</span></span> <span data-ttu-id="b1eb6-111">您現有的備份伺服器設定會保持不變。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-111">Your existing Backup Server settings remain intact.</span></span>

<span data-ttu-id="b1eb6-112">您可以在 Windows Server 2012 R2 或 Windows Server 2016 上安裝備份伺服器 v2。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-112">You can install Backup Server v2 on Windows Server 2012 R2 or Windows Server 2016.</span></span> <span data-ttu-id="b1eb6-113">若要利用新功能 (例如 System Center 2016 Data Protection Manager 的新式備份儲存體)，您必須在 Windows Server 2016 上安裝備份伺服器 v2。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-113">To take advantage of new features like System Center 2016 Data Protection Manager Modern Backup Storage, you must install Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="b1eb6-114">在安裝或升級為備份伺服器 v2 之前，請先閱讀[安裝必要條件](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-114">Before you upgrade to or install Backup Server v2, read about the [installation prerequisites](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites).</span></span>

> [!NOTE]
> <span data-ttu-id="b1eb6-115">Azure 備份伺服器具有和 System Center Data Protection Manager 一樣的程式碼基底。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-115">Azure Backup Server has the same code base as System Center Data Protection Manager.</span></span> <span data-ttu-id="b1eb6-116">備份伺服器 v1 相當於 Data Protection Manager 2012 R2，備份伺服器 v2 則相當於 Data Protection Manager 2016。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-116">Backup Server v1 is equivalent to Data Protection Manager 2012 R2, and Backup Server v2 is equivalent to Data Protection Manager 2016.</span></span> <span data-ttu-id="b1eb6-117">本文偶爾會參考 Data Protection Manager 文件。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-117">This article occasionally references the Data Protection Manager documentation.</span></span>
>
>

## <a name="upgrade-backup-server-to-v2"></a><span data-ttu-id="b1eb6-118">將備份伺服器升級為 v2</span><span class="sxs-lookup"><span data-stu-id="b1eb6-118">Upgrade Backup Server to v2</span></span>
<span data-ttu-id="b1eb6-119">若要從備份伺服器 v1 升級為備份伺服器 v2，請確定您的安裝具有所需更新：</span><span class="sxs-lookup"><span data-stu-id="b1eb6-119">To upgrade from Backup Server v1 to Backup Server v2, make sure your installation has the required updates:</span></span>

- <span data-ttu-id="b1eb6-120">在受保護的伺服器上[更新保護代理程式](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent)。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-120">[Update the protection agents](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent) on the protected servers.</span></span>
- <span data-ttu-id="b1eb6-121">將 Windows Server 2012 R2 升級為 Windows Server 2016。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-121">Upgrade Windows Server 2012 R2 to Windows Server 2016.</span></span>
- <span data-ttu-id="b1eb6-122">在所有生產伺服器上升級 Azure 備份伺服器遠端系統管理員。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-122">Upgrade Azure Backup Server Remote Administrator on all production servers.</span></span>
- <span data-ttu-id="b1eb6-123">確定備份已設定為繼續執行而不要重新啟動生產伺服器。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-123">Ensure that backups are set to continue without restarting your production server.</span></span>


### <a name="upgrade-steps-for-backup-server-v2"></a><span data-ttu-id="b1eb6-124">備份伺服器 v2 的升級步驟</span><span class="sxs-lookup"><span data-stu-id="b1eb6-124">Upgrade steps for Backup Server v2</span></span>

1. <span data-ttu-id="b1eb6-125">在下載中心[下載升級安裝程式](https://go.microsoft.com/fwlink/?LinkId=626082)。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-125">In the Download Center, [download the upgrade installer](https://go.microsoft.com/fwlink/?LinkId=626082).</span></span>

2. <span data-ttu-id="b1eb6-126">在將設定精靈解壓縮之後，先確定您已選取 [執行 setup.exe]，再選取 [完成]。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-126">After you extract the setup wizard, make sure that **Execute setup.exe** is selected, and then select **Finish**.</span></span>

  ![設定安裝程式 - 執行設定](./media/backup-mabs-upgrade-to-v2/run-setup.png)

3. <span data-ttu-id="b1eb6-128">在 Microsoft Azure 備份伺服器精靈的 [安裝] 底下，選取 [Microsoft Azure 備份伺服器]。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-128">In the Microsoft Azure Backup Server wizard, under **Install**, select **Microsoft Azure Backup Server**.</span></span>

  ![設定安裝程式 - 選取安裝](./media/backup-mabs-upgrade-to-v2/mabs-installer-s1.png)

4. <span data-ttu-id="b1eb6-130">在 [歡迎使用] 頁面上檢閱警告，然後選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-130">On the **Welcome** page, review the warnings, and then select **Next**.</span></span>

  ![設定安裝程式 - [歡迎使用] 頁面](./media/backup-mabs-upgrade-to-v2/mabs-installer-s2.png)

5. <span data-ttu-id="b1eb6-132">設定精靈會執行必要條件檢查以確定您的環境是否可以升級。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-132">The setup wizard performs prerequisite checks to make sure your environment can upgrade.</span></span> <span data-ttu-id="b1eb6-133">在 [必要條件檢查] 頁面上，選取 [檢查]。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-133">On the **Prerequisite Checks** page, select **Check**.</span></span>

  ![設定安裝程式 - [必要條件檢查] 頁面](./media/backup-mabs-upgrade-to-v2/mabs-installer-s3-perform-checks.png)

6. <span data-ttu-id="b1eb6-135">您的環境必須通過必要條件檢查。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-135">Your environment must pass the prerequisite checks.</span></span> <span data-ttu-id="b1eb6-136">如果您的環境未通過檢查，請記下所發生的問題，並加以修正。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-136">If your environment doesn't pass the checks, note the issues and fix them.</span></span> <span data-ttu-id="b1eb6-137">然後，選取 [再檢查一次]。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-137">Then, select **Check Again**.</span></span> <span data-ttu-id="b1eb6-138">通過必要條件檢查之後，選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-138">After you pass the prerequisite checks, select **Next**.</span></span>

  ![設定安裝程式 - [再檢查一次] 按鈕](./media/backup-mabs-upgrade-to-v2/mabs-installer-s4-pass-checks.png)

7. <span data-ttu-id="b1eb6-140">在 [SQL 設定] 頁面上，選取 SQL 安裝的相關選項，然後選取 [檢查並安裝]。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-140">On the **SQL Settings** page, select the relevant option for your SQL installation, and then select **Check and Install**.</span></span>

  ![設定安裝程式 - [SQL 設定] 頁面](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5-sql-settings.png)

  <span data-ttu-id="b1eb6-142">檢查可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-142">The checks might take a few minutes.</span></span> <span data-ttu-id="b1eb6-143">檢查完畢後，選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-143">When the checks are finished, select **Next**.</span></span>

  ![設定安裝程式 - [SQL 設定] 的 [檢查並安裝] 按鈕](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5a-check-and fix-settings.png)

8. <span data-ttu-id="b1eb6-145">在 [安裝設定] 頁面上，對備份伺服器安裝所在的位置或臨時位置進行任何變更。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-145">On the **Installation Settings** page, make any changes to the location where Backup Server is installed, or to the Scratch Location.</span></span> <span data-ttu-id="b1eb6-146">選取 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-146">Select **Next**.</span></span>

  ![設定安裝程式 - [安裝設定] 頁面](./media/backup-mabs-upgrade-to-v2/mabs-installer-s6-installation-settings.png)

9. <span data-ttu-id="b1eb6-148">若要完成設定精靈，請選取 [完成]。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-148">To finish the setup wizard, select **Finish**.</span></span>

  ![設定安裝程式 - 完成](./media/backup-mabs-upgrade-to-v2/run-setup.png)



## <a name="add-storage-for-modern-backup-storage"></a><span data-ttu-id="b1eb6-150">為新式備份儲存體新增儲存體</span><span class="sxs-lookup"><span data-stu-id="b1eb6-150">Add storage for Modern Backup Storage</span></span>

<span data-ttu-id="b1eb6-151">為了提升備份儲存體效率，備份伺服器 v2 新增了磁碟區支援。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-151">To improve backup storage efficiency, Backup Server v2 adds support for volumes.</span></span> <span data-ttu-id="b1eb6-152">和備份伺服器 v1 一樣，備份伺服器 v2 也支援磁碟。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-152">Like Backup Server v1, Backup Server v2 supports disks.</span></span>

### <a name="add-volumes-and-disks"></a><span data-ttu-id="b1eb6-153">新增磁碟區和磁碟</span><span class="sxs-lookup"><span data-stu-id="b1eb6-153">Add volumes and disks</span></span>
<span data-ttu-id="b1eb6-154">如果您在 Windows Server 2016 上執行備份伺服器 v2，您可以使用磁碟區來儲存備份資料。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-154">If you run Backup Server v2 on Windows Server 2016, you can use volumes to store backup data.</span></span> <span data-ttu-id="b1eb6-155">磁碟區可節省儲存空間並提高備份速度。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-155">Volumes offer storage savings and faster backups.</span></span> <span data-ttu-id="b1eb6-156">磁碟區是備份伺服器的新功能，因此您必須新增磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-156">Because volumes are new to Backup Server, you must add them.</span></span> 

<span data-ttu-id="b1eb6-157">當您在備份伺服器中新增磁碟區時，您可以讓磁碟區有個好記的名稱。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-157">When you add a volume to Backup Server, you can give the volume a friendly name.</span></span> <span data-ttu-id="b1eb6-158">對您想要命名的磁碟區按一下 [易記名稱] 資料行。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-158">Click the **Friendly Name** column of the volume you want to name.</span></span> <span data-ttu-id="b1eb6-159">如有必要，您可於稍後變更名稱。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-159">You can change the name later, if necessary.</span></span> <span data-ttu-id="b1eb6-160">您也可以使用 PowerShell 來新增或變更磁碟區的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-160">You also can use PowerShell to add or change friendly names for volumes.</span></span>

<span data-ttu-id="b1eb6-161">若要在管理員主控台中新增磁碟區：</span><span class="sxs-lookup"><span data-stu-id="b1eb6-161">To add a volume in the Administrator Console:</span></span>

1. <span data-ttu-id="b1eb6-162">在 Azure 備份伺服器管理員主控台中，選取 [管理] > [磁碟儲存體] > [新增]。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-162">In the Azure Backup Server Administrator Console, select **Management** > **Disk Storage** > **Add**.</span></span>

    ![開啟「新增磁碟儲存體」精靈](./media//backup-mabs-upgrade-to-v2/open-add-disk-storage-wizard.png)

    <span data-ttu-id="b1eb6-164">這會開啟「新增磁碟儲存體」精靈。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-164">This opens the Add Disk Storage wizard.</span></span>

2. <span data-ttu-id="b1eb6-165">在 [新增磁碟儲存體] 頁面上，於 [可用磁碟區] 方塊中選取磁碟區，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-165">On the **Add Disk Storage** page, in the **Available volumes** box, select a volume, and then select **Add**.</span></span>
3. <span data-ttu-id="b1eb6-166">在 [已選取的磁碟區] 方塊中，為磁碟區輸入易記名稱，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-166">In the **Selected volumes** box, enter a friendly name for the volume, and then select **OK**.</span></span>

      ![新增磁碟儲存體精靈 - 新增磁碟區](./media/backup-mabs-upgrade-to-v2/add-volume.png)

  <span data-ttu-id="b1eb6-168">如果您想要新增磁碟，該磁碟必須屬於具有舊式儲存體的保護群組。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-168">If you want to add a disk, the disk must belong to a protection group that has legacy storage.</span></span> <span data-ttu-id="b1eb6-169">這些磁碟僅能用於這些保護群組。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-169">These disks can only be used for these protection groups.</span></span> <span data-ttu-id="b1eb6-170">如果備份伺服器所擁有的來源並沒有舊式保護功能，則磁碟不會列出。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-170">If Backup Server doesn't have sources that have legacy protection, the disk isn't listed.</span></span>

  <span data-ttu-id="b1eb6-171">如需新增磁碟的詳細資訊，請參閱[新增磁碟以增加舊式儲存體](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage)。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-171">For more information about adding disks, see [Adding disks to increase legacy storage](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage).</span></span> <span data-ttu-id="b1eb6-172">您不能對磁碟賦予易記名稱。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-172">You can't give a disk a friendly name.</span></span>


### <a name="assign-workloads-to-volumes"></a><span data-ttu-id="b1eb6-173">將工作負載指派給磁碟區</span><span class="sxs-lookup"><span data-stu-id="b1eb6-173">Assign workloads to volumes</span></span>

<span data-ttu-id="b1eb6-174">在備份伺服器中，您會指定要將哪些工作負載指派給哪些磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-174">In Backup Server, you specify which workloads are assigned to which volumes.</span></span> <span data-ttu-id="b1eb6-175">例如，您可以將支援大量每秒輸入/輸出作業 (IOPS) 的高度耗費資源磁碟區，設定為僅儲存需要頻繁且大量備份的工作負載。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-175">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) to store only workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="b1eb6-176">舉例來說，具有交易記錄的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-176">An example is SQL Server with transaction logs.</span></span>

#### <a name="update-dpmdiskstorage"></a><span data-ttu-id="b1eb6-177">Update-DPMDiskStorage</span><span class="sxs-lookup"><span data-stu-id="b1eb6-177">Update-DPMDiskStorage</span></span>

<span data-ttu-id="b1eb6-178">若要更新備份伺服器儲存集區磁碟區的屬性，請使用 PowerShell Cmdlet Update-DPMDiskStorage。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-178">To update the properties of a volume in the storage pool in Backup Server, use the PowerShell cmdlet Update-DPMDiskStorage.</span></span>

<span data-ttu-id="b1eb6-179">語法：</span><span class="sxs-lookup"><span data-stu-id="b1eb6-179">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

<span data-ttu-id="b1eb6-180">您使用 PowerShell 所進行的變更都會反映在 UI 中。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-180">All changes that you make by using PowerShell are reflected in the UI.</span></span>


## <a name="protect-data-sources"></a><span data-ttu-id="b1eb6-181">保護資料來源</span><span class="sxs-lookup"><span data-stu-id="b1eb6-181">Protect data sources</span></span>
<span data-ttu-id="b1eb6-182">若要開始保護資料來源，請建立保護群組。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-182">To begin protecting data sources, create a protection group.</span></span> <span data-ttu-id="b1eb6-183">下列步驟會特別指出「新增保護群組」精靈中有變更或新增的地方。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-183">The following steps highlight changes or additions to the New Protection Group wizard.</span></span>

<span data-ttu-id="b1eb6-184">若要建立保護群組：</span><span class="sxs-lookup"><span data-stu-id="b1eb6-184">To create a protection group:</span></span>

1. <span data-ttu-id="b1eb6-185">在備份伺服器管理員主控台中選取 [保護]。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-185">In the Backup Server Administrator Console, select **Protection**.</span></span>

2. <span data-ttu-id="b1eb6-186">在工具功能區中選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-186">On the tool ribbon, select **New**.</span></span>

    <span data-ttu-id="b1eb6-187">這會開啟「建立新保護群組」精靈。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-187">This opens the Create New Protection Group wizard.</span></span>

  ![建立新保護群組精靈](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-1.png)

3. <span data-ttu-id="b1eb6-189">在 [歡迎] 頁面上，選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-189">On the **Welcome** page, select **Next**.</span></span>
4. <span data-ttu-id="b1eb6-190">在 [選取保護群組類型] 頁面上，選取您要建立的保護群組類型，然後選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-190">On the **Select Protection Group Type** page, select the type of protection group you want to create, and then select **Next**.</span></span>

  ![[選取保護群組類型] 頁面](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-2.png)

5. <span data-ttu-id="b1eb6-192">[選取群組成員] 頁面上的 [可用成員] 窗格中會列出具有保護代理程式的成員。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-192">On the **Select Group Members** page, in the **Available members** pane, the members with protection agents are listed.</span></span> <span data-ttu-id="b1eb6-193">在此範例中，選取磁碟區 D:\ 和 E:\，並將其新增至 [已選取的成員] 窗格。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-193">For this example, select volume D:\ and E:\ and add them to the **Selected members** pane.</span></span> <span data-ttu-id="b1eb6-194">選取 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-194">Select **Next**.</span></span>

  ![[選取群組成員] 頁面](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-3.png)

6. <span data-ttu-id="b1eb6-196">在 [選取資料保護方式] 頁面上輸入**保護群組名稱**，選取保護方式，然後選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-196">On the **Select Data Protection Method** page, enter a **Protection group name**, select the protection method, and then select **Next**.</span></span> <span data-ttu-id="b1eb6-197">如果您想要短期保護，則必須選取 [磁碟] 備份方式。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-197">If you want short-term protection, you must select the **Disk** backup method.</span></span>

  ![[選取資料保護方式] 頁面](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-4.png)

7. <span data-ttu-id="b1eb6-199">在 [指定短期目標] 頁面上，選取 [保留範圍] 和 [同步處理頻率] 的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-199">On the **Specify Short-Term Goals** page, select the details for **Retention range** and **Synchronization frequency**.</span></span> <span data-ttu-id="b1eb6-200">然後，選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-200">Then, select **Next**.</span></span> <span data-ttu-id="b1eb6-201">(選擇性) 若要變更復原點的擷取排程，請選取 [修改]。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-201">Optionally, to change the schedule for when recovery points are taken, select **Modify**.</span></span>

  ![[指定短期目標] 頁面](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-5.png)

8. <span data-ttu-id="b1eb6-203">在 [檢閱磁碟儲存體配置] 頁面上，檢閱您所選取之資料來源的詳細資料、其大小，以及要佈建的空間值和目標儲存體磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-203">On the **Review Disk Storage Allocation** page, review details about the data sources you selected, their size, and  values for the space to be provisioned and the target storage volume.</span></span>

  ![[檢閱磁碟儲存體配置] 頁面](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-6.png)

  <span data-ttu-id="b1eb6-205">儲存體磁碟區是以工作負載磁碟區配置 (使用 PowerShell 來設定) 和可用儲存體為基礎。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-205">Storage volumes are based on the workload volume allocation (set by using PowerShell) and the available storage.</span></span> <span data-ttu-id="b1eb6-206">您可以在下拉式功能表中選取其他磁碟區來變更儲存體磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-206">You can change the storage volumes by selecting other volumes in the drop-down menu.</span></span> <span data-ttu-id="b1eb6-207">如果您變更 [目標儲存體] 的值，[可用磁碟儲存體] 的值會動態變更，以反映 [可用空間] 和 [佈建不足的空間] 底下的值。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-207">If you change the value for **Target Storage**, the value for **Available disk storage** dynamically changes to reflect values under **Free Space** and **Underprovisioned Space**.</span></span>

  <span data-ttu-id="b1eb6-208">如果資料來源按計劃成長，[可用磁碟儲存體] 中的 [佈建不足的空間] 資料行的值會反映另外需要的儲存體數量。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-208">If the data sources grow as planned, the value for the **Underprovisioned Space** column in **Available disk storage** reflects the amount of additional storage that's needed.</span></span> <span data-ttu-id="b1eb6-209">請使用此值來協助規劃您的儲存需求，以便順利進行備份。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-209">Use this value to help plan your storage needs for smooth backups.</span></span> <span data-ttu-id="b1eb6-210">如果值為零，則在可預見的未來將不可能發生任何儲存問題。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-210">If the value is zero, there are no potential problems with storage in the foreseeable future.</span></span> <span data-ttu-id="b1eb6-211">如果值為零以外的數字，則表示所配置的儲存體不足 (根據您的保護原則和受保護成員的資料大小)。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-211">If the value is a number other than zero, you do not have sufficient storage allocated  (based on your protection policy and the data size of your protected members).</span></span>

  ![配置不足的磁碟儲存體](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-7.png)

   <span data-ttu-id="b1eb6-213">若要完成保護群組的建立，請完成精靈。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-213">To finish creating your protection group, complete the wizard.</span></span>

## <a name="migrate-legacy-storage-to-modern-backup-storage"></a><span data-ttu-id="b1eb6-214">將舊式儲存體移轉至新式備份儲存體</span><span class="sxs-lookup"><span data-stu-id="b1eb6-214">Migrate legacy storage to Modern Backup Storage</span></span>
<span data-ttu-id="b1eb6-215">在安裝或升級為備份伺服器 v2，並將作業系統升級為 Windows Server 2016 之後，請將您的保護群組更新為使用新式備份儲存體。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-215">After you upgrade to or install Backup Server v2 and upgrade the operating system to Windows Server 2016, update your protection groups to use Modern Backup Storage.</span></span> <span data-ttu-id="b1eb6-216">根據預設，系統不會變更保護群組。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-216">By default, protection groups are not changed.</span></span> <span data-ttu-id="b1eb6-217">保護群組會繼續依照一開始的設定方式運作。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-217">They continue to function as they were initially set up.</span></span> 

<span data-ttu-id="b1eb6-218">您可以選擇是否將保護群組更新為使用新式備份儲存體。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-218">Updating protection groups to use Modern Backup Storage is optional.</span></span> <span data-ttu-id="b1eb6-219">若要更新保護群組，請使用保留資料選項來停止保護所有資料來源。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-219">To update the protection group, stop protection of all data sources by using the retain data option.</span></span> <span data-ttu-id="b1eb6-220">然後，將資料來源新增至新的保護群組。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-220">Then, add the data sources to a new protection group.</span></span>

1. <span data-ttu-id="b1eb6-221">在管理員主控台中選取 [保護] 功能。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-221">In the Administrator Console, select the **Protection** feature.</span></span> <span data-ttu-id="b1eb6-222">在 [保護群組成員] 清單中，以滑鼠右鍵按一下成員，然後選取 [停止保護成員]。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-222">In the **Protection Group Member** list, right-click the member, and then select **Stop protection of member**.</span></span>

  ![停止保護成員](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-stop-protection1.png)

2. <span data-ttu-id="b1eb6-224">在 [從群組中移除] 對話方塊中，檢閱儲存集區中已使用的磁碟空間和可用空間。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-224">In the **Remove from Group** dialog box, review the used disk space and the available free space for the storage pool.</span></span> <span data-ttu-id="b1eb6-225">預設值是讓復原點留在磁碟上，並讓復原點按照所關聯的保留原則來到期。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-225">The default is to leave the recovery points on the disk and allow them to expire per their associated retention policy.</span></span> <span data-ttu-id="b1eb6-226">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-226">Click **OK**.</span></span>

  <span data-ttu-id="b1eb6-227">如果您想要立即將已使用的磁碟空間歸還給可用的儲存集區，請選取 [刪除磁碟上的複本] 核取方塊，以刪除與該成員相關聯的備份資料 (與復原點)。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-227">If you want to immediately return the used disk space to the free storage pool, select the **Delete replica on disk** check box to delete the backup data (and recovery points) associated with that member.</span></span>

  ![[從群組中移除] 對話方塊](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-retain-data.png)

3. <span data-ttu-id="b1eb6-229">建立使用新式備份儲存體的保護群組。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-229">Create a protection group that uses Modern Backup Storage.</span></span> <span data-ttu-id="b1eb6-230">納入未受保護的資料來源。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-230">Include the unprotected data sources.</span></span>


## <a name="add-disks-to-increase-legacy-storage"></a><span data-ttu-id="b1eb6-231">新增磁碟以增加舊式儲存體</span><span class="sxs-lookup"><span data-stu-id="b1eb6-231">Add disks to increase legacy storage</span></span>

<span data-ttu-id="b1eb6-232">如果您想要在備份伺服器中使用舊式儲存體，您可能需要新增磁碟以增加舊式儲存體。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-232">If you want to use legacy storage with Backup Server, you might need to add disks to increase legacy storage.</span></span> 

<span data-ttu-id="b1eb6-233">若要新增磁碟儲存體：</span><span class="sxs-lookup"><span data-stu-id="b1eb6-233">To add disk storage:</span></span>

1. <span data-ttu-id="b1eb6-234">在管理員主控台中，選取 [管理] > [磁碟儲存體] > [新增]。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-234">In the Administrator Console, select **Management** > **Disk Storage** > **Add**.</span></span>

    ![[新增磁碟儲存體] 對話方塊](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-add-disk-storage.png)

4. <span data-ttu-id="b1eb6-236">在 [新增磁碟儲存體] 對話方塊中選取 [新增磁碟]。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-236">In the **Add Disk Storage** dialog, select **Add disks**.</span></span>

5. <span data-ttu-id="b1eb6-237">在可用磁碟清單中選取您要新增的磁碟，選取 [新增]，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-237">In the list of available disks, select the disks you want to add, select **Add**, and then select **OK**.</span></span>

## <a name="update-the-data-protection-manager-protection-agent"></a><span data-ttu-id="b1eb6-238">升級 Data Protection Manager 保護代理程式</span><span class="sxs-lookup"><span data-stu-id="b1eb6-238">Update the Data Protection Manager protection agent</span></span>

<span data-ttu-id="b1eb6-239">備份伺服器會使用 System Center Data Protection Manager 保護代理程式來進行更新。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-239">Backup Server uses the System Center Data Protection Manager protection agent for updates.</span></span> <span data-ttu-id="b1eb6-240">如果您要升級的保護代理程式未連線到網路，您將無法使用 Data Protection Manager 管理員主控台來完成已連線代理程式的升級。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-240">If you are upgrading a protection agent that is not connected to the network, you cannot use the Data Protection Manager Administrator Console to complete a connected agent upgrade.</span></span> <span data-ttu-id="b1eb6-241">您必須在非作用中的網域環境升級保護代理程式。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-241">You must upgrade the protection agent in a nonactive domain environment.</span></span> <span data-ttu-id="b1eb6-242">在用戶端電腦連線到網路之前，Data Protection Manager 管理員主控台會顯示保護代理程式更新受到擱置。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-242">Until the client computer is connected to the network, the Data Protection Manager Administrator Console shows that the protection agent update is pending.</span></span>

<span data-ttu-id="b1eb6-243">下列幾節會說明如何更新已連線用戶端電腦和未連線用戶端電腦的保護代理程式。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-243">The following sections describe how to update protection agents for client computers that are connected and client computers that are not connected.</span></span>

### <a name="update-a-protection-agent-for-a-connected-client-computer"></a><span data-ttu-id="b1eb6-244">更新已連線用戶端電腦的保護代理程式</span><span class="sxs-lookup"><span data-stu-id="b1eb6-244">Update a protection agent for a connected client computer</span></span>

1. <span data-ttu-id="b1eb6-245">在備份伺服器管理員主控台中選取 [管理] > [代理程式]。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-245">In the Backup Server Administrator Console, select **Management** > **Agents**.</span></span>

2. <span data-ttu-id="b1eb6-246">在顯示窗格中，選取您要更新保護代理程式的用戶端電腦。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-246">In the display pane, select the client computers for which you want to update the protection agent.</span></span>

  > [!NOTE]
  > <span data-ttu-id="b1eb6-247">[代理程式更新] 資料行會在各個受保護的電腦可以進行保護代理程式更新時予以指出。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-247">The **Agent Updates** column indicates when a protection agent update is available for each protected computer.</span></span> <span data-ttu-id="b1eb6-248">在 [動作] 窗格中，只有當您已選取受保護的電腦且其可供更新時，才可使用 [更新] 動作。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-248">In the **Actions** pane, the **Update** action is available only when a protected computer is selected and updates are available.</span></span>
  >
  >

3. <span data-ttu-id="b1eb6-249">若要在選取的電腦上安裝已更新的保護代理程式，請在 [動作] 窗格中選取 [更新]。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-249">To install updated protection agents on the selected computers, in the **Actions** pane, select **Update**.</span></span>

### <a name="update-a-protection-agent-on-a-client-computer-that-is-not-connected"></a><span data-ttu-id="b1eb6-250">在未連線用戶端電腦上更新保護代理程式</span><span class="sxs-lookup"><span data-stu-id="b1eb6-250">Update a protection agent on a client computer that is not connected</span></span>

1. <span data-ttu-id="b1eb6-251">在備份伺服器管理員主控台中選取 [管理] > [代理程式]。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-251">In the Backup Server Administrator Console, select **Management** > **Agents**.</span></span>

2. <span data-ttu-id="b1eb6-252">在顯示窗格中，選取您要更新保護代理程式的用戶端電腦。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-252">In the display pane, select the client computers for which you want to update the protection agent.</span></span>

  > [!NOTE]
   > <span data-ttu-id="b1eb6-253">[代理程式更新] 資料行會在各個受保護的電腦可以進行保護代理程式更新時予以指出。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-253">The **Agent Updates** column indicates when a protection agent update is available for each protected computer.</span></span> <span data-ttu-id="b1eb6-254">在 [動作] 窗格中，除非已選取的受保護電腦可供更新，否則您無法使用 [更新] 動作。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-254">In the **Actions** pane, the **Update** action is not available when a protected computer is selected unless updates are available.</span></span>
  >
  >

3. <span data-ttu-id="b1eb6-255">若要在選取的電腦上安裝已更新的保護代理程式，請選取 [更新]。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-255">To install updated protection agents on the selected computers, select **Update**.</span></span>

4. <span data-ttu-id="b1eb6-256">對於未連線到網路的用戶端電腦，除非該電腦連線到網路，否則 [代理程式狀態] 資料行會顯示 [更新擱置中] 的狀態。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-256">For a client computer that is not connected to the network, until the computer is connected to the network, the **Agent Status** column shows a status of **Update Pending**.</span></span>

  <span data-ttu-id="b1eb6-257">在用戶端電腦連線到網路之後，用戶端電腦的 [代理程式更新] 資料行會顯示 [更新中] 狀態。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-257">After a client computer is connected to the network, the **Agent Updates** column for the client computer shows a status of **Updating**.</span></span>
  
### <a name="move-legacy-protection-groups-from-old-version-and-sync-the-new-version-with-azure"></a><span data-ttu-id="b1eb6-258">將舊版保護群組從舊版本中移出，並透過 Azure 同步處理新版本</span><span class="sxs-lookup"><span data-stu-id="b1eb6-258">Move legacy Protection groups from old version and sync the new version with Azure</span></span>

<span data-ttu-id="b1eb6-259">一旦更新 Azure 備份伺服器與 OS，您就可以使用新式備份儲存體來保護新的資料來源。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-259">Once Azure Backup Server and the OS are both updated, you are ready to protect new data sources using Modern Backup Storage.</span></span> <span data-ttu-id="b1eb6-260">不過，已受保護的資料來源會繼續在舊版中受到保護 (如同在 Azure 備份伺服器中一樣)，但所有新的保護將使用新式備份儲存體。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-260">However already protected data sources will continue to be protected in the legacy way as they were in Azure Backup Server but all new protection will use Modern Backup Storage.</span></span>

<span data-ttu-id="b1eb6-261">下列步驟會將資料來源從傳統的保護模式移轉到新式備份儲存體。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-261">Below steps are to migrate data sources from legacy  mode of protection to Modern backup storage.</span></span>

<span data-ttu-id="b1eb6-262">• 將新磁碟區新增到 DPM 儲存集區，並視需要指派易記的名稱和資料來源標籤。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-262">• Add the new volume(s) to the DPM storage pool and assign friendly names and data source tags if desired.</span></span>
<span data-ttu-id="b1eb6-263">• 對於傳統模式下的每個資料來源，停止資料來源保護並「保留受保護的資料」。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-263">• For each data source that is in legacy mode, stop protection of the data sources and “Retain Protected Data”.</span></span>  <span data-ttu-id="b1eb6-264">這允許在移轉之後復原舊的復原點。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-264">This will allow recovery of old recovery points after migration.</span></span>

<span data-ttu-id="b1eb6-265">• 建立新的 PG，然後選取要使用新格式儲存的資料來源。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-265">• Create a new PG and select the data sources that are to be stored using new format.</span></span>
<span data-ttu-id="b1eb6-266">• DPM 將在本機執行從舊版備份儲存體到新式備份儲存體磁碟區的複本複製。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-266">• DPM will do a replica copy from the legacy backup storage into the Modern Backup Storage volume locally.</span></span>
<span data-ttu-id="b1eb6-267">注意：這會被視為復原後作業 • 所有新的同步處理和復原點則會儲存在新式備份儲存體中。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-267">Note: This will be seen as a post-recovery operation job • All new sync and recovery points will then be stored in Modern Backup Storage.</span></span>
<span data-ttu-id="b1eb6-268">• 舊的復原點將在過期時剪除，最終會釋出磁碟空間。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-268">• Old recovery points will be pruned out as they expire and eventually free up the disk space.</span></span>
<span data-ttu-id="b1eb6-269">• 從舊儲存體中刪除所有舊式磁碟區後，就可以從 Azure 備份和系統中移除磁碟。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-269">• Once all the legacy volumes are deleted from the old storage, the disk can be removed from Azure backup and the system.</span></span>
<span data-ttu-id="b1eb6-270">• 進行 Azure DPMDB 的備份。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-270">• Take a backup of the  Azure DPMDB.</span></span>

<span data-ttu-id="b1eb6-271">第 2 部分︰重要事項 -> 新伺服器的名稱必須與原始 Azure 備份伺服器相同。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-271">Part 2: -Important items> The new server will need to be named same as the original Azure Backup server.</span></span> <span data-ttu-id="b1eb6-272">如果您想要使用舊的儲存集區和 DPMDB 來保留復原點，則無法變更新 Azure 備份伺服器的名稱 - 必須具有 DPMDB 備份，因為必須將它還原</span><span class="sxs-lookup"><span data-stu-id="b1eb6-272">You cannot change the name of the new Azure backup server if you want to use old storage pool and DPMDB to retain recovery points -Must have backup of DPMDB  as it will need to be restored</span></span>

1) <span data-ttu-id="b1eb6-273">關閉原始 Azure 備份伺服器，或讓它離線。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-273">Shutdown the original Azure backup server or take it off the wire.</span></span>
2) <span data-ttu-id="b1eb6-274">在 Active Directory 中重設電腦帳戶。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-274">Reset the machine account in active directory.</span></span>
3) <span data-ttu-id="b1eb6-275">在新機器上安裝 Server 2016 並將它命名為與原始 Azure 備份伺服器相同的電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-275">Install Server 2016 on new machine and name it the same machine name as the original Azure Backup server.</span></span>
4) <span data-ttu-id="b1eb6-276">加入網域</span><span class="sxs-lookup"><span data-stu-id="b1eb6-276">Join the Domain</span></span>
5) <span data-ttu-id="b1eb6-277">安裝 Azure 備份伺服器 V2 (從舊伺服器中移出 DPM 儲存集區並匯入)</span><span class="sxs-lookup"><span data-stu-id="b1eb6-277">Install Azure Backup server V2 (Move DPM Storage pool disks from old server and import)</span></span>
6) <span data-ttu-id="b1eb6-278">還原取自第 2 部分結尾的 DPMDB</span><span class="sxs-lookup"><span data-stu-id="b1eb6-278">Restore the DPMDB taken from end of part 2</span></span>
7) <span data-ttu-id="b1eb6-279">將原始備份伺服器的儲存體連結到新伺服器。</span><span class="sxs-lookup"><span data-stu-id="b1eb6-279">Attach the storage from the original backup server to the new server.</span></span>
8) <span data-ttu-id="b1eb6-280">從 SQL 還原 DPMDB</span><span class="sxs-lookup"><span data-stu-id="b1eb6-280">From SQL Restore the DPMDB</span></span>
9) <span data-ttu-id="b1eb6-281">從新伺服器上的系統管理員命令列，切換至 Microsoft Azure 備份安裝位置和 bin 資料夾</span><span class="sxs-lookup"><span data-stu-id="b1eb6-281">From admin command line on new server cd to Microsoft Azure Backup install location and bin folder</span></span>

<span data-ttu-id="b1eb6-282">路徑範例：C:\windows\system32>cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\\</span><span class="sxs-lookup"><span data-stu-id="b1eb6-282">Path example: C:\windows\system32>cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\\</span></span>
<span data-ttu-id="b1eb6-283">至 Azure 備份 執行 DPMSYNC -SYNC</span><span class="sxs-lookup"><span data-stu-id="b1eb6-283">to Azure backup Run DPMSYNC -SYNC</span></span>

10) <span data-ttu-id="b1eb6-284">執行 DPMSYNC -SYNC 注意 如果您已將「新」磁碟新增至 DPM 儲存集區，而非移動就磁碟，則執行 DPMSYNC -Reallocatereplica</span><span class="sxs-lookup"><span data-stu-id="b1eb6-284">Run DPMSYNC -SYNC Note If you have added NEW disks to the DPM Storage pool instead of moving the old ones, then run DPMSYNC -Reallocatereplica</span></span>

## <a name="new-powershell-cmdlets-in-v2"></a><span data-ttu-id="b1eb6-285">v2 中的新 PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="b1eb6-285">New PowerShell cmdlets in v2</span></span>

<span data-ttu-id="b1eb6-286">當您在安裝 Azure 備份伺服器 v2 時，系統有兩個新的 Cmdlet 可供使用：</span><span class="sxs-lookup"><span data-stu-id="b1eb6-286">When you install Azure Backup Server v2, two new cmdlets are available:</span></span> 
* [<span data-ttu-id="b1eb6-287">Mount-DPMRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="b1eb6-287">Mount-DPMRecoveryPoint</span></span>](https://technet.microsoft.com/library/mt787159.aspx)
* [<span data-ttu-id="b1eb6-288">Dismount-DPMRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="b1eb6-288">Dismount-DPMRecoveryPoint</span></span>](https://technet.microsoft.com/library/mt787158.aspx)

## <a name="next-steps"></a><span data-ttu-id="b1eb6-289">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b1eb6-289">Next steps</span></span>

<span data-ttu-id="b1eb6-290">了解如何準備您的伺服器或開始保護工作負載：</span><span class="sxs-lookup"><span data-stu-id="b1eb6-290">Learn how to prepare your server or begin protecting a workload:</span></span>
- [<span data-ttu-id="b1eb6-291">準備備份伺服器工作負載</span><span class="sxs-lookup"><span data-stu-id="b1eb6-291">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="b1eb6-292">使用備份伺服器來備份 VMware 伺服器</span><span class="sxs-lookup"><span data-stu-id="b1eb6-292">Use Backup Server to back up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="b1eb6-293">使用備份伺服器來備份 SQL Server</span><span class="sxs-lookup"><span data-stu-id="b1eb6-293">Use Backup Server to back up SQL Server</span></span>](backup-azure-sql-mabs.md)
- [<span data-ttu-id="b1eb6-294">在備份伺服器中使用新式備份儲存體</span><span class="sxs-lookup"><span data-stu-id="b1eb6-294">Use Modern Backup Storage with Backup Server</span></span>](backup-mabs-add-storage.md)

