---
title: "在 Azure 中的 aaaTroubleshoot Windows 虛擬機器啟用問題 |Microsoft 文件"
description: "提供 hello 疑難排解在 Azure 中修正 Windows 虛擬機器啟用問題的步驟"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 4ebdac66166e80dcd68cd9e2931b30a29ac01eef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-windows-virtual-machine-activation-problems"></a><span data-ttu-id="8cbb0-103">針對 Azure Windows 虛擬機器啟用問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="8cbb0-103">Troubleshoot Azure Windows virtual machine activation problems</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="8cbb0-104">如果您無法啟用 Azure Windows 虛擬機器 (VM)，建立從自訂映像時，您可以使用此文件 tootroubleshoot hello 問題中提供的 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="8cbb0-104">If you have trouble when activating Azure Windows virtual machine (VM) that is created from a custom image, you can use hello information provided in this document tootroubleshoot hello issue.</span></span> 

## <a name="symptom"></a><span data-ttu-id="8cbb0-105">徵狀</span><span class="sxs-lookup"><span data-stu-id="8cbb0-105">Symptom</span></span>

<span data-ttu-id="8cbb0-106">當您嘗試 tooactivate Azure Windows VM 時，您會收到錯誤訊息類似下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="8cbb0-106">When you try tooactivate an Azure Windows VM, you receive an error message resembles hello following sample:</span></span>

<span data-ttu-id="8cbb0-107">**錯誤： 無法啟動該 hello 電腦回報 0xC004F074 hello 軟體 LicensingService。無法聯繫金鑰管理服務 (KMS)。請 hello 應用程式事件記錄檔，如需詳細資訊，參閱。**</span><span class="sxs-lookup"><span data-stu-id="8cbb0-107">**Error: 0xC004F074 hello Software LicensingService reported that hello computer could not be activated. No Key ManagementService (KMS) could be contacted. Please see hello Application Event Log for additional information.**</span></span>

## <a name="cause"></a><span data-ttu-id="8cbb0-108">原因</span><span class="sxs-lookup"><span data-stu-id="8cbb0-108">Cause</span></span>
<span data-ttu-id="8cbb0-109">一般而言，Azure VM 啟用問題發生原因 hello Windows VM 並未設定使用 hello 適當的 KMS 用戶端安裝識別碼，或是 hello Windows VM 有連線問題 toohello Azure KMS 服務 （kms.core.windows.net、 連接埠 1668年）。</span><span class="sxs-lookup"><span data-stu-id="8cbb0-109">Generally, Azure VM activation issues occur if hello Windows VM is not configured by using hello appropriate KMS client setup key, or hello Windows VM has a connectivity problem toohello Azure KMS service (kms.core.windows.net, port 1668).</span></span> 

## <a name="solution"></a><span data-ttu-id="8cbb0-110">方案</span><span class="sxs-lookup"><span data-stu-id="8cbb0-110">Solution</span></span>

>[!NOTE]
><span data-ttu-id="8cbb0-111">如果您使用站對站 VPN，而且強制通道，請參閱[使用 Azure 自訂路由 tooenable KMS 啟用強制通道](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx)。</span><span class="sxs-lookup"><span data-stu-id="8cbb0-111">If you are using a site-to-site VPN and forced tunneling, see [Use Azure custom routes tooenable KMS activation with forced tunneling](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx).</span></span> 
>
><span data-ttu-id="8cbb0-112">如果您使用 ExpressRoute，您有已發佈的預設路由，請參閱[Azure VM 可能會透過 ExpressRoute 失敗 tooactivate](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx)。</span><span class="sxs-lookup"><span data-stu-id="8cbb0-112">If you are using ExpressRoute and you have a default route published, see [Azure VM may fail tooactivate over ExpressRoute](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx).</span></span>

### <a name="step-1-configure-hello-appropriate-kms-client-setup-key-for-windows-server-2016-and-windows-server-2012-r2"></a><span data-ttu-id="8cbb0-113">步驟 1 設定 hello 適當的 KMS 用戶端安裝識別碼 （適用於 Windows Server 2016 和 Windows Server 2012 R2）</span><span class="sxs-lookup"><span data-stu-id="8cbb0-113">Step 1 Configure hello appropriate KMS client setup key (for Windows Server 2016 and Windows Server 2012 R2)</span></span>

<span data-ttu-id="8cbb0-114">Hello 從 Windows Server 2016 或 Windows Server 2012 R2 的自訂映像建立的 VM，您必須設定 hello 適當的 KMS 用戶端安裝識別碼 hello VM。</span><span class="sxs-lookup"><span data-stu-id="8cbb0-114">For hello VM that is created from a custom image of Windows Server 2016 or Windows Server 2012 R2, you must configure hello appropriate KMS client setup key for hello VM.</span></span>

<span data-ttu-id="8cbb0-115">TooWindows 2012 或 Windows 2008 R2，則不適用此步驟。</span><span class="sxs-lookup"><span data-stu-id="8cbb0-115">This step does not apply tooWindows 2012 or Windows 2008 R2.</span></span> <span data-ttu-id="8cbb0-116">它會使用 hello 自動化虛擬機器啟用 (AVMA) 功能，才支援 Windows Server 2016 和 Windows Server 2012 R2。</span><span class="sxs-lookup"><span data-stu-id="8cbb0-116">It uses hello Automation Virtual Machine Activation (AVMA) feature, which is supported only by Windows Server 2016 and Windows Server 2012 R2.</span></span>

1. <span data-ttu-id="8cbb0-117">在提升權限的命令提示字元執行 **slmgr.vbs /dlv**。</span><span class="sxs-lookup"><span data-stu-id="8cbb0-117">Run **slmgr.vbs /dlv** at an elevated command prompt.</span></span> <span data-ttu-id="8cbb0-118">檢查 hello hello 輸出中的描述值，然後決定是否已建立從零售 （零售通路） 或磁碟區 (VOLUME_KMSCLIENT) 授權媒體：</span><span class="sxs-lookup"><span data-stu-id="8cbb0-118">Check hello Description value in hello output, and then determine whether it was created from retail (RETAIL channel) or volume (VOLUME_KMSCLIENT) license media:</span></span>
  
    ```
    cscript c:\windows\system32\slmgr.vbs /dlv
    ```

2. <span data-ttu-id="8cbb0-119">如果**slmgr.vbs /dlv**顯示零售通路，執行下列命令 tooset hello hello [KMS 用戶端安裝識別碼](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396)hello 版本的 Windows Server 正在使用，而且強制它 tooretry 啟用：</span><span class="sxs-lookup"><span data-stu-id="8cbb0-119">If **slmgr.vbs /dlv** shows RETAIL channel, run hello following commands tooset hello [KMS client setup key](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) for hello version of Windows Server being used, and force it tooretry activation:</span></span> 

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk <KMS client setup key>

    cscript c:\windows\system32\slmgr.vbs /ato
     ```

    <span data-ttu-id="8cbb0-120">比方說，Windows Server 2016 資料中心，您可以執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="8cbb0-120">For example, for Windows Server 2016 Datacenter, you would run hello following command:</span></span>

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk CB7KF-BWN84-R7R2Y-793K2-8XDDG
    ```

### <a name="step-2-verify-hello-connectivity-between-hello-vm-and-azure-kms-service"></a><span data-ttu-id="8cbb0-121">步驟 2 確認 hello 連線之間 hello VM 和 Azure KMS 服務</span><span class="sxs-lookup"><span data-stu-id="8cbb0-121">Step 2 Verify hello connectivity between hello VM and Azure KMS service</span></span>

1. <span data-ttu-id="8cbb0-122">下載並解壓縮 hello [Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) hello VM，不會啟動的工具 tooa 本機資料夾。</span><span class="sxs-lookup"><span data-stu-id="8cbb0-122">Download and extract hello [Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) tool tooa local folder in hello VM that does not activate.</span></span> 

2. <span data-ttu-id="8cbb0-123">移 tooStart 搜尋 Windows PowerShell、 Windows PowerShell 中，以滑鼠右鍵按一下，然後選取 以系統管理員身分執行。</span><span class="sxs-lookup"><span data-stu-id="8cbb0-123">Go tooStart, search on Windows PowerShell, right-click Windows PowerShell, and then select Run as administrator.</span></span>

3. <span data-ttu-id="8cbb0-124">請確定該 vm 的 hello 設定 toouse hello 正確的 Azure KMS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="8cbb0-124">Make sure that hello VM is configured toouse hello correct Azure KMS server.</span></span> <span data-ttu-id="8cbb0-125">toodo 這點，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="8cbb0-125">toodo this, run the following command:</span></span>
  
    ```
    iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /skms
    kms.core.windows.net:1688
    ```
    <span data-ttu-id="8cbb0-126">hello 命令應該會傳回： 金鑰管理服務的電腦名稱設定 tookms.core.windows.net:1688 成功。</span><span class="sxs-lookup"><span data-stu-id="8cbb0-126">hello command should return: Key Management Service machine name set tookms.core.windows.net:1688 successfully.</span></span>

4. <span data-ttu-id="8cbb0-127">使用 Psping 您有連線能力 toohello KMS 伺服器驗證。</span><span class="sxs-lookup"><span data-stu-id="8cbb0-127">Verify by using Psping that you have connectivity toohello KMS server.</span></span> <span data-ttu-id="8cbb0-128">切換 toohello hello Pstools.zip 下載、 解壓縮的資料夾，然後執行 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="8cbb0-128">Switch toohello folder where you extracted hello Pstools.zip download, and then run hello following:</span></span>
  
    ```
    \psping.exe kms.core.windows.net:1688
    ```
  
  <span data-ttu-id="8cbb0-129">在 hello 輸出 hello 倒數第二行，請確定您看到： 傳送 = 4，已接收 = 4，遺失 = 0 （0%遺失）。</span><span class="sxs-lookup"><span data-stu-id="8cbb0-129">In hello second-to-last line of hello output, make sure that you see: Sent = 4, Received = 4, Lost = 0 (0% loss).</span></span>

  <span data-ttu-id="8cbb0-130">如果遺失大於 0 （零），hello VM 並沒有連線 toohello KMS 的伺服器。</span><span class="sxs-lookup"><span data-stu-id="8cbb0-130">If Lost is greater than 0 (zero), hello VM does not have connectivity toohello KMS server.</span></span> <span data-ttu-id="8cbb0-131">在此情況下，如果 hello VM 虛擬網路中，且具有自訂指定的 DNS 伺服器，您必須確定該 DNS 伺服器是可以 tooresolve kms.core.windows.net。</span><span class="sxs-lookup"><span data-stu-id="8cbb0-131">In this situation, if hello VM is in a virtual network and has a custom DNS server specified, you must make sure that DNS server is able tooresolve kms.core.windows.net.</span></span> <span data-ttu-id="8cbb0-132">或者，變更解決 kms.core.windows.net hello DNS 伺服器 tooone。</span><span class="sxs-lookup"><span data-stu-id="8cbb0-132">Or, change hello DNS server tooone that does resolve kms.core.windows.net.</span></span>

  <span data-ttu-id="8cbb0-133">請注意，如果您從虛擬網路中移除所有 DNS 伺服器，VM 將會使用 Azure 的內部 DNS 服務。</span><span class="sxs-lookup"><span data-stu-id="8cbb0-133">Notice that if you remove all DNS servers from a virtual network, VMs use Azure’s internal DNS service.</span></span> <span data-ttu-id="8cbb0-134">此服務可以解析 kms.core.windows.net。</span><span class="sxs-lookup"><span data-stu-id="8cbb0-134">This service can resolve kms.core.windows.net.</span></span>
  
<span data-ttu-id="8cbb0-135">也請確認尚未設定 hello 客體防火牆會封鎖啟用嘗試的方式。</span><span class="sxs-lookup"><span data-stu-id="8cbb0-135">Also verify that hello guest firewall has not been configured in a manner that would block activation attempts.</span></span>

5. <span data-ttu-id="8cbb0-136">驗證成功的連線 tookms.core.windows.net 之後，執行下列命令，該高權限的 Windows PowerShell 提示字元的 hello。</span><span class="sxs-lookup"><span data-stu-id="8cbb0-136">After you verify successful connectivity tookms.core.windows.net, run hello following command at that elevated Windows PowerShell prompt.</span></span> <span data-ttu-id="8cbb0-137">此命令會多次嘗試啟用。</span><span class="sxs-lookup"><span data-stu-id="8cbb0-137">This command tries activation multiple times.</span></span>

    ```
    1..12 | % { iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /ato” ; start-sleep 5 }
    ```

<span data-ttu-id="8cbb0-138">成功的啟用會傳回類似 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="8cbb0-138">A successful activation returns information that resembles hello following:</span></span>

<span data-ttu-id="8cbb0-139">**正在啟用 Windows(R) Server Datacenter 版本 (12345678-1234-1234-1234-12345678) … 產品已成功啟用。**</span><span class="sxs-lookup"><span data-stu-id="8cbb0-139">**Activating Windows(R), ServerDatacenter edition (12345678-1234-1234-1234-12345678) … Product activated successfully.**</span></span>

## <a name="faq"></a><span data-ttu-id="8cbb0-140">常見問題集</span><span class="sxs-lookup"><span data-stu-id="8cbb0-140">FAQ</span></span> 

### <a name="i-created-hello-windows-server-2016-from-azure-marketplace-do-i-need-tooconfigure-kms-key-for-activating-hello-windows-server-2016"></a><span data-ttu-id="8cbb0-141">我可以建立 Windows Server 2016 hello Azure marketplace。</span><span class="sxs-lookup"><span data-stu-id="8cbb0-141">I created hello Windows Server 2016 from Azure Marketplace.</span></span> <span data-ttu-id="8cbb0-142">需要啟動 Windows Server 2016 hello tooconfigure KMS 金鑰嗎？</span><span class="sxs-lookup"><span data-stu-id="8cbb0-142">Do I need tooconfigure KMS key for activating hello Windows Server 2016?</span></span> 
 
<span data-ttu-id="8cbb0-143">否。</span><span class="sxs-lookup"><span data-stu-id="8cbb0-143">No.</span></span> <span data-ttu-id="8cbb0-144">在 Azure Marketplace 中的 hello 影像的 hello 適當的 KMS 用戶端安裝識別碼已經設定。</span><span class="sxs-lookup"><span data-stu-id="8cbb0-144">hello image in Azure Marketplace has hello appropriate KMS client setup key already configured.</span></span> 

### <a name="does-windows-activation-work-hello-same-way-regardless-if-hello-vm-is-using-azure-hybrid-use-benefit-hub-or-not"></a><span data-ttu-id="8cbb0-145">沒有 Windows 啟動工作 hello 相同方式不論如果 hello VM 或不使用 Azure 混合式使用權益 （集線器）？</span><span class="sxs-lookup"><span data-stu-id="8cbb0-145">Does Windows activation work hello same way regardless if hello VM is using Azure Hybrid Use Benefit (HUB) or not?</span></span> 
 
<span data-ttu-id="8cbb0-146">是。</span><span class="sxs-lookup"><span data-stu-id="8cbb0-146">Yes.</span></span> 
 
### <a name="what-happens-if-windows-activation-period-expires"></a><span data-ttu-id="8cbb0-147">如果 Windows 啟用期間已到期，會發生什麼情況？</span><span class="sxs-lookup"><span data-stu-id="8cbb0-147">What happens if Windows activation period expires?</span></span> 
 
<span data-ttu-id="8cbb0-148">當 hello 寬限期已過期，仍然未啟用 Windows，Windows Server 2008 R2 和更新版本的 Windows 會顯示啟動相關的其他通知。</span><span class="sxs-lookup"><span data-stu-id="8cbb0-148">When hello grace period has expired and Windows is still not activated, Windows Server 2008 R2 and later versions of Windows will show additional notifications about activating.</span></span> <span data-ttu-id="8cbb0-149">hello 桌面底色圖案維持黑色，以及安全性和重大更新，但不是選擇性的更新，將會安裝 Windows Update。</span><span class="sxs-lookup"><span data-stu-id="8cbb0-149">hello desktop wallpaper remains black, and Windows Update will install security and critical updates only, but not optional updates.</span></span> <span data-ttu-id="8cbb0-150">請參閱 hello 通知區段底部 hello hello[授權條件](http://technet.microsoft.com/en-us/library/ff793403.aspx)頁面。</span><span class="sxs-lookup"><span data-stu-id="8cbb0-150">See  hello Notifications section at hello bottom of hello [Licensing Conditions](http://technet.microsoft.com/en-us/library/ff793403.aspx) page.</span></span>   

## <a name="need-help-contact-support"></a><span data-ttu-id="8cbb0-151">需要協助嗎？</span><span class="sxs-lookup"><span data-stu-id="8cbb0-151">Need help?</span></span> <span data-ttu-id="8cbb0-152">請連絡支援人員。</span><span class="sxs-lookup"><span data-stu-id="8cbb0-152">Contact support.</span></span>
<span data-ttu-id="8cbb0-153">如果您仍需要協助，[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)tooget 快速解決您的問題。</span><span class="sxs-lookup"><span data-stu-id="8cbb0-153">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>
