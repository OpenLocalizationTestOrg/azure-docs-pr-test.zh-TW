---
title: "在 Linux 中的 aaaTroubleshoot Azure 檔案儲存體問題 |Microsoft 文件"
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
ms.openlocfilehash: 3dc537d714244451a5ff8e01f4a27f03873cf2fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-linux"></a><span data-ttu-id="6f24e-103">針對 Linux 中的 Azure 檔案儲存體問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="6f24e-103">Troubleshoot Azure File storage problems in Linux</span></span>

<span data-ttu-id="6f24e-104">本文列出常見的問題，則相關的 tooMicrosoft Azure 檔案儲存體，當您從 Linux 用戶端連接。</span><span class="sxs-lookup"><span data-stu-id="6f24e-104">This article lists common problems that are related tooMicrosoft Azure File storage when you connect from Linux clients.</span></span> <span data-ttu-id="6f24e-105">文中也會提供這些問題的可能原因和解決方案。</span><span class="sxs-lookup"><span data-stu-id="6f24e-105">It also provides possible causes and resolutions for these problems.</span></span>

<a id="permissiondenied"></a>
## <a name="permission-denied-disk-quota-exceeded-when-you-try-tooopen-a-file"></a><span data-ttu-id="6f24e-106">「 超過 [拒絕的權限] 磁碟配額 」 您試著 tooopen 檔案</span><span class="sxs-lookup"><span data-stu-id="6f24e-106">"[permission denied] Disk quota exceeded" when you try tooopen a file</span></span>

<span data-ttu-id="6f24e-107">在 Linux，您會收到類似 hello 下列的錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="6f24e-107">In Linux, you receive an error message that resembles hello following:</span></span>

<span data-ttu-id="6f24e-108">**<filename> [使用權限被拒] 超出磁碟配額**</span><span class="sxs-lookup"><span data-stu-id="6f24e-108">**<filename> [permission denied] Disk quota exceeded**</span></span>

### <a name="cause"></a><span data-ttu-id="6f24e-109">原因</span><span class="sxs-lookup"><span data-stu-id="6f24e-109">Cause</span></span>

<span data-ttu-id="6f24e-110">您已達到上限同時開啟的控制代碼所允許的檔案 hello。</span><span class="sxs-lookup"><span data-stu-id="6f24e-110">You have reached hello upper limit of concurrent open handles that are allowed for a file.</span></span>

### <a name="solution"></a><span data-ttu-id="6f24e-111">方案</span><span class="sxs-lookup"><span data-stu-id="6f24e-111">Solution</span></span>

<span data-ttu-id="6f24e-112">減少 hello 數目同時開啟的控制代碼關閉某些控點，然後再重試 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="6f24e-112">Reduce hello number of concurrent open handles by closing some handles, and then retry hello operation.</span></span> <span data-ttu-id="6f24e-113">如需詳細資訊，請參閱 [Microsoft Azure 儲存體效能與延展性檢查清單](storage-performance-checklist.md)。</span><span class="sxs-lookup"><span data-stu-id="6f24e-113">For more information, see [Microsoft Azure Storage performance and scalability checklist](storage-performance-checklist.md).</span></span>

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-linux"></a><span data-ttu-id="6f24e-114">複製 tooand 從 linux 的 Azure 檔案儲存體的緩慢檔案</span><span class="sxs-lookup"><span data-stu-id="6f24e-114">Slow file copying tooand from Azure File storage in Linux</span></span>

-   <span data-ttu-id="6f24e-115">如果您沒有特定的最小 I/O 大小需求，我們建議您使用的是 1 MB，如 hello I/O 大小，以獲得最佳效能。</span><span class="sxs-lookup"><span data-stu-id="6f24e-115">If you don’t have a specific minimum I/O size requirement, we recommend that you use 1 MB as hello I/O size for optimal performance.</span></span>
-   <span data-ttu-id="6f24e-116">如果您知道 hello 最終大小，您會使用寫入時，擴充的檔案，而且您的軟體不會遇到相容性問題，當 security 的結尾 hello 檔案上包含零，然後設定事先而不是進行每次寫入延伸的 hello 檔案大小撰寫。</span><span class="sxs-lookup"><span data-stu-id="6f24e-116">If you know hello final size of a file that you are extending by using writes, and your software doesn’t experience compatibility problems when an unwritten tail on hello file contains zeros, then set hello file size in advance instead of making every write an extending write.</span></span>
-   <span data-ttu-id="6f24e-117">使用 hello 右複製方法：</span><span class="sxs-lookup"><span data-stu-id="6f24e-117">Use hello right copy method:</span></span>
    -   <span data-ttu-id="6f24e-118">針對兩個檔案共用之間的所有傳輸，使用 [AzCopy](storage-use-azcopy.md#file-copy)。</span><span class="sxs-lookup"><span data-stu-id="6f24e-118">Use [AzCopy](storage-use-azcopy.md#file-copy) for any transfer between two file shares.</span></span>
    -   <span data-ttu-id="6f24e-119">在內部部署電腦上的檔案共用之間，使用 [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="6f24e-119">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) between file shares on an on-premises computer.</span></span>

<a id="error112"></a>
## <a name="mount-error112-host-is-down-because-of-a-reconnection-time-out"></a><span data-ttu-id="6f24e-120">因連線逾時而發生「掛接錯誤 (112)：主機已關機」</span><span class="sxs-lookup"><span data-stu-id="6f24e-120">"Mount error(112): Host is down" because of a reconnection time-out</span></span>

<span data-ttu-id="6f24e-121">是"112"掛上發生錯誤 hello Linux 用戶端 hello 用戶端已經閒置很長的時間。</span><span class="sxs-lookup"><span data-stu-id="6f24e-121">A "112" mount error occurs on hello Linux client when hello client has been idle for a long time.</span></span> <span data-ttu-id="6f24e-122">擴充的閒置時間之後, hello 用戶端中斷連接和 hello 連接逾時。</span><span class="sxs-lookup"><span data-stu-id="6f24e-122">After extended idle time, hello client disconnects and hello connection times out.</span></span>  

### <a name="cause"></a><span data-ttu-id="6f24e-123">原因</span><span class="sxs-lookup"><span data-stu-id="6f24e-123">Cause</span></span>

<span data-ttu-id="6f24e-124">hello 連接可閒置的 hello 下列原因：</span><span class="sxs-lookup"><span data-stu-id="6f24e-124">hello connection can be idle for hello following reasons:</span></span>

-   <span data-ttu-id="6f24e-125">避免使用 hello 預設 「 軟式 」 掛接選項時，重新建立 TCP 連線 toohello 伺服器的網路通訊失敗</span><span class="sxs-lookup"><span data-stu-id="6f24e-125">Network communication failures that prevent re-establishing a TCP connection toohello server when hello default “soft” mount option is used</span></span>
-   <span data-ttu-id="6f24e-126">未出現在較舊核心中的最近重新連線修正</span><span class="sxs-lookup"><span data-stu-id="6f24e-126">Recent reconnection fixes that are not present in older kernels</span></span>

### <a name="solution"></a><span data-ttu-id="6f24e-127">方案</span><span class="sxs-lookup"><span data-stu-id="6f24e-127">Solution</span></span>

<span data-ttu-id="6f24e-128">這個 hello Linux 核心中的重新連線問題現在已修正一部分 hello 下列變更：</span><span class="sxs-lookup"><span data-stu-id="6f24e-128">This reconnection problem in hello Linux kernel is now fixed as part of hello following changes:</span></span>

- [<span data-ttu-id="6f24e-129">修正重新連線 toonot 延遲 smb3 工作階段重新連線長時間之後重新連線通訊端</span><span class="sxs-lookup"><span data-stu-id="6f24e-129">Fix reconnect toonot defer smb3 session reconnect long after socket reconnect</span></span>](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/fs/cifs?id=4fcd1813e6404dd4420c7d12fb483f9320f0bf93)
-   [<span data-ttu-id="6f24e-130">在通訊端重新連線之後立即呼叫 Echo 服務 (英文)</span><span class="sxs-lookup"><span data-stu-id="6f24e-130">Call echo service immediately after socket reconnect</span></span>](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=b8c600120fc87d53642476f48c8055b38d6e14c7)
-   [<span data-ttu-id="6f24e-131">CIFS：修正重新連線期間可能發生的記憶體損毀 (英文)</span><span class="sxs-lookup"><span data-stu-id="6f24e-131">CIFS: Fix a possible memory corruption during reconnect</span></span>](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=53e0e11efe9289535b060a51d4cf37c25e0d0f2b)
-   <span data-ttu-id="6f24e-132">[CIFS：修正重新連線期間可能發生的 Mutex 雙重鎖定 (針對核心 4.9 版與更新版本)](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="6f24e-132">[CIFS: Fix a possible double locking of mutex during reconnect (for kernel v4.9 and later)](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183)</span></span>

<span data-ttu-id="6f24e-133">不過，尚未 tooall hello Linux 散發套件，可能無法移植這些變更。</span><span class="sxs-lookup"><span data-stu-id="6f24e-133">However, these changes might not be ported yet tooall hello Linux distributions.</span></span> <span data-ttu-id="6f24e-134">下列常用的 Linux 核心 hello 做此修正程式和其他重新連線修正： 4.4.40、 4.8.16 和 4.9.1。</span><span class="sxs-lookup"><span data-stu-id="6f24e-134">This fix and other reconnection fixes are made in hello following popular Linux kernels: 4.4.40, 4.8.16, and 4.9.1.</span></span> <span data-ttu-id="6f24e-135">您可以升級 tooone 這些建議的核心版本來取得此修正程式。</span><span class="sxs-lookup"><span data-stu-id="6f24e-135">You can get this fix by upgrading tooone of these recommended kernel versions.</span></span>

### <a name="workaround"></a><span data-ttu-id="6f24e-136">因應措施</span><span class="sxs-lookup"><span data-stu-id="6f24e-136">Workaround</span></span>

<span data-ttu-id="6f24e-137">您可以指定硬掛接，以解決此問題。</span><span class="sxs-lookup"><span data-stu-id="6f24e-137">You can work around this problem by specifying a hard mount.</span></span> <span data-ttu-id="6f24e-138">這會強制 hello 用戶端 toowait 建立連接或明確地中斷，並可能會使用的 tooprevent 錯誤，因為網路逾時為止。</span><span class="sxs-lookup"><span data-stu-id="6f24e-138">This forces hello client toowait until a connection is established or until it’s explicitly interrupted and can be used tooprevent errors because of network time-outs.</span></span> <span data-ttu-id="6f24e-139">不過，這個因應措施可能會導致無限期等候。</span><span class="sxs-lookup"><span data-stu-id="6f24e-139">However, this workaround might cause indefinite waits.</span></span> <span data-ttu-id="6f24e-140">是必要的已備妥的 toostop 連線。</span><span class="sxs-lookup"><span data-stu-id="6f24e-140">Be prepared toostop connections as necessary.</span></span>

<span data-ttu-id="6f24e-141">您無法升級 toohello 最新的核心版本，可以保持在 hello Azure 檔案共用，您必須撰寫 tooevery 30 秒或更短的檔案來解決這個問題。</span><span class="sxs-lookup"><span data-stu-id="6f24e-141">If you cannot upgrade toohello latest kernel versions, you can work around this problem by keeping a file in hello Azure file share that you write tooevery 30 seconds or less.</span></span> <span data-ttu-id="6f24e-142">這必須是寫入作業，例如重寫 hello 建立或修改 hello 檔案上的日期。</span><span class="sxs-lookup"><span data-stu-id="6f24e-142">This must be a write operation, such as rewriting hello created or modified date on hello file.</span></span> <span data-ttu-id="6f24e-143">否則，您可能會收到快取的結果，而且您的作業可能不會觸發 hello 重新連線。</span><span class="sxs-lookup"><span data-stu-id="6f24e-143">Otherwise, you might get cached results, and your operation might not trigger hello reconnection.</span></span>

<a id="error115"></a>
## <a name="mount-error115-operation-now-in-progress-when-you-mount-azure-file-storage-by-using-smb-30"></a><span data-ttu-id="6f24e-144">當您使用 SMB 3.0 掛接 Azure 檔案儲存體時，發生「掛接錯誤 (115)：作業進行中」</span><span class="sxs-lookup"><span data-stu-id="6f24e-144">"Mount error(115): Operation now in progress" when you mount Azure File storage by using SMB 3.0</span></span>

### <a name="cause"></a><span data-ttu-id="6f24e-145">原因</span><span class="sxs-lookup"><span data-stu-id="6f24e-145">Cause</span></span>

<span data-ttu-id="6f24e-146">某些 Linux 發行版本目前還不支援加密功能 SMB 3.0 中，如果嘗試 toomount Azure 檔案儲存體使用 SMB 3.0，因為遺漏的功能，使用者可能會收到 「 115 」 錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="6f24e-146">Some Linux distributions do not yet support encryption features in SMB 3.0 and users might receive a "115" error message if they try toomount Azure File storage by using SMB 3.0 because of a missing feature.</span></span>

### <a name="solution"></a><span data-ttu-id="6f24e-147">方案</span><span class="sxs-lookup"><span data-stu-id="6f24e-147">Solution</span></span>

<span data-ttu-id="6f24e-148">4.11 核心推出 Linux 的 SMB 3.0 適用的加密功能。</span><span class="sxs-lookup"><span data-stu-id="6f24e-148">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="6f24e-149">此功能讓您可從內部部署或不同 Azure 區域的 Azure 檔案共用進行掛接。</span><span class="sxs-lookup"><span data-stu-id="6f24e-149">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="6f24e-150">在發行的 hello 階段，這項功能已被 backported tooUbuntu 17.04 和 Ubuntu 16.10。</span><span class="sxs-lookup"><span data-stu-id="6f24e-150">At hello time of publishing, this functionality has been backported tooUbuntu 17.04 and Ubuntu 16.10.</span></span> <span data-ttu-id="6f24e-151">如果您的 Linux SMB 用戶端不支援加密，裝載 Azure 檔案儲存體使用從 Azure Linux VM 所在的 SMB 2.1 hello 相同的資料中心，因為 hello 檔案儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6f24e-151">If your Linux SMB client does not support encryption, mount Azure File storage by using SMB 2.1 from an Azure Linux VM that's in hello same datacenter as hello File storage account.</span></span>

<a id="slowperformance"></a>
## <a name="slow-performance-on-an-azure-file-share-mounted-on-a-linux-vm"></a><span data-ttu-id="6f24e-152">掛接在 Linux VM 上的 Azure 檔案共用效能變慢</span><span class="sxs-lookup"><span data-stu-id="6f24e-152">Slow performance on an Azure file share mounted on a Linux VM</span></span>

### <a name="cause"></a><span data-ttu-id="6f24e-153">原因</span><span class="sxs-lookup"><span data-stu-id="6f24e-153">Cause</span></span>

<span data-ttu-id="6f24e-154">效能變慢可能的一個原因是已停用快取。</span><span class="sxs-lookup"><span data-stu-id="6f24e-154">One possible cause of slow performance is disabled caching.</span></span>

### <a name="solution"></a><span data-ttu-id="6f24e-155">方案</span><span class="sxs-lookup"><span data-stu-id="6f24e-155">Solution</span></span>

<span data-ttu-id="6f24e-156">toocheck 是否已停用快取，尋找 hello**快取 =**項目。</span><span class="sxs-lookup"><span data-stu-id="6f24e-156">toocheck whether caching is disabled, look for hello **cache=** entry.</span></span> 

<span data-ttu-id="6f24e-157">**Cache=none** 表示已停用快取。</span><span class="sxs-lookup"><span data-stu-id="6f24e-157">**Cache=none** indicates that caching is disabled.</span></span>  <span data-ttu-id="6f24e-158">重新掛接 hello 共用使用 hello 預設 mount 命令，或明確加入 hello**快取 = strict**選項 toohello 掛接命令 tooensure 預設快取或"strict"快取模式會啟用。</span><span class="sxs-lookup"><span data-stu-id="6f24e-158">Remount hello share by using hello default mount command or by explicitly adding hello **cache=strict** option toohello mount command tooensure that default caching or "strict" caching mode is enabled.</span></span>

<span data-ttu-id="6f24e-159">在某些情況下，hello **serverino**裝載選項會使 hello **ls**命令 toorun stat 針對每個目錄項目。</span><span class="sxs-lookup"><span data-stu-id="6f24e-159">In some scenarios, hello **serverino** mount option can cause hello **ls** command toorun stat against every directory entry.</span></span> <span data-ttu-id="6f24e-160">當您要列出大型目錄時，這個行為會導致效能降低。</span><span class="sxs-lookup"><span data-stu-id="6f24e-160">This behavior results in performance degradation when you're listing a big directory.</span></span> <span data-ttu-id="6f24e-161">您可以檢查 hello 掛接選項，您**/etc/hosts fstab**項目：</span><span class="sxs-lookup"><span data-stu-id="6f24e-161">You can check hello mount options in your **/etc/fstab** entry:</span></span>

`//azureuser.file.core.windows.net/cifs /cifs cifs vers=3.0,serverino,username=xxx,password=xxx,dir_mode=0777,file_mode=0777`

<span data-ttu-id="6f24e-162">您也可以檢查是否正在使用 hello 正確的選項執行 hello **sudo 掛接 | grep cifs**命令，並檢查其輸出，例如下列範例輸出的 hello:</span><span class="sxs-lookup"><span data-stu-id="6f24e-162">You can also check whether hello correct options are being used by running hello  **sudo mount | grep cifs** command and checking its output, such as hello following example output:</span></span>

`//mabiccacifs.file.core.windows.net/cifs on /cifs type cifs (rw,relatime,vers=3.0,sec=ntlmssp,cache=strict,username=xxx,domain=X,uid=0,noforceuid,gid=0,noforcegid,addr=192.168.10.1,file_mode=0777, dir_mode=0777,persistenthandles,nounix,serverino,mapposix,rsize=1048576,wsize=1048576,actimeo=1)`

<span data-ttu-id="6f24e-163">如果 hello**快取 = strict**或**serverino**選項是不存在、 卸載和從 hello 執行 hello mount 命令再次掛接 Azure 檔案儲存體[文件](storage-how-to-use-files-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="6f24e-163">If hello **cache=strict** or **serverino** option is not present, unmount and mount Azure File storage again by running hello mount command from hello [documentation](storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="6f24e-164">然後，重新檢查該 hello **/etc/hosts fstab**項目都有 hello 正確的選項。</span><span class="sxs-lookup"><span data-stu-id="6f24e-164">Then, recheck that hello **/etc/fstab** entry has hello correct options.</span></span>

<a id="timestampslost"></a>
## <a name="time-stamps-were-lost-in-copying-files-from-windows-toolinux"></a><span data-ttu-id="6f24e-165">在中從 Windows tooLinux 複製的檔案遺失時間戳記</span><span class="sxs-lookup"><span data-stu-id="6f24e-165">Time stamps were lost in copying files from Windows tooLinux</span></span>

<span data-ttu-id="6f24e-166">Linux/Unix 平台上，hello **cp-p**如果檔案 1 和 2 的檔案不同的使用者所擁有，命令就會失敗。</span><span class="sxs-lookup"><span data-stu-id="6f24e-166">On Linux/Unix platforms, hello **cp -p** command fails if file 1 and file 2 are owned by different users.</span></span>

### <a name="cause"></a><span data-ttu-id="6f24e-167">原因</span><span class="sxs-lookup"><span data-stu-id="6f24e-167">Cause</span></span>

<span data-ttu-id="6f24e-168">hello force 旗標**f** COPYFILE 中導致執行**cp-p f**在 Unix 上。</span><span class="sxs-lookup"><span data-stu-id="6f24e-168">hello force flag **f** in COPYFILE results in executing **cp -p -f** on Unix.</span></span> <span data-ttu-id="6f24e-169">此命令也會失敗，您並不擁有 hello 檔案 toopreserve hello 時間戳記。</span><span class="sxs-lookup"><span data-stu-id="6f24e-169">This command also fails toopreserve hello time stamp of hello file that you don't own.</span></span>

### <a name="workaround"></a><span data-ttu-id="6f24e-170">因應措施</span><span class="sxs-lookup"><span data-stu-id="6f24e-170">Workaround</span></span>

<span data-ttu-id="6f24e-171">使用 hello 儲存體帳戶的使用者複製 hello 檔案：</span><span class="sxs-lookup"><span data-stu-id="6f24e-171">Use hello storage account user for copying hello files:</span></span>

- `Useadd : [storage account name]`
- `Passwd [storage account name]`
- `Su [storage account name]`
- `Cp -p filename.txt /share`

## <a name="need-help-contact-support"></a><span data-ttu-id="6f24e-172">需要協助嗎？</span><span class="sxs-lookup"><span data-stu-id="6f24e-172">Need help?</span></span> <span data-ttu-id="6f24e-173">請連絡支援人員。</span><span class="sxs-lookup"><span data-stu-id="6f24e-173">Contact support.</span></span>

<span data-ttu-id="6f24e-174">如果您仍需要協助，[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)tooget 快速解決問題。</span><span class="sxs-lookup"><span data-stu-id="6f24e-174">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your problem resolved quickly.</span></span>
