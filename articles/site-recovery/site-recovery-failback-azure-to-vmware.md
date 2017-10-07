---
title: "從 Azure tooon 內部 aaaFailback VMware Vm |Microsoft 文件"
description: "深入了解的 VMware Vm 和實體伺服器 tooAzure 容錯移轉後容錯回復 toohello 在內部部署站台。"
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: 5a47337f-89a9-43e8-8fdc-7da373c0fb0f
ms.service: site-recovery
ms.devlang: na
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 03/27/2017
ms.author: ruturajd
ms.openlocfilehash: 258f5a55252083135b2040e5a235fa1ffbf3b9d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-vmware-virtual-machines-and-physical-servers-toohello-on-premises-site"></a>失敗後的 VMware 虛擬機器和實體伺服器 toohello 在內部部署站台


本文說明如何 toofailback Azure 虛擬機器從 Azure toohello 在內部部署站台。 Hello 遵循此處當您準備好 toofail 回您的 VMware 虛擬機器或 Windows 或 Linux 的實體伺服器之後重新受保護電腦使用這個[參考](site-recovery-how-to-reprotect.md)。

>[!NOTE]
>如果您使用 hello 傳統 Azure 入口網站，請參閱 tooinstructions 提及[這裡](site-recovery-failback-azure-to-vmware-classic.md)增強 VMware tooAzure 架構和[這裡](site-recovery-failback-azure-to-vmware-classic-legacy.md)hello 舊版架構

## <a name="overview"></a>概觀
本節中的 hello 圖表會顯示此案例中的 hello 容錯回復架構。

當 hello 處理序伺服器是在內部部署，您要使用 Azure ExpressRoute 連接時使用這個架構：

![Expressroute 的架構圖](./media/site-recovery-failback-azure-to-vmware-classic/architecture.png)

當處理序伺服器位於 Azure 與您的 hello 有 VPN 或 ExpressRoute 連線，使用這個架構：

![VPN 的架構圖](./media/site-recovery-failback-azure-to-vmware-classic/architecture2.png)

連接埠和 hello 容錯回復架構圖表的完整清單，請參閱 toohello 下列映像：

![所有連接埠的容錯移轉-容錯回復清單](./media/site-recovery-failback-azure-to-vmware-classic/Failover-Failback.png)

您無法透過 tooAzure 之後，您容錯回復 tooyour 在內部部署站台三個階段：

* **階段 1**： 開始複寫您的內部部署站台執行的背景 toohello VMware Vm 重新保護 hello Azure Vm。
* **階段 2**： 您的 Azure Vm 就會複寫的 tooyour 在內部部署站台之後，您容錯移轉 toofail 回從執行 Azure。
* **階段 3**： 資料回失敗之後，您重新保護的 hello 失敗，您的內部部署 Vm 後，好讓它們開始複寫 tooAzure。

### <a name="fail-back-toohello-original-location-or-an-alternate-location"></a>失敗後 toohello 原始位置或替代位置
您容錯移轉 VMware VM 之後，您可以容錯回復 toohello 相同來源 VM，如果它仍然在內部部署。 在此案例中，只有 hello 差異無法回。

如果您容錯實體伺服器時，錯誤後回復永遠是 tooa 新 VMware VM。 在容錯回復實體機器之前，請注意：
* 受保護實體機器的 Azure tooVMware 回容錯時傳回的虛擬機器是。 Windows Server 2008 R2 SP1 的實體機器，不能是回失敗時受保護且容錯 tooAzure。 啟動內部部署虛擬機器的 Windows Server 2008 R2 SP1 機器將會無法 toofail 上一步。
* 請確定您會發現至少一個主要目標伺服器以及 hello 需 ESX/ESXi 主機，您需要 toofail 回。

如果您無法回復 toohello 原始 VM，hello 需要下列憑證：

* 如果 hello VM 受管理的 vCenter 伺服器，hello 主要目標 ESX 主機應該具有存取 toohello Vm 資料存放區。
* 如果 hello VM 在 ESX 主機，但不是由 vCenter 管理，hello hello 硬碟 VM 必須可供 hello MT 的主機存取的資料存放區中。
* 如果您的 VM 位在 ESX 主機，而不使用 vCenter，您應該先完成的 hello MT hello ESX 主機的探索之前您重新保護。 如果您要容錯回復實體伺服器，則也適用這一條件。
* （如果 hello 內部部署 VM 存在） 的另一個選項是 toodelete 前執行容錯回復。 容錯回復然後會在 hello 相同裝載為 hello 主要目標 ESX 主機上建立新的 VM。

當您無法回復 tooan 替代位置時，是復原的 toohello hello 資料相同的資料存放區和 hello 與 hello 在內部部署主要目標伺服器所使用的相同 ESX 主機。

## <a name="prerequisites"></a>必要條件
* toofail 後 VMware Vm 及實體伺服器，您必須在 VMware 環境。 失敗後 tooa 不支援在實體伺服器。
* toofail 上一步，您必須建立 Azure 網路開始設定保護時。 容錯回復需要 VPN 或 ExpressRoute 連線從 hello Azure 網路中的 hello Azure Vm 的所在的 toohello 在內部部署站台。
* 如果您想 toofail hello Vm 將 tooare vCenter server 所管理，請確定您擁有 hello Vm 探索 vCenter 伺服器上的必要權限。 如需詳細資訊，請參閱[複寫 VMware 虛擬機器和實體伺服器與 Azure Site Recovery 的 tooAzure](site-recovery-vmware-to-azure-classic.md)。
* 如果 VM 上有快照，重新保護程序將會失敗。 您可以刪除 hello 快照集或 hello 磁碟。
* 進行容錯回復之前，請建立這些元件：
  * **在 Azure 中建立處理伺服器**。 此元件是您在容錯回復期間建立並保持運作的 Azure VM。 完成容錯回復之後，您可以刪除 hello VM。
  * **建立主要目標伺服器**: hello 主要目標伺服器傳送及接收錯誤後回復資料。 您建立內部部署的 hello 管理伺服器已依預設會安裝在主要目標伺服器。 不過，根據 hello 磁碟區的容錯回復流量，您可能需要 toocreate 個別的主要目標伺服器進行容錯回復。
  * toocreate 在 Linux 執行的其他主要目標伺服器設定 hello Linux VM，再安裝 hello 主要目標伺服器，如稍後所述。
* 執行容錯回復時，組態伺服器必須為內部部署。 在容錯回復期間 hello 虛擬機器必須存在於 hello 組態伺服器資料庫。 Hello 組態伺服器資料庫不包含任何 VM，如果無法成功容錯回復。 因此，請確定您定期備份伺服器。 在損毀時，您需要 toorestore 它以 hello 相同 IP 位址，以便容錯回復運作。
* 設定的 hello disk.enableUUID=true 設定**組態參數**hello 主要的目標在 VMware 中的 VM。 如果此列不存在，請新增它。 這項設定是必要的 tooprovide 一致的通用唯一識別碼 (UUID) toohello 虛擬機器磁碟 (VMDK) 檔案，因此正確裝載。
* 請留意"主要目標伺服器不能儲存體 vMotioned 」 條件，可能會導致 hello 容錯回復 toofail。 hello VM 不會因為 hello 磁碟不會變成可用 tooit。
* 新增磁碟機中，稱為 hello 主要目標伺服器保留磁碟機。 請新增磁碟，然後格式化 hello 磁碟機。

## <a name="failback-policy"></a>容錯回復原則
tooreplicate 後 tooon 內部部署，您必須容錯回復原則。 當您建立正向方向的原則，並且自動關聯 hello 組態伺服器時，會自動建立 hello 原則。 您無法編輯它。 hello 原則具有下列複寫設定的 hello:

* RPO 臨界值 = 15 分鐘
* 復原點保留 = 24 小時
* 應用程式一致快照頻率 = 60 分鐘

 ![Hello 容錯回復原則的複寫設定](./media/site-recovery-failback-azure-to-vmware-new/failback-policy.png)

## <a name="set-up-a-process-server-in-azure"></a>在 Azure 中設定處理伺服器
在 Azure 中安裝處理序伺服器 hello Azure Vm 可以傳送 hello 資料回復 toohello 在內部部署主要目標伺服器。

如果您保護您的虛擬機器做為傳統資源 （也就是 VM 復原在 Azure 中的 hello 是使用 hello 傳統部署模型所建立的 VM），您需要在 Azure 中的處理序伺服器。 如果您已經復原 hello Vm 與 hello 部署類型為 Azure 資源管理員，hello 處理序伺服器必須具有資源管理員 hello 部署類型。 hello 部署類型選取由 hello Azure 虛擬網路，您將部署 hello 至處理序伺服器。

1. 在**保存庫** > **設定** > **站台復原基礎結構**(下**管理**) > **設定伺服器**(下**的 VMware 和實體機器**)，請選取 hello 組態伺服器。
2. 按一下 [處理伺服器]。

  ![[處理伺服器] 按鈕](./media/site-recovery-failback-azure-to-vmware-classic/add-processserver.png)
3. 選擇 toodeploy hello 做為處理序伺服器**部署在 Azure 中的處理序伺服器的容錯回復**。
4. 選取您已經復原 hello Vm hello 訂用帳戶。
5. 選取 hello 您復原 hello Vm 的 Azure 網路。 hello hello 以便 hello 復原 Vm 且 hello 處理序伺服器通訊的相同網路中的處理序伺服器的需求 toobe。
6. 如果您選取*傳統部署模型*網路、 建立透過 hello Azure Marketplace 的 VM，然後 hello 處理序伺服器在安裝它。

 ![hello [新增處理序伺服器] 視窗](./media/site-recovery-failback-azure-to-vmware-classic/add-classic.png)

 為您要建立 hello 處理序伺服器，請特別注意 toohello 下列：
 * hello hello 映像名稱是*Microsoft Azure 站台復原處理序伺服器 V2*。 選取**傳統**為 hello 部署模型。

       ![Select "Classic" as hello Process Server deployment model](./media/site-recovery-failback-azure-to-vmware-classic/templatename.png)
 * 安裝 hello 處理序伺服器相應 toohello 中的指示[複寫 VMware 虛擬機器和實體伺服器與 Azure Site Recovery 的 tooAzure](site-recovery-vmware-to-azure-classic.md)。
7. 如果您選取 hello*資源管理員*Azure 網路，藉由提供下列資訊的 hello 部署處理序伺服器 hello:

  * hello 要 toodeploy hello 伺服器的 hello 資源群組名稱
  * hello hello 伺服器名稱
  * 使用者名稱和密碼登入 toohello 伺服器
  * hello 要 toodeploy hello 伺服器的儲存體帳戶
  * hello 子網路和您想 tooconnect tooit hello 網路介面
   >[!NOTE]
   >您必須建立自己[網路介面](../virtual-network/virtual-networks-multiple-nics.md)(NIC) 和部署處理序伺服器 hello 時選取它。

    ![在 hello 新增處理序伺服器 對話方塊中輸入資訊](./media/site-recovery-failback-azure-to-vmware-classic/psinputsadd.png)

8. 按一下 [確定] 。 這個動作會觸發 hello 處理序伺服器安裝期間建立的資源管理員部署類型的虛擬機器的工作。 tooregister hello 伺服器 toohello 組態伺服器上執行的 hello 內設定 hello VM 中的 hello 指示[複寫 VMware 虛擬機器和實體伺服器與 Azure Site Recovery 的 tooAzure](site-recovery-vmware-to-azure-classic.md)。 也會觸發工作 toodeploy hello 處理序伺服器。

  hello 處理序伺服器會列在 hello**設定伺服器** > **相關聯伺服器** > **處理序伺服器** 索引標籤。

    ![](./media/site-recovery-failback-azure-to-vmware-new/pslistingincs.png)

    > [!NOTE]
    > hello 處理序伺服器看不見下**VM 屬性**。 它僅會出現在 hello**伺服器**hello 管理伺服器登錄到中的索引標籤。 可能需要 10 hello 處理序伺服器 tooappear too15 分鐘。


## <a name="set-up-hello-master-target-server-on-premises"></a>Hello 主要目標伺服器上內部設定
hello 主要目標伺服器收到 hello 容錯回復資料。 hello 伺服器會自動安裝 hello 在內部部署管理伺服器上，但如果您正在失敗太多資料，您可能需要其他主要目標伺服器 tooset。 tooset 上一個主要目標伺服器在內部，請不要遵循 hello:

> [!NOTE]
> 在 Linux 上的主要目標伺服器上的 tooset 略過 toohello 下一個程序。 使用 hello 主要目標 OS 只 CentOS 6.6 最小作業系統。

1. 如果您正要設定 hello 主要目標伺服器在 Windows 上，開啟 hello 快速入門頁面從 hello 您要安裝 hello 主要目標伺服器的 VM。
2. Hello 安裝檔案下載 hello Azure Site Recovery 統一的安裝精靈。
3. 執行 hello 安裝程式並在**開始之前**，選取**新增部署外的其他處理序伺服器 tooscale**。
4. 完整的 hello 精靈在 hello 相同方式時您[設定 hello 管理伺服器](site-recovery-vmware-to-azure-classic.md)。 在 hello**組態伺服器詳細資料**頁面上，指定 IP 位址，hello hello 主要目標伺服器，然後輸入複雜密碼 tooaccess hello VM。

### <a name="set-up-a-linux-vm-as-hello-master-target-server"></a>將 Linux VM 設定為 hello 主要目標伺服器
tooset hello Linux VM，以執行 hello 主要目標伺服器的管理伺服器安裝 hello CentOS 6.6 最小作業系統。 接下來，擷取每個 SCSI 硬碟 hello SCSI 識別碼，請安裝某些其他的封裝，並套用自訂的某些變更。

#### <a name="install-centos-66"></a>安裝 CentOS 6.6

1. Hello 管理伺服器 VM 上安裝 hello CentOS 6.6 最小作業系統。 Hello ISO DVD 光碟機，且 hello 系統開機。 略過 hello 媒體測試。 選取**英文 （美國)** hello 語言選取**基本的存放裝置**，hello 硬碟機的核取不會有任何重要資料，按一下**是**，並捨棄任何資料。 輸入 hello hello 管理伺服器、 主機名稱並選取 hello server 網路介面卡。  在 hello**編輯系統**對話方塊中，選取**時自動連線**，然後再加入靜態 IP 位址、 網路和 DNS 設定。 指定時區。 tooaccess hello 管理伺服器上，輸入 hello 根密碼。
2. 當詢問您要何種類型的安裝時，選取**建立自訂版面配置**為 hello 磁碟分割。 按一下 [下一步] 。 選取 可用，然後按一下建立。 使用 [FS 類型：ext4] 來建立 **/**、**/var/crash** 和 **/home** 磁碟分割。 建立 hello 交換分割為**FS 類型： 交換**。
3. 如果找到現存裝置，將會出現警告訊息。 按一下**格式**tooformat hello 磁碟機與 hello 分割區設定。 按一下**寫入變更 toodisk** tooapply hello 資料分割變更。
4. 選取**安裝開機載入器** > **下一步**tooinstall hello 開機載入器 hello 根磁碟分割上的。
5. Hello 安裝完成時，按一下**重新開機**。

#### <a name="retrieve-hello-scsi-ids"></a>擷取 hello SCSI 識別碼

1. Hello 安裝之後，擷取每個 SCSI 硬碟 hello VM 中的 hello SCSI 識別碼。 因此，關閉 hello 管理伺服器 VM toodo。 在 VMware 中的 hello VM 屬性，以滑鼠右鍵按一下 hello VM 項目 >**編輯設定** > **選項**。
2. 選取 進階 > 一般項目，然後按一下組態參數。 Hello 機器正在執行時，無法使用此選項。 Hello 選項 toobe 可用，如 hello 機器必須關閉。
3. 執行 hello 下列其中一項：
 * 如果 hello 資料列**磁碟。EnableUUID**存在，請確定 hello 值設定得**True** （區分大小寫）。 如果 hello 值已設定 tooTrue，您可以取消，並開機之後，測試為客體作業系統內的 hello SCSI 命令。
 * 如果 hello 資料列**磁碟。EnableUUID**不存在，請按一下**加入資料列**，然後將它加入以 hello **True**值。 請勿使用雙引號。

#### <a name="install-additional-packages"></a>安裝其他套件
下載並安裝其他套件。

1. 請確定 hello 主要目標伺服器已連線的 toohello 網際網路。
2. toodownload 和安裝 15 套件 hello CentOS 儲存機制上，從執行下列命令： `# yum install –y xfsprogs perl lsscsi rsync wget kexec-tools`。
3. 如果您要保護 hello 來源機器正在執行 Linux 與 Reiser 或 XFS 檔案系統 hello 根或開機裝置，請下載並安裝其他封裝，如下所示：

   * \# cd /usr/local
   * \# wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm)
   * \# wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm)
   * \# rpm –ivh kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm
   * \# wget [http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm](http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm)
   * \# rpm –ivh xfsprogs-3.1.1-16.el6.x86_64.rpm
   * \#yum 安裝裝置對應程式-多重路徑 （使用 hello 主要目標伺服器上需要的 tooenable 多重路徑封裝）

#### <a name="apply-custom-changes"></a>套用自訂變更
Hello 後續安裝步驟和已安裝的 hello 封裝完成之後，套用自訂的變更進行 hello 下列：

1. 將複製 hello RHEL 6 64 整合代理程式二進位 toohello VM。 toountar hello 二進位，執行下列命令： `tar –zxvf <file name>`。
2. toogive 權限，執行下列命令： `# chmod 755 ./ApplyCustomChanges.sh`。
3. 執行 hello 下列指令碼： `# ./ApplyCustomChanges.sh`。 只要執行一次。 已順利執行之後，請將 hello 伺服器重新開機。

## <a name="run-hello-failback"></a>執行 hello 容錯回復
### <a name="reprotect-hello-azure-vms"></a>重新保護 hello Azure Vm
1. 在**保存庫**，請在**複寫項目**，以滑鼠右鍵按一下 hello 已超過失敗的 VM，然後選取**重新保護**。
2. 在 hello 刀鋒視窗中，您可以看到的保護該 hello 方向**Azure tooOn 內部**已選取。
3. 在**主要目標伺服器**和**處理序伺服器**選取 hello 在內部部署主要目標伺服器，hello Azure VM 的處理序伺服器。
4. 您想 toorecover hello 磁碟選取 hello 資料存放區提供從內部部署。 Hello 內部刪除 VM，您需要 toocreate 新磁碟時，請使用此選項。 如果 hello 磁碟已經存在，但是您仍然需要 toospecify 值，請忽略 hello 選項。
5. 使用 保留磁碟機 toostop hello 點 hello VM 時複寫後 tooon 內部部署的時間。 這裡列出保留磁碟機的一些條件。 這些條件，沒有 hello 磁碟機未列出 hello 主要目標伺服器。

  * 磁碟區不能使用於其他用途 (做為複寫目標等)。
  * 磁碟區不能處於鎖定模式。
  * 磁碟區不能是快取磁碟區。 （hello 主要目標安裝不應該存在於該磁碟區上。 hello 處理序伺服器和主要目標的自訂安裝磁碟區不符合資格的保留磁碟區。 在這裡，hello 安裝處理序伺服器加上主要目標是 hello 快取磁碟區的 hello 主要目標。）
  * FAT 及 FAT32，不應該是 hello 磁碟區的檔案系統類型。
  * hello 磁碟區容量應為非零。
  * 適用於 Windows hello 預設保留磁碟區是 R 磁碟區。
  * 適用於 Linux 的 hello 預設保留磁碟區是 /mnt/retention。

6. hello 容錯回復原則會自動選取。
7. 按一下 之後**確定**toobegin 重新保護，在工作開始 tooreplicate hello VM 從 Azure toohello 在內部部署站台。 您可以在 hello 追蹤 hello 進度**作業** 索引標籤。

如果您想 toorecover tooan 替代位置，選取 hello 保留磁碟機和資料存放區，已針對 hello 主要目標伺服器。 當您無法回復 toohello 在內部部署站台時，hello 容錯回復保護計劃中的 hello VMware Vm 使用 hello 與 hello 主要目標伺服器的相同資料存放區。 如果您想 toorecover hello 複本 Azure VM toohello 相同內部 VM，hello 內部部署 VM 應該已可在 hello 相同資料存放區為 hello 主要目標伺服器。 如果內部部署環境中沒有任何 VM，則會在重新保護期間建立一個新的 VM。

![「 Azure tooon 內部部署 」 功能表中選取 [hello] 下拉式清單](./media/site-recovery-failback-azure-to-vmware-new/reprotectinputs.png)

您也可以在復原計劃層級重新保護。 如果您有一個複寫群組，則只能使用復原方案來重新保護它。 當您重新保護使用復原計劃時，使用每個受保護機器 hello 先前的值。

> [!NOTE]
> 複寫群組應該受到保護以 hello 回相同的主要目標。 如果使用不同的主要目標伺服器重新保護，則無法針對它們判斷一般時間點。

### <a name="run-a-failover-toohello-on-premises-site"></a>執行容錯移轉 toohello 在內部部署站台
您重新保護 hello VM 之後，您可以起始從 Azure tooon 內部部署的容錯移轉。

1. 在 hello 複寫的項目頁面上，hello 虛擬機器，以滑鼠右鍵按一下，然後選取**規劃的容錯移轉**。
2. 在**確認容錯移轉**，確認 hello 容錯移轉方向 （從 Azure)，然後選取 hello toouse 需 hello 容錯移轉 （最新，hello 或 hello 最近的應用程式一致復原點） 的復原點。 應用程式一致復原點，就會發生 hello 最新的點之前的時間，而會造成部分資料遺失。
3. 容錯移轉期間，站台復原會關閉 hello Azure Vm。 檢查在已完成如預期般容錯回復之後，您可以檢查 hello Azure Vm 已關閉如預期般的 tooensure。

### <a name="reprotect-hello-on-premises-site"></a>重新保護 hello 在內部部署站台
在完成容錯回復之後，會刪除 hello Vm 在 Azure 中復原的認可 hello 虛擬機器 tooensure。 toodo 因此 hello 受保護的項目，以滑鼠右鍵按一下，然後再按一下**認可**。 這個動作會觸發移除 hello 先前復原的虛擬機器在 Azure 中的工作。

Hello 認可完成之後，資料應該在 hello 在內部部署站台，但不會受到保護。 toostart 複寫 tooAzure 同樣地，請勿 hello 遵循：

1. 在**保存庫**，請在**設定** > **複寫項目**，選取的復原失敗，然後按一下hello Vm**重新保護**.
2. 指定處理序伺服器需要使用 toobe toosend 資料回復 tooAzure hello hello 的值。
3. 按一下 [確定] 。

Hello 重新保護已完成之後，hello VM 複寫 tooAzure 後，您可以在容錯移轉。

### <a name="resolve-common-failback-issues"></a>解決常見容錯回復問題
* 如果您執行唯讀的使用者 vCenter 探索並保護虛擬機器，這樣會成功且容錯回復可作用。 重新保護，在容錯移轉失敗，因為找不到 hello datastores。 問題徵兆所在，不會看到 hello datastores 列出期間重新保護。 tooresolve 這個問題，您可以使用適當的帳戶具有權限更新 hello vCenter 認證，然後重試 hello 作業。 如需詳細資訊，請參閱[複寫 VMware 虛擬機器和實體伺服器 tooAzure 與 Azure Site Recovery](site-recovery-vmware-to-azure-classic.md)
* 當您進行容錯回復 Linux VM，並在內部部署執行時，您可以看到該 hello 網路管理員封裝已從 hello 電腦解除安裝。 由於 hello 網路管理員封裝會移除在復原之後 hello VM 在 Azure 中，會發生此解除安裝。
* 當 VM 設定為使用靜態 IP 位址，並且會容轉移 tooAzure 時，透過 DHCP 取得 hello IP 位址。 當您容錯移轉後 tooon 內部時，hello VM 會繼續 toouse DHCP tooacquire hello IP 位址。 手動登入 toohello 機器，並設定必要時 hello IP 位址後 tooa 靜態位址。
* 如果您是使用 ESXi 5.5 免費版或 vSphere 6 Hypervisor 免費版，則容錯移轉會成功，但容錯回復不會成功。 tooenable 容錯回復，升級 tooeither 程式評估授權。
* 如果您無法連接從處理序伺服器 hello hello 組態伺服器，檢查 Telnet toohello 組態伺服器電腦上連接埠 443 連線 toohello 組態伺服器。 您也可以嘗試從 hello 處理序伺服器機器 tooping hello 組態伺服器。 處理序伺服器也應具有活動訊號時連接的 toohello 組態伺服器。
* 如果您嘗試 toofail 後 tooan 替代 vCenter，確定已探索您新增的 vCenter，而且也會發現該 hello 主要目標伺服器。 一般症狀就是 hello datastores 不存取或看到在 hello**重新保護** 對話方塊。
* 實體在內部部署機器不能無法從 Azure tooon 內部，保護 WS2008R2SP1 機器。

## <a name="fail-back-with-expressroute"></a>透過 ExpressRoute 進行容錯回復
您可以透過 VPN 連線或 ExpressRoute 連線進行容錯回復。 如果您想 toouse ExpressRoute 連線，請注意 hello 下列：

* hello ExpressRoute 連線應該設定 hello hello 來源機器容錯移轉 tooand 的 Azure 虛擬網路上 hello Azure Vm 位於何處 hello 容錯移轉發生後。
* 資料會複寫的 tooan 公用端點上的 Azure 儲存體帳戶。 公用對等互連中 ExpressRoute hello 目標資料中心複寫站台復原設定 toouse ExpressRoute 連線。
