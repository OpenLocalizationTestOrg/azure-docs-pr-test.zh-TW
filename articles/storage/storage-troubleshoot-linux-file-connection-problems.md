---
title: "針對 Linux 中的 Azure 檔案儲存體問題進行疑難排解 | Microsoft Docs"
description: "針對 Linux 中的 Azure 檔案儲存體問題進行疑難排解"
services: storage
documentationcenter: 
author: genlin
manager: willchen
editor: na
tags: storage
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: genli
ms.openlocfilehash: 62cd62ec3a2900f06acacc0852a48b5e3ff1c8cd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-linux"></a><span data-ttu-id="5d229-103">針對 Linux 中的 Azure 檔案儲存體問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="5d229-103">Troubleshoot Azure File storage problems in Linux</span></span>

<span data-ttu-id="5d229-104">本文列出當您從 Linux 用戶端連線時，與 Microsoft Azure 檔案儲存體相關的常見問題。</span><span class="sxs-lookup"><span data-stu-id="5d229-104">This article lists common problems that are related to Microsoft Azure File storage when you connect from Linux clients.</span></span> <span data-ttu-id="5d229-105">文中也會提供這些問題的可能原因和解決方案。</span><span class="sxs-lookup"><span data-stu-id="5d229-105">It also provides possible causes and resolutions for these problems.</span></span>

<a id="permissiondenied"></a>
## <a name="permission-denied-disk-quota-exceeded-when-you-try-to-open-a-file"></a><span data-ttu-id="5d229-106">當您嘗試開啟檔案時，「[使用權限被拒] 超出磁碟配額」</span><span class="sxs-lookup"><span data-stu-id="5d229-106">"[permission denied] Disk quota exceeded" when you try to open a file</span></span>

<span data-ttu-id="5d229-107">在 Linux 中，您會收到類似以下的錯誤訊息︰</span><span class="sxs-lookup"><span data-stu-id="5d229-107">In Linux, you receive an error message that resembles the following:</span></span>

<span data-ttu-id="5d229-108">**<filename> [使用權限被拒] 超出磁碟配額**</span><span class="sxs-lookup"><span data-stu-id="5d229-108">**<filename> [permission denied] Disk quota exceeded**</span></span>

### <a name="cause"></a><span data-ttu-id="5d229-109">原因</span><span class="sxs-lookup"><span data-stu-id="5d229-109">Cause</span></span>

<span data-ttu-id="5d229-110">您已達到檔案所允許的同時開啟控點上限。</span><span class="sxs-lookup"><span data-stu-id="5d229-110">You have reached the upper limit of concurrent open handles that are allowed for a file.</span></span>

### <a name="solution"></a><span data-ttu-id="5d229-111">方案</span><span class="sxs-lookup"><span data-stu-id="5d229-111">Solution</span></span>

<span data-ttu-id="5d229-112">關閉一些控點以減少同時開啟的控點數，然後再次嘗試操作。</span><span class="sxs-lookup"><span data-stu-id="5d229-112">Reduce the number of concurrent open handles by closing some handles, and then retry the operation.</span></span> <span data-ttu-id="5d229-113">如需詳細資訊，請參閱 [Microsoft Azure 儲存體效能與延展性檢查清單](storage-performance-checklist.md)。</span><span class="sxs-lookup"><span data-stu-id="5d229-113">For more information, see [Microsoft Azure Storage performance and scalability checklist](storage-performance-checklist.md).</span></span>

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-to-and-from-azure-file-storage-in-linux"></a><span data-ttu-id="5d229-114">從 Linux 中的 Azure 檔案儲存體複製檔案或將檔案複製到其中的速度變慢</span><span class="sxs-lookup"><span data-stu-id="5d229-114">Slow file copying to and from Azure File storage in Linux</span></span>

-   <span data-ttu-id="5d229-115">如果您沒有特定的 I/O 大小需求下限，建議您使用 1 MB 的 I/O 大小以獲得最佳效能。</span><span class="sxs-lookup"><span data-stu-id="5d229-115">If you don’t have a specific minimum I/O size requirement, we recommend that you use 1 MB as the I/O size for optimal performance.</span></span>
-   <span data-ttu-id="5d229-116">如果您知道擴充寫入檔案的最終大小，而且當檔案上未寫入的結尾中有零時您的軟體不會產生相容性問題，則請事先設定檔案大小，而不是將每次寫入設為擴充寫入。</span><span class="sxs-lookup"><span data-stu-id="5d229-116">If you know the final size of a file that you are extending by using writes, and your software doesn’t experience compatibility problems when an unwritten tail on the file contains zeros, then set the file size in advance instead of making every write an extending write.</span></span>
-   <span data-ttu-id="5d229-117">使用正確的複製方法：</span><span class="sxs-lookup"><span data-stu-id="5d229-117">Use the right copy method:</span></span>
    -   <span data-ttu-id="5d229-118">針對兩個檔案共用之間的所有傳輸，使用 [AzCopy](storage-use-azcopy.md#file-copy)。</span><span class="sxs-lookup"><span data-stu-id="5d229-118">Use [AzCopy](storage-use-azcopy.md#file-copy) for any transfer between two file shares.</span></span>
    -   <span data-ttu-id="5d229-119">在內部部署電腦上的檔案共用之間，使用 [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="5d229-119">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) between file shares on an on-premises computer.</span></span>

<a id="error112"></a>
## <a name="mount-error112-host-is-down-because-of-a-reconnection-time-out"></a><span data-ttu-id="5d229-120">因連線逾時而發生「掛接錯誤 (112)：主機已關機」</span><span class="sxs-lookup"><span data-stu-id="5d229-120">"Mount error(112): Host is down" because of a reconnection time-out</span></span>

<span data-ttu-id="5d229-121">當用戶端閒置很長時間時，Linux 用戶端上發生「112」掛接錯誤。</span><span class="sxs-lookup"><span data-stu-id="5d229-121">A "112" mount error occurs on the Linux client when the client has been idle for a long time.</span></span> <span data-ttu-id="5d229-122">加長閒置時間之後，用戶端中斷連線且連線逾時。</span><span class="sxs-lookup"><span data-stu-id="5d229-122">After extended idle time, the client disconnects and the connection times out.</span></span>  

### <a name="cause"></a><span data-ttu-id="5d229-123">原因</span><span class="sxs-lookup"><span data-stu-id="5d229-123">Cause</span></span>

<span data-ttu-id="5d229-124">連線可能因下列原因而閒置：</span><span class="sxs-lookup"><span data-stu-id="5d229-124">The connection can be idle for the following reasons:</span></span>

-   <span data-ttu-id="5d229-125">使用預設的「軟」掛接選項時，造成無法重新建立 TCP 連線以連線到伺服器的網路通訊失敗</span><span class="sxs-lookup"><span data-stu-id="5d229-125">Network communication failures that prevent re-establishing a TCP connection to the server when the default “soft” mount option is used</span></span>
-   <span data-ttu-id="5d229-126">未出現在較舊核心中的最近重新連線修正</span><span class="sxs-lookup"><span data-stu-id="5d229-126">Recent reconnection fixes that are not present in older kernels</span></span>

### <a name="solution"></a><span data-ttu-id="5d229-127">方案</span><span class="sxs-lookup"><span data-stu-id="5d229-127">Solution</span></span>

<span data-ttu-id="5d229-128">此 Linux 核心中的重新連線問題已隨下列變更修正：</span><span class="sxs-lookup"><span data-stu-id="5d229-128">This reconnection problem in the Linux kernel is now fixed as part of the following changes:</span></span>

- [<span data-ttu-id="5d229-129">修正重新連線在通訊端重新連線許久之後不會延遲 SMB3 工作階段重新連線 (英文)</span><span class="sxs-lookup"><span data-stu-id="5d229-129">Fix reconnect to not defer smb3 session reconnect long after socket reconnect</span></span>](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/fs/cifs?id=4fcd1813e6404dd4420c7d12fb483f9320f0bf93)
-   [<span data-ttu-id="5d229-130">在通訊端重新連線之後立即呼叫 Echo 服務 (英文)</span><span class="sxs-lookup"><span data-stu-id="5d229-130">Call echo service immediately after socket reconnect</span></span>](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=b8c600120fc87d53642476f48c8055b38d6e14c7)
-   [<span data-ttu-id="5d229-131">CIFS：修正重新連線期間可能發生的記憶體損毀 (英文)</span><span class="sxs-lookup"><span data-stu-id="5d229-131">CIFS: Fix a possible memory corruption during reconnect</span></span>](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=53e0e11efe9289535b060a51d4cf37c25e0d0f2b)
-   <span data-ttu-id="5d229-132">[CIFS：修正重新連線期間可能發生的 Mutex 雙重鎖定 (針對核心 4.9 版與更新版本)](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="5d229-132">[CIFS: Fix a possible double locking of mutex during reconnect (for kernel v4.9 and later)](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183)</span></span>

<span data-ttu-id="5d229-133">但是，這些變更可能尚未移植到所有 Linux 發行版本。</span><span class="sxs-lookup"><span data-stu-id="5d229-133">However, these changes might not be ported yet to all the Linux distributions.</span></span> <span data-ttu-id="5d229-134">此修正和其他重新連線修正在下列常見 Linux 核心中進行：4.4.40、4.8.16 和 4.9.1.</span><span class="sxs-lookup"><span data-stu-id="5d229-134">This fix and other reconnection fixes are made in the following popular Linux kernels: 4.4.40, 4.8.16, and 4.9.1.</span></span> <span data-ttu-id="5d229-135">您可以升級至其中一個建議的核心版本，以完成此修正。</span><span class="sxs-lookup"><span data-stu-id="5d229-135">You can get this fix by upgrading to one of these recommended kernel versions.</span></span>

### <a name="workaround"></a><span data-ttu-id="5d229-136">因應措施</span><span class="sxs-lookup"><span data-stu-id="5d229-136">Workaround</span></span>

<span data-ttu-id="5d229-137">您可以指定硬掛接，以解決此問題。</span><span class="sxs-lookup"><span data-stu-id="5d229-137">You can work around this problem by specifying a hard mount.</span></span> <span data-ttu-id="5d229-138">這會強制用戶端一直等候直到連線建立或明確中斷，而且它可用來防止因為網路逾時而發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="5d229-138">This forces the client to wait until a connection is established or until it’s explicitly interrupted and can be used to prevent errors because of network time-outs.</span></span> <span data-ttu-id="5d229-139">不過，這個因應措施可能會導致無限期等候。</span><span class="sxs-lookup"><span data-stu-id="5d229-139">However, this workaround might cause indefinite waits.</span></span> <span data-ttu-id="5d229-140">請準備好視需要停止連線。</span><span class="sxs-lookup"><span data-stu-id="5d229-140">Be prepared to stop connections as necessary.</span></span>

<span data-ttu-id="5d229-141">如果您無法升級至最新的核心版本，您可以使用下列因應措施解決此問題：在 Azure 檔案共用中保留一個每 30 秒 (或更短時間) 就會寫入的檔案。</span><span class="sxs-lookup"><span data-stu-id="5d229-141">If you cannot upgrade to the latest kernel versions, you can work around this problem by keeping a file in the Azure file share that you write to every 30 seconds or less.</span></span> <span data-ttu-id="5d229-142">這必須是寫入作業，例如重寫檔案的建立或修改日期。</span><span class="sxs-lookup"><span data-stu-id="5d229-142">This must be a write operation, such as rewriting the created or modified date on the file.</span></span> <span data-ttu-id="5d229-143">否則，您可能會取得快取的結果，而您的作業可能不會觸發重新連線。</span><span class="sxs-lookup"><span data-stu-id="5d229-143">Otherwise, you might get cached results, and your operation might not trigger the reconnection.</span></span>

<a id="error115"></a>
## <a name="mount-error115-operation-now-in-progress-when-you-mount-azure-file-storage-by-using-smb-30"></a><span data-ttu-id="5d229-144">當您使用 SMB 3.0 掛接 Azure 檔案儲存體時，發生「掛接錯誤 (115)：作業進行中」</span><span class="sxs-lookup"><span data-stu-id="5d229-144">"Mount error(115): Operation now in progress" when you mount Azure File storage by using SMB 3.0</span></span>

### <a name="cause"></a><span data-ttu-id="5d229-145">原因</span><span class="sxs-lookup"><span data-stu-id="5d229-145">Cause</span></span>

<span data-ttu-id="5d229-146">某些 Linux 散發套件尚未支援 SMB 3.0 的加密功能，如果使用者因為功能遺失而嘗試使用 SMB 3.0 來掛接 Azure 檔案儲存體，可能會收到「115」錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="5d229-146">Some Linux distributions do not yet support encryption features in SMB 3.0 and users might receive a "115" error message if they try to mount Azure File storage by using SMB 3.0 because of a missing feature.</span></span>

### <a name="solution"></a><span data-ttu-id="5d229-147">方案</span><span class="sxs-lookup"><span data-stu-id="5d229-147">Solution</span></span>

<span data-ttu-id="5d229-148">4.11 核心推出 Linux 的 SMB 3.0 適用的加密功能。</span><span class="sxs-lookup"><span data-stu-id="5d229-148">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="5d229-149">此功能讓您可從內部部署或不同 Azure 區域的 Azure 檔案共用進行掛接。</span><span class="sxs-lookup"><span data-stu-id="5d229-149">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="5d229-150">發佈時，這項功能已向前移植到 Ubuntu 17.04 和 Ubuntu 16.10。</span><span class="sxs-lookup"><span data-stu-id="5d229-150">At the time of publishing, this functionality has been backported to Ubuntu 17.04 and Ubuntu 16.10.</span></span> <span data-ttu-id="5d229-151">如果您的 Linux SMB 用戶端不支援加密，在與檔案儲存體帳戶相同的資料中心上，從 Azure Linux VM 使用 SMB 2.1 掛接 Azure 檔案儲存體。</span><span class="sxs-lookup"><span data-stu-id="5d229-151">If your Linux SMB client does not support encryption, mount Azure File storage by using SMB 2.1 from an Azure Linux VM that's in the same datacenter as the File storage account.</span></span>

<a id="slowperformance"></a>
## <a name="slow-performance-on-an-azure-file-share-mounted-on-a-linux-vm"></a><span data-ttu-id="5d229-152">掛接在 Linux VM 上的 Azure 檔案共用效能變慢</span><span class="sxs-lookup"><span data-stu-id="5d229-152">Slow performance on an Azure file share mounted on a Linux VM</span></span>

### <a name="cause"></a><span data-ttu-id="5d229-153">原因</span><span class="sxs-lookup"><span data-stu-id="5d229-153">Cause</span></span>

<span data-ttu-id="5d229-154">效能變慢可能的一個原因是已停用快取。</span><span class="sxs-lookup"><span data-stu-id="5d229-154">One possible cause of slow performance is disabled caching.</span></span>

### <a name="solution"></a><span data-ttu-id="5d229-155">方案</span><span class="sxs-lookup"><span data-stu-id="5d229-155">Solution</span></span>

<span data-ttu-id="5d229-156">若要查看是否停用快取，請尋找 **cache=** 項目。</span><span class="sxs-lookup"><span data-stu-id="5d229-156">To check whether caching is disabled, look for the **cache=** entry.</span></span> 

<span data-ttu-id="5d229-157">**Cache=none** 表示已停用快取。</span><span class="sxs-lookup"><span data-stu-id="5d229-157">**Cache=none** indicates that caching is disabled.</span></span>  <span data-ttu-id="5d229-158">使用預設的 mount 命令或明確地為 mount 命令加上 **cache=strict** 選項來重新掛接共用，以確保啟用預設快取或 "strict" 快取模式。</span><span class="sxs-lookup"><span data-stu-id="5d229-158">Remount the share by using the default mount command or by explicitly adding the **cache=strict** option to the mount command to ensure that default caching or "strict" caching mode is enabled.</span></span>

<span data-ttu-id="5d229-159">在某些情況下，**serverino** 掛接選項可能導致 **ls** 命令對每個目錄項目執行 stat。</span><span class="sxs-lookup"><span data-stu-id="5d229-159">In some scenarios, the **serverino** mount option can cause the **ls** command to run stat against every directory entry.</span></span> <span data-ttu-id="5d229-160">當您要列出大型目錄時，這個行為會導致效能降低。</span><span class="sxs-lookup"><span data-stu-id="5d229-160">This behavior results in performance degradation when you're listing a big directory.</span></span> <span data-ttu-id="5d229-161">您可以檢查 **/etc/fstab** 項目中的掛接選項：</span><span class="sxs-lookup"><span data-stu-id="5d229-161">You can check the mount options in your **/etc/fstab** entry:</span></span>

`//azureuser.file.core.windows.net/cifs /cifs cifs vers=3.0,serverino,username=xxx,password=xxx,dir_mode=0777,file_mode=0777`

<span data-ttu-id="5d229-162">您也可以執行 **sudo mount | grep cifs** 命令並檢查其輸出 \(例如以下範例輸出\)，來檢查是否使用正確的選項：</span><span class="sxs-lookup"><span data-stu-id="5d229-162">You can also check whether the correct options are being used by running the  **sudo mount | grep cifs** command and checking its output, such as the following example output:</span></span>

`//mabiccacifs.file.core.windows.net/cifs on /cifs type cifs (rw,relatime,vers=3.0,sec=ntlmssp,cache=strict,username=xxx,domain=X,uid=0,noforceuid,gid=0,noforcegid,addr=192.168.10.1,file_mode=0777, dir_mode=0777,persistenthandles,nounix,serverino,mapposix,rsize=1048576,wsize=1048576,actimeo=1)`

<span data-ttu-id="5d229-163">如果沒有 **cache=strict** 或 **serverino** 選項，請執行[文件](storage-how-to-use-files-linux.md)中的掛接命令，將 Azure 檔案儲存體卸載並再次掛接。</span><span class="sxs-lookup"><span data-stu-id="5d229-163">If the **cache=strict** or **serverino** option is not present, unmount and mount Azure File storage again by running the mount command from the [documentation](storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="5d229-164">然後，重新檢查 **/etc/fstab** 項目是否有正確的選項。</span><span class="sxs-lookup"><span data-stu-id="5d229-164">Then, recheck that the **/etc/fstab** entry has the correct options.</span></span>

<a id="timestampslost"></a>
## <a name="time-stamps-were-lost-in-copying-files-from-windows-to-linux"></a><span data-ttu-id="5d229-165">將檔案從 Windows 複製到 Linux 時，遺失時間戳記</span><span class="sxs-lookup"><span data-stu-id="5d229-165">Time stamps were lost in copying files from Windows to Linux</span></span>

<span data-ttu-id="5d229-166">在 Linux/Unix 平台上，如果檔案 1 和檔案 2 由不同的使用者所擁有，**cp -p** 命令會失敗。</span><span class="sxs-lookup"><span data-stu-id="5d229-166">On Linux/Unix platforms, the **cp -p** command fails if file 1 and file 2 are owned by different users.</span></span>

### <a name="cause"></a><span data-ttu-id="5d229-167">原因</span><span class="sxs-lookup"><span data-stu-id="5d229-167">Cause</span></span>

<span data-ttu-id="5d229-168">COPYFILE 中的強制旗標 **f** 會導致在 Unix 上執行 **cp -p -f**。</span><span class="sxs-lookup"><span data-stu-id="5d229-168">The force flag **f** in COPYFILE results in executing **cp -p -f** on Unix.</span></span> <span data-ttu-id="5d229-169">此命令也無法保留您並不擁有之檔案的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="5d229-169">This command also fails to preserve the time stamp of the file that you don't own.</span></span>

### <a name="workaround"></a><span data-ttu-id="5d229-170">因應措施</span><span class="sxs-lookup"><span data-stu-id="5d229-170">Workaround</span></span>

<span data-ttu-id="5d229-171">使用儲存體帳戶使用者來複製檔案：</span><span class="sxs-lookup"><span data-stu-id="5d229-171">Use the storage account user for copying the files:</span></span>

- `Useadd : [storage account name]`
- `Passwd [storage account name]`
- `Su [storage account name]`
- `Cp -p filename.txt /share`

## <a name="need-help-contact-support"></a><span data-ttu-id="5d229-172">需要協助嗎？</span><span class="sxs-lookup"><span data-stu-id="5d229-172">Need help?</span></span> <span data-ttu-id="5d229-173">請連絡支援人員。</span><span class="sxs-lookup"><span data-stu-id="5d229-173">Contact support.</span></span>

<span data-ttu-id="5d229-174">如果仍需要協助，請[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)以快速解決您的問題。</span><span class="sxs-lookup"><span data-stu-id="5d229-174">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your problem resolved quickly.</span></span>
