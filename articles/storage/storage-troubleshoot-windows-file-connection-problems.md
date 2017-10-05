---
title: "針對 Windows 中的 Azure 檔案儲存體問題進行疑難排解 | Microsoft Docs"
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
ms.openlocfilehash: 71a8f4edf7776556b383f446e5aad007748ef090
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-windows"></a><span data-ttu-id="bac56-103">針對 Windows 中的 Azure 檔案儲存體問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="bac56-103">Troubleshoot Azure File storage problems in Windows</span></span>

<span data-ttu-id="bac56-104">本文列出當您從 Windows 用戶端連線時，與 Microsoft Azure 檔案儲存體相關的常見問題。</span><span class="sxs-lookup"><span data-stu-id="bac56-104">This article lists common problems that are related to Microsoft Azure File storage when you connect from Windows clients.</span></span> <span data-ttu-id="bac56-105">文中也會提供這些問題的可能原因和解決方案。</span><span class="sxs-lookup"><span data-stu-id="bac56-105">It also provides possible causes and resolutions for these problems.</span></span> <span data-ttu-id="bac56-106">除了本文中的疑難排解步驟，您也可以使用 [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) \(英文\) 來確保 Windows 用戶端環境具備正確的必要條件。</span><span class="sxs-lookup"><span data-stu-id="bac56-106">In addition to the troubleshooting steps in this article, you can also use [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) to ensure that the Windows client environment has correct prerequisites.</span></span> <span data-ttu-id="bac56-107">AzFileDiagnostics 會自動偵測本文中提及的大部分徵兆，並協助設定您的環境以取得最佳效能。</span><span class="sxs-lookup"><span data-stu-id="bac56-107">AzFileDiagnostics automates detection of most of the symptoms mentioned in this article and helps set up your environment to get optimal performance.</span></span> <span data-ttu-id="bac56-108">您也可以在 [Azure 檔案共用疑難排解員](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares)中找到此資訊，其提供步驟以協助您解決連線/對應/掛接 Azure 檔案共用的問題。</span><span class="sxs-lookup"><span data-stu-id="bac56-108">You can also find this information in the [Azure Files shares Troubleshooter](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) that provides steps to assist you with problems connecting/mapping/mounting Azure Files shares.</span></span>


<a id="error53-67-87"></a>
## <a name="error-53-error-67-or-error-87-when-you-mount-or-unmount-an-azure-file-share"></a><span data-ttu-id="bac56-109">當您嘗試掛接或取消掛接 Azure 檔案共用時發生錯誤 53、錯誤 67 或錯誤 87</span><span class="sxs-lookup"><span data-stu-id="bac56-109">Error 53, Error 67, or Error 87 when you mount or unmount an Azure file share</span></span>

<span data-ttu-id="bac56-110">當您嘗試從內部部署或不同資料中心掛接檔案共用時，可能會收到下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="bac56-110">When you try to mount a file share from on-premises or from a different datacenter, you might receive the following errors:</span></span>

- <span data-ttu-id="bac56-111">發生系統錯誤 53。</span><span class="sxs-lookup"><span data-stu-id="bac56-111">System error 53 has occurred.</span></span> <span data-ttu-id="bac56-112">找不到網路路徑。</span><span class="sxs-lookup"><span data-stu-id="bac56-112">The network path was not found.</span></span>
- <span data-ttu-id="bac56-113">發生系統錯誤 67。</span><span class="sxs-lookup"><span data-stu-id="bac56-113">System error 67 has occurred.</span></span> <span data-ttu-id="bac56-114">找不到網路名稱。</span><span class="sxs-lookup"><span data-stu-id="bac56-114">The network name cannot be found.</span></span>
- <span data-ttu-id="bac56-115">發生系統錯誤 87。</span><span class="sxs-lookup"><span data-stu-id="bac56-115">System error 87 has occurred.</span></span> <span data-ttu-id="bac56-116">參數錯誤。</span><span class="sxs-lookup"><span data-stu-id="bac56-116">The parameter is incorrect.</span></span>

### <a name="cause-1-unencrypted-communication-channel"></a><span data-ttu-id="bac56-117">原因 1：通訊通道未加密</span><span class="sxs-lookup"><span data-stu-id="bac56-117">Cause 1: Unencrypted communication channel</span></span>

<span data-ttu-id="bac56-118">基於安全考量，如果通訊通道未加密，而且未從 Azure 檔案共用所在的相同資料中心進行連線嘗試，與 Azure 檔案共用的連線就會遭到封鎖。</span><span class="sxs-lookup"><span data-stu-id="bac56-118">For security reasons, connections to Azure file shares are blocked if the communication channel isn’t encrypted and if the connection attempt isn't made from the same datacenter where the Azure file shares reside.</span></span> <span data-ttu-id="bac56-119">唯有當使用者的用戶端作業系統支援 SMB 加密，才會提供通訊通道加密。</span><span class="sxs-lookup"><span data-stu-id="bac56-119">Communication channel encryption is provided only if the user’s client OS supports SMB encryption.</span></span>

<span data-ttu-id="bac56-120">Windows 8、Windows Server 2012 和更新版本的每個系統交涉都要求包含支援加密的 SMB 3.0。</span><span class="sxs-lookup"><span data-stu-id="bac56-120">Windows 8, Windows Server 2012, and later versions of each system negotiate requests that include SMB 3.0, which supports encryption.</span></span>

### <a name="solution-for-cause-1"></a><span data-ttu-id="bac56-121">原因 1 的解決方案</span><span class="sxs-lookup"><span data-stu-id="bac56-121">Solution for cause 1</span></span>

<span data-ttu-id="bac56-122">從執行下列其中一項的用戶端連線：</span><span class="sxs-lookup"><span data-stu-id="bac56-122">Connect from a client that does one of the following:</span></span>

- <span data-ttu-id="bac56-123">符合 Windows 8 和 Windows Server 2012 或更新版本的需求</span><span class="sxs-lookup"><span data-stu-id="bac56-123">Meets the requirements of Windows 8 and Windows Server 2012 or later versions</span></span>
- <span data-ttu-id="bac56-124">從與用於 Azure 檔案共用的 Azure 儲存體帳戶相同之資料中心的虛擬機器連線</span><span class="sxs-lookup"><span data-stu-id="bac56-124">Connects from a virtual machine in the same datacenter as the Azure storage account that is used for the Azure file share</span></span>

### <a name="cause-2-port-445-is-blocked"></a><span data-ttu-id="bac56-125">原因 2：連接埠 445 遭到封鎖</span><span class="sxs-lookup"><span data-stu-id="bac56-125">Cause 2: Port 445 is blocked</span></span>

<span data-ttu-id="bac56-126">如果連接埠 445 至 Azure 檔案儲存體資料中心的輸出通訊遭到封鎖，可能會發生系統錯誤 53 或系統錯誤 67。</span><span class="sxs-lookup"><span data-stu-id="bac56-126">System error 53 or system error 67 can occur if port 445 outbound communication to an Azure File storage datacenter is blocked.</span></span> <span data-ttu-id="bac56-127">若要查看 ISP 是否允許從連接埠 445 進行存取的摘要，請參閱 [TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="bac56-127">To see the summary of ISPs that allow or disallow access from port 445, go to [TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).</span></span>

<span data-ttu-id="bac56-128">若要了解這是否為「系統錯誤 53」訊息的原因，您可以使用 Portqry 查詢 TCP:445 端點。</span><span class="sxs-lookup"><span data-stu-id="bac56-128">To understand whether this is the reason behind the "System error 53" message, you can use Portqry to query the TCP:445 endpoint.</span></span> <span data-ttu-id="bac56-129">如果篩選顯示 TCP:445 端點，則 TCP 連接埠會被封鎖。</span><span class="sxs-lookup"><span data-stu-id="bac56-129">If the TCP:445 endpoint is displayed as filtered, the TCP port is blocked.</span></span> <span data-ttu-id="bac56-130">查詢範例如下：</span><span class="sxs-lookup"><span data-stu-id="bac56-130">Here is an example query:</span></span>

  `g:\DataDump\Tools\Portqry>PortQry.exe -n [storage account name].file.core.windows.net -p TCP -e 445`

<span data-ttu-id="bac56-131">如果 TCP 連接埠 445 被網路路徑規則所封鎖，您將看到下列輸出：</span><span class="sxs-lookup"><span data-stu-id="bac56-131">If TCP port 445 is blocked by a rule along the network path, you will see the following output:</span></span>

  `TCP port 445 (microsoft-ds service): FILTERED`

<span data-ttu-id="bac56-132">如需如何使用 Portqry 的詳細資訊，請參閱 [Portqry.exe 命令列公用程式說明](https://support.microsoft.com/help/310099)。</span><span class="sxs-lookup"><span data-stu-id="bac56-132">For more information about how to use Portqry, see [Description of the Portqry.exe command-line utility](https://support.microsoft.com/help/310099).</span></span>

### <a name="solution-for-cause-2"></a><span data-ttu-id="bac56-133">原因 2 的解決方案</span><span class="sxs-lookup"><span data-stu-id="bac56-133">Solution for cause 2</span></span>

<span data-ttu-id="bac56-134">聯絡您的 IT 部門，要求開啟連接埠 445 輸出到 [Azure IP 範圍](https://www.microsoft.com/download/details.aspx?id=41653) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="bac56-134">Work with your IT department to open port 445 outbound to [Azure IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

### <a name="cause-3-ntlmv1-is-enabled"></a><span data-ttu-id="bac56-135">原因 3：已啟用 NTLMv1</span><span class="sxs-lookup"><span data-stu-id="bac56-135">Cause 3: NTLMv1 is enabled</span></span>

<span data-ttu-id="bac56-136">如果用戶端上已啟用 NTLMv1 通訊，就會發生系統錯誤 53 或系統錯誤 87。</span><span class="sxs-lookup"><span data-stu-id="bac56-136">System error 53 or system error 87 can occur if NTLMv1 communication is enabled on the client.</span></span> <span data-ttu-id="bac56-137">Azure 檔案儲存體僅支援 NTLMv2 驗證。</span><span class="sxs-lookup"><span data-stu-id="bac56-137">Azure File storage supports only NTLMv2 authentication.</span></span> <span data-ttu-id="bac56-138">啟用 NTLMv1 會使用戶端變得較不安全。</span><span class="sxs-lookup"><span data-stu-id="bac56-138">Having NTLMv1 enabled creates a less-secure client.</span></span> <span data-ttu-id="bac56-139">因此，Azure 檔案儲存體會封鎖通訊。</span><span class="sxs-lookup"><span data-stu-id="bac56-139">Therefore, communication is blocked for Azure File storage.</span></span> 

<span data-ttu-id="bac56-140">若要判斷這是否為錯誤的原因，請確認已將下列登錄子機碼的值設為 3：</span><span class="sxs-lookup"><span data-stu-id="bac56-140">To determine whether this is the cause of the error, verify that the following registry subkey is set to a value of 3:</span></span>

<span data-ttu-id="bac56-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**</span><span class="sxs-lookup"><span data-stu-id="bac56-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**</span></span>

<span data-ttu-id="bac56-142">如需詳細資訊，請參閱 TechNet 上的 [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) 主題。</span><span class="sxs-lookup"><span data-stu-id="bac56-142">For more information, see the [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) topic on TechNet.</span></span>

### <a name="solution-for-cause-3"></a><span data-ttu-id="bac56-143">原因 3 的解決方案</span><span class="sxs-lookup"><span data-stu-id="bac56-143">Solution for cause 3</span></span>

<span data-ttu-id="bac56-144">在下列登錄子機碼中，將 **LmCompatibilityLevel** 值還原為預設值 3：</span><span class="sxs-lookup"><span data-stu-id="bac56-144">Revert the **LmCompatibilityLevel** value to the default value of 3 in the following registry subkey:</span></span>

  <span data-ttu-id="bac56-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span><span class="sxs-lookup"><span data-stu-id="bac56-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span></span>

<a id="error1816"></a>
## <a name="error-1816-not-enough-quota-is-available-to-process-this-command-when-you-copy-to-an-azure-file-share"></a><span data-ttu-id="bac56-146">當您複製到 Azure 檔案共用時發生錯誤 1816「配額不足無法處理此命令」</span><span class="sxs-lookup"><span data-stu-id="bac56-146">Error 1816 “Not enough quota is available to process this command” when you copy to an Azure file share</span></span>

### <a name="cause"></a><span data-ttu-id="bac56-147">原因</span><span class="sxs-lookup"><span data-stu-id="bac56-147">Cause</span></span>

<span data-ttu-id="bac56-148">當您到達同時開啟的控制代碼上限時 (此為針對掛接檔案共用之電腦上的檔案所允許的上限)，即會發生錯誤 1816。</span><span class="sxs-lookup"><span data-stu-id="bac56-148">Error 1816 happens when you reach the upper limit of concurrent open handles that are allowed for a file on the computer where the file share is being mounted.</span></span>

### <a name="solution"></a><span data-ttu-id="bac56-149">方案</span><span class="sxs-lookup"><span data-stu-id="bac56-149">Solution</span></span>

<span data-ttu-id="bac56-150">關閉一些控制代碼以減少同時開啟的控制代碼數，然後再試一次。</span><span class="sxs-lookup"><span data-stu-id="bac56-150">Reduce the number of concurrent open handles by closing some handles, and then retry.</span></span> <span data-ttu-id="bac56-151">如需詳細資訊，請參閱 [Microsoft Azure 儲存體效能與延展性檢查清單](storage-performance-checklist.md)。</span><span class="sxs-lookup"><span data-stu-id="bac56-151">For more information, see [Microsoft Azure Storage performance and scalability checklist](storage-performance-checklist.md).</span></span>

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-to-and-from-azure-file-storage-in-windows"></a><span data-ttu-id="bac56-152">從 Windows 中的 Azure 檔案儲存體複製檔案或將檔案複製到其中的速度變慢</span><span class="sxs-lookup"><span data-stu-id="bac56-152">Slow file copying to and from Azure File storage in Windows</span></span>

<span data-ttu-id="bac56-153">當您嘗試將檔案傳輸到 Azure 檔案服務時，可能會看到效能變慢。</span><span class="sxs-lookup"><span data-stu-id="bac56-153">You might see slow performance when you try to transfer files to the Azure File service.</span></span>

- <span data-ttu-id="bac56-154">如果您沒有特定的 I/O 大小需求下限，建議您使用 1 MB 的 I/O 大小以獲得最佳效能。</span><span class="sxs-lookup"><span data-stu-id="bac56-154">If you don’t have a specific minimum I/O size requirement, we recommend that you use 1 MB as the I/O size for optimal performance.</span></span>
-   <span data-ttu-id="bac56-155">如果您知道擴充寫入檔案的最終大小，而且當檔案上未寫入的結尾中有零時您的軟體不會產生相容性問題，則請事先設定檔案大小，而不是將每次寫入設為擴充寫入。</span><span class="sxs-lookup"><span data-stu-id="bac56-155">If you know the final size of a file that you are extending with writes, and your software doesn’t have compatibility problems when the unwritten tail on the file contains zeros, then set the file size in advance instead of making every write an extending write.</span></span>
-   <span data-ttu-id="bac56-156">使用正確的複製方法：</span><span class="sxs-lookup"><span data-stu-id="bac56-156">Use the right copy method:</span></span>
    -   <span data-ttu-id="bac56-157">針對兩個檔案共用之間的所有傳輸，使用 [AzCopy](storage-use-azcopy.md#file-copy)。</span><span class="sxs-lookup"><span data-stu-id="bac56-157">Use [AzCopy](storage-use-azcopy.md#file-copy) for any transfer between two file shares.</span></span>
    -   <span data-ttu-id="bac56-158">在內部部署電腦上的檔案共用之間，使用 [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="bac56-158">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) between file shares on an on-premises computer.</span></span>

### <a name="considerations-for-windows-81-or-windows-server-2012-r2"></a><span data-ttu-id="bac56-159">針對 Windows 8.1 或 Windows Server 2012 R2 的考量</span><span class="sxs-lookup"><span data-stu-id="bac56-159">Considerations for Windows 8.1 or Windows Server 2012 R2</span></span>

<span data-ttu-id="bac56-160">若用戶端執行 Windows 8.1 或 Windows Server 2012 R2，請確定已安裝 [KB3114025](https://support.microsoft.com/help/3114025) Hotfix。</span><span class="sxs-lookup"><span data-stu-id="bac56-160">For clients that are running Windows 8.1 or Windows Server 2012 R2, make sure that the [KB3114025](https://support.microsoft.com/help/3114025) hotfix is installed.</span></span> <span data-ttu-id="bac56-161">此 Hotfix 可改善建立和關閉控制代碼的效能。</span><span class="sxs-lookup"><span data-stu-id="bac56-161">This hotfix improves the performance of create and close handles.</span></span>

<span data-ttu-id="bac56-162">您可以執行下列指令碼來檢查是否已安裝此 Hotfix：</span><span class="sxs-lookup"><span data-stu-id="bac56-162">You can run the following script to check whether the hotfix has been installed:</span></span>

`reg query HKLM\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies`

<span data-ttu-id="bac56-163">如果已安裝 hotfix，則會顯示下列輸出︰</span><span class="sxs-lookup"><span data-stu-id="bac56-163">If hotfix is installed, the following output is displayed:</span></span>

`HKEY_Local_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies {96c345ef-3cac-477b-8fcd-bea1a564241c} REG_DWORD 0x1`

> [!Note]
> <span data-ttu-id="bac56-164">自 2015 年 12 月起，Azure Marketplace 中的 Windows Server 2012 R2 映像預設已安裝 Hotfix KB3114025。</span><span class="sxs-lookup"><span data-stu-id="bac56-164">Windows Server 2012 R2 images in Azure Marketplace have hotfix KB3114025 installed by default, starting in December 2015.</span></span>

<a id="shareismissing"></a>
## <a name="no-folder-with-a-drive-letter-in-my-computer"></a><span data-ttu-id="bac56-165">[我的電腦] 中沒有任何含磁碟機代號的資料夾</span><span class="sxs-lookup"><span data-stu-id="bac56-165">No folder with a drive letter in **My Computer**</span></span>

<span data-ttu-id="bac56-166">如果您以系統管理員身分使用 net use 對應 Azure 檔案共用，該共用似乎就會遺失。</span><span class="sxs-lookup"><span data-stu-id="bac56-166">If you map an Azure file share as an administrator by using net use, the share appears to be missing.</span></span>

### <a name="cause"></a><span data-ttu-id="bac56-167">原因</span><span class="sxs-lookup"><span data-stu-id="bac56-167">Cause</span></span>

<span data-ttu-id="bac56-168">根據預設，Windows 檔案總管不會以系統管理員身分執行。</span><span class="sxs-lookup"><span data-stu-id="bac56-168">By default, Windows File Explorer does not run as an administrator.</span></span> <span data-ttu-id="bac56-169">如果您從系統管理命令提示字元執行 net use，就是以系統管理員身分對應網路磁碟機。</span><span class="sxs-lookup"><span data-stu-id="bac56-169">If you run net use from an administrative command prompt, you map the network drive as an administrator.</span></span> <span data-ttu-id="bac56-170">因為對應的磁碟機是以使用者為中心，如果磁碟機掛接在不同的使用者帳戶下，登入的使用者帳戶不會顯示此磁碟機。</span><span class="sxs-lookup"><span data-stu-id="bac56-170">Because mapped drives are user-centric, the user account that is logged in does not display the drives if they are mounted under a different user account.</span></span>

### <a name="solution"></a><span data-ttu-id="bac56-171">方案</span><span class="sxs-lookup"><span data-stu-id="bac56-171">Solution</span></span>
<span data-ttu-id="bac56-172">從非系統管理員命令掛接共用。</span><span class="sxs-lookup"><span data-stu-id="bac56-172">Mount the share from a non-administrator command line.</span></span> <span data-ttu-id="bac56-173">或者，您可以依照[此 TechNet 主題](https://technet.microsoft.com/library/ee844140.aspx)設定 **EnableLinkedConnections** 登錄值。</span><span class="sxs-lookup"><span data-stu-id="bac56-173">Alternatively, you can follow [this TechNet topic](https://technet.microsoft.com/library/ee844140.aspx) to configure the **EnableLinkedConnections** registry value.</span></span>

<a id="netuse"></a>
## <a name="net-use-command-fails-if-the-storage-account-contains-a-forward-slash"></a><span data-ttu-id="bac56-174">如果儲存體帳戶包含斜線，net use 命令就會失敗</span><span class="sxs-lookup"><span data-stu-id="bac56-174">Net use command fails if the storage account contains a forward slash</span></span>

### <a name="cause"></a><span data-ttu-id="bac56-175">原因</span><span class="sxs-lookup"><span data-stu-id="bac56-175">Cause</span></span>

<span data-ttu-id="bac56-176">Net use 命令會將斜線 (/) 解譯為命令列選項。</span><span class="sxs-lookup"><span data-stu-id="bac56-176">The net use command interprets a forward slash (/) as a command-line option.</span></span> <span data-ttu-id="bac56-177">如果您的使用者帳戶名稱開頭為斜線，磁碟機對應將會失敗。</span><span class="sxs-lookup"><span data-stu-id="bac56-177">If your user account name starts with a forward slash, the drive mapping fails.</span></span>

### <a name="solution"></a><span data-ttu-id="bac56-178">方案</span><span class="sxs-lookup"><span data-stu-id="bac56-178">Solution</span></span>

<span data-ttu-id="bac56-179">您可以使用下列其中一種方式來解決這個問題：</span><span class="sxs-lookup"><span data-stu-id="bac56-179">You can use either of the following steps to work around the problem:</span></span>

- <span data-ttu-id="bac56-180">執行下列 PowerShell 命令：</span><span class="sxs-lookup"><span data-stu-id="bac56-180">Run the following PowerShell command:</span></span>

  `New-SmbMapping -LocalPath y: -RemotePath \\server\share -UserName accountName -Password "password can contain / and \ etc" `

  <span data-ttu-id="bac56-181">從批次檔中，您可以使用此方式執行命令：</span><span class="sxs-lookup"><span data-stu-id="bac56-181">From a batch file, you can run the command this way:</span></span>

  `Echo new-smbMapping ... | powershell -command –`

- <span data-ttu-id="bac56-182">除非斜線是第一個字元，否則，可以用雙引號括住金鑰來解決此問題。</span><span class="sxs-lookup"><span data-stu-id="bac56-182">Put double quotation marks around the key to work around this problem--unless the forward slash is the first character.</span></span> <span data-ttu-id="bac56-183">如果是，可使用互動模式分開輸入您的密碼，或者，重新產生金鑰，以取得不是斜線開頭的金鑰。</span><span class="sxs-lookup"><span data-stu-id="bac56-183">If it is, either use the interactive mode and enter your password separately or regenerate your keys to get a key that doesn't start with a forward slash.</span></span>

<a id="cannotaccess"></a>
## <a name="application-or-service-cannot-access-a-mounted-azure-file-storage-drive"></a><span data-ttu-id="bac56-184">應用程式或服務無法存取掛接的 Azure 檔案儲存體磁碟機</span><span class="sxs-lookup"><span data-stu-id="bac56-184">Application or service cannot access a mounted Azure File storage drive</span></span>

### <a name="cause"></a><span data-ttu-id="bac56-185">原因</span><span class="sxs-lookup"><span data-stu-id="bac56-185">Cause</span></span>

<span data-ttu-id="bac56-186">磁碟機是按每個使用者掛接。</span><span class="sxs-lookup"><span data-stu-id="bac56-186">Drives are mounted per user.</span></span> <span data-ttu-id="bac56-187">如果您的應用程式或服務正在與掛接磁碟機之帳戶不同的使用者帳戶下執行，應用程式將不會看到該磁碟機。</span><span class="sxs-lookup"><span data-stu-id="bac56-187">If your application or service is running under a different user account than the one that mounted the drive, the application will not see the drive.</span></span>

### <a name="solution"></a><span data-ttu-id="bac56-188">方案</span><span class="sxs-lookup"><span data-stu-id="bac56-188">Solution</span></span>

<span data-ttu-id="bac56-189">使用下列其中一個解決方案：</span><span class="sxs-lookup"><span data-stu-id="bac56-189">Use one of the following solutions:</span></span>

-   <span data-ttu-id="bac56-190">從應用程式所屬的相同使用者帳戶掛接磁碟機。</span><span class="sxs-lookup"><span data-stu-id="bac56-190">Mount the drive from the same user account that contains the application.</span></span> <span data-ttu-id="bac56-191">您可以使用 PsExec 之類的工具。</span><span class="sxs-lookup"><span data-stu-id="bac56-191">You can use a tool such as PsExec.</span></span>
- <span data-ttu-id="bac56-192">在 net use 命令的使用者名稱和密碼參數中傳遞儲存體帳戶名稱和金鑰。</span><span class="sxs-lookup"><span data-stu-id="bac56-192">Pass the storage account name and key in the user name and password parameters of the net use command.</span></span>

<span data-ttu-id="bac56-193">遵循這些指示執行之後，當您針對系統/網路服務帳戶執行 net use 時，可能會收到下列錯誤訊息：「發生系統錯誤 1312。</span><span class="sxs-lookup"><span data-stu-id="bac56-193">After you follow these instructions, you might receive the following error message when you run net use for the system/network service account: "System error 1312 has occurred.</span></span> <span data-ttu-id="bac56-194">指定的登入工作階段不存在。</span><span class="sxs-lookup"><span data-stu-id="bac56-194">A specified logon session does not exist.</span></span> <span data-ttu-id="bac56-195">可能已被終止。」</span><span class="sxs-lookup"><span data-stu-id="bac56-195">It may already have been terminated."</span></span> <span data-ttu-id="bac56-196">如果發生這種情況，請確定傳遞至 net use 的使用者名稱包含網域資訊 (例如，"[storage account name].file.core.windows.net")。</span><span class="sxs-lookup"><span data-stu-id="bac56-196">If this occurs, make sure that the username that is passed to net use includes domain information (for example: "[storage account name].file.core.windows.net").</span></span>

<a id="doesnotsupportencryption"></a>
## <a name="error-you-are-copying-a-file-to-a-destination-that-does-not-support-encryption"></a><span data-ttu-id="bac56-197">「您正將檔案複製到不支援加密的目的地」錯誤</span><span class="sxs-lookup"><span data-stu-id="bac56-197">Error "You are copying a file to a destination that does not support encryption"</span></span>

<span data-ttu-id="bac56-198">透過網路複製檔案時，該檔案會在來源電腦上解密、以純文字傳送，並在目的地上重新加密。</span><span class="sxs-lookup"><span data-stu-id="bac56-198">When a file is copied over the network, the file is decrypted on the source computer, transmitted in plaintext, and re-encrypted at the destination.</span></span> <span data-ttu-id="bac56-199">不過，您可能會在嘗試複製加密的檔案時看到下列錯誤：「您正在將檔案複製到不支援加密的目的地。」</span><span class="sxs-lookup"><span data-stu-id="bac56-199">However, you might see the following error when you're trying to copy an encrypted file: "You are copying the file to a destination that does not support encryption."</span></span>

### <a name="cause"></a><span data-ttu-id="bac56-200">原因</span><span class="sxs-lookup"><span data-stu-id="bac56-200">Cause</span></span>
<span data-ttu-id="bac56-201">如果您使用加密檔案系統 (EFS)，可能會發生此問題。</span><span class="sxs-lookup"><span data-stu-id="bac56-201">This problem can occur if you are using Encrypting File System (EFS).</span></span> <span data-ttu-id="bac56-202">BitLocker 加密的檔案可以複製到 Azure 檔案儲存體。</span><span class="sxs-lookup"><span data-stu-id="bac56-202">BitLocker-encrypted files can be copied to Azure File storage.</span></span> <span data-ttu-id="bac56-203">不過，Azure 檔案儲存體不支援 NTFS EFS。</span><span class="sxs-lookup"><span data-stu-id="bac56-203">However, Azure File storage does not support NTFS EFS.</span></span>

### <a name="workaround"></a><span data-ttu-id="bac56-204">因應措施</span><span class="sxs-lookup"><span data-stu-id="bac56-204">Workaround</span></span>
<span data-ttu-id="bac56-205">若要透過網路複製檔案，您必須先將它解密。</span><span class="sxs-lookup"><span data-stu-id="bac56-205">To copy a file over the network, you must first decrypt it.</span></span> <span data-ttu-id="bac56-206">使用下列其中一種方法：</span><span class="sxs-lookup"><span data-stu-id="bac56-206">Use one of the following methods:</span></span>

- <span data-ttu-id="bac56-207">使用 **copy /d** 命令。</span><span class="sxs-lookup"><span data-stu-id="bac56-207">Use the **copy /d** command.</span></span> <span data-ttu-id="bac56-208">它可讓加密的檔案另存為目的地上的解密檔案。</span><span class="sxs-lookup"><span data-stu-id="bac56-208">It allows the encrypted files to be saved as decrypted files at the destination.</span></span>
- <span data-ttu-id="bac56-209">設定下列登錄機碼：</span><span class="sxs-lookup"><span data-stu-id="bac56-209">Set the following registry key:</span></span>
  - <span data-ttu-id="bac56-210">路徑 = HKLM\Software\Policies\Microsoft\Windows\System</span><span class="sxs-lookup"><span data-stu-id="bac56-210">Path = HKLM\Software\Policies\Microsoft\Windows\System</span></span>
  - <span data-ttu-id="bac56-211">數值類型 = DWORD</span><span class="sxs-lookup"><span data-stu-id="bac56-211">Value type = DWORD</span></span>
  - <span data-ttu-id="bac56-212">Name = CopyFileAllowDecryptedRemoteDestination</span><span class="sxs-lookup"><span data-stu-id="bac56-212">Name = CopyFileAllowDecryptedRemoteDestination</span></span>
  - <span data-ttu-id="bac56-213">Value = 1</span><span class="sxs-lookup"><span data-stu-id="bac56-213">Value = 1</span></span>

<span data-ttu-id="bac56-214">請注意，設定登錄機碼會影響所有對網路共用所做的複製作業。</span><span class="sxs-lookup"><span data-stu-id="bac56-214">Be aware that setting the registry key affects all copy operations that are made to network shares.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="bac56-215">需要協助嗎？</span><span class="sxs-lookup"><span data-stu-id="bac56-215">Need help?</span></span> <span data-ttu-id="bac56-216">請連絡支援人員。</span><span class="sxs-lookup"><span data-stu-id="bac56-216">Contact support.</span></span>
<span data-ttu-id="bac56-217">如果仍需要協助，請[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)以快速解決您的問題。</span><span class="sxs-lookup"><span data-stu-id="bac56-217">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your problem resolved quickly.</span></span>
