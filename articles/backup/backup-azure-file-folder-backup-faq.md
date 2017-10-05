---
title: "Azure 備份代理程式常見問題集 | Microsoft Docs"
description: "有關以下常見問題的解答︰Azure 備份代理程式的運作方式、備份和保留限制。"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: "備份和災害復原; 備份服務"
ms.assetid: 778c6ccf-3e57-4103-a022-367cc60c411a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/18/2017
ms.author: trinadhk;pullabhk;
ms.openlocfilehash: 227cdc87f3e2c8ed393145f4bbde7f74606bdf3b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="questions-about-the-azure-backup-agent"></a><span data-ttu-id="be6d3-104">關於 Azure 備份代理程式的問題</span><span class="sxs-lookup"><span data-stu-id="be6d3-104">Questions about the Azure Backup agent</span></span>
<span data-ttu-id="be6d3-105">本文包含常見問題的解答，可協助您快速了解 Azure 備份代理程式元件。</span><span class="sxs-lookup"><span data-stu-id="be6d3-105">This article has answers to common questions to help you quickly understand the Azure Backup agent components.</span></span> <span data-ttu-id="be6d3-106">在某些答案中，有具有完整資訊的文章連結。</span><span class="sxs-lookup"><span data-stu-id="be6d3-106">In some of the answers, there are links to the articles that have comprehensive information.</span></span> <span data-ttu-id="be6d3-107">您也可以在 [論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup)中張貼有關 Azure 備份服務的問題。</span><span class="sxs-lookup"><span data-stu-id="be6d3-107">You can also post questions about the Azure Backup service in the [discussion forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).</span></span>

## <a name="configure-backup"></a><span data-ttu-id="be6d3-108">設定備份</span><span class="sxs-lookup"><span data-stu-id="be6d3-108">Configure backup</span></span>
### <a name="where-can-i-download-the-latest-azure-backup-agent-br"></a><span data-ttu-id="be6d3-109">哪裡可以下載最新的 Azure 備份代理程式？</span><span class="sxs-lookup"><span data-stu-id="be6d3-109">Where can I download the latest Azure Backup agent?</span></span> <br/>
<span data-ttu-id="be6d3-110">您可以下載最新的代理程式，以便從 [這裡](http://aka.ms/azurebackup_agent)備份 Windows Server、System Center DPM 或 Windows 用戶端。</span><span class="sxs-lookup"><span data-stu-id="be6d3-110">You can download the latest agent for backing up Windows Server, System Center DPM, or Windows client, from [here](http://aka.ms/azurebackup_agent).</span></span> <span data-ttu-id="be6d3-111">如果您想要備份虛擬機器，請使用 VM 代理程式 (這會自動安裝適當的擴充功能)。</span><span class="sxs-lookup"><span data-stu-id="be6d3-111">If you want to back up a virtual machine, use the VM Agent (which automatically installs the proper extension).</span></span> <span data-ttu-id="be6d3-112">從 Azure 資源庫建立的虛擬機器上已經有 VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="be6d3-112">The VM Agent is already present on virtual machines created from the Azure gallery.</span></span>

### <a name="when-configuring-the-azure-backup-agent-i-am-prompted-to-enter-the-vault-credentials-do-vault-credentials-expire"></a><span data-ttu-id="be6d3-113">當設定 Azure 備份代理程式時，系統提示我要輸入保存庫認證。</span><span class="sxs-lookup"><span data-stu-id="be6d3-113">When configuring the Azure Backup agent, I am prompted to enter the vault credentials.</span></span> <span data-ttu-id="be6d3-114">保存庫認證是否過期？</span><span class="sxs-lookup"><span data-stu-id="be6d3-114">Do vault credentials expire?</span></span>
<span data-ttu-id="be6d3-115">是，保存庫認證將於 48 小時後過期。</span><span class="sxs-lookup"><span data-stu-id="be6d3-115">Yes, the vault credentials expire after 48 hours.</span></span> <span data-ttu-id="be6d3-116">若檔案已過期，請登入 Azure 入口網站，並從您的保存庫下載保存庫認證檔。</span><span class="sxs-lookup"><span data-stu-id="be6d3-116">If the file expires, log in to the Azure portal and download the vault credentials files from your vault.</span></span>

### <a name="what-types-of-drives-can-i-back-up-files-and-folders-from-br"></a><span data-ttu-id="be6d3-117">我可以從何種類型的磁碟機備份檔案和資料夾？</span><span class="sxs-lookup"><span data-stu-id="be6d3-117">What types of drives can I back up files and folders from?</span></span> <br/>
<span data-ttu-id="be6d3-118">您無法備份下列磁碟機/磁碟區：</span><span class="sxs-lookup"><span data-stu-id="be6d3-118">You can't back up the following drives/volumes:</span></span>

* <span data-ttu-id="be6d3-119">卸除式媒體：所有備份項目來源必須報告為固定式。</span><span class="sxs-lookup"><span data-stu-id="be6d3-119">Removable Media: All backup item sources must report as fixed.</span></span>
* <span data-ttu-id="be6d3-120">唯讀磁碟區：必須為可寫入磁碟區，才能使磁碟區陰影複製服務 (VSS) 正常運作。</span><span class="sxs-lookup"><span data-stu-id="be6d3-120">Read-only Volumes: The volume must be writable for the volume shadow copy service (VSS) to function.</span></span>
* <span data-ttu-id="be6d3-121">離線磁碟區：必須為線上磁碟區，才能使 VSS 正常運作。</span><span class="sxs-lookup"><span data-stu-id="be6d3-121">Offline Volumes: The volume must be online for VSS to function.</span></span>
* <span data-ttu-id="be6d3-122">網路共用：必須為本機磁碟區，才能使用線上備份來備份伺服器。</span><span class="sxs-lookup"><span data-stu-id="be6d3-122">Network share: The volume must be local to the server to be backed up using online backup.</span></span>
* <span data-ttu-id="be6d3-123">受 Bitlocker 保護的磁碟區：磁碟區必須先解除鎖定才能執行備份。</span><span class="sxs-lookup"><span data-stu-id="be6d3-123">Bitlocker-protected volumes: The volume must be unlocked before the backup can occur.</span></span>
* <span data-ttu-id="be6d3-124">檔案系統識別碼：NTFS 是唯一支援的檔案系統。</span><span class="sxs-lookup"><span data-stu-id="be6d3-124">File System Identification: NTFS is the only file system supported.</span></span>

### <a name="what-file-and-folder-types-can-i-back-up-from-my-serverbr"></a><span data-ttu-id="be6d3-125">我可以從伺服器備份何種類型的檔案和資料夾？</span><span class="sxs-lookup"><span data-stu-id="be6d3-125">What file and folder types can I back up from my server?</span></span><br/>
<span data-ttu-id="be6d3-126">支援下列類型：</span><span class="sxs-lookup"><span data-stu-id="be6d3-126">The following types are supported:</span></span>

* <span data-ttu-id="be6d3-127">已加密</span><span class="sxs-lookup"><span data-stu-id="be6d3-127">Encrypted</span></span>
* <span data-ttu-id="be6d3-128">已壓縮</span><span class="sxs-lookup"><span data-stu-id="be6d3-128">Compressed</span></span>
* <span data-ttu-id="be6d3-129">疏鬆</span><span class="sxs-lookup"><span data-stu-id="be6d3-129">Sparse</span></span>
* <span data-ttu-id="be6d3-130">已壓縮 + 疏鬆</span><span class="sxs-lookup"><span data-stu-id="be6d3-130">Compressed + Sparse</span></span>
* <span data-ttu-id="be6d3-131">永久連結：不支援並略過</span><span class="sxs-lookup"><span data-stu-id="be6d3-131">Hard Links: Not supported, skipped</span></span>
* <span data-ttu-id="be6d3-132">重新分析點：不支援並略過</span><span class="sxs-lookup"><span data-stu-id="be6d3-132">Reparse Point: Not supported, skipped</span></span>
* <span data-ttu-id="be6d3-133">已加密 + 疏鬆：不支援並略過</span><span class="sxs-lookup"><span data-stu-id="be6d3-133">Encrypted + Sparse: Not supported, skipped</span></span>
* <span data-ttu-id="be6d3-134">已壓縮資料流：不支援並略過</span><span class="sxs-lookup"><span data-stu-id="be6d3-134">Compressed Stream: Not supported, skipped</span></span>
* <span data-ttu-id="be6d3-135">疏鬆資料流：不支援並略過</span><span class="sxs-lookup"><span data-stu-id="be6d3-135">Sparse Stream: Not supported, skipped</span></span>

### <a name="can-i-install-the-azure-backup-agent-on-an-azure-vm-already-backed-by-the-azure-backup-service-using-the-vm-extension-br"></a><span data-ttu-id="be6d3-136">我可以在已由 Azure 備份服務所備份的 Azure VM 上使用 VM 擴充功能來安裝 Azure 備份代理程式嗎？</span><span class="sxs-lookup"><span data-stu-id="be6d3-136">Can I install the Azure Backup agent on an Azure VM already backed by the Azure Backup service using the VM extension?</span></span> <br/>
<span data-ttu-id="be6d3-137">當然。</span><span class="sxs-lookup"><span data-stu-id="be6d3-137">Absolutely.</span></span> <span data-ttu-id="be6d3-138">Azure 備份使用 VM 擴充功能為 Azure VM 提供 VM 層級備份。</span><span class="sxs-lookup"><span data-stu-id="be6d3-138">Azure Backup provides VM-level backup for Azure VMs using the VM extension.</span></span> <span data-ttu-id="be6d3-139">若要保護客體 Windows OS 上的檔案和資料夾﹐請在客體 Windows OS 上安裝 Azure 備份代理程式。</span><span class="sxs-lookup"><span data-stu-id="be6d3-139">To protect files and folders on the guest Windows OS, install the Azure Backup agent on the guest Windows OS.</span></span>

### <a name="can-i-install-the-azure-backup-agent-on-an-azure-vm-to-back-up-files-and-folders-present-on-temporary-storage-provided-by-the-azure-vm-br"></a><span data-ttu-id="be6d3-140">我可以在 Azure VM 上安裝 Azure 備份代理程式來備份 Azure VM 所提供的暫存儲存體中存在的檔案和資料夾嗎？</span><span class="sxs-lookup"><span data-stu-id="be6d3-140">Can I install the Azure Backup agent on an Azure VM to back up files and folders present on temporary storage provided by the Azure VM?</span></span> <br/>
<span data-ttu-id="be6d3-141">是。</span><span class="sxs-lookup"><span data-stu-id="be6d3-141">Yes.</span></span> <span data-ttu-id="be6d3-142">在客體 Windows OS 上安裝 Azure 備份代理程式，並將檔案和資料夾備份至暫存儲存體。</span><span class="sxs-lookup"><span data-stu-id="be6d3-142">Install the Azure Backup agent on the guest Windows OS, and back up files and folders to temporary storage.</span></span> <span data-ttu-id="be6d3-143">一旦抹除暫存儲存體資料，備份工作就會失敗。此外，如果暫存儲存體資料已遭刪除，您只能還原至非變動性儲存體。</span><span class="sxs-lookup"><span data-stu-id="be6d3-143">Backup jobs fail once temporary storage data is wiped out. Also, if the temporary storage data has been deleted, you can only restore to non-volatile storage.</span></span>

### <a name="whats-the-minimum-size-requirement-for-the-cache-folder-br"></a><span data-ttu-id="be6d3-144">什麼是快取資料夾的最低大小需求？</span><span class="sxs-lookup"><span data-stu-id="be6d3-144">What's the minimum size requirement for the cache folder?</span></span> <br/>
<span data-ttu-id="be6d3-145">快取資料夾的大小可決定您正在備份的資料量。</span><span class="sxs-lookup"><span data-stu-id="be6d3-145">The size of the cache folder determines the amount of data that you are backing up.</span></span> <span data-ttu-id="be6d3-146">快取資料夾應該是資料儲存體所需空間的 5%。</span><span class="sxs-lookup"><span data-stu-id="be6d3-146">Your cache folder should be 5% of the space required for data storage.</span></span>

### <a name="how-do-i-register-my-server-to-another-datacenterbr"></a><span data-ttu-id="be6d3-147">我如何向其他資料中心註冊我的伺服器？</span><span class="sxs-lookup"><span data-stu-id="be6d3-147">How do I register my server to another datacenter?</span></span><br/>
<span data-ttu-id="be6d3-148">備份資料會傳送至保存庫的資料中心以進行註冊。</span><span class="sxs-lookup"><span data-stu-id="be6d3-148">Backup data is sent to the datacenter of the vault to which it is registered.</span></span> <span data-ttu-id="be6d3-149">若要變更資料中心，最簡單的方式是將代理程式解除安裝並重新安裝，然後向所需資料中心的新保存庫進行註冊。</span><span class="sxs-lookup"><span data-stu-id="be6d3-149">The easiest way to change the datacenter is to uninstall the agent and reinstall the agent and register to a new vault that belongs to desired datacenter.</span></span>

### <a name="does-the-azure-backup-agent-work-on-a-server-that-uses-windows-server-2012-deduplication-br"></a><span data-ttu-id="be6d3-150">Azure 備份代理程式是否在使用 Windows Server 2012 重複資料刪除的伺服器上運作？</span><span class="sxs-lookup"><span data-stu-id="be6d3-150">Does the Azure Backup agent work on a server that uses Windows Server 2012 deduplication?</span></span> <br/>
<span data-ttu-id="be6d3-151">是。</span><span class="sxs-lookup"><span data-stu-id="be6d3-151">Yes.</span></span> <span data-ttu-id="be6d3-152">當代理程式服務準備備份作業時，會將重複資料刪除的資料轉換成一般資料。</span><span class="sxs-lookup"><span data-stu-id="be6d3-152">The agent service converts the deduplicated data to normal data when it prepares the backup operation.</span></span> <span data-ttu-id="be6d3-153">它接著會最佳化資料以備份，加密資料，然後將加密的資料傳送至線上備份服務。</span><span class="sxs-lookup"><span data-stu-id="be6d3-153">It then optimizes the data for backup, encrypts the data, and then sends the encrypted data to the online backup service.</span></span>

## <a name="backup"></a><span data-ttu-id="be6d3-154">備份</span><span class="sxs-lookup"><span data-stu-id="be6d3-154">Backup</span></span>
### <a name="how-do-i-change-the-cache-location-specified-for-the-azure-backup-agentbr"></a><span data-ttu-id="be6d3-155">如何變更為 Azure 備份代理程式指定的快取位置？</span><span class="sxs-lookup"><span data-stu-id="be6d3-155">How do I change the cache location specified for the Azure Backup agent?</span></span><br/>
<span data-ttu-id="be6d3-156">使用下列清單來變更快取位置。</span><span class="sxs-lookup"><span data-stu-id="be6d3-156">Use the following list to change the cache location.</span></span>

1. <span data-ttu-id="be6d3-157">在提高權限的命令提示字元中執行下列命令以停止備份引擎：</span><span class="sxs-lookup"><span data-stu-id="be6d3-157">Stop the Backup engine by executing the following command in an elevated command prompt:</span></span>

    ```PS C:\> Net stop obengine``` 
  
2. <span data-ttu-id="be6d3-158">請勿移動檔案。</span><span class="sxs-lookup"><span data-stu-id="be6d3-158">Do not move the files.</span></span> <span data-ttu-id="be6d3-159">相反地，請將快取空間資料夾複製到具有足夠空間的其他磁碟機。</span><span class="sxs-lookup"><span data-stu-id="be6d3-159">Instead, copy the cache space folder to a different drive with sufficient space.</span></span> <span data-ttu-id="be6d3-160">確認備份使用新的快取空間之後，就可以移除原始的快取空間。</span><span class="sxs-lookup"><span data-stu-id="be6d3-160">The original cache space can be removed after confirming the backups are working with the new cache space.</span></span>
3. <span data-ttu-id="be6d3-161">更新下列登錄項目，其具備新快取空間資料夾的路徑。</span><span class="sxs-lookup"><span data-stu-id="be6d3-161">Update the following registry entries with the path to the new cache space folder.</span></span><br/>

    | <span data-ttu-id="be6d3-162">登錄路徑</span><span class="sxs-lookup"><span data-stu-id="be6d3-162">Registry path</span></span> | <span data-ttu-id="be6d3-163">登錄金鑰</span><span class="sxs-lookup"><span data-stu-id="be6d3-163">Registry Key</span></span> | <span data-ttu-id="be6d3-164">值</span><span class="sxs-lookup"><span data-stu-id="be6d3-164">Value</span></span> |
    | --- | --- | --- |
    | `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config` |<span data-ttu-id="be6d3-165">ScratchLocation</span><span class="sxs-lookup"><span data-stu-id="be6d3-165">ScratchLocation</span></span> |<span data-ttu-id="be6d3-166">*「新的快取資料夾位置」*</span><span class="sxs-lookup"><span data-stu-id="be6d3-166">*New cache folder location*</span></span> |
    | `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider` |<span data-ttu-id="be6d3-167">ScratchLocation</span><span class="sxs-lookup"><span data-stu-id="be6d3-167">ScratchLocation</span></span> |<span data-ttu-id="be6d3-168">*「新的快取資料夾位置」*</span><span class="sxs-lookup"><span data-stu-id="be6d3-168">*New cache folder location*</span></span> |

4. <span data-ttu-id="be6d3-169">在提高權限的命令提示字元中執行下列命令以重新啟動備份引擎：</span><span class="sxs-lookup"><span data-stu-id="be6d3-169">Restart the Backup engine by executing the following command in an elevated command prompt:</span></span>

    ```PS C:\> Net start obengine```

<span data-ttu-id="be6d3-170">一旦在新的快取位置成功完成備份建立，您就可以移除原始的快取資料夾。</span><span class="sxs-lookup"><span data-stu-id="be6d3-170">Once the backup creation is successfully completed in the new cache location, you can remove the original cache folder.</span></span>


### <a name="where-can-i-put-the-cache-folder-for-the-azure-backup-agent-to-work-as-expectedbr"></a><span data-ttu-id="be6d3-171">我可以把快取資料夾放在何處，以讓 Azure 備份代理程式如預期般運作？</span><span class="sxs-lookup"><span data-stu-id="be6d3-171">Where can I put the cache folder for the Azure Backup Agent to work as expected?</span></span><br/>
<span data-ttu-id="be6d3-172">快取資料夾不建議使用下列位置︰</span><span class="sxs-lookup"><span data-stu-id="be6d3-172">The following locations for the cache folder are not recommended:</span></span>

* <span data-ttu-id="be6d3-173">網路共用或卸除式媒體︰快取資料夾必須是在需要使用線上備份進行備份之伺服器的本機位置。</span><span class="sxs-lookup"><span data-stu-id="be6d3-173">Network share or Removable Media: The cache folder must be local to the server that needs backing up using online backup.</span></span> <span data-ttu-id="be6d3-174">不支援網路位置或卸除式媒體，例如 USB 磁碟機。</span><span class="sxs-lookup"><span data-stu-id="be6d3-174">Network locations or removable media like USB drives are not supported.</span></span>
* <span data-ttu-id="be6d3-175">離線磁碟區︰快取資料夾必須在線上才能使用 Azure 備份代理程式進行預期的備份。</span><span class="sxs-lookup"><span data-stu-id="be6d3-175">Offline Volumes: The cache folder must be online for expected backup using Azure Backup Agent.</span></span>

### <a name="are-there-any-attributes-of-the-cache-folder-that-are-not-supportedbr"></a><span data-ttu-id="be6d3-176">快取資料夾是否有任何不受支援的屬性？</span><span class="sxs-lookup"><span data-stu-id="be6d3-176">Are there any attributes of the cache-folder that are not supported?</span></span><br/>
<span data-ttu-id="be6d3-177">快取資料夾不支援下列屬性或其組合︰</span><span class="sxs-lookup"><span data-stu-id="be6d3-177">The following attributes or their combinations are not supported for the cache folder:</span></span>

* <span data-ttu-id="be6d3-178">已加密</span><span class="sxs-lookup"><span data-stu-id="be6d3-178">Encrypted</span></span>
* <span data-ttu-id="be6d3-179">已刪除重複資料</span><span class="sxs-lookup"><span data-stu-id="be6d3-179">De-duplicated</span></span>
* <span data-ttu-id="be6d3-180">已壓縮</span><span class="sxs-lookup"><span data-stu-id="be6d3-180">Compressed</span></span>
* <span data-ttu-id="be6d3-181">疏鬆</span><span class="sxs-lookup"><span data-stu-id="be6d3-181">Sparse</span></span>
* <span data-ttu-id="be6d3-182">重新分析點</span><span class="sxs-lookup"><span data-stu-id="be6d3-182">Reparse-Point</span></span>

<span data-ttu-id="be6d3-183">快取資料夾和中繼資料 VHD 都不具有 Azure 備份代理程式所需的屬性。</span><span class="sxs-lookup"><span data-stu-id="be6d3-183">The cache folder and the metadata VHD do not have the necessary attributes for the Azure Backup agent.</span></span>

### <a name="is-there-a-way-to-adjust-the-amount-of-bandwidth-used-by-the-backup-servicebr"></a><span data-ttu-id="be6d3-184">是否有辦法調整備份服務所使用的頻寬量？</span><span class="sxs-lookup"><span data-stu-id="be6d3-184">Is there a way to adjust the amount of bandwidth used by the Backup service?</span></span><br/>
  <span data-ttu-id="be6d3-185">是，使用備份代理程式中的 [變更屬性]  選項來調整頻寬。</span><span class="sxs-lookup"><span data-stu-id="be6d3-185">Yes, use the **Change Properties** option in the Backup Agent to adjust bandwidth.</span></span> <span data-ttu-id="be6d3-186">您可以調整頻寬量以及使用該頻寬的時間。</span><span class="sxs-lookup"><span data-stu-id="be6d3-186">You can adjust the amount of bandwidth and the times when you use that bandwidth.</span></span> <span data-ttu-id="be6d3-187">如需逐步指示，請參閱**[啟用網路節流](backup-configure-vault.md#enable-network-throttling)**。</span><span class="sxs-lookup"><span data-stu-id="be6d3-187">For step-by-step instructions, see **[Enable network throttling](backup-configure-vault.md#enable-network-throttling)**.</span></span>

## <a name="manage-backups"></a><span data-ttu-id="be6d3-188">管理備份</span><span class="sxs-lookup"><span data-stu-id="be6d3-188">Manage backups</span></span>
### <a name="what-happens-if-i-rename-a-windows-server-that-is-backing-up-data-to-azurebr"></a><span data-ttu-id="be6d3-189">若重新命名正在將資料備份至 Azure 的 Windows 伺服器，則會發生什麼情況？</span><span class="sxs-lookup"><span data-stu-id="be6d3-189">What happens if I rename a Windows server that is backing up data to Azure?</span></span><br/>
<span data-ttu-id="be6d3-190">當您重新命名伺服器時，所有目前設定的備份都會停止。</span><span class="sxs-lookup"><span data-stu-id="be6d3-190">When you rename a server, all currently configured backups are stopped.</span></span>
<span data-ttu-id="be6d3-191">向備份保存庫註冊伺服器的新名稱。</span><span class="sxs-lookup"><span data-stu-id="be6d3-191">Register the new name of the server with the Backup vault.</span></span> <span data-ttu-id="be6d3-192">當您向保存庫註冊新名稱時，第一個備份作業是*完整*備份。</span><span class="sxs-lookup"><span data-stu-id="be6d3-192">When you register the new name with the vault, the first backup operation is a *full* backup.</span></span> <span data-ttu-id="be6d3-193">如果您需要復原已備份到採用舊伺服器名稱之保存庫的資料，請使用 [復原資料] 精靈中的 [[其他伺服器](backup-azure-restore-windows-server.md#use-instant-restore-to-restore-data-to-an-alternate-machine)] 選項。</span><span class="sxs-lookup"><span data-stu-id="be6d3-193">If you need to recover data backed up to the vault with the old server name, use the [**Another server**](backup-azure-restore-windows-server.md#use-instant-restore-to-restore-data-to-an-alternate-machine) option in the **Recover Data** wizard.</span></span>

### <a name="what-is-the-maximum-file-path-length-that-can-be-specified-in-backup-policy-using-azure-backup-agent-br"></a><span data-ttu-id="be6d3-194">使用 Azure 備份代理程式時，最多可在備份代理程式中指定多長的檔案路徑？</span><span class="sxs-lookup"><span data-stu-id="be6d3-194">What is the maximum file path length that can be specified in Backup policy using Azure Backup agent?</span></span> <br/>
<span data-ttu-id="be6d3-195">Azure 備份代理程式依存於 NTFS。</span><span class="sxs-lookup"><span data-stu-id="be6d3-195">Azure Backup agent relies on NTFS.</span></span> <span data-ttu-id="be6d3-196">[檔案路徑長度規格受限於 Windows API](https://msdn.microsoft.com/library/aa365247.aspx#fully_qualified_vs._relative_paths)。</span><span class="sxs-lookup"><span data-stu-id="be6d3-196">The [filepath length specification is limited by the Windows API](https://msdn.microsoft.com/library/aa365247.aspx#fully_qualified_vs._relative_paths).</span></span> <span data-ttu-id="be6d3-197">如果您要保護之檔案的檔案路徑長度超過 Windows API 所允許的長度，請備份父資料夾或磁碟機。</span><span class="sxs-lookup"><span data-stu-id="be6d3-197">If the files you want to protect have a file-path length longer than what is allowed by the Windows API, back up the parent folder or the disk drive.</span></span>  

### <a name="what-characters-are-allowed-in-file-path-of-azure-backup-policy-using-azure-backup-agent-br"></a><span data-ttu-id="be6d3-198">使用 Azure 備份代理程式時，Azure 備份原則的檔案路徑中允許哪些字元？</span><span class="sxs-lookup"><span data-stu-id="be6d3-198">What characters are allowed in file path of Azure Backup policy using Azure Backup agent?</span></span> <br>
 <span data-ttu-id="be6d3-199">Azure 備份代理程式依存於 NTFS。</span><span class="sxs-lookup"><span data-stu-id="be6d3-199">Azure Backup agent relies on NTFS.</span></span> <span data-ttu-id="be6d3-200">它可讓 [NTFS 支援的字元](https://msdn.microsoft.com/library/aa365247.aspx#naming_conventions) 成為檔案規格的一部分。</span><span class="sxs-lookup"><span data-stu-id="be6d3-200">It enables [NTFS supported characters](https://msdn.microsoft.com/library/aa365247.aspx#naming_conventions) as part of file specification.</span></span> 
 
### <a name="i-receive-the-warning-azure-backups-have-not-been-configured-for-this-server-even-though-i-configured-a-backup-policy-br"></a><span data-ttu-id="be6d3-201">我收到「Azure 備份尚未針對此伺服器設定」警告，即使我已設定備份原則</span><span class="sxs-lookup"><span data-stu-id="be6d3-201">I receive the warning, "Azure Backups have not been configured for this server" even though I configured a backup policy</span></span> <br/>
<span data-ttu-id="be6d3-202">當本機伺服器儲存的備份排程設定與備份保存庫儲存的設定不同時，會發生此警告。</span><span class="sxs-lookup"><span data-stu-id="be6d3-202">This warning occurs when the backup schedule settings stored on the local server are not the same as the settings stored in the backup vault.</span></span> <span data-ttu-id="be6d3-203">當伺服器或設定已復原至已知的良好狀態時，備份排程可能會失去同步處理。</span><span class="sxs-lookup"><span data-stu-id="be6d3-203">When either the server or the settings have been recovered to a known good state, the backup schedules can lose synchronization.</span></span> <span data-ttu-id="be6d3-204">如果您收到此警告，請[重新設定備份原則](backup-azure-manage-windows-server.md)，然後 [立即執行備份] 以重新同步處理本機伺服器與 Azure。</span><span class="sxs-lookup"><span data-stu-id="be6d3-204">If you receive this warning, [reconfigure the backup policy](backup-azure-manage-windows-server.md) and then **Run Back Up Now** to resynchronize the local server with Azure.</span></span>
