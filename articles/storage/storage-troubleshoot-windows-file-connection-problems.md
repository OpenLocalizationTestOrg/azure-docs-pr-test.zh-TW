---
title: "在 Windows 中的 aaaTroubleshoot Azure 檔案儲存體問題 |Microsoft 文件"
description: "針對 Windows 中的 Azure 檔案儲存體問題進行疑難排解"
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
ms.date: 06/28/2017
ms.author: genli
ms.openlocfilehash: ba0315d1add76a27fec93a9aee3aa99ccb7fa164
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-windows"></a><span data-ttu-id="32686-103">針對 Windows 中的 Azure 檔案儲存體問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="32686-103">Troubleshoot Azure File storage problems in Windows</span></span>

<span data-ttu-id="32686-104">本文列出常見的問題，則相關的 tooMicrosoft Azure 檔案儲存體，當您從 Windows 用戶端連接。</span><span class="sxs-lookup"><span data-stu-id="32686-104">This article lists common problems that are related tooMicrosoft Azure File storage when you connect from Windows clients.</span></span> <span data-ttu-id="32686-105">文中也會提供這些問題的可能原因和解決方案。</span><span class="sxs-lookup"><span data-stu-id="32686-105">It also provides possible causes and resolutions for these problems.</span></span> <span data-ttu-id="32686-106">此外 toohello 疑難排解這篇文章中的步驟，您也可以使用[AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5)以確保該 hello Windows 用戶端的環境具有正確的必要條件。</span><span class="sxs-lookup"><span data-stu-id="32686-106">In addition toohello troubleshooting steps in this article, you can also use [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) to ensure that hello Windows client environment has correct prerequisites.</span></span> <span data-ttu-id="32686-107">AzFileDiagnostics 會自動偵測大部份的本文中提到的 hello 徵狀以及可協助您環境的 tooget 最佳效能設定。</span><span class="sxs-lookup"><span data-stu-id="32686-107">AzFileDiagnostics automates detection of most of hello symptoms mentioned in this article and helps set up your environment tooget optimal performance.</span></span> <span data-ttu-id="32686-108">您也可以找到此資訊在 hello [Azure 檔案共用疑難排解](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares)提供步驟 tooassist 連接/對應/掛接 Azure 檔案共用您的問題。</span><span class="sxs-lookup"><span data-stu-id="32686-108">You can also find this information in hello [Azure Files shares Troubleshooter](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) that provides steps tooassist you with problems connecting/mapping/mounting Azure Files shares.</span></span>


<a id="error53-67-87"></a>
## <a name="error-53-error-67-or-error-87-when-you-mount-or-unmount-an-azure-file-share"></a><span data-ttu-id="32686-109">當您嘗試掛接或取消掛接 Azure 檔案共用時發生錯誤 53、錯誤 67 或錯誤 87</span><span class="sxs-lookup"><span data-stu-id="32686-109">Error 53, Error 67, or Error 87 when you mount or unmount an Azure file share</span></span>

<span data-ttu-id="32686-110">當您嘗試的 toomount 檔案共用從內部部署或不同資料中心時，您可能會收到下列錯誤 hello:</span><span class="sxs-lookup"><span data-stu-id="32686-110">When you try toomount a file share from on-premises or from a different datacenter, you might receive hello following errors:</span></span>

- <span data-ttu-id="32686-111">發生系統錯誤 53。</span><span class="sxs-lookup"><span data-stu-id="32686-111">System error 53 has occurred.</span></span> <span data-ttu-id="32686-112">找不到 hello 網路路徑。</span><span class="sxs-lookup"><span data-stu-id="32686-112">hello network path was not found.</span></span>
- <span data-ttu-id="32686-113">發生系統錯誤 67。</span><span class="sxs-lookup"><span data-stu-id="32686-113">System error 67 has occurred.</span></span> <span data-ttu-id="32686-114">找不到 hello 網路名稱。</span><span class="sxs-lookup"><span data-stu-id="32686-114">hello network name cannot be found.</span></span>
- <span data-ttu-id="32686-115">發生系統錯誤 87。</span><span class="sxs-lookup"><span data-stu-id="32686-115">System error 87 has occurred.</span></span> <span data-ttu-id="32686-116">hello 參數不正確。</span><span class="sxs-lookup"><span data-stu-id="32686-116">hello parameter is incorrect.</span></span>

### <a name="cause-1-unencrypted-communication-channel"></a><span data-ttu-id="32686-117">原因 1：通訊通道未加密</span><span class="sxs-lookup"><span data-stu-id="32686-117">Cause 1: Unencrypted communication channel</span></span>

<span data-ttu-id="32686-118">基於安全性理由，如果沒有加密 hello 通訊通道，並 hello 連接不嘗試從封鎖 tooAzure 檔案共用的連線 hello hello Azure 檔案共用所在的相同資料中心。</span><span class="sxs-lookup"><span data-stu-id="32686-118">For security reasons, connections tooAzure file shares are blocked if hello communication channel isn’t encrypted and if hello connection attempt isn't made from hello same datacenter where hello Azure file shares reside.</span></span> <span data-ttu-id="32686-119">只有當 hello 使用者的用戶端作業系統支援 SMB 加密，提供通訊通道加密。</span><span class="sxs-lookup"><span data-stu-id="32686-119">Communication channel encryption is provided only if hello user’s client OS supports SMB encryption.</span></span>

<span data-ttu-id="32686-120">Windows 8、Windows Server 2012 和更新版本的每個系統交涉都要求包含支援加密的 SMB 3.0。</span><span class="sxs-lookup"><span data-stu-id="32686-120">Windows 8, Windows Server 2012, and later versions of each system negotiate requests that include SMB 3.0, which supports encryption.</span></span>

### <a name="solution-for-cause-1"></a><span data-ttu-id="32686-121">原因 1 的解決方案</span><span class="sxs-lookup"><span data-stu-id="32686-121">Solution for cause 1</span></span>

<span data-ttu-id="32686-122">從沒有 hello 下列其中一種用戶端連線：</span><span class="sxs-lookup"><span data-stu-id="32686-122">Connect from a client that does one of hello following:</span></span>

- <span data-ttu-id="32686-123">符合 Windows 8 和 Windows Server 2012 或更新版本中的 hello 需求</span><span class="sxs-lookup"><span data-stu-id="32686-123">Meets hello requirements of Windows 8 and Windows Server 2012 or later versions</span></span>
- <span data-ttu-id="32686-124">會從 hello 中的虛擬機器連線相同資料中心為 hello hello Azure 檔案共用所使用的 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="32686-124">Connects from a virtual machine in hello same datacenter as hello Azure storage account that is used for hello Azure file share</span></span>

### <a name="cause-2-port-445-is-blocked"></a><span data-ttu-id="32686-125">原因 2：連接埠 445 遭到封鎖</span><span class="sxs-lookup"><span data-stu-id="32686-125">Cause 2: Port 445 is blocked</span></span>

<span data-ttu-id="32686-126">如果已封鎖連接埠 445 連出通訊 tooan Azure 檔案儲存體資料中心，會發生系統錯誤 53 或系統錯誤 67。</span><span class="sxs-lookup"><span data-stu-id="32686-126">System error 53 or system error 67 can occur if port 445 outbound communication tooan Azure File storage datacenter is blocked.</span></span> <span data-ttu-id="32686-127">允許或禁止存取連接埠 445 的 Isp toosee hello 摘要太移[TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx)。</span><span class="sxs-lookup"><span data-stu-id="32686-127">toosee hello summary of ISPs that allow or disallow access from port 445, go too[TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).</span></span>

<span data-ttu-id="32686-128">toounderstand 是否 hello hello 「 系統錯誤 53 」 訊息的原因，您可以使用 Portqry tooquery hello TCP:445 端點。</span><span class="sxs-lookup"><span data-stu-id="32686-128">toounderstand whether this is hello reason behind hello "System error 53" message, you can use Portqry tooquery hello TCP:445 endpoint.</span></span> <span data-ttu-id="32686-129">如果篩選會顯示 hello TCP:445 端點，則會封鎖 hello TCP 連接埠。</span><span class="sxs-lookup"><span data-stu-id="32686-129">If hello TCP:445 endpoint is displayed as filtered, hello TCP port is blocked.</span></span> <span data-ttu-id="32686-130">查詢範例如下：</span><span class="sxs-lookup"><span data-stu-id="32686-130">Here is an example query:</span></span>

  `g:\DataDump\Tools\Portqry>PortQry.exe -n [storage account name].file.core.windows.net -p TCP -e 445`

<span data-ttu-id="32686-131">如果 TCP 通訊埠 445 遭到封鎖 hello 網路路徑的規則，您會看到下列輸出的 hello:</span><span class="sxs-lookup"><span data-stu-id="32686-131">If TCP port 445 is blocked by a rule along hello network path, you will see hello following output:</span></span>

  `TCP port 445 (microsoft-ds service): FILTERED`

<span data-ttu-id="32686-132">如需有關如何 toouse Portqry，請參閱[hello Portqry.exe 命令列公用程式的說明](https://support.microsoft.com/help/310099)。</span><span class="sxs-lookup"><span data-stu-id="32686-132">For more information about how toouse Portqry, see [Description of hello Portqry.exe command-line utility](https://support.microsoft.com/help/310099).</span></span>

### <a name="solution-for-cause-2"></a><span data-ttu-id="32686-133">原因 2 的解決方案</span><span class="sxs-lookup"><span data-stu-id="32686-133">Solution for cause 2</span></span>

<span data-ttu-id="32686-134">使用您的 IT 部門 tooopen 埠 445 輸出太[Azure IP 範圍](https://www.microsoft.com/download/details.aspx?id=41653)。</span><span class="sxs-lookup"><span data-stu-id="32686-134">Work with your IT department tooopen port 445 outbound too[Azure IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

### <a name="cause-3-ntlmv1-is-enabled"></a><span data-ttu-id="32686-135">原因 3：已啟用 NTLMv1</span><span class="sxs-lookup"><span data-stu-id="32686-135">Cause 3: NTLMv1 is enabled</span></span>

<span data-ttu-id="32686-136">如果 hello 用戶端上啟用 NTLMv1 通訊不會發生系統錯誤 53 或系統錯誤 87。</span><span class="sxs-lookup"><span data-stu-id="32686-136">System error 53 or system error 87 can occur if NTLMv1 communication is enabled on hello client.</span></span> <span data-ttu-id="32686-137">Azure 檔案儲存體僅支援 NTLMv2 驗證。</span><span class="sxs-lookup"><span data-stu-id="32686-137">Azure File storage supports only NTLMv2 authentication.</span></span> <span data-ttu-id="32686-138">啟用 NTLMv1 會使用戶端變得較不安全。</span><span class="sxs-lookup"><span data-stu-id="32686-138">Having NTLMv1 enabled creates a less-secure client.</span></span> <span data-ttu-id="32686-139">因此，Azure 檔案儲存體會封鎖通訊。</span><span class="sxs-lookup"><span data-stu-id="32686-139">Therefore, communication is blocked for Azure File storage.</span></span> 

<span data-ttu-id="32686-140">toodetermine 是否這是 hello 錯誤的原因 hello，確認下列登錄子機碼的 hello 設定 tooa 值為 3:</span><span class="sxs-lookup"><span data-stu-id="32686-140">toodetermine whether this is hello cause of hello error, verify that hello following registry subkey is set tooa value of 3:</span></span>

<span data-ttu-id="32686-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**</span><span class="sxs-lookup"><span data-stu-id="32686-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**</span></span>

<span data-ttu-id="32686-142">如需詳細資訊，請參閱 hello [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) TechNet 上的主題。</span><span class="sxs-lookup"><span data-stu-id="32686-142">For more information, see hello [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) topic on TechNet.</span></span>

### <a name="solution-for-cause-3"></a><span data-ttu-id="32686-143">原因 3 的解決方案</span><span class="sxs-lookup"><span data-stu-id="32686-143">Solution for cause 3</span></span>

<span data-ttu-id="32686-144">還原 hello **LmCompatibilityLevel**值 3 的下列登錄子機碼的 hello toohello 預設值：</span><span class="sxs-lookup"><span data-stu-id="32686-144">Revert hello **LmCompatibilityLevel** value toohello default value of 3 in hello following registry subkey:</span></span>

  <span data-ttu-id="32686-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span><span class="sxs-lookup"><span data-stu-id="32686-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span></span>

<a id="error1816"></a>
## <a name="error-1816-not-enough-quota-is-available-tooprocess-this-command-when-you-copy-tooan-azure-file-share"></a><span data-ttu-id="32686-146">錯誤 1816年"沒有足夠的配額是這個命令可用 tooprocess 「 當您複製 tooan Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="32686-146">Error 1816 “Not enough quota is available tooprocess this command” when you copy tooan Azure file share</span></span>

### <a name="cause"></a><span data-ttu-id="32686-147">原因</span><span class="sxs-lookup"><span data-stu-id="32686-147">Cause</span></span>

<span data-ttu-id="32686-148">當您到達 hello 的並行能用於 hello 檔案共用所掛接的 hello 電腦上檔案的開啟控制代碼的時間上限，就會發生錯誤 1816年。</span><span class="sxs-lookup"><span data-stu-id="32686-148">Error 1816 happens when you reach hello upper limit of concurrent open handles that are allowed for a file on hello computer where hello file share is being mounted.</span></span>

### <a name="solution"></a><span data-ttu-id="32686-149">方案</span><span class="sxs-lookup"><span data-stu-id="32686-149">Solution</span></span>

<span data-ttu-id="32686-150">減少 hello 數目同時開啟的控制代碼關閉某些控點，然後再試一次。</span><span class="sxs-lookup"><span data-stu-id="32686-150">Reduce hello number of concurrent open handles by closing some handles, and then retry.</span></span> <span data-ttu-id="32686-151">如需詳細資訊，請參閱 [Microsoft Azure 儲存體效能與延展性檢查清單](storage-performance-checklist.md)。</span><span class="sxs-lookup"><span data-stu-id="32686-151">For more information, see [Microsoft Azure Storage performance and scalability checklist](storage-performance-checklist.md).</span></span>

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-windows"></a><span data-ttu-id="32686-152">複製 tooand 從在 Windows Azure 檔案儲存體的緩慢檔案</span><span class="sxs-lookup"><span data-stu-id="32686-152">Slow file copying tooand from Azure File storage in Windows</span></span>

<span data-ttu-id="32686-153">當您嘗試 tootransfer 檔案 toohello Azure 檔案服務時，您可能會看到效能變慢。</span><span class="sxs-lookup"><span data-stu-id="32686-153">You might see slow performance when you try tootransfer files toohello Azure File service.</span></span>

- <span data-ttu-id="32686-154">如果您沒有特定的最小 I/O 大小需求，我們建議您使用的是 1 MB，如 hello I/O 大小，以獲得最佳效能。</span><span class="sxs-lookup"><span data-stu-id="32686-154">If you don’t have a specific minimum I/O size requirement, we recommend that you use 1 MB as hello I/O size for optimal performance.</span></span>
-   <span data-ttu-id="32686-155">如果您知道 hello 最終大小，您會使用擴充的檔案寫入，且您的軟體沒有相容性問題，當 hello security 的結尾 hello 檔案上包含零，然後設定 hello 檔案大小事先而不是進行每次寫入擴充的寫入。</span><span class="sxs-lookup"><span data-stu-id="32686-155">If you know hello final size of a file that you are extending with writes, and your software doesn’t have compatibility problems when hello unwritten tail on hello file contains zeros, then set hello file size in advance instead of making every write an extending write.</span></span>
-   <span data-ttu-id="32686-156">使用 hello 右複製方法：</span><span class="sxs-lookup"><span data-stu-id="32686-156">Use hello right copy method:</span></span>
    -   <span data-ttu-id="32686-157">針對兩個檔案共用之間的所有傳輸，使用 [AzCopy](storage-use-azcopy.md#file-copy)。</span><span class="sxs-lookup"><span data-stu-id="32686-157">Use [AzCopy](storage-use-azcopy.md#file-copy) for any transfer between two file shares.</span></span>
    -   <span data-ttu-id="32686-158">在內部部署電腦上的檔案共用之間，使用 [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="32686-158">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) between file shares on an on-premises computer.</span></span>

### <a name="considerations-for-windows-81-or-windows-server-2012-r2"></a><span data-ttu-id="32686-159">針對 Windows 8.1 或 Windows Server 2012 R2 的考量</span><span class="sxs-lookup"><span data-stu-id="32686-159">Considerations for Windows 8.1 or Windows Server 2012 R2</span></span>

<span data-ttu-id="32686-160">用戶端執行 Windows 8.1 或 Windows Server 2012 R2，請確定該 hello [KB3114025](https://support.microsoft.com/help/3114025)安裝 hotfix。</span><span class="sxs-lookup"><span data-stu-id="32686-160">For clients that are running Windows 8.1 or Windows Server 2012 R2, make sure that hello [KB3114025](https://support.microsoft.com/help/3114025) hotfix is installed.</span></span> <span data-ttu-id="32686-161">此 hotfix 可改善建立 hello 效能，並關閉控制代碼。</span><span class="sxs-lookup"><span data-stu-id="32686-161">This hotfix improves hello performance of create and close handles.</span></span>

<span data-ttu-id="32686-162">您可以執行下列指令碼 toocheck 是否已安裝 hello hotfix hello:</span><span class="sxs-lookup"><span data-stu-id="32686-162">You can run hello following script toocheck whether hello hotfix has been installed:</span></span>

`reg query HKLM\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies`

<span data-ttu-id="32686-163">如果已安裝 hotfix，hello 會顯示下列輸出：</span><span class="sxs-lookup"><span data-stu-id="32686-163">If hotfix is installed, hello following output is displayed:</span></span>

`HKEY_Local_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies {96c345ef-3cac-477b-8fcd-bea1a564241c} REG_DWORD 0x1`

> [!Note]
> <span data-ttu-id="32686-164">自 2015 年 12 月起，Azure Marketplace 中的 Windows Server 2012 R2 映像預設已安裝 Hotfix KB3114025。</span><span class="sxs-lookup"><span data-stu-id="32686-164">Windows Server 2012 R2 images in Azure Marketplace have hotfix KB3114025 installed by default, starting in December 2015.</span></span>

<a id="shareismissing"></a>
## <a name="no-folder-with-a-drive-letter-in-my-computer"></a><span data-ttu-id="32686-165">[我的電腦] 中沒有任何含磁碟機代號的資料夾</span><span class="sxs-lookup"><span data-stu-id="32686-165">No folder with a drive letter in **My Computer**</span></span>

<span data-ttu-id="32686-166">如果您使用 net 使用對應的 Azure 檔案共用系統管理員身分，hello 共用就會出現 toobe 遺失。</span><span class="sxs-lookup"><span data-stu-id="32686-166">If you map an Azure file share as an administrator by using net use, hello share appears toobe missing.</span></span>

### <a name="cause"></a><span data-ttu-id="32686-167">原因</span><span class="sxs-lookup"><span data-stu-id="32686-167">Cause</span></span>

<span data-ttu-id="32686-168">根據預設，Windows 檔案總管不會以系統管理員身分執行。</span><span class="sxs-lookup"><span data-stu-id="32686-168">By default, Windows File Explorer does not run as an administrator.</span></span> <span data-ttu-id="32686-169">如果您從 系統管理命令提示字元執行 net 使用，您會將 hello 網路磁碟機對應身為系統管理員。</span><span class="sxs-lookup"><span data-stu-id="32686-169">If you run net use from an administrative command prompt, you map hello network drive as an administrator.</span></span> <span data-ttu-id="32686-170">因為對應磁碟機是以使用者為中心，hello 登入的使用者帳戶不會顯示 hello 磁碟機如果它們已掛接於不同的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="32686-170">Because mapped drives are user-centric, hello user account that is logged in does not display hello drives if they are mounted under a different user account.</span></span>

### <a name="solution"></a><span data-ttu-id="32686-171">方案</span><span class="sxs-lookup"><span data-stu-id="32686-171">Solution</span></span>
<span data-ttu-id="32686-172">從非系統管理員命令列掛接 hello 共用。</span><span class="sxs-lookup"><span data-stu-id="32686-172">Mount hello share from a non-administrator command line.</span></span> <span data-ttu-id="32686-173">或者，您可以依照[本 TechNet 主題](https://technet.microsoft.com/library/ee844140.aspx)tooconfigure hello **EnableLinkedConnections**登錄值。</span><span class="sxs-lookup"><span data-stu-id="32686-173">Alternatively, you can follow [this TechNet topic](https://technet.microsoft.com/library/ee844140.aspx) tooconfigure hello **EnableLinkedConnections** registry value.</span></span>

<a id="netuse"></a>
## <a name="net-use-command-fails-if-hello-storage-account-contains-a-forward-slash"></a><span data-ttu-id="32686-174">如果 hello 儲存體帳戶包含正斜線，net use 命令會失敗</span><span class="sxs-lookup"><span data-stu-id="32686-174">Net use command fails if hello storage account contains a forward slash</span></span>

### <a name="cause"></a><span data-ttu-id="32686-175">原因</span><span class="sxs-lookup"><span data-stu-id="32686-175">Cause</span></span>

<span data-ttu-id="32686-176">hello net use 命令會將正斜線 （/） 解譯為命令列選項。</span><span class="sxs-lookup"><span data-stu-id="32686-176">hello net use command interprets a forward slash (/) as a command-line option.</span></span> <span data-ttu-id="32686-177">如果您的使用者帳戶名稱開頭是正斜線，hello 磁碟機對應將會失敗。</span><span class="sxs-lookup"><span data-stu-id="32686-177">If your user account name starts with a forward slash, hello drive mapping fails.</span></span>

### <a name="solution"></a><span data-ttu-id="32686-178">方案</span><span class="sxs-lookup"><span data-stu-id="32686-178">Solution</span></span>

<span data-ttu-id="32686-179">您可以使用其中一個遵循步驟 toowork hello 問題 hello:</span><span class="sxs-lookup"><span data-stu-id="32686-179">You can use either of hello following steps toowork around hello problem:</span></span>

- <span data-ttu-id="32686-180">執行下列 PowerShell 命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="32686-180">Run hello following PowerShell command:</span></span>

  `New-SmbMapping -LocalPath y: -RemotePath \\server\share -UserName accountName -Password "password can contain / and \ etc" `

  <span data-ttu-id="32686-181">批次檔中，您可以執行以此方式 hello 命令：</span><span class="sxs-lookup"><span data-stu-id="32686-181">From a batch file, you can run hello command this way:</span></span>

  `Echo new-smbMapping ... | powershell -command –`

- <span data-ttu-id="32686-182">除非 hello 正斜線 hello 第一個字元，請將雙引號括住 hello 金鑰 toowork 解決這個問題。</span><span class="sxs-lookup"><span data-stu-id="32686-182">Put double quotation marks around hello key toowork around this problem--unless hello forward slash is hello first character.</span></span> <span data-ttu-id="32686-183">如果是，請使用 hello 互動模式，分別輸入您的密碼，或重新產生您的索引鍵 tooget 開頭不是正斜線的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="32686-183">If it is, either use hello interactive mode and enter your password separately or regenerate your keys tooget a key that doesn't start with a forward slash.</span></span>

<a id="cannotaccess"></a>
## <a name="application-or-service-cannot-access-a-mounted-azure-file-storage-drive"></a><span data-ttu-id="32686-184">應用程式或服務無法存取掛接的 Azure 檔案儲存體磁碟機</span><span class="sxs-lookup"><span data-stu-id="32686-184">Application or service cannot access a mounted Azure File storage drive</span></span>

### <a name="cause"></a><span data-ttu-id="32686-185">原因</span><span class="sxs-lookup"><span data-stu-id="32686-185">Cause</span></span>

<span data-ttu-id="32686-186">磁碟機是按每個使用者掛接。</span><span class="sxs-lookup"><span data-stu-id="32686-186">Drives are mounted per user.</span></span> <span data-ttu-id="32686-187">如果在 hello 裝載 hello 磁碟機的其中一個不同的使用者帳戶下執行應用程式或服務，hello 應用程式不會看到 hello 磁碟機。</span><span class="sxs-lookup"><span data-stu-id="32686-187">If your application or service is running under a different user account than hello one that mounted hello drive, hello application will not see hello drive.</span></span>

### <a name="solution"></a><span data-ttu-id="32686-188">方案</span><span class="sxs-lookup"><span data-stu-id="32686-188">Solution</span></span>

<span data-ttu-id="32686-189">使用其中一種 hello 下列方案：</span><span class="sxs-lookup"><span data-stu-id="32686-189">Use one of hello following solutions:</span></span>

-   <span data-ttu-id="32686-190">從 hello 掛接 hello 磁碟機包含 hello 應用程式的相同使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="32686-190">Mount hello drive from hello same user account that contains hello application.</span></span> <span data-ttu-id="32686-191">您可以使用 PsExec 之類的工具。</span><span class="sxs-lookup"><span data-stu-id="32686-191">You can use a tool such as PsExec.</span></span>
- <span data-ttu-id="32686-192">傳入 hello 使用者名稱和密碼參數的 hello net use 命令 hello 儲存體帳戶名稱和金鑰。</span><span class="sxs-lookup"><span data-stu-id="32686-192">Pass hello storage account name and key in hello user name and password parameters of hello net use command.</span></span>

<span data-ttu-id="32686-193">請遵循下列指示之後，您可能會收到 hello 時執行 net hello 系統或網路服務帳戶使用，下列錯誤訊息: 「 發生系統錯誤 1312年。</span><span class="sxs-lookup"><span data-stu-id="32686-193">After you follow these instructions, you might receive hello following error message when you run net use for hello system/network service account: "System error 1312 has occurred.</span></span> <span data-ttu-id="32686-194">指定的登入工作階段不存在。</span><span class="sxs-lookup"><span data-stu-id="32686-194">A specified logon session does not exist.</span></span> <span data-ttu-id="32686-195">可能已被終止。」</span><span class="sxs-lookup"><span data-stu-id="32686-195">It may already have been terminated."</span></span> <span data-ttu-id="32686-196">如果發生這種情況，請確定傳遞 toonet 使用該 hello 使用者名稱包含網域資訊 (例如:"[儲存體帳戶名稱]。 file.core.windows.net")。</span><span class="sxs-lookup"><span data-stu-id="32686-196">If this occurs, make sure that hello username that is passed toonet use includes domain information (for example: "[storage account name].file.core.windows.net").</span></span>

<a id="doesnotsupportencryption"></a>
## <a name="error-you-are-copying-a-file-tooa-destination-that-does-not-support-encryption"></a><span data-ttu-id="32686-197">"您要複製不支援加密的檔案 tooa 目的地 」 的錯誤</span><span class="sxs-lookup"><span data-stu-id="32686-197">Error "You are copying a file tooa destination that does not support encryption"</span></span>

<span data-ttu-id="32686-198">Hello 網路上複製檔案時，hello 時檔案解密 hello 來源電腦上，以純文字傳送，並重新加密 hello 目的地端。</span><span class="sxs-lookup"><span data-stu-id="32686-198">When a file is copied over hello network, hello file is decrypted on hello source computer, transmitted in plaintext, and re-encrypted at hello destination.</span></span> <span data-ttu-id="32686-199">不過，您可能會看到下列錯誤，當您考慮 toocopy 加密檔案的 hello: 「 您所複製不支援加密的 hello 檔案 tooa 目的地 」。</span><span class="sxs-lookup"><span data-stu-id="32686-199">However, you might see hello following error when you're trying toocopy an encrypted file: "You are copying hello file tooa destination that does not support encryption."</span></span>

### <a name="cause"></a><span data-ttu-id="32686-200">原因</span><span class="sxs-lookup"><span data-stu-id="32686-200">Cause</span></span>
<span data-ttu-id="32686-201">如果您使用加密檔案系統 (EFS)，可能會發生此問題。</span><span class="sxs-lookup"><span data-stu-id="32686-201">This problem can occur if you are using Encrypting File System (EFS).</span></span> <span data-ttu-id="32686-202">BitLocker 加密的檔案可以複製的 tooAzure 檔案存放裝置。</span><span class="sxs-lookup"><span data-stu-id="32686-202">BitLocker-encrypted files can be copied tooAzure File storage.</span></span> <span data-ttu-id="32686-203">不過，Azure 檔案儲存體不支援 NTFS EFS。</span><span class="sxs-lookup"><span data-stu-id="32686-203">However, Azure File storage does not support NTFS EFS.</span></span>

### <a name="workaround"></a><span data-ttu-id="32686-204">因應措施</span><span class="sxs-lookup"><span data-stu-id="32686-204">Workaround</span></span>
<span data-ttu-id="32686-205">toocopy hello 網路上的檔案，您必須先將其解密。</span><span class="sxs-lookup"><span data-stu-id="32686-205">toocopy a file over hello network, you must first decrypt it.</span></span> <span data-ttu-id="32686-206">使用其中一種 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="32686-206">Use one of hello following methods:</span></span>

- <span data-ttu-id="32686-207">使用 hello**複製 /d**命令。</span><span class="sxs-lookup"><span data-stu-id="32686-207">Use hello **copy /d** command.</span></span> <span data-ttu-id="32686-208">它可讓加密的 hello toobe 儲存為 hello 目的地端的解密檔案的檔案。</span><span class="sxs-lookup"><span data-stu-id="32686-208">It allows hello encrypted files toobe saved as decrypted files at hello destination.</span></span>
- <span data-ttu-id="32686-209">設定下列登錄機碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="32686-209">Set hello following registry key:</span></span>
  - <span data-ttu-id="32686-210">路徑 = HKLM\Software\Policies\Microsoft\Windows\System</span><span class="sxs-lookup"><span data-stu-id="32686-210">Path = HKLM\Software\Policies\Microsoft\Windows\System</span></span>
  - <span data-ttu-id="32686-211">數值類型 = DWORD</span><span class="sxs-lookup"><span data-stu-id="32686-211">Value type = DWORD</span></span>
  - <span data-ttu-id="32686-212">Name = CopyFileAllowDecryptedRemoteDestination</span><span class="sxs-lookup"><span data-stu-id="32686-212">Name = CopyFileAllowDecryptedRemoteDestination</span></span>
  - <span data-ttu-id="32686-213">Value = 1</span><span class="sxs-lookup"><span data-stu-id="32686-213">Value = 1</span></span>

<span data-ttu-id="32686-214">請注意該設定 hello 登錄機碼會影響所有的複製作業所 toonetwork 共用。</span><span class="sxs-lookup"><span data-stu-id="32686-214">Be aware that setting hello registry key affects all copy operations that are made toonetwork shares.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="32686-215">需要協助嗎？</span><span class="sxs-lookup"><span data-stu-id="32686-215">Need help?</span></span> <span data-ttu-id="32686-216">請連絡支援人員。</span><span class="sxs-lookup"><span data-stu-id="32686-216">Contact support.</span></span>
<span data-ttu-id="32686-217">如果您仍需要協助，[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)tooget 快速解決問題。</span><span class="sxs-lookup"><span data-stu-id="32686-217">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your problem resolved quickly.</span></span>
