---
title: "aaaTroubleshoot 保護失敗 VMware/實體 tooAzure |Microsoft 文件"
description: "本文說明 hello 常見 VMware 機器複寫錯誤和如何 tootroubleshoot 它們"
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
ms.openlocfilehash: b821e9aa2610482ba1900645fb75e75744dc442f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-on-premises-vmwarephysical-server-replication-issues"></a>針對內部部署 VMware/實體伺服器複寫問題進行疑難排解
使用 Azure Site Recovery 保護您的 VMware 虛擬機器或實體伺服器時，您可能會收到特定的錯誤訊息。 本文詳細說明的某些 hello 較常見的錯誤訊息發生，以及疑難排解步驟 tooresolve 它們。


## <a name="initial-replication-is-stuck-at-0"></a>初始複寫卡在 0%。
大多數 hello 發現在支援的初始複寫失敗是因為來源伺服器-處理序伺服器或處理序伺服器-Azure 之間 tooconnectivity 問題。
大部分情況下，您可以自行依照下面所列的 hello 步驟疑難排解這些問題。

###<a name="check-hello-following-on-source-machine"></a>檢查來源電腦上的 hello 下列
* 從來源伺服器電腦的命令列，使用 Telnet tooping hello 處理序伺服器與 https 連接埠 （預設值 9443） toosee 如下所示，如果有任何網路連線問題或封鎖問題的防火牆連接埠。
     
    `telnet <PS IP address> <port>`
> [!NOTE]
    > 使用 Telnet，請不要使用 PING tootest 連線。  如果未安裝 Telnet，請遵循 hello 步驟清單[這裡](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)

如果無法 tooconnect，允許傳入的連接埠 9443 hello 處理序伺服器上，並選取 如果 hello 問題仍會結束。 曾有案例是處理序伺服器位在 DMZ 之後而造成此問題。

* 檢查服務狀態 hello`InMage Scout VX Agent – Sentinel/OutpostStart`如果尚未執行，並核取如果 hello 問題仍然存在。   
 
###<a name="check-hello-following-on-process-server"></a>檢查 hello 下列處理序伺服器上

* **檢查是否處理序伺服器在主動推入資料 tooAzure** 

從處理序伺服器電腦，開啟 hello 工作管理員 （按 esc Shift Ctrl 鍵）。 移 toohello 效能] 索引標籤，然後按一下 [開啟資源監視器 ' 連結。 從 資源管理員 中，移 tooNetwork 索引標籤。檢查「網路活動的處理序」中的 cbengine.exe 是否主動傳送大量資料 (以 MB 為單位)。

![啟用複寫](./media/site-recovery-protection-common-errors/cbengine.png)

如果不是下面所列步驟 hello:

* **檢查處理序伺服器是否能夠 tooconnect Azure Blob**： 選取並檢查 cbengine.exe tooview hello 'TCP 連線' toosee，如果沒有從處理序伺服器 tooAzure 儲存體 blob URL 的連線。

![啟用複寫](./media/site-recovery-protection-common-errors/rmonitor.png)

如果不是前往 tooControl 面板 > 服務，可讓您檢查下列服務的 hello 是否已啟動並執行：

     * cxprocessserver
     * InMage Scout VX Agent – Sentinel/Outpost
     * Microsoft Azure Recovery Services Agent
     * Microsoft Azure Site Recovery Service
     * tmansvc
     * 
（重新）啟動未執行任何服務，並檢查 hello 問題仍然存在。

* **檢查處理序伺服器是否能夠 tooconnect tooAzure 公用 IP 位址使用連接埠 443**

開啟 hello 從最新 CBEngineCurr.errlog`%programfiles%\Microsoft Azure Recovery Services Agent\Temp`並搜尋： 443 與連接嘗試失敗。

![啟用複寫](./media/site-recovery-protection-common-errors/logdetails1.png)

如果有問題，然後從處理序伺服器的命令列使用 telnet tooping hello CBEngineCurr.currLog 中找到您 Azure 公用 IP 位址 （在上述映像遮罩） 使用連接埠 443。

      telnet <your Azure Public IP address as seen in CBEngineCurr.errlog>  443
如果您無法 tooconnect，然後檢查 hello 存取問題是否由於 toofirewall 或下一個步驟中所述的 Proxy。


* **檢查是否處理序伺服器上的 IP 位址基礎防火牆會封鎖存取**： 如果您使用 hello 伺服器上的 IP 位址為基礎的防火牆規則，然後下載 hello 的 Microsoft Azure Datacenter IP 範圍從的完整清單[這裡](https://www.microsoft.com/download/details.aspx?id=41653)並將其新增 tooyour 防火牆組態 tooensure 它們允許通訊 tooAzure （和 hello HTTPS (443) 連接埠）。  允許的 IP 位址範圍 hello Azure 區域，您的訂用帳戶，以及美國西部 （用於存取控制與身分識別管理）。

* **檢查是否處理序伺服器上的 URL 為基礎的防火牆不會封鎖存取**： 如果您使用 hello 伺服器上的基礎 URL 防火牆規則，請確認下列 Url 的 hello 會新增 toofirewall 組態。 
     
  `*.accesscontrol.windows.net:` 用於存取控制和身分識別管理

  `*.backup.windowsazure.com:` 用於複寫資料的傳輸和協調

  `*.blob.core.windows.net:`用於存取 toohello 儲存儲存體帳戶複寫的資料

  `*.hypervrecoverymanager.windowsazure.com:` 用於複寫管理作業和協調

  `time.nist.gov`和`time.windows.com`： 使用 toocheck 系統與通用時間之間的時間同步處理。

適用於 **Azure Government 雲端**的 URL：

`* .ugv.hypervrecoverymanager.windowsazure.us`

`* .ugv.backup.windowsazure.us`

`* .ugi.hypervrecoverymanager.windowsazure.us`

`* .ugi.backup.windowsazure.us` 

* **檢查處理序伺服器上的 Proxy 設定是否封鎖存取**。  如果您使用 Proxy 伺服器，請確定 hello DNS 伺服器解析 hello proxy 伺服器名稱。
toocheck 您所提供的組態伺服器安裝程式 hello 次。 Go tooregistry 索引鍵

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Azure Site Recovery\ProxySettings`

現在，請確定該 hello Azure Site Recovery 代理程式 toosend 資料都使用相同的設定。
搜尋 Microsoft Azure 備份 

![啟用複寫](./media/site-recovery-protection-common-errors/mab.png)

開啟它，然後按一下 [動作] > [變更屬性]。 在 Proxy 設定索引標籤上，您應該會看到 hello proxy 位址，且應位於相同的 hello 登錄設定所示。 如果沒有，請將它變更 toohello 相同的位址。

![啟用複寫](./media/site-recovery-protection-common-errors/mabproxy.png)

* **檢查節流的頻寬不限制處理序伺服器上**： 增加 hello 頻寬，並檢查 hello 問題仍然存在。

##<a name="next-steps"></a>後續步驟
如果您需要更多說明，然後張貼您的查詢太[ASR 論壇](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr)。 我們有一個作用中的社群和我們的工程師的其中一個將會無法 tooassist 您。
