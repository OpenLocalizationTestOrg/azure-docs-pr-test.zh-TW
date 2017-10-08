---
title: "aaaAzure 備份代理程式常見問題集 |Microsoft 文件"
description: "關於回答 toocommon 問題： 如何 hello Azure 備份代理程式的運作方式、 備份和保留的限制。"
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
ms.openlocfilehash: bdefb4efb39301f38cdf692bdc93c841a2bbb441
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="questions-about-hello-azure-backup-agent"></a><span data-ttu-id="1eb91-104">Hello Azure 備份代理程式的相關問題</span><span class="sxs-lookup"><span data-stu-id="1eb91-104">Questions about hello Azure Backup agent</span></span>
<span data-ttu-id="1eb91-105">這篇文章有解答 toocommon 問題 toohelp 快速了解 hello Azure 備份代理程式元件。</span><span class="sxs-lookup"><span data-stu-id="1eb91-105">This article has answers toocommon questions toohelp you quickly understand hello Azure Backup agent components.</span></span> <span data-ttu-id="1eb91-106">在某些 hello 解答，會有連結 toohello 文件具有完整的資訊。</span><span class="sxs-lookup"><span data-stu-id="1eb91-106">In some of hello answers, there are links toohello articles that have comprehensive information.</span></span> <span data-ttu-id="1eb91-107">您也可以張貼疑問 hello Azure 備份服務在 hello[討論區論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup)。</span><span class="sxs-lookup"><span data-stu-id="1eb91-107">You can also post questions about hello Azure Backup service in hello [discussion forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).</span></span>

## <a name="configure-backup"></a><span data-ttu-id="1eb91-108">設定備份</span><span class="sxs-lookup"><span data-stu-id="1eb91-108">Configure backup</span></span>
### <a name="where-can-i-download-hello-latest-azure-backup-agent-br"></a><span data-ttu-id="1eb91-109">哪裡可以下載最新 Azure Backup agent hello？</span><span class="sxs-lookup"><span data-stu-id="1eb91-109">Where can I download hello latest Azure Backup agent?</span></span> <br/>
<span data-ttu-id="1eb91-110">您可以下載 hello 最新的代理程式來備份 Windows Server、 System Center DPM 或 Windows 用戶端，從[這裡](http://aka.ms/azurebackup_agent)。</span><span class="sxs-lookup"><span data-stu-id="1eb91-110">You can download hello latest agent for backing up Windows Server, System Center DPM, or Windows client, from [here](http://aka.ms/azurebackup_agent).</span></span> <span data-ttu-id="1eb91-111">如果您想 tooback 的虛擬機器，請使用 hello VM 代理程式 」 （會自動安裝 hello 適當擴充功能）。</span><span class="sxs-lookup"><span data-stu-id="1eb91-111">If you want tooback up a virtual machine, use hello VM Agent (which automatically installs hello proper extension).</span></span> <span data-ttu-id="1eb91-112">hello VM 代理程式已存在於建立 hello Azure 組件庫的虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="1eb91-112">hello VM Agent is already present on virtual machines created from hello Azure gallery.</span></span>

### <a name="when-configuring-hello-azure-backup-agent-i-am-prompted-tooenter-hello-vault-credentials-do-vault-credentials-expire"></a><span data-ttu-id="1eb91-113">設定 hello Azure Backup agent，我提示的 tooenter hello 保存庫認證。</span><span class="sxs-lookup"><span data-stu-id="1eb91-113">When configuring hello Azure Backup agent, I am prompted tooenter hello vault credentials.</span></span> <span data-ttu-id="1eb91-114">保存庫認證是否過期？</span><span class="sxs-lookup"><span data-stu-id="1eb91-114">Do vault credentials expire?</span></span>
<span data-ttu-id="1eb91-115">是，hello 保存庫認證會在 48 小時後過期。</span><span class="sxs-lookup"><span data-stu-id="1eb91-115">Yes, hello vault credentials expire after 48 hours.</span></span> <span data-ttu-id="1eb91-116">如果 hello 檔案到期，登入 toohello Azure 入口網站並下載 hello 保存庫認證檔案從您的保存庫。</span><span class="sxs-lookup"><span data-stu-id="1eb91-116">If hello file expires, log in toohello Azure portal and download hello vault credentials files from your vault.</span></span>

### <a name="what-types-of-drives-can-i-back-up-files-and-folders-from-br"></a><span data-ttu-id="1eb91-117">我可以從何種類型的磁碟機備份檔案和資料夾？</span><span class="sxs-lookup"><span data-stu-id="1eb91-117">What types of drives can I back up files and folders from?</span></span> <br/>
<span data-ttu-id="1eb91-118">您無法備份下列磁碟區的磁碟機/hello:</span><span class="sxs-lookup"><span data-stu-id="1eb91-118">You can't back up hello following drives/volumes:</span></span>

* <span data-ttu-id="1eb91-119">卸除式媒體：所有備份項目來源必須報告為固定式。</span><span class="sxs-lookup"><span data-stu-id="1eb91-119">Removable Media: All backup item sources must report as fixed.</span></span>
* <span data-ttu-id="1eb91-120">唯讀磁碟區： hello 磁碟區必須可供 hello 磁碟區陰影複製服務 (VSS) toofunction 寫入。</span><span class="sxs-lookup"><span data-stu-id="1eb91-120">Read-only Volumes: hello volume must be writable for hello volume shadow copy service (VSS) toofunction.</span></span>
* <span data-ttu-id="1eb91-121">離線的磁碟區： hello 磁碟區必須在線上，VSS toofunction。</span><span class="sxs-lookup"><span data-stu-id="1eb91-121">Offline Volumes: hello volume must be online for VSS toofunction.</span></span>
* <span data-ttu-id="1eb91-122">網路共用： hello 磁碟區必須是本機 toohello 伺服器 toobe 使用線上備份執行備份。</span><span class="sxs-lookup"><span data-stu-id="1eb91-122">Network share: hello volume must be local toohello server toobe backed up using online backup.</span></span>
* <span data-ttu-id="1eb91-123">受 Bitlocker 保護的磁碟區： hello 磁碟區必須先解除鎖定 hello 備份可能會發生。</span><span class="sxs-lookup"><span data-stu-id="1eb91-123">Bitlocker-protected volumes: hello volume must be unlocked before hello backup can occur.</span></span>
* <span data-ttu-id="1eb91-124">檔案系統識別： NTFS 是 hello 支援唯一的檔案系統。</span><span class="sxs-lookup"><span data-stu-id="1eb91-124">File System Identification: NTFS is hello only file system supported.</span></span>

### <a name="what-file-and-folder-types-can-i-back-up-from-my-serverbr"></a><span data-ttu-id="1eb91-125">我可以從伺服器備份何種類型的檔案和資料夾？</span><span class="sxs-lookup"><span data-stu-id="1eb91-125">What file and folder types can I back up from my server?</span></span><br/>
<span data-ttu-id="1eb91-126">支援下列類型的 hello:</span><span class="sxs-lookup"><span data-stu-id="1eb91-126">hello following types are supported:</span></span>

* <span data-ttu-id="1eb91-127">已加密</span><span class="sxs-lookup"><span data-stu-id="1eb91-127">Encrypted</span></span>
* <span data-ttu-id="1eb91-128">已壓縮</span><span class="sxs-lookup"><span data-stu-id="1eb91-128">Compressed</span></span>
* <span data-ttu-id="1eb91-129">疏鬆</span><span class="sxs-lookup"><span data-stu-id="1eb91-129">Sparse</span></span>
* <span data-ttu-id="1eb91-130">已壓縮 + 疏鬆</span><span class="sxs-lookup"><span data-stu-id="1eb91-130">Compressed + Sparse</span></span>
* <span data-ttu-id="1eb91-131">永久連結：不支援並略過</span><span class="sxs-lookup"><span data-stu-id="1eb91-131">Hard Links: Not supported, skipped</span></span>
* <span data-ttu-id="1eb91-132">重新分析點：不支援並略過</span><span class="sxs-lookup"><span data-stu-id="1eb91-132">Reparse Point: Not supported, skipped</span></span>
* <span data-ttu-id="1eb91-133">已加密 + 疏鬆：不支援並略過</span><span class="sxs-lookup"><span data-stu-id="1eb91-133">Encrypted + Sparse: Not supported, skipped</span></span>
* <span data-ttu-id="1eb91-134">已壓縮資料流：不支援並略過</span><span class="sxs-lookup"><span data-stu-id="1eb91-134">Compressed Stream: Not supported, skipped</span></span>
* <span data-ttu-id="1eb91-135">疏鬆資料流：不支援並略過</span><span class="sxs-lookup"><span data-stu-id="1eb91-135">Sparse Stream: Not supported, skipped</span></span>

### <a name="can-i-install-hello-azure-backup-agent-on-an-azure-vm-already-backed-by-hello-azure-backup-service-using-hello-vm-extension-br"></a><span data-ttu-id="1eb91-136">可以安裝 hello Azure 備份代理程式已經 hello Azure 備份服務使用 hello VM 延伸模組所支援的 Azure VM 上嗎？</span><span class="sxs-lookup"><span data-stu-id="1eb91-136">Can I install hello Azure Backup agent on an Azure VM already backed by hello Azure Backup service using hello VM extension?</span></span> <br/>
<span data-ttu-id="1eb91-137">當然。</span><span class="sxs-lookup"><span data-stu-id="1eb91-137">Absolutely.</span></span> <span data-ttu-id="1eb91-138">Azure 備份提供 VM 層級備份就 Azure vm 使用 hello VM 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="1eb91-138">Azure Backup provides VM-level backup for Azure VMs using hello VM extension.</span></span> <span data-ttu-id="1eb91-139">hello 客體 Windows 作業系統上 tooprotect 檔案和資料夾安裝 hello Azure Backup agent 在 hello 客體 Windows 作業系統上。</span><span class="sxs-lookup"><span data-stu-id="1eb91-139">tooprotect files and folders on hello guest Windows OS, install hello Azure Backup agent on hello guest Windows OS.</span></span>

### <a name="can-i-install-hello-azure-backup-agent-on-an-azure-vm-tooback-up-files-and-folders-present-on-temporary-storage-provided-by-hello-azure-vm-br"></a><span data-ttu-id="1eb91-140">可以安裝 hello Azure 備份代理程式上的 Azure VM tooback 檔案及資料夾上 hello Azure VM 所提供的暫存儲存體嗎？</span><span class="sxs-lookup"><span data-stu-id="1eb91-140">Can I install hello Azure Backup agent on an Azure VM tooback up files and folders present on temporary storage provided by hello Azure VM?</span></span> <br/>
<span data-ttu-id="1eb91-141">是。</span><span class="sxs-lookup"><span data-stu-id="1eb91-141">Yes.</span></span> <span data-ttu-id="1eb91-142">Hello 客體 Windows 作業系統上安裝 hello Azure 備份代理程式和備份檔案和資料夾 tootemporary 儲存體。</span><span class="sxs-lookup"><span data-stu-id="1eb91-142">Install hello Azure Backup agent on hello guest Windows OS, and back up files and folders tootemporary storage.</span></span> <span data-ttu-id="1eb91-143">一旦抹除暫存儲存體資料，備份工作就會失敗。此外，如果 hello 暫存資料都已刪除，您可以只還原 toonon 揮發性儲存體。</span><span class="sxs-lookup"><span data-stu-id="1eb91-143">Backup jobs fail once temporary storage data is wiped out. Also, if hello temporary storage data has been deleted, you can only restore toonon-volatile storage.</span></span>

### <a name="whats-hello-minimum-size-requirement-for-hello-cache-folder-br"></a><span data-ttu-id="1eb91-144">Hello hello 快取資料夾的最低大小需求為何？</span><span class="sxs-lookup"><span data-stu-id="1eb91-144">What's hello minimum size requirement for hello cache folder?</span></span> <br/>
<span data-ttu-id="1eb91-145">hello hello 快取資料夾大小會決定 hello 要備份的資料量。</span><span class="sxs-lookup"><span data-stu-id="1eb91-145">hello size of hello cache folder determines hello amount of data that you are backing up.</span></span> <span data-ttu-id="1eb91-146">快取資料夾應該是空間的 5 %hello 所需來儲存資料。</span><span class="sxs-lookup"><span data-stu-id="1eb91-146">Your cache folder should be 5% of hello space required for data storage.</span></span>

### <a name="how-do-i-register-my-server-tooanother-datacenterbr"></a><span data-ttu-id="1eb91-147">如何註冊我的伺服器 tooanother 資料中心？</span><span class="sxs-lookup"><span data-stu-id="1eb91-147">How do I register my server tooanother datacenter?</span></span><br/>
<span data-ttu-id="1eb91-148">備份資料會傳送 hello 保存庫 toowhich 已註冊的 toohello 資料中心。</span><span class="sxs-lookup"><span data-stu-id="1eb91-148">Backup data is sent toohello datacenter of hello vault toowhich it is registered.</span></span> <span data-ttu-id="1eb91-149">hello 最簡單方式 toochange hello datacenter toouninstall hello 代理程式並重新安裝 hello 代理程式並註冊 tooa 新的保存庫所屬 toodesired 資料中心。</span><span class="sxs-lookup"><span data-stu-id="1eb91-149">hello easiest way toochange hello datacenter is toouninstall hello agent and reinstall hello agent and register tooa new vault that belongs toodesired datacenter.</span></span>

### <a name="does-hello-azure-backup-agent-work-on-a-server-that-uses-windows-server-2012-deduplication-br"></a><span data-ttu-id="1eb91-150">Hello Azure 備份代理程式工作使用 Windows Server 2012 重複資料刪除的伺服器嗎？</span><span class="sxs-lookup"><span data-stu-id="1eb91-150">Does hello Azure Backup agent work on a server that uses Windows Server 2012 deduplication?</span></span> <br/>
<span data-ttu-id="1eb91-151">是。</span><span class="sxs-lookup"><span data-stu-id="1eb91-151">Yes.</span></span> <span data-ttu-id="1eb91-152">準備 hello 備份作業時，hello 代理程式服務將重複資料刪除的 hello 資料 toonormal 資料轉換。</span><span class="sxs-lookup"><span data-stu-id="1eb91-152">hello agent service converts hello deduplicated data toonormal data when it prepares hello backup operation.</span></span> <span data-ttu-id="1eb91-153">然後最佳化用於備份的 hello 資料、 加密 hello 資料，並接著會傳送 hello 加密資料 toohello 線上備份服務。</span><span class="sxs-lookup"><span data-stu-id="1eb91-153">It then optimizes hello data for backup, encrypts hello data, and then sends hello encrypted data toohello online backup service.</span></span>

## <a name="backup"></a><span data-ttu-id="1eb91-154">備份</span><span class="sxs-lookup"><span data-stu-id="1eb91-154">Backup</span></span>
### <a name="how-do-i-change-hello-cache-location-specified-for-hello-azure-backup-agentbr"></a><span data-ttu-id="1eb91-155">如何變更 hello 快取位置指定 hello Azure 備份代理程式？</span><span class="sxs-lookup"><span data-stu-id="1eb91-155">How do I change hello cache location specified for hello Azure Backup agent?</span></span><br/>
<span data-ttu-id="1eb91-156">使用下列清單 toochange hello 快取位置中的 hello。</span><span class="sxs-lookup"><span data-stu-id="1eb91-156">Use hello following list toochange hello cache location.</span></span>

1. <span data-ttu-id="1eb91-157">停止 hello 備份引擎藉由執行下列命令，在提升權限的命令提示字元中的 hello:</span><span class="sxs-lookup"><span data-stu-id="1eb91-157">Stop hello Backup engine by executing hello following command in an elevated command prompt:</span></span>

    ```PS C:\> Net stop obengine``` 
  
2. <span data-ttu-id="1eb91-158">不會移動 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="1eb91-158">Do not move hello files.</span></span> <span data-ttu-id="1eb91-159">相反地，複製 hello 快取空間資料夾 tooa 不同的磁碟機具有足夠空間。</span><span class="sxs-lookup"><span data-stu-id="1eb91-159">Instead, copy hello cache space folder tooa different drive with sufficient space.</span></span> <span data-ttu-id="1eb91-160">確認備份使用新的快取空間 hello hello 之後，就可以移除 hello 原始的快取空間。</span><span class="sxs-lookup"><span data-stu-id="1eb91-160">hello original cache space can be removed after confirming hello backups are working with hello new cache space.</span></span>
3. <span data-ttu-id="1eb91-161">更新下列登錄項目與 hello 路徑 toohello 新快取空間資料夾 hello。</span><span class="sxs-lookup"><span data-stu-id="1eb91-161">Update hello following registry entries with hello path toohello new cache space folder.</span></span><br/>

    | <span data-ttu-id="1eb91-162">登錄路徑</span><span class="sxs-lookup"><span data-stu-id="1eb91-162">Registry path</span></span> | <span data-ttu-id="1eb91-163">登錄金鑰</span><span class="sxs-lookup"><span data-stu-id="1eb91-163">Registry Key</span></span> | <span data-ttu-id="1eb91-164">值</span><span class="sxs-lookup"><span data-stu-id="1eb91-164">Value</span></span> |
    | --- | --- | --- |
    | `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config` |<span data-ttu-id="1eb91-165">ScratchLocation</span><span class="sxs-lookup"><span data-stu-id="1eb91-165">ScratchLocation</span></span> |<span data-ttu-id="1eb91-166">*「新的快取資料夾位置」*</span><span class="sxs-lookup"><span data-stu-id="1eb91-166">*New cache folder location*</span></span> |
    | `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider` |<span data-ttu-id="1eb91-167">ScratchLocation</span><span class="sxs-lookup"><span data-stu-id="1eb91-167">ScratchLocation</span></span> |<span data-ttu-id="1eb91-168">*「新的快取資料夾位置」*</span><span class="sxs-lookup"><span data-stu-id="1eb91-168">*New cache folder location*</span></span> |

4. <span data-ttu-id="1eb91-169">重新啟動 hello 備份引擎，藉由執行下列命令，在提升權限的命令提示字元中的 hello:</span><span class="sxs-lookup"><span data-stu-id="1eb91-169">Restart hello Backup engine by executing hello following command in an elevated command prompt:</span></span>

    ```PS C:\> Net start obengine```

<span data-ttu-id="1eb91-170">一旦建立 hello 備份順利完成在 hello 新快取位置中，您可以移除 hello 原始的快取資料夾。</span><span class="sxs-lookup"><span data-stu-id="1eb91-170">Once hello backup creation is successfully completed in hello new cache location, you can remove hello original cache folder.</span></span>


### <a name="where-can-i-put-hello-cache-folder-for-hello-azure-backup-agent-toowork-as-expectedbr"></a><span data-ttu-id="1eb91-171">我可以在放置 hello Azure Backup Agent toowork 如預期般的 hello 快取資料夾？</span><span class="sxs-lookup"><span data-stu-id="1eb91-171">Where can I put hello cache folder for hello Azure Backup Agent toowork as expected?</span></span><br/>
<span data-ttu-id="1eb91-172">hello hello 快取資料夾的下列位置不建議使用：</span><span class="sxs-lookup"><span data-stu-id="1eb91-172">hello following locations for hello cache folder are not recommended:</span></span>

* <span data-ttu-id="1eb91-173">網路共用或卸除式媒體： hello 快取資料夾必須是本機 toohello 伺服器需要使用線上備份進行備份。</span><span class="sxs-lookup"><span data-stu-id="1eb91-173">Network share or Removable Media: hello cache folder must be local toohello server that needs backing up using online backup.</span></span> <span data-ttu-id="1eb91-174">不支援網路位置或卸除式媒體，例如 USB 磁碟機。</span><span class="sxs-lookup"><span data-stu-id="1eb91-174">Network locations or removable media like USB drives are not supported.</span></span>
* <span data-ttu-id="1eb91-175">離線的磁碟區： hello 快取資料夾必須在線上，預期的備份使用 Azure Backup Agent。</span><span class="sxs-lookup"><span data-stu-id="1eb91-175">Offline Volumes: hello cache folder must be online for expected backup using Azure Backup Agent.</span></span>

### <a name="are-there-any-attributes-of-hello-cache-folder-that-are-not-supportedbr"></a><span data-ttu-id="1eb91-176">有不支援的任何屬性的 hello 快取資料夾嗎？</span><span class="sxs-lookup"><span data-stu-id="1eb91-176">Are there any attributes of hello cache-folder that are not supported?</span></span><br/>
<span data-ttu-id="1eb91-177">hello 下列屬性或其組合不支援為 hello 快取資料夾：</span><span class="sxs-lookup"><span data-stu-id="1eb91-177">hello following attributes or their combinations are not supported for hello cache folder:</span></span>

* <span data-ttu-id="1eb91-178">已加密</span><span class="sxs-lookup"><span data-stu-id="1eb91-178">Encrypted</span></span>
* <span data-ttu-id="1eb91-179">已刪除重複資料</span><span class="sxs-lookup"><span data-stu-id="1eb91-179">De-duplicated</span></span>
* <span data-ttu-id="1eb91-180">已壓縮</span><span class="sxs-lookup"><span data-stu-id="1eb91-180">Compressed</span></span>
* <span data-ttu-id="1eb91-181">疏鬆</span><span class="sxs-lookup"><span data-stu-id="1eb91-181">Sparse</span></span>
* <span data-ttu-id="1eb91-182">重新分析點</span><span class="sxs-lookup"><span data-stu-id="1eb91-182">Reparse-Point</span></span>

<span data-ttu-id="1eb91-183">hello 快取資料夾和 hello 中繼資料 VHD 並沒有 hello hello Azure 備份代理程式的必要屬性。</span><span class="sxs-lookup"><span data-stu-id="1eb91-183">hello cache folder and hello metadata VHD do not have hello necessary attributes for hello Azure Backup agent.</span></span>

### <a name="is-there-a-way-tooadjust-hello-amount-of-bandwidth-used-by-hello-backup-servicebr"></a><span data-ttu-id="1eb91-184">有一個方式 tooadjust hello 頻寬總量 hello 備份服務使用嗎？</span><span class="sxs-lookup"><span data-stu-id="1eb91-184">Is there a way tooadjust hello amount of bandwidth used by hello Backup service?</span></span><br/>
  <span data-ttu-id="1eb91-185">是，使用 hello**變更屬性**hello Backup Agent tooadjust 頻寬的選項。</span><span class="sxs-lookup"><span data-stu-id="1eb91-185">Yes, use hello **Change Properties** option in hello Backup Agent tooadjust bandwidth.</span></span> <span data-ttu-id="1eb91-186">您可以調整 hello 成長的頻寬和 hello 的時間，當您使用的頻寬量。</span><span class="sxs-lookup"><span data-stu-id="1eb91-186">You can adjust hello amount of bandwidth and hello times when you use that bandwidth.</span></span> <span data-ttu-id="1eb91-187">如需逐步指示，請參閱**[啟用網路節流](backup-configure-vault.md#enable-network-throttling)**。</span><span class="sxs-lookup"><span data-stu-id="1eb91-187">For step-by-step instructions, see **[Enable network throttling](backup-configure-vault.md#enable-network-throttling)**.</span></span>

## <a name="manage-backups"></a><span data-ttu-id="1eb91-188">管理備份</span><span class="sxs-lookup"><span data-stu-id="1eb91-188">Manage backups</span></span>
### <a name="what-happens-if-i-rename-a-windows-server-that-is-backing-up-data-tooazurebr"></a><span data-ttu-id="1eb91-189">如果我重新命名 Windows 伺服器的備份資料 tooAzure，怎樣？</span><span class="sxs-lookup"><span data-stu-id="1eb91-189">What happens if I rename a Windows server that is backing up data tooAzure?</span></span><br/>
<span data-ttu-id="1eb91-190">當您重新命名伺服器時，所有目前設定的備份都會停止。</span><span class="sxs-lookup"><span data-stu-id="1eb91-190">When you rename a server, all currently configured backups are stopped.</span></span>
<span data-ttu-id="1eb91-191">Hello 備份保存庫中註冊 hello 伺服器 hello 新名稱。</span><span class="sxs-lookup"><span data-stu-id="1eb91-191">Register hello new name of hello server with hello Backup vault.</span></span> <span data-ttu-id="1eb91-192">Hello 保存庫中註冊 hello 新名稱，hello 的第一個備份作業時，*完整*備份。</span><span class="sxs-lookup"><span data-stu-id="1eb91-192">When you register hello new name with hello vault, hello first backup operation is a *full* backup.</span></span> <span data-ttu-id="1eb91-193">如果您需要 toorecover 資料備份 toohello 保存庫與 hello 舊的伺服器名稱，請使用 hello [**另一部伺服器**](backup-azure-restore-windows-server.md#use-instant-restore-to-restore-data-to-an-alternate-machine)選項在 hello**復原資料**精靈。</span><span class="sxs-lookup"><span data-stu-id="1eb91-193">If you need toorecover data backed up toohello vault with hello old server name, use hello [**Another server**](backup-azure-restore-windows-server.md#use-instant-restore-to-restore-data-to-an-alternate-machine) option in hello **Recover Data** wizard.</span></span>

### <a name="what-is-hello-maximum-file-path-length-that-can-be-specified-in-backup-policy-using-azure-backup-agent-br"></a><span data-ttu-id="1eb91-194">可以使用 Azure 備份代理程式的備份原則中指定的 hello 最大的檔案路徑長度為何？</span><span class="sxs-lookup"><span data-stu-id="1eb91-194">What is hello maximum file path length that can be specified in Backup policy using Azure Backup agent?</span></span> <br/>
<span data-ttu-id="1eb91-195">Azure 備份代理程式依存於 NTFS。</span><span class="sxs-lookup"><span data-stu-id="1eb91-195">Azure Backup agent relies on NTFS.</span></span> <span data-ttu-id="1eb91-196">hello [filepath 長度規格會受到 hello Windows API](https://msdn.microsoft.com/library/aa365247.aspx#fully_qualified_vs._relative_paths)。</span><span class="sxs-lookup"><span data-stu-id="1eb91-196">hello [filepath length specification is limited by hello Windows API](https://msdn.microsoft.com/library/aa365247.aspx#fully_qualified_vs._relative_paths).</span></span> <span data-ttu-id="1eb91-197">如果您想要 tooprotect hello 檔案的檔案路徑長度超過所允許的 hello Windows API，備份 hello 父資料夾或 hello 磁碟機。</span><span class="sxs-lookup"><span data-stu-id="1eb91-197">If hello files you want tooprotect have a file-path length longer than what is allowed by hello Windows API, back up hello parent folder or hello disk drive.</span></span>  

### <a name="what-characters-are-allowed-in-file-path-of-azure-backup-policy-using-azure-backup-agent-br"></a><span data-ttu-id="1eb91-198">使用 Azure 備份代理程式時，Azure 備份原則的檔案路徑中允許哪些字元？</span><span class="sxs-lookup"><span data-stu-id="1eb91-198">What characters are allowed in file path of Azure Backup policy using Azure Backup agent?</span></span> <br>
 <span data-ttu-id="1eb91-199">Azure 備份代理程式依存於 NTFS。</span><span class="sxs-lookup"><span data-stu-id="1eb91-199">Azure Backup agent relies on NTFS.</span></span> <span data-ttu-id="1eb91-200">它可讓 [NTFS 支援的字元](https://msdn.microsoft.com/library/aa365247.aspx#naming_conventions) 成為檔案規格的一部分。</span><span class="sxs-lookup"><span data-stu-id="1eb91-200">It enables [NTFS supported characters](https://msdn.microsoft.com/library/aa365247.aspx#naming_conventions) as part of file specification.</span></span> 
 
### <a name="i-receive-hello-warning-azure-backups-have-not-been-configured-for-this-server-even-though-i-configured-a-backup-policy-br"></a><span data-ttu-id="1eb91-201">我收到 hello 警告時，「 Azure 備份尚未設定此伺服器 」，即使設定備份原則</span><span class="sxs-lookup"><span data-stu-id="1eb91-201">I receive hello warning, "Azure Backups have not been configured for this server" even though I configured a backup policy</span></span> <br/>
<span data-ttu-id="1eb91-202">Hello hello 本機伺服器上儲存的備份排程設定不的 hello 與相同 hello hello 備份保存庫中儲存的設定時，就會發生這個警告。</span><span class="sxs-lookup"><span data-stu-id="1eb91-202">This warning occurs when hello backup schedule settings stored on hello local server are not hello same as hello settings stored in hello backup vault.</span></span> <span data-ttu-id="1eb91-203">當伺服器 hello 或 hello 設定已復原的 tooa 已知良好的狀態時，hello 備份排程可能會失去同步處理。</span><span class="sxs-lookup"><span data-stu-id="1eb91-203">When either hello server or hello settings have been recovered tooa known good state, hello backup schedules can lose synchronization.</span></span> <span data-ttu-id="1eb91-204">如果您收到這個警告，[重新設定備份原則的 hello](backup-azure-manage-windows-server.md)然後**立即執行備份**tooresynchronize hello 本機伺服器與 Azure。</span><span class="sxs-lookup"><span data-stu-id="1eb91-204">If you receive this warning, [reconfigure hello backup policy](backup-azure-manage-windows-server.md) and then **Run Back Up Now** tooresynchronize hello local server with Azure.</span></span>
