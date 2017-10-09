---
title: "aaaProtect Active Directory 和 DNS 與 Azure Site Recovery |Microsoft 文件"
description: "本文章說明如何使用 Azure Site Recovery 的 Active Directory 的嚴重損壞修復解決方案 tooimplement。"
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: af1d9b26-1956-46ef-bd05-c545980b72dc
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 7/20/2017
ms.author: pratshar
ms.openlocfilehash: 49903e54f6d6e1839b0571b7a852c6d7517f0aa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="protect-active-directory-and-dns-with-azure-site-recovery"></a>以 Azure Site Recovery 保護 Active Directory 和 DNS
企業應用程式，例如 SharePoint、 Dynamics AX 和 SAP 取決於 Active Directory 和 DNS 基礎結構 toofunction 正確。 當您建立應用程式的災害復原解決方案時，它是您需要 tooprotect，並復原之前 hello 的 Active Directory 和 DNS 的重要 tooremember 其他應用程式元件、 tooensure 當災害發生時，項目正常運作。

Site Recovery 是一項 Azure 服務，可藉由協調虛擬機器的複寫、容錯移轉及復原，提供災害復原功能。 站台復原支援複寫案例 tooconsistently 保護，且順暢地容錯移轉虛擬機器和應用程式 tooprivate、 public 或主機服務提供者雲端的數的字。

使用 Site Recovery，您可以針對 Active Directory 建立一個完整的自動化災害復原計畫。 當發生中斷情況時，您可以在幾秒鐘內從任何地方起始容錯移轉，並在數分鐘內啟動並執行 Active Directory。 如果您已部署 Active Directory 的多個應用程式，例如 SharePoint 和 SAP 中您的主要站台，而且您想 toofail 在 hello 完成站台上，您可以容錯移轉第一個使用 Active Directory 站台復原，然後容錯移轉 hello 其他應用程式使用應用程式專屬復原計劃。

本文說明如何 toocreate Active Directory 的災害復原方案、 如何 tooperform 規劃、 未規劃，並使用一種單鍵復原計劃的測試容錯移轉 hello 支援的組態和必要條件。  開始之前，您應該先熟悉 Active Directory 與 Azure Site Recovery。

## <a name="replicating-domain-controller"></a>複寫網域控制站

您需要 toosetup[站台復原複寫](#enable-protection-using-site-recovery)至少一個裝載網域控制站和 DNS 的虛擬機器上。 如果您有[多個網域控制站](#environment-with-multiple-domain-controllers)在環境中，此外 tooreplicating hello 網域控制站虛擬機器使用站台復原也將最多有 tooset[其他網域控制站](#protect-active-directory-with-active-directory-replication) hello 目標站台 （Azure 或內部次要資料中心） 上。 

### <a name="single-domain-controller-environment"></a>單一網域控制站環境
如果您有少數應用程式和只有單一網域控制站，和您想 toofail 在 hello 整個站台上，則建議使用 Site Recovery tooreplicate hello 網域控制站 toohello 次要站台 (您是否無法透過 tooAzure 或tooa 次要站台）。 hello 相同複寫的網域控制站/DNS 虛擬機器可用於[測試容錯移轉](#test-failover-considerations)以及。

### <a name="environment-with-multiple-domain-controllers"></a>含有多個網域控制站的環境
如果您有許多應用程式和多個網域控制站在 hello 環境中，或是如果您打算 toofail 一些應用程式上一次，我們建議，此外 tooreplicating hello 網域控制站虛擬機器的 Site Recovery 您也設定[其他網域控制站](#protect-active-directory-with-active-directory-replication)hello 目標站台 （Azure 或內部次要資料中心） 上。 如[測試容錯移轉](#test-failover-considerations)，您可以使用複寫的站台復原和容錯移轉，hello hello 目標站台上的其他網域控制站的網域控制站。 


hello 下列各節說明如何 tooenable 保護 Site Recovery 中的網域控制站以及如何在 Azure 中的網域控制站 tooset。

## <a name="prerequisites"></a>必要條件
* 內部部署 Active Directory 和 DNS 伺服器。
* 在 Microsoft Azure 訂用帳戶中有 Azure Site Recovery 服務保存庫。
* 如果您要複寫 tooAzure，Vm tooensure 上執行 hello Azure 虛擬機器整備評估工具，變更就 Azure Vm 與 Azure Site Recovery Services 相容。

## <a name="enable-protection-using-site-recovery"></a>使用 Site Recovery 啟用保護
### <a name="protect-hello-virtual-machine"></a>保護 hello 虛擬機器
啟用 hello 網域控制站 /DNS Site Recovery 中的虛擬機器的保護。 設定 hello 虛擬機器類型 （HYPER-V 或 VMware） 為基礎的站台復原設定。 複寫使用站台復原的 hello 網域控制站用於[測試容錯移轉](#test-failover-considerations)。 請確定它符合下列需求的 hello:

1. hello 網域控制站是通用類別目錄伺服器
2. hello 網域控制站應該 hello FSMO 角色的擁有者將需要在測試容錯移轉期間的角色 (這些角色還需要 toobe[抓住](http://aka.ms/ad_seize_fsmo)hello 容錯移轉之後)

### <a name="configure-virtual-machine-network-settings"></a>設定虛擬機器的網路設定
Hello 網域控制站/DNS 虛擬機器，如此 hello 虛擬機器將附加的 toohello 正確網路容錯移轉之後，在站台復原中設定網路設定。 

![VM 網路設定](./media/site-recovery-active-directory/DNS-Target-IP.png)

## <a name="protect-active-directory-with-active-directory-replication"></a>以 Active Directory 複寫保護 Active Directory
### <a name="site-to-site-protection"></a>站對站保護
Hello 次要站台上建立網域控制站。 當您升級 hello 伺服器 tooa 網域控制站角色時，指定 hello hello 名稱正在使用 hello 主要站台的相同網域。 您可以使用 hello **Active Directory 站台及服務**嵌入式管理單元 tooconfigure hello 站台連結上的設定物件會加入 toowhich hello 站台。 藉由設定網站連結，您可以控制兩個以上的網站之間的複寫發生的時間和頻率。 如需詳細資訊，請參閱[排程網站之間的複寫](https://technet.microsoft.com/library/cc731862.aspx)。

### <a name="site-to-azure-protection"></a>站對 Azure 保護
請依照下列指示 hello 太[在 Azure 虛擬網路中建立的網域控制站](../active-directory/active-directory-install-replica-active-directory-domain-controller.md)。 當您升級 hello 伺服器 tooa 網域控制站角色時，指定 hello hello 主要站台上使用相同的網域名稱。

然後[hello hello 虛擬網路的 DNS 伺服器重新設定](../active-directory/active-directory-install-replica-active-directory-domain-controller.md#reconfigure-dns-server-for-the-virtual-network)，在 Azure 中的 toouse hello DNS 伺服器。

![Azure 網路](./media/site-recovery-active-directory/azure-network.png)

**Azure 實際執行網路中的 DNS**

## <a name="test-failover-considerations"></a>測試容錯移轉考量
測試容錯移轉是在與生產網路隔離的網路中發生，因此不會影響生產工作負載。

大部分的應用程式也需要網域控制站和 DNS 伺服器 toofunction hello 存在。 因此，hello 應用程式容錯移轉之前，網域控制站需要 toobe hello 隔離網路 toobe 用於測試容錯移轉中建立。 hello 最簡單的方式 toodo 這是 tooreplicate 與 Site Recovery 的網域控制站/DNS 虛擬機器。 然後執行測試容錯移轉的 hello 網域控制站虛擬機器，才能執行 hello hello 應用程式的復原計劃的測試容錯移轉。 以下是做法：

1. [複寫](site-recovery-replicate-vmware-to-azure.md)hello 網域控制站/DNS 虛擬機器使用站台復原。
1. 建立隔離的網路。 在 Azure 中建立的任何虛擬網路預設是與其他網路隔離。 我們建議 hello 這個網路的 IP 位址範圍與您的生產網路相同。 請勿在此網路上啟用網站對網站連線能力。
1. 提供建立，做為您預期 hello DNS 虛擬機器 tooget hello IP 位址的 hello 網路中的 DNS IP 位址。 如果您要複寫 tooAzure，然後提供 hello IP 位址使用中的容錯移轉的 VM hello**目標 IP**中設定**計算與網路**設定。 

    ![目標 IP](./media/site-recovery-active-directory/DNS-Target-IP.png) **目標 IP**

    ![Azure 測試網路](./media/site-recovery-active-directory/azure-test-network.png)

    **Azure 測試網路中的 DNS**

> [!TIP]
> 站台復原嘗試 toocreate 測試虛擬機器中相同名稱的子網路，以及使用 hello 與中提供的相同 IP**計算與網路**hello 虛擬機器的設定。 如果相同名稱的子網路不是 hello 為測試容錯移轉時，所提供的 Azure 虛擬網路中可用的則依字母順序建立 hello 第一個子網路中測試虛擬機器。 Hello 目標 IP 是 hello 選擇子網路的一部分，如果站台復原會嘗試 toocreate hello 測試容錯移轉虛擬機器使用 hello 目標 IP。 如果 hello 目標 IP 不屬於 hello 選擇子網路，然後取得建立測試容錯移轉虛擬機器，在 hello 選擇子網路中使用任何可用的 IP。 
>
>


1. 如果您要複寫 tooanother 在內部部署站台，而且您使用 DHCP，請依照下列指示 hello 太[針對測試容錯移轉設定 DNS 和 DHCP](site-recovery-test-failover-vmm-to-vmm.md#prepare-dhcp)
1. 執行 hello 網域控制站虛擬機器在 hello 隔離網路中執行測試容錯移轉。 使用的最新可用的**應用程式一致**hello 網域控制站虛擬機器 toodo hello 測試容錯移轉的復原點。 
1. 執行包含 hello 應用程式的虛擬機器的 hello 復原計劃的測試容錯移轉。 
1. 測試完成之後，**清除測試容錯移轉**hello 網域控制站虛擬機器上。 此步驟會刪除針對測試容錯移轉建立 hello 網域控制站。


### <a name="removing-reference-tooother-domain-controllers"></a>移除參考 tooother 網域控制站
當您在進行測試容錯移轉時，您不將所有 hello 網域控制站在 hello 測試網路。 tooremove hello 參考存在於實際執行環境中其他網域控制站，您可能需要過[拿取 FSMO Active Directory 角色](http://aka.ms/ad_seize_fsmo)執行[中繼資料清除](https://technet.microsoft.com/library/cc816907.aspx)遺漏網域控制站。 



> [!IMPORTANT]
> 某些 hello 之後 > 一節中所述的 hello 組態不 hello 標準/預設網域控制站組態。 如果您不想 toomake 這些變更 tooa 實際執行網域控制站，則您可以建立用於 Site Recovery 測試容錯移轉網域控制站專用 toobe 及進行這些變更 toothat。  
>
>

### <a name="issues-because-of-virtualization-safeguards"></a>由於虛擬化保護措施所產生的問題 

從 Windows Server 2012 開始，[Active Directory Domain Services 已內建額外保護措施](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100)。 這些保護，可協助保護對 USN 回復的虛擬的網域控制站，只要基礎 hypervisor 平台 hello 支援-VM 世代識別碼。 Azure 支援 Vm-generationid，這表示執行 Windows Server 2012 或更新版本的 Azure 虛擬機器的網域控制站具有 hello 額外的保護措施。 


重設 hello-VM 世代識別碼，則當 hello hello AD DS 資料庫的 invocationID 也會重設、，捨棄 RID 集區 hello 和 SYSVOL 會標示為非系統授權。 如需詳細資訊，請參閱[簡介 tooActive Directory 網域服務虛擬化](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100)和[安全地虛擬化 DFSR](https://blogs.technet.microsoft.com/filecab/2013/04/05/safely-virtualizing-dfsr/)

容錯移轉 tooAzure 可能會導致重設 Vm-generationid 的介入 hello 額外的保護措施在 Azure 中的 hello 網域控制站虛擬機器啟動時。 這可能會導致**明顯的延遲**使用者不能 toologin toohello 網域控制站虛擬機器中。 此網域控制站只會用於測試容錯移轉，因此不需要虛擬化保護措施。 -VM 世代識別碼 hello 網域控制站虛擬機器不會變更，則您可以變更下列 DWORD too4 hello 在內部部署網域控制站中的 hello 值的 tooensure。

        
        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\gencounter\Start
 

#### <a name="symptoms-of-virtualization-safeguards"></a>虛擬化保護措施的徵兆
 
如果在測試容錯移轉之後執行了虛擬化保護措施，您可能會看到下列一或多個徵兆︰  

世代識別碼變更

![世代識別碼變更](./media/site-recovery-active-directory/Event2170.png)

叫用識別碼變更

![叫用識別碼變更](./media/site-recovery-active-directory/Event1109.png)

無法使用 Sysvol 與 Netlogon 共用

![Sysvol 共用](./media/site-recovery-active-directory/sysvolshare.png)

![Ntfrs Sysvol](./media/site-recovery-active-directory/Event13565.png)

任何 DFSR 資料庫都會遭到刪除

![DFSR DB 刪除](./media/site-recovery-active-directory/Event2208.png)


> [!IMPORTANT]
> 某些 hello 之後 > 一節中所述的 hello 組態不 hello 標準/預設網域控制站組態。 如果您不想 toomake 這些變更 tooa 實際執行網域控制站，則您可以建立用於 Site Recovery 測試容錯移轉網域控制站專用 toobe 及進行這些變更 toothat。  
>
>


### <a name="troubleshooting-domain-controller-issues-during-test-failover"></a>在測試容錯移轉期間，對網域控制站問題進行疑難排解


在命令提示字元中，執行下列命令 toocheck 是否共用 SYSVOL 與 NETLOGON 資料夾的 hello:

    NET SHARE

Hello 命令提示字元處執行下列命令 hello 網域控制站的 tooensure 運作正常的 hello。

    dcdiag /v > dcdiag.txt

Hello 輸出記錄檔中尋找 hello 網域控制站的下列文字 tooconfirm 正常運作。 

* "passed test Connectivity"
* "passed test Advertising"
* "passed test MachineAccount"

如果 hello 上述條件符合，它可能是該 hello 網域控制站正常運作。 如果沒有，請嘗試下列步驟。


* 請勿 hello 網域控制站的系統授權還原。
    * 雖然[不建議使用 toouse FRS 複寫](https://blogs.technet.microsoft.com/filecab/2014/06/25/the-end-is-nigh-for-frs/)，但是，如果您仍在使用它，然後遵循所提供的 hello 步驟[這裡](https://support.microsoft.com/kb/290762)toodo 系統授權還原。 您可以閱讀更多有關 Burflags hello 先前連結中討論[這裡](https://blogs.technet.microsoft.com/janelewis/2006/09/18/d2-and-d4-what-is-it-for/)。
    * 如果您使用 DFSR 複寫，請依照 hello 步驟可用[這裡](https://support.microsoft.com/kb/2218556)toodo 系統授權還原。 您也可以使用這個[連結](https://blogs.technet.microsoft.com/thbouche/2013/08/28/dfsr-sysvol-authoritative-non-authoritative-restore-powershell-functions/)中的 Powershell 函式執行權威復原。 
    
* 藉由設定下列登錄金鑰 too0 hello 在內部部署網域控制站中的，略過初始同步處理需求。 如果此 DWORD 不存在，您可以在節點 'Parameters' 下建立。 您可以在[此處](https://support.microsoft.com/kb/2001093)閱讀相關資訊

        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters\Repl Perform Initial Synchronizations

* 停用的通用類別目錄伺服器是可用 toovalidate 使用者登入，藉由設定下列登錄金鑰 too1 hello 在內部部署網域控制站中的 hello 需求。 如果此 DWORD 不存在，您可以在節點 'Lsa' 下建立。 您可以在[此處](http://support.microsoft.com/kb/241789)閱讀相關資訊

        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\IgnoreGCFailures



### <a name="dns-and-domain-controller-on-different-machines"></a>不同電腦上的 DNS 和網域控制站
如果在 hello 的 DNS 不相同的虛擬機器為 hello 網域控制站，您需要 toocreate DNS VM hello 測試容錯移轉。 如果它們位於 hello 相同的 VM，您可以略過本節。

您可以使用全新的 DNS 伺服器，並建立 hello 所需的所有區域。 例如，如果您的 Active Directory 網域為 contoso.com，您可以建立 DNS 區域與 hello 名稱 contoso.com。hello 項目對應 tooActive 目錄必須更新在 DNS 中，如下所示：

1. 請確定這些設定已就緒 hello 復原計劃中的任何其他虛擬機器出現之前：
   
   * hello 區域必須為名 hello 樹系根名稱。
   * hello 區域必須是檔案備份。
   * hello 區域必須啟用安全和非安全更新。
   * hello 的 hello 網域控制站虛擬機器的解析程式應該指向 toohello hello DNS 虛擬機器的 IP 位址。
2. 執行下列命令，在網域控制站虛擬機器上的 hello:
   
    `nltest /dsregdns`
3. Hello DNS 伺服器上加入區域、 允許不安全的更新，並加入項目，tooDNS:
   
        dnscmd /zoneadd contoso.com  /Primary
        dnscmd /recordadd contoso.com  contoso.com. SOA %computername%.contoso.com. hostmaster. 1 15 10 1 1
        dnscmd /recordadd contoso.com %computername%  A <IP_OF_DNS_VM>
        dnscmd /config contoso.com /allowupdate 1

## <a name="next-steps"></a>後續步驟
讀取[可以保護哪些工作負載？](site-recovery-workload.md) toolearn 深入了解保護與 Azure Site Recovery 的企業工作負載。

