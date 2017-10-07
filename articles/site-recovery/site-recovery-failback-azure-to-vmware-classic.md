---
title: "aaaFail hello 傳統入口網站中從 Azure 備份 VMware Vm |Microsoft 文件"
description: "深入了解的 VMware Vm 和實體伺服器 tooAzure 容錯移轉後容錯回復 toohello 在內部部署站台。"
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: 7ca86e21-7a5d-45ab-8f4b-e42da90f199a
ms.service: site-recovery
ms.devlang: na
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: ruturajd
ms.openlocfilehash: 80bc3ab2708a5df953c6532b353da19a4c44ac34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-vmware-virtual-machines-and-physical-servers-toohello-on-premises-site-classic-portal"></a>失敗後的 VMware 虛擬機器和實體伺服器 toohello 在內部部署站台 （傳統入口網站）
> [!div class="op_single_selector"]
> * [Azure 入口網站](site-recovery-failback-azure-to-vmware.md)
> * [Azure 傳統入口網站](site-recovery-failback-azure-to-vmware-classic.md)
> * [Azure 傳統入口網站 (舊版)](site-recovery-failback-azure-to-vmware-classic-legacy.md)
>
>

此文章描述 toofail 從 Azure toohello 在內部部署站台所備份的 Azure 虛擬機器。 當你準備好 toofail 本文的後續 hello 指示回您的 VMware 虛擬機器或實體 Windows/Linux 的伺服器從 hello 在內部部署站台 tooAzure 使用這項功能已失敗的移轉後[教學課程](site-recovery-vmware-to-azure-classic.md)。

## <a name="overview"></a>概觀
這個圖表會顯示此案例中的 hello 容錯回復架構。

Hello 處理序伺服器是在內部部署和使用 ExpressRoute 時，請使用此架構。

![](./media/site-recovery-failback-azure-to-vmware-classic/architecture.png)

Hello 處理序伺服器已經在 Azure 上，而且您有 VPN 或 ExpressRoute 連線，請使用此架構。

![](./media/site-recovery-failback-azure-to-vmware-classic/architecture2.png)

連接埠和 hello 容錯回復架構圖表 toosee hello 完整清單，請參閱下面的 toohello 影像

![](./media/site-recovery-failback-azure-to-vmware-classic/Failover-Failback.png)

容錯回復的運作方式如下：

* 您無法透過 tooAzure 之後，您容錯回復 tooyour 在內部部署站台幾個階段中：
  * **階段 1**： 開始複寫在內部部署站台中執行的後 tooVMware Vm 重新保護 hello Azure Vm。 啟用重新保護將 hello VM 移至您最初建立 hello 容錯移轉保護群組時自動建立的容錯回復保護群組。 如果您加入容錯移轉的保護群組 tooa 復原計劃 hello 容錯回復保護群組已也會自動加入 toohello 計劃。  在重新保護您指定如何 tooplan toofail 回。
  * **階段 2**： 您的 Azure Vm 正在複寫 tooyour 在內部部署站台之後，您執行失敗 toofail 透過從 Azure。
  * **階段 3**： 資料回失敗之後，您重新保護的 hello 失敗，您的內部部署 Vm 後，好讓它們開始複寫 tooAzure。


  [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Failback/player]

### <a name="failback-toohello-original-or-alternate-location"></a>容錯回復 toohello 原始或替代位置
如果您容錯 VMware VM，您就可以容錯回復 toohello 相同來源 VM，如果它仍然在內部部署。 在此案例中會傳回失敗 hello 差異變更。 請注意：

* 如果您容錯移轉實體伺服器，則錯誤後回復永遠是 tooa 新 VMware VM。
  * 在容錯回復實體機器之前，請注意：
  * 傳回的虛擬機器容錯移轉從 Azure tooVMware 時是受保護實體機器
  * 請確定您會發現至少一個主要目標伺服器以及 hello 必要 ESX/ESXi 主機 toowhich 需要 toofailback。
* 如果您進行容錯回復 toohello 原始 VM hello 需要滿足下列條件：

  * 如果 hello VM 由管理的 vCenter 伺服器 hello 主要目標的 ESX 主機應該具有存取 toohello Vm 資料存放區。
  * 如果 hello VM 在 ESX 主機，但不是受 vCenter 則 hello hello 硬碟 VM 必須是中的資料存放區存取 hello MT 的主機。
  * 如果您的 VM 位在 ESX 主機，而不使用 vCenter 您應該完成 hello ESX 主機的 hello MT 的探索之前您重新保護。 如果您要容錯回復實體伺服器，則也適用這一條件。
  * （如果 hello 內部部署 VM 存在） 的另一個選項是 toodelete 前執行容錯回復。 然後容錯回復接著會建立新的 VM hello 相同裝載為 hello 主要目標 ESX 主機上。
* 當您的容錯回復 tooan 替代位置 hello 資料將會復原的 toohello 相同的資料存放區和 hello 與 hello 在內部部署主要目標伺服器所使用的相同 ESX 主機。

## <a name="prerequisites"></a>必要條件
* 您將需要順序 toofail 回 VMware Vm 和實體伺服器中的 VMware 環境。 失敗後 tooa 不支援在實體伺服器。
* 在訂單 toofail 回您應該已經建立 Azure 網路開始設定保護時。 容錯回復需要 VPN 或 ExpressRoute 連線從 hello Azure 網路中的 hello Azure Vm 的所在的 toohello 在內部部署站台。
* 如果您想 toofail 後 tooare vCenter server 所管理的 hello Vm，您將需要 toomake 確定您擁有所需的 hello Vm 探索 vCenter 伺服器上的權限。 [閱讀更多資訊](site-recovery-vmware-to-azure-classic.md)。
* 如果 VM 上有快照，重新保護程序將會失敗。 您可以刪除 hello 快照集或 hello 磁碟。
* 您的容錯回復之前，您必須先 toocreate 多個元件：
  * **在 Azure 中建立處理序伺服器**。 這是在 Azure VM，您將需要 toocreate，並在容錯回復期間繼續執行。 完成容錯回復之後，您可以刪除 hello 機器。
  * **建立主要目標伺服器**: hello 主要目標伺服器傳送及接收錯誤後回復資料。 您建立內部部署的 hello 管理伺服器的預設安裝的主要目標伺服器。 不過，根據 hello 磁碟區的失敗後的流量您可能需要 toocreate 個別的主要目標伺服器的容錯回復。
  * 如果您想 toocreate 在 Linux 上執行的其他主要目標伺服器，您需要 tooset hello Linux VM 上的才安裝 hello 主要目標伺服器，如下所述。
* 執行容錯回復時，組態伺服器必須為內部部署。 在容錯回復期間 hello 虛擬機器必須存在於 hello 組態伺服器資料庫失敗的容錯回復不會先成功完成。 因此，請確定您定期排定備份伺服器。 萬一嚴重損壞，您將需要 toorestore hello 與相同 IP 位址，讓錯誤後回復運作。

## <a name="set-up-hello-process-server-in-azure"></a>設定在 Azure 中的 hello 處理序伺服器
您需要 tooinstall 在 Azure 中的處理序伺服器，如此 hello Azure Vm 可以傳送 hello 資料回復 tooon 內部部署主要目標伺服器。

1. Hello Site Recovery 入口網站 >**設定伺服器**選取 tooadd 新的處理序伺服器。

   ![](./media/site-recovery-failback-azure-to-vmware-classic/ps1.png)
2. 指定處理序伺服器名稱，並輸入名稱和密碼，您將使用 tooconnect toohello Azure VM，以系統管理員。 在**組態伺服器**選取 hello 在內部部署管理伺服器，並指定 hello Azure 網路中的 hello 應該部署處理序伺服器。 這應該是 hello Azure Vm 位於 hello 網路。 指定唯一的 IP 位址從 hello 選取子網路，然後開始進行部署。

   ![](./media/site-recovery-failback-azure-to-vmware-classic/ps2.png)

   將會觸發工作 toodeploy hello 處理序伺服器

   ![](./media/site-recovery-failback-azure-to-vmware-classic/ps3.png)

   Hello 之後處理序伺服器部署在 Azure，您可以登入使用您指定的 hello 認證。 hello 第一次登入 hello 處理序伺服器 對話方塊將會執行。 在 hello IP 位址的 hello 在內部部署管理伺服器的類型和其複雜密碼。 保留 hello 預設連接埠 443 設定。 您也可以將留 hello 資料複寫的預設 9443 通訊埠除非您特別修改此設定，當您設定 hello 在內部部署管理伺服器。

   > [!NOTE]
   > hello 伺服器將不會顯示在**VM 屬性**。 它只會顯示在 [hello**伺服器**中已註冊的 hello 管理伺服器 toowhich] 索引標籤。 需要有關 hello 處理序伺服器 tooappear 的 10-15 分鐘。
   >
   >

## <a name="set-up-hello-master-target-server-on-premises"></a>Hello 主要目標伺服器上內部設定
hello 主要目標伺服器收到 hello 容錯回復資料。 主要目標伺服器會自動安裝 hello 在內部部署管理伺服器上，但如果回無法處理大量資料，您可能需要 tooset 其他主要目標伺服器。 以下列方式來執行此動作：

> [!NOTE]
> 如果您想 tooinstall on Linux 主要目標伺服器，請遵循 hello 下一個程序中的 hello 指示。
>
>

1. 如果您要在 Windows 上安裝 hello 主要目標伺服器，請從 hello VM 安裝 hello 主要目標伺服器，和 hello hello Azure Site Recovery 統一的安裝精靈的安裝檔案下載開啟 hello 快速入門 頁面。
2. 執行安裝程式並在**開始之前**選取**新增額外的處理序伺服器 tooscale 出部署**。
3. 完整的 hello 精靈在 hello 相同方式時您[設定 hello 管理伺服器](site-recovery-vmware-to-azure-classic.md)。 在 hello**組態伺服器詳細資料**頁面上，指定這個主要目標伺服器和 VM 的複雜密碼 tooaccess hello hello IP 位址。

### <a name="set-up-a-linux-vm-as-hello-master-target-server"></a>將 Linux VM 設定為 hello 主要目標伺服器
hello 管理伺服器 hello 主要目標伺服器執行 Linux VM，您將需要 tooinstall hello 美分 tooset) S 6.6 最小作業系統，擷取每個 SCSI 硬碟 hello SCSI 識別碼，請安裝某些其他封裝，並套用自訂的某些變更。

#### <a name="install-centos-66"></a>安裝 CentOS 6.6
1. Hello 管理伺服器 VM 上安裝 hello CentOS 6.6 最小作業系統。 將 hello ISO 保留在 DVD 磁碟機和開機 hello 系統。 在 hello 語言中，選取測試，略過 hello 媒體選取英文 （美國）**基本的存放裝置**，hello 硬碟的檢查沒有任何重要資料，然後再按一下**是**，捨棄任何資料。 輸入 hello hello 管理伺服器的主機名稱並選取 hello server 網路介面卡。  在 hello**編輯系統**對話方塊選取 * * 自動連線 * * 並加入靜態 IP 位址、 網路和 DNS 設定。 指定時區，以及根密碼 tooaccess hello 管理伺服器。
2. 當系統要求您安裝 hello 類型您想要選取**建立自訂版面配置**為 hello 磁碟分割。 按一下 [下一步] 之後，請選取 [免費] 並按一下 [建立]。 使用 [FS 類型：ext4] 來建立 **/**、**/var/crash** 和 **/home** 磁碟分割。 建立 hello 交換分割為**FS 類型： 交換**。
3. 如果找到現存裝置，將會出現警告訊息。 按一下**格式**tooformat hello 磁碟機與 hello 分割區設定。 按一下**寫入變更 toodisk** tooapply hello 資料分割變更。
4. 選取**安裝開機載入器** > **下一步**tooinstall hello 開機載入器 hello 根磁碟分割上的。
5. 安裝完成時，按一下 [重新開機] 。

#### <a name="retrieve-hello-scsi-ids"></a>擷取 hello SCSI 識別碼
1. 安裝完成後擷取每個 SCSI 硬碟 hello VM 中的 hello SCSI 識別碼。 toodo 這關閉 hello 管理伺服器 VM，則在 hello VM VMware 中的屬性按一下滑鼠右鍵 hello VM 項目 >**編輯設定** > **選項**。
2. 選取 [進階]  >  [一般項目]，然後按一下 [組態參數]。 Hello 機器執行時，就能 de-active 此選項。 toomake it 作用中的 hello 機器必須關閉。
3. 如果 hello 資料列**磁碟。EnableUUID**存在確定 hello 值設定得**True** （區分大小寫）。 如果已取消，以測試為客體作業系統內的 hello SCSI 命令後開機。
4. 如果 hello 資料列不現有按一下**加入資料列**– 並將它加入以 hello **True**值。 請勿使用雙引號。

#### <a name="install-additional-packages"></a>安裝其他封裝
您將需要 toodownload 並安裝某些其他的封裝。

1. 請確定 hello 主要目標伺服器已連線的 toohello 網際網路。
2. 執行這個命令 toodownload 並從 hello CentOS 儲存機制安裝套件 15: **# yum 安裝 – y xfsprogs perl lsscsi rsync wget kexec 工具**。
3. 如果您要保護的 hello 來源機器執行 Linux wit Reiser XFS 檔案 hello 根的系統或開機裝置，則您應該下載並安裝其他封裝，如下所示：

   * # <a name="cd-usrlocal"></a>cd /usr/local
   * # <a name="wget-httpelrepoorglinuxelrepoel6x8664rpmskmod-reiserfs-00-1el6elrepox8664rpmhttpelrepoorglinuxelrepoel6x8664rpmskmod-reiserfs-00-1el6elrepox8664rpm"></a>wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm)
   * # <a name="wget-httpelrepoorglinuxelrepoel6x8664rpmsreiserfs-utils-3621-1el6elrepox8664rpmhttpelrepoorglinuxelrepoel6x8664rpmsreiserfs-utils-3621-1el6elrepox8664rpm"></a>wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm)
   * # <a name="rpm-ivh-kmod-reiserfs-00-1el6elrepox8664rpm-reiserfs-utils-3621-1el6elrepox8664rpm"></a>rpm –ivh kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm
   * # <a name="wget-httpmirrorcentosorgcentos66osx8664packagesxfsprogs-311-16el6x8665rpmhttpmirrorcentosorgcentos66osx8664packagesxfsprogs-311-16el6x8665rpm"></a>wget [http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm](http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm)
   * # <a name="rpm-ivh-xfsprogs-311-16el6x8664rpm"></a>rpm –ivh xfsprogs-3.1.1-16.el6.x86_64.rpm

#### <a name="apply-custom-changes"></a>套用自訂變更
執行下列 tooapply 自訂變更之後您已經完成 hello 後續安裝步驟和已安裝的 hello 套件, hello:

1. 將複製 hello RHEL 6 64 整合代理程式二進位 toohello VM。 執行這個命令 toountar hello 二進位： **tar – zxvf<file name>**
2. 執行這個命令 toogive 權限： **# chmod 755./ApplyCustomChanges.sh**
3. 執行 hello 指令碼： **#./ApplyCustomChanges.sh**。您應該一次只執行 hello 指令碼。 Hello 伺服器 hello 指令碼順利執行之後重新開機。

## <a name="run-hello-failback"></a>執行 hello 容錯回復
### <a name="reprotect-hello-azure-vms"></a>重新保護 hello Azure Vm
1. Hello Site Recovery 入口網站 >**機器** 索引標籤選取 hello 已容錯移轉的 VM，然後按一下**重新保護**。
2. 在**主要目標伺服器**和**處理序伺服器**選取 hello 在內部部署主要目標伺服器和 hello Azure VM 的處理序伺服器。
3. 選取您設定為連接 toohello VM hello 帳戶。
4. 選取 hello hello 保護群組的容錯回復版本。 例如，如果您必須先 tooselect PG1_Failback hello VM 保護 PG1 的。
5. 如果您想 toorecover tooan 替代位置，選取 hello 保留磁碟機和資料存放區 hello 主要目標伺服器設定。 當您無法回復 toohello 在內部部署站台 hello VMware Vm hello 容錯回復保護計劃中將會使用 hello 與 hello 主要目標伺服器的相同資料存放區。 如果您想 toorecover hello 複本的 Azure VM toohello 相同內部 VM 則 hello 內部部署 VM 應該已可在 hello 相同資料存放區做為 hello 主要目標伺服器。 如果內部部署環境中沒有任何 VM，則會在重新保護期間建立一個新的 VM。

   ![](./media/site-recovery-failback-azure-to-vmware-classic/failback1.png)
6. 按一下 之後**確定**toobegin 重新保護工作開始 tooreplicate hello VM 從 Azure toohello 在內部部署站台。 您可以在 hello 追蹤 hello 進度**作業** 索引標籤。

   ![](./media/site-recovery-failback-azure-to-vmware-classic/failback2.png)

### <a name="run-a-failover-toohello-on-premises-site"></a>執行容錯移轉 toohello 在內部部署站台
之後重新保護 hello VM 移動的 toohello 容錯回復版本其保護群組，如果有一個用於 hello 容錯移轉 tooAzure toohello 復原方案會自動加入。

1. 在 hello**復原計劃**頁面選取 hello 復原方案中包含 hello 容錯回復的群組，然後按一下**容錯移轉** > **規劃的容錯移轉**。
2. 在**確認容錯移轉**確認 hello 容錯移轉方向 (tooAzure) 並選取您想 toouse hello 容錯移轉 （最新版） 的 hello 復原點。 如果您啟用**多部 VM**當您設定複寫屬性則可以復原 toohello 最新的應用程式或當機一致復原點。 按一下 hello 核取記號 toostart hello 容錯移轉。
3. 在容錯移轉期間 hello Azure Vm 會先關閉站台復原。 您檢查如您預期般完成容錯回復後可以您可以檢查該 hello Azure Vm 已關閉如預期般。

### <a name="reprotect-hello--on-premises-site"></a>重新保護 hello 在內部部署站台
容錯回復完成後您的資料回 hello 在內部部署站台，將會是，但不會受到保護。 toostart 複寫 tooAzure 再次 hello 遵循：

1. Hello Site Recovery 入口網站 >**機器**索引標籤上的備份失敗，按一下 選取 hello Vm**重新保護**。
2. 在您確認該複寫 tooAzure 正常運作之後，在 Azure 中您可以刪除 hello Azure Vm （目前未執行） 已傳回失敗。

### <a name="common-issues-in-failback"></a>容錯回復的常見問題
1. 如果您執行唯讀的使用者 vCenter 探索並保護虛擬機器，這樣會成功且容錯回復可作用。 在 hello 重新保護時，它將會失敗，因為找不到 hello datastores。 問題徵兆所在不會看到 hello datastores 列出同時重新保護。 tooresolve，您可以使用適當的帳戶具有權限更新 hello vCenter 認證，然後重試 hello 作業。 [閱讀更多資訊](site-recovery-vmware-to-azure-classic.md)
2. 當您容錯回復 Linux VM，然後執行內部，您會看到該 hello 網路管理員封裝會從 hello 電腦解除安裝。 這是因為在復原之後 hello VM 在 Azure 中，要移除 hello 網路管理員封裝。
3. 當 VM 設定為使用靜態 IP 位址，並且會容轉移 tooAzure 時，透過 DHCP 取得 hello IP 位址。 當您容錯移轉後 tooOn 內部時，hello VM 會繼續 toouse DHCP tooacquire hello IP 位址。 您必須於 hello 機器 toomanually 登入和回 tooStatic 位址，視需要設定 hello IP 位址。
4. 如果您是使用 ESXi 5.5 免費版或 vSphere 6 Hypervisor 免費版，則容錯移轉會成功，但容錯回復不會成功。 您會使用 tooupgrade tooeither Evaluation 授權 tooenable 容錯移轉。

## <a name="failing-back-with-expressroute"></a>透過 ExpressRoute 容錯回復
您可以透過 VPN 連線或 Azure ExpressRoute 進行容錯回復。 如果您想 toouse ExpressRoute 注意 hello 下列：

* ExpressRoute 應該在 hello Azure 虛擬網路 toowhich 來源機器容錯移轉，並以 Azure Vm 屬於位於 hello 容錯移轉發生後設定。
* 資料會複寫的 tooan 公用端點上的 Azure 儲存體帳戶。 您應該設定為站台復原複寫 toouse ExpressRoute hello 目標資料中心中 ExpressRoute 公用互連。
