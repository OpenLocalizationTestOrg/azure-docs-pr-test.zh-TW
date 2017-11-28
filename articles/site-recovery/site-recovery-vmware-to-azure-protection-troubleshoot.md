---
title: "針對 VMware/實體到 Azure 的保護錯誤進行疑難排解 | Microsoft Docs"
description: "本文說明常見的 VMware 機器複寫錯誤以及如何疑難排解"
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/26/2017
ms.author: asgang
ms.openlocfilehash: 6ebec2e06566b1e2d6834fdd81c0d8b2801b80b9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-on-premises-vmwarephysical-server-replication-issues"></a><span data-ttu-id="00c3a-103">針對內部部署 VMware/實體伺服器複寫問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="00c3a-103">Troubleshoot on-premises VMware/Physical server replication issues</span></span>
<span data-ttu-id="00c3a-104">使用 Azure Site Recovery 保護您的 VMware 虛擬機器或實體伺服器時，您可能會收到特定的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="00c3a-104">You may receive a specific error message when protecting your VMware virtual machines or physical servers using Azure Site Recovery.</span></span> <span data-ttu-id="00c3a-105">本文將詳述一些較常發生的錯誤訊息，並提供解決它們的疑難排解步驟。</span><span class="sxs-lookup"><span data-stu-id="00c3a-105">This article details some of the more common error messages encountered, along with troubleshooting steps to resolve them.</span></span>


## <a name="initial-replication-is-stuck-at-0"></a><span data-ttu-id="00c3a-106">初始複寫卡在 0%。</span><span class="sxs-lookup"><span data-stu-id="00c3a-106">Initial replication is stuck at 0%</span></span>
<span data-ttu-id="00c3a-107">我們支援部門遇到的大部分初始複寫失敗，都是來自來源伺服器到處理序伺服器或處理序伺服器到 Azure 之間的連線問題。</span><span class="sxs-lookup"><span data-stu-id="00c3a-107">Most of the initial replication failures that we encounter at support are due to connectivity issues between source server-to-process server or process server-to-Azure.</span></span>
<span data-ttu-id="00c3a-108">大部分情況下，您可以依照下面所列的步驟自行疑難排解這些問題。</span><span class="sxs-lookup"><span data-stu-id="00c3a-108">For most cases, you can self troubleshoot these issues by following the steps listed below.</span></span>

###<a name="check-the-following-on-source-machine"></a><span data-ttu-id="00c3a-109">檢查來源機器的下列事項</span><span class="sxs-lookup"><span data-stu-id="00c3a-109">Check the following on SOURCE MACHINE</span></span>
* <span data-ttu-id="00c3a-110">在來源伺服器機器的命令列中，如下所示使用 Telnet 來偵測搭配 https 連接埠 (預設值 9443) 的處理序伺服器，以查看是否有任何網路連線問題或防火牆連接埠封鎖問題。</span><span class="sxs-lookup"><span data-stu-id="00c3a-110">From Source Server machine command line, use Telnet to ping the Process Server with https port (default 9443) as shown below to see if there are any network connectivity issues or firewall port blocking issues.</span></span>
     
    `telnet <PS IP address> <port>`
> [!NOTE]
    > <span data-ttu-id="00c3a-111">使用 Telnet，不要使用 PING 來測試連線。</span><span class="sxs-lookup"><span data-stu-id="00c3a-111">Use Telnet, don’t use PING to test connectivity.</span></span>  <span data-ttu-id="00c3a-112">如未安裝 Telnet，請依照[這裡](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)的步驟操作。</span><span class="sxs-lookup"><span data-stu-id="00c3a-112">If Telnet is not installed, follow the steps list [here](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)</span></span>

<span data-ttu-id="00c3a-113">如果無法連線，允許處理序伺服器上的輸入連接埠 9443，然後檢查問題是否仍然存在。</span><span class="sxs-lookup"><span data-stu-id="00c3a-113">If unable to connect, allow inbound port 9443 on the Process Server and check if the problem still exits.</span></span> <span data-ttu-id="00c3a-114">曾有案例是處理序伺服器位在 DMZ 之後而造成此問題。</span><span class="sxs-lookup"><span data-stu-id="00c3a-114">There has been some cases where process server was behind DMZ, which was causing this problem.</span></span>

* <span data-ttu-id="00c3a-115">檢查服務 `InMage Scout VX Agent – Sentinel/OutpostStart` 的狀態，是否沒有在執行，以及檢查問題是否仍然存在。</span><span class="sxs-lookup"><span data-stu-id="00c3a-115">Check the status of service `InMage Scout VX Agent – Sentinel/OutpostStart` if it is not running and check if the problem still exists.</span></span>   
 
###<a name="check-the-following-on-process-server"></a><span data-ttu-id="00c3a-116">檢查處理序伺服器的下列事項</span><span class="sxs-lookup"><span data-stu-id="00c3a-116">Check the following on PROCESS SERVER</span></span>

* <span data-ttu-id="00c3a-117">**檢查處理序伺服器是否主動將資料推送至 Azure**</span><span class="sxs-lookup"><span data-stu-id="00c3a-117">**Check if process server is actively pushing data to Azure**</span></span> 

<span data-ttu-id="00c3a-118">在處理序伺服器機器上，按 Ctrl-Shift-Esc 開啟 [工作管理員]。</span><span class="sxs-lookup"><span data-stu-id="00c3a-118">From Process Server machine, open the Task Manager (press Ctrl-Shift-Esc ).</span></span> <span data-ttu-id="00c3a-119">移至 [效能] 索引標籤，按一下 [開啟資源監視器] 連結。</span><span class="sxs-lookup"><span data-stu-id="00c3a-119">Go to the Performance tab and click ‘Open Resource Monitor’ link.</span></span> <span data-ttu-id="00c3a-120">在 Resource Manager 中，移至 [網路] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="00c3a-120">From Resource Manager, go to Network tab.</span></span> <span data-ttu-id="00c3a-121">檢查「網路活動的處理序」中的 cbengine.exe 是否主動傳送大量資料 (以 MB 為單位)。</span><span class="sxs-lookup"><span data-stu-id="00c3a-121">Check if cbengine.exe in ‘Processes with Network Activity’ is actively sending large volume (in Mbs) of data.</span></span>

![啟用複寫](./media/site-recovery-protection-common-errors/cbengine.png)

<span data-ttu-id="00c3a-123">如果沒有，依照下列步驟操作：</span><span class="sxs-lookup"><span data-stu-id="00c3a-123">If not follow the steps listed below:</span></span>

* <span data-ttu-id="00c3a-124">**檢查處理序伺服器是否能夠連線至 Azure Blob**：選擇並勾選 cbengine.exe 以檢視 TCP 連線，查看是否有處理序伺服器到 Azure 儲存體 blob URL 的連線。</span><span class="sxs-lookup"><span data-stu-id="00c3a-124">**Check if Process server is able to connect Azure Blob**: Select and check cbengine.exe to view the ‘TCP Connections’ to see if there is connectivity from Process server to Azure Storage blob URL.</span></span>

![啟用複寫](./media/site-recovery-protection-common-errors/rmonitor.png)

<span data-ttu-id="00c3a-126">如果沒有，則移至 [控制台] > [服務]，檢查下列服務是否已啟動並執行：</span><span class="sxs-lookup"><span data-stu-id="00c3a-126">If not then go to Control Panel > Services, check if the following services are up and running:</span></span>

     * cxprocessserver
     * InMage Scout VX Agent – Sentinel/Outpost
     * Microsoft Azure Recovery Services Agent
     * Microsoft Azure Site Recovery Service
     * tmansvc
     * 
<span data-ttu-id="00c3a-127">(重新) 啟動任何沒有在執行的服務，然後檢查問題是否仍然存在。</span><span class="sxs-lookup"><span data-stu-id="00c3a-127">(Re)Start any service which is not running and check if the problem still exists.</span></span>

* <span data-ttu-id="00c3a-128">**檢查處理序伺服器是否能夠使用連接埠 443 連線到 Azure 公用 IP 位址**</span><span class="sxs-lookup"><span data-stu-id="00c3a-128">**Check if Process server is able to connect to Azure Public IP address using port 443**</span></span>

<span data-ttu-id="00c3a-129">從 `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` 開啟最新的 CBEngineCurr.errlog，搜尋 ":443" 和 "connection attempt failed"。</span><span class="sxs-lookup"><span data-stu-id="00c3a-129">Open the latest CBEngineCurr.errlog from `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` and search for :443  and connection attempt failed.</span></span>

![啟用複寫](./media/site-recovery-protection-common-errors/logdetails1.png)

<span data-ttu-id="00c3a-131">如果有問題，則從處理序伺服器的命令列，使用 telnet 偵測您 Azure 公用 IP 位址 (上圖中遮蔽的部分，也就是在 CBEngineCurr.currLog 中以連接埠 443 找到的位址)。</span><span class="sxs-lookup"><span data-stu-id="00c3a-131">If there are issues, then from Process Server command line, use telnet to ping your Azure Public IP address (masked in above image) found in the CBEngineCurr.currLog using port 443.</span></span>

      telnet <your Azure Public IP address as seen in CBEngineCurr.errlog>  443
<span data-ttu-id="00c3a-132">如果您無法連線，則檢查存取問題是否由於防火牆或 Proxy (如下一個步驟中所述)。</span><span class="sxs-lookup"><span data-stu-id="00c3a-132">If you are unable to connect, then check if the access issue is due to firewall or Proxy as described in next step.</span></span>


* <span data-ttu-id="00c3a-133">**檢查處理序伺服器上的 IP 位址型防火牆是否封鎖存取**：如果您的伺服器使用 IP 位址型的防火牆規則，請從[這裡](https://www.microsoft.com/download/details.aspx?id=41653)下載 Microsoft Azure Datacenter 的 IP 範圍完整清單，將它們新增到您的防火牆設定中，以確保它們允許對 Azure (和 HTTPS (443) 連接埠) 的通訊。</span><span class="sxs-lookup"><span data-stu-id="00c3a-133">**Check if IP address-based firewall on Process server are not blocking access**: If you are using an IP address-based firewall rules on the server, then download the complete list of Microsoft Azure Datacenter IP Ranges from [here](https://www.microsoft.com/download/details.aspx?id=41653) and add them to your firewall configuration to ensure they allow communication to Azure (and the HTTPS (443) port).</span></span>  <span data-ttu-id="00c3a-134">允許訂用帳戶的 Azure 區域和美國西部使用 IP 位址範圍 (用於存取控制和身分識別管理)。</span><span class="sxs-lookup"><span data-stu-id="00c3a-134">Allow IP address ranges for the Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

* <span data-ttu-id="00c3a-135">**檢查處理序伺服器上的 URL 型防火牆是否封鎖存取**：如果您的伺服器使用 URL 型的防火牆規則，請確定下列 URL 已新增至防火牆設定。</span><span class="sxs-lookup"><span data-stu-id="00c3a-135">**Check if URL-based firewall on Process server is not blocking access**:  If you are using a URL based firewall rules on the server, ensure the following URLs are added to firewall configuration.</span></span> 
     
  <span data-ttu-id="00c3a-136">`*.accesscontrol.windows.net:` 用於存取控制和身分識別管理</span><span class="sxs-lookup"><span data-stu-id="00c3a-136">`*.accesscontrol.windows.net:` Used for access control and identity management</span></span>

  <span data-ttu-id="00c3a-137">`*.backup.windowsazure.com:` 用於複寫資料的傳輸和協調</span><span class="sxs-lookup"><span data-stu-id="00c3a-137">`*.backup.windowsazure.com:` Used for replication data transfer and orchestration</span></span>

  <span data-ttu-id="00c3a-138">`*.blob.core.windows.net:` 用於存取儲存體帳戶來儲存複寫的資料</span><span class="sxs-lookup"><span data-stu-id="00c3a-138">`*.blob.core.windows.net:` Used for access to the storage account that stores replicated data</span></span>

  <span data-ttu-id="00c3a-139">`*.hypervrecoverymanager.windowsazure.com:` 用於複寫管理作業和協調</span><span class="sxs-lookup"><span data-stu-id="00c3a-139">`*.hypervrecoverymanager.windowsazure.com:` Used for replication management operations and orchestration</span></span>

  <span data-ttu-id="00c3a-140">`time.nist.gov` 和 `time.windows.com`：用於檢查系統時間與通用時間之間的時間同步處理</span><span class="sxs-lookup"><span data-stu-id="00c3a-140">`time.nist.gov` and `time.windows.com`: Used to check time synchronization between system and global time.</span></span>

<span data-ttu-id="00c3a-141">適用於 **Azure Government 雲端**的 URL：</span><span class="sxs-lookup"><span data-stu-id="00c3a-141">URLs for **Azure Government Cloud**:</span></span>

`* .ugv.hypervrecoverymanager.windowsazure.us`

`* .ugv.backup.windowsazure.us`

`* .ugi.hypervrecoverymanager.windowsazure.us`

`* .ugi.backup.windowsazure.us` 

* <span data-ttu-id="00c3a-142">**檢查處理序伺服器上的 Proxy 設定是否封鎖存取**。</span><span class="sxs-lookup"><span data-stu-id="00c3a-142">**Check if Proxy Settings on Process server are not blocking access**.</span></span>  <span data-ttu-id="00c3a-143">如果您使用 Proxy 伺服器，請確定 DNS 伺服器可解析 Proxy 伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="00c3a-143">If you are using a Proxy Server, ensure the proxy server name is resolving by the DNS server.</span></span>
<span data-ttu-id="00c3a-144">若要查看您在設定伺服器安裝時所提供的資訊，</span><span class="sxs-lookup"><span data-stu-id="00c3a-144">To check what you have provided at the time of Configuration Server setup.</span></span> <span data-ttu-id="00c3a-145">請移至登錄機碼</span><span class="sxs-lookup"><span data-stu-id="00c3a-145">Go to registry key</span></span>

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Azure Site Recovery\ProxySettings`

<span data-ttu-id="00c3a-146">現在，請確保 Azure Site Recovery 代理程式使用相同設定來傳送資料。</span><span class="sxs-lookup"><span data-stu-id="00c3a-146">Now ensure that the same settings are being used by Azure Site Recovery agent to send data.</span></span>
<span data-ttu-id="00c3a-147">搜尋 Microsoft Azure 備份</span><span class="sxs-lookup"><span data-stu-id="00c3a-147">Search Microsoft Azure  Backup</span></span> 

![啟用複寫](./media/site-recovery-protection-common-errors/mab.png)

<span data-ttu-id="00c3a-149">開啟它，然後按一下 [動作] > [變更屬性]。</span><span class="sxs-lookup"><span data-stu-id="00c3a-149">Open it and click on Action > Change Properties.</span></span> <span data-ttu-id="00c3a-150">在 [Proxy 設定] 索引標籤上，您會看到 Proxy 位址，這應該和登錄設定顯示的相同。</span><span class="sxs-lookup"><span data-stu-id="00c3a-150">Under Proxy Configuration tab, you should see the proxy address, which should be same as shown by the registry settings.</span></span> <span data-ttu-id="00c3a-151">如果沒有，請將它變更為相同的位址。</span><span class="sxs-lookup"><span data-stu-id="00c3a-151">If not, please change it to the same address.</span></span>

![啟用複寫](./media/site-recovery-protection-common-errors/mabproxy.png)

* <span data-ttu-id="00c3a-153">**檢查處理序伺服器是否限制節流頻寬**：增加頻寬，然後檢查問題是否仍然存在。</span><span class="sxs-lookup"><span data-stu-id="00c3a-153">**Check if Throttle bandwidth is not constrained on Process server**:  Increase the bandwidth  and check if the problem still exists.</span></span>

##<a name="next-steps"></a><span data-ttu-id="00c3a-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="00c3a-154">Next steps</span></span>
<span data-ttu-id="00c3a-155">如果您需要更多說明，請在 [ASR 論壇](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr)上張貼您的問題。</span><span class="sxs-lookup"><span data-stu-id="00c3a-155">If you need more help, then post your query to [ASR forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).</span></span> <span data-ttu-id="00c3a-156">我們有一個使用中的社群，我們的其中一位工程師將協助您。</span><span class="sxs-lookup"><span data-stu-id="00c3a-156">We have an active community and one of our engineers will be able to assist you.</span></span>