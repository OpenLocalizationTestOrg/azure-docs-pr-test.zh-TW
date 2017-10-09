---
title: "aaaReplicate VMware Vm 或實體伺服器 tooanother 網站 （傳統 Azure 入口網站） |Microsoft 文件"
description: "使用發行項 tooreplicate VMware Vm 或 Windows/Linux 實體伺服器 tooa 此次要站台與 Azure Site Recovery。"
services: site-recovery
documentationcenter: 
author: nsoneji
manager: jwhit
editor: 
ms.assetid: b2cba944-d3b4-473c-8d97-9945c7eabf63
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: nisoneji
ms.openlocfilehash: 5789ca07f0aa15cf194615fd33103dac930d7b7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-on-premises-vmware-virtual-machines-or-physical-servers-tooa-secondary-site-in-hello-classic-azure-portal"></a>複寫在內部部署 VMware 虛擬機器或實體伺服器 tooa 次要站台 hello 傳統 Azure 入口網站中

## <a name="overview"></a>概觀
Azure Site Recovery 中的 InMage Scout 可提供內部部署 VMware 網站之間的即時複寫。 InMage Scout 包含在 Azure Site Recovery 服務訂用帳戶中。 

## <a name="prerequisites"></a>必要條件
**Azure 帳戶**：您將需要一個 [Microsoft Azure](https://azure.microsoft.com/) 帳戶。 您可以從 [免費試用](https://azure.microsoft.com/pricing/free-trial/)開始。 [深入了解](https://azure.microsoft.com/pricing/details/site-recovery/) Site Recovery 價格。

## <a name="step-1-create-a-vault"></a>步驟 1：建立保存庫
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 按一下 [新增] > [管理] > [備份和 Site Recovery (OMS)]。 或者，您也可以按一下 [瀏覽] > [復原服務保存庫] > [加入]。
3. 在**名稱**指定易記名稱 tooidentify hello 保存庫。 如果您有多個訂用帳戶，請選取其中一個。
4. 在「資源群組」中，建立新的資源群組，或選取現有的資源群組。 指定 Azure 區域 toocomplete 必要欄位。
5. 在**位置**，選取 hello hello 保存庫的地理區域。 支援的 toocheck 區域，請參閱[Azure 站台復原定價](https://azure.microsoft.com/pricing/details/site-recovery/)。
6. 如果您想從儀表板 hello tooquickly 存取 hello 保存庫按一下 Pin toodashboard，，然後按一下建立。
7. hello 新的保存庫會出現在 hello 儀表板 > 所有資源，並在 hello 主要復原服務保存庫刀鋒視窗。

## <a name="step-2-configure-hello-vault-and-download-inmage-scout-components"></a>步驟 2： 設定 hello 保存庫，並下載 InMage Scout 元件
1. Hello 復原服務保存庫刀鋒視窗中選取您的保存庫並按一下 [設定]。
2. 在 [設定] > [快速入門] 中，按一下 [Site Recovery] > [步驟 1︰準備基礎結構] > [保護目標]。
3. 在**保護目標**選取 toorecovery 站台，並選取 [是] 與 VMware vSphere Hypervisor。 然後按一下 [確定]。
4. 在**Scout 安裝**，按一下 下載 toodownload InMage Scout 8.0.1 GA 軟體和登錄機碼。 所有 hello hello 安裝程式檔案都需要位於 hello 下載的.zip 檔案中的元件。

## <a name="step-3-install-component-updates"></a>步驟 3：安裝元件更新
最新閱讀 hello[更新](#updates)。 您將安裝在伺服器上的 hello 更新檔案中順序的 hello:

1. RX 伺服器 (如果有的話)
2. 設定伺服器
3. 處理序伺服器
4. 主要目標伺服器
5. vContinuum 伺服器
6. 來源伺服器 (Windows 和 Linux 伺服器)

安裝 hello 更新，如下所示：

1. 下載 hello[更新](https://aka.ms/asr-scout-update5).zip 檔案。 此.zip 檔案包含下列檔案的 hello:

   * RX_8.0.4.0_GA_Update_4_8725872_16Sep16.tar.gz
   * CX_Windows_8.0.4.0_GA_Update_4_8725865_14Sep16.exe
   * UA_Windows_8.0.5.0_GA_Update_5_11525802_20Apr17.exe
   * UA_RHEL6-64_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz
   * vCon_Windows_8.0.5.0_GA_Update_5_11525767_20Apr17.exe
   * 適用於 RHEL5、OL5、OL6、SUSE 10、SUSE 11 的 UA update4 位元：UA_<Linux OS>_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz
2. Hello.zip 檔案解壓縮。<br>
3. **Hello RX server**： 複製**RX_8.0.4.0_GA_Update_4_8725872_16Sep16.tar.gz** toohello RX 伺服器並將它解壓縮。 在 hello 擷取資料夾中，執行**/安裝**。<br>
4. **Hello 組態伺服器/處理序伺服器**： 複製**CX_Windows_8.0.4.0_GA_Update_4_8725865_14Sep16.exe** toohello 組態伺服器和處理序伺服器。 按兩下 toorun 它。<br>
5. **Hello Windows 主要目標伺服器**: tooupdate hello 整合代理程式，複製**UA_Windows_8.0.5.0_GA_Update_5_11525802_20Apr17.exe** toohello 主要目標伺服器。 按兩下該 toorun 它。 如果來源不會更新直到 Update4 請注意，hello 統一的代理程式也是適用的 toohello 來源伺服器。 您應該它 hello 來源伺服器上安裝以及，稍後在此清單中所述。<br>
6. **Hello vContinuum 伺服器**： 複製**vCon_Windows_8.0.5.0_GA_Update_5_11525767_20Apr17.exe** toohello vContinuum 伺服器。  請確定您已經關閉 hello vContinuum 精靈。 按兩下 hello 檔案 toorun 它。<br>
7. **Hello Linux 主要目標伺服器**: tooupdate hello 整合代理程式，複製**UA_RHEL6 64_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz** toohello 主要目標伺服器，並將它解壓縮。 在 hello 擷取資料夾中，執行**/安裝**。<br>
8. **Hello Windows 來源伺服器**： 如果來源已經存在於 update4 不需要更新 5 tooinstall 來源上的代理程式。 如果小於 update4 時，會套用 hello update 5 代理程式。
tooupdate hello 整合代理程式，複製**UA_Windows_8.0.5.0_GA_Update_5_11525802_20Apr17.exe** toohello 來源伺服器。 按兩下該 toorun 它。 <br>
9. **Hello Linux 來源伺服器**: tooupdate hello 統一的代理程式、 將複製對應 UA 檔案 toohello Linux 伺服器的版本，並將它解壓縮。 在 hello 擷取資料夾中，執行**/安裝**。  範例： RHEL 6.7 64 位元伺服器上，複製**UA_RHEL6 64_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz** toohello 伺服器並將它解壓縮。 在 hello 擷取資料夾中，執行**/安裝**。

## <a name="step-4-set-up-replication"></a>步驟 4：設定複寫
1. 站台設定 hello 來源和目標 VMware 之間的複寫。
2. 如需指引，使用 hello 產品 hello 下載 InMage Scout 文件。 或者，您可以存取 hello 文件集如下：

   * [版本資訊](https://aka.ms/asr-scout-release-notes)
   * [相容性矩陣](https://aka.ms/asr-scout-cm)
   * [使用者指南](https://aka.ms/asr-scout-user-guide)
   * [RX 使用者指南](https://aka.ms/asr-scout-rx-user-guide)
   * [快速安裝指南](https://aka.ms/asr-scout-quick-install-guide)

## <a name="updates"></a>更新
### <a name="azure-site-recovery-scout-801-update-5"></a>Azure Site Recovery Scout 8.0.1 Update 5
Scout Update 5 是累積更新， 它有所有的 hello 修正的 update1，直到 update4 和下列新的 bug 修正和增強功能。
從 ASR Scout update4 tooupdate5 新增的修正程式是特定 tooMaster 目標以及 vContinuum 元件。 如果所有的來源伺服器，主要目標、 設定伺服器、 處理序伺服器和 RX 中已存在的 ASR Scout update4 然後您 tooapply 需要更新 5 只能在主要目標伺服器上。 

**新平台支援**
* SUSE Linux Enterprise Server 11 Service Pack 4 (SP4)

> [!NOTE]
> SLES 11 SP4 64 位元 **InMage_UA_8.0.1.0_SLES11-SP4-64_GA_13Apr2017_release.tar.gz** 與基底 Scout GA 套件 **InMage_Scout_Standard_8.0.1 GA.zip** 封裝在一起。 請依照[步驟 1](#step-1-create-a-vault) 所述，從入口網站下載 Scout GA 套件。
>

**錯誤修正和增強功能**

* 增加 Windows 叢集支援的可靠性
    * 某些 hello P2V MSCS 叢集磁碟變成固定-有時 RAW 復原之後
    * 因為 toodisk 次序不相符而 Fixed-P2V MSCS 叢集的復原失敗
    * 已修正 - MSCS 叢集新增磁碟作業因磁碟大小不相符而失敗
    * 已修正 - 來源 MSCS 叢集與 RDM LUN 對應整備檢查在大小確認步驟失敗
    * 因為 tooSCSI 不相符問題而失敗 Fixed-單一節點叢集的保護 
    * 如果目標叢集磁碟存在，就會失敗 Fixed-重新保護的 hello P2V Windows 叢集伺服器。 
    
* 在容錯回復保護期間如果選取的 MT 不在 hello 相同 ESXi 伺服器為 hello 的受保護來源電腦 （在正向保護），然後 vContinuum 收到 hello 錯誤 MT 容錯回復復原期間，且後續的復原作業會失敗。

> [!NOTE]
> 
> * P2V 叢集修正上層為一些適用 tooonly 全新受到 ASR Scout update5 這些實體 MSCS 叢集中。 在 hello tooavail hello 叢集修正已受保護的 P2V MSCS 叢集使用舊的更新，toofollow hello 升級步驟 12 hello > 一節所述，您需要升級受保護的 P2V MSCS 叢集 tooScout Update5 [ASR Scout 版本附註](https://aka.ms/asr-scout-release-notes)。
> 
> * 重新保護實體 MSCS 叢集的可重複使用現有的目標磁碟僅如果次 hello 的重新保護相同的磁碟集正在 hello 叢集節點時最初受保護的每個使用中的 hello。 如果沒有，則手動步驟 12 的區段中所述[ASR Scout 版本資訊](https://aka.ms/asr-scout-release-notes)太移動 hello 目標端磁碟 toohello 正確的資料存放區路徑 toore 使用它們時再重新啟用保護。 如果您未遵循的升級步驟重新保護 P2V 模式中的 hello MSCS 叢集就會在 hello 目標 ESXi 伺服器上建立新的磁碟。 您需要從 hello 資料存放區的 toomanually 刪除 hello 舊磁碟。
> 
> * 每當來源 SLES11 或 SLES11 與服務組件的任何伺服器重新開機後依正常程序，則其中一個應該手動標示 hello**根**就不會通知 CX UI 中的磁碟複寫配對的重新同步處理。 如果您沒有 ' 標記 hello 根磁碟重新同步處理，您可能會看到資料完整性 (DI) 問題。
> 

### <a name="azure-site-recovery-scout-801-update-4"></a>Azure Site Recovery Scout 8.0.1 Update 4
Scout Update 4 是累積更新。 它有所有的 hello 修正的 update1，直到 update3 和下列新的 bug 修正和增強功能。

**新平台支援**

* 新增對 vCenter/vSphere 6.0、6.1 及 6.2 的支援
* 新增對下列 Linux 作業系統的支援
  * Red Hat Enterprise Linux (RHEL)7.0、7.1 及 7.2
  * CentOS 7.0、7.1 及 7.2
  * Red Hat Enterprise Linux (RHEL) 6.8
  * CentOS 6.8

> [!NOTE]
> RHEL/CentOS 7 64 位元 **InMage_UA_8.0.1.0_RHEL7-64_GA_06Oct2016_release.tar.gz** 與基底 Scout GA 套件 **InMage_Scout_Standard_8.0.1 GA.zip** 封裝在一起。 請依照[步驟 1](#step-1-create-a-vault) 所述，從入口網站下載 Scout GA 套件。
>
>

**錯誤修正和增強功能**

* 改善的關機處理下列 Linux 作業系統和複製品 tooprevent 不想要重新同步處理的問題。
  * Red Hat Enterprise Linux (RHEL) 6.x
  * Oracle Linux (OL) 6.x
* 適用於 Linux，限制 toohello 本機使用者整合的代理程式安裝目錄中的權限現在是完整的資料夾存取。
* 在 Windows 上，在負載繁重的分散式應用程式 (例如 SQL 和 Share Point 叢集) 上發出通用分散式一致性書籤時的逾時問題。
* 在 CX 基底安裝程式中新增記錄相關的修正。
* VMware vCLI 6.0 下載連結加入 tooWindows 主要目標的基底安裝程式。
* 針對容錯移轉與 DR 演練期間的網路設定變更，新增更多檢查和記錄。
* 不報告的 toohello CX 有時保留資訊。  
* 針對實體叢集，當發生來源磁碟區壓縮時，透過 vContinuum 精靈執行的磁碟區調整大小作業會失敗。
* 叢集失敗，發生錯誤 「 無法 toofind hello 磁碟簽章 」 的保護時的叢集磁碟是 PRDM 磁碟。
* cxps 傳輸伺服器會因發生超出範圍例外狀況而當機。
* 現在在 vContinuum 精靈的推送安裝頁面中可以調整伺服器名稱和 IP 資料行的大小。
* RX API 增強功能
  * 提供 5 個最新可用的共同一致性點 (僅限 [保證] 標記)。
  * 提供所有的容量與可用空間詳細資料 hello 受保護的裝置。
  * 提供來源伺服器上的 Scout 驅動程式狀態。

> [!NOTE]
> * **InMage_Scout_Standard_8.0.1_GA.zip** 基底套件現在包含已更新的 CX 基底安裝程式 **InMage_CX_8.0.1.0_Windows_GA_26Feb2015_release.exe**  和「Windows 主要目標」基底安裝程式 **InMage_Scout_vContinuum_MT_8.0.1.0_Windows_GA_26Feb2015_release.exe**。 針對所有新的安裝，請使用新的 CX 和「Windows 主要目標」GA 位元。
> * Update 4 可以直接在 8.0.1 GA 上套用。
> * 它們 hello 系統上套用之後，無法回復 hello 組態伺服器和接收更新。
>
>

### <a name="azure-site-recovery-scout-801-update-3"></a>Azure Site Recovery Scout 8.0.1 Update 3
Update 3 包含 hello 下列 bug 修正和增強功能：

* hello 組態伺服器和 RX 失敗 tooregister toohello Site Recovery 保存庫，當它們 hello proxy 後方。
* hello hello 復原點目標 (RPO) 的時數不符合並未更新 hello 健康情況報告中。
* hello 組態伺服器未同步處理與 RX hello ESX 硬體詳細資料] 或 [網路詳細資料包含任何 utf-8 字元時。
* Windows Server 2008 R2 網域控制站失敗 tooboot 之後復原。
* 離線同步處理未如預期般運作。
* 虛擬機器 (VM) 容錯移轉之後，複寫組刪除一直顯示 hello CX UI 段長時間，而且使用者無法完成 hello 容錯回復或繼續作業。
* 已經過最佳化由 hello 一致性的快照集作業的整體 toohelp 減少應用程式像是 SQL 用戶端中斷連接。
* hello 一致性工具 (VACP.exe) 的 hello 效能已改善藉由減少所需的 Windows 上建立快照集 hello 記憶體使用量。
* hello 推入安裝服務當機，當 hello 密碼大於 16 個字元。
* vContinuum 無法檢查及 hello 認證變更時，輸入新的 vCenter 認證提示。
* On Linux，hello 主要目標快取管理員 (cachemgr) 不從會導致複寫組節流 hello 處理序伺服器下載檔案。
* 當 hello 實體的容錯移轉叢集 (MSCS) 磁碟順序是不相同 hello hello 的所有節點上時，複寫未設定某些 hello 叢集磁碟區。
  <br/>請注意該 hello 叢集中需要重新保護 toobe tootake 利用此修正程式。  
* SMTP 功能無法如預期般從 Scout 7.1 tooScout 8.0.1 升級 RX 後運作。
* 詳細的統計資料已經 hello 記錄檔中加入的 hello 回復作業 tootrack hello 時間花 toocomplete 它。
* 已加入的 hello 來源伺服器上的 Linux 作業系統的支援：
  * Red Hat Enterprise Linux (RHEL) 6 Update 7
  * CentOS 6 Update 7
* hello CX 和 RX UI 現在可以顯示 hello 通知 hello 配對，便會進入點陣圖模式。
* hello 下列安全性問題修正已加入 RX 中：

| **問題描述** | **實作程序** |
| --- | --- |
| 透過竄改參數略過授權 |限制的存取 toonon 適用的使用者。 |
| 跨網站偽造要求 |實作的 hello 頁面語彙基元概念，隨機產生的每個頁面。 <br/>利用這項實作，您將會看到： <li> 只有單一登入執行個體的 hello 相同的使用者。</li><li>頁面重新整理無法運作-它將會重新導向 toohello 儀表板。</li> |
| 惡意檔案上傳 |限制的檔案 toocertain 擴充功能。 允許的副檔名︰7z、aiff、asf、avi、bmp、csv、doc、docx、fla、flv、gif、gz、gzip、jpeg、jpg、log、mid、mov、mp3、mp4、mpc、mpeg、mpg、ods、odt、pdf、png、ppt、pptx、pxd、qt、ram、rar、rm、rmi、rmvb、rtf、sdc、sitd、swf、sxc、sxw、tar、tgz、tif、tiff、txt、vsd、wav、wma、wmv、xls、xlsx、xml、zip。 |
| 持續性跨網站指令碼 |加入輸入驗證。 |

> [!NOTE]
> * 所有的 Site Recovery 更新都是累計的。 Update 3 已更新 1 和 Update 2 中的所有 hello 修正。 Update 3 可以直接套用於 8.0.1 GA。
> * 它們 hello 系統上套用之後，無法回復 hello 組態伺服器和接收更新。
>
>

### <a name="azure-site-recovery-scout-801-update-2-update-03dec15"></a>Azure Site Recovery Scout 8.0.1 Update 2 (Update 03Dec15)
Update 2 中的修正包括：

* **設定伺服器**: hello 31 天的免費計量功能無法運作，所預期會在 hello 組態伺服器已登錄在站台復原問題的修正程式。
* **統一的代理程式**: hello 更新正在伺服器上未安裝 hello 主要目標在從 8.0 版 too8.0.1 升級時所導致的更新 1 中問題的修正程式。

### <a name="azure-site-recovery-scout-801-update-1"></a>Azure Site Recovery Scout 8.0.1 Update 1
Update 1 包含 hello 下列 bug 修正和新功能：

* 每個伺服器執行個體享有 31 天的免費保護。 這可讓您 tootest 功能或設定的概念證明。
  * Hello 在伺服器上，包括容錯移轉和容錯回復，所有作業都是免費的 hello 第 31 天內，從站台復原 Scout 先受保護伺服器的 hello 時間算起。
  * 從 hello 32nd 一天開始，每個受保護的伺服器會收費速率 hello 標準執行個體的 Azure Site Recovery 保護 tooa 客戶擁有站台。
  * 在任何時候，目前計費的受保護伺服器的 hello 數目是 hello Azure Site Recovery 保存庫的 hello 儀表板頁面上所提供。
* 加入對 vSphere 命令列介面 (vCLI) 5.5 Update 2 的支援。
* 新增 hello 來源伺服器上的 Linux 作業系統的支援：
  * RHEL 6 Update 6
  * RHEL 5 Update 11
  * CentOS 6 Update 6
  * CentOS 5 Update 11
* Bug 修正 tooaddress hello 下列問題：
  * 保存庫註冊失敗 hello 組態伺服器或 RX 伺服器。
  * 當叢集虛擬機器在恢復期間重新受到保護，叢集磁碟區就不會如預期般出現。
  * 容錯回復失敗時 hello 主要目標伺服器裝載在不同的 ESXi 伺服器 hello 在內部部署生產環境的虛擬機器上。
  * 升級 too8.0.1，這會影響保護及操作時，會變更組態檔的權限。
  * hello 重新同步處理臨界值並不執行如預期般，這會導致 tooinconsistent 複寫行為。
  * hello RPO 設定不會正確出現在 hello 組態伺服器介面。 未壓縮的 hello 資料值不正確地顯示 hello 壓縮值。
  * hello 移除作業並不會如預期般在 hello vContinuum 精靈中，刪除並複寫不會遭到刪除從 hello 組態伺服器介面。
  * 在 hello vContinuum 精靈 hello 磁碟自動未選取，當您按一下**詳細資料**MSCS 虛擬機器的保護期間的 hello 磁碟檢視中。
  * Hello 實體對虛擬 (P2V) 案例中，在所需的 HP 服務，例如 CIMnotify 和 CqMgHost，不會移動的 toomanual 中虛擬機器復原。 這會導致額外的開機時間。
  * Hello 主要目標伺服器上有超過 26 個磁碟時，就會失敗 Linux 虛擬機器保護。

## <a name="next-steps"></a>後續步驟
張貼 hello 有任何問題[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。
