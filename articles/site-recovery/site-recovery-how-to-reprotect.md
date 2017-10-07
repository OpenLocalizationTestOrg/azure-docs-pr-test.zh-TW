---
title: "從 Azure tooan 在內部部署站台 aaaReprotect |Microsoft 文件"
description: "容錯移轉之後的 Vm tooAzure，您可以起始容錯回復 toobring Vm 後 tooon 內部。 深入了解如何 tooreprotect 之前容錯回復。"
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: ruturajd
ms.openlocfilehash: 94c86e79cba4cd3f0c5821fdd5509cca1d0e7820
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="reprotect-from-azure-tooan-on-premises-site"></a>從 Azure tooan 在內部部署站台重新保護



## <a name="overview"></a>概觀
本文說明如何 tooreprotect Azure 虛擬機器從 Azure tooan 在內部部署站台。 當你準備好 toofail 本文的後續 hello 指示回您的 VMware 虛擬機器或實體 Windows/Linux 的伺服器從 hello 在內部部署站台 tooAzure 已失敗的移轉後 (如所述[複寫的 VMware 虛擬機器和實體伺服器與 Azure Site Recovery 的 tooAzure](site-recovery-failover.md))。

> [!WARNING]
> 您無法失敗之後您[完成移轉](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration)、 移動虛擬機器 tooanother 資源群組，或刪除 Azure 虛擬機器。


重新保護完成 hello 受保護的虛擬機器要複寫後，您可以起始 hello 虛擬機器 toobring 上的容錯回復它們 toohello 在內部部署站台。

將註解或問題張貼結尾 hello 這份文件或在 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。

取得快速概觀，觀賞 hello 下列關於如何從 Azure tooan 透過 toofail 內部部署站台的視訊。
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video5-Failback-from-Azure-to-On-premises/player]


## <a name="prerequisites"></a>必要條件
當您準備 tooreprotect 虛擬機器時，採用，或考慮 hello 遵循一些必要的動作：

* 如果您管理的 vCenter 伺服器 hello 虛擬機器的 toofail 回，請確定您擁有 hello[必要的權限](site-recovery-vmware-to-azure-classic.md)探索 vCenter server 上的虛擬機器。

  > [!WARNING]
  > 如果快照集上 hello 有內部部署主要目標或 hello 的虛擬機器，重新保護會失敗。 在您繼續 tooreprotect 之前，您可以刪除 hello hello 主要目標上的快照集。 hello hello 虛擬機器上的快照集重新保護工作期間，會自動合併。

* 在容錯回復之前，先建立兩個其他元件：

  * **處理序伺服器**: hello[處理序伺服器](site-recovery-vmware-setup-azure-ps-resource-manager.md)接收來自 Azure 中的 hello 受保護的虛擬機器資料，並將傳送資料 toohello 在內部部署站台。 Hello 處理序伺服器與 hello 受保護的虛擬機器之間需要低延遲網路。 因此，如果您使用 Azure ExpressRoute 連線，或 Azure 型處理序伺服器和 VPN，則可擁有內部部署處理序伺服器。
  
  * **主要目標伺服器**: hello 主要目標伺服器收到的錯誤後回復資料。 hello 在內部部署管理伺服器，您所建立的預設安裝的主要目標伺服器。 不過，根據 hello 磁碟區的容錯回復流量，您可能需要 toocreate 個別的主要目標伺服器進行容錯回復。
    * [Linux 虛擬機器需要 Linux 主要目標伺服器](site-recovery-how-to-install-linux-master-target.md)。
    * Windows 虛擬機器需要 Windows 主要目標伺服器。 您可以再次使用 hello 內部處理序伺服器與主要目標電腦。

    hello 主要目標有其他必要條件中所列[之前重新保護的主要目標上的通用項目 toocheck](site-recovery-how-to-reprotect.md#common-things-to-check-after-completing-installation-of-the-master-target-server)。

* 執行容錯回復時，組態伺服器必須為內部部署。 在容錯回復期間 hello 虛擬機器必須存在於 hello 組態伺服器資料庫。 否則，將無法成功容錯回復。 

> [!IMPORTANT]
> 請確定您定期排程備份設定伺服器。 如果發生嚴重損壞，以相同的 IP 位址，讓錯誤後回復的運作方式的 hello 的 hello 伺服器還原。

* 設定 hello `disk.EnableUUID=true` hello VMware 中的 hello 主要目標虛擬機器組態參數中設定。 如果此列不存在，請新增它。 此設定是必要的 tooprovide 一致 UUID toohello 虛擬機器磁碟 (VMDK)，讓它正確掛載。

* *您無法使用 Storage vMotion hello 主要目標伺服器上*。 這可能會造成 hello 容錯回復 toofail。 hello 虛擬機器無法啟動，所以沒有可用的 tooit hello 磁碟。 tooprevent 這個問題，請從 vMotion 清單排除 hello 主要目標伺服器。

* 加入新的磁碟機 toohello 主要目標伺服器： 保留磁碟機。 加入新的磁碟和格式 hello 磁碟機。


### <a name="frequently-asked-questions"></a>常見問題集

#### <a name="why-do-i-need-a-s2s-vpn-or-an-expressroute-connection-tooreplicate-data-back-toohello-on-premises-site"></a>為什麼需要 S2S VPN 或 ExpressRoute 連線 tooreplicate 資料回復 toohello 在內部部署站台？
而從內部部署 tooAzure 複寫可能是透過網際網路 hello 或 ExpressRoute 具有用於公用互連連接、 保護和容錯回復需要-網站 (S2S) VPN tooreplicate 資料。 提供 hello 網路，以便在 Azure 中的 hello 容錯虛擬機器可以連線到 (ping) hello 在內部部署組態伺服器。 您也可以部署在 hello hello 容錯虛擬機器的 Azure 網路中的處理序伺服器。 此處理序伺服器也應該能夠 toocommunicate 與 hello 在內部部署組態伺服器。

#### <a name="when-should-i-install-a-process-server-in-azure"></a>何時應該在 Azure 中安裝處理序伺服器？


hello 想 tooreprotect Azure 上的虛擬機器傳送複寫資料 tooa 處理序伺服器。 設定您的網路，以便 hello Azure 上的虛擬機器都可以聯繫 hello 處理序伺服器。

您可以部署在 Azure 中的處理序伺服器，或使用 hello 現有處理序伺服器容錯移轉期間使用。 hello 重要點 tooconsider 是 hello 延遲 toosend hello 資料 hello Azure toohello 處理序伺服器上的虛擬機器。

如果您有設定 ExpressRoute 連線，您可以使用內部部署處理序伺服器 toosend 資料，因為 hello hello 虛擬機器與 hello 處理序伺服器之間的延遲很低。

 ![Expressroute 的架構圖](./media/site-recovery-failback-azure-to-vmware-classic/architecture.png)



不過，如果您有只 S2S VPN，我們建議部署在 Azure 中的 hello 處理序伺服器。

 ![VPN 的架構圖](./media/site-recovery-failback-azure-to-vmware-classic/architecture2.png)


請記住該複寫後，只能透過 hello S2S VPN 或使用私用對等互連的 ExpressRoute 網路 hello。 請確定該網路通道上有足夠的可用頻寬。

如需安裝 Azure 型處理序伺服器的資訊，請參閱[管理在 Azure 中執行的處理伺服器](site-recovery-vmware-setup-azure-ps-resource-manager.md)。

> [!TIP]
> 我們建議在容錯回復期間使用 Azure 型處理序伺服器。 如果 hello 處理序伺服器是複寫虛擬機器 （hello Azure 中的容錯移轉機器） 的深入 toohello 較高者為 hello 複寫效能。 不過，在 (poc) 或示範概念證明，您可以使用 ExpressRoute 以及 hello 內部處理序伺服器以私用對等互連 toocomplete hello POC 更快。



#### <a name="what-ports-should-i-open-on-different-components-so-that-reprotection-can-work"></a>在不同的元件上應該開啟哪些連接埠，重新保護才能運作？

![容錯移轉和容錯回復的端點](./media/site-recovery-failback-azure-to-vmware-classic/Failover-Failback.png)

#### <a name="which-master-target-server-should-i-use-for-reprotection"></a>哪一個主要目標伺服器應用於重新保護？
在內部部署主要目標伺服器是必要的 tooreceive 資料從 hello 處理序伺服器，然後撰寫 toohello 在內部部署虛擬機器的 VMDK。 如果您要保護 Windows 虛擬機器，您需要 Windows 主要目標伺服器。 您可以重複使用 hello 內部處理序伺服器與主要目標<!-- !todo component -->。 針對 Linux 虛擬機器，您需要 tooset 設定額外的內部部署 Linux 主要目標。


如需安裝主要目標伺服器的資訊，請參閱：

* [如何 tooinstall Windows 主要目標伺服器](site-recovery-vmware-to-azure.md)
* [如何 tooinstall Linux 主要目標伺服器](site-recovery-how-to-install-linux-master-target.md)


#### <a name="what-datastore-types-are-supported-on-hello-on-premises-esxi-host-during-failback"></a>在容錯回復期間 hello 內部 ESXi 主機上支援哪些資料存放區類型？

目前，Azure Site Recovery 支援容錯回只有 tooa 虛擬機器檔案系統 (VMFS) 或 vSAN 資料存放區。 不支援 NFS 資料存放區。 由於 toothis 限制 hello 資料存放區選取範圍中所輸入的 hello 重新保護畫面是空的 NFS datastores hello 案例中，或顯示 hello vSAN 資料存放區，但在 hello 作業期間發生失敗。 如果您想 toofail 上一步，您可以建立 VMFS 資料存放區在內部部署，並容錯回復 tooit。 此錯誤後回復會導致 hello VMDK 完整下載。

### <a name="common-things-toocheck-after-completing-installation-of-hello-master-target-server"></a>常見的項目 toocheck 完成 hello 主要目標伺服器的安裝之後

* 如果 hello 虛擬機器存在於內部部署上 hello vCenter server，hello 主要目標伺服器需要存取 toohello 在內部部署虛擬機器的 VMDK。 需要的 toowrite hello 複寫資料 toohello 虛擬機器的磁碟存取。 請確認 hello 在內部部署虛擬機器的資料存放區會掛接具有讀取/寫入存取權的 hello 主要目標的主機上。

* 如果 hello 虛擬機器不存在內部 hello vCenter server 上，hello Site Recovery 服務在重新保護期間的需求 toocreate 新的虛擬機器。 建立 hello 主要目標的 hello ESX 主機上建立此虛擬機器。 小心，選擇 hello ESX 主機，以便您想要的 hello 主機上建立 hello 容錯回復的虛擬機器。

* *您無法使用 Storage vMotion hello 主要目標伺服器*。 這可能會造成 hello 容錯回復 toofail。 hello 虛擬機器無法啟動，所以沒有可用的 tooit hello 磁碟。

  > [!WARNING]
  > 如果主要的目標會經歷儲存體 vMotion 工作重新保護之後，所附加的 toohello 主要目標的 hello 受保護的虛擬機器磁碟移轉 toohello hello vMotion 工作目標。 如果您嘗試 toofail 上一步是在此之後，中斷連結的 hello 磁碟失敗，因為找不到 hello 磁碟。 然後，它會變成永久 toofind hello 磁碟儲存體帳戶中。 您需要 toofind 它們以手動方式將其連接 toohello 虛擬機器。 在這之後，就可以啟動 hello 在內部部署虛擬機器。

* 新增保留磁碟機 tooyour 現有 Windows 主要目標伺服器。 加入新的磁碟和格式 hello 磁碟機。 hello 保留磁碟機是使用的 toostop hello 點何時 hello 虛擬機器複寫後 toohello 在內部部署站台。 以下是保留磁碟機的一些條件。 這些條件，沒有 hello 磁碟機不會列出 hello 主要目標伺服器。

   * hello 磁碟區不用於任何其他目的，例如複寫的目標。

   * hello 磁碟區不是處於鎖定模式。

   * hello 磁碟區不是快取磁碟區。 hello 主要目標安裝不應該存在於該磁碟區。 hello hello 處理序伺服器與主要目標的自訂安裝磁碟區不適合保留磁碟區。 Hello 處理序伺服器與主要目標磁碟區上安裝之後，hello 是快取磁碟區的 hello 主要目標。

   * hello hello 磁碟區的檔案系統型別不是 FAT 或 FAT32。

   * hello 磁碟區容量為非零值。

   * 適用於 Windows hello 預設保留磁碟區是 hello R 磁碟區。

   * 適用於 Linux 的 hello 預設保留磁碟區是 /mnt/retention。

  > [!IMPORTANT]
  > 如果您使用現有的處理序伺服器/組態伺服器電腦或小數位數或處理序伺服器/主要目標伺服器電腦，您會需要 tooadd 新磁碟機。 hello 新磁碟機必須符合上述需求的 hello。 如果 hello 保留磁碟機不存在，它不會出現在 hello 入口網站上的 hello 選擇下拉式清單中。 您將加入的磁碟機 toohello 在內部部署主要目標之後，它會使用 too15 hello hello hello 入口網站上的選取範圍中的磁碟機 tooappear 分鐘的時間。 如果 hello 磁碟機不會出現在 15 分鐘之後，您也可以重新整理 hello 組態伺服器。

* Linux 容錯移轉虛擬機器需要 Linux 主要目標伺服器。 Windows 容錯移轉虛擬機器需要 Windows 主要目標伺服器。

* Hello 主要目標伺服器上安裝 VMware 工具。 如果沒有 hello VMware 工具，就無法偵測 hello datastores hello 主要目標的 ESXi 主機上。

* 啟用 hello `disk.EnableUUID=true` hello 主要目標虛擬機器使用 hello vCenter 屬性上的參數。 <!-- !todo Needs link. -->

* hello 主要目標必須至少一個 VMFS 資料存放區連接。 如果沒有，hello**資料存放區**hello 重新保護頁面上的輸入將為空白，且您無法繼續。

* hello 主要目標伺服器不能在 hello 磁碟上有快照集。 如果有快照集，重新保護和容錯回復會失敗。

* hello 主要目標不能有 Paravirtual SCSI 控制器。 hello 控制器只能 LSI 邏輯控制站。 如果沒有 LSI Logic 控制器，重新保護會失敗。

<!--
### Failback policy
tooreplicate back tooon-premises, you will need a failback policy. This policy get automatically created when you create a forward direction policy. Note that

1. This policy gets auto associated with hello configuration server during creation.
2. This policy is not editable.
3. hello set values of hello policy are (RPO Threshold = 15 Mins, Recovery Point Retention = 24 Hours, App Consistency Snapshot Frequency = 60 Mins)
   ![](./media/site-recovery-failback-azure-to-vmware-new/failback-policy.png)

-->

## <a name="steps-tooreprotect"></a>步驟 tooreprotect

> [!NOTE]
> 在 Azure 中的虛擬機器啟動之後，花一些時間 hello 代理程式 tooregister 後 toohello 設定伺服器 （向上 too15 分鐘為單位）。 在此期間，保護失敗，且錯誤訊息表示未安裝該 hello 代理程式。 請等候幾分鐘，然後再次嘗試重新保護。



1. 在**保存庫** > **複寫項目**，hello 已容錯移轉的虛擬機器上按一下滑鼠右鍵，然後選取**重新保護**。 您也可以按一下電腦，並選取 hello**重新保護**hello 命令按鈕。
2. 在 hello 刀鋒視窗中，請注意的保護，該 hello 方向**Azure tooOn 內部**，已選取。
3. 在**主要目標伺服器**和**處理序伺服器**選取 hello 在內部部署主要目標伺服器，hello 處理序伺服器。
4. 如**資料存放區**，選取 hello 想 toorecover hello 磁碟在內部部署資料存放區 toowhich。 刪除 hello 在內部部署虛擬機器，且您需要 toocreate 新磁碟時，會使用這個選項。 如果 hello 磁碟已經存在，但是您仍然需要 toospecify 值，則會忽略這個選項。
5. 選擇 hello 保留磁碟機。
6. hello 容錯回復原則會自動選取。
7. 按一下**確定**toobegin 重新保護。 作業會開始從 Azure toohello 在內部部署站台 tooreplicate hello 虛擬機器。 您可以在 hello 追蹤 hello 進度**作業** 索引標籤。

如果您想 toorecover tooan 替代位置 （刪除 hello 在內部部署虛擬機器） 時，選取 hello 保留磁碟機和資料存放區，已針對 hello 主要目標伺服器。 當您無法回復 toohello 在內部部署站台時，hello VMware 虛擬機器在 hello 容錯回復保護計劃使用 hello hello 主要為相同的資料存放區為目標伺服器。 接著會在 vCenter 中建立新的虛擬機器。

如果您想 toorecover hello 虛擬機器對 Azure tooan 現有內部部署虛擬機器，掛接 hello 內部部署虛擬機器的 datastores hello 主要目標伺服器的 ESXi 主機上的讀取/寫入存取。
    ![重新保護對話方塊](./media/site-recovery-failback-azure-to-vmware-new/reprotectinputs.png)

您也可以重新保護復原方案的 hello 層級。 只能透過復原方案重新保護複寫群組。 當您重新保護使用復原計劃時，您會需要每個受保護的機器 tooprovide hello 值。

> [!NOTE]
> 使用 hello 相同的主要目標伺服器 tooreprotect 複寫群組。 如果您使用不同的主要目標伺服器 tooreprotect 複寫群組，hello 伺服器無法及時提供通用的點。

> [!NOTE]
> hello 在內部部署虛擬機器已關閉期間重新保護。 這有助於確保資料在複寫期間的一致性。 要重新保護完成之後，再將 hello 虛擬機器。

Hello 重新保護成功之後，hello 虛擬機器將會進入受保護的狀態。

## <a name="next-steps"></a>後續步驟

Hello 虛擬機器已進入受保護的狀態之後，您可以[起始容錯回復](site-recovery-how-to-failback-azure-to-vmware.md#steps-to-fail-back)。 

hello 容錯回復會關閉 hello Azure 中的虛擬機器和開機 hello 在內部部署虛擬機器。 預期 hello 應用程式停機一段時間。 Hello 應用程式可容許停機時間時，請選擇容錯回復的時間。

## <a name="common-problems"></a>常見問題

* 如果您使用範本 toocreate 虛擬機器，請確定每部虛擬機器都有它自己的 hello 磁碟 UUID。 如果 hello 內部部署虛擬機器的 UUID 衝突的 hello 主要目標，因為兩者都從建立 hello 相同範本中，保護會失敗。 尚未建立 hello 從相同的另一個主要目標的部署範本。

* 如果您執行唯讀的使用者 vCenter 探索並保護虛擬機器，保護會成功且容錯回復可作用。 重新保護，在容錯移轉失敗，因為找不到 hello datastores。 症狀就是該 hello datastores 未列出期間重新保護。 tooresolve 這個問題，您可以使用適當的帳戶具有權限，更新 hello vCenter 認證，然後重試 hello 作業。 如需詳細資訊，請參閱[複寫 VMware 虛擬機器和實體伺服器與 Azure Site Recovery 的 tooAzure](site-recovery-vmware-to-azure-classic.md)。

* 當您 Linux 虛擬機器進行容錯回復，並在內部部署執行時，您可以看到該 hello 網路管理員封裝已從 hello 電腦解除安裝。 此解除安裝不會因為 hello 網路管理員封裝便會移除 hello 虛擬機器會在 Azure 中復原。

* 當 Linux 虛擬機器使用靜態 IP 位址設定，而且無法透過 tooAzure 時，從 DHCP 取得 hello IP 位址。 當您容錯移轉 tooon 內部時，hello 虛擬機器會繼續 toouse DHCP tooacquire hello IP 位址。 以手動方式登入 toohello 機器，並設定 hello IP 位址後 tooa 靜態位址，如有必要。 Windows 虛擬機器可以再次取得其靜態 IP。

* 如果您是使用 ESXi 5.5 免費版或 vSphere 6 Hypervisor 免費版，則容錯移轉會成功，但容錯回復不會成功。 tooenable 容錯回復，升級 tooeither 程式評估授權。

* 如果您無法連接從 hello 處理序伺服器 hello 組態伺服器，使用 Telnet toocheck 連線 toohello 設定伺服器連接埠 443。 您也可以嘗試從 hello 處理序伺服器 tooping hello 組態伺服器。 處理序伺服器也應具有活動訊號時連接的 toohello 組態伺服器。

* 如果您嘗試 toofail 後 tooan 替代 vCenter，請確定會探索您的新 vCenter 和 hello 主要目標伺服器。 一般症狀就是 hello datastores 不存取或看到在 hello**重新保護** 對話方塊。

* 受實體內部部署伺服器的 Windows Server 2008 R2 SP1 伺服器無法無法從 Azure tooan 在內部部署站台。
